# 性能指标

## 分配时间

  `tcmalloc` 与 `ptmalloc2` 的几个不同的性能指标可以从下图中看出优劣:

  ![对比图1](/pt2vstc2.png)

  * 在绝大多数情况下， `tcmalloc` 比 `ptmalloc2` 更快，特别是对于小分配。 因为在 `tcmalloc` 内， 线程之间的争用不是什么问题.

  * `tcmalloc` 的性能会随着分配大小的增加而下降。 这是因为每线程缓存在达到阈值（默认为 `2MB`）时会被垃圾收集。 分配大小越大，在垃圾收集之前可以在缓存中存储的对象就越少。
  
  * 在最大分配大小约为 `32K` 时，`tcmalloc` 的性能明显下降；尺寸越大性能下降得越慢。 因为每线程缓存中对象的最大大小为 `32K`； 对于大于此 `TCMalloc` 的对象，需要向中央页堆中分配。

  * `tcmalloc` 比 `ptmalloc2` 具有更一致的可扩展性 - 线程总数 > `1` 时， 它可实现约 `700` ~ `900` 万/秒 的分配操作，适用于小型内存分配； 而对于大内存块则降至约 `200` 万/秒。这个数值在 `ptmalloc2` 中则会低得多， 约 `400` 万/秒 的小内存块分配，大内存块分配则 小于 `100` 万/秒。
  

## 分配开销

  每秒 `CPU` 时间的操作数（百万次）与线程数，最大分配大小在 `64` Bytes - `128` Kbytes 之间:

  ![对比图2](/pt2vstc22.png)

  在这里可以再次看到 `tcmalloc` 比 `ptmalloc` 更一致、更高效。 对于最大分配大小 `<32K`， `tcmalloc` 通常可以在大量线程的情况下实现大约 `250`万次每秒的`CPU`操作时间，而 `ptmalloc2` 通常只能实现 `50`万-`100`万次每秒的 `CPU` 操作时间，很多`libc`实现了小于这个数字。 超过 `32K` 最大分配大小时，`tcmalloc` 的 `CPU` 时间会下降到每秒`100`万-`150`万次操作，而对于大量线程的`ptmalloc2`几乎下降到零（即，使用 `ptmalloc2`，大量的 `CPU` 时间被消耗在等待大量线程的锁上）多线程情况）。


# 应用测试


## MariaDB

  |特性 | Jemalloc | TCMalloc|
  |:-:|:-:|:-:|
  |多线程效率 |高 | 非常高|
  |内存碎片 |低 |中等|
  |分配速度 |优秀 |优秀|
  |内存消耗 |略高 |较低|

  此基准测试来源于[这里](https://www.managedserver.eu/Improve-mysql-and-mariadb-performance-with-memory-allocators-like-jemalloc-and-tcmalloc/), 不过目前推荐用[这里](https://mariadb.com/kb/en/using-mariadb-with-tcmalloc-or-jemalloc/)提到的方式来设置.
  
  可以明显看出在不同的负载场景和硬件配置下，jemalloc、tcMalloc 和 glibc malloc 之间存在较为明显的性能差异。

  ![对比图4](/je_tc_pt.png)

  * 4 个 vCPU：在有限的核心数量情况下，分配器的性能几乎相同，平均吞吐量约为 2500 TPS（每秒事务数）。
  * 8 个 vCPU：Jemalloc 和 TCMalloc 的吞吐量翻了一番，达到了 5000 TPS，而 glibc malloc 在线程数达到 64-128 时，吞吐量显著下降至 3500 TPS。
  * 16 个 vCPU：Jemalloc 和 TCMalloc 在线程数达到 4096 时，吞吐量保持稳定增长且达到 6300 TPS。相反 glibc malloc 在线程数超过 16 后吞吐量急剧下降，稳定在 4000 TPS 左右。

## PerconaDB

  *优化之前*：

  ![之前的负载](/percona-before.png)

  *jemalloc 在生产环境中的表现*：

```
一开始使用 jemalloc 还不错，但后来内存使用量开始出现严重的峰值。这些峰值非常高而且难以预测，所以决定重新使用 glibc。
```  

  ![JEMALLOC](/je_in_pro.png)

  *Glibc malloc 在生产环境中的表现*：

```
之后为这台机器添加了大量的额外内存，使用 glibc 因此不再是问题。我们看到的趋势：系统内存使用量呈上升曲线，然后就是稳步增长。
```

  ![GLIBC](/pt_in_pro.png)
  
  *tcmalloc 在生产环境中的表现*：

```
在某次备份运行后，我们发现内存使用量已达到上限，并且一直保持在这个水平。使用 tcmalloc 和 mysql 后，内存使用量稳定得令人难以置信。
```

  ![TCMALLOC](/tc_in_pro.png)

  *数据对比*：

  ![对比图3](/pt_tc_je.png)

```
注意：这里使用的 percona 构建是自定义的，但我们在 CentOS 上运行上游构建的结果与此类似。
```

  在本次测试中，tcmalloc 无疑是赢家。它的性能相当不错，但内存占用却是三者中最低的，这一点毋庸置疑。由于我们正在寻找降低内存占用的方法，因此必须将 tcmalloc 与 mysql 进行实际数据库测试，看看它是否有效。结果非常令人期待。

  原文在这里：

  * [MySQL（或 percona）内存使用情况 I](https://blog.herecura.eu/blog/2020-04-23-mysql-memory-usage/)

  * [MySQL（或 percona）内存使用情况 II](https://blog.herecura.eu/blog/2020-05-12-mysql-memory-usage-in-real-life/)

  * 32 个 vCPU：Jemalloc 和 TCMalloc 表现出显著的提升，峰值达到 12500 TPS，并且在线程数达到 1024 时仍保持高性能，超过此阈值后略有下降。相反，Glibc malloc 的性能却急剧下降，TPS 低于 8 和 16 个 vCPU 测试的水平，稳定在 3100 TPS 左右。

  简而言之，在 32 个 vCPU 的服务器上进行的 OLTP_RO（只读在线事务处理）测试中，glibc malloc 与 Jemalloc/TCMalloc 之间的性能差异约为 4 倍。这凸显了随着并发核心和线程数量的增加，Jemalloc 和 TCMalloc 如何确保更稳定、更可扩展的性能，从而显著减少 glibc malloc 低效内存分配造成的瓶颈。
