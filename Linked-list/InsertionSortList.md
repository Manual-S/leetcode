# 147. Insertion Sort List

- 解法一

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
      ListNode* insertionSortList(ListNode* head) 
  	{
          if(head == NULL || head->next == NULL)
  		{
  			return head;
  		}
  		
  		
  		ListNode* phead = new ListNode(-1);  //表示无效值
  		phead->next = head;
  		
  		ListNode* start = phead->next;
  		ListNode* end = phead->next;  //start end分别维护已经排好序的链表的头和尾
  		ListNode* cur = start->next;
  		ListNode* pro = phead;  //pro是start的前驱节点
  		
  		while(cur != NULL && start != NULL)
  		{
  			if(cur->val < start->val)
  			{
  				ListNode* temp = cur->next;
  				//插入到start前面
  				pro->next = cur;
  				cur->next = start;
  				end->next = temp;
  				
  				cur = temp;
  				start = phead->next;
  				pro = phead;
  				
  				if(temp == NULL)
  				{
  					return phead->next;
  				}
  			}
  			else if(cur->val >= end->val)
  			{
  				end = cur;
  				cur = cur->next;
  			}
  			else
  			{
  				start = start->next;
  				pro = pro->next;
  			}
  		}
  		
  		return phead->next;
      }
  };
  ```

  这个题目我理解的不好，其实可以申请一个新的链表头，然后把旧的链表往上挂，代码更容易实现。
  
- 简洁的解法

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
      ListNode* insertionSortList(ListNode* head) 
  	{
          if(head == NULL || head->next == NULL)
  		{
  			return head;
  		}
  		
  		ListNode* phead = new ListNode(-1);
  		phead->next = NULL;
  		ListNode* ptr = NULL;
  		ListNode* cur = phead;
  		
  		while(head != NULL)
  		{
  			ListNode* t = head->next;
              cur = phead;
  			while(cur->next && cur->next->val <= head->val)
  			{
  				cur = cur->next;
  			}
  			head->next = cur->next;
  			cur->next = head;
  			head = t;
  		}
  		
  		ptr = phead->next;
  		delete phead;
  		return ptr;
      }
  };
  ```

  
