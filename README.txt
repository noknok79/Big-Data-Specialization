#################################################################
#For Master Install Postgres


yum install https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm -y
sleep 2
yum install postgresql10 postgresql10-server postgresql10-contrib postgresql10-libs -y
sleep 1
/usr/pgsql-10/bin/postgresql-10-setup initdb
sleep 2
systemctl enable postgresql-10.service && systemctl start postgresql-10.service && systemctl status postgresql-10.service
	
su – postgres
psql
sudo /opt/cloudera/cm/schema/scm_prepare_database.sh postgresql fly postgres

create database bigdata;
create database hive;
create database amon;
create database rman;
create database oozie_oozie_server;
create database hue;
create database sentry;
create database nav;
create database navms;
create database clouderascm;


create user hive with encrypted password 'markv109';
create user amon with encrypted password 'markv109';
create user rman with encrypted password 'markv109';
create user oozie_oozie_server with encrypted password 'markv109';
create user hue with encrypted password 'markv109';
create user sentry with encrypted password 'markv109';
create user nav with encrypted password 'markv109';
create user navms with encrypted password 'markv109';
create user clouderascm with encrypted password 'markv109';
create user noknok with encrypted password 'markv109';


grant all privileges on database bigdata to noknok;
grant all privileges on database hive to noknok;
grant all privileges on database amon to noknok;
grant all privileges on database rman to noknok;
grant all privileges on database oozie_oozie_server to noknok;
grant all privileges on database hue to noknok;
grant all privileges on database sentry to noknok;
grant all privileges on database nav to noknok;
grant all privileges on database navms to noknok;
grant all privileges on database clouderascm to noknok;



#################################################################
#For Master M
#MAKE SURE YOU HAVE SET THE TIMEZONE TO PHILIPPINES
#DOUBLE CHECK IF THE FIREWALLD is DISABLE

STEP 1
#!/bin/bash

echo never > /sys/kernel/mm/transparent_hugepage/enabled 

sleep 1
echo never > /sys/kernel/mm/transparent_hugepage/defrag 

sleep 1
sysctl vm.swappiness=1

sleep 1
iptables-save > ~/firewall.rules 

sleep 1
systemctl stop firewalld 

sleep 1
systemctl disable firewalld

sed -i "/^SELINUX=enforcing*/c\SELINUX=disabled" /etc/selinux/config

#dnf install -y https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-13.noarch.rpm

init 6

clear




STEP 2
#!/bin/bash
 
yum -y install ntp

sleep 1
systemctl start ntpd

sleep 1 
systemctl enable ntpd

sleep 1 
systemctl status ntpd

sleep 1
systemctl status chronyd 

slee5 1
systemctl disable chronyd

hostname $(hostname -I)

sleep 1
yum -y install java-1.8.0-openjdk-devel

sleep 1
systemctl disable autofs

sleep 1
systemctl is-enabled autofs

cd /boot/grub2
stat /boot/grub2/grub.cfg
chmod og-rwx /boot/grub2/grub.cfg
echo "copy and execute"
echo "grub2-mkconfig > /boot/grub2/grub.cfg"
echo "grub2-mkconfig > /boot/grub2/grub.cfg"
grub2-mkpasswd-pbkdf2 




Step 3 SETUP YOUR IP IN /ETC/HOSTS
#!/bin/bash

yum remove prelink
cd /home
sleep 1
yum -y install httpd

sleep 1
systemctl start httpd

sleep 1
systemctl enable httpd

sleep 1
systemctl status httpd

#touch hosts.txt
#echo -n "" > hosts.txt
#echo -n "" > /etc/hosts
#echo "10.128.0.52 instance-1.trisha.com master1" >> hosts.txt
#echo "10.128.0.53 instance-2.trisha.com worker1" >> hosts.txt
#echo "10.142.0.18 instance-3.trisha.com worker2" >> hosts.txt
#echo "10.128.0.54 instance-4.trisha.com worker3" >> hosts.txt
#echo "10.128.0.55 instance-5.trisha.com worker4" >> hosts.txt

sleep 1
#touch hosts.txt
#echo -n "" > hosts.txt
#echo -n "" > /etc/hosts
#echo "35.238.126.251 master1.trisha.com ma1" >> hosts.txt
#echo "35.232.230.24 worker1.trisha.com wm1" >> hosts.txt
#echo "35.202.100.194 worker2.trisha.com wm2" >> hosts.txt
#echo "34.121.21.128 worker3.trisha.com wm3" >> hosts.txt
#echo "34.70.36.0 worker4.trisha.com wm4" >> hosts.txt
#echo "34.122.245.56 worker5.trisha.com wm5" >> hosts.txt
#cat hosts.txt >> /etc/hosts
#systemctl restart systemd-hostnamed 
#systemctl restart network 

sed -i "/^PasswordAuthentication no*/c\PasswordAuthentication yes" /etc/ssh/sshd_config
sed -i "/^PermitRootLogin no*/c\PermitRootLogin yes" /etc/ssh/sshd_config
systemctl restart sshd
sed -i "/^## Allow root to run any commands anywhere*/c\noknok    ALL=(ALL)       ALL" /etc/sudoers
echo "create username noknok,sudo su noknok, then run the ssh-keygen"
echo "ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.2.x"




Step 4 
#!/bin/bash
cd /home
sleep 1
mkdir -p /var/www/html/cloudera-repos/
mkdir -p /var/www/html/cloudera-repos/cm6
cd /var/www/html/cloudera-repos/cm6
yum install wget -y

wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/cloudera-manager-server-db-2-6.2.0-968826.el7.x86_64.rpm \ 
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/cloudera-manager-server-6.2.0-968826.el7.x86_64.rpm \
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/cloudera-manager-daemons-6.2.0-968826.el7.x86_64.rpm \
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/cloudera-manager-agent-6.2.0-968826.el7.x86_64.rpm \
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/enterprise-debuginfo-6.2.0-968826.el7.x86_64.rpm \
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/oracle-j2sdk1.8-1.8.0%2Bupdate181-1.x86_64.rpm \
wget https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-13.noarch.rpm

sleep 1
yum install -y cloudera-manager-daemons-6.2.0-968826.el7.x86_64.rpm cloudera-manager-server-6.2.0-968826.el7.x86_64.rpm cloudera-manager-agent-6.2.0-968826.el7.x86_64.rpm cloudera-manager-server-db-2-6.2.0-968826.el7.x86_64.rpm oracle-j2sdk1.8-1.8.0+update181-1.x86_64.rpm

#yum clean all
#yum update -y

#cd /etc/yum.repos.d/
#rm -r -f cloudera-manager-repo
#echo -n "" > /etc/yum.repos.d/cloudera-manager.repo
#echo -n "" > repo2.txt
#echo "[cloudera-repo] " >> repo2.txt
#echo "name=cloudera-manager " >> repo2.txt
#echo "baseurl=http://35.237.185.141/cloudera-repos/cdh/ " >> repo2.txt
#echo "enabled=1 " >> repo2.txt
#echo "gpgcheck=0 " >> repo2.txt

#touch -a cloudera-manager.repo 
#cat repo2.txt >> cloudera-manager.repo

cd /etc/yum.repos.d/
rm -r -f cloudera-manager-repo
echo -n "" > /etc/yum.repos.d/cloudera-manager.repo
echo -n "" > repo2.txt
echo "[cloudera-manager] " >> repo2.txt
echo "# Packages for Cloudera Manager, Version 6, on RedHat or CentOS 7 x86_64 " >> repo2.txt
echo "name=Cloudera Manager " >> repo2.txt
echo "#baseurl=http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/5/ " >> repo2.txt
echo "baseurl=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/ " >> repo2.txt
echo "#gpgkey=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera " >> repo2.txt
echo "#gpgkey=http://39.98.155.100/cloudera-repos/cm6/6.2.1/redhat7/yum/RPM-GPG-KEY-cloudera " >> repo2.txt
echo "enable = 1 " >> repo2.txt
echo "gpgcheck = 1 " >> repo2.txt

touch -a cloudera-manager.repo 
cat repo2.txt >> cloudera-manager.repo

#listening_ip=listening_ip=34.70.36.0
#listening_hostname=listening_hostname=34.70.36.0
#sed -i "/^server_host=localhost*/c$server_host" /etc/cloudera-scm-agent/config.ini
#sed -i "/^# listening_ip=*/c$listening_ip" /etc/cloudera-scm-agent/config.ini
#sed -i "/^# listening_hostname=*/c$listening_hostname" /etc/cloudera-scm-agent/config.ini

touch /etc/cloudera-scm-server/db.properties
systemctl start cloudera-scm-agent && systemctl enable cloudera-scm-agent && systemctl status cloudera-scm-agent 
systemctl start cloudera-scm-server && systemctl enable cloudera-scm-server && systemctl status cloudera-scm-server
sleep 3
systemctl start cloudera-scm-server-db && systemctl enable cloudera-scm-server-db && systemctl status cloudera-scm-server-db
rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid


sleep 1
mkdir /var/www/html/cloudera-repos/cdh
cd /var/www/html/cloudera-repos/cdh
#wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cdh6/parcels/latest/CDH-6.2.0-1.cdh6.2.0.p0.967373-el7.parcel.sha256 \
#wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cdh6/parcels/latest/CDH-6.2.0-1.cdh6.2.0.p0.967373-el7.parcel \
#wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cdh6/parcels/latest/manifest.json 
cd /home

rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid
netstat -tulpn |grep LISTEN
echo "CHANGE THE SERVICE IP ADDRESS IN AGEN CONFIG FILES"
echo " watch 'tail /var/log/cloudera-scm-server/cloudera-scm-server.log' "







#Run the command if the admin page giving you error

touch /etc/cloudera-scm-server/db.mgmt.properties
touch /etc/cloudera-scm-server/db.properties 
rm -rf /etc/cloudera-scm-server/db.properties.*
rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid
init 6






to access

http://localhost:7180



#CDH Parcel 
http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cdh6/parcels/6.2.0/

#IN AWS Server Ports must be open
7180, 7182, 80, 443, 22

#################################################
Troubleshooting in Cloudera
#TO have healthy host
rm /var/lib/cloudera-scm-agent/cm_guid

#Failing to install oozie
rm -rf /rms/var/lib/oozie/*

##################################################
additional execution for workers		 #
input the ip address in for hosts and server_host#
##################################################
rm /var/lib/cloudera-scm-agent/cm_guid
rm -rf /rms/var/lib/oozie/*
hostname $(hostname -I)
server_host=server_host=localhost
sed -i "/^server_host=localhost*/c$server_host" /etc/cloudera-scm-agent/config.ini
systemctl restart cloudera-scm-agent && systemctl status cloudera-scm-agent
systemctl stop cloudera-scm-server && systemctl stop cloudera-scm-server-db

sleep 1
rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid
hostname $(hostname -I)
touch hosts.txt
echo -n "" > hosts.txt
echo -n "" > /etc/hosts
echo "192.168.2.112 master1.trisha.com ma1" >> hosts.txt
echo "10.128.0.6 worker1.trisha.com wm1" >> hosts.txt
echo "10.128.0.7 worker2.trisha.com wm2" >> hosts.txt
echo "10.128.0.8 worker3.trisha.com wm3" >> hosts.txt
echo "34.70.36.0 worker4.trisha.com wm4" >> hosts.txt
echo "34.122.245.56 worker5.trisha.com wm5" >> hosts.txt
echo "127.0.0.1 localhost" >> hosts.txt
cat hosts.txt >> /etc/hosts
systemctl restart systemd-hostnamed 
systemctl restart network

#For localhost installation

sleep 1
rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid
hostname $(hostname -I)
touch hosts.txt
echo -n "" > hosts.txt
echo -n "" > /etc/hosts
echo "192.168.2.28 localhost" >> hosts.txt
echo "127.0.0.1 master1.trisha.com" >> hosts.txt
cat hosts.txt >> /etc/hosts
systemctl restart systemd-hostnamed 
systemctl restart network



##################################################
additional execution for workers		 #
input the ip address in for hosts and server_host#
##################################################

hostname $(hostname -I)
systemctl stop cloudera-scm-server
systemctl stop cloudera-scm-server-db
systemctl disable cloudera-scm-server
systemctl disable cloudera-scm-server-db

server_host=server_host=localhost
sed -i "/^server_host=localhost*/c$server_host" /etc/cloudera-scm-agent/config.ini
systemctl restart cloudera-scm-agent && systemctl status cloudera-scm-agent

sleep 1
rm -rf /rms/var/lib/oozie/*
rm -f -r /var/lib/cloudera-scm-agent/cm_guid
touch hosts.txt
echo -n "" > hosts.txt
echo -n "" > /etc/hosts
echo "192.168.2.248 master1.trisha.com ma1" >> hosts.txt
echo "192.168.2.42 worker1.trisha.com wm1" >> hosts.txt
echo "35.239.128.56 worker2.trisha.com wm2" >> hosts.txt
echo "34.121.21.128 worker3.trisha.com wm3" >> hosts.txt
echo "34.70.36.0 worker4.trisha.com wm4" >> hosts.txt
echo "34.122.245.56 worker5.trisha.com wm5" >> hosts.txt
echo "127.0.0.1 localhost" >> hosts.txt
cat hosts.txt >> /etc/hosts
systemctl restart systemd-hostnamed 
systemctl restart network



shutdown now

to check log files 

watch 'head -n 2 /var/log/cloudera-scm-server/cloudera-scm-server.log;' 
watch 'tail /var/log/cloudera-scm-server/cloudera-scm-server.log;'

#TO make it work in 1 localhost pc, 2 vm machines.
master node must be live ip
worker node must be inside ip that connects to live ip.
worker node listening ip/host must set inside ip
########################################################################
########################################################################
########################################################################
#netstat -tulpn | grep LISTEN

#REMINDER:
To make sure the agents are manage to the server, it is a MUST to set the server_hostname=10.x.x.x of server in /etc/cloudera-scm-agent/config.ini
no other necessary configuration to other files.


#BEFORE RUNNING THE SCRIPT, IT IS REQUIRED TO SECURE THE VM
useradd -m <new_user>
passwd <new_user>
mkdir tmp #directo for rsakeys
cd tmp/
ssh-keygen
#enter the folder /home/<username>/tmp/<filename_of_keys>, enter then enter
ssh-copy-id -i <folder/file_key> username@ip

[cloudera-cdh]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 6 x86_64
name=Cloudera Manager
#baseurl=http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/5/
baseurl=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/
gpgkey=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgcheck = 1

[cloudera-manager]
# Packages for Cloudera Manager, Version 5, on RedHat or CentOS 6 x86_64
name=Cloudera Manager
#baseurl=http://archive.cloudera.com/cm5/redhat/6/x86_64/cm/5/
baseurl=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/
#gpgkey=http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm5/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
gpgkey=http://39.98.155.100/cloudera-repos/cm6/6.2.1/redhat7/yum/RPM-GPG-KEY-cloudera
gpgcheck = 1

#How to install Hadoop
https://github.com/bright60/hadoop_install
# ALLKEYS.asc
https://mirror.one.com/cloudera/cm6/6.2.0/allkeys.asc
http://39.98.155.100/cloudera-repos/cm6/6.2.1/

#Cloudera RPM-GPN-Key
http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/RPM-GPG-KEY-cloudera
http://39.98.155.100/cloudera-repos/cm6/6.2.1/redhat7/yum/RPM-GPG-KEY-cloudera
http://39.98.155.100/cloudera-repos/cm6/6.2.1/redhat7/yum/RPM-GPG-KEY-cloudera

#CDH Parcel 
#http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cdh6/parcels/6.2.0/
#CM6 link
#http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/
#http://39.98.155.100/cloudera-repos/cm6/6.2.1/redhat7/yum/
#REMIND to check the service-hostname in the /etc/cloudera-scm-agent/config it must be lastest master ip

#To adduser/change noknok to no password login to other server

adduser -m noknok
passwd noknok
vi /etc/sudoers
root    ALL=(ALL)       ALL
noknok  ALL=(ALL)       ALL
sed -i "/^## Allow root to run any commands anywhere*/c\noknok    ALL=(ALL)       ALL" /etc/sudoers 
sed -i "/^PasswordAuthentication no*/c\PasswordAuthentication yes" /etc/ssh/sshd_config
systemctl restart sshd

sudo su noknok
ssh-keygen 
ssh-copy-id -i ~/.ssh/id_rsa.pub noknok@ip

#To secure grub boot, should run in all master and worker servers.

cd /boot/grub2
stat /boot/grub2/grub.cfg
chmod og-rwx /boot/grub2/grub.cfg
grub2-mkpasswd-pbkdf2 

grub2-mkconfig > /boot/grub2/grub.cfg

#how to install mysql server follow the link
https://docs.cloudera.com/documentation/enterprise/6/6.3/topics/cm_ig_mysql.html#cmig_topic_5_5_2

#Connecting mysql to jdbc, important in setting up mysql as database for production follow the link
#input the suggestion configuration file in /etc/my.cnf
https://docs.cloudera.com/documentation/enterprise/6/6.3/topics/prepare_cm_database.html
https://docs.cloudera.com/documentation/enterprise/6/6.3/topics/cm_ig_mysql.html#cmig_topic_5_5

#Creating SSH to login from windows into linux server without password using putty-ssh
https://www.howtoforge.com/how-to-configure-ssh-keys-authentication-with-putty-and-linux-server-in-5-quick-steps

# Steps how to install Cloudera in CeontOS
https://www.tecmint.com/best-practices-for-deploying-hadoop-server-on-centos/

#Generate RootCACert.pem RootCAKey.pem follow this instruction
https://www.ibm.com/docs/en/runbook-automation?topic=certificate-generate-root-ca-key

#To install TSL/SSL in Cloudera for security messures follow this instruction
https://docs.cloudera.com/documentation/enterprise/6/6.2/topics/sg_add_root_ca_explicit_trust.html

create this directory /opt/cloudera/security/pki/
download install oracle-jdk.18
wget http://ro-bucharest-repo.bigstepcloud.com/cloudera-repos/cm6/redhat/7/x86_64/cm/6.2.0/RPMS/x86_64/oracle-j2sdk1.8-1.8.0%2Bupdate181-1.x86_64.rpm

#How to secure Cloudera
openssl genrsa -out rootCAKey.pem 2048
openssl req -x509 -sha256 -new -nodes -key rootCAKey.pem -days 3650 -out rootCACert.pem
openssl x509 -in rootCACert.pem -text

mkdir /opt
mkdir /opt/cloudera/security/
mkdir /opt/cloudera/security/pki
mkdir /jre
mkdir /jre/lib/
mkdir /jre/lib/security/
cp  root* /opt/cloudera/security/pki/

sudo keytool -importcert -alias rootca -keystore $JAVA_HOME/jre/lib/security/jssecacerts \
-file /opt/cloudera/security/pki/rootCACert.pem -storepass markv109

sudo cat /opt/cloudera/security/pki/rootCACert.pem >> \
/opt/cloudera/security/pki/$(hostname -f)-server.cert.pem

#How to download/install/configure mysql
yum install mysql-server
systemctl enable mysqld
systemctl start mysqld
/usr/bin/mysql_secure_installation


wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
sudo yum update -y
sudo yum install -y mysql-server
sudo systemctl start mysqld
/usr/bin/mysql_secure_installation





#Create databases for standard for service

create database rmon DEFAULT CHARACTER SET utf8;
create database hive DEFAULT CHARACTER SET utf8;
create database sentry DEFAULT CHARACTER SET utf8;
create database nav DEFAULT CHARACTER SET utf8;
create database navms DEFAULT CHARACTER SET utf8;
create database hue DEFAULT CHARACTER SET utf8;
create database clouderascm DEFAULT CHARACTER SET utf8;

#Create a database users and passwords.

grant all on bigdata.* TO 'rmon'@'%' IDENTIFIED BY 'markv109';
grant all on rmon.* TO 'rmon'@'%' IDENTIFIED BY 'markv109';
grant all on hive.* TO 'hive'@'%' IDENTIFIED BY 'markv109';
grant all on sentry.* TO 'sentry'@'%' IDENTIFIED BY 'markv109';
grant all on nav.* TO 'nav'@'%' IDENTIFIED BY 'markv109';
grant all on navms.* TO 'navms'@'%' IDENTIFIED BY 'markv109';
grant all on hue.* TO 'hue'@'%' IDENTIFIED BY 'markv109';
grant all on clouderascm.* TO 'clouderascm'@'%' IDENTIFIED BY 'markv109';


#create database oozie default character set utf8;
grant all privileges on oozie.* to 'oozie'@'localhost' identified by 'markv109';
grant all privileges on oozie.* to 'oozie'@'%' identified by 'markv109';

Ports need to be in in fre
7180,9864,7183,7187,7183,8020,50010,10110,10111,7182,7432,7190, 7191,9000,7184,7185, 8084, 10101, 8086, 9997, 9996, 8087, 9999, 9998, 8091, 9091, 9995, 9994, 5678, 8083, 7186, 8089
###############################################################################################
##################################################################################################################################
RHEL howto's

#EPEL For RHEL	
dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm

How to enable systemd on WSL2: Ubuntu 20 and CentOS 8
https://www.javaer101.com/en/article/11055970.html

Installating GNOME for RHEL
yum group install GNOME base-x -y

subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms
yum install xorg-x11-apps -y

https://packages.microsoft.com/config/rhel/8/
https://packages.microsoft.com/config/centos/8/

#How to install VNC Server
https://www.tecmint.com/install-vnc-server-on-rhel-8/


#To run the guiG
systemctl set-default graphical.target


rpm -i https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm
wsl -d genie -s #running the RHWSL sysmtemd on #drawbacks are you cannot update


How to Fix “Failed to set locale, defaulting to C.UTF-8”
https://www.tecmint.com/fix-failed-to-set-locale-defaulting-to-c-utf-8-in-centos/

dnf install @postgresql -y
dnf install langpacks-en glibc-all-langpacks -y
dnf install glibc-langpack-en


#If registration is getting error
# subscription-manager refresh
# subscription-manager attach --auto
# subscription-manager status

# subscription-manager remove --all
# subscription-manager unregister
# subscription-manager clean

#Try again
# subscription-manager register
# subscription-manager attach --auto

#EPEL-Release for RHEL
yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm


#VNC Files download ang install all, with --skip-broken paramater
https://homes.esat.kuleuven.be/~rtheys/vnc/

#how to install VNC in IBM
https://www.ibm.com/support/pages/how-configure-vnc-server-red-hat-enterprise-linux-8

#Download the old TigerVNC from the link

wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-1.11.0-5.el8.esat~esat1.src.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-icons-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-license-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-selinux-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-minimal-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-module-1.11.0-5.el8.esat~esat1.x86_64.rpm



#Step by step to install VNC working in working in RHWSL8 
yum install -y \
tigervnc-1.11.0-5.el8.esat~esat1.src.rpm \
tigervnc-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-icons-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-license-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-selinux-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-server-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-server-minimal-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-server-module-1.11.0-5.el8.esat~esat1.x86_64.rpm \
--skip-broken  


#Creat vncuser
su - noknok
vncpasswd

#Crete a service connection for VNC for OLD Style
cp /usr/lib/systemd/system/vncserver\@.service /etc/systemd/system/vncserver\@:1.service \
cp /usr/lib/systemd/system/vncserver\@.service /etc/systemd/system/vncserver\@:2.service \
cp /usr/lib/systemd/system/vncserver\@.service /etc/systemd/system/vncserver\@:3.service
vi /etc/systemd/system/vncserver@:3.service

#For latest VNC server
cp /usr/lib/systemd/system/vncserver\@.service /etc/systemd/system/vncserver\@.service
vi /etc/systemd/system/vncserver@.service
systemctl daemon-reload

systemctl start vncserver@:1
systemctl start vncserver@:2
systemctl start vncserver@:3

#Copy this configuration 
[Service]
Type=forking
ExecStart=/usr/sbin/runuser -l noknok -c "/usr/bin/vncserver %i -geometry 1366x768"
PIDFile=/home/noknok/.vnc/%H%i.pid
#ExecStart=/usr/libexec/vncsession-start %i
#PIDFile=/run/vncsession-%i.pid
SELinuxContext=system_u:system_r:vnc_session_t:s0

#Restart daemon, so the configuration will take effect
systemctl daemon-reload

#Create start-up in the service
systemctl enable vncserver@:3.service
systemctl start vncserver@:3.service


#Before install nomachine
systemctl unmask systemd-logind


#No Machine  EnableUserDB and EnablePasswordDB to 1 then
vi /usr/NX/etc/server.cfg
sudo /etc/NX/nxserver --useradd mark --system
sudo /etc/NX/nxserver --passwd <username>

#Firewalld
/etc/firewalld/firewalld.conf
firewall-cmd --zone=public --permanent --add-service=http
firewall-cmd --zone=public --permanent --add-port=7180/tcp
firewall-cmd --zone=public --permanent --add-port=7181/tcp
firewall-cmd --zone=public --permanent --add-port=7182/tcp
firewall-cmd --reload


#How to install mysql-workbench in mysql repo
wget https://dev.mysql.com/get/mysql80-community-release-el8-1.noarch.rpm
sudo rpm -Uvh mysql80-community-release-el8-1.noarch.rpm
sudo yum update -y
sudo yum install -y mysql-workbench-community



#How to install Mysql-Workbench in RHEL via snapd
https://snapcraft.io/install/mysql-workbench-community/rhel

sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf -y upgrade
sudo subscription-manager repos --enable "rhel-*-optional-rpms" --enable "rhel-*-extras-rpms"
sudo yum install -y snapd
sudo systemctl enable --now snapd.socket
sudo ln -s /var/lib/snapd/snap /snap
sudo snap install mysql-workbench-community

#How to install setup Postgresql
https://www.cyberciti.biz/faq/install-and-setup-postgresql-on-rhel-8/
sudo yum module list | grep postgresql
sudo yum install -y @postgresql:10
sudo postgresql-setup --initdb
sudo passwd postgres
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo -i -u postgres
psql -U posgres flights

vi /var/lib/pgsql/10/data/pg_hba.conf

host    all             all             127.0.0.1/32            trust
host    all             all             ::1/128                 trust

#How to install pgadmin4-web
https://www.pgadmin.org/download/pgadmin-4-rpm/
sudo rpm -i https://ftp.postgresql.org/pub/pgadmin/pgadmin4/yum/pgadmin4-redhat-repo-1-1.noarch.rpm
sudo yum install -y pgadmin4-web
sudo /usr/pgadmin4/bin/setup-web.sh
sudo rpm -e pgadmin4-redhat-repo


#How to install phpMyAdmin in RHEL
https://www.itzgeek.com/how-tos/linux/centos-how-tos/how-to-install-phpmyadmin-on-rhel-8.html

yum install -y php-json php-mbstring \
yum install -y wget php php-pdo php-pecl-zip php-json php-common php-fpm php-mbstring php-cli php-mysqlnd

wget https://files.phpmyadmin.net/phpMyAdmin/4.9.1/phpMyAdmin-4.9.1-all-languages.tar.gz
tar -zxvf phpMyAdmin-4.9.1-all-languages.tar.gz
mv phpMyAdmin-4.9.1-all-languages /usr/share/phpMyAdmin

cp -pr /usr/share/phpMyAdmin/config.sample.inc.php /usr/share/phpMyAdmin/config.inc.php
vi /usr/share/phpMyAdmin/config.inc.php

mysql -u root -p mysql < /usr/share/phpMyAdmin/sql/create_tables.sql

vi /etc/httpd/conf.d/phpMyAdmin.conf

Alias /phpMyAdmin /usr/share/phpMyAdmin
Alias /phpmyadmin /usr/share/phpMyAdmin

<Directory /usr/share/phpMyAdmin/>
   AddDefaultCharset UTF-8

   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny> 
      Require all granted
     </RequireAny>
   </IfModule>
   <IfModule !mod_authz_core.c>
     # Apache 2.2
     Order Deny,Allow
     Deny from All
     Allow from 127.0.0.1
     Allow from ::1
   </IfModule>
</Directory>

<Directory /usr/share/phpMyAdmin/setup/>
   <IfModule mod_authz_core.c>
     # Apache 2.4
     <RequireAny>
       Require all granted
     </RequireAny>
   </IfModule>
   <IfModule !mod_authz_core.c>
     # Apache 2.2
     Order Deny,Allow
     Deny from All
     Allow from 127.0.0.1
     Allow from ::1
   </IfModule>
</Directory>


mkdir /usr/share/phpMyAdmin/tmp
chmod 777 /usr/share/phpMyAdmin/tmp

chown -R apache:apache /usr/share/phpMyAdmin
systemctl restart httpd

http://localhost/phpMyAdmin

############################################################################
How to create database in Postgre, outside the post postgre console
############################################################################
createdb --username=postgres --host=localhost --password sakila
pg_restore --username=postgres --host=localhost --password --dbname=sakila < sakila_pgsql_dump.tar
pg_dump --username=postgres --host=localhost --password --dbname=sakila --table=store --format=plain > sakila_store_pgsql_dump.sql

pg_restore --username=postgres --host=localhost --password --dbname=sakila < sakila_pgsql_dump.tar


postgres=# \connect sakila;
\include sakila_pgsql_dump.sql;





############################################################################
How to install RHEL 8 in WSL2 with GNOME via VNC Client
############################################################################
Google "RHWSL8 github"
wsl -s RHWSL8 --version 2
wsl -d RHWSL8 genie -s
#Login your RHEL credential#
--
yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

yum remove -y firewalld
sudo systemctl mask --now firewalld

yum remove -y iptables
sudo systemctl mask --now iptables

yum group install GNOME base-x -y
systemctl unmask systemd-logind

#Download the old TigerVNC from the link, 
#Installation of old version of TigerVNC

wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-1.11.0-5.el8.esat~esat1.src.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-icons-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-license-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-selinux-1.11.0-5.el8.esat~esat1.noarch.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-minimal-1.11.0-5.el8.esat~esat1.x86_64.rpm \
wget https://homes.esat.kuleuven.be/~rtheys/vnc/tigervnc-server-module-1.11.0-5.el8.esat~esat1.x86_64.rpm



#Step by step to install VNC working in working in RHWSL8 
yum install -y \
tigervnc-1.11.0-5.el8.esat~esat1.src.rpm \
tigervnc-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-icons-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-license-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-selinux-1.11.0-5.el8.esat~esat1.noarch.rpm \
tigervnc-server-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-server-minimal-1.11.0-5.el8.esat~esat1.x86_64.rpm \
tigervnc-server-module-1.11.0-5.el8.esat~esat1.x86_64.rpm \
--skip-broken  

#Creat vncuser
su - noknok
vncpasswd

#For latest VNC server
cp /usr/lib/systemd/system/vncserver\@.service /etc/systemd/system/vncserver\@.service
vi /etc/systemd/system/vncserver@.service

#Copy this configuration 
[Service]
Type=forking
ExecStart=/usr/sbin/runuser -l noknok -c "/usr/bin/vncserver %i -geometry 1366x768"
PIDFile=/home/noknok/.vnc/%H%i.pid
#ExecStart=/usr/libexec/vncsession-start %i
#PIDFile=/run/vncsession-%i.pid
SELinuxContext=system_u:system_r:vnc_session_t:s0

#Restart daemon, so the configuration will take effect
systemctl unmask systemd-logind
systemctl daemon-reload

systemctl start vncserver@:1
systemctl enable vncserver@:1
systemctl status vncserver@:1


#Installation of NXServer
Download NXServer in the website.
nomachine_7.4.1_1_x86_64.rpm

#Before installing nomachine
systemctl unmask systemd-logind

rpm -i nomachine_7.4.1_1_x86_64.rpm

#Check the listening port
netstat -tulpn |grep LISTEN

#Here's the weird part, restart the VNC Service.

systemctl restart vncserver@:1

#It will occur errro, but you can login to GNOMO gui via VNC Client localhost:5901
#or your live ip address with 172.x.x.x

viola, full RED HAT Enterpise Linux without Virtual Machine App.


######################################
#IP Tables
sudo iptables -L
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
service iptables save

systemctl stop firewalld
systemctl disable  firewalld
systemctl start iptables
systemctl status iptables
systemctl enable iptables

sudo iptables-save > /etc/sysconfig/iptables

sudo service iptables save

#File transfer in LINUX using scp

scp user@ip:<source_folder>/<file/s> <destination> 

######################################
Coursera:
######################################
#how to extract database in Hive
https://medium.com/analytics-vidhya/best-way-to-export-hive-table-to-csv-file-326063f0f229
https://stackoverflow.com/questions/17086642/how-to-export-a-hive-table-into-a-csv-file


#Dumping Database in mysql
mysqldump -u root -p <database> > filename.sql

#Restoring Dataase in mysql
mysqldump -u root -p <created database> < filename.sql


Importing csv into mysql
https://www.coursera.org/learn/introduction-to-relational-databases/lecture/seo5u/loading-data-in-mysql

#Sample Database
https://github.com/words-sdsc/coursera

https://community.ibm.com/community/user/businessanalytics/blogs/steven-macko/2019/07/12/beanie-coffee-1113

https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/CoffeeData/GeneratedScript.sql

https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/CoffeeData/CoffeeData.sql


wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/sakila/sakila_mysql_dump.sql \

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/sakila/sakila_pgsql_dump.sql \

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/eBooks/eBooks_mysql_dump.sql

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/sakila/sakila_pgsql_dump.tar \

wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/datasets/eBooks/eBooks_pgsql_dump.tar


hive -e 'set hive.cli.print.header=true; select * from fly.planes' | sed 's/[\t]/,/g'  > /home/fly.planes.csv
hive -e 'set hive.cli.print.header=true; select * from fly.airlines' | sed 's/[\t]/,/g'  > /home/fly.airlines.csv

hive -e 'set hive.cli.print.header=true; select * from your_Table' | sed 's/[\t]/,/g'  > /home/yourfile.csv
hive -e 'set hive.cli.print.header=true; select * from your_Table' | sed 's/[\t]/,/g'  > /home/yourfile.csv

hadoop fs -cat hdfs://servername/user/hive/warehouse/databasename/table_csv_export_data/* > ~/output.csvCopy

#how to upgrade from CentOS6 into CentOS7
https://itbeginner.net/upgrade-centos-6-7.html


[upg]
name=CentOS-$releasever - Upgrade Tool
baseurl=https://buildlogs.centos.org/centos/6/upg/x86_64/
gpgcheck=1
enabled=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6


######################################################################
exporting, importing, creating tables from hive database.
https://www.convertcsv.com/csv-to-sql.htm

adjustment in php.ini restarting the httpd service
https://stackoverflow.com/questions/3958615/import-file-size-limit-in-phpmyadmin

how to import large csv via psql cli
su - postgres
psql -U posgres flights
psql -U postgres fly
first create tables in psql cli
COPY flights FROM '/mnt/c/RHWSL8/flights.csv' delimiter ',' csv;
COPY flights FROM '/mnt/c/RHWSL8/hive-csv/fly.flights.csv' delimiter ',' csv;
\COPY flights FROM '/mnt/c/RHWSL8/hive-csv/fly.flights.csv' DELIMITER ',' CSV HEADER;

#Display and delete the last line of a file
tail -n 1 "$file" | tee >(wc -c | xargs -I {} truncate "$file" -s -{})

######################################################################
4 left join querry, 4 table query, in fly database

select r.carrier as Carriers, origin as Origin, p.name as Origin_Airport, f.dest, d.name as Destination_Airport, l.manufacturer as Manufacturer, f.tailnum as TailNum 
from 
airports as p 
join flights as f on p.faa = f.origin 
join airports as d on d.faa = f.dest 
join planes as l on l.tailnum = f.tailnum
join airlines as r on r.carrier = f.carrier
where (f.origin = 'LAX' or f.dest = 'LAX') and (f.origin = 'SFO' or f.dest = 'SFO') 
group by f.tailnum, f.origin, p.name, f.dest, d.name, l.tailnum, l.manufacturer, r.carrier;


######################################################################

######################################################################
create database fly;
use fly;

CREATE TABLE planes(
   tailnum      VARCHAR(10) NOT NULL
  ,year         VARCHAR(6) Default NULL
  ,type         VARCHAR(30) Default NULL
  ,manufacturer VARCHAR(30) Default NULL
  ,model        VARCHAR(30) Default NULL
  ,engines      INTEGER  Default NULL
  ,seats        INTEGER  Default NULL
  ,engine       VARCHAR(20) Default NULL
);


CREATE TABLE flights(
   year           INTEGER  NOT NULL  
  ,month          VARCHAR(8)  DEFAULT NULL
  ,day            VARCHAR(8)  DEFAULT NULL
  ,dep_time       VARCHAR(8)  DEFAULT NULL
  ,sched_dep_time VARCHAR(8)  DEFAULT NULL
  ,dep_delay      VARCHAR(8)  DEFAULT NULL
  ,arr_time       VARCHAR(8)  DEFAULT NULL
  ,sched_arr_time VARCHAR(8)  DEFAULT NULL
  ,arr_delay      VARCHAR(8)  DEFAULT NULL
  ,carrier        VARCHAR(6) DEFAULT NULL
  ,flight         VARCHAR(8)  DEFAULT NULL
  ,tailnum        VARCHAR(6) DEFAULT NULL
  ,origin         VARCHAR(6) DEFAULT NULL
  ,dest           VARCHAR(6) DEFAULT NULL
  ,air_time       VARCHAR(8)  DEFAULT NULL
  ,distance       VARCHAR(8)  DEFAULT NULL
);

CREATE TABLE airlines(
   carrier VARCHAR(2) NOT NULL 
  ,name    VARCHAR(27) DEFAULT NULL
);

CREATE TABLE airports(
   faa  VARCHAR(3) NOT NULL 
  ,name VARCHAR(60) DEFAULT NULL
  ,lat  VARCHAR(18) DEFAULT NULL
  ,lon  VARCHAR(19) DEFAULT NULL
  ,alt  INTEGER  DEFAULT NULL
  ,tz   VARCHAR(8)  DEFAULT NULL
);

===========================================

Query: describe customers
+---------+--------+---------+
| name    | type   | comment |
+---------+--------+---------+
| cust_id | string |         |
| name    | string |         |
| country | string |         |
+---------+--------+---------+
Fetched 3 row(s) in 6.52s


Query: describe employees
+------------+--------+---------+
| name       | type   | comment |
+------------+--------+---------+
| empl_id    | int    |         |
| first_name | string |         |
| last_name  | string |         |
| salary     | int    |         |
| office_id  | string |         |
+------------+--------+---------+

Query: describe offices
+----------------+--------+---------+
| name           | type   | comment |
+----------------+--------+---------+
| office_id      | string |         |
| city           | string |         |
| state_province | string |         |
| country        | string |         |
+----------------+--------+---------+




Query: describe orders
+----------+--------------+---------+
| name     | type         | comment |
+----------+--------------+---------+
| order_id | int          |         |
| cust_id  | string       |         |
| empl_id  | int          |         |
| total    | decimal(5,2) |         |
+----------+--------------+---------+

Query: describe salary_grades
+------------+---------+---------+
| name       | type    | comment |
+------------+---------+---------+
| grade      |  |         |
| min_salary | int     |         |
| max_salary | int     |         |
+------------+---------+---------+

Query: describe card_rank
+-------+---------+---------+
| name  | type    | comment |
+-------+---------+---------+
| rank  | string  |         |
| value | tinyint |         |
+-------+---------+---------+


Query: describe card_suit
+-------+--------+---------+
| name  | type   | comment |
+-------+--------+---------+
| suit  | string |         |
| color | string |         |
+-------+--------+---------+


Query: describe games
+-------------+--------------+---------+
| name        | type         | comment |
+-------------+--------------+---------+
| id          | int          |         |
| name        | string       |         |
| inventor    | string       |         |
| year        | string       |         |
| min_age     | tinyint      |         |
| min_players | tinyint      |         |
| max_players | tinyint      |         |
| list_price  | decimal(5,2) |         |
+-------------+--------------+---------+


Query: describe inventory
+-------+--------------+---------+
| name  | type         | comment |
+-------+--------------+---------+
| shop  | string       |         |
| game  | string       |         |
| qty   | int          |         |
| aisle | tinyint      |         |
| price | decimal(5,2) |         |
+-------+--------------+---------+
Fetched 5 row(s) in 2.90s


Query: describe makers
+------+--------+---------+
| name | type   | comment |
+------+--------+---------+
| id   | int    |         |
| name | string |         |
| city | string |         |
+------+--------+---------+

Query: describe toys
+----------+--------------+---------+
| name     | type         | comment |
+----------+--------------+---------+
| id       | int          |         |
| name     | string       |         |
| price    | decimal(5,2) |         |
| maker_id | int          |         |
+----------+--------------+---------+
#############################################################################################
ALTER TABLE tablename SET TBLPROPERTIES ("skip.header.line.count"="1");


CREATE TABLE airlines(
   carrier string
  ,name    string
);
LOAD DATA INPATH '/user/hive/warehouse/fly.airlines.csv' INTO TABLE fly.airlines;


CREATE TABLE airports(
   faa  char(3) 
  ,name string 
  ,lat  double
  ,lon  double
  ,alt  smallint
  ,tz   smallint
);
LOAD DATA INPATH '/user/hive/warehouse/fly.airports.csv' INTO TABLE fly.airports;


CREATE TABLE flights(
   year           smallint   
  ,month          tinyint
  ,day            tinyint
  ,dep_time       smallint
  ,sched_dep_time smallint
  ,dep_delay      smallint
  ,arr_time       smallint
  ,sched_arr_time smallint
  ,arr_delay      smallint
  ,carrier        string 
  ,flight         smallint 
  ,tailnum        string 
  ,origin         string 
  ,dest           string 
  ,air_time       smallint
  ,distance       smallint
);
LOAD DATA INPATH '/user/hive/warehouse/fly.flights.csv' INTO TABLE fly.flights;

CREATE TABLE planes(
   tailnum       string
   ,year         int
   ,type         string
   ,manufacturer string
   ,model        string
   ,engines      INT
   ,seats        INT
   ,engine       string
);
LOAD DATA INPATH '/user/hive/warehouse/fly.planes.csv' INTO TABLE fly.planes;



#############################################################################################
create database default1;
use default1;

CREATE TABLE customers(
   cust_id string 
  ,name    string 
  ,country string 
);
LOAD DATA INPATH '/user/hive/warehouse/default.customers.csv' INTO TABLE default.customers;

CREATE TABLE employees(
   empl_id    int    
  ,first_name string 
  ,last_name  string 
  ,salary     int    
  ,office_id  string 
);
LOAD DATA INPATH '/user/hive/warehouse/default.employees.csv' INTO TABLE default.employees;


CREATE TABLE offices(
   office_id      string 
  ,city           string 
  ,state_province string 
  ,country        string 
);
LOAD DATA INPATH '/user/hive/warehouse/default.offices.csv' INTO TABLE default.offices;

CREATE TABLE orders(
   order_id int          
  ,cust_id  string       
  ,empl_id  int          
  ,total    decimal(5,2)
);
LOAD DATA INPATH '/user/hive/warehouse/default.orders.csv' INTO TABLE default.orders;

CREATE TABLE salary_grades(
   grade      tinyint
  ,min_salary int 
  ,max_salary int 
);
LOAD DATA INPATH '/user/hive/warehouse/default.salary_grades.csv' INTO TABLE default.salary_grades;


#############################################################################################
create database toy;

CREATE TABLE card_rank(
   rank  string  
  ,value tinyint 
);

CREATE TABLE card_suit(
   suit  string 
  ,color string 
);
LOAD DATA INPATH '/user/hive/warehouse/fun.card_rank.csv' INTO TABLE fun.card_rank;


#############################################################################################
create database fun;
CREATE TABLE games(
   id          int          
  ,name        string
  ,inventor    string
  ,year        string
  ,min_age     tinyint
  ,min_players tinyint
  ,max_players tinyint
  ,list_price  decimal(5,2)
);
LOAD DATA INPATH '/user/hive/warehouse/fun.games.csv' INTO TABLE fun.games;


CREATE TABLE inventory(
   shop  string        
  ,game  string       
  ,qty   int          
  ,aisle tinyint      
  ,price decimal(5,2)
);
LOAD DATA INPATH '/user/hive/warehouse/fun.inventory.csv' INTO TABLE fun.inventory;


CREATE TABLE makers(
   id   int    
  ,name string 
  ,city string 
  ,zip  int
);
LOAD DATA INPATH '/user/hive/warehouse/toy.makers.csv' INTO TABLE toy.makers;


CREATE TABLE toys(
   id       int          
  ,name     string       
  ,price    decimal(5,2)
  ,maker_id int          
);
LOAD DATA INPATH '/user/hive/warehouse/toy.toys.csv' INTO TABLE toy.toys;


#############################################################################################
create database wax;

CREATE TABLE crayons(
   color varchar(25)
  ,hex   char(6)
  ,red   smallint 
  ,green smallint 
  ,blue  smallint 
  ,pack  tinyint 
);
LOAD DATA INPATH '/user/hive/warehouse/wax.crayons.csv' INTO TABLE wax.crayons;


#############################################################################################

============================================
create database flights;
use flights

CREATE TABLE flights(
   YEAR                INTEGER  NOT NULL
  ,MONTH               INTEGER  DEFAULT NULL
  ,DAY                 INTEGER  DEFAULT NULL
  ,DAY_OF_WEEK         INTEGER  DEFAULT NULL
  ,AIRLINE             VARCHAR(8) DEFAULT NULL
  ,FLIGHT_NUMBER       INTEGER  DEFAULT NULL
  ,TAIL_NUMBER         VARCHAR(8) DEFAULT NULL
  ,ORIGIN_AIRPORT      VARCHAR(8) DEFAULT NULL
  ,DESTINATION_AIRPORT VARCHAR(8) DEFAULT NULL
  ,SCHEDULED_DEPARTURE INTEGER  DEFAULT NULL
  ,DEPARTURE_TIME      INTEGER  DEFAULT NULL
  ,DEPARTURE_DELAY     INTEGER  DEFAULT NULL
  ,TAXI_OUT            INTEGER  DEFAULT NULL
  ,WHEELS_OFF          INTEGER  DEFAULT NULL
  ,SCHEDULED_TIME      INTEGER  DEFAULT NULL
  ,ELAPSED_TIME        INTEGER  DEFAULT NULL
  ,AIR_TIME            INTEGER  DEFAULT NULL
  ,DISTANCE            INTEGER  DEFAULT NULL
  ,WHEELS_ON           INTEGER  DEFAULT NULL
  ,TAXI_IN             INTEGER  DEFAULT NULL
  ,SCHEDULED_ARRIVAL   INTEGER  DEFAULT NULL
  ,ARRIVAL_TIME        INTEGER  DEFAULT NULL
  ,ARRIVAL_DELAY       INTEGER  DEFAULT NULL
  ,DIVERTED            INTEGER  DEFAULT NULL
  ,CANCELLED           INTEGER  DEFAULT NULL
  ,CANCELLATION_REASON VARCHAR(30) DEFAULT NULL
  ,AIR_SYSTEM_DELAY    VARCHAR(30) DEFAULT NULL
  ,SECURITY_DELAY      VARCHAR(30) DEFAULT NULL
  ,AIRLINE_DELAY       VARCHAR(30) DEFAULT NULL
  ,LATE_AIRCRAFT_DELAY VARCHAR(30) DEFAULT NULL
  ,WEATHER_DELAY       VARCHAR(30) DEFAULT NULL
);

INSERT INTO flights(flightsyear,flightsmonth,flightsday,flightsdep_time,flightssched_dep_time,flightsdep_delay,flightsarr_time,flightssched_arr_time,flightsarr_delay,flightscarrier,flightsflight,flightstailnum,flightsorigin,flightsdest,flightsair_time,flightsdistance) VALUES (2013,3,31,NULL,1828,NULL,NULL,1913,NULL,OO,5306,N233SW,LAX,CLD,NULL,86);

2013,3,31,NULL,1828,NULL,NULL,1913,NULL,OO,5306,N233SW,LAX,CLD,NULL,86


Query: describe flights
+----------------+----------+---------+
| name           | type     | comment |
+----------------+----------+---------+
| year           | smallint |         |
| month          | tinyint  |         |
| day            | tinyint  |         |
| dep_time       | smallint |         |
| sched_dep_time | smallint |         |
| dep_delay      | smallint |         |
| arr_time       | smallint |         |
| sched_arr_time | smallint |         |
| arr_delay      | smallint |         |
| carrier        | string   |         |
| flight         | smallint |         |
| tailnum        | string   |         |
| origin         | string   |         |
| dest           | string   |         |
| air_time       | smallint |         |
| distance       | smallint |         |
+----------------+----------+---------+

Query: describe airlines
+---------+--------+---------+
| name    | type   | comment |
+---------+--------+---------+
| carrier | string |         |
| name    | string |         |
+---------+--------+---------+

Query: describe airports
+------+----------+---------+
| name | type     | comment |
+------+----------+---------+
| faa  | char(3)  |         |
| name | string   |         |
| lat  | double   |         |
| lon  | double   |         |
| alt  | smallint |         |
| tz   | tinyint  |         |
+------+----------+---------+

Query: describe planes
+--------------+--------+-------------------+
| name         | type   | comment           |
+--------------+--------+-------------------+
| tailnum      | string | from deserializer |
| year         | int    | from deserializer |
| type         | string | from deserializer |
| manufacturer | string | from deserializer |
| model        | string | from deserializer |
| engines      | int    | from deserializer |
| seats        | int    | from deserializer |
| engine       | string | from deserializer |
+--------------+--------+-------------------+
Fetched 8 row(s) in 11.09s

Query: describe customers
+---------+--------+---------+
| name    | type   | comment |
+---------+--------+---------+
| cust_id | string |         |
| name    | string |         |
| country | string |         |
+---------+--------+---------+
Fetched 3 row(s) in 6.52s

Query: describe employees
+------------+--------+---------+
| name       | type   | comment |
+------------+--------+---------+
| empl_id    | int    |         |
| first_name | string |         |
| last_name  | string |         |
| salary     | int    |         |
| office_id  | string |         |
+------------+--------+---------+

Query: describe offices
+----------------+--------+---------+
| name           | type   | comment |
+----------------+--------+---------+
| office_id      | string |         |
| city           | string |         |
| state_province | string |         |
| country        | string |         |
+----------------+--------+---------+

Query: describe orders
+----------+--------------+---------+
| name     | type         | comment |
+----------+--------------+---------+
| order_id | int          |         |
| cust_id  | string       |         |
| empl_id  | int          |         |
| total    | decimal(5,2) |         |
+----------+--------------+---------+

Query: describe salary_grades
+------------+---------+---------+
| name       | type    | comment |
+------------+---------+---------+
| grade      | tinyint |         |
| min_salary | int     |         |
| max_salary | int     |         |
+------------+---------+---------+

Query: describe card_rank
+-------+---------+---------+
| name  | type    | comment |
+-------+---------+---------+
| rank  | string  |         |
| value | tinyint |         |
+-------+---------+---------+

Query: describe card_suit
+-------+--------+---------+
| name  | type   | comment |
+-------+--------+---------+
| suit  | string |         |
| color | string |         |
+-------+--------+---------+

Query: describe games
+-------------+--------------+---------+
| name        | type         | comment |
+-------------+--------------+---------+
| id          | int          |         |
| name        | string       |         |
| inventor    | string       |         |
| year        | string       |         |
| min_age     | tinyint      |         |
| min_players | tinyint      |         |
| max_players | tinyint      |         |
| list_price  | decimal(5,2) |         |
+-------------+--------------+---------+

Query: describe inventory
+-------+--------------+---------+
| name  | type         | comment |
+-------+--------------+---------+
| shop  | string       |         |
| game  | string       |         |
| qty   | int          |         |
| aisle | tinyint      |         |
| price | decimal(5,2) |         |
+-------+--------------+---------+
Fetched 5 row(s) in 2.90s

Query: describe makers
+------+--------+---------+
| name | type   | comment |
+------+--------+---------+
| id   | int    |         |
| name | string |         |
| city | string |         |
+------+--------+---------+

Query: describe toys
+----------+--------------+---------+
| name     | type         | comment |
+----------+--------------+---------+
| id       | int          |         |
| name     | string       |         |
| price    | decimal(5,2) |         |
| maker_id | int          |         |
+----------+--------------+---------+

Query: describe crayons
+-------+-------------+---------+
| name  | type        | comment |
+-------+-------------+---------+
| color | varchar(25) |         |
| hex   | char(6)     |         |
| red   | smallint    |         |
| green | smallint    |         |
| blue  | smallint    |         |
| pack  | tinyint     |         |
+-------+-------------+---------+

############################################################
SAMPLE join queries, 4 tables is being join
############################################################
select r.carrier as Carriers, origin as Origin, p.name as Origin_Airport, f.dest, d.name as Destination_Airport, l.manufacturer as Manufacturer, f.tailnum as TailNum 
from 
airports as p 
join flights as f on p.faa = f.origin 
join airports as d on d.faa = f.dest 
join planes as l on l.tailnum = f.tailnum
join airlines as r on r.carrier = f.carrier
where (f.origin = 'LAX' or f.dest = 'LAX') and (f.origin = 'SFO' or f.dest = 'SFO') 
group by f.tailnum, f.origin, p.name, f.dest, d.name, l.tailnum, l.manufacturer, r.carrier

#############################################################
Basic Hadoop command
#############################################################

hadoop fs -ls -R / | grep "^d"
hdfs dfs -ls hdfs:/
hdfs dfs -put *.csv hdfs:///user/hive/warehouse

#Import csv into hive 
LOAD DATA INPATH '/user/hive/warehouse/fly.planes.csv' INTO TABLE fly.planes;



LOAD DATA INPATH '/user/hive/data/data.csv' INTO TABLE emp.employee;

#############################################################
How to create RHEL in WSL2
#############################################################

https://www.lennysh.com/rhel-w10-with-wsl2/
wsl.exe --import RHEL7 c:\RH79 rhel7.9.tar.gz --version 2
wsl.exe --import RHEL7 c:\RH79 rhel7.9.tools.tar.gz --version 2
 wsl.exe --import centos C:\centos7wsl centos7.tar.gz --version 2

sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
sudo yum install -y dotnet-sdk-3.1 dotnet-sdk-5.0


Genie
https://github.com/arkane-systems/genie


files required


sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
sudo yum install -y dotnet-sdk-3.1 dotnet-sdk-5.0

systemd-containeer
https://download-ib01.fedoraproject.org/pub/fedora/linux/releases/32/Everything/x86_64/os/Packages/s/systemd-container-245.4-1.fc32.x86_64.rpm
https://repo.almalinux.org/almalinux/8.3-beta/BaseOS/x86_64/os/Packages/systemd-container-239-41.el8_3.1.x86_64.rpm

rpm -e --nodeps --justdb systemd-libs

genie 
https://github.com/arkane-systems/genie/releases/download/v1.42/genie-1.42-1.fc33.x86_64.rpm

Daemonize
https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/d/daemonize-1.7.7-1.el7.x86_64.rpm

https://wsl.dev/mobyrhel8/

rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm


CentOS 7 Systemd
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-208.20-6.el7.centos.src.rpm \
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-208.20-6.el7.centos.x86_64.rpm \
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-EOL-208.21-1.el7.noarch.rpm \
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-devel-208.20-6.el7.centos.x86_64.rpm \
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-libs-208.20-6.el7.centos.x86_64.rpm \
wget https://buildlogs.centos.org/centos/7/systemd-container/systemd-container-python-208.20-6.el7.centos.x86_64.rpm

Compiling
https://kennedy-han.github.io/2015/10/14/build-Systemd.html

#######################################################################################
Fixing set locale language
#######################################################################################
localectl set-locale LANG=en_US.UTF-8

#######################################################################################
how to fix missing repo
#######################################################################################

To attach the subscriptions execute the following commands :

sudo subscription-manager register
sudo subscription-manager refresh
sudo subscription-manager attach --auto

To enable additional repositories execute these commands :

sudo subscription-manager repos --enable rhel-7-server-extras-rpms
sudo subscription-manager repos --enable rhel-7-server-optional-rpms
sudo subscription-manager repos --enable rhel-server-rhscl-7-rpms

subscription-manager repos --enable rhel-7-server-rpms --enable rhel-7-server-extras-rpms  --enable rhel-7-server-optional-rpms --enable rhel-7-server-supplementary-rpms --enable rhel-7-server-rh-common-rpms


wsl -d <distro> genie -c bash

#########################################################################################
How to install genie in wsl / linux distro
#########################################################################################
wsl DOTNET_ROOT=/opt/dotnet/ genie -v -s
git clone https://github.com/arkane-systems/genie.git


how to update systemd
https://linoxide.com/install-systemd-centos-redhat/


#########################################################################################
CentOS7
#########################################################################################

"Unable to verify server's identity: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed "
vi /etc/rhsm/rhsm.conf
Set to 1 to disable certificate validation:

insecure = 1






















ROM gcc:latest AS builder

RUN curl -L https://github.com/bmc/daemonize/archive/release-1.7.8.tar.gz -o daemonize.tar.gz
RUN tar -xpf daemonize.tar.gz && cd daemonize-* && sh configure && make && make install

WORKDIR /tmp
RUN curl -L https://github.com/arkane-systems/genie/releases/download/1.27/systemd-genie_1.27_amd64.deb -o systemd-genie.deb
RUN ar x systemd-genie.deb data.tar.xz && mkdir -p systemd-genie && tar xpf data.tar.xz -C systemd-genie

curl -L https://github.com/arkane-systems/genie/releases/download/v1.42/systemd-genie_1.42_amd64.deb -o systemd-genie.deb



FROM archlinux:latest

WORKDIR /etc/pacman.d
RUN \
# echo 'Server = https://mirrors.tuna.tsinghua.edu.cn/archlinux/$repo/os/$arch' > mirrorlist && \
pacman -Sy --noconfirm --needed vim nano dotnet-runtime zsh grml-zsh-config && \
rm -f /var/lib/pacman/sync/* /var/cache/pacman/pkg/* && cp -f mirrorlist.pacnew mirrorlist

COPY --from=builder /usr/local/sbin/daemonize /usr/local/sbin/daemonize
COPY --from=builder /usr/local/share/man/man1/daemonize.1 /usr/local/share/man/man1/daemonize.1

COPY --from=builder /tmp/systemd-genie/etc /etc
COPY --from=builder /tmp/systemd-genie/usr /usr

COPY ./post-install.sh /root/post-install.sh

WORKDIR /usr/bin
RUN ln -sf vim vi

WORKDIR /root
RUN usermod -s /bin/zsh root && echo "bash -c 'source /root/post-install.sh'" >> .zshrc


 Microsoft.AspNetCore.App 3.1.7 [/usr/lib64/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 3.1.7 [/usr/lib64/dotnet/shared/Microsoft.NETCore.App]

how to complie systemd

https://www.linuxfromscratch.org/lfs/view/8.3-systemd/chapter06/systemd.html

https://www.linuxfromscratch.org/patches/downloads/systemd/

https://tutorialforlinux.com/2018/06/13/how-to-install-meson-centos-7-gnulinux-easy-guide/2/

rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
dnf install -y dotnet-sdk-3.1 dotnet-sdk-5.0


Make sure to edit /etc/selinux/config and put SELinux to permissive before you update, otherwise your system will not boot anymore!
# wget https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo -O /etc/yum.repos.d/jsynacek-systemd-centos-7.repo
# yum update -y systemd


timedatectl set-timezone America/New_York

how to upgrade glibc
https://unix.stackexchange.com/questions/176489/how-to-update-glibc-to-2-14-in-centos-6-5



rpm -Uvh --force http://mirror.centos.org/centos-7/7.9.2009/os/x86_64/Packages/centos-release-7-9.2009.0.el7.centos.x86_64.rpm

rpm -qlp http://mirror.centos.org/centos-7/7.9.2009/os/x86_64/Packages/centos-release-7-9.2009.0.el7.centos.x86_64.rpm 2>/dev/null | grep repo





wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64/dnf-conf-0.6.4-2.sdl7.noarch.rpm \
wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64//dnf-0.6.4-2.sdl7.noarch.rpm \
wget http://springdale.math.ias.edu/data/puias/unsupported/7/x86_64/python-dnf-0.6.4-2.sdl7.noarch.rpm \
yum install python-dnf-0.6.4-2.sdl7.noarch.rpm  dnf-0.6.4-2.sdl7.noarch.rpm dnf-conf-0.6.4-2.sdl7.noarch.rpm



wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-2.17-55.el6.x86_64.rpm
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-common-2.17-55.el6.x86_64.rpm
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-devel-2.17-55.el6.x86_64.rpm
wget http://copr-be.cloud.fedoraproject.org/results/mosquito/myrepo-el6/epel-6-x86_64/glibc-2.17-55.fc20/glibc-headers-2.17-55.el6.x86_64.rpm

sudo rpm -Uvh glibc-2.17-55.el6.x86_64.rpm \
glibc-common-2.17-55.el6.x86_64.rpm \
glibc-devel-2.17-55.el6.x86_64.rpm \
glibc-headers-2.17-55.el6.x86_64.rpm --force --nodeps


util-linux
https://github.com/karelzak/util-linux


util-linux-2.37-0.1.fc35.x86_64.rpm

ls -la /var/www/ | grep "\->"


# Just put the bits in the right places.
mkdir -p "/usr/local/libexec/genie"
# Binaries.
install -Dm 4755 -o root "binsrc/genie/bin/ReleaseLocal/net5.0/linux-x64/publish/genie" -t "/usr/local/libexec/genie"
install: failed to access ‘/usr/local/libexec/genie’: No such file or directory


compiling util-linux 2.34
https://noknow.info/it/os/install_util_linux_from_source?lang=en#sec4



https://www.thegeekstuff.com/2015/02/rpm-build-package-example/

7 Steps to Build a RPM Package from Source on CentOS / RedHat


rpmbuild -bb --define "_binary_filedigest_algorithm  1"  --define "_binary_payload 1" util-linux-2.36.2.spec
rpmbuild -ba util-linux.2.36.2.spec


├── 	
│   └── util-linux-2.36.2-0.x86_64
├── RPMS
│   └── x86_64
│       ├── util-linux-2.36.2-0.x86_64.rpm
│       └── util-linux-debuginfo-2.36.2-0.x86_64.rpm
├── SOURCES
│   └── v2.36.2.tar.gz
├── SPECS
│   └── util-linux-2.36.2.spec
└── SRPMS
    └── util-linux-2.36.2-0.src.rpm


how to comvert to RPM
https://www.tecmint.com/convert-from-rpm-to-deb-and-deb-to-rpm-package-using-alien/s

rpmrebuild –pe dateutils-0.3.1-2.1.x86_64.rpm 

Specs for 2.37
https://src.fedoraproject.org/rpms/util-linux/blob/rawhide/f/util-linux.spec

How to upgrade to the latest kernel
https://phoenixnap.com/kb/how-to-upgrade-kernel-centos
https://phoenixnap.com/kb/how-to-upgrade-kernel-centos

epel-release
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm


ELRepo
https://phoenixnap.com/kb/how-to-upgrade-kernel-centos
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

Make sure to edit /etc/selinux/config and put SELinux to permissive before you update, otherwise your system will not boot anymore!
# wget https://copr.fedorainfracloud.org/coprs/jsynacek/systemd-backports-for-centos-7/repo/epel-7/jsynacek-systemd-backports-for-centos-7-epel-7.repo -O /etc/yum.repos.d/jsynacek-systemd-centos-7.repo
# yum update -y systemd

Daemonize

http://download-ib01.fedoraproject.org/pub/epel/7/x86_64/
rpm -Uvh epel-release*rpm
yum install -y daemonize

sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
sudo yum install -y dotnet-sdk-3.1 dotnet-sdk-5.0

yum install -y https://download-ib01.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-13.noarch.rpm


● auditd.service               loaded failed failed Security Auditing Service
● systemd-modules-load.service loaded failed failed Load Kernel Modules
● multipathd.socket

rpmbuild of util-linux in CentOS, pre-requisites app

.NET Core runtimes installed:
  Microsoft.AspNetCore.App 3.1.15 [/usr/lib64/dotnet/shared/Microsoft.AspNetCore.App]
  Microsoft.NETCore.App 3.1.15 [/usr/lib64/dotnet/shared/Microsoft.NETCore.App]


############################################################################################
Pre-requsite for the compilation of util-linux
############################################################################################
required in every compile

to check mount version
pkg-config --modversion mount

get the source file of util-linux
https://mirrors.edge.kernel.org/pub/linux/utils/util-linux/v2.36/util-linux-2.36.2.tar.xz

rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install -y cargo
yum install -y wget mlocate

dnf install -y audit-libs-devel ncurses-devel  readline-devel pam-devel  zlib-devel  popt-devel libutempter-devel systemd-devel libuser-devel libcap-ng-devel  python3-devel  pcre2-devel rubygem-asciidoctor libselinux-devel

dnf install -y http://mirror.centos.org/centos/8/BaseOS/x86_64/os/Packages/audit-libs-devel-3.0-0.17.20191104git1c2f876.el8.x86_64.rpm
dnf install -y https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/ncurses-devel-6.1-7.20180224.el8.x86_64.rpm
dnf install -y https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/readline-devel-7.0-10.el8.x86_64.rpm
dnf install -y http://mirror.centos.org/centos/8/BaseOS/x86_64/os/Packages/pam-devel-1.3.1-14.el8.x86_64.rpm
dnf install -y http://mirror.centos.org/centos/8-stream/BaseOS/x86_64/os/Packages/popt-devel-1.18-1.el8.x86_64.rpm
dnf install -y https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/libutempter-devel-1.1.6-14.el8.x86_64.rpm
dnf install -y https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/libuser-devel-0.62-23.el8.x86_64.rpm
dnf install -y https://download.opensuse.org/repositories/home:/matthewdva:/rubygems/rb27_el8/noarch/rubygem-asciidoctor-1.5.6.1-0.12.71.el8.noarch.rpm

wget https://mirrors.edge.kernel.org/pub/linux/utils/util-linux/v2.36/util-linux-2.36.2.tar.xz
wget https://github.com/systemd/systemd-stable/archive/refs/tags/v248.3.tar.gz

subscription-manager repos --enable codeready-builder-for-rhel-7-x86_64-rpms

https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/



Problem encountered: POSIX caps headers not found
yum install -y libcap-devel

ERROR: Dependency "mount" not found, tried pkgconfig
yum install libmount-devel

############################################################################################
Pre-requsite for the compilation of systemd
############################################################################################
yum -y install https://harbottle.gitlab.io/harbottle-main/8/x86_64/harbottle-main-release.rpm
dnf --nogpg install https://mirror.ghettoforge.org/distributions/gf/gf-release-latest.gf.el8.noarch.rp

rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
yum install -y dnf mlocate
yum install -y podman wget daemonize
rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
yum install -y dotnet-sdk-3.1 dotnet-sdk-5.0
rm -rf /etc/yum.repos.d/microsoft-prod.repo
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
yum -y install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm
subscription-manager register
subscription-manager attach --auto


dnf install -y docker podman wget daemonize dotnet-sdk-3.1 dotnet-sdk-5.0

rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org

yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install -y dnf mlocate
yum install -y podman cargo wget dnf
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install -y docker wget dnf daemonize
rpm -Uvh https://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
yum-config-manager --enable cr -y
dnf makecache
yum makecache

subscription-manager repos --enable rhel-7-server-rpms --enable rhel-7-server-extras-rpms  --enable rhel-7-server-optional-rpms --enable rhel-7-server-supplementary-rpms --enable rhel-7-server-rh-common-rpms --enable rhel-7-server-devtools-rpms --enable rhel-7-server-eus-optional-rpms --enable rhel-7-server-eus-supplementary-rpms --enable rhel-7-server-optional-rpms --enable rhel-7-server-rhn-tools-rpms --enable rhel-7-server-thirdparty-oracle-java-rpms

rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
yum install -y dotnet-sdk-3.1 dotnet-sdk-5.0

wget https://mirrors.edge.kernel.org/pub/linux/utils/util-linux/v2.36/util-linux-2.36.2.tar.xz
wget https://github.com/systemd/systemd-stable/archive/refs/tags/v248.3.tar.gz


yum --nogpg install -y https://mirror.ghettoforge.org/distributions/gf/gf-release-latest.gf.el7.noarch.rpm
rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

yum -y install https://harbottle.gitlab.io/harbottle-main/7/x86_64/harbottle-main-release.rpm
yum install -y docker podman wget mlocate   cargo

yum update -y


dnf install -y audit-libs-devel bzip2-devel cryptsetup-devel dbus-devel docbook-style-xsl elfutils-devel gcc gcc-c++ gnu-efi gnu-efi-devel gnutls-devel gobject-introspection-devel gperf iptables-devel kmod-devel libacl-devel libblkid-devel libcap-devel libcurl-devel  libfdisk-devel  libgcrypt-devel libgpg-error-devel libidn2-devel libmicrohttpd-devel libmount-devel libpwquality-devel libseccomp-devel libselinux-devel libxkbcommon-devel libzstd-devel  lz4 lz4-devel meson openssl-devel pam-devel perl pkgconfig qrencode-devel valgrind-devel xz-devel  lz4-devel openssl-devel qrencode-devel pkgconfig libxslt python3 meson valgrind-devel libcap pkg-config gperf  python meson ninja glibc  libcap pkg-config gperf python-jinja2  python ninja

https://repo.cloudlinux.com/cloudlinux/8.1/BaseOS/x86_64/



https://github.com/arkane-systems/genie/issues/70


to compile systemd
dnf install -y meson gperf libmount-devel libcap-devel m4
meson setup build/ && meson compile -C build/
meson install -C build/

#Codebuilder Repo for RHEL8
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms


systemctl mask emergency.service

$ podman login registry.access.redhat.com
Username: {REGISTRY-SERVICE-ACCOUNT-USERNAME}
Password: {REGISTRY-SERVICE-ACCOUNT-PASSWORD}
Login Succeeded!

to check the cointainer ID 	
podman ps -a

RHEL UBI

podman pull registry.access.redhat.com/ubi7/ubi-minimal:latest
podman pull registry.access.redhat.com/ubi8/ubi-minimal:latest
podman pull registry.access.redhat.com/ubi8:8.4-203



$ podman pull registry.access.redhat.com/rhel7/rhel:latest
podman run -it registry.access.redhat.com/rhel7/rhel /bin/bash
podman export -o rhel7.latest.tar.gz aa1d92990b86 cointainer -id


Pull using docker
docker login registry.redhat.io
docker pull registry.redhat.io/rhel8/rhel-guest-image:latest
docker images
docker run -it --name test registry.access.redhat.com/ubi8/ubi:8.1 bash
docker export --output="centos-genie.tar.gz" bf659c03dc14


https://developers.redhat.com/blog/2020/03/24/red-hat-universal-base-images-for-docker-users#introducing_red_hat_universal_base_images
docker run -it --name test registry.access.redhat.com/ubi8/ubi:8.1 bash

#to remove images	
docker rmi  4239cd2958c6 7e0aa2d69a15

#to return to the existing/running docker image
docker ps -a
docker start container id-1

#after you start, you'll be inside docker #1, to attach execute
docker attach container id-2

#to run cloudera-quickstart image
docker run --hostname=quickstart.cloudera --privileged=true -t -i -p 8888:8888 -p 7180:7180 -p 80:80 4239cd2958c6 /usr/bin/docker-quickstart

#Howto run docker inside the docker
https://devopscube.com/run-docker-in-docker/#:~:text=To%20run%20docker%20inside%20docker,sock%20as%20a%20volume.&text=Just%20a%20word%20of%20caution,container%20gets%20access%20to%20docker.

#how to have docker container inside the docker container.

docker run -v /var/run/docker.sock:/var/run/docker.sock -it docker_image




docker pull centos6.10









