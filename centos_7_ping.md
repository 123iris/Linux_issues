# Issues In Centos 7 

## 1. Not able to ping google.com

* Not able to ping to google.com or other domains but able to ping using there IP address

### Issue

```
[root@oNode ~]# ping am.tfrnd.net
ping: am.tfrnd.net: Name or service not known
[root@oNode ~]# 
[root@oNode ~]# 
[root@oNode ~]# ping 13.235.64.124             				# This is the public IP am.tfrnd.net
PING 13.235.64.124 (13.235.64.124) 56(84) bytes of data.
64 bytes from 13.235.64.124: icmp_seq=1 ttl=48 time=50.1 ms
64 bytes from 13.235.64.124: icmp_seq=2 ttl=48 time=69.3 ms
^C
--- 13.235.64.124 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 50.144/59.725/69.307/9.584 ms
[root@oNode ~]# 
[root@oNode ~]# 
[root@oNode ~]# ping localhost
PING localhost (127.0.0.1) 56(84) bytes of data.
64 bytes from localhost (127.0.0.1): icmp_seq=1 ttl=64 time=0.044 ms
64 bytes from localhost (127.0.0.1): icmp_seq=2 ttl=64 time=0.112 ms
^C
--- localhost ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1000ms
rtt min/avg/max/mdev = 0.044/0.078/0.112/0.034 ms
```

### Solution:

* Problem is with DNS. Add 8.8.8.8 8.8.4.4 into /etc/resolv.conf file

```
$ sudo vi /etc/resolv.conf

nameserver 8.8.8.8 8.8.4.4
```

* Now try to ping am.tfrnd.net or google.com

```
[root@oNode ~]# ping am.tfrnd.net
PING am.tfrnd.net (13.235.64.124) 56(84) bytes of data.
64 bytes from ec2-13-235-64-124.ap-south-1.compute.amazonaws.com (13.235.64.124): icmp_seq=1 ttl=48 time=44.6 ms
64 bytes from ec2-13-235-64-124.ap-south-1.compute.amazonaws.com (13.235.64.124): icmp_seq=2 ttl=48 time=65.9 ms
64 bytes from ec2-13-235-64-124.ap-south-1.compute.amazonaws.com (13.235.64.124): icmp_seq=3 ttl=48 time=70.5 ms
^C
--- am.tfrnd.net ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 44.610/60.392/70.579/11.319 ms
[root@oNode ~]# 
[root@oNode ~]# 
[root@oNode ~]# ping google.com
PING google.com (172.217.163.206) 56(84) bytes of data.
64 bytes from maa05s06-in-f14.1e100.net (172.217.163.206): icmp_seq=1 ttl=115 time=42.8 ms
64 bytes from maa05s06-in-f14.1e100.net (172.217.163.206): icmp_seq=2 ttl=115 time=45.9 ms
^C
--- google.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 42.835/44.380/45.926/1.559 ms
```