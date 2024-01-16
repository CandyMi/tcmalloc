# TCMalloc : Thread-Caching Malloc

  `tcmalloc` 是 `Google` 对 `C` 的 `malloc()` 和 `C++` 的 `operator new` 运算符的定制实现，用于替换 `C` 和 `C++` 代码中默认的分配内存接口。 
  
  `tcmalloc` 最初是为多线程而构建的, 且也比`libc`的实现在实际的应用场景中更高效。

# 优势

  * 比`libc`提供的标准接口更快， 对多线程程序进行优化并减少内存分配开销.

  * 更好的`page`管理与分配策略， 更多的配置参数可以减少内存浪费、增加业务贴合度.

  * 拥有丰富的外置功能，配合内存分配器能实现更多的特性：内存检查、泄漏检查等.

  * 可以减少系统内存碎片的产生，对于长期运行的程序更加友好.

# 文档

  * [基本介绍(中文)](introduce.md)

  * [高级配置(中文)](configure.md)

  * [安装方法(中文)](build.md)

  * [性能指标(中文)](performance.md)

# 许可

  [BSD-3-Clause license](https://raw.githubusercontent.com/gperftools/gperftools/master/COPYING)
