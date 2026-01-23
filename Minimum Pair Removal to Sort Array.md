# 3507. Minimum Pair Removal to Sort Array I

## Link :-   [LeetCode Link](https://leetcode.com/problems/minimum-pair-removal-to-sort-array-i/description/)

---

## Solution 

```cpp
class Solution {
public:
    int minimumPairRemoval(vector<int>& nums) {
               
        int operations = 0;

        // Repeat until array is non-decreasing
        while (true) {
            bool sorted = true;
            for (int i = 0; i + 1 < nums.size(); i++) {
                if (nums[i] > nums[i + 1]) {
                    sorted = false;
                    break;
                }
            }

            if (sorted) 
                break;

            // Find adjacent pair with minimum sum
            int minSum = INT_MAX;
            int index = -1;
            for (int i = 0; i + 1 < nums.size(); i++) {
                int s = nums[i] + nums[i + 1];
                if (s < minSum) {
                    minSum = s;
                    index = i;
                }
            }

            // Replace pair with their sum
            nums[index] = minSum;
            nums.erase(nums.begin() + index + 1);
            operations++;
        }

        return operations;
        
    }
};


```

---

## DRY RUN 


**Target Code:** `Solution::minimumPairRemoval`  
**Input Case:** `[2, 2, -1, 3, -2, 2, 1, 1, 1, 0, -1]`  
**Status:** COMPLETE  

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category | Status | Details |
| :--- | :--- | :--- |
| **Language** | C++ | Standard C++ compilation assumed. Code uses `vector` and `INT_MAX`. |
| **Compilation** | **Valid** | Syntax is correct. Requires headers `<vector>` and `<climits>`. |
| **Mutability** | **Mutable** | `vector<int>& nums` allows direct modification of the input array. |
| **Scope** | **Local** | All variables (`i`, `minSum`, `index`, `sorted`) are scoped correctly within loops. |
| **Logic** | **Deterministic** | Behavior is strictly defined by input values and standard arithmetic. |

**Assumptions:**
1. Input vector is valid and non-null.
2. `INT_MAX` is standard (2,147,483,647).

---

## PHASE 1 — COMPLETE STATE INVENTORY

### 1. Variables & Registers

| Variable | Type | Initial Value | Role |
| :--- | :--- | :--- | :--- |
| `nums` | `vector<int>` | `[2, 2, -1, 3, -2, 2, 1, 1, 1, 0, -1]` | The dynamic array being operated on. |
| `operations` | `int` | `0` | Counter for operations performed. |
| `sorted` | `bool` | `true` (reset per loop) | Flag to check if array is non-decreasing. |
| `minSum` | `int` | `INT_MAX` | Tracks the lowest sum found in current scan. |
| `index` | `int` | `-1` | Stores the index of the pair to be merged. |
| `s` | `int` | Undefined | Temporary storage for pair sum. |
| `i` | `int` | `0` | Loop iterator. |

### 2. Data Structure: Input Vector `nums` (Initial State)

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Value** | 2 | 2 | -1 | 3 | -2 | 2 | 1 | 1 | 1 | 0 | -1 |

---

## PHASE 2 — EXECUTION TRACE

#### [Step 1] Initialization
* `operations` initialized to **0**.

### OUTER LOOP — Pass 1
**Current Array:** `[2, 2, -1, 3, -2, 2, 1, 1, 1, 0, -1]`

#### Sub-Routine: Check Sorted Status
* **Goal:** Determine if `nums[i] <= nums[i+1]` for all `i`.
* **Flag:** `sorted` = `true`.

| Iteration `i` | Comparison (`nums[i]` > `nums[i+1]`) | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 2` | 2 > 2 | `FALSE` | Continue |
| 1 | `2 > -1` | 2 > -1 | **TRUE** | `sorted = false`; **BREAK** |

**Condition Check:** `if (sorted)` is `false`. Proceed to finding min pair.

#### Sub-Routine: Find Minimum Adjacent Pair
* **Goal:** Find smallest sum `s`. On tie, keep first found (leftmost).
* **State:** `minSum` = `INT_MAX`, `index` = `-1`.

| Iteration `i` | Calculation (`nums[i] + nums[i+1]`) | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 2` | 4 | `4 < INT_MAX` | **4** | **0** |
| 1 | `2 + (-1)` | 1 | `1 < 4` | **1** | **1** |
| 2 | `-1 + 3` | 2 | `2 < 1` | No | - |
| 3 | `3 + (-2)` | 1 | `1 < 1` | No (Tie) | - |
| 4 | `-2 + 2` | 0 | `0 < 1` | **0** | **4** |
| 5 | `2 + 1` | 3 | `3 < 0` | No | - |
| 6 | `1 + 1` | 2 | `2 < 0` | No | - |
| 7 | `1 + 1` | 2 | `2 < 0` | No | - |
| 8 | `1 + 0` | 1 | `1 < 0` | No | - |
| 9 | `0 + (-1)` | -1 | `-1 < 0` | **-1** | **9** |

#### Mutation Operation
* **Target Pair:** Index 9 and 10 (Values: `0` and `-1`).
* **Sum:** `-1`.
* **Modification:**
    1. `nums[9]` = `-1`.
    2. `nums.erase(10)`.
    3. `operations`: 0 → **1**.

**New Array State:** `[2, 2, -1, 3, -2, 2, 1, 1, 1, -1]`

---

### OUTER LOOP — Pass 2
**Current Array:** `[2, 2, -1, 3, -2, 2, 1, 1, 1, -1]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 2` | 2 > 2 | `FALSE` | Continue |
| 1 | `2 > -1` | 2 > -1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair
* **State:** `minSum` = `INT_MAX`, `index` = `-1`.

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 2` | 4 | `4 < INT_MAX` | **4** | **0** |
| 1 | `2 + (-1)` | 1 | `1 < 4` | **1** | **1** |
| 2 | `-1 + 3` | 2 | `2 < 1` | No | - |
| 3 | `3 + (-2)` | 1 | `1 < 1` | No | - |
| 4 | `-2 + 2` | 0 | `0 < 1` | **0** | **4** |
| 5 | `2 + 1` | 3 | `3 < 0` | No | - |
| 6 | `1 + 1` | 2 | `2 < 0` | No | - |
| 7 | `1 + 1` | 2 | `2 < 0` | No | - |
| 8 | `1 + (-1)` | 0 | `0 < 0` | No (Tie) | - |

#### Mutation Operation
* **Target Pair:** Index 4 and 5 (Values: `-2` and `2`).
* **Sum:** `0`.
* **Modification:**
    1. `nums[4]` = `0`.
    2. `nums.erase(5)`.
    3. `operations`: 1 → **2**.

**New Array State:** `[2, 2, -1, 3, 0, 1, 1, 1, -1]`

---

### OUTER LOOP — Pass 3
**Current Array:** `[2, 2, -1, 3, 0, 1, 1, 1, -1]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 2` | 2 > 2 | `FALSE` | Continue |
| 1 | `2 > -1` | 2 > -1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair
* **State:** `minSum` = `INT_MAX`, `index` = `-1`.

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 2` | 4 | `4 < MAX` | **4** | **0** |
| 1 | `2 + (-1)` | 1 | `1 < 4` | **1** | **1** |
| 2 | `-1 + 3` | 2 | `2 < 1` | No | - |
| 3 | `3 + 0` | 3 | `3 < 1` | No | - |
| 4 | `0 + 1` | 1 | `1 < 1` | No | - |
| 5 | `1 + 1` | 2 | `2 < 1` | No | - |
| 6 | `1 + 1` | 2 | `2 < 1` | No | - |
| 7 | `1 + (-1)` | 0 | `0 < 1` | **0** | **7** |

#### Mutation Operation
* **Target Pair:** Index 7 and 8 (Values: `1` and `-1`).
* **Sum:** `0`.
* **Modification:**
    1. `nums[7]` = `0`.
    2. `nums.erase(8)`.
    3. `operations`: 2 → **3**.

**New Array State:** `[2, 2, -1, 3, 0, 1, 1, 0]`

---

### OUTER LOOP — Pass 4
**Current Array:** `[2, 2, -1, 3, 0, 1, 1, 0]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 2` | 2 > 2 | `FALSE` | Continue |
| 1 | `2 > -1` | 2 > -1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair
* **State:** `minSum` = `INT_MAX`, `index` = `-1`.

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 2` | 4 | `4 < MAX` | **4** | **0** |
| 1 | `2 + (-1)` | 1 | `1 < 4` | **1** | **1** |
| 2 | `-1 + 3` | 2 | `2 < 1` | No | - |
| 3 | `3 + 0` | 3 | `3 < 1` | No | - |
| 4 | `0 + 1` | 1 | `1 < 1` | No (Tie) | - |
| 5 | `1 + 1` | 2 | `2 < 1` | No | - |
| 6 | `1 + 0` | 1 | `1 < 1` | No (Tie) | - |

#### Mutation Operation
* **Target Pair:** Index 1 and 2 (Values: `2` and `-1`).
* **Sum:** `1`.
* **Modification:**
    1. `nums[1]` = `1`.
    2. `nums.erase(2)`.
    3. `operations`: 3 → **4**.

**New Array State:** `[2, 1, 3, 0, 1, 1, 0]`

---

### OUTER LOOP — Pass 5
**Current Array:** `[2, 1, 3, 0, 1, 1, 0]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 1` | 2 > 1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 1` | 3 | `3 < MAX` | **3** | **0** |
| 1 | `1 + 3` | 4 | `4 < 3` | No | - |
| 2 | `3 + 0` | 3 | `3 < 3` | No | - |
| 3 | `0 + 1` | 1 | `1 < 3` | **1** | **3** |
| 4 | `1 + 1` | 2 | `2 < 1` | No | - |
| 5 | `1 + 0` | 1 | `1 < 1` | No (Tie) | - |

#### Mutation Operation
* **Target Pair:** Index 3 and 4 (Values: `0` and `1`).
* **Sum:** `1`.
* **Modification:**
    1. `nums[3]` = `1`.
    2. `nums.erase(4)`.
    3. `operations`: 4 → **5**.

**New Array State:** `[2, 1, 3, 1, 1, 0]`

---

### OUTER LOOP — Pass 6
**Current Array:** `[2, 1, 3, 1, 1, 0]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 1` | 2 > 1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 1` | 3 | `3 < MAX` | **3** | **0** |
| 1 | `1 + 3` | 4 | `4 < 3` | No | - |
| 2 | `3 + 1` | 4 | `4 < 3` | No | - |
| 3 | `1 + 1` | 2 | `2 < 3` | **2** | **3** |
| 4 | `1 + 0` | 1 | `1 < 2` | **1** | **4** |

#### Mutation Operation
* **Target Pair:** Index 4 and 5 (Values: `1` and `0`).
* **Sum:** `1`.
* **Modification:**
    1. `nums[4]` = `1`.
    2. `nums.erase(5)`.
    3. `operations`: 5 → **6**.

**New Array State:** `[2, 1, 3, 1, 1]`

---

### OUTER LOOP — Pass 7
**Current Array:** `[2, 1, 3, 1, 1]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 1` | 2 > 1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 1` | 3 | `3 < MAX` | **3** | **0** |
| 1 | `1 + 3` | 4 | `4 < 3` | No | - |
| 2 | `3 + 1` | 4 | `4 < 3` | No | - |
| 3 | `1 + 1` | 2 | `2 < 3` | **2** | **3** |

#### Mutation Operation
* **Target Pair:** Index 3 and 4 (Values: `1` and `1`).
* **Sum:** `2`.
* **Modification:**
    1. `nums[3]` = `2`.
    2. `nums.erase(4)`.
    3. `operations`: 6 → **7**.

**New Array State:** `[2, 1, 3, 2]`

---

### OUTER LOOP — Pass 8
**Current Array:** `[2, 1, 3, 2]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `2 > 1` | 2 > 1 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `2 + 1` | 3 | `3 < MAX` | **3** | **0** |
| 1 | `1 + 3` | 4 | `4 < 3` | No | - |
| 2 | `3 + 2` | 5 | `5 < 3` | No | - |

#### Mutation Operation
* **Target Pair:** Index 0 and 1 (Values: `2` and `1`).
* **Sum:** `3`.
* **Modification:**
    1. `nums[0]` = `3`.
    2. `nums.erase(1)`.
    3. `operations`: 7 → **8**.

**New Array State:** `[3, 3, 2]`

---

### OUTER LOOP — Pass 9
**Current Array:** `[3, 3, 2]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `3 > 3` | 3 > 3 | `FALSE` | Continue |
| 1 | `3 > 2` | 3 > 2 | **TRUE** | `sorted = false`; **BREAK** |

#### Sub-Routine: Find Minimum Adjacent Pair

| Iteration `i` | Calculation | Result `s` | Check `s < minSum` | Update `minSum` | Update `index` |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | `3 + 3` | 6 | `6 < MAX` | **6** | **0** |
| 1 | `3 + 2` | 5 | `5 < 6` | **5** | **1** |

#### Mutation Operation
* **Target Pair:** Index 1 and 2 (Values: `3` and `2`).
* **Sum:** `5`.
* **Modification:**
    1. `nums[1]` = `5`.
    2. `nums.erase(2)`.
    3. `operations`: 8 → **9**.

**New Array State:** `[3, 5]`

---

### OUTER LOOP — Pass 10
**Current Array:** `[3, 5]`

#### Sub-Routine: Check Sorted Status
| Iteration `i` | Comparison | Values | Result | Action |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `3 > 5` | 3 > 5 | `FALSE` | Continue |

**End of Loop Check:**
* Loop completed without `break`.
* `sorted` remains **TRUE**.

**Branch Taken:** `if (sorted) break;` -> **EXIT OUTER LOOP**.

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output
```cpp
9
