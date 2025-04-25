# TCMalloc: Thread-Caching Malloc

*久经考验的高性能内存分配器*

---

## 概述

  **TCMalloc**（Thread-Caching Malloc）是Google开发的内存分配器，作为glibc malloc的替代方案，且为多线程应用设计并优化。


## 安装方式

```bash
git clone https://github.com/gperftools/gperftools.git
cd gperftools && cmake -B build -DCMAKE_BUILD_TYPE=Release && cmake --build build
```

## 适用场景

* ✅ 高并发服务
* ✅ 长期运行进程
* ✅ 内存敏感型应用
* ✅ 需要堆分析的场景
