---
{"dg-publish":true,"dg-path":"8 零散笔记/打印全部的 DataFrame 行和列.md","permalink":"/8 零散笔记/打印全部的 DataFrame 行和列/","created":"2025-04-07","updated":"2025-04-07"}
---


在写 Python 时，经常需要打印 DataFrame 用于检查，但 DataFrame 的默认显示设置会对打印出来的行数和列数进行限制。

如果希望打印出 DataFrame 的全部行和列，可以通过如下方法设置：

```python
import pandas as pd

pd.set_option('display.max_rows', None)  # 显示所有行
pd.set_option('display.max_columns', None)  # 显示所有列
pd.set_option('display.expand_frame_repr', False)  # 禁止自动换行
pd.set_option('display.width', None)  # 设置显示宽度为无限制
```