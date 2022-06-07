## Warm up

## Sales by Match

There is a large pile of socks that must be paired by color. Given an array of integers representing the color of each sock, determine how many pairs of socks with matching colors there are.

**Example**



There is one pair of color and one of color . There are three odd socks left, one of each color. The number of pairs is .

**Function Description**

Complete the *sockMerchant* function in the editor below.

sockMerchant has the following parameter(s):

- *int n:* the number of socks in the pile
- *int ar[n]:* the colors of each sock

**Returns**

- *int:* the number of pairs

```cpp
int sockMerchant(int n, vector<int> ar) {
    unordered_map<int, int> table; 
    int count = 0; 
    for(auto a: ar){
        table[a]++; 
    }

    for(auto m: table){
        count += m.second/2; 
    }
    
    return count; 
}
```

