# 复原IP地址

**有效 IP 地址** 正好由四个整数（每个整数位于 `0` 到 `255` 之间组成，且不能含有前导 `0`），整数之间用 `'.'` 分隔。

- 例如：`"0.1.2.201"` 和` "192.168.1.1"` 是 **有效** IP 地址，但是 `"0.011.255.245"`、`"192.168.1.312"` 和 `"192.168@1.1"` 是 **无效** IP 地址。

给定一个只包含数字的字符串 `s` ，用以表示一个 IP 地址，返回所有可能的**有效 IP 地址**，这些地址可以通过在 `s` 中插入 `'.'` 来形成。你 **不能** 重新排序或删除 `s` 中的任何数字。你可以按 **任何** 顺序返回答案。

[93. 复原 IP 地址 - 力扣（LeetCode）](https://leetcode.cn/problems/restore-ip-addresses/description/)

```c++
class Solution {
public:
    vector<string> ans;
    vector<string> path;
    bool isValid(vector<string> s){
        for (string str : s) {
            if (str[0] == '0'){
                if (str.size() > 1){
                    return false;
                }else{
                    continue;
                }
            }else if (!(stoi(str) >=0 && stoi(str) <= 255)){
                return false;
            }
        }
        return true;
        
    }
    void traverse(string s){

        if (path.size() == 4) {
            if (s.size() == 0){
                if (isValid(path)){
                string res = "";
                for (int i = 0; i < 4; ++i) {
                    if (i == 3){
                        res += path[i];
                    }else{
                        res += path[i] + '.';
                    }
                }
                ans.push_back(res);
                }
            }
            return;
        }

        for (int len = 1; len <= s.size() && len <= 4; ++len) {
            path.push_back(s.substr(0,len));
            traverse(s.substr(len));
            path.pop_back();
        }

    }
    vector<string> restoreIpAddresses(string s) {
        traverse(s);
        return ans;
    }
};
```

```c#
public class Solution
{
    public IList<string> ans = new List<string>();
    public List<string> track = new List<string>();

    public bool isValid(string s)
    {
        if ('0' == s[0])
        {
            if (s.Length == 1) return true;
            else return false;
        }
        else
        {
            if (Int32.Parse(s) >= 0 && Int32.Parse(s) <= 255) return true;
            else return false;
        }
    }
    public void BackTrack(string s)
    {

        if (track.Count == 4)
        {
            if (s.Length == 0){
                string res = "";
                for (int i = 0; i < 4; i++)
                {
                    if (i == 0) res += track[i];
                    else res += '.' + track[i];
                }
                ans.Add(res);
            }
            return;
        }

        for (int length = 1; length <= s.Length && length <= 4; length++)// 树枝是下标从0开始的不同长度的子串
        {
            if (!isValid(s.Substring(0,length))) continue;
                
            track.Add(s.Substring(0,length));
            BackTrack(s.Substring(length));
            track.RemoveAt(track.Count-1);
        }
            
    }
    public IList<string> RestoreIpAddresses(string s) {
        BackTrack(s);
        return ans;
    }
}
```

