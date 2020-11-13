1. 此处安装v5.1.1分支，因为如果直接git clone下载的是最新的develop分支，而develop是测试分支，不是正式分支。当然也可以直接切换主分支后再git clone。
    
        git clone -b v5.1.1 https://github.com/vuejs/vue-devtools.git

2. 安装依赖包

        cd vue-devtools
        cnpm install

3.  打包项目
    
        npm run build  
        
4.  看到有的博主说要修改shells  chrome 下的 manifest.json文件，把"persistent":false改成true  ，  但我没改  直接打包也好使...


5. 扩展Chrome插件

   Chrome浏览器 > 更多程序 > 拓展程序
   
   右上角选择开发者模式=>点击加载已解压程序按钮=> 选择 vue-devtools > shells > chrome 放入
   
   使用这个扩展程序

运行你的项目   f12   可以看到控制台多了个Vue调试窗口   尽情体验吧。
