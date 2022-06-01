# Dynamic programming

* If any problem can be divided into subproblems, which in turn are divided into smaller subproblems, and if there are overlapping among these subproblems, then the solutions to these subproblems can be saved for future reference. 
*  This method of solving a solution is referred to as dynamic programming.
* Dynamic programming amounts to **breaking down an optimization problem** into simpler sub-problems, and **storing the solution to each sub-problem** so that each sub-problem is only solved once.

#### sub problems

* Sub-problems are smaller versions of the original problem
* If formulated correctly, sub-problems build on each other in order to obtain the solution to the original problem.
* In dynamic programming, after you solve each sub-problem, you must memoize, or store it

#### Fibonacci

```cpp
int fibonacci(int n){
  if(n == 0) return 0;
  if(n == 1) return 1;
  else return fibonacci(n-2) + fibonacci(n-1);
}
```

## 509. Fibonacci Numbers

* The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0` and `1`. That is,

  ```
  F(0) = 0, F(1) = 1
  F(n) = F(n - 1) + F(n - 2), for n > 1.
  ```

  Given `n`, calculate `F(n)`.

* ```cpp
  // basic solution
  class Solution {
  public:
      int fib(int n) {
        if(n == 0) return 0;
        if(n == 1) return 1;
        else return fib(n-2) + fib(n-1);
      }
  };
  ```

### Top down Approach (Memoization): TDM

* Solve for all of the sub-problems, use memoization to store the pre-computed answers, then return the answer for N*N*

* ```cpp
  class Solution {
  public:
  
      map<int, int> cache;
  
      int fibonacci(int n){
        auto it = cache.find(n);
        if(it != cache.end()){
          return it->second;
        } else {
          cache[n] = fibonacci(n-2) + fibonacci(n-1);
          return cache[n]; 
        }
  
      }
  
      int fib(int n) {
        cache[0] = 0;
        cache[1] = 1;
  
        return fibonacci(n);
      }
  };
  
  ```

### Bottom Up Approach (Tabulation)

* 