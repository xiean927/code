```
#include <bits/stdc++.h>

using namespace std;

int screw[110][110];

int main(){
    int row,col;
    scanf("%d%d",&row,&col);
    for(int i=0;i<row;i++)
    for(int j=0;j<col;j++)
        scanf("%d",&screw[i][j]);
/*
    for(int j=0;j<col;j++)
        cout<<screw[0][j]<<endl;
    for(int i=1;i<row;i++)
        cout<<screw[i][col-1]<<endl;
    for(int j=col-2;j>=0;j--)
        cout<<screw[row-1][j]<<endl;
    for(int i=row-2;i>=1;i--)
        cout<<screw[i][0]<<endl;

    for(int j=1;j<col-1;j++)
        cout<<screw[1][j]<<endl;
    for(int i=2;i<row-1;i++)
        cout<<screw[i][col-2]<<endl;
    for(int j=col-3;j>=1;j--)
        cout<<screw[row-2][j]<<endl;
    for(int i=row-3;i>=2;i--)
        cout<<screw[i][1]<<endl;
*/
    int rst=0,cst=0,red=row,ced=col;
    while(rst<=red&&cst<=ced){
        for(int j=cst;j<ced;j++)
            cout<<screw[rst][j]<<endl;
        for(int i=rst+1;i<red;i++)
            cout<<screw[i][ced-1]<<endl;
        for(int j=ced-2;j>=cst;j--)
            cout<<screw[red-1][j]<<endl;
        for(int i=red-2;i>=rst+1;i--)
            cout<<screw[i][cst]<<endl;
        red--;ced--;rst++;cst++;
    }
    return 0;

}




```
