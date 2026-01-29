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

---

Yes! Let's explain this code like a story.

Imagine a **Classroom**.

### The Setup (First Principles)

1. **The Students (Values):** The numbers inside the array are students. Their IDs are `1, 2, 3, 4...`
2. **The Chairs (Indices):** The positions in the array are the chairs.
* Chair `0` belongs to Student `1`.
* Chair `1` belongs to Student `2`.
* Chair `2` belongs to Student `3`.
* And so on...



**The Problem:** The teacher lost the attendance sheet! We need to find out **which students are absent (missing)**.
**The Rule:** We cannot use extra paper (No extra space). We have to use the chairs we have.

---

### The Strategy: "The Paint Trick"

Since we can't write a list, we will play a game to mark attendance.

**The Game Plan:**
We walk through the classroom one by one. When we see a student (say, Student ID **3**), we don't write "3 is present" on paper.
Instead, we go to **Chair Number 2** (which belongs to Student 3) and throw **Red Paint** (make it Negative) on whoever is sitting there.

It doesn't matter *who* is sitting in Chair 2. The **Red Paint** on that chair proves that **Student 3 exists** somewhere in the room.

---

### Let's Play (The Dry Run)

**Classroom:** `[4, 3, 2, 7, 8, 2, 3, 1]`

**Turn 1:**

* You meet the first student. His ID is **4**.
* **Action:** Go to **Chair 3** (because Chair 3 belongs to ID 4).
* **Mark it:** The person sitting there is `7`. Make them **-7**.
* *Meaning: "ID 4 is present."*
* **Room:** `[4, 3, 2, -7, 8, 2, 3, 1]`

**Turn 2:**

* You meet the next student. His ID is **3**.
* **Action:** Go to **Chair 2** (because Chair 2 belongs to ID 3).
* **Mark it:** The person sitting there is `2`. Make them **-2**.
* *Meaning: "ID 3 is present."*
* **Room:** `[4, 3, -2, -7, 8, 2, 3, 1]`

**Turn 3:**

* You meet the next student. Who is it?
* It looks like **-2**. Wait! ID cards can't be negative. The paint is just a mark.
* **The Magic Glasses (`abs`):** You use `abs(-2)` to see the real ID is **2**.
* **Action:** Go to **Chair 1** (belongs to ID 2).
* **Mark it:** The person sitting there is `3`. Make them **-3**.
* *Meaning: "ID 2 is present."*
* **Room:** `[4, -3, -2, -7, 8, 2, 3, 1]`

... *Fast forward to the end of the loop* ...

**The Final Room:**
`[-4, -3, -2, -7, 8, 2, -3, -1]`

### The Result (Who is Missing?)

Now, look at the chairs one by one.

* **Chair 0:** Has `-4`. (Paint is there -> Student 1 was here).
* **Chair 1:** Has `-3`. (Paint is there -> Student 2 was here).
* **Chair 2:** Has `-2`. (Paint is there -> Student 3 was here).
* **Chair 3:** Has `-7`. (Paint is there -> Student 4 was here).
* **Chair 4:** Has **8** (Positive!).
* **Wait! No Paint?** That means nobody went to Chair 4.
* Who owns Chair 4? **Student 5**.
* **Conclusion:** Student 5 is MISSING!


* **Chair 5:** Has **2** (Positive!).
* **No Paint?** That means nobody went to Chair 5.
* Who owns Chair 5? **Student 6**.
* **Conclusion:** Student 6 is MISSING!



### Summary for the Kid

1. **Read the ID** of the current student. (Use `abs` to ignore paint).
2. **Run to the Chair** that belongs to that ID.
3. **Splash Red Paint** (Negative sign) on whoever is sitting in that chair.
4. At the end, look for the **Clean Chairs** (Positive numbers). The owners of those chairs are the missing ones!


---
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
