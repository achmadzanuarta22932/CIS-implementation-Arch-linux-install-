persiapkan partisi dengan 

crytpsetup ke /dev/[partisi] lalu open dengan luksOpen /dev/[partisi]
buat pvcreate, vgcreate, lvcreate 
setelahnya masukan format _mkfs.ext4_ untuk format linux , _mkfs.vfat_ untuk bootloader 

mount dengan penerapan - _rw,nosuid,nodev,noexec,relatime_

pacstrap /mnt amd-ucode linux-lts linux-lts-headers linux-firmware base docker  neovim lvm2 firewalld pacman which grep sudo curl iwd mkinitcpio 

