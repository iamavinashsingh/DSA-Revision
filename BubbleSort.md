# Bubble Sort

Imagine morning assembly in school.
All students must stand according to height — shortest in front, tallest at the back.
But today, they’re standing randomly.

What the teacher does (Bubble Sort):

- The teacher looks at two students standing next to each other.
- If the taller student is in front of the shorter one,
👉 the teacher tells them to swap places.
- The teacher moves to the next pair and does the same check.
- This continues till the last student.

After one round:

- The tallest student reaches the back of the line.

- Then the teacher starts again from the front of the line.

- They repeat this until:

- Everyone is standing properly height-wise,

- No swapping is needed.

---

```cpp
void bubbleSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

```

---

## DRY RUN 



**Input Status:**
* **Source:** C++ `bubbleSort` function using `std::vector`.
* **Test Case:** `arr = [5, 3, 7, 2, 4]`

---

### PHASE 0 — SANITY & SEMANTICS CHECK

| Category | Assessment |
| :--- | :--- |
| **Language** | C++ (Standard Template Library used). |
| **Correctness** | Syntax is valid. Algorithm is standard Bubble Sort. |
| **Mutability** | `vector<int>& arr` is passed by reference. The original vector **will** be modified. |
| **Memory** | In-place sorting. $O(1)$ auxiliary space excluding the vector itself. |
| **Scope** | `i` and `j` are block-scoped to their loops. `temp` is scoped to the `if` block. |
| **Determinism** | Deterministic. Output depends solely on input order and values. |

---

# Bubble Sort — Detailed Pass-wise Tables

---

This document breaks **Bubble Sort execution** into **clear table-based traces**, grouped by each outer-loop pass (`i`).

---

## Pass 1 — `i = 0`

Initial Array: `[5, 3, 7, 2, 4]`

| State / Step        | j = 0     | j = 1     | j = 2     | j = 3     |
| ------------------- | --------- | --------- | --------- | --------- |
| **Array before**    | 5,3,7,2,4 | 3,5,7,2,4 | 3,5,7,2,4 | 3,5,2,7,4 |
| `i`                 | 0         | 0         | 0         | 0         |
| `j`                 | 0         | 1         | 2         | 3         |
| `arr[j]`            | 5         | 5         | 7         | 7         |
| `arr[j+1]`          | 3         | 7         | 2         | 4         |
| `arr[j] > arr[j+1]` | TRUE      | FALSE     | TRUE      | TRUE      |
| Swap performed      | Yes       | No        | Yes       | Yes       |
| **Array after**     | 3,5,7,2,4 | 3,5,7,2,4 | 3,5,2,7,4 | 3,5,2,4,7 |

Result after Pass 1: `[3, 5, 2, 4, 7]`

---

## Pass 2 — `i = 1`

Initial Array: `[3, 5, 2, 4, 7]`

| State / Step        | j = 0     | j = 1     | j = 2     |
| ------------------- | --------- | --------- | --------- |
| **Array before**    | 3,5,2,4,7 | 3,5,2,4,7 | 3,2,5,4,7 |
| `i`                 | 1         | 1         | 1         |
| `j`                 | 0         | 1         | 2         |
| `arr[j]`            | 3         | 5         | 5         |
| `arr[j+1]`          | 5         | 2         | 4         |
| `arr[j] > arr[j+1]` | FALSE     | TRUE      | TRUE      |
| Swap performed      | No        | Yes       | Yes       |
| **Array after**     | 3,5,2,4,7 | 3,2,5,4,7 | 3,2,4,5,7 |

Result after Pass 2: `[3, 2, 4, 5, 7]`

---

## Pass 3 — `i = 2`

Initial Array: `[3, 2, 4, 5, 7]`

| State / Step        | j = 0     | j = 1     |
| ------------------- | --------- | --------- |
| **Array before**    | 3,2,4,5,7 | 2,3,4,5,7 |
| `i`                 | 2         | 2         |
| `j`                 | 0         | 1         |
| `arr[j]`            | 3         | 3         |
| `arr[j+1]`          | 2         | 4         |
| `arr[j] > arr[j+1]` | TRUE      | FALSE     |
| Swap performed      | Yes       | No        |
| **Array after**     | 2,3,4,5,7 | 2,3,4,5,7 |

Result after Pass 3: `[2, 3, 4, 5, 7]`

---

## Pass 4 — `i = 3`

Initial Array: `[2, 3, 4, 5, 7]`

| State / Step        | j = 0     |
| ------------------- | --------- |
| **Array before**    | 2,3,4,5,7 |
| `i`                 | 3         |
| `j`                 | 0         |
| `arr[j]`            | 2         |
| `arr[j+1]`          | 3         |
| `arr[j] > arr[j+1]` | FALSE     |
| Swap performed      | No        |
| **Array after**     | 2,3,4,5,7 |

Result after Pass 4: `[2, 3, 4, 5, 7]`

---

## Final Sorted Array

`[2, 3, 4, 5, 7]`

---

### PHASE 3 — FINAL STATE & VALIDATION

**1. Final Output**
`arr` = `[2, 3, 4, 5, 7]`

**2. Operation Counters**
| Metric | Count | Details |
| :--- | :--- | :--- |
| **Passes (Outer Loop)** | 4 | `i` = 0, 1, 2, 3 |
| **Comparisons** | 10 | Sum of inner loop iterations (4 + 3 + 2 + 1) |
| **Swaps** | 6 | Total successful `if` blocks executed |
| **Assignments** | 18 | 6 Swaps × 3 assignments each |

**3. Observed Complexity**
* **Time:** $O(n^2)$ — Specifically $\frac{n(n-1)}{2}$ comparisons performed regardless of data state.
* **Space:** $O(1)$ — Only `temp`, `i`, `j`, `n` used.
