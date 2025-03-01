### 问题描述

给定 `n`，有一个数列是排列（permutation），即从 1 到 `n` 不重复数字组成的数列，要求满足任意前缀和不是完全平方，即 $\neq x^2$。如果不存在这样的排列则输出 -1。

### 解决方案思路

#### 1. 判断不存在的情况
总的前缀和 $\frac{n\times(n + 1)}{2}=x^2$，判断是否为完全平方数，代码如下：
```cpp
bool check(int x){
    int j = sqrtl((int64_t)x * (x + 1) / 2); //sqrt:double 15 - 17, sqrtl:long double 18 - 36
    return ((int64_t)j * j != (int64_t)x * (x + 1)); //int64_t 1e19 - 2e19
}
```

#### 2. 构造存在的数列
可沿用 `check` 函数，即构造 `ans[i] = i` 的数列，每次判断某点前缀和是否是完全平方数，如果是，可交换 `ans[i]` 和 `ans[i + 1]`，交换后的前缀和即为 $x^2 + 1$。代码如下：
```cpp
void solve(){
    int n;
    cin >> n;
    for(int i = 0; i < 8; i++){
        if(n == a[i]){
            cout << -1 << endl;
            return;
        }
    }
    vector<int> ans(n + 1);
    for(int i = 1; i <= n; i++) ans[i] = i;
    int j = 0;
    for(int i = 1; i <= n; i++){
        while((int64_t)j * j < (int64_t)i * (i + 1) / 2) j++;
        if((int64_t)j * j == (int64_t)i * (i + 1) / 2)
            swap(ans[i], ans[i + 1]);
        cout << ans[i] << " ";
    }
    cout << endl;
    return;
}
```

### 错误点说明
`int64_t` 和 `sqrtl` 可应对精度相对高的整数，防止栈溢出。

### 完整代码
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long
int a[8] = {1, 8, 49, 288, 1681, 9800, 57121, 332928};

bool check(int x){
    int j = sqrtl((int64_t)x * (x + 1) / 2); //sqrt:double 15 - 17, sqrtl:long double 18 - 36
    return ((int64_t)j * j != (int64_t)x * (x + 1)); //int64_t 1e19 - 2e19
}

void solve(){
    int n;
    cin >> n;
    for(int i = 0; i < 8; i++){
        if(n == a[i]){
            cout << -1 << endl;
            return;
        }
    }
    vector<int> ans(n + 1);
    for(int i = 1; i <= n; i++) ans[i] = i;
    int j = 0;
    for(int i = 1; i <= n; i++){
        while((int64_t)j * j < (int64_t)i * (i + 1) / 2) j++;
        if((int64_t)j * j == (int64_t)i * (i + 1) / 2)
            swap(ans[i], ans[i + 1]);
        cout << ans[i] << " ";
    }
    cout << endl;
    return;
}

int main(){
    ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    int tt = 1;
    cin >> tt;
    while(tt--){
        solve();
    }
    return 0;
}
```

你可以直接复制上述内容到 Markdown 编辑器中，它会按照代码块、标题等格式进行渲染。 
