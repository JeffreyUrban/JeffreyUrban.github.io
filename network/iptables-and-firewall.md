---
title: iptables & firewalld
parent: Network
---

`iptables` \(inc. firewall\)  
  List IP tables:  
   `iptables -L`  
   ---  
   Flags:  
    `-n`: no hostname or service name lookups \(much faster\)  
    `-t` nat: View NAT \(network address translation\)  
    `--line-number`: View line numbers  
  Add rule:  
   `-I`: Insert \(add before existing entries\)  
   `-I` : \(add at line number\)  
   `-A`: Append \(add after existing entries\)  
   ---  
   Add rule permitting TCP traffic from specified client IP on specified port  
    `iptables -I INPUT -p tcp -s  --dport  -j ACCEPT`  
     # `-I`: insert at level, `-p`: protocol, `-s`: source, `--dport`: destination port, `j`: jump to  
   Add port forwarding for TCP to different port on same machine:  
    Notes:  
     See `firewalld` for much simpler alternative.  
     Consider limiting source IPs for security.  
    `iptables -t nat -A PREROUTING -p tcp -dport  -j REDIRECT --to-port`   
     \# Append \(`-A`\) to `PREROUTING` table to redirect tcp from  to   
     Note: Ensure this entry as last under `PREROUTING` is `OK`  
    `iptables -I INPUT  -p tcp -m state --state NEW -m tcp --dport  -j ACCEPT`  
     \# Insert \(`-I`\) in `INPUT` table at  to accept tcp when state matches new on destination   
     Note: It's OK to filter out the source port, since `PREROUTING` is handled before `INPUT`.  
   Add port forwarding for TCP to different port on different machine:  
    Notes:  
     See `firewalld` for much simpler alternative.  
     Consider limiting source IPs for security.  
    `iptables -t nat -A PREROUTING -p tcp --dport  -j DNAT --to-destination :`  
     \# Append \(`-A`\) to `PREROUTING` table to \(redirect\) tcp from  via Destination NAT to  and   
    `iptables -t nat -A POSTROUTING -j MASQUERADE`  
     \# Need to enable masquerading  
    `iptables -I FORWARD -p tcp -d  --dport  -m state --state NEW -j ACCEPT`  
     \# Need to forward new packets  
    `iptables -I FORWARD -m state --state RELATED,ESTABLISHED -j ACCEPT`  
     \# Forward packets on established connections as well  
    Enable IP forwarding  
     Check if enabled:  
      `cat /proc/sys/net/ipv4/ip\_forward \# 0: disabled; 1: enabled`  
     Temporarily enable:  
      `echo 1 > /proc/sys/net/ipv4/ip_forward`  
     Permanent:  
      \(change via `syscontrol`\)  
  Save rules \(for persistence through reboot\):  
   `service iptables save`  

 `firewalld`  
  Note: if using, may want to disable and prevent `iptables` from running, allow `firewalld`  
   `systemctl stop iptables`  
   `systemctl mask iptables`  
   `systemctl unmask firewalld`  
  core set of concepts: service, ipset, zone, rich rule  
  Create entry for new service:  
   Create configuration file for new service:  
    `firewall-cmd --permanent --new-service=`  
    `firewall-cmd --permanent --service= --set-description=`      
    `firewall-cmd --permanent --service= --add-port=`  
    \# See new file `/etc/firewalld/services/.xml`  
   Make configuration file available:  
    `firewall-cmd --reload`  
  Add service \(existing or newly created per above\) to default zone \(public\):  
    \*\*\* clarify that: `firewall-cmd --permanent --add-service=` applies to an existing service.  
  Create ipset:  
   Create configuration file for ipset:  
    `firewall-cmd --permanent --new-ipset= --type=`  
    \# See `/etc/firewalld/ipsets/.xml`  
   Add to ipset:  
    `firewall-cmd --permanent --ipset= --add-entry=<single entry e.g. 1.2.3.4, or subnet 1.2.3.4/24>`  
   Make ipset available:  
    `firewall-cmd --reload`  
  View ipset:  
   `firewall-cmd --ipset= --get-entries`  
  Set `ipset` to `DROP` zone \(to block access from those IPs\):  
   `firewall-cmd --permanent --zone=drop --add-source=ipset`  
  Rich rules  
   Ordering:  
    Unlike iptables, order doesn't matter for overlapping rules  
   Add rich rule to accept traffic from specific IP or range on specific port:  
    `firewall-cmd --permanent --add-rich-rule='rule family= source address=<single entry e.g. 1.2.3.4, or subnet 1.2.3.4/24> port port= protocol= accept'`  
   Remove rich rule:  
    `firewall-cmd --permanent --remove-rich-rule=''`  
  Zones:  
   View zones:  
   `firewall-cmd --get-active-zones`  
   `firewall-cmd --list-all-zones`  
   `firewall-cmd --info-zone=`  
   Create zone:  
    `firewall-cmd --permanent --new-zone=`
    \# See `/etc/firewalld/zones/.xml`  
   Make zone available:  
    `firewall-cmd --reload`  
   Add subnet as zone source:  
    `firewall-cmd --permanent --zone= --add-source=<subnet e.g. 1.2.3.4/24>`  
  Set up port forwarding to different port on same machine:  
   Note: Consider limiting source IPs for security.  
   Allow tcp on target port:  
    `firewall-cmd --add-port=/tcp`  
   Add forwarding rule:  
    `firewall-cmd --add-forward-port=port=:proto=tcp:toport=`  
  Set up port forwarding to different port on different machine:  
   Note: Consider limiting source IPs for security.  
   Note: This method forwards incoming packets from other machines, not same machine.  
   Add forwarding rule:  
    `firewall-cmd --add-forward-port=port=:proto=tcp:toport=:toaddr=`  
   Add masquerading to permit forwarding:  
    `firewall-cmd --add-masquerade`  

Share Wi-Fi to Ethernet:
  https://help.ubuntu.com/community/Internet/ConnectionSharing
    sudo iptables -A FORWARD -o <wifi-interface> -i <Ethernet-interface> -s <subnet, e.g. 10.42.1.0/24> -m conntrack --ctstate NEW -j ACCEPT
    sudo iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
    sudo iptables -t nat -F POSTROUTING
    sudo iptables -t nat -A POSTROUTING -o <wifi-interface> -j MASQUERADE
    sudo iptables-save | sudo tee /etc/iptables.sav
    sudo vi /etc/rc.local
      iptables-restore < /etc/iptables.sav

iptables
	Reset iptables:
		sudo iptables -P INPUT ACCEPT
		sudo iptables -P OUTPUT ACCEPT
		sudo iptables -P FORWARD ACCEPT
		sudo iptables -F
	Set IP tables restore
    sudo vi /etc/rc.local
      iptables-restore < /etc/iptables.sav
	Set rules for sharing Wi-Fi internet wlp82s0 to bridge br0 and physical NIC enp0s31f6
		sudo iptables -A FORWARD -o wlp82s0 -i enp0s31f6 -s 10.42.1.0/24 -m conntrack --ctstate NEW -j ACCEPT
    sudo iptables -A FORWARD -o wlp82s0 -i br0 -s 10.42.1.0/24 -m conntrack --ctstate NEW -j ACCEPT
		sudo iptables -A FORWARD -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
		sudo iptables -t nat -F POSTROUTING
		sudo iptables -t nat -A POSTROUTING -o wlp82s0 -j MASQUERADE
		sudo iptables-save | sudo tee /etc/iptables.sav

