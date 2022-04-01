### ARM

|bin|hex|axf|
|---|---|---|
|data|data|data|
||addr|addr|
|||debug|

### ISO vs IMG

(ISO)[http://cdimage.ubuntu.com/ubuntu/releases/18.04/release/ubuntu-18.04.6-server-arm64.iso] format is used to create CD and DVD images.

*As of Ubuntu 12.04, the .iso file sizes are now over 700 MB, which means you cannot even burn it to CD any more. You would have to waste a whole 4 GB blank DVD instead—all the more reason to "burn" to USB instead.*

```
# file ubuntu-18.04.6-server-arm64.iso
ubuntu-18.04.6-server-arm64.iso: DOS/MBR boot sector; partition 1 : ID=0xcd, start-CHS (0x0,2,1), end-CHS (0x3e3,33,24), startsector 64, 2038776 sectors; partition 2 : ID=0xef, start-CHS (0x3e3,33,25), end-CHS (0x3e4,11,24), startsector 2038840, 1344 sectors 

# fdisk -l ubuntu-18.04.6-server-arm64.iso
Disk ubuntu-18.04.6-server-arm64.iso: 996.2 MiB, 1044574208 bytes, 2040184 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device                           Boot   Start     End Sectors   Size Id Type
ubuntu-18.04.6-server-arm64.iso1           64 2038839 2038776 995.5M cd unknown
ubuntu-18.04.6-server-arm64.iso2      2038840 2040183    1344   672K ef EFI (FAT-12/16/32)

# 
```


(IMG) format is used to create hard disk image files.

- (ubuntu)[wget http://cloud-images.ubuntu.com/daily/server/daily/server/minimal/releases/bionic/release-20220325/ubuntu-18.04-minimal-cloudimg-amd64.img]


- (busybox)[]

```
$ fdisk grub-busybox-arm64.img

Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.


Command (m for help): p
Disk grub-busybox-arm64.img: 17 MiB, 17825792 bytes, 34816 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: A61F2B17-AE1F-4E83-BA0E-90EC5817A4F0

Device                  Start   End Sectors    Size Type
grub-busybox-arm64.img1  2048  4094    2047 1023.5K Microsoft basic data
grub-busybox-arm64.img2  4096 32766   28671     14M Linux filesystem

Command (m for help): q

$ fdisk -l grub-busybox-arm64.img
Disk grub-busybox-arm64.img: 17 MiB, 17825792 bytes, 34816 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: A61F2B17-AE1F-4E83-BA0E-90EC5817A4F0

Device                  Start   End Sectors    Size Type
grub-busybox-arm64.img1  2048  4094    2047 1023.5K Microsoft basic data
grub-busybox-arm64.img2  4096 32766   28671     14M Linux filesystem
$
```



<a href="#top">Back to top</a>
