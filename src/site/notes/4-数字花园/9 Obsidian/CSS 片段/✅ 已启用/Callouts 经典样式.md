---
{"dg-publish":true,"permalink":"/4-数字花园/9 Obsidian/CSS 片段/✅ 已启用/Callouts 经典样式/","created":"2025-06-09","updated":"2025-07-31"}
---


简介:: 使用 css 将 Callout 恢复为经典样式。
来源:: [PKMer](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E5%A4%96%E8%A7%82/css-%E7%89%87%E6%AE%B5/obsidian%E6%A0%B7%E5%BC%8F-callout%E6%A0%B7%E5%BC%8F/#%E6%81%A2%E5%A4%8D%E7%BB%8F%E5%85%B8%E7%9A%84-callout-%E6%A0%B7%E5%BC%8F)

```css
 /*
 * @Author: cumany cuman@qq.com
 * @Source: Pkmer.cn
*/
.callout {
  --callout-radius: 2px;
  border-left: solid 4px rgb(var(--callout-color));
}

.callout .callout-title {
  padding: 6px;
  background-color: rgba(var(--callout-color), 0.4);
}
.callout .callout-content {
  background-color: rgba(var(--callout-color), 0.1);
}

.callout {
  padding: 0;
  background-color:var(--admonition-bg-color);
}

.callout-content {
  padding: 5px 15px;
}
```