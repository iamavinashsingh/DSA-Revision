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


