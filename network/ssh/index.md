---
title: SSH
parent: Network
has_children: true
---

# Pass SSH keys to server

`ssh-copy-id <user>@<ip-address>`

# Disable non-key SSH access:

1. Modify `/etc/ssh/sshd_config`:

```text
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM no
```

2. Restart SSH: `sudo systemctl restart ssh`

# SSH tunnels  

For each example consider three hosts:  

Host outside private network (e.g. laptop)  

Private Network: Public Host (e.g. web server) <-> Private Host (e.g. database server)  

## Local Tunnel  

From outside, access private through public.  

Use case: troubleshoot database server for web application.  

`ssh -L :: <user>@`  

Multiple local tunnels from single SSH:  

`ssh -L :: -L :: <user>@`  

## Remote Tunnel  

From outside, allow private to access outside through public.  

Use case: deliver API from development computer to collaborate with colleague.  

`ssh -R :localhost: <user>@`  

Prerequisite:  
- Set `GatewayPorts yes` in `/etc/ssh/ssh_config`  
- `systemctl restart sshd`  

## Dynamic Tunnel  

From outside, access reachable hosts through public.  

Configure browser to use that address and port as a SOCKS (socket) proxy to access resources.  

_e.g. Firefox Preferences -> Network Proxy -> Settings_

- _Manual proxy configuration, SOCKS Host: localhost, Port: , SOCKS v5_

Use case: access private network resources similar to VPN. SOCKS proxy is more secure and more flexible \(for different protocols and ports\) than an HTTP proxy.  

`ssh -D  <user>@`  

# Clear keys for target

`ssh-keygen -f "~/.ssh/known\_hosts" -R`

# Set up tunnel for one-step SSH

[Reference](https://www.sweetprocess.com/procedures/_AmM86Weq31FO0WDp5kRZFDBKRjB/ssh-tunnel-between-two-servers-behind-firewalls/)

## On bridge server:

`/etc/ssh/sshd_config`: `GatewayPorts yes`

(Open port on firewall)  

# ngrok

ssh access

## target:

```bash
nohup ./ngrok tcp 22 > /dev/null &
export WEBHOOK_URL="$(curl http://localhost:4040/api/tunnels | jq ".tunnels[0].public_url")"
echo $WEBHOOK_URL
```

## local:

`ssh <user>@0.tcp.ngrok.io -p <port>  # URL and port from WEBHOOK_URL`

# AutoSSH

Drop-in replacement for SSH that includes health-check, so connection shouldn't drop (and leave process alive without connection)

