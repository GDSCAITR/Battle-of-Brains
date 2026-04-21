# 📡 Signal Recovery Window

## 🧩 Problem Statement

You are given a binary array representing a signal stream:

- `1` → stable unit  
- `0` → unstable unit  

You can change **at most `k` zeros into ones**.

Your goal is to find the **maximum length of a contiguous subarray** consisting only of `1`s after at most `k` changes.

---

## 📥 Input Format

- First line: two integers `n` and `k`
- Second line: `n` space-separated integers (0 or 1)

---

## 📌 Constraints

- `1 ≤ n ≤ 10^5`
- `0 ≤ k ≤ n`

---

## 📤 Output Format

- Print the maximum length of valid subarray

---

## 🧠 Approach (Sliding Window)

We use a **two-pointer / sliding window** technique.

### Idea:
Maintain a window where:
- Number of zeros ≤ `k`

### Steps:

1. Initialize:
   - `left = 0`
   - `zero_count = 0`
   - `max_len = 0`

2. Move `right` pointer:
   - If `arr[right] == 0` → increment `zero_count`

3. If `zero_count > k`:
   - Shrink window from left
   - If `arr[left] == 0` → decrement `zero_count`
   - Move `left++`

4. Update:
```
max_len = max(max_len, right - left + 1)
```

---

## 🔍 Dry Run

### Input
```
1 0 0 1 1 0 1, k = 2
```

### Window Expansion
```
Best window → [1 0 0 1 1] → flip 2 zeros → length = 5
```

---

## ⏱️ Complexity

- Time: `O(n)`
- Space: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python
```python
n, k = map(int, input().split())
arr = list(map(int, input().split()))

left = 0
zero_count = 0
max_len = 0

for right in range(n):
    if arr[right] == 0:
        zero_count += 1

    while zero_count > k:
        if arr[left] == 0:
            zero_count -= 1
        left += 1

    max_len = max(max_len, right - left + 1)

print(max_len)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int k = sc.nextInt();

        int[] arr = new int[n];
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();

        int left = 0, zeroCount = 0, maxLen = 0;

        for (int right = 0; right < n; right++) {
            if (arr[right] == 0) zeroCount++;

            while (zeroCount > k) {
                if (arr[left] == 0) zeroCount--;
                left++;
            }

            maxLen = Math.max(maxLen, right - left + 1);
        }

        System.out.println(maxLen);
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
#include <vector>
using namespace std;

int main() {
    int n, k;
    cin >> n >> k;

    vector<int> arr(n);
    for (int i = 0; i < n; i++) cin >> arr[i];

    int left = 0, zeroCount = 0, maxLen = 0;

    for (int right = 0; right < n; right++) {
        if (arr[right] == 0) zeroCount++;

        while (zeroCount > k) {
            if (arr[left] == 0) zeroCount--;
            left++;
        }

        maxLen = max(maxLen, right - left + 1);
    }

    cout << maxLen;
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Using brute force (checking all subarrays) → `O(n²)` ❌
- Not shrinking window when zeros exceed `k`
- Forgetting to update max length correctly
- Miscounting zeros

---

## 💡 Takeaway

Whenever you see:
- "longest subarray"
- "at most k changes"

👉 Think **Sliding Window immediately**