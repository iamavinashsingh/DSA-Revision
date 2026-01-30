# Peak Index in a Mountain Array

## LINK :- [LeetCode](https://leetcode.com/problems/peak-index-in-a-mountain-array/)

---

## SOLUTION (C++)

```cpp
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int n = arr.size();
        int start = 1, end = n - 2;
        while (start <= end) {
            int mid = start + (end - start) / 2;
            if (arr[mid] > arr[mid - 1] && arr[mid] > arr[mid + 1]) {
                return mid;
            }
            else if (arr[mid] < arr[mid + 1]) {
                start = mid + 1;
            }
            else {
                end = mid - 1;
            }
        }
        return -1;
    }
};
```

---

## STORY EXPLANATION — THE MOUNTAIN RIDGE

Picture a **single mountain ridge**.

* You start climbing from the left.
* At some point, you reach the **highest peak**.
* After that, the path only goes **downward**.

This array is a perfect mountain:

* strictly increasing
* one peak
* strictly decreasing

Your task is to find **where the peak is**, without walking the whole mountain.

Binary search is your helicopter.

---

## CORE IDEA (FIRST PRINCIPLES)

At any index `mid`, only **three shapes** are possible:

1. **Peak**  → `arr[mid] > arr[mid-1] && arr[mid] > arr[mid+1]`
2. **Ascending slope** → `arr[mid] < arr[mid+1]`
3. **Descending slope** → otherwise

The direction of the slope tells you **where the peak must lie**.

---

## PHASE 0 — SANITY CHECK

**Input:**

```
arr = [1,2,3,4,6,8,10,9,7,5]
```

**Expected Output:**

```
6
```

(10 is the peak, at index 6)

---

## PHASE 1 — INITIAL STATE

| Variable | Value                  |
| -------- | ---------------------- |
| arr      | [1,2,3,4,6,8,10,9,7,5] |
| n        | 10                     |
| start    | 1                      |
| end      | 8                      |

We avoid index `0` and `n-1` because the peak **cannot** be at the edges.

---

## PHASE 2 — BINARY SEARCH DRY RUN

### Iteration 1

| start | end | mid | arr[mid] | Comparison | Decision               |
| ----- | --- | --- | -------- | ---------- | ---------------------- |
| 1     | 8   | 4   | 6        | `6 < 8`    | ascending → move right |

```
start = mid + 1 = 5
```

---

### Iteration 2

| start | end | mid | arr[mid] | Comparison         | Decision   |
| ----- | --- | --- | -------- | ------------------ | ---------- |
| 5     | 8   | 6   | 10       | `10 > 8 && 10 > 9` | peak found |

```
return 6
```

---

## PHASE 3 — FINAL OUTPUT

```
Peak Index = 6
```

---

## WHY THIS WORKS

* A mountain array has **exactly one peak**
* On an ascending slope, the peak is **to the right**
* On a descending slope, the peak is **to the left**
* Binary search eliminates **half the mountain** each step

---

## EDGE CASES HANDLED

| Case                 | Reason                 |
| -------------------- | ---------------------- |
| Minimum size (n ≥ 3) | guaranteed by problem  |
| Peak not found       | returns -1 (defensive) |
| Strict mountain      | ensures correctness    |

---

## COMPLEXITY ANALYSIS

| Metric | Value    |
| ------ | -------- |
| Time   | O(log n) |
| Space  | O(1)     |

---

## MENTAL MODEL TO REMEMBER

You are not searching for a value.

You are searching for **a shape**.

* Upward slope → peak ahead
* Downward slope → peak behind
* Taller than both neighbors → summit reached

Binary search is simply **reading the terrain intelligently**.

