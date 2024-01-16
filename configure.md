# 配置修改

  您可以通过修改以下环境变量的方式来达到更精细地控制`tcmalloc`的行为：

## 常用设置

  |名称|默认值|描述|
  |:-:|:-:|-|
  |TCMALLOC_SAMPLE_PARAMETER|0|采样的间隔区间. 也就是说我们大约每分配一个字节就采样一次. 采样堆信息可通过`tcmalloc_sample_parmeterMallocExtension::GetHeapSample()` 或 `MallocExtension::ReadStackTraces()` 获得.|
  |TCMALLOC_RELEASE_RATE|1.0|在受支持的系统上设置未使用内存的归还速率. `0`意味着永远不会将内存释放归还系统. 增大可以更快地返回内存，减少它可以较慢地恢复内存. 合理的比率在 [0,10] 范围内|
  |TCMALLOC_MAX_TOTAL_THREAD_CACHE_BYTES|16777216|限制分配给线程缓存的字节总数. 这个限制并不严格, 因此缓存在某些情况下可能会超出. 默认值为 `16MB`. 对于具有许多线程的应用程序可能不够大导致影响性能. 如果您怀疑您的应用程序由于`tcmalloc`中的锁争用而无法扩展到许多线程, 则可以尝试增加此值. 这可能会提高性能, 但代价是 `tcmalloc` 会使用更多的内存.|

## 高级设置

  |名称|默认值|描述|
  |:-:|:-:|-|
  |TCMALLOC_SKIP_MMAP|false|如果为`true`，则不会尝试使用`mmap`从内核获取内存.|
  |TCMALLOC_SKIP_SBRK|false|如果为`true`，则不会尝试使用`sbrk`从内核获取内存.|
  |TCMALLOC_DEVMEM_START|0|`/dev/mem`分配的物理内存起始位置（以`MB`为单位）. 将其设置为`0`将禁用`/dev/mem`分配。|
  |TCMALLOC_DEVMEM_LIMIT|0|`/dev/mem` 分配的物理内存限制位置（以`MB`为单位）。 设置为`0`表示没有限制。|
  |TCMALLOC_DEVMEM_DEVICE|"/dev/mem"|指定用于分配非托管（unmanaged memory）内存的设备。|
