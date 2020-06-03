## 174. 地下城游戏
丑陋无比的代码：

```c++
class Solution
{
public:
	int calculateMinimumHP(vector<vector<int>>& dungeon)
	{
		int row = dungeon.size();
		int col = dungeon[0].size();
		cout << row << col;
		vector<vector<int>> dp(row, vector<int>(col));

		dp[row - 1][col - 1] = dungeon[row - 1][col - 1] > 0 ? 1 : 1 - dungeon[row - 1][col - 1];

		//初始化 最后一个横着的行
		for (int j = col - 2; j >= 0; j--)
		{
			dp[row - 1][j] = std::max(dp[row - 1][j + 1] - dungeon[row - 1][j], 1);
			//cout << "i = " << row - 1 << " j = " << j << " " << dp[row - 1][j] << endl;
		}
		if (row == 1)
		{
			return dp[0][0];
		}
		//初始化 最后一个竖着的列
		for (int i = row - 2; i >= 0; i--)
		{
			dp[i][col - 1] = std::max(dp[i + 1][col - 1] - dungeon[i][col - 1], 1);
		}

		for (int i = row - 2; i >= 0; i--)
		{
			for (int j = col - 2; j >= 0; j--)
			{
				dp[i][j] = std::max(1, std::min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j]);
				//cout << "i = " << i << " j = " << j << " " << dp[i][j] << endl;
			}
		}

		return dp[0][0];
	}
};
```
