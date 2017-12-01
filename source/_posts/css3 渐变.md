---
title: css3 渐变
date: 2017-05-20 00:15:39
tags: [css3, 渐变]
categories: css3
---
渐变分线性渐变(linear-gradient)和径向渐变(radial-gradient);这里写的代码省去了-webkit-,-moz-,-o-这些前缀,使用的时候不要忘记.
# 线性渐变(linear-gradient)

![image.png](http://upload-images.jianshu.io/upload_images/1969397-261a8f109bb7efa1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下面几个属性分开介绍
<!-- more -->
## 渐变方向
默认的渐变方向:从上到下
可以采用角度的方式指定方向:如
**默认方向(从上到下),也即180deg方向**
 html :
```
<div></div>
```
css:
```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(red, blue);
}
```

![默认方向(从上到下)](http://upload-images.jianshu.io/upload_images/1969397-73c3da4e7ddfa049.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
**45度方向(左下到右上)**
 html :
```
<div></div>
```
css:
```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(45deg, red, blue);
}
```

![45度方向(左下到右上)](http://upload-images.jianshu.io/upload_images/1969397-d52517df2c508649.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
按照下图,

![方向示意图](http://upload-images.jianshu.io/upload_images/1969397-57878af27f9dd12c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

以此类推:
0deg : 从 **下 **到 **上**
45deg: 从 **左下 **到 **右上**
90deg: 从 **左 **到 **右**
135deg: 从 **左上 **到 **右下**
180deg: 从 **上 **到 **下**
270(-90)deg: 从 **右 **到 **左**
...
表示方向还有另外一种方式,
例如将"45deg"换成"to right top" ,或者换成"left bottom",都表示一样的效果,个人习惯使用角度,其他不演示了.
## 渐变颜色
写在前面的是初始颜色,写在后面的是结束颜色;就像我们以上例子中所写的.
我们可以使用rgb,rgba,十六进制或者像以上例子中语义化的颜色值来表示渐变颜色;
如果需要用到透明度,需要使用rgba
## 渐变位置
 html :
```
<div></div>
```
css:
```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(90deg, red 20%, blue 80%);
}
```
![渐变位置](http://upload-images.jianshu.io/upload_images/1969397-886bb1ca488b108b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个渐变位置也就是我们颜色值后面的百分比,这一点不常用,很多人容易把它搞混.
拿上例来说,
20%表示在渐变这条线上,从渐变长度的20%处开始渐变,20%之前的都是纯red色;
80%表示,到渐变长度的80%处停止渐变,80%之后的都是纯blue色;
也就是说,渐变区间是渐变这条线上,20%-80%这一区间;
默认的渐变区间是0%-100%.
## 重复线性渐变
repeat-linear-gradient函数用于创建重复的线性渐变
 html :
```
<div></div>
```
css:
```
div {
    height: 100px;
    width: 200px;
    background: repeating-linear-gradient(90deg, red 10%, blue 20%);
}
```

![重复的线性渐变](http://upload-images.jianshu.io/upload_images/1969397-8b2b37aa59ca9468.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 径向渐变(radial-gradient)
径向渐变是由中心向外渐变的。可以控制它的中心(默认渐变是中心是center),形状（圆形或者椭圆形）,大小,以及上面讲到的渐变范围等。
 html :
```
<div></div>
```
css:
```
div {
    height: 100px;
    width: 200px;
    background: radial-gradient(red 20%, blue 80%);
}
```

![径向渐变](http://upload-images.jianshu.io/upload_images/1969397-b838ce4cd1170557.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
