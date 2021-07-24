---
title: Redis 查看内存信息
date: 2020-11-24 20:09:32
categories:
- redis
tags:
- reids
---

redis 查看内存信息。

```javascript
% redis-cli 
127.0.0.1:6379> info memory
# Memory
used_memory:1064496
used_memory_human:1.02M
used_memory_rss:2289664
used_memory_rss_human:2.18M
used_memory_peak:1123024
used_memory_peak_human:1.07M
used_memory_peak_perc:94.79%
used_memory_overhead:1018896
used_memory_startup:1001456
used_memory_dataset:45600
used_memory_dataset_perc:72.34%
allocator_allocated:1019376
allocator_active:2251776
allocator_resident:2251776
total_system_memory:8589934592
total_system_memory_human:8.00G
used_memory_lua:37888
used_memory_lua_human:37.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:0
maxmemory_human:0B
maxmemory_policy:noeviction
allocator_frag_ratio:2.21
allocator_frag_bytes:1232400
allocator_rss_ratio:1.00
allocator_rss_bytes:0
rss_overhead_ratio:1.02
rss_overhead_bytes:37888
mem_fragmentation_ratio:2.25
mem_fragmentation_bytes:1270288
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:17440
mem_aof_buffer:0
mem_allocator:libc
active_defrag_running:0
lazyfree_pending_objects:0
```

