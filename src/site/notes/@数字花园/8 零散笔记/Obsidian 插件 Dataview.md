---
{"dg-publish":true,"dg-path":"8 零散笔记/Obsidian 插件 Dataview.md","permalink":"/8 零散笔记/Obsidian 插件 Dataview/","created":"2023-10-31","updated":"2025-08-01"}
---


简介:: 数据视图插件

## 常用字段

#### 基本格式

```
<Query-Type> <Fields>
From <Source> 
<Data-Command> <Expression> 
<Data-Command> <Expression> 

%% 注释：可以有很多个 <Data-Command> %%
```

Query-Type
- LIST
- TABLE
- TASK
- CALENDAR

[Obsidian 插件：Dataview](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E7%A4%BE%E5%8C%BA%E6%8F%92%E4%BB%B6/dataview/dataview/)

## 四种查询方式

- **DQL 行内查询**	可以直接插入文章中，像 excel 中使用函数那样，可以实现级联，缺点是功能不完整
- **DQL 代码块查询**	Dataview 用的最多的查询方式
- **DVJS 行内查询**	和 DQL 行内查询类似，但是功能更多，但是需要用 javascript
- **DVJS 代码块查询**	可以满足大部分要求

#### DQL 行内查询

- Obsidian 插件 Dataview

#### DQL 代码块查询

#### DVJS 行内查询

#### DVJS 代码块查询

## 今日完成

```
task
where completion = date("<% tp.date.now("YYYY-MM-DD") %>")
```

## 今日创建

```
table type,status
where created = this.created
sort type asc
```