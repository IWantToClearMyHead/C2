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

### Self Cal
```
#define _GNU_SOURCE
#include <asm/unistd.h>
#include <linux/perf_event.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ioctl.h>
#include <unistd.h>

#include <inttypes.h>
#include <sys/types.h>

#include <time.h>
static long
perf_event_open(struct perf_event_attr *hw_event, pid_t pid,
                int cpu, int group_fd, unsigned long flags)
{
    int ret;

    ret = syscall(__NR_perf_event_open, hw_event, pid, cpu,
                    group_fd, flags);
    return ret;
}


int
main(int argc, char **argv)
{
    struct perf_event_attr pe;
    long long count;
    int fd;

    uint64_t n;
    if (argc > 1) {
        n = strtoll(argv[1], NULL, 0);
    } else {
        n = 10000;
    }

    memset(&pe, 0, sizeof(struct perf_event_attr));
    pe.type = PERF_TYPE_HARDWARE;
    pe.size = sizeof(struct perf_event_attr);
    pe.config = PERF_COUNT_HW_INSTRUCTIONS;
    pe.disabled = 1;
    pe.exclude_kernel = 1;
    // Don't count hypervisor events.
    pe.exclude_hv = 1;

    fd = perf_event_open(&pe, 0, -1, -1, 0);
    if (fd == -1) {
        fprintf(stderr, "Error opening leader %llx\n", pe.config);
        exit(EXIT_FAILURE);
    }

    ioctl(fd, PERF_EVENT_IOC_RESET, 0);
    ioctl(fd, PERF_EVENT_IOC_ENABLE, 0);

clock_t start, finish;
double duration;


start = clock();
    long i = 100000000L;
    while(i--);
    /* Loop n times, should be good enough for -O0.
    __asm__ (
        "1:;\n"
        "sub $1, %[n];\n"
        "jne 1b;\n"
        : [n] "+r" (n)
        :
        :
    );
    */

finish = clock();
duration = (double)(finish - start) / CLOCKS_PER_SEC;
printf("%.7f seconds\n", duration);
    ioctl(fd, PERF_EVENT_IOC_DISABLE, 0);
    read(fd, &count, sizeof(long long));

    printf("%lld instructions\n", count);

    close(fd);
}

g++ -static -ggdb3 -O0 -std=c++11 -Wall -Wextra -pedantic -o a.out a.c
```


<a href="#top">Back to top</a>
