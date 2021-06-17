# CISCO 端口测试指令
端口测试的指令可以在对应的仓库中看到。  
  
当测试常见的 **`CISCO`** 路由器和交换机时,  
首先使用 `sh ip int b` 以获取ip端口信息。  
  
常见的 **`CISCO 交换机`** 端口ping测试步骤:  
1. `en`
2. `config t`
3. `int vlan1`
4. `ip add <ip address> <subnet address>`
5. `no shut`
6. `int range <first interface> <1st port number> - <last port number>`
7. `spanning-tree portfast`
8. `spanning-tree bpdufilter en`
9. `int range <second interface> <1st port number> - <last port number>`
10. `spanning-tree portfast`
11. `spanning-tree bpdufilter en`  
...  
12. `end`
13. `en`
14. `ping <ip address of the other switch> size 2000 repeat 1500000000`

----
  
常见的 **`CISCO 路由器`** 端口ping测试步骤:  
1. `en`
2. `conf t`
3. `int <first interface>`
4. `ip add <ip address> <subnet address>`
5. `no shut`
6. `end`
7. `ping <ip address of the other switch> size 2000 repeat 1500`  
  
第一个端口测试完成后，删除分配的IP地址。  
  
8. `conf t`
9. `int <first interface>`
10. `no ip add`
11. `end`
  
重复上述步骤，测试下一个端口
  
12. `int <second interface>`
13. `ip add <ip address> <subnet address>`
14. `no shut`
15. `end`
16. `ping <ip address of the other switch> 2000 repeat 1500`
17. `conf t`
18. `int <second int>`
19. `no ip add`
20. `end`  
...  
测试其余的端口

----
  
**`CISCO NEXUS 交换机`** 端口ping测试步骤:  
1. `sh int brief`
2. `configure terminal`
3. `system default switchport`
4. `feature interface-vlan`
5. `interface Vlan1`
6. `no shutdown`
7. `ip address <ip address>`
8. `int <first interface> <1st port number> - <last port number>`
9. `speed 1000`
10. `spanning-tree port type edge`
11. `no shut`
12. `ip route 0.0.0.0/0 172.16.20.254`
13. `ip route 0.0.0.0/0 Vlan1 172.16.20.254`
14. `end`
15. `ping <ip address of another switch> count unlimit`
