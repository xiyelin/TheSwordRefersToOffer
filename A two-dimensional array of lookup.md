#### 二维数组中的查找

	题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。这样的二维数组
	
		 又叫做 “杨氏矩阵”。
	
		 请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
		 
<br> 
	
	分析：每次选择右上角的元素和要查找的元素做比较，如果右上角元素大于该元素，则排除该列，缩小查找的范围；
	
	     如果右上角元素小于该元素，则排除该行，向下查找；重复上述操作，如果找到则返回true,如果最后的查找
	     
	     范围为空，则返回false。
	

![image](http://hbimg.b0.upaiyun.com/61808ac120686e6267ef50cc22e925bf257ab53310052-Pvzk6X_fw658)
	     
<br>


#### 代码

```cpp

		# include <iostream>
		using namespace std;
		# include <assert.h>
		
		bool Find(int* arr, int rows, int cols, const int x)
		{
			assert(arr);
			int i = 0;
			--cols;                                				//数组下标从零开始
		
			while (rows >= 0 && cols >= 0)
			{
				if (x < arr[i*rows + cols])        				//排除一列
					--cols;
				else if (x> arr[i*rows + cols])    				//排除一行
					++i;
				else
					return true;
			}
		
			return false;
		}
		
		
		
```




	    
