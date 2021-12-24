### install and build arm

```
apt install build-essential git m4 scons zlib1g zlib1g-dev libprotobuf-dev protobuf-compiler libprotoc-dev libgoogle-perftools-dev python-dev python

#git clone https://gem5.googlesource.com/public/gem5
git clone https://github.com/gem5/gem5.git

#git config --global  --unset https.https://github.com.proxy 
#git config --global  --unset http.https://github.com.proxy

vi /etc/sudoers

python3 `which scons` build/ARM/gem5.opt -j9

echo "My Shell name is: $SHELL"

lsof -p $$

source shrc

build/ARM/gem5.opt configs/example/se.py -c tests/test-progs/hello/bin/arm/linux/hello

cat  tests/test-progs/hello/src/hello.c

```

### load os

[download image](https://www.gem5.org/documentation/general_docs/fullsystem/guest_binaries)

```
export M5_PATH=/home/ankita/gem5/full_system_images/
cd gem5
build/ARM/gem5.opt configs/example/fs.py --disk-image=/home/ankita/gem5/full_system_images/disks/arm-ubuntu-natty-headless.img --kernel=/home/ankita/gem5/full_system_images/binaries/vmlinux.arm.smp.fb.2.6.38.8
telnet 127.0.0.1 3456
# wait 30 mins...
# Type root to login and type command who ,scp to test the running of simulated image

```

### generate bbv

```

export M5_PATH="$PWD/full_system_images"
build/ARM/gem5.opt configs/example/fs.py --simpoint-profile --simpoint-interval 10000000 --cpu-type=NonCachingSimpleCPU --disk-image=/home/zzx/full_system_images/disks/aarch64-ubuntu-trusty-headless.img --kernel=/home/zzx/full_system_images/binaries/vmlinux.arm.smp.fb.3.2

build/ARM/gem5.opt <base options> configs/example/se.py --simpoint-profile --simpoint-interval 10000000 --cpu-type=AtomicSimpleCPU --fastmem

build/ARM/gem5.opt configs/example/se.py --simpoint-profile --simpoint-interval 10000000 --cpu-type=NonCachingSimpleCPU --kernel=/home/zzx/full_system_images/binaries/vmlinux.arm.smp.fb.3.2

```

### simpoint 

- adding to Utilities.h
``` 
#include <cstdlib>
#include <cstring>
#include <limits.h>
#include <iostream>
#include <fstream>
```
- adding to Datapoint.h 
```
#include <iostream>
```

- make and cd to SimPoint/bin
```
simpoint -loadFVFile simpoint.bb.gz -maxK 30 -saveSimpoints bb.simpoint -saveSimpointWeights bb.weight -inputVectorsGzipped

cat bb.weight
0.02 0
0.446 1
0.216 2
0.016 3
0.146 4
0.022 5
0.086 6
0.048 7

```

each line represents a simpoint taken. Within each line, the number on the left means the interval number of this simpoint, the number on the right is the simpoint index. 

### run in gem5

```
build/ARM/gem5.opt <base options> configs/example/se.py --take-simpoint-checkpoint=<simpoint file path>,<weight file path>,<interval length>,<warmup length> <rest of se.py options>

build/ARM/gem5.opt <base options> configs/example/fs.py --restore-simpoint-checkpoint -r <N> --checkpoint-dir <simpoint checkpoint path> --cpu-type=TimingSimpleCPU --restore-with-cpu=DerivO3CPU <rest of fs.py options>

```

<a href="#top">Back to top</a>
