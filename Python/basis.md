
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


