# Setting up a BTRFS Pool on top of LUKS

Since BTRFS doesn't currently have a built in encryption method we must build our BTRFS pool on top of disks encrypted with LUKS.

#### (Optionally) Create the pool encryption key file.
**If you plan to use a key file, make sure that you are saving it on an encrypted disk**
`dd if=/dev/urandom of=/root/.pool_key bs=2 count=512`

#### Format each drive with the LUKS encryption.
##### Without Key File
`cryptsetup luksFormat /dev/sdX1`

##### With Key File
`cryptsetup luksFormat /dev/sdX1 /root/.pool_key`

#### (Optionally) Add drives to `/etc/crypttab` to unlock at boot
##### Find the UUID of the encrypted partition.
`sudo cryptsetup luksDump /dev/sdX1 | grep "UUID"`

##### Add the following line to your /etc/crypttab
###### /etc/crypttab without file key
`sdb1_crypt UUID=INSERT-UUID-HERE luks,discard`

###### /etc/crypttab with file key
`sdX1_crypt UUID=INSERT-UUID-HERE /root/.pool_key luks,discard`

#### Create BTRFS Pool on top of LUKS mapper devices.
`sudo mkfs.btrfs -f -m raid1 -d raid1 /dev/mapper/sda1_crypt /dev/mapper/sdb1_crypt`

#### Find the UUID of the Pool
`sudo btrfs fi show`

### Mount the pool at boot
###### /etc/fstab
`UUID=INSERT-UUID-HERE       /mnt/pool        btrfs   defaults        0       0`