---
title: Network
has_children: true
---

System activity record  
  Check network activity:  
   `sar -n DEV 1`  
 Interfaces:  
  `ip a`  
  `nmcli`  
  Device mounting rules:  
   `/etc/udev/rules.d/70-persistent-net.rules`  
  Config:  
   `/etc/sysconfig/network-scripts/ifcfg-`  
    \(Device name and MAC address must match rules\)  
  Devices:  
   `nmcli d show`  
  Connections:  
   `nmcli c show`  
   More detail:  
    `nmcli c show`   
   Bring up/down  
    `nmcli con down`   
    `nmcli con up`   
  Set static IP  
   `nmcli con mod  ipv4.method manual ipv4.address / ipv4.gateway  ipv4.dns`  \# To apply, `systemctl restart network`  
    Set multiple IPs on one interface: iv4.address /,/ ...  
    Set same IP on multiple interfaces: See options: teaming and bonding  
     Supports redundancy, performance  
     [https://linuxacademy.com/cp/courses/lesson/course/3127/lesson/3/module/262](https://linuxacademy.com/cp/courses/lesson/course/3127/lesson/3/module/262)  
  Add IP addresses to connection:  
   `nmcli con mod  iv4.address /,/` \# To apply, systemctl restart network  
  Set to DHCP  
   `nmcli con mod  ipv4.method auto ipv4.address "" ipv4.gateway "" ipv4.dns ""` \# To apply: `systemctl restart network`  
  DHCP  
   Leases:  
    `/var/lib/dhcp/dhclient.leases`  
   Release address:  
    `dhclient -r`  
   Restart client  
    `dhclient`  
 Check for open ports, etc.  
  `ss -tulp`  
  `sudo lsof -n -P -i4\|grep LISTEN`  
 Inspect packets:  
  `tcpdump`  
   Caution:  
    Doesn't scale well, due to massive text output  
   `-i`: interface \(or, 'any'. Caution, may default to a specific interface\)  
   port   
   `-A`: packet contents  
   `-n`: IP as address, not hostname  
   `-w` : write to file  
   `-r` : read from file  
   `-v`: verbose  
   `-vv`: extra verbose  
  `tshark`  
   \(arguments similar to tcpdump\)  
   Filters \(command line options\):  
    Limit to port:  
     `'port '`  
    Exclude port:  
     `'port not '`  
   Options:  
    hex and ASCII content display:  
     `-x`  
 Interface stats:  
  `nicstat`  
 Sockets:  
  `ss -mop` \# m:memory, o:timer, p:processes  
 Ethernet interface:  
   `sudo ethtool`   
   `sudo ethtool --statistics eth0`  
 Reachability  
  `ping`   
  `traceroute`   
  `mtr --curses`   
  \(see also connect\)  
 ARP table \(maps layer 3 \[IP\] to layer 2 \[MAC\]\)  
  `ip n`
  `arp`
 Performance  
  `sudo ping  -i 0.01`  
  `curl -o /dev/null http://speedtest.wdc01.softlayer.com/downloads/test10.zip`  
 Routing  
  `netstat -rn`  
  `ip r` \# ip route show  
  `ip route get`  
  `routel`  
  Configure routes \(does not survive restart\):  
   Set route through interface:  
    `ip route set  dev`   
    `ip route set  via  dev`   
   Set route using gateway:  
    `ip route set` / `via`   
   Prohibit route:  
    `ip route`    
     `route-drop-types`: generated errors  
      `prohibit`: `EACCES` \(administratively prohibited\)  
      `blackhole`: `EINVAL` \(invalid, i.e. silently discarded\)  
      `unreachable`: `EHOSTUNREACH` \(unreachable\)  
   Flush route:  
    `ip route flush`  \# Be careful on cloud. Too general breaks connectivity  
 Name Services  
  Configuration:  
   Sources:  
    `/etc/nsswitch.conf`  
  Files \(if `file` specified for `hosts` in `nsswitch.conf`\):  
   `/etc/hosts`  
  Get name service information \(as resolved\):  
   `getent ahosts`   
  DNS  
   Configuration:  
    Nameservers \(if `dns` specified for `hosts` in `nsswitch.conf`\):  
     `/etc/resolv.conf`  
   Troubleshooting \(Domain Information Groper\):  
    `host`   
    `dig` \(more detail and options\):  
     Per `nameserver` in `/etc/resolv.conf`:  
      `dig`   
     Specified nameserver:  
      `dig @`   
     Reverse DNS:  
      `dig -x`   
     Nameserver records:  
      `dig NS`   
     Authority record:  
      `dig SOA`   
     Options:  
      Suppress all output \(except specified after\):  
       `+noall`  
      Answer:  
       `+answer`  
      Trace:  
       `+trace`
      Short response:  
       `+short`  
      List from file:  
       `-f`   
      All records:  
       `ANY`  
 Ports  
  Info:  
   List:  
    `/etc/services`  
   Common:  
    22: SSH, 80: HTTP, 443: HTTPS  
  Scan range of ports  
    `nc -zv  80-84`  
  Check for open / filtered port  
    `nmap -p`    
  Check packet filtering and NAT:  
   `iptables -L`  
  Check sockets:  
   `ss -lntp`  
  Listen on port \(TCP and UDP\):  
   `nc -l`   
   Pipe input to command:  
    `nc -l  -e`   
 Connections  
  per iptables  
   `cat /proc/net/nf_conntrack`  
   `conntrack -L` \# Syntax similar to that of iptables  
 Connect  
  HTTP  
   `curl`   
   Header only:  
    `curl -I`   
   Text browser:  
    `links`  
   `telnet <ip> <port>`  // TCP  
  To port, not sending anything:  
   `nc -vz`    
 Firewall using `firewalld` daemon  
  Check rules:  
   `firewall-cmd --list-all`  
  Add port:  
   `firewall-cmd --permanent --add-port=514/tcp`  
    need to reload for port open to take effect  
  Add service:  
   `firewall-cmd --permanent --add-service=`  
    need to reload for port open to take effect  
  Reload:  
   `firewall-cmd --reload`  
 Wi-Fi  
  Check number and signal quality of WiFi SSIDs:  
   `sudo iwlist mlan0 scan \| grep Signal`  

 Check Layer 2 MAC reachability:  
  `arping`  
  `ip n` \# \(ARP table\) same as: ip neighbor show  
 Check Layer 3 \(IP\) reachability:  
  `tracepath` \# similar to `traceroute`, only does not not require superuser privileges  

 View Kernel IP routing table:  
  `route -n`  
 Create IP routing table for outgoing to subnet to be routed via device:  
  `ip route add <subnet e.g. 1.2.3.4/24>; dev  tab`   
 Add IP routing rule for incoming from subnet to use table:  
  `ip rule add from <subnet e.g. 1.2.3.4/24> tab`   
 `ping`:  
   _**Add: not reliable for unknown networks, since ICMP is often blocked**_   

 Packet Capture:  
  Note: Often will report checksum errors on most/all packets, due to NIC checksum offloading being enabled. Can disable for troubleshooting. See: [https://sokratisg.net/2012/04/01/udp-tcp-checksum-errors-from-tcpdump-nic-hardware-offloading/](https://sokratisg.net/2012/04/01/udp-tcp-checksum-errors-from-tcpdump-nic-hardware-offloading/)  
  Note: Typical to filter out SSH \(from troubleshooting effort, noisy\).  
  Note: Wireshark is good for playing with filters  
  Filters: [http://alumni.cs.ucr.edu/~marios/ethereal-tcpdump.pdf](http://alumni.cs.ucr.edu/~marios/ethereal-tcpdump.pdf)  
    _**Try these**_   
  Examples: [https://hackertarget.com/tcpdump-examples/](https://hackertarget.com/tcpdump-examples/)  
    _**Try these**_   
  ---  
  `tcpdump` / `tshark` \(same format, since both based on `libpcap`\):  
   Typical usage \(extra verbose from single IP, filtering out SSH\):  
    `tcpdump -vv src  and not dst port 22`  
   ---  
   Capture to file:  
    `-w .pcap`  
    With filter to exclude port:  
     `port not`   

 Test connection speed  
  `speedtest-cli --bytes`  

 Configure Ethernet port mode:  
  `nm-connection-editor` \# GUI tool  
   Wired Connection  -&gt; IPv4 Settings  
    Set up as client \(Default\):  
     Automatic \(DHCP\)  
    Set up as route for other clients:  
     'Shared to Other Computers'  

 Hostname and machine info \(systemd\): view, update  
  `hostnamectl`  

 `netstat` network related information such as network connections, routing tables, interface statistics, masquerade connections, multicast memberships etc.  

 `ntop` is just like top, but for network traffic  

 `vnstat` is a command line utility that displays and logs network traffic of the interfaces on your systems  
  depends on the network statistics provided by the kernel. So, vnstat doesn’t add any additional load to your system for monitoring and logging the network traffic.  
 `ss` stands for socket statistics  

 Look into Data Plane Development Kit for high performance networking and packet inspection features on Linux [https://www.dpdk.org/](https://www.dpdk.org/)  

 Command-line network configuration  
  [https://docs.fedoraproject.org/en-US/Fedora/20/html/Networking\_Guide/sec-Connecting\_to\_a\_Network\_Using\_nmcli.html](https://docs.fedoraproject.org/en-US/Fedora/20/html/Networking_Guide/sec-Connecting_to_a_Network_Using_nmcli.html)  
  [https://www.thegeekdiary.com/how-to-configure-and-manage-network-connections-using-nmcli/](https://www.thegeekdiary.com/how-to-configure-and-manage-network-connections-using-nmcli/)  

 Look into Zeek for network monitoring and event triggers: [https://www.zeek.org/](https://www.zeek.org/)  

 NetHogs track of real time network traffic bandwidth used by each program or application  

 Networking  
  Use `nc` \(netcat\) instead of `telnet`. More scriptable. Divides `stdout` `stderr` better.  
  Set chains using `iptables` to route traffic based on type / source.  
  Use `ss` to check open sockets and associated processes.  

 `nmtui`: Network Manager using Text User Interface  

 Port range  
  [https://serverfault.com/questions/103626/what-is-the-maximum-port-number](https://serverfault.com/questions/103626/what-is-the-maximum-port-number)  

 SNMP? Daemon: `snmpd`  

 List open ports  
  `sudo lsof -n -P -i4|grep LISTEN`

NetworkManager detailed configuration: `nm-connection-editor`

## netplan

Config files, processed in lexigraphical order:

```text
/etc/netplan/<integer>-<name>.yaml
```

Example content \(server with DHCP client on internet uplink and serving as gateway on other link\):

```text
network:
  version: 2
  renderer: networkd
  ethernets:
    enp4s0:
      dhcp4: yes
      gateway4: <static-ip-of-upstream-server>
    eno1:
      addresses: [<static-ip>/<cidr>]
      dhcp4: no
```

`sudo netplan try`

`sudo netplan apply`

`sudo netplan ip leases <interface>`

## nmap

[Manual: Port Scanning Techniques](https://nmap.org/book/man-port-scanning-techniques.html)

### Scan multiple hosts

`nmap 1.1.1.1,3,6  # ending octet  
nmap 1.1.1.1-5    # range  
nmap 1.1.1.1/24   # subnet`

### Host discovery

Found hosts may not overlap among these

`nmap -sL <hosts>  # List scan  
nmap -sn <hosts>  # Plain ping  
nmap -PS <hosts>  # TCP SYN Ping  
nmap -PA <hosts>  # TCP ACK Ping  
nmap -PE <hosts>  # ICMP Echo Ping  
nmap -PU <hosts>  # UDP Ping`

### Host scan

`nmap -sS <hosts>  # TCP SYN Scan  
nmap -sT <hosts>  # TCP Connect Scan (useful when lacking priviledges for SYN)  
nmap -sU <hosts>  # UDP Scan (rarely blocked)  
nmap -sO <hosts>  # IP Protocol Scan`

### General flags

`-n  # Skip DNS resolution  
-p <port>-<port>  # Include range of ports  
--exclude <port>-<port>  # Exclude range of ports`

Stop NetworkManager from managing interface
  /etc/NetworkManager/NetworkManager.conf
    [keyfile]
    unmanaged-devices=mac:<mac-address>
Set up netplan to manage Ethernet interface (DHCP, DNS managed separately)
  sudo vim /etc/netplan/01-netcfg.yaml
    network:
      version: 2
      renderer: networkd
      ethernets:
        <Ethernet-interface>:
          dhcp4: false
          addresses: [<subnet, e.g. 10.42.1.0/24>]

Set up netplan to manage Ethernet interface with bridge to virtual network (DHCP, DNS managed separately)
  sudo vim /etc/netplan/01-netcfg.yaml
    network:
      version: 2
      renderer: networkd

      ethernets:
        <Ethernet-interface>:
          dhcp4: false
          dhcp6: false

      bridges:
        br0:
          interfaces: [<Ethernet-interface>]
          addresses: [<subnet, e.g. 10.42.1.0/24>]
          parameters:
            stp: true  # Spanning Tree Protocol
            forward-delay: 4  # Seconds before
          dhcp4: false
          dhcp6: false

sudo netplan generate
sudo netplan --debug apply
brctl show  # deprecated. Use ip link
networkctl status br0
virt-manager

