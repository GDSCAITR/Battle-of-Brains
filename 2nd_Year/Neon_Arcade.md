# 🎮 Neon Arcade - The Glitch Scoreboard

## 🧩 Problem Statement

You are playing an arcade game with a glitched scoring system.

You receive a sequence of operations that modify your score record.

Each operation works as follows:

- **Integer X** → Add score `X`
- **"+"** → Add sum of last two scores
- **"D"** → Add double of last score
- **"C"** → Remove last score

Your task is to process all operations and return the final sum of the scores.

---

## 📥 Input Format

- First line: integer `N` (number of operations)
- Second line: `N` space-separated operations

---

## 📌 Constraints

- `1 ≤ N ≤ 1000`
- Values range: `[-30000, 30000]`
- Operations are always valid

---

## 📤 Output Format

- Print the final sum of all scores

---

## 🧠 Approach

We simulate the process using a **stack (or list)**.

### Why Stack?
Because we always work with:
- Last score
- Last two scores

### Steps:

1. Initialize empty stack
2. Traverse each operation:
   - If number → push to stack
   - If `"+"` → push sum of last two
   - If `"D"` → push double of last
   - If `"C"` → pop last element
3. Return sum of stack

---

## 🔍 Dry Run

### Input
```
5 2 C D +
```

### Steps
```
[5]
[5, 2]
[5]
[5, 10]
[5, 10, 15]
```

### Output
```
30
```

---

## ⏱️ Complexity

- Time: `O(N)`
- Space: `O(N)`

---

## 💻 Code Implementations

### 🟦 Python
```python
n = int(input())
ops = input().split()

stack = []

for op in ops:
    if op == "+":
        stack.append(stack[-1] + stack[-2])
    elif op == "D":
        stack.append(2 * stack[-1])
    elif op == "C":
        stack.pop()
    else:
        stack.append(int(op))

print(sum(stack))
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < n; i++) {
            String op = sc.next();

            if (op.equals("+")) {
                int top = stack.pop();
                int newScore = top + stack.peek();
                stack.push(top);
                stack.push(newScore);
            } else if (op.equals("D")) {
                stack.push(2 * stack.peek());
            } else if (op.equals("C")) {
                stack.pop();
            } else {
                stack.push(Integer.parseInt(op));
            }
        }

        int sum = 0;
        for (int val : stack) sum += val;

        System.out.println(sum);
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

    vector<string> ops(n);
    for (int i = 0; i < n; i++) cin >> ops[i];

    vector<int> stack;

    for (auto &op : ops) {
        if (op == "+") {
            stack.push_back(stack[stack.size()-1] + stack[stack.size()-2]);
        } else if (op == "D") {
            stack.push_back(2 * stack.back());
        } else if (op == "C") {
            stack.pop_back();
        } else {
            stack.push_back(stoi(op));
        }
    }

    int sum = 0;
    for (int x : stack) sum += x;

    cout << sum;
    return 0;
}
```

---

## ⚠️ Common Mistakes

- Not handling `"+"` correctly (needs last TWO values)
- Forgetting stack order when popping in Java
- Trying to solve without stack → messy logic
- Not converting string to integer properly

---

## 💡 Takeaway

Whenever problem says:
- "last", "previous", "undo", "history"

👉 Think **STACK immediately**