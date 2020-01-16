## 遍历 Object 属性时的 hasOwnProperty

`hasOwnProperty` 方法是 `Javascript` 中唯一一个处理对象属性而不会往上遍历原型链的

```js
Object.prototype.bar = 1;
var foo = {goo: undefined};

foo.bar; // 1
'bar' in foo; // true

foo.hasOwnProperty('bar'); // false
foo.hasOwnProperty('goo'); // true
```
> 在这里，只有 `hasOwnProperty` 能给出正确答案，这在遍历一个对象的属性时是非常必要的。


`Javascript` 并未将 `hasOwnProperty` 设为敏感词，这意味着你可以拥有一个命名为 `hasOwnProperty` 的属性。这个时候你无法使用本身的 `hasOwnProperty` 方法来判断属性，所以你需要使用外部的 `hasOwnProperty` 方法来进行判断。
示例：
```js
var foo = {
hasOwnProperty: function() {
return false;
},
bar: 'Here be dragons'
};

foo.hasOwnProperty('bar'); // always returns false

// Use another Object's hasOwnProperty and call it with 'this' set to foo
({}).hasOwnProperty.call(foo, 'bar'); // true

// It's also possible to use hasOwnProperty from the Object
// prototype for this purpose
Object.prototype.hasOwnProperty.call(foo, 'bar'); // true
```