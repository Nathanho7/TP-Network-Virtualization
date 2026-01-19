# Part1 : Network Setup

## 7. Proof or lie¶
🌞 Tout le monde doit pouvoir se ping

- au sein du même LAN :

* node1 peut ping node2
```sh
node1> ping 10.2.1.12

84 bytes from 10.2.1.12 icmp_seq=1 ttl=64 time=0.761 ms
84 bytes from 10.2.1.12 icmp_seq=2 ttl=64 time=0.514 ms
84 bytes from 10.2.1.12 icmp_seq=3 ttl=64 time=0.452 ms
84 bytes from 10.2.1.12 icmp_seq=4 ttl=64 time=0.661 ms
84 bytes from 10.2.1.12 icmp_seq=5 ttl=64 time=0.514 ms

```
* node3 peut ping node4
  ```sh
  node3> ping 10.2.2.12

  84 bytes from 10.2.2.12 icmp_seq=1 ttl=64 time=2.490 ms
  84 bytes from 10.2.2.12 icmp_seq=2 ttl=64 time=0.522 ms
  84 bytes from 10.2.2.12 icmp_seq=3 ttl=64 time=0.424 ms
  84 bytes from 10.2.2.12 icmp_seq=4 ttl=64 time=0.568 ms
  84 bytes from 10.2.2.12 icmp_seq=5 ttl=64 time=0.676 ms
  ```

 - le routage doit fonctionner :
   * node1 peut ping node3
     ```sh
     node1> ping 10.2.2.11
      84 bytes from 10.2.2.11 icmp_seq=1 ttl=63 time=28.216 ms
      84 bytes from 10.2.2.11 icmp_seq=2 ttl=63 time=12.137 ms
      84 bytes from 10.2.2.11 icmp_seq=3 ttl=63 time=11.806 ms
      84 bytes from 10.2.2.11 icmp_seq=4 ttl=63 time=13.580 ms
      84 bytes from 10.2.2.11 icmp_seq=5 ttl=63 time=19.515 ms
    ```
* node4 peut ping node2
  ```sh
  node4> ping 10.2.1.12

  84 bytes from 10.2.1.12 icmp_seq=1 ttl=63 time=28.263 ms
  84 bytes from 10.2.1.12 icmp_seq=2 ttl=63 time=20.456 ms
  84 bytes from 10.2.1.12 icmp_seq=3 ttl=63 time=12.719 ms
  84 bytes from 10.2.1.12 icmp_seq=4 ttl=63 time=16.258 ms
  84 bytes from 10.2.1.12 icmp_seq=5 ttl=63 time=16.103 ms
  ```
 ➜ Wireshark this shiet
 ```sh
 Ping de node1 vers node4
 Dispo dans  p1_routed_ping.pcap
 ```

# Part2 : C'est mieux avec internet

🌞 Prouver que...

```SH
r1.tp2.efrei#ping  1.1.1.1

Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 1.1.1.1, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 16/24/36

msnode1> ping 1.1.1.1
1.1.1.1 icmp_seq=1 timeout
1.1.1.1 icmp_seq=2 timeout
1.1.1.1 icmp_seq=3 timeout
1.1.1.1 icmp_seq=4 timeout
1.1.1.1 icmp_seq=5 timeout
```

## 2. Accès internet clients

```sh
node3>  ping 1.1.1.1

84 bytes from 1.1.1.1 icmp_seq=1 ttl=253 time=30.857 ms
84 bytes from 1.1.1.1 icmp_seq=2 ttl=253 time=32.959 ms
84 bytes from 1.1.1.1 icmp_seq=3 ttl=253 time=34.179 ms
84 bytes from 1.1.1.1 icmp_seq=4 ttl=253 time=26.647 ms
84 bytes from 1.1.1.1 icmp_seq=5 ttl=253 time=28.490 ms
Pour le reste des VPCS ils ont aussi accès à internet
```

## 3. Vrai accès internet clients¶

🌞 Prove it

```sh
node1> ping efrei.fr
efrei.fr resolved to 51.210.229.203

84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=50.502 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=39.780 ms
84 bytes from 51.210.229.203 icmp_seq=3 ttl=253 time=37.430 ms
84 bytes from 51.210.229.203 icmp_seq=4 ttl=253 time=26.568 ms
84 bytes from 51.210.229.203 icmp_seq=5 ttl=253 time=32.975 ms
```

## 4. DHCP again

🌞 Test test test 

```sh
node5> ip dhcp
DORA IP 10.2.1.100/24 GW 10.2.1.254
```
```sh
node5> show

NAME   IP/MASK              GATEWAY           MAC                LPORT  RHOST:PORT
node5  10.2.1.100/24        10.2.1.254        00:50:79:66:68:04  20026  127.0.0.1:20027
       fe80::250:79ff:fe66:6804/64
```

```sh
node5> ping efrei.fr
efrei.fr resolved to 51.210.229.203

84 bytes from 51.210.229.203 icmp_seq=1 ttl=253 time=30.481 ms
84 bytes from 51.210.229.203 icmp_seq=2 ttl=253 time=42.941 ms
84 bytes from 51.210.229.203 icmp_seq=3 ttl=253 time=38.548 ms
84 bytes from 51.210.229.203 icmp_seq=4 ttl=253 time=39.979 ms
84 bytes from 51.210.229.203 icmp_seq=5 ttl=253 time=38.153 ms
```

# Part3 : Time to attack all this

## 3. ARP spoofing




















# Part4 : Alors koa c tou ? On refé just la mem choz ke o tp1 enfet enfet ? Bah non

## 2. Go for it¶
A. Setup

🌞 Préparer le DNS spoof
```sh
[gustave@localhost ~]$ echo "10.2.1.188 efrei.fr" > /tmp/dns_spoof_hosts
[gustave@localhost ~]$ cat << EOF > /tmp/dnsmasq.conf
> interface=enp0s9
listen-address=10.2.1.188
port=53
no-hosts
addn-hosts=/tmp/dns_spoof_hosts
no-resolv
server=1.1.1.1
server=8.8.8.8
EOF
```

B. Vérification¶
🌞 S'assurer que c'est up & running, on en profite pour réviser un peu de shell

```sh

[gustave@localhost tmp]$ sudo dnsmasq -C /tmp/dnsmasq.conf -q
[gustave@localhost tmp]$ ps -ef | grep dnsmasq
dnsmasq     2505       1  0 04:06 ?        00:00:00 dnsmasq -C /tmp/dnsmasq.conf -q
gustave     2519    1500  0 04:09 pts/2    00:00:00 grep --color=auto dnsmasq
[gustave@localhost tmp]$ sudo ss -unlp | grep :53
UNCONN 0      0            0.0.0.0:53        0.0.0.0:*    users:(("dnsmasq",pid=2505,fd=4))
UNCONN 0      0               [::]:53           [::]:*    users:(("dnsmasq",pid=2505,fd=6))
```

- DIG1
```sh
  [gustave@localhost tmp]$ dig @1.1.1.1 efrei.fr

; <<>> DiG 9.16.23-RH <<>> @1.1.1.1 efrei.fr
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 58280
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
;; QUESTION SECTION:
;efrei.fr.                      IN      A

;; ANSWER SECTION:
efrei.fr.               20      IN      A       51.210.229.203

;; Query time: 21 msec
;; SERVER: 1.1.1.1#53(1.1.1.1)
;; WHEN: Mon Jan 19 04:12:08 CET 2026
;; MSG SIZE  rcvd: 53
```

 - DIG2
   ```sh
   [gustave@localhost tmp]$ dig @127.0.0.1 efrei.fr
   
    ; <<>> DiG 9.16.23-RH <<>> @127.0.0.1 efrei.fr
    ; (1 server found)
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39588
    ;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
    
    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 1232
    ;; QUESTION SECTION:
    ;efrei.fr.                      IN      A
    
    ;; ANSWER SECTION:
    efrei.fr.               0       IN      A       10.2.1.188
    
    ;; Query time: 6 msec
    ;; SERVER: 127.0.0.1#53(127.0.0.1)
    ;; WHEN: Mon Jan 19 04:13:50 CET 2026
    ;; MSG SIZE  rcvd: 53
   ```

  ## C. Hax ?¶
  
C. Hax ?¶
🌞 Relance ton attaque DHCP spoof depuis la machine attaquante
```sh
 option domain-name-servers 10.2.1.188;
```

🌞 Test test test :
```sh
PC7> ip dhcp
DDORA IP 10.2.1.242/24 GW 10.2.1.188
PC7> show ip

NAME        : PC7[1]
IP/MASK     : 10.2.1.242/24
GATEWAY     : 10.2.1.188
DNS         : 10.2.1.188
DHCP SERVER : 10.2.1.188
DHCP LEASE  : 596, 600/300/525
MAC         : 00:50:79:66:68:06
LPORT       : 20031
RHOST:PORT  : 127.0.0.1:20032
MTU         : 1500

PC7> ping efrei.fr
efrei.fr resolved to 10.2.1.188

84 bytes from 10.2.1.188 icmp_seq=1 ttl=64 time=6.389 ms
84 bytes from 10.2.1.188 icmp_seq=2 ttl=64 time=2.736 ms
84 bytes from 10.2.1.188 icmp_seq=3 ttl=64 time=2.904 ms
84 bytes from 10.2.1.188 icmp_seq=4 ttl=64 time=3.114 ms
84 bytes from 10.2.1.188 icmp_seq=5 ttl=64 time=4.612 ms
``` 
   






 



