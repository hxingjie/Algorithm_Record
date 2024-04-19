## 链表

### 1.合并有序链表

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        p1: ListNode = list1
        p2: ListNode = list2

        list_ans = ListNode(-1, None)
        p = list_ans
        while p1 != None and p2 != None:
            if p1.val < p2.val:
                p.next = p1
                p1 = p1.next
            else:
                p.next = p2
                p2 = p2.next
            p = p.next
        
        p.next = p1 if p1 != None else p2

        return list_ans.next
```



### 2.反转链表

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head == None or head.next == None:
            return head

        head_n: ListNode = self.reverseList(head.next)
        p: ListNode = head_n
        while p.next != None:  # 前面的约束可以保证p != None
            p = p.next
        p.next = head
        head.next = None

        return head_n
```



### 3.分割链表

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def partition(self, head: Optional[ListNode], x: int) -> Optional[ListNode]:
        head_min: ListNode = ListNode(-1, None)
        tail_min: ListNode = head_min
        head_max: ListNode = ListNode(-1, None)
        tail_max: ListNode = head_max

        p: ListNode = head
        while p:
            if p.val < x:
                tail_min.next = p
                p = p.next
                tail_min = tail_min.next
                tail_min.next = None
            else:
                tail_max.next = p
                p = p.next
                tail_max = tail_max.next
                tail_max.next = None
        tail_min.next = head_max.next
        return head_min.next
```



### 4.删除链表中的节点

```python
class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        node.val = node.next.val
        node.next = node.next.next
```



### 5.随机链表的复制

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        head_n: Node = Node(-1, None, None)
        p_n = head_n
        p: Node = head
        node2idx: Dict[Node, int] = dict()
        idx2node: Dict[int, Node] = dict()
        idx = 0
        while p:
            cur: Node = Node(p.val, None, None)
            p_n.next = cur

            node2idx[p] = idx
            idx2node[idx] = cur
            idx += 1
    
            p = p.next
            p_n = p_n.next
        
        p_n = head_n.next
        p = head
        while p:
            if p.random == None:
                p_n.random = None
            else:
                cur_idx = node2idx[p.random]
                p_n.random = idx2node[cur_idx]
            p_n = p_n.next
            p = p.next
        
        return head_n.next
```





## 栈

### 1.有效的括号

```python
class Solution:
    def is_match(self, l: str, r: str):
        if l == '(' and r == ')':
            return True
        elif l == '{' and r == '}':
            return True
        elif l == '[' and r == ']':
            return True
        else:
            return False

    def isValid(self, s: str) -> bool:
        my_stack: deque = deque()

        for c in s:
            if c == '(' or c == '{' or c == '[':
                my_stack.append(c)
            else:
                if len(my_stack) == 0 or not self.is_match(my_stack.pop(), c):
                    return False
        
        return True if len(my_stack) == 0 else False
```



### 2.最小栈

```python
class MinStack:

    def __init__(self):
        self.my_stack: deque = deque()
        self.min_stack: deque = deque()  # 栈顶元素是my_stack中最小的元素

    def push(self, val: int) -> None:
      	# 必须是小于 && 等于
        if len(self.my_stack) == 0 or val <= self.min_stack[-1]:
            self.min_stack.append(val)

        self.my_stack.append(val)

    def pop(self) -> None:
        if self.my_stack[-1] == self.min_stack[-1]:
            self.min_stack.pop()

        self.my_stack.pop()

    def top(self) -> int:
        return self.my_stack[-1]

    def getMin(self) -> int:
        return self.min_stack[-1]
```



### 3.用栈实现队列

```python
class MyQueue:

    def __init__(self):
        self.sup_stack: Deque = deque()
        self.tmp_stack: Deque = deque()

    def push(self, x: int) -> None:
        self.sup_stack.append(x)

    def pop(self) -> int:
        while len(self.sup_stack) > 1:
            val = self.sup_stack.pop()
            self.tmp_stack.append(val)
        ans: int = self.sup_stack.pop()
        while len(self.tmp_stack) > 0:
            val = self.tmp_stack.pop()
            self.sup_stack.append(val)
        return ans

    def peek(self) -> int:
        val: int = 0
        while len(self.sup_stack) > 0:
            val = self.sup_stack.pop()
            self.tmp_stack.append(val)
        ans: int = val
        while len(self.tmp_stack) > 0:
            val = self.tmp_stack.pop()
            self.sup_stack.append(val)
        return ans

    def empty(self) -> bool:
        return True if len(self.sup_stack) == 0 else False

# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```



### 4.字符串解码

```py
class Solution:
    def decodeString(self, s: str) -> str:
        num_stack: Deque = deque()
        char_stack: Deque = deque()
        ans: str = ""
        i: int = 0
        while i < len(s):
            if s[i].isdigit():
                num = ord(s[i]) - ord('0')
                i += 1
                while s[i].isdigit():
                    num = num * 10 + (ord(s[i]) - ord('0'))
                    i += 1
                num_stack.append(num)
            elif len(num_stack) == 0 and s[i].isalpha():
                ans += s[i]
                i += 1
            elif len(num_stack) > 0 and s[i].isalpha():
                char_stack.append(s[i])
                i += 1
            elif s[i] == '[':
                char_stack.append(s[i])
                i += 1
            elif s[i] == ']':
                rc_sz: int = num_stack.pop()
                rc_list: List[str] = []
                while char_stack[-1] != '[':
                    rc_list.append(char_stack.pop())
                char_stack.pop()  # 弹出'['
                
                rc_list.reverse()
                rc_str = "".join(rc_list) * rc_sz

                if len(char_stack) > 0:
                    for c in rc_str:
                        char_stack.append(c)
                else:
                    ans += rc_str
                i += 1
            
        return ans
```



## 哈希表

### 1.有效的字母异位词

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        rec_s: List[int] = [0 for _ in range(26)]
        rec_t: List[int] = [0 for _ in range(26)]

        for c in s:
            rec_s[ord(c)-ord('a')] += 1
        for c in t:
            rec_t[ord(c)-ord('a')] += 1
        
        for i in range(26):
            if rec_s[i] != rec_t[i]:
                return False
                
        return True
```



### 2.字符串中的第一个唯一字符

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        sup_list: List[int] = [0] * 26
        for c in s:
            sup_list[ord(c)-ord('a')] += 1
        
        for i in range(len(s)):
            if sup_list[ord(s[i])-ord('a')] == 1:
                return i
        
        return -1
```



### 3.同构字符串

```py
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        s2t: Dict[str, str] = dict()
        t2s: Dict[str, str] = dict()
        for c1, c2 in zip(s, t):
            if c1 not in s2t.keys() and c2 not in t2s.keys():
                s2t[c1] = c2
                t2s[c2] = c1
            elif c1 in s2t.keys() and s2t[c1] != c2:  # 1 to more
                return False
            elif c2 in t2s.keys() and t2s[c2] != c1:  # more to 1
                return False
        
        return True
```



### 4.最长回文字符串

```python
class Solution:
    def longestPalindrome(self, s: str) -> int:
        sup_list : List[int] = [0] * 52

        for c in s:
            sup_list[ord(c)-ord('a')] += 1
        
        ans: int = 0
        tmp: int = 0
        for i in sup_list:
            if i % 2 == 0:
                ans += i
            else:
                ans += i - 1
                tmp = 1
        
        return ans + tmp
```



## 双指针



### 1.判断子序列

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        
        m: int = len(s)
        n: int = len(t)
        p1: int = 0
        p2: int = 0

        while p1 < m and p2 < n:
            if s[p1] == t[p2]:
                p1 += 1
                p2 += 1
            else:
                p2 += 1
        
        return True if p1 == m else False
```



### 2.链表的中间节点

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        sup_head: ListNode = ListNode(-1, head)
        slow: ListNode = sup_head
        fast: ListNode = sup_head

        while fast != None:
            slow = slow.next

            fast = fast.next
            if fast != None: fast = fast.next

        return slow
```



### 3.相交链表

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> Optional[ListNode]:
        sup_head1 = ListNode(-1, headA)
        sup_head2 = ListNode(-1, headB)
        p1: ListNode = sup_head1
        p2: ListNode = sup_head2

        while True:
            p1 = p1.next
            p2 = p2.next

            if p1 == p2:
                return p1

            if p1 == None: p1 = sup_head2
            elif p2 == None: p2 = sup_head1
        
        return None
```



### 4.两数之和II-输入有序数组

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l: int = 0
        r: int = len(numbers)-1

        while l < r:
            if numbers[l] + numbers[r] == target:
                return [l+1, r+1]
            elif numbers[l] + numbers[r] < target:
                l += 1
            elif numbers[l] + numbers[r] > target:
                r -= 1
        
        return [-1, -1]
```



### 5.环形链表II

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:

        sup_head: ListNode = ListNode(-1, head)
        slow: ListNode = sup_head
        fast: ListNode = sup_head

        while fast != None and fast.next != None:
            slow = slow.next
            fast = fast.next.next

            if slow == fast:  # has cycle
                slow = sup_head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        
        return None  # no cycle
```



### 6.反转字符串中的单词

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        # [' ', 't', 'h', 'e', ' ', ' ', 's', 'k', 'y', ' ']
        n: int = len(s)
        words: List[List[str]] = []
        word: List[str] = []
        for i in range(n):
            if s[i] != ' ':
                word.append(s[i])
            elif s[i] == ' ' and len(word) > 0:
                words.append(word)
                word = []
        if len(word) > 0:
            words.append(word)
        
        ans = ""
        for i in range(len(words)-1, -1, -1):
            if i == len(words)-1:
                ans += "".join(words[i])
            else:
                ans += " " + "".join(words[i])
        
        return ans
```



### 7.无重复字符的最长子串

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        sup_set: Set[str] = set()

        l: int = 0
        r: int = 0
        n: int = len(s)
        ans: int = 0
        while r < n:
            c1: str = s[r]
            r += 1

            if c1 not in sup_set:
                sup_set.add(c1)
                continue
            else:
                ans = max(ans, r-1-l)
                while c1 in sup_set:
                    c2: str = s[l]
                    l += 1
                    sup_set.remove(c2)
                sup_set.add(c1)

        ans = max(ans, r-l)
        return ans
```



### 8.三数之和

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()

        n: int = len(nums)
        ans: List[List[int]] = []
        for i in range(n-2):
            if i > 0 and nums[i] == nums[i-1]:
                continue

            l: int = i + 1
            r: int = n-1
            while l < r:
                if nums[i] + nums[l] + nums[r] == 0:
                    ans.append([nums[i], nums[l], nums[r]])
                    l += 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
                    r -= 1
                    while l < r and nums[r] == nums[r+1]:
                        r -= 1
                elif nums[i] + nums[l] + nums[r] < 0:
                    l += 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
                elif nums[i] + nums[l] + nums[r] > 0:
                    r -= 1
                    while l < r and nums[r] == nums[r+1]:
                        r -= 1

        return ans
```



### 9.滑动窗口最大值

```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        # 单调队列: 大 -> 小
        sup_queue: Deque[int] = deque()
        n: int = len(nums)
        ans: List[int] = []
        for i in range(n):
            if i < k-1:
                while len(sup_queue) > 0 and nums[i] > sup_queue[-1]:
                    sup_queue.pop()
                sup_queue.append(nums[i])
                continue
            
            while len(sup_queue) > 0 and nums[i] > sup_queue[-1]:
                sup_queue.pop()
            sup_queue.append(nums[i])
            ans.append(sup_queue[0])

            if sup_queue[0] == nums[i-k+1]:
                sup_queue.popleft()
                
        return ans
```



## 模拟

### 1.字符串相加

```python
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:

        n1: List[int] = [ord(c)-ord('0') for c in num1]
        n2: List[int] = [ord(c)-ord('0') for c in num2]
        n1.reverse()
        n2.reverse()

        if len(n1) < len(n2):
            n1.extend([0 for _ in range(len(n2)-len(n1))])
        else:
            n2.extend([0 for _ in range(len(n1)-len(n2))])

        ans: List[str] = []
        carry: int = 0
        for i in range(max(len(n1), len(n2))):
            tmp: int = n1[i] + n2[i] + carry
            ans.append(chr(tmp % 10 + ord('0')))
            carry = int(tmp / 10)
        
        if carry == 1:
            ans.append('1')

        ans.reverse()

        return "".join(ans)
```



### 2.旋转字符串

```py
class Solution:
    def create_supList(self, s: str) -> List[int]:
        n: int = len(s)
        sup_list: List[int] = [0] * n
        l: int = 0
        r: int = 1
        while r < n:
            if s[l] == s[r]:
                sup_list[r] = l + 1
                l += 1
                r += 1
            else:
                if l > 0:
                    l = sup_list[l-1]
                else:
                    sup_list[r] = 0
                    r += 1
        return sup_list  # sup_list[i]: s[0...i]最长公告前后缀长度
    
    def find_subStr(self, haystack: str, needle: str) -> int:
        m: int = len(haystack)
        n: int = len(needle)
        sup_list = self.create_supList(needle)

        i: int = 0
        j: int = 0
        while i < m and j < n:
            if haystack[i] == needle[j]:
                i += 1
                j += 1
            else:
                if j > 0: j = sup_list[j-1]
                else: i += 1

        return i - n if j == n else -1

    def rotateString(self, s: str, goal: str) -> bool:   
        if len(s) == len(goal) and self.find_subStr(goal*2, s) != -1:
            return True
        else:
            return False
```



### 3.验证栈序列

```python
class Solution:
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        sup_stack: Deque[int] = deque()
        sup_set: Set[int] = set()  # 记录是否已经入过栈
        idx_push: int = 0
        for i in range(len(popped)):
            if popped[i] not in sup_set:
                while idx_push < len(pushed):
                    val: int = pushed[idx_push]
                    idx_push += 1
                    sup_stack.append(val)
                    sup_set.add(val)
                    if val == popped[i]:
                        break
                sup_stack.pop()
            elif popped[i] == sup_stack[-1]:
                sup_stack.pop()
            elif  popped[i] != sup_stack[-1]:
                return False
        
        return True
```



### 4.Z字形变换

```python
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1: return s
        n: int = len(s)
        sup_list: List[List[str]] = ['' for _ in range(numRows)]

        cnt: int = 0  # 0 1 2 3 2 1 0
        dir: bool = True
        for c in s:
            sup_list[cnt] += c
            cnt += 1 if dir else -1
            if cnt == numRows or cnt == -1:
                cnt += -2 if dir else 2
                dir = not dir
        
        ans: str = ''
        for _s in sup_list:
            ans += _s
        
        return ans

class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows == 1: return s

        n: int = len(s)
        sup_list: List[List[str]] = [[' ' for j in range(n)] for i in range(numRows)]
        
        b: bool = True
        idx: int = 0; row: int = 0; col: int = 0
        
        while idx < n:
            if b:
                sup_list[row][col] = s[idx]
                row += 1
            else:
                sup_list[row][col] = s[idx]
                row -= 1; col += 1

            if b and row == numRows:
                b = not b; row -= 2; col += 1
            if not b and row < 0:
                b = not b; row += 2;col -= 1
            
            idx += 1

        ans: str = ""
        for i in range(numRows):
            for j in range(n):
                if sup_list[i][j] != ' ':
                    ans += sup_list[i][j]
        
        return ans
```



### 5.螺旋矩阵

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        m: int = len(matrix); n: int = len(matrix[0])
        edge_right: int = n-1; edge_down: int = m-1
        edge_left: int = 0; edge_up: int = 0

        row: int = 0
        col: int = 0
        
        ans: List[int] = []
        cnt: int = 0
        while True:
            while col <= edge_right:  # to right
                ans.append(matrix[row][col])
                cnt += 1
                col += 1
            if cnt == m*n: break
            edge_up += 1
            row += 1; col -= 1

            while row <= edge_down:  # to down
                ans.append(matrix[row][col])
                cnt += 1
                row += 1
            if cnt == m*n: break
            edge_right -= 1
            row -= 1; col -= 1

            while col >= edge_left:  # to left
                ans.append(matrix[row][col])
                cnt += 1
                col -= 1
            if cnt == m*n: break
            edge_down -= 1
            row -= 1; col += 1

            while row >= edge_up:  # to down
                ans.append(matrix[row][col])
                cnt += 1
                row -= 1
            if cnt == m*n: break
            edge_left += 1
            row += 1; col += 1

        return ans
```



### 6.螺旋矩阵II

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        ans: List[List[int]] = [[0 for j in range(n)] for i in range(n)]
        val: int = 1
        row: int = 0; col: int = 0
        e_right: int = n-1; e_down: int = n-1
        e_left: int = 0; e_up: int = 0

        while True:
            while col <= e_right:  # to right
                ans[row][col] = val
                col += 1
                val += 1
            if val > n*n: break
            e_up += 1
            row += 1; col -= 1

            while row <= e_down:  # to down
                ans[row][col] = val
                row += 1
                val += 1
            if val > n*n: break
            e_right -= 1
            row -= 1; col -= 1

            while col >= e_left:  # to left
                ans[row][col] = val
                col -= 1
                val += 1
            if val > n*n: break
            e_down -= 1
            row -= 1; col += 1

            while row >= e_up:  # to up
                ans[row][col] = val
                row -= 1
                val += 1
            if val > n*n: break
            e_left += 1
            row += 1; col += 1

        return ans
```



### 7.旋转图像

```python
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        # 0,2 -> 2,0
        # 1 4 7.   7 4 1
        # 2 5 8 -> 8 5 2
        # 3 6 9.   9 6 3
        n: int = len(matrix)
        for i in range(n):
            for j in range(n):
                if i == j: break
                tmp: int = matrix[i][j]
                matrix[i][j] = matrix[j][i]
                matrix[j][i] = tmp

        for i in range(n):
            l: int = 0; r: int = n-1
            while l < r:
                tmp: int = matrix[i][l]
                matrix[i][l] = matrix[i][r]
                matrix[i][r] = tmp
                l += 1; r -= 1

class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n: int = len(matrix)
        for i in range(n):
            for j in range(n):
                if i == j: break
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        for i in range(n):
            matrix[i].reverse()
```



### 8.字符串转换整数

```python
class Solution:
    def myAtoi(self, s: str) -> int:
        idx = 0
        while idx < len(s):
            if s[idx] == ' ':
                idx += 1
                continue
            else:
                break
        if idx == len(s): return 0
        
        isposive: int = 1
        min_val:int = -(2**31); max_val: int = 2**31-1
        num: int = 0

        if s[idx] == '+' or s[idx] == '-':
            isposive = -1 if s[idx] == '-' else 1
            idx += 1
        while idx < len(s) and s[idx].isdigit():
            num = num*10 + (ord(s[idx])-ord('0'))
            
            if num*isposive < min_val:
                return min_val
            elif num*isposive > max_val:
                return max_val

            idx += 1

        return num*isposive
```



## 查找

### 1.二分查找

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l: int = 0
        r: int = len(nums)-1

        while l <= r:
            mid: int = l + (r-l) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                l = mid + 1
            elif nums[mid] > target:
                r = mid - 1
        
        return -1
```



### 2.第一个错误版本

```py
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        # g g b b b
        l: int = 1
        r: int = n

        while l <= r:
            mid: int = l + (r-l)//2
            if isBadVersion(mid) == False:
                l = mid + 1
            elif isBadVersion(mid) == True:
                r = mid - 1
        
        return l  # b一定存在
```



### 3.寻找数组的中心下标

```python
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        n: int = len(nums)
        l_sum = 0; r_sum = sum(nums)

        for i in range(n):
            l_sum += nums[i-1] if i > 0 else 0
            r_sum -= nums[i]
            if l_sum == r_sum:
                return i

        return -1
```



### 4.寻找重复数

```py
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        n: int = len(nums)

        sup_list: List[int] = [0] * n

        for num in nums:
            sup_list[num] += 1
        
        for i in range(len(sup_list)):
            if sup_list[i] > 1:
                return i
        
        return -1

class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        n: int = len(nums)

        slow: int = 0
        fast: int = 0

        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if slow == fast:
                slow = 0
                while True:
                    slow = nums[slow]
                    fast = nums[fast]
                    if slow == fast: return slow
        
        return -1
```







## 搜索

### 1.二叉树的层序遍历

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        ans: List[List[int]] = list()
        if root == None:
            return ans
            
        sup_queue: deque[int] = deque()

        # 进队前判断
        sup_queue.append(root)
        # 进队后标记

        while len(sup_queue) > 0:
            sz: int = len(sup_queue)
            tmp_l: List[int] = list()
            for _ in range(sz):
                cur = sup_queue.popleft()

                tmp_l.append(cur.val)
                if cur.left != None:
                    sup_queue.append(cur.left)
                if cur.right != None:
                    sup_queue.append(cur.right)
            ans.append(tmp_l)
        
        return ans
```



### 2.二叉树的锯齿形层序遍历

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def zigzagLevelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        ans: List[List[int]] = list()
        if root == None: return ans

        sup_queue: Deque[TreeNode] = deque()

        sup_queue.append(root)
        
        l2r: bool = True

        while sup_queue:
            sz: int = len(sup_queue)
            tmp: List[int] = list()
            for _ in range(sz):
                cur: TreeNode = sup_queue.popleft()
                tmp.append(cur.val)

                if cur.left != None: sup_queue.append(cur.left)
                if cur.right != None: sup_queue.append(cur.right)
            if not l2r: tmp.reverse()
            l2r = not l2r
            ans.append(tmp)

        return ans
```



### 3.二叉树的最近公共祖先

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.sup_dict: Dict[TreeNode, TreeNode] = dict()
    def find_node(self, root: TreeNode, p: TreeNode, q: TreeNode):
        if root == None: return None

        if root in self.sup_dict.keys():
            return self.sup_dict[root]

        if root == p or root == q:
            self.sup_dict[root] = root
            return self.sup_dict[root]

        left = self.find_node(root.left, p, q)
        if left:
            self.sup_dict[root] = left
            return self.sup_dict[root]
        
        right = self.find_node(root.right, p, q)
        if right:
            self.sup_dict[root] = right
            return self.sup_dict[root]

        self.sup_dict[root] = None
        return self.sup_dict[root]

    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root == None: return None

        if root == p or root == q:
            return root

        left: TreeNode = self.find_node(root.left, p, q)
        right: TreeNode = self.find_node(root.right, p, q)

        if left and right:
            return root
        elif left:
            return self.lowestCommonAncestor(root.left, p, q)
        elif right:
            return self.lowestCommonAncestor(root.right, p, q)
```



### 4.二叉搜索树中第k小的元素

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.cnt: int = 0
        self.ans: int = -1
    def traverse(self, root: TreeNode, k: int):
        if root == None or self.ans != -1:
            return
        
        self.traverse(root.left, k)

        self.cnt += 1
        if self.cnt == k:
            self.ans = root.val
            
        self.traverse(root.right, k)

    def kthSmallest(self, root: Optional[TreeNode], k: int) -> int:
        
        self.traverse(root, k)
        return self.ans
```



### 5.二叉搜索树的最近公共祖先

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inMid(self, v1, v2, v3):
        if (v1 > v2 and v1 < v3) or (v1 > v3 and v1 < v2):
            return True
        else:
            return False

    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root == None:
            return None

        if self.inMid(root.val, p.val, q.val) or root == p or root == q:
            return root
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        return left if isinstance(left, TreeNode) else right
```



### 6.数组中的第k个最大元素

```python
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



### 7.课程表

```python
class Solution:
    def __init__(self):
        self.graph: List[List[int]] = None
        self.isVisited: List[bool] = None
        self.onPath: List[bool] = None
        self.ans: bool = None

    def dfs(self, cur: int):
        if self.onPath[cur]:
            self.ans = False

        if self.ans == False or self.isVisited[cur]:
            return
        
        self.isVisited[cur] = True
        self.onPath[cur] = True

        for i in self.graph[cur]:
            self.dfs(i)

        self.onPath[cur] = False

    def create_graph(self, numCourses: int, prerequisites: List[List[int]]):
        self.graph = [[] for _ in range(numCourses)]
        for edge in prerequisites:
            beg: int = edge[1]; end: int = edge[0]
            self.graph[beg].append(end)

    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        self.ans = True
        self.create_graph(numCourses, prerequisites)
        self.isVisited = [False for _ in range(numCourses)]
        self.onPath = [False for _ in range(numCourses)]
        
        for i in range(numCourses):
            if not self.isVisited[i]:
                self.dfs(i)
                
        return self.ans
```



## 回溯

### 1.二叉树的最大深度

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.height: int = 0
        self.ans: int = 0
    def dfs(self, root: Optional[TreeNode]) -> None:
        if root == None:
            self.ans = max(self.ans, self.height)
            return
        
        self.height += 1

        self.dfs(root.left)
        self.dfs(root.right)

        self.height -= 1

    def maxDepth(self, root: Optional[TreeNode]) -> int:
        self.dfs(root)

        return self.ans
```



### 2.路径总和II

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.target: int = 0
        self.track: List[int] = None
        self.ans: List[List[int]] = None
    def dfs(self, root: TreeNode, sum: int):
        if root == None:
            return
        
        self.track.append(root.val)

        sum += root.val
        
        if root.left == None and root.right == None and sum == self.target:
            self.ans.append(self.track.copy())
            self.track.pop()
            return
        
        self.dfs(root.left, sum)
        self.dfs(root.right, sum)

        self.track.pop()

    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        self.target = targetSum
        self.track = list()
        self.ans = list()
        self.dfs(root, 0)

        return self.ans
```



### 3.全排列

```python
class Solution:
    def __init__(self):
        self.track: List[int] = list()
        self.ans: List[List[int]] = list()
        self.onPath: Set[int] = set()

    def traverse(self, nums: List[int]):
        if len(self.track) == len(nums):
            self.ans.append(self.track.copy())

        for num in nums:
            if num in self.onPath: continue
            self.onPath.add(num)
            self.track.append(num)
            
            self.traverse(nums)
            
            self.track.pop()
            self.onPath.remove(num)


    def permute(self, nums: List[int]) -> List[List[int]]:
        self.traverse(nums)

        return self.ans
```



### 4.全排列II

```python
class Solution:
    def __init__(self):
        self.track: List[int] = list()
        self.ans: List[List[int]] = list()
        self.onPath: Set[int] = set()

    def traverse(self, nums: List[int]):
        if len(self.track) == len(nums):
            self.ans.append(self.track.copy())
            return

        used: Set[int] = set()
        for i in range(len(nums)):
            if i in self.onPath: continue

            if nums[i] in used: continue  # 排除该层中的相同值不同下标的元素
            used.add(nums[i])

            self.onPath.add(i)
            self.track.append(nums[i])

            self.traverse(nums)

            self.onPath.remove(i)
            self.track.pop()


    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        self.traverse(nums)

        return self.ans
```



### 5.组合总和

```python
class Solution:
    def __init__(self):
        self.track: List[int] = list()
        self.ans: List[List[int]] = list()
    
    def traverse(self, candidates: List[int], target: int, cur: int, sum: int):
        if sum == target:
            self.ans.append(self.track.copy())
            return
        if sum > target:
            return

        for i in range(cur, len(candidates)):
            self.track.append(candidates[i])
            self.traverse(candidates, target, i, sum+candidates[i])
            self.track.pop()

    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        self.traverse(candidates, target, 0, 0)

        return self.ans
```



### 6.组合总和II

```python
class Solution:
    def __init__(self):
        self.track: List[int] = list()
        self.ans: List[int] = list()

    def traverse(self, candidates: List[int], target: int, cur: int, sum: int):
        if sum == target:
            self.ans.append(self.track.copy())
            return
        if sum > target:
            return

        hasUsed: Set[int] = set()
        for i in range(cur, len(candidates)):
            if candidates[i] in hasUsed: continue
            self.track.append(candidates[i])
            hasUsed.add(candidates[i])
            self.traverse(candidates, target, i+1, sum+candidates[i])
            self.track.pop()

    # 2 5 2 1 2
    # 1 2 2 2 5
    def combinationSum2(self, candidates: List[int], target: int) -> List[List[int]]:
        candidates.sort()
        self.traverse(candidates, target, 0, 0)

        return self.ans
```



### 7.单词搜索

```python
class Solution:
    def traverse(self, board: List[List[str]], word: str, cur: int, row: int, col: int, ans):
        if cur == len(word):
            ans[0] = True
            return
        if ans[0] or \
           row < 0 or row >= len(board) or col < 0 or col >= len(board[0]) or \
           board[row][col] != word[cur] or board[row][col] == '*':
            return
        
        board[row][col] = '*'

        for i, j in ((-1, 0), (1, 0), (0, -1), (0, 1)):
            self.traverse(board, word, cur+1, row+i, col+j, ans)
        
        board[row][col] = word[cur]

    def exist(self, board: List[List[str]], word: str) -> bool:
        ans: List[bool] = [False]

        for i in range(len(board)):
            for j in range(len(board[0])):
                self.traverse(board, word, 0, i, j, ans)
        
        return ans[0]
```



## 分治

### 1.翻转二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def invertTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        if root == None:
            return None

        self.invertTree(root.left)
        self.invertTree(root.right)

        tmp: TreeNode = root.left
        root.left = root.right
        root.right = tmp

        return root
```



### 2.对称二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def func(self, left: TreeNode, right: TreeNode):
        if left == None and right == None:
            return True

        if left == None or right == None:
            return False

        return left.val == right.val and \
               self.func(left.left, right.right) and self.func(left.right, right.left)

    def isSymmetric(self, root: Optional[TreeNode]) -> bool:

        return self.func(root.left, root.right)
```



### 3.Pow(x, n)

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:
        # b为奇数: a^b = a * a^(b-1)
        # b为偶数: a^b = (a^(b/2))^2
        if n == 0:
            return 1
        elif n == -2147483648:
            return self.myPow(1/x, -(n+1)) / x
        elif n < 0:
            return self.myPow(1/x, -n)
        else:
            if n % 2 == 0:  # 幂是偶数，x^n == [x^(n//2)] ^ 2
                return self.myPow(x, n//2) ** 2
            else:
                return x * self.myPow(x, n-1)
```



### 4.平衡二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isBalandHeight(self, root: TreeNode):
        if root == None:
            return True, 0
            
        left, hl = self.isBalandHeight(root.left)
        right, hr = self.isBalandHeight(root.right)

        if left and right and abs(hl-hr) <= 1:
            return True, max(hl, hr)+1
        else:
            return False, -1

    def isBalanced(self, root: Optional[TreeNode]) -> bool:
        ans, _ = self.isBalandHeight(root)
        return ans
      
class Solution:
    def getHeight(self, root: TreeNode):
        if root == None:
            return 0

        height_l = self.getHeight(root.left)
        if height_l == -1: return -1  # left is not balanced
        height_r = self.getHeight(root.right)
        if height_r == -1: return -1  # right is not balanced

        if abs(height_l - height_r) <= 1: return max(height_l, height_r)+1
        else: return -1

    def isBalanced(self, root: Optional[TreeNode]) -> bool:

        return True if self.getHeight(root) != -1 else False
```



### 5.从前序与中序遍历构造二叉树

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if len(preorder) == 0:
            return None
        val_root: int = preorder[0]

        idx_in = -1
        for i in range(len(inorder)):
            if inorder[i] == val_root:
                idx_inorder = i
        
        l_pre = preorder[1 : idx_inorder+1] if idx_inorder+1 >= 1 else []
        l_in = inorder[0 : idx_inorder] if idx_inorder >= 0 else []
        r_pre = preorder[idx_inorder+1 :] if len(preorder) >= idx_inorder+1 else []
        r_in = inorder[idx_inorder+1 :] if len(inorder) >= idx_inorder+1 else []

        root = TreeNode(val_root, self.buildTree(l_pre, l_in), self.buildTree(r_pre, r_in))

        return root
```



## 动态规划

### 1.斐波那契数列

```python
class Solution:
    def fib(self, n: int) -> int:
        # state -> define
        # define and choice -> recursion formula
        # recursion formula -> traverse order
        # traverse order -> base case

        # dp[i] = dp[i-1] + dp[i-2]
        if n == 0 or n == 1:
            return n
            
        dp: list[int] = [0 for i in range(n+1)]

        dp[0] = 0
        dp[1] = 1
        for i in range(2, len(dp)):
            dp[i] = dp[i-1] + dp[i-2]

        return dp[n]
      
class Solution:
    def fib(self, n: int) -> int:
        # state -> define
        # define and choice -> recursion formula
        # recursion formula -> traverse order
        # traverse order -> base case

        # dp[i] = dp[i-1] + dp[i-2]
        if n == 0 or n == 1:
            return n

        dp_i_2 = 0
        dp_i_1 = 1
        
        for i in range(2, n+1):
            tmp = dp_i_1
            dp_i_1 = dp_i_1 + dp_i_2
            dp_i_2 = tmp

        return dp_i_1
```



### 2.爬楼梯

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        # dp[i] = dp[i-1] + dp[i-2]
        if n == 1 or n == 2:
            return n
            
        dp: list[int] = [0 for i in range(n+1)]
        dp[1] = 1
        dp[2] = 2

        for i in range(3, len(dp)):
            dp[i] = dp[i-1] + dp[i-2]
        
        return dp[n]
 
class Solution:
    def climbStairs(self, n: int) -> int:
        # dp[i] = dp[i-1] + dp[i-2]
        if n == 1 or n == 2:
            return n

        dp_i_2: int = 1
        dp_i_1: int = 2

        for i in range(3, n+1):
            tmp: int = dp_i_1
            dp_i_1 = dp_i_1 + dp_i_2
            dp_i_2 = tmp
        
        return dp_i_1
```



### 3.一维动态数组和

```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        # dp[i] = dp[i-1] + nums[i]
        dp: List[int] = [0 for i in range(len(nums))]
        dp[0] = nums[0]
        for i in range(1, len(dp)):
            dp[i] = dp[i-1] + nums[i]

        return dp
```



### 4.买卖股票的最佳时机

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
        # dp[i][1] = max(dp[i-1][1], -prices[i])
        n: int = len(prices)
        dp: List[List[List[int]]] = [[[0 for k in range(2)] for j in range(2)] for i in range(n)]

        dp[0][0][0] = 0
        dp[0][0][1] = -1 # 取不到
        dp[0][1][0] = 0
        dp[0][1][1] = -prices[0]

        for i in range(1, n):
            for j in range(1, 2):
                dp[i][j][0] = max(dp[i-1][j][0], dp[i-1][j][1]+prices[i])
                dp[i][j][1] = max(dp[i-1][j][1], dp[i-1][j-1][0]-prices[i])

        return dp[n-1][1][0]
      
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
        # dp[i][1] = max(dp[i-1][1], -prices[i])
        n: int = len(prices)
        dp: List[List[int]] = [[0 for j in range(2)] for i in range(n)]

        dp[0][0] = 0
        dp[0][1] = -prices[0]

        for i in range(1, n):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
            dp[i][1] = max(dp[i-1][1], 0-prices[i])

        return dp[n-1][0]
      
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
        # dp[i][1] = max(dp[i-1][1], -prices[i])
        n: int = len(prices)
        dp: List[int] = [0 for j in range(2)]

        dp[0] = 0
        dp[1] = -prices[0]

        for i in range(1, n):
            dp[0] = max(dp[0], dp[1]+prices[i])
            dp[1] = max(dp[1], 0-prices[i])

        return dp[0]
      
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        # dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
        # dp[i][1] = max(dp[i-1][1], -prices[i])
        n: int = len(prices)

        dp_0 = 0
        dp_1 = -prices[0]

        for i in range(1, n):
            dp_0 = max(dp_0, dp_1+prices[i])
            dp_1 = max(dp_1, 0-prices[i])

        return dp_0
```



### 5.买卖股票的最佳时机II

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        n: int = len(prices)

        dp: List[List[int]] = [[0 for j in range(2)] for i in range(n)]
        
        dp[0][0] = 0
        dp[0][1] = -prices[0]
        for i in range(1, n):
            dp[i][0] = max(dp[i-1][0], dp[i-1][1]+prices[i])
            dp[i][1] = max(dp[i-1][1], dp[i-1][0]-prices[i])

        return dp[n-1][0]
      
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        n: int = len(prices)
        
        dp_0 = 0
        dp_1 = -prices[0]
        for i in range(1, n):
            tmp = dp_0
            dp_0 = max(dp_0, dp_1+prices[i])
            dp_1 = max(dp_1, tmp-prices[i])

        return dp_0
```



### 6.最小路径和

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        # dp[i][j] = max(dp[i-1][j], dp[i][j-1]) + 1

        m: int = len(grid)
        n: int = len(grid[0])
        dp: List[List[int]] = [[0 for j in range(n)] for i in range(m)]

        dp[0][0] = grid[0][0]
        for i in range(1, m): dp[i][0] = dp[i-1][0] + grid[i][0]
        for j in range(1, n): dp[0][j] = dp[0][j-1] + grid[0][j]

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j]
        
        return dp[m-1][n-1]
```



### 7.最大子数组和

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # dp[i] = nums[i], dp[i-1]+nums[i]
        
        dp: List[int] = [0 for i in range(len(nums))]
        dp[0] = nums[0]
        ans: int = nums[0]
        
        for i in range(1, len(dp)):
            dp[i] = max(nums[i], nums[i] + dp[i-1])
            ans = max(ans, dp[i])
        
        return ans
   
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # dp[i] = nums[i], dp[i-1]+nums[i]
        
        dp: int = nums[0]
        ans: int = nums[0]
        
        for i in range(1, len(nums)):
            dp = max(nums[i], nums[i] + dp)
            ans = max(ans, dp)
        
        return ans
```



### 8.打家劫舍

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # dp[i] = max(dp[i-2] + nums[i], dp[i-1])

        n: int = len(nums)
        if n == 1: return nums[0]
        elif n == 2: return max(nums[0], nums[1])

        dp: List[int] = [0 for i in range(n)]
        dp[0], dp[1] = nums[0], max(nums[0], nums[1])

        for i in range(2, n):
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])
        
        return dp[n-1]

class Solution:
    def rob(self, nums: List[int]) -> int:
        # dp[i] = max(dp[i-2] + nums[i], dp[i-1])

        n: int = len(nums)
        if n == 1: return nums[0]
        elif n == 2: return max(nums[0], nums[1])

        dp_2, dp_1 = nums[0], max(nums[0], nums[1])

        for i in range(2, n):
            tmp: int = dp_1
            dp_1 = max(dp_2 + nums[i], dp_1)
            dp_2 = tmp
        
        return dp_1
```



### 9.打家劫舍II

```python
class Solution:
    def func(self, nums: List[int], front: int, back: int):
        n: int = len(nums)
        dp: List[int] = [0 for i in range(n)]

        if front == 0:
            dp[0], dp[1] = nums[0], max(nums[0], nums[1])
        elif front == 1:
            dp[0], dp[1] = 0, nums[1]
        
        for i in range(2, back+1):
            dp[i] = max(dp[i-1], dp[i-2]+nums[i])
        
        return dp[back]

    def rob(self, nums: List[int]) -> int:
        n: int = len(nums)

        if n == 1: return nums[0]
        elif n == 2: return max(nums[0], nums[1])

        return max(self.func(nums, 0, n-2), self.func(nums, 1, n-1))

class Solution:
    def func(self, nums: List[int], front: int, back: int):
        n: int = len(nums)

        if front == 0:
            dp_2, dp_1 = nums[0], max(nums[0], nums[1])
        elif front == 1:
            dp_2, dp_1 = 0, nums[1]
        
        for i in range(2, back+1):
            tmp: int = dp_1
            dp_1 = max(dp_1, dp_2+nums[i])
            dp_2 = tmp
        
        return dp_1

    def rob(self, nums: List[int]) -> int:
        n: int = len(nums)

        if n == 1: return nums[0]
        elif n == 2: return max(nums[0], nums[1])

        return max(self.func(nums, 0, n-2), self.func(nums, 1, n-1))
```



## 位运算

### 1.位1的个数

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans: int = 0
        while n > 0:
            ans += n & 1
            n >>= 1

        return ans
      
class Solution:
    def hammingWeight(self, n: int) -> int:
        ans: int = 0
        while n > 0:
            ans += 1
            n = n & (n-1)  # 消去最右边的1
        return ans
```



## 数学

### 1.除自身以外数组的乘积

```python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        n: int = len(nums)
        ans: List[int] = [0 for i in range(n)]

        for i in range(n):
            if i == 0:
                ans[i] = 1
            else:
                ans[i] = ans[i-1] * nums[i-1]
        
        tmp: int = 0
        for i in range(n-1, -1, -1):
            if i == n-1:
                tmp = nums[i]
                continue
            ans[i] = ans[i] * tmp
            tmp = tmp * nums[i]

        return ans
```





Now you are expert of emotional and character analysis. The follow is a conversation which involves several speaks.



Here is a conversation:

Speaker_0:"Guess what?"

Speaker_1:"What?"

Speaker_0:"I did it, I asked her to marry me."

Speaker_1:"Good for you!"

Speaker_0:"Yes, I did it!"

Speaker_1:"When?"

Speaker_0:"Oh my god, it was just last weekend."



Please give the vector of  Speaker_0's character, the vector has 6 elements, representing <optimism, depression, neuroticism, irritability, enthusiasm, caution>, and each value in the vector should fall between 0 and 1

Speaker_0 's character vector is [0.9,0.1,0.2,0.1,0.9,0.5], representing <optimism, depression, neuroticism, irritability, enthusiasm, caution>, Please select the emotional label of <Speaker_0:"Oh my god, it was just last weekend."> from <happy, sad, neutral, angry, excited, frustrated>.

