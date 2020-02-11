# 101. Symmetric Tree

- 以下解法有BUG

  ```
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
      bool isSymmetric(TreeNode* root) 
  	{
          LVR(root->left);
  		RVL(root->right);
  		int length1 = data1.size();
  		int length2 = data2.size();
  		if(length1 != length2)
  		{
  			return false;
  		}
  		else
  		{
  			for(int i = 0;i < length1;i++)
  			{
  				if(data1[i] != data2[i])
  				{
  					return false;
  				}
  			}
  			
  			return true;
  		}
  		
      }
  private:
      void LVR(TreeNode* root1)
  	{
  	    if(root1 != NULL)
  		{
  			LVR(root1->left);
  			//cout << root1->val << " ";
  			data1.push_back(root1->val);
  			LVR(root1->right);
  		}
  	}
  	void RVL(TreeNode* root2)
  	{
  		if(root2 != NULL)
  		{
  			RVL(root2->right);
  		    //cout << root2->val << " ";
  			data2.push_back(root2->val);
  		    RVL(root2->left);
  		}
  	}
  	vector<int> data1;
  	vector<int> data2;
  };
  ```

  测出BUG的测试用例为`[1,2,2,2,null,2]`。其左子树的遍历为`[2,2]`，右子树的遍历为`[2,2]`但是显然这并不是一棵对称的二叉树。
  

- 正确解法

    ```
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
        bool isSymmetric(TreeNode* root) 
    	{
            if(!root)
            {
                return true;
            }
            return recursion(root->left,root->right);
        }
    private:
        bool recursion(TreeNode* root1,TreeNode* root2)
    	{
    		if(root1 == NULL && root2 != NULL ||
    		   root1 != NULL && root2 == NULL)
    		{
    			return false;
    		}
    				
    		if(root1 != NULL && root2 != NULL)
    		{
    			int bool1 = false;
    			int bool2 = false;
    			int bool3 = false;
    			
    			bool1 = recursion(root1->left,root2->right);
    			if(root1->val == root2->val)
    			{
    				bool2 = true;
    			}
    			bool3 = recursion(root1->right,root2->left);
    			
    			return bool1 && bool2 && bool3;
    		}
    		
    		return true;
    	}
    	
        void LVR(TreeNode* root1)
    	{
    	    if(root1 != NULL)
    		{
    			LVR(root1->left);
    			//cout << root1->val << " ";
    			//data1.push_back(root1->val);
    			LVR(root1->right);
    		}
    	}
    	void RVL(TreeNode* root2)
    	{
    		if(root2 != NULL)
    		{
    			RVL(root2->right);
    		    //cout << root2->val << " ";
    			//data2.push_back(root2-val);
    		    RVL(root2->left);
    		}
    	}
    };
    ```

    
