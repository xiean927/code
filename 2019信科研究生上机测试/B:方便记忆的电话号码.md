

* 

```
#include <bits/stdc++.h>

using namespace std;

map<string,int> mp;
int cti[256];

int main(){
    cti['A']=2;cti['B']=2;cti['C']=2;
    cti['D']=3;cti['E']=3;cti['F']=3;
    cti['G']=4;cti['H']=4;cti['I']=4;
    cti['J']=5;cti['K']=5;cti['L']=5;
    cti['M']=6;cti['N']=6;cti['O']=6;
    cti['P']=7;cti['R']=7;cti['S']=7;
    cti['T']=8;cti['U']=8;cti['V']=8;
    cti['W']=9;cti['X']=9;cti['Y']=9;

    int n;
    string line;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        cin>>line;
        string resline;
        int flag=0;///符号位只能有一个
        for(int i=0;i<(int)line.size();i++){
            if(line[i]=='-')    continue;
            if(line[i]>='0'&&line[i]<='9')
                resline+=line[i];
            if(line[i]>='A'&&line[i]<'Z'&&line[i]!='Q')
                resline+=(cti[line[i]] + '0');

        }
        mp[resline]+=1;

    }
    for(map<string,int>::iterator it=mp.begin();it!=mp.end();it++){
        if(it->second>=2)
            cout<<it->first<<" "<<it->second<<endl;
    }
    return 0;
}
```

* [大神Hash](https://blog.csdn.net/fingertipx/article/details/41548329)
```
#include <stdio.h>
int Table[256];
int Count[1000][10000];
int main()
{
	Table['A'] = Table['B'] = Table['C'] = 2;
	Table['D'] = Table['E'] = Table['F'] = 3;
	Table['G'] = Table['H'] = Table['I'] = 4;
	Table['J'] = Table['K'] = Table['L'] = 5;
	Table['M'] = Table['N'] = Table['O'] = 6;
	Table['P'] = Table['R'] = Table['S'] = 7;
	Table['T'] = Table['U'] = Table['V'] = 8;
	Table['W'] = Table['X'] = Table['Y'] = 9;
	for (unsigned char x = '0'; x <= '9'; x++) {
		Table[x] = (int)(x - '0');
	}
	int n; 
	scanf("%d",&n);
	char Tel[201];
	while (n) {
		n--;
		scanf("%s", Tel);
		int t1 = 0, t2 = 0;
		int Tmp[7]; int Index = 0;
		int i = 0;
		while (Tel[i] != 0) {
			if (Tel[i] != '-') {
				Tmp[Index] = Table[Tel[i]];
				Index++;
			}
			i++;
		}
		t1 = 100 * Tmp[0] + 10 * Tmp[1] + Tmp[2];
		t2 = 1000 * Tmp[3] + 100 * Tmp[4] + 10 * Tmp[5] + Tmp[6];
		Count[t1][t2]++;
	} 
	
	bool Out = true;	
	for (int i = 0; i < 1000; i++) {
		for (int j = 0; j < 10000; j++) {
			if (Count[i][j] > 1) {
				printf("%.3d-%.4d %d\n", i, j, Count[i][j]);
				Out = false;
			}
		}
	}
	
	if (Out) printf("No duplicates.");
	return 0;
}
```
