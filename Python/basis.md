
#### 'map'
##### 题目1：输入三个整数，输出最大值
* 输入三个整数，输出最大值，可以用以下语句输入3个整数：
```
a, b, c = map(int, input().split())
```
* 输入样例
```
10 20 30
```
* 输出样例
```
30
```
```
Code:
a, b, c = map(int, input("输入三个整数：").split(" "))

maxAB = max(a, b)
maxABC = max(maxAB, c)

print(maxABC)

Output:
输入三个整数：10 20 30
30

```

* [Python的map、reduce函数](https://zhuanlan.zhihu.com/p/77311224)

#### 'reduce函数'

```
求10的阶乘，就可以用reduce做：

# 导入reduce
from functools import reduce 
# 定义函数
def f(x,y):
    return x*y
# 定义序列，含1~10的元素
items = range(1,11)
# 使用reduce方法
result = reduce(f,items)
print(result)
```















