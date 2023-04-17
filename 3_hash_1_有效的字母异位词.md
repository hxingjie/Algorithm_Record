```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int hash[26];
        for (int i = 0; i < 26; i++){
            hash[i] = 0;
        }

        for(char c : s){
            hash[(int)c-97]++;
        }
        for(char c : t){
            hash[(int)c-97]--;
        }

        for(int i : hash){
            if (i != 0){
                return false;
            }
        }
        return true;
    }
};
```

```c#
public class Solution {
    public bool IsAnagram(string s, string t) {
        int[] hash = new int[26];
        for (int i = 0; i < 26; i++){
            hash[i] = 0;
        }

        foreach(char c in s){
            hash[(int)c - 97]++;
        }
        foreach(char c in t){
            hash[(int)c - 97]--;
        }

        foreach(int i in hash){
            if (i != 0) { return false; }
        }
        return true;

    }
}
```

