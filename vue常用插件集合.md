### 在vue使用clipboard.js进行一键复制文本
    
1. 安装依赖：  
    
        cnpm install clipboard --save

2. 这个功能用到的地方不多  所以在需要用到的页面引入就可以啦，当然可以直接在main.js中引入 并注册到vue原型上

        // 在某.vue文件中
        import Clipboard from 'clipboard';
    
        // 模板页面中使用
        <p class="wx_href">...</p>  // 复制的内容  wx_href  是要给 data-clipboard-text 绑定用的
        <el-button :data-clipboard-text="wx_href" id="copy_text"  @click="copy" >复制</el-button>
        
        
        // 复制方法
        copy: function () {
            let that = this;
            let clipboard = new Clipboard('#copy_text');
            clipboard.on('success', e => {
                console.log(e);
                this.$message({
                    message: '复制成功!',
                    type: 'success'
                });
                // 释放内存
                clipboard.destroy()
            });
            clipboard.on('error', e => {
                // 不支持复制
                that.$message.error('复制失败，该浏览器不支持自动复制!');
                // 释放内存
                clipboard.destroy()
            })
        },
 