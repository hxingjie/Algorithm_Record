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

byte ushort uint ulong
sbyte short int long
float double decimal

int num = int.Parse("12"); string -> T
string str = num.ToString(); T -> string
num = Convert.ToInt32(str); T -> T

ref:必须显示初始化
out:必须在内部赋值
值类型：基本数据类型、枚举类型、结构类型
引用类型：string 类 接口 数组 

```

 ```c#
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

public class Solution
    {
        public class MyCompare : IComparer<int>// 比较类
        {
            public int Compare(int lhs, int rhs)
            {
                return rhs - lhs;
            }
        }
        public int[] TopKFrequent(int[] nums, int k)
        {
            MyCompare myCompare = new MyCompare();// 实例化比较类
            PriorityQueue<int, int> pq = new PriorityQueue<int, int>(myCompare);// 实例化pq
	    // <int, int>(myCompare) 分别是元素类型，优先级类型，比较类
            
            // 迭代方式1
            foreach (KeyValuePair<int,int> pair in dict)
                pq.Enqueue(pair.Key, pair.Value);
            // 迭代方式2
            for (int i = 0; i < dict.Count; i++)
            	pq.Enqueue(dict.ElementAt(i).Key,dict.ElementAt(i).Value);  

            List<int> list = new List<int>();
            for (int i = 0;i < k; i++) list.Add(pq.Dequeue());

            int[] res = list.ToArray<int>();
            return res;
        }
    }

```

