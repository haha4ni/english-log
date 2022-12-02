- BTS([[Queue]])
- queue的存取已層為單位, 使用queue pop出該層的node並且去存下一層level中的node
- ```C++
  class Solution {
  public:
      vector<vector<int>> levelOrder(TreeNode* root) {
          vector<vector<int>> output;
          vector<int> single;
          queue<TreeNode*> myq;
      
          if(root == NULL)return output;    
          
          myq.push(root);
          
          while (!myq.empty()) {
              single.clear();
              
              int size = myq.size();
              for(int i = 0; i<size; i++)
              {
                  TreeNode* node = myq.front();
                  
                  single.push_back(node->val);
                  if(node->left != NULL)
                      myq.push(node->left);
                  if(node->right != NULL)
                      myq.push(node->right);
                  myq.pop();
              }
              output.push_back(single);
          }
          
          return output;
      }
  };
  ```