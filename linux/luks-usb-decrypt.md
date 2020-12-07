## How to Automatically Decrypt a LUKS disk with a USB Key
1)
```
fdisk ${USB_DEVICE} <<EOF
o
n
p
1
 
+64M
w
EOF
```
2)
```
mkfs.ext4 ${USB_DEVICE}1
```
3)
```
mkdir /boot/tmp
```
4)
```
mount {USB_DEVICE}1 /boot/tmp
```
5)
```
dd if=/dev/urandom of=/boot/tmp/.boot_key bs=2 count=512
```
6)
```
cryptsetup luksAddKey /dev/disk/by-uuid/{LUKS_VOLUME_UUID} /boot/tmp/.boot_key
```
7) Create
##### /etc/dracut.conf.d/usb-decrypt.conf
```
omit_dracutmodules+="systemd"
filesystems+="ext4"
```
8)
```
dracut -fv
```
9) Modify `/etc/default/grub` and add to `CMDLINE_LINUX`
```
rd.luks.key=/.boot_key:UUID={USB_DEVICE_UUID}
```
10)
```
update-grub
```
