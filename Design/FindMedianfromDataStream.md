# 295 数据流的中位数

- 解法一 使用大根堆和小根堆

  ```C++
  class MedianFinder 
  {
  public:
      /** initialize your data structure here. */
      MedianFinder() 
  	{
          
      }
      
      void addNum(int num) 
  	{
          if(maxqueue.empty() || num < maxqueue.top())
  		{
  			//进入大根堆
  			maxqueue.push(num);
  		}
  		else
  		{
  			//num >= 大根堆堆顶元素
  			minqueue.push(num);
  		}
  		
  		//大根堆的元素总是要比小根堆的元素大一个 或相等
  	    if(maxqueue.size() < minqueue.size())
  		{
  			maxqueue.push(minqueue.top());
  			minqueue.pop();
  		}
          else if(maxqueue.size() - minqueue.size() == 2)
  		{
  			minqueue.push(maxqueue.top());
  			maxqueue.pop();
  		}
  		
      }
      
      double findMedian() 
  	{
          if(maxqueue.size() == minqueue.size())
  		{
  			return (double)(maxqueue.top() + minqueue.top()) / 2;
  		}
  		else
  		{
  			return (double)maxqueue.top();
  		}
      }
  private:
      priority_queue<int,vector<int>,std::less<int>> maxqueue;
  	priority_queue<int,vector<int>,std::greater<int>> minqueue;
  };
  
  /**
   * Your MedianFinder object will be instantiated and called as such:
   * MedianFinder* obj = new MedianFinder();
   * obj->addNum(num);
   * double param_2 = obj->findMedian();
   */
  ```

  时间复杂度为`O(NlonN)`。

- 解法二 使用RB tree

  ```C++
  class MedianFinder 
  {
  public:
      /** initialize your data structure here. */
      MedianFinder() 
  	{
          
      }
      
      void addNum(int num) 
  	{
  		if(data.empty())
  		{
  			data.insert(num);
  			right = data.begin();
  			left = data.begin();
  		}
          else if(data.size() % 2 == 0)
  		{
  			data.insert(num);
  			//偶数
  			if(num >= *right)
  			{
  				left++;
  			}
  			else
  			{
  				right--;
                  left = right;
  			}
  		}
  		else
  		{
  			data.insert(num);
  			//奇数
  			if(num >= *right)
  			{
  				//data.insert(num);
  				right++;
  			}
  			else
  			{
  				//data.insert(num);
  				left--;
  			}
  		}
  		
      }
      
      double findMedian() 
  	{
          //cout << *left << " " << *right << endl;
          return double(*left + *right) / 2;
      }
  private:
      multiset<int> data;
  	multiset<int>::iterator left;
  	multiset<int>::iterator right;
  };
  
  /**
   * Your MedianFinder object will be instantiated and called as such:
   * MedianFinder* obj = new MedianFinder();
   * obj->addNum(num);
   * double param_2 = obj->findMedian();
   */
  ```

  
