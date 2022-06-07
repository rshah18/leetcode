## 215. Kth Largest Element in an Array

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        unique(nums.begin(), nums.end());        
        sort(nums.begin(), nums.end()); 
        vector<int>::reverse_iterator itr = nums.rbegin();
        int i = 0;
        while(i < k-1){
            itr++; 
            i++; 
        }
        return *itr; 
    }
};
```

