## ajax的全新封装
> 统一走fetch的风格。


### 版本
> 共有2个版本, 一个传统版本, 基于`XMLHttpRequest`; 另一个是新一代版本, 基于`window.fetch()`。2个版本功能基本一致, 使用上没有区别。

`**注意:**`

由于`window.fetch()`只支持`http/https`协议, 所以在一些特殊的环境下(如electron等), 请使用传统版。