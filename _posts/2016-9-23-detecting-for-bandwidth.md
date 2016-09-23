---
layout: blogs_singles
thumbnail: https://assets.paessler.com/common/files/screenshots/bandwidth-monitoring.png
title: JavaScript - DETECTING FOR BANDWIDTH.
description:  The focus of image loading, so far has been based on image dimensions and screen-size; I think what really matters there is file size and available bandwidth. Just because browser window is small doesn’t necessarily mean it can’t handle a high-res image.
date: 23 Sep 2016
author: Huongph
---

The focus of image loading, so far has been based on image dimensions and screen-size; I think what really matters there is `file size` and `available bandwidth`. Just because browser window is small doesn’t necessarily mean it can’t handle a high-res image.

On a recent project I was looking for a way to test online/offline state, I came across Using navigator.connection in Android. Which is a blog post covering the Network Information API.

I built out a simple demo based off the blog post which checks bandwidth and returns another image version. To set up the HTML, we’re using a normal <img> tag and loading in the small version of the image incase nothing works, you’ll get the small version:


# HTML

{% highlight html %}
{% raw %}
    <img src="images/small-fella.jpg" data-large="images/large-fella.jpg">
{% endraw %}
{% endhighlight %}

Using the data-large attribute let’s use store the image inside the <img> tag, so it feels more natural.

The JavaScript will check the bandwidth using the network information API, loop through all the img[data-large] and re-set the image src attribute.


#JavaScript

{% highlight javascript %}
{% raw %}
    <script>


        (function(){
    
            // initialize some variables
            var connection,
                connectionSpeed,
                images = document.querySelectorAll("img[data-large]"),
                imageCount = images.length,
                i;

            // create a custom object if navigator.connection isn't available
            connection = navigator.connection || { 'type': '0' };

            // if statement checking for WIFI, ETHERNET or UNKNOWN
            if(imageCount > 0 && connection.type === '0' || connection.type === '1' || connection.type === '2') {

                // loop through each image with the data-large attribute
                for (i = 0; i < imageCount; i = i + 1) {

                    var obj = images[i],
                        largeImg = obj.getAttribute('data-large');

                    // reset the image src to the larger version of the image
                    obj.setAttribute('src', largeImg);

                }

            }
        })();
 
    </script>
{% endraw %}
{% endhighlight %}

See demo  [here](http://csskarma.com/lab/_javascript/network-connection/){:target="_blank"}