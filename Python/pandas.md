
#### 读取`csv`、`excel`
* [python读取csv文件的几种方式（含实例说明）](https://blog.csdn.net/qq_43160348/article/details/124331781)
* [用Pandas读取CSV](https://blog.csdn.net/sirobot/article/details/126177390)
* [未看 50_Pandas读取 Excel 文件 (xlsx, xls)](https://blog.csdn.net/qq_18351157/article/details/124865696)
* [6种Pandas读取Excel的方法](https://baijiahao.baidu.com/s?id=1737230506657192730&wfr=spider&for=pc)
```
pd.read_excel('fake2excel.xlsx', index_col=0)                               # 使用index_col=0，指定第1列作为索引列。
pd.read_excel('fake2excel.xlsx', index_col=None)                             # 不指定索引列
pd.read_excel(open('fake2excel.xlsx', 'rb'), sheet_name='Sheet2')               # 使用sheet_name=0，指定读取sheet2里面的内容。
pd.read_excel('fake2excel.xlsx', index_col=None, header=None)                       # 使用header=None，取消header读取。
pd.read_excel('fake2excel.xlsx', index_col=None,na_values={'name':"庞强"})          # 使用na_values，自己定义不显示的数据
pd.read_excel('fake2excel.xlsx', index_col=None, comment='#')                   # pandas提供了处理Excel注释行的方法。

```


#### 数据类型`DataFrame`
* [Pandas DataFrame入门教程（图解版）](http://c.biancheng.net/pandas/dataframe.html)
* [读取DataFrame的某行或某列](https://blog.csdn.net/weixin_44709340/article/details/122538469)
```
import pandas as pd
dict=[[1,2,3,4,5,6],[2,3,4,5,6,7],[3,4,5,6,7,8],[4,5,6,7,8,9],[5,6,7,8,9,10]]
data=pd.DataFrame(dict)
print(data)
for indexs in data.index:
    print(data.loc[indexs].values, data.loc[indexs].values[0], data.loc[indexs].values[1])
```
* [Python中Dataframe数据的排序（含实例讲解）](https://blog.csdn.net/wzk4869/article/details/126370595)
* [Python 取dataframe某一列为特定值](https://blog.csdn.net/weixin_42788078/article/details/109294575)
```
df_sub=df[df.column==2]
# column是需要限定条件列的名称，“==”后可限制任意值。
# df_sub即为所有满足column=1的数据组成的新DataFrame。
```
* [DataFrame求某列数据的均值，方差等统计数](https://blog.csdn.net/qq_53817374/article/details/123387027)

