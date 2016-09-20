---
layout: blogs_singles
thumbnail: https://github.com/huongph/huongph.github.io/blob/master/uploads/img/banner-embed-youtube.png?raw=true
title: Youtube Api - Cách đưa embed youtube vào javascript.
description:  Việc đưa iframe hay embed của youtube vào web thì không còn xa lạ gì với những người chuyên và không chuyên về website, nhưng để làm mượt mà và biến nó thành của mình thì không hể đơn giản chút nào. Sau đây thì tôi sẽ hướng dẫn cho các bạn một phương thức bằng Javascript.
date: 20 Sep 2016
author: Huongph
---

Copy-paste đoạn mã sau đây bất cứ nơi nào trong trang web của bạn mà bạn muốn đoạn video YouTube xuất hiện. Nhớ thay VIDEO_ID với ID thực tế của video YouTube.

{% highlight html %}
    // với VIDEO-ID là id của Youtube
    <div class="youtube-player" data-id="VIDEO_ID"></div>
{% endhighlight %}

Chiều cao và chiểu rộng thì các bạn tự fix như css bình thường nhé. 
Và add tiếp đoạn script này vào web của bạn.

{% highlight javascript %}
    <script>


        document.addEventListener("DOMContentLoaded",
            function() {
                var div, n,
                    v = document.getElementsByClassName("youtube-player");
                for (n = 0; n < v.length; n++) {
                    div = document.createElement("div");
                    div.setAttribute("data-id", v[n].dataset.id);
                    div.innerHTML = demoThumb(v[n].dataset.id);
                    div.onclick = demoIframe;
                    v[n].appendChild(div);
                }
            });

        function demoThumb(id) {
            var thumb = '<img src="https://i.ytimg.com/vi/ID/hqdefault.jpg">',
                play = '<div class="play"></div>';
            return thumb.replace("ID", id) + play;
        }

        function demoIframe() {
            var iframe = document.createElement("iframe");
            var embed = "https://www.youtube.com/embed/ID?autoplay=1";
            iframe.setAttribute("src", embed.replace("ID", this.dataset.id));
            iframe.setAttribute("frameborder", "0");
            iframe.setAttribute("allowfullscreen", "1");
            this.parentNode.replaceChild(iframe, this);
        }
 
    </script>
{% endhighlight %}

Để tôi giải thích một chút về code này: Nếu các bạn có thể copy code này chạy trong [jsbin](https://jsbin.com/) thì các
bạn thấy rõ hơn rất nhiều.
Thứ nhất khi dom load xong thì chỉ hiện thị thumbnail và button play mà thôi. Cho nên người dùng nhìn vào thì sẽ không biết đó là youtube.
Thứ hai , loadmetadata chưa chạy thì các bạn không lo về sự chậm trể của page.

Nếu muốn các bạn cho thêm những thuộc tính sao trong line `https://www.youtube.com/embed/ID?autoplay=1`

![alt text](https://github.com/huongph/huongph.github.io/blob/master/uploads/img/api-youtube-huong-pham.png?raw=true "Những thuộc tính api embed");

### Đây là ví dụ cụ thể

