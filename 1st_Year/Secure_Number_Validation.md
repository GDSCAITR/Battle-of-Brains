# 🔐 Secure Number Validation

## 🧩 Problem Statement

A number is considered **secure** if:

- Every **prefix** of the number is a prime number  
- Every **suffix** of the number is also a prime number  

### Definitions:
- **Prefix**: First `k` digits of the number  
- **Suffix**: Last `k` digits of the number  

---

## 📥 Input Format

- A single integer `num`

---

## 📌 Constraints

- `1 ≤ num ≤ 10^9`

---

## 📤 Output Format

- Print `"true"` if the number is secure  
- Print `"false"` otherwise  

---

## 🧠 Approach

### Step 1: Convert number to string
This makes it easy to extract prefixes and suffixes.

### Step 2: Check all prefixes
For each `i` from `1 → length`:
- Take `num[0:i]`
- Convert to integer
- Check if prime

### Step 3: Check all suffixes
For each `i` from `0 → length-1`:
- Take `num[i:]`
- Convert to integer
- Check if prime

### Step 4:
- If any prefix or suffix is **not prime** → return `"false"`
- Otherwise → `"true"`

---

## 🔍 Dry Run

### Input
```
23
```

### Prefixes:
```
2 → prime
23 → prime
```

### Suffixes:
```
3 → prime
23 → prime
```

### Output
```
true
```

---

## 🔧 Prime Check Logic

A number is prime if:
- Greater than 1
- Divisible only by 1 and itself

Efficient check:
- Try dividing from `2` to `√n`

---

## ⏱️ Complexity

- Let `d = number of digits`
- Prime check: `O(√n)`
- Total: `O(d * √n)` (acceptable for constraints)

---

## 💻 Code Implementations

### 🟦 Python
```python
import math

def is_prime(n):
    if n < 2:
        return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if n % i == 0:
            return False
    return True

num = input().strip()
n = len(num)

# check prefixes
for i in range(1, n + 1):
    if not is_prime(int(num[:i])):
        print("false")
        exit()

# check suffixes
for i in range(n):
    if not is_prime(int(num[i:])):
        print("false")
        exit()

print("true")
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {

    public static boolean isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String num = sc.next();
        int n = num.length();

        // prefixes
        for (int i = 1; i <= n; i++) {
            int val = Integer.parseInt(num.substring(0, i));
            if (!isPrime(val)) {
                System.out.println("false");
                return;
            }
        }

        // suffixes
        for (int i = 0; i < n; i++) {
            int val = Integer.parseInt(num.substring(i));
            if (!isPrime(val)) {
                System.out.println("false");
                return;
            }
        }

        System.out.println("true");
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
#include <cmath>
using namespace std;

bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    string num;
    cin >> num;
    int n = num.size();

    // prefixes
    for (int i = 1; i <= n; i++) {
        int val = stoi(num.substr(0, i));
        if (!isPrime(val)) {
            cout << "false";
            return 0;
        }
    }

    // suffixes
    for (int i = 0; i < n; i++) {
        int val = stoi(num.substr(i));
        if (!isPrime(val)) {
            cout << "false";
            return 0;
        }
    }

    cout << "true";
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Forgetting that `1` is **not prime**
- Not checking all prefixes/suffixes
- Using inefficient prime check (full `O(n)` loop)
- Treating number as integer instead of string (harder slicing)

---

## 💡 Takeaway

This problem combines:
- String manipulation  
- Number theory (prime checking)  

Key skill:
👉 Breaking a number into meaningful parts and validating each independently