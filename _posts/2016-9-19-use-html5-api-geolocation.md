---
layout: blogs_single
thumbnail: https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/uploads/img/geolocation.png?raw=true
title: JavaScript - Hướng dẫn sử dụng HTML5 Api Geolocation
logouser: https://avatars1.githubusercontent.com/u/15043041?v=3&s=466
description:  Geolocation của HTML5 giúp trong việc xác định vị trí của người sử dụng, có thể được sử dụng để cung cấp thông tin vị trí hoặc hướng tuyến đường cụ thể chi tiết cho người dùng.
date: 17 Sep 2016
---

<article class="post tag-article">
    <div align='center'><img class='post-top' src='https://avatars1.githubusercontent.com/u/15043041?v=3&s=466' /></div>
    <h1 class="post-title">[JavaScript] - Hướng dẫn sử dụng HTML5 Api Geolocation</h1>
    <div align='center'>
        <span class="post-meta">
        Posted On <time datetime="2016-09-19">19 Sep 2016</time> by Nguyen Tungs
        </span>
    </div>
    <section class="post-content">
        <p><img src="https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/uploads/img/geolocation.png?raw=true" alt="" />
        </p>

        
        <p>Có nhiều kỹ thuật được sử dụng để xác định vị trí của người dùng. Một trình duyệt máy tính để bàn thường sử dụng WIFI hoặc các kỹ thuật định vị dựa trên IP trong khi một trình duyệt di động sử dụng tam giác di động, GPS, A-GPS, WIFI kỹ thuật dựa vào vị trí, vv Định vị API sẽ sử dụng bất kỳ một trong những kỹ thuật này để xác định vị trí của người dùng. Các API vị trí địa bảo vệ sự riêng tư của người dùng bằng cách bắt buộc mà cho phép người sử dụng nên được tìm kiếm và thu được trước khi gửi thông tin vị trí của người sử dụng cho bất kỳ trang web. Vì vậy, người dùng sẽ được nhắc nhở với một popover hoặc hộp thoại yêu cầu cho phép của người dùng để chia sẻ thông tin vị trí. Người dùng có thể chấp nhận hoặc từ chối yêu cầu.</p>
        <p>Bước đầu tiên trong việc sử dụng bất kỳ các API HTML5 là để kiểm tra khả năng tương thích của nó với các trình duyệt</p>
        <pre class="language-javascript"><code class="language-javascript">
        if (navigator.geolocation) {
                // Lấy vị trí người dùng hiện tại.
        } else {
                // Trình duyệt không hỗ trợ Geolocation.
        }
        </code></pre> 
        
        <p>Nếu trình duyệt hỗ trợ Geolocation thì chúng ta có thể lấy vị trí của người dùng hiện tại.</p>
        
        <pre><code>
        if (navigator.geolocation) {
                // Lấy vị trí người dùng hiện tại.

                navigator.geolocation.getCurrentPosition(showPosition, showError, optn);
        } else {
                // Trình duyệt không hỗ trợ Geolocation.
        }
        
        // Lấy vị trí rồi show ra : 
        function showPosition(position) {
            document.write('Latitude: '+position.coords.latitude+'Longitude: '+position.coords.longitude);
        }
        
        // Callback bị lỗi 
        function showError(error) {
            switch(error.code) {
                case error.PERMISSION_DENIED:
                        alert("User denied the request for Geolocation.");
                        break;
                case error.POSITION_UNAVAILABLE:
                        alert("Location information is unavailable.");
                        break;
                case error.TIMEOUT:
                        alert("The request to get user location timed out.");
                        break;
                case error.UNKNOWN_ERROR:
                        alert("An unknown error occurred.");
                        break;
            }
        }
        </code></pre>
    
        <p>Sau đây mình sẽ trinh bày code đầy đủ về tính năng này: </p>
        <p> Đầu tiên mình tạo file index.html</p>
        <pre><code>
        // index.html XXXXX là key api của bạn.
        &lt;script type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=true&key=XXXXX"&gt;
        &lt;section id="result"&gt;
        &lt;section id="gMap"&gt;
        </code></pre>
        <p>Sau đó add code javascript sau : </p>
        <pre><code>
        var result = document.querySelector('#result');
        navigator.geolocation.getCurrentPosition(geoFunc, errFunc);

        function geoFunc(e) {
            console.log(e);
            var lati = e.coords.latitude;
            var loti = e.coords.longitude;
            var accu = e.coords.accuracy;
            result.innerHTML = 'Latitude: ' + lati + '<br>Longitude: ' + loti + '<br>Accuracy: ' + accu;

            var mapcanvas = document.createElement('div');
            mapcanvas.id = 'mapcontainer';
            mapcanvas.style.height = '400px';
            mapcanvas.style.width = '600px';
            document.querySelector('#gMap').appendChild(mapcanvas);
            var coords = new google.maps.LatLng(lati, loti);
            var options = {
                zoom: 15,
                center: coords,
                mapTypeControl: true,
                navigationControlOptions: {
                    style: google.maps.NavigationControlStyle.SMALL
                },
                mapTypeId: google.maps.MapTypeId.ROADMAP
            };
            var map = new google.maps.Map(document.getElementById("mapcontainer"), options);
            var marker = new google.maps.Marker({
                position: coords,
                map: map,
                title: "You are here!"
            });
        }
        function errFunc(e) {
            console.log(e);
        }
        </code></pre>
        <p>Sau đây là kết quả : </p>
        <p><img src="https://github.com/NguyenTungs/NguyenTungs.github.io/blob/master/uploads/img/geolocation.png?raw=true" alt="" />
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
            
            
          


