
  这有一些常见问题解答.

## 请简单介绍?

  `tcmalloc`是由`google`公司早期开发的**内存分配器**, 可以轻松与大部分项目配合使用. 

## 如何快速使用?

  我们可以通过以下方式来使用

### 1. 动态链接

  通过动态链接`tcmalloc`/`tcmalloc_minimal`, 这种方式适用于大部分系统(包括:`Windows`)

### 2. 优先加载

  通过设置`LD_PRELOAD=/path/libtcmalloc.so`, 这种方式适用于大部分[Unix-Like](https://en.wikipedia.org/wiki/Unix-like)系统.

## 优势和性能差异?

  您可以在[性能指标](https://baike.baidu.com/item/%E7%B1%BBUNIX%E7%B3%BB%E7%BB%9F/4336219)文章里获得信息, 也可以通过从网上分享的文章来了解更多.

  这里简单描述一下优势：

  * 拥有线程本地缓存.

  * 使用更低开销的锁.

  * 降低系统调用频率.

  * 自适应算法减少内存浪费.

  * 合并归还算法减少内存碎片.

## 申请和分配的含义?

  对于 **将系统中可用的内存空间分配给程序或进程以供其使用** 的行为, 我们将其称为: **申请内存**. 而 **"将之前已申请但不再使用的内存块交还"** 的行为, 我们将其称为: **释放内存**
  
  如果您使用不同的编程语言, 则会有不同的使用:

  * `C` - [申请](https://zh.cppreference.com/w/c/memory/malloc)、[释放](https://zh.cppreference.com/w/c/memory/free)

  * `C++` - [申请](https://zh.cppreference.com/w/cpp/memory/new/operator_new)、[释放](https://zh.cppreference.com/w/cpp/memory/new/operator_delete)

  * 实现 `Zero-Copy` 或 `file-mapping` 时可以使用[mmap/munmap](https://man7.org/linux/man-pages/man2/mmap.2.html)等函数.
  
  * 在栈上临时申请非固定大小的内存可以使用[alloca](https://man7.org/linux/man-pages/man3/alloca.3.html)等函数.

## 可以缓解内存碎片吗?

  可以! 没有使用`tcmalloc`的程序在动态地分配和释放内存时, 会导致内存中出现不连续的小块空闲内存. 这些小块空闲内存如果不能被有效地利用就会形成**内存碎片**.

  而`tcmalloc`利用合理的内存池和分配策略能减少频繁的向系统进行小内存的分配, 在缓解内存碎片产生的同时减少了大量系统调用, 因此可以认为提高了整体的内存申请效率.

## 为什么比xLibc的性能更差?

  * 检查您使用的动态库是否使用`CMAKE`构建且处于非`Release`或`RelWithDebugInfo`模式.

  * 当前系统、内核是否提供完整的优化特性, 对于有限支持的环境应该进行完整的测试用例覆盖后再决定是否使用.
