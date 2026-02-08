# 牛客 2026 寒假算法集训营第一场补题

其实前两个小时我都忘记还有这沟槽的比赛了（）写了最后一题就玩手机了，懈怠这一块。

## C Array Covering

这个挺简单的，主要需要三个数：

数组的头和尾，以及头尾之间（不包含头尾）中这些数字里的最大数。分别记为 L、M、R。

题目允许我们挑两个点，看两个点的数比一下，谁大谁就把这两个点中间的所有数字都替换成这个大数，没有限制操作次数。因为它只能改两点中间的数，而不能替换区间两边的端点，所以数组的头尾两个数是不可能被替换的。我们现在的目的是要把数组头尾之间的数字全部拉成最大值，那么当然中间的数全部都要替换成 `max(L, M, R)`。和的公式即为 `sum = max(L, M, R) * min(n - 2, 0) + L + R`。

这样子其实也不用开一个大小为 `n` 的 `vector`，开三个变量就行，头尾两个，中间一个，中间的那个数就根据读入的数去撑出一个头尾之间这些数字的最大值。

我当时补题代码其实写的挺糙的，当然是哪个写的快写哪个。

从题目给定的数据来看，和最大能到 5e14，这题得开 `long long`。

```cpp
#include <bits/stdc++.h>

using namespace std;
using ll = long long;
using ull = unsigned long long;

int main() {
    ios::sync_with_stdio(0), cin.tie(0);
    int t;
    cin >> t;
    while (t--) {
        ll n;
        cin >> n;
        if (n == 1) {
            cin >> n;
            cout << n << '\n';
            continue;
        }
        if (n == 2) {
            ll tmp;
            cin >> tmp >> n;
            cout << tmp + n << '\n';
            continue;
        }
        ll arr[3];
        arr[1] = LLONG_MIN;
        cin >> arr[0];
        for (int i = 1; i < n - 1; i++) {
            ll tmp;
            cin >> tmp;
            arr[1] = max(arr[1], tmp);
        }
        cin >> arr[2];
        auto maxp = max_element(arr, arr + 3);
        ll ans = *maxp * (n - 2) + arr[0] + arr[2];
        cout << ans << '\n';
    }
}
```

## K Constructive

~~注意力失调~~ 好吧其实就是单纯自己琢磨了半天，什么规律下一个数列能拼出一个符合题目要求的数组，结果看了一眼题解，只有两个解，一个是数组长度为 1 或 3 时，由于题目要求字典序最小，数组升序着排就行了。

没什么好说的，代码如下：

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    ios::sync_with_stdio(0), cin.tie(0);
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        if (n==1||n==3) {
            cout << "YES\n";
            if (n==1) cout << "1\n";
            else cout << "1 2 3\n";
        } else {
            cout << "NO\n";
        }
    }
}
```
