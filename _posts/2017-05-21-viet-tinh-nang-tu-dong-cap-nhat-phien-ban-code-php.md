---
layout: post
title: Viết tính năng tự động nâng cấp phiên bản cho code PHP (PHP auto-upgrade system)
thumbnail: upgrade_thumb.png
category: Chuyện lập trình
related_posts:
 - title: Series nghịch ngợm - Lập trình phần mềm paint, vẽ trên web với html5 và javascript
   link: http://laptrinhcuocsong.com/series-nghich-ngom-lap-trinh-phan-mem-paint-ve-tren-web-html5-javascript.html
 - title: Nếu một ngày những đoạn mã lập trình biến mất
   link: http://laptrinhcuocsong.com/neu-mot-ngay-nhung-doan-ma-lap-trinh-bien-mat.html
 - title: Tổng hợp tất tần tật những công cụ cần thiết cho web developer
   link: http://laptrinhcuocsong.com/tong-hop-nhung-cong-cu-can-thiet-cho-web-developer.html
---
Nếu bạn có ý định phát hành code php của mình ra cộng đồng, hãy nghĩ đến việc tạo cho nó tính năng tự động cập nhật phiên bản ngay từ khi bắt đầu. Bởi vì khi code đã được sử dụng, việc nâng cấp là hết sức khó khăn với người dùng, phải copy đè file này file kia, chạy câu lệnh này câu lệnh kia cực kỳ phiền phức và dễ sai sót.

Hầu hết các CMS hiện nay đều có hệ thống tự động cập nhật phiên bản, dễ thấy nhất là wordpress, khi có phiên bản mới từ nhà phát triển, wordpress sẽ hiện "Cập nhật hệ thống" và người dùng chỉ cầm bấm nút cập nhật, họ đã có phiên bản mới nhất.

## Quá trình nâng cấp gồm các bước sau:

- Bước 1: Chuyển website về chế độ bảo trì: Khi người dùng truy cập vào sẽ có thông báo hệ thống đang bảo trì.
- Bước 2: Sao lưu phiên bản code hiện tại: Việc này nhằm tránh trường hợp nếu cập nhật không thành công vẫn có thể restore về phiên bản cũ.
- Bước 3: Tải bản code cập nhật mới từ remote server về hosting
- Bước 4: Giải nén và ghi đè các file cũ.
- Bước 5: Nâng cấp cơ sở dữ liệu.
- Bước 6: Chuyển website về chế độ bình thường.

Chúng ta sẽ viết tính năng tương tự như thế nhưng ở mức độ đơn giản hơn, chỉ thực hiện bước 3, 4 và 5, tức là tải bản code cập nhật mới từ remote server về hosting, giải nén, ghi đè các file cũ và nâng cấp cơ sở dữ liệu.

**Cấu trúc thư mục như sau**:

![Cấu trúc thư mục](images/upgrade_folder_struct.png)

Thư mục server được chạy trên website của nhà phát triển (tức là chúng ta) tạm gọi là remote server, bao gồm file get_version.php để trả về chuối phiên bản hiện tại (1.0.1 chẳng hạn), file nén zip tương ứng chứa các file cần ghi đè và file upgrade_database.php gồm các câu lệnh query để nâng cấp cơ sở dữ liệu.

**File nén zip như thế này**:

![File nén](images/upgrade_php.png)

Ở website của khách hàng, chúng ta có thư mục upgrade để chứa file nén sẽ tải về, file version.php để lưu phiên bản hiện tại của website đơn giản như thế này:

<?php define("WEBSITE_VERSION", "1.0.0"); ?>

Ở file upgrade.php chúng ta sẽ thực hiện lấy số phiên bản mới nhất bằng cách đọc file get_version.php từ remote server.

```javascript
set_time_limit (60);

define('UPGRADE_SERVER_URL', 'http://update.your-domain.com/');
require_once 'version.php';

$remote_version = get_version();
echo 'Current version: '.WEBSITE_VERSION.'<br>';
echo 'Remote_version: '.$remote_version.'<br>';

function get_version(){
    return file_get_contents(UPGRADE_SERVER_URL.'get_version.php');
}
```

Chúng ta thực hiện so sánh phiên bản hiện tại với phiên bản mới nhất trên remote server, nếu phiên bản hiện tại chưa phải là phiên bản mới nhất mới thực hiện nâng cấp.

```javascript
function upgrade_available(){
    global $remote_version;
    return version_compare($remote_version, WEBSITE_VERSION) == 1;
}
```

Đầu tiên, chúng ta tải file zip tương ứng về thư mục upgrade

```javascript
function download_upgrade_package(){
    global $remote_version;
    echo 'Downloading upgrade package<br>';
    return file_put_contents('upgrade/'.$remote_version.'.zip', fopen(UPGRADE_SERVER_URL.$remote_version.'.zip', 'r'));
}
```

Và giải nén nó ra thư mục với tên là số phiên bản, ví dụ "1.0.1.zip" thì giải nén ra thư mục tên là "1.0.1"

```javascript
function extract_package(){
    global $remote_version;
    $zip = new ZipArchive;
    if ($zip->open('upgrade/'.$remote_version.'.zip') === TRUE) {
        $zip->extractTo('upgrade/'.$remote_version);
        $zip->close();
        echo 'Extract package success<br>';
        return true;
    } else {
        echo 'Extract package failed<br>';
        return false;
    }
}
```

Tiếp theo, chúng ta phải lấy hết danh sách các file và thư mục của gói cài đặt này:

```javascript
function get_all_files($dir){

    $result = array(); 

    $scan_dir = scandir($dir); 

    foreach ($scan_dir as $key => $value) 
    { 
        if (!in_array($value,array(".","..")))
        { 
            if (is_dir($dir.'/'.$value)) 
            { 
                $sub_dir_files = get_all_files($dir.'/'.$value);
                $result[] = $dir.'/'.$value;
                $result = array_merge($result, $sub_dir_files);
            } 
            else 
            { 
                $result[] = $dir.'/'.$value; 
            } 
        } 
    } 

    return $result; 
}
```

Hàm trên sẽ trả về danh sách tên các file và thư mục dưới dạng mảng giống như sau:

```javascript
Array
(
    [0] => upgrade/1.0.1/includes
    [1] => upgrade/1.0.1/includes/test2.php
    [2] => upgrade/1.0.1/test.php
    [3] => upgrade/1.0.1/upgrade_database.php
)
```

Copy các file theo danh sách trên vào các vị trí tương ứng:

```javascript
function copy_files($files){
    global $remote_version;

    foreach($files as $key => $file){
        $file = substr($file, strlen('upgrade/'.$remote_version.'/'));

        if ( is_dir('upgrade/'.$remote_version.'/'.$file) ){
            if (!file_exists($file)){
                echo 'Making dir: '.$file.'<br>';
                mkdir($file);
            }
        }
        else {
            echo 'Copy: upgrade/'.$remote_version.'/'.$file.' to '.$file.'<br>';
            copy('upgrade/'.$remote_version.'/'.$file, $file);
        }
    }
}
```

Đến đây, khách hàng đã có bộ code mới nhất được tự động lấy từ server của nhà phát triển, nhưng thường thì, việc thay đổi code cũng kèm theo thay đổi database, để đơn giản chúng ta cho tất cả các câu query cập nhật database vào file upgrade_database.php trong file zip luôn, nội dung file upgrade_database.php kiểu như sau:

```javascript
<?php
$sql = "UPDATE table_name SET column_name = 'value' WHERE something = 'something'";
mysql_query($sql);
?>
```

Khi nâng cấp, require luôn file upgrade_database.php để nó chạy, thế là database của khách hàng đã được update theo ý của chúng ta.

Việc cuối cùng, đó là sửa số phiên bản hiện tại của website lên phiên bản vừa nâng cấp, để nó khỏi nâng cấp lần nữa. Sửa file version.php đã nói ở trên.

```javascript
function update_local_version(){
    global $remote_version;
    file_put_contents('version.php', '<?php define("WEBSITE_VERSION", "'.$remote_version.'"); ?>');
}
```

Đoạn code nâng cấp như sau:

```javascript
if (upgrade_available()){
    global $remote_version;
    echo 'Start upgrade<br>';
    download_upgrade_package();
    extract_package();
    $files = get_all_files('upgrade/'.$remote_version);
    copy_files($files);

    update_local_version();
    echo 'Upgrade database<br>';
    require_once('upgrade/'.$remote_version.'/upgrade_database.php');
    echo 'Upgrade system success';
}
else {
    echo 'You have lastest version';
}
```
