- 解法

```C++
class Solution 
{
public:
    void rotate(vector<vector<int>>& matrix) 
	{
        int row = matrix.size();
		int col = matrix[0].size();
		
		int a = 0;
		int b = 0;
		int c = row - 1;
		int d = col - 1;
		
		while(a < c && b < d)
		{
            rotateside(a,b,c,d,matrix);			
			a++;
			b++;
			c--;
			d--;
		}
    }
private:
    void rotateside(int a,int b,int c,int d,vector<vector<int>>& matrix)
	{	
	    int num = c - a;  //num表示需要旋转的次数
		//cout << a << " " << b << " " << c << " " << d << endl;
        
        for(int i = 0;i < num;i++)
		{
		    int temp = matrix[a + i][d];
			
		    matrix[a + i][d] = matrix[a][b + i];
			
		    matrix[a][b + i] = matrix[c - i][b];
			
		    matrix[c - i][b] = matrix[c][d - i];
			
		    matrix[c][d - i] = temp;
		}	
	}
};
```
