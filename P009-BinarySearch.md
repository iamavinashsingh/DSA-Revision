# Binary Search

Imagine a **dictionary**.
You never start reading from page 1 to find a word.

Instead:

* You open the **middle**.
* Decide whether the word lies **left** or **right**.
* Throw away half the pages.
* Repeat.

Binary Search works exactly like this — **divide, decide, discard**.

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

* **Source:** C++ `binarySearch` using `std::vector`
* **Array:** `[2, 4, 5, 7, 8, 9, 10, 13, 15]`
* **Target:** `7`

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category         | Assessment                         |
| :--------------- | :--------------------------------- |
| **Language**     | C++ (STL vector)                   |
| **Precondition** | Array must be **sorted**           |
| **Correctness**  | Standard iterative Binary Search   |
| **Mutability**   | Read-only access (no modification) |
| **Memory**       | $O(1)$ auxiliary space             |
| **Determinism**  | Deterministic                      |

---

# Binary Search — Iteration-wise Trace

---

## Iteration 1

| Variable   | Value             |
| ---------- | ----------------- |
| `low`      | 0                 |
| `high`     | 8                 |
| `mid`      | `0 + (8-0)/2 = 4` |
| `arr[mid]` | 8                 |

Comparison:

* `8 > 7` → discard **right half**

Update:

* `high = mid - 1 = 3`

---

## Iteration 2

| Variable   | Value             |
| ---------- | ----------------- |
| `low`      | 0                 |
| `high`     | 3                 |
| `mid`      | `0 + (3-0)/2 = 1` |
| `arr[mid]` | 4                 |

Comparison:

* `4 < 7` → discard **left half**

Update:

* `low = mid + 1 = 2`

---

## Iteration 3

| Variable   | Value             |
| ---------- | ----------------- |
| `low`      | 2                 |
| `high`     | 3                 |
| `mid`      | `2 + (3-2)/2 = 2` |
| `arr[mid]` | 5                 |

Comparison:

* `5 < 7` → discard **left half**

Update:

* `low = mid + 1 = 3`

---

## Iteration 4

| Variable   | Value             |
| ---------- | ----------------- |
| `low`      | 3                 |
| `high`     | 3                 |
| `mid`      | `3 + (3-3)/2 = 3` |
| `arr[mid]` | 7                 |

Comparison:

* `7 == target` → **FOUND**

---

## Search Terminated

Target found at index **3**.

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output

```text
Index = 3
```

### 2. Operation Counters

| Metric             | Count | Details           |
| :----------------- | :---- | :---------------- |
| **Iterations**     | 4     | Loop executions   |
| **Comparisons**    | 4     | One per iteration |
| **Array Accesses** | 4     | `arr[mid]`        |

### 3. Observed Complexity

* **Time:** $O(\log_2 n)$
* **Space:** $O(1)$ — Iterative

---

### Key Insight

Binary Search is powerful because:

* Each step removes **half** the problem
* Performance scales logarithmically

But it is **fragile**:

* One unsorted element breaks correctness
* Off-by-one errors break implementations

Mastery comes from tracing `low`, `mid`, and `high` with discipline.
