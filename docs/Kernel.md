### Build
```
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.9.263.tar.xz
tar -Jvxf linux-4.9.263.tar.xz # decomp

apt-get install git build-essential libelf-dev xz-utils libssl-dev bc libncurses5-dev libncursesw5-dev

# config file
wget https://gitee.com/songtianlun/USTC_OS/raw/master/term2021/lab1/.config 

make -j20

# wait until
Kernel: arch/x86/boot/bzImage is ready  (#1)
# the all set
```

the process is as below,

~~~
                                                                                Bootable
                                                              (vmlinux)         Kernelxxx
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

### rootfs
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

### boot with [qemu](QEMU_KVM.md) 

- <a name="hw"></a>bare metal helloworld
```
#
# one should make sure x11 is enable if remote connect 
qemu-system-x86_64 -s \
    -kernel ./linux-4.9.263/arch/x86/boot/bzImage  \
    -initrd ./linux-4.9.263/rootfs/initramfs \
    -append "init=/init" # remove root=/dev/ram, otherwise we have VFS problem
    
# -s, so we can use gdb on tcp:1234
gdb linux-4.9.263/vmlinux

target remote localhost:1234
```
- we can mount helloworld into busybox
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
sudo makdir -p proc sys dev etc/init.d
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
        printf("hello, fvp.\n");
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
hello, fvp.
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


### boot with [fvp](https://gitlab.arm.com/arm-reference-solutions/arm-reference-solutions-docs/-/tree/master/docs/infra/rdn2cfg1)

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
```
/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/../../../support/Model/FVP_RD_N2_Cfg1
--data
css.scp.armcortexm7ct=../../../../output/rdn2cfg1/rdn2cfg1/scp_ramfw.bin@0x0BD80000
--data
css.mcp.armcortexm7ct=../../../../output/rdn2cfg1/rdn2cfg1/mcp_ramfw.bin@0x0BF80000
-C
css.mcp.ROMloader.fname=../../../../output/rdn2cfg1/rdn2cfg1/mcp_romfw.bin
-C
css.scp.ROMloader.fname=../../../../output/rdn2cfg1/rdn2cfg1/scp_romfw.bin
-C
css.trustedBootROMloader.fname=../../../../output/rdn2cfg1/rdn2cfg1/tf-bl1.bin
-C
board.flashloader0.fname=../../../../output/rdn2cfg1/rdn2cfg1/fip-uefi.bin
-C
board.flashloader1.fname=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor1_flash.img
-C
board.flashloader1.fnameWrite=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor1_flash.img
-C
board.flashloader2.fname=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor2_flash.img
-C
board.flashloader2.fnameWrite=/home/zzx/fvp/rdn2-cfg1/model-scripts/rdinfra/platforms/rdn2cfg1/nor2_flash.img
-S
-R
-C
css.scp.pl011_uart_scp.out_file=rdn2cfg1/refinfra-370754-uart-0-scp_2022-02-07_09.55.03
-C
css.scp.pl011_uart_scp.unbuffered_output=1
-C
css.scp.pl011_uart_scp.uart_enable=true
-C
css.pl011_s_uart_ap.out_file=rdn2cfg1/refinfra-370754-uart-0-console_2022-02-07_09.55.03
-C
soc.pl011_uart_mcp.out_file=rdn2cfg1/refinfra-370754-uart-0-mcp_2022-02-07_09.55.03
-C
soc.pl011_uart_mcp.unbuffered_output=1
-C
soc.pl011_uart0.out_file=rdn2cfg1/refinfra-370754-uart-0-armtf_2022-02-07_09.55.03
-C
soc.pl011_uart0.unbuffered_output=1
-C
soc.pl011_uart0.flow_ctrl_mask_en=1
-C
soc.pl011_uart0.enable_dc4=0
-C
soc.pl011_uart1.out_file=rdn2cfg1/refinfra-370754-uart-1-mm_2022-02-07_09.55.03
-C
soc.pl011_uart1.unbuffered_output=1
-C
soc.pl011_uart1.flow_ctrl_mask_en=1
-C
soc.pl011_uart1.enable_dc4=0
-C
css.pl011_s_uart_ap.unbuffered_output=1
-C
css.gic_distributor.ITS-device-bits=20
-C
pcie_group_0.pciex16.hierarchy_file_name=<default>
-C
pcie_group_0.pciex16.pcie_rc.ahci0.endpoint.ats_supported=true
-C
soc.nonPCIe_devices_iomacro.pl330_dma_0.p_controller_nsecure=1
-C
soc.nonPCIe_devices_iomacro.pl330_dma_0.p_irq_nsecure=1
-C
soc.nonPCIe_devices_iomacro.pl330_dma_0.p_periph_nsecure=1
-C
soc.nonPCIe_devices_iomacro.pl330_dma_1.p_controller_nsecure=1
-C
soc.nonPCIe_devices_iomacro.pl330_dma_1.p_irq_nsecure=1
-C
soc.nonPCIe_devices_iomacro.pl330_dma_1.p_periph_nsecure=1
-C
board.virtioblockdevice.image_path=../../../../output/rdn2cfg1/grub-busybox.img
-C
board.flash0.diagnostics=1
```

<a href="#top">Back to top</a>
