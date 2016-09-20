---
layout: blogs_single
thumbnail: https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/assets/img/mongodb-logo.png?raw=true
title: Mongodb - Hướng dẫn tạo index trong mongodb
logouser: https://avatars1.githubusercontent.com/u/15043041?v=3&s=466
description:  Khi truy vấn dữ liệu trong mongodb, thì bạn nên set index cho các collection để được truy vấn nhanh hơn, và hiệu quả hơn. Sau đây mình sẽ hướng dẫn các bạn cách tạo , xoá, và tạo nhiều index trên một Collection.
date: 17 Sep 2016
---
<article class="post tag-article">
    <div align='center'><img class='post-top' src='https://avatars1.githubusercontent.com/u/15043041?v=3&s=466' /></div>

    <h1 class="post-title">[Mongodb] - Hướng dẫn tạo index trong mongodb</h1>
    <div align='center'>
        <span class="post-meta">
        Posted On <time datetime="2016-09-18">18 Sep 2016</time> by Nguyen Tungs
        </span>
    </div>
    <section class="post-content">
        <p><img src="https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/assets/img/mongodb-logo.png?raw=true" alt="" />
        </p>

        
        <p>Đầu tiên mình sẽ tạo những record sau đây: </p>
        
        <pre><code>
        {
            "subject":"Nhà tôi có nuôi con voi", 
            "content":"Con void là bạn thân của tôi.", 
            "likes": 60, 
            "year": 2015, 
            "language": "english"
        }

        {
            "subject":"Nhà tôi có nuôi con tinh tinh", 
            "content":"Con void va con tinh tinh là bạn thân của tôi.", 
            "likes": 61, 
            "year": 2015, 
            "language": "english"
        }
        </code></pre> 
        
        <p>Mình sẽ insert những dữ liệu đó vào collection messages: </p>
        
        <pre><code>
        db.messages.insert({"subject":"Nhà tôi có nuôi con voi", "content":"Con void là bạn thân của tôi.", "likes": 60, "year":2015, "language":"english"})
        db.messages.insert({"subject":"Nhà tôi có nuôi con tinh tinh", "content":"Con void va con tinh tinh là bạn thân của tôi.", "likes": 61, "year":2015, "language":"english"})
        </code></pre>
    
        <p>Tạo một chỉ mục văn bản trên các "subject" của dữ liệu mà mình mới insert bằng cách sử dụng truy vấn sau đây:</p>
        <pre><code>
        db.messages.createIndex({"subject":"text"})
        </code></pre>
        <p>Sau đó mình sẽ truy vấn như sau : </p>
        <pre><code>
        db.messages.find({$text: {$search: "voi"}}, {score: {$meta: "textScore"}}).sort({score:{$meta:"textScore"}})
        </code></pre>

        <p>Các truy vấn trên trả về các record sau đây có chứa những từ "voi" trong "subject" của mình.</p>
        <pre><code>
            db.messages.insert({"subject":"Nhà tôi có nuôi con voi", "content":"Con void là bạn thân của tôi.", "likes": 60, "year":2015, "language":"english"})
        </code></pre>

        <p>Xong rồi đó, với việc minh toạ index thì một cấu trúc dữ liệu được lưu trữ trên ổ cứng tương ứng với một table hoặc view nhằm mục đích tăng tốc độ việc truy xuất dữ liệu từ table hoặc view đó.</p>
        <p>Muốn xoá thì dùng lệnh sau : </p>
        
        <pre><code>
            db.messages.dropIndex("subject_text") 
        </code></pre>

        <p>Chúng ta có thể add nhiều index trong một collection : </p>
        
        <pre><code>
            db.messages.createIndex({"subject":"text","content":"text"})
        </code></pre>

        <p><i>Cảm ơn các bạn đã cùng chia sẻ.</i></p>
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