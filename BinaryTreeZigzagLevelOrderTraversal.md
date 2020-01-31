# 103. Binary Tree Zigzag Level Order Traversal

- 解法一

  这个方法其实参考了[102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)的解法。

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) 
	{
        if(!root)
		{
			return {};
		}
		
		queue<TreeNode*> dataqueue;
		vector<vector<int>> ans;
		vector<int> curdata;
		TreeNode* nlast = NULL;
		TreeNode* last = NULL;
		TreeNode* temp = NULL;
		
		int level = 0;
		
		dataqueue.push(root);
		last = root;
		
		while(!dataqueue.empty())
		{
			temp = dataqueue.front();
			
			dataqueue.pop();
			
			//cout << temp->val << " ";
			curdata.push_back(temp->val);
			
			if(temp->left != NULL)
			{
				dataqueue.push(temp->left);
				nlast = temp->left;
			}
			
			if(temp->right != NULL)
			{
				dataqueue.push(temp->right);
				nlast = temp->right;
			}
			
			if(temp == last)
			{
				//应该换行
				if(level % 2 == 0)
				{
					ans.push_back(curdata);
				}
				else
				{
					stack<int> datastack;
					for(int i = 0;i < curdata.size();i++)
					{
						datastack.push(curdata[i]);
					}
					
					for(int i = 0;i < curdata.size();i++)
					{
						//datastack.push(curdata[i]);
						curdata[i] = datastack.top();
						datastack.pop();
					}
					ans.push_back(curdata);
				}
				
				last = nlast;
				curdata.resize(0);
				level++;
			}
		}
		
		return ans;
    }
};
```

  上面的写法中

```
					stack<int> datastack;
					for(int i = 0;i < curdata.size();i++)
					{
						datastack.push(curdata[i]);
					}
					
					for(int i = 0;i < curdata.size();i++)
					{
						//datastack.push(curdata[i]);
						curdata[i] = datastack.top();
						datastack.pop();
					}
					ans.push_back(curdata);
```

翻转`curdata`中的数据可以使用函数`reverse()`。

修改之后的代码:

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) 
	{
        if(!root)
		{
			return {};
		}
		
		queue<TreeNode*> dataqueue;
		vector<vector<int>> ans;
		vector<int> curdata;
		TreeNode* nlast = NULL;
		TreeNode* last = NULL;
		TreeNode* temp = NULL;
		
		int level = 0;
		
		dataqueue.push(root);
		last = root;
		
		while(!dataqueue.empty())
		{
			temp = dataqueue.front();
			
			dataqueue.pop();
			
			//cout << temp->val << " ";
			curdata.push_back(temp->val);
			
			if(temp->left != NULL)
			{
				dataqueue.push(temp->left);
				nlast = temp->left;
			}
			
			if(temp->right != NULL)
			{
				dataqueue.push(temp->right);
				nlast = temp->right;
			}
			
			if(temp == last)
			{
				//应该换行
				if(level % 2 == 0)
				{
					ans.push_back(curdata);
				}
				else
				{
                    reverse(curdata.begin(),curdata.end());
					ans.push_back(curdata);
				}
				
				last = nlast;
				curdata.resize(0);
				level++;
			}
		}
		
		return ans;
    }
};
```

- 解法二

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
      vector<vector<int>> zigzagLevelOrder(TreeNode* root) 
  	{
          if(!root)
  		{
  			return {};
  		}
  		
  		queue<TreeNode*> dataqueue;
  		vector<vector<int>> ans;
  		vector<int> curdata;
  		TreeNode* temp = NULL;
  		bool lefttoright = true;
  				
  		dataqueue.push(root);
  		
  		while(!dataqueue.empty())
  		{
  			int queuesize = dataqueue.size();
  			curdata.resize(queuesize);
  			
  			for(int i = 0;i < queuesize;i++)
  			{
  				temp = dataqueue.front();
  				
  				int ix = lefttoright ? i : queuesize - i - 1;
  				
  				curdata[ix] = temp->val;
                  //cout << temp->val << " ";
                  //cout << curdata[ix] << " ";
  				
  				dataqueue.pop();
  				
  				if(temp->left != NULL)
  				{
  					dataqueue.push(temp->left);
  				}
  				
  				if(temp->right != NULL)
  				{
  					dataqueue.push(temp->right);
  				}
  			}
  			//cout << curdata.size() << " ";
  			ans.push_back(curdata);
  			lefttoright = !lefttoright;
  			//curdata.clear();
  		}
  		
  		return ans;
      }
  };
  ```

  
