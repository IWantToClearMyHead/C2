### Platform

* `FVP_Base_AEMv8A-AEMv8A-AEMv8A-AEMv8A-CCN502`
    
* `FVP_Base_AEMv8A-AEMv8A` (For certain configurations also uses 11.14/21)
    
* `FVP_Base_AEMv8A-GIC600AE`
    
* `FVP_Base_AEMvA` (For certain configurations also uses 0.0/6684)
    
* `FVP_Base_Cortex-A32x4` (Version 11.12/38)
    
* `FVP_Base_Cortex-A35x4`
    
* `FVP_Base_Cortex-A53x4`
    
* `FVP_Base_Cortex-A55x4`
    
* `FVP_Base_Cortex-A55x4+Cortex-A75x4`
    
* `FVP_Base_Cortex-A57x1-A53x1`
    
* `FVP_Base_Cortex-A57x2-A53x4`
    
* `FVP_Base_Cortex-A57x4-A53x4`
    
* `FVP_Base_Cortex-A57x4`
    
* `FVP_Base_Cortex-A65AEx8`
    
* `FVP_Base_Cortex-A65x4`
    
* `FVP_Base_Cortex-A710x4`
    
* `FVP_Base_Cortex-A72x4-A53x4`
    
* `FVP_Base_Cortex-A72x4`
    
* `FVP_Base_Cortex-A73x4-A53x4`
    
* `FVP_Base_Cortex-A73x4`
    
* `FVP_Base_Cortex-A75x4`
    
* `FVP_Base_Cortex-A76AEx4`
    
* `FVP_Base_Cortex-A76AEx8`
    
* `FVP_Base_Cortex-A76x4`
    
* `FVP_Base_Cortex-A77x4`
    
* `FVP_Base_Cortex-A78x4`
    
* `FVP_Base_Neoverse-E1x1`
    
* `FVP_Base_Neoverse-E1x2`
    
* `FVP_Base_Neoverse-E1x4`
    
* `FVP_Base_Neoverse-N1x4`
    
* 
```diff
+ FVP_Base_Neoverse-N2x4` (Version 11.12 build 38)
```
    
* `FVP_Base_Neoverse-V1x4`
    
* `FVP_Base_RevC-2xAEMvA` (For certain configurations also uses 0.0/6557)
    
* `FVP_CSS_SGI-575` (Version 11.15/26)
    
* `FVP_Morello` (Version 0.11/19)
    
* `FVP_RD_E1_edge` (Version 11.15/26)
    
* `FVP_RD_N1_edge_dual` (Version 11.15/26)
    
* `FVP_RD_N1_edge` (Version 11.15/26)
    
* `FVP_RD_V1` (Version 11.15/26)
    
* `FVP_TC0`
    
* `FVP_TC1`

### Alpine

- host
```
./build-scripts/build-test-uefi.sh -p rdn2cfg1 all
export MODEL=/home/alpine/models/Linux64_GCC-6.4/FVP_RD_N2_Cfg1

ip tuntap add dev tap0 mode tap user root
ifconfig tap0 0.0.0.0 promisc up
brctl addif virbr0 tap0

./distro.sh -p rdn2cfg1 -i /home/alpine/alpine-standard-3.15.0-aarch64.iso -s 16 -n true
ps aux grep FVP
screen //telnet 127.0.0.1 5018
```
- guest
```
ip addr add 192.168.122.22/24 dev eth0
ip link show eth0
ip link set eth0 up
 
echo "nameserver 192.168.122.1" >  /etc/resolv.conf 
echo "nameserver 8.8.8.8" >> /etc/resolv.conf
cat /etc/resolv.conf
route add default gw 192.168.122.1 eth0

cat /etc/issue

echo "http://dl-cdn.alpinelinux.org/alpine/v3.15/main" > /etc/apk/repositories
echo "http://dl-cdn.alpinelinux.org/alpine/v3.15/community" >> /etc/apk/repositories
sleep 1
echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
cat /etc/apk/repositories

sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories

cat > a.c << EOF; $(echo)
#include <stdio.h>
int main()
{
  printf("Hello world\n");
}
EOF

gcc a.c

```

<a href="#top">Back to top</a>
