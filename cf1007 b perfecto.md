给定n，有一个数列是permutation 即从1到n不重复数字组成的数列，满足任意前缀和不是完全平方，即≠x^2.如果不存在输出-1

1.首先判断不存在
总的前缀和n*(n+1)/2==x^2
判断完全平方
bool check(int x){
int j=sqrtl((int64_t)x*(x+1)/2); //sqrt:double 1517 sqrtl:long double 1836
return ((int64_t)jj!=(int64_t)x(x+1)); //int64_t 1e192e19
}
2.构造存在的数列
可沿用check，即构造ans[i]=i的数列，每次判断某点前缀和是否是完全平方数，如果是，可交换ans[i],ans[i+1]
交换后的前缀和即为x^2+1
代码如下
void solve(){
int n;
cin>>n;
for(int i=0;i<8;i++){
if(n==a[i]){
cout<<-1<<endl;
return;
}
}
vector ans(n+1);
for(int i=1;i<=n;i++) ans[i]=i;
int j=0;
for(int i=1;i<=n;i++){
while((int64_t)jj<(int64_t)i(i+1)/2) j++;
if((int64_t)jj==(int64_t)i(i+1)/2)
swap(ans[i],ans[i+1]);
cout<<ans[i]<<" ";
}
cout<<endl;
return;
}
错误点：int64_t,sqrtl可应对精度相对高的整数，防止栈溢出
完整代码：
#include<bits/stdc++.h>
using namespace std;
#define ll long long
int a[8]={1,8,49,288,1681,9800,57121,332928};
bool check(int x){
int j=sqrtl((int64_t)x*(x+1)/2); //sqrt:double 1517 sqrtl:long double 1836
return ((int64_t)jj!=(int64_t)x(x+1)); //int64_t 1e192e19
}

void solve(){
int n;
cin>>n;
for(int i=0;i<8;i++){
if(n==a[i]){
cout<<-1<<endl;
return;
}
}
vector ans(n+1);
for(int i=1;i<=n;i++) ans[i]=i;
int j=0;
for(int i=1;i<=n;i++){
while((int64_t)jj<(int64_t)i(i+1)/2) j++;
if((int64_t)jj==(int64_t)i(i+1)/2)
swap(ans[i],ans[i+1]);
cout<<ans[i]<<" ";
}
cout<<endl;
return;
}

int main(){
ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
int tt=1;
cin>>tt;
while(tt--){
solve();
}
return 0;
}
