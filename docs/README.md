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

!>和结构体搭配使用时需重载运算符

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

<br/>

```

```
