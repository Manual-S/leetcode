- 解法一

  这道题目要求：

  > 你能想出一个仅使用常数空间的一趟扫描算法吗？

```C++
class Solution 
{
public:
    void sortColors(vector<int>& nums) 
	{
        int length = nums.size();
		
        if(length == 0 || length == 1)
        {
            return;
        }
        
		int pivot = 1;
		
		int less = -1;
		int more = length;
		int cur = 0;
		
		while(cur != more)
		{
            cout << cur << " ";
			if(nums[cur] < pivot)
			{
				swap(nums[cur],nums[++less]);
				//less++;
				cur++;
			}
			else if(nums[cur] > pivot)
			{
				swap(nums[cur],nums[--more]);
				//more--;
			}
			else if(nums[cur] == pivot)
			{
				cur++;
			}
            
		}
    }
};
```

