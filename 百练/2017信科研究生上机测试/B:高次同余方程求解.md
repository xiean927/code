

```
//高次同余方程求解
#include<iostream>
using namespace std;
int main(){
	int k, n;
	cin >> k >> n;
	int res = 1;
	for (int x = 1; x < n; x++){
		res = 1;
		for (int i = 1; i <= k; i++){//求x的k次方
			res = res*x;
			res = res%n;//根据提示，取余是为了防止数据溢出
		}
		if (res == 1){
			cout << x << endl;
		}
	}
	return 0;
}

```
