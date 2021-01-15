---
title: devpi (PyPi local mirror server)
parent: Python
---

Install devpi-server:  
 [https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-pypimirror.html](https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-pypimirror.html)  
 ---  
```
 virtualenv -p python3 venv-devpi  
 source venv-devpi/bin/activate  
 pip install -U devpi-server  
    pip install -U devpi-web  
 devpi-server --start --init \# Remove '--init' for reinstall  
```
Set up as systemd service:  
 `devpi-server --stop`  
 \(move ~/.devpi/server to desired data directory\)  
 `/etc/systemd/system/devpi.service`  
```
  [Unit]  
  Description=Devpi Server  
  Requires=network-online.target  
  After=network-online.target  

  [Service]  
  Restart=on-success  
  ExecStart=/home/jurban/Development/devpi/venv-devpi/bin/devpi-server --port 3141 --serverdir   
  # set User according to user which is able to run the devpi-server  
  User=  

  [Install]  
  WantedBy=multi-user.target
```  
 `sudo systemctl start devpi`  
 `sudo systemctl enable devpi`  
Install package using devpi as caching mirror:  
 `pip install -i http://:3141/root/pypi/`   
Install `devpi-web` \(for search\):  
```
 pip install -U devpi-web  
 devpi-server --stop  
 devpi-server --recreate-search-index --offline  
 devpi-server --start  
```
Search index with pip:  
 `pip search --index http://localhost:3141/root/pypi/`
GUI:  
 [http://localhost:3141](http://localhost:3141)  
 Docs: [https://devpi.net/docs/devpi/devpi/stable/+doc/adminman/web.html](https://devpi.net/docs/devpi/devpi/stable/+doc/adminman/web.html)  
 ---  
 Check status, search repos, basic package documentation.  
Set up devpi client:  
```
 pip install devpi-client  
 devpi use http://localhost:3141
 devpi login root  
 devpi user -m root password=
```  
 Create the first non-root user:  
  `devpi user -c  email= password=`  
 `devpi logout`
Client Login:  
 `devpi login`   
Client logout:  
 `devpi logout`  
Configure pip to use devpi:  
 `~/.pip/pip.conf`  
  Caution: Use absolute paths, since variable `$HOME/` or relative path `~/` are not respected, at least on my Jetson Nano install.  
  ---  
```
  [global]  
  index-url = http://localhost:3141/root/pypi/  
  default-timeout = 60  
  respect-virtualenv = true  
  download-cache = ~/.pip/cache  
  log-file = /home//.pip/pip.log  
  build = /home//.pip/build  

  [search]  
  index = http://localhost:3141/root/pypi/
```
Configure PyCharm to use devpi:  
 [https://blog.jetbrains.com/pycharm/page/33/?ref=driverlayer.com](https://blog.jetbrains.com/pycharm/page/33/?ref=driverlayer.com)  
 ---  
 Settings -&gt; Project -&gt; Project Interpreter -&gt; + Manage Repositories  
 Add URL\(s\) for devpi repos.  
 ? Remove other, such as default?  
---  
Organize rough notes:
 Need to create user before can use `restrict-modify` in `config.yml`, except user root is created by default, so can include `restrict-modify: root`
   root password is empty by default.
 Open questions:  
 What is `/etc/devpi-server/secret` used for? See `devpi-server.yml`  
 How to block the `/+changelog` route ?  
  [https://devpi.net/docs/devpi/devpi/stable/+doc/adminman/security.html](https://devpi.net/docs/devpi/devpi/stable/+doc/adminman/security.html)  
 Since I've specified to use `devpi` in `~/.pip/pip.conf`, do I still need to set up the `devpi` repo in PyCharm projects?  

[https://www.devpi.net/](https://www.devpi.net/)  
  Docs: [https://devpi.net/docs/devpi/devpi/stable/%2Bd/index.html](https://devpi.net/docs/devpi/devpi/stable/%2Bd/index.html)  
  Non-permanent install:  
   [https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-pypimirror.html](https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-pypimirror.html)  
  Permanent install:  
   [https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-server.html](https://devpi.net/docs/devpi/devpi/stable/+doc/quickstart-server.html)  
  Supported in PyCharm:  
   [https://blog.jetbrains.com/pycharm/page/33/?ref=driverlayer.com](https://blog.jetbrains.com/pycharm/page/33/?ref=driverlayer.com)
