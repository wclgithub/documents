1. vant-image 标签  默认src为网络图片 ：  

        <van-image  width="100" height="100" src="https://img.yzcdn.cn/vant/cat.jpeg" />

    当要引用本地的图片时，直接写图片的路径在vue项目中会刷不出图片（但用 <img> 标签可以显示 ）。

 * 解决方法： 在图片的链接外包上一层 require（） 这样，图片就可以显示
