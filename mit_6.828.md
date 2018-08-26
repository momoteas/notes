# Mit_6.828 #

* starting on: Aug 26, 2018


### Lec 1 ###

---

* chap_1 the first process  - book-rev6

  * Paging hardware
    * PTEs: page table entries
    * An x86 page table is logically an array of 2^20 (1,048,576) page table entries(PTEs). Each PTE contains a 20-bit physical page number (PPN) and some flags. The paging hardware translates a virtual address by using its top 20 bits to index into the page table to find a PTE, and replacing those bits with the PPN in the PTE. The paging hardware copies the low 12 bits unchanged from the virtual to the translated physical address.
    * a page: 4096 (2^12) bytes

  * address space overview
    * Xv6 uses the paging hardware to give each process its own view of memory, called an address space
    * 

* lab 1

  * 这里先简单介绍一下地址的计算方法，在实模式下，指令中出现的地址都是采用

    　　　　**(段基址：段内偏移)**

    的形式的。其中这两个字段的值，通常是存放寄存器中的。其中段基址必须放在段寄存器中，包括CS(代码段), DS(数据段), SS(堆栈段), ES(扩展段)。不同的段寄存器存放的是你程序不同的段的起始地址

  * 数组/串处理指令

    * 80x86家族的处理器提供了几条与数组一起使用的指令。这些指令称为串处理指令。它们使用变址寄存器(ESI和EDI)来执行一个操作，然后这两个寄存器自动地进行增1或减1操作。FLAGS寄存器里的方向标志位(DF) 决定了这些变址寄存器是增加还是减少。有两条指令用来修改方向标志位：
      CLD 清方向标志位。这种情况下，变址寄存器是自动增加的。
      STD 置方向标志位。这种情况下，变址寄存器是自动减少的。

  * 这三个操作中涉及到两个新的指令out, in。这两个操作是用于操作IO端口的。这种IO端口的操作我们后面会经常接触到，这里大致说下。

    　  CPU与外部设备通讯时，通常是通过访问，修改设备控制器中的寄存器来实现的。那么这些位于设备控制器当中的寄存器也叫做**IO端口**。为了方便管理，80x86CPU采用IO端口单独编址的方式，即所有设备的端口都被命名到一个IO端口地址空间中。这个空间是独立于内存地址空间的。所以必须采用和访问内存的指令不一样的指令来访问端口。

     　 所以这里引入in，out操作：

    　      **in %al, PortAddress    向端口地址为PortAddress的端口写入值，值为al寄存器中的值**

    　　  out PortAddres,%al    把端口地址为PortAddress的端口中的值读入寄存器al中
