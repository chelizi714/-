单链表：

最大用处：邻接表----存储图和树

双链表：

最大用处：优化某些问题



单链表-----



<img src="C:\Users\Lenovo\Desktop\c++课程笔记\算法基础课\单链表\1.png" style="zoom:40%;" />

e[n]是存放的值，ne[n]是下一个位置的下标

例题：

实现一个单链表，链表初始为空，支持三种操作：

1. 向链表头插入一个数；
2. 删除第 k� 个插入的数后面的一个数；
3. 在第 k� 个插入的数后插入一个数。

现在要对该链表进行 M� 次操作，进行完所有操作后，从头到尾输出整个链表。

**注意**:题目中第 k� 个插入的数并不是指当前链表的第 k� 个数。例如操作过程中一共插入了 n� 个数，则按照插入的时间顺序，这 n� 个数依次为：第 11 个插入的数，第 22 个插入的数，…第 n� 个插入的数。

```
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
//head表示头节点的下标
//e[i]表示下标i的值
//ne[i]表示节点i的next指针是多少
//idx用于存储当前已经用到了哪个点
int head,e[N],ne[N],idx;

//初始化
void init()		
{
    head = -1;
    idx = 1;	
}

//将x插到头节点
void add_to_head(int x)
{
    e[idx] = x;
    ne[idx] = head;
    head = idx;
    idx ++;
}

//将x插到k的位置
void add(int k,int x)
{
    e[idx] = x;
    ne[idx] = ne[k];
    ne[k] = idx;
    idx ++;
}

//将下标是k的点后面的点删掉
void remove(int k)
{
    ne[k] = ne[ne[k]];
}




int main()
{
    int m;
    cin >> m;
    init();
    while (m --)
    {
        int k,x;
        char op;
        cin >> op;
        if (op == 'H')
        {
            cin >> x;
            add_to_head(x);
        }
        else if (op == 'D')
        {
            cin >> k;
            if (!k) head = ne[head];
            else remove(k);
        }
        else
        {
            cin >> k >> x;
            add(k,x);
        }
    }
    for (int i=head;i != -1;i = ne[i]) cout << e[i] << " ";
    return 0;
}
```





双链表----

两个指针，一个指向前，一个指向后

图中为插入的第k位置

<img src="C:\Users\Lenovo\Desktop\c++课程笔记\算法基础课\单链表\2.png" style="zoom: 50%;" />

图中为删除第k个位置

<img src="C:\Users\Lenovo\Desktop\c++课程笔记\算法基础课\单链表\3.png" style="zoom: 50%;" />

```
#include<iostream>
#include<string>
using namespace std;
const int N=1e5+10;
int e[N],r[N],l[N],idx;
//e[i]表示下标为i的值
//r[i]表示下标为i的下一个节点的索引
//l[i]表示下标为i的上一个节点的索引
//idx用于存储当前已经用到了哪个点
void chushihua() //初始化，0的右边是1，1的左边是0
{
    r[0]=1;
    l[1]=0;
    idx=2;
}
void charu(int k,int x)  //插入第k个位置，如果要在k的左边那个点插入，则可以用charu(l[k],x)来简写
{
    e[idx]=x;
    r[idx]=r[k];
    l[idx]=k;
    l[r[k]]=idx;
    r[k]=idx++;
}
void remove(int k)		//删除第k个位置
{
    r[l[k]]=r[k];
    l[r[k]]=l[k];
}

int main()
{
    int m;
    cin>>m;
    chushihua();
    while(m--)
    {
        string s;
        int k,x;
        cin>>s;
        if(s=="R")
        {
            cin>>x;
            charu(l[1],x);
        }
        else if(s=="L")
        {
            cin>>x;
            charu(0,x);
        }
        else if(s=="IL"){
            cin>>k>>x;
            charu(l[k+1],x);
        }
        else if(s=="D")
        {
            cin>>k;
            remove(k+1);
        }
        else
        {
            cin>>k>>x;
            charu(k+1,x);
        }
    }
    for(int i=r[0];i!=1;i=r[i])cout<<e[i]<<' ';
    cout<<endl;
}
```

