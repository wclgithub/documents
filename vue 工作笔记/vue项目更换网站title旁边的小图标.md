两种方式：

1.  修改 index.html 页面

        <link rel="icon" type="image/x-icon" href="static/logo.png">  // 浏览器这里并不认识 src 文件夹 图片要放在static 文件下
        // 或 
        <link rel="icon" href="<%= BASE_URl %>favicon.ico"> //public/favicon.ico替换调这个图片就可以
        
       
2. 亲测

*  利用图片在线转换器将图片转换成.ico格式   放到项目根目录下（与index.html同级）

* 在build文件夹下的 webpack.dev.cinf.js文件中  找到 HtmlWebpackPlugin   添加 ： favicon: './favicon.ico' 如下：

        new HtmlWebpackPlugin({
            filename: 'index.html',
            template: 'index.html',
            favicon: './favicon.ico', // 引入图片地址
            inject: true
        }),

* 上面是本地环境  同样的生产环境也来一份 ：webpack.dev.prod.js

        new HtmlWebpackPlugin({
            filename: config.build.index,
            template: 'index.html',
            favicon: './favicon.ico', // 引入图片地址
            inject: true,
            minify: {
                removeComments: true,
                collapseWhitespace: true,
                removeAttributeQuotes: true
                // more options:
                // https://github.com/kangax/html-minifier#options-quick-reference
            },
            // necessary to consistently work with multiple chunks via CommonsChunkPlugin
            chunksSortMode: 'dependency'
        }),


这样打包之后就会发现dist文件夹下多了一张图片~  加油~伟大的程序员！
