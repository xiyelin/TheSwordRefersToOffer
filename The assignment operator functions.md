### 赋值运算符函数

<br>

	给出类型CMyString的声明，请为该类型添加赋值运算符函数：

```cpp

		class CMyString
		{
		public:
			CMyString(char* pData = NULL);
			CMyString(const CMyString& str);
			~CMyString(void);
		
		private:
			char* m_pData;
		};
		
		
```


<br>
#### 实现一个赋值运算符函数应该注意以下几点：

- [x] 函数返回类型为该类型的引用，在函数结束之前，返回实例自身的引用(即*this)，以便支持链式访问(连续赋值)。

- [x] 参数为该类型的常量引用，如果采用传值方式，就会多调用一次拷贝构造函数，增加了开销。

- [x] 在赋值之前一定要释放原有的内存之后再分配新的内存，防止内存泄露。(这里注意抛出异常，内存分配失败)。

- [x] 在所有函数内部操作之前，检查是否是自己给自己赋值，如果是，直接返回。否则被释放之后就就找不到赋值的内容。


<br>
#### 解法一：

```cpp

		class CMyString
		{
		public:
			CMyString(char* pData = NULL)
			{
				if (NULL == pData)
				{
					m_pData = new char[1];
					*m_pData = '\0';
				}
				else
				{
					m_pData = new char[sizeof(pData)];
					strcpy(m_pData, pData);
				}
			}
			CMyString(const CMyString& str)
			{
				m_pData = new char[sizeof(str.m_pData)];
		
				strcpy(m_pData, str.m_pData);
			}
			~CMyString(void)
			{
				if (m_pData)
				{
					delete[] m_pData;
					m_pData = NULL;
				}
			}
			CMyString& operator=(const CMyString& str)
			{
				if (this != &str)
				{
					if (m_pData)
						delete[] m_pData;                        //在开辟新空间之前释放原来的空间
		
					m_pData = new char[sizeof(str.m_pData)];     //问题：这里可能会new失败，原有空间内容又被释放
					strcpy(m_pData, str.m_pData);
				}
		
				return *this;
			}

		
		private:
			char* m_pData;
		};
		
		
```

#### 解法二：

```cpp

		class CMyString
		{
		public:
			CMyString(char* pData = NULL)
			{
				if (NULL == pData)
				{
					m_pData = new char[1];
					*m_pData = '\0';
				}
				else
				{
					m_pData = new char[sizeof(pData)];
					strcpy(m_pData, pData);
				}
			}
			CMyString(const CMyString& str)
			{
				m_pData = new char[sizeof(str.m_pData)];
		
				strcpy(m_pData, str.m_pData);
			}
			~CMyString(void)
			{
				if (m_pData)
				{
					delete[] m_pData;
					m_pData = NULL;
				}
			}
			CMyString& operator=(const CMyString& str)
			{
				if (this != &str)
				{
					CMyString tmp(str);           //构造临时对象，出作用域会调用析构函数，
											      //在构造函数中如果new失败，直接抛出异常，这里*this还是原来的值
					char* m_tmp = tmp.m_pData;         
					tmp.m_pData = m_pData;
					m_pData = m_tmp;                   
				}
		
				return *this;
			}
		
		private:
			char* m_pData;
		};
		
		
```




