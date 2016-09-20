---
layout: blogs_singles
thumbnail: https://github.com/huongph/huongph.github.io/blob/master/uploads/img/options-checkbox.png?raw=true
title: Bootstrap - Sử dụng Jquery chọn nhiều option trong checkboxes dùng plugin bootstrap-multiselect.js
description:  Trong bài này mình sẽ hướng dẫn cho các bạn cách chọn nhiều option trong group checkbox, dùng plugin bootstrap-multiselect.js. Đoạn code này chỉ năm trên client nên việc sử dụng cho framework nào là khá đơn giản.
date: 20 Sep 2016
author: Huongph
---

Trong bài này mình sẽ hướng dẫn cho các bạn cách chọn nhiều option trong group checkbox, dùng plugin bootstrap-multiselect.js. Đoạn code này chỉ năm trên client nên việc sử dụng cho framework nào là khá đơn giản.

Copy-paste đoạn mã sau đây bất cứ nơi nào trong trang web của bạn mà bạn muốn:

{% highlight html %}
{% raw %}
    <html lang="en">
    <head>
      <title>Demo jquery mutilple select</title>
      <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.js"></script>
      <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
      <script type="text/javascript" src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-multiselect/0.9.13/js/bootstrap-multiselect.js"></script>
      <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-multiselect/0.9.13/css/bootstrap-multiselect.css">
    </head>
    <body>

    <div class="container">
            <strong>Select Language:</strong>
        <select id="multiple-checkboxes" multiple="multiple">
            <option value="php">PHP</option>
            <option value="javascript">JavaScript</option>
            <option value="java">Java</option>
            <option value="sql">SQL</option>
            <option value="jquery">Jquery</option>
            <option value=".net">.Net</option>
        </select>
    </div>

    <script type="text/javascript">
        $(document).ready(function() {
            $('#multiple-checkboxes').multiselect();
        });
    </script>

    </body>
    </html>
{% endraw %}
{% endhighlight %}


Các bạn có thể xem demo va code full ở đây [Full Code](https://output.jsbin.com/kadata){:target="_blank"}

_Ref : http://itsolutionstuff.com/_


