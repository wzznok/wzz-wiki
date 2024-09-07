# 笔记-C++

**作者:** WZZ-11 (wzz)

---

## 目录 (完善中……)
[|> 基础 <|](#基础)  
|—— [|O2优化|](#优化2)  
|—— [|O3优化|](#优化3)  
|—— [|标准模板|](#标准模板)  
|—— [|泛型编程|](#泛型编程)  
———————————————  
[|> 算法 <|](#算法)  
|—— [|二分查找|](#二分查找)  
|—— [|归并排序|](#归并排序)  
|—— [|高精度计算|](#高精度计算)  
|—— |—— [|高精度输入|](#高精度输入)  
|—— |—— [|高精度乘法|](#高精度乘法)  
|—— |—— [|高精度除法|](#高精度除法)  
|—— [|广度优先搜索模板|](#广度优先搜索模板)  
———————————————  
[|> 数据结构 <|](#数据结构)  
|—— [|树|](#树)  
|—— |—— [|树-基本概念及定义|](#树-基本概念及定义)  
|—— |—— [|二叉树-基本概念及定义和变体|](#二叉树-基本概念及定义和变体)  
|—— |—— [|树的遍历|](#树的遍历)  
|—— [|图|](#图)  
|—— |—— [|图-基本概念及定义|](#图-基本概念及定义)  
|—— |—— [|图-存储|](#图-存储)  
———————————————  

---

<span id="基础"></span>
## ==基础== 

<span id="优化2"></span>
### O2优化

```cpp
#pragma GCC optimize(2)
```

<span id="优化3"></span>
### O3优化

```cpp
#pragma GCC optimize(1)
#pragma GCC optimize(2)
#pragma GCC optimize(3)
#pragma GCC optimize("Ofast")
#pragma GCC optimize("inline")
#pragma GCC optimize("-fgcse")
#pragma GCC optimize("-fgcse-lm")
#pragma GCC optimize("-fipa-sra")
#pragma GCC optimize("-ftree-pre")
#pragma GCC optimize("-ftree-vrp")
#pragma GCC optimize("-fpeephole2")
#pragma GCC optimize("-ffast-math")
#pragma GCC optimize("-fsched-spec")
#pragma GCC optimize("unroll-loops")
#pragma GCC optimize("-falign-jumps")
#pragma GCC optimize("-falign-loops")
#pragma GCC optimize("-falign-labels")
#pragma GCC optimize("-fdevirtualize")
#pragma GCC optimize("-fcaller-saves")
#pragma GCC optimize("-fcrossjumping")
#pragma GCC optimize("-fthread-jumps")
#pragma GCC optimize("-funroll-loops")
#pragma GCC optimize("-freorder-blocks")
#pragma GCC optimize("-fschedule-insns")
#pragma GCC optimize("inline-functions")
#pragma GCC optimize("-ftree-tail-merge")
#pragma GCC optimize("-fschedule-insns2")
#pragma GCC optimize("-fstrict-aliasing")
#pragma GCC optimize("-falign-functions")
#pragma GCC optimize("-fcse-follow-jumps")
#pragma GCC optimize("-fsched-interblock")
#pragma GCC optimize("-fpartial-inlining")
#pragma GCC optimize("no-stack-protector")
#pragma GCC optimize("-freorder-functions")
#pragma GCC optimize("-findirect-inlining")
#pragma GCC optimize("-fhoist-adjacent-loads")
#pragma GCC optimize("-frerun-cse-after-loop")
#pragma GCC optimize("inline-small-functions")
#pragma GCC optimize("-finline-small-functions")
#pragma GCC optimize("-ftree-switch-conversion")
#pragma GCC optimize("-foptimize-sibling-calls")
#pragma GCC optimize("-fexpensive-optimizations")
#pragma GCC optimize("inline-functions-called-once")
#pragma GCC optimize("-fdelete-null-pointer-checks")
```
<span id="标准模板"></span>
### 标准模板

```cpp
#include<bits/stdc++.h>
using namespace std;
int main(){
    
    return 0;
}
```
<span id="泛型编程"></span>
### 泛型编程

##### tips: T可替换

```cpp
template<T>
T jia(T a,T b){
    return a + b;
}
```

---
<span id="算法"></span>
## ==算法== 

<span id="二分查找"></span>
### 二分查找

tips: l:左 r:右 t:寻找的数字 a[]:查找的数组

```cpp
int dichotomy(int l,int r,int t,long long int a[]){
    while(l<r){
        int mid=(l+r)/2;
        if(a[mid] >= t){
            r=mid;
        }
        else{
            l=mid+1;
        }
    }
    if(a[r]==t) return r;
    return -1;
}
```
<span id="归并排序"></span>

### 归并排序

```cpp
/* C++ Code */
//可更改数组大小 
int fun_temp[1000005];
void fun(int left_bj,int right_bj,int fun_sz[]){
	int fun_mid = (left_bj+right_bj)/2;
	if(left_bj==right_bj) return;
	fun(left_bj,fun_mid,fun_sz);
	fun(fun_mid+1,right_bj,fun_sz);
	int temp_l = left_bj,temp_j = fun_mid+1,temp_k = temp_l; 
	while(temp_l<=fun_mid && temp_j<=right_bj){
		if(fun_sz[temp_l] <= fun_sz[temp_j]) fun_temp[temp_k++] = fun_sz[temp_l++];
		else{
			fun_temp[temp_k++] = fun_sz[temp_j++];
		}
	} 
	while(temp_l<=fun_mid){
		fun_temp[temp_k++] = fun_sz[temp_l++];
	}
	while(temp_j<=right_bj){
		fun_temp[temp_k++] = fun_sz[temp_j++];
	}
	for(int i=left_bj;i<=right_bj;i++) fun_sz[i] = fun_temp[i];
}
//引用此函数(推荐)
//left:左边界  right:右边界  mer[]:数组名称(无需"[]")
void merge_s(int left,int right,int mer[],string mode){
	fun(left,right,mer);
	if(mode=="cover"){
		for(int i=left;i<=right;i++) mer[i] = fun_temp[i];
	}
	else if(mode!="staging"){
		cout<<"no mode:merge_s";
		return;
	}
}
```

---

<span id="高精度计算"></span>
### 高精度计算

<span id="高精度输入"></span>
#### 高精度输入

```cpp
//高精度输入: C++17 Code
//日期: 2024/4/13

//高精度输入(输入数字[控制台] | 输出数组)
//函数返回位数
const int MAX_INT=10005;
int hp_input(int a[]){
    char b[MAX_INT];
    cin>>b;
    int i=0;
    while(b[i]>='0' && b[i]<='9'){a[i]=b[i]-'0';i++;}
    return strlen(b);
}
```

<span id="高精度乘法"></span>
#### 高精度乘法

```cpp
//高精度乘: C++17 Code
//日期: 2024/4/13
//额外引用"高精度输入"(hp_input)

//高精度乘法(输入a[],b[],a_len,b_len | 输出out[])
//函数返回位数
int hp_multiplication(int a[],int b[],int a_len,int b_len,int out[]){
    int t_a[MAX_INT],t_b[MAX_INT],t_out[MAX_INT],len=a_len+b_len,t_s=0;
    for(int i=0;i<a_len;i++) t_a[a_len-i-1] = a[i];
    for(int i=0;i<b_len;i++) t_b[b_len-i-1] = b[i];
    for(int i=0;i<a_len;i++) for(int j=0;j<b_len;j++) t_out[i+j] += t_a[i] * t_b[j];
    for(int i=0;i<len;i++){t_out[i+1] += t_out[i]/10;t_out[i]%=10;}
    if(t_out[len-1]==0 && len>1) len--;
    for(int i=len-1;i>=0;i--){out[t_s] = t_out[i]; t_s++;}
    return len;
}

//-------------------------------------------------------------------------------------

//实例(A*B Problem): C++17 Code
int main(){
    int a[MAX_INT],b[MAX_INT],out[MAX_INT];
    int alen = hp_input(a);
    int blen = hp_input(b);
    int f = hp_multiplication(a,b,alen,blen,out);
    for(int i=0;i<f;i++){
        cout<<out[i];
    }
    return 0;
}
```

<span id="高精度除法"></span>
#### 高精度除法

```cpp
//高精度除法(高精度除以低精度): C++17 Code
//日期: 2024/4/13
//额外引用"高精度输入"(hp_input)

//高精度除法(输入a[],b,a_len, | 输出out[])
//函数返回位数
int hp_division(int a[],long long int b,int a_len,int out[]){
    int t_out[MAX_INT],a_t[MAX_INT],temp=0,s=0;
    long long x=0;
    for(int i=0;i<a_len;i++){
        a_t[i] = a[i];
    }
    for(int i=0;i<a_len;i++){
        t_out[i] = (a_t[i]+x*10) / b;
        x = (a_t[i] + x*10) % b;
    }
    while(t_out[temp]==0) temp++;
    for(int i=temp;i<a_len;i++){
        out[s] = t_out[i];
        s++;
    }
    return s;
}

//-------------------------------------------------------------------------------------

//实例(小学除法): C++17 Code
int main(){
    int a[MAX_INT],out[MAX_INT];
    long long b;
    int alen = hp_input(a);
    cin>>b;
    int num = hp_division(a,b,alen,out);
    for(int i=0;i<num;i++){
        cout<<out[i];
    }
    
    return 0;
}
```

---

<span id="广度优先搜索模板"></span>
### 广度优先搜索模板

```cpp
//广度优先搜索模板
//实例: 希蒙的上学之路2
//日期: 2024/6/8

//----------------------
//维护格子信息
struct Node{
    int x,y,step;
};
//标记数组
bool vis[505][505];//(根据题目修改)
//位移数组
int dx[4]={-1,0,1,0};
int dy[4]={0,1,0,-1};
// x,y地图长宽 map[a][b](a,b根据题目修改)  return输出(所需最短步数)
int bfs(int x,int y,char mp[505][505]){
    //st开始点 fi结束点 wa墙 (根据题目修改)
    char st='S',fi='T',wa='X';
    int st_x=0,st_y=0,fi_x=0,fi_y=0;
    for(int i=1;i<=x;i++){
        for(int j=1;j<=y;j++){
            if(mp[i][j] == st){st_x = i; st_y = j; }
            if(mp[i][j] == fi){fi_x = i; fi_y = j; }
        }
    }
    queue<Node> q;
    Node t={st_x,st_y,1};//第三位的 0 因题目而变
    q.push(t);
    vis[st_x][st_y] = 1;
    while(!q.empty()){
        t=q.front();
        q.pop();
        if(t.x == fi_x  && t.y == fi_y){
            return t.step;
        }
        for(int i=0;i<4;i++){
            int xx = t.x + dx[i];
            int yy = t.y + dy[i];
            if(mp[xx][yy]!=wa && xx<=x && xx>=1 && yy>=1 && yy<=y && vis[xx][yy]!=1){
                q.push({xx,yy,t.step+1});
                vis[xx][yy] = 1;
            }
        }
    }
    return -1;
}
//main主函数
int main(){
    int n,m;
    cin>>n>>m;
    char ma[505][505];
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>ma[i][j];
        }
    }
    cout<<bfs(n,m,ma);
    return 0;
}
//----------------------
```

---
<span id="数据结构"></span>
## ==数据结构== 
### **数据结构**
**数组，链表，栈，队列，哈希表，树，图，堆**

---

### STL容器

不涉及迭代器

#### 栈

```c
// 头文件 : <stack>
// 栈 :  1、先进后出   2、只能从一端进出，另一端封闭
// push   :  往栈里添加一个元素 (进栈、入栈、压栈) 
// pop    :  从栈顶删除一个元素 (出栈、弹栈)
// top    :  访问栈顶元素
// empty  :  判断栈是否为空，如果为空 1
// size   :  获取栈中元素的个数
```

#### 队列

```cpp
// 头文件 :  <queue>
// 队列 :  1、先进先出    2、从一端进，另一端出
// 进数据的一端：队尾
// 出数据的一端：队首
// push   :  从队尾添加一个元素 (入队)
// pop    :  从队首删除一个元素 (出队)
// front  :  访问队首元素
// back   :  访问队尾元素
// empty  :  判断栈是否为空，如果为空 1
// size   :  获取栈中元素的个数
```

#### 优先队列

```cpp
// 头文件 :  <queue>
// 优先队列 :  具有最高优先级的元素先出的特征
// push   :  从队尾添加一个元素 (入队)
// pop    :  从队首删除一个元素 (出队)
// top    :  访问队首元素
// 不能访问队尾元素
// empty  :  判断栈是否为空，如果为空 1
// size   :  获取栈中元素的个数

// 1、优先队列存放的数据类型
// 2、优先队列的底层容器
// 3、优先级规则, 不写就默认降序
//      greater<int>  升序
//      less<int>     降序
priority_queue<int, vector<int>, greater<int> >  q;
priority_queue<int, vector<int>, less<int> > p;
```

---

以下涉及迭代器

#### 迭代器方法遍历

```cpp
//附加(迭代器遍历):
    vector<int> vec_1(10,0);
    for(auto temp: vec_1){
        cout<<temp<<' ';
    }
//----------
//set专属遍历输出:
    //升序
    set<int,less<int>> se_1(10);
    //倒序
    set<int,greater<int>> se_1(10);
//----------
```

#### 动态数组

```cpp
//动态数组常用用法
//日期: 2024/4/27

//初始化:
//----------
    // 创建一个新的空的动态数组
    vector<int> vec_1;
    // 创建一个新的空的初始空间为10的动态数组 -元素默认为0
    vector<int> vec_2(10);
    // 创建一个新的空的初始空间为10的动态数组 -元素默认为3
    vector<int> vec_3(10,3);
    // 创建一个新的空的动态数组 -拷贝vec_3的内容
    vector<int> vec_4(vec_3);
    // 创建一个新的空的动态数组 -拷贝list_1的内容(前五个)
    int list[10]={1,2,3,4,5,6,7,8,9};
    vector<int> vec_5(list,list+5);
//----------

//访问内容(从0开始):
cout<<vec_5[2];

//操作内容:
//----------
    //普通:
    //在vec_1的末尾添加一个元素
    vec_1.push_back(114514);
    //在vec_1的末尾删除一个元素
    vec_1.pop_back();
    //获取vec_1动态数组的第一个元素
    vec_1.front();
    //获取vec_1动态数组的最后一个元素
    vec_1.back();
    //获取vec_1动态数组的长度
    vec_1.size();
    //判定vec_1是否为空
    vec_1.empty();
    //清空vec_1
    vec_1.clear();

    //迭代器需求:
    //获取vec_1的第一个元素的迭代器
    vec_1.begin();
    //获取vec_1的最后一个的后一位的元素的迭代器
    vec_1.end();
    //删除vec_1指定位置的元素
    vec_1.erase(vec_1.begin());
//----------
```

#### 集合

```cpp
//集合常用用法
//日期: 2024/4/27

//概念:
//----------
    //set: 有序且元素不重复的类型
    //multiset: 有重复元素的集合
//----------

//初始化:
//----------
    //初始化一个set_1集合
    set<int> se_1;
    //初始化一个se_2集合内容复制se_1
    set<int> se_2(se_1);
    //初始化一个se_3集合内容复制list_1(+10可自定义)
    int list_1[100] = {1,2,3,4,5,6,7,8,9};
    set<int> se_3(list_1,list_1+10)
//----------

//操作:
//----------
    //普通:
    //给se_1添加内容
    se_1.insert(114);
    //获取se_1的长度
    se_1.size();
    //判定se_1是否为空
    se_1.empty();
    //清空se_1
    se_1.clear();
    //查找元素在se_1中是否出现过，找到就返回回应的迭代器，否则就返回end()
    se_1.find(114);
    //删除se_1中指定的内容
    se_1.erase(10);

    //迭代器需求:
    //遍历(其他没有了)
//----------
```

#### 哈希表

```cpp
//哈希表常用用法
//日期: 2024/4/27

//概念:
//----------
    /*
    一键对一值
    键是唯一的
    值可以重复
    键不可修改
    值可以修改
    */
//----------

//初始化:
//----------
    //定义一个'键'为string类型'值'为int类型的哈希表
    map<string,int> ma_1;
//----------

//输出: 
//----------
    //mode 1
    cout<<ma_1["键"];
    //mode 2
    map<string,int>::iterator it;
    it = ma_1.find("2233");
    if(it!=end()){
        cout<<it->first<<" "<<it->second<<endl;
    }
    //遍历
    for(auto i: ma_1){
        cout<<i.first<<" "<<i.second<<endl;
    }
//----------

//操作:
//----------
    //新建一个键值对(键为"apple"值为1)
    ma_1.insert({"apple",32});
    //寻找哈希表中键为"boom"的迭代器
    ma_1.find("boom");
    //统计哈希表中"apple"出现的次数 (由于哈希表键不能重复 所以只会返回0\1)
    ma_1.count("2233");
    //删除键"2233"
    ma_1.erase("2233");
//----------
```

---

### **树**

#### 树-基本概念及定义

```language
<1> 非线性数据结构 且不存在环
<2> 一棵树至少有一节点 这一节点没有前驱节点 这个节点叫根节点
<3> 子节点、孙节点均为其父节点的后继节点
<4> 孩子节点是子节点（会分左右：左子节点、右子节点，通常用于二叉树）如下图，根节点有三个子结点，他的度为3，
 -> 整个树中度最大的节点的度就是这个树的度
<5> 兄弟节点即为同一层的节点
<6> 定义根节点的层数为1，则从上向下2、3、4、5……进行数数，为树的层数
<7> 编号：从上到下，从左到右

------

样例 (如下)
  O ->根节点
/ | \
O O O ->为根节点的子节点
|
O ->为根节点的孙节点
```

#### 二叉树-基本概念及定义和变体

```language
<1> 指的最大度数只有2的树为二叉树（binary tree简写BT）
<2> 满二叉树：每一层的节点必须是满的 每一层节点数为 2的k(层数)-1次幂 任一左子节点一定为为偶数(2k)、右子节点
 -> 为奇数2k+1
<3> n0 = n2 + 1
<4> 完全二叉树：前n-1层为满二叉树，最后一层从左往右连续
<5> 总节点数：2^n-1 (n是总层数)
<6> 二叉排序树：一个节点的左子节点的所有节点均小于此节点、它的右子节点的所有节点均大于此节点
<7> 平衡二叉树：本质为二叉排序树，添加条件根节点的左右子树深度相差最大为1

------

样例1 (如下 满二叉树)
   O
 /   \
 O   O
/\   /\
OO   OO

样例2 (如下 完全二叉树)
   O
 /   \
 O   O
/\   /
OO   O
```

#### 树的遍历

```language
<-> 共计六种
<1> 先序：根->左->右
<2> 中序：左->根->右
<3> 后序：左->右->根
<4> 层次遍历：从左至右，从上至下
<5> 深度遍历：类似于深度优先搜索
<6> 广度遍历：类似于广度优先搜索 层次遍历pro版/(^o^)/
```

---

### **图**

#### 图-基本概念及定义

```language
<1> 图由V(顶集){V1, V2, V3 ...}和E(边集){E1, E2, E3 ...} G代表这个图，由两个集合构成 G=(V, E)
<2> 注意，边集可以为空，但是点集不能为空（至少有一个点）

<无向图> 没有方向，可以互相到达
<有向图> 每一条边必须有方向，只能按照边的方向到达
<有向图-提示> 可能为两条边或双向边
<有向图-图例>
O-->O
^   |
|   v
O<->O
<无向图 to 有向图> 加一条边后加上箭头
<有向图 to 无向图> 把箭头抹了就行

<完全图> 任意两点之间均有边 (完全有向图任意两点之间均有两条边)

<子图> 在点集中选出一些作为点的子集，同理再取出边集，用它们作的图叫做子图

<度-无向图> 这个点有几条边与其链接，那么他就有几条边
<度-有向图> 分入度\出度 入度: 有多少条边的指向是指定点  出度: 有多少条边从此出发 

<路径> 指从一个点，经过一系列的边与点，抵达另一个点(经过的路径和经过的边可重复)

<回路> 指起点和终点一样的路径
<欧拉回路> 指经过所有边\点 且不重复经过的回路
<环> 不包含重复边的回路(至少三个顶点)

<连通图> 任意两点之间均有路径 (无向图)
<强连通图> 在有向图中两点之间均有路径
<弱连通图> 将原图化作无向图后，任意两点之间均有路径，原图则为弱连通图

<权> 图的边有一个数值，这个数值为权，代表经过的代价或距离

<网> 带有权的图称作网

<极大连通子图> 无法扩大的连通的子图
<连通分量> 就是极大连通子图
<极大强连通子图> 无法扩大的双向连通的子图
<强连通分量> 就是极大强连通子图
<极小连通子图> 有n个点，(n-1)个边，连通的子图
```

#### 图-存储
```language
<1> = 邻接矩阵 =
 |  使用一个二维数组作存储，行为起点，列为终点
 |  ----------------------------------------
 |  例如 1->4 2->1 1->2 3->4 (无权 \ 有向)
 |  终点 1 2 3 4
 |  起点 - - - -
 |  1  | 0 1 0 1
 |  2  | 1 0 0 0
 |  3  | 0 0 0 1
 |  4  | 0 0 0 0
 |  ----------------------------------------
 |  有多少个非0元素就有几条边 (无向图记得/2)
 |  如果加权，那么就将(bool)改成(int权值)便可
 |  ----------------------------------------
 |  优点: 代码简单易懂、查询任意两边的连通关系
 |  的复杂度为 O(1)、结构简单
 |  缺点: 空间复杂度高
 |  ----------------------------------------
<2> = 邻接表(链表) =
 |  图例 (无权有向表)
 |  大格子: 1 2 3 4 5 均为链表 
 |  1->2  1->5  2->4  4->2  4->3  4->5
 |  /---\ /---\ /---\ /---\ /---\
 |  | 1 | | 2 | | 3 | | 4 | | 5 |
 |  \---/ \---/ \---/ \---/ \---/
 |  |2|*| |4|*|       |2|*|
 |  |5|*|             |3|*|
 |                    |5|*|
 |  ----------------------------------------
 |  优点: 空间复杂度低O(v+e)、灵活性高
 |  缺点: 查询效率低,查询两点连通关系时间复杂
 |  度为O(度数)
 |  ----------------------------------------
<3> = 链式前向星 =
 |  具有空间复杂度和时间复杂度的优势(优化)
 |  ----------------------------------------
```

完全图公式1: n个顶点的完全无向图有多少条边: $n*(n-1)/2$

完全图公式2: n个顶点的完全有向图有多少条边: $n*(n-1)$

---
