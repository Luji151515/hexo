title: CSS解决居中问题方案汇总
author: 黄凯阳
avatar: /images/favicon.png
authorLink: 'http://huangkaiyang.cn'
authorAbout: 'http://huangkaiyang.cn'
authorDesc: 「敲代码的时候我可是一本正经的」
categories: 前端
tags: css
date: 2018-01-17 19:59:53
keywords:
description: 在你刚入前端之初，居中这个问题有时候会带给你一些烦恼，特别是垂直居中，这篇博客将从水平居中——垂直居中——整体居中方面提供全套解决方案。
photos:
---
## CSS解决居中问题方案汇总
>在你刚入前端之初，居中这个问题有时候会带给你一些烦恼，特别是垂直居中，这篇博客将从水平居中——垂直居中——整体居中方面提供全套解决方案。

*注：着急看垂直居中或者整体居中可以直接往后翻*
#### 水平居中
我们的需求是实现不定宽高的居中，初始代码如下
```
    <div class="father" style="background-color:aqua">
        <div class="child" style="background-color: yellow">
            居中
        </div>
    </div>
```
结果是这样的
![1.png](http://upload-images.jianshu.io/upload_images/762103-5fbe8d00a22f405e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

很容易发现子元素占用了父元素的所有宽度。下面列出了三种水平居中的解决方案
##### 1. text-align + inline-block
```
        .father{
            text-align: center;
        }
        .child{
            display: inline-block;
        }
inline-block: 收敛子元素的宽度使其宽度随内容而定，text-align, 使收敛后的子元素居中
```
优点：兼容性好，除了IE6,7之外，基本上无兼容问题。
缺点：text-align导致子元素内容也居中，这在某些情况下是不希望见到的。
##### 2. table + margin
table: 表面上像block，其实他的宽度是跟着内容走的于是乎我们可以这样
```
        .father{}
        .child{
            display: table;
            margin: 0 auto;
        }
```
结果是这样的
![2.png](http://upload-images.jianshu.io/upload_images/762103-792118e0636c37f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
优点：只作用父元素，兼容IE8及以上
##### 3. relative + absolute
这个不多说，相信大家平时用的也比较多
```
        .father{
            position: relative;
        }
        .child{
            position: absolute;
            left:50%;
            transform: translateX(-50%);
        }
```
值得注意的是父元素相对定位后，其高度塌陷为0导致背景颜色无法显示，但居中目的确实是达到了。
![3.png](http://upload-images.jianshu.io/upload_images/762103-30356a903dbb1c61.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 4. flex + justify
Flex:牵涉到弹性盒子布局，如果对此不了解，很乐意当一个传送门
[Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
假定你已经了解了Flex或者看完了上述介绍，那我就直奔主题直接给出代码。
```
        .father{
            display: flex;
            justify-content: center;
        }
        .child{}
```
优点：简单
缺点：兼容性，甚至在某些较新的非IE浏览器还依据需要加上厂商前缀
***
#### 垂直居中
相信你对vertical-align不陌生，听说可以使元素垂直居中，但为啥每次使用都没效果，在这说明一下，vertical-align只对inline, inline-block, table等级别元素有效，注意这里不包括block。好了，直奔主题。

##### 1. table-cell + vertical
```
        .father{
            display: table-cell;
            vertical-align: middle;
        }
```
细心的你可能发现了子元素的宽度等同于父元素
![5.png](http://upload-images.jianshu.io/upload_images/762103-260e229887b26b73.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
优点： 简单，只作用于父元素
缺点： 除了很低版本的IE外，好像还真没啥
##### 2. absolute + transform
原理很简单，直接给出代码
```
        .father{
            position: relative;
        }
        .child{
            position: absolute;
            top:50%;
            transform: translateY(-50%);
        }
```
![6.png](http://upload-images.jianshu.io/upload_images/762103-14f3ba10d0d54428.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个刚好子元素的宽度为其内容宽度。
缺点：兼容问题 详查[Can I use?](https://caniuse.com/)
##### 3. flex + align-items
不多说，你都看到这里,这就不是问题了，什么你真是跳着看的，好吧，再次勉为其难的送上一道传送门。
[Flex](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
```
        .father{
            display: flex;
            align-items: center;
        }
```
效果如上
缺点：兼容问题  详查[Can I use?](https://caniuse.com/)
***
#### 整体居中
##### 1. inline-block + text-align + table-cell + vertical
思路很简单，先实现水平居中再实现垂直居中，你要反过来也可以。
```
        .father{
            text-align: center;
            display: table-cell;
            vertical-align: middle;
        }
        .child{
            display: inline-block;
        }
```
##### 2. absolute + transform
```
        .father{
            position: relative;
        }
        .child{
            position: absolute;
            top:50%;
            left:50%;
            transform: translate(-50%,-50%);
        }
```
![7.png](http://upload-images.jianshu.io/upload_images/762103-fac145663ec76546.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##### 3. flex + justify + align-items
```
        .father{
            display: flex;
            justify-content: center;
            align-items: center;
        }
```


















