# Find First and Last Position of Element in Sorted Array

## LINK :-  [LeetCode](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

---

## SOLUTION (C++)

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> ans;
        int index1 = -1;
        int index2 = -1;
        int n = nums.size();
        
        // First occurrence
        int start = 0, end = n - 1;
        while(start <= end) {
            int mid = start + (end - start) / 2;
            if(nums[mid] == target) {
                index1 = mid;
                end = mid - 1;   // move left
            }
            else if(nums[mid] > target) {
                end = mid - 1;
            }
            else {
                start = mid + 1;
            }
        }
        
        // Second occurrence
        start = 0;
        end = n - 1;
        while(start <= end) {
            int mid = start + (end - start) / 2;
            if(nums[mid] == target) {
                index2 = mid;
                start = mid + 1; // move right
            }
            else if(nums[mid] > target) {
                end = mid - 1;
            }
            else {
                start = mid + 1;
            }
        }

        ans.push_back(index1);
        ans.push_back(index2);
        return ans;
    }
};
```

---

## STORY EXPLANATION — THE LIBRARY AISLE

Imagine a **long, sorted library shelf**.

* Every book has the **same title printed multiple times**.
* You are searching for one specific title: **`target`**.
* The shelf is **sorted**, so all identical titles sit together.

### Your Mission

Not to find *a* book.

But to find:

* the **first book** with that title
* the **last book** with that title

You are allowed to walk only using **binary search rules** — no full scan.

---

## CORE IDEA (FIRST PRINCIPLES)

Binary search normally **stops** when it finds the target.

Here, we **do not stop**.

We:

* keep searching **left** to find the *first occurrence*
* keep searching **right** to find the *last occurrence*

So we run **binary search twice**, with different intentions.

---

## PHASE 0 — SANITY & SEMANTICS CHECK

**Input:**

```
nums   = [5, 7, 7, 8, 8, 10]
target = 8
n = 6
```

**Expected Output:**

```
[3, 4]
```

---

## PHASE 1 — INITIAL STATE

| Variable | Value               |
| -------- | ------------------- |
| nums     | [5, 7, 7, 8, 8, 10] |
| target   | 8                   |
| index1   | -1                  |
| index2   | -1                  |
| start    | 0                   |
| end      | 5                   |

---

## PHASE 2 — FIRST OCCURRENCE (LEFTMOST 8)

**Rule:**
If you find the target, **store it** and **move left**.

### Iteration Trace

| Step | start | end | mid | nums[mid] | Action            | index1 |
| ---- | ----- | --- | --- | --------- | ----------------- | ------ |
| 1    | 0     | 5   | 2   | 7         | move right        | -1     |
| 2    | 3     | 5   | 4   | 8         | found → move left | 4      |
| 3    | 3     | 3   | 3   | 8         | found → move left | 3      |
| Stop | 3     | 2   | —   | —         | loop ends         | 3      |

**Result after first search:**

```
index1 = 3
```

---

## PHASE 3 — SECOND OCCURRENCE (RIGHTMOST 8)

**Rule:**
If you find the target, **store it** and **move right**.

### Iteration Trace

| Step | start | end | mid | nums[mid] | Action             | index2 |
| ---- | ----- | --- | --- | --------- | ------------------ | ------ |
| 1    | 0     | 5   | 2   | 7         | move right         | -1     |
| 2    | 3     | 5   | 4   | 8         | found → move right | 4      |
| 3    | 5     | 5   | 5   | 10        | move left          | 4      |
| Stop | 5     | 4   | —   | —         | loop ends          | 4      |

**Result after second search:**

```
index2 = 4
```

---

## PHASE 4 — FINAL OUTPUT

```
ans = [3, 4]
```

---

## WHY THIS WORKS

* The array is **sorted** — duplicates are contiguous
* Binary search guarantees **log(n)** time
* We bias the search:

  * left bias → first occurrence
  * right bias → last occurrence

---

## EDGE CASES HANDLED

| Case                    | Result   |
| ----------------------- | -------- |
| target not present      | [-1, -1] |
| array empty             | [-1, -1] |
| single element match    | [0, 0]   |
| all elements are target | [0, n-1] |

---

## COMPLEXITY ANALYSIS

| Metric | Value                          |
| ------ | ------------------------------ |
| Time   | O(log n) + O(log n) = O(log n) |
| Space  | O(1) (excluding output)        |

---

## MENTAL MODEL TO REMEMBER

Binary search is not just about **finding**.

It is about **shrinking space with intent**.

* Want the *first*? Push right wall left.
* Want the *last*? Push left wall right.

Once this clicks, every boundary problem becomes predictable.
