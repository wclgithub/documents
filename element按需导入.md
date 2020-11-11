### 按需引入需要的组件

1. 按照官网的提示安装按需加载的依赖包 配置成功后即可

2. 新建elementUi 包  新建index.js  代码如下所示

        import {
            Button,
            Select,
            Switch,
            Menu,
            MenuItem,
            Submenu,
            Aside,
            Container,
            Main,
            Tooltip,
            Form,
            FormItem,
            Input,
            Divider,
            Table,
            TableColumn,
            DatePicker,
            Checkbox,
            CheckboxButton,
            CheckboxGroup,
            TimePicker,
            Radio,
            RadioButton,
            RadioGroup,
            Option,
            OptionGroup,
            Col,
            Row,
            Dialog,
            MessageBox,
            Message } from 'element-ui'
        const element = {
            install: function(Vue) {
                Vue.use(Dialog)
                Vue.use(Row)
                Vue.use(Col)
                Vue.use(OptionGroup)
                Vue.use(Option)
                Vue.use(RadioGroup)
                Vue.use(RadioButton)
                Vue.use(Radio)
                Vue.use(TimePicker)
                Vue.use(CheckboxGroup)
                Vue.use(CheckboxButton)
                Vue.use(Checkbox)
                Vue.use(Button)
                Vue.use(Switch)
                Vue.use(Select)
                Vue.use(Menu)
                Vue.use(MenuItem)
                Vue.use(Submenu)
                Vue.use(Container)
                Vue.use(Aside)
                Vue.use(Main)
                Vue.use(Tooltip)
                Vue.use(Form)
                Vue.use(FormItem)
                Vue.use(Input)
                Vue.use(Divider)
                Vue.use(Table)
                Vue.use(TableColumn)
                Vue.use(DatePicker)
        
                Vue.prototype.$msgbox = MessageBox
                Vue.prototype.$alert = MessageBox.alert
                Vue.prototype.$confirm = MessageBox.confirm
                Vue.prototype.$message = Message
            }
        }
        export default element

3. 在main.js中

        import element from './elementUi'
        Vue.use(element)        
            
