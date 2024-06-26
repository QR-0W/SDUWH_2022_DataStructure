# 数据结构

# 目录

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

	常见的时间复杂度按照从小到大的顺序可以排列如下：

	1. **O(1)**：常数时间复杂度。无论数据规模如何变化，算法所需时间都是固定的。
	2. **O(log n)**：对数时间复杂度。算法执行时间的增长速度比线性时间慢，常见于二分查找等算法。
	3. **O(n)**：线性时间复杂度。算法执行时间与数据规模成正比，例如简单的遍历操作。
	4. **O(n log n)**：线性对数时间复杂度。比线性时间复杂度高，但比平方时间复杂度低，常见于快速排序、归并排序等。
	5. **O(n^2)**：平方时间复杂度。算法执行时间与数据规模的平方成正比，例如冒泡排序、选择排序等。
	6. **O(n^3)**：立方时间复杂度。比平方时间复杂度更高，常见于某些复杂的动态规划算法或矩阵乘法。
	7. **O(2^n)**：指数时间复杂度。算法执行时间随数据规模的增加呈指数级增长，常见于某些递归算法。
	8. **O(n!)**：阶乘时间复杂度。算法执行时间随数据规模的增加极其迅速地增长，常见于解决旅行商问题等。

	

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

     

 3.  栈的重要数学性质：卡特兰数

     $n$ 个不同元素进栈，出栈元素的不同排列个数为：
     $$
     N = \frac{1}{n+1}C_{2n}^{n} = \frac{(2n)!}{n!(n+1)!}
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

 1.  队列的定义

     队列 Queue 也是一种操作受限的线性表，只允许在表的异端进行插入，另一端进行删除。

     ![image-20230926102922102](./assets/image-20230926102922102.png)

     

 2.  队列的基本操作

     ```C++
     InitQueue(&Q)，初始化队列
     
     QueueEmpty(Q)，判断队空
     
     EnQueue(&Q, x)，入队
     
     DeQueue(&Q, &x)，出队
     
     GetHead(Q, &x)，读取队头元素
      
     ```

     

### 3.2.2 队列的顺序存储结构

 1.  队列的顺序存储

     ​	队列的顺序存储类型可以描述为：

     ```C++
     #define MaxSize 50
     typedef struct
     {
         ElemType data[MaxSize];             //存放队列元素
         int front, rear;                    //队头、队尾指针
     } SqQueue;
     ```

     ​	队空条件：Q.front == Q.rear == 0

     

     ​	在这里存在“假溢出”的问题：

     ![image-20230926103611186](./assets/image-20230926103611186.png)

     ​	可以看到，即使队中可以存放元素，但也出现了上溢出。

     

 2.  循环队列

     ​	在这里引入循环队列的操作，利用取余实现队列的自动循环。

     ​	初始时 Q.front = Q.rear = 0，而每次前进都有 Q.rear/front = (Q.rear/front + 1) % MaxSize 。队列的长度则为 (Q.rear - Q.front + MaxSize) % MaxSize 。

     ​	但是在这种情况下无法区分队满和队空的区别，因此常用的方法是牺牲一个存储单元来区分队空与队满，如下图所示：

     ![image-20230926104258105](./assets/image-20230926104258105.png)

     ​	在这种情况下，队满条件为 (Q.rear + 1) % MaxSize == Q.front ，而队空条件仍然为 Q.front == Q.rear 。

     此时元素个数仍然为 (Q.rear - Q.front + MaxSize) % MaxSize 。

     

 3.  循环队列的操作

     1. 初始化

        ```C++
        void InitQueue(SqQueue &Q)
        {
            Q.rear = Q.front = 0;               //初始化队首、队尾
        }
        ```

        

     2. 判空

        ```C++
        bool isEmpty(SqQueue Q)
        {
            if(Q.rear == Q.front)               //队空
                return true;
            else
                return false;
        }
        ```

        

     3. 入队

        ```C++
        bool EnQueue(SqQueue &Q, ElemType e)
        {
            if((Q.rear + 1) % MaxSize == Q.front)
                return false;                   //队满
            Q.data[Q.rear] = e;
            Q.rear = (Q.rear + 1) % MaxSize;    //队尾+1取模
            return true;
        }
        ```

        

     4. 出队

        ```C++
        bool DeQueue(SqQueue &Q, ElemType &e)
        {
            if(Q.rear == Q.front)
                return false;                   //队空
            e = Q.data[Q.front];
            Q.front = (Q.front + 1) % MaxSize;  //队头+1取模
            return true;
        }
        ```

        

### 3.2.3 队列的链式存储结构

 1.  队列的链式存储

     ​	链队实际上是一个同时带有队头指针和队尾指针的单链表，头指针指向队头结点，尾指针指向队尾结点。存储表示如下所示：

     ```C++
     typedef struct LinkNode
     {
         ElemType data;
         struct LinkNode *Next;
     } LinkNode;
     
     typedef struct
     {
         LinkNode *front, *rear;
     } LinkQueue;
     ```

     ​	当 Q.front == NULL 且 Q.rear == NULL 的时候，队列为空。

     

     ​	在链式队列中，不带头结点的操作往往比较困难，因此需要采用带头结点的单链表来实现。

     ![image-20230926111045012](./assets/image-20230926111045012.png)

     ​	

 2.  链式队列的基本操作

     1. 初始化

        ```C++
        void InitQueue(LinkQueue &Q)
        {
            Q.front = Q.rear = (LinkNode *)malloc(sizeof(LinkNode));
            Q.front->Next = NULL;               //初始为空
        }
        ```

        

     2. 判空

        ```C++
        bool isEmpty(LinkQueue Q)
        {
            if(Q.front == Q.rear)
                return true;
            return false;
        }
        ```

        

     3. 入队

        ```C++
        void EnQueue(LinkQueue &Q, ElemType e)
        {
            LinkNode *s = (LinkNode *)malloc(sizeof(LinkNode));
            s->data = e;
            
            s->Next = NULL;                     //尾插法
            Q.rear->Next = s;
            Q.rear = s;
        }
        ```

        

     4. 出队

        ```C++
        bool DeQueue(LinkQueue &Q, ElemType &e)
        {
            if(Q.front == Q.rear)
                return false;
            LinkNode *p = Q.front->Next;
        
            e = p->data;
            Q.front->Next = p->Next;
        
            if(Q.rear == p)                     //若队列中只有一个结点，还需要调整rear
                Q.rear = Q.front;
            
            free(p);
            return true;
        }
        ```

        

### 3.2.4 双端队列

​	双端队列是指两端都可以入队和出队的队列。

![image-20230926112247314](./assets/image-20230926112247314.png)

​	

​	通常考察的为输入/输出受限的双端队列。

​	输出受限的双端队列是指允许在一端进行插入删除，另一端只能输入的队列：

![image-20230926112346366](./assets/image-20230926112346366.png)

​	而输入受限的双端队列是指允许在一端进行插入删除，另一端只能输出的双端队列：

![image-20230926112447097](./assets/image-20230926112447097.png)

​	在考察中，判断是否能根据条件得出序列方法往往是<u>一个个带入验证</u>即可。



## 3.3 栈和队列的应用

### 3.3.1 括号匹配

​	假设有一个括号序列，如下所示：

![image-20230926144725974](./assets/image-20230926144725974.png)

​	算法的基本思想如下：

- 利用栈存储左括号，遇到右括号就匹配，如果失匹就失败，否则消解。
- 一直重复直到扫描完成，若此时栈中还有括号，则失败。

​	

### 3.3.2 表达式转换、求值

​	主要是中缀、前缀和后缀表达式的转换。常见流程如下图所示：

![image-20230926161134571](./assets/image-20230926161134571.png)

​	

```C++
//计算优先度
int getPriority(char op)
{
    if (op == '+' || op =='-')
        return 0;
    else
        return 1;
}
```

​	如果需要用到栈与队列来实现的话，假设这里有一个中缀表达式 $a+b-a*((c+d)/e-f)+g $ ，则流程如下：

 1. 中缀转后缀

    ​	自左向右扫描，数字进入队列。

    ​	运算符用一个栈来保存。若栈空，则运算直接入栈。若栈非空，则有三种情况：

    ​	1、栈顶为左括号，则当前元素直接入栈；

    ​	2、当前元素为右括号，则将栈顶至左括号的全部元素全部出栈，并消除括号；

    ​	3、若栈顶为其他运算符，则循环比较当前运算符和栈顶运算符，如果栈顶运算符优先级$\ge$当前运算符优先级，则出栈并继续循环；否则入栈当前运算符，并停止循环。

    ```C++
    void infixToPostFix(char infix[], char s2[], int &top2) //s2为结果栈
    {
        char s1[MaxSize];
        int top1 = -1;
        int i = 0;
        while (infix[i]!='\0')
        {
            // 若为数字则直接入队
            if('0'<=infix[i] && infix[i]<='9')              
            {
                s2[top2++] = infix[i];                      //入队之后到下一位 
                ++i;
            }
            // 若为左括号则直接入栈
            else if (infix[i] == '(')                       
            {
                s1[++top1] = '(';
                ++i;
            }
            // 若为运算符则进行判断
            else if (infix[i] == '+' || infix[i] == '-' || infix[i] == '*' || infix[i] == '/')
            {
                if(top1 ==-1 || s1[top1] == '(' || getPriority(infix[i]) > getPriority(s1[top1]))
                //栈空/左括号/当前运算符大于栈顶预算夫优先级则入栈
                {
                    s1[++top1] = infix[i];
                    ++i;
                }
                else
                    s2[++top2] = s1[top1--];                //否则出栈
            }
            // 若为右括号
            else if (infix[i] == ')')                      
            {
                while (s1[top1]!='(')
                    s2[++top2] = s1[top1--];                //不停出栈
                --top1;                                     //左括号出栈
                ++i;                                        //跳过右括号
            }
        }
        // 将剩余的符号全部放入结果中
        while (top1 != -1)                                  
        {
            s2[++top2] = s1[top1--];
        }
    }
    ```

    

 2. 中缀转前缀

    ​	自右向左扫描，数字之间进入队列。

    ​	运算符用一个栈来保存。若栈空，则运算直接入栈。若栈非空，则有三种情况：

    ​	1、栈顶为右括号，则当前元素直接入栈；

    ​	2、当前元素为左括号，则将栈顶至右括号的全部元素全部出栈，并消除括号；

    ​	3、若栈顶为其他运算符，则循环比较当前运算符和栈顶运算符，如果栈顶运算符优先级$\gt$当前运算符优先级，则出栈并继续循环；否则入栈当前运算符，并停止循环。

    ```C++
    void infixToPreFix(char infix[], int len, char s2[], int &top2) // s2为结果栈
    {
        char s1[MaxSize];
        int top1 = -1;
        int i = len - 1;
        while (i >= 0)
        {
            // 若为数字则直接入队
            if ('0' <= infix[i] && infix[i] <= '9')
            {
                s2[top2++] = infix[i]; // 入队之后到下一位
                --i;
            }
            // 若为右括号则直接入栈
            else if (infix[i] == ')')
            {
                s1[++top1] = ')';
                --i;
            }
            // 若为运算符则进行判断
            else if (infix[i] == '+' || infix[i] == '-' || infix[i] == '*' || infix[i] == '/')
            {
                if (top1 == -1 || s1[top1] == ')' || getPriority(infix[i]) >= getPriority(s1[top1]))
                // 栈空/右括号/当前运算符大于等于栈顶预算夫优先级则入栈
                {
                    s1[++top1] = infix[i];
                    --i;
                }
                else
                    s2[++top2] = s1[top1--]; // 否则出栈
            }
            // 若为左括号
            else if (infix[i] == '(')
            {
                while (s1[top1] != ')')
                    s2[++top2] = s1[top1--]; // 不停出栈
                --top1;                      // 右括号出栈
                --i;                         // 跳过左括号
            }
        }
        // 将剩余的符号全部放入结果中
        while (top1 != -1)
        {
            s2[++top2] = s1[top1--];
        }
    }
    ```

    

 3. 后缀转前缀

    ​	每当扫描到一个运算符的时候，就将两个子表达式放到该运算符的后面。（参考表达式求值）

    

### 3.3.3 表达式求值

​	主要是中缀、前缀和后缀表达式的求值。

```C++
//计算优先度
int getPriority(char op)
{
    if (op == '+' || op =='-')
        return 0;
    else
        return 1;
}
//计算结果
int calSub(float opand1, char op, float opand2, float &result)
{
    if (op == '+')
        result = opand1 + opand2;
    if (op == '-')
        result = opand1 - opand2;
    if (op == '*')
        result = opand1 * opand2;
    if (op == '/')
    {
        if (fabs(opand2) < MIN)
            return 0;
        else
            result = opand1 / opand2;
    }
    return 1;
}
```



 1.  中缀表达式求值

     ​	需要用到两个栈，一个存数据，一个存符号。

     ```C++
     float calInfix(char exp[])
     {
         float s1[MaxSize];
         char s2[MaxSize];
         int top1 = -1, top2 = -1;
         int i = 0;
         while (exp[i] != '\0')
         {
             //数字直接入栈
             if ('0' <= exp[i] && exp[i] <= '9')
             {
                 s1[++top1] = exp[i] - '0';
                 ++i;
             }
             //左括号入运算符栈
             else if (exp[i] == '(')
             {
                 s2[++top2] = '(';
                 ++i;
             }
             //运算符要判断
             else if (exp[i] == '+' || exp[i] == '-' || exp[i] == '*' || exp[i] == '/')
             {
                 //栈空、栈顶为左括号、当前优先级高直接入栈
                 if (top2 == -1 || s2[top2] == '(' || getPriority(exp[i] > getPriority(s2[top2])))
                 {
                     s2[++top2] = exp[i];
                     ++i;
                 }
                 else
                 {
                     float opnd1, opnd2, result;
                     char op;
                     int flag;
                     opnd2 = s1[top1--]; // 第二个操作数先出栈
                     opnd1 = s1[top1--]; // 第一个操作数后出栈
                     op = s2[top2--]; 
                     flag = calSub(opnd1, op, opnd2, result);
                     if (flag == 0)
                     {
                         cout << "ERROR" << endl;
                         break;
                     }
                     s1[++top1] = result; // 将结果压入栈中
                 }
             }
             //右括号
             else if (exp[i] == ')')
             {
                 while(s2[top2] != '(')
                 {
                     float opnd1, opnd2, result;
                     char op;
                     int flag;
                     opnd2 = s1[top1--]; // 第二个操作数先出栈
                     opnd1 = s1[top1--]; // 第一个操作数后出栈
                     op = s2[top2--];
                     flag = calSub(opnd1, op, opnd2, result);
                     if (flag == 0)
                     {
                         cout << "ERROR" << endl;
                         break;
                     }
                     s1[++top1] = result; // 将结果压入栈中
                 }
                 --top2;                  // 左括号出栈
                 ++i;                     // 跳过右 括号
             }
         }
         //如果栈中还有元素，则进行运算 
         while (top2 != -1)
         {
             float opnd1, opnd2, result;
             char op;
             int flag;
             opnd2 = s1[top1--]; // 第二个操作数先出栈
             opnd1 = s1[top1--]; // 第一个操作数后出栈
             op = s2[top2--];
             flag = calSub(opnd1, op, opnd2, result);
             if (flag == 0)
             {
                 cout << "ERROR" << endl;
                 break;
             }
             s1[++top1] = result; // 将结果压入栈中
         }
         return s1[top1];
     }
     ```

     

 2.  后缀表达式求值

     ​	需要用到一个栈，同时存放数据和符号。

     ```C++
     float calPostFix(char exp[])
     {
         float s[MaxSize];
         int top = -1;
         int i = 0;
         while (exp[i] != '\0')
         {
             // 若为数字则直接入队
             if ('0' <= exp[i] && exp[i] <= '9')
                 s[++top] = exp[i] -  '0';
             // 若为运算符则直接计算
             else if (exp[i] == '+' || exp[i] == '-' || exp[i] == '*' || exp[i] == '/')
             {
                 float opnd1, opnd2, result;
                 char op;
                 int flag;
                 opnd2 = s[top--];           //第二个操作数先出栈
                 opnd1 = s[top--];           //第一个操作数后出栈 
                 op = exp[i];
                 flag = calSub(opnd1, op, opnd2, result);
                 if(flag == 0)
                 {
                     cout << "ERROR" << endl;
                     break;
                 }
                 s[++top] = result;          //将结果压入栈中
             }
             ++i;
         }
         return s[top];
     }
     ```

     

 3.  前缀表达式求值

     ​	需要用到一个栈，同时存放数据和符号，但是使从后往前扫描，且取出顺序不同。

     ```C++
     float calPreFix(char exp[], int len)
     {
         float s[MaxSize];
         int top = -1;
         for (int i = len - 1; i >= 0; --i)
         {
             if('0' <= exp[i] && exp[i] <= '9')
                 s[++top] = exp[i] - '0';
             else
             {
                 float opnd1, opnd2, result;
                 char op;
                 int flag;
                 opnd1 = s[top--]; // 第一个操作数先出栈
                 opnd2 = s[top--]; // 第二个操作数后出栈
                 op = exp[i];
                 flag = calSub(opnd1, op, opnd2, result);
                 if (flag == 0)
                 {
                     cout << "ERROR" << endl;
                     break;
                 }
                 s[++top] = result; // 将结果压入栈中
             }
         }
         return s[top];
     }
     ```

     

## 3.4 数组和特殊矩阵

在这里，我们将精力主要集中在如何将矩阵更有效的存储在内存中吗，并能方便地的从矩阵中提取元素。

### 3.4.1 数组的定义

​	数组是由 n 个相同类型的数据元素构成的有限序列。



### 3.4.2 数组的存储结构

​	大多数计算机提供了数组数据类型，逻辑意义上的数组可以采用计算机语言中的数组数据类型进行存储，一个数组的所有元素在内存中占用了一段连续的存储空间。

​	对于一维数组，其存储结构关系式为：
$$
LOC(a_{i}) = LOC(a_{0})+i \times L (0\le i \le n)
$$
​	对于二维数组，按照行优先的存储形式为：

![image-20230926224520482](./assets/image-20230926224520482.png)

​	关系式为：
$$
LOC(a_{i,j})=LOC(a_{0,0})+[i \times (h_{2}+1)+j]\times L
$$
​	按照列优先的存储形式为：

![image-20230926224752266](./assets/image-20230926224752266.png)

​	关系式为：
$$
LOC(a_{i,j})=LOC(a_{0,0})+[j \times (h_{1}+1)+i]\times L
$$


### 3.4.3 特殊矩阵的压缩存储

 1.  对称矩阵

     ​	对于n阶对称矩阵，上三角区和下三角所有对应元素相同，若仍然采用二维数组存储，则几乎会浪费一半的存储空间，为此可以只存储一半的矩阵。

     ![image-20230926225029939](./assets/image-20230926225029939.png)

     ​	在这里有，假设我们只存储下三角部分：

     ​	第一行：1个元素

     ​	第二行：2个元素

     ​	...

     ​	第 i 行：j - 1个元素

     ​	则元素 $a_{i,j}$ 在数组 B 中的下标 $k=1+2+...+(i-1)+(j-1)=\frac{i(i-1)}{2}+j-1$ 。

     ​	因此，元素之间的对应下标有：
     $$
     k=
     \left\{\begin{matrix} 
       \frac{i(i-1)}{2}+j-1，\space下三角、主对角线\\  
       \frac{j(j-1)}{2}+i-1，\space上三角
     \end{matrix}\right.
     $$

     

 2.  三角矩阵

     在下三角矩阵中，上三角区中所有元素均为同一常量。其存储思想和对称矩阵类似。

     在下三角矩阵中，元素下标之间的对应关系为：
     $$
     k=
     \left\{\begin{matrix} 
       \frac{i(i-1)}{2}+j-1，\space i\ge j （下三角和主对角线）\\  
       \frac{n(n+1)}{2}，\space j < j （上三角区）
     \end{matrix}\right.
     $$
     下三角矩阵在内存中的存储形式：

     ![image-20231012223807379](./assets/image-20231012223807379.png)

     

     上三角矩阵中，下三角区的所有元素均为同一常量。

     在上三角矩阵中，元素下标之间的对应关系为：
     $$
     k=
     \left\{\begin{matrix} 
       \frac{(i-1)(2n-i+2)}{2}+(j-i)，\space i \le j （上三角和主对角线）\\  
       \frac{n(n+1)}{2}，\space j < j （下三角区）
     \end{matrix}\right.
     $$
     上三角矩阵的在内存中的存储形式：

     ![image-20231012224316436](./assets/image-20231012224316436.png)

     

 3.  三对角矩阵

     ![image-20231012224354978](./assets/image-20231012224354978.png)
     
     元素与下标之间的对应关系为：
     $$
     k=2i+j-3
     $$
     在内存中存储形式为：
     
     ![image-20231012224540011](./assets/image-20231012224540011.png)
     
     反之，要是知道元素在数组的第k个位置，则可以得到
     $$
     i= \lfloor \frac{(k+1)}{3} + 1 \rfloor ,\space j=k-2i+3
     $$
     

### 3.4.4 稀疏矩阵

​	一般来说，矩阵里面元素个数很少的情况就称为稀疏矩阵。

​	稀疏矩阵既可以用数组存储，也可以采用十字链表法存储。



------



# 第四章 串

重点部分：

- KMP算法原理
- next数组推理过程
- nextval数组求解方法

提示：手工计算next数组可以先计算出表然后变形。nextval数组的求解方法需要了解。

## *4.1 串的定义和实现

### 4.1.1 串的定义

​	略。



### 4.1.2 串的存储结构

​	略。



### 4.1.3 串的基本操作

​	略。



## 4.2 串的模式匹配

### 4.2.1 简单模式匹配算法

​	略。



### 4.2.2 KMP算法（看天勤视频）

​	在 KMP 算法中，查找是不回头的，一次查找就结束。为了实现这个想法，我们需要利用前后缀。前缀指的是除了最后一个字符以外的所有头部子串，而后缀指的是除了第一个字符以外的所有尾部子串。

​	在 KMP 算法中如果出现失匹，则直接移动模式串，<u>把原来的前缀移动到后缀的位置</u>。（这里需要注意的是，在计算机中无法直接移动模式串，因此实际代码略有不同）

​	而在这里可以发现，实际上移动的位置就是最长公共前后缀的位置。

​	因此，根本无需主串，只需要知道模式串就可以得出如何移动即可。

​	在这里，为了方便起见，在 KMP 算法中，模式串的 [0] 位置通常为空，从 [1] 开始存储。

​	例如对于模式串$S$：
$$
A\space B\space A\space B\space A\space A\space A\space B\space A\space B\space A\space A
$$
​	$S[0]$为空，$S[1]$为A... 

​	因为对于这个模式串$S$，任何位置都有可能发生失匹，因此每一位都要求出对应的移动位置。如果将<u>移动模式串用计算机语言来表述</u>，则应该说：
$$
对于S[1]发生失匹，则下次从S[0]开始比较；\\
对于S[2]发生失匹，则下次从S[1]开始比较；\\
对于S[3]发生失匹，则下次从S[1]开始比较；\\
对于S[4]发生失匹，则下次从S[2]开始比较...
$$
​	将这里的目标记为一个数组，则有：
$$
0 \space 1 \space 1 \space2...
$$
​	依次类推，可以得到一个数组：
$$
0\space 1\space 1\space 2\space 3\space 4\space 2\space 2\space 3\space 4\space 5\space 6
$$
​	将最前面 [0] 位置置空，这就是 next 数组。



​	但是如果利用这个方法计算 next 数组，时间复杂度为$O(n^2)$，这没有意义。因此需要一种高效的方式来求 next 数组。

​	我们知道，在一个 next 数组中，必然有$t, j$，使得 $next[j]=t$ 。那么在这种情况下我们就可以尝试推导 $next[j+1]$ 的值：

- 若 $p_j=p_t$ ，则可得其最长公共前后缀+1，也即 $next[j+1]=t+1=next[j]+1$ 。
- 若 $p_j \ne p_i$ ，则可以转成“模式串失匹，需要移动到什么位置的问题”，循环的将 $t$ 赋值为 $next[t]$ ，直到 $t=0$ 或者满足 $p_j=p_t$ 为止。当 $t=0$ 时， $next[j+1]=1$ 。

​	代码见视频。



如何求解nextval数组？



------



# 第五章 树

重点部分：

- 树的基本概念
- 二叉树
- 树与森林
- 哈夫曼树、哈夫曼编码
- 并查集及其应用

提示：需要掌握树与二叉树的性质、遍历、转换、存储结构等，满二叉树、完全二叉树、线索二叉树、哈夫曼树的性质，二叉排序树和二叉平衡树的性质和操作，都是必然会涉及的内容。

## 5.1 树的基本概念

### 5.1.1 树的定义

​	树是 n 个结点的有限集，有且仅有一个特定的称为根的结点。

### 5.1.2 基本术语

​	度：树中一个结点的孩子个数称为该节点的度，树中结点的最大度数称为树的度。度为0的结点称为叶子节点。

​	深度：自根节点开始自顶向下逐层累加。

​	高度：自叶节点开始自底向上逐层累加。

### 5.1.3 树的性质

- （重要）对于任何树，都有：$结点数=所有结点度数之和+1$，也即 $n=n_1+2*n_2+..+k*n_k+1$ 。
- （重要）对于任何树，都有：$n=n_0+n_1+...+n_k$ 。
- 度为 $m$ 的树中，第i层上最多有 $m^{i-1}$ 个结点。
- 高度为 $h$ 的 $m$ 叉树，至多有 $\frac{m^k-1}{m-1}$ 个结点。
- 具有 $n$ 个结点的 $m$ 叉树，其最小高度为 $\lceil log_m(n(m-1)+1) \rceil$ 。



## 5.2 二叉树的概念

### 5.2.1 二叉树的定义及其主要特性

​	二叉树是一种特殊的树形结构，不存在度大于 2 的结点。二叉树是一颗有序树。



​	二叉树的性质：

- 对于一个非空二叉树，有 $n_0=n_2+1$ 。

- 高度为 $h$ 非空二叉树上第 $k$ 层最多有 $2^{k-1}$ 个结点，整个树上最多有 $2^h-1$ 个结点。

  



​	满二叉树：高度为 $h$ ，且含有 $2^h-1$ 个结点的二叉树。

![image-20231015220042016](./assets/image-20231015220042016.png)

- 对于满二叉树，除了叶子节点之外的每个结点度数均为 2 。
- 在满二叉树中，对于编号为 $i$ 的结点，若有双亲，则双亲编号为 $\lfloor \frac{i}{2} \rfloor$；若有左孩子，则左孩子编号为 $2i$ ；若有右孩子，则右孩子编号为 $2i+1$ 。



​	完全二叉树：高度为 $h$ ，有 $n$ 个结点的二叉树，当且仅当每个结点与高度为 $h$ 的满二叉树中编号为 1~n 的结点一一对应时称为完全二叉树。

![image-20231015220507501](./assets/image-20231015220507501.png)

- 若 $i \le \lfloor \frac{n}{2} \rfloor$ ，则结点为分支，否则为叶子结点。
- 度为 1 的结点只有一个，且只有左孩子。
- 对一个有 $n$ 个结点的完全二叉树，若高度为h，有 $2^{h-1} -1< n \le 2^h-1$ 或 $2^{h-1} \le n<2^h$ ，因此有 $h-1<log_2(n+1) \le h$ ，也即：$h = \lceil log_2(n+1) \rceil $ 或 $h = \lfloor log_2n \rfloor + 1$ 。



### 5.2.2 二叉树的存储结构

 1.  顺序存储结构

     

 2.  链式存储结构

     二叉树一般采用的是链式存储结构，用链表结点来存储二叉树中的每个结点。存储结构表示如下：

     ![image-20231016093535147](./assets/image-20231016093535147.png)

     其存储结构描述如下：

     ```C++
     typedef struct BiTNode
     {
         ElemType data;
         struct BiTNode *lChild, *rChild;
     } BiTNode, *BiTree;
     ```



​	在这里，需要注意的是，在一个含有 n 个结点的二叉链表中，含有 n+1 个空链域，这可以用来构成线索链表。



## 5.3 二叉树的遍历和线索二叉树

### 5.3.1 二叉树的遍历

​	二叉树的遍历是指按某条搜索路径访问树中每个结点。

​	由二叉树的递归定义可知，遍历一颗二叉树要决定对根节点 N，左子树 L 和右子树 R 的访问顺序。

 1.  先序遍历

	先序遍历的访问顺序：根 - 左 - 右

	```C++
	void PreOrder(BiTree T)
	{
	    if (T!=NULL)
	    {
	        visit(T);
	        PreOrder(T->lChild);
	        PreOrder(T->rChild);
	    }
	}
	```

	

 2.  中序遍历

	中序遍历的访问顺序：左 - 根 - 右

	```C++
	void InOrder(BiTree T)
	{
	    if(T!=NULL)
	    {
	        InOrder(T->lChild);
	        visit(T);
	        InOrder(T->rChild);
	    }
	}
	```

	

 3.  后序遍历

	后序遍历的访问顺序：左 - 右 - 根

	```C++
	void PostOrder(BiTree T)
	{
	    if(T!=NULL)
	    {
	        PostOrder(T->lChild);
	        PostOrder(T->rChild);
	        visit(T);
	    }
	}
	```

	

### 5.3.2 线索二叉树

1. 线索二叉树的基本概念

  ​	传统的二叉树进能够体现父子关系，而不能直接得到节点在遍历中的前驱或者后继。但是我们知道，在含有 n 个节点的二叉树中，有 n+1 个空指针。由此可以利用这些空指针来加速查找结点前驱和后继的速度。

  ​	线索二叉树的结构如下：

  ![image-20231105215835937](./assets/image-20231105215835937.png)

  ​	而标志域的含义如下：

  ![image-20231105215853921](./assets/image-20231105215853921.png)

  ​	对于线索二叉树，其存储结构描述如下：

  ```C++
  typedef struct ThreadNode
  {
      ElemType data;
      struct ThreadNode* lChild, *rChild;
      int lTag, rTag;
  }ThreadNode, *ThreadTree;
  ```

  

2. 中序线索二叉树的构造

  ​	二叉树的**线索化**是指将二叉链表中的空指针改为指向前驱或者后继的线索。线索化的实质就是遍历一次二叉树。

  ​	以中序线索二叉树的建立为例。附设指针 pre 指向刚刚访问过的结点，指针 p 指向正在访问的结点，即 pre 指向 p 的前驱。在中序遍历的过程中，检查 p 的左指针是否为空，若为空就将它指向 pre ；检查 pre 的右指针是否为空，若为空就将它指向 p 。

  ![image-20231105220700206](./assets/image-20231105220700206.png)

  ​	通过中序遍历对二叉树线索化的递归算法如下：

  ```C++
  void InThread(ThreadTree &p, ThreadTree &pre)
  {
      if (p != NULL)
      {
          InThread(p->lChild, pre);   //递归，线索化左子树
          if (p->lChild == NULL)      //左子树为空，建立前驱线索
          {
              p->lChild = pre;
              p->lTag = 1;
          }
          if (pre != NULL && pre->rChild == NULL)
          {
              pre->rChild = p;        //建立前驱结点的后继线索
              pre->rTag = 1;
          }
          pre = p;                    //标记当前节点成为刚刚访问过的结点
          InThread(p->rChild, pre);   //递归，线索化右子树
      }
  }
  ```

  ​	主要过程算法如下：

  ```C++
  void CreateInThread(ThreadTree T)
  {
      ThreadTree pre = NULL;
      if (T != NULL)
      {
          InThread(T, pre);       //对非空二叉树线索化
          pre->rChild = NULL;
          pre->rTag = 1;          //处理最后一个结点
      }
  }
  ```

  ​	

  ​	为了方便，可以在二叉树的线索链表上也添加一个头结点，使其 lChild 的指针指向根节点，rChild 的指针指向中序遍历访问时最后一个结点；而二叉树中的第一个结点 lChild 指针和最后一个结点的 rChild 指针指向头结点。

  ![image-20231105222156601](./assets/image-20231105222156601.png)

  

3. 中序线索二叉树的遍历

	中序线索二叉树的节点中隐含了线索二叉树的前驱和后继信息。因此遍历的过程可以这么表述：

	```C++
	ThreadNode *Firstnode(ThreadNode *p)    //求第一个结点
	{
	    while (p->lTag == 0)
	    {
	        p = p->lChild;
	    }
	    return p;
	}               
	
	ThreadNode *Nextnode(ThreadNode *p)     //求后继
	{
	    if (p->rTag == 0)
	    {
	        return Firstnode(p->rChild);
	    }
	    else
	    {
	        return p->rChild;
	    }
	}
	
	void Inorder(ThreadNode *T)
	{
	    for (ThreadNode *p = Firstnode(T);p!=NULL;p = Nextnode(p))
	        visit(p);
	}
	```

	

4. 先序和后序线索二叉树

	通过变动线索化构造的代码段与调用左右子树递归函数的位置，就可以建立先序、后序线索二叉树。

	

## 5.4 树、森林

### 5.4.1 树的存储结构

​	树的存储方式有多种，这里介绍三种常用的存储结构：

1. 双亲表示法

	​	这种存储方式采用一组连续空间来存储每个结点，同时在每个节点中增设一个伪指针，用来指示位置。

	![image-20231106153603354](./assets/image-20231106153603354.png)

	​	双亲表示法的存储结构描述如下：

	```C++
	#define MAX_TREE_SIZE 100
	typedef struct
	{
	    ElemType data;
	    int parent;
	} PTNode;
	
	typedef struct
	{
	    PTNode node[MAX_TREE_SIZE];
	    int n;
	} PTree;
	```

	

2. 孩子表示法

	​	孩子表示法是将每个结点的孩子结点动用单链表链接奇拉形成一个线性结构，此时 n 个结点就有 n 个孩子链表。

	![image-20231106160414328](./assets/image-20231106160414328.png)

	

3. 孩子兄弟表示法

	​	孩子兄弟表示法又称**二叉树表示法**，即以二叉链表作为树的存储结构。孩子兄弟表示法的存储结构描述如下：

	```C++
	typedef struct CSNode
	{
	    ElemType data;
	    struct CSNode *firstChild, *nextSibling;
	} CSNode, *CSTree;
	```

	![image-20231106160622806](./assets/image-20231106160622806.png)

	

### 5.4.2 树、森林、二叉树的转换

​	给定一棵树，可以找到唯一的一颗二叉树与之对应。从物理结构上看，他们的二叉链表是相同的，只不过是解释不同而已。

![image-20231106161454551](./assets/image-20231106161454551.png)

​	树转换为二叉树的规则是：左孩子右兄弟，也就是每个结点的左指针指向它的第一个孩子，右指针指向它在树中相邻的右兄弟。



​	森林转化为二叉树的规则与树类似，先将森林中的每棵树转化为二叉树，由于任何一棵和树对应的二叉树右子树必为空，则可以把第二棵树根视为第一颗树根的有兄弟等以此类推，将森林可以转化为二叉树。

![image-20231106163031951](./assets/image-20231106163031951.png)

​	二叉树转换为森林的规则：若二叉树非空，则二叉树的根及其左子树为第一棵树的二叉树形式，将根的右链断开。二叉树根的右子树又可以视为一个由除了第一棵树以外的森林转换后的二叉树，以此类推可以转化为内知道最后一棵没有右子树的二叉树为止。



### 5.4.3 树、森林的遍历



## 5.5 树与二叉树的应用

### 5.5.1 哈夫曼树、哈夫曼编码

1. 哈夫曼树的定义

	​	在许多应用中，树中结点会被赋予**权重**。从树根到该结点的路径长度与结点权重的乘积，称为该结点的**带权路径长度**，树中所有叶结点的带权路径长度之后称为**树的带权路径长度**，记为
	$$
	WPL = \sum_{i=1}^{n} w_{i}l_{i}
	$$
	​	其中，$w_i$ 是权重，$l_i$ 是路径长度。

	​	在含有 n 个带权叶结点的二叉树中，WPL 最小的二叉树称为哈夫曼树，也即**最优二叉树**。比如在下图中，C 的 WPL 最小，也就是哈夫曼树。

	![image-20231106165548932](./assets/image-20231106165548932.png)

	

	

2. 哈夫曼树的构造

	​	给定 n 个权值分别为 w1，w2，…，wn 的结点，构造哈夫曼树的算法描述如下：
	​	1、将这 n 个结点分别作为 n 棵仅含一个结点的二叉树，构成森林 F 。
	​	2、构造一个新结点，从 F 中选取两棵根结点权值最小的树作为新结点的左、右子树，并且将新结点的权值置为左、右子树上根结点的权值之和。
	​	3、从 F 中删除刚才选出的两棵树，同时将新得到的树加入 F 中。
	​	4、重复步骤 2 和 3 ，直至 F 中只剩下一棵树为止。

	​	

	​	比如下图就展示了一个过程。

	![image-20231106170625318](./assets/image-20231106170625318.png)

	

3. 哈夫曼编码

	​	哈夫曼编码是一种有效的数据压缩编码。

	​	若没有一个编码是另一个编码的前缀，我们就称这样的编码为**前缀编码**。

	​	由哈夫曼树得到哈夫曼编码的过程如下：将每个字符当作一个独立的结点，其权值为出现的次数，构造出对应的哈夫曼树。显然所有的字符节点都出现在叶结点中。然后将字符的编码解释为根到路径上标记的序列。比如下图所示。

	![image-20231106171458395](./assets/image-20231106171458395.png)

	​	这样构造出的哈夫曼树 WPL 为
	$$
	WPL=1×45+3×(13+12+16)+4×(5+9)=224
	$$
	​	需要注意的是，构造出的哈夫曼树可能是不同的，但是 WPL 必然是相同的。

	

### 5.5.2 并查集

​		通常用树的双亲表示作为并查集的存储结构，每个子集以一棵树表示。所有表示子集的树构成表示全集的森林，存放在双亲表示数组内。通常用数组元素的下标代表元素名，用根节点的下标代表子集名，根节点的双亲结点为负数。

​	例如，若开始时有一个集合 $S = \left \{  0,1,2,3,4,5,6,7,8,9 \right \}  $ 的表示如下：

![image-20231106215622734](./assets/image-20231106215622734.png)

​	经过一段时间的计算变成三个子集 $S_1 = \left \{  0,6,7,8\right \},S_2=\left \{ 1,4,9 \right \},S_3=\left \{ 2,3,5 \right \}   $ 的表示如下：

![image-20231106215633522](./assets/image-20231106215633522.png)

​	那么为了得到两个子集的并，只需要将其中一个子集的根节点的双亲指针指向另一个集合的根节点。也即 $S_1 \cup S_2$ 的表示如下：

![image-20231106215845359](./assets/image-20231106215845359.png)

​	在采用树的双亲指针数组作为并查集的存储表示的时候，集合的元素编号是从 0 到 size - 1。

​	

​	并查集的结构定义如下：

```C++
#define SIZE 100
int UFSets[SIZE];
```

​	并查集的初始化：

```C++
void Initial(int S[])
{
    for (int i = 0; i < SIZE; i++)
        S[i] = -1;
}
```

​	并查集的查找：

```C++
int Find(int S[], int x)
{
    while (S[x] >= 0)
    {
        x = S[x];
    }
    return x;
}
```

​	并查集的并操作：

```C++
void Union(int S[], int Root1, int Root2)
{
    S[Root2] = Root1;
}
```



------



# 第六章 图

重点部分：

- 图的基本概念
- 图的存储及基本操作：邻接矩阵、邻接表、邻接多重表、十字链表
- 图的遍历：BFS、DFS
- 图的基本应用：最小生成树、最短路径、拓扑排序、关键路径

提示：图的相关算法较多，通常只要求掌握基本思想和实现步骤，而算法的实现不是重点。



## 6.1 图的基本概念

### 6.1.1 图的定义

​	图 G 由顶点集 V 和边集 E 组成，记为 G = （V，E）。

 1.  有向图

	​	有方向的图。

 2.  无向图

	​	没有方向的图。

 3.  简单图、多重图

	​	一个图如果满足：1、不存在重复边，2、不存在顶点到自身的边，那么称之为简单图。若图中某两个顶点之间的边大于一条，又允许顶点和自身关联，则是多重图。

 4.  完全图

	​	有 $\frac{n(n-1)}{2}$ 条的边的**无向图**被称为完全图。在完全图中，任意两个顶点之间都存在边。

	​	而对于有向图，则是有 $n(n-1)$ 条弧的**有向图**称为完全有向图。在有向完全图中，任意两个顶点之间都存在方向相反的弧。

 5.  子图

	​	对于一个图 G，若有图 G‘ 使得 V’∈V、E‘∈E，则称 G' 是 G 的子图。

 6.  连通、连通图和连通分量

	​	在无向图中，若从顶点 v 到顶点 w 有路径存在，则称 v 和 w 是连通的。若 G 中任意两个顶点都是连通的，则称 G 是**连通图**，否则是**非连通图**。无向图中的**极大连通子图**称为**连通分量**。

 7.  强连通图、强连通分量

	​	在有向图中，若有一对顶点 v 和 w，互相都有路径，则称这两个顶点是强连通的。如图中任何一对顶点都是强连通的，则称其为**强连通图**。有向图中的**极大强连通子图**称为**强连通分量**。

 8.  生成树、生成森林

	​	连通图的生成树是包含图中全部顶点的**极小连通子图**。若图中顶点数为 n，则生成树含有 n-1 条边。

 9.  顶点的度、入度和出度

	​	在无向图中，顶点 v 的度是指顶点 v 的边的条数。对于 n 个顶点，e 条边的无向图，度数之和 = 2e，也就是无向图的全部顶点的度等于边数的两倍。

	​	有向图中，顶点 v 的度分为入度和出度，入度和出度之和是顶点的度。对于 n 个顶点，e 条边的有向图，入度之和 = 出度之和 = e。

 10.  边的权和网

	​	在一个图中，每条边都可以带权，这种边上有权的图称为网。

 11.  稠密图、稀疏图

	​	边数很少的图称为稀疏图。反之称之为稠密图。

 12.  路径、路径长度和回路

	​	顶点 v 到 w 之间的路径。路径上边的数量称为路径长度。

 13.  简单路径、简单回路

	​	在路径中，顶点不重复出现的路径称为简单路径。

	​	除了第一个顶点和最后一个顶点以外，其余顶点不重复出现的路径叫做简单回路。

 14.  距离

	​	如果最短路径存在，则称此路径的长度是距离。如果不存在路径，则距离记为无穷。

 15.  有向树



## 6.2 图的存储以及基本操作

### 6.2.1 邻接矩阵法

​	所谓的邻接矩阵是指用一个一维数组存储顶点的信息，用一个二维数组存储图中边的信息。这一二维数组被称为邻接矩阵。

![image-20231109162044249](./assets/image-20231109162044249.png)

​	有向图、无向图和网对应的邻接矩阵如图所示。图的邻接矩阵存储结构定义如下：

```C++
#define MaxVertexNum 100
typedef char VertexType;
typedef int EdgeType;

typedef struct
{
    VertexType Vex[MaxVertexNum];               //顶点表
    EdgeType Edge[MaxVertexNum][MaxVertexNum];  //邻接矩阵表
    int vexNum, arcNum;
} MGraph;
```

​	

​	图的邻接矩阵有以下特点：

1. 无向图的邻接矩阵一定是对称矩阵（并且唯一）。因此在实际存储时只需要存储三角矩阵。
1. 对于**无向图**，邻接矩阵的第 $i$ 行（或者第 $i$ 列）**非零元素的个数**正好是顶点的**度**。
1. 对于**有向图**，邻接矩阵的**第 $i$ 行非零元素的个数**正好是顶点的**出度**；**第 $i$ 列非零元素的个数**正好是顶点的**入度**。
1. 对于任意一个图 $G$ 的邻接矩阵 $A$，$A^n[i][j]$ 的元素等于由顶点 $i$ 到 $j$ 的长度为 $n$ 的**路径的数量**。



### 6.2.2 邻接表法

​	邻接表法更适合稀疏图。邻接表就是对图 $G$ 中的每个顶点 $v_i$ 建立一个单链表，第 $i$ 个单链表中的结点表示依附于顶点 $v_i$ 的边（对有向图是以该顶点为尾的弧），这个单链表就称为顶点 $v_i$ 的边表。边表的头指针和顶点的数据信息采用顺序存储，在邻接表中有两种结点：顶点表结点和边表结点。

![image-20231109221827173](./assets/image-20231109221827173.png)

​	无向图、有向图的邻接表示例如下所示：

![image-20231109221907591](./assets/image-20231109221907591.png)

​	图的邻接表存储结构定义如下：

```C++
#define MaxVertexNum 100

typedef struct ArcNode                          //边表结点
{
    int adjvex;                                 //弧指向的顶点位置
    struct ArcNode *next;                       //指向下一条弧的指针
} ArcNode;

typedef struct VNode                            //顶点表结点
{
    VertexType data;                            //顶点信息
    ArcNode *first;                             //指向第一条依附于该顶点的弧的指针
} VNode, AdjList[MaxVertexNum];

typedef struct
{
    AdjList vertices;                           //邻接表
    int vexnum, arcnum;                         //图的顶点数和弧数
} ALGraph;
```

​	

​	图的邻接表有以下特点：

1. 若 $G$ 为无向图，则所需的存储空间是 $O(\left | V \right | + \left | 2E \right | )$ ；若 $G$ 是有向图，则所需的存储空间是 $O(\left | V \right | + \left | E \right | )$。前者的倍数是 $2$ 是因为无向图中每条边出现两次。
2. 在邻接表中，给定一顶点，只需要读取他的邻接表就能找到他的所有邻边；但是在邻接矩阵中，相同的操作需要扫描一行，需要 $O(n)$ 的时间。但是若要确定两顶点之间是否存在边，邻接表需要在对应的结点边表中查找另一个结点，而邻接矩阵可以直接找到。
3. 在**有向图**的邻接表表示中，求一个给定顶点的出度只需要计算邻接表的中的节点个数，但是计算入度就需要遍历所有的邻接表。



### 6.2.3 十字链表法

​	十字链表是**有向图**的一种存储结构。弧和顶点都有对应的结点。

​	![image-20231110084547726](README.assets/image-20231110084547726.png)

​	弧结点中有五个域：$tailvex$ 和 $headvex$ 指示弧尾和弧头的位置，$hlink$ 指向弧头相同的下一条弧，$tlink$ 指向弧尾相同的下一条弧，$info$ 指向弧的相关信息。顶点结点中有三个域：$data$ 存放信息，$firstin$ 和 $firstout$ 指向以该顶点为弧头或弧尾的第一个弧结点。例如下图所示：

![image-20231110085448767](README.assets/image-20231110085448767.png)

​	在十字链表中，很容易求得顶点的入度和出度。



### 6.2.4 邻接多重表

​	邻接多重表是**无向图**的另一种链式存储结构。在邻接表中，求两个顶点之间是否存在边的效率较低。

​	与十字链表类似，在邻接多重表中，每条边用一个结点表示，结构如图所示：

![image-20231110090820918](README.assets/image-20231110090820918.png)

​	$mark$ 为标志域，用来标记是否被搜索过；$ivex$ 和 $jvex$ 为该边依附的两个顶点的位置；$ilink$ 指向下一条依附于顶点 $ivex$ 的边；$jlink$ 指向下一条依附于顶点 $jvex$ 的边。

​	每个顶点也用一个结点表示，由两个域组成：

![image-20231110091648643](README.assets/image-20231110091648643.png)

​	$data$ 存放顶点信息，$firstedge$ 指示第一条依附于该顶点的边。如下图所示，邻接多重表的各种基本操作与邻接表类似。

![image-20231110091812654](README.assets/image-20231110091812654.png)



### 6.2.5 图的基本操作

​	图的基本操作是独立于存储结构的。



## 6.3 图的遍历

​	图的遍历是指从图中的某一顶点出发，按照某种搜索方法沿着图中的边对图中所有顶点访问一次且仅访问一次。图的遍历算法主要有两种：BFS 和 DFS。



### 6.3.1 广度优先搜索 BFS

​	广度优先搜索 Breadth-First-Search 类似于层序遍历算法，基本思想是分层的查找，每向前走一步就访问一批顶点。不像 DFS 那样有回退的过程，它不是一个递归的算法。

​	广度优先搜索的伪代码如下：

```C++
bool visited[MAX_VERTEX_NUM];                   //访问标记数组

void BESTraverse(Graph G)                       //对图进行广度优先遍历
{
    for (i = 0; i < G.vexnum; ++i)
    {
        visited[i] = FALSE;                     //访问标记数组初始化
    }
    InitQueue(Q);                               //初始化辅助队列
    for (i = 0; i < G.vexnum; ++i)              //从 0 号顶点开始遍历
    {
        if (!visited[i])                        //对每个连通分量 BFS
        {
            BFS(G, i);
        }
    }
}

void BFS(Graph G, int v)                        //从顶点 v 开始，广度优先遍历图 G
{                                   
    visit(v);                                   //访问初始顶点 v
    visited[v] = TRUE;                          //标记已访问
    Enqueue(Q, v);                              //顶点 v 入队 Q
    while (!isEmpty(Q))
    {
        DeQueue(Q, v);                          //顶点 v 出队
        for (w = FirstNeighbour(G, v); w >= 0; w = NextNeighbour(G, v, W))
                                                //检测 v 所有邻接点
        {
            if (!visited[w])                    //w 为 v 的尚未访问的邻接顶点
            {
                visit(w);                       //访问 w
                visited[w] = TRUE;
                EnQueue(Q, w);
            }
        }
    }
}

```

​	

​	1、性能分析

​	在性能方面，BFS 算法无论是邻接表还是邻接矩阵的存储方式，都需要借助一个辅助队列 $Q$，$n$ 个顶点均需要入队一次，最坏的情况下的空间复杂度为 $O(\left | V \right |)$ 。

​	采用邻接表的存储方式时，每个顶点均需要搜索一次（也就是入队一次），故时间复杂度为 $O(\left | V \right | )$ ，在搜索邻接点的时候，每条边至少访问一次，故时间复杂度为 $O(|E|)$，因此总时间复杂度为 $O(|V|+|E|)$ 。而采用邻接矩阵的存储方式的时候，查找每个顶点的邻接点所需要的时间是 $O(|V|)$ ，因此总时间复杂度是 $O(|V|^2)$ 。



​	2、单源最短路径问题

​	使用 BFS 可以求解非带权图的单源最短路径问题，这是由广度优先搜索总是按照距离由近到远的特性决定的。

​	算法如下：

```C++
void BFS_Min_Distance(Grapg G, int u)
{
    for (i = 0; i < G.vexnum; ++i)
    {
        d[i] = INFINITY;            //d[i] 表示从 u 到 i 的最短路径，此处先初始化
    }
    visited[u] = TRUE;
    d[u] = 0;
    EnQueue(Q, u);
    while (!isEmpty(Q))             //BFS 算法主过程
    {
        DeQueue(Q, u);              //队头 u 出队
        for (w = FirstNeighbour(G, u); w >= 0; w = NextNeighbour(G, u, w))
        {
            if (!visited[w])        //w 为u 尚未访问的邻接顶点
            {
                visited[w] = TRUE;  //标记为已访问
                d[w] = d[u] + 1;    //路径长度 + 1
            }
        }
    }
}
```



​	3、广度优先生成树

​	在广度遍历的过程中，可以得到一棵**广度优先生成树**。

![image-20231110111736508](./assets/image-20231110111736508.png)

​	需要注意的是，给定一个图的邻接矩阵存储表示是唯一的，广度优先生成树也是唯一的，但是邻接表的存储表示不唯一，因此广度优先生成树也不唯一。



### 6.3.2 深度优先搜索 DFS

​	深度优先搜索 Depth-First-Search 类似于先序遍历。它的基本思想是尽可能“深”的搜索一个图。

​	其递归形式的算法如下：

```C++
bool visited[MAX_VERYEX_NUM];

void DFSTraverse(Graph G)
{
    for (v = 0; v < G.vexnum; ++v)
    {
        visited[v] = FALSE;         //初始化
    }
    for (v = 0; v < G.vexnum; ++v)  //本代码从 v=0 开始遍历
    {
        if (!visited[v])
        {
            DFS(G, v);
        }
    }
}

void DFS(Graph G, int v)
{
    visit(v);
    visited[v] = TRUE;
    for (w = FirstNeighbour(G, v); w >= 0; w = NextNeighbour(G, v, w))                        
    {
        if (!visited[w])            // w 为 v 的未访问邻接顶点
        {
            DFS(G, w);
        }
    }
}
```

​	

​	1、性能分析

​	DFS 是一个递归算法，需要借助一个递归栈来工作，因此空间复杂度是 $O( |V| )$ 。

​	遍历的过程实际上是对每个顶点查找其邻接点的过程，因此耗费的时间取决于存储结构。以邻接矩阵表示的时候，查找顶点的邻接点需要的时间是 $O( |V| )$ ，因此总时间复杂度为 $O( |V| ^2)$ 。而采用邻接表的时候，总时间复杂度为 $O(|V|+ |E| )$ 。



​	2、深度优先生成树和生成森林

​	与 BFS 一样，DFS 也会产生一棵深度优先生成树。但是只有对连通图调用 DFS 才能产生深度优先生成树，否则会产生深度优先生成森林。

​	与 BFS 类似，基于邻接表存储的深度优先生成树是不唯一的。



### 6.3.3 图的遍历、图的连通性

​	图的遍历算法可以用来判断图的连通性。对于无向图来说，如果图是连通的，那么从任一结点出发，都可以一次遍历就访问所有的顶点。对于有向图来说，若从初始顶点到图中的每个顶点都有路径，那么能够访问到图中所有的顶点。



## 6.4 图的应用

图的应用是历年的重点。更多的是结合图的实例来考察算法的具体操作过程，因此需要学会手动模拟哥哥算法的执行过程。



### 6.4.1 最小生成树

​	一个连通图的生成树包含图的所有顶点，并且只含有尽可能少的边。对于生成树来说，若砍去他的一条边，就会变成非连通图；若增加一条边，则会形成回路。

​	对于最小生成树来说，有以下性质：

​	1、对于一个图来说，最小生成树不是唯一的。只有当图中的各边的权值互不相等时，才有唯一的最小生成树。

​	2、若无向连通图中的边数比顶点数少 1 ，则其本身就是一棵树，图的最小生成树就是它本身。

​	3、最小生成树的边的权值的之和是唯一的，而且是最小的。

​	4、最小生成树的边数为顶点数减 1 。



​	常见的最小生成树算法有：Prim 算法和 Kruskal 算法。他们都基于贪心策略。对这两种算法应当能够手工模拟算法的实现步骤。

 1.  Prim 算法

	​	Prim 算法的执行过程非常类似于寻找图的最短路径的 Djikstra 算法。 

	​	Prim 算法初始时先任意取一个顶点加入树 T，然后每次选择一个与 T 中顶点集合距离最近的顶点，并将该顶点和相应的边都加入 T 。重复操作，直到图中所有**顶点**都加入 T 。

	![image-20231111223410488](./assets/image-20231111223410488.png)

	对于 Prim 算法的简单实现如下：

	![image-20231111223452992](./assets/image-20231111223452992.png)

	​	Prim 算法的时间复杂度为 $O( |V|^2 )$ ，不依赖于 $|E|$ 。因此它适用于求解**边稠密的图**的最小生成树。

	

 2.  Kruskal 算法

	​	Kruskal 算法是一种按照权值的递增次序选择合适的边来构造最小生成树的算法。
	
	​	与 Prim 算法不同，Kruskal 算法初始时为只有 n 个顶点为没有边的非连通图，然后循环的按照边的权值由小到大的顺序，不断选取当前未被选取过的、权值最小的边，若该边依附的顶点不在生成树中，则将其加入生成树，否则舍弃这个边选取下一条权值最小的边。重复这个过程直至所有顶点都加入了生成树。
	
	![image-20231112203336185](./assets/image-20231112203336185.png)
	
	​	对于 Kruskal 算法的简单实现如下所示：
	
	![image-20231112203955796](./assets/image-20231112203955796.png)
	
	​	在 Kruskal 算法中，采用堆来存放边的集合，因此每次选择最小权值的边需要 $O(log|E|)$ 的时间。此外，由于生成树中所有边可以被视为一个等价类，因此每次添加新的边类似于求解等价类的过程，因此可以采用并查集的数据结构来描述生成树 T，从而构造 T 的时间复杂度为 $O(|E|log|E|)$ 。因此，Kruskal 算法适用于**边稀疏但是顶点多**的图。
	
	

### 6.4.2 最短路径

​	当图是带权图的时候，把一个顶点到图中任意一个顶点的一条路径所经过边上的权值之和，定义为该路径的带权路径长度，把最短的路径称为**最短路径**。

​	求解最短路径的算法通常依赖于一种性质，即两点之间的最短路径也包含了路径上其他顶点间的最短路径。对于单源最短路径，利用 Djikstra 算法求解；对于每对顶点之间的最短路径，通过 Floyd 算法求解。

​	

​	1、Dijkstra 算法求解单源最短路问题

​	Dijkstra 算法利用一个集合 $S$ 记录已经求出的最短路径的顶点，初始时将源点 $v_0$ 放入 $S$ ，$S$ 每加入一个新顶点 $v_i$ 都要修改源点 $v_0$ 到集合 $V-S$ 中顶点当前的最短路径长度值。在构造过程中还设置两个辅助数组：

- dist [ ] ：记录从源点到其他顶点当前的最短路径长度。
- path [ ] ：path[i] 标识从源点到顶点 i 之间最短路径的前驱结点。

​	

​	Dijkstra算法的步骤可以整理如下：

1. **初始化**：开始时，集合S只包含起点（假设为节点0），即`S = {0}`。距离数组`dist[]`初始化为从起点到各个顶点的距离，对应于邻接矩阵`arcs[0][i]`的值。
2. **选择最短路径顶点**：从集合V（所有顶点）减去集合S（已经找到最短路径的顶点集合）中选择一个顶点`vj`，使得`dist[j]`是最小的，即`dist[j] = Min{dist[i] | vi ∈ V-S}`。然后将`vj`加入集合S中，即`S = S ∪ {j}`。
3. **更新距离数组**：更新起点到集合V-S中所有顶点的最短路径长度。如果通过新加入集合S的顶点`vj`到某顶点`vk`的路径比当前已知的路径短，即如果`dist[j] + arcs[j][k] < dist[k]`，则更新`dist[k]`为`dist[j] + arcs[j][k]`。
4. **重复步骤**：重复步骤2和步骤3共n-1次，直到所有顶点都被包含在集合S中。这时，`dist[]`数组中存储的就是起点到所有其他顶点的最短路径长度。

​	

​	使用邻接矩阵表示时，时间复杂度为 $O( |V |^2 )$ 。使用带权的邻接表表示时，虽然修改 dist 数组的时间减少了，但是由于在 dist 数组中选择最小分量的时间不变，时间复杂度仍为 $ O( |V|^2 ) $ 。另外，求解从源点到特定顶点的最短路径的时间复杂度，与求解源点到其他顶点的最短路径一样，都是 $ O( |V|^2 ) $ 。

​	需要注意的是，如果边上有负权值的时候，Dijkstra 算法并不适用。若允许边上带有负权值，则无法确定最短路径长度了。

​	

​	2、Floyd 算法求解各顶点之间最短路径问题

​	Floyd 算法的基本思想是：

​	Floyd算法通过递推地更新路径长度矩阵来找到所有顶点对之间的最短路径。初始矩阵\( A^{(-1)} \)为图的邻接矩阵，其中：

$$
A^{(-1)}[i][j] = 
\begin{cases} 
\text{边的权值} & \text{如果存在从} v_i \text{到} v_j \text{的边} \\
\infty & \text{如果不存在从} v_i \text{到} v_j \text{的边}
\end{cases}
$$

​	在每个递推步骤\( k \)（其中\( k = 0, 1, ..., n-1 \)），算法尝试通过顶点\( k \)作为中介来更新路径长度。更新规则为：

$$
A^{(k)}[i][j] = \min(A^{(k-1)}[i][j], A^{(k-1)}[i][k] + A^{(k-1)}[k][j])
$$

​	经过\( n-1 \)次更新后，最终矩阵\( A^{(n-1)} \)包含了所有顶点对之间的最短路径长度。



​	Floyd 算法利用邻接矩阵不断地计算，从而求解出所有的最短路径。它的时间复杂度为 $O(|V|^3)$ ，也允许图中带有负权值的边，但不允许有包含带负权值的边组成的回路。Floyd 算法永阳适用于带权无向图，因为带权无向图可以视为权值相同往返二重边的有向图。



### 6.4.3 有向无环图描述表达式

​	若一个有向图中不存在环，则称为有向无环图，简称 DAG 图。有向无环图是描述含有公共子式的表达式的有效工具。

​	例如，对于表达式 $((a+b)*(b*(c+d))+(c+d)*e)*((c+d)*e)$ ，可以用二叉树表示。观察子式可以发现存在相同的子表达式 $(c+d)$ 和 $(c+d)*e$ ，而在二叉树中,它们也重复出现。若利用有向无环图，则可实现对相同子式的共享，从而节省存储空间。

![image-20231116101058724](./assets/image-20231116101058724.png)



### 6.4.4 拓扑排序

​	若用 DAG 图表示一个工程，用顶点表示活动，用有向边 $<V_i, V_j>$ 表示活动 $V_i$ 必须先于活动 $V_j$ 进行的关系，则将这种有向图称为定点表示活动的网络，记为 AOV 网。

​	在图论中，由一个有向无环图的顶点组成的序列，当且仅当满足以下条件的时候，称为拓扑排序：

1. 每个顶点出现且只出现一次
2. 若顶点 A 排在顶点 B 后面，则不存在 B 到 A 的路径。

​	拓扑排序是对有向无环图的顶点的一种排序，它使得若存在一条从顶点 A 到顶点 B 的路径，则在排序中顶点 B 出现在顶点 A 的后面。每个 AOV 网都有一个或多个拓扑排序序列。



​	对 AOV 网进行拓扑排序的算法如下：

1. **选择顶点**：从 AOV 网络中选择一个没有前驱（即没有指向它的边）的顶点，并输出这个顶点。
2. **删除顶点和边**：从网络中删除刚刚选择的顶点，以及所有以这个顶点为起点的有向边。
3. **重复操作**：重复步骤 1 和 2 ，直到当前的 AOV 网络为空，或者网络中不存在无前驱的顶点为止。如果出现后者的情况，这说明有向图中存在环。

​	这个算法的核心是不断移除无前驱的顶点，通过这种方式来确定顶点的顺序。如果无法继续执行这个过程，表明图中存在环，因此无法进行拓扑排序。

​	下图展示的是一个拓扑排序算法的过程：

![image-20231116103249476](./assets/image-20231116103249476.png)

​	由于输出每个顶点的同时还要删除以它为起点的边，因此采用邻接表的时候，时间复杂度为 $O(|V|+|E|)$ ，采用邻接矩阵的时候时间复杂度为 $O(|V|^2)$ 。

​	

​	此外，对于一个 AOV 网，也可以输出逆拓扑排序：

1. **选择顶点**：从 AOV 网中选择一个没有后继的顶点（即出度为 0，没有从该顶点出发的边）并输出。
2. **删除顶点和边**：从网络中删除该顶点以及所有以它为终点的有向边。
3. **重复步骤**：重复步骤 1 和 2，直到当前的 AOV 网为空。

​	逆拓扑排序的过程和普通的拓扑排序相反，它从没有后继的顶点开始，逐步去除顶点及其关联的边。



### 6.4.5 关键路径

​	在带权有向图中，用顶点表示时间，用有向边表示活动，用边上的权值表示完成该活动的开销，称之为用边表示活动的网络，简称 AOE 网。AOE 和 AOV 网都是有向无环图。

​	在 AOE 网中，因为路径长度可能不同，但是只有完成所有路径上的活动才算完成工程。因此，具有最大路径长度的路径称为**关键路径**，而关键路径上的活动称为**关键活动**。完成整个工程的最短时间就是关键路径的长度。

​	求解关键路径的步骤是：

1. 求事件最早发生时间 $ve(i)$ ：正向求顶点。源点是 0，剩下的顶点有 $ ve[i]=Max \{ ve[j]+weight(v_j,v_i) \} $ （也就是从源点开始，选取最大的入度加上去）。
2. 求事件最晚发生时间 $vl(i)$ ：逆向求顶点。按照逆拓扑排序序列，设置 $vl[汇点]=ve[汇点]$，$ vl[i]=Min \{ vl[j]-weight(v_i,v_j) \} $，$v_i$ 为 $v_j$ 的任意前驱。（从汇点开始，选取最小的出度差）
3. 求活动最早开始时间 $e(i)$：正向求有向边。若边 $<v_i,v_j>$ 表示活动 $i$ ，则有 $e[j]=ve[i]$ 。（最早开始时间是源点的 $ve$ ）
4. 求活动最晚发生时间 $l(i)$ ：逆向求有向边。若边 $<vi,vj>$ 表示活动 $i$ ，则有 $l[i]=vl[j]-weight(v_i,v_j)$ 。（最晚发生时间是源点的 $vl$ 减去边的权值）
5. 求时间余量 $d(i)$：$l(i) - e(i)$，如果为 0 就说明是关键活动，必须要如期完成。

​	在实际应用中，如果是选择题，则求 $ve$ 的过程就能知道关键路径了。

![image-20231116115053070](./assets/image-20231116115053070.png)



​	扩展解法思路参考自一位博主写的408真题篇，个人进行了改善。可以借助贪心算法的思想来选择。例如下面这张图：

![image-20231116113533395](./assets/image-20231116113533395.png)

​	可以先找出里面最长的几条边构造关键路径，b=5、f=4、i=4、d=3、e=3，枚举到这里就差不多了，我们发现 b=5、e=3、i=4 已经能将起点终点连通了。

​	假设这就是起点到终点的最长路径，下面开始看看起点到终点的最短路径 a=2、c=1、g=1，我们可以观察到反差最明显的，就是路径3 -> 6 可以分解为3->4->6，g 的时间余量明显是很大的。

​	但是要注意的是，这种贪心解法高效，但是正确率并非 100%。





------



# 第七章 查找

重点部分：

- 折半查找
- 哈希表
- B 树
- B+树

对于散列查找，需要掌握构造、查找长度‘性能分析等。对于折半查找，需要掌握过程、判定树、平均查找长度等。B 树需要掌握插入、删除、查找的过程，B+树需要了解基本概念和性质。



## 7.1 查找的基本概念



## 7.2 顺序查找和折半查找

### 7.2.1 顺序查找

​	顺序查找对于顺序表和链表都是适用的。

1. 一般线性表的顺序查找

	在一般线性表的顺序查找中，会引入“哨兵”的概念，即从后往前查找，将最前面的元素设为哨兵，防止数组越界。

	​	查找成功时，顺序查找的平均长度为
	$$
	ASL_{成功} = \sum _{i=1}^{n} P_i(n-i+1)
	$$
	​	当每个元素查找概率相同的时候，有
	$$
	ASL_{成功} = \sum _{i=1}^{n} P_i(n-i+1) = \frac {n+1}{2}
	$$
	​	查找不成功的时候，与表中关键字比较的次数显然是 $n+1$ 次，从而平均查找长度 $ASL_{不成功} = n+1$ 。

	

2. 有序表的顺序查找

	​	若在查找之前就知道表是有序的，则查找失败的时候可以降低平均查找长度。

	​	可以利用判定树来表示有序线性表的查找过程。树中圆形结点表示存在的元素，而矩形则是失败节点。若查找到失败结点，则说明查找不成功。

	![image-20231116141459877](./assets/image-20231116141459877.png)

​		在这里，查找成功的 ASL 和一般线性表的顺序查找一样。而查找失败时，查找指针一定到了某个失败节点，但是由于失败节点是虚构的，因此实际长度是上一个圆形结点所在的层数，因此有 
$$
ASL_{不成功} = \sum _{j=1}^{n} q_j(l_j - 1) = \frac{1+2+···+n+n}{n+1} = \frac{n}{2}+\frac{n}{n+1}
$$
​		其中 $q_j$ 是达到第 $j$ 个失败结点的概率，在相同查找概率的情况下是 $\frac{1}{n+1}$；$l_j$ 是第 $j$ 个失败结点所在的层数。



### 7.2.2 折半查找

​	折半查找又称二分查找，仅适用于有序顺序表。算法思想：

- 比较待查找值 key 与表中间位置的元素。
- 如果相等，则查找成功，返回该元素位置。
- 如果不等，根据表的排序情况（如升序），确定查找范围在中间元素的前半部分或后半部分。
- 在缩小的范围内重复查找，直到找到元素或确定元素不存在。

​	代码实现（C语言）：
```C++
int Binary_Search(SeqList L, ElemType key) {
    int low = 0, high = L.TableLen - 1, mid;
    while (low <= high) {
        mid = (low + high) / 2; // 取中间位置
        if (L.elem[mid] == key)
            return mid; // 查找成功则返回所在位置
        else if (L.elem[mid] > key)
            high = mid - 1; // 从前半部分继续查找
        else
            low = mid + 1; // 从后半部分继续查找
    }
    return -1; // 查找失败，返回-1
}
```
​	在这段代码中，通过不断调整查找范围的上下界 `low` 和 `high` 来缩小搜索区域，直到找到目标值或区间为空时，表明查找失败。

​	折半查找的过程可以用判定树来表示。显然，判定树是一颗平衡二叉树。

![image-20231116144137170](./assets/image-20231116144137170.png)

​	ASL成功需要计算每个元素查找成功时的查找长度之和，然后除以元素的总数。具体计算方法取决于元素的分布和树的高度。

​	ASL不成功需要计算查找失败时的平均查找长度。在等概率的情况下，通常计算为树的平均高度加一（因为查找失败通常需要走完整个查找路径）。

​	在图所示的判定树中，在等概率情况下，查找成功（圆形结点）的 $ASL=(1×1+2×2+3×4+4×4)/11=3$ ，查找不成功（方形结点）的 $ASL=(3×4+4×8)/12=11/3$ 。



### 7.2.3 分块查找

​	分块查找又称按索引顺序查找。它将查找表分为若干子块，块内元素可以是无序的，但是块之间是有序的。然后再建立一个索引表，表中的每个元素是各块的最大关键字和第一个元素的地址，按照关键字有序排列。

​	分块查找在查找时分为两步：第一步是在索引表中，利用顺序查找或者折半查找确定块；第二步在块内顺序查找。

![image-20231116171934115](./assets/image-20231116171934115.png)

​	分块查找的 $ASL = L_l+L_S$ ，将长度为 $n$ 的查找表均匀地分为 $b$ 块，每块 $s$ 个记录，在等概率的情况下，若在块内采用顺序查找，则平均查找长度为：
$$
ASL = L_l+L_s = \frac{b+1}{2}+\frac{s+1}{2}= \frac{s^2+2s+n}{2s}
$$
​	此时，若 $s = \sqrt{n} $，则有 $ASL_{min} = \sqrt{n}+1$ 。

​	若对索引表采用折半查找，则平均查找长度为：
$$
ASL = L_l+L_s=\lceil log_2(b+1)+\frac{s+1}{2} \rceil
$$


## 7.3 树形查找

### 7.3.1 二叉排序树 BST

1. 二叉排序树的定义

  二叉排序树要么是一颗空树，要么是符合以下特性的树：

  - 若左子树非空，则左子树上所有结点的值小于根节点的值；
  - 若右子树非空，则右子树上所有结点的值大于根节点的值；
  - 左右子树也是二叉排序树。

  ![image-20231116175752662](./assets/image-20231116175752662.png)

  

2. 二叉排序树的查找

  ​	二叉排序树的查找过程可以描述如下：

  ​	当二叉排序树非空时，查找开始于树的根节点。首先，将待查找的值与根节点的关键字进行比较。如果两者相等，则查找成功。如果待查找的值小于根节点的关键字，则在根节点的左子树上继续查找；反之，如果大于根节点的关键字，则在根节点的右子树上查找。

  ​	这是一个递归的过程，意味着每一步查找都按照相同的规则在子树上进行，直至找到目标值或达到叶子节点（查找失败）。

  ​	代码如下：

  ```C++
  BSTNode *BST_Search(BiTree T, ElemType key) {
      while (T != NULL && key != T->data) { // 循环，直到找到节点或遍历完树
          if (key < T->data) 
              T = T->lchild; // 若查找值小于当前节点值，则在左子树上继续查找
          else 
              T = T->rchild; // 若查找值大于当前节点值，则在右子树上继续查找
      }
      return T; // 返回找到的节点，若未找到则返回 NULL
  }
  ```

  

3. 二叉排序树的插入

  ​	二叉排序树是查找的过程中，当树中不存在关键字值等于给定值的结点时，再进行插入的。二叉排序树的插入过程可以这样描述：

  - 如果原二叉排序树为空，新插入的节点直接成为树的根节点。

  - 如果树非空，插入操作开始于根节点。比较待插入节点的关键字 k 与当前节点的关键字。

  - 如果 k 小于当前节点的值，继续在左子树上进行插入操作；如果 k 大于当前节点的值，则在右子树上进行插入。

  - 这个过程是递归的，直到找到一个适当的叶子节点位置进行插入。新插入的节点始终是叶子节点，即它没有子节点，并且它是查找过程中最后访问的节点的左孩子或右孩子。

  ![image-20231116180726347](./assets/image-20231116180726347.png)

  ​	代码如下：

  ```C++
  int BST_Insert(BiTree &T, KeyType k) {
      if (T == NULL) {
          // 原树为空,新插入的记录作为根结点
          T = (BiTree)malloc(sizeof(BSTNode));
          T->data = k;
          T->lchild = T->rchild = NULL;
          return 1; // 返回1,插入成功
      } else if (k == T->data) {
          return 0; // 树中存在相同关键字的结点,插入失败
      } else if (k < T->data) {
          // 插入到T的左子树
          return BST_Insert(T->lchild, k);
      } else {
          // 插入到T的右子树
          return BST_Insert(T->rchild, k);
      }
  }
  ```

  

4. 二叉排序树的构造

	​	从一颗空树出发创建。

	![image-20231116182145656](./assets/image-20231116182145656.png)

	​	代码如下：

	```C++
	void Creat_BST(BiTree &T, KeyType str[], int n) {
	    T = NULL; // 初始时 T 为空树
	    int i = 0;
	    while (i < n) {
	        // 依次将每个关键字插入到二叉排序树中
	        BST_Insert(T, str[i]);
	        i++;
	    }
	}
	```

	

5. 二叉排序树的删除

	​	在二叉排序树中删除一个结点的时候，不能把以该节点为根的子树上的结点都删除，必须先把被删除结点从结点摘下，然后将断开结点的二叉链表重新连接起来，还要保证二叉排序树的性质不会丢失。

	​	二叉排序树的删除有三种情况：

	​	1、被删除结点 z 是叶子结点：这种情况可以直接删除。

	![image-20231116182434023](./assets/image-20231116182434023.png)

	​	

	​	2、被删除结点 z 只有一棵子树：让 z 的子树，变成 z 的父结点的子树。

	![image-20231116182441833](./assets/image-20231116182441833.png)

	​	

	​	3、被删除结点 z 有两棵子树：在要删除的节点的右子树中找到最小的节点，将找到的替代节点的值复制到被删除节点的位置，然后删除替代结点，并重新构造剩下的部分。

	![image-20231116182500962](./assets/image-20231116182500962.png)

	

6. 二叉排序树的查找效率分析

	​	二叉排序树的效率取决于树的高度。若二叉排序树的左右子树高度差不超过 1，则称其为平衡二叉树，它的 ASL 为 $O(log_2n)$ 。若二叉排序树是一个单支树，则 ASL 为 $O(n)$ 。

	![image-20231116183329097](./assets/image-20231116183329097.png)

	​	但是通常而言，它的时间性能和二分查找差不多。

	

### 7.3.2 平衡二叉树

1. 平衡二叉树的定义

	​	左右子树的高度差的绝对值不超过 1 的二叉树称为**平衡二叉树**。一个结点的左子树与右子树的高度差为该结点的**平衡因子**。

	

2. 平衡二叉树的调整

	​	我觉得看这个视频比较好：

	[【一秒学会 平衡二叉树的调整，非标题党！不简单你打我！ （考研数据结构）】 ](https://www.bilibili.com/video/BV16m4y1F7do/?share_source=copy_web&vd_source=662a39278574867e68e19ee73fcdbd61)

	

3. 平衡二叉树的查找

	​	在平衡二叉树上进行查找的过程与二叉排序树的相同，因此，在查找过程中，与给定值进行的比较的关键字个数不超过树的深度。

	

### 7.3.3 红黑树

1. 红黑树的定义

	

2. 红黑树的插入

	

3. 红黑树的删除

	

## 7.4 B树、B+树

考研大纲对 B 树和 B+ 树的要求各不相同，重点在于考查 B 树，不仅要求理解 B 树的基本特点，还要求掌握 B 树的建立、插入和删除操作，而对 B+ 树则只考查基本概念。

### 7.4.1 B树及其基本操作

​	B 树（多路平衡查找树）中，所有结点的孩子个数的最大值称为 B 树的阶，用 $m$ 表示。一棵 $m$ 阶 B 树要么是空树，要么满足以下条件：

- 每个结点至多有 $m$ 棵子树，也就是最多有 $m - 1$个关键字。

- 若根节点不是终端结点，则至少有两棵子树。

- 除了根节点以外的所有非叶结点至少有 $\lceil \frac{m}{2} \rceil$ 棵子树，也即最少含有 $\lceil \frac{m}{2} \rceil -1 $ 个关键字。

- 所有非叶结点的构造如下：

	![image-20231120153549681](./assets/image-20231120153549681.png)

	- **关键字（K1, K2, ..., Kn）**：每个节点包含一系列的关键字，这些关键字按顺序排列，满足 K1 < K2 < ... < Kn。
	- **子树指针（P1, P2, ..., Pn）**：每个节点还包含指向其子树根节点的指针。对于任意指针 Pi，Pi-1 所指向的子树中所有节点的关键字都小于 Ki，而 Pi 所指向的子树中所有节点的关键字都大于 Ki。
	- **关键字的数量（n）**：节点中关键字的个数 n 有一定的限制，通常位于 $\lceil m/2 \rceil -1$ 到 m-1 的范围内，其中 m 是树的阶数。

- 所有的叶结点出现在同一层次上，并且不带信息。



​	B 树的所有结点的平衡因子都为 0 。比如下列的 5 阶 B 树。

![image-20231120154502993](./assets/image-20231120154502993.png)



1. B 树的高度

  ​	B 树中大部分操作所需的存取次数与 B 树的高度成正比。首先需要明确的是，B 树的高度不包括最后的不带任何信息的叶节点所处的那一层。

  ​	若 $n \ge 1 $，则对任意一个包含 $n$ 个关键字，高度为 $h$，阶数为 $m$ 的 B 树，有：

  - 因为 B 树中每个结点最多有 $m$ 棵子树，$m - 1$ 个关键字，所以在一棵高度为 $h$ 的 $m$ 阶 B 树中，关键字的个数应该满足 $ n \ge (m-1)(1+m+m^2+...+m^{h-1}) = m^h-1$ ，因此有：

  	$$
  	h \ge log_m(n+1)
  	$$

  - 若让每个结点中的关键字个数达到最少，则容纳同样多的关键字的 B 树高度达到最大。在 B 树中，除了根节点之外的每个非叶结点至少有 $\lceil m/2 \rceil$ 棵子树，因此对于第 $h+1$ 层至少有 $2(\lceil m/2 \rceil)^{h-1}$ 个结点。对于关键字个数是 $n$ 的 B 树，叶节点为 $n+1$ ，因此有 $n+1 \ge 2(\lceil m/2 \rceil)^{h-1}$，也即 

  	$$
  	h \le log_{\lceil \frac{m}{2} \rceil}(\frac{n+1}{2}+1)
  	$$




2. B 树的查找

  ​	在 B 树上进行查找与二叉查找树很相似，但是每个结点上做的是多路分支。B 树的查找包含两个基本操作：在 B 树中查找结点，在结点中查找关键字。由于 B 树通常是存储在磁盘中的，因此前一个操作是在磁盘上进行的，后一个则是在内存中进行的。

  ​	在 B 树中找到某个结点后，先在有序表中查找，若找到则查找成功，否则按照对应的指针信息区子树中查找。查到叶结点的时候说明树中没有对应关键字，查找失败。

  

3. B 树的插入

	​	B 树的插入过程包括几个关键步骤，以确保树在插入新关键字后仍然保持其平衡性质。以下是 B 树插入过程的概述：

	1. **查找正确的节点**：从根节点开始，向下遍历 B 树以找到应该插入新关键字的叶子节点。这个过程类似于在二叉查找树中查找插入位置。
	2. **插入关键字**：在找到的叶子节点中插入新关键字，并保持关键字的有序性。
	3. **分裂满节点**：
		- 如果插入关键字后，节点中的关键字数量超过了最大限制（通常是节点容量 $m-1$），则需要分裂该节点。
		- 节点被分裂为两个新节点，每个新节点包含一半的关键字。
		- 分裂节点的中间关键字被提升到父节点中，以保持 B 树的平衡。
	4. **递归向上分裂**：如果父节点也因为接收新的关键字而变得过满，则同样需要进行分裂操作，并且继续向上递归，直到根节点。
	5. **创建新根节点**：如果根节点也被分裂，则创建一个新的根节点，其唯一的关键字是原根节点分裂时提升的中间关键字。

	![image-20231123210238965](./assets/image-20231123210238965.png)

	

4. B 树的删除

	​	在 B 树中，删除关键字分为两种情况：在终端结点中，以及不在终端结点中。

	​	当被删除的关键字 K 不在终端结点中的时候，需要找到该关键字的直接前驱，即左子树中的最大关键字，然后将找到的替代关键字替代 K 。

	![image-20231123224439776](./assets/image-20231123224439776.png)

	​	

	​	当被删除的关键字 K 在终端结点的时候，有三种情况：

	1. **直接删除**：如果该节点在删除关键字后仍保持有足够的关键字（即关键字数量不少于最小要求 $\lceil m/2 \rceil - 1$ 个，其中 $m$ 是 B 树的阶），那么可以直接删除关键字，无需进一步调整。

		

	2. **兄弟够借**：如果该节点的兄弟节点有足够的关键字（即关键字数量超过最小要求），则可以从兄弟节点借一个关键字。同时，需要调整父节点中的关键字来反映这种借用。

		![image-20231123224833042](./assets/image-20231123224833042.png)

		

	3. **兄弟不够借**：如果该节点及其所有兄弟节点都只有最小要求的关键字数，那么无法借用关键字。在这种情况下，需要将该节点与一个兄弟节点合并，并将一个父节点的关键字下移以填补合并后的节点。如果合并导致父节点关键字数量不足，可能需要递归向上调整。

		![image-20231123224846215](./assets/image-20231123224846215.png)

		

	

### 7.4.2 B+树的基本概念

​	B+树是一种自平衡的树数据结构，通常用于数据库和文件系统的索引和查找。它是B树的一个变种，具有以下特点：

1. **所有键值都出现在叶子节点**：在B+树中，所有的数据记录都存储在叶子节点中。这与B树不同，B树的数据可以存储在内部节点和叶子节点中。
2. **叶子节点之间的链表**：B+树的叶子节点通过指针相互连接，形成一个有序链表。这种结构使得范围查询变得非常高效，因为可以通过遍历链表来访问有序的数据。
3. **内部节点作为索引**：B+树的内部节点（非叶子节点）仅用作索引，它们包含了指向子节点的指针和键值的副本。这些键值作为分割点，指导搜索操作向下寻找正确的叶子节点。
4. **高效的搜索性能**：由于所有数据都在叶子节点上，且叶子节点是完全填充的，B+树可以提供非常高效的搜索性能。此外，由于内部节点仅存储键和子节点指针，它们可以拥有更多的子节点，从而减少树的高度。
5. **插入和删除操作**：B+树在插入和删除数据时，可能需要重新平衡。这通常涉及到节点的分裂或合并，以保持树的平衡。B+树的设计确保了这些操作的效率，同时保持了树的有序性。

![image-20231124222235244](./assets/image-20231124222235244.png)



## 7.5 哈希（散列）表

### 7.5.1 散列表的基本概念

​	散列函数：把查找表中的关键字映射成该关键字对应地址的函数，记为 Hash (Key) = Addr 。

​	散列函数可能会把两个或者两个以上的不同的关键字映射到同一地址，称这种情况为**冲突**，这些发生碰撞的不同关键字称为**同义词**。

​	散列表：根据关键字而直接进行访问的数据结构。散列表相当于建立了**关键字和存储地址之间的一种直接映射关系**。

​	理想情况下，对于散列表查找的时间复杂度应当是 $O(1)$ 。



### 7.5.2 散列函数的构造方法

1. **直接定址法**：

	- **原理**：直接使用键或者是键的线性函数作为散列地址。即，散列函数 $H(key) = key$ 或 $H(key) = a*key + b$，其中 a 和 b 是常数。
	- **适用场景**：适用于键的范围不大且分布均匀时，可以快速定位数据。
	- **优点**：简单，无冲突，查找速度快。
	- **缺点**：如果键的范围很大但实际键很少，会造成散列表空间的极大浪费。

2. **除留余数法**：

	- **原理**：取键被某个不大于散列表表长m的数p除后所得余数为散列地址。即，散列函数 $H(key) = key % p$，其中 p 通常为质数或不包含小于 20 的质因子的合数。
	- **适用场景**：适用于不知道键的分布，且不希望产生过多冲突的情况。
	- **优点**：实现简单，对于随机分布的键，分布较均匀。
	- **缺点**：选择不当的 p 值可能会增加冲突。

3. **数字分析法**：

	- **原理**：分析键的分布特征，从键中提取部分数字作为散列地址。
	- **适用场景**：适用于键的数字位分布不均匀的情况，例如某些位上数字变化小，而某些位上数字变化大。
	- **优点**：能够根据数据特性定制，减少冲突。
	- **缺点**：需要对数据特性有足够了解，实现相对复杂。

4. **平方取中法**：

	- **原理**：先取键的平方值，然后从平方值中提取中间几位作为散列地址。
	- **适用场景**：适用于键本身不均匀分布的情况。
	- **优点**：可以使得散列地址分布更加均匀。
	- **缺点**：计算相对复杂，且取中位数的位数选择对结果影响较大。

	

### 7.5.3 处理冲突的方法

1. 开放定址法

	所谓开放定址法，是指可存放新表项的空闲地址，既向他的同义词表项开放，有向它的非同义词表项开放。

	1. **线性探测法**：

		- **原理**：当发生冲突时，顺序探测表中的下一个位置，直到找到空位。
		- **优点**：实现简单。
		- **缺点**：容易产生“聚集”现象，即连续的位置被占用，导致插入和查找效率降低。

	2. **平方探测法**：

		- **原理**：在冲突时，探测的位置是原始位置的平方序列，即先探测原位置±1的平方，再探测原位置±2的平方，依此类推。
		- **优点**：相比线性探测，减少了聚集现象。
		- **缺点**：可能会出现“二次聚集”问题，且不一定能探测到所有的空位。

	3. **双散列法**：

		- **原理**：使用两个散列函数，当第一个散列函数产生冲突时，使用第二个散列函数确定探测序列。
		- **优点**：减少了聚集现象，提高了散列表的性能。
		- **缺点**：计算相对复杂，需要合理设计两个散列函数。

	4. **伪随机序列法**：

		- **原理**：使用伪随机数生成器产生探测序列。
		- **优点**：探测序列不固定，减少了聚集现象。
		- **缺点**：计算成本较高，且随机性可能导致性能不稳定。

		

2. 拉链法

	拉链法是另一种常用的解决散列冲突的方法，它将散列到同一个值的所有元素保留在一个链表中。

	![image-20231125152702457](./assets/image-20231125152702457.png)

	

### 7.5.4 散列查找及其性能分析

​	对于散列表的查找，首先利用散列函数查找对应位置上是否有记录，若无记录则返回查找失败。若有记录则确认是否是查找元素，是的话则返回成功，否则用处理冲突方法计算下一个散列地址，继续查找。

​	对于散列表来说，查找效率一般取决于三个因素：散列函数、处理冲突的方法和装填因子。其中装填因子 $\alpha$ 是：
$$
\alpha = \frac{表中记录数}{散列表长度}
$$
​	也就是说，散列表的 ASL 取决于 $\alpha$ ，$\alpha$ 越大，表示装填的越满，发生冲突的可能性越大。



------



# 第八章 排序

重点部分：

- 直接插入、折半插入、希尔排序
- 冒泡排序、快排
- 简单选择排序、堆排序
- 二路归并排序
- 基数排序
- 外部排序
- 排序算法的分析与运用

堆排序、快排、归并排序是重难点。对于常用排序算法要能熟练编写，对于特定序列能够选择最优算法。



## 8.1 排序的基本概念

### 8.1.1 排序的定义

​	排序算法的稳定性是指在排序过程中，具有相等键值的元素在排序前后的相对顺序不发生改变的特性。如果一个排序算法能保持任何两个相等元素的相对位置不变，则称这个算法是稳定的。

​	注意，对于不稳定的算法，只需要举出一组关键字的示例即可。



## 8.2 插入排序

### 8.2.1 直接插入排序

​	假设待排序的数组为 `arr`，其长度为 `n`。排序过程如下：

1. **初始状态**：将数组的第一个元素视为已经排好序的序列（只包含一个元素）。
2. **从第二个元素开始**：遍历数组中的每个元素（从 `arr[1]` 到 `arr[n-1]`）。
3. **插入操作**：
	- 将当前元素（记为 `current`）与已排序序列的最后一个元素比较。
	- 如果 `current` 较小，则继续向前比较，直到找到一个元素小于或等于 `current`，或者已经比较到了序列的第一个元素。
	- 将 `current` 插入到这个找到的位置之后。
4. **重复步骤 3**：对数组中的每个元素重复上述插入操作，直到整个数组排序完成。



​	例如，对数组 `[5, 3, 4, 1, 2]` 进行直接插入排序：

- 初始已排序序列：`[5]`
- 将 `3` 插入：比较 `3` 和 `5`，`3` 较小，插入到 `5` 前面，得到 `[3, 5]`
- 将 `4` 插入：比较 `4` 和 `5`，`4` 较小，插入到 `5` 前面，得到 `[3, 4, 5]`
- 将 `1` 插入：比较 `1` 和 `5`，`1` 较小，继续比较 `1` 和 `4`，`1` 较小，继续比较 `1` 和 `3`，`1` 较小，插入到 `3` 前面，得到 `[1, 3, 4, 5]`
- 将 `2` 插入：类似地，`2` 最终插入到 `1` 和 `3` 之间，得到 `[1, 2, 3, 4, 5]`

```C++
void InsertSort(ElemType A[], int n) {
    int i, j;
    // 外层循环：遍历数组中的每个元素（从第二个元素开始）
    for (i = 2; i <= n; i++) {
        // 如果当前元素小于其前一个元素，则需要进行插入操作
        if (A[i] < A[i - 1]) {
            // 将当前元素复制到哨兵位置（A[0]）
            A[0] = A[i];
            // 从后往前查找待插入位置
            for (j = i - 1; A[0] < A[j]; --j) {
                // 向后挪位，为插入操作腾出空间
                A[j + 1] = A[j];
            }
            // 将哨兵位置的元素（原A[i]）复制到找到的插入位置
            A[j + 1] = A[0];
        }
    }
}
```

​	直接插入排序是稳定的。它的时间复杂度为 $O(n^2)$，在数据量小或者部分数据已经有序的情况下效率较高。



### 8.2.2 折半插入排序

​	当排序表为顺序表的时候，可以对直接插入排序算法做如下改进：由于是顺序存储的线性表，所以查找有序子表的时候可以用折半查找来实现。确定待插入位置之后，可以统一的向后移动元素。

```C++
void InsertSort(ElemType A[], int n) {
    int i, j, low, high, mid;
    // 外层循环：遍历数组中的每个元素（从第二个元素开始）
    for (i = 2; i <= n; i++) {
        // 将当前元素暂存到A[0]（哨兵）
        A[0] = A[i];
        // 初始化折半查找的范围
        low = 1;
        high = i - 1;
        // 折半查找（二分查找）找到插入位置
        while (low <= high) {
            mid = (low + high) / 2;
            if (A[mid] > A[0]) {
                // 查找左半子表
                high = mid - 1;
            } else {
                // 查找右半子表
                low = mid + 1;
            }
        }
        // 统一后移元素，空出插入位置
        for (j = i - 1; j >= high + 1; --j) {
            A[j + 1] = A[j];
        }
        // 插入操作
        A[high + 1] = A[0];
    }
}

```



### 8.2.3 希尔排序

​	虽然直接插入排序的算法时间复杂度是 $O(n^2)$ ，但是当待排序序列是正序的时候，时间复杂度变为 $O(n)$ 。而希尔排序就是针对其更适用于”基本有序的排序表“以及”数据量不大“的特点改进而来的。

​	希尔排序的基本思想如下：

1. **间隔选择**：选择一个适当的间隔序列 $(h_1, h_2, ..., h_t)$，其中 $(h_t = 1)$（即最后一步是普通的插入排序）。常见的间隔序列有希尔原始序列（$$(N/2, N/4, ..., 1)$$）和Hibbard序列等。

2. **分组插入排序**：对于每个间隔 \($h_i$\)，将数组分为若干子序列，每个子序列的元素间隔为 \($h_i$\)。对每个子序列独立进行插入排序。

3. **逐步缩小间隔**：重复上述过程，逐步减小间隔 \($h_i$\)，直到最后间隔为1，即进行一次普通的插入排序。

![image-20231126091348666](./assets/image-20231126091348666.png)

```C++
void ShellSort(ElemType A[], int n) {
    int i, j, dk;
    // A[0]只是暂存单元,不是哨兵,当j <= 0时,插入位置已到
    // 步长变化
    for (dk = n / 2; dk >= 1; dk = dk / 2) {
        // 遍历所有的间隔序列
        for (i = dk; i < n; ++i) {
            // 需将A[i]插入有序增量子表
            if (A[i] < A[i - dk]) {
                A[0] = A[i]; // 暂存在A[0]
                // 记录后移，查找插入的位置
                for (j = i - dk; j >= 0 && A[0] < A[j]; j -= dk) {
                    A[j + dk] = A[j];
                }
                // 插入
                A[j + dk] = A[0];
            }
        }
    }
}

```

​	由于希尔排序只使用常数个辅助单元，因此空间复杂度为 $O(1)$ 。而希尔排序的时间复杂度约为 $O(n^{1.3})$，最坏情况下的时间复杂度为 $O(n^2)$。

​	希尔排序是一种不稳定的排序方法。且只适用于线性表为顺序存储的情况。

​	

## 8.3 交换排序

### 8.3.1 冒泡排序

​		冒泡排序的基本思想是通过重复遍历要排序的数列，比较相邻元素的值，如果它们的顺序错误就把它们交换过来。这个过程重复进行，直到没有再需要交换的元素为止，这时数列就被排序完成了。

具体步骤如下：

1. **比较相邻的元素**：从数列的开始，比较相邻两个元素的值。
2. **交换顺序**：如果第一个比第二个大（对于升序排序），就交换它们的位置。
3. **重复步骤1和2**：对每一对相邻元素做同样的工作，从开始第一对到结尾的最后一对。这步做完后，最后的元素会是最大的数。
4. **重复步骤1-3**：除了最后一个元素，重复步骤1到3，直到没有任何一对数字需要比较。

![image-20231126094051878](./assets/image-20231126094051878.png)

```C++
void BubbleSort(ElemType A[], int n) {
    int i, j;
    bool flag; // 用于标记本趟冒泡是否发生交换

    for (i = 0; i < n - 1; i++) { // 进行n-1趟冒泡
        flag = false; // 每趟冒泡开始前，设置flag为false

        // 一趟冒泡过程
        for (j = n - 1; j > i; j--) { // 从后向前，依次比较相邻两个元素
            if (A[j - 1] > A[j]) { // 若为逆序，则交换
                swap(A[j - 1], A[j]); // 交换两个元素
                flag = true; // 发生了交换，将flag设置为true
            }
        }

        // 本趟遍历后没有发生交换，说明表已经有序
        if (flag == false) {
            return; // 提前结束排序
        }
    }
}

```

​	虽然冒泡排序是一种简单直观的排序算法，但它在最坏的情况下和平均情况下都有较高的时间复杂度（$O(n^2)$），因此在处理大量数据时效率不是很高。冒泡排序由使用了常数个辅助单元，因此空间复杂度为 $O(1)$ 。

​	冒泡排序是一种稳定的算法。



### 8.3.2 快速排序

​	它的基本思想是“分治法”。快速排序的核心在于选择一个“基准”元素，然后围绕这个基准元素将数组分为两部分，一部分包含所有小于基准的元素，另一部分包含所有大于基准的元素。这个过程称为“划分”。然后，独立地对这两部分进行快速排序。整个过程可以递归地进行，直到整个序列变得有序。

​	快速排序的步骤通常包括：

1. **选择基准**：从数组中选择一个元素作为基准。这个选择可以是随机的，也可以是基于某种策略的（如选择中间元素或首尾元素的中点）。

2. **划分操作**：重新排列数组，使得所有小于基准的元素都在基准的左边，所有大于基准的元素都在基准的右边。在这个过程中，基准元素本身也找到了其最终位置。

3. **递归排序子数组**：递归地对基准左边和右边的子数组进行快速排序。

​	

```C++
// 快速排序函数
void QuickSort(ElemType A[], int low, int high) {
    if (low < high) { // 递归跳出的条件
        // Partition() 是划分操作，将数组 A[low…high] 划分为两个子数组
        int pivotpos = Partition(A, low, high); // 划分
        QuickSort(A, low, pivotpos - 1); // 递归排序左子数组
        QuickSort(A, pivotpos + 1, high); // 递归排序右子数组
    }
}

// 划分函数
int Partition(ElemType A[], int low, int high) {
    ElemType pivot = A[low]; // 将当前数组的第一个元素设为枢轴
    while (low < high) {
        while (low < high && A[high] >= pivot) 
            --high; // 将比枢轴小的元素移动到左端
        A[low] = A[high]; // 交换位置
        while (low < high && A[low] <= pivot) 
            ++low; // 将比枢轴大的元素移动到右端
        A[high] = A[low]; // 交换位置
    }
    A[low] = pivot; // 枢轴元素存放到最终位置
    return low; // 返回存放枢轴的最终位置
}

```

​	由于快速排序是递归的，需要借助递归工作栈来保存信息，其重量应当与递归调用的最大深度一直：最好的情况下是 $O(log_2n)$；最坏情况下因为要进行 $n-1$ 次递归调用，因此是 $O(n)$；平均情况下是 $O(log_2n)$ 。

​	快速排序的效率取决于划分的均匀程度。在最好的情况下，每次划分都将数组分为大小大致相等的两部分，这样可以达到最优的时间复杂度 $O(n log n)$。然而，在最坏的情况下（比如当数组已经有序或者每次选择的基准都是最小或最大元素时），快速排序的时间复杂度会退化为 $O(n^2)$ 。快速排序是所有内部排序算法中平均性能最好的排序算法。

​	快速排序算法是不稳定的。



## 8.4 选择排序

选择排序的基本思想是：每一趟排序都会选择最小的元素，作为子序列的元素，直到待排序元素只剩一个。选择排序是考察的重点。

### 8.4.1 简单选择排序

​	假设排序表为 $L[1...n]$，那么在每趟排序中都选择关键字最小的元素进行交换，这样每趟排序都可以确定一个元素的最终位置。因此经过 $n-1$ 次排序就可以使得整个排序表有序。

```C++
void SelectSort(ElemType A[], int n) {
    int i, j, min;
    for (i = 0; i < n - 1; i++) { // 外层循环，总共进行 n-1 趟
        min = i; // 初始化最小元素的位置为当前趟的起始位置
        for (j = i + 1; j < n; j++) { // 内层循环，在 A[i ... n-1] 中选择最小的元素
            if (A[j] < A[min]) {
                min = j; // 更新最小元素的位置
            }
        }
        if (min != i) {
            swap(A[i], A[min]); // 如果最小元素不在当前位置，则与起始位置交换
        }
        // swap() 函数通常会移动元素 3 次来完成交换操作
    }
}

```

​	因为简单选择排序算法仅使用常数个辅助单元，因此空间效率为 $O(1)$ 。而在整个过程中，元素移动的操作次数很少，不会超过 $3(n-1)$ 次，最好的情况是不移动；而元素间比较的次数始终是 $\frac{n(n-1)}{2}$ 次，因此时间复杂度始终是 $O(n^2)$ 。

​	简单选择排序是不稳定的。



### 8.4.2 堆排序

​	堆是一种完全二叉树，可以分为大根堆和小根堆。

- 大根堆：每个结点的值都 $\ge$ 它的子结点的值。这意味着根节点包含最大的元素。
- 小根堆：每个节点的值都 $\le$ 它的子结点的值。这一位置根节点包含最小的元素。

![image-20231126133858240](./assets/image-20231126133858240.png)

​	以大根堆为例，堆排序的思路很简单：首先将待排序序列建立成堆，此时堆顶元素就是最大值。然后输出堆顶元素后，通常将堆底元素送入堆顶。此时由于大根堆性质被破坏，因此需要进行调整。调整完毕后再输出堆顶元素。如此重复直到仅剩一个元素。

​	因此，堆排序需要解决的两个问题是：如何将无序序列构造成初始堆？如何将剩余元素调整成新的堆？

​	

​	首先是构造初始堆。

- 在数组表示中，如果数组长度为 $n$，则最后一个非叶子节点的位置是 $\frac{n}{2}$ 。从这个节点开始，向上逐个处理每个非叶子节点。
- 对于每个非叶子节点，比较它与其子节点的值。在大根堆中，如果子节点的值大于父节点的值，就将父节点与最大的子节点交换。
- 但是每次交换可能会破坏下一层的堆性质，因此每次交换后需要递归地对交换的子节点执行下沉操作，直到该节点的子节点都满足堆的性质。
- 重复上述过程，直到处理完数组中的第一个元素（堆的根节点）。这样，整个数组就被调整为一个大根堆。

![image-20231126135522065](./assets/image-20231126135522065.png)

```C++
// 堆排序中构建大根堆的函数
void BuildMaxHeap(ElemType A[], int len) {
    // 从最后一个非叶子节点开始，向上调整所有非叶子节点
    for (int i = len / 2; i > 0; i--) {
        HeadAdjust(A, i, len);
    }
}

// 调整函数，使以k为根的子树符合大根堆的性质
void HeadAdjust(ElemType A[], int k, int len) {
    // A[0]用于暂存子树的根节点
    A[0] = A[k];

    // 沿着节点k的较大的子节点向下筛选
    for (int i = 2 * k; i <= len; i *= 2) {
        // 选择较大的子节点
        if (i < len && A[i] < A[i + 1]) {
            i++;
        }

        // 如果根节点已经大于子节点，则停止筛选
        if (A[0] >= A[i]) break;

        // 否则，继续筛选
        A[k] = A[i];
        k = i;
    }

    // 将被筛选节点的值放入最终位置
    A[k] = A[0];
}

```

​	调整的时间与树高有关，为 $O(h)$ 。在建立含有 $n$ 个元素的堆的时候，关键字比较总次数不超过 $4n$ ，因此时间复杂度为 $O(n)$ 。

​	下面是堆排序算法：

```C++
// 堆排序函数
void HeapSort(ElemType A[], int len) {
    // 首先建立大根堆
    BuildMaxHeap(A, len);

    // 通过n-1趟的交换和重建堆的过程完成排序
    for (int i = len; i > 1; i--) {
        // 将堆顶元素（最大值）与堆底元素交换
        Swap(A[i], A[1]);

        // 调整剩余的i-1个元素，重新构建大根堆
        HeadAdjust(A, 1, i - 1);
    }
}

```



​	同样，堆也支持插入操作。对堆进行插入的时候，先将新结点放在堆的末端，在对这个结点向上进行调整。比如下图展示了大根堆的插入操作：

![image-20231126144359827](./assets/image-20231126144359827.png)



​	堆排序使用了常数个辅助单元，因此空间复杂度为 $O(1)$ 。由于建立初始堆的时间为 $O(n)$，然后又有 $n-1$ 次向下调整操作，因此在最好、最坏和平均情况下，其时间复杂度为 $O(nlog_2n)$ 。

​	堆排序是不稳定的。



## 8.5 归并排序、基数排序

### 8.5.1 归并排序

​	归并排序是一种分而治之的算法，其核心思想是将两个或两个以上的有序表合并成一个新的有序表。

​	假设待排序表有 n 个记录，那么就将其视为 n 个有序子表，然后两两归并排序...如此重复，直到得到一个长度为 n 的有序表为止。下图是一个二路归并排序的例子：

![image-20231126151155552](./assets/image-20231126151155552.png)

​	递归形式的二路归并算法是一句分治的，首先是将含有 $n$ 个元素的待排序表分成各含有 $n/2$ 个元素的子表，采用二路归并算法堆两个子表递归的排序，然后是合并两个已排序的子表。

```C++
void MergeSort(ElemType A[], int low, int high) {
    if (low < high) {
        // 找到中间位置
        int mid = (low + high) / 2;

        // 对左半部分进行递归排序
        MergeSort(A, low, mid);

        // 对右半部分进行递归排序
        MergeSort(A, mid + 1, high);

        // 合并两个有序序列
        Merge(A, low, mid, high);
    }
}

// Merge函数：合并两个有序子数组
void Merge(ElemType A[], int low, int mid, int high) {
    // B数组用于辅助合并
    ElemType *B = (ElemType *)malloc((high + 1) * sizeof(ElemType));

    // 将A中所有元素复制到B中
    for (int k = low; k <= high; k++) {
        B[k] = A[k];
    }

    int i, j, k;
    // i和j分别为两个子数组的起始位置，k为合并后数组的起始位置
    for (i = low, j = mid + 1, k = i; i <= mid && j <= high; k++) {
        // 比较B的左右两段中的元素，将较小值复制到A中
        if (B[i] <= B[j]) {
            A[k] = B[i++];
        } else {
            A[k] = B[j++];
        }
    }

    // 若第一个子数组未检测完，将剩余元素复制到A中
    while (i <= mid) {
        A[k++] = B[i++];
    }

    // 若第二个子数组未检测完，将剩余元素复制到A中
    while (j <= high) {
        A[k++] = B[j++];
    }

    // 释放B数组的内存
    free(B);
}

```

​	对于二路归并算法来说，辅助空间刚好为 n 个单元，因此空间复杂度为 $O(n)$。而每趟归并的时间复杂度为 $O(n)$，共需要进行 $log_2n$ 次归并，因此时间复杂度是 $O(nlog_2n)$ 。

​	由于 Merge() 并不会该边次序，因此二路归并算法是稳定的。



### 8.5.2 基数排序

​	基数排序是一种特别的排序算法，它基于关键字各位的大小进行排序。其原理是将整数按位数切割成不同的数字，然后按每个位数分别比较。由于整数也可以表示字符串（如电话号码）、日期等，基数排序也可以用来排序非整数数据。

​	基数排序的基本步骤如下：

1. **分配**：根据待排序列中元素的某一位（如个位、十位等），将所有元素分配到0-9共10个“桶”中。这个过程是稳定的，即相同的元素会保持原有的顺序关系。
2. **收集**：将这些桶中的元素按顺序收集起来，这时候元素是按照当前位数排序的。
3. **重复**：重复上述过程，对于每一位进行分配和收集。对于整数，先从个位开始，然后是十位、百位，直到最高位。

​	在基数排序中，一趟需要的辅助存储空间为 b ，但是因为以后的排序中会重复使用这个队列，因此其空间复杂度实际上为 $O(r)$ 。

​	基数排序的效率取决于待排序列的位数 $d$，它的时间复杂度是 $O(d*(n+b))$，其中 $n$ 是排序元素的个数，$b$ 是数字基数（例如，十进制数的基数是10）。

​	基数排序是稳定的。



## 8.6 各种内部排序算法的比较和应用

### 8.6.1 内部排序算法比较

​	在实际考察中，对于各类算法的比较是必考的。一般基于三个因素对比：时空复杂度、稳定性、算法的过程特征。

根据您提供的信息，我可以整理和校正这些排序算法的性质。请注意，您提供的数据中有一些错误或不准确之处，特别是在时间复杂度方面。以下是更准确的信息：

| 算法种类     | 最好情况     | 平均情况     | 最坏情况     | 空间复杂度 | 是否稳定 | 特征                 |
| ------------ | ------------ | ------------ | ------------ | ---------- | -------- | -------------------- |
| 直接插入排序 | $O(n)$       | $O(n^2)$     | $O(n^2)$     | $O(1)$     | 是       |                      |
| 冒泡排序     | $O(n)$       | $O(n^2)$     | $O(n^2)$     | $O(1)$     | 是       | 每趟排序都能产生最值 |
| 简单选择排序 | $O(n^2)$     | $O(n^2)$     | $O(n^2)$     | $O(1)$     | 否       |                      |
| 希尔排序     |              |              |              | $O(1)$     | 否       |                      |
| 快速排序     | $O(n log n)$ | $O(n log n)$ | $O(n^2)$     | $O(log n)$ | 否       |                      |
| 堆排序       | $O(n log n)$ | $O(n log n)$ | $O(n log n)$ | $O(1)$     | 否       | 每趟排序都能产生最值 |
| 2路归并排序  | $O(n log n)$ | $O(n log n)$ | $O(n log n)$ | $O(n)$     | 是       |                      |
| 基数排序     | $O(d(n+b))$  | $O(d(n+b))$  | $O(d(n+b))$  | $O(b)$     | 是       |                      |



### 8.6.2 内部排序算法应用

1. **小规模数据集**：
   - 当数据量较小（n较小）时，适合使用直接插入排序或简单选择排序。
   - 直接插入排序在记录移动次数上多于简单选择排序，因此当记录信息量较大时，推荐使用简单选择排序。

2. **基本有序的数据集**：
   - 如果文件的初始状态已经基本有序，直接插入排序或冒泡排序是较好的选择。

3. **大规模数据集**：
   - 对于较大的数据量（n较大），应考虑使用时间复杂度为 $O(nlogn)$ 的排序算法，如快速排序、堆排序或归并排序。
   - 快速排序在关键字随机分布的情况下平均时间最短，但它是不稳定的，且在最坏情况下性能下降。
   - 堆排序占用的辅助空间少于快速排序，并且避免了快速排序的最坏情况，但也是不稳定的。
   - 归并排序是稳定的，适用于要求稳定排序的场景。它可以与直接插入排序结合使用，先通过直接插入排序创建较长的有序子文件，然后进行归并。

4. **基于比较的排序算法的理论下限**：
   - 在基于比较的排序方法中，由于每次比较只有两种可能的结果，可以用二叉树描述比较过程。因此，可以证明任何基于比较的排序算法在随机分布的关键字情况下至少需要 $O(nlogn)$ 的时间。

5. **特殊情况下的排序选择**：
   - 当n非常大，且关键字位数较少并且可以分解时，基数排序是一个好的选择。
   - 当记录本身信息量较大，为避免大量的记录移动，可以使用链表作为存储结构，以减少移动开销。



## 8.7 外部排序

外部排序的算法比较复杂，不会考察算法设计，一般考察概念、方法和排序过程。

### 8.7.1 外部排序的基本概念

​	在需要对大文件进行排序的时候，需要涉及到内存和外存之间的交换。



### 8.7.2 外部排序的方法

​	外部排序通常采用归并排序法。因为在外部排序的过程中，涉及到磁盘的读写，因此最重要的是降低 I/O 次数。

![image-20231126163046606](./assets/image-20231126163046606.png)

​	在进行外部排序时，对于初始的r个归并段，如果执行k路平衡归并，归并过程可以用一个严格的k叉树来表示。这样的树只包含度数为k（即有k个子节点）和度数为0（即没有子节点）的节点。

1. **第一趟归并**：在第一趟归并中，可以将 $r$ 个初始归并段合并成 $[r/k]$ 个归并段，其中 $[r/k]$ 表示 $r$ 除以 $k$ 的向上取整结果。

2. **后续归并**：在随后的每一趟归并中，将 $m$ 个归并段合并成 $[m/k]$ 个归并段，直到最后形成一个大的归并段。

3. **归并趟数**：归并树的高度减 1 等于归并的趟数 $S$ ，即 $S = \lceil \log_k r \rceil$。这里 $\lceil \log_k r \rceil$ 表示对 $r$ 以 $k$ 为底的对数向上取整。

4. **优化策略**：通过增加归并路数k或减少初始归并段的个数r，可以减少归并的趟数S。这样做可以减少对磁盘的读写次数，从而提高外部排序的速度。



### 8.7.3 多路平衡归并与败者树

​	我们知道，增加归并路数 $k$ 能够减少归并次数 $S$。但是增加归并路数 $k$ 的时候，内部归并时间将增加。因此这将抵消由于减少 $k$ 带来的收益。因此，引入了败者树。

​	败者树是一种特殊的二叉树结构，主要用于高效地处理多路归并排序问题，尤其在外部排序中表现出色。它的核心思想是将多个排序序列的元素进行有效比较和选择，以确定当前最小（或最大）的元素。在败者树中，每个叶子节点代表一个排序序列中的当前元素，而内部节点则存储了所谓的“败者”的信息，即在比较过程中较大（或较小，取决于排序顺序）的元素的索引。

​	构建败者树时，首先将每个归并段的当前元素放入叶子节点。然后，通过比较叶子节点的值，逐级向上构建树，直到根节点。根节点最终指向所有叶子节点中值最小（或最大）的那个。每次从根节点提取元素后，相应的归并段会提供下一个元素，然后对树进行局部调整，以确保根节点始终指向当前最小（或最大）的元素。

​	

### 8.7.4 置换选择排序

​	从上面可以直到，减少初始归并段个数 $r$ 也可以减少归并次数 $S$ 。但是采用内部排序方法得到的各个初始归并段长度都相同，它依赖于内部排序时可用内存工作区的大小。因此，必须使用新的方法来产生更长的初始归并段。这就是置换-选择算法。

​	置换选择排序是一种用于生成初始归并段的有效方法，特别适用于外部排序。它的目标是在有限的内存空间中生成尽可能长的有序归并段，从而减少归并排序的总体趟数和磁盘I/O操作。



### 8.7.5 最佳归并树

​	文件经过置换选择排序之后，得到的是长度不等的初始归并段。这些归并段随后可以用于构建最佳归并树。通过置换选择排序，可以在有限的内存下生成尽可能长的归并段，这些归并段作为最佳归并树的叶子节点，从而减少总的归并次数。







