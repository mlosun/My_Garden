---
{"dg-publish":true,"dg-path":"8 零散笔记/HTTP请求：GET和POST对比.md","permalink":"/8 零散笔记/HTTP请求：GET和POST对比/","created":"2025-05-25","updated":"2025-05-25"}
---


| 项目    | GET 请求                | POST 请求             |
| ----- | --------------------- | ------------------- |
| 参数位置  | 请求的参数附加在 URL 之后       | 请求的参数放在请求体内         |
| 数据大小  | URL 长度存在限制，传递的数据量相对较小 | 理论上不受限，可以传递更多的数据。   |
| 数据缓存  | 可以被缓存，历史记录可以保存        | 不会被缓存，也不会留在浏览器历史记录中 |
| 后退/刷新 | 无害                    | 数据会被重新提交            |
| 适用场景  | 适合公开的、无副作用的数据检索操作。    | 适合创建或更新资源。          |

参考链接：
- [HTTP 方法：GET 对比 POST](https://www.runoob.com/tags/html-httpmethods.html)
- [GET和POST请求到底有什么区别？](https://zhuanlan.zhihu.com/p/689906347)