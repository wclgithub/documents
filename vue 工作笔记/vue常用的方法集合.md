#### 使用过滤器将时间戳转时间字符串:

        setTimeFilter(val) {
            const time = new Date(val);
            const Y = time.getFullYear()
            const M = (time.getMonth() + 1).toString().padStart(2, '0')
            const D = time.getDate().toString().padStart(2, '0')
            const h = time.getHours().toString().padStart(2, '0')
            const m = time.getMinutes().toString().padStart(2, '0')
            const s = time.getSeconds().toString().padStart(2, '0')
            return `${Y}-${M}-${D} ${h}:${m}:${s}`
        }

#### 排序array.sort()

sort是按照字符编码的顺序对数组中的元素进行排序  不是按照数值大小 在原数组上对数组元素进行排序, 所以往往不能直接达到我么想要的效果，要提供比较函数

* 数字数组排序
        menuIds.sort() 
        //比较函数
        menuIds.sort(function (m, n) {
            if (m < n) return -1  // 前<后 返回一个小于零的数
            else if (m > n) return 1  前>后 返回一个大于零的数
            else return 0  // 等于
        });

* 对包含对象的数组排序，要求根据对象中的某个字段(数值)进行由大到小的顺序排列

        var arr = [{'name': '张三', age: 26},{'name': '李四', age: 12},{'name': '王五', age: 37},{'name': '赵六', age: 4}];
        var objectArraySort = function (keyName) {
            return function (objectN, objectM) {
                var valueN = objectN[keyName]
                var valueM = objectM[keyName]
                if (valueN < valueM) return 1
                else if (valueN > valueM) return -1
                else return 0
            }
        }
        arr.sort(objectArraySort('age'))
        console.log(arr) // [{'name': '王五', age: 37},{'name': '张三', age: 26},{'name': '李四', age: 12},{'name': '赵六', age: 4}]

#### 数组去重 

* 集合 set 去重 

        this.checkList = [...new Set(this.checkList)]
        
* indexOf 去重   新建一新数组，遍历传入数组，值不在新数组就push进该新数组中 最简单

        function uniq(array){
            var temp = []; //一个新的临时数组
            for(var i = 0; i < array.length; i++){
                if(temp.indexOf(array[i]) == -1){
                    temp.push(array[i]);
                }
            }
            return temp;
        }
* 获取没重复的最右一值放入新数组 （检测到有重复值时终止当前循环同时进入顶层循环的下一轮判断） 方法的实现代码相当酷炫；

      function uniq(array){
          var temp = [];
          var index = [];
          var l = array.length;
          for(var i = 0; i < l; i++) {
              for(var j = i + 1; j < l; j++){
                  if (array[i] === array[j]){
                      i++;
                      j = i;
                  }
              }
              temp.push(array[i]);
              index.push(i);
          }
          console.log(index);
          return temp;
      }


#### 计算两个时间戳之间相差的天数

    // value，value2格式  2020-12-12
    let time1 = new Date(value).getTime()
    let time2 = new Date(value2).getTime()
    if (time1 <= time2||Math.floor((time1-time2)/86400000)<7) {
        callback(new Error('考试开始时间至少大于考试报名时间7天！'));
    }

#### 触发隐藏的文件按钮 实现  本地预览  上传功能
    
        // html
        <div v-if="!formData.imgUrl" class="sketch-img" @click="selectImg">
            <i class="el-icon-plus"></i>
        </div>
        <img v-else class="sketch-show" :src="formData.imgUrl" alt="" @click="selectImg">
        <input type="file" ref="inputFile" style="display: none" @change="fileChange">
        <p class="tips">推荐图片900px * 300px; 图片大小不超过500kb</p>
        
        
        // methods
        /**
        * 触发选择图片事件
        * 点击图片触发上传按钮事件  这样就等于点击上传按钮了
        * 一定要保证 ref 对象在文件流中
        * */
        selectImg() {
            this.$refs.inputFile.dispatchEvent(new MouseEvent('click'))
        },
        /**
        * 文件元素的文件选择事件
        * */
        fileChange(event) {
            let imgFile = event.target.files[0];
            if (!imgFile) {
                return
            }
            if (!(imgFile.size / 1024 / 1024<10)) {
                this.tools.syMessage('图片大小不能超过10M！','0')
                return
            }
            this.ImgFile = imgFile
            // 获取图片本地地址
            let reader = new FileReader();
            reader.readAsDataURL(imgFile)
            reader.onload = () => {
                let url_base64 = reader.result;
                this.formData.imgUrl = url_base64
            }
        },
        

#### 获取屏幕可建区域宽高

    document.documentElement.clientHeight  (有的浏览器的值为，BODY对象高度加上Margin高)
    
    document.documentElement.clientWidth  (有的浏览器的值为，BODY对象宽度加上Margin宽)
    
    // body  宽高
    document.body.clientWidth ==> BODY对象宽度
    
    document.body.clientHeight ==> BODY对象高度
    
   // 所以我们在设计页面的时候 将body 的margin/padding  设置为0 ，获取可视区域就用
   
   document.documentElement.clientHeight 
   
   document.documentElement.clientWidth

    
    
