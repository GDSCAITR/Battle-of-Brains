# 🪞 The Kingdom of Mirrors

## 🧩 Problem Statement

You are given a string `S`.

You must partition it into substrings such that:

- Every substring is a **palindrome**
- You want to minimize the number of **cuts**

---

## 📥 Input Format

- A single string `S`

---

## 📌 Constraints

- `1 ≤ length(S) ≤ 12`

---

## 📤 Output Format

- Print minimum number of cuts required

---

## 🧠 Approach (DP + Palindrome Check)

### Goal:
Minimize number of cuts

---

### Step 1: Define DP

Let:
```
dp[i] = minimum cuts needed for substring S[0...i]
```

---

### Step 2: Transition

For each `i`, try all possible partitions:

If substring `S[j...i]` is a palindrome:

```
dp[i] = min(dp[i], dp[j-1] + 1)
```

Special case:
- If `j == 0` → no cut needed → `dp[i] = 0`

---

### Step 3: Palindrome Check

A string is palindrome if:
```
s[l] == s[r] while moving inward
```

---

## 🔍 Dry Run

### Input
```
abcb
```

### Partitions
```
a | bcb → valid (1 cut)
```

### Output
```
1
```

---

## ⏱️ Complexity

- Time: `O(n^3)` (palindrome check inside loops)
- Space: `O(n)`

Since `n ≤ 12`, this is fine.

---

## 💻 Code Implementations

### 🟦 Python
```python
s = input().strip()
n = len(s)

def is_pal(l, r):
    while l < r:
        if s[l] != s[r]:
            return False
        l += 1
        r -= 1
    return True

dp = [0] * n

for i in range(n):
    dp[i] = i  # worst case: all cuts

    for j in range(i + 1):
        if is_pal(j, i):
            if j == 0:
                dp[i] = 0
            else:
                dp[i] = min(dp[i], dp[j - 1] + 1)

print(dp[n - 1])
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {

    static boolean isPal(String s, int l, int r) {
        while (l < r) {
            if (s.charAt(l) != s.charAt(r)) return false;
            l++;
            r--;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        int n = s.length();

        int[] dp = new int[n];

        for (int i = 0; i < n; i++) {
            dp[i] = i;

            for (int j = 0; j <= i; j++) {
                if (isPal(s, j, i)) {
                    if (j == 0) dp[i] = 0;
                    else dp[i] = Math.min(dp[i], dp[j - 1] + 1);
                }
            }
        }

        System.out.println(dp[n - 1]);
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
using namespace std;

bool isPal(string &s, int l, int r) {
    while (l < r) {
        if (s[l] != s[r]) return false;
        l++;
        r--;
    }
    return true;
}

int main() {
    string s;
    cin >> s;
    int n = s.size();

    int dp[n];

    for (int i = 0; i < n; i++) {
        dp[i] = i;

        for (int j = 0; j <= i; j++) {
            if (isPal(s, j, i)) {
                if (j == 0) dp[i] = 0;
                else dp[i] = min(dp[i], dp[j - 1] + 1);
            }
        }
    }

    cout << dp[n - 1];
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Not checking all partitions
- Forgetting base case (`j == 0`)
- Recomputing palindrome inefficiently (fine here due to small n)
- Confusing number of partitions vs number of cuts

---

## 💡 Takeaway

Whenever:
- "minimum cuts"
- "partition string"
- "palindrome constraint"

👉 Think **DP on partitions**