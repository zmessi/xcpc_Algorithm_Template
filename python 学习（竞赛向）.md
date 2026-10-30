# python 学习（竞赛向）

## 变量

```
global x
全局变量
在函数中使用全局变量的时候需要先global声明一下
```

## 自定义优先级

```
class Number:
    def __init__(self, val1, val2):
        self.val1 = val1
        self.val2 = val2
    
    def __eq__(self, other):
        if self is other:
            return True
        if hasattr(other, 'val1') and hasattr(other, 'val2'):
            return self.val1 == other.val1 and self.val2 == other.val2
    
    def __gt__(self, other):
        if self.val2 == other.val2:
            return self.val1 > other.val1
        else:
            return self.val2 > other.val2
    
    def __ge__(self, other):
        if self.val2 == other.val2:
            return self.val1 >= other.val1
        else:
            return self.val2 > other.val2

```

## 输入输出

```
输入整数 a = int(input())
输入字符串 s = input()
输入一行a数组 map(int, input().split()) 
list(map(int, input().split()))

输出(自动回车)：print(a, b)
输出一行带空格：  print(a, end=" ")
```

## 快读

```
import sys

input = lambda:sys.stdin.readline()
```

### 循环

```
for i in range(l, r, step):
[L, r)步长为step
```

### 数组

```
 一维：pre = [[INF] * (n + 10)]
 二维：st = [[0] * (m + 1) for _ in range(n + 1)]
 长度 len(st)
 高维：dp = [[[-1000000 for _ in range(2)] for _ in range(6)] for __ in range(n + 2)]
```

### 优先队列

小根堆

```
import queue as pq
q = pq.PriorityQueue()
//判断队列是否为空
q.empty()
//放入对位
q.put()
//取出队头元素
q.get()
```

### 容器

#### dict（词典）

```
re创建： dict = {}
查询是否在不在 c in/not in dict
一开始不存在需要先赋值为1
```

## 取消python的递归层数

```
import sys
sys.setrecursionlimit(10**5)
```

## 保留小数位数

```
四舍五入
num = 3.14159
result = round(num, 2)
print(result)

输出：

number = 3.14159
print(format(number, '.2f'))
```



## 线段树

```
class node:
    def __init__(self, l, r, v=0):
        self.l = l
        self.r = r
        self.v = v


dp = [0] * N
f = [0] * N
tr = [None for _ in range(4 * N)]


def pushup(u):
    global tr
    tr[u].v = max(tr[u << 1].v, tr[u << 1 | 1].v)


def build(u, l, r):
    global tr
    tr[u] = node(l, r)

    if l == r:
        return
    else:
        mid = l + r >> 1
        build(u << 1, l, mid)
        build(u << 1 | 1, mid + 1, r)


def query(u, l, r):
    global tr
    if l <= tr[u].l and tr[u].r <= r:
        return tr[u].v

    mid = tr[u].l + tr[u].r >> 1
    res = 0
    if (l <= mid): res = query(u << 1, l, r)
    if (r > mid): res = max(res, query(u << 1 | 1, l, r))
    return res


def modify(u, l, r, v):
    global tr
    if l <= tr[u].l and tr[u].r <= r:
        tr[u].v = v
        return
    else:
        mid = tr[u].l + tr[u].r >> 1
        if (l <= mid):
            modify(u << 1, l, r, v)
        else:
            modify(u << 1 | 1, l, r, v)
        pushup(u)
        return
```

## 树状数组

```
def lowbit(x):
    return x & -x

def add(x, v):  
    while x < N:
        tr[x] += v
        x += lowbit(x)

def query(x):
    res = 0
    while x:
        res += tr[x]
        x -= lowbit(x)
    return res

```

 
