# KMP算法

给你两个字符串 `haystack` 和 `needle` ，请你在 `haystack` 字符串中找出 `needle` 字符串的第一个匹配项的下标（下标从 0 开始）。如果 `needle` 不是 `haystack` 的一部分，则返回 `-1` 。

https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/submissions/

```c++
class Solution {
public:
    int maxPrePostStr(string s, int r){// 计算[0,r]的最长相等前后缀
        // len >= 2
        for (int len = r ; len > 0; len--)// 穷举所有长度的前后缀
        {
            int lpos = 0, rpos = r-len+1;
            for ( ; rpos <= r; lpos++, rpos++)
            {
            	if (s[lpos] != s[rpos]) break;
            }
            if (rpos > r) return len;         
        }
        return 0;     
    }
    int strStr(string haystack, string needle) {
        vector<int> rec(needle.size());
        for (int i = 0; i < rec.size(); i++)
        {
            if (i == 0) rec[i] = -1;
            else if (i == 1) rec[i] = 0;
            else{
                rec[i] = maxPrePostStr(needle,i-1);
            }
        }
        
        int i = 0, j = 0;
        while (i < haystack.size() && j < needle.size())
        {
            if (haystack[i] == needle[j]) { i++; j++; }// 匹配成功就同时向前 
            else{
                j = rec[j];// 不匹配就回退
                if (j == -1) { i++; j++; }// 如果第一个字符就不想等，i也应该向前，因为j此时等于-1，所以也向前，-1只是一个标志值代表此时是第一个字符不匹配
            }            
        }
        if (j == needle.size()) return i-j;
        else return -1;
    }
};
```

