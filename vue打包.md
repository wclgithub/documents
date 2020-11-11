### vue 打包失败解决办法 （亲测可行）
 报错信息如下：  building for production...Error processing file: static/css/app.e8b75d3d19abc5bbbd9bd916f459f0d0.css
 
 **1. 在webpack.prod.conf.js中注释 （这是webpack压缩css的配置）**
 
        const OptimizeCSSPlugin = require('optimize-css-assets-webpack-plugin')
         
        new OptimizeCSSPlugin({
              cssProcessorOptions: config.build.productionSourceMap
                ? { safe: true, map: { inline: false } }
                : { safe: true }
            }),
            
注释之后，可正常打包项目，但是css没有被压缩
            
**2. 在utils.js种添加minimize:true**

           const cssLoader = {
               loader: 'css-loader',
               options: {
                 sourceMap: options.sourceMap,
                 minimize:true
               }
           }
           
这样，项目就可以正常打包，css也可压缩，项目打包后可以正常上线


#### 错误2  　　在vue开发中，本地测试以及测试环境中都没有遇到问题，当发布生产，有虚拟路径时，便出现js、css均报错404；
         
1. 首先在config的index.js文件中，将assetsPublicPath修改为'./'，
        
          build: {
            // Template for index.html
            index: path.resolve(__dirname, '../dist/index.html'),
        
            // Paths
            assetsRoot: path.resolve(__dirname, '../dist'),
            assetsSubDirectory: 'static',
            assetsPublicPath: './',
            
2. 然而打包发布后发现放在assets文件夹中的图片资源又报404，观察那个路径，发现多了一层statics/css/img的路径，我们要找到build文件中的utils.js，在如下所示地方新增一条publicPath为'../../'；         
         
            if (options.extract) {
               return ExtractTextPlugin.extract({
                 use: loaders,
                 fallback: 'vue-style-loader',
                 publicPath:'../../'
               })
             } else {
               return ['vue-style-loader'].concat(loaders)
             }
             

### 一个ip  多个域名打包配置

        server {
            listen       80;
            server_name  admin.drumsky.com;
        
            location / {
                root   association;
                # try_files $uri $uri/ /association/index.html; # 耳机路由 刷新页面丢失处理
                try_files $uri $uri/ /index.html;
                index  index.html index.htm;
            }
        }
        
        server {
            listen       80;
            server_name  school.drumsky.com;
        
            location / {
                root   mechanism;
                # try_files $uri $uri/ /mechanism/index.html; 
                try_files $uri $uri/ /index.html;
                index  index.html index.htm;
            }
        }
        
        server {
            listen       80;
            server_name  student.drumsky.com;
        
            location / {
                root   mobile;
                # try_files $uri $uri/ /mobile/index.html; # 配置使用路由
                try_files $uri $uri/ /index.html; # 配置使用路由
                index  index.html index.htm;
            }
        }
        
        
### 一个ip 多个项目部署

        location /YsLiveArchives {
            alias   YsLiveArchives;
            try_files $uri $uri/ /YsLiveArchives/index.html;
            index  index.html index.htm;
        }

        location /YsFocusSupervise {
            alias   YsFocusSupervise;
            try_files $uri $uri/ /YsFocusSupervise/index.html;
            index  index.html index.htm;
          }    
          
        # 路由配置信息  
        location @router {
           rewrite ^.*$ /index.html last;
        }

        
        
