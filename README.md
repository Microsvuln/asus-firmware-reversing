# asus-firmware-reversing


Bootup with full system emulation :

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
