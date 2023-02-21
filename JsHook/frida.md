## 获取地址

#### 获取模块地址

```js
//获取 libil2cpp.so 的首地址
var address = Module.findBaseAddress('libil2cpp.so')
```

#### 获取函数地址

```js
//获取在 libil2cpp.so 中 func 函数的地址
var targetFunc = Module.findExportByName("libil2cpp.so", "func");

//如果知道 libil2cpp.so 的首地址到方法的偏移量的话,可以先获取 libil2cpp.so 的地址在加上偏移量
var offset = '0x013eeda0' //偏移量
var address = Module.findBaseAddress('libil2cpp.so')
var targetFunc = address.add(offset)
```







## hook native  函数

```js
// 找到要拦截的函数地址
var targetFunc = Module.findExportByName("libfoo.so", "foo");

// 注册一个拦截器
Interceptor.attach(targetFunc, {
    onEnter: function(args) {
        // 打印函数参数
        console.log("foo(" + args[0] + ", " + args[1] + ")");

        // 修改参数
        args[0] = 0;
        args[1] = ptr("0x12345678");
    },
    onLeave: function(retval) {
        // 打印函数返回值
        console.log("foo => " + retval);
    }
});
```



## native 主动调用

```js
var friendlyFunctionName = new NativeFunction(friendlyFunctionPtr, 'void', ['pointer', 'pointer']);
var returnValue = Memory.alloc(sizeOfLargeObject);
friendlyFunctionName(returnValue, param1);
```

