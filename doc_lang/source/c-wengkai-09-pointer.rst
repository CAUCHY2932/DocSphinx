9 翁恺C语言-指针
*************************


9-1-4 指针与数组
=====================





9-1-5 指针与const
=====================

指针的本质是一个指向一段内存的值

指针可以是const，值可以是const

指针是const
----------------

- 表示一旦得到某个变量的地址，不能再指向其他变量
  
  * int \*const q = &i; // q 是 const
  * \*q= 26; // ok
  * q++; // ERROR

所指的是 const
------------------

- 表示不能通过这个指针去修改那个变量（并不能使得那个变量成为const）
  
  - const int \*p = &i;
  - \*p = 26; // ERROR! (\*p) 是 const
  - i = 26; // ok
  - p = &j; // ok

分辨
-----------------

以下内容::

    int i;
    const int* p1 = &i;
    int const* p2 = &i;
    int *const P3 = &i;

判断哪个被const了的标志是const在*的前面还是后面

转换
-----------------


总是可以把一个非const的值转换成const的::

    void f(const int* x);
    int a = 15;
    f(&a); // ok
    const int b = a;

    f(&b); // ok
    b = a + 1; // ERROR

当要传递的参数的类型比地址大的时候，这是常用的手段；既能用比较少的字节数传递值给参数，又能避免函数对外面的变量的修改


const 数组
----------------

- const int a[] = {1, 2, 3, 4, 5};
- 数组变量已经是const的指针了，这里的const表明数组的每个单元都是const int
- 所以必须通过初始化进行赋值


保护数组值
----------------

- 因为把数组传入函数时，传递的是地址，所以那个函数内部可以修改数组的值
- 为了保护数组不被函数破坏，可以设置参数为const

  - int sum(const int a[], int length);

9-2-1 指针运算
==============


指针计算
-------------

- 这些算术运算可以对指针做

  - 给指针加、减一个整数(+, +=, -, -=)
  - 递增 ++, --
  - 两个指针相减

加减的都是指针指向的数据类型的sizeof字节数

\*p++
------------

- 取出p所指的那个数据来，完事之后顺便把p移到下一个位置去
- \*的优先级虽然高，但是没有++ 高
- 常用于数组类的连续空间操作
- 在某些CPU上，这可以直接被翻译成一条汇编指令

程序实例::

    #include <stdio.h>
    int main()
    {
        char ac[] = {0, 1, 2, 3, 4, 5, 6, 9, -1};
        char *p = &ac[0];
        int i;
        for (i = 0; i < sizeof(ac)/ sizeof(ac[0]); i++) {
            printf("%d", ac[i]);
        }

        for (p = ac; *p != -1; ){
            printf("%d\n", *p++);
        }

        // 哨兵
        while (*p != -1){
            printf("%d\n", *p++);
        }
        return 0;
    }


指针比较
------------

- <, <=, ==, >, >= != 都可以对指针做
- 比较他们在内存中的地址
- 数组中的单元的地址肯定是线性递增的


0地址
------------


- 当然你的内存中有0地址，但是0地址通常是个不能随便碰的地址
- 所以你的指针不应该具有0值
- 因此你可以用0地址表示特殊的事情

  - 返回的指针是无效的
  - 指针没有被真正初始化（先初始化为0）
- NULL是一个预定定义的符号，表示0地址

  - 有的编译器不愿意你用0来表示0地址


指针的类型
-----------


- 无论指向什么类型，所有的指针的大小都是一样的，因为都是地址
- 但是指向不同类型的指针是不能直接互相赋值的
- 这是为了避免用错指针

实例::

    int ai[] = {1, 2, 3};
    int *p = ai;

    char ac[] = {1, 2, 3};
    char *q = ac;

    p = q; // ERROR



指针的类型转换
----------------

- void* 表示不知道指向什么东西的指针

  - 计算时，与 char* 相同（但不相通）

- 指针也可以转换类型

  - int *p = &i; void* q = (void* )p;

- 这并没有改变p所指的变量的类型，而是让后人用不同的眼光通过p看它所指的变量

  - 我不再当你是int啦，我认为你是个void!

9-2-2 动态内存分配
====================


- 如果输入数据，先告诉你个数，然后再输入，要记录每个数据
- C99 可以用变量做数组定义的大小，C99 之前呢
- int \*a = (int \*)malloc(n \*sizeof(int));

man malloc 实例::

    MALLOC(3)                BSD Library Functions Manual                MALLOC(3)

    NAME
        calloc, free, malloc, realloc, reallocf, valloc -- memory allocation

    SYNOPSIS
        #include <stdlib.h>

        void *
        calloc(size_t count, size_t size);

        void
        free(void *ptr);

        void *
        malloc(size_t size);

        void *
        realloc(void *ptr, size_t size);

        void *
        reallocf(void *ptr, size_t size);

        void *
        valloc(size_t size);

    DESCRIPTION
        The malloc(), calloc(), valloc(), realloc(), and reallocf() functions allocate memory.  The allocated memory is aligned such that it can
        be used for any data type, including AltiVec- and SSE-related types.  The free() function frees allocations that were created via the
        preceding allocation functions.

        The malloc() function allocates size bytes of memory and returns a pointer to the allocated memory.

        The calloc() function contiguously allocates enough space for count objects that are size bytes of memory each and returns a pointer to
        the allocated memory.  The allocated memory is filled with bytes of value zero.

        The valloc() function allocates size bytes of memory and returns a pointer to the allocated memory.  The allocated memory is aligned on a
        page boundary.

        The realloc() function tries to change the size of the allocation pointed to by ptr to size, and returns ptr.  If there is not enough
        room to enlarge the memory allocation pointed to by ptr, realloc() creates a new allocation, copies as much of the old data pointed to by
        ptr as will fit to the new allocation, frees the old allocation, and returns a pointer to the allocated memory.  If ptr is NULL,
        realloc() is identical to a call to malloc() for size bytes.  If size is zero and ptr is not NULL, a new, minimum sized object is allo-
        cated and the original object is freed.  When extending a region allocated with calloc(3), realloc(3) does not guarantee that the addi-


程序实例::

    #include <stdio.h>
    #include <stdlib.h>

    int main() 
    {
        int number;
        int* a;
        printf("输入数量:");
        scanf("%d", &number);

        // int a[number];
        a = (int *)malloc(number*sizeof(int));
        
        for (i =0; i< number; i++) {}
            scanf("%d", &a[i]);
        }

        for (i=number-1;i<=0; i--) {
            printf("%d\n", a[i]);
        }
        free(a);
        return 0;
    }


malloc
----------



#include <stdlib.h>

void* malloc(size_t size);

- 向malloc 申请的空间的大小是以字节为单位的
- 返回的结果是void\*，需要类型转换为自己需要的类型
- (int \*)malloc(n \* sizeof(int))

没空间了
----------

- 如果申请失败啧返回0，或者叫做NULL
- 你的系统能给你多大的空间？

实例如下::

    #include <stdio.h>
    #include <stdlib.h>

    int main()
    {

        void *p;
        int cnt =0;

        while((p=malloc(100*1024*1024))) {
            cnt++;
        }
        printf("分配了%d00MB的空间\n", cnt);

        return 0;
    }



free
----------

- 把申请得来的空间还给『系统』
- 申请过的空间，最终都是要还的
- 只能还申请来的空间的首地址
- free(NULL) 不会报错

常见问题
-----------

- 申请了没free 长时间运行内存逐渐下降
  
  - 新手：忘了
  - 老手：找不到合适的时机

- 解决方法：

  - malloc 必须free
  - 找好时机

- free 过了再去free
- 地址变过了，直接去free



