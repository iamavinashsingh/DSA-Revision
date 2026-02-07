# DRY RUN — `isPalindrome` Function

---

## TARGET CODE

```cpp
bool isPalindrome(string& s) {
    int n = s.size();
    int start = 0, end = n - 1;
    while(start <= end){
        if(s[start] != s[end]){
            return false;
        }
        start++;
        end--;
    }
    return true;
}
```

---

## INPUT CASE (PRIMARY DRY RUN)

```text
s = "racecar"
```

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category    | Status          | Details                                     |
| ----------- | --------------- | ------------------------------------------- |
| Language    | C++             | Uses `string`, index access                 |
| Compilation | Valid           | Requires `<string>`                         |
| Mutability  | Read-only logic | String passed by reference but not modified |
| Technique   | Two-pointer     | Symmetric comparison from ends              |
| Early Exit  | Yes             | Returns immediately on mismatch             |

---

## PHASE 1 — INITIAL STATE

### Variable Initialization

| Variable | Type      | Initial Value | Purpose          |
| -------- | --------- | ------------- | ---------------- |
| `s`      | `string&` | "racecar"     | Input string     |
| `n`      | `int`     | 7             | Length of string |
| `start`  | `int`     | 0             | Left pointer     |
| `end`    | `int`     | 6             | Right pointer    |

### String Layout

```
Index : 0 1 2 3 4 5 6
Char  : r a c e c a r
```

---

## PHASE 2 — EXECUTION TRACE

### Loop Condition

```
while(start <= end)
```

---

### Iteration-by-Iteration Breakdown

| Iteration | start | end | s[start] | s[end] | Comparison | Result   |
| --------- | ----- | --- | -------- | ------ | ---------- | -------- |
| 1         | 0     | 6   | 'r'      | 'r'    | Equal      | Continue |
| 2         | 1     | 5   | 'a'      | 'a'    | Equal      | Continue |
| 3         | 2     | 4   | 'c'      | 'c'    | Equal      | Continue |
| 4         | 3     | 3   | 'e'      | 'e'    | Equal      | Continue |

After each successful comparison:

```
start++
end--
```

---

### Loop Termination

After iteration 4:

```
start = 4
end   = 2
```

Condition check:

```
start <= end  →  false
```

Loop exits normally.

---

## PHASE 3 — RETURN PATH

Since **no mismatch** was found during traversal:

```cpp
return true;
```

---

## FINAL OUTPUT

```text
true
```

---

## FAILURE PATH (EARLY EXIT CASE)

### Example Input

```text
s = "racedar"
```

### Mismatch Snapshot

```
start = 2 → 'c'
end   = 4 → 'd'
```

### Execution

```cpp
if(s[start] != s[end]){
    return false;
}
```

Function terminates immediately without further checks.

---

## TIME & SPACE COMPLEXITY

| Metric           | Value         |
| ---------------- | ------------- |
| Time Complexity  | O(n/2) → O(n) |
| Space Complexity | O(1)          |

---

## EDGE CASES HANDLED

* Empty string (`""`) → `true`
* Single character (`"a"`) → `true`
* Even length strings (`"abba"`)
* Odd length strings (`"madam"`)

---

## KEY INSIGHT

This algorithm works because **palindrome symmetry** allows us to verify correctness by checking only mirrored pairs. The two-pointer method minimizes comparisons, guarantees early termination on failure, and uses constant space—making it optimal for this problem.

