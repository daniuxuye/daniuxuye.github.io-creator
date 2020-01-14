# CSS知识点复习
下面文章分为3部分
分别是：
   1. 浏览器渲染原理我是怎么理解的
   2. CSS 动画的两种做法（transition 和 animation）
   3. 我对CSS的一些自己的看法
   
## **<big>第一部分</big>**
## 浏览器的渲染原理
### <font size=2>一句话总结就是：在渲染引擎的作用下把页面内容、内容样式、应用逻辑和效果等等这些元素优化整合后呈现到屏幕上。</font>

## 浏览器的渲染过程
* 解析html为dom树，解析css为cssom。
* 把dom和cssom结合起来生成渲染树
* 布局渲染树，计算几何形状
* 把渲染树展示到屏幕上
  
! [渲染树](../../static/images/渲染树.png)

## **<big>第二部分</big>**
### CSS 动画的两种做法（transition 和 animation）
## <table><tr><td bgcolor=black>**使用transition做动画**</td></tr></table>
过渡可以为一个元素在不同状态之间切换的时候定义不同的过渡效果。比如在不同的伪元素之间切换，像是 :hover，:active 或者通过 JavaScript 实现的状态变化。

`transition`属性可以被指定为一个或多个 CSS 属性的过渡效果，多个属性之间用逗号进行分隔。 例如要在`:hover`伪元素之间切换定义过渡效果
````
#heart{
  transition: all 1s;
  
}
#heart:hover{
  transform: scale(1.2);
  
}
````
## <table><tr><td bgcolor=black>**使用animation做动画**</td></tr></table>
首先要声明关键帧，有两种写法，一种写法是from to
````
@keyframes animation {
    from {
        transform:translateX(0%);
    }
    to {
        transform:transateX(100%);
    }
}
````
另一种写法是百分数
````
@keyframes animation {
    from {
        transform:translateX(0%);
    }
    to {
        transform:transateX(100%);
    }
}
````
### <table><tr><td bgcolor=black>**我的看法**</td></tr></table>
**transition关注的是CSS property的变化，property值和时间的关系是一个三次贝塞尔曲线。
animation作用于元素本身而不是样式属性，可以使用关键帧的概念，应该说可以实现更自由的动画效果。**

## **<big>第三部分</big>**
 我对CSS的一些自己的看法
 * 多敲比多瞎想更重要
 * 对于刚学习不久的选手来说，学最好的办法是挑个小任务先搞起了，这样学习效率比较快
 * css就是别人创造的语法而已，就好像日本人交流用日语一样。他创造出一个语法然后定义它为某个含义，有时候根本就不知道为什么会是这样，只要记住就好。因为你不知道发明者为什么发明这种语法来定义这个用处。
 * 记得向MDN求救
 * 自学路漫漫， CSS学不完，挑常用的学先，讲究效率。



