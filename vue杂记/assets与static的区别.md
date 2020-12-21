### static和assets的区别，原理就在于webpack是如何处理静态资源的


#### assets

1. 在vue组件中，所有模板和css都会被vue-html-loader和css-loader解析，并查找资源url。

        <img src="./logo.png" />  或者  background: url("./logo.png")
        
    因为./logo.png是相对的资源路径，将会由webpack解析为模块依赖；

2. 由于logo.png不是js，当被视作模块依赖时，需要使用url-loader和file-loader处理它，vue-cli已经配好了这些loader（webpack）因此可以使用相对/模块路径。

3. 由于这些资源可能在构建过程中被内联、复制、重命名，所以它们基本是代码的一部分，即webpack处理的静态资源放在/src目录中，和其它资源文件放在一起。

事实上，不必把它们全部放在/src/assets文件下，可以使用"模块/组件"的组织方式来使用它们

例：可以在每个放置组件的目录中存放静态资源。无非是引用的路径改改


#### static

1. static目录下的文件并不会被webpack处理，它们会直接复制到最终目录（dist/static）下。

     必须使用绝对路径引用这些文件，这是通过在config.js的build.assetsPublicPath和build.assetsSubDirectory连接确定的。

2. 任何放在static/的文件需要以绝对路径形式引用：/static/[name]。

   如果更改assetsSubDirectory的值为assets，那么路径需更改为：/assets/[filename]。
   
   
   
### 总结

assets里面的资源会被webpack打包进代码，static里面的资源就直接引用了；

一般在static里放一些类库的文件，assets放属于项目的资源文件。

说的再通俗一点，就是static放别人家的资源，assets放自己家的资源。
