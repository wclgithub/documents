### 没有这个文件在根目录下创建一个  （亲测害没发现有啥效果 哭唧唧）   
   
    module.exports = {
        /** 区分打包环境与开发环境
         * process.env.NODE_ENV==='production'  (打包环境)
         * process.env.NODE_ENV==='development' (开发环境)
         * baseUrl: process.env.NODE_ENV==='production'?"https://cdn.didabisai.com/front/":'front/',
         */
        // 项目部署的基础路径
        // 我们默认假设你的应用将会部署在域名的根部,
        // 例如 https://www.my-app.com/
        // 如果你的应用部署在一个子路径下，那么你需要在这里
        // 指定子路径。比如将你的应用部署在
        // https://www.foobar.com/my-app/
        // 那么将这个值改为 '/my-app/'
        baseUrl: "/ExaminationManagement/",
        publicPath:'/', // 部署应用包时的基本 URL， 用法和 webpack 本身的 output.publicPath 一致。
        outputDir: "dist", // 构建时的输出目录
        assetsDir:'static', //放置生成的静态资源 (js、css、img、fonts) 的目录
        indexPath:'index.html', // 指定生成的 index.html 的输出路径 (相对于 outputDir)。也可以是一个绝对路径。
        // filenameHashing:'', //文件名哈希；默认情况下，生成的静态资源在它们的文件名中包含了 hash 以便更好的控制缓存。然而，这也要求 index 的 HTML 是被 Vue CLI 自动生成的。如果你无法使用 Vue CLI 生成的 index HTML，你可以通过将这个选项设为 false 来关闭文件名哈希。

        lintOnSave: false, //是否在保存的时候使用 `eslint-loader` 进行检查。 有效的值：`ture` | `false` | `"error"`  当设置为 `"error"` 时，检查出的错误会触发编译失败。
        runtimeCompiler: false, //是否使用包含运行时编译器的 Vue 构建版本。设置为 true 后你就可以在 Vue 组件中使用 template 选项了，但是这会让你的应用额外增加 10kb 左右。
        transpileDependencies: [
            //默认情况下 babel-loader 会忽略所有 node_modules 中的文件。如果你想要通过 Babel 显式转译一个依赖，可以在这个选项中列出来。
            /* string or regex */
        ],
    
    
    
        productionSourceMap: false, // // 是否为生产环境构建生成sourceMap?
    
    
        chainWebpack: () => {}, //  是一个函数，会接收一个基于 webpack-chain 的 ChainableConfig 实例。允许对内部的 webpack 配置进行更细粒度的修改。
        configureWebpack: () => {},   //如果这个值是一个对象，则会通过 webpack-merge 合并到最终的配置中。 如果这个值是一个函数，则会接收被解析的配置作为参数。该函数及可以修改配置并不返回任何东西，也可以返回一个被克隆或合并过的配置版本。
    
        css: {
            // CSS 相关选项
            // 将组件内部的css提取到一个单独的css文件（只用在生产环境）
            // 也可以是传递给 extract-text-webpack-plugin 的选项对象
            extract: true,  //是否将组件中的 CSS 提取至一个独立的 CSS 文件中 (而不是动态注入到 JavaScript 中的 inline 代码)。
            sourceMap: false, //允许生成 CSS source maps? 设置为 true 之后可能会影响构建的性能。
            // 预处理器的loader传递自定义选项，例如传递给Css-loader时  使用 `{Css:{...}}`
            loaderOptions: {
                css:{
                    //这里传递给css-loader
                },
                postcss:{
                    //这里传递给postcss-loader
                }
            },
            modules: false //为所有CSS/预处理器文件启用CSS模块。//此选项不影响*.vue文件。 设置为 true 后你就可以去掉文件名中的 .module 并将所有的 *.(css|scss|sass|less|styl(us)?) 文件视为 CSS Modules 模块。
        },
        parallel: require("os").cpus().length > 1, // 是否为 Babel 或 TypeScript 使用 thread-loader。该选项在系统的 CPU 有多于一个内核时自动启用，仅作用于生产构建。
        pwa: {}, // 向 PWA 插件传递选项。
        devServer: {//所有 webpack-dev-server 的选项都支持。注意： 有些值像 host、port 和 https 可能会被命令行参数覆写。 有些值像 publicPath 和 historyApiFallback 不应该被修改，因为它们需要和开发服务器的 publicPath 同步以保障正常的工作。
            open: process.platform === "darwin",
            disableHostCheck: false,
            host: "0.0.0.0",
            port: 8088,
            https: false,
            hotOnly: false, // See https://github.com/vuejs/vue-cli/blob/dev/docs/cli-service.md#configuring-proxy
            proxy: null // string | Object  如果你的前端应用和后端 API 服务器没有运行在同一个主机上，你需要在开发环境下将 API 请求代理到 API 服务器。这个问题可以通过 vue.config.js 中的 devServer.proxy 选项来配置。
            // before: app => {}
        },
        // 第三方插件配置
        pluginOptions: {
            // 这是一个不进行任何 schema 验证的对象，因此它可以用来传递任何第三方插件选项。
        },
    
    };
