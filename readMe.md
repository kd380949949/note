## 1.实现一个call（）

    **1.实现一个call（）**
    Function.prototype.mycall(context){
        if(typeof this !== 'function'){
            throw new TypeError('Error');
        }
        const args = [...arguments].slice(1);
        context = context||window;
        context.fn = this; //把调用call的 方法或函数 加到 对象身上
        const result = context.fn(...args);
        delete context.fn;
        return result;
    }
## **2.实现一个apply（）**

    **2.实现一个apply（）**
    Function.prototype.myApply(context){
        if(typeof this !== 'function'){
            throw new ErrorType('Error');
        }
        context = context||window;
        context.fn = this;////把调用apply的 方法或函数 加到 对象身上
        let result;
        if(arguments[1]){
            result = context.fn(...arguments[1])
        }else{
            result = context.fn()
        }
        delete context.fn;
        return result;
    }
## **3.实现一个bind（）**

    **3.实现一个bind（）**
    Function.prototype.myBind(context){
        if(typeof this !== 'function'){
            throw new TypeError('Error');
        }
        context = context || window;
        const _this = this;
        const args = [...arguments].slice(1);
        return function F(){
                if(this instanceof F){
                    return new _this(...args,...arguments)
                }else{
                    return _this.apply(context,args.concat([...arguments]))
                }
        }
    }
## **4.实现一个instanceof**

    **4.实现一个instanceof**
    function myInstanceof(left,right){ //left实例，right构造函数
        let prototype = right.prototype;
        left = left.__proto__;
        while(true){
            if(left===null || left===undefined){
                return false
            }
            if(prototype === left ){
                return true;
            }
            left = left.__proto__;
    }
## **5.实现一个new**

    **5.实现一个new**
    function create(){
        let obj = new Object();
        let args = [...arguments]
        let Con = args[0];
        obj.__proto__ = Con.prototype;
        let result = Con.apply(obj,arguments.slice(1))
    }