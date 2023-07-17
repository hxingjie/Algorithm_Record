# 反转字符串II

给定一个字符串 `s` 和一个整数 `k`，从字符串开头算起，每计数至 `2k` 个字符，就反转这 `2k` 字符中的前 `k` 个字符。

- 如果剩余字符少于 `k` 个，则将剩余字符全部反转。
- 如果剩余字符小于 `2k` 但大于或等于 `k` 个，则反转前 `k` 个字符，其余字符保持原样。

https://leetcode.cn/problems/reverse-string-ii/description/

```c++
class Solution {
public:
    void reStr(string &s, int l, int r){
        while (l <= r){
            swap(s[l],s[r]);
            l++, r--;
        }
    }
    
    string reverseStr(string s, int k) {
        int pos = 0;
        while (pos < s.size()){
            if (pos+k-1 < s.size())
            {
                reStr(s,pos,pos+k-1);
            }else{
                reStr(s,pos,s.size()-1);
            }
            pos += 2*k;
        }
        return s;
    }
};
```

