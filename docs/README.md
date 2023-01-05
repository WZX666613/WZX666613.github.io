<!-- tabs:start -->

#### **English**

Hello!

#### **French**

Bonjour!

#### **Italian**

Ciao!

<!-- tabs:end -->


# 函数

## map

1. 定义：`map <下标类型 , 数据类型> 变量名;`
2. map类似于桶 ， 但可以统计字符串和负数
3. map时间复杂度高于桶，map存取时间复杂度为`O(log n)`，桶为`O(1)`
4. map会自动初始化，但`char`类型变量不会被初始化为`''`而是ASCII编码为0的字符

```c_cpp
map <string , int> mp;//定义
mp["xxx"] = 0;//将下标xxx设为1
mp["xxx"] ++;//将下标xx增加1
```

## 优先队列

1. 可以直接获取最大的元素
2. 定义：`priority_queue <数据类型> 变量名`

!>和结构体搭配使用时需[重载运算符](/?id=函数#/?id=重载运算符)

```c_cpp
priority_queue <int> pq;//定义
pq.push(1);//往队列里放一个1
pq.top();//得到最大的元素
pq.pop();//删除最大的元素
pq.size();//元素个数
pq.empty();//是不是空的，如果是返回true，不是返回false
```

## 结构体

过于简单，这里不讲

### 重载运算符

可以自定义运算符的作用，这里只讲作为结构体成员函数用法

```c_cpp
//放在struct函数内
bool operator < (node b) const//b为参数，bool为需重载运算符的类型 ， <为需重载的运算符
{
  if (id < b.id) return true;//bool类型必须返回true或false
  else return false;
}//重载运算符"<"
```

# 算法

## dfs深搜

示例：洛谷P1706全排列问题

```c_cpp
#include <bits/stdc++.h>
using namespace std;
int vis[15] , n;//vis:标记每个数是否已经被放了
int ans[15];//格子数组

void dfs(int x)//往第x个格子上放数，调用函数放下一个格子
{
    if (x > n)//到了第n+1个格子
    {
        for (int i = 1 ; i <= n ; i++)
        {
            cout << setw(5) << ans[i];
        }
        cout << "\n";
        return;
    }
    for (int i = 1 ; i <= n ; i++)
    {
        if (vis[i] == 0)//i没被放进去
        {
            ans[x] = i;//把i放进第x个格子
            vis[i] = 1;//标记i已经被放过了
            dfs(x+1);//放下一个格子
            ans[x] = 0;//还回去
            vis[i] = 0;//i表只因为没放过
        }
    }
}

int main()
{
    cin >> n;
    dfs(1);
    
    return 0;
 }
```

## 二维dfs

以一本通1215迷宫为例：

```c_cpp
#include<bits/stdc++.h> 
using namespace std;

int dx[5] = {0 , 1 , -1 , 0 , 0};
int dy[5] = {0 , 0 , 0 , 1 , -1};
bool vis[105][105] = {0};
char a[105][105];
int n , ex , ey , sx , sy;

//走到x,y
void dfs(int x , int y)
{
    for (int i = 0 ; i <= 4 ; i++)
    {
        int nx = x + dx[i];
        int ny = y + dy[i];
        //往(nx,ny)走
        if (nx >= 1 && nx <= n && ny >= 1 && ny <= n && a[nx][ny] == '.' && vis[nx][ny] == 0 && vis[ex][ey] == 0)
        {
            vis[nx][ny] = true;
            dfs(nx , ny);
        }
    }
}

int main()
{
    int t;
    cin >> t;
    while(t--)
    {
        memset (vis , 0 , sizeof(vis));//清零
        cin >> n;
        for (int i = 1 ; i <= n ; i++)
        {
            for (int j = 1 ; j <= n ; j++)
            {
                cin >> a[i][j];
            }
        }
        cin >> sx >> sy >> ex >> ey;
        sx+=1;
        ex+=1;
        sy+=1;
        ey+=1;
        dfs(sx , sy);
        if (vis[ex][ey] == 1) cout << "YES\n";
        else cout << "NO\n";
    }
    
    return 0;
}
```

### 连通块问题

连通块定义：能够互相走到的点为连通块

1. 走的点不能超过范围
2. 不能是“地雷”
3. 一般来说，走过的点不再走
4. 如果有终点，走到终点就不走
5. 起点要特殊考虑

以一本通1249：Lake Counting为例

```c_cpp
#include<bits/stdc++.h> 
using namespace std;

int dx[9] = {0 , -1 , -1 , -1 , 0 , 0 , 1 , 1 , 1};
int dy[9] = {0 , -1 , 0 , 1 , -1 , 1 , -1 , 0 , 1};
int vis[115][115] = {0};
int cnt;
char a[115][115];
int n , sx , sy , m;

void dfs(int x,int y)
{ 
    for(int i=1;i<=8;i++)
    { 
        int nx=x+dx[i];
        int ny=y+dy[i];
        if(nx>=1 &&nx<=m &&ny>=1 &&ny<=n &&a[nx][ny]!='.'&&vis[nx][ny]==0)
        { 
            vis[nx][ny]=cnt;
            dfs(nx,ny);
        }
    
    } 
} 

int main()
{
    cin >> m >> n;
    for (int i = 1 ; i <= m ; i++)
    {
        for (int j = 1 ; j <= n ; j++)
        {
            cin >> a[i][j];    
        }    
    }
    for (int i = 1 ; i <= m ; i++)
    {
        for(int  j = 1 ; j <= n ; j++)
        {
            if (a[i][j] != '.' && vis[i][j] == 0)
            {
                cnt++;
                vis[i][j] = cnt;
                dfs(i,j);
            }
        }    
    }
    cout << cnt; 
    return 0;
}
```

# 题解

!>以下题解仅供学习参考使用
抄袭、复制题解，以达到刷 AC 率/AC 数量或其他目的的行为，在洛谷是严格禁止的。洛谷非常重视学术诚信。此类行为将会导致您成为作弊者。 具体细则请查看洛谷社区规则。(黑题抄题解如果被发现后果自负)

## [JNTM2050 普鸡组](https://www.luogu.com.cn/team/48067)

### [普通题目聚集地](https://www.luogu.com.cn/training/218538#problems)

#### [ T268520 绿藻球快乐啤酒 “劲啊！”](https://www.luogu.com.cn/problem/T268520)

等待填坑.jpg

### [深鸡1](https://https://www.luogu.com.cn/training/213500#problems)

#### [T268640 【深鸡1.例3】暗藏玄鸡](https://www.luogu.com.cn/problem/T268640)

```c_cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
    char c;
    int m,n,sum=0;
    cin>>m>>c>>n;
    for(int i=1;i<=9;i++)
    {
        for(int j=1;j<=9;j++)
        {
            if(i==m&&j==n)
                cout<<"鸡";
            else cout<<"鸭";
        }
        cout<<endl; 
    }
    return 0;
}
```

#### [T268642 【深鸡1.例4】暗藏玄鸡2.0（全新升级版）](https://www.luogu.com.cn/problem/T268642)

等待填坑.jpg

### [JNTM2050普鸡组](https://www.luogu.com.cn/training/213497#problems)

#### [T266503 JNTM2050 普鸡组 无](https://www.luogu.com.cn/problem/T266503)

```c_cpp
#include<bits/stdc++.h>
using namespace std;
signed main()
{
    string s;
    cin>>s;
    cout<<s;
    return 0;
} 
```

#### [T266508 JNTM2050 普鸡组 明明的树枝666](https://www.luogu.com.cn/problem/T266508)

```c_cpp
#include<bits/stdc++.h>
using namespace std;
char c[105][1005];
signed main()
{
	int n;
	cin>>n;
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=1000;j++)
		cin>>c[i][j];
	}
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=1000;j++)
		cout<<c[i][j];
	}
	return 0;
} 
```

#### [T268502 JNTM2050 普鸡组 Cxk的行程 ](https:///problem/T268502?contestId=81676)

```c_cpp
#include<bits/stdc++.h>
using namespace std;
char c[105][1005];
signed main()
{
	int n;
	cin>>n;
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=1000;j++)
		cin>>c[i][j];
	}
	for(int i=1;i<=n;i++)
	{
		for(int j=1;j<=1000;j++)
		cout<<c[i][j];
	}
	return 0;
} 
```

#### [T266543 JNTM2050 普鸡组 超时的小明](https://www.luogu.com.cn/problem/T266543)

还没人完成这道题~

<br/>

鸣谢

|[lougu@livepan](https://www.luogu.com.cn/user/52896) a盘老师|
|--|
|[JNTM2050 普鸡组](https://www.luogu.com.cn/team/48067)全体成员|
|[JNTM2050 提瓜组](https://www.luogu.com.cn/team/48954)全体成员|