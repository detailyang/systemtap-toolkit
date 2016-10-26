NAME
====
my systemtap toolkit to online analyze on production

Table of Contents
=================

* [NAME](#name)
* [tcp-passive-syn-ack-time](#tcp-passive-syn-ack-time)
* [tcp-active-syn-ack-time](#tcp-active-syn-ack-time)
* [tcp-retrans](#tcp-retrans)
* [who-open-file](#who-open-file)
* [syscall-connect](#syscall-connect)
* [sample-bt](#sample-bt)
* [watch-wvar](#watch-var)


tcp-passive-syn-ack-time
===============
````bash
[root@localhost tmp]# ./tcp-passive-syn-ack-timee -p 80 -t 5000
Collecting tcp dport (80)...syn-ack time

interval min:197us, max:858us avg:519us, cnt:3
value |-------------------------------------------------- count
   32 |                                                   0
   64 |                                                   0
  128 |@                                                  1
  256 |@                                                  1
  512 |@                                                  1
 1024 |                                                   0
 2048 |                                                   0
````



tcp-active-syn-ack-time
===============

````bash
[root@localhost systemtap-toolkit]# ./tcp-active-syn-ack-time -p 80 -t 5000
Collecting tcp dport (80)...syn-ack time

dport:80 min:417us, max:542us avg:460us, cnt:3
value |-------------------------------------------------- count
   64 |                                                   0
  128 |                                                   0
  256 |@@                                                 2
  512 |@                                                  1
 1024 |                                                   0
 2048 |                                                   0

````

tcp-retrans
===========
````bash
[root@localhost systemtap-toolkit]# ./tcp-retrans
Printing tcp retransmission

10.0.2.15:49896 -> 172.17.9.41:80 state:TCP_SYN_SENT rto:0 -> 1000 ms
10.0.2.15:49896 -> 172.17.9.41:80 state:TCP_SYN_SENT rto:1000 -> 2000 ms
10.0.2.15:49896 -> 172.17.9.41:80 state:TCP_SYN_SENT rto:2000 -> 4000 ms
````

who-open-file
=============

````bash
[root@localhost systemtap-toolkit]# ./who-open-file -f 123 -t 10000
Collecting who is opening filename 123

cat(13740) is opening the filename: "123"
cat(13741) is opening the filename: "123"
````

syscall-connect
==============
````bash
telnet(8062) is connecting to AF_INET@192.168.33.10:1800
telnet(8063) is connecting to AF_INET@192.168.33.10:1800
telnet(8064) is connecting to AF_INET@192.168.33.10:1800
telnet(8065) is connecting to AF_INET@192.168.33.10:1800
telnet(8066) is connecting to AF_INET@192.168.33.10:1800
telnet(8067) is connecting to AF_INET@192.168.33.10:1800
telnet(8068) is connecting to AF_INET@192.168.33.10:1800
telnet(8069) is connecting to AF_INET@192.168.33.10:1800
telnet(8070) is connecting to AF_INET@192.168.33.10:1800
````

sample-bt
=========
from [agentzh](https://github.com/openresty/nginx-systemtap-toolkit#sample-bt)
````bash
$ ./sample-bt -p 8736 -t 5 -u > a.bt
WARNING: Tracing 8736 (/opt/nginx/sbin/nginx) in user-space only...
WARNING: Missing unwind data for module, rerun with 'stap -d stap_df60590ce8827444bfebaf5ea938b5a_11577'
WARNING: Time's up. Quitting now...(it may take a while)
WARNING: Number of errors: 0, skipped probes: 24
````

watch-var
=========

````bash
[root@localhost systemtap-toolkit]# ./watch-var  -f syscall.open -v filename -p 25849
WARNING: Tracing vars syscall.open filename in 25849...
a.out[25849] kernel.function("SyS_open@fs/open.c:1036").call filename: "" => ""./test""
````
