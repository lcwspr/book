# 信息收集

## 主机发现

### nmap

1. 扫描方式

    * TCP: `-sT`
    * SYN: `-sS`
    * ACK: `-sA`
    * UDP: `-sU`
    * RPC: `-sR`
    * ICMP: `-sP`
    * Disable port Scan: `-sn`

2. 常见扫描方案
   * `nmap -sV`: 版本探测
   * `-S 源地址`： 定义扫描源地址，为了不被发现
   * `--host-timeout`: 主机超时时间: `18000`
   * `--scan-delay`: 报文间隔: `1000`
   * `host -l company.com | cut -d ' ' -f 4 | name -v -iL -`
   * `-O`: 操作系统扫描
3. 输出
   * `-oN <file>`: 
   * `-oX <xml file>`
   * `-oG <file>`

### masscan

* 高级选项
  * `--adapter-ip`: 指定发包的ip地址
  * `--adapter-port`: 指定发包的源地址
  * `--adapter-mac`: 指定发包的源mac地址
  * `--router-mac`: 网关的MAC地址
  * `--exclude`: 排查地址
  * `--excludefile`: 排除地址

### ntbscan

* 用于windows主机扫描
* 扫描c段
  * `nbtscan -r 192.168.1.0/24`
* 扫描范围
  * `nbtscan -v -s 192.168.1.24-124`
* 从文件读取扫描
  * `nbtscan -f <file>`

### hping3

* 主要测试防火墙的拦截规则，对于网络设备进行测试
* 常用模式
  * `-0`: ip原始报文
  * `-1`: icp报文
  * `-2`: udp模式
  * `-8`: 扫描模式`--scan`
  * `9`: 监听模式

* 测试防火墙对于icmp包的反应，是否支持traceroute, 是否开放某个端口，对防火墙进行DDOS。