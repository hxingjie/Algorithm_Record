#

## wei yun suan qiu he
```c++
class Solution {
public:
    int getSum(int a, int b) {

        while (b != 0){
            int c = (a&b) << 1;
            a = a ^ b;
            b = c;
        }

        return a;
    }
};
```

## zhi chu xian yi ci de shu zi
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        
        int ans = nums[0];
        for (int i = 1; i < nums.size(); i++)
            ans = ans  ^ nums[i];
        
        return ans;
    }
};
```

## zhi chu xian yi ci de shu zi II
```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        vector<int> cnt= vector(32, 0);

        for (int i = 0; i < nums.size(); i++){
            for (int j = 0; j < 32; j++){
                cnt[j] += nums[i]&1;// huo qu er jin zhi de mei ge zhi
                nums[i] = nums[i] >> 1;
            }
        }

        int ans = 0;
        for (int i = 0; i < cnt.size(); i++)
            cnt[i] %= 3;

        for (int i = 0; i < cnt.size(); i++){// 2 jin zhi -> int
            ans <<= 1;
            ans |= cnt[31-i];
        }

        return ans;

    }
};
```
