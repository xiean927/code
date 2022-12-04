

### 计时是程序中非常常见的需求，可以通过其判断程序运行的实时性。最常见的计时功能实现如下：
```
#include <iostream>
#include <ctime>

int main()
{
	clock_t start = clock();
	//耗时计算
	for (size_t i = 0; i < 100000; i++)
	{
		cos(1);
		sin(1);
		tan(1);
	}
	clock_t end = clock();
	std::cout << "花费了" << (double)(end - start) / CLOCKS_PER_SEC << "秒" << std::endl;
}


```
### 使用C++11标准的chrono函数则可以将精度提升到微妙级别：
```
#include <iostream>
#include <chrono>

int main()
{
	std::chrono::system_clock::time_point start=std::chrono::system_clock::now();
	//耗时计算
	for (size_t i = 0; i < 100000; i++)
	{
		cos(1);
		sin(1);
		tan(1);
	}
	std::chrono::system_clock::time_point end = std::chrono::system_clock::now();
	std::cout << "花费了" << std::chrono::duration_cast<std::chrono::microseconds>(end - start).count() << "微秒" << std::endl;
}


```
