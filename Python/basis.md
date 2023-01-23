

#### `map`
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

#### `reduce函数`

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

#### [python中yield的用法详解](https://blog.csdn.net/mieleizhi0522/article/details/82142856/)


### 函数
#### '->'
```
def add(x, y) -> int:
  return x+y
  
def add(x:int, y:int) ->bool:
    if(x>y):
        return True
    else:
        return False

```
* `->` 常常出现在python函数定义的函数名后面，为函数添加元数据，描述函数返回的数据类型。
* 优点 可以强制规定返回数据的类型，同时还可以设定返回类型为None，也就是不返回任何东西。利于后期查看掌握函数的返回类型。

* [Python:Optional和带默认值的参数](https://blog.csdn.net/qq_44683653/article/details/108990873)




