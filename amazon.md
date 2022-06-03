## 12. Integer to Roman

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, `2` is written as `II` in Roman numeral, just two one's added together. `12` is written as `XII`, which is simply `X + II`. The number `27` is written as `XXVII`, which is `XX + V + II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral.

```cpp
class Solution {
public:
    string intToRoman(int num) {
      string roman;
      map<int, string> romanInt;

      romanInt[1] = 		"I",
      romanInt[4] =     "IV",
      romanInt[5] = 		"V",
      romanInt[9] = 	  "IX",
      romanInt[10] = 	  "X",
      romanInt[40] = 	  "XL",
      romanInt[50] = 	  "L";
      romanInt[90] = 	  "XC",
      romanInt[100] = 	"C";
      romanInt[400] = 	"CD",
      romanInt[500] = 	"D";
      romanInt[900] = 	"CM",
      romanInt[1000] = 	"M";

      auto it = romanInt.rbegin(); 
      while(it != romanInt.rend() && num > 0){
        while(it->first <= num){
          num -= it->first; 
          roman.append(it->second);
        }
        it++; 
      }

      return roman;
    }
};

```

- Time complexity : O(1)*O*(1).

  As there is a finite set of roman numerals, there is a hard upper limit on how many times the loop can iterate. This upper limit is `15` times, and it occurs for the number `3888`, which has a representation of `MMMDCCCLXXXVIII`. Therefore, we say the time complexity is constant, i.e. O(1)*O*(1).

- Space complexity : O(1)*O*(1).

  The amount of memory used does not change with the size of the input integer, and is therefore constant.

## 49. Group anagram

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

```cpp
// my approach  104 / 117 test cases passed.
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
      unordered_map<unsigned int, vector<string>> table;
      vector<vector<string>> strv;

      for(int i = 0; i < strs.size(); i++){
        int ascii_sum = 0;
        for(auto s: strs[i]){
          unsigned int val = int(s);
          ascii_sum += (val*val);
        }
        cout << ascii_sum << " " << strs[i] << endl;
        table[ascii_sum].push_back(strs[i]);
      }

      for(auto m: table){
        strv.push_back(m.second);
      }

      return strv;

    }
};

```

```cpp
int(character) // provides ascii value 
```

```cpp
// instead of taking a sum just sort the words and take those values 

class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
      unordered_map<string, vector<string>> table;
      vector<vector<string>> strv;

      for(int i = 0; i < strs.size(); i++){
        string temp = strs[i]; 
        sort(temp.begin(), temp.end()); 
        
        table[temp].push_back(strs[i]);
      }

      for(auto m: table){
        strv.push_back(m.second);
      }

      return strv;

    }
};
```

## 696. Count Binary Substrings

* Given a binary string `s`, return the number of non-empty substrings that have the same number of `0`'s and `1`'s, and all the `0`'s and all the `1`'s in these substrings are grouped consecutively.

  Substrings that occur multiple times are counted the number of times they occur.

   

  **Example 1:**

  ```
  Input: s = "00110011"
  Output: 6
  Explanation: There are 6 substrings that have equal number of consecutive 1's and 0's: "0011", "01", "1100", "10", "0011", and "01".
  Notice that some of these substrings repeat and are counted the number of times they occur.
  Also, "00110011" is not a valid substring because all the 0's (and 1's) are not grouped together.
  ```

* ```cpp
  // brute force 
  class Solution {
  public:
      int count = 0;
  
      void subString(string s, int start, int end){
        if(end  == s.size()){
          return;
        }
        if(start > end){
          subString(s, 0, end+1);
        }
        else if(start <= end){
          map<char, int> table;
          vector<char> vc;
          for(int i = start; i <= end; i++){
            cout << s[i] << " ";
            table[s[i]]++;
            vc.push_back(s[i]);
          }
          cout << endl;
            
          bool s1 = is_sorted(vc.begin(), vc.end()); // acending 
          bool s2 = is_sorted(vc.rbegin(), vc.rend()); // descending 
          
          if(table['0'] == table['1'] && (s1||s2)){
            cout<< " yes" << endl;
            count++; 
          }
          subString(s, start+1, end);
        }
      }
  
      int countBinarySubstrings(string s) {
  
  
        subString(s, 0, 0);
  
  
        return count;
  
  
  
      }
  };
  ```

* ```cpp
  // not workable s
  class Solution {
  public:
      int countBinarySubstrings(string s) {
          vector<int> sb;
          int count = 1;
          for(int i = 0; i < s.size(); i++){
            if(s[i-1] == s[i] ){
              count++;
            }
            else {
              sb.push_back(count);
              count = 1; 
            }
          }
  
          int ans  = 0; 
          for(int i = 1; i < sb.size(); i++){
             ans += min(sb[i-1], sb[i]); 
          }
          return ans; 
          
      }
  };
  
  ```

* 
