### Perf Flame

```
git clone https://github.com/brendangregg/FlameGraph.git
```

### CPU Time
~~~
CPU time = CPU clock cycles x clock cycle time = CPU clock cycles / clock rate(this is frequency, i.e. 2.6GHz)

CPU clock cycles = (instructions/program) x (clock cycles/instruction) = Instruction count x CPI

CPU time = Instruction count x CPI / clock rate(i.e. 256739 * 0.66 / 2.6E9 = 0.00006517 = 0.6ms)

~~~

### CPI
~~~
Assume that a benchmark has 100 instructions:
25 instructions are loads/stores (each take 2 cycles)
50 instructions are adds (each takes 1 cycle)
25 instructions are square root (each takes 50 cycles)

What is the CPI for this benchmark?
CPI = ((0.25 * 2) + (0.50 * 1) + (0.25 * 50)) = 13.5
~~~

|||||||||
|---|---|---|---|---|---|---|---|
|Op|F|CPI|CPI|x|F|%|Time|
|ALU|50%|1|.5|23%|
|Load|20%|5|1.0|45%|
|Store|10%|3|.3|14%|
|Branch|20%|2|.4|18%|
|Total|100%|2.2|100%|

<a href="#top">Back to top</a>
