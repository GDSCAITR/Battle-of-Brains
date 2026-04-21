# 🚦 Signal State Decoder

## 🧩 Problem Statement

A smart traffic control system uses a countdown timer (in seconds) to determine the# 🔍 The Missing ID

## 🧩 Problem Statement

During a university tech fest, every participant is assigned an ID number. Each ID is recorded exactly twice — once at entry and once at exit.

However, due to a system glitch, one participant’s ID was recorded only once.

You are given a list `nums` containing all recorded IDs.

Your task is to find the ID that appears only once.

---

## 📥 Input Format

- First line: Integer `N` (number of IDs)
- Second line: `N` space-separated integers

---

## 📌 Constraints

- `1 <= N <= 3 * 10^4`
- `-3 * 10^4 <= nums[i] <= 3 * 10^4`
- Every element appears twice except one

---

## 📤 Output Format

- Print the integer that appears only once

---

## 🧠 Approach (Key Insight)

We use the **XOR (^) operation**.

### Properties of XOR:
- `a ^ a = 0`
- `a ^ 0 = a`
- XOR is commutative and associative

### Idea:
If we XOR all numbers:
- Duplicate numbers cancel out
- Only the unique number remains

---

## 🔍 Dry Run

### Input
```
4 1 2 1 2
```

### Steps
```
result = 0
result = 0 ^ 4 = 4
result = 4 ^ 1 = 5
result = 5 ^ 2 = 7
result = 7 ^ 1 = 6
result = 6 ^ 2 = 4
```

### Output
```
4
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
nums = list(map(int, input().split()))

result = 0
for num in nums:
    result ^= num

print(result)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int result = 0;
        for (int i = 0; i < n; i++) {
            int num = sc.nextInt();
            result ^= num;
        }

        System.out.println(result);
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
using namespace std;

int main() {
    int n;
    cin >> n;

    int result = 0;
    for (int i = 0; i < n; i++) {
        int num;
        cin >> num;
        result ^= num;
    }

    cout << result;
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Using extra space like hashmap (violates constraint)
- Sorting the array (unnecessary `O(N log N)`)
- Not understanding why XOR works

---

## 💡 Takeaway

This problem is not about coding — it’s about recognizing patterns.

Whenever:
- Every element appears twice except one  
→ Think **XOR immediately** current state of a traffic signal.

The signal follows a predefined schedule:

- At exactly **0 seconds** → Vehicles can move → `"Green"`
- At exactly **30 seconds** → Warning phase → `"Orange"`
- For **30 < timer ≤ 90** → Vehicles must stop → `"Red"`
- Any other value → `"Invalid"`

---

## 📥 Input Format

A single integer:
```
timer
```

---

## 📌 Constraints

```
0 <= timer <= 1000
```

---

## 📤 Output Format

Print one of:
```
Green
Orange
Red
Invalid
```

---

## 🧠 Approach

We use simple conditional checks:

1. If `timer == 0` → `"Green"`
2. Else if `timer == 30` → `"Orange"`
3. Else if `timer > 30 && timer <= 90` → `"Red"`
4. Else → `"Invalid"`

⚠️ Order matters. Always check exact values before ranges.

---

## 🔍 Dry Run

### Input
```
60
```

### Output
```
Red
```

### Explanation

`60` lies in the range `(30, 90]`, so the signal is `"Red"`.

---

## ⏱️ Complexity

- Time Complexity: `O(1)`
- Space Complexity: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python
```python
timer = int(input())

if timer == 0:
    print("Green")
elif timer == 30:
    print("Orange")
elif 30 < timer <= 90:
    print("Red")
else:
    print("Invalid")
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int timer = sc.nextInt();

        if (timer == 0) {
            System.out.println("Green");
        } else if (timer == 30) {
            System.out.println("Orange");
        } else if (timer > 30 && timer <= 90) {
            System.out.println("Red");
        } else {
            System.out.println("Invalid");
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
    int timer;
    cin >> timer;

    if (timer == 0) {
        cout << "Green";
    } else if (timer == 30) {
        cout << "Orange";
    } else if (timer > 30 && timer <= 90) {
        cout << "Red";
    } else {
        cout << "Invalid";
    }

    return 0;
}
```

---

## ⚠️ Common Mistakes

- Using `timer >= 30` instead of `timer > 30`
- Checking range before exact values
- Forgetting edge case `timer == 0`

