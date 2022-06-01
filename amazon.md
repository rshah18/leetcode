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