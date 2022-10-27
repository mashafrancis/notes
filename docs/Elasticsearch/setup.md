## Installing Elasticsearch

The installation on this article is based on RHEL version 8, you can use dnf instead of yum.

Switch to superuser

    sudo su

Update applications installed on a system

    yum update

Install vim editor - the colored editor may indicate errors in the config files

    yum -y install vim

Install java. You can specify the version and release you desire.

    yum -y install java

Import the elasticsearch GnuPG key

    rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch

Create a file called `elasticsearch.repo` in the `/etc/yum.repos.d/` directory with the command

    vim /etc/yum.repos.d/elasticsearch.repo

and paste the following then save the file:

    [elasticsearch] name=Elasticsearch repository for  8.x packages
    baseurl=https://artifacts.elastic.co/packages/8.x/yum
    gpgcheck=1 
    gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
    enabled=0 
    autorefresh=1 
    type=rpm-md

Install Elasticsearch

    yum install --enablerepo=elasticsearch elasticsearch
    systemctl daemon-reload
    systemctl enable elasticsearch.service
    systemctl start elasticsearch.service
    
    
Reference link
[Elasticsearch setup](https://www.elastic.co/guide/en/elasticsearch/reference/current/rpm.html)
