







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



