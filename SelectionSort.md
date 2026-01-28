# Selection Sort

Imagine morning assembly in school again.
But this time, the teacher follows a **very strict rule**.

* The teacher looks at the **entire line**.
* Finds the **shortest student**.
* Brings that student to the **front position**.

Then:

* The teacher ignores the first position (it’s now correct).
* Looks at the remaining students.
* Again finds the shortest among them.
* Places them in the next position.

This continues until every position is fixed.

That’s **Selection Sort** — select the minimum, place it correctly, repeat.

---

```cpp
void selectionSort(vector<int>& arr) {
    int n = arr.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        if (minIndex != i) {
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
}
```

---

## DRY RUN

**Input Status:**

* **Source:** C++ `selectionSort` using `std::vector`
* **Test Case:** `arr = [5, 3, 7, 2, 4]`

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category        | Assessment                                     |
| :-------------- | :--------------------------------------------- |
| **Language**    | C++ (STL vector)                               |
| **Correctness** | Standard Selection Sort                        |
| **Mutability**  | Passed by reference — original vector modified |
| **Memory**      | In-place, $O(1)$ extra space                   |
| **Stability**   | ❌ Not stable (can disturb equal elements)      |
| **Determinism** | Deterministic                                  |

---

# Selection Sort — Detailed Pass-wise Tables

---

## Pass 1 — `i = 0`

Initial Array: `[5, 3, 7, 2, 4]`

| j | Current Min | Comparison | minIndex |
| - | ----------- | ---------- | -------- |
| 1 | 3           | 3 < 5      | 1        |
| 2 | 7           | 7 < 3 ❌    | 1        |
| 3 | 2           | 2 < 3      | 3        |
| 4 | 4           | 4 < 2 ❌    | 3        |

Swap `arr[0]` and `arr[3]`

Array after Pass 1: **[2, 3, 7, 5, 4]**

---

## Pass 2 — `i = 1`

Initial Array: `[2, 3, 7, 5, 4]`

| j | Current Min | Comparison | minIndex |
| - | ----------- | ---------- | -------- |
| 2 | 7           | 7 < 3 ❌    | 1        |
| 3 | 5           | 5 < 3 ❌    | 1        |
| 4 | 4           | 4 < 3 ❌    | 1        |

No swap needed (already minimum)

Array after Pass 2: **[2, 3, 7, 5, 4]**

---

## Pass 3 — `i = 2`

Initial Array: `[2, 3, 7, 5, 4]`

| j | Current Min | Comparison | minIndex |
| - | ----------- | ---------- | -------- |
| 3 | 5           | 5 < 7      | 3        |
| 4 | 4           | 4 < 5      | 4        |

Swap `arr[2]` and `arr[4]`

Array after Pass 3: **[2, 3, 4, 5, 7]**

---

## Pass 4 — `i = 3`

Initial Array: `[2, 3, 4, 5, 7]`

| j | Current Min | Comparison | minIndex |
| - | ----------- | ---------- | -------- |
| 4 | 7           | 7 < 5 ❌    | 3        |

No swap needed

Array after Pass 4: **[2, 3, 4, 5, 7]**

---

## Final Sorted Array

`[2, 3, 4, 5, 7]`

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output

`arr = [2, 3, 4, 5, 7]`

### 2. Operation Counters

| Metric          | Count | Details                  |
| :-------------- | :---- | :----------------------- |
| **Passes**      | 4     | `i = 0 → 3`              |
| **Comparisons** | 10    | Always fixed: `n(n-1)/2` |
| **Swaps**       | 2     | One per pass (at most)   |
| **Assignments** | 6     | 2 swaps × 3 assignments  |

### 3. Observed Complexity

* **Best Case:** $O(n^2)$
* **Average Case:** $O(n^2)$
* **Worst Case:** $O(n^2)$
* **Space:** $O(1)$ — In-place

---

### Key Insight

Selection Sort minimizes **writes/swaps**, not comparisons.

It is useful when:

* Swapping is expensive
* Memory writes must be minimized
* Simplicity matters more than speed
