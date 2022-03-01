# bitcoin-eclipse
比特币日蚀攻击模拟实现
## 攻击概述
日蚀攻击（eclipse）是针对比特币（区块链）P2P网络的一种攻击方式，旨在控制受害节点的所有网络连接，以满足攻击者的恶意目的，比如提升自身挖矿优势，对受害节点进行双花攻击等。
## 攻击原理
攻击者通过自身的网络拓扑优势，收集大量可控的IP地址对受害节点的内部数据库（new table和tried table）进行填充。当受害节点向这些可控IP发起连接时，连接就会被攻击者控制。
## 实验环境
* victim：接收传入连接，并将内部数据库中的IP输出在addr_data中。执行getpeerinfo时会将newtable，triedtable，以及外出连接的情况输出。
* 攻击脚本（attacker_script.txt）:使用iptables的地址转发功能，将发往35.0.0.0/8的流量导向攻击主机。
* attacker：向victim高速发送包含可控IP的addr（35.0.0.0/8）。请在victim主机中运行攻击脚本（attacker_script.txt）,将发往35.0.0.0/8的流量导向攻击主机
* 注：在两台linux主机中分别运行victim与attacker，并将attacker连接至victim（使用connect命令），当victim的多数或全部传出连接指向攻击主机，日蚀成功。本实验只劫持受害节点的外出连接，传入连接相对简单，不予讨论。
