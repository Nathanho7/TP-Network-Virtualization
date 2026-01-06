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






     


