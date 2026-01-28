# Binary Search

Imagine searching for a name in a **dictionary**.
You never start from page one.

Instead:

* You open the book in the **middle**.
* Decide whether the word is on the **left half** or **right half**.
* Throw away the other half completely.
* Repeat the process on the remaining half.

That’s **Binary Search** — repeatedly halving the search space.

---

```cpp
int binarySearch(vector<int>& arr, int target) {
    int low = 0;
    int high = arr.size() - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
            return mid;
        else if (arr[mid] < target)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}
```

---

## DRY RUN

**Input Status:**

* **Source:** C++ iterative `binarySearch`
* **Precondition:** Array **must be sorted**
* **Test Case:** `arr = [2, 3, 4, 5, 7]`, `target = 4`

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category         | Assessment                            |
| :--------------- | :------------------------------------ |
| **Language**     | C++ (STL vector)                      |
| **Correctness**  | Valid iterative Binary Search         |
| **Mutability**   | Read-only access (array not modified) |
| **Memory**       | $O(1)$ extra space                    |
| **Precondition** | Array must be sorted                  |
| **Determinism**  | Deterministic                         |

---

# Binary Search — Step-by-Step Execution Table

---

## Iteration 1

Initial State:

* `low = 0`
* `high = 4`

| Variable   | Value               |
| ---------- | ------------------- |
| mid        | `0 + (4 - 0)/2 = 2` |
| arr[mid]   | 4                   |
| Comparison | `4 == 4`            |

Target found.

---

## Result

Index returned: **2**

---

## Alternate Dry Run — Target Not Present

**Target:** `6`

| Iteration | low | high | mid | arr[mid] | Action       |
| --------- | --- | ---- | --- | -------- | ------------ |
| 1         | 0   | 4    | 2   | 4        | Search right |
| 2         | 3   | 4    | 3   | 5        | Search right |
| 3         | 4   | 4    | 4   | 7        | Search left  |
| End       | 4   | 3    | —   | —        | Stop         |

Return value: **-1**

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output

* If target exists → index returned
* If not → `-1`

### 2. Operation Counters

| Metric          | Count                  | Details                    |
| :-------------- | :--------------------- | :------------------------- |
| **Iterations**  | ≤ `log2(n)`            | Halving each step          |
| **Comparisons** | ≤ `log2(n)`            | Equality + direction check |
| **Assignments** | Constant per iteration | low, high, mid             |

### 3. Observed Complexity

* **Best Case:** $O(1)$ — Found at mid
* **Average Case:** $O(log n)$
* **Worst Case:** $O(log n)$
* **Space:** $O(1)$

---

### Key Insight

Binary Search trades **ordering cost upfront** for **extremely fast lookup**.

If searching happens often:

* Sort once
* Search many times

That’s why it’s foundational in systems, databases, and low-level libraries.
