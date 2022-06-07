# Binary tree problems

## 1382. Balance a Binary Search Tree

Given the `root` of a binary search tree, return *a **balanced** binary search tree with the same node values*. If there is more than one answer, return **any of them**.

A binary search tree is **balanced** if the depth of the two subtrees of every node never differs by more than `1`.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/08/10/balance1-tree.jpg)

```
Input: root = [1,null,2,null,3,null,4,null,null]
Output: [2,1,3,null,null,null,4]
Explanation: This is not the only correct answer, [3,1,4,null,2] is also correct.
```

**Example 2:**



```cpp
class Solution {
public:
    
    
    void collect(TreeNode * root, vector<TreeNode *> &c){
        if(root->left != nullptr){
          collect(root->left, c); 
        }

        c.push_back(root);
        
        if(root->right != nullptr){
          collect(root->right, c); 
        }
    }

   TreeNode * buildTree(int start, int end, vector<TreeNode *> &c ){
      if(start > end){
        return nullptr; 
      }

      int mid = (start+end)/2; 
      TreeNode * root = c[mid]; 

      root->left = buildTree(start, mid-1, c);
      root->right = buildTree( mid +1, end, c); 
      return root; 
    }
    
    TreeNode* balanceBST(TreeNode* root) {
      vector<TreeNode *> c; 
        collect(root, c);
        return buildTree(0, c.size()-1, c);
    }
};
```

## 111. Minimum depth of a binary tree

* Given a binary tree, find its minimum depth.

  The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

  **Note:** A leaf is a node with no children.

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2020/10/12/ex_depth.jpg)

  ```
  Input: root = [3,9,20,null,null,15,7]
  Output: 2
  ```

  **Example 2:**

  ```
  Input: root = [2,null,3,null,4,null,5,null,6]
  Output: 5
  ```

```cpp
// our solution wrong 
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == nullptr){
          return 0; 
        } else {
          return min(minDepth(root->left), minDepth(root->right)) +1;
        }
    }
};
```

```cpp
// correct solution 
class Solution {
public:
    int minDepth(TreeNode* root) {
        if(root == nullptr){
          return 0; 
        } 

        if(root->left == nullptr && root->right == nullptr){
          return 1; 
        }

        int min_depth = INT_MAX;
        if(root->left != nullptr){
          min_depth = min(min_depth, minDepth(root->left)); 
        }

        if(root->right != nullptr){
          min_depth = min(min_depth, minDepth(root->right)); 
        }

        return min_depth +1; 
    }
};
```

## 104. Maximum depth of binary tree

* Given the `root` of a binary tree, return *its maximum depth*.

  A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

  ```
  Input: root = [3,9,20,null,null,15,7]
  Output: 3
  ```

  **Example 2:**

  ```
  Input: root = [1,null,2]
  Output: 2
  ```

   

```cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
      if(root == nullptr){
        return 0; 
      } 

      if(root->left == nullptr && root->right == nullptr){
        return 1; 
      }

      int max_depth = INT_MIN;
      if(root->left != nullptr){
        max_depth = max(max_depth, maxDepth(root->left)); 
      }

      if(root->right != nullptr){
        max_depth = max(max_depth, maxDepth(root->right)); 
      }

      return max_depth +1; 
    }
};
```

