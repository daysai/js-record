# hash

## 快速哈希函数

- A string hash function based on Daniel J. Bernstein's popular 'times 33' algorithm.

```js
function hash(text) {
  let hash = 5381;
  let index = text.length;

  while (index) {
    hash = (hash * 33) ^ text.charCodeAt(--index);
  }

  return hash >>> 0;
}
```

> time33 哈希函数因其高效且分布好（不容易冲突），是已知的针对 string 的最好的哈希函数之一，被 perl 使用并出现在 Berkeley DB 中。
