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
