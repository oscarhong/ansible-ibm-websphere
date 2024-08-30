# ansible-ibm-websphere
Ansible playbooks for IBM WebSphere Application Server, Connections 6 and others

# Playbooks

| Playbook name                 | Status         |           Description                                        |
|-------------------------------|----------------|--------------------------------------------------------------|
| ibm-was-nd-complete.yml       | Complete       | Install IBM HTTP Server - 9.0.5.18  |
| ibm-http-server-complete.yml  | Complete       | Install IBM WebSphere Application Server - Network Deployment - 9.0.5.18  |

# Roles

| Role name                       |            Description of Role                                          |
|---------------------------------|-------------------------------------------------------------------------|
| connections-install             | Install IBM Connections |
| db2-jdbc-driver-install         | Deploy db2 jdbc driver |
| ibm-http-adminctl-restart       | Restart IHS Admin Servers |
| ibm-http-adminctl-start         | Start IHS Admin Servers |
| ibm-http-adminctl-stop          | Stop IHS Admin Servers |
| ibm-http-config-plgwct          | Configure HTTP Plugin |
| ibm-http-httpdconf              | Configure httpd.conf |
| ibm-http-server-fix-install     | Install IBM HTTP Server Fixes |
| ibm-http-server-install         | Install IBM HTTP Server |
| ibm-http-server-restart         | Restart IBM HTTP Server Servers |
| ibm-http-server-start           | Start IBM HTTP Server Servers |
| ibm-http-server-stop            | Stop IBM HTTP Server Servers |
| installation-manager-install    | Install IBM Installation Manager   |
| sametime-server-install         | DRAFT: Install Sametime WAS Servers   |
| was-backup-dir-pre-fixes        | Backup WAS directories before apply a fix|
| was-dmgr-config-jvm             | Tune Java Virtual Machine of DMGR |
| was-dmgr-config-ldap            | Configure LDAP Repository (Server must be started) |
| was-dmgr-config-webserver       | Configure WebServers on DMGR |
| was-dmgr-create-profile         | Create a profile for Deployment Manager |
| was-dmgr-enable-app-sec         | Enable application security  |
| was-dmgr-full-sync-nodes        | Do a Full Synchronize with nodes  |
| was-dmgr-import-tls-cert        | Add TLS Signer Certificate to Cell Default Trust Store (Server must be started)|
| was-dmgr-restart                | Restart Deployment Manager |
| was-dmgr-start                  | Start Deployment Manager |
| was-dmgr-stop                   | Stop Deployment Manager |
| was-java-install                | Install IBM Java for WAS  |
| was-nd-fix-install              | Install IBM WAS ND Fixes  |
| was-nd-install                  | Install IBM WebSphere Application Server - Network Deployment - 9.0.5  |
| was-nodeagent-start             | Start Node Agent |
| was-nodeagent-stop              | Stop Node Agent |
| was-profile-cleanup-logs        | Delete and truncate log files for Application Servers|
| was-profile-cleanup-temps       | Delete temp files on WAS Profile (server must be stopped) |
| was-profile-create              | Create a profile for WAS Servers |
| was-profile-delete-all          | Delete all profiles on WAS Servers |
| was-server-start                | Start Applications Servers |
| was-server-stop                 | Stop Applications Servers |



# Getting start

## Prerequisites

1) Download installation files:

* IBM Installation Manager 1.9.2.7 (agent.installer.linux.gtk.x86_64_1.9.2007.20240131_1836.zip)
* IBM WebSphere Application Server 9.0.5
* IBM WebSphere Application Server 9.0.5 Fix Pack 18
* IBM Java software development kits (SDKs) 

2) Copy files to Web Server

Example of my repository
```
-- was
    |-- installation
    |   |-- agent.installer.linux.gtk.x86_64_1.9.2007.20240131_1836.zip
    |-- 9.0.5
    |   |-- was.repo.90501.nd.zip
    |   |-- was.repo.90501.ihs.zip
    |   |-- was.repo.90501.wct.zip
    |   |-- was.repo.90501.plugins.zip
    |   |-- ibm-java-sdk-8.0-8.20-linux-x64-installmgr.zip
    |   |-- FP18
    |   |   |-- 9.0.5-WS-WAS-FP018.zip
    |   |   |-- 9.0.5-WS-IHSPLG-FP018.zip
    |   |   `-- 9.0.5-WS-WCT-FP018.zip 
```
## Configure Ansible hosts file

Change you ansible host file like **hosts.example**


## Cloning ansible-ibm-websphere from git

```
cd /etc/ansible

git clone https://github.com/oscarhong/ansible-ibm-websphere.git
```

## Running playbooks

```
cd /etc/ansible

ansible-playbooks -i environments/hosts.development -u <username> -k playbooks/ibm-was-nd-complete.yml

```

## Running specific Playbooks

```
cd /etc/ansible

ansible-playbooks -i environments/hosts.development -u <username> -k playbooks/ibm-was-nd/ibm-installation-manager.yml

ansible-playbooks -i environments/hosts.development -u <username> -k playbooks/ibm-was-nd/ibm-was-nd.yml

```


# For other versions of IIM, WAS and WAS fixes

1) If you are using a different Fix Pack than FP 15, you must change generate sha256 hashes.

```
Example: sha256sum  9.0.5-WS-WAS-FP018.zip
```
and set variables:

4) Change you ansible host file like

```
[was_servers]
was1.company.com

[was_servers:vars]
...
was_version="9.0.5001.20190828_0616"
```

# Authors

* **Enio Basso** - *Initial work* - [My Repository](https://github.com/ebasso)
* **Oscar Hong** - *Adoption to WAS 9.0.5* - [My Repository](https://github.com/oscarhong)


See also the list of [contributors](https://github.com/ebasso/ansible-ibm-websphere/graphs/contributors) who participated in this project.

# License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
