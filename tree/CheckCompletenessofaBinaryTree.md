- 解法一

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
    bool isCompleteTree(TreeNode* root) 
	{
		if(!root)
		{
			return true;
		}
		
        queue<TreeNode*> dataqueue;
		TreeNode* temp;
		bool isleaf = false;
		dataqueue.push(root);
		
		while(!dataqueue.empty())
		{
			temp = dataqueue.front();
			dataqueue.pop();
			//cout << temp->val << " ";
			
			if(temp->left != NULL)
			{
				dataqueue.push(temp->left);
			}
			
			if(temp->right != NULL)
			{
				dataqueue.push(temp->right);
			}
			
			if(temp->left == NULL && temp->right != NULL)
			{
				return false;
			}
			
			if(isleaf == true && (temp->left != NULL || temp->right != NULL))
			{
				return false;
			}
			
			if( (temp->left != NULL && temp->right == NULL) 
			|| (temp->left == NULL && temp->right == NULL) )
			{
				//以后遍历的节点 都必须是叶节点
				isleaf = true;
			}
		}
		
		return true;
    }
};

```
