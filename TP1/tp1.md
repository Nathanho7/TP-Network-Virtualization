# Part 1 : Most simplest LAN

## 3. Know your MAC

🌞 Déterminer l'adresse MAC de vos deux machines
```sh
- node1

VPCS> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64

- node2
VPCS> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64

```

## 4. IP Setup¶

🌞 Définir une IP statique sur les deux machines

```sh
J’ai utilisé la commande [ip] , puis renseigné l'IP de la machine pour mettre une adresse IP statique sur les machines dans GNS3.
VPCS> ip 10.1.1.1/24
Checking for duplicate address...
PC1 : 10.1.1.1 255.255.255.0

VPCS> ip 10.1.1.2/24
Checking for duplicate address...
PC1 : 10.1.1.2 255.255.255.0
```

🌞 Proof !
```sh
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64
```

🌞 Effectuer un ping d'une machine à l'autre
- Ping de node2 depuis node1
```sh
VPCS> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=1.049 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=0.438 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=1.134 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=2.044 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=1.875 ms
```

- Ping de node 1 depuis node2

```sh
VPCS> ping 10.1.1.1
84 bytes from 10.1.1.1 icmp_seq=1 ttl=64 time=1.404 ms
84 bytes from 10.1.1.1 icmp_seq=2 ttl=64 time=1.053 ms
84 bytes from 10.1.1.1 icmp_seq=3 ttl=64 time=0.904 ms
84 bytes from 10.1.1.1 icmp_seq=4 ttl=64 time=1.928 ms
84 bytes from 10.1.1.1 icmp_seq=5 ttl=64 time=1.263 ms

```

# 5. Analyze

🌞 Protocolz ?

```sh
Protocole utilisé ICMP ( Internet Control Message Protocol) : il appartient à la couche 3 du modèle OSI. (couche Réseau) 
Autre, lors l'execution du ping, le protocole ICMP envoie un datagramme à l'hôte spécifié et attend la réponse. Le protocole ICMP permet de gérer les erreurs se produisant sur les réseaux TCP/IP.
```

# Part 2 : Bring that switch in


# 3. Même chose en fast

🌞 Déterminer l'adresse MAC de vos trois machines

```sh
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64

VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64

  VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.3/24          0.0.0.0           00:50:79:66:68:02  10010  127.0.0.1:10011
       fe80::250:79ff:fe66:6802/64
```

🌞 Définir une IP statique sur les trois machines

```sh
-node1
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.1/24          0.0.0.0           00:50:79:66:68:00  10000  127.0.0.1:10001
       fe80::250:79ff:fe66:6800/64

-node2
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.2/24          0.0.0.0           00:50:79:66:68:01  10002  127.0.0.1:10003
       fe80::250:79ff:fe66:6801/64

-node3
VPCS> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
VPCS1  10.1.1.3/24          0.0.0.0           00:50:79:66:68:02  10010  127.0.0.1:10011
       fe80::250:79ff:fe66:6802/64
```

🌞 Effectuer des ping d'une machine à l'autre

```sh

Voir dossier ping.pcap2
```

# 4. ARP old friend

🌞 Afficher la table ARP de node1

```sh
VPCS> arp

arp table is empty

VPCS> ping 10.1.1.2
84 bytes from 10.1.1.2 icmp_seq=1 ttl=64 time=0.750 ms
84 bytes from 10.1.1.2 icmp_seq=2 ttl=64 time=1.028 ms
84 bytes from 10.1.1.2 icmp_seq=3 ttl=64 time=1.145 ms
84 bytes from 10.1.1.2 icmp_seq=4 ttl=64 time=2.926 ms
84 bytes from 10.1.1.2 icmp_seq=5 ttl=64 time=1.733 ms

VPCS> ping 10.1.1.3
84 bytes from 10.1.1.3 icmp_seq=1 ttl=64 time=2.288 ms
84 bytes from 10.1.1.3 icmp_seq=2 ttl=64 time=2.422 ms
84 bytes from 10.1.1.3 icmp_seq=3 ttl=64 time=0.694 ms
84 bytes from 10.1.1.3 icmp_seq=4 ttl=64 time=2.870 ms
84 bytes from 10.1.1.3 icmp_seq=5 ttl=64 time=2.780 ms

VPCS> arp

00:50:79:66:68:01  10.1.1.2 expires in 99 seconds
00:50:79:66:68:02  10.1.1.3 expires in 107 seconds
```

➜ Capturer un échange ARP
```sh
Voire ficher p2_arp_node2.pcap
Voire ficher p2_arp_node3.pcap
```


# Part 3 : DHCP is a nice guy

## 3. Setuuuup

🌞 Installer un serveur DHCP

```sh
[gustave@vbox ~]$ sudo dnf -y install dhcp-server
Rocky Linux 9 - BaseOS                                                                                                                              1.9 MB/s | 7.5 MB     00:03
Rocky Linux 9 - AppStream                                                                                                                           1.9 MB/s |  12 MB     00:06
Rocky Linux 9 - Extras                                                                                                                              6.0 kB/s |  17 kB     00:02
Dependencies resolved.
====================================================================================================================================================================================
 Package                                     Architecture                           Version                                            Repository                              Size
====================================================================================================================================================================================
Installing:
 dhcp-server                                 x86_64                                 12:4.4.2-19.b1.el9                                 baseos                                 1.2 M
Installing dependencies:
 dhcp-common                                 noarch                                 12:4.4.2-19.b1.el9                                 baseos                                 128 k

Transaction Summary
====================================================================================================================================================================================
Install  2 Packages

Total download size: 1.3 M
Installed size: 4.2 M
Downloading Packages:
(1/2): dhcp-server-4.4.2-19.b1.el9.x86_64.rpm                                                                                                       763 kB/s | 1.2 MB     00:01
(2/2): dhcp-common-4.4.2-19.b1.el9.noarch.rpm                                                                                                        77 kB/s | 128 kB     00:01
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                               713 kB/s | 1.3 MB     00:01
Rocky Linux 9 - BaseOS                                                                                                                              412 kB/s | 1.7 kB     00:00
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
  Preparing        :                                                                                                                                                            1/1
  Installing       : dhcp-common-12:4.4.2-19.b1.el9.noarch                                                                                                                      1/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                                                                      2/2
  Installing       : dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                                                                      2/2
  Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                                                                      2/2
  Verifying        : dhcp-common-12:4.4.2-19.b1.el9.noarch                                                                                                                      1/2
  Verifying        : dhcp-server-12:4.4.2-19.b1.el9.x86_64                                                                                                                      2/2

Installed:
  dhcp-common-12:4.4.2-19.b1.el9.noarch                                                    dhcp-server-12:4.4.2-19.b1.el9.x86_64

Complete!
```

-Config:

```sh
[gustave@vbox ~]$ sudo vi /etc/dhcp/dhcpd.conf
# DHCP Server Configuration file.
#   see /usr/share/doc/dhcp-server/dhcpd.conf.example
#   see dhcpd.conf(5) man page

# specify domain name
option domain-name     "tp1.efrei";

# specify DNS server's IP address
option domain-name-servers     8.8.8.8;

# default lease time
default-lease-time 600;

# max lease time
max-lease-time 7200;

# this DHCP server to be declared valid
authoritative;

# specify network address and subnetmask
subnet 10.1.1.0 netmask 255.255.255.0 {
    # specify the range of lease IP address (10.1.1.10 à 10.1.1.50)
    range dynamic-bootp 10.1.1.10 10.1.1.50;

    # specify broadcast address
    option broadcast-address 10.1.1.255;

    # specify gateway (ton adresse de serveur)
    option routers 10.1.1.253;
}
[gustave@vbox ~]$ sudo systemctl enable --now dhcpd
Created symlink /etc/systemd/system/multi-user.target.wants/dhcpd.service → /usr/lib/systemd/system/dhcpd.service.
```

4. Proof or you're lying¶
🌞 Récupérer une IP automatiquement depuis les 3 nodes

-node1
```sh
VPCS> ip dhcp
DDORA IP 10.1.1.10/24 GW 10.1.1.253
```

-node2
```sh
VPCS> ip dhcp
DDORA IP 10.1.1.11/24 GW 10.1.1.253
```

-node3
```sh
VPCS> ip dhcp
DDORA IP 10.1.1.12/24 GW 10.1.1.253
```

➜ Wireshark !
Voir 📁 p3_dhcp.pcap



# 5. DHCP lease

🌞 Bail DHCP
```sh
[gustave@vbox ~]$ sudo cat /var/lib/dhcpd/dhcpd.leases
# The format of this file is documented in the dhcpd.leases(5) manual page.
# This lease file was written by isc-dhcp-4.4.2b1

# authoring-byte-order entry is generated, DO NOT DELETE
authoring-byte-order little-endian;

server-duid "\000\001\000\0010\360\177\377\010\000'\362z\315";

lease 10.1.1.10 {
  starts 3 2026/01/07 02:24:49;
  ends 3 2026/01/07 02:34:49;
  cltt 3 2026/01/07 02:24:49;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "VPCS1";
}
lease 10.1.1.11 {
  starts 3 2026/01/07 02:24:56;
  ends 3 2026/01/07 02:34:56;
  cltt 3 2026/01/07 02:24:56;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:01;
  uid "\001\000Pyfh\001";
  client-hostname "VPCS1";
}
lease 10.1.1.12 {
  starts 3 2026/01/07 02:25:02;
  ends 3 2026/01/07 02:35:02;
  cltt 3 2026/01/07 02:25:02;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:03;
  uid "\001\000Pyfh\003";
  client-hostname "VPCS1";
}
```

🌞 Use grep

```sh
[gustave@vbox ~]$ sudo cat /var/lib/dhcpd/dhcpd.leases | grep "client-hostname \"VPCS1\";"
[sudo] password for gustave:
  client-hostname "VPCS1";
  client-hostname "VPCS1";
  client-hostname "VPCS1";
  client-hostname "VPCS1";
  client-hostname "VPCS1";
  client-hostname "VPCS1";
[gustave@vbox ~]$ sudo cat /var/lib/dhcpd/dhcpd.leases | grep -A 9 "lease 10.1.1.10"
lease 10.1.1.10 {
  starts 3 2026/01/07 02:24:49;
  ends 3 2026/01/07 02:34:49;
  cltt 3 2026/01/07 02:24:49;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "VPCS1";
--
lease 10.1.1.10 {
  starts 3 2026/01/07 02:31:01;
  ends 3 2026/01/07 02:41:01;
  cltt 3 2026/01/07 02:31:01;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 00:50:79:66:68:00;
  uid "\001\000Pyfh\000";
  client-hostname "VPCS1";
```



# Part 4 : real haxor

## 1. DHCP spoofing¶
### A. Setup

🌞 Installez et configurez un serveur DHCP sur votre machine attaquante

```sh
# Configuration Rogue DHCP
authoritative;
default-lease-time 600;
max-lease-time 7200;

# specify network address and subnetmask
subnet 10.1.1.0 netmask 255.255.255.0 {

# specify plage of attack (10.1.1.210 and 10.1.1.250)
    range 10.1.1.210 10.1.1.250;
}
```

🌞 Test !

 -kill dhcp
 
```sh
[gustave@vbox ~]$ sudo systemctl stop dhcpd
[gustave@vbox ~]$ systemctl status dhcpd
○ dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: inactive (dead) since Wed 2026-01-07 04:18:01 CET; 10s ago
   Duration: 55min 5.391s
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
    Process: 11348 ExecStart=/usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --n>
   Main PID: 11348 (code=killed, signal=TERM)
     Status: "Dispatching packets..."
        CPU: 292ms
```

 - test VPCS ( node2 par exemple)

   ```sh
   VPCS> ip dhcp
   DDORA IP 10.1.1.210/24 GW 10.1.1.253
   ```

  ## B. Race !

  
  ```sh
  [gustave@vbox ~]$ sudo systemctl start dhcpd
[sudo] password for gustave:
[gustave@vbox ~]$ sudo systemctl status dhcpd
● dhcpd.service - DHCPv4 Server Daemon
     Loaded: loaded (/usr/lib/systemd/system/dhcpd.service; enabled; preset: disabled)
     Active: active (running) since Wed 2026-01-07 04:35:14 CET; 1min 4s ago
       Docs: man:dhcpd(8)
             man:dhcpd.conf(5)
   Main PID: 11595 (dhcpd)
     Status: "Dispatching packets..."
      Tasks: 1 (limit: 22979)
     Memory: 4.7M (peak: 4.8M)
        CPU: 76ms
     CGroup: /system.slice/dhcpd.service
             └─11595 /usr/sbin/dhcpd -f -cf /etc/dhcp/dhcpd.conf -user dhcpd -group dhcpd --no-pid

Jan 07 04:35:14 vbox dhcpd[11595]:
Jan 07 04:35:14 vbox dhcpd[11595]: No subnet declaration for enp0s3 (10.0.2.15).
Jan 07 04:35:14 vbox dhcpd[11595]: ** Ignoring requests on enp0s3.  If this is not what
Jan 07 04:35:14 vbox dhcpd[11595]:    you want, please write a subnet declaration
Jan 07 04:35:14 vbox dhcpd[11595]:    in your dhcpd.conf file for the network segment
Jan 07 04:35:14 vbox dhcpd[11595]:    to which interface enp0s3 is attached. **
Jan 07 04:35:14 vbox dhcpd[11595]:
Jan 07 04:35:14 vbox dhcpd[11595]: Sending on   Socket/fallback/fallback-net
Jan 07 04:35:14 vbox dhcpd[11595]: Server starting service.
Jan 07 04:35:14 vbox systemd[1]: Started DHCPv4 Server Daemon.

```

```
Node 1:
VPCS> ip dhcp
DORA IP 10.1.1.212/24 GW 10.1.1.253

Node2:
VPCS> ip dhcp
DORA IP 10.1.1.210/24 GW 10.1.1.13

Node3:
VPCS> ip dhcp
DORA IP 10.1.1.211/24 GW 10.1.1.13

Node4 (new):
VPCS> ip dhcp IP 10.1.1.214/24
DORA IP 10.1.1.14/24 GW 10.1.1.253

Node5 (new):
VPCS> ip dhcp
DORA IP 10.1.1.215/24 GW 10.1.1.13

Node6 (new):
VPCS> ip dhcp
DORA IP 10.1.1.216/24 GW 10.1.1.13
```

➜ Wireshark this please
Voire 📁 p4_dhcp_race.pcap






















     


