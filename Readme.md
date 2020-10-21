## ajax的全新封装
> 统一走fetch的风格。内置参数处理, 支持多实例。


## 浏览器兼容性

![Chrome](https://raw.github.com/alrra/browser-logos/master/src/chrome/chrome_48x48.png) | ![Firefox](https://raw.github.com/alrra/browser-logos/master/src/firefox/firefox_48x48.png) | ![Safari](https://raw.github.com/alrra/browser-logos/master/src/safari/safari_48x48.png) | ![Opera](https://raw.github.com/alrra/browser-logos/master/src/opera/opera_48x48.png) | ![Edge](https://raw.github.com/alrra/browser-logos/master/src/edge/edge_48x48.png) | ![IE](https://raw.github.com/alrra/browser-logos/master/src/archive/internet-explorer_9-11/internet-explorer_9-11_48x48.png) |
--- | --- | --- | --- | --- | --- |
Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | 10+ ✔ |


### 版本
> 共有2个版本, 一个传统版本, 基于`XMLHttpRequest`; 另一个是新一代版本, 基于`window.fetch()`。

`**注意:**`

由于`window.fetch()`只支持`http/https`协议, 所以在一些特殊的环境下(如electron等), 请使用传统版。

### 2个版本的区别

1. 超时的返回值不一样。fetch版没有额外处理, 全由原生返回; 传统版为处理过, 统一返回`Response对象`。

2. 缓存参数不一致, 传统版只有传入`no-store`才不会缓存,其他任何值都会缓存, 缓存机制由headers及浏览器机制决定。  fetch版支持完整的参数, 详见原生fetch文档。

3. 验证机制,传参不一样。传统版credentials为布尔值; fetch版本则是支持omit, same-origin, include。


### 示例

```js
import fetch from '//dist.bytedo.org/fetch/dist/index.js'   // 传统版
// import fetch from '//dist.bytedo.org/fetch/dist/next.js'  // fetch版


fetch('/get_list', {body: {page: 1}})
  .then(r => r.json())
  .then(list => {
    console.log(list)
  })


// 创建一个新的fetch实例, 可传入新的基础域名, 和公共参数等
var f1 = fetch.create('//192.168.1.101', {headers: {token: 123456}})

f1('/get_list', {body: {page: 1}})
  .then(r => r.json())
  .then(list => {
    console.log(list)
  })


```



### APIs

1. fetch(url[, options<Object>])
> 发起一个网络请求, options的参数如下。 同时支持配置公共域名, 公共参数。

  + method<String> 默认GET, 可选GET/POST/PUT/DELETE...
  + body<Any> 要发送的数据, 如果是GET方式, 会被自动拼接到url上
  + cache<String>  是否缓存, 
  + credentials<String/Boolean> 是否校验
  + signal<Object>  网络控制信号, 可用于中断请求
  + timeout<Number>  超时时间, 默认30秒, 单位毫秒

```js
fetch.BASE_URL = '//192.168.1.100'
fetch.__INIT__ = {headers: {token: 123456}}

```


2. fetch.create([base_url][, options<Object>])
> 创建一个新的fetch实例
