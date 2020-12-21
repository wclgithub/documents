1.diff 算法的核心部分

    function patch (oldVnode, vnode) {
        if (sameVnode(oldVnode, vnode)) {
            patchVnode(oldVnode, vnode)
        } else {
            const oEl = oldVnode.el
            let parentEle = api.parentNode(oEl)
            createEle(vnode)
            if (parentEle !== null) {
                api.insertBefore(parentEle, vnode.el, api.nextSibling(oEl))
                api.removeChild(parentEle, oldVnode.el)
                oldVnode = null
            }
        }
        return vnode
    }

* patch函数有两个参数，vnode和oldVnode，也就是新旧两个虚拟节点。

* 虚拟节点的结构（举例）

        {
          el:  div  //对真实的节点的引用，本例中就是document.querySelector('#id.classA')
          tagName: 'DIV',   //节点的标签
          sel: 'div#v.classA'  //节点的选择器
          data: null,       // 一个存储节点属性的对象，对应节点的el[prop]属性，例如onclick , style
          children: [], //存储子节点的数组，每个子节点也是vnode结构
          text: null,    //如果是文本节点，对应文本节点的textContent，否则为null
        }

    el属性引用的是此 virtual dom对应的真实dom
    
2.解释


    if (sameVnode(oldVnode, vnode)) {
    	patchVnode(oldVnode, vnode)
    } 

sameVnode函数就是看这两个节点是否值得比较，代码相当简单：

    function sameVnode(oldVnode, vnode){
    	return vnode.key === oldVnode.key && vnode.sel === oldVnode.sel
    }
    
两个vnode的key和sel相同才去比较它们，比如p和span，div.classA和div.classB都被认为是不同结构而不去比较它们。

#### 如果值得比较会执行patchVnode(oldVnode, vnode)。 

    patchVnode (oldVnode, vnode) {
        const el = vnode.el = oldVnode.el
        let i, oldCh = oldVnode.children, ch = vnode.children
        if (oldVnode === vnode) return
        if (oldVnode.text !== null && vnode.text !== null && oldVnode.text !== vnode.text) {
            api.setTextContent(el, vnode.text)
        }else {
            updateEle(el, vnode, oldVnode)
        	if (oldCh && ch && oldCh !== ch) {
    	    	updateChildren(el, oldCh, ch)
    	    }else if (ch){
    	    	createEle(vnode) //create el's children dom
    	    }else if (oldCh){
    	    	api.removeChildren(el)
    	    }
        }
    }
    
* const el = vnode.el = oldVnode.el 这是很重要的一步，让vnode.el(对象)引用到现在的真实dom，当el修改时，vnode.el会同步变化。

* 节点的比较有5种情况：
    
    * if (oldVnode === vnode)，他们的引用一致，可以认为没有变化。
    * if(oldVnode.text !== null && vnode.text !== null && oldVnode.text !== vnode.text)，文本节点的比较，需要修改，则会调用Node.textContent = vnode.text。
    * if( oldCh && ch && oldCh !== ch ), 两个节点都有子节点，而且它们不一样，这样我们会调用updateChildren函数比较子节点，这是diff的核心，也比较复杂。
    * else if (ch)，只有新的节点有子节点，调用createEle(vnode)，vnode.el已经引用了老的dom节点，createEle函数会在老dom节点上添加子节点。
    * else if (oldCh)，新节点没有子节点，老节点有子节点，直接删除老节点。
* updateEle(el, vnode, oldVnode) 改变当前节点 ， 然后再比较子节点

#### 当节点不值得比较，进入else中

    else {
        const oEl = oldVnode.el
        let parentEle = api.parentNode(oEl)
        createEle(vnode)
        if (parentEle !== null) {
            api.insertBefore(parentEle, vnode.el, api.nextSibling(oEl))
            api.removeChild(parentEle, oldVnode.el)
            oldVnode = null
        }
    }
    	
当不值得比较时，新节点直接把老节点整个替换了，过程如下： 

* 取得oldvnode.el的父节点，parentEle是真实dom

* createEle(vnode)会为vnode创建它的真实dom，令vnode.el =真实dom

* 将新的dom插入，移除旧的dom


#### 这里展示的例子并没有完全的契合vue  vue中实际的diff算法更复杂；它考虑到了class的动态绑定和input的type值，对sameVnode进行了修改等等
