---
{"dg-publish":true,"permalink":"/4-数字花园/2 代码编程/MySQL/","created":"2025-05-09","updated":"2025-05-09"}
---


## MySQL 常用的 SQL 语句

### 针对数据库的增删改查

```sql
/* 创建数据库 */
CREATE DATABASE 数据库名称;

/* 删除数据库 */
DROP DATABASE 数据库名称;

/* 查看所有数据库 */
SHOW DATABASES;

/* 查看当前数据库的字符集等信息 */
SHOW CREATE DATABASE 数据库名称;

/* 修改数据库的字符集等属性 */
ALTER DATABASE 数据库名称 CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
```

### 针对数据表的增删改查

```sql
/* 创建数据表 */
CREATE TABLE 数据表名称 (字段1 数据类型1, 字段2 数据类型2, ...);

/* 删除数据表 */
DROP TABLE 数据表名称;

/* 查看当前数据库中的所有数据表 */
SHOW TABLES;

/* 查看数据表的结构 */
DESCRIBE 数据表名称;

/* 查看数据表的创建语句 */
SHOW CREATE TABLE 数据表名称;

/* 添加新列 */
ALTER TABLE 数据表名称 ADD COLUMN 新字段 数据类型;

/* 修改列的数据类型 */
ALTER TABLE 数据表名称 MODIFY COLUMN 字段1 新数据类型;

/* 重命名列 */
ALTER TABLE 数据表名称 CHANGE COLUMN 字段1 新字段名 数据类型;

/* 删除列 */
ALTER TABLE 数据表名称 DROP COLUMN 字段1;
```

### 针对数据行的增删改查

```sql
/* 插入数据行 */
INSERT INTO 数据表名称 (字段1, 字段2, ...) VALUES (值1, 值2, ...);

/* 查询数据行 */
SELECT 字段1, 字段2, ... FROM 数据表名称 WHERE 字段1 = '条件值1';

/* 更新数据行 */
UPDATE 数据表名称 SET 字段1 = '新值1', 字段2 = '新值2', ... WHERE 字段1 = '条件值1';

/* 删除数据行 */
DELETE FROM 数据表名称 WHERE 字段1 = '条件值1';
```

## MySQL 常用的数据类型

### 数值类型

| 数据类型 | 说明 | 示例 | 说明 |
|----------|------|------|------------|
| `INT` | 普通大小的整数 | `INT` |  |
| `BIGINT` | 大整数 | `BIGINT` |  |
| `FLOAT` | 单精度浮点数 | `FLOAT(10,2)` | `(10,2)` 表示总长度为 10 位，其中 2 位是小数 |
| `DOUBLE` | 双精度浮点数 | `DOUBLE(15,2)` | `(15,2)` 表示总长度为 15 位，其中 2 位是小数 |
| `DECIMAL` | 定点数，适合精确计算 | `DECIMAL(10,2)` | `(10,2)` 表示总长度为 10 位，其中 2 位是小数 |

### 字符串类型

| 数据类型 | 说明 | 示例 | 说明 |
|----------|------|------|------------|
| `VARCHAR` | 可变长度的字符串 | `VARCHAR(255)` | `(255)` 表示最大长度为 255 字符 |
| `TEXT` | 较长的字符串 | `TEXT` |  |

### 日期和时间类型

| 数据类型 | 说明 | 示例 | 说明 |
|----------|------|------|------------|
| `DATETIME` | 日期和时间 | `DATETIME` |  |
| `TIMESTAMP` | 时间戳 | `TIMESTAMP` |  |

### JSON 类型

| 数据类型 | 说明 | 示例 | 括号内含义 |
|----------|------|------|------------|
| `JSON` | 用于存储 JSON 格式的数据 | `JSON` |  |
