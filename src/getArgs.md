# getArgs

读取函数参数名的方法，参考 [promisify-node](https://github.com/nodegit/promisify-node)

```js
function getArgs(func) {
  // 首先匹配函数括弧里的参数
  var args = func.toString().match(/function\s.*?\(([^)]*)\)/)[1];

  // 分解参数成数组
  return args.split(",").map(function(arg) {
    // 去空格和内联注释
    return arg.replace(/\/\*.*\*\//, "").trim();
  }).filter(function(arg) {
    // 确保没有undefineds
    return arg;
  });
}
```

效果展示

```js
function myCustomFn(arg1, arg2,arg3) {}

console.log(getArgs(myCustomFn)); // ["arg1", "arg2", "arg3"]
```
