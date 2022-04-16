## Домашнее задание к занятию "3.3. Операционные системы, лекция 1"

# Задание 1.
Какой системный вызов делает команда `cd`? В прошлом ДЗ мы выяснили, что `cd` не является самостоятельной  программой, это `shell builtin`, поэтому запустить `strace` непосредственно на `cd` не получится. Тем не менее, вы можете запустить `strace` на `/bin/bash -c 'cd /tmp'`. В этом случае вы увидите полный список системных вызовов, которые делает сам `bash` при старте. Вам нужно найти тот единственный, который относится именно к `cd`.

# Ответ:

Системный вызов команды cd /tmp  выглядит как chdir("/tmp") 


# Задание 2.

Попробуйте использовать команду `file` на объекты разных типов на файловой системе. Например:

```bash

vagrant@netology1:~$ file /dev/tty

/dev/tty: character special (5/0)

vagrant@netology1:~$ file /dev/sda

/dev/sda: block special (8/0)

vagrant@netology1:~$ file /bin/bash

/bin/bash: ELF 64-bit LSB shared object, x86-64

```

Используя `strace` выясните, где находится база данных `file` на основании которой она делает свои догадки.

# Ответ:

openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3

и пользовательские:

stat("/home/dhebn/.magic.mgc", 0x7fff8ff29750) = -1 ENOENT (Нет такого файла или каталога)
stat("/home/dhebn/.magic", 0x7fff8ff29750) = -1 ENOENT (Нет такого файла или каталога)
openat(AT_FDCWD, "/etc/magic.mgc", O_RDONLY) = -1 ENOENT (Нет такого файла или каталога)
stat("/etc/magic", {st_mode=S_IFREG|0644, st_size=111, ...}) = 0
openat(AT_FDCWD, "/etc/magic", O_RDONLY) = 3

# Задание 3. 
Предположим, приложение пишет лог в текстовый файл. Этот файл оказался удален (deleted в lsof), однако возможности сигналом сказать приложению переоткрыть файлы или просто перезапустить приложение – нет. Так как приложение продолжает писать в удаленный файл, место на диске постепенно заканчивается. Основываясь на знаниях о перенаправлении потоков предложите способ обнуления открытого удаленного файла (чтобы освободить место на файловой системе).

# Ответ:
```bash
vagrant@vagrant:~$ lsof -p 1126

python3  1126 vagrant    3r   REG    8,2        4 7101175 /home/vagrant/test_txt (deleted)

vagrant@vagrant:~$ echo '' >/proc/1126/fd/3

1126 Pid
```
3 - дескриптор файла , который предварительно удалил.

# 4. Занимают ли зомби-процессы какие-то ресурсы в ОС (CPU, RAM, IO)?

# Ответ:

Зомби процессы освобождают ресурсы, но висят в таблице процессов.

# 5. В iovisor BCC есть утилита `opensnoop`:

    ```bash
    root@vagrant:~# dpkg -L bpfcc-tools | grep sbin/opensnoop
    /usr/sbin/opensnoop-bpfcc
    ```
    На какие файлы вы увидели вызовы группы `open` за первую секунду работы утилиты? Воспользуйтесь пакетом `bpfcc-tools` для Ubuntu 20.04. Дополнительные [сведения по установке](https://github.com/iovisor/bcc/blob/master/INSTALL.md).

# Ответ:

```bash
vagrant@vagrant:~sudo -i
root@vagrant:~# dpkg -L bpfcc-tools | grep sbin/opensnoop
/usr/sbin/opensnoop-bpfcc
root@vagrant:~# /usr/sbin/opensnoop-bpfcc
PID    COMM               FD ERR PATH
766    vminfo              6   0 /var/run/utmp
562    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
562    dbus-daemon        18   0 /usr/share/dbus-1/system-services
562    dbus-daemon        -1   2 /lib/dbus-1/system-services
562    dbus-daemon        18   0 /var/lib/snapd/dbus-1/system-services/
```

# 6. Какой системный вызов использует `uname -a`? Приведите цитату из man по этому системному вызову, где описывается альтернативное местоположение в `/proc`, где можно узнать версию ядра и релиз ОС.

# Ответ:

Используется ситемный вызов - uname()

Part of the utsname information is also accessible via
/proc/sys/kernel/{ostype, hostname, osrelease, version,
domainname}.

# 7. Чем отличается последовательность команд через `;` и через `&&` в bash? Например:

     ```bash
     root@netology:~# test -d /tmp/some_dir; echo Hi
     Hi
     root@netology:~# test -d /tmp/some_dir && echo Hi
     root@netology:~#
     ```
     Есть ли смысл использовать в bash `&&`, если применить `set -e`?

# Ответ:

```bash
&&   - условный оператор, 
;    - разделитель последовательных команд

test -d /tmp/some_dir && echo Hi - в данном случае echo  отработает только при успешном заверщении команды test

set -e - прерывает сессию при любом ненулевом значении исполняемых команд в конвеере кроме последней.
в случае &&  вместе с set -e- вероятно не имеет смысла, так как при ошибке, выполнение команд прекратиться. 
```

# 8. Из каких опций состоит режим bash `set -euxo pipefail` и почему его хорошо было бы использовать в сценариях?

# Ответ:
```bash
-е Немедленный выход, если команда завершается с ненулевым статусом выхода.

-u Неустановленные параметры и переменные считаются как ошибки, с выводом в stderr текста ошибки и выполнит завершение неинтерактивного вызова.

-x Вывод трейса простых команд.

-o pipefail Возвращает код возврата набора последовательности команд, ненулевой при последней команды или 0 для успешного выполнения команд.

 Эти опции повышают деталезацию вывода ошибок при отладке или сбоях.
```

# 9. Используя `-o stat` для `ps`, определите, какой наиболее часто встречающийся статус у процессов в системе. В `man ps` ознакомьтесь (`/PROCESS STATE CODES`) что значат дополнительные к основной заглавной буквы статуса процессов. Его можно не учитывать при расчете (считать S, Ss или Ssl равнозначными).


# Ответ:
```bash
Ss -Прерывистый сон (ожидание завершения события) лидер сеанса

R+ -Работает или готово к работе (в очереди ) находится в группе процессов переднего плана

s -лидер сеанса

+ -находится в группе процессов переднего плана

```