### Main

[C2][Main](index.md)😃.

### Ubuntu

- version 

|       version        |       name        |  timeline  |
| -------------------- | ----------------- | ---------- |
| 22.04                | Jammy Jellyfish   | 2022/4/22  |
| 21.1                 | Impish Indri      | 2021/10/14 |
| 21.04                | Hirsute Hippo     | 2021/04/22 |
| 20.1                 | Groovy Gorilla    | 2020/10/22 |
| 20.04 LTS            | Focal Fossa       | 2020/4/23  |
| 19.1                 | Eoan Ermine       | 2019/10/17 |
| 19.04                | Disco Dingo       | 2019/4/19  |
| 18.1                 | Cosmic Cuttlefish | 2018/10/18 |
| 18.04 LTS            | Bionic Beaver     | 2018/4/26  |
| 17.10(GNOME Desktop) | Artful Aardvark   | 2017/10/21 |
| 17.04                | Zesty Zapus       | 2017/4/13  |
| 16.1                 | Yakkety Yak       | 2016/10/20 |
| 16.04 LTS            | Xenial Xerus      | 2016/4/21  |
| 15.1                 | Wily Werewolf     | 2015/10/23 |
| 15.04                | Vivid Vervet      | 2015/4/22  |
| 14.1                 | Utopic Unicorn    | 2014/10/23 |
| 14.04 LTS            | Trusty Tahr       | 2014/4/18  |
| 13.1                 | Saucy Salamander  | 2013/10/17 |
| 13.04                | Raring Ringtail   | 2013/4/25  |
| 12.1                 | Quantal Quetzal   | 2012/10/18 |
| 12.04 LTS            | Precise Pangolin  | 2012/4/26  |
| 11.1                 | Oneiric Ocelot    | 2011/10/13 |
| 11.04(Unity Desktop) | Natty Narwhal     | 2011/4/28  |
| 10.1                 | Maverick Meerkat  | 2010/10/10 |
| 10.04 LTS            | Lucid Lynx        | 2010/4/29  |
| 9.1                  | Karmic Koala      | 2009/10/29 |
| 9.04                 | Jaunty Jackalope  | 2009/4/23  |
| 8.1                  | Intrepid Ibex     | 2008/10/30 |
| 8.04 LTS             | Hardy Heron       | 2008/4/24  |
| 7.1                  | Gutsy Gibbon      | 2007/10/18 |
| 7.04                 | Feisty Fawn       | 2007/4/19  |
| 6.1                  | Edgy Eft          | 2006/10/26 |
| 6.06 LTS             | Dapper Drake      | 2006/6/1   |
| 5.1                  | Breezy Badger     | 2005/10/13 |
| 5.04                 | Hoary Hedgehog    | 2005/4/8   |
| 4.10(First)          | Warty Warthog     | 2004/10/20 |

LTS means long term support, equal to five years. Take 18.04 LTS as an example, it starts from 2018/4/26, ends in 2023/4/26.
[18.04 LTS](https://releases.ubuntu.com/18.04) bases on Linux kernel 4.15, uses OpenJDK 10, Python 3.6, GNOME 3.28, supports LXD 3.0, QEMU 2.11.1, libvirt 4.0, DPDK 17.11.x, Open vSwitch 2.9, Nginx 1.14.0, PHP 7.2.x, Apache 2.4.29.

### Build

Build linux on Ubuntu is simple, follow below steps

- kernel

```
# origin https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.15.6.tar.xz
wget http://ftp.sjtu.edu.cn/sites/ftp.kernel.org/pub/linux/kernel/v4.x/linux-4.15.6.tar.xz
tar -Jvxf linux-4.15.6.tar.xz # decomp

apt-get install git build-essential libelf-dev xz-utils libssl-dev bc libncurses5-dev libncursesw5-dev

# config file
wget https://gitee.com/songtianlun/USTC_OS/raw/master/term2021/lab1/.config 
# export ARCH=x86
make -j20

# wait until
# Kernel: arch/x86/boot/bzImage is ready  (#1)
# then all set
```

the process is as below,

~~~
                                                                                Bootable
                                                              (vmlinuz)         Kernelxxx
┌─────────────┐      ┌─────────────┐     ┌─────────────┐    ┌────────────┐    ┌─────────────┐
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │OBJ   │             │     │             │    │            │OBJ │             │
│  vmlinux    ├─────►│  Image      ├────►│     gz      ├───►│    *.o     ├───►│    zImage   │
│             │ copy │             │gzip │             │asm │            │copy│             │
│     ELF     │      │  BIN        │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
│             │      │             │     │             │    │            │    │             │
└─────────────┘      └─────────────┘     └─────────────┘    └────────────┘    └─────────────┘
     Kernel            Stripped             Compressed
     Porper            Image                Kernel

~~~

bzImage is the Ubuntu kernel file

|  file   |              |            |                                |
| ------- | ------------ | ---------- | ------------------------------ |
| vmlinux | uncompressed | unbootable |                                |
| vmlinuz | compressed   | bootable   |                                |
| zImage  |              |            | copied vmlinuz                 |
| bzImage |              |            | big zImage(for memory > 640KB) |

- rootfs

Build oneline rootfs follow below steps 

```
mkdir rootfs
cd rootfs


# cat init.c

#include <stdio.h>
void main()
{
    printf("Welcome to qemu\n");
    printf("and first program:\n");
    printf("=> init\n");
    fflush(stdout);
    while(1);
}

gcc -static -o init init.c

echo init | cpio -o --format=newc > initramfs

```

### Boot 

- <a name="hw"></a>bare metal hello with [qemu](QEMU_KVM.md) 


```
#
# one should make sure x11 is enable if remote connect 
qemu-system-x86_64 -s \
    -kernel ./linux-4.15.6/arch/x86/boot/bzImage  \
    -initrd ./linux-4.15.6/rootfs/initramfs \
    -append "init=/init" # remove root=/dev/ram, otherwise we have VFS problem
    
# -s, so we can use gdb on tcp:1234
gdb linux-4.15.6/vmlinux

target remote localhost:1234
```

- <a name="hw"></a>mount hello into busybox img with [qemu](QEMU_KVM.md) 

```
tar -jxf busybox-1.32.1.tar.bz2 
cd busybox-1.32.1/
make menuconfig # remember to make static lib
make -j20
make install # this will give _install
qemu-img create -f raw disk.img 1G
sudo mkfs.ext4 disk.img
mkdir rootfs
sudo mount disk.img rootfs
sudo rsync -ar busybox-1.32.1/_inistall/* rootfs/
cd rootfs
sudo chown root:root * -R
sudo mkdir -p proc sys dev etc/init.d
sudo mknod -m 622 dev/console c 5 1
sudo mknod -m 666 dev/null c 1 3
sudo mknod -m 666 dev/zero c 1 5
sudo mknod -m 666 dev/ptmx c 5 2
sudo mknod -m 666 dev/tty c 5 0
sudo mknod -m 444 dev/random c 1 8
sudo mknod -m 444 dev/urandom c 1 9
sudo chown root:tty dev/{console,ptmx,tty}
sudo sh -c 'echo "#!/bin/sh\nmount -t proc none /proc\nmount -t sysfs no'
sudo chmod a+x etc/init.d/rcS
sudo umount rootfs

# bzImage is compressed linux kernel, vmlinux is uncompressed
qemu-system-x86_64 -kernel bzImage -nographic -append "console=ttyS0 root=/dev/sda rw" -drive file=disk.img,format=raw,id=hd0

# one can debug kernel by gdb, remember to enable config though
Kernel hacking->Compile-time checks and compiler options->Compile the kernel with debug info&&Provide GDB scripts for kernel debugging
# one can use vmlinux, if PVH Note is enabled
Processor type and features->Linux guest support->Support for running PVH guests
# F6 save, F9 exit

# add hello
#include <stdio.h>

int main(void)
{
        printf("hello.\n");
        return 0;
}

gcc -static a.c -o hello

# remount
sudo mount disk.img rootfs
sudo mv hello rootfs/usr/sbin/
sudo umount rootfs
# and restart qemu
qemu-system-x86_64 -kernel bzImage -nographic -append "console=ttyS0 root=/dev/sda rw" -drive file=disk.img,format=raw,id=hd0
# below is qemu console
Please press Enter to activate this console. 
/ # hello
hello.
[    8.918524] hello (1038) used greatest stack depth: 13856 bytes left
# ctrl a+x to quit

# -S -s
cd linux
gdb vmlinux
target remote :1234
b start_kernel
layout src
c
```

- <a name="applet"></a>add applet into busybox is so hard💀


- rdn2 with [fvp](https://gitlab.arm.com/arm-reference-solutions/arm-reference-solutions-docs/-/tree/master/docs/infra/rdn2cfg1)

the fvp opens 11 telnet port, s0 = armtf = 0+6 = 12+6
~~~
tcp        0      0 0.0.0.0:5012            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5013            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5014            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5015            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5016            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 localhost:afs3-callback 0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5017            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5018            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5019            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5020            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5021            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf 
tcp        0      0 0.0.0.0:5022            0.0.0.0:*               LISTEN      512127/FVP_RD_N2_Cf

terminal_uart_scp: Listening for serial connection on port 5000

terminal_uart_mcp: Listening for serial connection on port 5001

terminal_ns_uart_ap: Listening for serial connection on port 5002

terminal_s_uart_ap: Listening for serial connection on port 5003

iomacro_terminal_0: Listening for serial connection on port 5004

iomacro_terminal_1: Listening for serial connection on port 5005

terminal_s0: Listening for serial connection on port 5006

terminal_s1: Listening for serial connection on port 5007

terminal_mcp: Listening for serial connection on port 5008

terminal_0: Listening for serial connection on port 5009

terminal_1: Listening for serial connection on port 5010
~~~

- connect via nc
```
nc -nvz 127.0.0.1 5018

nc 127.0.0.1 5018
```

- parameters

|short|long|function|
|---|---|---|
|-S|--cadi-server|start CADI server allowing debuggers to connect to targets in the simulation|
|-R|--run|run the simulation immediately at start of simulation when a debug server is started. Use in combination with --cadi-server or --iris-server|
|-C|--parameter SPEC|set parameter, format: -C INST.PARAM=VALUE|
|-s|--save DIR|Save checkpoint to DIR on simulation exit|
|-r|--restore DIR|Restore checkpoint from DIR on simulation start|
||--log FILE|log|
||--stat|print some run statistics on simulation exit|
|-T|--timelimit N|number of wall clock seconds for the simulator to run, excluding startup and shutdown.|
||--cpulimit N||
||--cyclelimit N||
||--simlimit N||
|-Q|--quantum N|Number of ticks per quantum|
||--start ADDRESS|set initial PC to application start address, format: --start [INST=]ADDRESS|
-o|--output FILE|redirect parameters, memory and instance lists to output file FILE|

```
/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/../../../support/Model/FVP_RD_N2_Cfg1 --data css.scp.armcortexm7ct=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/scp_ramfw.bin@0x0BD80000 --data css.mcp.armcortexm7ct=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/mcp_ramfw.bin@0x0BF80000 -C css.mcp.ROMloader.fname=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/mcp_romfw.bin -C css.scp.ROMloader.fname=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/scp_romfw.bin -C css.trustedBootROMloader.fname=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/tf-bl1.bin -C board.flashloader0.fname=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/rdn2cfg1/fip-uefi.bin -C board.flashloader1.fname=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor1_flash.img -C board.flashloader1.fnameWrite=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor1_flash.img -C board.flashloader2.fname=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor2_flash.img -C board.flashloader2.fnameWrite=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor2_flash.img  -C css.scp.pl011_uart_scp.out_file=rdn2cfg1/refinfra-948586-uart-0-scp_2022-02-08_06.39.15 -C css.scp.pl011_uart_scp.unbuffered_output=1 -C css.scp.pl011_uart_scp.uart_enable=true -C css.pl011_s_uart_ap.out_file=rdn2cfg1/refinfra-948586-uart-0-console_2022-02-08_06.39.15 -C soc.pl011_uart_mcp.out_file=rdn2cfg1/refinfra-948586-uart-0-mcp_2022-02-08_06.39.15 -C soc.pl011_uart_mcp.unbuffered_output=1 -C soc.pl011_uart0.out_file=rdn2cfg1/refinfra-948586-uart-0-armtf_2022-02-08_06.39.15 -C soc.pl011_uart0.unbuffered_output=1 -C soc.pl011_uart0.flow_ctrl_mask_en=1 -C soc.pl011_uart0.enable_dc4=0 -C soc.pl011_uart1.out_file=rdn2cfg1/refinfra-948586-uart-1-mm_2022-02-08_06.39.15 -C soc.pl011_uart1.unbuffered_output=1 -C soc.pl011_uart1.flow_ctrl_mask_en=1 -C soc.pl011_uart1.enable_dc4=0 -C css.pl011_s_uart_ap.unbuffered_output=1 -C css.gic_distributor.ITS-device-bits=20 -C pcie_group_0.pciex16.hierarchy_file_name=\<default\> -C pcie_group_0.pciex16.pcie_rc.ahci0.endpoint.ats_supported=true -C soc.nonPCIe_devices_iomacro.pl330_dma_0.p_controller_nsecure=1 -C soc.nonPCIe_devices_iomacro.pl330_dma_0.p_irq_nsecure=1 -C soc.nonPCIe_devices_iomacro.pl330_dma_0.p_periph_nsecure=1 -C soc.nonPCIe_devices_iomacro.pl330_dma_1.p_controller_nsecure=1 -C soc.nonPCIe_devices_iomacro.pl330_dma_1.p_irq_nsecure=1 -C soc.nonPCIe_devices_iomacro.pl330_dma_1.p_periph_nsecure=1 -C board.virtioblockdevice.image_path=/home/zzx/fvp/rdn2-cfg1/output/rdn2cfg1/grub-busybox.img -C board.flash0.diagnostics=1 -s /home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/rdn2cfg1/  --stat --log rdn2cfg1/log -C board.virtio_net.hostbridge.interfaceName=tap0 -C board.virtio_net.enabled=1 -C board.virtio_net.transport=legacy
```

- figlet design init.sh

```
echo '
 _          _ _
| |__   ___| | | ___
| \  \ / _ \ | |/ _ \
| | | |  __/ | | (_) |
|_| |_|\___|_|_|\___/
                           
  '
```

multiple line must use single quote
-E is the default, which wont convert backslash
-e is the opposite
figlet is a tool for badge
-n is keeping one line for echo
s/\\/\\\\/g
echo ''"'"''

- Autorun [SPEC2017](SPEC2017.md) inside OS via fork 

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <time.h>
#define KNRM  "\x1B[0m"
#define KRED  "\x1B[31m"
#define KGRN  "\x1B[32m"
#define KYEL  "\x1B[33m"
#define KBLU  "\x1B[34m"
#define KMAG  "\x1B[35m"
#define KCYN  "\x1B[36m"
#define KWHT  "\x1B[37m"

int main(void)
{
        FILE *fp;
        char buffer[80];
        printf("Linx : ");
        fp = popen("uname -r", "r");
        fgets(buffer, sizeof(buffer), fp);
        printf("%s", buffer);
        pclose(fp);
        printf("Bbox : ");
        fp = popen("busybox --help | head -n 1", "r");
        fgets(buffer, sizeof(buffer), fp);
        printf("%s", buffer);
        pclose(fp);
        printf("Date : %s\n", __DATE__);
        printf("Time : %s\n", __TIME__);
        //printf("File : %s\n", __FILE__);
        //printf("Line : %d\n", __LINE__);

        unsigned theTick = 0U;
        struct timespec ts, te;
        long start, finish, duration;
        clock_gettime( CLOCK_REALTIME, &ts );
        start = ts.tv_sec;
        printf("=====start @%ld=====\n", start);


        int cpid = fork();
        if(cpid == 0) {
                puts("\e[5m\n"
" _______     ______  \n"
"|  ___\\ \\   / /  _ \\ \n"
"| |_   \\ \\ / /| |_) |\n"
"|  _|   \\ V / |  __/ \n"
"|_|      \\_/  |_|    \e[0m\n");
                printf("Spec : %d\n", 508);
                start = clock();
                //some algorithm
                /*
                long i = 100000000L;
                while(i--);
                */

                int status = system("508/namd_r --input 508/apoa1.input --output 508/apoa1.ref.output --iterations 1");
//              status = execl("508/namd_r", "508/namd_r", "--input", "508/apoa1.input", "--output", "508/apoa1.ref.output", "--iterations", "1", (char*)0);
                //printf("\e[1;34m%f\e[0m seconds\n", duration);
                //printf("%s%f%s\n", KRED, duration, KNRM);
                exit(0);
        }
        printf("\033[4m Running Spec On \033[0m\n");
        wait(cpid);

        clock_gettime( CLOCK_REALTIME, &te );
        finish = te.tv_sec;
        printf("=====finish @%ld=====\n", finish);
        duration = (finish - start);
        printf("Secs : %ld\n", duration);


        theTick  = (te.tv_nsec - ts.tv_nsec) / 1000000;
        theTick += (te.tv_sec - ts.tv_sec) * 1000;
        printf("Tcks : %u\n", theTick);
        //printf("\e[1;34m%6u\e[0m     ticks\n", theTick);
//how to mimic key stroke? so we can exit qemu...
        return 0;
        
}
```

### Sequence

| Poweron |                                                                        |         |
| ------- | ---------------------------------------------------------------------- | ------- |
| ALARM   |                                                                        | di      |
| POST    | CPU－ROM－BIOS－System Clock－DMA－RAM－IRQ－GC(graphic card)－I/O－CMOS |         |
| BIOS    | Nor－Flash                                                              |         |
| MBR     | copy 512byte boot loader from SSD ROM to DDR RAM                       | stage1  |
| GRUB    | load vmlinuz initramfs                                                 | stage2  |
| Kernel  | start_kernel()                                                         |         |
| Rootfs  | /sbin/init, set runlevel from /etc/inittab                             |         |
|         | /etc/rcS.d/, then /etc/rcN.d/, N equal to runlevel                     |         |
|         | /etc/rcS.d/S35mountall.sh                                              | mount   |
|         | /etc/rcS.d/S40networking                                               | network |
|         | /etc/rc2.d/S13gdm                                                      | login   |
|         | /etc/rc2.d/S20makedev                                                  | dev     |
|         | /etc/rc2.d/S23xinetd                                                   | xinetd  |

initramfs equal to using cpio put initrd into kernel
initrd equal to initial ramdisk

### DDR

- memory

Memory in modern linux is not accessed directly. A virtual address space is used that is backed by physical memory. Conceptually, virtual and physical memory is divided into chunks called pages. The typical page size is 4096 bytes.

So, what does this buy us? Well, quite a lot, as it turns out. For one, there's less memory management hassle while sharing memory among processes. This model is also more secure, as each process has its own virtual memory space (memory isolation). It also yields virtually unlimited memory, as backing with physical pages can be on-demand (demand paging). Moreover, the system can swap inactive pages to the hard drive. Refer to our article on managing swap-space for additional information.

Virtual memory space is segregated into user and kernel space. The kernel space is the higher part of the virtual memory address space. For example, in x86_64 architecture, this mapping starts at 0xffff800000000000.

Besides memory regions, hardware architectures also provide restrictions on I/O ports and CPU instructions. For example, in x86, we have four protection rings numbered 0 to 3, although in Linux, we only use ring-0 (kernel mode) and ring-3 (user mode).

If a user process requires services that are restricted, it can use system calls (syscalls). Collectively, these syscalls form an interface for user applications to access kernel resources.

In the user space, we can find the user stack that grows downward to lower addresses, whereas dynamic allocations (heap) grow upwards to higher addresses. The user stack is only used while the process is running in user mode.

The kernel stack is part of the kernel space. Hence, it is not directly accessible from a user process. Whenever a user process uses a syscall, the CPU mode switches to kernel mode. During the syscall, the kernel stack of the running process is used.

The size of the kernel stack is configured during compilation and remains fixed. This is usually two pages (8KB) for each thread. Moreover, additional per-CPU interrupt stacks are used to process external interrupts. While the process runs in user mode, these special stacks don’t have any useful data.

Unlike the kernel stack, we can change the user stack via `ulimit`.

- space

|         |                              32                               |                                       64                                        |
| ------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| address | 4GB(2^32)                                                     | 16EB(2^64)                                                                      |
| user    | 0~3G                                                          | 128TB（0x0000 00000000∼0x7FFF FFFFFFFF                                           |
| kernel  | 3G~4G                                                         | 128TB（0xFFFF8000 00000000∼0xFFFFFFFF FFFFFFFF）                                 |
| cpu     | 32-bit operating systems and applications require 32-bit CPUs | 64-bit OS demands 64-bit CPU, and 64-bit applications require 64-bit OS and CPU |
| ram     | 3.2 GB                                                        | 17 Billion GB                                                                   |
|         |                                                               |                                                                                 |

- C layout


user space (reserve -> text -> data -> bss -> heap -> ... -> mmap -> stack -> argc, argv -> env)                                                  -> kernel space

reserve: null
text: cpu instruction code
data: variables not equal to 0
bss: variables equal to 0
heap: to high
mmap: dynamic so, input file
stack: to low





<a href="#top">Back to top</a>
