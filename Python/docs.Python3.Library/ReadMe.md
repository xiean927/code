
## 基础
### `字符串string`
* [Python字符串字母大小写转换](https://blog.csdn.net/TINA_JING_LIU/article/details/122691669)
```
str1.lower()
str1.upper()
```
* [python如何读取txt文件内容](https://m.php.cn/article/479676.html)
* [python将数据写入txt](https://blog.csdn.net/HoyAnGx/article/details/124835576)
* [总结几个Python中常见的遍历字典的方法](https://blog.csdn.net/yaoyuanna/article/details/126009259)
* [用python将数据写入Excel文件中](https://blog.csdn.net/weixin_44322716/article/details/127790436)

* `查找find函数`
```
语法：S.find(sub[, start[, end]]) -> int
参数
    str：要查找的字符串。
    start：可选参数，开始索引，默认为0。
    end：可选参数，结束索引，默认为字符串长度。
返回值
    如果包含子字符串返回开始的索引值，否则返回-1。
示例
str = '我爱我的爸妈'
print('返回子字符串开始的偏移量：', str.find('我的'))
print('指定开始索引：', str.find('我的', 3))
print('指定结束索引：', str.find('我的', 0, 2))
print('没有找到的情况下返回-1：', str.find('姐姐'))

Out:
返回子字符串开始的偏移量： 2
指定开始索引： -1
指定结束索引： -1
没有找到的情况下返回-1： -1

help(str.find)
find(...) method of builtins.str instance
    S.find(sub[, start[, end]]) -> int
    
    Return the lowest index in S where substring sub is found,
    such that sub is contained within S[start:end].  Optional
    arguments start and end are interpreted as in slice notation.
    
    Return -1 on failure.
```


## `import库`
* Python中的n次方用pow()方法来表示，pow()方法返回 xy（x的y次方）的值。
```
import math
math.pow( x, y )

内置的 pow() 方法
pow(x, y[, z])
函数是计算x的y次方，如果z在存在，则再对结果进行取模，其结果等效于pow(x,y) %z
注意：pow() 通过内置的方法直接调用，内置方法会把参数作为整型，而 math 模块则会把参数转换为 float。

```

### 爬虫
* [python爬取论文](https://www.cnblogs.com/znjy/p/14884125.html)


* [python 判断字符是否是字母](https://blog.csdn.net/weixin_46507345/article/details/123406895)
* [Python中交换字典键值对的方法](https://blog.csdn.net/weixin_46707326/article/details/117387329)
* [python将整数转换成二进制形式的方法](https://blog.csdn.net/ACBC12345/article/details/124441879)

### pdf处理
* [Python实现PDF复制自动去除换行及空格](https://blog.csdn.net/m0_59426411/article/details/122808275)
* [pdfminer.pdfparser 用python从PDF格式论文中读取其中的参考文献](https://www.jianshu.com/p/bee9b09abaf5)


### pathlib — Object-oriented filesystem paths
* [pathlib — Object-oriented filesystem paths](https://docs.python.org/3/library/pathlib.html)
* [pathlib --- 面向对象的文件系统路径](https://docs.python.org/zh-cn/3/library/pathlib.html#)

### glob模块
* [glob库中主要的3个函数：glob()函数、iglob()函数、escape()函数](https://blog.csdn.net/weixin_41261833/article/details/108069945)
* [python复制、移动文件到指定文件夹](https://blog.csdn.net/longshaonihaoa/article/details/105679517?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-0-105679517-blog-124631123.pc_relevant_3mothn_strategy_recovery&spm=1001.2101.3001.4242.1&utm_relevant_index=3)
* []()

## 算法
### `哈夫曼树`
* [Python实现哈夫曼编码（Huffman code）(不怎么用)](https://blog.csdn.net/qq_42932667/article/details/121952585)
* [Python 代码实现哈夫曼编码](https://blog.csdn.net/amnesia_h/article/details/123671999)


## 可视化
### 绘制二叉树 Python
* [使用python绘制二叉树（matplotlib + networkx）](https://blog.csdn.net/weixin_50425288/article/details/124019369)


## 概率论
* [实现随机正态分布数据，并导出到表格](https://blog.csdn.net/m0_53533553/article/details/127639771)
* [python如何生成正态分布随机数_python 生成正态分布数据,并绘图和解析](https://blog.csdn.net/weixin_42436482/article/details/112183032)
* 标准差（Standard Deviation） ，数学术语，是离均差平方的算术平均数（即：方差）的算术平方根，用σ表示。标准差也被称为标准偏差，或者实验标准差，在概率统计中最常使用作为统计分布程度上的测量依据。
* 标准差是方差的算术平方根。标准差能反映一个数据集的离散程度。平均数相同的两组数据，标准差未必相同。










