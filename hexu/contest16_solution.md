[比赛链接](http://www.hzxjhs.com:83/contest/749)

# 比赛中解决的问题
## A
### Problem description
> 给你一个长度为N的正整数序列，如果一个连续的子序列，子序列的和能够被K整
除，那么就视此子序列合法，求原序列包括多少个合法的连续子序列？
对于一个长度为8的序列,K=4的情况：2, 1, 2, 1, 1, 2, 1, 2 。它的答案为6，子序列
是位置1->位置8,2->4,2->7,3->5,4->6,5->7。

### Data Limit：n <= 50000,k<=1000000  Time Limit: 1s

### Solution
> 设有a b c d e，(a+b)%mod=k,(a+b+c+d+e)%mod=k,那么(c+d+e)%mod=0，即该子序列是mod K=0。
### Code
```cpp
#include<iostream>
#include<cstdio>
using namespace std;
int map[1000010],t,n,k;
int main()
{
    scanf("%d",&t);
    while (t--){
        scanf("%d%d",&k,&n);
        map[0]=1;   int s = 0;
        for (int i=1; i<=n; ++i){
            long long  j;
            scanf("%d",&j);
            s = s+j;
            if (s>=k) s = s%k;
            ++map[s];          
        }
        long long  ans = 0;
        for (int i=0; i<=1000005; ++i){
            if (map[i]>1) ans = ans + map[i]*(map[i]-1)/2;
            map[i] = 0;
        }
        printf("%d\n",ans);
    }
}
```
*****

## B
### Problem description
> 钓鱼是捕捉鱼类的一种方法。</P>
-----维基百科</P>
我们把钓鱼的过程放在坐标系里来考虑。图中蓝色的点为船，初始时它的坐标记为</P>
(Ax,y)。河深为y，河宽为x。某个时刻会从左边界或右边界游出来一条鱼(左边的往右边游，</P>
右边的往左边游)，即鱼游出来时的横坐标为0或x，这条鱼每秒会游D个单位长度，鱼的长</P>
度为L。初始时刻为0，对于每个时刻x，船可以选择花费1s向左或向右移动最多Q个单位</P>
长度，或者选择在当前位置进行钓鱼，钓鱼的动作是瞬间的，且发生在时刻x，鱼还来不及</P>
移动就被钓上了。如果选择钓鱼，那么在时刻x就不能动。{x+1时刻可以选择移动}设当前</P>
位置为z，将鱼看成一条线段，当线段与直线x=z相交时就认为鱼上钩了，所以一次钓鱼动</P>
作可能会钓多条鱼。</P>
聪明的你告诉钓鱼者，在T时刻前最多能钓多少鱼?</P>

### Data Limit：100%的数据满足1<=T,time<=10 ，1<=Ax,Ay,Q,x,y,D,L<=10，1<=N<=1430%的数据满足 1<=N<=5
### Time Limit: 1s
### Solution
> 考虑预处理出可能发生的所有情况，因为鱼的个数和N都很小，所以可以用状压DP保存下所有的状态，然后枚举可能的状态，计算一下和就可以了。

### Code
```cpp
#include<iostream>
#include<cstring>
#include<cstdio>
bool f[12][11][1<<14],hx;
struct fish{int l,r,speed,time;}a[15];
int max(int a,int b){return a>b?a:b;}
int min(int a,int b){return a<b?a:b;}
int main()
{
    int t,x;
    scanf("%d%d%d",&t,&x,&hx);
    int n,ax,q; scanf("%d%d%d",&ax,&q,&n); f[0][ax][0]=1;
    for (int i=1; i<=n; ++i){
        int xx,dd,ll,tt; scanf("%d%d%d%d%d",&xx,&hx,&dd,&ll,&tt);
        if (xx==0){
            a[i].l=xx-ll; a[i].r=xx; a[i].speed = dd; a[i].time = tt;
        }else {
            a[i].l=xx;    a[i].r=xx+ll; a[i].speed = -dd; a[i].time = tt;
        }
    }
    for (int i=0; i<=t; ++i)
        for (int j=0;j<=x; ++j)
            for (int k=0; k<(1<<n);++k)
            if (f[i][j][k]){
                for (int p=-q; p<=q; ++p) if (j+p>=0&&j+p<=x) f[i+1][j+p][k] = 1;
                int t = k;
                for (int p=1; p<=n; ++p)
                if ((a[p].l+a[p].speed*(i-a[p].time))<=j&&(a[p].r+a[p].speed*(i-a[p].time)>=j))   t= t|1<<(p-1);
                f[i+1][j][t]=1;
            }
    int Max=0;
    for (int i=0; i<=x; ++i)
        for (int j=0; j<(1<<n); ++j)
        if (f[t+1][i][j])
        {
            int ans = 0;
            for (int k=0; k<n; ++k) if (j&(1<<k)) ++ans;
            Max = max(Max,ans);
        }
    printf("%d\n",Max);
    return 0;  
}
```
*****

## D
### Problem description
> 给你一些符号，然后要你给这些符号赋上一些值，同样的符号可以值赋值一次，我们可以赋值a 1次，赋值b16次，赋值c 8 次，赋值D 8次</P>
赋值E 16次。要你求出符号的个数*符号的权值的最小总和

### Data Limit：n <= 1e5  Time Limit: 1s
### Solution
> 贪心即可。

### Code
```cpp
#include<iostream>
#include<algorithm>
#include<cstdio>
#include<cstring>
using namespace std;
int a,b,c,d,e,n,tot;
int map[1500];
int aa[100];
struct node{int t,p;}cc[6];
char ch;
bool cmp(node a,node b){
    return a.p<b.p;
}
int main(){
    scanf("%d%d%d%d%d",&a,&b,&c,&d,&e);
    cc[5].t=15; cc[5].p=e;
    cc[1].t=8;  cc[1].p=d;
    cc[2].t=8;  cc[2].p=c;
    cc[3].t=16; cc[3].p=b;
    cc[4].t=1;  cc[4].p=a;
    sort(cc+1,cc+1+5,cmp);
//  for (int i=1; i<=5; ++i) printf("%d %d\n",cc[i].t,cc[i].p);
    scanf("%d\n",&n);
    for (int i=1; i<=n; ++i){
        scanf("%c",&ch);
        int j=int (ch);
        ++map[j];  
        //printf("%d ",j);         
    }
    tot = 0;
    for (int i=0; i<1500; ++i)
    if (map[i]>0) {
        ++tot;
        aa[tot] = map[i];      
    }
    //printf("%d",tot);
    sort(aa+1,aa+1+tot);
    //  for (int i=1; i<=tot; ++i) printf("%d ",aa[i]);
    //printf("\n");
    int ans = 0;
    for (int i=tot; i>=1; --i)   {
        for (int j=1; j<=5; ++j)
        if (cc[j].t>0) {
            --cc[j].t;
            ans +=cc[j].p*aa[i];
             
            break;
        }      
    }
        printf("%d",ans);
 
}
```
*****

# 赛后补题

## C
### Problem description
> 树是由N个等腰三角形构成的，每个三角形的对称轴在y轴上，且每个三角形与上面和下 </P>
面的三角形有接触。雪以与x轴成a角(0<a<pi)下落,问雪与三角形有接触的长度是多少? </P>
(也可以理解为成a角的平行光源射向树，问被照亮的长度)</P>
### Data Limit：n <=100000  Time Limit: 1s

### Solution
> 模拟，我们可以假设一条移动的线，每次求这条线和当前三角形的交点，然后求出投影长度，如果投影长度小于此三角形的斜边的长度</P>
  就把直线移动到通过此三角形的左边的点上。继续即可。


### Code
```cpp
include<cstdio>
#include<cmath>
using namespace std;
double pi=acos(-1),eps=1e-5,a;
int n;
struct data {
    double l,nowa,lon,loc;
}f[1000001];
int main() {
    scanf("%lf%d",&a,&n);
    if (a>pi/2) a=pi-a;
    double ans=0,bk=tan(a);
    for (int i=1;i<=n;i++) {
        scanf("%lf%lf",&f[i].l,&f[i].nowa);
        f[i].lon=(f[i].l*0.5)/sin(f[i].nowa*0.5);
        f[i].loc=f[i-1].loc+(f[i].l*0.5)/tan(f[i].nowa*0.5);
    }
    double n1=0,n2=0;
    for (int i=1;i<=n;i++) {
        double ng=tan(a)*f[i].l*0.5;
        double ng1=-f[i].loc-ng,ng2=-f[i].loc+ng;
        double nk=-tan((pi-f[i].nowa)/2),nb=-f[i-1].loc;
        double nx1=(n1-nb)/(nk-bk),nx2=(n2-nb)/(-nk-bk);
        double l1=2*nx1*f[i].lon/f[i].l,l2=2*nx2*f[i].lon/f[i].l;
        if (!(ng1>n1)) n1=ng1,ans+=f[i].lon-l1;
        if (!(ng2<n2)) n2=ng2,ans+=f[i].lon+l2;
    }
    printf("%.1lf\n",ans);
    return 0;
}
```
*****




#
