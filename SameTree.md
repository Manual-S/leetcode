- 解法一

  先序遍历两棵树，依次比较每个节点的值。

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
      bool isSameTree(TreeNode* p, TreeNode* q) 
  	{
          if((p == NULL && q != NULL) || (p != NULL && q == NULL))
  		{
  			return false;
  		}
  		//preorder(p);
  		
  		return preorder(p,q);
      }
  private:
      /*一棵树的先序递归遍历*/
      bool preorder(TreeNode* p,TreeNode* q)
  	{
  		if(p != NULL && q != NULL)
  		{
  			//cout << p->val << " ";
  			if(p->val != q->val)
  			{
  				return false;
  			}        
  			return preorder(p->right,q->right) && preorder(p->left,q->left);
  		}
  		
  		if(p == NULL && q == NULL)
  		{
  			return true;
  		}
  		else
  		{
  			return false;
  		}
  	}
  };
```

  时间：2020/1/29
