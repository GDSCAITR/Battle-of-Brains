# 🕵️ The Hidden Payload

## 🧩 Problem Statement

You are given:

- A string `S` (suspected payload)
- A string `T` (network traffic)

The payload `S` is considered successfully hidden if all its characters appear in `T` **in the same order**, but **not necessarily consecutively**.

This is known as a **subsequence**.

---

## 📥 Input Format

- First line: string `S`
- Second line: string `T`

---

## 📌 Constraints

- `0 ≤ S.length ≤ 100`
- `0 ≤ T.length ≤ 10,000`
- Only lowercase letters

---

## 📤 Output Format

- Print `"true"` if `S` is a subsequence of `T`
- Print `"false"` otherwise

---

## 🧠 Approach (Two Pointer Technique)

We use two pointers:

- `i` → for string `S`
- `j` → for string `T`

### Steps:

1. Start both pointers at `0`
2. Traverse `T`:
   - If `S[i] == T[j]` → move both pointers
   - Else → move only `j`
3. If `i == len(S)` → all characters matched → `"true"`
4. Otherwise → `"false"`

---

## 🔍 Dry Run

### Input
```
S = "abc"
T = "ahbgdc"
```

### Steps
```
a == a → move both
b == h → skip h
b == b → move both
c == g → skip g
c == d → skip d
c == c → move both
```

### Output
```
true
```

---

## ⏱️ Complexity

- Time: `O(n)` where `n = len(T)`
- Space: `O(1)`

---

## 💻 Code Implementations

### 🟦 Python
```python
s = input().strip()
t = input().strip()

i = 0

for char in t:
    if i < len(s) and s[i] == char:
        i += 1

print("true" if i == len(s) else "false")
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();

        int i = 0;

        for (int j = 0; j < t.length(); j++) {
            if (i < s.length() && s.charAt(i) == t.charAt(j)) {
                i++;
            }
        }

        if (i == s.length())
            System.out.println("true");
        else
            System.out.println("false");
    }
}
```

---

### 🟥 C++
```cpp
#include <iostream>
using namespace std;

int main() {
    string s, t;
    cin >> s >> t;

    int i = 0;

    for (char c : t) {
        if (i < s.size() && s[i] == c) {
            i++;
        }
    }

    if (i == s.size())
        cout << "true";
    else
        cout << "false";

    return 0;
}
```

---

## ⚠️ Common Mistakes

- Trying to use substring instead of subsequence ❌
- Using nested loops (O(n²)) unnecessarily
- Not handling empty string `S` (should return `"true"`)

---

## 💡 Takeaway

Whenever you see:
- "same order"
- "not necessarily consecutive"

👉 Think **Subsequence → Two Pointers**