# graph pattern problems

## 733 Flood fill

* An image is represented by an `m x n` integer grid `image` where `image[i][j]` represents the pixel value of the image.

  You are also given three integers `sr`, `sc`, and `newColor`. You should perform a **flood fill** on the image starting from the pixel `image[sr][sc]`.

  To perform a **flood fill**, consider the starting pixel, plus any pixels connected **4-directionally** to the starting pixel of the same color as the starting pixel, plus any pixels connected **4-directionally** to those pixels (also with the same color), and so on. Replace the color of all of the aforementioned pixels with `newColor`.

  Return *the modified image after performing the flood fill*.

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2021/06/01/flood1-grid.jpg)

  ```
  Input: image = [[1,1,1],[1,1,0],[1,0,1]], sr = 1, sc = 1, newColor = 2
  Output: [[2,2,2],[2,2,0],[2,0,1]]
  Explanation: From the center of the image with position (sr, sc) = (1, 1) (i.e., the red pixel), all pixels connected by a path of the same color as the starting pixel (i.e., the blue pixels) are colored with the new color.
  Note the bottom corner is not colored 2, because it is not 4-directionally connected to the starting pixel.
  ```

```cpp
class Solution {
public:

    void fill(vector<vector<int>>& image, int sr, int sc, int newColor, int oldColor){
      if(sr < 0 || sr >= image.size() || sc < 0 || sc >= image[sr].size()){
        return;
      }

      if(image[sr][sc] == newColor || image[sr][sc] != oldColor ) return;

      image[sr][sc] = newColor;

      fill(image, sr-1, sc, newColor, oldColor);
      fill(image, sr+1, sc, newColor, oldColor);
      fill(image, sr, sc+1, newColor, oldColor);
      fill(image, sr, sc-1, newColor, oldColor);


    }

    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        if(newColor == image[sr][sc]) return image; 
        
        fill(image, sr, sc, newColor, image[sr][sc]);
        return image;
    }
};


```

## 200. Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

 

**Example 1:**

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**

```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

 



```cpp
class Solution {
public:

    int numIslands(vector<vector<char>>& grid) {

      int num_islands = 0; 

      for(int r = 0; r < grid.size(); r++){
        for(int c = 0; c < grid.at(r).size(); c++){
          if(grid[r][c] == '1'){

            num_islands++; 

            grid[r][c] = '0'; // mark as visited 

            queue<pair<int,int>> nbrs; 
            nbrs.push({r,c});

            while(!nbrs.empty()){

              auto rc = nbrs.front(); nbrs.pop(); 
  
              int row = rc.first;
              int col = rc.second; 

              if(row -1 >=0 && grid[row-1][col] == '1'){
                nbrs.push({row-1, col}); grid[row-1][col] = '0'; 
              }

              if(row+1 < grid.size() && grid[row+1][col] == '1'){
                nbrs.push({row+1, col}); grid[row+1][col] = '0'; 
              }

              if(col -1 >= 0 && grid[row][col-1] == '1'){
                nbrs.push({row, col-1}); grid[row][col-1] = '0'; 
              }

              if(col+1 < grid[0].size() && grid[row][col+1] == '1'){
                nbrs.push({row, col+1}); grid[row][col+1] = '0'; 
              }


              
            } // while 
            
          } // if '1'
        } // for c
      } // for r




      return num_islands; 

    

    }// fun
};
```

* Time complexity : *O*(*M*×*N*) where M*M* is the number of rows and N*N* is the number of columns.
* Space complexity :*O*(*m**i**n*(*M*,*N*)) because in worst case where the grid is filled with lands, the size of queue can grow up to min(M,N*M*,*N*).

## 286. Walls and Gates

You are given an `m x n` grid `rooms` initialized with these three possible values.

- `-1` A wall or an obstacle.
- `0` A gate.
- `INF` Infinity means an empty room. We use the value `231 - 1 = 2147483647` to represent `INF` as you may assume that the distance to a gate is less than `2147483647`.

Fill each empty room with the distance to *its nearest gate*. If it is impossible to reach a gate, it should be filled with `INF`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/03/grid.jpg)

```
Input: rooms = [[2147483647,-1,0,2147483647],[2147483647,2147483647,2147483647,-1],[2147483647,-1,2147483647,-1],[0,-1,2147483647,2147483647]]
Output: [[3,-1,0,1],[2,2,1,-1],[1,-1,2,-1],[0,-1,3,4]]
```

**Example 2:**

```
Input: rooms = [[-1]]
Output: [[-1]]
```

 