struct 结构体类型名

{

     成员表；

     成员函数；

}结构体变量表；

交换swap (a[j],a[j+1]);

输入cin >>a[i],name;

 赋值student op = { "zhangsan", 89, 90, 179};

一般形式：

          结构体变量名.成员名；

 cin >> a[i].name;

a[i].total =  a[i].chinese+a[i].math;

struct 结构体类型名

{

       成员表；

       成员函数；

}结构体指针变量表；

or struct 结构体类型名{};

结构体名 结构体指针变量表；



赋值是把结构体变量的首地址赋予该指针变量，不能把结构体名赋予该指针变量。

1.指针名-> 成员名

2.（*指针名）.成员名

（*stu1）.chinese == stu1->chinese

struct stu{

stu p;

}//不合法，大小不确定，相当于无限自循环；

struct stu{

stu*p

}//合法，地址的大小由系统产生，编译前就已经知道，所以合法

顺序存储结构：数组

存取方便、容量难扩充、插入删除元素麻烦

链式存储结构：链表

资源重复利用，可随时修改、利用。需要分配内存前驱和后驱位置（地址）




Node（结点）

---->数据域|指针域------>数据域|指针域----->数据域|指针域

尾结点：指针域为NULL

头结点（head）：不存储数据；

例：struct Node{

     int data；//数据域

     Node *next； //指针域

}；

Node *p；//结构体变量表

p = new Node；//p初始化

  -----------------------------------------------------------

链表创建流程：head 连一个r，p拉来一个x|NULL，然后r->next = p或者head->next = p;把head连到p上，然后p断开去拉下一个x|NULL。

#include<bits/stdc++.h>

using namespace std;

struct Node{

int data;

Node *next;

};

Node *head, *p, *r;//设置*head ， *p ， *r中都有Node 表的data和 *next 元素；

int x;

int main(){

 cin >> x;

head = new Node;//初始化

r = head;

while(x!=-1){

p = new Node;//初始化

p->data = x;//p的数据域存储x

p->next = NUll;

r->next = p;//把新结点链接到前面的链表里

r=p;//让r往后移到下一个结点

cin >> x;

}

p = head->next;

while(p!->next =NULL){

cout<< p->data<< " ";

p = p->next;

}

cout<< p->data<<endl;

int i=0;

while(p->next != NULL;){

 if(p->data==3){

i++;

}

p=p->next;

}

cout<< "其中数据为3的个数有"<<i<<"个"<<endl;

return 0;

}

输入1234 -1

输出 1234

        链表不适合需要大量访问的问题

插入：c的结点链接到b上，a链接到c上，ab断开就行了

s->next = p->next;//c连b

p->next = s;//a连c

删除：a连c，ab断开

s = p->next;//b给s

p->next = p->next->next;//让连接p->next（b的位置）连接到p->next->next（c的位置）

Free(s);//解放s即解放b



del(head,2);//删除head开始的第二个结点

约瑟夫环：即每次第i个的数被删除，每次删除，把其他数往前移i位即可

#include<bits/stdc++.h>

using namespeace std;

struct node{

 long d;

node *next;

};

long n,m;

node *head.*p,*r;

int main(){

  long i;

  cin>> n>> m;

 head  = new node;

head->d = 1;

head->next = NULL;

r = head;

for(i = 2;i <= n;i++){

 p = new node;

 p->d = i;

p->next = NULL;

r->next = p;

r = p;

}

r->next = head;

r = head;

for(i = 1; i <= n;i++){

   for(j = 1; j<= m-2; j++){

         r = r->next;

}

cout<< r->next->d<<" ";

r->next = r->next->next;;

r = r->next;

}

return 0;

}

