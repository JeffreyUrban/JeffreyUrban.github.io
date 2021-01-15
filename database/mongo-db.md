---
title: MongoDB
parent: Database
---

Uses `bson` \(JSON in binary\)

Document is like a pre-computed join.

## Installation:

[https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)  
Using the official version, so check for and uninstall the ubuntu packaged version \(unsupported\):  
`sudo apt list --installed | grep mongodb`

Install \(here, version 4.2\):

```bash
wget -qO - https://www.mongodb.org/static/pgp/server-4.2.asc | sudo apt-key add -
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.2.list
sudo apt update
```

## **Interactive Shell:**

Open: `mongo`

### Free Monitoring

Toggle:  
`db.enableFreeMonitoring()  
db.disableFreeMonitoring()`

Access:  
https://cloud.mongodb.com/freemonitoring/cluster/&lt;unique-id&gt;
