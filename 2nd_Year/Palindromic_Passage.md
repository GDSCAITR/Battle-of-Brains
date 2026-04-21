# 🪞 Palindromic Passage

## 🧩 Problem Statement

In the city of Numeria, a mystical gate opens only for numbers that read the same forward and backward.

### Rules:
- If the number remains the same when reversed → Gate opens
- If it changes → Gate stays closed
- Negative numbers are automatically rejected

---

## 📥 Input Format

- A single integer `x`

---

## 📌 Constraints

- `-2^31 ≤ x ≤ 2^31 - 1`

---

## 📤 Output Format

- Print `1` if the number is a palindrome  
- Print `0` otherwise  

---

## 🧠 Approach

### Step 1: Handle negative numbers
- If `x < 0` → return `0`

### Step 2: Reverse the number
- Extract digits using `% 10`
- Build reversed number

### Step 3: Compare
- If original == reversed → palindrome

---

## 🔍 Dry Run

### Input
```
121
```

### Steps
```
Original = 121
Reversed = 121
```

### Output
```
1
```

---

### Input
```
-121
```

### Output
```
0
```

---

## ⏱️ Complexity

- Time: `O(d)` (digits in number)
- Space: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python (Math Approach)
```python
x = int(input())

if x < 0:
    print(0)
else:
    original = x
    rev = 0

    while x > 0:
        digit = x % 10
        rev = rev * 10 + digit
        x //= 10

    print(1 if original == rev else 0)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();

        if (x < 0) {
            System.out.println(0);
            return;
        }

        int original = x;
        int rev = 0;

        while (x > 0) {
            int digit = x % 10;
            rev = rev * 10 + digit;
            x /= 10;
        }

        if (original == rev)
            System.out.println(1);
        else
            System.out.println(0);
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
using namespace std;

int main() {
    int x;
    cin >> x;

    if (x < 0) {
        cout << 0;
        return 0;
    }

    int original = x;
    int rev = 0;

    while (x > 0) {
        int digit = x % 10;
        rev = rev * 10 + digit;
        x /= 10;
    }

    cout << (original == rev ? 1 : 0);
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Treating negative numbers as palindrome ❌
- Using string method without understanding logic
- Forgetting to store original value
- Integer overflow (not an issue here due to constraints, but important concept)

---

## 💡 Takeaway

This problem builds foundation for:
- Digit manipulation
- Reverse logic
- Thinking beyond strings

👉 Always prefer **math-based approach** when possible