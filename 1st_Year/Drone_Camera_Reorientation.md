# 🚁 Drone Camera Reorientation

## 🧩 Problem Statement

A surveillance drone captures a square image represented as an `n × n` matrix.

Due to a rotation in the air, the image must be rotated **90 degrees clockwise**.

### Constraint:
- You must perform the rotation **in-place**
- ❌ No extra 2D matrix allowed

---

## 📥 Input Format

- First line: integer `n`
- Next `n` lines: `n` space-separated integers (matrix)

---

## 📌 Constraints

- `1 ≤ n ≤ 500`
- `-10^9 ≤ matrix[i][j] ≤ 10^9`

---

## 📤 Output Format

- Print the rotated matrix

---

## 🧠 Approach (Core Idea)

To rotate a matrix 90° clockwise **in-place**, we do it in 2 steps:

### Step 1: Transpose the matrix
Convert rows into columns:
```
matrix[i][j] ↔ matrix[j][i]
```

### Step 2: Reverse each row
This completes the 90° clockwise rotation

---

## 🔍 Dry Run

### Input
```
1 2 3
4 5 6
7 8 9
```

### After Transpose
```
1 4 7
2 5 8
3 6 9
```

### After Reversing Rows
```
7 4 1
8 5 2
9 6 3
```

---

## ⏱️ Complexity

- Time: `O(n^2)`
- Space: `O(1)` (in-place)

---

## 💻 Code Implementations

### 🟦 Python
```python
n = int(input())
matrix = [list(map(int, input().split())) for _ in range(n)]

# Step 1: Transpose
for i in range(n):
    for j in range(i, n):
        matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

# Step 2: Reverse each row
for i in range(n):
    matrix[i].reverse()

# Print result
for row in matrix:
    print(*row)
```

---

### 🟨 Java
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int[][] matrix = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = sc.nextInt();
            }
        }

        // Step 1: Transpose
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Step 2: Reverse each row
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - j - 1];
                matrix[i][n - j - 1] = temp;
            }
        }

        // Print result
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(matrix[i][j] + " ");
            }
            System.out.println();
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
    int n;
    cin >> n;

    int matrix[n][n];

    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> matrix[i][j];

    // Step 1: Transpose
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }

    // Step 2: Reverse rows
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n / 2; j++) {
            swap(matrix[i][j], matrix[i][n - j - 1]);
        }
    }

    // Print result
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

---

## ⚠️ Common Mistakes

- Using extra matrix (violates constraint ❌)
- Forgetting to restrict transpose to `j >= i`
- Reversing columns instead of rows
- Confusing clockwise vs anticlockwise

---

## 💡 Takeaway

This is a **pattern problem**.

Whenever you see:
> Rotate matrix in-place (90° clockwise)

Immediately think:
👉 **Transpose + Reverse rows**