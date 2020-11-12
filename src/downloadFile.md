# 前端手动模拟浏览器下载文件

## 利用 base64

```js
/**
 * 下载文件
 * @param {String} path - 下载地址/下载请求地址
 * @param {String} name - 下载文件的名字（考虑到兼容性问题，最好加上后缀名）
 */
downloadFile (path, name) {
  const xhr = new XMLHttpRequest();
  xhr.open('get', path);
  xhr.responseType = 'blob';
  xhr.setRequestHeader('authorization', '');
  xhr.send();
  xhr.onload = function () {
    if (this.status === 200 || this.status === 304) {
      const fileReader = new FileReader();
      fileReader.readAsDataURL(this.response);
      fileReader.onload = function () {
        const a = document.createElement('a');
        a.style.display = 'none';
        a.href = this.result;
        a.download = name;
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
      };
    }
  };
}
```

## 关于文件名

> 针对请求时并不知道文件名，或后端指定文件名的情况

### Content-Disposition

```js
// xhr -> XMLHttpRequest
function getFileName() {
  const content = xhr.getResponseHeader('content-disposition'); // 全小写
  if (content) {
    let name1 = content.match(/filename=(.*);/)[1]; // 解析 filename
    let name2 = content.match(/filename\*=(.*)/)[1]; // 解析 filename*
    name1 = decodeURIComponent(name1);
    name2 = decodeURIComponent(name2.substring(6)); // 解码并去掉 UTF-8''
    return name2 || name1;
  }
}
```

> 优先使用 `name2`，`name1` 包含中文或特殊符号时，存在编码还原问题

- `filename*`，现代浏览器支持的，解决 `filename` 的中文或特殊符号编码还原问题，一般是 `UTF-8`，解码使用 `decodeURIComponent` ，需要去掉`UTF-8''`

### 自定义 header

在跨域的情况下，前端获取到的 `header` 只有默认的6个基本字段：`Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`、`Pragma`。

```js
Access-Control-Expose-Headers: Content-Disposition, Custom-Header
```

> 前端通过 `Custom-Header` 获取，`Content-Disposition` 仍需保留
