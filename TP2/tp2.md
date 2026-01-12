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


 



