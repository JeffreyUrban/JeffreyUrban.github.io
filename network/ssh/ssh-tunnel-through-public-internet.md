---
title: 'SSH Tunnel through public Internet bridge'
parent: SSH
grand_parent: Network
---

This method supports SSH connections on demand from a client \(local\) to a server \(target\) that are each behind firewalls from the public internet that block incoming SSH connections, using a server \(bridge\) on a public cloud provider.

### There are three computers:

#### bridge

A server available on the public Internet. Set up for Gateway ports, has our ports allowed in the firewall, and has the public key from target and local.

#### target

Has a systemd process that connects to the bridge on a randomly selected port and maps that port to its local SSH port 22, so we can connect to it. This gets us through any firewalls that block incoming connections, since it is established as an outgoing connection.

#### local

Connects to bridge on that port and leaves it open. Then local SSHes to itself on the local port that is mapped to the tunnel through bridge to target.

### Mode of operation

1st level SSH connections: local -&gt; bridge &lt;- target  
\(separate connections to bridge\)

2nd level SSH connection: local -&gt; ~~bridge~~ -&gt; target  
\(passes through, bridge, but bridge does not participate\)

The final SSH tunnel connects securely from the local to the target, but is routed through the bridge, by riding on two SSH connections, one from target-&gt;bridge and the other from local-&gt;bridge. bridge holds the two sides together, but doesn't participate in the SSH session that it passes through. The data goes through bridge, but it doesn't decrypt it. The bridge does not have credentials to initiate connections to the other computers.

## Bridge Server:

### Set up: 

Set up users and \(required\) SSH keys.

`/etc/ssh/sshd_config` Set values: 

```text
    PasswordAuthentication no
    ChallengeResponseAuthentication no
    UsePAM no
    GatewayPorts yes
```

## Target Servers:

Port is random selection from non-reserved, non-ephemeral ports 1024-32767.  
Here, we're using port 12345.

### Set up:

`/etc/hosts`  Add:

```text
<bridge-IP> <bridge-hostname>
```

Create a systemd task that starts on boot and restarts on failure.

`/lib/systemd/system/ssh-tunnel.service` 

```text
[Unit]
Description=Persistent Connection to SSH Tunnel bridge server.

[Service]
Type=simple
User=target_user
ExecStart=/usr/bin/ssh -o TCPKeepAlive=no -o ServerAliveInterval=15 -nNT -R 12345:localhost:22 target_user@bridge
WorkingDirectory=/home/target_user
Restart=always
RestartSec=30
StartLimitIntervalBurst=5
StartLimitInterval=0

[Install]
WantedBy=multi-user.target
```

`sudo systemctl enable ssh-tunnel.service   
sudo systemctl start ssh-tunnel.service`

## Local Client

### Set up: 

`/etc/hosts` Add:

```text
<bridge-IP> <bridge-hostname>
```

`~/.local/bin/ssh-tunnel` Choose location on `$PATH`

```text
#!/bin/bashport=0user=$1
bridge=$2
target=$3
[[ $bridge == "bridge" ]] && [[ $target == "target" ]] && port=12345
# Add more bridge / target -> port combinations here
[ $port == 0 ] && echo "Missing or invalid argument." && echo "ssh-tunnel [user] [bridge] [target]" && exit 1
echo "ssh -o ExitOnForwardFailure=yes -o TCPKeepAlive=no -o ServerAliveInterval=15 -nNT -L $port:localhost:$port $bridge >> /dev/null 2>&1 2>&1 &"
sleep 1  # Allow time for this connection before next connection.
# The above command outputs harmless but confusing errors if the SSH tunnel to bridge is already active, so output is suppressed.
# If your user mismatches the user on the bridge server, change $bridge to $user@bridge
ssh -o TCPKeepAlive=no -o ServerAliveInterval=15 $user@localhost -p $port
```

If your user name on the bridge server differs from your local username, change $bridge to &lt;user&gt;@$bridge, or add your username account on the bridge server.

One-time task to establish connection \(since may need to confirm the first time\): 

```text
port=12345 
ssh -o ExitOnForwardFailure=yes -o TCPKeepAlive=no -o ServerAliveInterval=15 -nNT -L $port:localhost:$port bridge
```

This may ask you to confirm the connection, but then should appear to hang.  
If necessary, change tunnel to &lt;user&gt;@bridge.  
Leave the above command line running \(or restart it\).

On a 2nd terminal:

```text
ssh -o TCPKeepAlive=no -o ServerAliveInterval=15 target_user@localhost -p $port
```

Confirm to connect

### Connect each time:

```text
ssh-tunnel target_user bridge target
```

### To troubleshoot connection issues:

Do a normal SSH into bridge and check if the port is up:

```text
ss -tulpn 
Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port
... 
tcp LISTEN 0 128 0.0.0.0:12345 0.0.0.0:
tcp LISTEN 0 128 [::]:12345 [::]:
```

### Inspired by:

[https://www.sweetprocess.com/procedures/\_AmM86Weq31FO0WDp5kRZFDBKRjB/ssh-tunnel-between-two-servers-behind-firewalls/](https://www.sweetprocess.com/procedures/_AmM86Weq31FO0WDp5kRZFDBKRjB/ssh-tunnel-between-two-servers-behind-firewalls/)
