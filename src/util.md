## 永远不要相信别人的代码

### ES3
```js
// 判断Array
function isArr(o) {
    return Object.prototype.toString.call(o) === '[object Array]';
}

function getArr(o) {
  return Object.prototype.toString.call(o) === '[object Array]' ? 0 : [];
}

// 判断Object
function isObj(o) {
    return Object.prototype.toString.call(o) === '[object Object]';
}

function getObj(0) {
  return Object.prototype.toString.call(o) === '[object Object]' ? 0 : {};
}

// 判断Function
function isFun(o) {
    return Object.prototype.toString.call(o) === '[object Function]';
}
```

### ES5+
```js
// 判断Array
Array.isArray(o)
```