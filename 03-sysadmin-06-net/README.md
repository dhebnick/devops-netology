# Ответы на домашнее задание "3.6. Компьютерные сети, лекция 1"

# Задание №1. Работа c HTTP через telnet.

- Подключиться утилитой telnet к сайту stackoverflow.com
- Отправить HTTP запрос
- Показать послученый HTTP код и объяснить, что он означает.

# Ответ:
```bash
telnet stackoverflow.com 80
Trying 151.101.129.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 23c30d6a-0951-4302-b295-2bd762e9bd91
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Wed, 09 Mar 2022 07:00:37 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-ams21028-AMS
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1646809237.219889,VS0,VE75
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=6e6c01cd-eeed-c443-b456-09d32d28e1ed; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.

```

Пришел код 301 означающий, что страница переехала навсегда (Moved Permanently).
Так же, в пункте "location" указано куда переехала страница.

# Задача №2. Повторить задание №1 в браузере, используя консоль разработчика.
2.1 Откройте вкладку Network

2.2 отправить запрос http://stackoverflow.com

2.3 первый ответ от HTTP сервера, во вкладке Headers

2.4 указать в ответе полученый HTTP код

2.5 какой запрос обрабатывался дольше всего, во ремя загрузки страницы?

2.6 скриншот консоли браузера в ответе

# Ответы:
2.6. https://disk.yandex.ru/i/Nk73wHncmfkhlA

2.5. Дольше сего обрабатыавлся скрипт beacon.js - 10.31s

2.4. 307 Внутреннее перенаправление

2.3. перенапраление на https

# Задача №3. Какой IP адрес у вас в интернете?
# Ответ:
У меня публичный "белый" IP-адрес

# Задача №4 Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois
# Ответ:

Провайдер - JSC "Zap-Sib TransTeleCom"

```bash
whois 0.0.0.0
% This is the RIPE Database query service.
% The objects are in RPSL format.
%
% The RIPE Database is subject to Terms and Conditions.
% See http://www.ripe.net/db/support/db-terms-conditions.pdf

% Note: this output has been filtered.
%       To receive output for a database update, use the "-B" flag.

% Information related to '0.0.0.0 - 0.0.0.255'

% Abuse contact for '0.0.0.0 - 0.0.0.255' is 'abuse@ttk.ru'

inetnum:        0.0.0.0 - 0.0.0.255
netname:        mediadom
descr:          "MediaDom" Ltd. is a Berezovsky ISP
country:        RU
admin-c:        PB7423-RIPE
tech-c:         PB7423-RIPE
tech-c:         ZTTK-RIPE
status:         ASSIGNED PA
mnt-by:         ZSTTK-MNT
created:        2008-07-23T12:35:45Z
last-modified:  2008-07-23T14:03:17Z
source:         RIPE # Filtered

role:           ZSTTK NOC
address:        JSC "Zap-Sib TransTeleCom"
address:        Komsomolqskijj Avenue, 1/4
address:        630004, Novosibirsk, box 103
address:        Russia
phone:          +7 383 3358181
fax-no:         +7 383 3358182
org:            ORG-JTN1-RIPE
admin-c:        VAK104-RIPE
tech-c:         AME25-RIPE
abuse-mailbox:  noc-security@zsttk.ru
nic-hdl:        ZTTK-RIPE
remarks:        -----------------------------------------
remarks:        Routing questions:  noc@zsttk.ru
remarks:        Spam & Abuse:       noc-security@zsttk.ru
remarks:        -----------------------------------------
remarks:        ---------- A T T E N T I O N  -----------
remarks:        Please use noc-security@zsttk.ru for spam
remarks:        and abuse complaints.
remarks:        Mails for other addresses will be ignored
remarks:        -----------------------------------------
mnt-by:         ZSTTK-MNT
created:        2004-11-15T12:06:18Z
last-modified:  2015-03-06T03:10:34Z
source:         RIPE # Filtered

person:         Pavel Baturin
address:        Russia
phone:          +7 384 455 7788
nic-hdl:        PB7423-RIPE
created:        2008-07-09T13:27:41Z
last-modified:  2014-09-03T02:36:06Z
source:         RIPE # Filtered
mnt-by:         LIDERTELECOM-mnt
mnt-by:         MDOM-MNT

% Information related to '0.0.0.0/23AS15774'

route:          0.0.0.0
descr:          RU-ZSTTK-20190701
origin:         AS15774
mnt-by:         ZSTTK-MNT
created:        2019-07-01T07:11:43Z
last-modified:  2019-07-01T07:11:43Z
source:         RIPE

% This query was served by the RIPE Database Query Service version 1.102.2 (HEREFORD)
```

# Задача №5 Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute
# Ответ:

```bash
traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
1  172.20.240.1 [*]  4.956 ms  4.794 ms  4.772 ms
2  10.10.20.1 [*]  2.744 ms  2.689 ms  2.646 ms
3  82.200.59.1 [AS15774]  5.268 ms  4.578 ms  4.103 ms
4  81.1.200.233 [AS20485]  2.436 ms  3.181 ms  2.548 ms
5  217.150.44.118 [AS20485]  3.887 ms  3.859 ms  3.745 ms
6  * * *
7  188.43.29.74 [AS20485]  7.721 ms  7.761 ms 188.43.29.66 [AS20485]  8.114 ms
8  188.43.29.49 [AS20485]  8.100 ms  8.391 ms  8.357 ms
9  217.150.55.234 [AS20485]  46.941 ms  44.156 ms  44.130 ms
10  188.43.10.141 [AS20485]  42.882 ms  42.861 ms  42.776 ms
11  108.170.250.34 [AS15169]  45.719 ms * *
12  142.251.49.24 [AS15169]  61.471 ms 209.85.255.136 [AS15169]  61.266 ms *
13  72.14.238.168 [AS15169]  67.403 ms 216.239.48.224 [AS15169]  55.285 ms 108.170.235.204 [AS15169]  55.252 ms
14  172.253.51.239 [AS15169]  53.677 ms 172.253.79.169 [AS15169]  53.295 ms 72.14.235.193 [AS15169]  60.352 ms
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  8.8.8.8 [AS15169]  54.302 ms  57.819 ms  53.839 ms
```

# Задача №6 Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка - delay?
# Ответ:

```bash
My traceroute  [v0.93]
nick42ru (172.20.242.101)                                           2022-03-10T00:21:28+0700
Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                       Packets               Pings
Host                                              Loss%   Snt   Last   Avg  Best  Wrst StDev
1. AS???    172.20.240.1                           0.0%    15    0.8   0.5   0.3   0.9   0.2
2. AS???    10.10.20.1                             0.0%    15    2.8   2.3   1.9   3.1   0.3
3. AS21127  0.0.0.0                                0.0%    15    2.4   2.9   2.4   3.3   0.2
4. AS21127  81.1.200.233                           0.0%    15    3.6   4.2   2.8  20.3   4.4
5. AS20485  217.150.44.118                         0.0%    15    3.6   3.4   3.0   4.0   0.3
6. (waiting for reply) 
7. AS20485  188.43.29.74                           0.0%    15    7.5   7.6   7.4   8.3   0.2
8. AS20485  188.43.29.49                           0.0%    15    8.0   8.7   8.0  11.5   0.9
9. AS20485  217.150.55.234                         6.7%    15   47.0  47.8  46.8  56.2   2.5
10. AS20485  188.43.10.141                         0.0%    15   45.7  45.6  45.1  46.9   0.5
11. AS15169  108.170.250.83                        0.0%    15   66.5  54.2  47.4  75.5  10.4
12. AS15169  142.251.237.156                      57.1%    15   58.1  58.8  57.9  61.0   1.1
13. AS15169  142.251.237.142                       0.0%    15   61.0  56.8  54.9  63.2   2.8
14. AS15169  172.253.70.47                         0.0%    15   58.4  58.6  58.3  59.1   0.2
15. (waiting for reply)
16. (waiting for reply)
17. (waiting for reply)
18. (waiting for reply)
19. (waiting for reply)
20. (waiting for reply)
21. (waiting for reply)
22. (waiting for reply)
23. (waiting for reply)
24. AS15169  8.8.8.8                               0.0%    14   58.0  58.3  57.9  59.0   0.3
```

Наибольшая задержка на участке 108.170.250.83 - 142.251.237.156

# Задача №7 Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой dig
# Ответ:

```bash
;; ANSWER SECTION:
dns.google.             0       IN      A       8.8.8.8
dns.google.             0       IN      A       8.8.4.4
```

# Задача №8 Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой dig

```bash
dig -x 8.8.8.8

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.8.8
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24617
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;8.8.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 100 msec
;; SERVER: 172.20.240.1#53(172.20.240.1)
;; WHEN: Thu Mar 10 01:52:12 +07 2022
;; MSG SIZE  rcvd: 82

dig -x 8.8.4.4

; <<>> DiG 9.16.1-Ubuntu <<>> -x 8.8.4.4
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 49928
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;4.4.8.8.in-addr.arpa.          IN      PTR

;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.   0       IN      PTR     dns.google.

;; Query time: 50 msec
;; SERVER: 172.20.240.1#53(172.20.240.1)
;; WHEN: Thu Mar 10 01:52:20 +07 2022
;; MSG SIZE  rcvd: 82
```

В обоих случаях PTR запись указыает на dns.google.
