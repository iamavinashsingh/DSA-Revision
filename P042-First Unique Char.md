# DRY RUN — `firstUniqChar` Function

---

## TARGET CODE

```cpp
class Solution {
public:
    int firstUniqChar(string s) {
        int n = s.size();
        vector<int> check(26, 0);
        for(int i = 0; i < n; i++){
            check[s[i] - 'a']++;
        }

        for(int j = 0; j < n; j++){
            if(check[s[j] - 'a'] == 1){
                return j;
            }
        }
        return -1;
    }
};
```

---

## INPUT CASE (PRIMARY DRY RUN)

```text
s = "leetcode"
```

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category      | Status             | Details                         |
| ------------- | ------------------ | ------------------------------- |
| Language      | C++                | Uses `string`, `vector<int>`    |
| Compilation   | Valid              | Requires `<string>`, `<vector>` |
| Character Set | Lowercase only     | Assumes `'a'` to `'z'`          |
| Technique     | Frequency Counting | Two-pass algorithm              |
| Determinism   | Deterministic      | Output fixed for given input    |

---

## PHASE 1 — INITIAL STATE

### Variable Initialization

| Variable | Type          | Initial Value | Purpose                     |
| -------- | ------------- | ------------- | --------------------------- |
| `s`      | `string`      | "leetcode"    | Input string                |
| `n`      | `int`         | 8             | Length of string            |
| `check`  | `vector<int>` | 26 zeros      | Frequency table for letters |

### String Layout

```
Index : 0 1 2 3 4 5 6 7
Char  : l e e t c o d e
```

---

## PHASE 2 — FREQUENCY COUNT PASS (FIRST LOOP)

### Loop

```cpp
for(int i = 0; i < n; i++)
```

### Character Mapping Logic

```
index = s[i] - 'a'
```

| i | s[i] | ASCII Calculation | Index | check[index] (after increment) |
| - | ---- | ----------------- | ----- | ------------------------------ |
| 0 | 'l'  | 'l'-'a' = 11      | 11    | 1                              |
| 1 | 'e'  | 'e'-'a' = 4       | 4     | 1                              |
| 2 | 'e'  | 4                 | 4     | 2                              |
| 3 | 't'  | 19                | 19    | 1                              |
| 4 | 'c'  | 2                 | 2     | 1                              |
| 5 | 'o'  | 14                | 14    | 1                              |
| 6 | 'd'  | 3                 | 3     | 1                              |
| 7 | 'e'  | 4                 | 4     | 3                              |

### Frequency Table Snapshot (Non-zero Only)

| Character | Count |
| --------- | ----- |
| c         | 1     |
| d         | 1     |
| e         | 3     |
| l         | 1     |
| o         | 1     |
| t         | 1     |

---

## PHASE 3 — FIRST UNIQUE CHARACTER SEARCH (SECOND LOOP)

### Loop

```cpp
for(int j = 0; j < n; j++)
```

| j | s[j] | check[s[j]-'a'] | Condition | Action   |
| - | ---- | --------------- | --------- | -------- |
| 0 | 'l'  | 1               | TRUE      | return 0 |

Loop terminates immediately on first unique character.

---

## FINAL OUTPUT

```text
0
```

---

## FAILURE CASE (NO UNIQUE CHARACTER)

### Example Input

```text
s = "aabb"
```

### Frequency Table

```
a → 2
b → 2
```

### Second Loop Result

No character satisfies `check[s[j]-'a'] == 1`

### Return Path

```cpp
return -1;
```

---

## TIME & SPACE COMPLEXITY

| Metric           | Value                |
| ---------------- | -------------------- |
| Time Complexity  | O(n)                 |
| Space Complexity | O(1) (fixed size 26) |

---

## EDGE CASES HANDLED

* Empty string (`""`) → `-1`
* All repeating characters
* First character unique
* Unique character at end of string

---

## KEY INSIGHT

This is a classic **two-pass frequency pattern**. The first pass builds global knowledge (counts), the second pass restores order awareness. This separation guarantees correctness while preserving linear time and constant space.
