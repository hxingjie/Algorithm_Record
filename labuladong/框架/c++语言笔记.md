## Tips
```c++
// 常用函数
stod:string to double

// 字符流的使用
stringstream ss(str);
vector<string> words;
string word;
while (getline(ss,word,' ')){
    if (!word.empty())
        words.push_back(word);s
}
ss.clear();// 重置状态
ss.str() = "";// 清空流

// 输入输出
scanf("%d-%d-%d, &n1, &n2, &n3);
printf("%d-%02d-%02d\n", y, m, d);
printf("%-06.2lf\n", num);// 0表示填充的字符，6表示整个数的位宽，2表示精确到几位小数，%-2d表示左对齐，不加-表示默认右对齐

// 位运算
位运算符：& ｜ ^异或  ~取反

```
---
## STL
```c++
bool cmp(const int &lhs, const int &rhs){// 函数 sort函数可以用
    if (lhs > rhs){
        return true;
    }else{
        return false;
    }
}

class Thing{// 对类型重载运算符 map,set,priority_queue数据结构都可以用，sort函数也可以用
public:
    int m, v, avg;
    bool operator < (const Thing &other) const{
        if (this->avg < other.avg) return true;
        else return false;
    }
};

struct func{// 仿函数 map,set,priority_queue数据结构都可以用，sort函数也可以用
public:
    bool operator () (const int &lhs, const int &rhs) const {
        if (lhs < rhs){
            return true;
        }else{
            return false;
        }
    }
};

int main(){
    vector<int> nums;
    sort(nums.begin(),nums.end(),&cmp);
    map<int,int,func> m;
    m[1] = 2;
    m[2] = 1;
    for (auto elem : m) {
        cout << elem.first << endl;
    }

    return 0;
}
```
