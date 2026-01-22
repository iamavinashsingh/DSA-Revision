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

```txt
nums = [2, 2, -1, 3, -2, 2, 1, 1, 1, 0, -1]
operations = 0
n = 11 (array size)
```
---

```
First While Loop Iteration (operations = 0):
Check if array is sorted (non-decreasing):

i=0: nums[0]=2, nums[1]=2 → 2 <= 2 ✓

i=1: nums[1]=2, nums[2]=-1 → 2 > -1 ✗ (sorted = false)
Array is NOT sorted, so we proceed

Find adjacent pair with minimum sum:
Initialize: minSum = INT_MAX (2147483647), index = -1

Checking each pair:

i=0: s = nums[0] + nums[1] = 2 + 2 = 4

s(4) < minSum(2147483647)? ✓ → minSum=4, index=0

i=1: s = nums[1] + nums[2] = 2 + (-1) = 1

s(1) < minSum(4)? ✓ → minSum=1, index=1

i=2: s = nums[2] + nums[3] = -1 + 3 = 2

s(2) < minSum(1)? ✗ → no change

i=3: s = nums[3] + nums[4] = 3 + (-2) = 1

s(1) < minSum(1)? ✗ (equal) → no change (leftmost wins)

i=4: s = nums[4] + nums[5] = -2 + 2 = 0

s(0) < minSum(1)? ✓ → minSum=0, index=4

i=5: s = nums[5] + nums[6] = 2 + 1 = 3

s(3) < minSum(0)? ✗ → no change

i=6: s = nums[6] + nums[7] = 1 + 1 = 2

s(2) < minSum(0)? ✗ → no change

i=7: s = nums[7] + nums[8] = 1 + 1 = 2

s(2) < minSum(0)? ✗ → no change

i=8: s = nums[8] + nums[9] = 1 + 0 = 1

s(1) < minSum(0)? ✗ → no change

i=9: s = nums[9] + nums[10] = 0 + (-1) = -1

s(-1) < minSum(0)? ✓ → minSum=-1, index=9

Result: minSum = -1, index = 9

Replace pair at index 9:

nums[index] = nums[9] = -1

Erase nums[index+1] = nums[10]

New array: [2, 2, -1, 3, -2, 2, 1, 1, 1, -1]

operations = 1
```
---
```
Second While Loop Iteration (operations = 1):
Check if array is sorted:

i=0: 2 <= 2 ✓

i=1: 2 <= -1 ✗ (sorted = false)

Find adjacent pair with minimum sum:
minSum = INT_MAX, index = -1

Pairs in [2, 2, -1, 3, -2, 2, 1, 1, 1, -1]:

i=0: s=2+2=4 → minSum=4, index=0

i=1: s=2+(-1)=1 → minSum=1, index=1

i=2: s=-1+3=2 → no change

i=3: s=3+(-2)=1 → no change (equal)

i=4: s=-2+2=0 → minSum=0, index=4

i=5: s=2+1=3 → no change

i=6: s=1+1=2 → no change

i=7: s=1+1=2 → no change

i=8: s=1+(-1)=0 → no change (equal, leftmost wins)

Result: minSum = 0, index = 4

Replace pair at index 4:

nums[4] = 0

Erase nums[5]

New array: [2, 2, -1, 3, 0, 1, 1, 1, -1]

operations = 2
```
---

```
Third While Loop Iteration (operations = 2):
Check if array is sorted:

i=0: 2 <= 2 ✓

i=1: 2 <= -1 ✗ (sorted = false)

Find minimum sum pair in [2, 2, -1, 3, 0, 1, 1, 1, -1]:

i=0: s=4 → minSum=4, index=0

i=1: s=1 → minSum=1, index=1

i=2: s=2 → no change

i=3: s=3 → no change

i=4: s=1 → no change (equal)

i=5: s=2 → no change

i=6: s=2 → no change

i=7: s=1+(-1)=0 → minSum=0, index=7

Result: minSum = 0, index = 7

Replace pair at index 7:

nums[7] = 0

Erase nums[8]

New array: [2, 2, -1, 3, 0, 1, 1, 0]

operations = 3
```
---

```
Fourth While Loop Iteration (operations = 3):
Check if array is sorted in [2, 2, -1, 3, 0, 1, 1, 0]:

i=0: 2 <= 2 ✓

i=1: 2 <= -1 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=4 → minSum=4, index=0

i=1: s=1 → minSum=1, index=1

i=2: s=2 → no change

i=3: s=3 → no change

i=4: s=1 → no change (equal)

i=5: s=2 → no change

i=6: s=1+0=1 → no change (equal)

Result: minSum = 1, index = 1

Replace pair at index 1:

nums[1] = 1

Erase nums[2]

New array: [2, 1, 3, 0, 1, 1, 0]

operations = 4
```
---

```
Fifth While Loop Iteration (operations = 4):
Check if array is sorted in [2, 1, 3, 0, 1, 1, 0]:

i=0: 2 <= 1 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=3 → minSum=3, index=0

i=1: s=4 → no change

i=2: s=3 → no change (equal, leftmost wins)

i=3: s=1 → minSum=1, index=3

i=4: s=2 → no change

i=5: s=1+0=1 → no change (equal)

Result: minSum = 1, index = 3

Replace pair at index 3:

nums[3] = 1

Erase nums[4]

New array: [2, 1, 3, 1, 1, 0]

operations = 5
```

---

```
Sixth While Loop Iteration (operations = 5):
Check if array is sorted in [2, 1, 3, 1, 1, 0]:

i=0: 2 <= 1 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=3 → minSum=3, index=0

i=1: s=4 → no change

i=2: s=4 → no change

i=3: s=2 → no change

i=4: s=1+0=1 → minSum=1, index=4

Result: minSum = 1, index = 4

Replace pair at index 4:

nums[4] = 1

Erase nums[5]

New array: [2, 1, 3, 1, 1]

operations = 6
```
---

```
Seventh While Loop Iteration (operations = 6):
Check if array is sorted in [2, 1, 3, 1, 1]:

i=0: 2 <= 1 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=3 → minSum=3, index=0

i=1: s=4 → no change

i=2: s=4 → no change

i=3: s=2 → minSum=2, index=3

Result: minSum = 2, index = 3

Replace pair at index 3:

nums[3] = 2

Erase nums[4]

New array: [2, 1, 3, 2]

operations = 7
```

---

```
Eighth While Loop Iteration (operations = 7):
Check if array is sorted in [2, 1, 3, 2]:

i=0: 2 <= 1 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=3 → minSum=3, index=0

i=1: s=4 → no change

i=2: s=5 → no change

Result: minSum = 3, index = 0

Replace pair at index 0:

nums[0] = 3

Erase nums[1]

New array: [3, 3, 2]

operations = 8
```

---

```
Ninth While Loop Iteration (operations = 8):
Check if array is sorted in [3, 3, 2]:

i=0: 3 <= 3 ✓

i=1: 3 <= 2 ✗ (sorted = false)

Find minimum sum pair:

i=0: s=6 → minSum=6, index=0

i=1: s=5 → minSum=5, index=1

Result: minSum = 5, index = 1

Replace pair at index 1:

nums[1] = 5

Erase nums[2]

New array: [3, 5]

operations = 9
```
---

```
Tenth While Loop Iteration (operations = 9):
Check if array is sorted in [3, 5]:

i=0: 3 <= 5 ✓
Array is sorted! sorted = true

Break out of while loop.

```
---

### Final Result:

```
Return value: 9
Final array: [3, 5]

```


--
