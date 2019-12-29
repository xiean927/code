* [解决了坑点的代码](https://blog.csdn.net/weixin_43108373/article/details/84714215)
* 我的代码未解决

```
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
#include <vector>
using namespace std;

const int maxn = 10010;
const int maxpro = 6;

//结构体初始化
struct student {
	int id;
	int scr[maxpro];
	int tol_scr;
	int cnt ;
	int perfect_pro;
	int rank;
}stu[maxn];
int problem_full[maxpro] = { 0 };

bool cmp(student &a, student &b) {
	if (a.tol_scr != b.tol_scr)
		return a.tol_scr > b.tol_scr;
	else if (a.perfect_pro != b.perfect_pro)
		return a.perfect_pro > b.perfect_pro;
	else
		return a.id < b.id;
}

int main() {
	int n, k, m;
	cin >> n >> k >> m;
	for (int i = 1; i <= k; i++) {
		cin >> problem_full[i];
	}
	///不用非得记录考生的id，输出时，按照格式输出即可
	for (int i = 1; i < maxn; i++) {
		stu[i].id = i;
		stu[i].perfect_pro=0;
		stu[i].cnt=0;
		stu[i].tol_scr=0;
		fill(stu[i].scr,stu[i].scr+maxpro,-1);
	}
	for (int i = 0; i < m;i++) {
		int tmp,num,score;
		cin >> tmp >> num >> score;
		if (score == -1) {
			stu[tmp].scr[num] = 0;
		}
		else {///存在满分情况，多次提交
			//if (problem_full[num] == score) {
		//		stu[tmp].perfect_pro++;
		//	}
			if(score>stu[tmp].scr[num])
				stu[tmp].scr[num] = score;
			stu[tmp].cnt++;
		}
	}

	for (int i = 1; i <= n; i++) {
		for (int j = 1; j <= k; j++) {
			if (stu[i].scr[j] != -1) {
				stu[i].tol_scr += stu[i].scr[j];
				if(stu[i].scr[j]==problem_full[j])
                    stu[i].perfect_pro++;
			}
		}
	}
	sort(stu+1, stu + n+1, cmp);
	stu[1].rank = 1;
	for (int i = 2; i <= n; i++) {
		if (stu[i].tol_scr == stu[i - 1].tol_scr) {
			stu[i].rank = stu[i - 1].rank;
		}
		else {
			stu[i].rank = i;
		}
	}

	for (int i = 1; i <= n; i++) {
		if (stu[i].cnt) {
			printf("%d %05d %d", stu[i].rank, stu[i].id, stu[i].tol_scr);
			for (int j = 1; j <= k; j++) {
				if (stu[i].scr[j] == -1)
					printf(" -");
				else
					printf(" %d", stu[i].scr[j]);
			}
			printf("\n");
		}
	}
	return 0;
}

```
