# Algorithms

## 704. Binary search

```cpp
// recursive 
class Solution {
public:

    int binarySearch(vector<int> v, int start, int end, int target){
        if(start <= end){
          int mid = start + (end -start)/2;

          if(v[mid] == target){
            return mid;
          }

          if(target > v[mid]){
            return binarySearch(v, mid+1, end, target);
          }

          if(target < v[mid]){
            return binarySearch(v, start, mid-1, target);
          }
        }

        return -1;
    }

    int search(vector<int>& nums, int target) {
        return binarySearch(nums, 0, nums.size()-1, target);
    }
};
```

```cpp
// iterative 
class Solution {
public:

    int binarySearch(vector<int> v, int start, int end, int target){
        while(start <= end){
          int mid = start + (end -start)/2;

          if(v[mid] == target){
            return mid;
          }

          if(target > v[mid]){
             start = mid+1; 
          }

          if(target < v[mid]){
            end = mid-1; 
          }
        }

        return -1;
    }

    int search(vector<int>& nums, int target) {
        return binarySearch(nums, 0, nums.size()-1, target);
    }
};
```

## 278. First Bad Version

```cpp
class Solution {
public:
  
    int firstBadVersion(int n) {
          int start = 1; 
          int end = n ; 
          
          while(start < end){
              int mid  = start + (end - start)/2; 
              
              if(isBadVersion(mid)){
                  end = mid; 
              }else {
                start = mid+1; 
              }
          }
          return start; 
    }
};

```

