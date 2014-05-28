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

##test single line latex##

abc

对于当前的$a$,$b$，如果$b=0$，那么$a$就是最大公约数，可以令$x=1$，$y=0$

否则，我们已经计算了$a^\prime$，$b^\prime$，$x^\prime$，$y^\prime$，并且$a^\prime x^\prime +b^\prime y^\prime =gcd(a,b)$

由于$a^\prime=b$，$b^\prime=a-\lfloor\frac{\displaystyle a}{\displaystyle b}\rfloor$
且$ax+by=gcd(a,b)$，代入可以求解得

$x=y^\prime$，$y=x^\prime-\lfloor\frac{\displaystyle a}{\displaystyle b}\rfloor y^\prime$

