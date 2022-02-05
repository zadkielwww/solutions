[比赛链接](https://www.acwing.com/activity/content/95/)  
AC : 3  
Wrong_Times : 2 (T1 T2)  
Rank : 14  
  
- #### T1：
  
签到题，但眼睛没脑子好用。  
思路：暴力枚举 x, y 即可，由于 n, a, b <= 1000，所以 x, y 的取值范围应该是 [0, 1000]，第一次错误是因为误将 x, y 的取值范围写成 (0, 1000]，应该注意一下**方程的解包括正负数**。  
代码：  
```
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int n, a, b;
    cin >> n >> a >> b;
    for (int i = 0; i <= 1000; i++)
        for (int j = 0; j <= 1000; j++)
            if (i * a + j * b == n)
                return printf("YES\n%d %d\n", i, j), 0; puts("NO");
}
```  
  
- #### T2:
双指针简单题，但是应该改正的老习惯：`#define int long long` 之后总是忘记将 `int main()` 的 `int` 改为 `signed`。  
思路：使 sum1, sum3 尽量的大，那么就是选择两区间 [1, a]，[b, n]，使得区间一的和等于区间二的和且尽量的大，我们可以用指针 l, r 分别指向 1, n，然后向中间移动（因为要使它们相等，所以当 [1, l] 的和 < [r, n] 的和时，那么就移动左指针，否则移动右指针），若它们相等则取 max。  
代码：
```
#include <bits/stdc++.h>
using namespace std;
#define int long long // 记得 signed main()
const int N = 200005;
int n, a[N];
signed main()
{
    scanf("%lld", &n);
    for (int i = 1; i <= n;) scanf("%lld", a + i++);
    int l = 1, r = n, res = 0, s1 = 0, s2 = 0;
    while (l < r)
    {
        s1 += a[l]; // 求 [1, l] 的和
        s2 += a[r]; // 求 [r, n] 的和
        a[l] = a[r] = 0; // 避免重复计算
        if (s1 == s2) res = max(res, s1); // 取 max
        if (s1 > s2) --r;
        else ++l; // 移动指针
    }
    printf("%lld\n", res);
}
```
  
- #### T3:
二分图的最大匹配。  
若存在一对 i, j 使得 |a[i] - b[j]| <= 1，那么就在 i, j 之间连一条无向边。  
最后求二分图的最大匹配不就得了。  
代码：  
```
#include <bits/stdc++.h>
using namespace std;
const int N = 10005;
bool vis[N]; int m[N];
int a[N], b[N];
int idx, h[N], e[N], ne[N];
void add(int x, int y)
{
    e[++idx] = y, ne[idx] = h[x], h[x] = idx;
}
bool find(int x) 
{
	for (int i = h[x]; i; i = ne[i]) 
		if (!vis[e[i]]) 
		{
			vis[e[i]] = 1;
			if (!m[e[i]] || find(m[e[i]])) 
			{
				m[e[i]] = x;
				return 1;
			}	
		}
	return 0;
}
int main() 
{
	int n1, n2, res = 0;
	scanf("%d", &n1);
	for (int i = 1; i <= n1;) scanf("%d", a + i++);
	scanf("%d", &n2);
	for (int i = 1; i <= n2;) scanf("%d", b + i++);
	for (int i = 1; i <= n1; i++)
	    for (int j = 1; j <= n2; j++)
	        if (abs(a[i] - b[j]) <= 1) add(i, j);
	for (int i = 1; i <= n1; i ++) 
	{
		memset (vis, 0, sizeof vis);
		res += find(i);
	}
	printf ("%d\n", res);
	return 0;
}
```