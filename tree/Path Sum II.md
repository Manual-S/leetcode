# 113. Path Sum II

- 我自己错误的解法

  ```C++
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     TreeNode *left;
   *     TreeNode *right;
   *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   * };
   */
  class Solution 
  {
  public:
      vector<vector<int>> pathSum(TreeNode* root, int sum) 
  	{
          dfs(root,sum);
  		return result;
      }
  private:
      void dfs(TreeNode* root,int sum)
  	{
  		if(root != NULL)
  		{
  			sum = sum - root->val;
  			cur.push_back(root->val);
              
  			if(sum == 0 && (root->left == NULL && root->right == NULL))
  			{
  				result.push_back(cur);
  				cur.erase(cur.end() - 1);
  				return;
  			}
  			else if(root->left == NULL && root->right == NULL)
  			{
  				cur.erase(cur.end() - 1);
  				return;
  			}
  			
  			dfs(root->left,sum); 
              dfs(root->right,sum);
              //
  		}
          else
          {
              cur.erase(cur.end() - 1);
              return;
          }
  	}
  private:
      vector<int> cur;
  	vector<vector<int>> result;
  };
  ```

  正确的解法：
  
  ```C++
  /**
   * Definition for a binary tree node.
   * struct TreeNode {
   *     int val;
   *     TreeNode *left;
   *     TreeNode *right;
   *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
   * };
   */
  class Solution 
  {
  public:
      vector<vector<int>> pathSum(TreeNode* root, int sum) 
  	{
          vector<vector<int>> ans;
  		vector<int> cur;
  		pathSum(root,sum,cur,ans);
  		return ans;
      }
  private:
      void pathSum(TreeNode* root,int sum,vector<int>& cur,vector<vector<int>>& ans)
  	{
          if(root == nullptr)
  		{
  			return;
  		}
  
          if(root->left == nullptr && root->right == nullptr)
  		{
  			//叶节点
  			if(sum == root->val)
  			{
  				ans.push_back(cur);
  				ans.back().push_back(root->val);
  			}
  			return;
  		}
  		cur.push_back(root->val);
  		int new_sum = sum - root->val;
  		pathSum(root->left,new_sum,cur,ans);
  		pathSum(root->right,new_sum,cur,ans);
  		
  		cur.pop_back();
  	}
  };
  ```
  
  
  
  
