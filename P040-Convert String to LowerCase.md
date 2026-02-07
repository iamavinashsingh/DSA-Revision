# DRY RUN — `toLower` Function

---

## TARGET CODE

```cpp
string toLower(string &s) {
    for(int i = 0; i < s.size(); i++){
        if(s[i] >= 'A' && s[i] <= 'Z'){
            s[i] = s[i] + 'a' - 'A';
        }
    }
    return s;
}
```

---

## INPUT CASE

```text
s = "LeEtCoDe123"
```

---

## PHASE 0 — SANITY & SEMANTICS CHECK

| Category         | Status        | Details                                      |
| ---------------- | ------------- | -------------------------------------------- |
| Language         | C++           | Uses `string` and ASCII character arithmetic |
| Compilation      | Valid         | Requires `<string>` header                   |
| Mutability       | In-place      | String passed by reference and modified      |
| Logic            | Deterministic | Each character processed independently       |
| ASCII Assumption | Required      | `'a' - 'A' == 32`                            |

---

## PHASE 1 — VARIABLE STATE

| Variable | Type      | Initial Value | Purpose                |
| -------- | --------- | ------------- | ---------------------- |
| `s`      | `string&` | "LeEtCoDe123" | Input string (mutable) |
| `i`      | `int`     | 0             | Index iterator         |

---

## PHASE 2 — EXECUTION TRACE

### Initial State

```
Index : 0 1 2 3 4 5 6 7 8 9 10
Char  : L e E t C o D e 1 2 3
```

---

### Iteration-by-Iteration Breakdown

| i  | s[i] | Condition (`'A' <= s[i] <= 'Z'`) | Action  | New s[i] |
| -- | ---- | -------------------------------- | ------- | -------- |
| 0  | 'L'  | TRUE                             | Convert | 'l'      |
| 1  | 'e'  | FALSE                            | Skip    | 'e'      |
| 2  | 'E'  | TRUE                             | Convert | 'e'      |
| 3  | 't'  | FALSE                            | Skip    | 't'      |
| 4  | 'C'  | TRUE                             | Convert | 'c'      |
| 5  | 'o'  | FALSE                            | Skip    | 'o'      |
| 6  | 'D'  | TRUE                             | Convert | 'd'      |
| 7  | 'e'  | FALSE                            | Skip    | 'e'      |
| 8  | '1'  | FALSE                            | Skip    | '1'      |
| 9  | '2'  | FALSE                            | Skip    | '2'      |
| 10 | '3'  | FALSE                            | Skip    | '3'      |

---

### Character Conversion Mechanism (ASCII Logic)

For uppercase letters:

```
s[i] = s[i] + ('a' - 'A')
     = s[i] + 32
```

Example:

```
'L' (76) → 'l' (108)
```

---

## PHASE 3 — FINAL STATE

### Final String Value

```text
"leetcode123"
```

### Return Value

```cpp
"leetcode123"
```

---

## TIME & SPACE COMPLEXITY

| Metric           | Value           |
| ---------------- | --------------- |
| Time Complexity  | O(n)            |
| Space Complexity | O(1) (in-place) |

---

## EDGE CASES HANDLED

* Already lowercase strings
* Mixed alphanumeric input
* Empty string (`s = ""`)
* Non-alphabetic characters (unchanged)

---

## KEY TAKEAWAY

This function is a textbook example of **ASCII-based character normalization**. It avoids library overhead, operates in-place, and scales linearly—exactly what you want in low-level string manipulation problems.

