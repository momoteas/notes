# The C Programming Language #

* reading on Aug 27, 2018
* IDE: Dev-C++
* tool: man func_name in Linux to check function details



### chap 5  Pointers and Arrays ###

----

* 5.1 Pointers and Addresses

  * A pointer is a group of cells (often two or four) that can hold an address;

  * The & operator only applies to objects in memory: variables and array elements. It cannot be applied to expressions, constants, or register variables;

  * The unary operator * is the indirection or dereferencing operator; when applied to a pointer, it
    accesses the object the pointer points to

  * a "pointer to void'' is used to hold any type of pointer but cannot be dereferenced itself.

  * The unary operators * and & bind more tightly than arithmetic operators, so the assignment
    y = *ip + 1
    takes whatever ip points at, adds 1, and assigns the result to y;


* 5.2 Pointers add Function Arguments
  * Since C passes arguments to functions by value, there is no direct way for the called function
    to alter a variable in the calling function.

* 5.3 Pointers and Arrays
  * The notation a[i] refers to the i-th element of the array. If pa is a pointer to an integer, declared as
    int *pa;
    then the assignment
    pa = &a[0];
    sets pa to point to element zero of a; that is, pa contains the address of a[0].
  * If pa points to a particular element of an array, then by definition pa+1 points to the next element, pa+i points i elements after pa, and pa-i points i elements before. Thus, if pa points to a[0],
    *(pa+1)
    refers to the contents of a[1], pa+i is the address of a[i], and *(pa+i) is the contents of a[i].
  * the name of an array is a synonym for the location of the initial element, the assignment pa=&a[0] can also be written as 
    pa = a;
  * There is one difference between an array name and a pointer that must be kept in mind. A pointer is a variable, so pa=a and pa++ are legal. But an array name is not a variable; constructions like a=pa and a++ are illegal

* 5.4 Address Arithmetic
  * 

* 5.5 Character Pointers and Functions
  * If pmessage is declared as
    char *pmessage;
    then the statement
    pmessage = "now is the time";
    assigns to pmessage a pointer to the character array. This is not a string copy; only pointers
    are involved
  * A string constant, written as
    "I am a string"
    is an array of characters. In the internal representation, the array is terminated with the null
    character '\0' so that programs can find the end.

----

### Others

* typedef, struct:

  ```
  #include <stdio.h>
  #include <string.h>
   
  typedef struct Books
  {
     char  title[50];
     char  author[50];
     char  subject[100];
     int   book_id;
  } Book;
   
  int main( )
  {
     Book book;
   
     strcpy( book.title, "C 教程");
     strcpy( book.author, "Runoob"); 
     strcpy( book.subject, "编程语言");
     book.book_id = 12345;
   
     printf( "书标题 : %s\n", book.title);
     printf( "书作者 : %s\n", book.author);
     printf( "书类目 : %s\n", book.subject);
     printf( "书 ID : %d\n", book.book_id);
   
     return 0;
  }
  ```

* typedef vs #define

  * **#define** 是 C 指令，用于为各种数据类型定义别名，与 **typedef** 类似，但是它们有以下几点不同：

    - **typedef** 仅限于为类型定义符号名称，**#define** 不仅可以为类型定义别名，也能为数值定义别名，比如您可以定义 1 为 ONE。
    - **typedef** 是由编译器执行解释的，**#define** 语句是由预编译器进行处理的。

  * ```
    #include <stdio.h>
     
    #define TRUE  1
    #define FALSE 0
     
    int main( )
    {
       printf( "TRUE 的值: %d\n", TRUE);
       printf( "FALSE 的值: %d\n", FALSE);
     
       return 0;
    }
    ```



* \r, \n
  * 回车符是光标从当前位置回到本行的行首, C语言中是'\r' 
  * 换行符是光标从当前位置换到下一行, C语言中是'\n' 
  * 回车换行符实际是两个字符, 就是\r\n



* sizeof
  * 计算数据类型的长度，以字节为单位
  * sizeof(int)