- 解法

```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution 
{
public:
    ListNode* swapPairs(ListNode* head) 
	{
        if(head == NULL || head->next == NULL)
		{
			return head;
		}
		
		ListNode* phead = new ListNode(-1);  //空链表头
		ListNode* rehead = phead;  //
		phead->next = head;
		
		ListNode* pback = head->next;
		ListNode* pnext = pback->next;
		
		while(head != NULL)
		{
			phead->next = pback;
			pback->next = head;
			head->next = pnext;
			
			if(pnext == NULL || pnext->next == NULL)
			{
				return rehead->next;
			}
			
			phead = head;
			head = pnext;
			pback = head->next;
			pnext = pback->next;

		}
		
		return rehead->next;
    }
};
```
