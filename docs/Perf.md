### Perf Flame

```
git clone https://github.com/brendangregg/FlameGraph.git
```

### CPU Time
- CPU time is a true measure of processor/memory performance
- Performance of processor/memory = 1 / CPU time 
~~~
CPU time = CPU clock cycles x clock cycle time = CPU clock cycles / clock rate(is given in Hz (=1/sec), i.e. 2.6GHz)

CPU clock cycles = (instructions/program) x (clock cycles/instruction) = Instruction count x CPI

CPU time = Instruction count x CPI / clock rate(i.e. 256739 * 0.66 / 2.6E9 = 0.00006517 = 0.6ms)


~~~

### CPI

- From instruction to CPI
~~~
Assume that a benchmark has 100 instructions:
25 instructions are loads/stores (each take 2 cycles)
50 instructions are adds (each takes 1 cycle)
25 instructions are square root (each takes 50 cycles)

What is the CPI for this benchmark?
CPI = ((0.25 * 2) + (0.50 * 1) + (0.25 * 50)) = 13.5
~~~

- Composite CPI: CPI = Σ CPI x F

|Op|F|CPI|CPIxF|%Time|
|---|---|---|---|---|
|ALU|50%|1|.5|23%|
|Load|20%|5|1.0|45%|
|Store|10%|3|.3|14%|
|Branch|20%|2|.4|18%|
|Total|100%|2.2|100%|


### Benchmark

- 508
```
# modify try1.cfg to have static linked via gcc before gem5 start

../bin/runcpu --config=try1.cfg --action=build 508.namd_r

# remove previous build if not first time
rm -rf benchspec/CPU/508.namd_r/build;
rm -rf benchspec/CPU/508.namd_r/run;
rm -rf benchspec/CPU/508.namd_r/exe;

# ls
ls ../benchspec/CPU/508.namd_r/build && ls ../benchspec/CPU/508.namd_r/run ; ls ../benchspec/CPU/508.namd_r/exe ; echo "Good"


```

- 509
```
../bin/runcpu --config=try1.cfg --action=build 519.lbm_r
```

### Perf Metric
- execution time : time to do the task
- throughput : number of tasks completed per unit time

||Instruction|CPI|Clock Freq|
|---|---|---|---|
|Program|x|||
|Compiler|x|x||
|Arch|x|x||
|Orgnization||x|x|
|Tech|||x|

### Profile
```
gcc -pg a.c -o a
./a
gprof a ./gmon.out > gmon.txt
cat gmon.txt

```



<a href="#top">Back to top</a>
