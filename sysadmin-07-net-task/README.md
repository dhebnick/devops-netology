# Домашнее задание к занятию "3.7. Компьютерные сети, лекция 2"

1. Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?

###Ответ:

```
nick@nick42ru:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: bond0: <BROADCAST,MULTICAST,MASTER> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 42:60:c1:2f:45:8a brd ff:ff:ff:ff:ff:ff
3: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 06:11:65:c6:c0:f9 brd ff:ff:ff:ff:ff:ff
4: tunl0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
    link/ipip 0.0.0.0 brd 0.0.0.0
5: sit0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
    link/sit 0.0.0.0 brd 0.0.0.0
6: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:15:5d:02:25:db brd ff:ff:ff:ff:ff:ff
    inet 172.19.202.21/20 brd 172.19.207.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::215:5dff:fe02:25db/64 scope link
       valid_lft forever preferred_lft forever

nick@nick42ru:~$ ifconfig -a
bond0: flags=5122<BROADCAST,MASTER,MULTICAST>  mtu 1500
        ether 42:60:c1:2f:45:8a  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

dummy0: flags=130<BROADCAST,NOARP>  mtu 1500
        ether 06:11:65:c6:c0:f9  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.19.202.21  netmask 255.255.240.0  broadcast 172.19.207.255
        inet6 fe80::215:5dff:fe02:25db  prefixlen 64  scopeid 0x20<link>
        ether 00:15:5d:02:25:db  txqueuelen 1000  (Ethernet)
        RX packets 1799  bytes 849921 (849.9 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 85  bytes 5942 (5.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

sit0: flags=128<NOARP>  mtu 1480
        sit  txqueuelen 1000  (IPv6-in-IPv4)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

tunl0: flags=128<NOARP>  mtu 1480
        tunnel   txqueuelen 1000  (IPIP Tunnel)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

В 90% случаев пользуюсь `ip a` в Linux. В Windows конечно `ifconfig`.

2. Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?

###Ответ:

Протокол CDP. Пакет `lldpd`. Команда `lldpctl`.

3. Какая технология используется для разделения L2 коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.
###Ответ:

Технология VLAN. Пакет `vlan`. 

```
auto eth0.7
iface eth0.7 inet static
	address 10.10.20.1
        netmask 255.255.255.0
        vlan_raw_device eth0
```
Можно управлять через утилиту vconfig.


4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.

```
mode=0 (balance-rr)
mode=1 (active-backup)
mode=2 (balance-xor)
mode=3 (broadcast)
mode=4 (802.3ad)
mode=5 (balance-tlb)
mode=6 (balance-alb)
```

```
auto eth0
iface eth0 inet manual
auto eth1
iface eth1 inet manual
auto bond0
iface bond inet static
address 192.168.0.100
netmask 255.255.255.0
gateway 192.168.0.1
dns-nameservers 8.8.8.8
dns-search domain.local
slaves eth0 eth1
bond_mode 4
bond-miimon 100
bond-downdelay 0
bond-updelay 0
```

5. Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.

###Ответ:

В сети с маской /29 - 8 ip-адресов

32 сети можно получить из сети с маской /24

###Пример:

```
10.10.10.0/29

10.10.10.8/29

10.10.10.16/29

10.10.10.24/29
```

6. Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.

###Ответ: `100.64.0.0/26`

7. Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?

###Ответ:

Windows:

`arp -a` - этa komaндa пokaжeт вce зaпиceй ARP нa лokaльнom кomпьютepe

`arp -d -a` - yдaлeниe вceх зaпиceй в тaблицe ARP

`arp -d` - yдaлeниe koнkpeтнoгo IP-aдpeca


Linux:

`ip neigh show` - проверить ARP таблицу

`ip neigh show all` - Эта команда удалит или очистит все записи из таблицы.

`ip neigh del [ip_address] dev [interface]` - удалит запись из таблицы ARP для определенного интерфейса.
