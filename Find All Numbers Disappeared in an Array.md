# Find All Numbers Disappeared in an Array

## LINK :-  [LeetCode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)


## SOLUTION 

```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        // Step 1: (Marking Presence)

        for(int i = 0; i < nums.size(); i++) {
            int index = abs(nums[i]) - 1;
            if(nums[index] > 0) {
                nums[index] = -nums[index];
            }
        }
        
        // Step 2: (Finding Missing)
        vector<int> res;
        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] > 0) {                
                res.push_back(i + 1);
            }
        }
        
        return res;
    }
};


```

## DRY RUN


---

## PHASE 0 — SANITY & SEMANTICS CHECK

**Input:**

```
nums = [4, 3, 2, 7, 8, 2, 3, 1]
n = 8
```

**Core Logic:**

1. Use values as indices: `index = |nums[i]| - 1`
2. Negate the value at that index to mark the number as **seen**
3. In a second pass, indices that remain **positive** correspond to missing numbers (`index + 1`)

---

## PHASE 1 — INITIAL STATE

| Variable      | Value                      |
| ------------- | -------------------------- |
| `nums`        | `[4, 3, 2, 7, 8, 2, 3, 1]` |
| `nums.size()` | `8`                        |
| `res`         | `[]`                       |

---

## PHASE 2 — STEP 1: MARKING PRESENCE

We iterate through the array once. For each value `x`, we go to index `x - 1` and flip the sign to **negative** (if not already).

| Step | i | nums[i] | abs(nums[i]) - 1 (index) | nums[index] before | nums[index] > 0 | nums[index] after |
| ---- | - | ------- | ------------------------ | ------------------ | --------------- | ----------------- |
| 1    | 0 | 4       | 3                        | 7                  | TRUE            | -7                |
| 2    | 1 | 3       | 2                        | 2                  | TRUE            | -2                |
| 3    | 2 | 2       | 1                        | 3                  | TRUE            | -3                |
| 4    | 3 | 7       | 6                        | 3                  | TRUE            | -3                |
| 5    | 4 | 8       | 7                        | 1                  | TRUE            | -1                |
| 6    | 5 | 2       | 1                        | -3                 | FALSE           | -3                |
| 7    | 6 | 3       | 2                        | -2                 | FALSE           | -2                |
| 8    | 7 | 1       | 0                        | 4                  | TRUE            | -4                |

**Array State after Step 1:**

```
[-4, -3, -2, -7, 8, 2, -3, -1]
```

---

## PHASE 2 — STEP 2: FINDING MISSING NUMBERS

We iterate through the modified array. Any index `i` where `nums[i]` is **positive** indicates that the number `i + 1` was never encountered.

| Step | i | nums[i] | nums[i] > 0 | res state | Action                 |
| ---- | - | ------- | ----------- | --------- | ---------------------- |
| 1    | 0 | -4      | FALSE       | `[]`      | Skip                   |
| 2    | 1 | -3      | FALSE       | `[]`      | Skip                   |
| 3    | 2 | -2      | FALSE       | `[]`      | Skip                   |
| 4    | 3 | -7      | FALSE       | `[]`      | Skip                   |
| 5    | 4 | 8       | TRUE        | `[5]`     | `res.push_back(4 + 1)` |
| 6    | 5 | 2       | TRUE        | `[5, 6]`  | `res.push_back(5 + 1)` |
| 7    | 6 | -3      | FALSE       | `[5, 6]`  | Skip                   |
| 8    | 7 | -1      | FALSE       | `[5, 6]`  | Skip                   |

---

## PHASE 3 — FINAL STATE & VALIDATION

### 1. Final Output

```
[5, 6]
```

### 2. Final State Snapshot

```
nums = [-4, -3, -2, -7, 8, 2, -3, -1]
res  = [5, 6]
```

### 3. Operation Counters

| Metric      | Count | Details                      |
| ----------- | ----- | ---------------------------- |
| Passes      | 2     | One to mark, one to collect  |
| Comparisons | 16    | 8 sign checks per pass       |
| Negations   | 6     | Successful sign flips        |
| Assignments | 6     | `nums[index] = -nums[index]` |

### 4. Observed Complexity

* **Time Complexity:** `O(n)` — Linear scan with constant work per element
* **Space Complexity:** `O(1)` — In-place marking (excluding output vector)

---

**Conclusion:**
This dry run demonstrates how the in-place negation technique efficiently tracks seen numbers without extra memory, while preserving linear performance guarantees.
