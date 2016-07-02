#### 从尾到头打印单链表

```cpp

 	单链表的结构：
 	
 	template<class T>
 	struct ListNode
 	{
 		T _data;                      //数据域
 		ListNode<T>* _next;           //指向下一个节点的指针域
 	};
 	
 
```


	分析：单链表，只能从前往后遍历，而不能从后往前走。如果该题说可以破坏原来的链表结构，我们可以将指针的指向反向。
	
	     但是，对于打印来说，一般不允许破坏原链表的结构。要想打印，我们必须遍历一次，要逆序，让我们想到先进后出的
	     
	     结构，所以我们可以利用栈来实现。除此之外，栈可以用来模拟函数栈帧，所以我们还可以用递归来实现，但是，如果
	     
	     链表长度太长，递归效率就会变得很低，甚至会导致栈溢出，程序崩溃。
	     
	     
<br>


#### 代码

```cpp

		# include <iostream>
		using namespace std;
		# include <stack>
		# include "vld.h"
		
		template<class T>
		struct ListNode
		{
			T _data;
			ListNode<T>* _next;
		
			ListNode(const T& x = T())
				:_data(x)
				, _next(NULL)
			{}
		};
		
		template<class T>
		class List
		{
			typedef ListNode<T> Node;
		public:
			List()
				:_head(NULL)
			{}
			~List()
			{
				while (_head)
				{
					Node* next = _head->_next;
					delete _head;
					_head = next;
				}
			}
		
		public:
			//顺序打印单链表
			void PrintList()
			{
				Node* cur = _head;
		
				while (cur)
				{
					cout << cur->_data << "->";
					cur = cur->_next;
				}
				cout << "NULL" << endl;
			}
		
			//尾插
			void PushBack(const T& x)
			{
				if (NULL == _head)
					_head = new Node(x);
				else
				{
					Node* cur = _head;
		
					while (cur && cur->_next)
					{
						cur = cur->_next;
					}
					cur->_next = new Node(x);
				}
			}
		
			//从尾到头打印单链表
			void FromTheBackPrintLists()
			{
				stack<T> s;
				Node* cur = _head;
		
				while (cur)
				{
					s.push(cur->_data);
					cur = cur->_next;
				}
		
				while (!s.empty())
				{
					cout << s.top() << "->";
					s.pop();
				}
				cout << "NULL" << endl;
			}
		
		private:
			Node* _head;
		};
		
		
		
```







	
