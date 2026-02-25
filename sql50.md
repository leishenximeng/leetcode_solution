







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

这题本质：

> 同一个 machine_id + process_id
> start 时间 和 end 时间 配对
> 然后求平均运行时间

👉 典型 **自连接 + GROUP BY**

------

#### 📌 表结构

**Activity**

| machine_id | process_id | activity_type | timestamp |

其中：

- activity_type = 'start'
- activity_type = 'end'

每个进程：

- 一条 start
- 一条 end

------

#### 📌 题目要求

输出：

| machine_id | processing_time |

processing_time 是：

> 每台机器的平均运行时间
> = 每个进程 (end - start) 的平均值

------

#### ✅ 标准写法（自连接）

```sql
SELECT a.machine_id,
       ROUND(AVG(b.timestamp - a.timestamp), 3) AS processing_time
FROM Activity a
JOIN Activity b
ON a.machine_id = b.machine_id
AND a.process_id = b.process_id
AND a.activity_type = 'start'
AND b.activity_type = 'end'
GROUP BY a.machine_id;
```

------

#### 🔎 思路拆解

##### 第一步：为什么自连接？

因为：

- 一条是 start
- 一条是 end
- 在同一张表

所以必须用两次 Activity。

------

##### 第二步：起两个别名

```
a → start 记录
b → end 记录
```

------

##### 第三步：匹配同一个进程

```
a.machine_id = b.machine_id
a.process_id = b.process_id
```

保证是同一机器同一进程。

------

##### 第四步：限制类型

```
a.activity_type = 'start'
b.activity_type = 'end'
```

确保：

- a 是开始
- b 是结束

------

##### 第五步：计算运行时间

```
b.timestamp - a.timestamp
```

得到：

> 单个进程运行时间

------

##### 第六步：求平均

```
AVG(...)
GROUP BY machine_id
```

按机器分组。

------

#### 🧠 这题的固定模型

看到：

- 同一表
- start / end 配对
- 求差值

脑子里立刻出现：

```sql
FROM 表 a
JOIN 表 b
ON 同一ID
AND a.type = 'start'
AND b.type = 'end'
```

------

#### 🚀 进阶理解（重要）

为什么不用 LEFT JOIN？

因为：

- 每个 start 一定有对应 end
- 题目保证数据合法

所以用 INNER JOIN。

------

#### ⭐ 这题在 SQL50 里的地位

属于：

> 中等偏简单的自连接应用

难点只有一个：

> 想到“同一表配对”

------

如果你愿意，我可以给你做一个：

- 「自连接专题总结」
- 或者整理一个 SQL50 连接类终极模板清单

你现在进度已经过半了 😄





### 577.员工奖金

这题本质：

> 查员工姓名 + 奖金
> 只显示「奖金 < 1000 或 没有奖金」的人

👉 典型 **LEFT JOIN + 条件筛选**

------

#### 📌 表结构

**Employee**

| empId | name | supervisor | salary |

**Bonus**

| empId | bonus |

------

#### 📌 题目要求

输出：

| name | bonus |

条件：

- bonus < 1000
- 或者 bonus 是 NULL（没有奖金记录）

------

#### ✅ 标准写法

```sql
SELECT e.name, b.bonus
FROM Employee e
LEFT JOIN Bonus b
ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;
```

------

#### 🔎 思路拆解

##### 第一步：为什么 LEFT JOIN？

因为：

> 有些员工可能没有奖金记录

如果用 INNER JOIN：

- 没有奖金的人会被过滤掉 ❌

所以必须用：

```
LEFT JOIN
```

保留所有员工。

------

##### 第二步：筛选条件

```
b.bonus < 1000 OR b.bonus IS NULL
```

为什么要加 `IS NULL`？

因为：

- 没有奖金记录 → bonus 为 NULL
- NULL < 1000 是不会成立的
- 所以必须单独写 IS NULL

------

#### 🧠 这题模型

```
主表保留全部
+ 右表可能不存在
+ 要筛选右表条件
```

固定结构：

```sql
FROM 主表
LEFT JOIN 右表
ON 条件
WHERE 右表列 条件
   OR 右表列 IS NULL
```

------

#### ⚠ 一个容易错的写法

很多人会写：

```sql
WHERE b.bonus < 1000
```

这样会：

- 自动过滤 NULL
- 变成类似 INNER JOIN 的效果 ❌

------

#### 🎯 一句话记忆

看到：

> “没有也要显示”

直接反射：

```
LEFT JOIN
+ IS NULL
```

------

你现在已经刷到：

- 自连接
- LEFT JOIN 判空
- 分组 + 聚合

SQL50 只剩下一些 GROUP BY + HAVING 的组合了 😄

要不要我给你做个：

> SQL50 高频易错点总结清单





### 1280.学生们参加各科测试的次数 

这题是：

> 所有学生 × 所有科目
> 统计每个学生每个科目参加考试的次数

👉 典型 **笛卡尔积 + LEFT JOIN + GROUP BY**

---

#### 📌 表结构

**Students**

| student_id | student_name |

**Subjects**

| subject_name |

**Examinations**

| student_id | subject_name |

---

#### 📌 题目要求

输出：

| student_id | student_name | subject_name | attended_exams |

要求：

* 即使没参加考试，也要显示 0
* 所以必须保留“所有学生 × 所有科目”

---

#### ✅ 标准写法

```sql
SELECT s.student_id,
       s.student_name,
       sub.subject_name,
       COUNT(e.student_id) AS attended_exams
FROM Students s
CROSS JOIN Subjects sub
LEFT JOIN Examinations e
ON s.student_id = e.student_id
AND sub.subject_name = e.subject_name
GROUP BY s.student_id, s.student_name, sub.subject_name
ORDER BY s.student_id, sub.subject_name;
```

---

#### 🔎 思路拆解（非常重要）

##### 第一步：为什么用 CROSS JOIN？

因为题目要：

> 每个学生 × 每个科目

比如：

* 3 个学生
* 2 个科目

必须得到 6 行基础数据。

```
Students × Subjects
```

这叫 **笛卡尔积**。

---

##### 第二步：LEFT JOIN Examinations

```
LEFT JOIN Examinations e
```

作用：

* 如果参加过考试 → 能匹配
* 如果没参加 → NULL

---

##### 第三步：COUNT(e.student_id)

关键点来了：

```
COUNT(e.student_id)
```

为什么不写 `COUNT(*)`？

因为：

* COUNT(*) 会把 NULL 也算进去 ❌
* COUNT(列名) 不会统计 NULL ✅

所以：

* 有考试 → +1
* 没考试 → 0

---

##### 第四步：GROUP BY

必须按：

```
学生 + 科目
```

分组统计次数。

---

#### 🧠 这题考的核心模型

```
要保留所有组合
→ 先做 CROSS JOIN
→ 再 LEFT JOIN 统计
```

---

#### 🔥 高频套路总结

| 需求         | 用法          |
| ------------ | ------------- |
| 全部组合     | CROSS JOIN    |
| 可能没有记录 | LEFT JOIN     |
| 统计次数     | COUNT(列名)   |
| 没有记 0     | COUNT(非空列) |

---

#### 🎯 一句话记忆

看到：

> 即使没有也要显示
> 每个 A 对应每个 B

脑子立刻：

```sql
A
CROSS JOIN B
LEFT JOIN C
GROUP BY
```

---

这题是 SQL50 里比较“综合”的一题，你能刷到这里说明已经理解 JOIN 结构了 👍

要不要我给你做个：

> JOIN 类型对比 + 典型题对应表（精简版）





### 570.至少有5名直接下属的经理

这题本质：

> 统计每个经理有多少“直接下属”
> 人数 ≥ 5 的经理输出名字

👉 典型 **自连接 + GROUP BY + HAVING**

------

#### 📌 表结构

**Employee**

| id | name | department | managerId |

含义：

- managerId = 上级的 id
- 如果是 NULL → 没有上级（最高层）

------

#### 📌 题目要求

输出：

| name |

这些人必须：

> 至少有 5 个员工的 managerId = 他的 id

------

#### ✅ 标准写法（自连接）

```sql
SELECT e2.name
FROM Employee e1
JOIN Employee e2
ON e1.managerId = e2.id
GROUP BY e2.id, e2.name
HAVING COUNT(e1.id) >= 5;
```

------

#### 🔎 思路拆解

##### 第一步：为什么自连接？

因为：

- 下属在 Employee 表
- 经理也在 Employee 表
- 是同一张表

所以必须自连接。

------

##### 第二步：两个别名

```
e1 → 下属
e2 → 经理
```

连接条件：

```sql
e1.managerId = e2.id
```

意思：

> 下属的 managerId 等于 经理的 id

------

##### 第三步：分组统计

```sql
GROUP BY e2.id, e2.name
```

意思：

> 每个经理一组

------

##### 第四步：HAVING 过滤

```sql
HAVING COUNT(e1.id) >= 5
```

意思：

> 这组（这个经理）的下属数量 ≥ 5

⚠ 注意：

不能写在 WHERE 里，因为：

- WHERE 在分组前执行
- COUNT 是聚合函数
- 聚合之后必须用 HAVING

------

#### 🧠 这题固定模型

看到：

- “至少几个”
- “统计数量”
- “同一张表上下级”

脑子自动：

```
自连接
+ GROUP BY
+ HAVING COUNT >= n
```

------

#### 🚀 更简洁写法（不用真的连两次）

其实也可以这样写：

```sql
SELECT name
FROM Employee
WHERE id IN (
    SELECT managerId
    FROM Employee
    GROUP BY managerId
    HAVING COUNT(*) >= 5
);
```

逻辑：

1. 先找出“下属 ≥ 5 的 managerId”
2. 再查出这些 id 对应的 name

------

#### ⭐ 关键知识点

| 关键词     | 用法   |
| ---------- | ------ |
| 统计人数   | COUNT  |
| 分组过滤   | HAVING |
| 上下级结构 | 自连接 |

------

#### 一句话总结

```sql
自连接
GROUP BY 经理
HAVING COUNT(下属) >= 5
```

------

你现在已经进入 SQL50 的“聚合 + 结构题阶段”了 👍

要不要我给你讲一下：

> WHERE 和 HAVING 的执行顺序区别（这个非常关键）





### 1934.确认率

这题本质：

> 每个用户的确认率
> = confirmed 次数 / 请求总次数

👉 典型 **LEFT JOIN + GROUP BY + 条件统计**

------

#### 📌 表结构

**Signups**

| user_id | time_stamp |

**Confirmations**

| user_id | time_stamp | action |

其中：

- action = 'confirmed'
- action = 'timeout'

------

#### 📌 题目要求

输出：

| user_id | confirmation_rate |

规则：

- confirmation_rate = confirmed 次数 / 总请求次数
- 如果没有请求 → 结果为 0
- 保留 2 位小数

------

#### ✅ 标准写法

```sql
SELECT s.user_id,
       ROUND(
           IFNULL(
               SUM(c.action = 'confirmed') / COUNT(c.action),
               0
           ),
           2
       ) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```

------

#### 🔎 逻辑拆解

##### 第一步：LEFT JOIN

```sql
FROM Signups s
LEFT JOIN Confirmations c
```

为什么必须 LEFT JOIN？

因为：

> 有些用户可能一次确认都没有

要保留所有用户。

------

##### 第二步：分组

```sql
GROUP BY s.user_id
```

每个用户一组。

------

##### 第三步：分子（confirmed 次数）

```sql
SUM(c.action = 'confirmed')
```

这是个关键技巧。

在 MySQL 里：

```sql
c.action = 'confirmed'
```

会返回：

- true → 1
- false → 0

所以：

```sql
SUM(c.action = 'confirmed')
```

= confirmed 的数量。

------

##### 第四步：分母（总请求次数）

```sql
COUNT(c.action)
```

统计所有请求次数。

⚠ 注意：

COUNT(列名) 不统计 NULL。

如果用户没有确认记录：

COUNT = 0。

------

##### 第五步：防止除以 0

如果没有记录：

```sql
SUM(...) / COUNT(...)
```

会变成：

```id="s8l6mz"
0 / 0 → NULL
```

所以用：

```sql
IFNULL(..., 0)
```

把 NULL 变成 0。

------

##### 第六步：保留两位小数

```sql
ROUND(..., 2)
```

------

#### 🧠 这题固定模型

看到：

- 比率
- 成功次数 / 总次数
- 即使没有记录也要显示

脑子自动：

```sql
LEFT JOIN
GROUP BY
SUM(条件)
/
COUNT(列)
```

------

#### 🚀 更清晰写法（CASE 版本）

```sql
SELECT s.user_id,
       ROUND(
           IFNULL(
               SUM(CASE WHEN c.action = 'confirmed' THEN 1 ELSE 0 END)
               / COUNT(c.action),
               0
           ),
           2
       ) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id = c.user_id
GROUP BY s.user_id;
```

逻辑完全一样，只是写法更标准。

------

#### ⭐ 高频考点

| 技巧      | 作用               |
| --------- | ------------------ |
| SUM(条件) | 统计满足条件的数量 |
| COUNT(列) | 统计非 NULL 数     |
| LEFT JOIN | 保留所有用户       |
| IFNULL    | 防止除 0           |

------

#### 一句话总结

```sql
确认率 = confirmed次数 / 总次数
```

实现套路：

```sql
LEFT JOIN
GROUP BY
SUM(条件) / COUNT
ROUND
```

------

你现在已经进入 SQL50 的“统计比例型题目”阶段了 👍

要不要我给你整理一个：

> SQL50 高频聚合函数技巧清单









## 聚合函数（to be done）

### 620.有趣的电影 

这题其实**不需要聚合函数（如 COUNT、SUM、GROUP BY）**，主要是条件筛选 + 排序。

题目要求：

- `description = 'boring'` 的电影要排除 → 只要 `description != 'boring'`
- `id` 为奇数 → `id % 2 = 1`
- 按 `rating` 降序排列

------

#### ✅ 标准写法（MySQL）

```sql
SELECT id, movie, description, rating
FROM Cinema
WHERE description != 'boring'
  AND id % 2 = 1
ORDER BY rating DESC;
```

------

#### 🔎 逻辑解释

##### 1️⃣ 过滤 boring 电影

```sql
description != 'boring'
```

只保留有趣的电影。

------

##### 2️⃣ 只要奇数 id

```sql
id % 2 = 1
```

取模运算：

- 5 % 2 = 1 ✅
- 6 % 2 = 0 ❌

------

##### 3️⃣ 按评分降序

```sql
ORDER BY rating DESC
```

评分高的排前面。

------

##### ❓ 为什么不用聚合函数？

因为题目：

- 没有要求分组
- 没有要求统计数量
- 没有求和或平均值

所以 **GROUP BY 完全不需要**。

------

#### 🎯 一句话总结

> 本题核心 = WHERE 条件筛选 + ORDER BY 排序
> 不涉及聚合函数。

------

如果你愿意，我可以顺便讲讲：

- `%` 在不同数据库里的写法区别
- 或者如果题目要求“统计有趣电影数量”该怎么改成聚合版本





### 1251.平均售价

目标：
计算每个产品的 **平均售价**，即总销售额 ÷ 总销售数量。

公式核心：

```sql
平均售价 = SUM(price * units) / SUM(units)
```

------

#### 表结构理解

**Prices**

| product_id | start_date | end_date | price |

表示某时间段的价格。

**UnitsSold**

| product_id | purchase_date | units |

表示某天卖出的数量。

⚠ 注意：`purchase_date` 必须在价格区间内，才能用对应价格计算。

------

#### SQL 写法

```sql
SELECT 
    p.product_id,
    IFNULL(ROUND(SUM(p.price * u.units) / SUM(u.units), 2), 0) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u
    ON p.product_id = u.product_id
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;
```

------

#### 逻辑拆解

##### 连接条件

```sql
u.purchase_date BETWEEN p.start_date AND p.end_date
```

确保使用正确时间区间的价格。

##### 总销售额

```sql
SUM(p.price * u.units)
```

每次卖出数量 × 当时价格，再累加。

##### 总销售数量

```sql
SUM(u.units)
```

##### 求平均售价

```sql
SUM(p.price * u.units) / SUM(u.units)
```

##### LEFT JOIN 和 IFNULL

- **LEFT JOIN** 保证有价格但没卖出记录的产品也能显示
- **IFNULL(..., 0)** 处理无销售量情况，返回 0

------

#### 执行顺序

1. `FROM Prices`
2. `LEFT JOIN UnitsSold` + 连接条件
3. `GROUP BY product_id`
4. 聚合函数计算总销售额和总销售数量
5. 计算平均售价

------

如果你需要，我可以顺便画一个小表格示例，把 **价格区间 + 销售数量 + 平均售价** 可视化，让聚合函数计算过程更直观。

你想让我画吗？



### 1075.项目员工 I

目标：
统计每个项目中员工人数，并返回 **project_id** 以及 **员工数量**，只显示至少有一名员工的项目。

这题是**典型聚合函数 + 分组**题。

------

#### 表结构理解

**Project**

| project_id | employee_id |

- 每条记录表示某个员工参与了某个项目。

------

#### SQL 写法

```sql
SELECT 
    project_id,
    COUNT(employee_id) AS num_employees
FROM Project
GROUP BY project_id;
```

------

#### 逻辑拆解

##### 聚合函数 COUNT

```sql
COUNT(employee_id)
```

- 统计每个项目参与的员工数量
- 聚合函数把同一个 `project_id` 的多条记录“压缩”为一个数量值

##### 分组

```sql
GROUP BY project_id
```

- 按 `project_id` 分组
- 每组计算一个 `COUNT(employee_id)`

------

#### 执行顺序

1. `FROM Project` 读取表数据
2. `GROUP BY project_id` 按项目分组
3. `COUNT(employee_id)` 统计每组员工数
4. `SELECT` 返回项目 ID 和员工数量

------

#### 小结

> 本题聚合函数的作用是**统计每个项目员工的总数**，`COUNT` 是最直接的聚合函数用法。

如果你想，我可以顺便画一个小表，把**每个项目对应的员工列表 → COUNT → 最终结果** 可视化，更直观理解聚合函数的效果。

你想让我画吗？



### 1633.各赛事的用户注册率

目标：
统计每个赛事的 **用户注册百分率** = 已注册人数 ÷ 总用户数 × 100，并保留两位小数。
按百分比降序排列，如果相同则按 `contest_id` 升序排列。

------

#### 表结构理解

**Users**

| user_id | user_name |

- 用户表，`user_id` 唯一

**Register**

| contest_id | user_id |

- 注册表，记录某用户注册了哪些比赛

------

#### SQL 写法

```sql
SELECT 
    r.contest_id,
    ROUND(COUNT(r.user_id) * 100.0 / (SELECT COUNT(*) FROM Users), 2) AS percentage
FROM Register r
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;
```

------

#### 逻辑拆解

##### 聚合函数 COUNT

```sql
COUNT(r.user_id)
```

- 统计每个比赛的注册人数

##### 总用户数

```sql
(SELECT COUNT(*) FROM Users)
```

- 计算 Users 表的总用户数

##### 百分比计算

```sql
COUNT(r.user_id) * 100.0 / (SELECT COUNT(*) FROM Users)
```

- 已注册人数 ÷ 总用户数 × 100
- `ROUND(..., 2)` 保留两位小数

##### 分组

```sql
GROUP BY r.contest_id
```

- 按比赛 ID 分组，统计每个比赛的注册人数

##### 排序

```sql
ORDER BY percentage DESC, r.contest_id ASC
```

- 百分比高的排前面，如果相同按 `contest_id` 升序

------

#### 执行顺序

1. `FROM Register` 读取注册表
2. `GROUP BY contest_id` 对每场比赛分组
3. `COUNT(user_id)` 统计每组注册人数
4. 用总用户数计算百分比
5. `ORDER BY` 返回排序结果

------

#### 小结

> 聚合函数在本题中体现为：
>
> - **COUNT(user_id)** → 每场比赛已注册用户数
> - **SELECT COUNT(\*) FROM Users** → 总用户数（也可以理解为常量）
> - 聚合函数配合分组，计算每场比赛的注册百分率

------

如果你愿意，我可以画一个小表，把每场比赛的注册用户 → COUNT → 百分比 → 排序 可视化，这样聚合函数作用更直观。

你希望我画吗？





## 排序和分组











## 高级查询和连接











## 子查询













## 高级字符串函数 / 正则表达式 / 子句















s





