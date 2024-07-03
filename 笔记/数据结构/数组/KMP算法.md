
```python
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

```
