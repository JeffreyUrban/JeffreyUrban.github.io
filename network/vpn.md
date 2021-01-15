---
title: VPN - OpenVPN
parent: Network
---

Set up \(basic skeleton configuration\)  
  Note: for easy-rsa on Ubuntu:  
   [https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-ubuntu-18-04)  
  On VPN server:  
   Install:  
    `yum install -y epel-release` \# Extra Packages for Enterprise Linux from Fedora  
     \# Applies to Enterprise Linux, including, but not limited to, Red Hat Enterprise Linux \(RHEL\), CentOS and Scientific Linux \(SL\), Oracle Linux \(OL\)  
    `yum install -y openvpn`  
   Set up firewall for desired port and protocol:  
    `firewall-cmd --permanent --add-port=`  
     \# Standard is `1194/udp`  
      Configure with UDP for higher performance, TCP for higher reliability  
      Choose `443/tcp` to make traffic indistinguishable from HTTPS  
    `firewall-cmd --permanent --add-masquerade`  
    `firewall-cmd --reload`  
   Set up keys / credentials:  
    RSA keys and certs for client and server:  
     `yum install -y easy-rsa`  
     `mkdir /etc/openvpn/easy-rsa`  
     `cd /etc/openvpn/easy-rsa/`  
     Temporarily add desired version to path:  
      `PATH=$PATH:/usr/share/easy-rsa/`  
     `easyrsa init-pki \# See /etc/openvpn/easy-rsa/pki`  
     `easyrsa build-ca \# See /etc/openvpn/easy-rsa/pki/private/ca.key`  
     `easyrsa gen-dh \# See /etc/openvpn/easy-rsa/pki/dh.pem`  
     `easyrsa gen-req server nopass \# See /etc/openvpn/easy-rsa/pki/private/server.key`  
      \# optionally `nopass` for no password on key.  
     `easyrsa sign-req server server` \# See `/etc/openvpn/easy-rsa/pki/issued/server.crt`  
      `yes`  
     `easyrsa gen-req client nopass` \# See `/etc/openvpn/easy-rsa/pki/private/client.key`  
      \# optionally `nopass` for no password on key.  
     `easyrsa sign-req client client` \# See `/etc/openvpn/easy-rsa/pki/issued/client.crt`  
    TLS key:  
     \(TLS ensures privacy of previous sessions, even if private key compromised\)  
     `cd /etc/openvpn`  
     `openvpn --genkey --secret pfs.key`  
   Configure:  
    Examples with documentation in: `/usr/share/doc/openvpn-/sample/sample-config-files/`  
     Can copy into `/etc/openvpn/server.conf`  
    `/etc/openvpn/server.conf`  
     Example:  
```
      port 1194  
      proto tcp  
      dev tun  
      ca /etc/openvpn/easy-rsa/pki/ca.crt  
      cert /etc/openvpn/easy-rsa/pki/issued/server.crt  
      key /etc/openvpn/easy-rsa/pki/private/server.key  
      dh /etc/openvpn/easy-rsa/pki/dh.pem  
      topology subnet  
      cipher AES-256-CBC  
      auth SHA512  
      server 10.8.0.0 255.255.255.0  
      push "redirect-gateway def1 bypass-dhcp"  
      push "dhcp-option DNS 8.8.8.8"  
      push "dhcp-option DNS 8.8.4.4"  
      ifconfig-pool-persist ipp.txt  
      keepalive 10 120  
      comp-lzo  
      persist-key  
      persist-tun  
      status openvpn-status.log  
      log-append openvpn.log  
      verb 3  
      tls-server  
      tls-auth /etc/openvpn/pfs.key  
 ```
     \(details on some entries\):  
      `dev tun` \# tun is routed IP tunnel. Other options available  
      `topology subnet` \# subnet is recommended topology  
      `server`  \# Subnet server uses for assigning IPs \(?\)  
        _**Do I need to request these from my cloud provider?**_   
      `push "dhcp-option DNS "` \# Select a DNS server   
      `ifconfig-pool-persist ipp.txt`  
       \# Record of client to virtual IP address associations, to assign same IPs in case openvpn restarts  
      `keepalive`    
       \# Configures keep alive message frequency b/w client, server  
      `comp-lzo` \# Configure compression. Client must match server.  
      `verb`  \# Log verbosity level from 0 \(only critical errors\) to 9 \(most verbose\)  
   Enable IPv4 packet forwarding:  
   Edit `sysctl.conf`:  
    `net.ipv4.ip_forward=1`  
    Reload `sysctl.conf`: `sysctl -p`  
   Start VPN:  
    `systemctl start openvpn@server.service` \# Include `@server.service` to use `server.conf`  
   Prepare keys for client:  
```
    cd /etc/openvpn  
    mkdir -p server1/keys  
    cp pfs.key server1/keys/  
    cp easy-rsa/pki/dh.pem server1/keys/  
    cp easy-rsa/pki/ca.crt server1/keys/  
    cp easy-rsa/pki/private/ca.key server1/keys/  
    cp easy-rsa/pki/private/client.key server1/keys/  
    cp easy-rsa/pki/issued/client.crt server1/keys/  
    tar cvzf /tmp/keys.tgz server1/  
```
   \(continue on client\)  
  On VPN client:  
   Install:  
    `yum install -y epel-release`  
    `yum install -y openvpn`  
   Collect keys:  
```
    cd /etc/openvpn  
    scp &lt;user&gt;@: ./  
    tar xvzf keys.tgz  
```
   Configure:  
    Examples in: `/usr/share/doc/openvpn-/sample/sample-config-files/`  
     Can copy into `/etc/openvpn/client.conf`  
    Example:  
```
     client  
     dev tun  
     proto tcp  
     remote 10.0.1.10 1194  
     ca server1/keys/ca.crt  
     cert server1/keys/client.crt  
     key server1/keys/client.key  
     tls-version-min 1.2  
     tls-cipher TLS-ECDHE-RSA-WITH-AES-128-GCM-SHA256:TLS-ECDHE-ECDSA-WITH-AES-128-GCM-SHA256:TLS-ECDHE-RSA-WITH-AES-256-GCM-SHA384:TLS-DHE-RSA-WITH-AES-256-CBC-SHA256  
     cipher AES-256-CBC  
     auth SHA512  
     resolv-retry infinite  
     auth-retry none  
     nobind  
     route-nopull  
     persist-key  
     persist-tun  
     ns-cert-type server  
     comp-lzo  
     verb 3  
     tls-client  
     tls-auth server1/keys/pfs.key  
    \(details on some entries\):  
     remote   \# Server IP and port  
     route-nopull \# Important. Not setting up any routing. \(?\)  
```
   Start VPN \(as service\):  
    `systemctl start openvpn@client.service` \# Include `@client` to use `client.conf`  
   Start VPN \(as application\):  
    `sudo openvpn --config .ovpn`  
   Check tunnel:  
    `ip a` \# see `tun0`, our VPN tunnel, with assigned IP from VPN server  
     \# Note, entry in `ip a` shows connection, but we may not be routing to it.  
    `ip r s` \# \(`ip route show`\) see `tun0` entry for routing rule to use VPN  
   Add static route for client to use VPN:  
    `ip r add  dev tun0`  
     _**How to monitor and identify which IPs / domains are blocked or perform poorly on / off VPN? Consider that I may not want to improve all IPs / domains \(ads, tracking, etc.\)**_   
 Monitor VPN:  
  Client connections for persistence:  
   `/etc/openvpn/ipp.txt` \# See `server.conf` `ifconfig-pool-persist ipp.txt`  
  General log:  
   `/etc/openvpn/openvpn.log` \# Per logging configuration in `server.conf`  
  Client list and connection details:  
   `/etc/openvpn/openvpn-status.log`  

https://superuser.com/questions/709376/is-it-possible-to-have-2-different-vpn-connections-simultaneously-on-the-same-ma
