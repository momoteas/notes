# The C Programming Language #

* reading on Aug 27, 2018



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

