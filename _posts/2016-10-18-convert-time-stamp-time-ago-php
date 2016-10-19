---
layout: blogs_singles
thumbnail: https://github.com/huongph/huongph.github.io/blob/master/uploads/img/banner-embed-youtube.png?raw=true
title: PHP - Time Ago PHP Function.
description:  Việc đưa iframe hay embed của youtube vào web thì không còn xa lạ gì với những người chuyên và không chuyên về website, nhưng để làm mượt mà và biến nó thành của mình thì không hể đơn giản chút nào. Sau đây thì tôi sẽ hướng dẫn cho các bạn một phương thức bằng Javascript.
date: 18 Oct 2016
author: Huongph
---

Copy-paste đoạn mã sau đây bất cứ nơi nào trong trang web của bạn mà bạn muốn đoạn video YouTube xuất hiện. Nhớ thay VIDEO_ID với ID thực tế của video YouTube.

{% highlight html %}
{% raw %}
    // với VIDEO-ID là id của Youtube
    <div class="youtube-player" data-id="VIDEO_ID"></div>
{% endraw %}
{% endhighlight %}

Chiều cao và chiểu rộng thì các bạn tự fix như css bình thường nhé. 
Và add tiếp đoạn script này vào web của bạn.

{% highlight javascript %}
{% raw %}
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
{% endraw %}
{% endhighlight %}

Để tôi giải thích một chút về code này: Nếu các bạn có thể copy code này chạy trong [jsbin](https://jsbin.com/) thì các
bạn thấy rõ hơn rất nhiều.
Thứ nhất khi dom load xong thì chỉ hiện thị thumbnail và button play mà thôi. Cho nên người dùng nhìn vào thì sẽ không biết đó là youtube.
Thứ hai , loadmetadata chưa chạy thì các bạn không lo về sự chậm trể của page.

Nếu muốn các bạn cho thêm những thuộc tính sao trong line `https://www.youtube.com/embed/ID?autoplay=1`

![alt text](https://github.com/huongph/huongph.github.io/blob/master/uploads/img/api-youtube-huong-pham.png?raw=true "Những thuộc tính api embed")

Xong , Các bạn có thể xem code full ở đây [Full Code Embed Api Youtube](https://output.jsbin.com/nekaro){:target="_blank"}

### Đây là ví dụ cụ thể

Ở đây các bạn có nhìn thấy nó có giổng của tôi không? :D 

###### Chú ý : 

* Không thể remove watermark YouTube 
* Không thể remove quản cáo YouTube

* Và còn nhiều điều nữa... hihi ^^ *

{::nomarkdown}
<div class="youtube-player" data-id="3AtDnEC4zak"></div>
<style>
    .youtube-player {
        position: relative;
        padding-bottom: 56.23%;
        /* Use 75% for 4:3 videos */
        height: 0;
        overflow: hidden;
        max-width: 100%;
        background: #000;
        margin: 5px;
    }
    
    .youtube-player iframe {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 100;
        background: transparent;
    }
    
    .youtube-player img {
        bottom: 0;
        display: block;
        left: 0;
        margin: auto;
        max-width: 100%;
        width: 100%;
        position: absolute;
        right: 0;
        top: 0;
        border: none;
        height: auto;
        cursor: pointer;
        -webkit-transition: .4s all;
        -moz-transition: .4s all;
        transition: .4s all;
    }
    
    .youtube-player img:hover {
        -webkit-filter: brightness(75%);
    }
    
    .youtube-player .play {
        height: 72px;
        width: 72px;
        left: 50%;
        top: 50%;
        margin-left: -36px;
        margin-top: -36px;
        position: absolute;
        background: url("//i.imgur.com/TxzC70f.png") no-repeat;
        cursor: pointer;
    }

</style>

<script>
   document.addEventListener("DOMContentLoaded",
        function() {
            var div, n,
                v = document.getElementsByClassName("youtube-player");
            for (n = 0; n < v.length; n++) {
                div = document.createElement("div");
                div.setAttribute("data-id", v[n].dataset.id);
                div.innerHTML = labnolThumb(v[n].dataset.id);
                div.onclick = labnolIframe;
                v[n].appendChild(div);
            }
        });
 
    function labnolThumb(id) {
        var thumb = '<img src="https://i.ytimg.com/vi/ID/hqdefault.jpg">',
            play = '<div class="play"></div>';
        return thumb.replace("ID", id) + play;
    }
 
    function labnolIframe() {
        var iframe = document.createElement("iframe");
        var embed = "https://www.youtube.com/embed/ID?autoplay=1&controls=0&showinfo=0&rel=0&modestbranding=0&playsinline=1&html5=1&enablejsapi=1&widgetid=1";
        iframe.setAttribute("src", embed.replace("ID", this.dataset.id));
        iframe.setAttribute("frameborder", "0");
        iframe.setAttribute("allowfullscreen", "1");
        this.parentNode.replaceChild(iframe, this);
    }
</script>
{:/nomarkdown}
