 # Part 1 : Most simplest LAN¶

## 3. Know your MAC

🌞 Déterminer l'adresse MAC de vos deux machines

-Node1
```sh
node1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node1  0.0.0.0/0            0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64
```

-Node2
```sh
node2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node2  0.0.0.0/0            0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64

```

4. IP Setup¶
🌞 Définir une IP statique sur les deux machines

```sh
node1> ip 10.1.1.1
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

node2>
node2> ip 10.1.1.2
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0
```

🌞 Proof !

```sh
node1> show ip

NAME        : node1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 10002
RHOST:PORT  : 127.0.0.1:10003
MTU:        : 1500

node2> show ip

NAME        : node2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 10000
RHOST:PORT  : 127.0.0.1:10001
MTU:        : 1500
```

🌞 Effectuer un ping d'une machine à l'autre

```sh
node1> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=1.357 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=1.499 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=2.196 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=0.909 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=1.467 ms

node2> ping 10.1.1.1
84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=1.723 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=2.345 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=1.747 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=1.695 ms
84 bytes from 10.1.1.1 icmp_seq=5 ttl=64 time=2.177 ms
```

5. Analyze¶
➜ Wireshark !

Voire node1.pcap and node2.pcap

🌞 Protocolz ?

```sh
Protocole ICMP ( Internet 

-Wireshark
Dispo dans 📁 p1_ping.pcap
```

# Part 2 : Bring that switch in¶

## 3. Même chose en fast¶

🌞 Déterminer l'adresse MAC de vos trois machines
```sh
node1> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node1  0.0.0.0/0            0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64
node2> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node2  0.0.0.0/0            0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64
node3> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node3  0.0.0.0/0            0.0.0.0           00:50:79:66:68:04  10012  127.0.0.1:10013
       fe80::250:79ff:fe66:6804/64
```

🌞 Définir une IP statique sur les trois machines

```sh
node1> ip 10.1.1.1
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

node1> show ip

NAME        : node1[1]
IP/MASK     : 10.1.1.1/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:01
LPORT       : 10002
RHOST:PORT  : 127.0.0.1:10003
MTU:        : 1500

node2> show ip

NAME        : node2[1]
IP/MASK     : 10.1.1.2/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:00
LPORT       : 10000
RHOST:PORT  : 127.0.0.1:10001
MTU:        : 1500

node3> ip 10.1.1.3
Checking for duplicate address...
PC1 : 10.1.1.3 255.255.255.0

node3> show ip

NAME        : node3[1]
IP/MASK     : 10.1.1.3/24
GATEWAY     : 0.0.0.0
DNS         :
MAC         : 00:50:79:66:68:04
LPORT       : 10012
RHOST:PORT  : 127.0.0.1:10013
MTU:        : 1500
```

🌞 Effectuer des ping d'une machine à l'autre

```sh
node1>  ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.855 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=2.290 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=1.365 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=2.126 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=2.449 ms

node2> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=0.944 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=1.686 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=2.097 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=2.428 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=1.906 ms

node1>  ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=1.932 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=1.235 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=1.648 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=1.492 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=2.972 ms
```

# 4. ARP old friend

🌞 Afficher la table ARP de node1
```sh
node1> arp

00:50:79:66:68:00  10.1.1.2 expires in 33 seconds
00:50:79:66:68:04  10.1.1.3 expires in 49 seconds
```

# Part 3 : DHCP is a nice guy

# 3. Setuuuup 
➜ Donner un accès Internet à la machine dhcp.tp1.efrei

-Test avec srv dns de google 
```sh
[gustave@vbox ~]$ ping  8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=255 time=148 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=255 time=43.2 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=255 time=35.9 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=255 time=52.5 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=255 time=39.4 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=255 time=35.8 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=255 time=34.1 ms
^C
--- 8.8.8.8 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6017ms
rtt min/avg/max/mdev = 34.113/55.580/148.096/38.214 ms
```

🌞 Installer un serveur DHCP

```sh
[gustave@vbox ~]$ sudo dnf -y install dhcp-server
Last metadata expiration check: 0:00:38 ago on Thu 08 Jan 2026 12:49:22 AM CET.
Dependencies resolved.
===================================================================================================================================
 Package                        Architecture              Version                                  Repository                 Size
===================================================================================================================================
Installing:
 dhcp-server                    x86_64                    12:4.4.2-19.b1.el9                       baseos                    1.2 M
Installing dependencies:
 dhcp-common                    noarch                    12:4.4.2-19.b1.el9                       baseos                    128 k

Transaction Summary
===================================================================================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M
Downloading Packages:
(1/2): dhcp-common-4.4.2-19.b1.el9.noarch.rpm                                                      157 kB/s | 128 kB     00:00
(2/2): dhcp-server-4.4.2-19.b1.el9.x86_64.rpm                                                      1.2 MB/s | 1.2 MB     00:01
-----------------------------------------------------------------------------------------------------------------------------------
Total                                                                                              858 kB/s | 1.3 MB     00:01
Rocky Linux 9 - BaseOS                                                                             364 kB/s | 1.7 kB     00:00
Importing GPG key 0x350D275D:
 Userid     : "Rocky Enterprise Software Foundation - Release key 2022 <releng@rockylinux.org>"
 Fingerprint: 21CB 256A E16F C54C 6E65 2949 702D 426D 350D 275D
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-Rocky-9
Key imported successfully
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                           1/1
  Installing       : dhcp-common-12:4.4.2-19.b1.el9.noarch                                                                     1/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                     2/2
  Installing       : dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                     2/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                     2/2
  Verifying        : dhcp-common-12:4.4.2-19.b1.el9.noarch                                                                     1/2
  Verifying        : dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                     2/2

Installed:
  dhcp-common-12:4.4.2-19.b1.el9.noarch                            dhcp-server-12:4.4.2-19.b1.el9.x86_64

Complete!

[gustave@vbox ~]$  sudo vi /etc/dhcp/dhcpd.conf

# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page
#
   # default lease time
default-lease-time 600;
# max lease time
max-lease-time 7200;
# this DHCP server to be declared valid
authoritative;

# specify network address and subnetmask
subnet 10.1.1.0 netmask 255.255.255.0 {

 # specify the range of lease IP address
    range dynamic-bootp 10.0.0.10 10.0.0.50;

    # specify gateway
    option routers 10.1.1.253;
}

[gustave@vbox ~]$ sudo systemctl enable --now dhcpd
[gustave@vbox ~]$ sudo firewall-cmd --add-service=dhcp
success
[gustave@vbox ~]$ sudo firewall-cmd --runtime-to-permanent
success
[gustave@vbox ~]$
```

## 4. Proof or you're lying

🌞 Récupérer une IP automatiquement depuis les 3 nodes

```sh
node1> ip dhcp
DDORA IP 10.1.1.10/24 GW 10.1.1.253

node1> show ip

NAME        : node1[1]
IP/MASK     : 10.1.1.10/24
GATEWAY     : 10.1.1.253
DNS         :
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 572, 600/300/525
MAC         : 00:50:79:66:68:00
LPORT       : 10006
RHOST:PORT  : 127.0.0.1:10007
MTU:        : 1500

node2> ip dhcp
DDORA IP 10.1.1.12/24 GW 10.1.1.253

node2> show ip

NAME        : node2[1]
IP/MASK     : 10.1.1.12/24
GATEWAY     : 10.1.1.253
DNS         :
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 575, 600/300/525
MAC         : 00:50:79:66:68:01
LPORT       : 10008
RHOST:PORT  : 127.0.0.1:10009
MTU:        : 1500

node3> ip dhcp
DDORA IP 10.1.1.11/24 GW 10.1.1.253

node3> show ip

NAME        : node3[1]
IP/MASK     : 10.1.1.11/24
GATEWAY     : 10.1.1.253
DNS         :
DHCP SERVER : 10.1.1.253
DHCP LEASE  : 575, 600/300/525
MAC         : 00:50:79:66:68:04
LPORT       : 10012
RHOST:PORT  : 127.0.0.1:10013
MTU:        : 1500
```

➜ Wireshark !
Dispo dans 📁 p3_dhcp.pcap (use of node3)


## 5. DHCP lease

🌞 Bail DHCP

```sh
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\0010\361\260.\010\000'\370\227\343";

lease 10.1.1.10 {
  starts 4 2026/01/08 00:06:49;
  ends 4 2026/01/08 00:16:49;
  cltt 4 2026/01/08 00:06:49;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "node11";
}
lease 10.1.1.11 {
  starts 4 2026/01/08 00:06:56;
  ends 4 2026/01/08 00:16:56;
  cltt 4 2026/01/08 00:06:56;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
lease 10.1.1.12 {
  starts 4 2026/01/08 00:07:02;
  ends 4 2026/01/08 00:17:02;
  cltt 4 2026/01/08 00:07:02;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:01;
  uid "\001\000Pyfh\001";
  client-hostname "node21";
}
lease 10.1.1.10 {
  starts 4 2026/01/08 00:11:53;
  ends 4 2026/01/08 00:21:53;
  cltt 4 2026/01/08 00:11:53;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "node11";
}
lease 10.1.1.11 {
  starts 4 2026/01/08 00:12:01;
  ends 4 2026/01/08 00:22:01;
  cltt 4 2026/01/08 00:12:01;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
lease 10.1.1.12 {
  starts 4 2026/01/08 00:12:06;
  ends 4 2026/01/08 00:22:06;
  cltt 4 2026/01/08 00:12:06;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:01;
  uid "\001\000Pyfh\001";
  client-hostname "node21";
}
lease 10.1.1.11 {
  starts 4 2026/01/08 00:14:52;
  ends 4 2026/01/08 00:24:52;
  cltt 4 2026/01/08 00:14:52;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
lease 10.1.1.10 {
  starts 4 2026/01/08 00:16:55;
  ends 4 2026/01/08 00:26:55;
  cltt 4 2026/01/08 00:16:55;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "node11";
}
lease 10.1.1.12 {
  starts 4 2026/01/08 00:17:08;
  ends 4 2026/01/08 00:27:08;
  cltt 4 2026/01/08 00:17:08;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:01;
  uid "\001\000Pyfh\001";
  client-hostname "node21";
}
```

🌞 Use grep

```sh
[gustave@vbox ~]$ cat /var/lib/dhcpd/dhcpd.leases | grep -A 10 "lease 10.1.1.11"
lease 10.1.1.11 {
  starts 4 2026/01/08 00:06:56;
  ends 4 2026/01/08 00:16:56;
  cltt 4 2026/01/08 00:06:56;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
--
lease 10.1.1.11 {
  starts 4 2026/01/08 00:12:01;
  ends 4 2026/01/08 00:22:01;
  cltt 4 2026/01/08 00:12:01;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
--
lease 10.1.1.11 {
  starts 4 2026/01/08 00:14:52;
  ends 4 2026/01/08 00:24:52;
  cltt 4 2026/01/08 00:14:52;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004";
  client-hostname "node31";
}
--
lease 10.1.1.11 {
  starts 4 2026/01/08 00:19:56;
  ends 4 2026/01/08 00:29:56;
  cltt 4 2026/01/08 00:19:56;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:04;
  uid "\001\000Pyfh\004"; 
  client-hostname "node31";
}
```
























