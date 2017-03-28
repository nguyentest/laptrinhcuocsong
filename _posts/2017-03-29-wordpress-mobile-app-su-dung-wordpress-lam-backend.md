---
layout: post
title: Series tạo app mobile cho website wordpress - Phần 1 - Sử dụng wordpress làm backend
thumbnail: mobile-app.png
category: Chuyện lập trình
---
Trong series này mình sẽ cùng các bạn lập trình ứng dụng mobile (android, ios) với backend sử dụng website wordpress. Trong thời buổi kết nối di động, có một ứng dụng mobile dành riêng cho website, blog sẽ làm nội dung của bạn tiếp cận người dùng nhanh hơn, tiện hơn. Giống như facebook có ứng dụng facebook, haivl có ứng dụng haivl, chúng ta cũng sẽ làm như họ.

App mobile của chúng ta sẽ bao gồm 2 phần:

- **Backend**: Làm công việc xử lý lưu trữ dữ liệu, trả về dữ liệu cho client. Trong series này chúng ta sẽ lập trình một plugin cho website wordpress để làm backend. Plugin này mình đã hoàn thành và đặt tên là "Open hybrid", bạn có thể tải về trên wordpress store [tại đây](https://wordpress.org/plugins/open-hybrid/) hoặc tìm "Open hybrid" trong trang quản trị wordpress.

- **Frontend**: Chính là cái app cài trên điện thoại hay máy tính bảng, nhận dữ liệu từ backend và hiển thị ra cho người dùng. Do mình không biết lập trình android, ios, nên mình sẽ làm hybrid app bằng phonegap.


## Cấu trúc thư mục:

Ở phần này chúng ta sẽ tạo plugin có nhiệm vụ trả về danh sách bài viết, chi tiết một bài viết, nên chỉ có một file main.php trong thư mục plugin là đủ, cấu trúc thư mục như sau:

```javascript
|---- wp-content
|----|---- open-hybrid
|----|----|---- main.php
```

## Đặt tên và các thông tin cơ bản của plugin:
Trong file main.php mình đặt các thông tin cơ bản trong comment như sau, các thông tin này sẽ được wordpress hiểu và hiển thị trong trang quản trị wordpress.

```javascript
<?php
/**
 * Plugin Name: Open Hybrid
 * Plugin URI: http://laptrinhcuocsong.com
 * Description: Plugin for the OpenHybirdWordpress, OpenHybirdWordpress is a free opensource project to build mobile applications use phonegap and wordpress.
 * Version: 0.2
 * Author: Bùi văn Nguyện
 * Author URI: http://buivannguyen.com
 * License: GPLv2 or later
 */
?>
```

Khi vào trang quản trị wordpress, bạn sẽ thấy plugin của chúng ta, bạn có thể kích hoạt nó nếu muốn.

![wordpress](images/wordpress-app-1.png)

## Action hook

Trong wordpress, action hook là một điểm neo để thực hiện một công việc gì đó vào một thời điểm nhất định. Trong bài này chúng ta sẽ sử dụng một hook có tên là template_redirect, hook này được thực hiện khi wordpress đã đọc dữ liệu từ database nhưng chưa hiển thị html ra cho người dùng.

```javascript
add_action( 'template_redirect', 'process_request' );
```

Hàm process_request sẽ được gọi tại thời điểm template_redirect, chúng ta sẽ phải viết hàm này.

```javascript
// process request
function process_request(){
	global $wp_query;

	if (! $_GET['json']){
        return;
    }

    $action = $_GET['json'];
    $data = array();
    
    switch ($action) {
        case 'post_list':
            $data = get_post_list();
        break;

        case 'post_detail':
            $data = get_post_detail();
        break;
    }

    response($data);
}
```

Ở đoạn code trên, nếu người dùng truy cập www.domain.com thì coi như không có chuyện gì xảy ra, họ xem trang web như bình thường, nếu người dùng truy cập từ app, chúng ta sẽ gọi lên website kèm theo tham số json. Mục đích là để phân biệt người truy cập website thông thường và thông qua app.

Nếu gọi `www.domain.com?json=post_list` chúng ta sẽ trả về danh sách bài viết

Nếu gọi `www.domain.com?json=post_detail&post_id={id_bai_viet}` chúng ta sẽ trả về chi tiết một bài viết

## Trả về nội dung json bằng hàm response:

```javascript
// output json
function response($data){
    header("Content-type: application/json; charset=utf-8");
    header("access-control-allow-origin: *");
    echo json_encode($data);
    die();
}
```

Công việc tiếp theo là viết 2 hàm `get_post_list` và `get_post_detail`, nếu các bạn đã sử dụng wordpress thì hoàn toàn không có khó khăn gì cả, mình vẫn sử dụng cái loop huyền thoại của wordpress thôi.

```javascript
// Get post list
function get_post_list() {

    $api_posts = new wp_query(
        array(
            'post_type'   => 'post',
            'post_status' => 'publish',
            'paged'       => intval($_GET['page'])
        )
    );

    $response = new stdClass();
    $response->total_pages = $api_posts->max_num_pages;

    // get post data
    $posts_data = array();

    if ($api_posts->have_posts()){
        while($api_posts->have_posts()){
            $api_posts->the_post();
            $new_post            = new stdClass();
            $new_post->id        = get_the_ID();
            $new_post->title     = get_the_title();
            $new_post->excerpt   = get_the_excerpt();
            $new_post->content   = get_the_content('');
            $new_post->thumbnail = get_the_post_thumbnail_url(get_the_ID());
            $posts_data[]        = $new_post;
        }
    }
    wp_reset_query();

    $response->posts = $posts_data;

    return $response;
}

// get post detail
function get_post_detail(){

    $post_id = intval($_GET['post_id']);
    $post    = get_post($post_id);
    
    $return_post            = new stdClass();
    $return_post->id        = $post->ID;
    $return_post->title     = $post->title;
    $return_post->excerpt   = $post->excerpt;
    $return_post->content   = nl2br($post->post_content);
    $return_post->thumbnail = get_the_post_thumbnail_url($post_id);
    return $return_post;
}
```

Như vậy chúng ta đã hoàn thành backend đơn giản, trả về json cho ứng dụng mobile, nó còn thiếu rất nhiều feature như: danh sách page, chi tiết page, trang cấu hình thông số... như trên sản phẩm thật.

Trong phần 2, chúng ta sẽ cùng lập trình app mobile để tương tác với backend này, như mình đã nói, mình không chuyên android hay ios, nên mình sẽ viết app dạng hybrid với html, css và javascript, build bằng phonegap để xuất ra cả 2 nền tảng android và ios.

Đây là kết quả khi gửi request từ postman.

![wordpress](images/wordpress-app-2.png)

Đây là toàn bộ file main.php của chúng ta:
