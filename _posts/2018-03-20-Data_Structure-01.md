---
layout: post
title: 数据结构复习之校赛篇
tags: 知识整理
---

### 数据结构的基本框架:
> *  线性结构:列表,链表,队列,栈
> * 树形结构: 二叉树,二叉搜索树,平衡二叉树,(B树竞赛的话还是算了,学习还是有必要的)
> * 图形结构: 矩阵,邻接表(竞赛推荐前向星存图),DFS,BFS,最短路,最小生成树,拓扑排序...
> * 排序: 插入,冒泡,选择,希尔,归并,堆排,快排
> * Ps : 这里简单写一下我在准备校赛时用到的.


### 线性结构:

 > STL 中的stack,queue实现栈和队列,链表可以自己手动实现.

### 树形结构:

 需要解决的问题:

        1.二叉树的搜索,前序(根左右),中序(左根右),后序(左右根),层次(借助队列实现)

        2.树的叶子数量,树的深度.二叉树与树,森林之间转换,

        3.前序中序求后序,中序后序求前序,

        4.平衡二叉树.


###  图形结构:

 需要解决的问题:

     1. 存图问题: 矩阵(二维数组),邻接表(前向星)

     2. 图的遍历: DFS,BFS

     3. 最短路问题: Dijikstra, spfa,Floyd算法

     4. 最小生成树MST,prim算法,克鲁斯卡尔算法

     5. 拓扑排序,还有一个??? (忘记了)

 > 推荐博客:[传送门](http://www.cnblogs.com/Yan-C/)




### 我写的模板:(没有注释(⊙o⊙)哦)

#### 平衡二叉树模板:

 ```
 #include <bits/stdc++.http://acm.sdut.edu.cn/onlinejudge2/index.php/Home/Index/problemdetail/pid/2144.htmlh>
using namespace std;
typedef struct node
{
     int data;
     int depth;
     node *lc,*rc;
}Tree,*Btree;
int Deep(Btree &t)
{
    if (t==NULL)
        return 0;
    else
    return t->depth;
}
Btree ll(Btree &t)
{
    Btree p;
    p=t->lc;
    t->lc=p->rc;
    p->rc =t;
    t->depth=max(Deep(t->lc),Deep(t->rc))+1;
    p->depth=max(Deep(p->lc),t->depth)+1;
    return p;
}
Btree rr(Btree &t)
{
    Btree p;
    p=t->rc;
    t->rc=p->lc;
    p->lc=t;
    t->depth=max(Deep(t->lc),Deep(t->rc))+1;
    p->depth=max(Deep(p->rc),t->depth)+1;
    return p;

}
Btree lr(Btree &t)
{
    t->lc=rr(t->lc);
    return ll(t);
}

Btree rl(Btree &t)
{
    t->rc=ll(t->rc);
    return rr(t);

}
Btree  Creat_tree(Btree &t,int &x)
{
    if (t==NULL)
    {
        t=new node ;
        t->data =x;
        t->depth=0;
        t->lc=t->rc=NULL;
    }
    else if (t->data>x) //left
    {
       t->lc=Creat_tree(t->lc,x);
       if (Deep(t->lc)-Deep(t->rc)==2)
       {
           if (t->lc->data>x)
            t=ll(t);
           else
            t=lr(t);
       }
    }
    else {
        t->rc = Creat_tree(t->rc,x);
        if (Deep(t->rc)-Deep(t->lc)==2)
        {
            if (t->rc->data<x)
              t=rr(t);
            else
              t=rl(t);
        }
    }
    t->depth=max(Deep(t->lc),Deep(t->rc))+1;
    return t;
}

int main ()
{
    int n;
    cin>>n;
    Btree t=NULL;
    while (n--)
    {
        int x;
        cin>>x;
        t=Creat_tree(t,x);
    }
    cout<<t->data<<endl;

    return 0;
}
 ```
#### 推荐题目：  [最短路](http://acm.sdut.edu.cn/onlinejudge2/index.php/Home/Index/problemdetail/pid/2143.html)  [最小生成树](http://acm.sdut.edu.cn/onlinejudge2/index.php/Home/Index/problemdetail/pid/2144.html) ：

 --- ---
#### 所需要的一点东西：
 Ps ：head[]数组初始化在主函数中
 ```
 #include <bits/stdc++.h>
 using namespace std;
 const int maxn =1e6+5; //数组的最大内存
 const int INF =0x3f3f3f; //定义的无限大
 bool vis[maxn]; //标记数组，prim，spfa算法用
 typedef pair <int ,int >qq; //定义的二元组 （dist[],pos）,frist是对应的dist[]值，pos表示位置
 int head[maxn]; //存储图的边的信息
 struct node  //存储图的信息
 {
     int to,next,data;
 }e[maxn];
 int dist[maxn];//最短距离
 int cnt ; //存储图
 int n,m;//节点n，边数m
 int num[maxn];//判断负环 spfa算法
 void add (int x,int y,int z) //添加边
 {
     e[cnt].to=y;
     e[cnt].data=z;
     e[cnt].next=head[x];
     head[x]=cnt++;
 }
 ```

####  Dijkstra算法：

 ```
 void Dijkstra(int st)
 {
     fill(dist,dist+n+1,INF);
     priority_queue<qq,vector<qq>,greater<qq> >q;
     q.push(qq(0,st));
     int i,j,k;
     dist[st]=0;
     while (!q.empty())
     {
         qq p=q.top();
         q.pop();
         int u =p.second;
         if (dist[u]<p.first)
             continue ;
         for (i=head[u];i!=-1;i=e[i].next)
         {
             node ee =e[i];
             if (dist[ee.to]>ee.data+dist[u])
             {
                 dist[ee.to]=ee.data+dist[u];
                 q.push(qq(dist[ee.to],ee.to));
             }
         }
     }
 }
 ```

#### Spfa算法：

 ```
 bool yes;    //判断负环
 void spfa(int st)
 {
     fill(vis,vis+n+1,0);
     fill(dist,dist+n+1,INF);
     queue<int >q;
     q.push(st);
     dist[st]=0;
     vis[st]=1;
     int i,j,k;
     yes =0;
     while (!q.empty())
     {
         int u=q.front();
         q.pop();
         vis[u]=0;
         for (i=head[u];i!=-1;i=e[i].next)
         {
             node ee =e[i];
             if (dist[ee.to]>dist[u]+ee.data)
             {
                 dist[ee.to]=dist[u]+ee.data;
                 if (!vis[ee.to])
                 {
                     vis[ee.to]=1;
                     num[ee.to]++;
                     if (num[ee.to]>n)
                        {
                            yes = 1 ;
                          return ;
                        }
                        q.push(ee.to);
                 }
             }
         }
     }

 }
 ```

#### Prim 算法，最小生成树：
 ```
 void prim(int st)
 {
     int i,j,k;
     fill(vis,vis+n+1,0);
     fill(dist,dist+n+1,INF);
     int ans =0;
      priority_queue<qq,vector<qq>,greater<qq> >q;
      q.push(qq(0,st));
      dist[st]=0;
      while (!q.empty())
      {
          qq p=q.top();
          q.pop();
          int u=p.second;
          if (vis[u])
             continue ;
          vis[u]=1;
          ans+=dist[u];
          for (i=head[u];i!=-1;i=e[i].next)
          {
              node ee =e[i];
              if (dist[ee.to]>ee.data)
              {
                  dist[ee.to]=ee.data;
                 q.push(qq(ee.data,ee.to));

              }
          }

      }
      cout<<ans<<endl;
 }
 ```

#### Dijikstra,spfa,prim 算法模板:

```
#include <bits/stdc++.h>
using namespace std;
const int maxn =1e6+5;
const int INF =0x3f3f3f;
bool vis[maxn];
typedef pair <int ,int >qq;
int head[maxn];
struct node
{
    int to,next,data;
}e[maxn];
int dist[maxn];
int cnt ;
int n,m;
int num[maxn];
void add (int x,int y,int z)
{
    e[cnt].to=y;
    e[cnt].data=z;
    e[cnt].next=head[x];
    head[x]=cnt++;
}
void Dijkstra(int st)
{
    fill(dist,dist+n+1,INF);
    priority_queue<qq,vector<qq>,greater<qq> >q;
    q.push(qq(0,st));
    int i,j,k;
    dist[st]=0;
    while (!q.empty())
    {
        qq p=q.top();
        q.pop();
        int u =p.second;
        if (dist[u]<p.first)
            continue ;
        for (i=head[u];i!=-1;i=e[i].next)
        {
            node ee =e[i];
            if (dist[ee.to]>ee.data+dist[u])
            {
                dist[ee.to]=ee.data+dist[u];
                q.push(qq(dist[ee.to],ee.to));
            }
        }
    }
}
bool yes;    //判断负环
void spfa(int st)
{
    fill(vis,vis+n+1,0);
    fill(dist,dist+n+1,INF);
    queue<int >q;
    q.push(st);
    dist[st]=0;
    vis[st]=1;
    int i,j,k;
    yes =0;
    while (!q.empty())
    {
        int u=q.front();
        q.pop();
        vis[u]=0;
        for (i=head[u];i!=-1;i=e[i].next)
        {
            node ee =e[i];
            if (dist[ee.to]>dist[u]+ee.data)
            {
                dist[ee.to]=dist[u]+ee.data;
                if (!vis[ee.to])
                {
                    vis[ee.to]=1;
                    num[ee.to]++;
                    if (num[ee.to]>n)
                       {
                           yes = 1 ;
                         return ;
                       }
                       q.push(ee.to);
                }
            }
        }
    }

}
void prim(int st)
{
    int i,j,k;
    fill(vis,vis+n+1,0);
    fill(dist,dist+n+1,INF);
    int ans =0;
     priority_queue<qq,vector<qq>,greater<qq> >q;
     q.push(qq(0,st));
     dist[st]=0;
     while (!q.empty())
     {
         qq p=q.top();
         q.pop();
         int u=p.second;
         if (vis[u])
            continue ;
         vis[u]=1;
         ans+=dist[u];
         for (i=head[u];i!=-1;i=e[i].next)
         {
             node ee =e[i];
             if (dist[ee.to]>ee.data)
             {
                 dist[ee.to]=ee.data;
                q.push(qq(ee.data,ee.to));

             }
         }

     }
     cout<<ans<<endl;
}
int main()
{
    while (cin>>n>>m)
    {
         int i,j,k;
         cnt=0;
         fill(head,head+maxn+1,-1);
         while(m--)
         {
             int x,y,z;
             cin>>x>>y>>z;
             add(x,y,z);
             add(y,x,z);
         }
//          Dijkstra(1);
         spfa(1);
          cout<<dist[n]<<endl;
    }
    return 0;
}

```

### 注意:
以上内容，作者一字一句码出来的，纯属不易，欢迎大家转载，转载是还请您表明出处。另外如果我有侵权行为，请在下方留言，确认后我会及时撤销相应内容，谢谢大家！

PS:欢迎大家来到我的小站,和我一起记录属于我们自己的大学！
