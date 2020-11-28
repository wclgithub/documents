1. 绑定class 的时候   推荐使用计算属性，计算属性有缓存，关联的数据不变  计算属性不执行 取缓存的值


2. jq 到各种框架的变化

jQuery是一个工具库，但框架不仅仅是一个库，更像是一个仓库的集合    

+ MVVM库意在处理DOM和数据更新 （其他设计思想也都有相似的处理优化）
+ ES6+Babel则是JS语言层面的提升
+ webpack等打包工具是前端工程化的一大进步
...
如果说处理单个功能，可能用框架显得复杂，但是就项目而言，不可能只处理一个功能，框架的出现，在项目的生产效率、成员协作、管理等方面产生了质的飞跃



3. 数组的过滤

let arr1 = array.filter((item)=>{
 return  item.id===prop  // 为真则返回  得到一个新数组
})
splice() 方法向/从数组中添加/删除项目，然后返回被删除的项目。 该方法会改变原始数组。
array.splice(startIndex,num,newArray)


4. 路由跳转传值： 建议使用 query 传参  如果是对象用 JSON.stringify 处理一下  变成字符串  这样刷新不会变成[object,object]的形式

        this.$router.push({path:'edit',query:{data:JSON.stringify(row)}})

