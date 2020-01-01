### 1，关于输入形如（没有说明输入的数字个数，直接输入两排数）
``` 
9 5 32 67
9 32 67 5
```
#### 读取方式
```
#include <bits/stdc++.h>

using namespace std;

int in[65536];
int post[65536];
int n;

int main()
{
	char c;
	c = getchar();
	n = 0;
	while (c != '\n')
	{
		if (c != ' ')
		{
			ungetc(c, stdin);
			cin >> in[n];
			n++;
		}
		c = getchar();
	}
	for (int i = 0; i < n; i++)
	{
		cin >> post[i];
	}

	for(int i=0;i<n;i++){
        cout<<"in "<<in[i]<<" post "<<post[i]<<endl;
	}
    return 0;
}

Out:
9 5 32 67
9 32 67 5
in 9 post 9
in 5 post 32
in 32 post 67
in 67 post 5

```
