```
T1:

#include <bits/stdc++.h>
using namespace std;
const int N = 100005;
struct Node
{
    int nxid;
    char c;
} a[N];
int h1, t1, h2, t2, n;
bool vis[N];
void print(int n, int k)
{
    if (!k) return;
    int w = pow(10, k - 1);
    if (n >= k) printf("%d", n / w);
    else printf("0");
    print(n % w, k - 1);
}
int main()
{
    scanf("%d %d %d\n", &h1, &h2, &n);
    if (h1 == -1 || h2 == -1) return puts("-1"), 0;
    for (int i = 1; i <= n; i++)
    {
        int id;
        scanf("%d ", &id);
        scanf("%c %d\n", &a[id].c, &a[id].nxid);
    }
    int t1 = h1;
    while (1)
    {
        vis[t1] = 1, t1 = a[t1].nxid;
        if (a[t1].nxid == -1)
        {
            vis[t1] = 1;
            break;
        }
    }
    int t2 = h2;
    while (1)
    {
        if (vis[t2])
            return print(t2, 5), 0;
        t2 = a[t2].nxid;
        if (a[t2].nxid == -1) break;
    }
    puts("-1");
}
```
```
T2:

#include <bits/stdc++.h>
using namespace std;
const int N = 100005;
struct Node
{
    int nxid;
    int v;
} a[N];
int h, t, n, k;
int q[N];
int w, r[N];
void print(int n, int k)
{
    if (!k) return;
    int w = pow(10, k - 1);
    if (n >= k) printf("%d", n / w);
    else printf("0");
    print(n % w, k - 1);
}
int main()
{
    scanf("%d%d%d", &h, &n, &k);
    for (int i = 1; i <= n; i++)
    {
        int id;
        scanf("%d", &id);
        scanf("%d%d", &a[id].v, &a[id].nxid);
    }
    t = h;
    int m = 0;
    while (1)
    {
        q[++m] = t;
        if (m == k) 
        {
            for (int i = m; i; i--) r[++w] = q[i];
            m = 0; 
        }
        t = a[t].nxid;
        if (t == -1) break;
    }
    for (int i = 1; i <= m; i++) r[++w] = q[i];
    r[++w] = -1;
    for (int i = 1; i < w; i++)
    {
        print(r[i], 5);   
        printf(" %d ", a[r[i]].v);
        if (r[i + 1] != -1) print(r[i + 1], 5);
        else printf("-1");
        puts("");
    }
    return 0;
}
```
```
T3:

#include <bits/stdc++.h>
using namespace std;
const int N = 100005;
struct Node
{
    int nxid;
    int v;
} a[N], r1[N], r2[N];
int k1, k2;
int h, t, n;
int w, r[N];
bool vis[N];
void print(int n, int k)
{
    if (!k) return;
    int w = pow(10, k - 1);
    if (n >= k) printf("%d", n / w);
    else printf("0");
    print(n % w, k - 1);
}
int main()
{
    scanf("%d%d", &h, &n);
    for (int i = 1; i <= n; i++)
    {
        int id;
        scanf("%d", &id);
        scanf("%d%d", &a[id].v, &a[id].nxid);
    }
    t = h;
    while (1)
    {
        r[++w] = t;
        t = a[t].nxid;
        if (t == -1) break;
    }
    for (int i = 1; i <= w; i++)
    {
        if (!vis[abs(a[r[i]].v)])
        {
            vis[abs(a[r[i]].v)] = 1;
            r1[k1].nxid = r[i];
            r1[++k1].v = a[r[i]].v;
            r1[k1].nxid = -1;
        }
        else 
        {
            r2[k2].nxid = r[i];
            r2[++k2].v = a[r[i]].v;
            r2[k2].nxid = -1;
        }
    }
    for (int i = 1; i <= k1; i++)
    {
        print(r1[i - 1].nxid, 5);
        printf(" %d ", r1[i].v);
        if (r1[i].nxid != -1) print(r1[i].nxid, 5);
        else printf("-1");
        puts("");
    }
    for (int i = 1; i <= k2; i++)
    {
        print(r2[i - 1].nxid, 5);
        printf(" %d ", r2[i].v);
        if (r2[i].nxid != -1) print(r2[i].nxid, 5);
        else printf("-1");
        puts("");
    }
    return 0;
}
```
```
T4: 

#include <bits/stdc++.h>
using namespace std;
const int N = 100005;
struct Node
{
    int nxid;
    int v;
} a[N], r1[N], r2[N], r3[N];
int k1, k2, k3;
int h, t, n, k;
int w, r[N];
void print(int n, int k)
{
    if (!k) return;
    int w = pow(10, k - 1);
    if (n >= k) printf("%d", n / w);
    else printf("0");
    print(n % w, k - 1);
}
int main()
{
    scanf("%d%d%d", &h, &n, &k);
    for (int i = 1; i <= n; i++)
    {
        int id;
        scanf("%d", &id);
        scanf("%d%d", &a[id].v, &a[id].nxid);
    }
    t = h;
    while (1)
    {
        r[++w] = t;
        t = a[t].nxid;
        if (t == -1) break;
    }
    r2[0].nxid = r3[0].nxid = -1;
    for (int i = 1; i <= w; i++)
    {
        if (a[r[i]].v < 0)
        {
            r1[k1].nxid = r[i];
            r1[++k1].v = a[r[i]].v;
            r1[k1].nxid = -1;
        }
        else if (a[r[i]].v <= k)
        {
            r2[k2].nxid = r[i];
            r2[++k2].v = a[r[i]].v;
            r2[k2].nxid = -1;
        }
        else 
        {
            r3[k3].nxid = r[i];
            r3[++k3].v = a[r[i]].v;
            r3[k3].nxid = -1;
        }
    }
    r1[k1].nxid = r2[0].nxid;
    r2[k2].nxid = r3[0].nxid;
    for (int i = 1; i <= k1; i++)
    {
        print(r1[i - 1].nxid, 5);
        printf(" %d ", r1[i].v);
        if (r1[i].nxid != -1) print(r1[i].nxid, 5);
        else printf("-1");
        puts("");
    }
    for (int i = 1; i <= k2; i++)
    {
        print(r2[i - 1].nxid, 5);
        printf(" %d ", r2[i].v);
        if (r2[i].nxid != -1) print(r2[i].nxid, 5);
        else printf("-1");
        puts("");
    }
    for (int i = 1; i <= k3; i++)
    {
        print(r3[i - 1].nxid, 5);
        printf(" %d ", r3[i].v);
        if (r3[i].nxid != -1) print(r3[i].nxid, 5);
        else printf("-1");
        puts("");
    }
    return 0;
}
```