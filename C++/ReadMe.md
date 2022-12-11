
#### C++ 将字符串转换为浮点数
主要用到C语言的两个函数，atof()和c_str()，其中c_str()函数将string转换为字符数组，而atof()将字符数组转换为浮点数；如下图程序所示：

```
string str="123.0123";
float f=atof(str.c_str());
cout<<f;
```
* [c语言中[Error] variable or field 'CreatList' declared void错误原因分析](https://blog.csdn.net/the_little_fairy___/article/details/73238049)
* [vector 多次删除第一个元素](https://www.cnblogs.com/robin2ML/p/7719002.html)
```
voidPrintInt(const int&nData)
{
    cout<<nData<<endl;
}
int main()
{
    vector<int> vecInt;
    for(int i=0; i<10;++i)
    {
       vecInt.push_back(i);
    }
    cout<<"向量中的内容为："<<endl;
    //for_each(vecInt.begin(),vecInt.end(),PrintInt);
    for(vector<int>::iterator iter = vecInt.begin(); iter != vecInt.end(); ++iter) {
        cout << *iter << " ";
    }
    cout << "\n";
    cout<<"vector contains "<<vecInt.size()<<" elements"<<endl;
    vecInt.pop_back();//删除最后一个元素
    cout<<"删除最后一个元素后，vector contains "<<vecInt.size()<<" elements"<<endl;
     
    vector<int>::iterator k = vecInt.begin();
    vecInt.erase(k);//删除第一个元素
     
    for(vector<int>::iterator iter = vecInt.begin(); iter != vecInt.end(); ++iter) {
        cout << *iter << " ";
    }
    cout << "\n";
     
    //vecInt.erase(k); //迭代器k已经失效，会出错
    cout<<"删除第一个元素后，vector contains "<<vecInt.size()<<" elements"<<endl;
    k = vecInt.begin();
    vecInt.erase(k);
     
    for(vector<int>::iterator iter = vecInt.begin(); iter != vecInt.end(); ++iter) {
        cout << *iter << " ";
    }
    cout << "\n";
     
    cout<<"删除第一个元素后，vector contains "<<vecInt.size()<<" elements"<<endl;
    //vecInt.erase(vecInt.begin(),vecInt.end()); //删除所有元素
    //cout<<"删除所有元素后，vector contains "<<vecInt.size()<<"elements"<<endl; //输出为0
    vector<int>::iterator vecNewEnd =remove(vecInt.begin(),vecInt.end(),5); //删除元素
    cout<<"删除元素后，vector contains "<<vecInt.size()<<" elements"<<endl;
    cout<<"向量开始到新结束为止的元素："<<endl;
    //for_each(vecInt.begin(),vecNewEnd,PrintInt);
    cout<<"向量中的元素："<<endl;
    //for_each(vecInt.begin(),vecInt.end(),PrintInt);
  
    return 0;
}

```


* [Code::Blocks今天突然乱码(中文) 报错 error:converting to execution character set:Illegal byte sequence](https://blog.csdn.net/qq_52722885/article/details/122196979?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1-122196979-blog-124531566.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-1-122196979-blog-124531566.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=1)

