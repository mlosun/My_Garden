---
{"dg-publish":true,"dg-path":"9 Obsidian/CSS 片段/✅ 已启用/MySnippets 多栏布局.md","permalink":"/9 Obsidian/CSS 片段/✅ 已启用/MySnippets 多栏布局/","created":"2025-06-09","updated":"2025-07-31"}
---


简介:: 用于定义 MySnippet 插件的状态栏菜单及其内部滚动菜单，并提供一个流畅的列布局，同时确保菜单在屏幕上有一个合理的最大高度和最小宽度。
来源:: [PKMer](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E5%A4%96%E8%A7%82/css-%E7%89%87%E6%AE%B5/obsidian%E6%8F%92%E4%BB%B6%E6%A0%B7%E5%BC%8F-mysnippets%E7%9A%84%E5%A4%9A%E6%A0%8F%E5%B8%83%E5%B1%80/)

```css
/* ! 插件：MySnippet */
.MySnippets-statusbar-menu {
  min-width: 50vw !important;
  max-height: 80vh !important;
  .menu-scroll {
    display: block !important;
    column-width: 320px;
    width: 100%;
    height: 100%;
  }

}
```