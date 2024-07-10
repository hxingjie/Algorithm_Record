## Tips
```c++
// 常用函数
stod:string to double
stoi
reverse(container.begin(), container.end());
string.resize(string.size() + cnt);

string.substr()

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
位运算符：& ｜ ^异或  ~取反  >>右移  <<左移
无符号左右移位，可以先将变量变为unsigned类型，再左右移位

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

class func{// 仿函数 map,set,priority_queue数据结构都可以用，sort函数也可以用
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
    // 使用仿函数
    map<int,int,func> m;
    set<int,func> s;
    priority_queue<int,vector<int>,func> q;
    sort(nums.begin(),nums.end(),cmp);

    return 0;
}
```
---
## 算法与数据结构

###  一、算法

#### 1.sort

```c++
#include <algorithm>
using namespace std;
bool cmp(int lhs, int rhs){// 数组元素类型
    // 此函数是相当于重载<号，所以两个元素相等时return false
    if (lhs < rhs){
        return true;
    }else{
        return false;
      	// 永远让比较函数对相同元素返回false
    }
}

int arr[5] = {1,3,5,2,10};
//begin是第一个元素，end是最后一个元素的后一个位置
sort(arr, arr+5, &cmp);// sort(begin,end,&func)

```

#### 2.binarySearch

```c++
bool binarySearch(int arr[], int value, int left, int right){
    while (left <= right){// 相等时仍要进入循环
        int mid = (left+right)/2;
        if (arr[mid] == value){
            return true;
        }else{
            if (arr[mid] < value){
                left = mid+1;
            }else{
                right = mid-1;
            }
        }
    }
    return false;
}
```

#### 3.广度优先遍历

```c++
#include <cstdio>
#include <queue>
#include <cmath>
using namespace std;

int main() {
    int n;
   
    scanf("%d", &n);

    queue<long long> q;
    long long first = 1;// 第一个元素入队
    q.push(first);

    while (!q.empty()){
        long long cur = q.front();// 出队
        q.pop();
        if (cur % n == 0){// 访问
            printf("%lld\n",cur);
            break;
        }

        q.push(cur*10);// 邻接点入队
        q.push(cur*10+1);// 邻接点入队
    }
    return 0;
}
```

#### 4.qsort

```c++
#include <iostream>
#include <stdlib.h>
using namespace std;
char arr[5] = { 'b','c','a','h','d' };

int cmp (const void * a, const void * b)
{
    char *p1 = (char*)a;
    char *p2 = (char*)b;
    if (*p1 < *p2)
        return -1;
    else if (*p1 == *p2)
        return 0;
    else
        return 1;
}
int func(int a){
    cout << a << endl;
    return 0;
}
int main()
{
    int(*pFunc)(int) = &func;//函数指针的声明
    pFunc = &func;//函数指针的赋值
    pFunc(10);//函数指针的调用
    
    qsort(arr, 5, sizeof(char), &cmp);

    return(0);
}
```

### 二、数据结构

#### 1.map

```c++
#include <cstdio>
#include <map>
#include <string>
using namespace std;
//自定义比较规则
struct cmp{
  	bool operator() (const type &lhs,const type &rhs) const {
    		if (lhs < rhs){
        	return true;
      	}else{
        	return false;
      	}
  	}
}
//key是结构体
struct info{
  	int id;
  	bool operator < (const info &r) const {
      	// id is lhs, r is rhs
      	if	(id < r.id){
          	return true;
        }else{
          	return false;
        }
    }
};

int main() {
    map<string,int> myMap;
    bool b = myMap.empty();
    int size = myMap.size();

    //1.方括号插入
    myMap["hello"] = 1;
    //2.insert插入
    myMap.insert(pair<string,int>("world",2));

    //3.删除元素
    myMap.erase("world");

    //4.迭代器遍历
    map<string,int>::iterator it;
    //.begin()是第一个元素的位置
    //.end()是最后一个元素的下一个位置
    for (it = myMap.begin(); it != myMap.end(); ++it) {
        //++it移动迭代器的指向，unordered_map不支持
        printf("%s %d\n",it->first.c_str(),it->second);
    }

    //5.find(key)
    it = myMap.find("hello");//return iterator
    if (it != myMap.end()){
        printf("It's exist: %s %d\n",it->first.c_str(),it->second);
    }else{
        printf("Not Found\n");
    }

    return 0;
}
```

#### 2.set

```c++
set<int> s;// 元素唯一，且有序，底层为红黑树
s.insert(val);
s.count(val);
s.find(val);
```

#### 3.string

```c++
#include <cstdio>
#include <string>
using namespace std;
  	// 1.输入：
    char buf[100] = {'\0'};// 使用c风格字符串输入输出
  
    scanf("%s",buf);// 读一个单词
  	while (scanf("%s",buf) != EOF){ }
  
    fgets(buf,sizeof(buf),stdin);// 读一行，会读入'\n'
  	while (fgets(buf,sizeof(buf),stdin) != NULL){ }
  	//scanf后缓冲区会留下'\n'，如果此时使用fgets读取，会将\n读入，然后结束函数，所以，中间应该使用getchar()读取'\n'

		string word;
		while(cin>>word){ }

		getline(cin,string,'\n')
    getline(stringstream,string,'\n')
    // 分割单词
    stringstream ss(string)
    while ((bool)getline(ss,string,' ') == true){ },' '会被吃掉，不会留在缓冲区
    ss.str()// 返回临时的string对象
    ss.clear();// 清空状态 
		ss.str("");// 清空流

    string str = buf;// C风格 --> C++风格
		printf("%s\n", str.c_str();)// C++风格 --> C风格
  
  	// 2.常用方法
  	str[0], str[1]
      
  	string = str.substr(begin_pos,len)
    string = str.substr(begin_pos)
    string =  string1 + string2;

  	int = str.size()
    str.push_back()
    str.pop_back()
  	str.erase(pos)
    
    int(pos) = str.find(char/string)
    int(count) = str.count(str.begin(),str.end(),char)
    str.c_str()
    str.clear()
```

#### 4.vector

```c++
#include <cstdio>
#include <vector>

using namespace std;

    //vector是无序，可重复，可以扩充的容器
    vector<int> v;// 声明
  	vector<int> v = {1,3,2};// 初始化
  	vector<int> v(100,0);// 申请100个空间，并初始化为0
    vector<int> v(v_src.begin(), v_src.end());
  
    v.size();//获取长度
  
    v.push_back(0);//尾部插入元素
  	v.pop_back();// 弹出尾部元素

    v[0];//下标读取
    v[0] = 10;//下标修改
    
  	// begin()指向容器第一个位置，end()指向容器最后一个位置的下一个位置
  
    // 迭代器遍历
    vector<int>::iterator it;
    for (it = v.begin(); it != v.end() ; ++it) {
        printf("%d\n",*it);// 要解引用
    }

    v1.insert(it,0);// 指定位置插入
    v1.erase(it);// 指定位置删除
```

#### 5.list
```c++
#include <iostream>
#include <cstdio>
#include <list>
using namespace std;

int main(){
    list<int> l;

  	// 常用函数
  	l.begin();
  	l.end();
  
  	l.push_front();
  	l.pop_front();
  	l.push_back();
  	l.pop_back();
  
    list<int>::iterator it;
    for (it = l.begin(); it != l.end(); ++it) { printf("%d ", *it); }// 迭代器遍历
		
  	
  	list<int>::iterator it;
  	.insert(it, val) 插入到迭代器所指向的前一个位置
    while (*it != val){ it++; }// 使迭代器指向值为val的元素
  	l.insert(it, val_insert)// 把val_insert插入到val后一个位置
    it++; l.insert(it, val_insert)// 把val_insert插入到val前一个位置
  
    return 0;
}
```

#### 6.queue

```c++
#include <queue>
using namespace std;

queue<type> q;
int = q.size();
bool = q.empty();

q.push(0);// 队尾插入
q.pop();// 队头弹出
type = q.front();// 获取队头元素
```

#### 7.stack

```c++
#include <stack>
using namespace std;

stack<int> myStack;
int = myStack.size();
bool = myStack.empty();

myStack.push(0);
myStack.pop();
type = myStack.top();
```

#### 8.二叉树

```c++
#include <cstdio>
#include <queue>
using namespace std;
struct TreeNode{
    int data;
    TreeNode * leftChild;// 指向左孩子
    TreeNode * rightChild;// 指向右孩子
};

struct QueueNode{
    TreeNode * parent;
    bool isLeftIn;
};

// 层序插入
void insert(TreeNode * &root, queue<QueueNode *> &myQueue, char data){
    if (data != '#'){
        TreeNode * pTreeNode = new TreeNode;
        //(*p).data = data;
        pTreeNode->data = data;

        QueueNode * pQueueNode = new QueueNode;
        pQueueNode->parent = pTreeNode;
        pQueueNode->isLeftIn = false;
        myQueue.push(pQueueNode);

        if (root == NULL){
            //说明插入的是第一个结点
            root = pTreeNode;
        }else{
            QueueNode * pParent = myQueue.front();
            if (pParent->isLeftIn == false){
                pParent->parent->leftChild = pTreeNode;
                pParent->isLeftIn = true;
            }else{
                pParent->parent->rightChild = pTreeNode;
                myQueue.pop();
                delete pParent;
            }
        }
    }else{
        if (root != NULL){
            QueueNode *pParent = myQueue.front();
            if (pParent->isLeftIn == false){
                pParent->parent->leftChild = NULL;
                pParent->isLeftIn = true;
            }else{
                pParent->parent->rightChild = NULL;
                myQueue.pop();
                delete pParent;
            }
        }
    }
}

// 层序遍历
void levelOrder(TreeNode * root){
    queue<TreeNode *> pos;
    pos.push(root);
    while (pos.empty() == false){
        TreeNode * pCur = pos.front();
        pos.pop();
        printf("%c",pCur->data);
        if (pCur->leftChild != NULL){
            pos.push(pCur->leftChild);
        }
        if (pCur->rightChild != NULL){
            pos.push(pCur->rightChild);
        }
    }
    printf("\n");
}

void preOrder(TreeNode * root){
    if (root == nullptr){
        return;
    }else{
        printf("%c",root->data);
        preOrder(root->leftChild);
        preOrder(root->rightChild);
    }
}
void midOrder(TreeNode * root){
    if (root == nullptr){
        return;
    }else{
        midOrder(root->leftChild);
        printf("%c",root->data);
        midOrder(root->rightChild);
    }
}
void postOrder(TreeNode * root){
    if (root == nullptr){
        return;
    }else{
        postOrder(root->leftChild);
        postOrder(root->rightChild);
        printf("%c",root->data);
    }
}

int main() {
    TreeNode * root = NULL;// 指向根结点
    char arr[] = "abc##de#g##f###";

    queue<QueueNode *> myQueue;// 新结点父亲的位置，以及左孩子是否插入

    for (int i = 0; arr[i] != '\0'; ++i) {
        insert(root,myQueue,arr[i]);
    }

    levelOrder(root);

    preOrder(root);
    printf("\n");

    midOrder(root);
    printf("\n");

    postOrder(root);
    printf("\n");

    return 0;
}
```

#### 9.priority_queue(堆)

```c++
#include <cstdio>
#include <queue>
using namespace std;

int main() {
 		//priority_queue<int> myPQueue;
    //1.myPQueue.push(6);
    //2.myPQueue.pop();
    //3.bool b = myPQueue.empty();
    //4.int element = myPQueue.top();
    priority_queue<int> myPQueue;
    int arr[6] = {2,4,6,1,3,5};
    for (int i = 0; i < 6; ++i) {
        myPQueue.push(arr[i]);
        printf("push %d, top %d\n",arr[i], myPQueue.top());
    }
    while (myPQueue.empty() == false){
        printf("top %d\n",myPQueue.top());
        myPQueue.pop();
    }

    return 0;
}

// 实现小顶堆
// 方法1:将元素取相反数
// 方法2:封装成类类型，运算符重载
#include <cstdio>
#include <queue>
using namespace std;
class Element{
public:
    int value;
};
bool operator < (Element lhs,Element rhs){// 小顶堆，将小于运算符含义取反
    if (lhs.value < rhs.value){
        return false;
    }else{
        return true;
    }
}
bool operator < (Element lhs,Element rhs){// 大顶堆
    if (lhs.value < rhs.value){
        return true;
    }else{
        return false;
    }
}

int main() {
    priority_queue<Element> pQueue;
    int arr[6] = {6,4,2,5,3,1};
    for (int i = 0; i < 6; ++i) {
        Element e;
        e.value = arr[i];
        pQueue.push(e);
    }
    while (pQueue.empty() == false){
        printf("top %d\n",pQueue.top().value);
        pQueue.pop();
    }

    return 0;
}
```

### 三、常见函数以及头文件

#### 1.内存布局

堆：new、delete

栈：局部变量、const修饰的局部变量

只读区：代码、常量、const修饰的全局变量

读写区：全局变量、静态变量

----------------

堆：new、delete

栈：局部变量

文本段（通常是只读）：代码、字符串常量、const修饰的全局变量

数据段：初始化的全局、静态变量

BSS段：未初始化的全局、静态变量

#### 2.程序过程

预处理

编译（高级程序语言->汇编语言）

汇编（汇编语言->机器语言）

链接

#### 3.头文件

string

cstring：strlen、strcmp、strcpy

cmath：sqrt、pow、abs、fabs、floor(向0取整) 2.5->2, -2.5->-2

cctype：isupper、islower、isalpha、isdigit、

algorithm：max、min、reverse(.begin(), .end())(string,array,vector)、sort

cstdio：printf、scanf

stdlib.h

climits：INT_MAX

cin 不读取空格等符号
要读取一整行，用fgets(str, sizeof(str), stdin)、getline(cin, str)（fgets会读入'\n'）

0--48, 9--57   A--65, Z--90   a--97, z--122

upper->lower：c = c + 32

lower->upper：c = c - 32

digit->int：c = c - 48('0')

```c++
scanf("%d %lld %f %lf",int name long long name float name double name);
scanf("%c",char name);
scanf("%s",char[] name);

//格式化输入！！！！！！！
scanf("%d+i%d", &re, &img);//1+i2
scanf("%d,i%d", &re, &img);//1,2

scanf()之后使用fgets()，可能需要使用getchar()读取换行符
  
stringstream
getline(cin/stringstream,string,'\n')
  
访问数组前要验证下标是否合法
使用指针前要验证指针是否为空
```

### 四、常见问题

#### 1.闰年：

year %400 == 0 || (year %100 != 0 && year %4 == 0)

#### 2.判断某一月份有多少天：

monthDay[13] = {0,31,28,31,30,31,30,31,31,30,31,30,31}

#### 3.格式打印：

printf("%04d\n", year); 

%0d 0填充，

%2d 占两位字符

%.2lf 保留两位小数 

%+/-2d，左右对齐

```c++
#include <iostream>

using namespace std;

int main(){
    double num = 12.34;
    printf("%08.4lf\n", num);

    int num1 = 12;
    printf("%04d\n", num1);

    int num2 = 12;
    printf("%+04d\n", num2);

    int num3 = 12;
    printf("%-04d\n", num3);// 默认左对齐

    return 0;
}
```



#### 4.递归

```c++
int func(int num){
    if (num == 1 || num == 2){
        return 1;
    }else{
        return ( func(num-1) + func(num-2) );
    }
}
int main(){
    double n;
    cin >> n;

    //1 1 2 3 5 8 13
    for (int i = 1; i <= n; ++i) {
        int a;
        cin >> a;
        cout << func(a) << endl;
    }

    return 0;
}
```

#### 5.判断质数

```c++
bool isPrimeNum(int num){
  	//质数又称素数。一个大于1的自然数，除了1和它自身外，不能被其他自然数整除的数叫做质数；否则称为合数（规定1既不是质数也不是合数）。
    if (num == 1){
        return false;// 1不是质数！！！！！！！！
    }
    for (int i = 2; i <= sqrt(num); ++i) {
        if (num %i == 0){
            return false;
        }
    }
    return true;
}
```

#### 6.反转数字

```c++
int reverse(int n){
    int num = 0;
    while (n > 0){
        num = num * 10 + n % 10;
        n /= 10;
    }
    return num;
}
```

#### 7.指针和引用

```c++
void swap(int * x, int * y){
    int temp = *x;
    *x = *y;
    *y = temp;
}

void swap(int & x, int & y){
    int temp = x;
    x = y;
    y = temp;
}

int main(){
  
}
```

```c++
int * addInt(int value){
    int * p = new int;
    *p = value;
    return p;
}

int main() {
    int * p = addInt(1);
    printf("%d",*p);
    delete p;

    return 0;
}
```

#### 8. for

```c++
for (auto &elem : vec){
  	cout << elem << endl;
}
```

