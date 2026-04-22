# 🚦 Signal State Decoder

## 🧩 Problem Statement

A smart traffic control system uses a countdown timer (in seconds) to determine

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

