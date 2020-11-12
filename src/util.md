# 永远不要相信别人的代码

## TS

```js
const isType = <T>(type: string | string[]) => (obj: unknown): obj is T =>
  obj != null &&
  (Array.isArray(type) ? type : [type]).some(
    t => Object.prototype.toString.call(obj) === `[object ${t}]`
  );
const isFn = isType<(...args: any[]) => any>([
  'Function',
  'AsyncFunction',
  'GeneratorFunction'
]);
const isArr = Array.isArray;
const isPlainObj = isType<object>('Object');
const isStr = isType<string>('String');
const isBool = isType<boolean>('Boolean');
const isNum = isType<number>('Number');
const isObj = (val: unknown): val is object => typeof val === 'object';
const isRegExp = isType<RegExp>('RegExp');
```

## JS

```js
function isType(type) {
  return function (obj) {
    return obj != null && (Array.isArray(type) ? type : [type]).some(
      t => Object.prototype.toString.call(obj) === `[object ${t}]`
    )
  }
}

const isArr = Array.isArray;
const isObj = isType('Object');
const isRegExp = isType('RegExp');
const isFn = isType([
  'Function',
  'AsyncFunction',
  'GeneratorFunction'
]);
```

## ES3

```js
// 判断Array
function isArr(o) {
  return Object.prototype.toString.call(o) === '[object Array]';
}

function getArr(o) {
  return Object.prototype.toString.call(o) === '[object Array]' ? o : [];
}

// 判断Object
function isObj(o) {
  return Object.prototype.toString.call(o) === '[object Object]';
}

function getObj(o) {
  return Object.prototype.toString.call(o) === '[object Object]' ? o : {};
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
