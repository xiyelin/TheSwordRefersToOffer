#### 替换空格

	题目：请实现一个函数，把字符串中的每个空格替换成%20。
	
	例如：输入 "we are happy." ，则输出 "we%20are%20happy."。
	
	
<br>

	思路一：如果不允许创建新的空间，只能在原数组上修改，有两种方式，一种是从前向后遍历，遇到空格替换，但是这种
	
		   方法的时间复杂度为0(N^2)；另一种思路是O(N)。
		   
	
	思路二：那就是可以创建新的空间，从前往后遍历，遇到非空格，直接push_back(x)，遇到空格就 += “%20”；这种方式的
	
	       前提是使用C++中的string对象才可以。


<br>

#### 代码

```cpp

		方法一：不开辟新空间，时间复杂度为O(N)
	
		void ReplaceBlank(char* str, int length)
		{
			assert(str);
			assert(length > 0);
		
			int BlankNum = 0;
			char* strTmp = str;
		
			while (*strTmp != '\0')                            //统计空格
			{
				if (*strTmp == ' ')
					++BlankNum;
		
				++strTmp;
			}
		
			int newLength = strlen(str) + 1 + BlankNum * 2;    
		
			if (length < newLength)
			{
				printf("数组容量不够！\n");
				return;
			}
		
			char* strTail = str + strlen(str) + 1;             //指向字符串的结尾
			char* arrayTail = str + newLength;                 //指向数组的结尾
		
			while (BlankNum)
			{
				if (*strTail != ' ')                           //非空格字符向后移动
				{
					*arrayTail = *strTail;
					--strTail;
					--arrayTail;
				}
				else                                           //替换空格
				{
					*arrayTail-- = '0';
					*arrayTail-- = '2';
					*arrayTail-- = '%';
		
					--strTail;
					--BlankNum;
				}
			}
		}
		
		
		
```


```cpp

		方法二：开辟新的空间，时间复杂度为O(N)
	
		void ReplaceBlank(const string& str, string& ret)
		{
			int i = 0;
		
			while (str[i] != '\0')
			{
				if (str[i] != ' ')
					ret.push_back(str[i]);
				else
					ret += "%20";
		
				++i;
			}
			ret.push_back('\0');
		}
		
		
```
	       
