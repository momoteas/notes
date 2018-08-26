### chap_2 计算机启动过程、GRUB以及multiboot标准  ###

----

 *  multiboot规范：描述如何构造一个能够被grub识别，并且 按照我们定义的规则去加载操作系统内核。( [ en version: multiboot specification][http://www.gnu.org/software/grub/manual/multiboot/multiboot.pdf] ),	( [cn version: multiboot specification][http://blog.sina.com.cn/s/blog_9e63e1e60101dkbs.html] )
 *  ELF: Executable and Linkable Format
 *  gcc有很多内建函数用来替换一些C语言的库函数以提升效率，比如把只有一个字符串参数的printf函数替换为puts函数
 *  文件系统：所谓的文件系统指的是操作系统用于明确磁盘或分区上的文件存储的方法和数据结构，即在磁盘上组织文件的方法。如果把这个1.44MB的软盘可以看做一个巨大的数组，那么每个数组成员都是一个扇区，拥有512字节的存储单元；
 *  [file system:][https://en.wikipedia.org/wiki/File_system] 
    * A file system consists of two or three layers:
      * The *logical file system* is responsible for interaction with the user application. This layer provides "file access, directory operations, [and] security and protection;
      * The second optional layer is the *virtual file system*. "This interface allows support for multiple concurrent instances of physical file systems, each of which is called a file system implementation;
      * The third layer is the *physical file system*. This layer is concerned with the physical operation of the storage device (e.g. disk). It processes physical [blocks](https://en.wikipedia.org/wiki/Block_(data_storage)) being read or written;

* stack: 

  * ![stack](https://upload.wikimedia.org/wikipedia/commons/thumb/8/8a/ProgramCallStack2_en.png/350px-ProgramCallStack2_en.png)

  * [definition: stack][https://en.wikipedia.org/wiki/Stack_(abstract_data_type)]


* [Intel 80386 programmer's reference manual][http://www.logix.cz/michal/doc/i386/]



### chap_4 字符模式下的显卡驱动 ###

---

* 在PC上要显示文字，通常需要显示器和显卡这两个硬件设备。一般来说显卡负责提供显示内容，并控制具体的显示模块和状态。显示器的职责是负责将显卡呈递的内容可视化的显示出来。既然显卡需要控制显示的数据，自然就需要存储这些待显示的内容，所以显卡就有自己的存储区域。这个存储区域叫做显示存储器（Video RAM，VRAM），简称显存。当然，访问显存就需要地址。CGA/EGA+ Chroma text video buffer 这个区域映射的就是工作在文本模式的显存。同时显卡还有另外一个工作模式叫做图形模式，这个模式是目前最最常用的模式。
* 4.2 显卡在文本模式下的显示规则
  * 所有在PC上工作的显卡，在加电初始化之后都会自动初始化到80*25的文本模式。42在这个模式下，屏幕被划分为25行，每行可以显示80个字符，所以一屏可以显示2000个字符。上图中的0xB8000～xBFFFF这个地址段便是映射到文本模式的显存的。当访问这些地址的时候，实际上读写的是显存区域，而显卡会周期性的读取这里的数据，并且把它们按顺序显示在屏幕上。
  * 那么，按照什么规则显示呢？这就要谈到内码了。内码定义了字符在内存中存储的形式，而英文编码就是大家所熟知的ASCII。。对应的关系很简单，从0xB8000这个地址开始，每2个字节表示屏幕上显示的一个字符。从屏幕的第一行开始对应，一行接着一行的对应下去。而这两个字节的前一个是显示字符的ASCII码，后一个是控制这个字符颜色和属性的控制信息

![1535263823459](C:\Users\ADMINI~1\AppData\Local\Temp\1535263823459.png)