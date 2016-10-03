---
layout: blogs_singles
thumbnail: https://encrypted-tbn3.gstatic.com/images?q=tbn:ANd9GcS9iigB6oNc_y3pjx1G3kYUXw2LyrwRliz8sug02hjXJNlesS7cvA
title: JavaScript - Detecting Arrays. Objects in JavaScript.
description:  Trong bài này mình sẽ hướng dẫn các bạn lọc được value trong objects. Ở đây mình dùng .map và instanceof. 
date: 30 Sep 2016
author: Huongph
---

Ở đây mình se có hai Object: 

#JavaScript

{% highlight javascript %}
{% raw %}
    var londonMarathon = {
        name: "London Marathon",
        date: "April 13, 2014"
    };

    // Cấp cao hơn nữa.

    var moreMarathons = [
        {
            name: "New York City Marathon",
            date: "November 2, 2014"
        },
        {
            name: "Chicago Marathon",
            date: "October 12, 2014"
        }
    ];


    // Các bạn sử dụng hàm này để get những value cần thiết trong các object
    
    function getListOfMarathonNames (marathons) {
        if (marathons instanceof Array) {
            // Return an array containing all marathon names.
            return marathons.map(function(race) {
                return race.name;
            });
        } else if (marathons instanceof Object) {
            // Return an array containing the name of the only
            // marathon given.
            return [marathons.name];
        }
    }

    console.log(getListOfMarathonNames(londonMarathon));
    // -> ["London Marathon"]

    console.log(getListOfMarathonNames(moreMarathons));
    // -> ["New York City Marathon", "Chicago Marathon"]

{% endraw %}
{% endhighlight %}


Vậy là ok rồi đó: 

Ref :  [here](http://adripofjavascript.com/blog/drips/detecting-arrays-vs-objects-in-javascript.html){:target="_blank"}