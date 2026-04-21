# 🌊 The Wavefront Scheduling

## 🧩 Problem Statement

You are given a **jagged array** (rows can have different lengths).

Each element at position `(i, j)` belongs to a **wave** defined by:

```
i + j = constant
```

### Processing Rules:

1. Waves are processed in **increasing order of (i + j)**
2. Within each wave, elements are processed in:
   - **decreasing order of row index (i)**

---

## 📥 Input Format

- First line: integer `N` (number of rows)
- Next `N` lines:
  - First value: `Kᵢ` (number of elements in row)
  - Followed by `Kᵢ` integers

---

## 📌 Constraints

- `1 ≤ N ≤ 10^5`
- Total elements ≤ `10^5`
- `1 ≤ values ≤ 10^9`

---

## 📤 Output Format

- Print all elements in required wave order

---

## 🧠 Approach

### Step 1: Traverse all elements

For each element:
- Compute `wave = i + j`
- Store `(i, value)` in a map:
```
wave_map[wave].append((i, value))
```

---

### Step 2: Process waves

- Iterate waves in **increasing order**
- For each wave:
  - Sort elements by **row index decreasing (i descending)**
  - Append values to result

---

## 🔍 Key Insight

We are grouping elements by diagonals (`i + j`), and within each diagonal:
👉 bottom-to-top traversal

---

## ⏱️ Complexity

- Time: `O(N log N)` (due to sorting per wave)
- Space: `O(N)`

---

## 💻 Code Implementations

### 🟦 Python
```python
n = int(input())

wave_map = {}

for i in range(n):
    row = list(map(int, input().split()))
    k = row[0]
    values = row[1:]

    for j in range(k):
        wave = i + j
        if wave not in wave_map:
            wave_map[wave] = []
        wave_map[wave].append((i, values[j]))

result = []

for wave in sorted(wave_map.keys()):
    # sort by row index decreasing
    wave_map[wave].sort(reverse=True)
    for _, val in wave_map[wave]:
        result.append(val)

print(*result)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        Map<Integer, List<int[]>> map = new HashMap<>();

        for (int i = 0; i < n; i++) {
            int k = sc.nextInt();
            for (int j = 0; j < k; j++) {
                int val = sc.nextInt();
                int wave = i + j;

                map.putIfAbsent(wave, new ArrayList<>());
                map.get(wave).add(new int[]{i, val});
            }
        }

        List<Integer> result = new ArrayList<>();

        List<Integer> keys = new ArrayList<>(map.keySet());
        Collections.sort(keys);

        for (int key : keys) {
            List<int[]> list = map.get(key);

            list.sort((a, b) -> b[0] - a[0]); // descending i

            for (int[] pair : list) {
                result.add(pair[1]);
            }
        }

        for (int x : result) {
            System.out.print(x + " ");
        }
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
#include <vector>
#include <map>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cin >> n;

    map<int, vector<pair<int,int>>> mp;

    for (int i = 0; i < n; i++) {
        int k;
        cin >> k;
        for (int j = 0; j < k; j++) {
            int val;
            cin >> val;
            int wave = i + j;

            mp[wave].push_back({i, val});
        }
    }

    vector<int> result;

    for (auto &entry : mp) {
        auto &vec = entry.second;

        sort(vec.begin(), vec.end(), [](auto &a, auto &b) {
            return a.first > b.first; // descending i
        });

        for (auto &p : vec) {
            result.push_back(p.second);
        }
    }

    for (int x : result) cout << x << " ";
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Sorting by value instead of row index ❌
- Ignoring jagged structure (assuming rectangular matrix)
- Forgetting `i + j` grouping
- Using brute force traversal without grouping

---

## 💡 Takeaway

Whenever you see:
- Diagonal traversal
- Condition like `i + j = constant`

👉 Think **grouping + ordering inside group**