# [1831. 每天的最大交易](https://leetcode.cn/problems/maximum-transaction-each-day)

[English Version](/solution/1800-1899/1831.Maximum%20Transaction%20Each%20Day/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>表: <code>Transactions</code></p>

<pre>
+----------------+----------+
| Column Name    | Type     |
+----------------+----------+
| transaction_id | int      |
| day            | datetime |
| amount         | int      |
+----------------+----------+
transaction_id 是此表的主键。
每行包括了该次交易的信息。
</pre>

<p> </p>

<p>写一条 SQL 返回每天交易金额 <code>amount</code> 最大的交易 ID 。如果某天有多个这样的交易，返回这些交易的 ID 。</p>

<p><span style="">返回结果根据 </span><code>transaction_id</code> 升序排列。</p>

<p>查询结果样例如下：</p>

<p> </p>

<pre>
Transactions table:
+----------------+--------------------+--------+
| transaction_id | day                | amount |
+----------------+--------------------+--------+
| 8              | 2021-4-3 15:57:28  | 57     |
| 9              | 2021-4-28 08:47:25 | 21     |
| 1              | 2021-4-29 13:28:30 | 58     |
| 5              | 2021-4-28 16:39:59 | 40     |
| 6              | 2021-4-29 23:39:28 | 58     |
+----------------+--------------------+--------+

Result table:
+----------------+
| transaction_id |
+----------------+
| 1              |
| 5              |
| 6              |
| 8              |
+----------------+
"2021-4-3"  --> 有一个 id 是 8 的交易，因此，把它加入结果表。 
"2021-4-28" --> 有两个交易，id 是 5 和 9 ，交易 5 的金额是 40 ，而交易 9 的数量是 21 。只需要将交易 5 加入结果表，因为它是当天金额最大的交易。
"2021-4-29" --> 有两个交易，id 是 1 和 6 ，这两个交易的金额都是 58 ，因此需要把它们都写入结果表。
最后，把交易 id 按照升序排列。</pre>

<p> </p>

<p><strong>进阶：</strong>你可以不使用 <code>MAX()</code> 函数解决这道题目吗?</p>

## 解法

<!-- 这里可写通用的实现逻辑 -->

<!-- tabs:start -->

### **SQL**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```sql
# Write your MySQL query statement below
select
    transaction_id
from
    (
        select
            transaction_id,
            rank() over(
                partition by date_format(day, '%Y-%m-%d')
                order by
                    amount desc
            ) rk
        from
            Transactions
        order by
            transaction_id
    ) t
where
    rk = 1
```

<!-- tabs:end -->
