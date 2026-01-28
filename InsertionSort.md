# Insertion Sort

Imagine morning assembly in school.
Students are standing in a line, and the teacher starts arranging them **one by one**.

At first, only the **first student** is considered sorted.
Then:

* The teacher picks the next student.
* Moves them **backwards** in the line.
* Compares with students already standing.
* Inserts the student into the **correct position** based on height.

This repeats until the entire line is perfectly ordered.

That’s **Insertion Sort**.

---

```cpp
void insertionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

---

## DRY RUN

**Input Status:**

* **Source:** C++ `insertionSort` using `std::vector`
* **Test Case:** `arr = [5, 3, 7, 2, 4]`

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category        | Assessment                                     |
| :-------------- | :--------------------------------------------- |
| **Language**    | C++ (STL vector)                               |
| **Correctness** | Standard Insertion Sort                        |
| **Mutability**  | Passed by reference — original vector modified |
| **Memory**      | In-place, $O(1)$ extra space                   |
| **Stability**   | Stable sorting algorithm                       |
| **Determinism** | Deterministic                                  |

---

# Insertion Sort — Detailed Pass-wise Tables

---

## Pass 1 — `i = 1`

Initial Array: `[5, 3, 7, 2, 4]`

| Step          | Action           | Array State   |
| ------------- | ---------------- | ------------- |
| key = 3       | Compare with 5   | 5 > 3 → shift |
| Shift 5 right | —                | 5,5,7,2,4     |
| Insert key    | Place at index 0 | **3,5,7,2,4** |

Result after Pass 1: `[3, 5, 7, 2, 4]`

---

## Pass 2 — `i = 2`

Initial Array: `[3, 5, 7, 2, 4]`

| Step     | Action           | Array State   |
| -------- | ---------------- | ------------- |
| key = 7  | Compare with 5   | 5 < 7 → stop  |
| No shift | Already in place | **3,5,7,2,4** |

Result after Pass 2: `[3, 5, 7, 2, 4]`

---

## Pass 3 — `i = 3`

Initial Array: `[3, 5, 7, 2, 4]`

| Step           | Action         | Array State   |
| -------------- | -------------- | ------------- |
| key = 2        | Compare with 7 | shift         |
| Shift 7        | —              | 3,5,7,7,4     |
| Compare with 5 | shift          |               |
| Shift 5        | —              | 3,5,5,7,4     |
| Compare with 3 | shift          |               |
| Shift 3        | —              | 3,3,5,7,4     |
| Insert key     | index 0        | **2,3,5,7,4** |

Result after Pass 3: `[2, 3, 5, 7, 4]`

---

## Pass 4 — `i = 4`

Initial Array: `[2, 3, 5, 7, 4]`

| Step           | Action         | Array State   |
| -------------- | -------------- | ------------- |
| key = 4        | Compare with 7 | shift         |
| Shift 7        | —              | 2,3,5,7,7     |
| Compare with 5 | shift          |               |
| Shift 5        | —              | 2,3,5,5,7     |
| Compare with 3 | stop           |               |
| Insert key     | index 2        | **2,3,4,5,7** |

Result after Pass 4: `[2, 3, 4, 5, 7]`

---

## Final Sorted Array

`[2, 3, 4, 5, 7]`

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output

`arr = [2, 3, 4, 5, 7]`

### 2. Operation Counters

| Metric          | Count | Details                     |
| :-------------- | :---- | :-------------------------- |
| **Passes**      | 4     | `i = 1 → 4`                 |
| **Comparisons** | 8     | Best depends on input order |
| **Shifts**      | 7     | Element movements           |
| **Insertions**  | 4     | One per pass                |

### 3. Observed Complexity

* **Best Case:** $O(n)$ — Already sorted
* **Average Case:** $O(n^2)$
* **Worst Case:** $O(n^2)$ — Reverse sorted
* **Space:** $O(1)$ — In-place

---

### Key Insight

Insertion Sort is efficient for:

* Small arrays
* Nearly sorted data
* Online sorting (data arrives gradually)

It behaves like how humans naturally sort cards in hand.
