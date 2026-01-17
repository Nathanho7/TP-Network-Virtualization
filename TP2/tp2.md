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






 



