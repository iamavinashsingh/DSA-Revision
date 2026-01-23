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

### PHASE 1 — COMPLETE STATE INVENTORY

**1. Variables & Registers**

| Variable | Type | Scope | Initial Value | Description |
| :--- | :--- | :--- | :--- | :--- |
| `arr` | `vector<int>&` | Parameter | `[5, 3, 7, 2, 4]` | Reference to input data. |
| `n` | `int` | Local | Undefined (initially) | Size of the vector. |
| `i` | `int` | Local | Undefined | Outer loop counter (pass number). |
| `j` | `int` | Local | Undefined | Inner loop counter (comparator). |
| `temp` | `int` | Block | Undefined | Temporary storage for swapping. |

**2. Data Structures (Vector Layout)**

| Index | 0 | 1 | 2 | 3 | 4 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Value** | **5** | **3** | **7** | **2** | **4** |

---

### PHASE 2 — EXECUTION TRACE

#### Initialization

[Step 0]
├── Line: `void bubbleSort(vector<int>& arr) {`
├── Operation: Function Entry
└── Next: Line 2

[Step 1]
├── Line: `int n = arr.size();`
├── Operation: size determination
├── Evaluation: `arr` has 5 elements.
├── After State:
│   └── Variables: `n` = **5**
└── Next: Line 3

---

### OUTER LOOP — Pass 1 (i = 0)
Target: Bubble the largest element to `arr[4]`.

[Step 2]
├── Line: `for (int i = 0; i < n - 1; i++)`
├── Operation: Loop Initialization & Check
├── Evaluation: `i` init to 0. Check `0 < (5 - 1)` $\rightarrow$ `0 < 4` $\rightarrow$ **TRUE**
├── After State:
│   └── Variables: `i` = **0**
└── Next: Line 4

#### INNER LOOP — Iteration 1 (j = 0)

[Step 3]
├── Line: `for (int j = 0; j < n - i - 1; j++)`
├── Operation: Inner Loop Init & Check
├── Evaluation: `j` init to 0. Check `0 < (5 - 0 - 1)` $\rightarrow$ `0 < 4` $\rightarrow$ **TRUE**
├── After State:
│   └── Variables: `j` = **0**
└── Next: Line 5

[Step 4]
├── Line: `if (arr[j] > arr[j + 1])`
├── Before State: `arr`=[5, 3, 7, 2, 4], j=0
├── Operation: Comparison
├── Evaluation: `arr[0]` (5) > `arr[1]` (3) $\rightarrow$ **TRUE**
└── Next: Line 6 (Swap Block)

[Step 5]
├── Line: `int temp = arr[j];`
├── Operation: Store temp
├── After State:
│   └── Variables: `temp` = **5**
└── Next: Line 7

[Step 6]
├── Line: `arr[j] = arr[j + 1];`
├── Operation: Overwrite left
├── After State:
│   └── Data Structures: `arr[0]`: 5 $\rightarrow$ **3**
└── Next: Line 8

[Step 7]
├── Line: `arr[j + 1] = temp;`
├── Operation: Overwrite right (Complete Swap)
├── After State:
│   └── Data Structures: `arr[1]`: 3 $\rightarrow$ **5**
│   └── Current Array: **[3, 5, 7, 2, 4]**
└── Next: Line 4 (Inner Loop Increment)

#### INNER LOOP — Iteration 2 (j = 1)

[Step 8]
├── Line: `for (...; j++)`
├── Operation: Increment & Check
├── Evaluation: `j` becomes 1. Check `1 < 4` $\rightarrow$ **TRUE**
├── After State:
│   └── Variables: `j` = **1**
└── Next: Line 5

[Step 9]
├── Line: `if (arr[j] > arr[j + 1])`
├── Before State: `arr`=[3, 5, 7, 2, 4], j=1
├── Operation: Comparison
├── Evaluation: `arr[1]` (5) > `arr[2]` (7) $\rightarrow$ **FALSE**
└── Next: Line 4 (Inner Loop Increment)

#### INNER LOOP — Iteration 3 (j = 2)

[Step 10]
├── Line: `for (...; j++)`
├── Operation: Increment & Check
├── Evaluation: `j` becomes 2. Check `2 < 4` $\rightarrow$ **TRUE**
├── After State:
│   └── Variables: `j` = **2**
└── Next: Line 5

[Step 11]
├── Line: `if (arr[j] > arr[j + 1])`
├── Before State: `arr`=[3, 5, 7, 2, 4], j=2
├── Operation: Comparison
├── Evaluation: `arr[2]` (7) > `arr[3]` (2) $\rightarrow$ **TRUE**
└── Next: Line 6 (Swap Block)

[Step 12]
├── Line: `int temp = arr[j];`
├── After State: `temp` = **7**
└── Next: Line 7

[Step 13]
├── Line: `arr[j] = arr[j + 1];`
├── After State: `arr[2]`: 7 $\rightarrow$ **2**
└── Next: Line 8

[Step 14]
├── Line: `arr[j + 1] = temp;`
├── After State: `arr[3]`: 2 $\rightarrow$ **7**
│   └── Current Array: **[3, 5, 2, 7, 4]**
└── Next: Line 4

#### INNER LOOP — Iteration 4 (j = 3)

[Step 15]
├── Line: `for (...; j++)`
├── Operation: Increment & Check
├── Evaluation: `j` becomes 3. Check `3 < 4` $\rightarrow$ **TRUE**
├── After State:
│   └── Variables: `j` = **3**
└── Next: Line 5

[Step 16]
├── Line: `if (arr[j] > arr[j + 1])`
├── Before State: `arr`=[3, 5, 2, 7, 4], j=3
├── Operation: Comparison
├── Evaluation: `arr[3]` (7) > `arr[4]` (4) $\rightarrow$ **TRUE**
└── Next: Line 6 (Swap Block)

[Step 17]
├── Line: `int temp = arr[j];`
├── After State: `temp` = **7**
└── Next: Line 7

[Step 18]
├── Line: `arr[j] = arr[j + 1];`
├── After State: `arr[3]`: 7 $\rightarrow$ **4**
└── Next: Line 8

[Step 19]
├── Line: `arr[j + 1] = temp;`
├── After State: `arr[4]`: 4 $\rightarrow$ **7**
│   └── Current Array: **[3, 5, 2, 4, 7]**
└── Next: Line 4

#### INNER LOOP — Termination

[Step 20]
├── Line: `for (...; j++)`
├── Operation: Check
├── Evaluation: `j` becomes 4. Check `4 < 4` $\rightarrow$ **FALSE**
└── Next: Line 3 (Outer Loop Increment)

---

### OUTER LOOP — Pass 2 (i = 1)
Target: Bubble 2nd largest element to `arr[3]`.
Current Array: `[3, 5, 2, 4, 7]`

[Step 21]
├── Line: `for (...; i++)`
├── Operation: Increment & Check
├── Evaluation: `i` becomes 1. Check `1 < 4` $\rightarrow$ **TRUE**
├── After State: `i` = **1**
└── Next: Line 4

#### INNER LOOP — Iteration 1 (j = 0)

[Step 22]
├── Line: `for (int j = 0; j < n - i - 1; j++)`
├── Operation: Reset & Check
├── Evaluation: `j` init to 0. Check `0 < (5 - 1 - 1)` $\rightarrow$ `0 < 3` $\rightarrow$ **TRUE**
├── After State: `j` = **0**
└── Next: Line 5

[Step 23]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[0]` (3) > `arr[1]` (5) $\rightarrow$ **FALSE**
└── Next: Line 4

#### INNER LOOP — Iteration 2 (j = 1)

[Step 24]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 1. Check `1 < 3` $\rightarrow$ **TRUE**
├── After State: `j` = **1**
└── Next: Line 5

[Step 25]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[1]` (5) > `arr[2]` (2) $\rightarrow$ **TRUE**
└── Next: Line 6

[Step 26-28]
├── Operation: Swap (5, 2)
├── After State:
│   ├── temp = 5
│   └── Current Array: **[3, 2, 5, 4, 7]**
└── Next: Line 4

#### INNER LOOP — Iteration 3 (j = 2)

[Step 29]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 2. Check `2 < 3` $\rightarrow$ **TRUE**
├── After State: `j` = **2**
└── Next: Line 5

[Step 30]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[2]` (5) > `arr[3]` (4) $\rightarrow$ **TRUE**
└── Next: Line 6

[Step 31-33]
├── Operation: Swap (5, 4)
├── After State:
│   ├── temp = 5
│   └── Current Array: **[3, 2, 4, 5, 7]**
└── Next: Line 4

#### INNER LOOP — Termination

[Step 34]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 3. Check `3 < 3` $\rightarrow$ **FALSE**
└── Next: Line 3

---

### OUTER LOOP — Pass 3 (i = 2)
Target: Bubble 3rd largest element to `arr[2]`.
Current Array: `[3, 2, 4, 5, 7]`

[Step 35]
├── Line: `for (...; i++)`
├── Evaluation: `i` becomes 2. Check `2 < 4` $\rightarrow$ **TRUE**
├── After State: `i` = **2**
└── Next: Line 4

#### INNER LOOP — Iteration 1 (j = 0)

[Step 36]
├── Line: `for (int j = 0; j < n - i - 1; j++)`
├── Evaluation: `j` init to 0. Check `0 < (5 - 2 - 1)` $\rightarrow$ `0 < 2` $\rightarrow$ **TRUE**
├── After State: `j` = **0**
└── Next: Line 5

[Step 37]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[0]` (3) > `arr[1]` (2) $\rightarrow$ **TRUE**
└── Next: Line 6

[Step 38-40]
├── Operation: Swap (3, 2)
├── After State:
│   ├── temp = 3
│   └── Current Array: **[2, 3, 4, 5, 7]**
└── Next: Line 4

#### INNER LOOP — Iteration 2 (j = 1)

[Step 41]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 1. Check `1 < 2` $\rightarrow$ **TRUE**
├── After State: `j` = **1**
└── Next: Line 5

[Step 42]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[1]` (3) > `arr[2]` (4) $\rightarrow$ **FALSE**
└── Next: Line 4

#### INNER LOOP — Termination

[Step 43]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 2. Check `2 < 2` $\rightarrow$ **FALSE**
└── Next: Line 3

---

### OUTER LOOP — Pass 4 (i = 3)
Target: Bubble 4th largest element to `arr[1]`.
Current Array: `[2, 3, 4, 5, 7]`

[Step 44]
├── Line: `for (...; i++)`
├── Evaluation: `i` becomes 3. Check `3 < 4` $\rightarrow$ **TRUE**
├── After State: `i` = **3**
└── Next: Line 4

#### INNER LOOP — Iteration 1 (j = 0)

[Step 45]
├── Line: `for (int j = 0; j < n - i - 1; j++)`
├── Evaluation: `j` init to 0. Check `0 < (5 - 3 - 1)` $\rightarrow$ `0 < 1` $\rightarrow$ **TRUE**
├── After State: `j` = **0**
└── Next: Line 5

[Step 46]
├── Line: `if (arr[j] > arr[j + 1])`
├── Evaluation: `arr[0]` (2) > `arr[1]` (3) $\rightarrow$ **FALSE**
└── Next: Line 4

#### INNER LOOP — Termination

[Step 47]
├── Line: `for (...; j++)`
├── Evaluation: `j` becomes 1. Check `1 < 1` $\rightarrow$ **FALSE**
└── Next: Line 3

---

### OUTER LOOP — Termination

[Step 48]
├── Line: `for (...; i++)`
├── Evaluation: `i` becomes 4. Check `4 < 4` $\rightarrow$ **FALSE**
└── Next: End of Function

[Step 49]
├── Operation: Return
└── Final State: Function exits.

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
