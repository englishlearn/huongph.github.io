---
layout: blogs_single
thumbnail: https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/uploads/img/parameter-javascript.jpg?raw=true
title: Javascript - Làm thế nào để lấy những parames trên url sử dụng javascript
logouser: https://avatars1.githubusercontent.com/u/15043041?v=3&s=466
description:  Có rất nhiều cách để lấy những parameters trên url, nhưng trong bài viết này tôi sử dụng javascript để thay thế cho nhiều cách khác. Và tôi nghĩ sẽ có nhiều lúc bạn sẽ cần đến nó...
date: 17 Sep 2016
---


<article class="post tag-article">
    <div align='center'><img class='post-top' src='https://avatars1.githubusercontent.com/u/15043041?v=3&s=466' /></div>
    <h1 class="post-title"> [Javascript] - Làm thế nào để lấy những parames trên url sử dụng javascript </h1>
    <div align='center'>
        <span class="post-meta">
        Posted On <time datetime="2016-09-18">18 Sep 2016</time> by Nguyen Tungs
        </span>
    </div>
    <section class="post-content">
        <p><img src="/uploads/img/parameter-javascript.jpg" alt="tungns - hướng dẫn cách lấy parame trên url dùng javascript" />
        </p>

        
        <p> Mình sử dụng `window.location.search` để lấy chuỗi sau domain, ví dụ: </p>
        
        <pre><code>
        //https://nguyentungs.github.io?port=3009&server=linux
            console.log(window.location.search);
        // thì ta có "?port=3009&server=linux

        // Giả sử ta có "?port=3009&server=linux"
        // Ta có thể get như thế này :
        
        var urlParams = new URLSearchParams(window.location.search);

        console.log(urlParams.has('port')); // true
        console.log(urlParams.get('server')); // "linux"
        console.log(urlParams.getAll('server')); // ["linux"]
        console.log(urlParams.toString()); // "?port=3009&server=linux"
        console.log(urlParams.append('active', '1')); // "?port=3009&server=linux&active=1"

        // Hoăc có cách đơn giản hơn nhiều dùng function mà chúng ta tự viết

        function getUrlParameter(name) {
            name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
            var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
            var results = regex.exec(location.search);
            return results === null ? '' : decodeURIComponent(results[1].replace(/\+/g, ' '));
        };

        //sử dụng :
        getUrlParameter('port'); // "3009"
        getUrlParameter('server'); // "linux"

        // với "name" là tên parame chúng ta truyền vào.
        </code></pre> 
        

        <p><i>Vậy là ok rồi. Cảm ơn các bạn đã cùng chia sẻ.</i></p>
    </section>
    <hr>
    <section class="share">
        <h4>Share this post</h4>
        <a class="icon-twitter" href="http://twitter.com/share?text=Lorem ipsum dolor sit amet&url=https://nguyentungs.github.io{{ post.url }}/" onclick="window.open(this.href, 'twitter-share', 'width=550,height=235');return false;">
            <span class="hidden">Twitter</span>
        </a>
        <a class="icon-facebook" href="https://www.facebook.com/sharer/sharer.php?u=https://nguyentungs.github.io{{ post.url }}/" onclick="window.open(this.href, 'facebook-share','width=580,height=296');return false;">
            <span class="hidden">Facebook</span>
        </a>
        <a class="icon-google-plus" href="https://plus.google.com/share?url=https://nguyentungs.github.io{{ post.url }}/" onclick="window.open(this.href, 'google-plus-share', 'width=490,height=530');return false;">
            <span class="hidden">Google+</span>
        </a>
    </section>
</article>

<br/>
<article class="post tag-article">
    <footer class="post-footer">
        <section class="author">
            <h4>Nguyen Tungs</h4>
            <img src='https://avatars1.githubusercontent.com/u/15043041?v=3&s=466' />
            <p>I am Nguyen Tungns a web developer from HCM, VietNam.</p>
        </section>
    </footer>
</article>
<br/>
<article class="post tag-article">
    <br/>
    <div id="disqus_thread">
        <div class="fb-comments" data-href="https://nguyentungs.github.io{{ post.url }}/" data-width="100%" data-num-posts="10" data-colorscheme="dark"></div>
    </div>
</article>