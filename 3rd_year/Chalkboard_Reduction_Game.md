# 🧮 Chalkboard Reduction Game

## 🧩 Problem Statement

Two players, **Aarya** and **Bhavesh**, play a game on a number `n`.

### Rules:

- Aarya starts first
- On each turn, a player chooses a number `x` such that:
  - `0 < x < n`
  - `x` divides `n`
- Then update:
```
n = n - x
```

### Losing Condition:
- If a player cannot make a move → they lose

---

## 📥 Input Format

- First line: integer `t` (number of test cases)
- Next `t` lines: integer `n`

---

## 📌 Constraints

- `1 ≤ t ≤ 10^5`
- `1 ≤ n ≤ 10^9`

---

## 📤 Output Format

- Print `"true"` if Aarya wins
- Print `"false"` otherwise

---

## 🧠 Approach (Key Insight)

This problem reduces to a simple observation:

### Pattern:
- If `n` is **even** → Aarya wins
- If `n` is **odd** → Aarya loses

---

## 🔍 Why?

### Case 1: n = even
- Aarya can always subtract `1` (since 1 divides every number)
- This makes `n` → odd for Bhavesh
- Eventually forces Bhavesh into `n = 1` → no moves → loses

---

### Case 2: n = odd
- Any divisor of an odd number is also odd
- Subtracting odd → result becomes even
- So Aarya always gives an advantage to Bhavesh

---

## 🔍 Dry Run

### Input
```
n = 2
```
Even → Aarya wins → `true`

---

### Input
```
n = 3
```
Odd → Aarya loses → `false`

---

### Input
```
n = 1
```
No moves → Aarya loses → `false`

---

## ⏱️ Complexity

- Time: `O(1)` per test case
- Space: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python
```python
t = int(input())

for _ in range(t):
    n = int(input())
    if n % 2 == 0:
        print("true")
    else:
        print("false")
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();

        while (t-- > 0) {
            int n = sc.nextInt();
            if (n % 2 == 0)
                System.out.println("true");
            else
                System.out.println("false");
        }
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
using namespace std;

int main() {
    int t;
    cin >> t;

    while (t--) {
        int n;
        cin >> n;

        if (n % 2 == 0)
            cout << "true\n";
        else
            cout << "false\n";
    }

    return 0;
}
```

---

## ⚠️ Common Mistakes

- Trying recursion / DP (TLE for large constraints)
- Overthinking divisor choices
- Not spotting the even/odd pattern

---

## 💡 Takeaway

Whenever:
- Turn-based game
- Optimal play
- Simple operations

👉 Look for **pattern / parity (even-odd)** before brute force