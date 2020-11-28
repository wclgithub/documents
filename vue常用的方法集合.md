1.  使用过滤器将时间戳转时间字符串: （当然放在公共方法中调用也是一样的）

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


