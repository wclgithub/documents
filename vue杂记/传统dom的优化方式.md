### 浏览器工作大体流程

渲染引擎首先通过网络获得所请求文档的内容，通常以8K分块的方式完成。

下面是渲染引擎在取得内容之后的基本流程：

* 解析html为dom树，解析css为css树 ： （渲染引擎开始解析html，并将标签转化为内容树中的dom节点。）

* 把dom和cssom结合起来生成渲染树(render) ： 解析外部CSS文件及style标签中的样式信息。这些样式信息以及html中的可见性指令将被用来构建另一棵树——render树。Render树由一些包含有颜色和大小等属性的矩形组成，它们将被按照正确的顺序显示到屏幕上。

* 布局渲染树，计算几何形状 ： Render树构建好了之后，将会执行布局过程，它将确定每个节点在屏幕上的确切坐标

* 把渲染树展示到屏幕上 ： 绘制，即遍历render树，并使用UI后端层绘制每个节点

        1.构建dom 树 构建css 树
        2.构建渲染树
        3.节点布局
        4.页面渲染

### dom优化

1. 为什么要做dom优化
 
DOM 引擎、JS 引擎 ， 相互独立，但又工作在同一线程（主线程） ，两者之间的切换有消耗



2.优化方式

* 减少访问DOM的次数

    两个独立的系统只能通过接口来进行连接，相当于每进行一次DOM操作，都需要两个接口通信一次，当访问DOM的次数越多的时候，所消耗的性能也就越高了。

* 节点Clone

    利用element.clone()来替代element.createElement()创建相同的元素。（提升不是特别大）




3. 重绘和重排

* 浏览器下载完所有资源后，将HTML，JavaScript,CSS，图片解析生成两个数据结构

        DOM树
        表示页面结构 （不对外，与css树共同构建成渲染树）
        渲染树
        表示DOM节点如何显示（我们看到的就是渲染树）
    DOM树中的每个节点都至少对应渲染树中的一个节点。当DOM树和渲染树构建完成之后，浏览器就开始绘制页面元素了。

* 重排

元素的几何属性发生变化后，浏览器重新计算元素的几何属性，其他元素的几何属性也会因为该元素变化而改变，

浏览器就会使渲染树中受到影响的部分失效，重新来构造渲染树。这个过程就是重排。

* 重绘

浏览器根据渲染树重新绘制受影响的部分，这个过程是重绘。


* 重排发生的情况 
    
        添加删除可见的DOM元素
        元素位置的改变
        元素尺寸的改变
        内容改变
        页面渲染器初始化
        浏览器窗口尺寸的改变
        
    这几点都一个特点，都是有元素的几何属性发生了变化
    
* 重排于重绘的优化

    * 减少重绘重排的发生次数
      
      合并一些样式修改，只进行一次重绘和重排

    * 当对元素进行大量修改的时候，使用中间元素或者隐藏再显示的方式修改，修改完成后再显示。整个过程只会触发了两次重排。 
        
        隐藏元素
        将元素copy一份，在copy的这份上进行操作，操作完成后使用copy的元素替换掉原本的元素

    * 元素脱离文档流
    
        在播放动画的时候，元素可能会导致大面积的重排，影响的面积越大，性能影响越大。
        
            float 、 absolute 、 fixed
            
            
            

            
