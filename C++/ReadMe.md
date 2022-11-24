
#### C++ 将字符串转换为浮点数
主要用到C语言的两个函数，atof()和c_str()，其中c_str()函数将string转换为字符数组，而atof()将字符数组转换为浮点数；如下图程序所示：

```
string str="123.0123";
float f=atof(str.c_str());
cout<<f;
```

