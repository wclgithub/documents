### rem 适配

postcss-pxtorem 是一款 postcss 插件，用于将单位转化为 rem

lib-flexible 用于设置 rem 基准值

### 设置 rem 函数  rem.js
    
    function setRem() {
        // 320 默认大小16px; 320px = 20rem ;每个元素px基础上/16
        let htmlWidth = document.documentElement.clientWidth || document.body.clientWidth;
    //得到html的Dom元素
        let htmlDom = document.getElementsByTagName('html')[0];
    //设置根元素字体大小
        htmlDom.style.fontSize = htmlWidth / 20 + 'px';
    }
    
    // 初始化
    setRem();
    // 改变窗口大小时重新设置 rem
    window.onresize = function () {
        setRem()
    }

### 还要给html  设置可视区的像素比

    <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">

### .postcssrc.js  配置文件 （没有自己建一个  虽然不知道有没有用，好像没用，生气）

    // https://github.com/michael-ciniawsky/postcss-load-config
    module.exports = {
      "plugins": {
        "postcss-import": {},
        "postcss-url": {},
        // to edit target browsers: use "browserslist" field in package.json
        "autoprefixer": {
          browsers: ['Android >= 4.0', 'iOS >= 5'],
        },
        "postcss-pxtorem": {
          rootValue: 37.5,
          propList: ['*'],
        },
      }
    }

    
### 引入

    // rem 转化
    import 'lib-flexible/flexible'
    //设置字体
    import './rem';
    
