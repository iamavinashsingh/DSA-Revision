# Sqrt(x)

This document performs a **complete, line-by-line execution trace** of the **Binary Search–based integer square root algorithm**. The goal is to compute the **floor value of √x** without using built-in square root functions.

---

## Link :- [LeetCode](https://leetcode.com/problems/sqrtx/description/)

## PROBLEM STATEMENT

Given a **non-negative integer `x`**, return the **integer part of its square root**.

* Decimal parts are truncated
* The result satisfies: `ans * ans ≤ x < (ans + 1)²`

---

## SOLUTION (C++)

```cpp
class Solution {
public:
    int mySqrt(int x) {
        if (x < 2) return x;

        int left = 1;
        int right = x / 2;
        int ans = 0;

        while (left <= right) {
            int mid = left + (right - left) / 2;

            if (mid == x / mid) {
                return mid;
            }
            else if (mid < x / mid) {
                ans = mid;
                left = mid + 1;
            }
            else {
                right = mid - 1;
            }
        }
        return ans;
    }
};
```

---

## STORY EXPLANATION — SEARCHING FOR THE PERFECT SQUARE

Imagine searching for a number whose **square fits inside `x`**, but the next number’s square would overflow.

You are not guessing randomly.
You are **shrinking a numeric window**, carefully, using binary search.

---

## PHASE 0 — SANITY & SEMANTICS CHECK

**Input:**

```
x = 56
```

**Expected Output:**

```
7
```

Explanation:

* `7 × 7 = 49 ≤ 56`
* `8 × 8 = 64 > 56`

---

## PHASE 1 — INITIAL STATE

| Variable | Value |
| -------- | ----- |
| x        | 56    |
| left     | 1     |
| right    | 28    |
| ans      | 0     |

---

## PHASE 2 — BINARY SEARCH EXECUTION TRACE

**Search Space:** integers in range `[1, x / 2]`

**Decision Rules:**

* If `mid == x / mid` → perfect square found
* If `mid < x / mid` → mid² < x → store mid, move right
* If `mid > x / mid` → mid² > x → move left

### Iteration Table

| Step | left | right | mid | x / mid | Comparison | Action                          | ans |
| ---- | ---- | ----- | --- | ------- | ---------- | ------------------------------- | --- |
| 1    | 1    | 28    | 14  | 4       | 14 > 4     | move left (`right = 13`)        | 0   |
| 2    | 1    | 13    | 7   | 8       | 7 < 8      | store & move right (`left = 8`) | 7   |
| 3    | 8    | 13    | 10  | 5       | 10 > 5     | move left (`right = 9`)         | 7   |
| 4    | 8    | 9     | 8   | 7       | 8 > 7      | move left (`right = 7`)         | 7   |
| Stop | 8    | 7     | —   | —       | —          | loop ends                       | 7   |

---

## PHASE 3 — LOOP TERMINATION LOGIC

The loop terminates when:

```
left > right
```

Final boundary state:

* `left = 8`
* `right = 7`
* `ans = 7`

At this point, `ans` holds the **largest integer whose square does not exceed `x`**.

---

## PHASE 4 — FINAL OUTPUT

```
7
```

---

## WHY THIS WORKS

* Squaring large numbers risks **overflow**
* Division (`x / mid`) avoids multiplication overflow
* Binary search guarantees convergence in **O(log x)** time

The algorithm always remembers the **last valid candidate** using `ans`.

---

## EDGE CASES HANDLED

| Case               | Result             |
| ------------------ | ------------------ |
| x = 0              | 0                  |
| x = 1              | 1                  |
| perfect square     | exact root         |
| non-perfect square | floor value        |
| large x            | safe from overflow |

---

## COMPLEXITY ANALYSIS

| Metric | Value    |
| ------ | -------- |
| Time   | O(log x) |
| Space  | O(1)     |

---

## MENTAL MODEL TO REMEMBER

You are not searching for equality.

You are searching for the **last number that still fits**.

Binary search becomes powerful when you stop thinking about values — and start thinking about **boundaries**.

