### chap_2 计算机启动过程、GRUB以及multiboot标准  ###

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
  * 

