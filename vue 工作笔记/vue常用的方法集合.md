1. 使用过滤器将时间戳转时间字符串: （当然放在公共方法中调用也是一样的）

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

2. 排序array.sort()

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
