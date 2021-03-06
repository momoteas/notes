# Assembly  #

* book: PC Assembly Language	-- Paul Carter
* Reading on: Aug 25, 2018



### chap 1 简介 ###

---

* chap 1:

  * 8086 16位寄存器:

    * 两个16位指针寄存器：SI 和DI 。通常它们都是当作指针来使用;

    * 16位BP和SP 寄存器用来指向机器语言堆栈里的数据，被各自称为基址寄存器和堆栈指针寄存器

    * 16位CS，DS，SS 和ES 寄存器是段寄存器。它们指出程序不同部分所使用的内存。CS代表代码段，DS 代表数据段，SS 代表堆栈段和ES代表附加段。ES当作一个暂时段寄存器来使用
    * 指令指针寄存器(IP) 与CS寄存器一起使用来跟踪CPU下一条执行指令的地址。通常，当一条指令执行时，IP提前指向内存里的下一条指令。
    * FLAGS寄存器储存了前面指令执行结果的重要信息。这些结果在寄存器里以单个的位储存;

  * 80386 32位寄存器:

    * 在80386里，段寄存器依然是16位的。这儿有两个新的段寄存器：FS和GS。它们名字并不代表什么。它们是附加段寄存器(像ES一样);

  * 实模式:

    * 偏移地址表示的物理地址可以由下面的公式计算：16 * selector + offset

  * 16位保护模式:
    * 保护模式使用了一种叫做虚拟内存的技术。虚拟内存的基本思想是仅仅保存程序现在正在使用的代码和数据到内存中。其它数据和代码暂时储存在硬盘中直到它们再次需要时
    * 在保护模式下，每一段都分配了一条描述符表里的条目。这个条目拥有系统想知道的关于这段的所有信息。这些信息包括：现在是否在内存中；如果在内存中，在哪；访问权限(例如： 只读)。段的条目的指针是储存在段寄存器里的段地址值

  * 32位保护模式:

    * 段可以分成较小的4K大小的单元，称为内存页。虚拟内存系统工作在页的方式下，代替了段方式。这就意味着一段在任何一个时刻只有部分可能在内存中。在28616位保护模式下，要么整个段在内存中，要么整个不在。这样在32位模式下允许的大的段的情况下很不实用。

  * 中断：
    * 每种类型的中断都分配了一个中断号。在物理内存的开始处，存在一张包含中断处理程序段地址的中断向量表。中断号是这张表中最基本的指针

    * 外部中断由CPU的外部引起。(鼠标就是这一类型的例子。)许多I/O设备引起中断(例如：键盘，时钟，硬盘驱动器，CD-ROM和声卡)。内部中断由CPU的内部引起，要么是由一个错误引起，要么由中断指令引起。错误中断称为陷阱。由中断指令引起的中断称为软中断

    * 许多中断处理程序当它执行完成时，将控制权返回给被中断的程序。它们恢复寄存器，里面的值与中断发生之前的值相同。因此，被中断的程序就像没有任何事情发生一样运行(除了它失去了一些CPU周期)。陷阱通常不返回。通常它们中止程序


  * 1.3 汇编语言

    * 1.3.3 指令操作数
      * 机器代码指令拥有个数和类型不同的操作数；然而，通常每个指令有几个固定的操作数(0到3个)。操作数可以有下面的类型：寄存器，内存，立即数，暗指的操作数

    * 1.3.4 基本指令
      * mov dest (目的操作数), src(源操作数)
      * 一个指令的两个操作数不能同时是内存操作数。这就指出了一个汇编古怪的地方。
      * add, inc, dec,

    * 指示符
      * 指示符是由汇编程序产生的而不是由CPU产生。它们通常用来要么指示汇编程序做什么要么提示汇编程序什么。它们并不翻译成机器代码。指示符普遍的应用有：
        ² 定义常量
        ² 定义用来储存数据的内存
        ² 将内存组合成段
        ² 有条件地包含源代码
        ² 包含其它文件
      * NASM 的预处理的指示符以%开头
      * equ指示符可以用来定义一个符号。符号被命名为可以在汇编程序里使用的常量。格式是：symbol equ value
      * %define 指示符, 这个指示符和C中的#define非常相似。它通常用来定义一个宏常量，像在C里面一样。%define SIZE 100
      * 数据指示符使用在数据段中用来定义内存空间。保留内存有两种方法。第一种方法仅仅为数据定义空间；第二种方法在定义数据空间的同时给与一个初始值。第一种方法使用RESX指示符中的一个。X可由字母替代，字母由需要储存的对象的大小来决定。表1.3给出了可能的值。第二种方法(同时定义一个初始值)使用DX指示符中的一个。X可以由字母替代，字母的值与RESX里的值一样
      * 记住变量可以用来表示代码中的数据。变量的使用方法有两种。如果一个平常的变量被使用了，它被解释为数据的地址(或偏移)。如果变量被放置在方括号([])中，它就被解释为在这个地址中的数据

    * 1.3.6 输入和输出
      * 汇编语言不提供标准库。它们必须要么直接访问硬件(在保护模式下为特权级操作)或使用任何操作系统提供的底层的程序。
      * CALL指令等价于在高级语言里的函数call。它跳转到代码的另一段去执行，然后等程序执行完成后又回到原始的地方。

    * 1.3.7 调试

      * 宏可以像普通的指令一样使用。宏的操作数由逗号隔开。


  * 1.4 创建一个程序
    * 四个调试程序称为dump regs，dump mem，dump stack和dump math；它们分别显示寄存器，内存，堆栈和数字协处理器的值
    * 连接是一个将在目标文件和库文件里的机器代码和数据结合到一起产生一个可执行文件的过程





### chap 2 基本汇编语言 ###

---

* 2.1 整形工作方式

  * 2.1.1 整形表示法

    * 所有的方法都把整形的最大有效位当作一个符号位来使用。如果数为正数，则这一位为0；为负数，这一位就为1
    * 补码
      现代的电脑使用第三种方法称为补码表示法。一个数的补码可以由下面两步得到：
      1. 找到该数的反码
      2. 将第一步的结果加1

    * 汇编语言并没有类型的概念，而高级语言有。数据解释成什么取决于使用在这个数据上的指令。到底十六进制数FF被看成一个有符号数¡1 还是无符号数+255取决于程序员

  * 2.1.2 正负号延伸
    * 增大数据的大小：一般说来，扩展一个无符号数，你需将所有的新位置为0.因此，FF就变成了00FF。但是，扩展一个有符号数，你必须扩展符号位
    * 80386通过提供一个新的指令MOVZX来解决在AX中的无符号字转换成在EAX中的无符号双字是不可能的这个问题
    * 80386加了好几条新的指令。CWDE (Convert Word to Double word Extended(字转换成扩展的双字))指令将AX正负号扩展成EAX。CDQ (Convert Double word toQuad word(双字扩展成四字))指令将EAX正负号扩展成EDX:EAX (64位!).最后，MOVSX 指令像MOVZX指令一样工作，除了它使用有符号数的规则外
    * 减小数据的大小：无符号数的规则是：为了能转换正确，所有需要移除的位都必须是0。有符号数的规则是：需要移除的位必须要么都是1,要么都是0。另外，没有移除的第一个比特位的值必须等于移除的位的第一位。这一位将会是变小的值的新的符号位。这一位与原始符号位相同是非常重要的！
    * C编程中的应用
      * EOF。这是一个宏，通常被定义为¡1

  * 2.1.3 补码运算
    * 实际上，乘法怎么执行取决于源操作数的大小。
    * 一个普遍的错误是在进行除法之前忘记了初始化DX或EDX。
    * NEG 指令通过计算它的单一的操作数补码来得到这个操作数的相反数。

  * 2.1.5 扩展精度运算

    * ADC 和SBB 指令使用了进位标志位里的信息


* 2.2 控制结构

  * 汇编语言并没有提供像这样的复杂控制结构。它使用声名狼藉的goto来替代，如果使用不恰当可能会导致非常复杂的代码
  * 2.2.1 比较
    * 控制结构决定做什么是基于数据的比较的。在汇编语言中，比较的结果储存在FLAGS寄存器中，以便以后使用。80x86提供CMP指令来执行比较操作。FLAGS寄存器根据CMP指令的两个操作数的不同来设置。
    * 对于无符号整形，有两个标志位(在FLAGS寄存器里的位) 是非常重要的：零标志位(zero flag(ZF)) 和进位标志位(carry flag(CF)) 。如果比较的结果是0的话，零标志位将置成(1) 。进位标志位在减法中当作一个借位来使用
    * 对于有符号整形，有三个标志位非常重要：零标志位(zero flag (ZF))，溢出标志位(overflow flag(OF))和符号标志位(sign flag (SF))。

  * 分支指令
    * 分支指令可以将执行控制权转移到一个程序的任意一点上。换言之，它们像goto一样运作。有两种类型的分支：无条件的和有条件的。一个无条件的分支就跟goto一样，它总会产生分支。一个有条件分支可能也可能不产生分支，它取决于在FLAGS寄存器里的标志位。如果一个有条件分支没有产生分支，控制权将传递到下一指令。
    * JMP (jump的简称)指令产生无条件分支。它唯一的参数通常是一个指向分支指向的指令的代码标号。jump指令的几个变更形式：
      * SHORT 这个跳转类型局限在一小范围内。它仅仅可以在内存中向上或向下移动128字节。
      * NEAR 这个跳转类型是无条件和有条件分支的缺省类型，它可以用来跳到一段中的任意地方。事实上，80386支持两种类型的近跳转
      * FAR 这个跳转类型允许控制转移到另一个代码段

  * 循环指令
    * 80x86提供了几条专门为实现像for一样的循环而设计的指令。每一个这样的指令带有一个代码标号作为它们唯一的操作数。
      * LOOP ECX自减，如果ECX 6= 0，分支到代码标号指向的地址
      * LOOPE, LOOPZ ECX自减(FLAGS寄存器没有被修改)，如果ECX 6= 0而且ZF = 1，则分支
      * LOOPNE, LOOPNZ ECX自减(FLAGS没有改变)，如果ECX 6= 0 而且ZF = 0，则分支



### chap 3 位操作 ###

---

* 3.1 移位操作

  * 3.1.1 逻辑移位

    * 新进来的比特位总是为0。SHL 和SHR 指令分别用来执行逻辑左移和逻辑右移。这些指令允许你移动任意的位数。位数可以是一个常量，也可以是储存在CL寄存器的值。最后从数据中移出的比特位储存在进位标志位中

  * 3.1.2 移位的应用
    * 快速的乘法和除法是移位操作最普遍的应用
    * 实际上，逻辑移位只可以用于无符号数的乘法和除法。一般它们不能应用于有符号数

  * 3.1.3 算数移位
    * 这些移位操作是为允许有符号数能快速地执行乘以和除以2的几次方的操作而设计的。它们保证符号位能被正确对待：
      * SAL 算术左移(Shift Arithmetic Left)
      * SAR 算术右移(Shift Arithmetic Right)

  * 3.1.4 循环移位

    * 循环移位指令像逻辑指令一样运作，除了把从数据的一端移出的比特位又移入到另一端外。因此，数据好像被当作一个循环结构体一样对待。ROL和ROR 是两个最简单的循环移位指令，它们分别执行左移和右移操作


* 3.2 布尔型按位运算
  * 有四个普遍的布尔型运算符，它们是：AND，OR，XOR和NOT
  * TEST指令执行一次AND运算，但是并不储存结果。它会基于可能的结果对FLAGS寄存器进行设置(非常像CMP指令执行了一次减法操作但是只是设置了FLAGS)
  * 位操作的应用
    * 位操作对于操纵数据单个位而不修改其它位来说是非常有用的



* 避免使用条件分支
  * 现代处理器使用了非常尖端的技术来尽可能快地执行代码。一个普遍技术称为预测执行。这种技术使用CPU的并行处理能力来同时执行多条指令。条件分支与这项技术有冲突。一般说来，处理器是不知道分支是否会执行。如果执行了，跟没有执行相比执行的是一组不同的指令。处理器试着预测分支是否执行。如果预测错误，处理器就浪费了它的时间去执行了一些错误的代码。一个避免这个问题的办法就是如果可能尽量避免使用条件分支。



### chap 4 子程序 ###

---

* 本章主要着眼于使用子程序来构成模块化程序和得到与高级语言(比如说C)的接口。函数和进程是高级语言中子程序的例子。调用了一个子程序的代码和这个子程序必须协商它们之间的数据如何传输。数据如何传输的这些规则称为调用约定。这一章的很大一部分都是在讨论使用在汇编子程序和C程序接口上的标准C调用约定。这个约定(和其它约定)通常都是通过传递数据的地址(也就是指针)来允许子程序访问内存中的数据。
* 4.1 间接寻址

  * 间接寻址允许寄存器像指针变量一样运作。要指出寄存器像一个指针一样被间接使用，需要用方括号([])将它括起来。、
* 4.3 堆栈
  * SS段寄存器指定包含堆栈的段(通常它与储存数据的段是一样)。ESP寄存器包含将要移除出栈数据的地址。这个数据也被称为栈顶。数据只能以双字的形式入栈。
  * PUSH指令通过把ESP减4来向堆栈中插入一个双字1，然后把双字储存到[ESP]中。POP指令从[ESP]中读取双字，然后再把ESP加4.

* 4.4 call和ret指令
  * CALL指
    令执行一个跳到子程序的无条件跳转，同时将下一条指令的地址推入栈中。RET指令弹出一个地址并跳转到这个地址去执行。使用这些指令的时候，正确处理堆栈以便RET指令能弹出正确的数值是非常重要的！

* 4.5 调用约定

  * 一个可重入的子程序可以在程序中的任意一点被安全调用(甚至在子程序内部)
  * 4.5.1 在堆栈上传递参数
    * 给子程序的参数需要在堆栈中传递。它们在CALL指令之前就已经被压入栈中了。和在C中是一样的，如果参数被子程序改变了，那么需要传递的是数据的地址，而不是值。如果参数的大小小于双字，它就需要在压入栈之前转换成双字。

  * 4.5.2 堆栈上的局部变量
    * 一个可重入的子程序不管在任何地方被调用都能正常运行，包括子程序本身。换句话说，可重入子程序可以嵌套调用。储存变量的堆栈同样在内存中。不储存在堆栈里的数据从程序开始到程序结束都使用内存(C称这种类型的变量为全局变量或静态变量)。储存在堆栈里的数据只有当定义它们的子程序是活动的时候才使用内存
    * 堆栈帧: 这一节的堆栈包含了参数，返回信息和局部变量，这样堆栈称为一个堆栈帧.。C函数的尽管ENTER和LEAVE指令事 每一次调用都会在堆栈上创建一个新的堆栈帧

* 4.6 多模块程序

  * 回忆一下连接程序将目标文件组合成一个可执行程序。连接程序必须把在一个模块(也就是目标文件)中引用的每个变量匹配到定义该变量的模块。为了让模块A能使用定义在模块B里的变量，就必须使用xtern(外部)指示符

* 4.7 C与汇编的接口技术

  * 有两种使用汇编语言的方法：在C中调用汇编子程序或内嵌汇编。内嵌汇编允许程序员把汇编语句直接放入到C代码中。这样是非常方便的；但是，内嵌汇编同样存在缺点。汇编语言的书写格式必须是编译器使用的格式。
  * 4.7.3 传递参数
    * 按照C调用约定，一个函数的参数将以一定顺序压入栈中，这个顺序与它们出现在函数调用里的顺序相反

  * 4.7.4 计算局部变量的地址
    * LEA (即Load E®ective Address，载入有效地址)。下面的代码就能计算出x的地址并将它储存到EAX中：
      lea eax, [ebp - 8]
      现在EAX中存有了x的地址，而且当调用函数foo的时候，就可以将其压入到栈中。不要搞混了，这条指令看起来是从[EBP - 8]中读数据；然而，这并不正确。LEA指令永远不会从内存中读数据。它仅仅计算出一个将会被其它指令使用到的地址，然后将这个地址储存到它的第一个操作数里。因为它并没有实际读内存，所以不指定内存大小(例如： dword)是必须的或说是允许的。

  * 4.7.5 返回值
    * 返回值不为空的C函数执行完后会返回一个值。C调用约定规定了这个要如何去做。返回值需通过寄存器传递。所有的整形类型(char，int，enum，等)通过EAX寄存器返回。

  * 4.7.6 其他调用约定

    * 当与汇编语言进行接口时，知道编译器调用你的函数时使用的是什么调用约定是非常重要的

  * 4.7.8 在汇编程序中调用C函数

    * C与汇编接口的一个主要优点是允许汇编代码访问大型C库和用户写的函数






















       




