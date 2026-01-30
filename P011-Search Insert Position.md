# Search Insert Position — Detailed Trace (dryrun.md)

This document performs a **complete, line-by-line execution trace** of the **Binary Search (Insert Position)** algorithm. The goal is to determine the index at which a target value should be inserted in a sorted array to maintain order.

---

## PROBLEM STATEMENT

Given a **sorted array** of distinct integers and a **target** value:

* Return the index if the target is found
* Otherwise, return the index where it would be inserted in order

---

## SOLUTION (C++)

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int start = 0, end = n - 1;
        int index = 0;
        
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            else if (nums[mid] > target) {
                end = mid - 1;
            }
            else {
                start = mid + 1;
                index = start;
            }
        }
        return index;
    }
};
```

---

## STORY EXPLANATION — THE NUMBER LINE

Imagine a **sorted number line**.

You are trying to place a new number (`target`) such that:

* Order is preserved
* No scanning is allowed
* Only **binary jumps** are permitted

If the number exists, you land on it.
If not, you stop exactly where it *should* live.

---

## PHASE 0 — SANITY & SEMANTICS CHECK

**Input:**

```
nums   = [1, 2, 3, 4, 5, 6, 8]
target = 7
n = 7
```

**Expected Output:**

```
6
```

Explanation: `7` should be inserted **before 8**, at index `6`.

---

## PHASE 1 — INITIAL STATE

| Variable | Value                 |
| -------- | --------------------- |
| nums     | [1, 2, 3, 4, 5, 6, 8] |
| target   | 7                     |
| n        | 7                     |
| start    | 0                     |
| end      | 6                     |
| index    | 0                     |

---

## PHASE 2 — BINARY SEARCH EXECUTION TRACE

**Rule Set:**

* If `nums[mid] == target` → return `mid`
* If `nums[mid] > target` → move left
* If `nums[mid] < target` → move right and update `index = start`

### Iteration Table

| Step | start | end | mid | nums[mid] | Comparison | Action                   | index |
| ---- | ----- | --- | --- | --------- | ---------- | ------------------------ | ----- |
| 1    | 0     | 6   | 3   | 4         | 4 < 7      | move right (`start = 4`) | 4     |
| 2    | 4     | 6   | 5   | 6         | 6 < 7      | move right (`start = 6`) | 6     |
| 3    | 6     | 6   | 6   | 8         | 8 > 7      | move left (`end = 5`)    | 6     |
| Stop | 6     | 5   | —   | —         | —          | loop ends                | 6     |

---

## PHASE 3 — LOOP TERMINATION LOGIC

The loop terminates when:

```
start > end
```

At this point:

* `start = 6`
* `end = 5`
* `index = 6`

This means the correct insertion position is **index 6**.

---

## PHASE 4 — FINAL OUTPUT

```
6
```

---

## WHY THIS WORKS

* The array is **sorted**
* Binary search narrows the valid insertion window
* `index` always tracks the next valid position after smaller elements

Even when the target is missing, the algorithm converges on the exact slot where order remains intact.

---

## EDGE CASES HANDLED

| Case                    | Result               |
| ----------------------- | -------------------- |
| target exists           | exact index returned |
| target smaller than all | 0                    |
| target larger than all  | n                    |
| single element array    | 0 or 1               |
| empty array             | 0                    |

---

## COMPLEXITY ANALYSIS

| Metric | Value    |
| ------ | -------- |
| Time   | O(log n) |
| Space  | O(1)     |

---

## MENTAL MODEL TO REMEMBER

Binary search is not only about **finding values**.

It is about finding **boundaries**.

When the value is missing:

* `start` becomes the insertion point

Once you internalize this, *every insert-position problem becomes mechanical, not magical*.

