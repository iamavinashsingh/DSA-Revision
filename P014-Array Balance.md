# 3634. Minimum Removals to Balance Array

---

## Link :- [LeetCode](https://leetcode.com/problems/minimum-removals-to-balance-array/?envType=daily-question&envId=2026-02-06)

## Target Problem

An array is **balanced** if:

```
max_element <= min_element * k
```

You may remove any number of elements (array must remain non-empty).
Return the **minimum removals** needed.

---

## Target Code

```cpp
class Solution {
public:
    int minRemoval(vector<int>& nums, int k) {
        int n = nums.size();
        if (n <= 1) return 0;

        sort(nums.begin(), nums.end());

        int left = 0;
        int maxSize = 1;

        for (int right = 0; right < n; right++) {
            while ((long long)nums[right] > (long long)nums[left] * k) {
                left++;
            }
            maxSize = max(maxSize, right - left + 1);
        }

        return n - maxSize;
    }
};
```

---

## DRY RUN

### Input Case (Primary Walkthrough)

```
nums = [1, 6, 2, 9]
k = 3
```

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category        | Status         | Details                         |
| --------------- | -------------- | ------------------------------- |
| Language        | C++            | Standard STL (`vector`, `sort`) |
| Sorting         | Required       | Enables two-pointer window      |
| Mutability      | In-place       | Input array modified            |
| Overflow Safety | Safe           | Uses `long long` casting        |
| Strategy        | Sliding Window | Optimal O(n log n)              |

---

## PHASE 1 — PREPROCESSING

### Step 1: Sort the Array

```
Original : [1, 6, 2, 9]
Sorted   : [1, 2, 6, 9]
```

### Initial State

| Variable | Value |
| -------- | ----- |
| n        | 4     |
| left     | 0     |
| maxSize  | 1     |

---

## PHASE 2 — SLIDING WINDOW EXECUTION

### Invariant Maintained

At any time:

```
nums[right] <= nums[left] * k
```

Window `[left ... right]` is balanced.

---

### RIGHT = 0

| State       | Value             |
| ----------- | ----------------- |
| nums[right] | 1                 |
| nums[left]  | 1                 |
| Check       | 1 <= 1 * 3 → TRUE |

Window: `[1]`

```
size = 1
maxSize = 1
```

---

### RIGHT = 1

| State       | Value             |
| ----------- | ----------------- |
| nums[right] | 2                 |
| nums[left]  | 1                 |
| Check       | 2 <= 1 * 3 → TRUE |

Window: `[1, 2]`

```
size = 2
maxSize = 2
```

---

### RIGHT = 2

| State       | Value              |
| ----------- | ------------------ |
| nums[right] | 6                  |
| nums[left]  | 1                  |
| Check       | 6 <= 1 * 3 → FALSE |

❌ Window invalid → move `left`

#### Move `left` → 1

| nums[left] | 2 |
| Check | 6 <= 2 * 3 → TRUE |

Window: `[2, 6]`

```
size = 2
maxSize = 2
```

---

### RIGHT = 3

| State       | Value              |
| ----------- | ------------------ |
| nums[right] | 9                  |
| nums[left]  | 2                  |
| Check       | 9 <= 2 * 3 → FALSE |

❌ Window invalid → move `left`

#### Move `left` → 2

| nums[left] | 6 |
| Check | 9 <= 6 * 3 → TRUE |

Window: `[6, 9]`

```
size = 2
maxSize = 2
```

---

## PHASE 3 — FINAL COMPUTATION

| Metric                  | Value       |
| ----------------------- | ----------- |
| Total elements          | 4           |
| Largest balanced subset | 2           |
| Minimum removals        | `4 - 2 = 2` |

---

## FINAL ANSWER

```
2
```

---

## WHY THIS WORKS (INTUITION)

* Sorting converts the problem into finding the **largest valid window**.
* Two pointers ensure every element is processed at most twice.
* We **maximize what we keep**, not minimize what we remove.

---

## COMPLEXITY ANALYSIS

| Aspect         | Cost       |
| -------------- | ---------- |
| Sorting        | O(n log n) |
| Sliding Window | O(n)       |
| Total          | O(n log n) |
| Extra Space    | O(1)       |

---

## EDGE CASES VERIFIED

| Case               | Result                        |
| ------------------ | ----------------------------- |
| Single element     | 0 removals                    |
| All equal elements | 0 removals                    |
| k = 1              | Only identical values allowed |
| Large values       | Overflow-safe                 |

---

## KEY TAKEAWAY

This is **not** a removal problem.

It is a **maximum valid subset** problem disguised as one.

Once you see that — the solution becomes inevitable.
