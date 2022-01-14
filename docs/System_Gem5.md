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

### Runcpu 

```
../bin/runcpu --config try1.cfg --rebuild --iterations 1 --noreportable --output_format=html --size=test --copies=1 508
# ls result/ -lrt | tail -4
-rw-r--r-- 1 root root  53657 Jan 11 01:31 CPU2017.021.fprate.test.rsf
-rw-r--r-- 1 root root  34271 Jan 11 01:31 CPU2017.021.fprate.test.flags.html
-rw-r--r-- 1 root root 106761 Jan 11 01:31 CPU2017.021.fprate.test.html
-rw-r--r-- 1 root root  33231 Jan 11 01:31 CPU2017.021.log

# ls benchspec/CPU/508.namd_r
build  data  Docs  exe  run  Spec  src  version.txt

# ls benchspec/CPU/508.namd_r/run/run_base_test_ysemi-ref-64.0000/apoa1.input
# ls benchspec/CPU/508.namd_r/run/run_base_test_ysemi-ref-64.0000/apoa1.test.output

```

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

- cpu2017
```
# change config to adapt gem5
OPTIMIZE = -O2 -fno-strict-aliasing -static

../bin/runcpu --config ysemi-ref.cfg --rebuild --iterations 1 --noreportable --output_format=html --size=test --copies=1 508

# just 508
./build/ARM/gem5.opt configs/example/se.py --cmd=/home/zzx/cpu2017/benchspec/CPU/508.namd_r/build/build_base_ysemi-ref-64.0000/namd_r --options="--input /home/zzx/cpu2017/benchspec/CPU/508.namd_r/run/run_base_refrate_ysemi-ref-64.0000/apoa1.input --output /home/zzx/cpu2017/benchspec/CPU/508.namd_r/run/run_base_refrate_ysemi-ref-64.0000/apoa1.ref.output --iterations 1" --mem-size=8GB --cpu-type=AtomicSimpleCPU

# No bench and no arg?

./build/ARM/gem5.opt ./configs/example/se.py --bench=namd_r -I 900000000000 --simpoint-profile --simpoint-interval=10000

>>> dir(OptionParser)
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', '_add_help_option', '_add_version_option', '_check_conflict', '_create_option_list', '_create_option_mappings', '_get_all_options', '_get_args', '_init_parsing_state', '_match_long_opt', '_populate_option_list', '_process_args', '_process_long_opt', '_process_short_opts', '_share_option_mappings', 'add_option', 'add_option_group', 'add_options', 'check_values', 'destroy', 'disable_interspersed_args', 'enable_interspersed_args', 'error', 'exit', 'expand_prog_name', 'format_description', 'format_epilog', 'format_help', 'format_option_help', 'get_default_values', 'get_description', 'get_option', 'get_option_group', 'get_prog_name', 'get_usage', 'get_version', 'has_option', 'parse_args', 'print_help', 'print_usage', 'print_version', 'remove_option', 'set_conflict_handler', 'set_default', 'set_defaults', 'set_description', 'set_process_default_values', 'set_usage', 'standard_option_list']
```

- redo in cmd

```
../bin/runcpu --config try1.cfg --rebuild --iterations 1 --noreportable --output_format=html --size=test --copies=1 508

./build/ARM/gem5.opt ./configs/example/se.py --cmd=/home/zzx/cpu2017/benchspec/CPU/508.namd_r/build/build_base_ysemi-ref-64.0000/namd_r --options="--input /home/zzx/cpu2017/benchspec/CPU/508.namd_r/run/run_base_refrate_ysemi-ref-64.0000/apoa1.input --output /home/zzx/cpu2017/benchspec/CPU/508.namd_r/run/run_base_refrate_ysemi-ref-64.0000/apoa1.ref.output --iterations 1" --mem-size=8GB --cpu-type=NonCachingSimpleCPU -I 900000000000 --simpoint-profile --simpoint-interval=10000
```

### bbv

 one must type the full command to get the bb file
```
# cat a.c
#include <stdio.h> 
int main()         
{                  
  printf("a\n");   
}                  

#
sudo valgrind --tool=exp-bbv --bb-out-file=a.bb --pc-out-file=a.pc --interval-size=100 --instr-count-only=no ./a
# Thread 1
#   Total intervals: 146 (Interval Size 100)
#   Total instructions: 14607
#   Total reps: 0
#   Unique reps: 0
#   Total fldcw instructions: 0

# cat a.bb
T:1:13   :2:15   :3:14   :4:36   :5:1   :6:5   :7:17
T:7:36   :10:6   :11:3   :15:8   :8:10   :9:4   :16:2   :17:1   :12:6   :13:6   :22:5   :18:2   :19:2   :14:4   :20:2   :21:3
T:10:12   :11:6   :15:14   :8:14   :9:8   :16:2   :17:1   :12:12   :13:10   :18:2   :14:10   :24:3   :25:3   :23:3
T:10:10   :11:4   :27:6   :28:4   :32:5   :15:11   :8:12   :9:6   :16:4   :17:1   :34:2   :35:2   :29:2   :30:4   :12:2   :13:2   :36:2   :37:5   :14:2   :31:4   :26:4   :33:6
T:52:8   :53:1   :56:4   :57:12   :58:3   :59:2   :60:1   :15:5   :8:4   :9:1   :16:2   :17:1   :34:2   :35:2   :39:1   :41:3   :42:3   :43:3   :44:3   :45:3   :46:2   :47:2   :48:2   :49:7   :50:4   :51:7   :36:2   :38:3   :40:2   :54:4
  :55:1
  
# each T means an interval, colon BID and colon frequency(the number of times the block was entered, multiplied by the number of instructions in the block)
# total 146 T
# each T measn size instructions(maxium 100)
# 

```

### perf

For a better perf analysis, goto [:boom:](Perf.md)
```
perf stat ./a
 Performance counter stats for './a':

              0.49 msec task-clock                #    0.495 CPUs utilized
                 0      context-switches          #    0.000 K/sec
                 0      cpu-migrations            #    0.000 K/sec
                18      page-faults               #    0.036 M/sec
+           488,265      cycles                    #    0.990 GHz = 488,265 / 0.49 * 1000 = 996459184 (cycles/task-clock)
           278,263      instructions              #    0.57  insn per cycle
   <not supported>      branches
             3,617      branch-misses

       0.000997607 seconds time elapsed

       0.000975000 seconds user
       0.000000000 seconds sys
      
sudo perf stat -e task-clock,context-switches,cpu-migrations,page-faults,cycles,stalled-cycles-frontend,stalled-cycles-backend,instructions,branches,branch-misses,L1-dcache-loads,L1-dcache-load-misses,LLC-load s,LLC-load-misses,dTLB-loads,dTLB-load-misses ./a
    
wget https://github.com/torvalds/linux/blob/455c988225c7eee84c7a2f86984404825a1830bb/tools/perf/Documentation/tips.txt
    
mkdir /usr/share/doc/perf-tip

perf record -g -F 99 ./a

perf report
```




<a href="#top">Back to top</a>
