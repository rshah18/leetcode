# 1 week prep

## Day 1

### 1. plus minus

Given an array of integers, calculate the ratios of its elements that are *positive*, *negative*, and *zero*. Print the decimal value of each fraction on a new line with places after the decimal.

**Note:** This challenge introduces precision problems. The test cases are scaled to six decimal places, though answers with absolute error of up to are acceptable.

**Example**

There are elements, two positive, two negative and one zero. Their ratios are , and . Results are printed as:

```
0.400000
0.400000
0.200000
```

```cpp
void plusMinus(vector<int> arr) {
    map<int, float> table; 
    for(auto a: arr){
        if(a < 0){
            table[-1]++;
        }
        if(a == 0){
            table[0]++;
        }
        if(a > 0){
            table[1]++;
        }
    }

    printf("%.6f\n", table[1]/arr.size()); 
    printf("%.6f\n", table[-1]/arr.size()); 
    printf("%.6f\n", table[0]/arr.size()); 

}
```

### 2. min-max sum

Given five positive integers, find the minimum and maximum values that can be calculated by summing exactly four of the five integers. Then print the respective minimum and maximum values as a single line of two space-separated long integers.

**Example**

The minimum sum is and the maximum sum is . The function prints

```
16 24
```

```cpp
void miniMaxSum(vector<int> arr) {
    vector<int> v = arr;
    sort(v.begin(), v.end());
    long min = 0; 
    long max = 0; 
    for(int i = 0; i < 4; i++){
        min+=v[i];
    }

    for(int i = 1; i < 5; i++){
        max+=v[i];
    }

    cout << min << " " << max << endl; 

}
```

#### choice of data type matters a lot 

### 3. Time conversion

Given a time in [-hour AM/PM format](https://en.wikipedia.org/wiki/12-hour_clock), convert it to military (24-hour) time.

Note: - 12:00:00AM on a 12-hour clock is 00:00:00 on a 24-hour clock.
\- 12:00:00PM on a 12-hour clock is 12:00:00 on a 24-hour clock.

**Example**

- 

  Return '12:01:00'.

- 

  Return '00:01:00'.

**Function Description**

Complete the *timeConversion* function in the editor below. It should return a new string representing the input time in 24 hour format.

timeConversion has the following parameter(s):

- *string s*: a time in hour format

**Returns**

- *string*: the time in hour format

**Input Format**

A single string that represents a time in -hour clock format (i.e.: or ).

**Constraints**

- All input times are valid

**Sample Input**

```
07:05:45PM
```

**Sample Output**

```
19:05:45
```



```cpp
string timeConversion(string s) {
    // hh:mm:ssAM
    string miltTime; 
    istringstream ss(s);
    string token;
    vector<string> ar; 
    //12:00:00AM on a 12-hour clock is 00:00:00 
    while(std::getline(ss, token, ':')) {
        ar.push_back(token);
    }

    if(s.substr(s.size()-2).compare("AM") == 0){
        // hr
        if(stoi(ar[0]) == 12){
            miltTime.append("00:");
        } else {
            miltTime.append(ar[0]); 
            miltTime.append(":");
        }
    } else {
        if(stoi(ar[0]) == 12){
            miltTime.append("12:");
        } else {
            string hr = to_string(stoi(ar[0])+12); 
            miltTime.append(hr); 
            miltTime.append(":");
        }
    }
        // min
    miltTime.append(ar[1]); 
    miltTime.append(":");
    miltTime.append(ar[2].substr(0,2)); 

    return miltTime; 

}
```

### 4. Lonely Integer

Given an array of integers, where all elements but one occur twice, find the unique element.

**Example**

The unique element is .

**Function Description**

Complete the *lonelyinteger* function in the editor below.

lonelyinteger has the following parameter(s):

- *int a[n]*: an array of integers

**Returns**

- *int:* the element that occurs only once

```cpp
int lonelyinteger(vector<int> a) {
    unordered_map<int, int> memo;
    int lonely = 0;  
    for(auto n: a){
        memo[n]++; 
    }

    for(auto m: memo){
        if(m.second == 1){
            lonely =  m.first; 
        }
    }

    return lonely; 
}
```



### 5. Diagonal difference 

Given a square matrix, calculate the absolute difference between the sums of its diagonals.

For example, the square matrix is shown below:

```
1 2 3
4 5 6
9 8 9  
```

The left-to-right diagonal = . The right to left diagonal = . Their absolute difference is .

**Function description**

Complete the function in the editor below.

diagonalDifference takes the following parameter:

- *int arr[n][m]*: an array of integers

**Return**

- *int*: the absolute diagonal difference

**Input Format**

The first line contains a single integer, , the number of rows and columns in the square matrix .
Each of the next lines describes a row, , and consists of space-separated integers .

**Constraints**

- 

**Output Format**

Return the absolute difference between the sums of the matrix's two diagonals as a single integer.

**Sample Input**

```
3
11 2 4
4 5 6
10 8 -12
```

**Sample Output**

```
15
```

```cpp
int diagonalDifference(vector<vector<int>> arr) {
    int rtl = 0; 
    int ltr = 0;
    int left = 0; 
    int right = arr[0].size()-1; 

    for(int i = 0; i < arr.size(); i++){
        ltr += arr[i][left++]; 
        rtl += arr[i][right--]; 
    }

    return abs(rtl-ltr);

}
```

## counting sort

```cpp
vector<int> countingSort(vector<int> arr) {
    vector<int> v; 
    map<int,int> memo; 
    for(auto a: arr){
        memo[a]++; 
    }

    for(auto m: memo){
		v.
    }

    return v; 
}
```

