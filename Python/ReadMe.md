### 如何查看Python 安装位置以及已经安装的库

```
法一
import sys
sys.path

```

```
法二
>>>where python

Output:
D:\Anaconda3\python.exe

进入
>>>cd D:\Anaconda3

可以显示下载的库
>>>pip list

>>>pip freeze
也可以显示已下载的库
输出类似于下面：
absl-py==1.0.0
alabaster @ file:///home/ktietz/src/ci/alabaster_1611921544520/work
anaconda-client @ file:///C:/ci/anaconda-client_1635342725944/work
anaconda-navigator==2.1.1
anaconda-project @ file:///tmp/build/80754af9/anaconda-project_1626085644852/work
...


查看过时的库
>>>pip list --outdated

```

### 相似度计算方法

* [关于相似度计算方法的python实现](https://blog.csdn.net/qq_33934427/article/details/123424166?spm=1001.2101.3001.6650.15&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-15-123424166-blog-124100957.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-15-123424166-blog-124100957.pc_relevant_multi_platform_whitelistv3&utm_relevant_index=20)
* [各种相似度计算的python实现](https://blog.csdn.net/a2099948768/article/details/82218478?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-82218478-blog-124100957.pc_relevant_multi_platform_whitelistv3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-82218478-blog-124100957.pc_relevant_multi_platform_whitelistv3&utm_relevant_index=2)



### 输入、输出、登录
* [简易用户登录系统【Python】](https://blog.csdn.net/weixin_64811333/article/details/126295552)
```
LoginSystem.py
应该是
from User import *


```

* [输入input](https://blog.csdn.net/qq_60899598/article/details/123829768)


* [UnicodeDecodeError: ‘utf-8‘ codec can‘t decode byte 0xc0 in position 0: invalid start byte报错解决](https://blog.csdn.net/Deng872347348/article/details/126308403)


