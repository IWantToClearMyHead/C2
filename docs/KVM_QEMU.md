### Qemu

qemu-system means FS(not SE) mode.
```
/usr/bin/qemu-img
/usr/bin/qemu-io
/usr/bin/qemu-nbd
/usr/bin/qemu-pr-helper
/usr/bin/qemu-system-i386
/usr/bin/qemu-system-x86_64
/usr/bin/qemu-system-x86_64-spice
```

For arch linux iso, one can go to [iso](http://mirrors.163.com/archlinux/iso/2022.01.01/)
and using 512M RAM to boot
```
qemu-system-x86_64 -boot d -cdrom archlinux.iso -m 512
```

and if we want use disk, we need to create ourselves,
```
qemu-img create mydisk.img 10G
qemu-system-x86_64 -boot d -cdrom image.iso -m 512 -hda mydisk.img
```

The structure for fs is as below,

to load kernel, disk and gdb, we go 
```
qemu-system-x86_64 -kernel linux/vmlinux -nographic -append "console=ttyS0 root=/dev/sda rw" -drive file=disk.img,format=raw,id=hd0 -S -s
```

and 

```
cd linux
gdb vmlinux # you may see .gdbinit
target remote :1234
b kernel_execve # b point
layout src
c
```



### Image

For an ubuntu img, one can go to [img](http://cloud-images.ubuntu.com/daily/server/daily/server/minimal/releases/) :wink:
```
apt install qemu-img
qemu-img convert -f raw -O qcow2 image.img image.qcow2
qemu-img info image.qcow2
```

| Image format | Argument to qemu-img |
|----------|----------|
| QCOW2 (KVM, Xen) | qcow2 |
| QED (KVM) | qed |
| raw | raw |
| VDI (VirtualBox) | vdi |
| VHD (Hyper-V) | vpc |
| VMDK (VMware) | vmdk |

<a href="#top">Back to top</a>
