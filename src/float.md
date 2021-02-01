# float

## 浮点数运算常用方案

```js
parseFloat((数学表达式).toFixed(digits))； // toFixed() 精度参数须在 0 与20 之间
// Example
parseFloat((1.0 - 0.9).toFixed(10)) // 结果为 0.1
parseFloat((0.3 / 0.1).toFixed(10)) // 结果为 3
parseFloat((9.7 * 100).toFixed(10)) // 结果为 970
parseFloat((2.22 + 0.1).toFixed(10)) // 结果为 2.32
```
