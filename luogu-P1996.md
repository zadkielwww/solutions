[题目链接](https://www.luogu.com.cn/problem/P1996)  
做这道题目主要是练习一下指针。  
- 做法1：双向链  
  
首先，建立双向链 List，使头指针 List -> head 的权值 val = 1，尾指针 List -> tail -> val = n，并将其相连成环，即  
```
head -> nxt = tail; head -> pre = tail;
tail -> nxt = head; tail -> pre = head;
```
其次，使节点 p(List*) = head，并开始在 (head,tail) 之间建立一个 val = (1,n) 的链表。  
每次新创建一个节点 q，使 q 与 p 和 tail 首尾相接，建立后使得 p = q，即在除 tail 外的最后一个节点与 tail 之间继续开点，代码：  
```
for (int i = 2; i < n; i++)
{
    Node *q = new Node;
    q -> val = i;
    q -> pre = p;
    q -> nxt = p -> nxt;
    p -> nxt -> pre = q;
    p -> nxt = q;
    p = p -> nxt;
}
```
那么后面的就模拟约瑟夫的出圈过程，每次使节点向后走 m-1 步（因为自己要先报 1)，走完后删除该节点，接着跳到被删除节点的下一个节点（因为这个节点要报 1），与此同时输出即可。  
双向链的代码：  
```
#include <bits/stdc++.h>
using namespace std;
struct Node
{
    int val;
    Node *pre, *nxt; // 前驱，后继
} *head, *tail, *p;
int m, n;
void build(int s)
{
    head = new Node;
    tail = new Node; 
    head -> nxt = tail; head -> pre = tail;
    tail -> nxt = head; tail -> pre = head;
    head -> val = 1; tail -> val = n; 
    p = head;
    for (int i = 2; i < n; i++)
    {
        Node *q = new Node;
        q -> val = i;
        q -> pre = p;
        q -> nxt = p -> nxt;
        p -> nxt -> pre = q;
        p -> nxt = q;
        p = p -> nxt;
    }
}
Node* getnext(Node *p) // 求节点 p 走 m-1 步后到达的点
{
    for (int i = 1; i < m; i++)
        p = p -> nxt;
    return p;
}
void print()
{
    for (int i = 1; i <= n; i++)
    {
        p = getnext(p);
        printf("%d ", p -> val);
        p -> pre -> nxt = p -> nxt;
        p -> nxt -> pre = p -> pre; // delete p
        p = p -> nxt;
    }
}
int main()
{
    scanf("%d%d", &n, &m);
    build(n), p = head; // 因为 p 指向的已经不是 head，所以要再赋值一次
    print();
    return 0;
}
```
- 做法2：单向链  
  
基本思路同上，但由于单向链更为简洁，所以在细节处理上单向链更加的麻烦。  
首先是建立 head, tail 的过程，因为不存储前驱节点，所以建立的时候只需要将 head -> nxt 指向 tail，将 tail -> nxt 指向 head，代码：  
```
head -> nxt = tail;
tail -> nxt = head;
```  
其次是开点过程，这里也是直接把前驱部分删除即可。  
```
for (int i = 2; i < n; i++)
{
    Node *q = new Node;
    q -> val = i;
    q -> nxt = p -> nxt;
    p -> nxt = q;
    p = q;
}
```
但在删除的过程中，我们由于没有前驱节点，所以不能用双向链中的方法删点。  
所以我们可以只走 m-2 步，然后在 m-2 的点上将 m-1 的点用 `p -> nxt = p -> nxt -> nxt;` 删除掉。  
综上所述，单向链的代码：  
```
#include <bits/stdc++.h>
using namespace std;
struct Node
{
    int val;
    Node *nxt;// 只需要记录后继节点即可
} *head, *tail, *p;
int m, n;
void build(int s)
{
    head = new Node;
    tail = new Node; 
    head -> nxt = tail;
    tail -> nxt = head;
    head -> val = 1; tail -> val = n; 
    p = head;
    for (int i = 2; i < n; i++)
    {
        Node *q = new Node;
        q -> val = i;
        q -> nxt = p -> nxt;
        p -> nxt = q;
        p = q;
    }
}
Node* getnext(Node *p)
{
    for (int i = 2; i < m; i++) // 只走 m-2 步
        p = p -> nxt;
    return p;
}
void print()
{
    for (int i = 1; i <= n; i++)
    {
        p = getnext(p);
        printf("%d ", p -> nxt -> val);
        p -> nxt = p -> nxt -> nxt; // 单向链将 p 点的后继节点删除，只需要将它的后继指针指到原后继点的后继节点即可。
        p = p -> nxt;
    }
}
int main()
{
    scanf("%d%d", &n, &m);
    build(n), p = head;
    print();
    return 0;
}
```