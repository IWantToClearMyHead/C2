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

For arch linux iso, one can go to [archlinux](http://mirrors.163.com/archlinux/iso/2022.01.01/)
and using 512M RAM to boot, remember to enable gtk or x11,
```
qemu-system-x86_64 -boot d -cdrom archlinux.iso -m 512
```

and if we want use disk, we need to create ourselves,
```
qemu-img create mydisk.img 10G
qemu-system-x86_64 -boot d -cdrom image.iso -m 512 -hda mydisk.img
```

The structure for fs is as below,





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


### [hello world](Kernel.md#hw)
the most simple fs, only one command and looping... 

### busybox

```
wget https://busybox.net/downloads/busybox-1.32.1.tar.bz2
tar -jxvf busybox-1.32.1.tar.bz2
# select static binary
make menuconfig
make -j20
make install
# now you should have _install

cd _install/
sudo mkdir dev 
sudo mknod dev/console c 5 1
sudo mknod dev/ram b 1 0 
sudo touch init
sudo vi init

#!/bin/sh
echo "INIT SCRIPT"
mkdir /proc
mkdir /sys
mount -t proc none /proc
mount -t sysfs none /sys
mkdir /tmp
mount -t tmpfs none /tmp
echo -e "\nThis boot took $(cut -d' ' -f1 /proc/uptime) seconds\n"
exec /bin/sh

sudo chmod +x init

find . -print0 | cpio --null -ov --format=newc | gzip -9 > initramfs-busybox-x64.cpio.gz

```

and with bzImage run

```
qemu-system-x86_64 -s \
    -kernel bzImage  \
    -initrd initramfs-busybox-x64.cpio.gz \
    --append "nokaslr root=/dev/ram init=/init"
```

### Parameter
| para  | note  |
| --- | --- |
| -M vexpress-a9 | machine: vexpress-a9 |
| -m 512M | dram=512MB |
| -cpu cortex-a9 | cpu arch=a9 |
| -smp n | cpu number, def=1 |
| -kernel ./zImage | image |
| -dtb ./vexpress-vap-ca9.dtb | device tree |
| -append cmdline | linux kernel options |
| -initrd file | use file for booting ram disk |
| -nographic | disable graph |
| -sd rootfs.ext3 | sd=rootfs.ext3 |
| -net nic | network |
| -net nic -net tap | bridge between host and guest |


<a href="#top">Back to top</a>
