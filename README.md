# 数据结构

这是阅读王道、天勤等数据结构考研的复习笔记。

[TOC]



------



# 第一章 绪论

重点部分：

- 算法时间复杂度、空间复杂度的分析与计算

提示：

​	算法设计中通常会要求分析时间复杂度、空间复杂度，同时也会出现考察时间复杂度的选择题。



## 1.1 数据结构的基本概念

### 1.1.1 基本概念和术语

 1.  数据

     数据是信息的载体。

 2.  数据元素

     数据元素是数据的基本单位。

 3.  数据对象

     数据对象是具有相同性质的数据元素的集合，是数据的一个子集。

 4.  数据类型

     数据类型是一个值的集合和定义在此集合上的一组操作的总称。

 5.  数据结构

     数据结构包括：逻辑结构、存储结构和数据运算。

     

### 1.1.2 数据结构三要素

 1.  数据的逻辑结构

     逻辑结构与存储无关，是独立于计算机的。下面展示的是逻辑结构的分类：

     ![image-20230924152505191](./assets/image-20230924152505191.png)

 2.  数据的存储结构

     存储结构是指数据在计算机中的表示，也称为物理结构。

     1. 顺序存储
     2. 链式存储
     3. 索引存储
     4. 散列存储

     

 3.  数据的运算



## 1.2 算法和算法评价

### 1.2.1 算法的基本概念



### 1.2.2 算法效率的度量

 1.  时间复杂度

     时间复杂度的求解一般关注最坏情况下的时间复杂度。

     对于循环体，有：

     ​	时间复杂度取决于最大的那个循环最内层执行次数。

     对于递归，有：

     ​	先推导出类似$T(n)=aT(\frac{n}{b})+f(n)$形式的递推式（其中$f(n)$为一个确定的正函数）。

     ​	然后有
     $$
     T(n)=
     \left\{\begin{matrix} 
     	O(n^{log_{b}a}),\space \space O(n^{log_{b}a}) > O(f(n)) \\ 
     	O(f(n)log_{}n), \space \space O(n^{log_{b}a}) = O(f(n)) \\ 
     	O(f(n)),\space \space O(n^{log_{b}a}) < O(f(n)) 
     \end{matrix}\right.
     $$

 2.  空间复杂度

     空间复杂度有时也会关注平均/最好情况下的空间复杂度。





------



# 第二章 线性表

重点部分：

- 线性表的基本概念
- 线性表的实现：顺序存储、链式存储
- 线性表的应用

提示：线性表是算法题命题的重点，主要着重在性能优化（时间、空间复杂度）上。



## 2.1 线性表的定义和基本操作

### 2.1.1 线性表的定义

​	线性表是具有相同数据类型的 $n\ \ (n\ge0)$ 个元素的有限序列。



### 2.1.2 线性表的基本操作

​	线性表的主要操作如下：

```c++
InitList(&L)，初始化表。

Length(&L)，求表长，返回L的长度。

LocateElem(L, e)，按值查找，查找表中值为e的元素。

GetElem(L, i)，按位查找，获取第i个元素的值。

ListInsert(&L, i, e)，插入操作，在第i个位置上插入e。

ListDelete(&L, i, &e)，删除操作，删除第i个位置的元素，并用e返回删除元素的值。

PrintList(L)，输出L。

Empty(L)，判定L是否为空。

DestroyList(&L)，销毁线性表。
```



## 2.2 线性表的顺序表示

### 2.2.1 顺序表的定义

​	线性表的顺序存储称为<u>顺序表</u>，顺序表的特点是表中元素的逻辑顺序与物理顺序相同。

​	顺序表的存储类型可以描述为：

```C++
#define MaxSize 50
typedef struct{
    ElemType data[MaxSize];
    int length;
}SqList;	//静态分配
```

```C++
#define InitSize 100
typedef struct{
    ElemType *data;
    int MaxSize, length;
}SqList;	//动态分配

L.data = (ElemType*)malloc(sizeof(ElemType)*InitSize);	//For C
L.data = new ElemType[InitSize];						//For C++
```

​	假设线性表 $L$ 纯初的起始位置是 LOC(A)，sizeof(ElemType) 是每个数据元素所占用存储空间的大小，则L对应的顺序存储如图所示：

![image-20230924162218937](./assets/image-20230924162218937.png)

​	

### 2.2.2 顺序表上基本操作的实现

​	由于其他操作都比较简单，这里只讨论插入、删除、查找的算法。

 1.  插入

     ```C++
     bool ListInsert(SqList &L, int i, ElemType e)
     {
         if (i < 1 || i > L.Length + 1)			//判断i范围是否有效
             return false;
         if (L.Length >= MaxSize)				//当前已满
             return false;
         for (int j = L.Length > j >= i; j--)	//元素后移
             L.data[j] = L.data[j - 1];
         L.data[i - 1] = e;						//放入i
         L.Length++;								//长度+1
         return true;
     }
     ```

     ​	平均情况：假设 $p_i=\frac{1}{n+1}$ 是在第 $i$ 个位置上插入一个结点的概率，则平均移动次数为
     $$
     \scriptsize \sum_{i=1}^{n+1}{p_i(n-i+1)}  = \sum_{i=1}^{n+1}{\frac{1}{n+1}(n-i+1)}  =
     \frac{1}{n+1} \sum_{i=1}^{n+1}{(n-i+1)}  = 
     \frac{1}{n+1} \frac{n(n+1)}{2} 
     = \frac{n}{2}
     $$
     ​	故平均时间复杂度为 $O(n)$。

     

 2.  删除

     ```C++
     bool ListDelete(SqList &L, int i, ElemType e)
     {
         if (i < 1 || i > L.Length)          //判断范围是否有效
             return false;
         e = L.data[i - 1];                  //把被删除的元素给e
         for (int j = i; j < L.Length; j++)  //元素前移
             L.data[j - 1] = L.data[j];      
         L.Length--;                         //长度-1
         return true;
     }
     ```

     ​	平均情况：假设假设 $p_i=\frac{1}{n}$ 是在第 $i$ 个位置上删除一个结点的概率，则平均移动次数为
     $$
     \scriptsize \sum_{i=1}^{n}{p_i(n-i)}  = \sum_{i=1}^{n}{\frac{1}{n}(n-i)}  =
     \frac{1}{n} \sum_{i=1}^{n}{(n-i)}  = 
     \frac{1}{n} \frac{n(n-1)}{2} 
     = \frac{n-1}{2}
     $$
     ​	故平均时间复杂度为 $O(n)$。

     

 3.  按值查找（顺序查找）

     ```C++
     int LocateElem(SqList L, ElemType e)
     {
         int i;
         for (i = 0; i < L.Length; i++)
             if (L.data[i] == e)
                 return i + 1;               //下表为i的元素等于e，返回位序i+1
         return 0;                           //查找失败
     }
     ```

     ​	平均情况：假设假设 $p_i=\frac{1}{n}$ 是要查找的元素在第 $i$ 个位置上的概率，则所需要的比较次数为
     $$
     \scriptsize 
     \sum_{i=1}^{n}{p_i\times i}  
     = \sum_{i=1}^{n}{\frac{1}{n} \times i}  
     = \frac{1}{n} \frac{n(n+1)}{2}  = \frac{n+1}{2}
     $$
     ​	故平均时间复杂度为 $O(n)$。
     
     

## 2.3 线性表的链式表示

顺序表可以随时存取表中的任意一个元素，但是插入和删除需要移动大量的元素。使用链式存储线性表的时候，则不需要移动元素。但是也会失去可随机存取的特性。

### 2.3.1 单链表的定义

​	线性表的链式存储又称为<u>单链表</u>，他是通过一组任意的存储单元来存储线性表中的数据元素。同时，还需要一个指向其后继的指针。

​	单链表中节点类型的描述如下：

```C++
typedef struct LNode                    // 定义节点类型
{
    ElemType data;                      // 数据域
    struct LNode *next;                 // 指针域
} LNode, *LinkList;
```

​	通常用<u>头指针</u>来标识单链表，如单链表 L，头指针为 NULL 的时候表示一个空表。此外，为了操作上的方便，在单链表第一个结点之前附加一个结点，称为头节点：

![image-20230925150051308](./assets/image-20230925150051308.png)



### 2.3.2 单链表上基本操作的实现

 1.  采用头插法建立单链表

     ​	从一个空表开始，生成新结点，并将读取到的数据插入到头结点之后，如图所示：

     ![image-20230925150327670](./assets/image-20230925150327670.png)

     ​	代码如下：

     ```C++
     LinkList List_HeadInsert(LinkList &L)   //头插法建立单链表
     {
         LNode *s;
         int x;
     
         L = (LNode *)malloc(sizeof(LNode)); //创建头节点
         L->next = NULL;                     //初始为空
     
         scanf("%d", &x);
         while (x != -1)                     //这里用-1代表结束
         {
             s = (LNode *)malloc(sizeof(LNode));
             s->data = x;
             s->next = L->next;
             L->next = s;                    //新结点插入到表中
             scanf("%d", &x);
         }
         return L;
     }
     ```

     ​	采用头插法建立单链表时，每个节点插入时间为 $O(1)$ ，长度为 $n$ 时，总时间复杂度为 $O(n)$ 。

     

 2.  采用尾插法建立单链表

     ​	头插法建立单链表的时候，生成的链表的次序是反过来的。如果希望两者次序一直，则应该采用尾插法。为此，需要增加一个尾指针 r，使其始终指向当前链表的尾结点，如图所示：

     ![image-20230925152800029](./assets/image-20230925152800029.png)

     ​	代码如下：

     ```C++
     LinkList List_TailInsert(LinkList &L)   //头插法建立单链表
     {
         int x;
         L = (LNode *)malloc(sizeof(LNode));
         LNode *s, *r = L;                   //r为表尾指针
         scanf("%d", &x);
         while (x != -1)
         {
             s = (LNode *)malloc(sizeof(LNode));
             s ->data = x;
             r -> next = s;
             r = s;                          //r指向新的表尾结点
             scanf("%d", &x);
         }
         r -> next = NULL;                   //尾指针置空
         return L;
     }
     ```

     ​	采用尾插法建立单链表时，每个节点插入时间为 $O(1)$ ，长度为 $n$ 时，总时间复杂度为 $O(n)$ 。

     

 3.  按序号查找结点

     ​	在单链表中从第一个结点出发，直到找到第i个结点为止，否则返回NULL：

     ```C++
     LNode *GetElem(LinkList L, int i)
     {
         int j = 1;                          //计数，初始为1
         LNode *p = L->next;
         if (i < 0)                          //若i无效，则返回NULL
             return NULL;
         if (i == 0)                         //如果i为0则返回头节点
             return L;
         while (p && j < i)                  //从第1个结点开始找
         {
             p = p->next;
             j++;
         }
         return p;                           //若i大于表长则返回NULL
     }
     ```

     ​	按序号查找的时间复杂度为 $O(n)$ 。

     

 4.  按值查找表结点

     ​	从单链表的第一个结点开始，从前向后一次比较表中各节点数据域的值，若某结点数据与的值等于给定值e，则返回指针，如果在整个单链表中都没有找到，则返回NULL。代码如下：

     ```C++
     LNode *LocateElem(LinkList L, ElemType e)
     {
         LNode *p = L->next;
         while (p != NULL && p->data != e)   //从第1个结点开始查找
             p = p->next;
         return p;                           //找到后返回，否则返回NULL
     }
     ```

     ​	按值查找的时间复杂度为 $O(n)$ 。

     

 5.  插入结点操作

     ​	插入结点操作将值为x的新结点插入到单链表的第i个位置上。一般是插入在i-1个结点的之后。

     ![image-20230925162810120](./assets/image-20230925162810120.png)

     ​	实现插入结点的代码片段如下：

     ```C++
     p = GetElem(L, i-1);					//查找插入位置的前一个结点
     s->next = p->next;
     p->next = s;
     ```

     ​	算法时间复杂度主要集中在查找上，故为 $O(n)$ 。

     

 6.  删除结点操作

     ​	删除结点操作时将单链表的第 i 个结点删除。

     ![image-20230925163849141](./assets/image-20230925163849141.png)

     ​	实现删除结点的代码片段如下：

     ```C++
     p = GetElem(L, i - 1);					//查找删除位置的前驱结点
     q = p->next;							
     p->next = q->next;						//领q从链表中断开，然后释放
     free(q);
     ```

     ​	算法时间复杂度主要集中在查找上，故为 $O(n)$ 。

     

 7.  求表长操作

     ​	求表长操作就是计算单链表中数据结点（不含头节点）的个数。

     ​	时间复杂度为 $O(n)$ 。

### 2.3.3 双链表

​	单链表节点中只有一个指向其后继的指针，使得单链表只能从头节点一次顺序的向后遍历。为了克服单链表的缺点缺点，引入双链表。

![image-20230925164308465](./assets/image-20230925164308465.png)

​	双链表中结点类型的描述如下：

```C++
typedef struct DNode                    //双链表
{   
    ElemType data;                      //数据域
    struct DNode *prior, *next;         //前驱后继
} DNode, *DLinkList;
```

​	双链表在查找的操作和单链表的相同，但是在插入和删除上有区别。

 1.  双链表的插入操作

     在双链表p所指的结点之后插入*s，如图所示：

     ![image-20230925164758494](./assets/image-20230925164758494.png)

     ​	插入操作的代码片段如下：

     ```C++
     s->next = p->next;
     p->next->prior = s;
     s->prior = p;
     p->next = s;
     ```

     ​	1、2步骤必须在4之前，否则*p的后继指针就会丢失。

     

 2.  双链表的删除操作

     ​	删除双链表中结点 *p 的后继节点 *q，如图所示：

     ![image-20230925165049104](./assets/image-20230925165049104.png)

     ​	删除操作的代码片段如下：

     ```C++
     p->next = q->next;
     q->next->prior = p;
     free(q);
     ```

     

### 2.3.4 循环链表

 1.  循环单链表

     ​	循环单链表和单链表的区别在于，表中最后的一个结点指向的是头节点，从而形成一个环：

     ![image-20230925165449728](./assets/image-20230925165449728.png)

     ​	在循环单链表中，判空的条件变成：

     ```C++
     L->next == L
     ```

     

 2.  循环双链表

     ​	在循环双链表中，头指针的prior指针还要指向表尾结点：

     ![image-20230925165859305](./assets/image-20230925165859305.png)

     ​	在撒谎链表中，判空的条件为：

     ```C++
     L->next == L && L->prior == L
     ```

     

### 2.3.5 静态链表

​	静态链表借助数组来描述线性表的链式存储结构，而这里的指针值得是结点的相对地址，又称游标。

![image-20230925170037922](./assets/image-20230925170037922.png)

​	静态链表结构类型描述如下：

```C++
#define MaxSize 50                      //静态链表的最大长度
typedef struct{
    ElemType data;  
    int next;                           //下一个元素的数组下标
}SLinkList[MaxSize];
```

​	静态链表用next==-1作为其结束的标志。

### 2.3.6 顺序表和链表的比较

​	



------



# 第三章 栈、队列、数组

重点部分：

- 栈和队列的基本概念、顺序存储结构、链式存储结构
- 多维数组的存储
- 特殊矩阵的压缩存储
- 栈、队列、数组的应用

提示：栈和队列的操作及其特征是重点，也容易出现在算法设计题中。



## 3.1 栈

### 3.1.1 栈的基本概念

 1.  栈的定义

     栈（Stack）是只允许在一端进行插入或者操作删除的线性表。

     ![image-20230925221534819](./assets/image-20230925221534819.png)

     

 2.  栈的基本操作

     ```C++
     InitStack(&S)，初始化一个空栈
         
     StackEmpty(S)，判断一个栈是否为空
         
     Push(&S, x)，进栈
         
     Pop(&S, &x)，出栈
         
     GetTop(S, &x)，读取栈顶元素
         
     DestroyStack(&S)，销毁并释放存储空间
         
     ```

     

 3.  卡特兰数

     $n$ 个不同元素进栈，出栈元素的不同排列个数为：
     $$
     N = \frac{1}{n+1}C_{2n}^{n}
     $$
     

### 3.1.2 栈的顺序存储结构

​	栈是一种操作受限的线性表，有两种对应的存储方式。

 1.  顺序栈的实现

     ​	顺序栈利用一组地址连续的存储单元存放自栈底到栈顶的数据元素，同时利用 top 指针指示当前栈顶元素的位置。其存储类型可以描述为：

     ```C++
     #define MaxSize 50
     typedef struct
     {
         ElemType data[MaxSize];             //存放数据元素
         int top;                            //栈顶指针
     }SqStack;
     ```

     ​	在这里，栈空条件为 S.top == -1，栈满条件为 S.top == MaxSize - 1。

     

 2.  顺序栈的基本运算

     ​	栈操作的示意图如下图所示：

     ![image-20230925222938551](./assets/image-20230925222938551.png)

     ​	下面是常用操作的实现：

      1.  初始化

          ```C++
          void InitStack(SqStack &S)
          {
              S.top = -1;                         //初始化栈顶指针
          }
          ```

          

      2.  判空

          ```C++
          bool StackEmpty(SqStack S)
          {
              if (S.top == -1)                    //栈空
                  return true;        
              else                                //非空
                  return false;
          }
          ```

          

      3.  入栈

          ```C++
          bool Push(SqStack &S, ElemType e)
          {
              if(S.top == MaxSize -1)             //栈满
                  return false;
              S.data[++S.top] = e;                //指针先+1再入栈
              return true;
          }
          ```

          

      4.  出栈

          ```C++
          bool Pop(SqStack &S, ElemType &e)
          {
              if(S.top == -1)                     //栈空
                  return false;
              e = S.data[S.top--];                //先出栈指针再-1
              return true;
          }
          ```

          

      5.  读取栈顶元素

          ```C++
          bool GetTop(SqStack S, ElemType &x)
          {
              if(S.top == -1)                     //栈空
                  return false;
              x = S.data[S.top];                  //x记录栈顶元素
              return true;
          }
          ```

          

 3.  共享栈

     ​	利用栈底位置相对不变的特性，让两个顺序栈共享一个数组空间。

     ![image-20230925224018725](./assets/image-20230925224018725.png)

     ​	top0 = -1 时0号栈为空、top1 = MaxSize 时1号栈为空；top1 - top0 = 1时栈满。	

### 3.1.3 栈的链式存储结构

​	采用链式存储的栈称为链栈，通常采用单链表实现。通常规定链栈没有头结点，Lhead指向栈顶元素。

![image-20230925224545239](./assets/image-20230925224545239.png)

```C++
typedef struct Linknode
{
    ElemType data;                      //数据域
    struct Linknode *next;              //指针域
} *LiStack;
```



## 3.2 队列

### 3.2.1 队列的基本概念



### 3.2.2 队列的顺序存储结构



### 3.2.3 队列的链式存储结构



### 3.2.4 双端队列



## 3.3 栈和队列的应用

### 3.3.1 括号匹配



### 3.3.2 表达式求值



### 3.3.3 递归



### 3.3.4  层序遍历



### 3.3.5 计算机系统中的应用



## 3.4 数组和特殊矩阵

### 3.4.1 数组的定义



### 3.4.2 数组的存储结构



### 3.4.3 特殊矩阵的压缩存储



### 3.4.4 稀疏矩阵





------



# 第四章 串



## *4.1 串的定义和实现

### 4.1.1 串的定义



### 4.1.2 串的存储结构



### 4.1.3 串的基本操作



## 4.2 串的模式匹配

### 4.2.1 简单模式匹配算法



### 4.2.2 KMP算法



### 4.2.3 KMP算法的进一步优化





------



# 第五章 树



## 5.1 树的基本概念

### 5.1.1 树的定义



### 5.1.2 基本术语



### 5.1.3 树的性质



## 5.2 二叉树的概念

### 5.2.1 二叉树的定义及其主要特性



### 5.2.2 二叉树的存储结构



## 5.3 二叉树的遍历和线索二叉树

### 5.3.1 二叉树的遍历



### 5.3.2 线索二叉树



## 5.4 树、森林

### 5.4.1 树的存储结构



### 5.4.2 树、森林、二叉树的转换



### 5.4.3 树、森林的遍历



## 5.5 树与二叉树的应用

### 5.5.1 哈夫曼树、哈夫曼编码



### 5.5.2 并查集





------



# 第六章 图



## 6.1 图的基本概念

### 6.1.1 图的定义



## 6.2 图的存储以及基本操作

### 6.2.1 邻接矩阵法



### 6.2.2 邻接表法



### 6.2.3 十字链表法



### 6.2.4 邻接多重表



### 6.2.5 图的基本操作



## 6.3 图的遍历

### 6.3.1 广度优先搜索



### 6.3.2 深度优先搜索



### 6.3.3 图的遍历、图的连通性



## 6.4 图的应用

### 6.4.1 最小生成树



### 6.4.2 最短路径



### 6.4.3 有向无环图描述表达式



### 6.4.4 拓扑排序



### 6.4.5 关键路径



------



# 第七章 查找



## 7.1 查找的基本概念



## 7.2 顺序查找和折半查找

### 7.2.1 顺序查找



### 7.2.2 折半查找



### 7.2.3 分块查找



## 7.3 树形查找

### 7.3.1 二叉排序树



### 7.3.2 平衡二叉树



### 7.3.3 红黑树



## 7.4 B树、B+树

### 7.4.1 B树及其基本操作



### 7.4.2 B+树的基本概念



## 7.5 哈希（散列）表

### 7.5.1 散列表的基本概念



### 7.5.2 散列函数的构造方法



### 7.5.3 处理冲突的方法



### 7.5.4 散列查找及其性能分析





------



# 第八章 排序



## 8.1 排序的基本概念

### 8.1.1 排序的定义



## 8.2 插入排序

### 8.2.1 直接插入排序



### 8.2.2 折半插入排序



### 8.2.3 希尔排序



## 8.3 交换排序

### 8.3.1 冒泡排序



### 8.3.2 快速排序



## 8.4 选择排序

### 8.4.1 简单选择排序



### 8.4.2 堆排序



## 8.5 归并排序、基数排序

### 8.5.1 归并排序



### 8.5.2 基数排序



## 8.6 各种内部排序算法的比较和应用

### 8.6.1 内部排序算法比较



### 8.6.2 内部排序算法应用



## 8.7 外部排序

### 8.7.1 外部排序的基本概念



### 8.7.2 外部排序的方法



### 8.7.3 多路平衡归并与败者树



### 8.7.4 置换选择排序



### 8.7.5 最佳归并树









