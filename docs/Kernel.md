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

### boot with fvp



<a href="#top">Back to top</a>
