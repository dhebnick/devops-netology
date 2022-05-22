# Домашнее задание к занятию "3.5. Файловые системы"

# Задание 1. Узнайте о [sparse] (разряженных) файлах.

### Ответ:

Хорошо подходит для 

# Задание 2. Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

### Ответ:
 
hardlink - это ссылка на сам файл права доступа и владелец одинаковы 

```bash
user@home42ru:~/test$ touch test
user@home42ru:~/test$ ls -li
total 0
3670030 -rw-rw-r-- 1 user user 0 May 15 07:47 test
user@home42ru:~/test$ ln test hardlink
user@home42ru:~/test$ ls -li
total 0
3670030 -rw-rw-r-- 2 user user 0 May 15 07:47 hardlink
3670030 -rw-rw-r-- 2 user user 0 May 15 07:47 test
user@home42ru:~/test$ chmod +x hardlink
user@home42ru:~/test$ ls -li
total 0
3670030 -rwxrwxr-x 2 user user 0 May 15 07:47 hardlink
3670030 -rwxrwxr-x 2 user user 0 May 15 07:47 test
```

# Задание 3. Сделайте `vagrant destroy` на имеющийся инстанс Ubuntu. Замените содержимое Vagrantfile следующим:

```bash
    Vagrant.configure("2") do |config|
      config.vm.box = "bento/ubuntu-20.04"
      config.vm.provider :virtualbox do |vb|
        lvm_experiments_disk0_path = "/tmp/lvm_experiments_disk0.vmdk"
        lvm_experiments_disk1_path = "/tmp/lvm_experiments_disk1.vmdk"
        vb.customize ['createmedium', '--filename', lvm_experiments_disk0_path, '--size', 2560]
        vb.customize ['createmedium', '--filename', lvm_experiments_disk1_path, '--size', 2560]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk0_path]
        vb.customize ['storageattach', :id, '--storagectl', 'SATA Controller', '--port', 2, '--device', 0, '--type', 'hdd', '--medium', lvm_experiments_disk1_path]
      end
    end
```

    Данная конфигурация создаст новую виртуальную машину с двумя дополнительными неразмеченными дисками по 2.5 Гб.

### Ответ:

```bash
vagrant@vagrant:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 55.4M  1 loop /snap/core18/2128
loop2                       7:2    0 70.3M  1 loop /snap/lxd/21029
loop3                       7:3    0 44.7M  1 loop /snap/snapd/15534
loop4                       7:4    0 55.5M  1 loop /snap/core18/2409
loop5                       7:5    0 61.9M  1 loop /snap/core20/1434
loop6                       7:6    0 67.8M  1 loop /snap/lxd/22753
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0    1G  0 part /boot
└─sda3                      8:3    0   63G  0 part 
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm  /
sdb                         8:16   0  2.5G  0 disk 
sdc                         8:32   0  2.5G  0 disk 
```

# Задание 4. Используя `fdisk`, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.

### Ответ:

```bash
Welcome to fdisk (util-linux 2.34).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0x818f2993.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-5242879, default 2048): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-5242879, default 5242879): +2G

Created a new partition 1 of type 'Linux' and of size 2 GiB.

Command (m for help): n
Partition type
   p   primary (1 primary, 0 extended, 3 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (2-4, default 2): 2
First sector (4196352-5242879, default 4196352): 
Last sector, +/-sectors or +/-size{K,M,G,T,P} (4196352-5242879, default 5242879): 

Created a new partition 2 of type 'Linux' and of size 511 MiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

root@vagrant:/home/vagrant# lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 55.4M  1 loop /snap/core18/2128
loop2                       7:2    0 70.3M  1 loop /snap/lxd/21029
loop3                       7:3    0 44.7M  1 loop /snap/snapd/15534
loop4                       7:4    0 55.5M  1 loop /snap/core18/2409
loop5                       7:5    0 61.9M  1 loop /snap/core20/1434
loop6                       7:6    0 67.8M  1 loop /snap/lxd/22753
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0    1G  0 part /boot
└─sda3                      8:3    0   63G  0 part 
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm  /
sdb                         8:16   0  2.5G  0 disk 
├─sdb1                      8:17   0    2G  0 part 
└─sdb2                      8:18   0  511M  0 part 
sdc                         8:32   0  2.5G  0 disk 

```


# Задание 5. Используя `sfdisk`, перенесите данную таблицу разделов на второй диск.

### Ответ:

```bash
root@vagrant:/home/vagrant# sfdisk -d /dev/sdb| sfdisk --force /dev/sdc
Checking that no-one is using this disk right now ... OK

Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Created a new DOS disklabel with disk identifier 0x818f2993.
/dev/sdc1: Created a new partition 1 of type 'Linux' and of size 2 GiB.
/dev/sdc2: Created a new partition 2 of type 'Linux' and of size 511 MiB.
/dev/sdc3: Done.

New situation:
Disklabel type: dos
Disk identifier: 0x818f2993

Device     Boot   Start     End Sectors  Size Id Type
/dev/sdc1          2048 4196351 4194304    2G 83 Linux
/dev/sdc2       4196352 5242879 1046528  511M 83 Linux

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks
```

# Задание 6. Соберите `mdadm` RAID1 на паре разделов 2 Гб.

### Ответ:

```bash
root@vagrant:/home/vagrant# mdadm --create --verbose /dev/md1 -l 1 -n 2 /dev/sd{b1,c1}
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
mdadm: size set to 2094080K
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md1 started.       
```

# Задание 7. Соберите `mdadm` RAID0 на второй паре маленьких разделов.

### Ответ:

```bash
root@vagrant:/home/vagrant# mdadm --create --verbose /dev/md0 -l 1 -n 2 /dev/sd{b2,c2}
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
mdadm: size set to 522240K
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
```
# Задание 8. Создайте 2 независимых PV на получившихся md-устройствах.

### Ответ:

```bash
root@vagrant:/home/vagrant# pvcreate /dev/md1 /dev/md0
  Physical volume "/dev/md1" successfully created.
  Physical volume "/dev/md0" successfully created.
```

# Задание 9. Создайте общую volume-group на этих двух PV.

### Ответ:

```bash
root@vagrant:/home/vagrant# vgcreate vg1 /dev/md1 /dev/md0
  Volume group "vg1" successfully created
```

# Задание 10. Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

### Ответ:

```bash
root@vagrant:/home/vagrant# lvcreate -L 100M vg1 /dev/md0
  Logical volume "lvol0" created.    
```

# Задание 11. Создайте `mkfs.ext4` ФС на получившемся LV.

### Ответ:
```bash
root@vagrant:/home/vagrant# mkfs.ext4 /dev/vg1/lvol0
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```

# Задание 12. Смонтируйте этот раздел в любую директорию, например, `/tmp/new`.

### Ответ:

```bash
root@vagrant:/home/vagrant# mkdir /tmp/new
root@vagrant:/home/vagrant# mount /dev/vg1/lvol0 /tmp/new
root@vagrant:/home/vagrant# lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55.4M  1 loop  /snap/core18/2128
loop2                       7:2    0 70.3M  1 loop  /snap/lxd/21029
loop3                       7:3    0 44.7M  1 loop  /snap/snapd/15534
loop4                       7:4    0 55.5M  1 loop  /snap/core18/2409
loop5                       7:5    0 61.9M  1 loop  /snap/core20/1434
loop6                       7:6    0 67.8M  1 loop  /snap/lxd/22753
sda                         8:0    0   64G  0 disk  
├─sda1                      8:1    0    1M  0 part  
├─sda2                      8:2    0    1G  0 part  /boot
└─sda3                      8:3    0   63G  0 part  
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk  
├─sdb1                      8:17   0    2G  0 part  
│ └─md1                     9:1    0    2G  0 raid1 
└─sdb2                      8:18   0  511M  0 part  
  └─md0                     9:0    0  510M  0 raid1 
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2.5G  0 disk  
├─sdc1                      8:33   0    2G  0 part  
│ └─md1                     9:1    0    2G  0 raid1 
└─sdc2                      8:34   0  511M  0 part  
  └─md0                     9:0    0  510M  0 raid1 
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
```

# Задание 13. Поместите туда тестовый файл, например `wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz`.

### Ответ:

```bash
root@vagrant:/home/vagrant# wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz
--2022-05-22 15:10:13--  https://mirror.yandex.ru/ubuntu/ls-lR.gz
Resolving mirror.yandex.ru (mirror.yandex.ru)... 213.180.204.183, 2a02:6b8::183
Connecting to mirror.yandex.ru (mirror.yandex.ru)|213.180.204.183|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 23283213 (22M) [application/octet-stream]
Saving to: ‘/tmp/new/test.gz’

/tmp/new/test.gz                                     100%[=====================================================================================================================>]  22.20M  4.66MB/s    in 8.3s    

2022-05-22 15:10:21 (2.68 MB/s) - ‘/tmp/new/test.gz’ saved [23283213/23283213]

root@vagrant:/home/vagrant# ll /tmp/new/
total 22764
drwxr-xr-x  3 root root     4096 May 22 15:10 ./
drwxrwxrwt 11 root root     4096 May 22 15:04 ../
drwx------  2 root root    16384 May 22 14:43 lost+found/
-rw-r--r--  1 root root 23283213 May 22 13:50 test.gz
```

# Задание 14. Прикрепите вывод `lsblk`.

### Ответ:

```bash
root@vagrant:/home/vagrant# lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 55.4M  1 loop  /snap/core18/2128
loop2                       7:2    0 70.3M  1 loop  /snap/lxd/21029
loop3                       7:3    0 44.7M  1 loop  /snap/snapd/15534
loop4                       7:4    0 55.5M  1 loop  /snap/core18/2409
loop5                       7:5    0 61.9M  1 loop  /snap/core20/1434
loop6                       7:6    0 67.8M  1 loop  /snap/lxd/22753
sda                         8:0    0   64G  0 disk  
├─sda1                      8:1    0    1M  0 part  
├─sda2                      8:2    0    1G  0 part  /boot
└─sda3                      8:3    0   63G  0 part  
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.5G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk  
├─sdb1                      8:17   0    2G  0 part  
│ └─md1                     9:1    0    2G  0 raid1 
└─sdb2                      8:18   0  511M  0 part  
  └─md0                     9:0    0  510M  0 raid1 
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2.5G  0 disk  
├─sdc1                      8:33   0    2G  0 part  
│ └─md1                     9:1    0    2G  0 raid1 
└─sdc2                      8:34   0  511M  0 part  
  └─md0                     9:0    0  510M  0 raid1 
    └─vg1-lvol0           253:1    0  100M  0 lvm   /tmp/new
```

# Задание 15. Протестируйте целостность файла:

     ```bash

     root@vagrant:~# gzip -t /tmp/new/test.gz
     root@vagrant:~# echo $?
     0
     ```

### Ответ:

```bash
root@vagrant:/home/vagrant# gzip -t /tmp/new/test.gz && echo $?
0
```

# Задание 16. Используя pvmove, переместите содержимое PV с RAID0 на RAID1.

 ### Ответ:
```bash
root@vagrant:/home/vagrant# pvmove /dev/md0
  /dev/md0: Moved: 68.00%
  /dev/md0: Moved: 100.00%
```

# Задание 17. Сделайте `--fail` на устройство в вашем RAID1 md.

### Ответ:

```bash
root@vagrant:/home/vagrant# mdadm /dev/md1 --fail /dev/sdb1
mdadm: set /dev/sdb1 faulty in /dev/md1
root@vagrant:/home/vagrant# mdadm -D /dev/md1
/dev/md1:
           Version : 1.2
     Creation Time : Sun May 22 14:39:13 2022
        Raid Level : raid1
        Array Size : 2094080 (2045.00 MiB 2144.34 MB)
     Used Dev Size : 2094080 (2045.00 MiB 2144.34 MB)
      Raid Devices : 2
     Total Devices : 2
       Persistence : Superblock is persistent

       Update Time : Sun May 22 15:20:19 2022
             State : clean, degraded 
    Active Devices : 1
   Working Devices : 1
    Failed Devices : 1
     Spare Devices : 0

Consistency Policy : resync

              Name : vagrant:1  (local to host vagrant)
              UUID : cede6b2a:da52500d:8f95d62e:9190423d
            Events : 19

    Number   Major   Minor   RaidDevice State
       -       0        0        0      removed
       1       8       33        1      active sync   /dev/sdc1

       0       8       17        -      faulty   /dev/sdb1

```

# Задание 18. Подтвердите выводом `dmesg`, что RAID1 работает в деградированном состоянии.

### Ответ:

```bash
root@vagrant:/home/vagrant# dmesg | grep md1
[ 1880.132489] md/raid1:md1: not clean -- starting background reconstruction
[ 1880.132491] md/raid1:md1: active with 2 out of 2 mirrors
[ 1880.132516] md1: detected capacity change from 0 to 2144337920
[ 1880.136176] md: resync of RAID array md1
[ 1890.688819] md: md1: resync done.
[ 4346.030742] md/raid1:md1: Disk failure on sdb1, disabling device.
               md/raid1:md1: Operation continuing on 1 devices.

```

# Задание 19. Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:

     ```bash
     root@vagrant:~# gzip -t /tmp/new/test.gz
     root@vagrant:~# echo $?
     0
     ```

### Ответ:

```bash
root@vagrant:/home/vagrant# gzip -t /tmp/new/test.gz && echo $?
0
```

# Задание 20. Погасите тестовый хост, `vagrant destroy`.

### Ответ:

```basha
 ~/netology --------------------------------------- 1h 8m 52s | 22:25:01 
> vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Forcing shutdown of VM...
==> default: Destroying VM and associated drives...
```
