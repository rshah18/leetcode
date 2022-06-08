# DP. Memoization

## Fibonacci Sequence

```cpp
int fib(int n){
   if(n <= 2){
       return 1; 
   }
   else {
       return fib(n-1) + fib(n-2);  
   }
}
```

```js
const fib = (n) =>{
    if(n <= 2) return 1; 
    return fib(n-1) + fib(n-2); 
}

console.log(fib(7)); 
```

<img src="C:\ravi\LeetCode\img\dp1.6.7.png" alt="dp1.6.7" style="zoom:80%;" />

* Time complexity of fib function is `O(2^n)`

## Time and space complexity of recursive function 

* Analysing time complexity of a recursive function
* <img src="C:\ravi\LeetCode\img\dp2.6.7.png" alt="dp2.6.7" style="zoom:80%;" />

* Space complexity 
  * when we analyse space complexity of recursive functions We should include any of the additional stack space 
* for a function 

```js
void dib(int n){
    if(n <= 1){
        return;
    }
    dib(n-1); 
    dib(n-1); 
}
```

* Height is the distance between the root node and the furthest leaf node
* At every level we are calling the functions doubling the number of function calls 
* for `n` levels our time complexity becomes `O(2^n)`

<img src="C:\ravi\LeetCode\img\dp3.6.7.png" alt="dp3.6.7" style="zoom:80%;" />

* At any point we use only 5 stacks for `dib(5)` 
* Because after reaching five stack calls the functions returns 
* it is only after return from left one we enter the right one. 
* <img src="C:\ravi\LeetCode\img\dp4.6.7.png" alt="dp4.6.7" style="zoom:60%;" />

* Time complexity is `O(n^2)` and space complexity is `O(n)`
* <img src="C:\ravi\LeetCode\img\dp5.6.7.png" alt="dp5.6.7" style="zoom:80%;" />

* Our Fibonacci function has `O(2^n)` time complexity and `O(n)` space complexity
* <img src="C:\ravi\LeetCode\img\dp6.6.67.png" alt="dp6.6.67" style="zoom:60%;" />

## Dynamic programming definition

<img src="C:\ravi\LeetCode\img\dp7.6.7.png" alt="dp7.6.7" style="zoom:60%;" />

* When we have some larger problem, we can decompose into smaller instances of the same problem. This concept of break down is called **Dynamic Programming**

## memoization

* We store duplicate subproblems as we can get those results later on.
* To implement a memoization we pick a fast access data structure 
* Usually a HashMap or a JavaScript object
* JavaScript passes data to function by reference

#### Memoization for Fibonacci

```cpp
int fib(int n){
    // create a memo 
    static unordered_map<int, int> memo; 
    // find the number 
    auto it = memo.find(n); 
    if(it != memo.end()){
        return memo[n]; 
    }

    if(n <= 2){
        return 1; 
    }
    
    // add to the memo 
    memo[n] = fib(n-1) + fib(n-2); 

    // return from memo  
    return memo[n]; 
}

```

```js

const fib = (n, memo = {}) =>{
    // check in memo
    if(n in memo) {
        return memo[n]; 
    }

    if(n <= 2) {
        return 1;
    } 

    memo[n] = fib(n-1, memo) + fib(n-2, memo); 
    return memo[n]; 
}

console.log(fib(30)); 
```

#### Memoized solution recursion tree

1. Without Memorization 

<img src="C:\ravi\LeetCode\img\dp8.6.7.png" alt="dp8.6.7" style="zoom:60%;" />

2. With memoization

   <img src="C:\ravi\LeetCode\img\dp9.6.7.png" alt="dp9.6.7" style="zoom:60%;" />

* Overall we have roughly `2n` nodes 
* <img src="C:\ravi\LeetCode\img\dp10.6.7.png" alt="dp10.6.7" style="zoom:60%;" />

* `Fib(9)` has this structure
* New time complexity is `O(n)` and space complexity is `O(n)`

## Grid Traveller

* You are a traveller on  a 2D Grid. You begin in the top-left corner and your goal is to travel to the bottom right corner. You may only move down or right.
* In how many ways can you travel to the goal on a grid with dimensions m*n?
* 

<img src="C:\ravi\LeetCode\img\dp11.6.7.png" alt="dp11.6.7" style="zoom:60%;" />

* Problems like this. 
  * Always start with the smallest possible scenario 
    * `gridTraverler(1,1) -> 1` since start is already at end
      * do nothing
    * `gridTraveler(0,1)` -> 0
      * invalid
    * `gridTraveler(3,3)` 
      * 
  * These can be thought of as base cases and can be used to construct the larger solution

* for a `gridTraveler(3,3)` 
  * As me move down the problem reduces to `gridTraveler(2,3)` 
* <img src="C:\ravi\LeetCode\img\dp12.png" alt="dp12" style="zoom:60%;" />
* <img src="C:\ravi\LeetCode\img\dp13.png" alt="dp13" style="zoom:60%;" />

* <img src="C:\ravi\LeetCode\img\dp14.png" alt="dp14" style="zoom:60%;" />

* 

<img src="C:\ravi\LeetCode\img\dp15.png" alt="dp15" style="zoom:60%;" />

* Any problem that looks like recursion always visualize a tree
* At every recursive call we are either reducing by 1 row or by 1 column 
* From the tree structure we can already tell which tree nodes were formed by which combination of moves. 
*  which combination gives a positive answer and which moves lead us to dead end 
* <img src="C:\ravi\LeetCode\img\dp16.png" alt="dp16" style="zoom:50%;" />

* The tree looks like a binary tree because at every point there are two possible ways to traverse the the grid either down or right
* This tree is now composed of two different factors : `m` and `n`. 
* We must take in account the other parameter
* The height of the tree 
  * To do that we travel furthest and see the base case
  * There are two base cases 
    * either one of them is 0 and we return
    * Or both are 1 and we count as 1
  * There are `m+n` levels
* <img src="C:\ravi\LeetCode\img\dp17.png" alt="dp17" style="zoom:60%;" />

#### Brute force recursive solution

```js
const gridTraveller = (m,n) =>{
    if(m === 1 && n === 1) return 1; 
    if(m === 0 || n === 0) return 0;

    return gridTraveller(m-1, n) + gridTraveller(m, n-1); 
}
```



#### Making improvements to counting number of ways we can reduce the recursive 

* We can notice there are duplicate subtrees
* `2,1` is same as `1,2`
* <img src="C:\ravi\LeetCode\img\dp18.png" alt="dp18" style="zoom:70%;" />

#### Strategy 

* To solve these recursive dynamic programming problems we need a brute force solution to the original recursive problem 
* A well formed recursion 

#### For memoization 

* We take the exact return recursive statement and assign it to the  `memo[key]`
* and return that value based key 
* 

#### Solution

```js
const gridTraveller = (m,n, memo={}) =>{
    let key = m + ','+n; 
    if(key in memo) return memo[key]; 
    if(m === 1 && n === 1) return 1; 
    if(m === 0 || n === 0) return 0;

    memo[key] = gridTraveller(m-1, n, memo) + gridTraveller(m, n-1, memo); 
    return memo[key]; 
}
```



* A pair cannot be used as key in unordered_list 

* ```cpp
  // wrong solution
  int gridTraveller(int n, int m){
      // create memo table 
      static unordered_map<pair<int, int>, int> memo; 
      // find the pair
      auto it = memo.find({n, m}); 
      if(it != memo.end()){
          return memo[{n,m}]; 
      }
  
      if(m == 1 && n == 1) return 1; 
  
      if(m == 0 || n == 1) return 0;
  
      memo[{n,m}] = gridTraveller(m-1, n) + gridTraveller(m, n-1); 
  }
  ```

```cpp

int gridTraveller(int n, int m){
    // crate a key 
    string key = to_string(n) + " , "+ to_string(m);
    // create memo table 
    static unordered_map<string, int> memo; 
    // find the pair
    auto it = memo.find(key); 
    if(it != memo.end()){
        return memo[key]; 
    }

    if(m == 1 && n == 1) return 1; 

    if(m == 0 || n == 0) return 0;

    memo[key] = gridTraveller(m-1, n) + gridTraveller(m, n-1); 
    return memo[key]; 
}

```





* 

