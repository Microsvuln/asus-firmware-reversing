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
