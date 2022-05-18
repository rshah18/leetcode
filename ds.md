## 2. Add two numbers

* ```cpp
  
   // Definition for singly-linked list.
    struct ListNode {
        int val;
        ListNode *next;
        ListNode() : val(0), next(nullptr) {}
        ListNode(int x) : val(x), next(nullptr) {}
        ListNode(int x, ListNode *next) : val(x), next(next) {}
    };
   
  // colon operator initializes the values 
  ```

* You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. 

* Add the two numbers and return the sum as a linked list.

* ```
  Input: l1 = [2,4,3], l2 = [5,6,4]
  Output: [7,0,8]
  Explanation: 342 + 465 = 807.
  ```

```cpp
#include <iostream>

using namespace std; 

struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};



class Solution {
public:
    static ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
       int carry = 0; 
       ListNode * curr = new ListNode(0); 
       ListNode * returnVal = curr; 
       while(l1 != nullptr || l2!=nullptr){
           int numa = 0; 
           int numb = 0; 
           int sum = 0; 
           
           if(l1!=nullptr){
               numa = l1->val; 
               l1 = l1->next;
           }

           if(l2!=nullptr){
               numb = l2->val; 
               l2 = l2->next; 
           }

           ListNode * node = new ListNode; 
           
           sum = numa + numb + carry; 
           
           if(sum >= 10){
               node->val = sum % 10; 
               carry = 1;  
           } else {
               node->val = sum; 
               carry = 0; 
           }

            curr->next = node;
            curr = curr->next;      

       } 

        if(carry > 0){
            curr->next = new ListNode(carry);
        }

       return returnVal->next; 
    }
};



int main(){

    
    
    ListNode n3(3);
    ListNode n2(4, &n3);
    ListNode n1(2, &n2);

    ListNode n6(4);
    ListNode n5(6, &n6);
    ListNode n4(5, &n5);
    
    

    Solution::addTwoNumbers(&n1, &n4);

    return 0; 
}
```

* create two nodes one to keep track of the other 

* the other starts at zero outside the loop

* its next is the new node, 

* ```cpp
              curr->next = node;
              curr = curr->next;   
  ```

* 

## 1. Two sum

* To get index from iterator : `distance(nums.begin(), itr)`
* convert set to vector 

```cpp
    std::set<char> s = { 'a', 'b', 'c', 'd', 'e' };
 
    std::vector<char> v(s.begin(), s.end());
```

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly\* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.



```cpp
// O(n^2)
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

        set<int> s;
        for(auto itr1 = nums.begin(); itr1 != nums.end(); ++itr1 ){
            for(auto itr2 = nums.begin(); itr2 != nums.end(); ++itr2 ){
                    if(*itr1 + *itr2 == target){
                      if(itr1 != itr2){
                        s.emplace(distance(nums.begin(), itr1));
                        s.emplace(distance(nums.begin(), itr2));
                      }
                    }
            }
        }
        vector<int> v(s.begin(), s.end());
        return v; 
    }
};


```

* Unordered map implements hash table

* Both at() and operator[] is used to refer the element present at the given ***position***, the only difference is, at() throws out-of-range exception whereas operator[] shows **undefined behavior** i.e. if operator[] is used to find the value corresponding to key and if key is not present in unordered map, it will first insert the key into the map and then assign the default value ‘0’ corresponding to that key. . 

* ```cpp
  #include <iostream>
  #include <unordered_map>
  using namespace std;
    
  int main()
  {
      // Declaring umap to be of <string, double> type
      // key will be of string type and mapped value will
      // be of double type
      unordered_map<string, double> umap;
    
      // inserting values by using [] operator
      umap["PI"] = 3.14;
      umap["root2"] = 1.414;
      umap["root3"] = 1.732;
      umap["log10"] = 2.302;
      umap["loge"] = 1.0;
    
      // inserting value by insert function
      umap.insert(make_pair("e", 2.718));
    
      string key = "PI";
    
      // If key not found in map iterator to end is returned
      if (umap.find(key) == umap.end())
          cout << key << " not found\n\n";
    
      // If key found then iterator to that key is returned
      else
          cout << "Found " << key << "\n\n";
    
      key = "lambda";
      if (umap.find(key) == umap.end())
          cout << key << " not found\n";
      else
          cout << "Found " << key << endl;
    
      //    iterating over all value of umap
      unordered_map<string, double>:: iterator itr;
      cout << "\nAll Elements : \n";
      for (itr = umap.begin(); itr != umap.end(); itr++)
      {
          // itr works as a pointer to pair<string, double>
          // type itr->first stores the key part  and
          // itr->second stores the value part
          cout << itr->first << "  " << itr->second << endl;
       }
  }
  ```

* Binary search tree is implemented by `map` 



* Solution

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        set<int> s;
        unordered_map<int, int> table;

        for(auto it = nums.begin(); it != nums.end(); ++it){
          table[*it] = distance(nums.begin(), it);
        }

        for(auto it = nums.begin(); it != nums.end(); ++it){
            int diff =target - *it ;
            if(table.find(diff) != table.end() && table[diff] != distance(nums.begin(), it)){
              s.emplace(table[diff]);
              s.emplace(distance(nums.begin(), it));
            }
        }

        vector<int> v(s.begin(), s.end());
        return v;
    }
};
```

## 53. Maximum subarray

```cpp
int generateAllSubArray(vector<int> nums, int start, int end){
    int sum = INT32_MIN; 
    if(end == nums.size()){
        return sum ; 
    }
    else if(start > end){
        return generateAllSubArray(nums, 0, end+1); 
    } else {
        int val = 0; 
        cout<< "sub: "; 
        for(int i = start; i<= end; i++){
            //cout << nums[i] << " "; 
            val += nums[i]; 
        }
        cout << endl; 

        if(sum < val) sum = val; 

        int r = generateAllSubArray(nums, start+1, end); 
        if (r > sum){
            return r; 
        } else return sum; 
    }
}


int main(){

    vector<int> nums = {1,2,3,4,5};

    int val =   generateAllSubArray(nums, 0, 0); 
    cout << " val : " << val; 

    return 0; 
}
```



## 88. Merge Sorted Array

* You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing order**, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

  **Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing order**.

  The final sorted array should not be returned by the function, but instead be *stored inside the array* `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {

      for(int i = 0; i < n; i++){
        nums1[m+i] = nums2[i];
      }
        
      sort(nums1.begin(), nums1.end());

    }
};
```

