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

## 二叉堆
二叉堆 PriorityQueue<TElement, TPriority>
 ```c#
class Cube : IComparable<Cube> {
	private int i;

	public int CompareTo(Cube other)
	{
		return this.i.CompareTo(other.i);
	}
}

class MyCompare : IComparer<int> {
	public int Compare(Cube lhsCube, Cube rhsCube) {
		//return lhsCube.i.CompareTo(rhsCube.i);
        return lhsCube.i - rhsCube.i;
	}
}

public class Solution {
    public class MyComparer : IComparer<int> {
        public int Compare(int lhs, int rhs) {
            return rhs - lhs;
        }
    }
    public int FindKthLargest(int[] nums, int k) {
        PriorityQueue<int, int> pq = new PriorityQueue<int, int>(new MyComparer());
        for (int i = 0; i < nums.Length; i++)
            pq.Enqueue(nums[i], nums[i]);

        int ans = 0;
        for (int i = 0; i < k; i++) {
            ans = pq.Dequeue();
        }
        return ans;
    }
}
 ```

## 数组
```c#
int[] ans = new int[2] {-1, -1};
int[,] direction = new int[4, 2] {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};

int n = 2;
int[][] grid = new int[n][];
grid[0] = new int[3] {2, 1, 1};
grid[1] = new int[3] {1, 1, 0};

int n = 2;
int m = 2;
int[,] grid = new int[n, m];
grid[0, 0] = 0;
grid[0, 1] = 1;
grid[1, 0] = 3;
grid[1, 1] = 4;
ans.Length
```

## 字符串
```c#
string str = "hello";
str.Lengh
str.Substring(startIndex, len);

StringBuilder track = new StringBuilder();
track.Length
track.Append();
track.Remove(beg_idx, len);
```

## List<T>
```c#
public class MyComparer : IComparer<int>
{
    public int Compare(int x, int y)
    {
        //return x.CompareTo(y);
        if (x < y) return -1;
        else if (x == y) return 0;
        else return 1;
    }
}

List<int> l = new List<T>();
List<int> nums = new List<int>() {0, 1, 2};
List<int> nums = new List<int>(src_nums); // src_nums is List
IList<IList<int>> ans = new List<IList<int>>();

int[] nums = new int[3] {1, 2, 3};
List<int> l = new List<int>(nums);

nums[0]
nums.Count;

nums.Add(val); nums.Insert(idx, val);
nums.Sort(new MyComparer());
nums.RemoveAt(idx); nums.Remove(val)
nums.Clear();
```

## 键值对
无序键值对：Dictionary<TKey,TValue>
有序键值对：SortedDictionary<TKey,TValue>
```c#
Dictionary<int, int> mm = new Dictionary<int, int>();
mm.Count
mm.ContainsKey(nums[i])
mm.Add(nums[i], i);

foreach (KeyValuePair<int, int> pair in dict)
    pair.Key, pair.Value
for (int i = 0; i < dict.Count; i++)
    dict.ElementAt(i).Key, dict.ElementAt(i).Value

```

## 哈希表
```c#
// HashSet<T>: 不含重复元素，无序
// SortedSet<T>: 不含重复元素，有序
HashSet<int> hs = new HashSet<int>();
HashSet<int> hs = new HashSet<int>() {1, 3, 5, 7, 9};
hs.Add(num);
hs.Contains(num);
hs.Remove(num)
foreach (int num in hs) {
    if (num > 10) {
        continue;
    }
}

// UnionWith
HashSet<int> oneNum = new HashSet<int>() {1, 3, 5, 7, 9, 10};
HashSet<int> towNum = new HashSet<int>() {2, 4, 6, 8, 10};
oneNum.UnionWith(towNum); // 重复元素不会并入 {1, 3, 5, 7, 9, 10, 2, 4, 6, 8};

HashSet<int> nums = new HashSet<int>() {1, 2, 3, 4, 5, 6};
HashSet<int> towNum = new HashSet<int>() {2, 4, 6, 8, 10};
nums.IntersectWith(towNum); // 抽取出属于两个集合的元素 {2, 4, 6}

HashSet<int> nums = new HashSet<int>() {1, 2, 3, 4, 5, 6};
HashSet<int> towNum = new HashSet<int>() {2, 4, 6, 8, 10};
nums.ExceptWith(towNum); // 抽取出不属于另一个集合的元素 {1, 3, 5}
```

## 栈
```c#
// Stack<T>
Stack<int> stack = new Stack<int>();
stack.Count
stack.Push(val);
int val = stack.Peek();
int val = stack.Pop();
stack.Clear();
stack.ToArray();
stack.ToString();

stack.Push(10);
stack.Push(20);
int[] nums = new int[stack.Count];
stack.CopyTo(nums, startIdx); // nums: {20, 10}

int tmp;
bool b = stack.TryPeek(out tmp);
bool b = stack.TryPop(out tmp);
if (b)  Debug.Log(tmp);
else Debug.Log("no elem");
```

## 队列
```c#
// 队列：Queue<T>
Queue<int> q = new Queue<int>();
q.Count
q.Enqueue(val);
int val = q.Dequeue();
int val = q.Peek();
```

## 链表
```c#
LinkedList<int> deque = new LinkedList<int>();
deque.RemoveLast();
deque.RemoveFirst();
deque.AddLast(nums[i]);
deque.AddFirst(nums[i]);
deque.First // LinkedListNode
deque.Last

deque.First.Value
deque.First.Next
deque.First.Previous
```

