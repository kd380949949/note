**1.实现一个call（）**
Function.prototype.mycall(context){
    if(typeof this !== 'function'){
        throw new TypeError('Error');
    }
    const args = [...arguments].slice(1);
    context = context||window;
    context.fn = this; //把所绑定的 方法或函数 加到 对象身上
    const result = context.fn(...args);
    delete context.fn;
    return result;
}
**2.实现一个apply（）**
Function.prototype.myApply(context){
    if(typeof this !== 'function'){
        throw new ErrorType('Error');
    }
    context = context||window;
    context.fn = this;
    let result;
    if(arguments[1]){
        result = context.fn(...arguments[1])
    }else{
        result = context.fn()
    }
    delete context.fn;
    return result;
}