# [2729. Check if The Number is Fascinating](https://leetcode.com/problems/check-if-the-number-is-fascinating)

[中文文档](/solution/2700-2799/2729.Check%20if%20The%20Number%20is%20Fascinating/README.md)

## Description

<p>You are given an integer <code>n</code> that consists of exactly <code>3</code> digits.</p>

<p>We call the number <code>n</code> <strong>fascinating</strong> if, after the following modification, the resulting number contains all the digits from <code>1</code> to <code>9</code> <strong>exactly</strong> once and does not contain any <code>0</code>&#39;s:</p>

<ul>
	<li><strong>Concatenate</strong> <code>n</code> with the numbers <code>2 * n</code> and <code>3 * n</code>.</li>
</ul>

<p>Return <code>true</code><em> if </em><code>n</code><em> is fascinating, or </em><code>false</code><em> otherwise</em>.</p>

<p><strong>Concatenating</strong> two numbers means joining them together. For example, the concatenation of <code>121</code> and <code>371</code> is <code>121371</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 192
<strong>Output:</strong> true
<strong>Explanation:</strong> We concatenate the numbers n = 192 and 2 * n = 384 and 3 * n = 576. The resulting number is 192384576. This number contains all the digits from 1 to 9 exactly once.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 100
<strong>Output:</strong> false
<strong>Explanation:</strong> We concatenate the numbers n = 100 and 2 * n = 200 and 3 * n = 300. The resulting number is 100200300. This number does not satisfy any of the conditions.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>100 &lt;= n &lt;= 999</code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def isFascinating(self, n: int) -> bool:
        s = str(n) + str(2 * n) + str(3 * n)
        return "".join(sorted(s)) == "123456789"
```

### **Java**

```java
class Solution {
    public boolean isFascinating(int n) {
        String s = "" + n + (2 * n) + (3 * n);
        int[] cnt = new int[10];
        for (char c : s.toCharArray()) {
            if (++cnt[c - '0'] > 1) {
                return false;
            }
        }
        return cnt[0] == 0 && s.length() == 9;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    bool isFascinating(int n) {
        string s = to_string(n) + to_string(n * 2) + to_string(n * 3);
        sort(s.begin(), s.end());
        return s == "123456789";
    }
};
```

### **Go**

```go
func isFascinating(n int) bool {
	s := strconv.Itoa(n) + strconv.Itoa(n*2) + strconv.Itoa(n*3)
	cnt := [10]int{}
	for _, c := range s {
		cnt[c-'0']++
		if cnt[c-'0'] > 1 {
			return false
		}
	}
	return cnt[0] == 0 && len(s) == 9
}
```

### **TypeScript**

```ts
function isFascinating(n: number): boolean {
    const s = `${n}${n * 2}${n * 3}`;
    return s.split('').sort().join('') === '123456789';
}
```

### **...**

```

```

<!-- tabs:end -->
