---
abbrlink: acwing 算法基础课模板
author: zheyuanzhang
categories:
- - ' 算法模板'
date: '2025-09-11T16:12:55.176200+08:00'
tags:
- 算法模板
- acwing 基础课
title: acwing 算法基础课模板
updated: '2025-09-11T16:12:55.210+08:00'
---
# acwing 算法基础课模板

> 【FlowUs 息流】acwing 算法基础课模板
> 
> https://flowus.cn/share/85525e48-ed80-434d-81c5-0ecbec3c109f?code=XAGV17

# 1. 基本模板

## △ C++ STL 用法

```C++
vector 变长数组，倍增的思想
    size()  返回元素个数
    empty()  返回是否为空
    clear()  清空
    front()/back()
    push_back() / pop_back()
    begin() / end()
    []
    支持比较运算，按字典序
pair<int, int>
    first, 第一个元
    second, 第二个元素
    支持比较运算，以first为第一关键字，以second为第二关键字（字典序）
string，字符串
    size()/length()  返回字符串长度
    empty()
    clear()
    substr(起始下标，(子串长度))  返回子串
    c_str()  返回字符串所在字符数组的起始地址
queue, 队列
    size()
    empty()
    push()  向队尾插入一个元素
    front()  返回队头元素
    back()  返回队尾元素
    pop()  弹出队头元素
priority_queue, 优先队列，默认是大根堆
    size()
    empty()
    push()  插入一个元素
    top()  返回堆顶元素
    pop()  弹出堆顶元素
    定义成小根堆的方式：
    priority_queue<int, vector<int>, greater<int> > q;
    priority_queue<coord, vector<coord>, decltype(&Lcmp)> pq(Lcmp);
    bool Lcmp (const coord & c1 , const coord & c2){
    return c1 .l < c2.l; }
stack, 栈
    size()
    empty()
    push()  向栈顶插入一个元素
    top()  返回栈顶元素
    pop()  弹出栈顶元素
deque, 双端队列
    size()
    empty()
    clear()
    front()/back()
    push_back()/pop_back()
    push_front()/pop_front()
    begin()/end()
    []
set, map, multiset, multimap, 基于平衡二叉树（红黑树），动态维护有序序列
    size()
    empty()
    clear()
    begin()/end()
    ++, -- 返回前驱和后继，时间复杂度 O(logn)

    set/multiset
        insert()  插入一个数
        find()  查找一个数
        count()  返回某一个数的个数
        erase()
            (1) 输入是一个数x，删除所有x   O(k + logn)
            (2) 输入一个迭代器，删除这个迭代器
    lower_bound()   /   upper_bound() // 找不到都返回后面
    lower_bound(x)  返回大于等于x的最小的数的迭代器
    upper_bound(x)  返回大于x的最小的数的迭代器
    //123456789递增序列     a    < x ,x，x,x,x,x,x   < b
   //                            low                  up
    map/multimap
        insert()  插入的数是一个pair
        erase()  输入的参数是pair或者迭代器
        find()
        []  注意multimap不支持此操作。 时间复杂度是 // O(logn)
        lower_bound()/upper_bound()

unordered_set, unordered_map, 
unordered_multiset, unordered_multimap, 哈希表
    和上面类似，增删改查的时间复杂度是 O(1)
    不支持 lower_bound()/upper_bound()， 迭代器的++，--

bitset, 圧位
    bitset<10000> s;
    ~, &, |, ^ // 取反， 位和， 位或， 位异或
    >>, <<     // 左右移动
    ==, !=
    []

    count()  返回有多少个1
    any()  判断是否至少有一个1
    none()  判断是否全为0
    set()  把所有位置成1
    set(k, v)  将第k位变成v
    reset()  把所有位变成0
    flip()  等价于~
    flip(k) 把第k位取
```

## 常用函数

```C++
#include<cmath>
pow(2,3)乘方运算
sqrt()
abs()
fmod(3.4,2.1)浮点取模
ceil()向上取整
floor()向下取整
round()四舍五入
cbrt()开三次方
hypot()计算斜边
sin(pi/2)
cos()
tan()
asin()
acos()
atan()
log()
log2()
log10()
#include<algorithm>
  fill(intArray,intArray+10,1)
  fill
```

## 快速排序

```C++
int arr[N];
void quickSort(int l, int r){
    if (r <= l) return; 
    int i = l - 1, j = r + 1;
    int x = arr[(l + r) >> 1]; 
    while (i < j){
        do i++; while (arr[i] < x); 
        do j--; while (x < arr[j]); 
        if (i < j) swap(arr[i], arr[j]);
    }
    quickSort(l, j) , quickSort(j + 1, r);
}
```

## 归并排序

```C++
void mergeSort(int l ,int r){
    if (r<=l)return;
    int mid = l + r >>1;
    mergeSort(l,mid), mergeSort(mid + 1,r);
    int k = 0 , i = l, j = mid +1;
    while(i <= mid && j <= r)
    {
        if (arr[i] <= arr[j] ) tmp[k++] = arr[i++];
        else tmp[k++] = arr[j++];
    }
    while(i<=mid) tmp[k++] = arr[i++];
    while(j<=r) tmp[k++] = arr[j++];
    for(int i = l ,j = 0 ;i<=r;i++,j++) arr[i] = tmp[j];
}
void merge_sort(int q[], int l, int r){
    if (l >= r) return;
    int mid = l + r >> 1;
    merge_sort(q, l, mid), merge_sort(q, mid + 1, r);
    int k = 0, i = l, j = mid + 1;
    while (i <= mid && j <= r)
        if (q[i] <= q[j]) tmp[k ++ ] = q[i ++ ];
        else tmp[k ++ ] = q[j ++ ]; // ans += mid - i + 1// 逆序对需要这个
    while (i <= mid) tmp[k ++ ] = q[i ++ ];
    while (j <= r) tmp[k ++ ] = q[j ++ ];
    for (i = l, j = 0; i <= r; i ++, j ++ ) q[i] = tmp[j];
}
```

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501021052764.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501021052764.png)

从j 后面开始比, 比如说 2 开始比, 2 比 3 小, 那么 3,5,7,9 都是逆序 mid - i + 1 个逆序对

## 整数二分

```C++
bool check(int x) {/* ... */} // 检查x是否满足某种性质
// 区间[l, r]被划分成[l, mid]和[mid + 1, r]时使用：
int bsearch_1(int l, int r){
    while (l < r){
        int mid = l + r >> 1;
        if (check(mid)) r = mid; // x <= a[mid] 
        else l = mid + 1;
    }
    return l;// 找不到的话,       (a) < x < (b)
             // l 是   b 的下标             
            // 但是相等时 ,返回第一个下标
            // 找 x <= a[s] 的第一个位置
    // lower_bound(begin() , end () , x ); //返回迭代器
} 
// 区间[l, r]被划分成[l, mid - 1]和[mid, r]时使用：
int bsearch_2(int l, int r){ 
    while (l < r){
        int mid = l + r + 1 >> 1;
        if (check(mid)) l = mid; // a[mid] <= x
        else r = mid - 1;
    }
    return l;// 找不到的话,       (a) < x < (b)
             // l 是   a 的下标  
            // 但是相等时,    返回最后一个下标
            // 找 a[s] <= x  的第一个位置
            // 和  upper_bound(begin() , end() , x);不一样一个返回前面，一个返回后面
}
```

这个板子和low/upper_bound不一样, 注意判断边界是`等于`还是`不等于`

## 二分答案

```C++
bool check(){};
int bsearch(int l ,int r ){
     int ans;
     while(l <= r ){ // 上面就是 l <= r 了, 和二分查找板子有所不同
       int mid =  l + r >> 1;
       if (check() <= x ){ // 这里一定是满足条件, 再记录, 
         ans  = mid;
         r = m - 1;
       }else {
         l = m + 1;
     }return ans;
}
```

## 三分

三分用来求单峰函数, 通过逼近法, 得到单峰值

```C++
for (int i = 1; i <= 1000; i++) {
        double lm = l + (r - l) / 3, rm = r - (r - l) / 3;
        if (check(lm) >= check(rm))l = lm;
        else r = rm;
    }
int t = n >>1 ; // 从1 开始
if (t & 1) x = t + 1 >>1 , y = t+x;       // 上取整
else       x = t >> 1    , y = t+x+1 ;    // 下取整
```

## 浮点二分

```C++
bool check(double x) {/* ... */} // 检查x是否满足某种性质
double bsearch_3(double l, double r){
    const double eps = 1e-6;   // eps 表示精度，取决于题目对精度的要求
    while (r - l > eps){
        double mid = (l + r) / 2;
        if (check(mid)) r = mid;
        else l = mid;
    }
    return l;
}
```

注意, 三次方根, 不需要分情况讨论, 单调函数何须讨论, 需要记住条件从 `[-inf,+inf ]`  讨论即可

## 高精度加减乘除

```C++
vector<int> add(vector<int> &A, vector<int> &B){
    if (A.size() < B.size()) return add(B, A);
    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ ){
        t += A[i];
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }
    if (t) C.push_back(t);
    return C;
}
vector<int> sub(vector<int> &A, vector<int> &B){
    vector<int> C;
    for (int i = 0, t = 0; i < A.size(); i ++ ){
        t = A[i] - t;
        if (i < B.size()) t -= B[i];
        C.push_back((t + 10) % 10);
        if (t < 0) t = 1;
        else t = 0;
    }
    removeZero(C);
    return C;
}
vector<int> mul(vector<int> &A, vector<int> &B) {
    vector<int> C(A.size() + B.size() + 7, 0); // 初始化为 0
    for (int i = 0; i < A.size(); i++)
        for (int j = 0; j < B.size(); j++)
            C[i + j] += A[i] * B[j];

    int t = 0;
    for (int i = 0; i < C.size(); i++) { 
        t += C[i];
        C[i] = t % 10;
        t /= 10;
    }
    removeZero(C);
    return C;
}
vector<int> div(vector<int> &A, int b, int &r){
    vector<int> C;
    r = 0;
    for (int i = A.size() - 1; i >= 0; i -- )
    {
        r = r * 10 + A[i];
        C.push_back(r / b);
        r %= b;
    }
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    return C;
}
void removeZero(vector<int>&a){
   while( a.size() > 1 &&  0 == a.back() )   a.pop_back();
}
void printNum(vector<int>& a){
 removeZero(a); // 保险点加上这个
 for(int i = a.size()-1 ; 0<=i ;i--){
         cout<<a[i];
 }
}
void cinNum(vector<int>&a){
 string tmp;cin>>tmp;
 for(int i =tmp.size()-1 ; 0<=i;i--){
     a.push_back(tmp[i]-'0');   
 }removeZero(a);
}
int above(vector<int>&a ,vector<int>&b){
    if (a.size() > b.size()) return 1;
    else if (a.size() == b.size()){
        for(int i = a.size()-1; 0<=i ; i--){
            if (a[i] > b[i]) 
                return 1;
            else if (a[i] < b[i]) return 0;
        }
    }return 0;
}
```

## 前缀和差分

### 一维前缀和

```C++
// 构造s
s[i]  = s[i-1] + a[i]
// a[l] +... + a[r]
s[r] - s[l-1] == a[l] + a[l+1] + ... + a[r];
```

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501021432446.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501021432446.png)

### 二维前缀和

```C++
// 构造s
s[y][x]  = s[y-1][x] + s[y][x-1] - s[y-1][x-1] + a[y][x]
// a[y1][x1] + ... + a[y2][x2]
矩阵元素求和 = s[y2][x2] - s[y2][x1-1] - s[y1-1][x2] + s[y1-1][x1-1]
```

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501021501573.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501021501573.png)

### 一维差分

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501021537516.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501021537516.png)

```C++
//构造
a[i] = s[i] - s[i-1]
//给区间[l, r]中的每个数加上c：
a[l] += c, a[r + 1] -= c 
//还原
s[i] = s[i-1] + a[i];
```

### 二维差分

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501021549145.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501021549145.png)

```C++
//构造
a[y][x] = s[y][x] - s[y-1][x] - s[y][x-1] + s[y-1][x-1];
//矩阵内每个元素加c
a[y1][x1]+=c , a[y2+1][x1]-=c , a[y1][x2+1]-=c; a[y2+1][x2+1]+=c;
//还原
s[y][x] = s[y-1][x] + s[y][x-1] -s[y-1][x-1] + a[y][x];
```

## 双指针

> 此类问题, 尽可能让其不要回溯, 否则会变成O(n^2)的算法

- acwing799`最长连续不重复子序列`给定一个长度为 n 的整数序列，请找出最长的不包含重复的数的连续区间，输出它的长度。

```C++
int a[N] , vis[N];
int main(){
    int n ;cin >>n;
    for(int i = 0 ;i<n ;i++) cin>>a[i];
    int ans = 0 , l = 0  , r  = 0 ;
    for( ; r<n ; r++ ){
        vis[a[r]] ++;
        while(l < r && vis[a[r]] > 1) {
            vis[  a[l]  ] -- , l ++ ;
        }
        ans = max(ans ,r-l+1);
    }
    cout <<ans<<endl;
}
```

- acwing800 数组元素的目标和…
- acwing2816判断子序列…

> 常见问题分类：  (1) 对于一个序列，用两个指针维护一段区间  (2) 对于两个序列，维护某种次序，比如归并排序中合并两个有序序列的操作

```C++
for (int i = 0, j = 0; i < n; i ++ ){
    while (j < i && check(i, j)) j ++ ;
    // 具体问题的逻辑
}
```

## 位运算

- 求n 的低k位数字: `n>> k & 1`
- 返回n的最后一位1: `n = n & -n` （返回的是二进制 ， 例如说 0110 ， 返回 0010）

例: 统计int k中1的个数 (太优美了)

```C++
int getK(int k){
    int cnt = 0 ;
    for(int i = k ; i ; i-= i&-i) cnt++;
    return cnt;
}
```

## 离散化和区间合并

### 离散化

```C++
#include<bits/stdc++.h>
using namespace std;
const int N = 300010; //n次插入和m次查询相关数据量的上界
int n, m;
int a[N];//存储坐标插入的值
int s[N];//存储数组a的前缀和
vector<int> alls;  //存储（所有与插入和查询有关的）坐标
vector<pair<int, int>> add, query; //存储插入和询问操作的数据
int find(int x) { //返回的是输入的坐标的离散化下标
    int l = 0, r = alls.size() - 1;
    while (l < r) {
        int mid = l + r >> 1;
        if (alls[mid] >= x) r = mid;
        else l = mid + 1;
    }return r + 1;
}
int main() {
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++) {
        int x, c;
        scanf("%d%d", &x, &c);
        add.push_back({x, c});
        alls.push_back(x);
    }
    for (int i = 1; i <= m; i++) {
        int l , r;
        scanf("%d%d", &l, &r);
        query.push_back({l, r});
        alls.push_back(l);
        alls.push_back(r);
    }
   //排序，去重
    sort(alls.begin(), alls.end());
    alls.erase(unique(alls.begin(), alls.end()), alls.end());
    //执行前n次插入操作
    for (auto item : add) {
        int x = find(item.first);
        a[x] += item.second;
    }
    //前缀和
    for (int i = 1; i <= alls.size(); i++) s[i] = s[i-1] + a[i];
    //处理后m次询问操作
    for (auto item : query) {
        int l = find(item.first);
        int r = find(item.second);
        printf("%d\n", s[r] - s[l-1]);
    }
    return 0;
}
```

模版

```C++
vector<int> alls; // 存储所有待离散化的值
sort(alls.begin(), alls.end()); // 将所有值排序
alls.erase(unique(alls.begin(), alls.end()), alls.end());   // 去掉重复元素
// 二分求出x对应的离散化的值
int find(int x){ // 找到第一个大于等于x的位置
    int l = 0, r = alls.size() - 1;
    while (l < r) {
        int mid = l + r >> 1;
        if (alls[mid] >= x) r = mid;
        else l = mid + 1;
    }
    return r + 1; // 映射到1, 2, ...n
}
```

### 区间合并

```C++
// 将所有存在交集的区间合并
typedef pair< int , int> PII;
void merge(vector<PII> &segs){
    vector<PII> res;
    sort(segs.begin(), segs.end());
    int st = -2e9, ed = -2e9;
    for (auto seg : segs)
        if (ed < seg.first){
            if (st != -2e9) res.push_back({st, ed});
            st = seg.first, ed = seg.second;
        }
        else ed = max(ed, seg.second);
    if (st != -2e9) res.push_back({st, ed});
    segs = res;
}
```

# 2. 基本数据结构

## 链表

### 单链表

![image-20250911161918895](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161918895.png)

```C++
// head存储链表头，e[]存储节点的值，ne[]存储节点的next指针，idx表示当前用到了哪个节点
int head, e[N], ne[N], idx;
// 初始化
void init(){
    head = -1;
    idx = 0;
}
// 在链表头插入一个数a
void addToHead(int a){
    e[idx] = a, ne[idx] = head, head = idx ++ ;
}
// 在第k次插入的元素后插入
void insert(int k ,int x){
    e[idx] = x , ne[idx] =  ne[k-1] , ne[k-1] = idx ++;
}
// 删除第k + 1 次插入的元素
void remove(int k){
    if // 不是头节点
        ne[k] = ne[ne[k]];
    else // 删除头结点
        head = ne[head];
}
void visit(){
    for(int i = head ; i != -1; i = ne[i])
        cout <<e[i]<<" ";
}
```

### 双链表

![image-20250911162019573](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911162019573.png)

```C++
// e[]表示节点的值，l[]表示节点的左指针，r[]表示节点的右指针，idx表示当前用到了哪个节点
int e[N], l[N], r[N], idx;
// 初始化
void init(){
    //0是左端点，1是右端点 
    r[0] = 1, l[1] = 0;
    idx = 2;
}
// 在节点a的右边插入一个数x , 如果在左边, insert(l[k] , x) 
void insert(int a, int x){
    e[idx] = x;
    l[idx] = a, r[idx] = r[a];
    l[r[a]] = idx, r[a] = idx ++ ;
}
// 或者这样写:
void insertR(int k, int x){
    e[idx] = x ; l[idx] = k ; r[idx] = r[k]; 
    l[r[k]] = idx;
    r[k] = idx++;
}
void insertL(int k , int x){
    e[idx]  = x;  l[idx] =  l[k] ; r[idx] = k;
    r[l[k]] = idx;
    l[k] = idx++;
}
// 删除节点
void remove(int a){
    l[r[a]] = l[a];
    r[l[a]] = r[a];
}
```

## 栈

保持左闭右开的习惯

### STL

```C++
stack<int> s;
s.pop() ;  cout << s.top() ; s.size() ; s.push(x);
```

### 单调栈

```C++
// 核心思想是让栈中从栈底到栈顶单调 ,插入x 之前, 把比x 大的都倒出来
for (int i =0 ;i< n;i ++){
    int x ;
    cin >>x;
    while(tt && s[tt-1] >= x) tt--;
    if (tt) cout <<s[tt-1] <<" ";
    else cout <<-1<<" "; 
    s[tt++] = x;
}
```

### 表达式求值 （递归写法参考牛客题单）

```C++
stack<int> num;
stack<char> op;
void eval(){
    auto b = num.top(); num.pop();
    auto a = num.top(); num.pop();
    auto c = op.top(); op.pop();
    int x;
    if (c == '+') x = a + b;
    else if (c == '-') x = a - b;
    else if (c == '*') x = a * b;
    else x = a / b;
    num.push(x);
}
int main(){
    unordered_map<char, int> pr{{'+', 1}, {'-', 1}, {'*', 2}, {'/', 2}};
    string str;
    cin >> str;
    for (int i = 0; i < str.size(); i ++ ){
        auto c = str[i];
        if (isdigit(c)){
            int x = 0, j = i;
            while (j < str.size() && isdigit(str[j]))
                x = x * 10 + str[j ++ ] - '0';
            i = j - 1;
            num.push(x);
        }
        else if (c == '(') op.push(c);
        else if (c == ')') {
            while (op.top() != '(') eval();
            op.pop();
        }
        else{
            while (op.size() && op.top() != '(' && pr[op.top()] >= pr[c]) eval();
            op.push(c);
        }
    }
    while (op.size()) eval();
    cout << num.top() << endl;
    return 0;
}
```

## 队列

### STL

```C++
queue <elem> q;
q.push( elem x );  elem q.front(); elem q.back();
q.pop();
q.size();
```

### 循环队列

```C++
// hh 表示队头，tt表示队尾的后一个位置
int q[N], hh = 0, tt = 0;
// 向队尾插入一个数
q[tt ++ ] = x;
if (tt == N) tt = 0;
// 从队头弹出一个数
hh ++ ;
if (hh == N) hh = 0;
// 队头的值
q[hh];
// 判断队列是否为空，如果hh != tt，则表示不为空
if (hh != tt)
```

### 单调队列

```C++
//常见模型：找出滑动窗口中的最大值/最小值
int hh = 0, tt = -1; // 队里面存的下标
for (int i = 0; i < n; i ++ ){
    while (hh <= tt && check_out(q[hh])) hh ++ ;  // 判断队头是否滑出窗口 , 改成if 也可以, 因为只前进一格
    while (hh <= tt && check(q[tt], i)) tt -- ;
    q[ ++ tt] = i;
}
```

### 滑动窗口

总体思路和单调栈类似， 整个窗口里都是从小到大排序，只不过这里存的是下标（方便固定窗口大小）

https://www.acwing.com/problem/content/156/

```C++
#include<bits/stdc++.h>
using namespace std;
const int N = 1e6+10;
deque<int > q; // 装下标
int a[N];
int main(){
    int n , k ;cin>>n>>k;
    for(int i = 0 ; i<n ; i++) cin >> a[i];
    for(int i = 0 ; i<n ; i++) {
        int x = a[i];
        if (q.size() && q.front() <= i - k ) q.pop_front();
        while (q.size() && x <= a[q.back()]) q.pop_back();
        q.push_back(i);
        if ( k - 1 <= i) cout << a[q.front()] <<" ";
    }
    q.clear();cout<<endl;
    for(int i = 0 ; i<n ; i++) {
        int x = a[i];
        if (q.size() && q.front() <= i - k ) q.pop_front();
        while (q.size() && a[q.back()] < x) q.pop_back();
        q.push_back(i);
        if ( k  - 1 <= i) cout << a[q.front()] <<" ";
    }
}
```

## 串

y 总的习惯是从 1 开始, 0的位置做通配符, 匹配的时候是p[i] == p[j+1]

### KMP

```C++
// s[]是长文本，p[]是模式串，n是p的长度，m是s的长度
int ne[N];
char s[M] , p[N];
int main(){
    int n , m;
    cin >>n >> p+1 >>m>>s+1;
    for (int i = 2, j = 0; i <= n; i ++ ){ 
        while (j && p[i] != p[j + 1]) j = ne[j];
        if (p[i] == p[j + 1]) j ++ ;
        ne[i] = j;
    } // 先构造next 表
    for (int i = 1, j = 0; i <= m; i ++ ){  // i 是主串， j是要匹配的串
        while (j && s[i] != p[j + 1]) j = ne[j];
        if (s[i] == p[j + 1]) j ++ ;
        if (j == n){
            j = ne[j];
        // 匹配成功后的逻辑
        // 输出下标 cout <<i - n <<" ";
        }
    }
}
```

## Trie树

26度的树  例如插入a b c   ,son [idx] [char] = 指针 , 通过idx 可以确定编号的结尾

```C++
int son[N][26], cnt[N], idx;
// 0号点既是根节点，又是空节点
// son[idx][u]存储树中每个节点的子节点 idx是自己的编号， 每个u是对应字母的位置
// cnt[]存储以每个节点结尾的单词数量
// 插入一个字符串 ,
void insert(char *str){
    int p = 0;
    for (int i = 0; str[i]; i ++ ){
        int u = str[i] - 'a';
        if (!son[p][u]) son[p][u] = ++ idx;
        p = son[p][u];
    }
    cnt[p] ++ ;
}
// 查询字符串出现的次数
int query(char *str){
    int p = 0;
    for (int i = 0; str[i]; i ++ ){
        int u = str[i] - 'a';
        if (!son[p][u]) return 0;
        p = son[p][u];
    }
    return cnt[p];
}
```

## 并查集

```C++
int p[N] , sz[N];
void init(int n){
    for(int i = 1; i<=n;i++) p[i]=i, // sz[i] = 1;
}
int find(int x){
    if (p[x]!= x) p[x] = find(p[x]);
    return p[x];
}
void merge(int a, int b){
    int ra = find(a),rb = find(b);
    if (ra != rb){
        // sz[ra] += sz[rb]; 
        p[ra] = rb;
    }else
        return ;
}
```

## 堆

```C++
int h[N] , cnt; // 完全二叉树, 从1开始
void down(int u){
    int t =  u ; 
    if (u * 2 <= cnt && h[u*2] < h[t] ) t = u*2;
    if (u * 2 + 1 <= cnt && h[u*2 + 1] < h[t]) t = u*2+1;
    if (u != t) swap (h[u] ,h[t]) , down(t);
}
void up(int u){
    while(u / 2 && h[u/2] > h[u]){
        hswap(u/2, u);    u/=2;
    }
}
void buildHeap(){ // floyd 建堆
    for(int i = n/2; i ; i--) down(i);// floyd bulid heap
}
// 堆可以用 priority_queue<elem>  来代替， 运算符重载， 需要自定义struct
struct elem { // 此种重载也适合于map
  int value;
  bool operator<(const elem & w)const{
    return value > w .value;
  }
};
struct Cmp{
bool operator()(const elem & a , const elem & b) {
  return a .value > b.value
  }
};
priority_queue<elem ,vector<elem> , Cmp> q; // pritority_queue < elem , 底层数据结构， 比较类>
```

## 哈希表

### 链式哈希

```C++
int h[N] , e[N] , ne[N] , idx;
void insert(int x){
    int k = (x % N + N) % N;
    e[idx] = x;  ne[idx] = h[k];
    h[k] = idx ++;
}
bool find(int x){
    int t = (x % N + N) % N;
    for(int i = h[t] ; i != -1 ; i = ne[i]){
        if(e[i] == x ) return true;
    }
    return false;
}
```

### 封闭哈希

```C++
int find(int x) {
    int t = (x % N + N) % N;
    while (h[t] != null && h[t] != x) {
        t++;
        if (t == N)  t = 0;
    }
    return t;  //如果这个位置是空的, 则返回的是他应该存储的位置
}
```

### 字符串哈希

|i|1|2|3|4|5|6|7|8|9|10| |-|-|-|-|-|-|-|-|-|-|-| |s|a|b|c|d|e|f|g|h|i|j| |h|a*M|a*M+b*M^2|a*M+b*M^2 +c*M^3|..|..|..|..|..|..|..| |p|M|M^2|M^3|M^4|M^5|..|..|..|..|..|

```C++
typedef unsigned long long ull; // ull 刚好溢出相当于取模
const int M = 131;
char str[N]; ull h[N],p[N];// h 装hash , p 装进制
ull get(int l ,int r){   return h[r] - h[l-1] * p[r-l +1];  }
void Khash(){
    for(int i = 1 ;i<=n;i++) 
        p[i] = p[i-1] * M  , h[i] = h[i-1] * M + str[i]; 
}
```

# 3. 图论

包括普通的树

**存储**

```
邻接矩阵
int g[N][N];
void add_edge(int a, int b, int v){
    g[a][b] = v;
}
邻接表
int h[N],
int ne[N],idx;
int e[N];
void add_edge(int a ,int b){ 
    e[idx] = b ,ne[idx] =h[a] , h[a] = idx++;
}
void init(){ idx = 0 ; memset(h,-1,sizeof h);}
int h[N] , idx;// head不变
struct edge{
  int to , ne , w ; // w表示边的权重
}e[N];
```

### DFS

```C++
int n , path[N];
bool vis[N];
void dfs(int u){
    if (u == n){ // 递归基
        return;
    }
    for (int i = 0; i < n; i ++ )// i : next_state
        if (!vis[i]){
            vis[u]  = true;
            path[u] = i + 1;
            dfs(u + 1);
            //vis[u] = false;// 求全部解则需要回溯
        }
}
通用思想
void dfs( elem :state){
    vis[state] = true
    if(终止条件) 
        //终止的操作 
        return;
    for(new_state : 转移模型)
        //处理vis
        dfs(new_state)
        //还原现场 (如果只需要一个结果, 不需要还原现场)
}
dfs(初始状态)
```

### BFS (PFS 换优先队列即可）

```C++
int bfs(){
    queue<type> q;
    q.push(start);// 初始化，包括初始元素入队， 初始点赋值等
    while(q.size()){
        auto t = q.front(); q.pop();           //出队列 元素标记为t
        for (int i = 0; i < 4; i ++ ){         //遍历t遍历树的下一层所有的状态"
            int x = t.first + dx[i], y = t.second + dy[i];
            if (!(1 <= x && x <=n && 1<=y && y<=m)) continue;//非法情况跳过(超出范围)
            if (g[x][y] == 'block')                 continue;//不可达
            if (~d[x][y])                           continue;//已访问过
            d[x][y] = d[t.first][t.second] + 1; // 更新距离
            q.push({x, y});// 放入队列
        }
    }
}
伪代码
queue<elem> q;
void bfs(elem :state){
    q.push(开始状态)
    while(q.size()){
        t = q.pop()
        for( st : t的下一层状态)
            if ( invalid (st) )continue;
            setvis(i);q.push(i);  
}
树的重心
```

> 给定一颗树，树中包含 n 个结点（编号 1∼n）和 n−1 条无向边。请你找到树的重心，并输出将重心删除后，剩余各个连通块中点数的最大值。  重心定义：重心是指树中的一个结点，如果将这个点删除后，剩余各个连通块中点数的最大值最小，那么这个节点被称为树的重心。

dfs( i )返回 以 i 为中心， 连通的大小

```C++
int h[N],e[M] , ne[M] , idx , ans = N , n;
bool vis[N];
void add(int a , int b){
    e[idx] = b ;
    ne[idx] = h[a];
    h[a] = idx ++;
}
int dfs(int u){ 
    vis[u] = true;
    int sum = 1,res = 0;
    for(int i = h[u];~i;i=ne[i]){
        int j= e[i];
        if (vis[j])continue;
        int vis_size = dfs(j);
        res = max (res ,vis_size);
        sum += vis_size; // 加上i，一共有多少个点
        }
    }
    int left = n - sum; 
    res = max(res , left);
    ans = min (res, ans);
    return sum;
}

int main(){
    cin >> n;
    memset(h,-1,sizeof h);
    for(int i = 0;i<n-1;i++){
        int a , b ; cin >>a >>b ; add(a,b) , add(b,a);
    }
    dfs(1); cout <<ans;
}
```

### 拓扑排序 (可以自定义队列， 也可以用一个vector 记录一下结果）

```C++
bool topsort(){
    int hh = 0, tt = -1;
    // din[i] 存储点i的入度
    for (int i = 1; i <= n; i ++ )
        if (!din[i]) q[ ++ tt] = i; // 入队
    while (hh <= tt){
        int t = q[hh ++ ]; // 出队，
        for (int i = h[t]; ~i ; i = ne[i]){
            int j = e[i];
            if (-- d[j] == 0) q[ ++ tt] = j;// 相连的点入度-1， 入度为0时加入队列
        }
    }
    // 如果所有点都入队了，说明存在拓扑序列；否则不存在拓扑序列。
    return tt == n - 1;// 也可以用vector 存，看是否有n个点
}
```

## 最短路径

迪杰斯特拉是用最短的边去更新其他 而spfa是上次更新的终点去更新其他边 贝尔曼则是非常暴力的每次更新所有边

|**算法**|**时间复杂度**|**限制/特点**|**其他说明**| |-|-|-|-| |**Dijkstra**|O((n+m)logm)|不能有负权边|常用于单源最短路径，若有负权边需考虑其他算法| |**Bellman-Ford（邻接矩阵）**|O(n^3)|不能有负权环|适用于含负权边但无负权环的场景| |**SPFA**|O(k×m)|不能有负权环|一种基于 Bellman-Ford 的优化算法| |**Floyd**|O(n^3)|可求多源最短路径|通常用于求所有点对最短路径|

- **n**：图中的顶点数
- **m**：图中的边数
- **k**：算法运行过程中某些边被松弛的平均次数（SPFA 分析中常用）

### dijkstra 算法

`朴素版`时间复杂度 $O(n^2+m)$ n表示点数,m表示边数（忽略即可）

```C++
int dijkstra(){ // g[][] 邻接矩阵形式
    memset(dis, 0x3f, sizeof dis);
    dis[1] = 0;
    for (int i = 0; i < n - 1; i++){
        int t = -1;
        for (int j = 1; j <= n; j++) // 找最近的点 dis[t]
            if (!vis[j] && (t == -1 || dis[t] > dis[j]))
                t = j;
        for (int j = 1; j <= n; j++) 
           // 在此基础上尝试 dis[t] + g[t][j] 更新 dis[j];
            dis[j] = min(dis[j], dis[t] + g[t][j]);
        vis[t] = true;
    }
    if ( dis[n] == 0x3f3f3f3f )
        return -1;
    return dis[n];
}
/******************** 邻接表 ********************/
int h[N], ne[N * 2], e[N * 2], idx, w[N * 2];
int dis[N];
bool vis[N];
void add(int a, int b, int v){
    e[idx] = b, ne[idx] = h[a];
    w[idx] = v;
    h[a] = idx++;
}
int dijkstra(){
    memset(dis, 0x3f, sizeof dis);
    dis[1] = 0;
    for (int i = 0; i < n - 1; i++)
    {
        int t = -1;
        for (int j = 1; j <= n; j++)
            if (!vis[j] && (t == -1 || dis[t] > dis[j]))
                t = j;

        for (int i = h[t]; i != -1; i = ne[i])
        {
            int node = e[i];
            dis[node] = min(dis[node], dis[t] + w[i]);
            // 就这里不一样, 其他一模一样
        }

        vis[t] = true;
    }
    if (dis[n] == 0x3f3f3f3f)
        return -1;
    return dis[n];
}
```

`堆优化版`时间复杂度$O(mlogn)$ n表示点数,m表示边数

```C++
int dijkstra(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    priority_queue<PII, vector<PII>, greater<PII>> heap;
    heap.push({0, 1}); // <dist , id>  , pair 默认用第一个键排序 
    while (heap.size()){
        auto t = heap.top(); heap.pop();
        int id = t.second, d = t.first;
        if(vis[id]) continue;
        vis[id] = 1;
        for (int i = h[id] ; ~i ; i = ne[i]){
            int j = e[i];
            if (dist[j] > d + w[i]){
                dist[j] = d + w[i];
                heap.push({dist[j], j});
            }
        }
    }
    if (dist[n] >= 0x3f3f3f3f) return -1; // 这边要写大于等于
    else return dist[n];
}
```

### Bellman-Ford 算法

```C++
int n, m;       // n表示点数，m表示边数
int dist[N], back[N];// dist[x]存储1到x的最短路距离, back 表示备份
struct Edge {    // 边，a表示出点，b表示入点，w表示边的权重
    int a, b, w;
}edges[M];
// 求1到n的最短路距离，如果无法从1走到n，则返回-1。
int bellman_ford(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    for (int i = 0; i < n; i ++ ){       //所有的边迭代 n 轮
        memcpy(back , dist ,sizeof dist);//保留副本
        for (int j = 0; j < m; j ++ ){
            int a = edges[j].a, b = edges[j].b, w = edges[j].w;
            dist[b] = min(dist[b] ,back[a] + w );
        }
    }
    if (dist[n] > 0x3f3f3f3f / 2) return -1;
    return dist[n];
}
```

### spfa 算法 (`队列`优化版的Bell-Ford算法) (负权边)

```C++
int h[M] , w[M] , ne[M] , idx, e[M] , dist[N], // cnt[N];
bool vis[N];
queue<int> q;
// 求1号点到n号点的最短路距离，如果从1号点无法走到n号点则返回-1
int spfa(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;q.push(1);
    vis[1] = 1;
    while (q.size()){
        auto t = q.front(); q.pop();
        vis[t] = false;
        for (int i = h[t]; ~i; i = ne[i]){
            int j = e[i];
            if (dist[j] > dist[t] + w[i]){
                dist[j] = dist[t] + w[i];
                if (!vis[j]){ // 不在队列中的元素入队
                    q.push(j);
                    vis[j] = 1;
                }
            }
        }
    }
}
```

`spfa`判断负环

```C++
bool spfa(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0;
    queue<int> q;
    for (int i = 1; i <= n; i++){
        q.push(i);
        vis[i]  = true;
    }
    while (q.size()){
        auto t = q.front(); q.pop();
        vis[t] = false;
        for (int i = h[t]; i != -1; i = ne[i]){
            int j = e[i];
            if (dist[j] > dist[t] + w[i]){
                dist[j] = dist[t] + w[i];
                cnt[j] = cnt[t] + 1; // 到此说明j号点，已经是最优解
                if (cnt[j] >= n ) return true;
                if (!vis[j]){
                    q.push(j);
                    vis[j] = true;
    }}}}
    return false;
}
```

### floyd算法

```C++
void init(){
    for (int i = 1; i <= n; i ++ )
        for (int j = 1; j <= n; j ++ )
            if (i == j) d[i][j] = 0;
            else d[i][j] = INF;
}
// 算法结束后，d[a][b]表示a到b的最短距离 d[a][b] > inf /2 为不可达
void floyd()
{
    for (int k = 1; k <= n; k ++ )
        for (int i = 1; i <= n; i ++ )
            for (int j = 1; j <= n; j ++ )
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
}
```

## 最小生成树

### prim

```cpp
朴素版
int n;      // n表示点数
int g[N][N];        // 邻接矩阵，存储所有边
int dist[N];        // 存储其他点到当前最小生成树的距离
bool st[N];     // 存储每个点是否已经在生成树中
// 如果图不连通，则返回INF(值是0x3f3f3f3f), 否则返回最小生成树的树边权重之和
int prim(){
    memset(dist, 0x3f, sizeof dist);
    dist[1] = 0; // 整个图从1号节点开始生成
    int res = 0;
    for (int i = 0; i < n; i ++ ){
        int t = -1;
        for (int j = 1; j <= n; j ++ )
            if (!st[j] && (t == -1 || dist[t] > dist[j]))//找距离生成树最近的点
                t = j;

        if (dist[t] == INF) return INF;// 不可达说明不是单连通图
        res += dist[t]; // 可达则加上到树的距离
        st[t] = true;

        for (int j = 1; j <= n; j ++ ) dist[j] = min(dist[j], g[t][j]);
        // 生成树变大, 更新其他点的距离
    }
    return res;
}
```

上面代码的时间复杂度为 O(n^2)。

与Dijkstra类似，Prim算法也可以用堆优化，优先队列代替堆，优化的Prim算法时间复杂度O(mlogn)。适用于稀疏图，但是稀疏图的时候求最小生成树，Kruskal 算法更加实用。

### Kruskal

```C++
int n, m;       // n是点数，m是边数
int p[N];       // 并查集的父节点数组
struct Edge{    // 存储边
    int a, b, w;
    bool operator< (const Edge &W)const{
        return w < W.w;
    }
}edges[M];
int find(int x) {  // 并查集核心操作
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}
int kruskal(){
    sort(edges, edges + m);
    for (int i = 1; i <= n; i ++ ) p[i] = i;    // 初始化并查集
    int res = 0, cnt = 0;
    for (int i = 0; i < m; i ++ ){
        int a = edges[i].a, b = edges[i].b, w = edges[i].w;
        a = find(a), b = find(b);
        if (a != b){ // 如果两个连通块不连通，则将这两个连通块合并
            p[a] = b;
            res += w;
            cnt ++ ;
        }
    }
    if (cnt < n - 1) return INF;
    return res;
}
```

## 其他

### 染色法二分图

```C++
int color[N];      // -1 means black , 0 means not write , 1 means white
bool dfs(int u, int c){ // try to use c to write node u  ; return  bin-graph ?
    color[u] = c;
    for (int i = h[u]; i != -1; i = ne[i]){
        int j = e[i];
        if (!color[j]){
            if (!dfs(j, -c))
                return false;
        }
        else if (color[j] == c)
            return false;
        // else if(color[j] == !c ) that means it is correct;
    }
    return true;
}
bool check(){
    memset(color, -1, sizeof color);
    bool flag = true;
    for (int i = 1; i <= n; i ++ )
        if (color[i] == -1)
            if (!dfs(i, 0)){
                flag = false;
                break;
            }
    return flag;
}
```

### 旬牙利 TODO(没理解， 直接答案抄过来了）

用于求二分图的最大匹配

```C++
int n1, n2;     // n1表示第一个集合中的点数，n2表示第二个集合中的点数
int h[N], e[M], ne[M], idx;
//邻接表存储所有边匈牙利算法中只会用到从第一个集合指向第二个集合的边，所以这里只用存一个方向的边
int match[N];   // 存储第二个集合中的每个点当前匹配的第一个集合中的点是哪个
bool st[N];     // 表示第二个集合中的每个点是否已经被遍历过
bool find(int x){
    for (int i = h[x]; i != -1; i = ne[i]){
        int j = e[i];
        if (!st[j]){
            st[j] = true;
            if (match[j] == 0 || find(match[j])){
                match[j] = x;
                return true;
            }
        }
    }
    return false;
}
// 求最大匹配数，依次枚举第一个集合中的每个点能否匹配第二个集合中的点
int res = 0;
for (int i = 1; i <= n1; i ++ ){
    memset(st, false, sizeof st);
    if (find(i)) res ++ ;
}
```

# 4. 数论

## 试除法判定质数

```C++
bool is_prime(int x){
    if (x < 2) return false;
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0)
            return false;
    return true;
}
```

## 试除法分解质因数

$n=p*1^{a*1} * p*2^{a*2} *p*3^{a*3}    …..    p*n^{a*n} $        $p_i$ 是质数

```C++
void divide(int x){
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0){
            int s = 0;
            while (x % i == 0) x /= i, s ++ ;
            cout << i << ' ' << s << endl;
        }
    if (x > 1) cout << x << ' ' << 1 << endl;
}
```

## 求素数

### 朴素筛

```C++
int primes[N], cnt; // primes[]存储所有素数
bool st[N];         // st[x]存储x是否被筛掉
void get_primes(int n){
    for (int i = 2; i <= n; i ++ ){
        if (st[i]) continue;
        primes[cnt ++ ] = i;
        for (int j = i + i; j <= n; j += i)
            st[j] = true;
    }
}
```

### 线性筛

```C++
int primes[N], cnt; // primes[]存储所有素数
bool st[N];         // st[x]存储x是否被筛掉
void get_primes(int n){
    for (int i = 2; i <= n; i ++ ){
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ ){
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}
```

### 埃式筛(不如线性筛)

## 试除法求约数

约数 n = a * b   ,求所有的a和b

```C++
vector<int> get_divisors(int x){
    vector<int> res;
    for (int i = 1; i <= x / i; i ++ )
        if (x % i == 0){
            res.push_back(i);
            if (i != x / i) res.push_back(x / i);
        }
    sort(res.begin(), res.end());
    return res;
}
```

## 约数个数和约数之和

如果 N = $p*1^{c*1} * p*2^{c*2}* … *p*k^{c*k}$

约数个数： $(c*1 + 1) \* (c*2 + 1) * … * (c_k + 1)$

约数之和：$ (p*1^0 + p*1^1 + … + p*1^{c*1}) * … * (p*k^0 + p*k^1 + … + p*k^{c*k})$

```C++
// 先分解质因数 
long long res = 1 ;unordered_map <int,int> primes
for(auto p : primes){
  LL a = p.first, b = p.second;
  LL t = 1;
  while (b -- ) t = (t * a + 1) % mod;
  res = res * t % mod;
}
```

## 欧几里得算法

```C++
int gcd(int a, int b){
    return b ? gcd(b, a % b) : a;
}
```

## 求欧拉函数

```C++
int phi(int x){
    int res = x;
    for (int i = 2; i <= x / i; i ++ )
        if (x % i == 0){
            res = res / i * (i - 1);
            while (x % i == 0) x /= i;
        }
    if (x > 1) res = res / x * (x - 1);
    return res;
}
```

## 筛法求欧拉函数

```C++
int primes[N], cnt;     // primes[]存储所有素数
int euler[N];           // 存储每个数的欧拉函数
bool st[N];         // st[x]存储x是否被筛掉

void get_eulers(int n){
    euler[1] = 1;
    for (int i = 2; i <= n; i ++ ) {
        if (!st[i]){
            primes[cnt ++ ] = i;
            euler[i] = i - 1;
        }
        for (int j = 0; primes[j] <= n / i; j ++ ){
            int t = primes[j] * i;
            st[t] = true;
            if (i % primes[j] == 0){
                euler[t] = euler[i] * primes[j];
                break;
            }
            euler[t] = euler[i] * (primes[j] - 1);
        }
    }
}
```

## 快速幂

```C++
求 m^k mod p，时间复杂度 O(logk)。
int qmi(int m, int k, int p) {
    int res = 1 % p, t = m;
    while (k){
        if (k&1) res = res * t % p;
        t = t * t % p;
        k >>= 1;
    }
    return res;
}
```

## 扩展欧几里得

```C++
// 求x, y，使得ax + by = gcd(a, b)
int exgcd(int a, int b, int &x, int &y){
    if (!b){
        x = 1; y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= (a/b) * x;
    return d;
}
```

## 高斯消元

```C++
// a[N][N]是增广矩阵
int gauss(){
    int c, r;
    for (c = 0, r = 0; c < n; c ++ ){
        int t = r;
        for (int i = r; i < n; i ++ )   // 找到绝对值最大的行
            if (fabs(a[i][c]) > fabs(a[t][c]))
                t = i;

        if (fabs(a[t][c]) < eps) continue;
        for (int i = c; i <= n; i ++ ) swap(a[t][i], a[r][i]);      // 将绝对值最大的行换到最顶端
        for (int i = n; i >= c; i -- ) a[r][i] /= a[r][c];      // 将当前行的首位变成1
        for (int i = r + 1; i < n; i ++ )       // 用当前行将下面所有的列消成0
            if (fabs(a[i][c]) > eps)
                for (int j = n; j >= c; j -- )
                    a[i][j] -= a[r][j] * a[i][c];
        r ++ ;
    }

    if (r < n){
        for (int i = r; i < n; i ++ )
            if (fabs(a[i][n]) > eps)
                return 2; // 无解
        return 1; // 有无穷多组解
    }
    for (int i = n - 1; i >= 0; i -- )
        for (int j = i + 1; j < n; j ++ )
            a[i][n] -= a[i][j] * a[j][n];
    return 0; // 有唯一解
}
```

## 递推法求组合数

```C++
// c[a][b] 表示从a个苹果中选b个的方案数
for (int i = 0; i < N; i ++ )
    for (int j = 0; j <= i; j ++ )
        if (!j) c[i][j] = 1;
        else c[i][j] = (c[i - 1][j] + c[i - 1][j - 1]) % mod;
```

## 通过预处理逆元的方式求组合数

```C++
//首先预处理出所有阶乘取模的余数fact[N]，以及所有阶乘取模的逆元infact[N]
//如果取模的数是质数，可以用费马小定理求逆元
int qmi(int a, int k, int p) {   // 快速幂模板
    int res = 1;
    while (k){
        if (k & 1) res = (LL)res * a % p;
        a = (LL)a * a % p;
        k >>= 1;
    }
    return res;
}
// 预处理阶乘的余数和阶乘逆元的余数
fact[0] = infact[0] = 1;
for (int i = 1; i < N; i ++ ){
    fact[i] = (LL)fact[i - 1] * i % mod;
    infact[i] = (LL)infact[i - 1] * qmi(i, mod - 2, mod) % mod;
}
```

## Lucas定理

```C++
//若p是质数，则对于任意整数 1 <= m <= n，有：
//    C(n, m) = C(n % p, m % p) * C(n / p, m / p) (mod p)

int qmi(int a, int k, int p){  // 快速幂模板
    int res = 1 % p;
    while (k){
        if (k & 1) res = (LL)res * a % p;
        a = (LL)a * a % p;
        k >>= 1;
    }
    return res;
}

int C(int a, int b, int p){  // 通过定理求组合数C(a, b)
    if (a < b) return 0;
    LL x = 1, y = 1;  // x是分子，y是分母
    for (int i = a, j = 1; j <= b; i --, j ++ ){
        x = (LL)x * i % p;
        y = (LL) y * j % p;
    }
    return x * (LL)qmi(y, p - 2, p) % p;
}

int lucas(LL a, LL b, int p){
    if (a < p && b < p) return C(a, b, p);
    return (LL)C(a % p, b % p, p) * lucas(a / p, b / p, p) % p;
}
```

## 分解质因数法求组合数

```C++
/*  当我们需要求出组合数的真实值，而非对某个数的余数时，分解质因数的方式比较好用：
    1. 筛法求出范围内的所有质数
    2. 通过 C(a, b) = a! / b! / (a - b)! 这个公式求出每个质因子的次数。 n! 中p的次数是 n / p + n / p^2 + n / p^3 + ...
    3. 用高精度乘法将所有质因子相乘
*/
int primes[N], cnt;     // 存储所有质数
int sum[N];     // 存储每个质数的次数
bool st[N];     // 存储每个数是否已被筛掉
void get_primes(int n) {     // 线性筛法求素数
    for (int i = 2; i <= n; i ++ ) {
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ ){
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}
int get(int n, int p){    // 求n！中的次数
    int res = 0;
    while (n){
        res += n / p;
        n /= p;
    }return res;
}
vector<int> mul(vector<int> a, int b)  {     // 高精度乘低精度模板
    vector<int> c;int t = 0;
    for (int i = 0; i < a.size(); i ++ ){
        t += a[i] * b;
        c.push_back(t % 10);
        t /= 10;
    }while (t){
        c.push_back(t % 10);
        t /= 10;
    }return c;
}
get_primes(a);  // 预处理范围内的所有质数
for (int i = 0; i < cnt; i ++ ) {    // 求每个质因数的次数

    int p = primes[i];
    sum[i] = get(a, p) - get(b, p) - get(a - b, p);
}
vector<int> res;
res.push_back(1);
for (int i = 0; i < cnt; i ++ )     // 用高精度乘法将所有质因子相乘
    for (int j = 0; j < sum[i]; j ++ )
        res = mul(res, primes[i]);
```

## 卡特兰数

```C++
给定n个0和n个1，它们按照某种顺序排成长度为2n的序列，满足任意前缀中0的个数都不少于1的个数的序列的数量为： Cat(n) = C(2n, n) / (n + 1)
```

## NIM游戏

给定N堆物品，第i堆物品有Ai个。两名玩家轮流行动，每次可以任选一堆，取走任意多个物品，可把一堆取光，但不能不取。取走最后一件物品者获胜。两人都采取最优策略，问先手是否必胜。

我们把这种游戏称为NIM博弈。把游戏过程中面临的状态称为局面。整局游戏第一个行动的称为先手，第二个行动的称为后手。若在某一局面下无论采取何种行动，都会输掉游戏，则称该局面必败。

所谓采取最优策略是指，若在某一局面下存在某种行动，使得行动后对面面临必败局面，则优先采取该行动。同时，这样的局面被称为必胜。我们讨论的博弈问题一般都只考虑理想情况，即两人均无失误，都采取最优策略行动时游戏的结果。

NIM博弈不存在平局，只有先手必胜和先手必败两种情况。

定理： NIM博弈先手必胜，当且仅当 A1 ^ A2 ^ … ^ An != 0

## 公平组合游戏ICG

若一个游戏满足：

由两名玩家交替行动；

1. 在游戏进程的任意时刻，可以执行的合法行动与轮到哪名玩家无关；
2. 不能行动的玩家判负；

则称该游戏为一个公平组合游戏。

NIM博弈属于公平组合游戏，但城建的棋类游戏，比如围棋，就不是公平组合游戏。因为围棋交战双方分别只能落黑子和白子，胜负判定也比较复杂，不满足条件2和条件3。

## 有向图游戏

给定一个有向无环图，图中有一个唯一的起点，在起点上放有一枚棋子。两名玩家交替地把这枚棋子沿有向边进行移动，每次可以移动一步，无法移动者判负。该游戏被称为有向图游戏。

任何一个公平组合游戏都可以转化为有向图游戏。具体方法是，把每个局面看成图中的一个节点，并且从每个局面向沿着合法行动能够到达的下一个局面连有向边。

## Mex运算

设S表示一个非负整数集合。定义mex(S)为求出不属于集合S的最小非负整数的运算，即：

mex(S) = min{x}, x属于自然数，且x不属于S

## SG函数

在有向图游戏中，对于每个节点x，设从x出发共有k条有向边，分别到达节点y1, y2, …, yk，定义SG(x)为x的后继节点y1, y2, …, yk 的SG函数值构成的集合再执行mex(S)运算的结果，即：

SG(x) = mex({SG(y1), SG(y2), …, SG(yk)})

特别地，整个有向图游戏G的SG函数值被定义为有向图游戏起点s的SG函数值，即SG(G) = SG(s)。

## 有向图游戏的和

设G1, G2, …, Gm 是m个有向图游戏。定义有向图游戏G，它的行动规则是任选某个有向图游戏Gi，并在Gi上行动一步。G被称为有向图游戏G1, G2, …, Gm的和。

有向图游戏的和的SG函数值等于它包含的各个子游戏SG函数值的异或和，即：

SG(G) = SG(G1) ^ SG(G2) ^ … ^ SG(Gm)

## 定理

有向图游戏的某个局面必胜，当且仅当该局面对应节点的SG函数值大于0

有向图游戏的某个局面必败，当且仅当该局面对应节点的SG函数值等于0。

# 5. 动态规划

**闫氏 DP 大法**

1. 状态表示
   1. f (x,y,z,…) = 表示的集合
   2. f (x,y,z,…)的属性 min 或 max
2. 状态计算
   1. 分类讨论
   2. 递推方程 (后无效性原则)

## 背包问题

这里包括了所有背包9讲的内容

### 01 背包

> n 件物品, 容量 m 的背包,  第i件物品, 体积为v[i] , 价值为w[i]  求 能够拿取的最大价值

```C++
/*  f[i][j] 表示  前i个物品,总体积为j的最大价值
    1. 第i件物品放不下时             f[i][j] = f[i-1][j];
    2. 第i件物品放得下时,考虑拿或不拿 f[i][j] = max(f[i-1][j-v[i]]+w[i],f[i-1][j])
*/
const int N =1e3+10;
int f[N][N] ;// f[i][j] 表示前i个物品, 背包j容量的最优解
int n ,m, v[N] , w[N];
int main(){
    cin>>n>>m;
    for(int i = 1;i<=n;i++) cin >>v[i] >>w[i];
    for(int i = 1 ;i<=n;i++) // 枚举所有物品
        for(int j = 1;j<=m;j++) // 枚举所有体积
        {
            if (j<v[i]) f[i][j] = f[i-1][j];
            else f[i][j] = max(f[i-1][j] , f[i-1][j-v[i]] + w[i]);
        }
    cout <<f[n][m];
    return 0;
}
```

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image.png)

根据  `dp的后无效性原则`  每次都是在上一行的结果上更新, 可以直接构造1维数组, 不断更新即可(这样会丢失中间过程, 适合只需要结果的题) , **注意更新的时候从后往前, 防止覆盖数据**

状态转移方程:  二维:  dp[i][j] = max(dp[i-1][j] , dp[i-1][j - w[i]] + c[i] ); 一维:  dp[j]    =  max(dp       [j] , dp       [j - w[i]] + c[i] );   **从后往前, 防止覆盖**

```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e3 + 10;
int f[N]; // f[j] 背包j容量的最优解 , 第i个物品, 第i次刷新即可
int n, m, v[N], w[N];
int main(){
    cin >> n >> m;
    for (int i = 1; i <= n; i++)  cin >> v[i] >> w[i];
    for (int i = 1; i <= n; i++)     // 枚举所有物品
        for (int j = m; v[i] <= j; j--) // 枚举所有体积
            f[j] = max(f[j], f[j - v[i]] + w[i]);
    cout << f[m];
}
```

### 完全背包

> n `种` 物品, 容量 m 的背包,  第i件物品, 体积为v[i] , 价值为w[i] , `物品不限量`  求 能够拿取的最大价值

```C++
cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    for (int i = 1; i <= n; i++)        // 枚举所有物品
        for (int j = m; v[i] <= j; j--) // 枚举所有体积
            for (int k = 0; k <= j / v[i]; k++) // 这里多个循环遍历拿k个物品
                f[j] = max(f[j], f[j - k * v[i]] + k * w[i]);
```

状态转移方程:  二维:  dp[i][j] = max(dp[i-1][j] , dp[i] ****[j - w[i]] + c[i] ); 一维:  dp    [j] = max(dp       [j] , dp     ****[j ****- ****w[i]] + c[i] ); **从前往后**

```C++
cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i];
    for (int i = 1; i <= n; i++)        // 枚举所有物品
        for (int j = v[i]; j <= m; j++) // 枚举所有体积
              f[j] = max(f[j] , f[j - v[i]] + w[i] );
```

### 多重背包

> N `种` 物品, 容量 m 的背包,  第i件物品, 体积为v[i] , 价值为w[i] , `物品上限为n[i]`  求 能够拿取的最大价值

```C++
cin >> n >> m;
    for (int i = 1; i <= n; i++) cin >> v[i] >> w[i] >> s[i];
    for (int i = 1; i <= n; i++)        // 枚举所有物品
        for (int j = m; v[i] <= j; j--) // 枚举所有体积
            for (int k = 0; k <= min( j / v[i] , s[i] ); k++) 
                f[j] = max(f[j], f[j - k * v[i]] + k * w[i]);
```

二进制优化 ; 数字n可以表示成为2进制, 比如说15 = 1 + 2 + 4 + 8  所以相当于拿物品的时候, 可以一次拿多个, 不需要单次+1 去枚举 相当于 **把 s 个物品, 打包成 1, 2 , 4 , 8 , … , 这些组, 然后变成01背包问题**

```C++
int f[N]; // f[j] 背包j容量的最优解
int n, m, vv[N], ww[N], ss[N] , cnt = 1;
cin >> n >> m;
for (int i = 1; i <= n; i++){
        int v, w, s;
        cin >> v >> w >> s;
        for (int k = 1; k <= s; k <<= 1){ // 在这里打包物品, 转换为01背包
            s -= k;
            vv[cnt] = k * v, ww[cnt++] = k * w;
        }if (s > 0){
            vv[cnt] = s * v, ww[cnt++] = s * w;
        }
    }
for (int i = 1; i < cnt; i++)
    for (int j = m; vv[i] <= j; j--)
        f[j] = max(f[j], f[j - vv[i]] + ww[i]);
cout << f[m];
```

单调队列优化: (单调队列看前面的板子)  此部分可以跳过，属于男人8题的难度 f[j] = max(f[j] , f[j - k * vv[i]] +  k  *  ww[i]; 上述为基本转移方程, 在此基础上枚举每个k对应的最大值, 其实就是一个单调队列问题

TODO 代码

### 混合背包问题

> N `种` 物品, 容量 m 的背包,  第i件物品, 体积为v[i] , 价值为w[i] , `物品有可能**无**限, 有可能**有**限`  求 能够拿取的最大价值

上述问题的组合, 在分类跟新下一个物品 (分类讨论即可)

```C++
cin >> n >> m;
 vector<good> goods;
 goods.push_back({INF, INF, INF});
 for (int i = 1; i <= n; i++){
        int v, c, s;
        cin >> v >> c >> s;
        if (s == -1) // 01 背包
            goods.push_back({v, c, 1});
        else if (s == 0) // 完全背包
            goods.push_back({v, c, 0});
        else { // 转换为 01 背包   
            for (int k = 1; k <= s; k <<= 1){
                s -= k;
                goods.push_back({k * v, k * c, 1}); // 打包
            }if (s > 0)
                goods.push_back({s * v, s * c, 1});
        }
  }  n = goods.size();
  for (int i = 1; i <= n; i++){
        int v = goods[i].v, s = goods[i].s, c = goods[i].c;
        if (s == 1)
            for (int j = m; v <= j; j--)
                f[j] = max(f[j], f[j - v] + c);
        else if (s == 0)
            for (int j = v; j <= m; j++)
                f[j] = max(f[j], f[j - v] + c);
  }  cout << f[m];
```

### 分组背包问题

> N `组` 物品, 容量 m 的背包,  第i组第j件物品, 体积为v[i][j] , 价值为w[i][j] , `每组只能拿一个物品`  求 能够拿取的最大价值

```C++
int n, m;
int g[N];               // 下标是组号, 内容是组的大小
int vv[N][N], cc[N][N]; // 第一个标号是组, 第二个标号是对应组中第i个物品, 值是对应的v,w 
for (int i = 1; i <= n; i++)
    for (int j = m; 0 <= j; j--) // 枚举体积
        for (int k = 1; k <= g[i]; k++)
            if (vv[i][k] <= j)  f[j] = max(f[j], f[j - vv[i][k]] + cc[i][k]);
cout << f[m];
```

### 二维费用背包问题

> N `个` 物品, 体积 V , 最大负重W 的背包,  第i件物品, 体积为v[i] , 重量为w[i] 价值为c[j] ,  `每组只能拿一个物品`  求 能够拿取的最大价值

```C++
cin >> gn >> gv >> gw;
    for (int i = 1; i <= gn; i++){
        int v, w, c;
        cin >> v >> w >> c;
        for (int jv = gv; v <= jv; jv--)
            for (int jw = gw; w <= jw; jw--)
                f[jv][jw] = max(f[jv][jw], f[jv - v][jw - w] + c);
    } cout << f[gv][gw];
```

## 线性DP

此类问题注意两个问题

- **值是负的还是正的**, 初始化的时候边界取负值,  并初始化起点
- **状态转移**方程式, 以及遍历顺序

### 数字三角形

```C++
for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++) cin >> a[i][j];
    for (int i = 0; i <= n; i++)
        for (int j = 0; j <= i + 1; j++) f[i][j] = -INF; // 因为值可以取负的, 这里要格外注意
    f[1][1] = a[1][1];
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++){
            f[i][j] = max(f[i][j], f[i - 1][j] + a[i][j]); // 状态转移方程
            f[i][j] = max(f[i][j], f[i - 1][j - 1] + a[i][j]);
        }
    int res = -INF;
    for (int i = 1; i <= n; i++) // 走到最下面一层, 不是走到f[n][n]
        res = max(f[n][i], res);
    cout << res;
```

### LIS (largest increased sequence) 最长上升子序列

**朴素版$ O(n^2)$**

表示:  f[i] = max length(以 a[i] 结尾的最长上升子序列) 转移:    双指针, j <  i **a[j] < a[i] 时 , f[i] = max(f[i] , f[j] + 1)**

```C++
for (int i = 2; i <= n; i++){   
        f[i] = 1;// 这个可能更新不到, 但是最小是1
        for (int j = 1; j < i; j++)
            if (a[j] < a[i])
                f[i] = max(f[i], f[j] + 1);
    }int res = -INF;
    for(int i = 1 ;i<=n;i++ )
        res = max(res , f[i]);
```

**优化版O(nlogn)**

题解中最难理解的地方在于栈中序列虽然递增，但是每个元素在原串中对应的位置其实可能是乱的，那为什么这个栈还能用于计算最长子序列长度？

实际上这个栈【不用于记录最终的最长子序列】，而是【以stk[i]结尾的子串长度最长为i】或者说【长度为i的递增子串中，末尾元素最小的是stk[i]】。理解了这个问题以后就知道为什么新进来的元素要不就在末尾增加，要不就替代第一个大于等于它元素的位置。

这里的【替换】就蕴含了一个贪心的思想，对于同样长度的子串，我当然希望它的末端越小越好，这样以后我也有更多机会拓展。

```C++
int n; cin >> n;
vector<int>arr(n);
for (int i = 0; i < n; ++i)cin >> arr[i];
vector<int>stk;//模拟堆栈
stk.push_back(arr[0]);
for (int i = 1; i < n; ++i) {
    if (arr[i] > stk.back())//如果该元素大于栈顶元素,将该元素入栈
        stk.push_back(arr[i]);
    else//替换掉第一个大于或者等于这个数字的那个数
        *lower_bound(stk.begin(), stk.end(), arr[i]) = arr[i];
}
cout << stk.size() << endl;
```

### LCS(largest common sequence) 最长公共子序列

递归版本，数据结构讲过这个问题比较好理解 （要写递归的话可以用记忆化数组，用map 记录）

![https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/img/202501201441307.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/202501201441307.png)

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552253.png)

```C++
for(int i  = 1 ;i<=n;i++)
        for(int j = 1 ;j<=m;j++)
        {
            f[i][j] = max(f[i-1][j] , f[i][j-1]);
            if (A[i]==B[j]) f[i][j] = max(f[i][j] , f[i-1][j-1] + 1);
        }
    cout <<f[n][m];
```

### 最短编辑距离

属性 : f[i][j] 表示 a[1~ i ] 到 b[1~ j] 的最小操作数 转移 : 对最后一位做修改 1 . 删除操作: 删掉 x 之后匹配, 在此之前a[1~**i - 1**]和b[1~ **j**   ] 匹配  2 . 增加操作: 增加 x 之后匹配, 在此之前a[1~**i**     ]和b[1~ **j-1**] 匹配 3 . 修改操作: 修改 x 之后匹配, 在此之前a[1~**i - 1**]和b[1~ **j-1**] 匹配

```C++
void match(const char *A, const char *B){
    int n = strlen(A + 1) , m = strlen(B + 1); // 0 当做哨兵使用  
    for (int i = 0; i <= n; i++)    f[i][0] = i;
    for (int j = 0; j <= m; j++)     f[0][j] = j;
    for (int i = 1; i <= n; i++)
          for (int j = 1; j <= m; j++){
              f[i][j] = min(f[i - 1][j], f[i][j - 1]) + 1;// 状态1 2
              if (A[i] == B[j]) f[i][j] = min(f[i][j], f[i - 1][j - 1]);//状态3
              else f[i][j] = min(f[i][j], f[i - 1][j - 1] + 1);
            }
    cout << f[n][m];
}
```

## 区间DP

绝大多数区间问题先枚举区间长度, 再枚举区间左端点

### 石子合并

属性 : f[i][j] 表示合并 i ~ j 区间的最小代价 转移 :  1 . f[l][r] = f[l][m] +f[m+1][r] + a[l]+ … + a[r];  (这里要用到**前缀和**) 2 . 增加操作: 增加 x 之后匹配, 在此之前a[1~**i**     ]和 b[1~ **j-1** ] 匹配 3 . 修改操作: 修改 x 之后匹配, 在此之前a[1~**i - 1**]和 b[1~ **j-1** ] 匹配

```C++
for (int len = 2; len <= n; len++)
        for (int l = 1; l + len - 1 <= n; l++){
            int r = l + len - 1; f[l][r] = INF; 
            for (int k = l; k <= r; k++)
                f[l][r] = min(f[l][r], f[l][k] + f[k + 1][r] + s[r] - s[l - 1]);
        }
    cout << f[1][n] << endl;
```

## 计数DP

### 整数划分

> 一个正整数n可以表示成若干个正整数之和 , 现在给定一个正整数n，请你求出n共有多少种不同的划分方法。

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552318.png)

**思路1 [完全背包]: 把1,2,3,..n 看做n种物品(数量无限) , 问体积为n的总方案数** 属性 : f[i][j] 表示前 **i** 个整数(1,2,…,i)恰好拼成  **j**  的方案数 转移 :  f[i][j]   = f[i - 1][j] + f[i - 1][j - i] + f[i - 1][j - 2 * i] + …; f[i][j-i] = f[i-1][j-1]+ f[i-1][j-2 * i] + … ;  `把集合选0个i，1个i，2个i，…全部加起来` 故 : f[i][j] = f[i][j-i] + f[i-1][j] ; 这里使用完全背包滚动数组即可

```C++
int n ; cin >> n;
    f[0] = 1;
    for (int i = 1;i<=n;i++) 
        for(int j = i ;j<=n;j++)
            f[j]  = ( f[j-i] + f[j] )% mod;
    cout <<f[n];
```

**思路2 总和为i , 用 j 个数表示的方案数** 属性: f[i][j] 表示 总和为 i 用 j个数表示 转移: f[i][j]  = 方案中最小值为1和方案中最小值大于1 f[i][j]  = f[i-1][j-1]            + f[i-j][j] (每个值都 -1 , 一共减去j , 方案数不变)

```C++
int n;cin >> n;
    f[0][0] = 1;
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= i; j++)
            f[i][j] = (f[i - 1][j - 1] + f[i - j][j]) % mod;

    int res = 0;
    for (int i = 1; i <= n; i++) res =(res + f[n][i]) % mod;
    cout << res;
```

## 数位统计DP

可以不用vector存每一位，        直接计算某位的左边和右边的整数是多少。

可以不用讨论那么多细枝末节，只需要知道，当i为0时其左边整数不能为0，就够了。

```C++
# include <iostream>
# include <cmath>
using namespace std;
int dgt(int n){ // 计算整数n有多少位
    int res = 0;
    while (n) ++ res, n /= 10;
    return res;
}
int cnt(int n, int i){ // 计算从1到n的整数中数字i出现多少次 
    int res = 0, d = dgt(n);
    for (int j = 1; j <= d; ++ j) {// 从右到左第j位上数字i出现多少次
        // l和r是第j位左边和右边的整数 (视频中的abc和efg); dj是第j位的数字
        int p = pow(10, j - 1), l = n / p / 10, r = n % p, dj = n / p % 10;
        // 计算第j位左边的整数小于l (视频中xxx = 000 ~ abc - 1)的情况
        if (i) res += l * p; 
        if (!i && l) res += (l - 1) * p; // 如果i = 0, 左边高位不能全为0(视频中xxx = 001 ~ abc - 1)
        // 计算第j位左边的整数等于l (视频中xxx = abc)的情况
        if ( (dj > i) && (i || l) ) res += p;
        if ( (dj == i) && (i || l) ) res += r + 1;
    }
    return res;
}
int main(){
    int a, b;
    while (cin >> a >> b , a){
        if (a > b) swap(a, b);
        for (int i = 0; i <= 9; ++ i) cout << cnt(b, i) - cnt(a - 1, i) << ' ';
        cout << endl;
    } return 0;
}
```

## 状态压缩DP （这部分算hard难度了，经典问题都很复杂）

### 蒙德里安的梦想

> 图片来自b站某博主的, 后序会把链接贴上 TODO

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552388.png)

在此过程中保证不出现奇数个0

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552496.png)

然后要保证不重叠1, 不出现连续的1

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552574.png)

```C++
void initOdds(){
    for (int i = 0; i < 1 << n; i++){
        odd1[i] = true;
        int cnt = 0;
        for (int j = 0; j < n; j++){
            if (i >> j & 1){
                if (cnt & 1)
                    odd1[i] = 0, cnt = 0;
            }else cnt++;
        }if (cnt & 1)
            odd1[i] = 0;
    }
}int solve(){
    memset(f, 0, sizeof f);
    f[0][0] = 1;
    for (int i = 1; i <= m; i++){
        for (int j = 0; j < 1 << n; j++){
            for (int k = 0; k < 1 << n; k++){
                if ((j & k) == 0 && odd1[j | k])
                    f[i][j] += f[i - 1][k];
            }
        }
    }return f[m][0];
}
```

### 哈密顿最短回路

属性: f[state][j] 表示state 点被用过 , 目前停留在j上面 , state 用**位**表示状态 转移: f[state][j] = f[state_k][k] + wei[k][j]  `state_k 表示去除j之后的集合,state_k 包含k`

```C++
cin >> n;
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++)
        cin >> g[i][j];
memset(f, 0x3f3f3f3f, sizeof f);
f[1][0] = 0;
for (int state = 0; state < (1 << n); state++) // state 
    for (int id = 0; id < n; id++)
        if (vis(state , id))//state 包含id,
            for (int k = 0; k < n; k++)
            { // f[state][id]=f[state_k][k] + wei[k][j]
                int state_k = state - (1<<id);
              // state_k 包含k 不包含j state_k = i - (1<<j) 而且 ,state_k >> k & 1
                if (state_k >> k & 1)
                    f[state][id] = min(f[state_k][k]+ g[k][id] , f[state][id]); 
            }cout << f[(1<< n) - 1][n-1]; //2 ^ n - 1 全为1,表示所有点都在state中
```

## 树形dp

### 没有上司的舞会

属性 : f[u][0] 表示选择u为根结点的子树 , 不包括(u)结点           f[u][1] 表示  选择u为根结点的子树 ,    包括(u)结点 转移 :  dfs 遍历 , 选择u的时候,  那么 f[u][1] += 所有子节点f[s][0]                      不选择u的时候,   那么 f[u][0] += max(所有子节点f[s][0]  , 所有子节点f[s][1])

```C++
void dfs(int u){
    f[u][1] = happy[u];
    for (int i = h[u]; ~i; i = ne[i]){
        int j = e[i];//son
        dfs(j);
        f[u][0] += max(f[j][1], f[j][0]);
        f[u][1] += f[j][0];
    }
}//找root 开一个数组,找谁没有father就行,或者说输入的时候记录一下谁有father
ans = max(f[root][1] , f[root][0]);
```

## 记忆化搜索

用递归写总是很简单的, 但是会存在超时问题 于是可以用数组记录中间结果, 避免同一个问题重复递归 以fib 为例

递归版

```C++
int fib(int n ){
  if (n < 3 )
      return 1;
  return fib(n-1) + fib(n-2);
```

记忆化数组版

```C++
int a[N];
int fib(int n){
  if (a[n]) return a[n] ; // 有结果无需再次递归
  a[n] = fib(n-1) + fib(n-2);
  return a[n];
}
```

### 滑雪

属性 f[i][j] 表示从 i ,  j 出发, 最长的距离 转移 :  f[i +dx][j+dy] 四个方向 比当前矮 f[i][j] = max ( f[i + dx][j + dy] + 1  , f[i][j] );

```C++
int dp(int x, int y){
    int &v = f[x][y];
    if (~v) return v;
    v = 1; // 这个我也不知道为什么要加，但是不加就会错，很神秘
    for (int i = 0; i < 4; i++){
        int nx = x + dx[i], ny = y + dy[i];
        if (1 <= nx && nx <= r && 
            1 <= ny && ny <= c && h[nx][ny] < h[x][y]){
            v = max (dp(nx, ny) + 1 , v);
        }
    }
    return v;
}
```

# 6. 贪心算法

这类问题往往需要借助排序, 修改排序函数就非常重要 ，重载时一般重载小于号

1. 运算符重载

```C++
typedef struct Coord{ // pair 也是默认这种排序
  int l , r ;
  bool operator < (const Coord & other ) const{
    return this->l < other -> l; 
}Coord;// 第一个const 指 调用的对象不能修改, 第二个const 指 this 不能修改
```

1. 函数指针

```C++
typedef struct Coord{
  int l ,r ;
}Coord;
bool cmp (const Coord & a , const Coord & b){
  return a .l < b. l;
}
vector<Coord> coords;
sort(coords.begin() , coords.end() , cmp);
```

1. 匿名函数

匿名函数相当于 return 一个函数指针，功能同2 [&] , [*] , [ ] 的区别请自行搜索

```C++
std::sort(begin, end, [](const Coord& a, const Coord& b) {
    // 自定义比较逻辑
    return a . l < b . l; // 例如：按升序排序
});
int main(){
   // 这里的auto是函数指针function<int(int,int)>add = [&](int a,int b)
    auto add = [&] (int a, int b){
      return a + b;
    };
    int c  = add(1,2);
    cout <<c << endl; // 输出3
}
```

## 区间dp

### 区间选点

> 选最少的点覆盖所有区间

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552639.png)

```C++
#include<bits/stdc++.h>
using namespace std;
const int N =1e5+10;
typedef struct range{
    int l, r;
    bool operator < (const range & a ) const {
        return this->r < a .r; 
    }
}range;
vector<range>pairs;
stack<int> rr;
int n ;
int main(){
    cin >> n;
    for(int i = 0 ;i<n;i++){
        int a ,b ;
        cin >> a >>b;
        pairs.push_back({a,b});
    }sort(pairs.begin() , pairs.end());
    for(auto &pa: pairs ){
        if (rr.empty())
            rr.push(pa.r);
        else if (pa.l <= rr.top() && rr.top() <= pa.r)
            continue;
        else 
            rr.push(pa.r);
    }cout << rr.size();
}
```

### 最大不相交区间数量

同上  , 一模一样的代码

### 区间分组

> 给定 N 个闭区间 [ai,bi]，请你将这些区间分成若干组，使得每组内部的区间两两之间（包括端点）没有交集，并使得组数尽可能小。

输出最小组数。

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552707.png)

```C++
#include<bits/stdc++.h>
using namespace std;
const int N =1e5+10;
typedef struct range{
    int l, r;
    bool operator < (const range & a ) const {
        return this->l < a .l; 
    }
}range;
typedef priority_queue<int ,vector<int> , greater<int> > small_heap;
vector<range>pairs;
small_heap maxrs;
int n ;
int main(){
    cin >> n;
    for(int i = 0 ;i<n;i++) {
        int a ,b ;
        cin >> a >>b;
        pairs.push_back({a,b});
    }sort(pairs.begin() , pairs.end());
    for(auto &pa: pairs ){
        if (maxrs.empty())
            maxrs.push(pa.r);
        else if ( maxrs.top() < pa.l ) {// could insert this pair into now group
            maxrs.pop();
            maxrs.push(pa.r);
        }else 
            maxrs.push(pa.r);
    }cout << maxrs.size();
}
```

### 区间覆盖

> 给定 N 个区间 [ai,bi] 以及一个区间 [s,t]，请你选择尽量少的区间，将指定区间完全覆盖。

输出最少区间数，如果无法完全覆盖则输出 −1。

思路不太好想, 还是记一下比较好

![image.png](https://zzhaire-markdown.oss-cn-shanghai.aliyuncs.com/imgs/image-20250911161552773.png)

```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 10;
const int inf = 1e9;
typedef struct range{
    int l, r;
    bool operator<(const range &a) const{
        return this->l < a.l;
    }
} range;
vector<range> pairs;
int n;
int st, ed;
int rangeNum(){
    sort(pairs.begin(), pairs.end());
    int cnt = 0;
    for (int i = 0; i < n; ){
        int r = -inf;
        int j;
        for (j = i; j < n && pairs[j].l <= st; j++){
            r = max(r, pairs[j].r);
        }if (r < st) return -1;
        cnt++;
        if (ed <= r) return cnt;
        st = r; i = j ;
    }
    return -1; // never reach there  , just for compile 
}
int main(){
    cin >> st >> ed;
    cin >> n;
    for (int i = 0; i < n; i++){
        int a, b;
        cin >> a >> b;
        pairs.push_back({a, b});
    }
    cout << rangeNum() << endl;
    system("pause");
    return 0;
}
```

## Huffman 树

### 合并果子

用哈夫曼贪心和动态规划都可以

```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 10;
typedef priority_queue<int, vector<int>, greater<int>> SmallHeap;
SmallHeap small_heap;
int n;
int main(){
    cin >> n;
    for (int i = 0; i < n; i++){
        int a;
        cin >> a;
        small_heap.push(a);
    } int cnt = 0;
    while (1){
        if (small_heap.size() == 1 )break;
        int a = small_heap.top(); small_heap.pop();
        int b = small_heap.top(); small_heap.pop();
        cnt += a+b; small_heap.push(a+b); 
    }cout <<cnt;
    return 0;
}
```

## 排序不等式

### 排队打水

> 安排打水顺序, 使得等待时间最小

操作系统中进程的 短作业优先算法

```C++
#include<bits/stdc++.h>
using namespace std;
const int N =1e5+10;
int n ;
vector<int> wait_time; 
int main(){
    cin >> n;
    for(int i = 0;i<n;i++){
        int a ;cin>>a;
        wait_time.push_back(a);
    }sort(wait_time.begin() , wait_time.end());
    long long  time = 0;
    for(int i = 0 ; i<n;i++){
        time  +=  wait_time[i] * (n - 1 -i);
    }cout <<time;
}
```

## 绝对值不等式

### 仓库选址

> 数轴上选一个点, 其他数到这个点距离和的最小值

取中点， 偶数取最中间两个任意一个（可以取端点）

## 推公式

### 耍杂技的牛 （国王游戏，合并数字等都是）

写表达式，进行运算符重载，代码意义不大，都是尝试交换，然后取最优

