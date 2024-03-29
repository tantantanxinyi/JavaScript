### 手写 call 函数

**Implementing the call Function Manually**



### call 函数的实现步骤：

Steps to Implement the call Function：



1. 判断调用对象是否为函数，即使我们是定义在函数的原型上的，但是可能出现使用 call 等方式调用的情况。

Determine if the caller is a function, even though it's defined on the function's prototype, it might be called using methods like **call**.



1. 判断传入上下文对象是否存在，如果不存在，则设置为 **window** 。

Check if the passed-in context object exists; if not, set it to **window**.



1. 处理传入的参数，截取第一个参数后的所有参数。

Process the passed-in arguments, slicing off all parameters after the first one.



1. 将函数作为上下文对象的一个属性。

Attach the function as a property of the context object.



1. 使用上下文对象来调用这个方法，并保存返回结果。

Invoke the method using the context object and save the result.



1. 删除刚才新增的属性。

Remove the newly added property.



1. 返回结果。

Return the result.



```plain
// call函数实现
Function.prototype.myCall = function(context) {
  // 判断调用对象
  if (typeof this !== "function") {
    console.error("type error");
  }
  // 获取参数
  let args = [...arguments].slice(1),
      result = null;
  // 判断 context 是否传入，如果未传入则设置为 window
  context = context || window;
  // 将调用函数设为对象的方法
  context.fn = this;
  // 调用函数
  result = context.fn(...args);
  // 将属性删除
  delete context.fn;
  return result;
};
```