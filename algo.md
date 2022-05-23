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

## 35. Search Insert Position

Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You must write an algorithm with `O(log n)` runtime complexity.

* for binary search, when low is equal to high that's where the target should have been if the list were sorted 

```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int low = 0;
        int high = nums.size()- 1;
        int midval = 0;
        while(low <= high){
            int mid = low + (high - low)/2;
            midval = mid;
            if(nums[mid] == target){
              return mid;
            } else if(nums[mid] > target){
              high = mid-1;
            } else if(nums[mid] < target){
              low = mid + 1;

              // when low == high thats where it should be 
            } else if(low == high){
              return low;
            }
        }
        return low; 
    }
};

```

## 977. Squares of a Sorted Array

Given an integer array `nums` sorted in **non-decreasing** order, return *an array of **the squares of each number** sorted in non-decreasing order*.

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
      map<int, int> map;
      vector<int> v;
        for(int i = 0; i < nums.size(); i++){
            int val = nums[i]*nums[i];
            cout << i << " "<< val << endl;
            map[val]++;

        }
        for(auto a : map){
          vector<int> v2(a.second, a.first);
          v.insert(v.end(), v2.begin(), v2.end()); 
        }
        return v;
    }
};

```

* Their solution

  * iterate over the negative part in reverse, and the positive part in the forward direction.

  * ```cpp
    class Solution {
    public:
        vector<int> sortedSquares(vector<int>& nums) {
            int n = nums.size();
    
            vector<int> result(n);
    
            int left = 0;
            int right = n - 1;
    
            for (int i = n - 1; i >= 0; i--) {
                int square;
                if (abs(nums[left]) < abs(nums[right])) {
                    square = nums[right];
                    right--;
                } else {
                    square = nums[left];
                    left++;
                }
                result[i] = square * square;
            }
            return result;
        }
    };
    ```

  * 

## 189. Rotate Array

Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

* cheated solution

* ```cpp
  class Solution {
  public:
      void rotate(vector<int>& nums, int k) {
          std::rotate(nums.begin(), nums.end()-k, nums.end());
      }
  };
  ```

* ```cpp
  class Solution {
  public:
      static void rotate(vector<int>& nums, int k) {
          vector<int> v(nums); // copy of nums
  
          for(int i = 0; i < nums.size(); i++){
            int findex = (i+k)%(nums.size());
            cout << findex << endl;
            nums[findex] = v[i]; 
  
          }
  
      }
  };
  ```


#### modulo operator (a=  b%c) keeps the value between of a between zero and c-1, when b == c, value is zero 



##  283. Move Zeroes

* Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

  **Note** that you must do this in-place without making a copy of the array.

  ```cpp
  class Solution {
  public:
      static void moveZeroes(vector<int>& nums) {
        queue<int> q;
        int zeroCounter = 0;
        for(auto a: nums){
          if(a != 0){
            q.push(a);
          } else zeroCounter++;
        }
  
        for(int i = 0; i < nums.size(); i++){
          if(!q.empty()){
            nums[i] = q.front();
            q.pop();
          } else {
            if(zeroCounter != 0){
              nums[i] = 0;
            }
          }
        }
  
      }
  };
  ```

  

## 167. Two Sum II - Input Array Is Sorted

* Given a **1-indexed** array of integers `numbers` that is already ***sorted in non-decreasing order\***, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

  Return *the indices of the two numbers,* `index1` *and* `index2`*, **added by one** as an integer array* `[index1, index2]` *of length 2.*

  The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

  Your solution must use only constant extra space.

  ```cpp
  class Solution {
  public:
      static vector<int> twoSum(vector<int>& numbers, int target) {
          unordered_map<int,int> maps;
          vector<int> v;
          for(int i = 0; i < numbers.size(); i++){
              int seeking = target - numbers[i];
              cout << "seeking: " << seeking << endl;
  
              auto it = maps.find(numbers[i]);
  
              if(it == maps.end()){
                 maps[seeking] = i+1;
              }
  
              else {
                v.push_back(it->second);
                v.push_back(i+1);
                cout << " found" ;
              }
  
          }
  
          return v;
      }
  };
  ```

  ```cpp
  // their solution
  class Solution {
  public:
      vector<int> twoSum(vector<int>& numbers, int target) {
          int low = 0;
          int high = numbers.size() - 1;
          while (low < high) {
              int sum = numbers[low] + numbers[high];
                            
              if (sum == target) {
                  return {low + 1, high + 1};
              } else if (sum < target) {
                  ++low;
              } else {
                  --high;
              }
          }
          // In case there is no solution, return {-1, -1}.
          return {-1, -1};
      }
  };
  ```

  

## 344. Reverse String

* Write a function that reverses a string. The input string is given as an array of characters `s`.

  You must do this by modifying the input array [in-place](https://en.wikipedia.org/wiki/In-place_algorithm) with `O(1)` extra memory.

   

  **Example 1:**

  ```
  Input: s = ["h","e","l","l","o"]
  Output: ["o","l","l","e","h"]
  ```

```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        int low = 0; 
        int high = s.size()-1; 
        while(low <= high){
          swap(s[low], s[high]); 
          low++; 
          high--; 
        }
    }
};

```

