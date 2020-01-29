# 96. Unique Binary Search Trees

- 递归解法

  ```
  class Solution
  {
  public:
  	int numTrees(int n)
  	{
  		return recursion(1, n);
          //return 0;
  	}
  private:
  	int recursion(int start, int end)
  	{
  		if (start > end)
  		{
  			return 1;
  		}
  
  		int result = 0;
  
  		for (int i = start; i <= end; i++)
  		{
  			int left = recursion(start, i - 1);
  			int right = recursion(i + 1, end);
  
  			result = left * right + result;
  		}
  
  		return result;
  	}
  };
  ```

  递归解法超时，是意料之中的事。

- 记忆化递归

  ```
  class Solution
  {
  public:
  	int numTrees(int n)
  	{
  		dp = vector<vector<int>>(n, vector<int>(n));
  		for (int i = 0;i < n;i++)
  		{
  			for (int j = 0;j < n;j++)
  			{
  				dp[i][j] = -1;
  			}
  		}
  		return recursion(1, n);
  	}
  private:
  	int recursion(int start, int end)
  	{
  		if (start > end)
  		{
  			return 1;
  		}
  
  		if (dp[start - 1][end - 1] != -1)
  		{
  			return dp[start - 1][end - 1];
  			//return 0;
  		}
  
  		int result = 0;
  
  		for (int i = start; i <= end; i++)
  		{
  			int left = recursion(start, i - 1);
  			int right = recursion(i + 1, end);
  
  			result = left * right + result;
  		}
  
  		dp[start - 1][end - 1] = result;
  		//dp[start][end] = 0;
  		return result;
  	}
  
  	vector<vector<int>> dp;
  };
  
  ```

  记忆化递归通过了全部测试用例。

- 动态规划思路

  ```
  class Solution
   {
  public:
      int numTrees(int n) 
  	{
          vector<int> dp(n + 1,0);
  		
  		dp[0] = 1;
  		
  		for(int i = 1;i <= n;i++)
  		{
  			for(int j = 1;j <= i;j++)
  			{
  				dp[i] = dp[i] + dp[j - 1] * dp[i - j];
  			}
  		}
  		
  		return dp[n];
      }
  };
  ```

  

- 卡特兰公式法

  ```
  class Solution 
  {
  public:
      int numTrees(int n) 
  	{
          long c = 1;
  		
  		for(int i = 1;i < n;i++)
  		{
  			c = c * (4 * i + 2) / (i + 2);
  		}
  		
  		return (int)c;
      }
  };
  ```

  
