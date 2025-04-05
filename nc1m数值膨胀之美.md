
```markdown
# 题目描述
定义一个数组的极差为：数组的元素最大值减去最小值。

小红拿到了一个数组，她准备进行恰好一次操作：选择一个非空区间，将其中所有元素都乘以 `2`。

小红希望最小化数组的极差，你能帮帮她吗？

## 输入描述:
第一行输入一个正整数 `𝑛` (`1 ≤ 𝑛 ≤ 10^5`) 代表数组中的元素数量。 

第二行输入 `𝑛` 个正整数 `𝑎1, 𝑎2, …, 𝑎𝑛` (`1 ≤ 𝑎𝑖 ≤ 10^9`) 代表数组元素。

## 输出描述:
输出一个整数，代表操作恰好一次后，数组的最小极差。

## 示例1
### 输入
2
3 4
### 输出
2
### 说明
在这个样例中，选择 `[1, 1]` 区间，数组变为 `{6, 4}`，极差为 `6−4 = 2`。

## 示例2
### 输入
4
1 2 4 3
### 输出
2
### 说明
在这个样例中，操作方案不唯一，可以选择

### 思路
显然我们优先将最小值翻倍。如果想要扩大区间，我们则选择“包含最小值和次小值”的最小区间，以此类推。

### 模拟方式
我们首先得到每个元素的下标，然后维护区间两个端点\(l\)和\(r\)。当我们需要翻倍的区间增大的时候（比如从最小值到次小值），只需要将\(l\)向左移动或者将\(r\)向右移动，直到包含当前需要选择的元素。

举个例子，假设当前我们翻倍的区间是\([6, 8]\)，这时下一个待翻倍的最小值位置在\(11\)，这时我们需要将第\(9, 10, 11\)这三个数同时翻倍。 `[1, 2]` 区间或者 `[1, 1]` 区间。

###代码如下
以下是将你提供的代码放在 Markdown 代码块中的形式：

```cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long

void solve(){
    ll n;
    cin>>n;
    vector<int> b(n+1);
    pair<int,int> a[200010];
    for(int i=0;i<n;i++){
        cin>>a[i].first;
        a[i].second=i;
        b[i]=a[i].first;
    }
    a[n].first=2e9;
    sort(a,a+n);
    int ma=max(a[0].first*2,a[n-1].first);
    int res=ma-min(a[0].first*2,a[1].first);
    int l=a[0].second,r=a[0].second;
    for(int i=1;i<n;i++){
        while(a[i].second<l){
            l--;
            ma=max(ma,b[l]*2);
        }
        while(a[i].second>r){
            r++;
            ma=max(ma,b[r]*2);
        }
        res=min(res,ma-min(a[0].first*2,a[i+1].first));
    }
    cout<<res<<endl;
    return;
}

int main(){
    ios::sync_with_stdio(0);
    cin.tie(0); cout.tie(0);
    int tt=1;
    //cin>>tt;
    while(tt--){
        solve();
    }
    return 0;
}
```
 
