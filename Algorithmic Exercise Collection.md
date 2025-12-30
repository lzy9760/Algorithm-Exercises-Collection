# 二分查找(PTA) *

[![pZ95ALn.png](https://s21.ax1x.com/2025/11/10/pZ95ALn.png)](https://imgchr.com/i/pZ95ALn)

``` C++
#include <iostream>
#include <algorithm>
using namespace std;
   
int main()
{
    int n;
    cin >> n;
    int arr1[101] = {0};
    int arr2[101] = {0};
    for(int i = 0; i<n;i++)
    {
        cin >> arr1[i];
    }
    int m;
    cin >> m;
    for(int j = 0; j<m;j++)
    {
        cin >> arr2[j];
    }
    
    sort(arr1,arr1+n);
    for(int k = 0; k<n;k++)
    {
        cout << arr1[k] << " ";
    }
    cout << endl;
    
    
    for(int j = 0; j<m;j++)
    {
    	int left = 0;
    int right = n-1;
    int flag = 0;
    int mid = 0;
    int result = 0;
    	
        while(left <= right)
    {
	 mid = (left + right) / 2;
	 flag = 0;
    if(arr1[mid] == arr2[j])
    {
        flag = 1;
	    result = mid;
        break;
    }
    else if(arr1[mid] < arr2[j])
    {
        left = mid+1;
    }
    else if(arr1[mid] > arr2[j])
    {
        right = mid-1;
    }
    }
    if(flag)
    {
    	cout << result + 1 << " ";
	}
	else
	{
		cout << "0" << " ";
	}
    }
    return 0;
}
```


# 前缀和(luogu)  **
# P1115 最大子段和

## 题目描述

给出一个长度为 $n$ 的序列 $a$，选出其中连续且非空的一段使得这段和最大。

## 输入格式

第一行是一个整数，表示序列的长度 $n$。

第二行有 $n$ 个整数，第 $i$ 个整数表示序列的第 $i$ 个数字 $a_i$。

## 输出格式

输出一行一个整数表示答案。

## 输入输出样例 #1

### 输入 #1

```
7
2 -4 3 -1 2 -4 3
```

### 输出 #1

```
4
```

## 说明/提示

#### 样例 1 解释

选取 $[3, 5]$ 子段 $\{3, -1, 2\}$，其和为 $4$。

#### 数据规模与约定

- 对于 $40\%$ 的数据，保证 $n \leq 2 \times 10^3$。
- 对于 $100\%$ 的数据，保证 $1 \leq n \leq 2 \times 10^5$，$-10^4 \leq a_i \leq 10^4$。
```C++
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

int main() {
    int n;
    cin >> n;
    vector<int> a(n);
    vector<long long> prefix(n + 1, 0);
    
    for(int i = 0; i < n; i++) {
        cin >> a[i];
    }
    
    // 正确计算前缀和：prefix[i] 表示前i个元素的和
    for(int i = 1; i <= n; i++) {
        prefix[i] = prefix[i - 1] + a[i - 1];
    }
    
    long long ret = -1e15;
    long long prevmin = prefix[0];  // 从prefix[0]开始
    
    for(int i = 1; i <= n; i++) {
        ret = max(ret, prefix[i] - prevmin);
        prevmin = min(prevmin, prefix[i]);
    }
    
    cout << ret << endl;
    return 0;
}
```
# 二分查找与插入排序(AtCoder,B Interactive Sorting,200/300 points)***
[![pZ95Zd0.png](https://s21.ax1x.com/2025/11/10/pZ95Zd0.png)](https://imgchr.com/i/pZ95Zd0)
[![pZ95eoV.png](https://s21.ax1x.com/2025/11/10/pZ95eoV.png)](https://imgchr.com/i/pZ95eoV)
```C++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    int N, Q;  // N=球的数量，Q=最多能问几次
    cin >> N >> Q;
    
    vector<char> sorted;  // 存放已经排好序的球
    
    sorted.push_back('A');  // 先把第一个球A放进去
    
    // 从第二个球开始处理（B、C、D...）
    for (int i = 1; i < N; i++) {
        char current = 'A' + i;  // 当前要插入的球
        
        // 用二分法找插入位置
        int left = 0, right = sorted.size();
        
        while (left < right) {
            int mid = (left + right) / 2;  // 取中间位置
            
            // 问问题：中间位置的球 vs 当前球，谁重？
            cout << "? " << sorted[mid] << " " << current << endl;
            cout.flush();
            
            char result;
            cin >> result;
            
            if (result == '<') {
                left = mid + 1;  // 当前球更重，往右找
            } else {
                right = mid;     // 当前球更轻，往左找
            }
        }
        
        // 找到位置了，把当前球插进去
        sorted.insert(sorted.begin() + left, current);
    }
    
    // 输出最终答案
    cout << "! ";
    for (char c : sorted) {
        cout << c;
    }
    cout << endl;
    
    return 0;
}
```

# 数组(传智杯校赛C题)**
[![pZ953LR.png](https://s21.ax1x.com/2025/11/10/pZ953LR.png)](https://imgchr.com/i/pZ953LR)
```C++
#include <bits/stdc++.h>
using namespace std;

void solve()
{
    int n = 0; 
    cin >> n;
    long long sum = 0;
    int num = 0;
    int ok = 0;
    
    for(int j = 0; j < n; j++)
    {
        int x;
        cin >> x;
        sum += abs(x);
        
        // 处理负数段
        if(x < 0 && ok == 0)
        {
            num++;
            ok = 1;
        }
        // 只有当遇到正数（不是0）时才重置状态
        else if(x > 0)
        {
            ok = 0;
        }
        // 对于0，我们保持当前状态不变
    }
    
    cout << sum << endl << num << endl;
}

int main()
{
    int T;
    cin >> T;
    
    for(int i = 0; i < T; i++)
    {
        solve();
    }
    
    return 0;
}
```
# 贪心+数学分析  ***
* #### 1.分配问题(PTA)
[![pZ95niT.png](https://s21.ax1x.com/2025/11/10/pZ95niT.png)](https://imgchr.com/i/pZ95niT)
```C++
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main() {
    long long M;
    int N;
    cin >> M >> N;
    
    vector<long long> demands(N);
    long long total_demand = 0;
    
    for (int i = 0; i < N; i++) {
        cin >> demands[i];
        total_demand += demands[i];
    }
    
    long long T = total_demand - M;
    if (T == 0) {
        cout << 0 << endl;
        return 0;
    }
    
    sort(demands.begin(), demands.end());//通过排序和优先处理小期望值孩子，确保小期望值孩子被完全剥夺（他们的平方贡献小），而大期望值孩子只被剥夺平均部分，从而平衡各孩子的剥夺量。

    
    long long anger = 0;
    long long remaining = T;
    
    for (int i = 0; i < N; i++) {
        // 计算当前孩子应该被剥夺的糖果数
        // 平均分配剩余剥夺量给剩下的孩子
        long long fair = remaining / (N - i);//平方函数，平均分配才可能有最小值
        
        // 当前孩子最多能被剥夺的糖果数
        long long take = min(demands[i], fair);
        
        anger += take * take;
        remaining -= take;
    }
    
    cout << anger << endl;
    return 0;
}
```
* #### 2.区间问题(bilibili) 
[![pZ95uJU.png](https://s21.ax1x.com/2025/11/10/pZ95uJU.png)](https://imgchr.com/i/pZ95uJU)
```C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    vector<vector<int>> intervals;
    int n;
    
    // 获取区间数量
    cout << "请输入区间数量: ";
    cin >> n;
    
    // 获取每个区间的起点和终点
    cout << "请输入" << n << "个区间（格式：起点 终点）:" << endl;
    for (int i = 0; i < n; i++) {
        int start, end;
        cin >> start >> end;
        intervals.push_back({start, end});
    }
    
    // 如果区间为空，直接返回0
    if (intervals.empty()) {
        cout << "需要移除的区间数量: 0" << endl;
        return 0;
    }
    
    // 按照结束时间排序
    sort(intervals.begin(), intervals.end(), 
         [](const vector<int>& a, const vector<int>& b) {
             return a[1] < b[1];
         });//lambda表达式
    
    int removeCount = 0; // 要移除的区间个数
    int currentEnd = intervals[0][1]; // 当前保留的最后一个区间的结束时间
    
    // 从第二个区间开始检查
    for (int i = 1; i < intervals.size(); i++) {
        int start = intervals[i][0]; // 当前区间的开始时间
        int end = intervals[i][1];   // 当前区间的结束时间
        
        if (start < currentEnd) {
            // 有重叠，优先移除当前区间(结束时间较大)
            removeCount++;
        } else {
            // 没有重叠，保留当前区间，更新结束时间
            currentEnd = end;
        }
    }
    
    cout << "需要移除的区间数量: " << removeCount << endl;
    
    return 0;
}
```

# DFS(luogu, B3622 枚举子集(递归实现指数型枚举))**

#### 题目描述

今有 $n$ 位同学，可以从中选出任意名同学参加合唱。

请输出所有可能的选择方案。

#### 输入格式

仅一行，一个正整数 $n$。

#### 输出格式

若干行，每行表示一个选择方案。

每一种选择方案用一个字符串表示，其中第 $i$ 位为 `Y` 则表示第 $i$ 名同学参加合唱；为 `N` 则表示不参加。

需要以字典序输出答案。

#### 输入输出样例 #1

#### 输入 #1

```
3
```

#### 输出 #1

```
NNN
NNY
NYN
NYY
YNN
YNY
YYN
YYY
```

#### 说明/提示

对于 $100\%$ 的数据，保证 $1\leq n\leq 10$。
```C++
#include <bits/stdc++.h>
using namespace std;
string path;//全局变量，记录每一步决策
int n;
void dfs(int x)
{
    if(x > n)
    {
        cout << path << endl;
        return;
    }
    path += 'N';
    dfs(x+1);
    path.pop_back();//回溯，回到起点,清空现场

    path += 'Y';
    dfs(x+1);
    path.pop_back();
}

int main()
{
    cin >> n;
    
    dfs(1);
    return 0;
}
```
# DFS(luogu,P1157 组合的输出) **

#### 题目描述

排列与组合是常用的数学方法，其中组合就是从 $n$ 个元素中抽出 $r$ 个元素（不分顺序且 $r \le n$），我们可以简单地将 $n$ 个元素理解为自然数 $1,2,\dots,n$，从中任取 $r$ 个数。

现要求你输出所有组合。

例如 $n=5,r=3$，所有组合为：

$123,124,125,134,135,145,234,235,245,345$。

#### 输入格式

一行两个自然数 $n,r(1<n<21,0 \le r \le n)$。

#### 输出格式

所有的组合，每一个组合占一行且其中的元素按由小到大的顺序排列，每个元素占三个字符的位置，所有的组合也按字典顺序。

**注意哦！输出时，每个数字需要 $3$ 个场宽。以 C++ 为例，你可以使用下列代码：**

```cpp
cout << setw(3) << x;
```

输出占 $3$ 个场宽的数 $x$。注意你需要头文件 `iomanip`。

#### 输入输出样例 #1

##### 输入 #1

```
5 3
```

### 输出 #1

```
1  2  3
  1  2  4
  1  2  5
  1  3  4
  1  3  5
  1  4  5
  2  3  4
  2  3  5
  2  4  5
  3  4  5
```
```C++
#include <bits/stdc++.h>
using namespace std;
int n,r;
vector<int>path;
void dfs(int begin)
{
if(path.size() == r)
{
    for(auto x : path) cout << setw(3) << x;
    cout << endl;
    return;

}
    
     for(int i = begin;i<=n;i++)
     {
         path.push_back(i);
         dfs(i+1);
         path.pop_back();
     }
    
}

int main()
{
    cin >> n >> r;
    dfs(1);
    
    return 0;
}
```

# DFS( P1025 [NOIP 2001 提高组] 数的划分) ***

#### 题目描述

将整数 $n$ 分成 $k$ 份，且每份不能为空，任意两个方案不相同（不考虑顺序）。

例如：$n=7$，$k=3$，下面三种分法被认为是相同的。

$1,1,5$;   
$1,5,1$;   
$5,1,1$.

问有多少种不同的分法。

#### 输入格式

$n,k$ （$6<n \le 200$，$2  \le k  \le  6$）。

#### 输出格式

$1$ 个整数，即不同的分法。

#### 输入输出样例 #1

#### 输入 #1

```
7 3
```

#### 输出 #1

```
4
```

#### 说明/提示

四种分法为：  
$1,1,5$;  
$1,2,4$;  
$1,3,3$;  
$2,2,3$.

**【题目来源】**

NOIP 2001 提高组第二题
```C++
#include <iostream>
using namespace std;
int n,k;
int path = 0;
int ret = 0;
void dfs(int pos,int begin)
{
    if(pos == k)
    {
        if(path==n)
        {
            ret++;
        }
        return;
    }
    //if(path + i*(k-pos) > n) return;//可行性剪枝，但位置不对，仍然有测试点超时
    for(int i = begin; i<=n;i++)
    {
        if(path + i*(k-pos) > n) return;//关键：可行性剪枝，在dfs开始之前
        
        path += i;
        dfs(pos+1,i);
        path -= i;//回溯
    }
}

int main()
{
    cin >> n >> k;
    dfs(0,1);
    cout << ret;
    return 0;
}
```
# DFS(记忆化搜索,LeetCode 509) **
[![pZPSzLt.md.png](https://s21.ax1x.com/2025/11/14/pZPSzLt.md.png)](https://imgchr.com/i/pZPSzLt)
```C++
class Solution {
    int f[35];

public:
    int dfs(int n)
    {
        if(f[n] != -1)
        {
            return f[n];
        }
        if(n==1 || n==0)
        {
            return n;
        }
        else
        {
            f[n] = dfs(n-1)+dfs(n-2);
            return f[n];
        }
    }



    int fib(int n) {
        memset(f,-1,sizeof(f));
        return dfs(n);
    }
};
```




# 奇偶约束排序(Codeforces Round 1062 Div4 C题) **
[![pZCBJrF.png](https://s21.ax1x.com/2025/11/12/pZCBJrF.png)](https://imgchr.com/i/pZCBJrF)
[![pZCBGKU.png](https://s21.ax1x.com/2025/11/12/pZCBGKU.png)](https://imgchr.com/i/pZCBGKU)
```C++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int t;
    cin >> t;
    
    while (t--) {
        int n;
        cin >> n;
        vector<int> a(n);
        
        bool has_odd = false, has_even = false;
        
        for (int i = 0; i < n; i++) {
            cin >> a[i];
            if (a[i] % 2 == 1) has_odd = true;
            else has_even = true;
        }
        
        // 如果同时存在奇数和偶数，可以完全排序
        if (has_odd && has_even) {
            sort(a.begin(), a.end());
        }
        // 否则（全奇数或全偶数），保持原顺序
        
        for (int i = 0; i < n; i++) {
            cout << a[i] << " \n"[i == n - 1];
        }
    }
    
    return 0;
}
```

# 双指针+约束排序+贪心归并(Deepseek) ***
[![pZCBB26.md.png](https://s21.ax1x.com/2025/11/12/pZCBB26.md.png)](https://imgchr.com/i/pZCBB26)
```C++
#include <iostream>
#include <vector>
using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int T;
    cin >> T;
    
    while (T--) {
        int n;
        cin >> n;
        
        vector<int> arr(n);
        vector<int> type(n);
        
        for (int i = 0; i < n; i++) {
            cin >> arr[i];
        }
        
        for (int i = 0; i < n; i++) {
            cin >> type[i];
        }
        
        // 分离两种类型的元素，保持相对顺序
        vector<int> type1, type2;
        for (int i = 0; i < n; i++) {
            if (type[i] == 1) {
                type1.push_back(arr[i]);
            } else {
                type2.push_back(arr[i]);
            }
        }
        
        // 双指针合并
        vector<int> result;
        int i = 0, j = 0;
        int size1 = type1.size();
        int size2 = type2.size();
        
        while (i < size1 && j < size2) {
            if (type1[i] < type2[j]) {
                result.push_back(type1[i]);
                i++;
            } else {
                result.push_back(type2[j]);
                j++;
            }
        }
        
        // 处理剩余元素
        while (i < size1) {
            result.push_back(type1[i]);
            i++;
        }
        while (j < size2) {
            result.push_back(type2[j]);
            j++;
        }
        
        // 输出结果
        for (int k = 0; k < n; k++) {
            cout << result[k] << " \n"[k == n - 1];
        }
    }
    
    return 0;
}
```

# 埃氏筛法
#### 1.2023蓝桥杯省赛真题 **
[![pZCORGn.md.png](https://s21.ax1x.com/2025/11/13/pZCORGn.md.png)](https://imgchr.com/i/pZCORGn)
```C++
#include <iostream>
#include <vector>
#include <cmath>
using namespace std;

const int MAX_N = 1000000;
vector<int> min_prime(MAX_N + 1, 0);

// 埃氏筛法变种：记录最小质因数
void build_sieve() {
    for (int i = 2; i <= MAX_N; i++) {
        if (min_prime[i] == 0) {  // i是质数
            min_prime[i] = i;
            for (int j = i * 2; j <= MAX_N; j += i) {
                if (min_prime[j] == 0) {
                    min_prime[j] = i;
                }
            }
        }
    }
}

// 计算不同质因数的个数
int count_distinct_prime_factors(int n) {
    if (n == 1) return 0;  // 1没有质因数
    
    int count = 0;
    int last_prime = 0;
    
    while (n > 1) {
        int p = min_prime[n];
        if (p != last_prime) {
            count++;
            last_prime = p;
        }
        n /= p;
    }
    return count;
}
```
#### 2.学校作业 **
[![pZCOfx0.md.png](https://s21.ax1x.com/2025/11/13/pZCOfx0.md.png)](https://imgchr.com/i/pZCOfx0)
```C++
#include <stdio.h>
#include <stdbool.h>

#define MAX_N 50

// 使用埃拉托斯特尼筛法生成素数表
void sieve_of_eratosthenes(bool is_prime[], int n) {
    for (int i = 0; i <= n; i++) {
        is_prime[i] = true;
    }
    is_prime[0] = is_prime[1] = false;
    for (int i = 2; i * i <= n; i++) {
        if (is_prime[i]) {
            for (int j = i * i; j <= n; j += i) {
                is_prime[j] = false;
            }
        }
    }
}

void guest(int n, bool is_prime[]) {
    for (int i = 2; i <= n / 2; i++) {
        if (is_prime[i] && is_prime[n - i]) {
            printf("%d=%d+%d ", n, i, n - i);
        }
    }
    printf("\n");
}

int main() {
    bool is_prime[MAX_N + 1];
    sieve_of_eratosthenes(is_prime, MAX_N);

    for (int n = 6; n <= MAX_N; n += 2) {
        guest(n, is_prime);
    }

    return 0;
}
```
# BFS(luogu) **
[![pZPFjSS.md.png](https://s21.ax1x.com/2025/11/14/pZPFjSS.md.png)](https://imgchr.com/i/pZPFjSS)
```C++
#include <iostream>
#include <queue>
#include <cstring>
using namespace std;

const int N = 410;  // 定义棋盘最大尺寸

// 定义坐标对类型
typedef pair<int, int> PII;

int n, m, x, y;
int dist[N][N];  // 存储每个位置的最短步数

// 骑士的8个移动方向（国际象棋中马的走法）
int dx[] = {1, 2, 2, 1, -1, -2, -2, -1};
int dy[] = {2, 1, -1, -2, -2, -1, 1, 2};

void bfs()
{
    // 初始化所有位置为-1（表示未访问）
    memset(dist, -1, sizeof dist);
    
    // 创建队列存储待处理的坐标
    queue<PII> q;
    
    // 起点入队并标记步数为0
    q.push({x, y});
    dist[x][y] = 0;
    
    // BFS主循环
    while (!q.empty())
    {
        // 取出队首元素
        auto t = q.front();
        q.pop();
        
        int current_x = t.first, current_y = t.second;
        
        // 尝试8个移动方向
        for (int k = 0; k < 8; k++)
        {
            // 计算新位置坐标
            int new_x = current_x + dx[k];
            int new_y = current_y + dy[k];
            
            // 检查边界：是否在棋盘范围内
            if (new_x < 1 || new_x > n || new_y < 1 || new_y > m) 
                continue;
            
            // 检查是否已经访问过该位置
            if (dist[new_x][new_y] != -1) 
                continue;
            
            // 更新步数并加入队列
            dist[new_x][new_y] = dist[current_x][current_y] + 1;
            q.push({new_x, new_y});
        }
    }
}

int main()
{
    // 输入棋盘大小和起始位置
    cin >> n >> m >> x >> y;
    
    // 执行BFS计算最短路径
    bfs();
    
    // 输出结果
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= m; j++)
        {
            cout << dist[i][j] << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```
# 前缀和+贪心+边界判断(传智杯校赛D题) **
[![pZPdxc8.md.png](https://s21.ax1x.com/2025/11/15/pZPdxc8.md.png)](https://imgchr.com/i/pZPdxc8)
```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

int main() {
    int T;
    cin >> T;
    
    vector<ll> results;
    
    for (int t = 0; t < T; t++) {
        int n, k;
        cin >> n >> k;
        vector<ll> a(n + 1), b(n + 1);
        vector<ll> prefix(n + 1, 0);
        
        for (int i = 1; i <= n; i++) {
            cin >> a[i];
        }
        for (int i = 1; i <= n; i++) {
            cin >> b[i];
        }
        
        for (int i = 1; i <= n; i++) {
            prefix[i] = prefix[i - 1] + b[i];
        }
        
        ll result = 0;
        for (int i = 1; i <= n; i++) {
            ll diff = prefix[i] - k;
            ll required = 0;
            if (diff > 0) {
                // 当diff是a[i]的倍数时，需加1保证严格大于
                if (diff % a[i] == 0) {
                    required = diff / a[i] + 1;
                } else {
                    // 普通向上取整
                    required = (diff + a[i] - 1) / a[i];
                }
            } else if (diff == 0) {
                // 此时需要x≥1才能满足a[i]x > 0
                required = 1;
            } else {
                // diff < 0时，x≥0即可
                required = 0;
            }
            result = max(result, required);
        }
        
        results.push_back(result);
    }
    
    for (ll res : results) {
        cout << res << endl;
    }
    
    return 0;
}
```
# 欧拉筛(传智杯校赛E题) ***
* 核心：每个合数只被它最小的质因数筛掉(标记)

[![pZPwwEd.md.png](https://s21.ax1x.com/2025/11/15/pZPwwEd.md.png)](https://imgchr.com/i/pZPwwEd)
```C++
#include <iostream>
#include <vector>
using namespace std;

const int MAXN = 100005;

int min_prime[MAXN];
vector<int> primes;
bool mark[MAXN];     // 标记需要排除的质因子（a中所有数的质因子），“坏质数”
bool in_a[MAXN];     // 标记1~k中是否在数组a中，“坏数字”

// 欧拉筛法预处理最小质因子（保持简洁）
void init(int n) {
    for (int i = 2; i <= n; i++) {
        if (min_prime[i] == 0) {
            min_prime[i] = i;
            primes.push_back(i);
        }
        for (int p : primes) {
            if (p > min_prime[i] || i * p > n) break;
            min_prime[i * p] = p;
        }
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, k;
    cin >> n >> k;
    init(k);

    // 读取a数组，同时标记in_a和a中所有数的质因子（合并循环）
    for (int i = 0; i < n; i++) {
        int x;
        cin >> x;
        // 1. 标记x是否在1~k范围内（在则标记in_a）
        if (x <= k) in_a[x] = true;
        // 2. 分解x的质因子，标记需要排除的质因子（仅处理<=k的质因子，超过k无意义）
        int tmp = x;
        while (tmp > 1) {
            int p = min_prime[tmp];
            if (p <= k) mark[p] = true;  // 只标记<=k的质因子（否则1~k中无该质因子的倍数）
            while (tmp % p == 0) tmp /= p;
        }
    }

    // 统计符合条件的数：不在a中 + 不包含任何标记的质因子
    int count = 0;
    for (int i = 1; i <= k; i++) {
        if (in_a[i]) continue;  // 跳过a中已有的数
        
        // 判断i是否与所有a的质因子互质（即不被任何mark[p]整除）
        bool is_valid = true;
        for (int p : primes) {
            if (p > i) break;  // 优化：p超过i时，i不可能被p整除，提前退出
            if (mark[p] && i % p == 0) {
                is_valid = false;
                break;
            }
        }
        if (is_valid) count++;
    }

    cout << count << endl;
    return 0;
}
```

# 单调栈(luogu) ***
[![pZF6sFU.md.png](https://s21.ax1x.com/2025/11/21/pZF6sFU.md.png)](https://imgchr.com/i/pZF6sFU)
```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 3e5+10;
long long a[N];

long long solve(bool isMax) {
    stack<int> st;
    long long sum = 0;
    
    for(int i = 1; i <= n + 1; i++) {
        while(!st.empty() && (i == n + 1 || 
              (isMax ? a[st.top()] <= a[i] : a[st.top()] >= a[i]))) {
            int idx = st.top(); st.pop();//注意栈里的下标不是按照顺序排序的，而是按照下标对应的值来排序，所以idx-left并不始终等于1
            int left = st.empty() ? 0 : st.top();
            sum += a[idx] * (idx - left) * (i - idx);
        }
        st.push(i);
    }
    return sum;
}

int main() {
    int n;
    cin >> n;
    for(int i = 1; i <= n; i++) cin >> a[i];
    
    long long sum_max = solve(true);   // 所有子数组最大值和
    long long sum_min = solve(false);  // 所有子数组最小值和
    
    cout << sum_max - sum_min << endl;
    return 0;
}
```

# 单调队列(luogu) **
# P1886 滑动窗口 /【模板】单调队列

## 题目描述

有一个长为 $n$ 的序列 $a$，以及一个大小为 $k$ 的窗口。现在这个窗口从左边开始向右滑动，每次滑动一个单位，求出每次滑动后窗口中的最小值和最大值。

例如，对于序列 $[1,3,-1,-3,5,3,6,7]$ 以及 $k = 3$，有如下过程：

$$\def\arraystretch{1.2}
\begin{array}{|c|c|c|}\hline
\textsf{窗口位置} & \textsf{最小值} & \textsf{最大值} \\ \hline
\verb![1   3  -1] -3   5   3   6   7 ! & -1 & 3 \\ \hline
\verb! 1  [3  -1  -3]  5   3   6   7 ! & -3 & 3 \\ \hline
\verb! 1   3 [-1  -3   5]  3   6   7 ! & -3 & 5 \\ \hline
\verb! 1   3  -1 [-3   5   3]  6   7 ! & -3 & 5 \\ \hline
\verb! 1   3  -1  -3  [5   3   6]  7 ! & 3 & 6 \\ \hline
\verb! 1   3  -1  -3   5  [3   6   7]! & 3 & 7 \\ \hline
\end{array}
$$

## 输入格式

输入一共有两行，第一行有两个正整数 $n,k$；\
第二行有 $n$ 个整数，表示序列 $a$。

## 输出格式

输出共两行，第一行为每次窗口滑动的最小值；   
第二行为每次窗口滑动的最大值。

## 输入输出样例 #1

### 输入 #1

```
8 3
1 3 -1 -3 5 3 6 7
```

### 输出 #1

```
-1 -3 -3 -3 3 3
3 3 5 5 6 7
```

## 说明/提示

【数据范围】    
对于 $50\%$ 的数据，$1 \le n \le 10^5$；  
对于 $100\%$ 的数据，$1\le k \le n \le 10^6$，$a_i \in [-2^{31},2^{31})$。

```C++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e6+10;
int a[N];
int main()
{
    int n,k;
    cin >> n >> k;
    for(int i = 1; i<=n;i++) cin >> a[i];

    deque<int>q;
    //求最小值，构造单调递增的队列
    for(int i = 1;i<=n;i++)
    {
        while(q.size() && a[q.back()] >= a[i]) q.pop_back();
        q.push_back(i);
        
        if(q.back() - q.front() + 1 > k) q.pop_front();
        if(i>=k) cout << a[q.front()] << " ";
    }
        q.clear();
        cout << endl;
    ///求最大值，构造单调递减的队列
    for(int j = 1;j<=n;j++)
    {
        while(q.size() && a[q.back()] <= a[j]) q.pop_back();
        q.push_back(j);
        
        if(q.back() - q.front() + 1 > k) q.pop_front();
        if(j>=k) cout << a[q.front()] << " ";
    }
    
    return 0;
}
```

# 单调栈(luogu) **
# P5788 【模板】单调栈

## 题目背景

模板题，无背景。  

2019.12.12 更新数据，放宽时限，现在不再卡常了。

## 题目描述

给出项数为 $n$ 的整数数列 $a_{1 \dots n}$。

定义函数 $f(i)$ 代表数列中第 $i$ 个元素之后第一个大于 $a_i$ 的元素的**下标**，即 $f(i)=\min_{i<j\leq n, a_j > a_i} \{j\}$。若不存在，则 $f(i)=0$。

试求出 $f(1\dots n)$。

## 输入格式

第一行一个正整数 $n$。

第二行 $n$ 个正整数 $a_{1\dots n}$。

## 输出格式

一行 $n$ 个整数表示 $f(1), f(2), \dots, f(n)$ 的值。

## 输入输出样例 #1

### 输入 #1

```
5
1 4 2 3 5
```

### 输出 #1

```
2 5 4 5 0
```

## 说明/提示

【数据规模与约定】

对于 $30\%$ 的数据，$n\leq 100$；

对于 $60\%$ 的数据，$n\leq 5 \times 10^3$ ；

对于 $100\%$ 的数据，$1 \le n\leq 3\times 10^6$，$1\leq a_i\leq 10^9$。

```C++
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int n; 
    cin >> n;
    vector<long long>a(n+1);
    vector<long long>ret(n+1);
    for(int i =1 ; i<=n;i++) cin >> a[i];

    stack<int>st;
    
    for(int j = n;j>=1;j--)
    {
        while(st.size() && a[st.top()] <= a[j]) st.pop();

        if(st.size()) ret[j] = st.top();
        
        st.push(j);
        
    }

    for(int k = 1;k<=n;k++) cout << ret[k] << " ";
    
    return 0;
}
```

# 快速幂+二进制(luogu) **
# P1226 【模板】快速幂

## 题目描述

给你三个整数 $a,b,p$，求 $a^b \bmod p$。

## 输入格式

输入只有一行三个整数，分别代表 $a,b,p$。

## 输出格式

输出一行一个字符串 `a^b mod p=s`，其中 $a,b,p$ 分别为题目给定的值， $s$ 为运算结果。

## 输入输出样例 #1

### 输入 #1

```
2 10 9
```

### 输出 #1

```
2^10 mod 9=7
```

## 说明/提示

**样例解释**

$2^{10} = 1024$，$1024 \bmod 9 = 7$。

**数据规模与约定**

对于 $100\%$ 的数据，保证 $0\le a,b < 2^{31}$，$a+b>0$，$2 \leq p \lt 2^{31}$。

```C++
#include <iostream>
#include <cstdio>
using namespace std;
typedef long long ll;
ll a, b, p;
ll qpow(ll a,ll b, ll p)
{
    ll ret = 1;
    while(b) 
    {
    if(b & 1) ret  = ret * a % p;//与操作，如果末尾为1，乘上对应的权值
    a=a*a % p;//二进制位对应的权值
    b >>= 1;//右移一位，大小减半
    }
    return ret;
}


int main()
{
    cin >> a >> b >> p;
    printf("%lld^%lld mod %lld=%lld",a,b,p,qpow(a,b,p));
    return 0;
}
```
# 线性dp(luogu) **
# B3637 最长上升子序列

## 题目描述

这是一个简单的动规板子题。

给出一个由 $n(n\le 5000)$ 个不超过 $10^6$ 的正整数组成的序列。请输出这个序列的**最长上升子序列**的长度。

最长上升子序列是指，从原序列中**按顺序**取出一些数字排在一起，这些数字是**逐渐增大**的。

## 输入格式

第一行，一个整数 $n$，表示序列长度。

第二行有 $n$ 个整数，表示这个序列。

## 输出格式

一个整数表示答案。

## 输入输出样例 #1

### 输入 #1

```
6
1 2 4 1 3 4
```

### 输出 #1

```
4
```

## 说明/提示

分别取出 $1$、$2$、$3$、$4$ 即可。
```C++
#include<bits/stdc++.h>
using namespace std;
const int N = 5010;
int a[N];
int dp[N];    
int main()
{
    int n;
    cin >> n;
    for(int i = 1;i<=n;i++) cin >> a[i];
    int ret = 0;
    for(int i = 1;i<=n;i++)
    {
        dp[i] = 1;
        for(int j = 1;j<i;j++)
        {
            if(a[i] > a[j])
            {
                dp[i] = max(dp[i],dp[j] + 1);
            }
        }
        ret = max(ret,dp[i]);
    }
    cout << ret << endl;
    return 0;
}
```

# 字符串哈希(luogu) **
# P3370 【模板】字符串哈希

## 题目描述

如题，给定 $N$ 个字符串（第 $i$ 个字符串长度为 $M_i$，字符串内包含数字、大小写字母，大小写敏感），请求出 $N$ 个字符串中共有多少个不同的字符串。


**友情提醒：如果真的想好好练习哈希的话，请自觉。**

## 输入格式

第一行包含一个整数 $N$，为字符串的个数。

接下来 $N$ 行每行包含一个字符串，为所提供的字符串。

## 输出格式

输出包含一行，包含一个整数，为不同的字符串个数。

## 输入输出样例 #1

### 输入 #1

```
5
abc
aaaa
abc
abcc
12345
```

### 输出 #1

```
4
```

## 说明/提示

### 数据范围

对于 $30\%$ 的数据：$N\leq 10$，$M_i≈6$，$M_{\max}\leq 15$。

对于 $70\%$ 的数据：$N\leq 1000$，$M_i≈100$，$M_{\max}\leq 150$。

对于 $100\%$ 的数据：$N\leq 10000$，$M_i≈1000$，$M_{\max}\leq 1500$。

### 样例说明

样例中第一个字符串 $\tt{abc}$ 和第三个字符串 $\tt{abc}$ 是一样的，所以所提供字符串的集合为 $\{\tt{aaaa},\tt{abc},\tt{abcc},\tt{12345}\}$，故共计 $4$ 个不同的字符串。

### 拓展阅读

以下的一些试题从不同层面体现出了字符串哈希算法的正确性分析。

- [P12197 Hash Killer I](https://www.luogu.com.cn/problem/P12197)
- [P12198 Hash Killer II](https://www.luogu.com.cn/problem/P12198)
- [P12199 （目前无解）Hash Killer III](https://www.luogu.com.cn/problem/P12199)
- [P12200 Hash Killer Extra](https://www.luogu.com.cn/problem/P12200)
- [P12201 Hash Killer Phantasm](https://www.luogu.com.cn/problem/P12201)
- [P7350 「MCOI-04」Dream and Strings](https://www.luogu.com.cn/problem/P7350)

```C++
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ULL;
const int N = 1e4+10, P = 131; // 131/13331 是常用的哈希进制
int n;
ULL a[N];

// 修正哈希计算：遍历字符串的合法下标
ULL get_hash(string &s)
{
    ULL ret = 0;
    // 方式1：按合法下标遍历
    // for(int i = 0; i < s.size(); i++)
    // {
    //     ret = ret * P + s[i];
    // }
    // 方式2：更简洁的范围遍历（推荐）
    for(char c : s)
    {
        ret = ret * P + c;
    }
    return ret;
}

int main()
{
    cin >> n;
    string s;
    for(int i = 1; i <= n; i++)
    {
        cin >> s;
        a[i] = get_hash(s);
    }

    int ret = 1;
    sort(a+1, a+1+n); // 排序后相同哈希值会相邻
    for(int i = 2; i <= n; i++)
    {
        if(a[i] != a[i-1])
        {
            ret++;
        }
    }
    cout << ret << endl;
    return 0;
}
```