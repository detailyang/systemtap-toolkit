# systemtap-toolkit
my systemtap toolkit to online analyze 

#Usage

##tcp-syn-ack-time

````bash
[root@localhost tmp]# ./tcp-syn-ack-time -p 80 -t 5000
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
