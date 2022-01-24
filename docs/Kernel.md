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

# we can try binding helloworld into busybox


```


<a href="#top">Back to top</a>
