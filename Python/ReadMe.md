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
类似于下面：
absl-py==1.0.0
alabaster @ file:///home/ktietz/src/ci/alabaster_1611921544520/work
anaconda-client @ file:///C:/ci/anaconda-client_1635342725944/work
anaconda-navigator==2.1.1
anaconda-project @ file:///tmp/build/80754af9/anaconda-project_1626085644852/work

查看过时的库
>>>pip list --outdated


```

