### 问题
```
if(window[j].endt>=540)///8时+540min=17时,17时结束
	sorry[index]=true;
window[j].endt+=time[index];
///if(window[j].endt>540)///q1
///    sorry[index]=true;
```
* 因为只要在17h之前被服务,服务时长超过17h也可以
