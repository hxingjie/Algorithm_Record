```c#
无序键值对：Dictionary<TKey,TValue>
           Hashtable
有序键值对：SortedDictionary<TKey,TValue> 红黑树
           SortedList<TKey,TValue> 列表
           SortedList

栈：Stack<T>    Stack
队列：Queue<T>    Queue
链表：LinkedList<T>
  
数组：List<T> 
     ArrayList：长度可变
     Array：定长
    
HashSet<T>: 不含重复元素，无序
SortedSet<T>: 不含重复元素，有序
    
二叉堆 PriorityQueue<TElement, TPriority>

string.Substring(startIndex, len);

T.Parse(stringvariable);
variable.ToString();
Convert.ToT(variable);

ref:必须显示初始化
out:必须在内部赋值
值类型：基本数据类型、枚举类型、结构类型
引用类型：string 类 接口 数组 
    
class Cube : IComparable<Cube>
{
	private int i;

	public int CompareTo(Cube other)
	{
		return this.i - other.i;
	}
}

class MyCompare : IComparer<int>
{
	public int Compare(int lhs, int rhs)
	{
		return lhs - rhs;
	}
}
```

