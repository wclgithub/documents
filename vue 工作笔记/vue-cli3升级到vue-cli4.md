### （待亲测，这个项目结束就试试）

### 在全局安装最新的 Vue CLI：

    npm install -g @vue/cli
    # OR
    yarn global add @vue/cli

检查一下安装版本：记得V大写

    vue -V
        
### 在项目根目录下执行

    vue upgrade
    
出现个警告就停止了，警告意思是：

当前存储库中有未提交的更改，建议先提交或隐藏它们。

是否仍然继续？

输入y即可：可以把项目拷贝一份，不怕出错

下一步出现升级插件的提示，输入 Y 即可  有不想更新的可以输入 n


### 更新完成后  主要有以下改动 具体改变内容再查查

1. bable.config.js

2.  pakage.json文件对应更新的三个文件的版本变成高版本了：


### 运行一下npm run serve启动一下本地项目
    
有报错： 报错截图就不上了

又启动一下就好了，项目成功启动


### vue cli 4 主要升级点总结：
    
"@vue/cli-plugin-babel", "@vue/cli-plugin-eslint", "@vue/cli-service"由 v3 的版本升级到了 v4
    
这个项目用的依赖比较少，可能没遇到很多的差异性的东西，所以升级的比较顺利  再次新建项目就有 vue.config.js文件了  让人头大......
