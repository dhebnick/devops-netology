# Домашнее задание к занятию "3.5. Файловые системы"

# Задание 1. Узнайте о [sparse] (разряженных) файлах.

### Ответ:

Хорошо подходит для 

# Задание 2. Могут ли файлы, являющиеся жесткой ссылкой на один объект, иметь разные права доступа и владельца? Почему?

### Ответ:
 
hardlink - это всего лишь ссылка на сам файл права доступа и владелец одинаковы 

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

```

# Задание 4. Используя `fdisk`, разбейте первый диск на 2 раздела: 2 Гб, оставшееся пространство.

### Ответ:

```bash

```

# Задание 5. Используя `sfdisk`, перенесите данную таблицу разделов на второй диск.

### Ответ:

```bash

```

# Задание 6. Соберите `mdadm` RAID1 на паре разделов 2 Гб.

### Ответ:

```bash
       
```

# Задание 7. Соберите `mdadm` RAID0 на второй паре маленьких разделов.

### Ответ:

```bash

```
# Задание 8. Создайте 2 независимых PV на получившихся md-устройствах.

### Ответ:

```bash

```

# Задание 9. Создайте общую volume-group на этих двух PV.

### Ответ:

```bash
   
```

# Задание 10. Создайте LV размером 100 Мб, указав его расположение на PV с RAID0.

### Ответ:

```bash
    
```

# Задание 11. Создайте `mkfs.ext4` ФС на получившемся LV.

### Ответ:
```bash

```

# Задание 12. Смонтируйте этот раздел в любую директорию, например, `/tmp/new`.

### Ответ:

```bash


```

# Задание 13. Поместите туда тестовый файл, например `wget https://mirror.yandex.ru/ubuntu/ls-lR.gz -O /tmp/new/test.gz`.

### Ответ:

```bash
 
```

# Задание 14. Прикрепите вывод `lsblk`.

### Ответ:

```bash

```

# Задание 15. Протестируйте целостность файла:

     ```bash

     root@vagrant:~# gzip -t /tmp/new/test.gz
     root@vagrant:~# echo $?
     0
     ```

### Ответ:

```bash



```

# Задание 16. Используя pvmove, переместите содержимое PV с RAID0 на RAID1.

 ### Ответ:
```bash

```

# Задание 17. Сделайте `--fail` на устройство в вашем RAID1 md.

### Ответ:

```bash

```

# Задание 18. Подтвердите выводом `dmesg`, что RAID1 работает в деградированном состоянии.

### Ответ:

```bash

```

# Задание 19. Протестируйте целостность файла, несмотря на "сбойный" диск он должен продолжать быть доступен:

     ```bash
     root@vagrant:~# gzip -t /tmp/new/test.gz
     root@vagrant:~# echo $?
     0
     ```

### Ответ:
```bash

```

# Задание 20. Погасите тестовый хост, `vagrant destroy`.

### Ответ:

```basha

```
