## 问题

首先是一个 div 块里需要一张背景，带文本和图案的那种，但是身为容器的 div 是能够随数据的改变而变化长度的，所以一张静态图片不免的会有拉伸和挤扁的状态，尤其是有图案和文本的情况下最为明显

```
      .bg {
        position: fixed;
        top: 0px;
        left: 0;
        width: 183px;
        height: 1106px;
        background: no-repeat center/183px 100% url("img/001.png");
      }
```

![bg04](https://github.com/easterCat/css/blob/master/background/img/004.png?raw=true)

当数据不够的时候就是一个扁扁的样子

```
      .bg {
        position: fixed;
        top: 0px;
        left: 0;
        width: 183px;
        height: 600px;
        background: no-repeat center/183px 100% url("img/001.png");
      }
```

![bg05](https://github.com/easterCat/css/blob/master/background/img/005.png?raw=true)

这时候就是想办法能够让图自适应且还能看的过去，于是就出现将头部变形比较明显的文字图案和底部颜色渐变分成，两个图的解决方法。这样头部文字不懂，颜色渐变进行拉伸就不那么明显了。于是分成两个 div，分别存放头部和底部，但是总感觉这方法有些繁琐，看了看文档发现 background 可以设置多背景

```
//缩写形式
      .bg {
        position: fixed;
        top: 0px;
        left: 0;
        width: 175px;
        height: 600px;
        background: no-repeat center 114px/175px calc(100% - 114px) url("img/002.png"), no-repeat center top/175px 114px url("img/003.png");
      }

//分写形式
      .bg {
        position: fixed;
        top: 0px;
        left: 0;
        width: 175px;
        height: 600px;
        /* background: no-repeat center 114px/175px calc(100% - 114px) url("img/002.png"), no-repeat center top/175px 114px url("img/003.png"); */
        background: url("img/002.png"), url("img/003.png");
        background-repeat: no-repeat, no-repeat;
        background-position: center 114px, center top;
        background-size: 175px calc(100% - 114px), 175px 114px;
      }
```

![bg06](https://github.com/easterCat/css/blob/master/background/img/006.png?raw=true)

> IE8 及更早的浏览器版本不支持一个元素有多个背景图片

#### background 语法

背景缩写属性可以在一个声明中设置所有的背景属性

> 可以设置的属性分别是：background-color, background-position, background-size, background-repeat, background-origin, background-clip, background-attachment,和 background-image 中间有些值缺少一两个，并没有什么问题

当然也可以分开写属性，比如下列属性，个人更喜欢飞鞋属性

- background-color 指定要使用的背景颜色
- background-position 指定背景图像的位置
- background-size 指定背景图片的大小
- background-repeat 指定如何重复背景图像
- background-origin 指定背景图像的定位区域
- background-clip 指定背景图像的绘画区域
- background-attachment 设置背景图像是否固定或者随着页面的其余部分滚动
- background-image 指定要使用的一个或多个背景图像

#### background-position

background-position 属性设置背景图像的起始位置

| 值                           | 描述                                                                                                                                                           |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| left top center bottom right | 如果仅指定一个关键字，其他值将会是"center"                                                                                                                     |
| x% y%                        | 第一个值是水平位置，第二个值是垂直。左上角是 0％0％。右下角是 100％100％。如果仅指定了一个值，其他值将是 50％。默认值为：0％0％                                |
| xpos ypos                    | 第一个值是水平位置，第二个值是垂直。左上角是 0。单位可以是像素（0px0px）或任何其他 CSS 单位。如果仅指定了一个值，其他值将是 50％。你可以混合使用％和 positions |
| inherit                      | 指定 background-position 属性设置应该从父元素继承                                                                                                              |

#### css3 的 calc 函数

calc() 函数用于动态计算长度值

- 运算符前后都需要保留一个空格，width: calc(100% - 10px)
- 任何长度值都可以使用 calc()函数进行计算
- calc()函数支持 "+", "-", "\*", "/" 运算
- calc()函数使用标准的数学运算优先级规则

[MDN - CSS -backgound](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background)
[MDN - CSS -backgound - 多重背景](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Backgrounds_and_Borders/Using_multiple_backgrounds)
