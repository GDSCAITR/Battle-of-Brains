# 🏁 The Circular Rally

## 🧩 Problem Statement

You are given:

- `gas[i]` → fuel available at checkpoint `i`
- `cost[i]` → fuel required to travel from `i` to `i+1`

You can start from any checkpoint with an empty tank.

### Goal:
Find the **starting index** from which you can complete the full circular route without fuel going negative.

If impossible → return `-1`

---

## 📥 Input Format

- First line: integer `N`
- Second line: `N` integers → `gas[]`
- Third line: `N` integers → `cost[]`

---

## 📌 Constraints

- `1 ≤ N ≤ 100,000`
- `0 ≤ gas[i], cost[i] ≤ 10,000`

---

## 📤 Output Format

- Print starting index or `-1`

---

## 🧠 Approach (Greedy)

### Step 1: Check feasibility

If:
```
sum(gas) < sum(cost)
```
→ Impossible → return `-1`

---

### Step 2: Find starting point

Traverse once:

- Maintain:
  - `tank` → current fuel
  - `start` → candidate starting index

### Logic:

For each index `i`:
```
tank += gas[i] - cost[i]
```

If `tank < 0`:
- Current start is invalid
- Move start to `i + 1`
- Reset tank = 0

---

## 🔍 Key Insight

If you fail at index `i`,  
then **any index between previous start and i also fails**.

So we skip them all in one step.

---

## 🔍 Dry Run

### Input
```
gas  = [1,2,3,4,5]
cost = [3,4,5,1,2]
```

### Steps
```
i=0 → tank = -2 → reset start = 1
i=1 → tank = -2 → reset start = 2
i=2 → tank = -2 → reset start = 3
i=3 → tank = 3
i=4 → tank = 6
```

### Output
```
3
```

---

## ⏱️ Complexity

- Time: `O(N)`
- Space: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python
```python
n = int(input())
gas = list(map(int, input().split()))
cost = list(map(int, input().split()))

if sum(gas) < sum(cost):
    print(-1)
else:
    start = 0
    tank = 0

    for i in range(n):
        tank += gas[i] - cost[i]

        if tank < 0:
            start = i + 1
            tank = 0

    print(start)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] gas = new int[n];
        int[] cost = new int[n];

        int totalGas = 0, totalCost = 0;

        for (int i = 0; i < n; i++) {
            gas[i] = sc.nextInt();
            totalGas += gas[i];
        }

        for (int i = 0; i < n; i++) {
            cost[i] = sc.nextInt();
            totalCost += cost[i];
        }

        if (totalGas < totalCost) {
            System.out.println(-1);
            return;
        }

        int start = 0, tank = 0;

        for (int i = 0; i < n; i++) {
            tank += gas[i] - cost[i];

            if (tank < 0) {
                start = i + 1;
                tank = 0;
            }
        }

        System.out.println(start);
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
    int n;
    cin >> n;

    vector<int> gas(n), cost(n);

    int totalGas = 0, totalCost = 0;

    for (int i = 0; i < n; i++) {
        cin >> gas[i];
        totalGas += gas[i];
    }

    for (int i = 0; i < n; i++) {
        cin >> cost[i];
        totalCost += cost[i];
    }

    if (totalGas < totalCost) {
        cout << -1;
        return 0;
    }

    int start = 0, tank = 0;

    for (int i = 0; i < n; i++) {
        tank += gas[i] - cost[i];

        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }

    cout << start;
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Trying all starting points → `O(n²)` ❌
- Skipping total gas check
- Not resetting tank properly
- Thinking multiple answers exist (problem guarantees unique)

---

## 💡 Takeaway

Whenever:
- Circular array
- Feasibility + optimal start

👉 Think **Greedy + Single Pass**