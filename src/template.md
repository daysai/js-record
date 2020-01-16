## JS一句话实现ES6类似的模板

```js
function template(str, obj) {
  return String(str).replace(/\$\{(.*?)\}/g, function(match, key) {
    return obj[key.trim()];
  });
}
```

> 经典之处在于，巧妙的使用 `repalce` 方法的回调函数，`match` 表示匹配到的对应字符片段，`key` 表示 `(.*?)` 非贪婪模式匹配到的 `${}` 中间的内容，回调函数返回的字符片段会用来执行`repalce`。需要注意的是，正则内部的匹配是全局匹配。这种方法还节省了 `obj` 多余遍历的可能性，以及对 `${}` 内部的空格进行了修正。