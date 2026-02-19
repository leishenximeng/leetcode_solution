







## 查询

### 1757. 可回收且低脂的产品

下面是 **力扣（LeetCode）第 1757 题：可回收且低脂的产品（Recyclable and Low Fat Products）** 的题目描述和 **标准 SQL 查询写法**。([goodtecher.com](https://www.goodtecher.com/leetcode-1757-recyclable-and-low-fat-products/?utm_source=chatgpt.com))

------

#### 📌 题目描述（中文）

有一个 `Products` 表，结构如下：

| 字段名     | 类型          |
| ---------- | ------------- |
| product_id | int 主键      |
| low_fats   | enum('Y','N') |
| recyclable | enum('Y','N') |

其中：

- `low_fats='Y'` 表示产品是低脂的，`'N'` 表示不是；
- `recyclable='Y'` 表示产品是可回收的，`'N'` 表示不可回收。

**要求返回既是低脂又是可回收的产品 ID**（顺序可以任意）。([goodtecher.com](https://www.goodtecher.com/leetcode-1757-recyclable-and-low-fat-products/?utm_source=chatgpt.com))

------

#### ✅ SQL 解法示例

下面是该题的标准 SQL 查询语句：

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```

这个查询使用了简单的 `WHERE` 条件筛选，选出满足两个条件的记录。([goodtecher.com](https://www.goodtecher.com/leetcode-1757-recyclable-and-low-fat-products/?utm_source=chatgpt.com))

------

#### 🧾 示例说明

例如表如下：

| product_id | low_fats | recyclable |
| ---------- | -------- | ---------- |
| 0          | Y        | N          |
| 1          | Y        | Y          |
| 2          | N        | Y          |
| 3          | Y        | Y          |
| 4          | N        | N          |

**返回结果应该是：**

| product_id |
| ---------- |
| 1          |
| 3          |

只有 1 和 3 同时满足低脂且可回收两个条件。([Leetcode](https://leetcode.ca/2021-04-09-1757-Recyclable-and-Low-Fat-Products/?utm_source=chatgpt.com))

------

如果你想要我帮你生成更多测试用例或讲解这个题怎么在力扣上运行，也可以继续问我！💡















### 584.寻找用户推荐人

这题也是**纯 SQL 入门题**，很适合热手 👍
我们直接来。

------

#### 🧩 力扣 584：寻找用户推荐人（Find Customer Referee）

##### 表结构：`Customer`

| 字段名     | 类型       |
| ---------- | ---------- |
| id         | int        |
| name       | varchar    |
| referee_id | int / null |

- `referee_id` 表示**推荐该用户的用户 id**
- 有些用户没有推荐人，`referee_id` 为 `NULL`

------

#### 🎯 题目要求

**找出所有不是被 id = 2 的用户推荐的用户姓名**

👉 注意两点：

1. `referee_id != 2`
2. **`referee_id IS NULL` 的也要算进去**（这是很多人第一次会 WA 的点）

------

#### ✅ 正确 SQL 写法（标准答案）

```sql
SELECT name
FROM Customer
WHERE referee_id != 2
   OR referee_id IS NULL;
```

------

#### 🧠 为什么要加 `IS NULL`？

因为在 SQL 里：

```sql
NULL != 2   -- 结果不是 true，而是 UNKNOWN
```

所以如果你只写：

```sql
WHERE referee_id != 2;
```

👉 **所有 `referee_id IS NULL` 的行都会被过滤掉** ❌

而题目是要保留这些人的。

------

#### 🧪 举个例子

##### Customer 表

| id   | name | referee_id |
| ---- | ---- | ---------- |
| 1    | Will | NULL       |
| 2    | Jane | NULL       |
| 3    | Alex | 2          |
| 4    | Bill | 3          |
| 5    | Zack | 1          |

##### 查询结果应为：

| name |
| ---- |
| Will |
| Jane |
| Bill |
| Zack |

❌ Alex 被 2 推荐 → 排除

------

#### ✅ 另一种等价写法（可读性好）

```sql
SELECT name
FROM Customer
WHERE referee_id IS NULL
   OR referee_id <> 2;
```

------

#### 🧠 这题考的核心其实是

- `NULL` 的比较规则
- `IS NULL` / `IS NOT NULL`
- `WHERE` 条件里的逻辑判断

------

如果你愿意，我可以帮你**总结一页「力扣 SQL 新手必踩的 NULL 坑」**，或者继续刷下一道（595 / 586 / 607 都是同一档）🔥











### 595.大的国家 

继续热身题 🔥 这道也很直给。

------

#### 🌍 力扣 595：大的国家（Big Countries）

##### 表结构：`World`

| 字段名     | 类型    |
| ---------- | ------- |
| name       | varchar |
| continent  | varchar |
| area       | int     |
| population | int     |
| gdp        | bigint  |

------

#### 🎯 题目要求

找出 **面积 ≥ 3,000,000**
**或者**
**人口 ≥ 25,000,000**

的国家，返回：

- `name`
- `population`
- `area`

------

#### ✅ 标准 SQL 查询

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000
   OR population >= 25000000;
```

------

#### 🧠 关键点

- 条件是 **或（OR）**，不是且（AND）
- 数字不用加引号
- 返回字段顺序按题目要求

------

#### 🧪 示例理解

假设数据：

| name | area    | population |
| ---- | ------- | ---------- |
| A    | 1000000 | 30000000   |
| B    | 4000000 | 10000000   |
| C    | 2000000 | 10000000   |

结果：

- A：人口大 ✅
- B：面积大 ✅
- C：都不大 ❌

------

#### 🏁 一句话记忆

> **大的国家 = 面积大 或 人口多**

------

你现在刷到的这几题（1757 / 584 / 595）基本是 **SQL 基础三板斧** 了
下一道如果是 **627（交换性别）** 或 **607（销售员）**，我也可以直接带你过 😄











### 1148.文章浏览 I

这题也是 **SQL 基础题 + 去重**，很舒服 👍
直接来。

------

#### 📰 力扣 1148：文章浏览 I（Article Views I）

##### 表结构：`Views`

| 字段名     | 类型 |
| ---------- | ---- |
| article_id | int  |
| author_id  | int  |
| viewer_id  | int  |
| view_date  | date |

------

#### 🎯 题目要求

**找出作者自己浏览了自己文章的作者 id**

👉 条件很关键：

```text
author_id = viewer_id
```

👉 结果要 **去重**，并按 `id` 升序返回

------

#### ✅ 正确 SQL 查询

```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;
```

------

#### 🧠 关键点拆解

##### 1️⃣ 自己看自己的文章

```sql
author_id = viewer_id
```

##### 2️⃣ 可能一个作者看过很多次 → 要去重

```sql
SELECT DISTINCT
```

##### 3️⃣ 按 id 升序（LeetCode 很爱考这个）

```sql
ORDER BY id
```

------

#### 🧪 示例理解

##### Views 表

| article_id | author_id | viewer_id |
| ---------- | --------- | --------- |
| 1          | 3         | 3         |
| 2          | 7         | 7         |
| 3          | 3         | 3         |
| 4          | 7         | 6         |

👉 符合条件的 author：

- 3（看了两次，但只返回一次）
- 7

------

##### 输出

| id   |
| ---- |
| 3    |
| 7    |

------

#### 🏁 一句话记忆

> **作者 = 浏览者 → DISTINCT → ORDER BY**

------

你现在这条刷题路线很对：
**1757 → 584 → 595 → 1148**
下一道常接的是 **1683 / 607 / 1484 / 1527**
要不要我按这个顺序直接带你刷下去 🚀





### 1683.无效的推文

来，这道还是**SQL 基础题 + 字符串长度判断**，不绕 👍

------

#### 🐦 力扣 1683：无效的推文（Invalid Tweets）

##### 表结构：`Tweets`

| 字段名   | 类型    |
| -------- | ------- |
| tweet_id | int     |
| content  | varchar |

------

#### 🎯 题目要求

**找出内容长度超过 15 个字符的推文 id**

👉 注意：

- 只返回 `tweet_id`
- 不要求排序（当然排了也不扣分）

------

#### ✅ 标准 SQL 查询（MySQL / LeetCode 通用）

```sql
SELECT tweet_id
FROM Tweets
WHERE CHAR_LENGTH(content) > 15;
```

------

#### 🧠 关键点（很重要）

##### 🔹 为什么用 `CHAR_LENGTH` 而不是 `LENGTH`？

- `CHAR_LENGTH()`：**字符数** ✅（题目要的）
- `LENGTH()`：**字节数** ❌（中文、emoji 会出问题）

👉 LeetCode 官方也是推荐 `CHAR_LENGTH`

------

##### 🧪 示例理解

| tweet_id | content                        |
| -------- | ------------------------------ |
| 1        | Hello World                    |
| 2        | This is a very very long tweet |

- `Hello World` → 11 个字符 ❌
- 第二条 > 15 个字符 ✅

------

#### 🏁 一句话记忆

> **无效推文 = CHAR_LENGTH(content) > 15**

------

你现在这波已经把 **SQL 入门必刷 5 连**打完了：

- 1757（条件筛选）
- 584（NULL）
- 595（OR）
- 1148（DISTINCT + ORDER）
- 1683（字符串函数）

下一道要不要直接上 **607（销售员）** 或 **1484（按日期分组）**？我可以继续陪你一路刷 👌









## 连接

### 1378.使用唯一标识码替换员工ID

这题是 LeetCode SQL 题：**1378. 使用唯一标识码替换员工ID**
核心就是：**把 Employees 表里的 id 替换成 EmployeeUNI 表里的 unique_id** —— 本质是一个 `LEFT JOIN`。

------

#### 📌 题目理解

有两张表：

##### Employees

| id   | name |
| ---- | ---- |
|      |      |

##### EmployeeUNI

| id   | unique_id |
| ---- | --------- |
|      |           |

要求输出：

| unique_id | name |

⚠ 注意：

- 有些员工 **可能没有 unique_id**
- 这种情况要返回 `NULL`
- 所以必须用 `LEFT JOIN`，不能用 `INNER JOIN`

------

#### ✅ SQL 写法

```sql
SELECT eu.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
ON e.id = eu.id;
```

------

#### 🔎 逻辑解释

##### 第一步：以 Employees 为主表

因为题目要保留所有员工（即使没有 unique_id）。

```
FROM Employees e
```

------

##### 第二步：左连接 EmployeeUNI

```
LEFT JOIN EmployeeUNI eu
ON e.id = eu.id
```

意思是：

> 用 Employees.id 去匹配 EmployeeUNI.id

- 如果能匹配 → 返回 unique_id
- 如果不能匹配 → unique_id = NULL

------

##### 🚫 为什么不能用 INNER JOIN？

如果写：

```sql
INNER JOIN EmployeeUNI eu
```

那么：

- 没有 unique_id 的员工会被过滤掉
- 结果不完整 ❌

------

##### 🧠 这题考什么？

典型的：

> “主表保留全部数据” → 用 LEFT JOIN

记忆口诀：

| 需求         | 用什么     |
| ------------ | ---------- |
| 保留左表全部 | LEFT JOIN  |
| 保留右表全部 | RIGHT JOIN |
| 只要匹配的   | INNER JOIN |

------

##### 🎯 最终标准答案

```sql
SELECT eu.unique_id, e.name
FROM Employees e
LEFT JOIN EmployeeUNI eu
ON e.id = eu.id;
```

------

如果你愿意，我可以再帮你：

- 画一张 LEFT JOIN 的图解
- 或出 2 道 JOIN 练习题让你巩固
- 或总结一套 SQL Hot100 连接题模板 🚀





### 1068.产品销售分析 I 

#### 1068. 产品销售分析 I（连接怎么写）

这题本质：
**把 Sales 表里的 product_id 和 Product 表连起来，查出产品名 + 销售信息。**

------

#### 📌 表结构理解

**Sales**

| sale_id | product_id | year | quantity | price |

**Product**

| product_id | product_name |

------

#### 📌 题目要求

输出：

| product_name | year | price |

也就是：

- 从 Product 里拿 product_name
- 从 Sales 里拿 year、price

------

#### ✅ 标准 SQL 写法

```sql
SELECT p.product_name, s.year, s.price
FROM Sales s
JOIN Product p
ON s.product_id = p.product_id;
```

------

#### 🔎 逻辑拆解

##### 第一步：确定主表

因为 year、price 在 Sales 里，所以：

```
FROM Sales s
```

------

##### 第二步：连接 Product

```
JOIN Product p
ON s.product_id = p.product_id
```

意思是：

> 用 Sales.product_id 去匹配 Product.product_id

------

#### ❓ 为什么用 INNER JOIN？

题目默认：

- Sales 里的 product_id 一定在 Product 表中存在
- 不需要保留未匹配的数据

所以直接用：

```
JOIN
```

= 默认就是 `INNER JOIN`

------

#### 🧠 和 1378 的区别

| 题号 | 用什么     | 原因           |
| ---- | ---------- | -------------- |
| 1378 | LEFT JOIN  | 要保留所有员工 |
| 1068 | INNER JOIN | 只要匹配数据   |

------

#### 🎯 记忆技巧

看到：

- “查询产品名 + 销售数据”
- 两张表
- 用 id 关联

脑子里直接浮现：

```sql
FROM 销售表
JOIN 产品表
ON product_id
```

------

如果你愿意，我可以把：

- SQL 连接题给你做一套「Hot50 JOIN 模板总结」
- 或者讲一下三种 JOIN 的底层执行逻辑图

你现在是在刷 SQL50 吗 😄



### 1581.进店却未进行过交易的顾客

#### 1581. 进店却未进行过交易的顾客

这题本质：

> 找「有 visit 记录」但「没有 transaction 记录」的顾客
> 👉 典型 **LEFT JOIN + 判空**

------

#### 📌 表结构理解

**Visits**

| visit_id | customer_id |

**Transactions**

| transaction_id | visit_id | amount |

关系：

- Transactions.visit_id = Visits.visit_id

------

#### 📌 题目要求

输出：

| customer_id | count_no_trans |

表示：

- 某顾客来过几次
- 但这些 visit 没有产生交易

------

#### ✅ 标准写法（推荐）

```sql
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM Visits v
LEFT JOIN Transactions t
ON v.visit_id = t.visit_id
WHERE t.transaction_id IS NULL
GROUP BY v.customer_id;
```

------

#### 🔎 思路拆解

##### 第一步：从 Visits 出发

因为题目是“进店的顾客”，核心是 visit。

```
FROM Visits v
```

------

##### 第二步：左连接 Transactions

```
LEFT JOIN Transactions t
ON v.visit_id = t.visit_id
```

意思：

- 如果该 visit 有交易 → 能匹配
- 如果没有交易 → t 相关字段为 NULL

------

##### 第三步：筛选“没有交易”

```
WHERE t.transaction_id IS NULL
```

这是关键。

> LEFT JOIN 后，右表没匹配 → 全是 NULL

------

##### 第四步：按顾客分组统计

```
GROUP BY v.customer_id
```

统计每个顾客“无交易 visit 次数”。

------

#### 🧠 这题在考什么？

经典模型：

```
找 A 中没有匹配 B 的数据
```

固定套路：

```sql
FROM A
LEFT JOIN B
ON 条件
WHERE B.xxx IS NULL
```

记住这个结构，SQL50 至少会出现 4~5 次。

------

#### 🚀 再给你一个进阶写法（等价）

也可以用 `NOT EXISTS`：

```sql
SELECT v.customer_id, COUNT(*) AS count_no_trans
FROM Visits v
WHERE NOT EXISTS (
    SELECT 1
    FROM Transactions t
    WHERE v.visit_id = t.visit_id
)
GROUP BY v.customer_id;
```

但 SQL50 阶段优先掌握 LEFT JOIN 写法。

------

你现在已经：

- 会普通 JOIN
- 会 LEFT JOIN 判空

再刷几题就会开始出现 GROUP BY + HAVING 组合了 😄

要不要我帮你总结一个：

> “SQL50 高频套路清单（精简版）”





### 197.上升的温度

#### 197. 上升的温度

这题本质是：

> 和“前一天”做对比
> 👉 典型 **自连接（self join）**

------

#### 📌 表结构

**Weather**

| id | recordDate | temperature |

------

#### 📌 题目要求

找出：

> 温度比“前一天”高的记录 id

------

#### ✅ 标准写法（自连接）

```sql
SELECT w1.id
FROM Weather w1
JOIN Weather w2
ON DATEDIFF(w1.recordDate, w2.recordDate) = 1
WHERE w1.temperature > w2.temperature;
```

------

#### 🔎 思路拆解

##### 第一步：为什么要自连接？

因为：

- 要拿“今天”
- 又要拿“昨天”

同一张表，需要用两次 → 自连接。

------

##### 第二步：起两个别名

```
Weather w1  → 今天
Weather w2  → 昨天
```

------

##### 第三步：匹配“昨天”

```
DATEDIFF(w1.recordDate, w2.recordDate) = 1
```

意思：

> w1 比 w2 晚 1 天

也就是：

今天 - 昨天 = 1

------

##### 第四步：比较温度

```
WHERE w1.temperature > w2.temperature
```

------

#### 🧠 这题考什么？

核心模型：

```
和上一条数据比较
```

解决方法：

| 场景       | 方法             |
| ---------- | ---------------- |
| 同一表对比 | 自连接           |
| 有顺序比较 | JOIN + 日期差    |
| 高级写法   | 窗口函数（后期） |

------

#### 🚀 进阶写法（用窗口函数）

如果数据库支持（MySQL 8+）：

```sql
SELECT id
FROM (
    SELECT id,
           temperature,
           LAG(temperature) OVER (ORDER BY recordDate) AS prev_temp
    FROM Weather
) t
WHERE temperature > prev_temp;
```

但 SQL50 阶段建议先熟练自连接。

------

#### 记忆模板

只要看到：

> 比前一天高
> 比上一次大

脑子里直接出现：

```sql
FROM 表 A
JOIN 表 B
ON 日期差 = 1
WHERE A.xxx > B.xxx
```

------

你现在已经刷到自连接了，说明 SQL50 进度过半了 😄
要不要我给你画个“SQL50 难度阶段图”？





### 1661.每台机器的进程平均运行时间











## 聚合函数











## 排序和分组











## 高级查询和连接











## 子查询













## 高级字符串函数 / 正则表达式 / 子句















s





