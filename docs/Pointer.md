### Size

|Type|Bit|
|----|----|
|bit|1|
|byte|8|
|arm64|64bit|
|word|arm64|

|Type|Byte|0s|2|
|----|----|----|----|
|1KB|1000|||
|1KiB|1024|3|2^10|
|1MiB|1048576|6|2^20|
|1GiB|1073741824|9|2^30|
|1TiB|1099511627776|12|2^40|
|1PiB|1125899906842624|15|2^50|
|1EiB|1152921504606846976|18|2^60|
|1ZiB|1180591620717411303424|21|2^70|
|1YiB|1208925819614629174706176|24|2^80|

### Endian

check out little or big
```
    int i = 1;   
    char *p = (char *)&i;   
    if(*p == 1)     
          printf("Little Endian"); 
    else
          printf("Big Endian");
```

take *two bytes file a* as example
```
# below is on little
# In this scheme, low-order byte is stored on the starting address (A) and high-order byte is stored on the next address (A + 1)
$ cat a
a
$ ls -l a
-rw-rw-r-- 1 zzx zzx 2 Mar  1 07:44 a
$ hexdump a # this is big
0000000 0a61
0000002
$ xxd a # this is little
00000000: 610a
```

|Hex|Char|Digit|
|0x61|a|97|
|0x0a|LF/NL(Line Feed/New Line)|10|

make random number

```
c=1
w=2
b=512
kB=1000
K=1024
MB=1000*1000
M=1024*1024
xM=M
GB=1000*1000*1000
G=1024*1024*1024
...
T (terabytes), P (petabytes), E (exabytes), Z (zettabytes), and Y (yottabytes)
# this makes 1024 byte file
dd if=/dev/urandom of=test.file bs=1024 count=1

xxd test.file
# use python get digit
>>> 0x000003ff
1023
>>> 0x00004000
16384
>>> 0x00000400
1024

# use linux bc
echo "ibase=16; 400" | bc
printf "%d\n" 0x400

printf "%d\n" 0x1ffff

# range size, MCP UART
echo "ibase=16; 4C001FFF-4C001000+1" | bc
4096
# this is 4KB

```

### Range

|Number|Order|Start|End|Range|
|----|----|----|----|----|
|1KB|10|0x00|0x3ff|0x400|
|2KB|11|0x00|0x7ff|0x800|
|4KB|12|0x000|0xfff|0x1000|
|1MB|20|0x00000|0xfffff|0x100000|
|1GB|30|0x00000|0x3fffffff|0x40000000|


<a href="#top">Back to top</a>
