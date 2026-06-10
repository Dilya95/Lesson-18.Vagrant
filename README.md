# Домашнее задание 18: Vagrant

## Задания
1. Подготовка окружения:<br>

Убедитесть, что установле VirtualBox и Vagrant.<br>
Создайте директорию для проекта.<br>
Создать базовую виртуальную машину:<br>
Использовать можно любой образ.<br>
Настроите память ВМ: 1024 МБ.<br>
Добавление дисков:<br>
Добавьте пару виртуальных диска размером 1 ГБ каждый.<br>
Настройка сети:<br>
Настройте проброс 80 порта с гостевой системы на порт 8080 хостовой системы.<br>
Провижининг:<br>

Напишите провижининг, который:<br>
Форматирует добавленные диски в файловую систему ext4.<br>
Создает точки монтирования /mnt/disk1 и /mnt/disk2.<br>
Монтирует диски в указанные директории.<br>
Добавляет записи в /etc/fstab для автоматического монтирования при загрузке.<br>



## Структура
├── README.md<br>
└── Vagrantfile<br>



## Выполнение

### Перешла в созданную для выполнения ДЗ директорию и запустила создание базовой виртуальной машины на базе приложенного в репозитории файла Vagrantfile
```
dilyam@MacBook-Pro-Dilya-2 ~ % cd /Users/dilyam/'linux prof'/'Урок 18'

dilyam@MacBook-Pro-Dilya-2 Урок 18 % vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Importing base box 'bento/ubuntu-26.04'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'bento/ubuntu-26.04' version '202606.01.0' is up to date...
==> default: Setting the name of the VM: 18_default_1781080043087_63097
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 80 (guest) => 8080 (host) (adapter 1)
    default: 22 (guest) => 2222 (host) (adapter 1)
==> default: Configuring storage mediums...
    default: Disk 'extra1' not found in guest. Creating and attaching disk to guest...
    default: Disk 'extra2' not found in guest. Creating and attaching disk to guest...
==> default: Running 'pre-boot' VM customizations...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
==> default: Setting hostname...
==> default: Running provisioner: shell...
    default: Running: inline script
    default: Get:1 http://security.ubuntu.com/ubuntu resolute-security InRelease [137 kB]
    default: Get:2 http://security.ubuntu.com/ubuntu resolute-security/main arm64 Packages [207 kB]
    default: Get:3 http://security.ubuntu.com/ubuntu resolute-security/main Translation-en [54.5 kB]
    default: Get:4 http://security.ubuntu.com/ubuntu resolute-security/main arm64 Components [29.2 kB]
    default: Get:5 http://security.ubuntu.com/ubuntu resolute-security/restricted arm64 Packages [263 kB]
    default: Hit:6 http://us.archive.ubuntu.com/ubuntu resolute InRelease
    default: Get:7 http://security.ubuntu.com/ubuntu resolute-security/restricted Translation-en [35.1 kB]
    default: Get:8 http://us.archive.ubuntu.com/ubuntu resolute-updates InRelease [137 kB]
    default: Get:9 http://security.ubuntu.com/ubuntu resolute-security/universe arm64 Packages [102 kB]
    default: Hit:10 http://us.archive.ubuntu.com/ubuntu resolute-backports InRelease
    default: Get:11 http://security.ubuntu.com/ubuntu resolute-security/universe Translation-en [33.1 kB]
    default: Get:12 http://security.ubuntu.com/ubuntu resolute-security/universe arm64 Components [42.7 kB]
    default: Get:13 http://us.archive.ubuntu.com/ubuntu resolute-updates/main arm64 Packages [216 kB]
    default: Get:14 http://us.archive.ubuntu.com/ubuntu resolute-updates/main Translation-en [56.9 kB]
    default: Get:15 http://us.archive.ubuntu.com/ubuntu resolute-updates/main arm64 Components [35.3 kB]
    default: Get:16 http://us.archive.ubuntu.com/ubuntu resolute-updates/universe arm64 Packages [106 kB]
    default: Get:17 http://us.archive.ubuntu.com/ubuntu resolute-updates/universe Translation-en [34.8 kB]
    default: Get:18 http://us.archive.ubuntu.com/ubuntu resolute-updates/universe arm64 Components [54.7 kB]
    default: Fetched 1,546 kB in 7s (218 kB/s)
    default: Reading package lists...
    default: Reading package lists...
    default: Building dependency tree...
    default: Reading state information...
    default: Solving dependencies...
    default: The following additional packages will be installed:
    default:   nginx-common
    default: Suggested packages:
    default:   fcgiwrap nginx-doc ssl-cert
    default: The following NEW packages will be installed:
    default:   nginx nginx-common
    default: 0 upgraded, 2 newly installed, 0 to remove and 14 not upgraded.
    default: Need to get 645 kB of archives.
    default: After this operation, 1,866 kB of additional disk space will be used.
    default: Get:1 http://us.archive.ubuntu.com/ubuntu resolute-updates/main arm64 nginx-common all 1.28.3-2ubuntu1.4 [37.1 kB]
    default: Get:2 http://us.archive.ubuntu.com/ubuntu resolute-updates/main arm64 nginx arm64 1.28.3-2ubuntu1.4 [608 kB]
    default: dpkg-preconfigure: unable to re-open stdin: No such file or directory
    default: Fetched 645 kB in 1s (474 kB/s)
    default: Selecting previously unselected package nginx-common.
(Reading database… 64209 files and directories currently installed.)
    default: Preparing to unpack …/nginx-common_1.28.3-2ubuntu1.4_all.deb…
    default: Unpacking nginx-common (1.28.3-2ubuntu1.4)…
    default: Selecting previously unselected package nginx.
    default: Preparing to unpack …/nginx_1.28.3-2ubuntu1.4_arm64.deb…
    default: Unpacking nginx (1.28.3-2ubuntu1.4)…
    default: Setting up nginx-common (1.28.3-2ubuntu1.4)…
    default: Created symlink '/etc/systemd/system/multi-user.target.wants/nginx.service' → '/usr/lib/systemd/system/nginx.service'.
    default: Setting up nginx (1.28.3-2ubuntu1.4)…
    default:  * Upgrading binary nginx                                   [ OK ] 
    default: Processing triggers for man-db (2.13.1-1build1)…
    default: Processing triggers for ufw (0.36.2-9build1)…
    default: 
    default: Running kernel seems to be up-to-date (ABI upgrades are not detected).
    default: 
    default: Failed to check for processor microcode upgrades.
    default: 
    default: No services need to be restarted.
    default: 
    default: No containers need to be restarted.
    default: 
    default: No user sessions are running outdated binaries.
    default: 
    default: No VM guests are running outdated hypervisor (qemu) binaries on this host.
    default: === Настраиваем диски ===
    default: Диски: /dev/sdb и /dev/sdc
    default: Форматируем /dev/sdb → ext4
    default: mke2fs 1.47.2 (1-Jan-2025)
    default: Creating filesystem with 262144 4k blocks and 65536 inodes
    default: Filesystem UUID: d5c95de8-3707-4ed9-9f90-d889399010f8
    default: Superblock backups stored on blocks:
    default: 	32768, 98304, 163840, 229376
    default: 
    default: Allocating group tables: done
    default: Writing inode tables: done
    default: Creating journal (8192 blocks): done
    default: Writing superblocks and filesystem accounting information: done
    default: 
    default: Форматируем /dev/sdc → ext4
    default: mke2fs 1.47.2 (1-Jan-2025)
    default: Creating filesystem with 262144 4k blocks and 65536 inodes
    default: Filesystem UUID: 8b4ddabb-de87-4384-a379-aea7922a07c6
    default: Superblock backups stored on blocks:
    default: 	32768, 98304, 163840, 229376
    default: 
    default: Allocating group tables: done
    default: Writing inode tables: done
    default: Creating journal (8192 blocks): done
    default: Writing superblocks and filesystem accounting information: done
    default: 
    default: Записи в fstab добавлены
```

### Проверила статус вм и подключилась к ней
```   
dilyam@MacBook-Pro-Dilya-2 Урок 18 % vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.


dilyam@MacBook-Pro-Dilya-2 Урок 18 % vagrant ssh
Welcome to Ubuntu 26.04 LTS (GNU/Linux 7.0.0-22-generic aarch64)

 * Documentation:  https://docs.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 System information as of Wed Jun 10 09:33:13 AM UTC 2026

  System load:             0.04
  Usage of /:              19.0% of 29.82GB
  Memory usage:            40%
  Swap usage:              0%
  Processes:               115
  Users logged in:         0
  IPv4 address for enp0s8: 10.0.2.15
  IPv6 address for enp0s8: fd17:625c:f037:2:a00:27ff:fe87:9c74


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento

Use of this system is acceptance of the OS vendor EULA and License Agreements.
```

### Приложила вывод проверок
```      
vagrant@otus-homework:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1G  0 part /boot/efi
├─sda2                      8:2    0    2G  0 part /boot
└─sda3                      8:3    0 60.9G  0 part 
  └─ubuntu--vg-ubuntu--lv 252:0    0 30.5G  0 lvm  /
sdb                         8:16   0    1G  0 disk /mnt/disk1
sdc                         8:32   0    1G  0 disk /mnt/disk2


vagrant@otus-homework:~$ cat /etc/fstab
# /etc/fstab: static file system information.
#
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
# / was on /dev/ubuntu-vg/ubuntu-lv during curtin installation
/dev/disk/by-id/dm-uuid-LVM-AOgLLsW63KqYDLMm5OeMezO6333BrXtbTIrpS8HsEaP3khxosydh1EpQUY63f1th / ext4 defaults 0 1
# /boot was on /dev/sda2 during curtin installation
/dev/disk/by-uuid/9cc29847-0cfa-4a84-88cf-20aa25721d7c /boot ext4 defaults 0 1
# /boot/efi was on /dev/sda1 during curtin installation
/dev/disk/by-uuid/6549-253D /boot/efi vfat defaults 0 1
/swap.img	none	swap	sw	0	0
#VAGRANT-BEGIN
# The contents below are automatically generated by Vagrant. Do not modify.
#VAGRANT-END
UUID=d5c95de8-3707-4ed9-9f90-d889399010f8  /mnt/disk1  ext4  defaults  0  2
UUID=8b4ddabb-de87-4384-a379-aea7922a07c6  /mnt/disk2  ext4  defaults  0  2


vagrant@otus-homework:~$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
tmpfs                              164M  944K  163M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv   30G  5.7G   23G  21% /
tmpfs                              408M     0  408M   0% /dev/shm
efivarfs                           256K  9.4K  247K   4% /sys/firmware/efi/efivars
none                               1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs                              408M  4.0K  408M   1% /tmp
none                               1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
/dev/sda2                          2.0G  118M  1.7G   7% /boot
/dev/sda1                          1.1G  6.6M  1.1G   1% /boot/efi
none                               1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
none                               1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
/dev/sdb                           974M  280K  906M   1% /mnt/disk1
/dev/sdc                           974M  280K  906M   1% /mnt/disk2
tmpfs                               82M   12K   82M   1% /run/user/1000


```
