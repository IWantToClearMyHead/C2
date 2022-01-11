### Hello

- Build
```
git clone https://gem5.googlesource.com/public/gem5

apt install build-essential git m4 scons zlib1g zlib1g-dev libprotobuf-dev protobuf-compiler libprotoc-dev libgoogle-perftools-dev python-dev python

apt install  python3  python3-dev

python3 /usr/bin/scons build/ARM/gem5.opt -j9

```

- Run
```
./build/ARM/gem5.opt configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/hello

./build/ARM/gem5.opt --debug-flags=Decode --debug-start=50000 --debug-file=my_trace.out configs/example/se.py -c tests/test-progs/hello/bin/arm/linux/hello

cat m5out/config.ini
./build/ARM/gem5.opt --debug-file=my_trace.out configs/example/se.py --cmd=tests/test-progs/hello/bin/arm/linux/hello --cpu-type=TimingSimpleCPU --l1d_size=64kB --l1i_size=16kB


```

###

### SimPoint

- [fatal: SimPoint/BPProbe should be done with an atomic cpu](https://github.com/uart/gem5-mirror/blob/master/configs/example/se.py)
```
if options.simpoint_profile:
    if not ObjectList.is_noncaching_cpu(CPUClass):
        fatal("SimPoint/BPProbe should be done with an atomic cpu")
    if np > 1:
        fatal("SimPoint generation not supported with more than one CPUs")
```

- [  Loading data from frequency vector file 'm5out/simpoint.bb.gz' (size: 0x0)]
```
./build/ARM/gem5.opt --debug-file=my_trace.out configs/example/se.py -c tests/test-progs/hello/bin/arm/linux/hello --cpu-type=NonCachingSimpleCPU --mem-type=SimpleMemory --simpoint-profile --simpoint-interval 10000000
file m5out/simpoint.bb.gz
./simpoint -loadFVFile m5out/simpoint.bb.gz -maxK 30 -saveSimpoints m5out/simpoint.bb.p -saveSimpointWeights m5out/simpoint.bb.w -inputVectorsGzipped

```

- self
```
cat > a.c << EOF; $(echo)
#include <stdio.h>
int main()
{
  printf("========a========\n");
}
EOF

gcc -static a.c -o a # this should be on arm64

./build/ARM/gem5.opt configs/example/se.py -c my/a


```

<a href="#top">Back to top</a>
