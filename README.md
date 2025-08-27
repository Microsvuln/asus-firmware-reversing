# asus-firmware-reversing


Bootup with full system emulation :

```
DTB_PATH="/home/arash/Downloads/linux-5.10.218/arch/arm/boot/dts/vexpress-v2p-ca9.dtb"
```

```
QEMU_AUDIO_DRV=none qemu-system-arm \
    -M vexpress-a9 \
    -m 512M \
    -kernel /home/arash/Downloads/linux-5.10.218/arch/arm/boot/zImage \
    -dtb "$DTB_PATH" \
    -sd asus_rootfs.img \
    -append "root=/dev/mmcblk0 rw console=ttyAMA0 earlyprintk loglevel=8" \
    -nographic

```


Corrected :

```
QEMU_AUDIO_DRV=none qemu-system-arm \
    -M vexpress-a9 \
    -m 512M \
    -kernel /home/arash/Downloads/linux-5.10.218/arch/arm/boot/zImage \
    -dtb /home/arash/Downloads/linux-5.10.218/arch/arm/boot/dts/vexpress-v2p-ca9.dtb \
    -sd asus_rootfs.img \
    -append "root=/dev/mmcblk0 rw console=ttyAMA0 init=/bin/sh" \
    -nographic
```



networking inside :

```
mount -t proc none /proc
mount -t sysfs none /sys
ifconfig eth0 up
udhcpc -i eth0
```



```
QEMU_AUDIO_DRV=none qemu-system-arm     -M vexpress-a9     -m 512M     -kernel /home/arash/Downloads/linux-5.10.218/arch/arm/boot/zImage     -dtb "$DTB_PATH"     -sd asus_rootfs.img     -append "root=/dev/mmcblk0 rw console=ttyAMA0 init=/bin/sh"     -nographic     -net nic     -netdev user,id=net0,hostfwd=tcp::8080-:80
```



some more logs and networking commands :

```
/ # mount -t proc none /proc
/ # mount -t sysfs none /sys
/ # ifconfig eth0 up
Generic PHY 4e000000.ethernet-ffffffff:01: attached PHY driver [Generic PHY] (mii_bus:phy_addr=4e000000.ethernet-ffffffff:01, irq=POLL)
smsc911x 4e000000.ethernet eth0: SMSC911x/921x identified at 0xa08b0000, IRQ: 30
/ # ifconfig eth0 
eth0      Link encap:Ethernet  HWaddr 52:54:00:12:34:56  
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          Interrupt:30 

/ # ifconfig eth0 10.0.2.15 netmask 255.255.255.0
/ # route add default gw 10.0.2.2
/ # ifconfig eth0 
eth0      Link encap:Ethernet  HWaddr 52:54:00:12:34:56  
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          Interrupt:30 


```
