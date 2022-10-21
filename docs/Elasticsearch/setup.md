## Installing Elasticsearch

```
docker rmi --force $(docker images | grep <image-name> | tr -s ' ' | cut -d ' ' -f 3) `
```

The installation on this article is based on RHEL version 8, you can use dnf instead of yum.

Switch to superuser
```
sudo su
```
Update applications installed on a system
```
yum update
```
Install vim editor - the colored editor may indicate errors in the config files
```
yum -y install vim
```
Install java. You can specify the version and release you desire.
```
yum -y install java
```
Import the elasticsearch GnuPG key
```
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```
Create a file called `elasticsearch.repo` in the `/etc/yum.repos.d/` directory with the command
```
vim /etc/yum.repos.d/elasticsearch.repo
```
and paste the following then save the file:
```
[elasticsearch]
name=Elasticsearch repository for 7.x packages
baseurl=https://artifacts.elastic.co/packages/7.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=0
autorefresh=1
type=rpm-md
```
Install Elasticsearch
```
yum install --enablerepo=elasticsearch elasticsearch
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
```

Elasticsearch import directories:
The RPM places config files, logs, and the data directory in the appropriate locations for an RPM-based system:
Type	Description	Default Location	Setting
home	Elasticsearch home directory or $ES_HOME	/usr/share/elasticsearch	 
bin	Binary scripts including elasticsearch to start a node and elasticsearch-plugin to install plugins	/usr/share/elasticsearch/bin	 
conf	Configuration files including elasticsearch.yml	/etc/elasticsearch	ES_PATH_CONF
conf	Environment variables including heap size, file descriptors.	/etc/sysconfig/elasticsearch	 
data	The location of the data files of each index / shard allocated on the node.	/var/lib/elasticsearch	path.data
 
