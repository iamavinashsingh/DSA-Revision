# Find First and Last Position of Element in Sorted Array


```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int>ans;
        int index1=-1;
        int index2=-1;
        int n = nums.size();
        
        // First occurence 
        int start=0, end=n-1;
        while(start<=end){
            int mid = start + (end - start)/2;
            if(nums[mid]==target){
                index1 = mid;
                end =  mid -1;

            }
            else if(nums[mid]>target){
                end = mid -1;
            }
            else{
                start = mid + 1;
            }
        }
        // Second occurence 
        start=0 ;
        end=n-1;
        while(start<=end){
            int mid = start + (end - start)/2;
            if(nums[mid]==target){
                index2 = mid;
                start = mid+1;
            }
            else if(nums[mid]>target){
                end = mid -1;
            }
            else{
                start = mid + 1;
            }
        }
       


        ans.push_back(index1);
        ans.push_back(index2);
        return ans;
    }
};


```
