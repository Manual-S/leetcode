- KMP解法

```C++
/*KMP算法*/
class Solution 
{
public:
    int strStr(string haystack, string needle) 
	{
        if(needle.length() == 0)
		{
			return 0;
		}
		vector<int> next(needle.length());
		
		int i = 0;
		int j = 0;
		int haystacksize = haystack.length();
		int needlesize = needle.length();
		getnext(needle,next);
                
		for(i = 0,j = 0;i < haystacksize && j < needlesize;)
		{
			if(haystack[i] == needle[j])
			{
				i++;
				j++;
			}
			else if(next[j] == -1)
			{
			    i++;
			}
			else
			{
				j = next[j];
			}
		}
		
		return j == needlesize ? (i - j) : -1;
    }
private:
    /*获取next数组*/
    void getnext(string needle,vector<int>& next)
	{
        int needlesize = needle.length();
		if(needlesize == 1)
		{
			next[0] = -1;
			return;
		}
		else if(needlesize == 2)
		{
			next[0] = -1;
			next[1] = 0;
            return;
		}
		else if(needlesize > 2)
		{
			next[0] = -1;
			next[1] = 0;
			int i = 2;
			int cn = 0;
            while(i < needlesize)
			{
				if(needle[i - 1] == needle[cn])
				{
					next[i] = cn + 1;
					cn++;
					i++;
				}
				else if(cn > 0)
				{
					cn = next[cn];
				}
				else
				{
					next[i++] = 0;
				}
			}
		}
	}
};
```
