persiapkan partisi dengan 

crytpsetup ke /dev/[partisi] lalu open dengan luksOpen /dev/[partisi]
buat pvcreate, vgcreate, lvcreate 
setelahnya masukan format _mkfs.ext4_ untuk format linux , _mkfs.vfat_ untuk bootloader 

mount dengan penerapan - _rw,nosuid,nodev,noexec,relatime_

untuk root dan var tidak memerlukan noexec akan dapat di baca 

pacstrap /mnt amd-ucode linux-lts linux-lts-headers linux-firmware base docker  neovim lvm2 firewalld pacman which grep sudo curl iwd mkinitcpio

genfstab -U /mnt >> /mnt/etc/fstab 

echo "tmpfs /tmp tmpfs defaults,rw,nodev,nosuid,noexec,relatime,size=1G 0 0" >> /mnt/etc/fstab 


## copy network 

cat /mnt/etc/fstab 

cp /etc/systemd/network/* /mnt/etc/systemd/network/


ls /mnt/etc/systemd/network

arch-chroot /mnt 

echo "advanworkplus" > /etc/hostname

ln -sf /usr/share/zoneinfo/Asia/Jakarta /etc/localtime 

hwclock --systohc 

nvim /etc/locale.gen 

discoment #en_US

locale-gen

locale > /etc/locale.conf

nvim /etc/locale.conf 

ganti C ke en_US.UTF-8
isi all ke en_US.UTF-8

useradd -m "namauser"

passwd "namauser"

echo "user ALL=(ALL:ALL) ALL" >> /etc/sudoers.d/administrator

## membuat kernel parameter 

mkdir /etc/cmdline.d

touch /etc/cmdline.d/{01-boot.conf,02-misc.conf}

ls /etc/cmdline.d/

echo "rd.luks.name=$(blkid -s UUID -o value /dev/lvmrootpwrtition)=[namadevice] root=/dev/[namavolumegroup]/root" >> /etc/cmdline.d/01-boot.conf

cat /etc/cmdline.d/01-boot.conf 

lsblk -o name, uuid 

## initramfs 

informasi kernel, fstab, module 
habus dan edit configurasi ulang 

ls /boot

rm /boot/initramfs-linux-lts.img 

ls /boot/

## configurasi initramfs

nvim /etc/mkinitcpio.conf

cari like hooks 

masukan setelah sd-vconsole

sd-encrypt lvm2 

nvim /etc/mkinitcpio.d/linux-lts.preset

uncomenting 
ALl_config 
 ALL_kver

nanti dah di sini ini 


touch /etc/vconsole.conf 

bootctl --path=/boot install

generate ulang initramfs 

mkinitcpio -P 

 



 


 



 











 

