# 语言学习

## 一、基础

#### 基础命令

​		预处理器指令

​		#include<stdio.h>

​		主函数

​		int main(){

​		显示消息

​			printf("hello world");

​		终止 main() 函数，并返回值 0

​			return 0;

​			}

base on B,for unix系统

最新的的C语言标准:C11

#### 基础语法

##### 	令牌

关键词、标识符、常量、字符串值、符号

​	printf("hello world! \n");   五个令牌

##### 	变量

​		变量定义就是告诉编译器在何处创建变量的存储，以及如何创建变量的存储

​		带有静态存储持续时间的变量会被隐式初始化为 NULL（所有字节的值都是 0），其他所有变量的初始值是未定义的。	

```cc
注意
extern int i; //声明，不是定义  不需要建立存储空间的
int i; //声明，也是定义   已经建立了存储空间。
```

##### **变量的内存寻址(**

​		(1)内存寻址由小到大，优先分配内存地址比较小的字节给变量，所以说变量越先定义，内存地址就越小。变量如果没有初始化，默认输出为 0。

​		(2)变量地址的获取方式：& 变量名。

​		(3)输出地址的方式：%p。

(4)一个变量一定要先初始化才可以使用，因为 c 语言中默认一个没有初始化的变量值是一个不可知的很大值

##### 常量

**	#define** 是宏定义，它不能定义常量，但宏定义可以实现在字面意义上和其它定义常量相同的功能，本质的区别就在于 **#define** 不为宏名分配内存，而 **const** 也不为常量分配内存，怎么回事呢，其实 **const** 并不是去定义一个常量，而是去改变一个变量的存储类，把该变量所占的内存变为只读！

##### static

**	static** 存储类指示编译器在程序的生命周期内保持局部变量的存在，而不需要在每次它进入和离开作用域时进行创建和销毁。因此，使用 static 修饰局部变量可以在函数调用之间保持局部变量的值。``

​	static 修饰符也可以应用于全局变量。当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内。

​	局部生命周期是否外面也可以调用

# 函数

##### 按引用：

​	通过引用传递方式，形参为指向实参地址的指针，当对形参的指向操作时，就相当于对实参本身进行的操作

# 数组

​	所有的数组都是由连续的内存位置组成。最低的地址对应第一个元素，最高的地址对应最后一个元素。

int function(int *pram) 等价  int function(int pram[])

##### C 从函数返回数组

​	C 语言不允许返回一个完整的数组作为函数的参数。但是，您可以通过指定不带索引的数组名来返回一个指向数组的指针.

​	int * myFunction()

​	C 不支持在函数外返回局部变量的地址，除非定义局部变量为 **static** 变量

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
/* 要生成和返回随机数的函数 */
int * getRandom( )
{
  static int  r[10];
  int i;
 
  /* 设置种子 */
  srand( (unsigned)time( NULL ) );
  for ( i = 0; i < 10; ++i)
  {
     r[i] = rand();
     printf( "r[%d] = %d\n", i, r[i]);
 
  }
 
  return r;
}
 
/* 要调用上面定义函数的主函数 */
int main ()
{
   /* 一个指向整数的指针 */
   int *p;
   int i;
 
   p = getRandom();
   for ( i = 0; i < 10; i++ )
   {
       printf( "*(p + %d) : %d\n", i, *(p + i));
   }
 
   return 0;
}
```

##### C 指向数组的指针

### 枚举

​	 c 语言中枚举元素的数据类型是被当成了 int 或者 unsigned int 型，不会是其他数据类型，如浮点型。

# C 指针

​	每一个变量都有一个内存位置，每一个内存位置都定义了可使用连字号（&）运算符访问的地址

```cc
int  var1;
"var1 变量的地址： %p\n", &var1 
```

​	**指针**是一个变量，其值为另一个变量的地址，即，内存位置的直接地址

```cc
int    *ip;    /* 一个整型的指针 */
double *dp;    /* 一个 double 型的指针 */
float  *fp;    /* 一个浮点型的指针 */
char   *ch;     /* 一个字符型的指针 */
```

​	不同数据类型的指针之间唯一的不同是，指针所指向的变量或常量的数据类型不同。都是一个代表内存地址的长的十六进制数。

```c
#include <stdio.h>
 
int main ()
{
   int  var = 20;   /* 实际变量的声明 */
   int  *ip;        /* 指针变量的声明 */
   // 除数组之外需要var取得地址
   ip = &var;  /* 在指针变量中存储 var 的地址 */
 
   printf("Address of var variable: %p\n", &var  );
 
   /* 在指针变量中存储的地址 */
    // 指针的不要&取地址
   printf("Address stored in ip variable: %p\n", ip );
 
   /* 使用指针访问值 */
   printf("Value of *ip variable: %d\n", *ip );
 
   return 0;
}
```

##### 函数指针

​	函数指针是指向函数的指针变量

```
int max(int x, int y)
int (* p)(int, int) = & max; // &可以省略
```

##### 回调函数

​		函数指针作为某个函数的参数

​		函数指针变量可以作为某个函数的参数来使用的，回调函数就是一个通过函数指针调用的函数。

##### 函数指针和指针函数的区别

​	1  指针函数是指带指针的函数，即本质是一个函数。函数返回类型是某一类型的指针。

​		**注意：**指针函数一定有函数返回值，函数返回值必须用同类型的指针变量来接受

​	2  函数指针是指向函数的指针变量，即本质是一个指针变量

### 字符串

​	字符串实际上是使用 **null** 字符 '\0' 终止的一维字符数组

```c
//如果没有在字符数组最后增加 \0 的话输出结果有误：
char str[] = {'I','a','m','h','a','p','p','y','\0'};
//在使用不定长数组初始化字符串时默认结尾为 \0
char str[] = "I am happy";
char str[] = {"I am happy"};
//(注意指针不能直接赋给数组)
char *str;
str = "I love China";
```

##### **strlen 与 sizeof的区别：**

strlen 是函数，sizeof 是运算操作符，二者得到的结果类型为 size_t，即 unsigned int 类型。

sizeof 计算的是变量的大小，以 **\0** 作为长度判定依据

而 strlen 计算的是字符串的长。不受字符 **\0** 影响；

## C 结构体

[结构体](https://www.runoob.com/cprogramming/c-structures.html)	

C 数组允许定义可存储相同类型数据项的变量，**结构**是 C 编程中另一种用户自定义的可用的数据类型，它允许您存储不同类型的数据项。

c比c++多了一个在使用的时候还需要加struct

结构体名字不代表指针

#### **typedef 与 #define 的区别**

1）#define可以使用其他类型说明符对宏类型名进行扩展，但对 typedef 所定义的类型名却不能这样做。

## 排序

![image-20200706103834220](E:\c语言\image-20200706103834220.png)

### 交换排序

##### 冒泡排序

```c
void bubble_sort(int arr[],int size) {
    //每一次交换的次数
    for (int i = 0; i < size-1; i++) {
        // 交换比较
        for (int j = 0; j < size-1-i; j++) {

            if (arr[j] > arr[j + 1]) {
                int mid = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = mid;
            }

        }
    }
}
```

在相邻元素相等时，它们并不会交换位置，所以，冒泡排序是稳定排序。

算法复杂度较高，在数据量大的时候不适合使用

数据完全有序 O(n)    其他情况下，几乎总是O( n2 )

改进：增加一个`swap`的标志

##### 选择排序

​	认为选择排序是冒泡排序的一种改进

1. 在未排序序列中找到最小（大）元素，存放到排序序列的起始位置

2. 从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。

3. 重复第二步，直到所有元素均排序完毕。

   ```c
   void bubble_sort(int arr[],int size) {
   
       for (int i = 0; i < size - 1; i++) {
           int m=i;
           for (int j = i+1; j < size; j++) {
               if (arr[j] < arr[m]) {
                   m = j;
               }
           }
           if(i!=m){
           int mid = arr[i];
           arr[i] = arr[m];
           arr[m] = mid;
               }
     }  
   }    
   
   ```

   选择排序不稳定：A 80 B 80 C 70 

   固有的O(n2)复杂度

   ### 插入排序

   ##### 直接插入排序

   ​	工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入

   1. 把待排序的数组分成已排序和未排序两部分，初始的时候把第一个元素认为是已排好序的。
   2. 从第二个元素开始，在已排好序的子数组中寻找到该元素合适的位置并插入该位置。
   3. 重复上述过程直到最后一个元素被插入有序子数组中

   ​	

   ```c
   void bubble_sort(int arr[],int size) {
   
       for (int i = 1; i < size; i++) {
           int var = arr[i];
           int pos = i;
           while (pos > 0 && arr[pos - 1] > var) {
               arr[pos] = arr[pos - 1];
               pos--;
           }
           arr[pos] = var;
      }
   }
   ```

   ​	直接插入排序是稳定的排序方法

   ​	O( n2 )的复杂度

   ​	一般做为快速排序的扩充。

   ##### 希尔排序

   1. 插入排序算法在数组基本有序的情况下，可以近似达到O(n)复杂度，效率极高。
   2. 但插入排序每次只能将数据移动一位，在数组较大且基本无序的情况下性能会迅速恶化

##### **快速排序**

https://wiki.jikexueyuan.com/project/easy-learn-algorithm/fast-sort.html

1. 从数列中挑出一个元素，称为"基准"（pivot），

2. 重新排序数列，所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面（相同的数可以到任何一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。

3. 递归地（recursively）把小于基准值元素的子数列和大于基准值元素的子数列排序。

   ```java
   public static void quickSort(int[] arr){
       qsort(arr, 0, arr.length-1);
   }
   private static void qsort(int[] arr, int low, int high){
       if (low >= high)
           return;
       int pivot = partition(arr, low, high);        //将数组分为两部分
       qsort(arr, low, pivot-1);                   //递归排序左子数组
       qsort(arr, pivot+1, high);                  //递归排序右子数组
   }
   private static int partition(int[] arr, int low, int high){
       int pivot = arr[low];     //基准
       while (low < high){
           while (low < high && arr[high] >= pivot) --high;
           arr[low]=arr[high];             //交换比基准大的记录到左端
           while (low < high && arr[low] <= pivot) ++low;
           arr[high] = arr[low];           //交换比基准小的记录到右端
       }
       //扫描完成，基准到位
       arr[low] = pivot;
       //返回的是基准的位置
       return low;
   }
   ```

   ​	快速排序并不是稳定的

   ​	尤其在数据量大的时候性能优越性更加明显。但是在必要的时候，需要考虑下优化以提高其在最坏情况下的性能。

### 选择排序

##### 堆排序

```java
public class ArrayHeap {
    private int[] arr;
    public ArrayHeap(int[] arr) {
        this.arr = arr;
    }
    private int getParentIndex(int child) {
        return (child - 1) / 2;
    }
    private int getLeftChildIndex(int parent) {
        return 2 * parent + 1;
    }
    private void swap(int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
    /**
     * 调整堆。
     */
    private void adjustHeap(int i, int len) {
        int left, right, j;
        left = getLeftChildIndex(i);
        while (left <= len) {
            right = left + 1;
            j = left;
            if (j < len && arr[left] < arr[right]) {
                j++;
            }
            if (arr[i] < arr[j]) {
                swap(array, i, j);
                i = j;
                left = getLeftChildIndex(i);
            } else {
                break; // 停止筛选
            }
        }
    }
    /**
     * 堆排序。
     * */
    public void sort() {
        int last = arr.length - 1;
        // 初始化最大堆
        for (int i = getParentIndex(last); i >= 0; --i) {
            adjustHeap(i, last);
        }
        // 堆调整
        while (last >= 0) {
            swap(0, last--);
            adjustHeap(0, last);
        }
    }

}
```

​	属于不稳定的排序算法

​	堆排序在建立堆和调整堆的过程中会产生比较大的开销，在元素少的时候并不适用

##### 归并排序

​	采用分治法的一个非常典型的应用。将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。若将两个有序表合并成一个有序表，称为2-路归并

# Huffman算法

​	[【算法】赫夫曼树（Huffman）的构建和应用（编码、译码）](https://www.cnblogs.com/penghuwan/p/8308324.html)https://www.cnblogs.com/penghuwan/p/8308324.html

# 数据结构

​	c++中栈队列堆链表的库文件以及相关操作

前序 中序 后序遍历c++实现

bfs和dfs

## 线性表

​	定义结构存储

c++中线性表库文件

## 顺序表

## 栈

### 顺序栈

栈的几个应用操作

链式栈

## 顺序搜索

顺序表中搜索

#### 折半搜索

有序顺序表 O(log2n)

### 动态搜索

#### BST  **二叉搜索树** **二叉排序树**

<img src="E:\c语言\image-20200709214925466.png" alt="image-20200709214925466" style="zoom:80%;" />

中序遍历该树可以按从小到大的顺序将各个结点的关键值排列起来，所以**BST也叫二叉排序树**

**搜索**

【思想】假设需要查找关键值为 k的元素，先从根开始。如果根为空，那么搜索树不包含任何元素，查找失败，否则将 k与根的关键值相比较：
如果 k小于根节点的关键值，则只需在左子树中搜索即可；
如果 k大于根节点的关键值，则只需在右子树中搜索即可；
如果 k等于根节点的关键值，则查找成功，搜索终止！

**时间复杂性为****O(h)** h为树得高度

输入的顺序导致bst的构造不一样

**对于有** **n** **个关键码的集合，其关键码有** **n!种不同排列，可构成不同二叉搜索树有**

​                      

​                         ![image-20200709220110908](E:\c语言\image-20200709220110908.png)

二叉搜索树的搜索、插入和删除的平均时间复杂度为O( log2n)

## 图

#### 存储

​	邻接矩阵 a【i】【j】=1

​    邻接表：n个单链表

​	多邻接表

 图的遍历：宽搜和深搜

<img src="E:\c语言\image-20200709222703836.png" alt="image-20200709222703836" style="zoom:80%;" />

<img src="E:\c语言\image-20200709222724558.png" alt="image-20200709222724558" style="zoom:80%;" />

#### Kruskal 算法： 克鲁斯卡尔

选择n-1条边；
【贪婪准则】
         从剩下的边中选择一条不会产生环路的具有最小耗费的边加入已选择的边的集合中。

​	不断找权值最小的加入其中

#### Prim算法

每次选择多条边来创建最小生成树，
选择下一条边的【贪婪准则】：从剩下的边中选择一条耗费最小的边，并且它的加入应使所有入选的边仍是一棵树。
【注意】可从任一顶点开始，往 T中加入一条代价最小的边(u,v)，使T与(u,v)的并仍是一棵树

##### Kruskal VS. Prim

prim算法只与网中节点数相关，适用于边稠密的网络。
Kruskal算法与网中边数相关，不仅适合于边稠密的情形，也适合于边稀疏的情形。
注意：当各边有相同权值时，由于选择的随意性，产生的生成树可能不唯一

####  Dijkstra

提出按各条最短路径长度递增的顺序逐步产生最短路径。

- 首先求出从源点v0到其余各顶点中长度最短的一条
- 然后参照它求出长度次短的一条最短路径，
- 依此类推，直到从源点v0到其余各顶点的最短路径全部求出为止。