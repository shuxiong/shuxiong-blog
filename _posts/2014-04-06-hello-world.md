---
published: true
layout: post
title: "Hello World"
date: 2014-04-06 12:05
comments: false
categories: ['test']
---

##test highlight line on##
{% highlight javascript linenos %}
var arr1 = new Array(arrayLength);
var arr2 = new Array(element0, element1, ..., elementN);
{% endhighlight %}

    {% highlight javascript linenos %}
    var arr1 = new Array(arrayLength);
    var arr2 = new Array(element0, element1, ..., elementN);
    {% endhighlight %}

```javascript
var arr1 = new Array(arrayLength);
var arr2 = new Array(element0, element1, ..., elementN);
```

    ```javascript
    var arr1 = new Array(arrayLength);
    var arr2 = new Array(element0, element1, ..., elementN);
    ```

##test foot print##
a[^ref-a]

 [^ref-a]: www.example.com

c[^ref-c]

  [^ref-c]:  www.example.com


##test hyper link##
[b][ref-b]

 [ref-b]: http://www.example.com

    [b][ref-b]
    [ref-b]: http://www.example.com


##test img##


![this is image description][1]

  [1]: https://www.google.com.hk/images/srpr/logo11w.png

```
![this is image description][1]

  [1]: https://www.google.com.hk/images/srpr/logo11w.png
```

##test latex##

$$
f[x][y] = \left\{
  \begin{array}{}
    false & : y=0 \ or\ x+y<=2 \\
    y\&1 & : x=0 \\
    !f[0][y] & : x=1 \\
    !f[x-2][y+1] & : other\ cases
  \end{array}
\right.
$$

a great reference can be found [here](http://en.wikibooks.org/wiki/LaTeX/Advanced_Mathematics).
