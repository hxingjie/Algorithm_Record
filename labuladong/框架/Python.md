# Python

```python
ord('a')  # 字符串转ASCII
chr(97)  # ASCII转字符串
"".join(word_l)  # 列表转字符串

l = len(*)
l_list.reverse()
l_list.sort()

n //= 2  # 整数除法
math.ceil(float)  # 向上取整
math.floor(float)  # 向下取整
math.int(float)  # 向0取整
math.round(float)  # 四舍五入

```

### 位运算
```python
& | >> <<
n & (n-1)  # 消去n最右边的1

```

### 数据结构
```python

q = deque()
q.append(item)
q.appendleft(item)
item = q.pop()
item = q.popleft()

my_list: list[list[int]] = list()
my_dict: dict[str, int] = dict()

my_queue: deque = deque()
my_stack: deque= deque()

my_set: set = set()

class Solution:
    class Elem:
        def __init__(self, val: int):
            self.val = val
        def __lt__(self, other):
            return self.val > other.val

    def findKthLargest(self, nums: List[int], k: int) -> int:
        sup_heapq: heapq = []
        for num in nums:
            heapq.heappush(sup_heapq, self.Elem(num))
        
        ans: int = 0
        for i in range(k):
            ans = heapq.heappop(sup_heapq).val
        
        return ans

```
