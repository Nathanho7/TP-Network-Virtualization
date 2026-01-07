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















