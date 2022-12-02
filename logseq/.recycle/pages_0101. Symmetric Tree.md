- [[divide and conquer]]
- 由根節點進去後, 狀況分三
	- 1. 子節點有NULL -> 比較左右兩邊是否一樣NULL
	- 2. 子節點有值 -> 比較左右兩邊值是否一樣
		- 如果一樣就繼續往下一層比 -> 兩個子節點要比(left->left, right->right) && (left->right, right->left)
		  #+BEGIN_TIP
		  開頭root只有一個點略有不同, 實際上就邏輯一值都只有比較自己與對象以及下一層兩個子節點
		   #+END_TIP
	- 3. 子節點值不一樣 -> 一定錯
-
- ```C++
  class Solution {
  public:
      bool checkSymmetric(TreeNode* left, TreeNode* right)
      {
          if(left == NULL || right == NULL)
              return left == right;
          else if(left->val == right->val)
              return checkSymmetric(left->left, right->right) && checkSymmetric(left->right, right->left);
          else
              return false;
      }
      
      bool isSymmetric(TreeNode* root) {
          if(root == NULL) return 1;
          return checkSymmetric(root->left, root->right);        
      }
  };
  ```