---
title: CSS3 黑科技 - 内凹圆角 - 径向渐变实现
date: 2017-06-01 23:30:46
tags: [css3, 渐变]
categories: css3
---
转自:[csdn](http://blog.csdn.net/qq_16415157/article/details/52818993)

圆角，大家一定都会做，border-radius, 内凹圆角如何实现？

可以拿个白色圆盒子盖住方形盒子的大半边实现，但是这样，是不透明的，背景发生改变时，就要改遮盖盒子的颜色，或者背景是渐变，改起来更麻烦，或背景是图片等等，就直接不太好改了，这种方法就有局限性。 说白了就是遮盖的那部分不透明以后，自适应性不强。

这里介绍一个用径向渐变实现的内凹圆角，可以解决上述问题。可以用CSS生成一个背景透明的内凹圆角。
<!-- more -->
## 1. 基本线性渐变
```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(90deg, red, blue);
}

<div>从左到右的红到蓝渐变</div>1
```
## 2. 加百分比调整渐变范围

```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(90deg, red 20%, blue 80%);
}

<div></div>
```
## 3. 浓缩渐变范围，直至重合，形成一个红蓝分隔的两个色块
```
div {
    height: 100px;
    width: 200px;
    background-image: linear-gradient(90deg, red 50%, blue 50%);
}

<div></div>
```
## 4. 颜色是可以设置透明色的，transparent, 将红色改成透明色，可以看到只有蓝色的色块了。
```
div {
   height: 100px;
   width: 200px;
   background-image: linear-gradient(90deg, transparent 50%, blue 50%);
}

<div></div>
```
## 5. 同理联想到径向渐变，同样缩小渐变圈，直至重合，靠近圆心的颜色设成transparent。
```
/* 径向渐变主体 */

.raidal {
    height: 100px;
    width: 100px;
    background:radial-gradient(transparent 50%,blue 50%);
}

<div class='raidal'></div>
```
## 6. 径向渐变是可以设置半径圆心位置的，所以设到左顶角，left top 调整半径大小为 200px，就发现背景透明的内凹圆角实现了。
应用时可以用伪元素设置，然后用绝对定位，子绝父相，调整位置，组合成想要的效果

```
/* 径向渐变主体 */
.raidal1 {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px at left top,transparent 50%,blue 50%);
}

<div class='raidal1'></div>
```
## 7. 同理四个方向, 调整圆心位置即可

```
/* 左上 */
.raidal1 {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px at left top,transparent 50%,blue 50%);
}

/* 右上 */
.raidal2 {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px at right top,transparent 50%,blue 50%);
}

/* 右下 */
.raidal3 {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px at right bottom,transparent 50%,blue 50%);
}
```
```
/* 左下 */
.raidal4 {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px at left bottom,transparent 50%,blue 50%);
}

<div class='raidal1'></div>
<div class='raidal2'></div>
<div class='raidal3'></div>
<div class='raidal4'></div>
```
## 8. 同样，不想这么圆角，也是可以椭圆的，半径设两个参数, 就是椭圆。
径向渐变有很多参数大家可以自己再尝试调整，可以出现各种奇怪的形状，这里就不演示了。相对来说，内凹圆角就够用了

 ```
/* 左上 */
.ellipse {
    height: 100px;
    width: 100px;
    background:radial-gradient(200px 300px at left top,transparent 50%,blue 50%);
}    
```
