
### [转自深森](https://blog.csdn.net/shensen0304/article/details/88246377)
* 简单模拟
* 想复杂了，一开始，能量还想着定义黑白球的，直接定义一个即可
* 方向翻转（怎么不太对啊!!）：
  * 碰到上墙，
    * （-1，1）  => （1，1）
    * （-1，-1） => （1，-1）
  * 碰到下墙，
    * （1，1）  => （-1，1）
    * （1，-1） => （-1，-1）
  * 碰到左墙，
    * （1，-1）  => （1，1）
    * （-1，-1） => （-1，1）
  * 碰到右墙，
    * （-1，1） => （-1，-1）
    * （1，1）  => （1，-1）
  
```
#include <bits/stdc++.h>

using namespace std;

bool win(int x, int y) {
	if ((x == 0 && y == 0) || (x == 8 && y == 0) || (x == 16 && y == 0) || (x == 0 && y == 5) || (x == 8 && y == 5) || (x == 16 && y == 5))
		return true;
	return false;
}

int main() {
	int wx, wy, bx, by;
	int dx, dy;
	int power;
	bool flag = true;//flag=true代表现在是白球在走，false代表现在是黑球在走
	scanf("%d %d", &wx, &wy);
	scanf("%d %d", &bx, &by);
	scanf("%d %d", &dx, &dy);
	scanf("%d", &power);
	int ans = 0;
	while (power > 0) {
		if (win(wx, wy))
			ans = -1;
		if (win(bx, by))
			ans = 1;
		if (ans == -1 || ans == 1)
			break;
		if (flag == true) {//白球在走
			wx += dx;//先走再判断
			wy += dy;
			power--;
			if (wx == bx && wy == by)//走完了发现装上黑球，flag=false
				flag = false;
			if (wy == 0||wy==5)//撞上上面或下面的墙壁，
				dy = -dy;
			if (wx == 0||wx==16)//撞上两边的墙壁
				dx = -dx;
		}
		if (flag == false) {
			bx += dx;
			by += dy;
			power--;
			if (by == 0 || by == 5)//撞上上面或下面的墙壁，
				dy = -dy;
			if (bx == 0 || bx == 16)//撞上两边的墙壁
				dx = -dx;
		}
	}
	printf("%d", ans);
	return 0;
}

```






