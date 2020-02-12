
```
#include <bits/stdc++.h>

using namespace std;

struct CMD{
    int id;
    long long time;
    string cmd;
    bool operator<(const CMD &a)const{
        if(time!=a.time)
            return id>a.id;
        else
            return time>a.time;
    }
};

const char *weeks_months[]={"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"};
const int days[]={0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

///判断是否是闰年,2月是否加1天
int leapyear(int year, int month)
{
    if(month == 2)
        return ( ((year%4==0) && (year%100!=0)) || (year%400==0) ) ? 1 : 0;
    else
        return 0;
}

const int V=5;
vector<pair<int,int> > v[V];
char buf[256];
string cmd;

///将字符串起始，终止的年 月 日 小时 分钟
///转为
int myatoi(char t[],int b,int e){
    int v=0;
    for(int i=b;i<=e;i++)
        v=v*10+t[i]-'0';
    return v;
}

 ///获取月份数 或者 星期数，
 /*
 星期日,一，二，三，四，五，六
 月份:一，二，三，四，五，六，七，八，九，十，十一，十二
 */
int getval(char t[])
{
    int i;

    t[0] = toupper(t[0]);///转为小写
    for(i = 1; t[i]; i++)
        t[i] = tolower(t[i]);

    for(i = 0; i < 12 + 7; i++)
        if(strcmp(t, weeks_months[i]) == 0)
            break;
    if(i < 12 + 7)///如果小于7,说明是星期几,如果大于等于7,说明是月份
        return i < 7 ? i : i - 6;
    else
        return -1;
}

///vector<pair<int,int> >说明一对,是起始,至终止位置的数
void setsubval(char s[], vector<pair<int, int> >& v)
{
    int p1 = 0, p2 = 0;
    for(int i = 0; s[i]; i++)
        if(s[i] == '-') {
            s[i] = '\0';///将连接符'-'分割开
            p2 = i + 1;
            break;
        }

    int val1, val2;
    if(p1 == p2) {///0==0,也就是没有'-',即字符串s是一个数
        if(isdigit(s[0]))
            val1 = atoi(s);
        else///用字母表示<month>,<day of week>范围
            val1 = getval(s);
        v.push_back(make_pair(val1, val1));
    } else {///存在'-',例如:0-6,Mon-Sat
        if(isdigit(s[0]))///0-6,的0
            val1 = atoi(s);
        else///Mon-Sat,的Mon
            val1 = getval(s);
        if(isdigit(s[p2]))///0-6,的6
            val2 = atoi(s + p2);
        else///Mon-Sat,的Sat
            val2 = getval(s + p2);
        v.push_back(make_pair(val1, val2));///val1起始位置,val2终止位置
    }
}

void setval(char s[], vector<pair<int, int> >& v)
{
    if(s[0] == '*')///如果是全部选择
        v.push_back(make_pair(-1, -1));
    else {///
        char *p = strtok(s, ",");
        while(p) {
            setsubval(p, v);
            p = strtok(NULL, ",");
        }
    }
}

///判断m是否在v.first,v.second的范围内
bool judge(int m, vector<pair<int, int> >& v)
{
    for(int i = 0; i < (int)v.size(); i++)
        if(v[i].first == -1 || (v[i].first <= m && m <= v[i].second))
            return true;
    return false;
}

///如果
bool end_time_check(int y, int m, int d, int h, int mi, int ey, int em, int ed, int eh, int emi)
{
    if(y < ey) return true;
    if(m > em) return false;///月份超过最后截止日期
    if(m < em) return true;
    if(d > ed) return false;
    if(d < ed) return true;
    if(h > eh) return false;
    if(h < eh) return true;
    if(mi > emi) return false;
    if(mi < emi) return true;
    return false;
}

int main(){
    int n;
    string s,t;

    priority_queue<CMD> q;

    cin>>n>>s>>t;

    strcpy(buf,s.c_str());
    int sy = myatoi(buf, 0, 3);
    int sm = myatoi(buf, 4, 5);
    int sd = myatoi(buf, 6, 7);
    int sh = myatoi(buf, 8, 9);
    int smi = myatoi(buf, 10, 11);
    strcpy(buf, t.c_str());
    int ey = myatoi(buf, 0, 3);
    int em = myatoi(buf, 4, 5);
    int ed = myatoi(buf, 6, 7);
    int eh = myatoi(buf, 8, 9);
    int emi = myatoi(buf, 10, 11);

    for(int i = 0; i < n; i++) {
        string ss;
        /// 分别处理：分钟，小时，日，月份，星期
        for(int j = 0; j < V; j++) {///V=5;
        ///<minutes> <hours> <day of month> <month> <day of week> <command>
            v[j].clear();

            cin >> ss;
            strcpy(buf, ss.c_str());
            setval(buf, v[j]);
        }
        cin >> cmd;
        int k = sm, l = sd, m = sh, n = smi;    /// 分别作为月份、日、小时和分钟的循环变量
        /// 分钟，小时，日，月份，星期
        for(int j = sy; j <= ey; j++, k=1)  /// 年循环处理
            for(; k <= 12; k++, l = 1)
            if(judge(k, v[3]))///<month>是否在第i个范围内 
                for(; l <= days[k] + leapyear(j, k); l++, m = 0)///<day of month>在范围内
                ///判断l是否在<day of month>范围内,星期几是否在范围内
                if(judge(l, v[2]) && judge(weekday(j, k, l), v[4]))///weekday函数 计算星期几，
                    for(; m < 24; m++, n = 0)
                    ///判断小时是否在范围内
                    if(judge(m, v[1]))/// <hours>
                    ///判断分钟是否在范围内
                        for(; n < 60; n++) {
                        if(!end_time_check(j, k, l, m, n, ey, em, ed, eh, emi))///在给定时间范围内
                            break;
                        if(judge(n, v[0])) {
                            CMD tmp;
                            tmp.id = i;
                            ///写成数字形式输出命令发出的时间,
                            ///j:年份; k:月份; l:日; m:小时; n:分钟
                            tmp.time = (long long)j * 100000000 + (long long)k * 1000000 + (long long)l * 10000 + (long long)m * 100 + n;
                            tmp.cmd = cmd;///
                            q.push(tmp);
                        }
                        }
        
    }
    return 0;
}


```
