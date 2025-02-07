# [1709. 访问日期之间最大的空档期](https://leetcode.cn/problems/biggest-window-between-visits)

[English Version](/solution/1700-1799/1709.Biggest%20Window%20Between%20Visits/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>表： <code>UserVisits</code></p>

<pre>+-------------+------+
| Column Name | Type |
+-------------+------+
| user_id     | int  |
| visit_date  | date |
+-------------+------+
该表没有主键。
该表包含用户访问某特定零售商的日期日志。</pre>

<p> </p>

<p>假设今天的日期是 <code>'2021-1-1'</code> 。</p>

<p>编写 SQL 语句，对于每个 <code>user_id</code> ，求出每次访问及其下一个访问（若该次访问是最后一次，则为今天）之间最大的空档期天数 <code>window</code> 。</p>

<p>返回结果表，按用户编号 <code>user_id</code> 排序。</p>

<p>查询格式如下示例所示：</p>

<p> </p>

<pre>UserVisits 表：
+---------+------------+
| user_id | visit_date |
+---------+------------+
| 1       | 2020-11-28 |
| 1       | 2020-10-20 |
| 1       | 2020-12-3  |
| 2       | 2020-10-5  |
| 2       | 2020-12-9  |
| 3       | 2020-11-11 |
+---------+------------+
结果表：
+---------+---------------+
| user_id | biggest_window|
+---------+---------------+
| 1       | 39            |
| 2       | 65            |
| 3       | 51            |
+---------+---------------+
对于第一个用户，问题中的空档期在以下日期之间：
    - 2020-10-20 至 2020-11-28 ，共计 39 天。
    - 2020-11-28 至 2020-12-3 ，共计 5 天。
    - 2020-12-3 至 2021-1-1 ，共计 29 天。
由此得出，最大的空档期为 39 天。
对于第二个用户，问题中的空档期在以下日期之间：
    - 2020-10-5 至 2020-12-9 ，共计 65 天。
    - 2020-12-9 至 2021-1-1 ，共计 23 天。
由此得出，最大的空档期为 65 天。
对于第三个用户，问题中的唯一空档期在 2020-11-11 至 2021-1-1 之间，共计 51 天。</pre>

## 解法

<!-- 这里可写通用的实现逻辑 -->

<!-- tabs:start -->

### **SQL**

```sql
# Write your MySQL query statement below
select
    user_id,
    max(datediff(nxt_day, visit_date)) as biggest_window
from
    (
        select
            user_id,
            visit_date,
            lead(visit_date, 1, '2021-1-1') over (
                partition by user_id
                order by
                    visit_date
            ) as nxt_day
        from
            UserVisits
    ) t
group by
    user_id
order by
    user_id;
```

<!-- tabs:end -->
