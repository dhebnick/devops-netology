# Домашнее задание к занятию "3.8. Компьютерные сети, лекция 3"

1. Подключитесь к публичному маршрутизатору в интернет. Найдите маршрут к вашему публичному IP
```
telnet route-views.routeviews.org
Username: rviews
show ip route x.x.x.x/32
show bgp x.x.x.x/32
```

###Ответ:

```
route-views>show ip route 000.000.000.000
Routing entry for 93.190.104.0/21
  Known via "bgp 6447", distance 20, metric 0
  Tag 3333, type external
  Last update from 193.0.0.56 2d06h ago
  Routing Descriptor Blocks:
  * 193.0.0.56, from 193.0.0.56, 2d06h ago
      Route metric is 0, traffic share count is 1
      AS Hops 4
      Route tag 3333
      MPLS label: none
route-views>show bgp 000.000.000.000
BGP routing table entry for 93.190.104.0/21, version 2302876461
Paths: (24 available, best #21, table default)
  Not advertised to any peer
  Refresh Epoch 1
  8283 31133 50928 47433
    94.142.247.3 from 94.142.247.3 (94.142.247.3)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 8283:1 8283:101 50928:12420
      unknown transitive attribute: flag 0xE0 type 0x20 length 0x18
        value 0000 205B 0000 0000 0000 0001 0000 205B
              0000 0005 0000 0001
      path 7FE0231D8840 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  53767 174 31133 31133 31133 31133 50928 47433
    162.251.163.2 from 162.251.163.2 (162.251.162.3)
      Origin IGP, localpref 100, valid, external
      Community: 174:21101 174:22005 53767:5000
      path 7FE0FB9ABE78 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  19214 174 31133 31133 31133 31133 50928 47433
    208.74.64.40 from 208.74.64.40 (208.74.64.40)
      Origin IGP, localpref 100, valid, external
      Community: 174:21101 174:22005
      path 7FE16088AEB0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3549 3356 9002 9002 9002 9002 9002 9049 48858 47433 47433 47433 47433 47433 47433
    208.51.134.254 from 208.51.134.254 (67.16.168.191)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 3356:2 3356:22 3356:100 3356:123 3356:503 3356:903 3356:2067 3549:2581 3549:30840
      path 7FE16B686E28 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  701 174 31133 31133 31133 31133 50928 47433
    137.39.3.55 from 137.39.3.55 (137.39.3.55)
      Origin IGP, localpref 100, valid, external
      path 7FE04A4B9758 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3356 9002 9002 9002 9002 9002 9049 48858 47433 47433 47433 47433 47433 47433
    4.68.4.46 from 4.68.4.46 (4.69.184.201)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 3356:2 3356:22 3356:100 3356:123 3356:503 3356:903 3356:2067
      path 7FE022C757E0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3561 3910 3356 9002 9002 9002 9002 9002 9049 48858 47433 47433 47433 47433 47433 47433
    206.24.210.80 from 206.24.210.80 (206.24.210.80)
      Origin IGP, localpref 100, valid, external
      path 7FE0A1BB65F8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  57866 9002 9049 48858 47433 47433 47433 47433 47433 47433
    37.139.139.17 from 37.139.139.17 (37.139.139.17)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 9002:0 9002:64667
      path 7FE0EE39CFC8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  7018 1299 31133 31133 31133 31133 50928 47433
    12.0.1.63 from 12.0.1.63 (12.0.1.63)
      Origin IGP, localpref 100, valid, external
      Community: 7018:5000 7018:37232
      path 7FE02A06A638 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  4901 6079 31133 50928 47433
    162.250.137.254 from 162.250.137.254 (162.250.137.254)
      Origin IGP, localpref 100, valid, external
      Community: 65000:10100 65000:10300 65000:10400
      path 7FE13E0438D0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  6939 31133 50928 47433
    64.71.137.241 from 64.71.137.241 (216.218.252.164)
      Origin IGP, localpref 100, valid, external
      path 7FE0BCBC6938 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20912 3257 28917 28917 28917 28917 28917 28917 28917 48858 48858 48858 47433 47433 47433 47433 47433 47433
    212.66.96.126 from 212.66.96.126 (212.66.96.126)
      Origin IGP, localpref 100, valid, external
      Community: 3257:4000 3257:8092 3257:50001 3257:50111 3257:54800 3257:54801 20912:65004
      path 7FE0874EED38 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3267 31133 50928 47433
    194.85.40.15 from 194.85.40.15 (185.141.126.1)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE18BC0B508 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3303 31133 50928 47433
    217.192.89.50 from 217.192.89.50 (138.187.128.158)
      Origin IGP, localpref 100, valid, external
      Community: 3303:1004 3303:1006 3303:1030 3303:3056 50928:12420
      path 7FE16875F418 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1221 4637 31133 50928 47433
    203.62.252.83 from 203.62.252.83 (203.62.252.83)
      Origin IGP, localpref 100, valid, external
      path 7FE13CF2B608 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 2
  2497 174 31133 31133 31133 31133 50928 47433
    202.232.0.2 from 202.232.0.2 (58.138.96.254)
      Origin IGP, localpref 100, valid, external
      path 7FE07E737CF8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  101 174 31133 31133 31133 31133 50928 47433
    209.124.176.223 from 209.124.176.223 (209.124.176.223)
      Origin IGP, localpref 100, valid, external
      Community: 101:20100 101:20110 101:22100 174:21101 174:22005
      Extended Community: RT:101:22100
      path 7FE187D7D6E8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  852 31133 50928 47433
    154.11.12.212 from 154.11.12.212 (96.1.209.43)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE04D7B00D0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  7660 2516 3257 28917 28917 28917 28917 28917 28917 28917 48858 48858 48858 47433 47433 47433 47433 47433 47433
    203.181.248.168 from 203.181.248.168 (203.181.248.168)
      Origin IGP, localpref 100, valid, external
      Community: 2516:1030 7660:9003
      path 7FE0B4ED5460 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3257 28917 28917 28917 28917 28917 28917 28917 48858 48858 48858 47433 47433 47433 47433 47433 47433
    89.149.178.10 from 89.149.178.10 (213.200.83.26)
      Origin IGP, metric 10, localpref 100, valid, external
      Community: 3257:4000 3257:8092 3257:50001 3257:50111 3257:54800 3257:54801
      path 7FE16F612028 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3333 31133 50928 47433
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin IGP, localpref 100, valid, external, best
      Community: 50928:12420
      path 7FDFFBEF9928 RPKI State not found
      rx pathid: 0, tx pathid: 0x0
  Refresh Epoch 1
  49788 12552 31133 50928 47433
    91.218.184.60 from 91.218.184.60 (91.218.184.60)
      Origin IGP, localpref 100, valid, external
      Community: 12552:12000 12552:12100 12552:12101 12552:22000
      Extended Community: 0x43:100:1
      path 7FE0DFA5BF38 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20130 6939 31133 50928 47433
    140.192.8.16 from 140.192.8.16 (140.192.8.16)
      Origin IGP, localpref 100, valid, external
      path 7FE11F3033F8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1351 6939 31133 50928 47433
    132.198.255.253 from 132.198.255.253 (132.198.255.253)
      Origin IGP, localpref 100, valid, external
      path 7FE0AF623C98 RPKI State not found
      rx pathid: 0, tx pathid: 0
```

2. Создайте dummy0 интерфейс в Ubuntu. Добавьте несколько статических маршрутов. Проверьте таблицу маршрутизации.

###Ответ:

```
user@home42ru:~$ ifconfig -a | grep dummy
dummy0: flags=195<UP,BROADCAST,RUNNING,NOARP>  mtu 1500
user@home42ru:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eno1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether d0:27:88:c1:10:a3 brd ff:ff:ff:ff:ff:ff
    inet 10.10.20.10/24 brd 10.10.20.255 scope global dynamic eno1
       valid_lft 86157sec preferred_lft 86157sec
    inet6 fe80::d227:88ff:fec1:10a3/64 scope link
       valid_lft forever preferred_lft forever
3: dummy0: <BROADCAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc noqueue state UNKNOWN group default qlen 1000
    link/ether ce:37:b8:be:9d:c8 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::cc37:b8ff:febe:9dc8/64 scope link
       valid_lft forever preferred_lft forever

user@home42ru:~$ sudo ip route add 10.10.40.0/24 via 10.10.20.1
user@home42ru:~$ sudo ip route add 10.10.50.0/24 dev dummy0
user@home42ru:~$ routel
         target            gateway          source    proto    scope    dev tbl
        default         10.10.20.1     10.10.20.10     dhcp            eno1
    10.10.20.0/ 24                     10.10.20.10   kernel     link   eno1
     10.10.20.1                        10.10.20.10     dhcp     link   eno1
    10.10.40.0/ 24      10.10.20.1                                     eno1
    10.10.50.0/ 24                                              link dummy0
     10.10.20.0          broadcast     10.10.20.10   kernel     link   eno1 local
    10.10.20.10              local     10.10.20.10   kernel     host   eno1 local
   10.10.20.255          broadcast     10.10.20.10   kernel     link   eno1 local
      127.0.0.0          broadcast       127.0.0.1   kernel     link     lo local
     127.0.0.0/ 8            local       127.0.0.1   kernel     host     lo local
      127.0.0.1              local       127.0.0.1   kernel     host     lo local
127.255.255.255          broadcast       127.0.0.1   kernel     link     lo local
            ::1                                      kernel              lo
        fe80::/ 64                                   kernel            eno1
        fe80::/ 64                                   kernel          dummy0
            ::1              local                   kernel              lo local
fe80::cc37:b8ff:febe:9dc8              local                   kernel          dummy0 local
fe80::d227:88ff:fec1:10a3              local                   kernel            eno1 local
/usr/bin/routel: 48: shift: can't shift that many
```

3. Проверьте открытые TCP порты в Ubuntu, какие протоколы и приложения используют эти порты? Приведите несколько примеров.

###Ответ:

```
user@home42ru:~$ sudo ss -lnpt
State        Recv-Q       Send-Q             Local Address:Port             Peer Address:Port       Process
LISTEN       0            80                     127.0.0.1:3306                  0.0.0.0:*           users:(("mysqld",pid=773,fd=22))
LISTEN       0            4096               127.0.0.53%lo:53                    0.0.0.0:*           users:(("systemd-resolve",pid=599,fd=13))
LISTEN       0            128                      0.0.0.0:22                    0.0.0.0:*           users:(("sshd",pid=785,fd=3))
LISTEN       0            511                            *:80                          *:*           users:(("apache2",pid=122480,fd=4),("apache2",pid=122479,fd=4),("apache2",pid=122478,fd=4),("apache2",pid=122477,fd=4),("apache2",pid=122476,fd=4),("apache2",pid=820,fd=4))
LISTEN       0            128                         [::]:22                       [::]:*           users:(("sshd",pid=785,fd=4))
user@home42ru:~$ sudo netstat -plnut
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      773/mysqld
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      599/systemd-resolve
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      785/sshd: /usr/sbin
tcp6       0      0 :::80                   :::*                    LISTEN      820/apache2
tcp6       0      0 :::22                   :::*                    LISTEN      785/sshd: /usr/sbin
udp        0      0 127.0.0.53:53           0.0.0.0:*                           599/systemd-resolve
udp        0      0 10.10.20.10:68          0.0.0.0:*                           126360/systemd-netw
user@home42ru:~$ sudo ss -plnut
Netid     State      Recv-Q     Send-Q             Local Address:Port           Peer Address:Port     Process
udp       UNCONN     0          0                  127.0.0.53%lo:53                  0.0.0.0:*         users:(("systemd-resolve",pid=599,fd=12))
udp       UNCONN     0          0               10.10.20.10%eno1:68                  0.0.0.0:*         users:(("systemd-network",pid=126360,fd=17))
tcp       LISTEN     0          80                     127.0.0.1:3306                0.0.0.0:*         users:(("mysqld",pid=773,fd=22))
tcp       LISTEN     0          4096               127.0.0.53%lo:53                  0.0.0.0:*         users:(("systemd-resolve",pid=599,fd=13))
tcp       LISTEN     0          128                      0.0.0.0:22                  0.0.0.0:*         users:(("sshd",pid=785,fd=3))
tcp       LISTEN     0          511                            *:80                        *:*         users:(("apache2",pid=122480,fd=4),("apache2",pid=122479,fd=4),("apache2",pid=122478,fd=4),("apache2",pid=122477,fd=4),("apache2",pid=122476,fd=4),("apache2",pid=820,fd=4))
tcp       LISTEN     0          128                         [::]:22                     [::]:*         users:(("sshd",pid=785,fd=4))
user@home42ru:~$ sudo lsof -nP -iTCP -sTCP:LISTEN
COMMAND      PID            USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
systemd-r    599 systemd-resolve   13u  IPv4  23747      0t0  TCP 127.0.0.53:53 (LISTEN)
mysqld       773           mysql   22u  IPv4  27687      0t0  TCP 127.0.0.1:3306 (LISTEN)
sshd         785            root    3u  IPv4  26787      0t0  TCP *:22 (LISTEN)
sshd         785            root    4u  IPv6  26789      0t0  TCP *:22 (LISTEN)
apache2      820            root    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
apache2   122476        www-data    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
apache2   122477        www-data    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
apache2   122478        www-data    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
apache2   122479        www-data    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
apache2   122480        www-data    4u  IPv6  26579      0t0  TCP *:80 (LISTEN)
```

4. Проверьте используемые UDP сокеты в Ubuntu, какие протоколы и приложения используют эти порты?

```
user@home42ru:~$ sudo ss -lpnu
State                        Recv-Q                       Send-Q                                                Local Address:Port                                             Peer Address:Port                       Process
UNCONN                       0                            0                                                     127.0.0.53%lo:53                                                    0.0.0.0:*                           users:(("systemd-resolve",pid=599,fd=12))
UNCONN                       0                            0                                                  10.10.20.10%eno1:68                                                    0.0.0.0:*                           users:(("systemd-network",pid=126360,fd=17))
```

5. Используя diagrams.net, создайте L3 диаграмму вашей домашней сети или любой другой сети, с которой вы работали. 

[home-lan](https://disk.yandex.ru/i/-9eyaY8QK4Ogbg)

