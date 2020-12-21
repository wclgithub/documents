### 单选按钮样式
    .el-radio-group>>>.el-radio-button{
        margin-right: 8px;
        border: #DDDDDD 1px solid;
        border-radius: 5px;
        width: 102px;
        text-align: center;
        box-shadow: none;
    }
    .el-radio-group>>>.el-radio-button .el-radio-button__inner{
        border: none !important;
        border-radius: 5px;
        width: 100px;
        box-shadow: none;
        padding: 9px 0;
    }
    .el-radio-group>>>.el-radio-button.is-active, .el-radio-group>>>.el-radio-button.is-active .el-radio-button__inner{
        border: none !important;
        /*background-color: #FED700;*/
    }
    .el-radio-group>>>.el-radio-button.is-active .el-radio-button__inner{
        color: #333333;
        background-color: #FED700;
    }

    .el-radio >>> .el-radio__input.is-checked .el-radio__inner {
        border-color: #FED700 !important;
        background: #FED700 !important;
    }

    .el-radio.is-checked >>> .el-radio__label {
        color: #333333;
    }
    
    
    

    
### 结构布局
        html, body {
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }
    
        * {
            padding: 0;
            margin: 0;
            box-sizing: border-box;
        }
    
        #main {
            height: 100%;
        }
    
        #nav {
            width: 100%;
            height: 64px;
            background-color: #FED700;
        }
    
        #content {
            width: 100%;
            position: absolute;
            top: 64px;
            /*bottom: 0;*/  //固定整个页面和屏幕等高
            left: 0;
            display: flex;
            background-color: #FAFBFC;
        }
    
    
        .menu {
            height: 100%;
            width: 14% !important;
        }
    
    
        .main {
            width: 86% !important;
            padding: 0;
        }
        

### 输入框 选择器等禁用样式
    /*    禁用输入框样式*/
    .el-input.is-disabled .el-input__inner,
    .el-range-editor.is-disabled,
    .el-range-editor.is-disabled input,
    .el-textarea.is-disabled .el-textarea__inner{
        background-color: #fff !important;
        color: #606266;
    }
