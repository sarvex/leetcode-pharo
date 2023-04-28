# [389. Find the Difference](https://leetcode.com/problems/find-the-difference)

[中文文档](/solution/0300-0399/0389.Find%20the%20Difference/README.md)

## Description

<p>You are given two strings <code>s</code> and <code>t</code>.</p>

<p>String <code>t</code> is generated by random shuffling string <code>s</code> and then add one more letter at a random position.</p>

<p>Return the letter that was added to <code>t</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;abcd&quot;, t = &quot;abcde&quot;
<strong>Output:</strong> &quot;e&quot;
<strong>Explanation:</strong> &#39;e&#39; is the letter that was added.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;&quot;, t = &quot;y&quot;
<strong>Output:</strong> &quot;y&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 1000</code></li>
	<li><code>t.length == s.length + 1</code></li>
	<li><code>s</code> and <code>t</code> consist of lowercase English letters.</li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        cnt = Counter(s)
        for c in t:
            cnt[c] -= 1
            if cnt[c] < 0:
                return c
```

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        a = sum(ord(c) for c in s)
        b = sum(ord(c) for c in t)
        return chr(b - a)
```

### **Java**

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int[] cnt = new int[26];
        for (int i = 0; i < s.length(); ++i) {
            ++cnt[s.charAt(i) - 'a'];
        }
        for (int i = 0; ; ++i) {
            if (--cnt[t.charAt(i) - 'a'] < 0) {
                return t.charAt(i);
            }
        }
    }
}
```

```java
class Solution {
    public char findTheDifference(String s, String t) {
        int ss = 0;
        for (int i = 0; i < t.length(); ++i) {
            ss += t.charAt(i);
        }
        for (int i = 0; i < s.length(); ++i) {
            ss -= s.charAt(i);
        }
        return (char) ss;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    char findTheDifference(string s, string t) {
        int cnt[26] = {0};
        for (char& c : s) ++cnt[c - 'a'];
        for (char& c : t) if (--cnt[c - 'a'] < 0) return c;
        return ' ';
    }
};
```

```cpp
class Solution {
public:
    char findTheDifference(string s, string t) {
        int a = 0, b = 0;
        for (char& c : s) a += c;
        for (char& c : t) b += c;
        return b - a;
    }
};
```

### **TypeScript**

```ts
function findTheDifference(s: string, t: string): string {
    const n = s.length;
    const count = new Array(26).fill(0);
    for (let i = 0; i < n; i++) {
        count[s.charCodeAt(i) - 'a'.charCodeAt(0)]++;
        count[t.charCodeAt(i) - 'a'.charCodeAt(0)]--;
    }
    count[t.charCodeAt(n) - 'a'.charCodeAt(0)]--;
    return String.fromCharCode(
        'a'.charCodeAt(0) + count.findIndex(v => v !== 0),
    );
}
```

```ts
function findTheDifference(s: string, t: string): string {
    return String.fromCharCode(
        [...t].reduce((r, v) => r + v.charCodeAt(0), 0) -
            [...s].reduce((r, v) => r + v.charCodeAt(0), 0),
    );
}
```

### **Rust**

```rust
impl Solution {
    pub fn find_the_difference(s: String, t: String) -> char {
        let s = s.as_bytes();
        let t = t.as_bytes();
        let n = s.len();
        let mut count = [0; 26];
        for i in 0..n {
            count[(s[i] - b'a') as usize] += 1;
            count[(t[i] - b'a') as usize] -= 1;
        }
        count[(t[n] - b'a') as usize] -= 1;
        char::from(b'a' + count.iter().position(|&v| v != 0).unwrap() as u8)
    }
}
```

```rust
impl Solution {
    pub fn find_the_difference(s: String, t: String) -> char {
        let mut ans = 0;
        for c in s.as_bytes() {
            ans ^= c;
        }
        for c in t.as_bytes() {
            ans ^= c;
        }
        char::from(ans)
    }
}
```

### **C**

```c
char findTheDifference(char *s, char *t) {
    int n = strlen(s);
    int count[26] = {0};
    for (int i = 0; i < n; i++) {
        count[s[i] - 'a']++;
        count[t[i] - 'a']--;
    }
    count[t[n] - 'a']--;
    int i;
    for (i = 0; i < 26; i++) {
        if (count[i]) {
            break;
        }
    }
    return 'a' + i;
}
```

```c
char findTheDifference(char *s, char *t) {
    int n = strlen(s);
    char ans = 0;
    for (int i = 0; i < n; i++) {
        ans ^= s[i];
        ans ^= t[i];
    }
    ans ^= t[n];
    return ans;
}
```

### **Go**

```go
func findTheDifference(s, t string) byte {
	cnt := [26]int{}
	for _, ch := range s {
		cnt[ch-'a']++
	}
	for i := 0; ; i++ {
		ch := t[i]
		cnt[ch-'a']--
		if cnt[ch-'a'] < 0 {
			return ch
		}
	}
}
```

```go
func findTheDifference(s string, t string) byte {
	ss := 0
	for _, c := range s {
		ss -= int(c)
	}
	for _, c := range t {
		ss += int(c)
	}
	return byte(ss)
}
```

### **...**

```

```

<!-- tabs:end -->