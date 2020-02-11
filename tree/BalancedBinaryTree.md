- 解法一

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
    class Return
	{
	public:
	    Return(bool b,int h)
		{
			isAVL = b;
			height = h;
		}
		
	    bool isAVL;
        int height;		
	};

    bool isBalanced(TreeNode* root)
	{
        if(!root)
		{
			return  true;
		}

        return process(root).isAVL;
    }
	
private:
    Return process(TreeNode* root)
	{
		
		if(!root)
		{
			return Return(true,0);  //空树是平衡的
		}
		
        Return left(false,-1);
		Return right(false,-1);
		
		left = process(root->left);
		if(left.isAVL == false)
		{
			return Return(false,-1);
		}
		
		right = process(root->right);
		if(right.isAVL == false)
		{
			return Return(false,-1);
		}
		
		if(abs(left.height - right.height) <= 1)
		{
			int h = (left.height > right.height ? left.height : right.height) + 1;
		    return Return(true,h);
		}
		else
		{
			return Return(false,-1);
		}
	}
};
```
