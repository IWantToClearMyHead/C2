### Linux get hardware

- architechture
```
arch

ls /sys/devices/system/node #only node0 means smp, more means numa node 
ls /sys/devices/system/node/node0 #get the logic CPU for node

```


- logic CPU
```
grep process /proc/cpuinfo

```

- core
```
grep core /proc/cpuinfo
```

- processor stat
```
cat /proc/stat
```

- run bit
```
getconf LONG_BIT #64means running at 64bit
```

- cache, l123
```
$ cat /sys/devices/system/cpu/cpu0/cache/index0/level #this is D-Cache
1
$ cat /sys/devices/system/cpu/cpu0/cache/index1/level #this is I-cache
1
$ cat /sys/devices/system/cpu/cpu0/cache/index2/level
2
$ cat /sys/devices/system/cpu/cpu0/cache/index3/level
3
$ ls /sys/devices/system/cpu/cpu0/cache
index0  index1  index2  index3  uevent
$ cat /sys/devices/system/cpu/cpu0/cache/index0/type
Data
$ cat /sys/devices/system/cpu/cpu0/cache/index1/type
Instruction
$ cat /sys/devices/system/cpu/cpu0/cache/index2/type
Unified
$ cat /sys/devices/system/cpu/cpu0/cache/index3/type
Unified

$ cat /sys/devices/system/cpu/cpu0/cache/index3/size
25600K
$ cat /sys/devices/system/cpu/cpu0/cache/index2/size
256K
$ cat /sys/devices/system/cpu/cpu0/cache/index1/size
32K
$ cat /sys/devices/system/cpu/cpu0/cache/index0/size
32K
```


- numa check on/off
```
dmesg | grep numa

find /sys -name numa_node | xargs cat #get device numa id
```




<a href="#top">Back to top</a>
