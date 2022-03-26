### Порядок запуска и подключения сервера OpenVPN.

#### Запуск ВМ на AWS
#### Установка сервера OpenVPN

* Установка сервера OpenVPN по [этой статье](https://openvpn.net/download-open-vpn/)
  * Выбрать вариант походящий по Дистрибутиву `Ubuntu-20.04 Focal`
  * Выполнить на сервере:

```
apt update && apt -y install ca-certificates wget net-tools gnupg
```
```
wget -qO - https://as-repository.openvpn.net/as-repo-public.gpg | apt-key add -
```
```
echo "deb http://as-repository.openvpn.net/as/debian focal main">/etc/apt/sources.list.d/openvpn-as-repo.list
```
```
apt update && apt -y install openvpn-as
```

* Практическое выполнение:

```
maestro@PC-Ubuntu:~/.ssh$ ssh -i "ubuntu-open-vpn.pem" ubuntu@ec2-3-82-174-127.compute-1.amazonaws.com
The authenticity of host 'ec2-3-82-174-127.compute-1.amazonaws.com (3.82.174.127)' can't be established.
ECDSA key fingerprint is SHA256:/83t8SN0yNMMog+XL+oA7UnzdedpSxqghTXykvw23x4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'ec2-3-82-174-127.compute-1.amazonaws.com,3.82.174.127' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 18.04.6 LTS (GNU/Linux 5.4.0-1060-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Mar 26 15:28:30 UTC 2022

  System load:  0.01              Processes:           97
  Usage of /:   14.9% of 7.69GB   Users logged in:     0
  Memory usage: 19%               IP address for eth0: 172.31.94.64
  Swap usage:   0%

0 updates can be applied immediately.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

ubuntu@ip-172-31-94-64:~$ 
ubuntu@ip-172-31-94-64:~$ 
```

```
ubuntu@ip-172-31-94-64:~$ sudo -i
root@ip-172-31-94-64:~# 
```

```
root@ip-172-31-94-64:~# apt update && apt -y install ca-certificates wget net-tools gnupg
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]
Get:4 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]         
Get:5 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [8570 kB]
Get:6 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe Translation-en [4941 kB]
Get:7 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/multiverse amd64 Packages [151 kB]
Get:8 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/multiverse Translation-en [108 kB]
Get:9 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages [2490 kB]
Get:10 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/main Translation-en [468 kB]
Get:11 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/restricted amd64 Packages [695 kB]
Get:12 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/restricted Translation-en [95.3 kB]
Get:13 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages [1797 kB]
Get:14 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/universe Translation-en [389 kB]
Get:15 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 Packages [24.8 kB]
Get:16 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/multiverse Translation-en [6012 B]
Get:17 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports/main amd64 Packages [10.3 kB]
Get:18 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports/main Translation-en [4824 B]
Get:19 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports/universe amd64 Packages [11.3 kB]
Get:20 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports/universe Translation-en [5772 B]
Get:21 http://security.ubuntu.com/ubuntu bionic-security/main amd64 Packages [2143 kB]
Get:22 http://security.ubuntu.com/ubuntu bionic-security/main Translation-en [376 kB]
Get:23 http://security.ubuntu.com/ubuntu bionic-security/restricted amd64 Packages [670 kB]
Get:24 http://security.ubuntu.com/ubuntu bionic-security/restricted Translation-en [91.3 kB]
Get:25 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages [1183 kB]
Get:26 http://security.ubuntu.com/ubuntu bionic-security/universe Translation-en [272 kB]
Get:27 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 Packages [17.6 kB]
Get:28 http://security.ubuntu.com/ubuntu bionic-security/multiverse Translation-en [3660 B]
Fetched 24.8 MB in 5s (4940 kB/s)                           
Reading package lists... Done
Building dependency tree       
Reading state information... Done
68 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
net-tools is already the newest version (1.60+git20161116.90da8a0-1ubuntu1).
net-tools set to manually installed.
ca-certificates is already the newest version (20210119~18.04.2).
ca-certificates set to manually installed.
gnupg is already the newest version (2.2.4-1ubuntu1.4).
gnupg set to manually installed.
wget is already the newest version (1.19.4-1ubuntu2.2).
wget set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 68 not upgraded.
root@ip-172-31-94-64:~# 
```

```
root@ip-172-31-94-64:~# wget -qO - https://as-repository.openvpn.net/as-repo-public.gpg | apt-key add -
OK
```

```
root@ip-172-31-94-64:~# echo "deb http://as-repository.openvpn.net/as/debian focal main">/etc/apt/sources.list.d/openvpn-as-repo.list
```

```
root@ip-172-31-94-64:~# apt update && apt -y install openvpn-as
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports InRelease                  
Hit:4 http://security.ubuntu.com/ubuntu bionic-security InRelease                                
Get:5 http://as-repository.openvpn.net/as/debian focal InRelease [5276 B]
Get:6 http://as-repository.openvpn.net/as/debian focal/main amd64 Packages [9761 B]
Fetched 15.0 kB in 0s (34.0 kB/s)
Reading package lists... Done
Building dependency tree       
Reading state information... Done
68 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 openvpn-as : Depends: libffi7 (>= 3.3~20180313) but it is not installable
              Depends: libgcc-s1 (>= 3.0) but it is not installable
              Depends: libstdc++6 (>= 9) but 8.4.0-1ubuntu1~18.04 is to be installed
E: Unable to correct problems, you have held broken packages.
root@ip-172-31-94-64:~# 
```

```
root@ip-172-31-94-64:~# echo "deb http://as-repository.openvpn.net/as/debian bionic main">/etc/apt/sources.list.d/openvpn-as-repo.list
root@ip-172-31-94-64:~# 
```

```
root@ip-172-31-94-64:~# apt update && apt -y install openvpn-as
Hit:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic InRelease
Hit:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates InRelease
Hit:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-backports InRelease                   
Get:4 http://as-repository.openvpn.net/as/debian bionic InRelease [3186 B]                            
Hit:5 http://security.ubuntu.com/ubuntu bionic-security InRelease                                     
Get:6 http://as-repository.openvpn.net/as/debian bionic/main amd64 Packages [11.7 kB]
Fetched 14.8 kB in 0s (35.3 kB/s)                   
Reading package lists... Done
Building dependency tree       
Reading state information... Done
68 packages can be upgraded. Run 'apt list --upgradable' to see them.
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  bridge-utils libmariadb3 libmysqlclient20 mysql-common openvpn-as-bundled-clients python3-decorator python3-ldap3 python3-migrate python3-mysqldb python3-pbr python3-sqlalchemy python3-sqlparse
  python3-tempita sqlite3
Suggested packages:
  ifupdown python-migrate-doc default-mysql-server | virtual-mysql-server python-egenix-mxdatetime python3-mysqldb-dbg python-sqlalchemy-doc python3-psycopg2 python3-pymysql python3-fdb
  python-sqlparse-doc sqlite3-doc
The following NEW packages will be installed:
  bridge-utils libmariadb3 libmysqlclient20 mysql-common openvpn-as openvpn-as-bundled-clients python3-decorator python3-ldap3 python3-migrate python3-mysqldb python3-pbr python3-sqlalchemy
  python3-sqlparse python3-tempita sqlite3
0 upgraded, 15 newly installed, 0 to remove and 68 not upgraded.
Need to get 189 MB of archives.
After this operation, 234 MB of additional disk space will be used.
Get:1 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 bridge-utils amd64 1.5-15ubuntu1 [30.1 kB]
Get:2 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe amd64 libmariadb3 amd64 3.0.3-1build1 [106 kB]
Get:3 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 mysql-common all 5.8+1.0.4 [7308 B]
Get:4 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/main amd64 libmysqlclient20 amd64 5.7.37-0ubuntu0.18.04.1 [689 kB]
Get:5 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic-updates/main amd64 sqlite3 amd64 3.22.0-1ubuntu0.4 [752 kB]
Get:6 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-decorator all 4.1.2-1 [9364 B]
Get:7 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 python3-pbr all 3.1.1-3ubuntu3 [53.8 kB]
Get:8 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 python3-sqlalchemy all 1.1.11+ds1-1ubuntu1 [680 kB]
Get:9 http://as-repository.openvpn.net/as/debian bionic/main amd64 openvpn-as-bundled-clients all 22 [171 MB]
Get:10 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 python3-sqlparse all 0.2.4-0.1 [28.1 kB]
Get:11 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 python3-tempita all 0.5.2-2 [13.9 kB]
Get:12 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-migrate all 0.11.0-2 [69.4 kB]
Get:13 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/main amd64 python3-mysqldb amd64 1.3.10-1build1 [46.0 kB]
Get:14 http://us-east-1.ec2.archive.ubuntu.com/ubuntu bionic/universe amd64 python3-ldap3 all 2.4.1-1 [217 kB]
Get:15 http://as-repository.openvpn.net/as/debian bionic/main amd64 openvpn-as amd64 2.10.2-3383e1e5-Ubuntu18 [15.5 MB]
Fetched 189 MB in 4s (43.2 MB/s)  
Selecting previously unselected package bridge-utils.
(Reading database ... 57598 files and directories currently installed.)
Preparing to unpack .../00-bridge-utils_1.5-15ubuntu1_amd64.deb ...
Unpacking bridge-utils (1.5-15ubuntu1) ...
Selecting previously unselected package libmariadb3:amd64.
Preparing to unpack .../01-libmariadb3_3.0.3-1build1_amd64.deb ...
Unpacking libmariadb3:amd64 (3.0.3-1build1) ...
Selecting previously unselected package mysql-common.
Preparing to unpack .../02-mysql-common_5.8+1.0.4_all.deb ...
Unpacking mysql-common (5.8+1.0.4) ...
Selecting previously unselected package libmysqlclient20:amd64.
Preparing to unpack .../03-libmysqlclient20_5.7.37-0ubuntu0.18.04.1_amd64.deb ...
Unpacking libmysqlclient20:amd64 (5.7.37-0ubuntu0.18.04.1) ...
Selecting previously unselected package sqlite3.
Preparing to unpack .../04-sqlite3_3.22.0-1ubuntu0.4_amd64.deb ...
Unpacking sqlite3 (3.22.0-1ubuntu0.4) ...
Selecting previously unselected package python3-decorator.
Preparing to unpack .../05-python3-decorator_4.1.2-1_all.deb ...
Unpacking python3-decorator (4.1.2-1) ...
Selecting previously unselected package python3-pbr.
Preparing to unpack .../06-python3-pbr_3.1.1-3ubuntu3_all.deb ...
Unpacking python3-pbr (3.1.1-3ubuntu3) ...
Selecting previously unselected package python3-sqlalchemy.
Preparing to unpack .../07-python3-sqlalchemy_1.1.11+ds1-1ubuntu1_all.deb ...
Unpacking python3-sqlalchemy (1.1.11+ds1-1ubuntu1) ...
Selecting previously unselected package python3-sqlparse.
Preparing to unpack .../08-python3-sqlparse_0.2.4-0.1_all.deb ...
Unpacking python3-sqlparse (0.2.4-0.1) ...
Selecting previously unselected package python3-tempita.
Preparing to unpack .../09-python3-tempita_0.5.2-2_all.deb ...
Unpacking python3-tempita (0.5.2-2) ...
Selecting previously unselected package python3-migrate.
Preparing to unpack .../10-python3-migrate_0.11.0-2_all.deb ...
Unpacking python3-migrate (0.11.0-2) ...
Selecting previously unselected package python3-mysqldb.
Preparing to unpack .../11-python3-mysqldb_1.3.10-1build1_amd64.deb ...
Unpacking python3-mysqldb (1.3.10-1build1) ...
Selecting previously unselected package openvpn-as-bundled-clients.
Preparing to unpack .../12-openvpn-as-bundled-clients_22_all.deb ...
Unpacking openvpn-as-bundled-clients (22) ...
Selecting previously unselected package python3-ldap3.
Preparing to unpack .../13-python3-ldap3_2.4.1-1_all.deb ...
Unpacking python3-ldap3 (2.4.1-1) ...
Selecting previously unselected package openvpn-as.
Preparing to unpack .../14-openvpn-as_2.10.2-3383e1e5-Ubuntu18_amd64.deb ...
Unpacking openvpn-as (2.10.2-3383e1e5-Ubuntu18) ...
Setting up libmariadb3:amd64 (3.0.3-1build1) ...
Setting up python3-pbr (3.1.1-3ubuntu3) ...
update-alternatives: using /usr/bin/python3-pbr to provide /usr/bin/pbr (pbr) in auto mode
Setting up python3-sqlalchemy (1.1.11+ds1-1ubuntu1) ...
Setting up python3-ldap3 (2.4.1-1) ...
Setting up python3-sqlparse (0.2.4-0.1) ...
Setting up python3-tempita (0.5.2-2) ...
Setting up mysql-common (5.8+1.0.4) ...
update-alternatives: using /etc/mysql/my.cnf.fallback to provide /etc/mysql/my.cnf (my.cnf) in auto mode
Setting up sqlite3 (3.22.0-1ubuntu0.4) ...
Setting up bridge-utils (1.5-15ubuntu1) ...
Setting up libmysqlclient20:amd64 (5.7.37-0ubuntu0.18.04.1) ...
Setting up python3-decorator (4.1.2-1) ...
Setting up openvpn-as-bundled-clients (22) ...
Setting up python3-mysqldb (1.3.10-1build1) ...
Setting up python3-migrate (0.11.0-2) ...
update-alternatives: using /usr/bin/python3-migrate to provide /usr/bin/migrate (migrate) in auto mode
update-alternatives: using /usr/bin/python3-migrate-repository to provide /usr/bin/migrate-repository (migrate-repository) in auto mode
Setting up openvpn-as (2.10.2-3383e1e5-Ubuntu18) ...
Beginning with OpenVPN AS 2.6.0 compression is disabled by default and on upgrades as security patch.

To reconfigure manually, use the /usr/local/openvpn_as/bin/ovpn-init tool.

+++++++++++++++++++++++++++++++++++++++++++++++
Access Server 2.10.2 has been successfully installed in /usr/local/openvpn_as
Configuration log file has been written to /usr/local/openvpn_as/init.log


Access Server Web UIs are available here:
Admin  UI: https://172.31.94.64:943/admin
Client UI: https://172.31.94.64:943/
Login as "openvpn" with "ppW5iLDBknVW" to continue
(password can be changed on Admin UI)
+++++++++++++++++++++++++++++++++++++++++++++++

Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Processing triggers for libc-bin (2.27-3ubuntu1.4) ...
root@ip-172-31-94-64:~# 
```



#### Конфигурирование сервера OpenVPN
#### Установка клиента OpenVPN на ОС Ubuntu

Статья по установке и настройке комента [OpenVPN 3 Linux](https://community.openvpn.net/openvpn/wiki/OpenVPN3Linux?_ga=2.137721525.403010542.1648301988-1657003433.1648301987)

* First ensure that your apt supports the https transport:
```
   # apt install apt-transport-https
```
* Install the OpenVPN repository key used by the OpenVPN 3 Linux packages

```
   # curl -fsSL https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub | gpg --dearmor > /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
   
```
* Then you need to install the proper repository. Replace $DISTRO with the release name depending on your Debian/Ubuntu distribution.
* $DISTRO - focal
```
   # curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-focal.list >/etc/apt/sources.list.d/openvpn3.list
   # apt update
```

|Distribution	Release|	Release name ($DISTRO)|	Architecture|	DCO support|
|--------------------|------------------------|-------------|------------|
|Debian|	9|	stretch|	amd64|	-|
|Debian|	10|	buster|	amd64, arm64*|	-|
|Debian	|11	|bullseye	|amd64, arm64*|	-|
|Ubuntu	|18.04|	bionic|	amd64, arm64*|	-|
|Ubuntu	|20.04|	focal|	amd64, arm64*|	yes*|
|Ubuntu	|21.04|	hirsute|	amd64, arm64*|	yes*|



* And finally the openvpn3 package can be installed
```
   # apt install openvpn3
```
---


```
maestro@PC-Ubuntu:~$ sudo apt install apt-transport-https
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие пакеты устанавливались автоматически и больше не требуются:
  ieee-data python3-argcomplete python3-dnspython python3-jinja2 python3-kerberos python3-libcloud python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux
  python3-winrm python3-xmltodict
Для их удаления используйте «sudo apt autoremove».
Следующие НОВЫЕ пакеты будут установлены:
  apt-transport-https
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 42 пакетов не обновлено.
Необходимо скачать 4 680 B архивов.
После данной операции объём занятого дискового пространства возрастёт на 162 kB.
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 apt-transport-https all 2.0.6 [4 680 B]
Получено 4 680 B за 0с (54,9 kB/s)                  
Выбор ранее не выбранного пакета apt-transport-https.
(Чтение базы данных … на данный момент установлен 266841 файл и каталог.)
Подготовка к распаковке …/apt-transport-https_2.0.6_all.deb …
Распаковывается apt-transport-https (2.0.6) …
Настраивается пакет apt-transport-https (2.0.6) …
```

```
maestro@PC-Ubuntu:~$ sudo curl -fsSL https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub | gpg --dearmor > /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
bash: /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg: Отказано в доступе
(23) Failed writing body
```

```
maestro@PC-Ubuntu:~$ sudo -i
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/repos/openvpn-repo-pkg-key.pub | gpg --dearmor > /etc/apt/trusted.gpg.d/openvpn-repo-pkg-keyring.gpg
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-$DISTRO.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-$DISTRO.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# apt update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Сущ:2 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Пол:3 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]                                                                                                                                   
Пол:4 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                                                                                                    
Сущ:5 https://dl.google.com/linux/chrome/deb stable InRelease                                                                                                                                                
Пол:6 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]                                                                                                  
Сущ:7 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                                   
Сущ:8 http://ppa.launchpad.net/inkscape.dev/stable/ubuntu focal InRelease                                                                                        
Ошб:9 https://apt.releases.hashicorp.com focal InRelease                                                                                                                            
  405  Not allowed [IP: 151.101.86.49 443]
Сущ:10 http://ppa.launchpad.net/linuxuprising/java/ubuntu focal InRelease                                    
Пол:11 http://ru.archive.ubuntu.com/ubuntu focal-updates/main i386 Packages [621 kB]
Пол:12 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1 674 kB]
Пол:13 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 DEP-11 Metadata [278 kB]
Пол:14 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 DEP-11 Metadata [391 kB]
Пол:15 http://ru.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 DEP-11 Metadata [944 B]
Пол:16 http://security.ubuntu.com/ubuntu focal-security/main amd64 DEP-11 Metadata [40,8 kB]
Пол:17 http://security.ubuntu.com/ubuntu focal-security/universe amd64 DEP-11 Metadata [66,4 kB]
Пол:18 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 DEP-11 Metadata [2 464 B]
Пол:19 http://ru.archive.ubuntu.com/ubuntu focal-backports/main amd64 DEP-11 Metadata [8 016 B]
Пол:20 http://ru.archive.ubuntu.com/ubuntu focal-backports/universe amd64 DEP-11 Metadata [30,8 kB]
Чтение списков пакетов… Готово                
E: Не удалось получить https://apt.releases.hashicorp.com/dists/focal/InRelease  405  Not allowed [IP: 151.101.86.49 443]
E: Репозиторий «https://apt.releases.hashicorp.com focal InRelease» больше не подписан.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «https://dl.google.com/linux/chrome/deb stable InRelease» не поддерживает архитектуру «i386»
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# apt install openvpn3
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
E: Невозможно найти пакет openvpn3
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname -a
Linux PC-Ubuntu 5.13.0-35-generic #40~20.04.1-Ubuntu SMP Mon Mar 7 09:18:32 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# cat /etc/*Release*
cat: '/etc/*Release*': Нет такого файла или каталога
root@PC-Ubuntu:~# cat /etc/Release*
cat: '/etc/Release*': Нет такого файла или каталога
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname
Linux
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# uname --help
Использование: uname [ПАРАМЕТР]…
Печатает определенные сведения о системе. Если ПАРАМЕТР не задан, то
подразумевается -s.

  -a, --all              напечатать всю информацию, в следующем порядке,
                         кроме -p и -i, если они неизвестны:
  -s, --kernel-name      напечатать имя ядра
  -n, --nodename         напечатать имя машины в сети
  -r, --kernel-release   напечатать информацию о выпуске ядра
  -v, --kernel-version     напечатать версию ядра
  -m, --machine            напечатать тип оборудования машины
  -p, --processor          напечатать тип процессора (непереносима)
  -i, --hardware-platform  напечатать тип аппаратной платформы (непереносима)
  -o, --operating-system   напечатать имя операционной системы
      --help     показать эту справку и выйти
      --version  показать информацию о версии и выйти

Страница справки по GNU coreutils: <https://www.gnu.org/software/coreutils/>
Об ошибках в переводе сообщений «uname» сообщайте по адресу <gnu@d07.ru>
Полная документация: <https://www.gnu.org/software/coreutils/uname>
или доступная локально: info '(coreutils) uname invocation'
root@PC-Ubuntu:~# uname -0
uname: неверный ключ — «0»
По команде «uname --help» можно получить дополнительную информацию.
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname -o
GNU/Linux
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname -s
Linux
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname -r
5.13.0-35-generic
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# echo $DISTRO

root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-Ubuntu-20.04.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-5.13.0-35-generic.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-Linux.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-`uname -s`-`uname -m`.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# uname -s && uname -m
Linux
x86_64
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-Linux-x86_64.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-Linux-x86_64.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.3 LTS"
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-Ubuntu.list >/etc/apt/sources.list.d/openvpn3.list
curl: (22) The requested URL returned error: 404 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# curl -fsSL https://swupdate.openvpn.net/community/openvpn3/repos/openvpn3-focal.list >/etc/apt/sources.list.d/openvpn3.list
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# apt update
Сущ:1 http://ru.archive.ubuntu.com/ubuntu focal InRelease
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]                                                                                                                                   
Сущ:3 http://download.virtualbox.org/virtualbox/debian focal InRelease                                                                                                                                       
Пол:4 https://swupdate.openvpn.net/community/openvpn3/repos focal InRelease [6 840 B]                                                                                                                        
Сущ:5 http://ppa.launchpad.net/inkscape.dev/stable/ubuntu focal InRelease                                                                                                                                    
Сущ:6 https://dl.google.com/linux/chrome/deb stable InRelease                                                                                                                                                
Пол:7 http://ru.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]                                                                                                                                 
Сущ:8 https://download.virtualbox.org/virtualbox/debian bionic InRelease                                                                                                                                     
Пол:9 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]                                                                                                                                    
Ошб:10 https://apt.releases.hashicorp.com focal InRelease                                                                                                                     
  405  Not allowed [IP: 151.101.86.49 443]
Сущ:11 http://ppa.launchpad.net/linuxuprising/java/ubuntu focal InRelease                                                                                               
Пол:12 https://swupdate.openvpn.net/community/openvpn3/repos focal/main amd64 Packages [10,7 kB]            
Пол:13 http://ru.archive.ubuntu.com/ubuntu focal-updates/main amd64 DEP-11 Metadata [278 kB]
Пол:14 http://ru.archive.ubuntu.com/ubuntu focal-updates/universe amd64 DEP-11 Metadata [390 kB]
Пол:15 http://ru.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 DEP-11 Metadata [944 B]
Пол:16 http://ru.archive.ubuntu.com/ubuntu focal-backports/main amd64 DEP-11 Metadata [8 004 B]
Пол:17 http://ru.archive.ubuntu.com/ubuntu focal-backports/universe amd64 DEP-11 Metadata [30,8 kB]
Пол:18 http://security.ubuntu.com/ubuntu focal-security/main amd64 DEP-11 Metadata [40,7 kB]
Пол:19 http://security.ubuntu.com/ubuntu focal-security/universe amd64 DEP-11 Metadata [66,3 kB]
Пол:20 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 DEP-11 Metadata [2 464 B]
Чтение списков пакетов… Готово              
E: Не удалось получить https://apt.releases.hashicorp.com/dists/focal/InRelease  405  Not allowed [IP: 151.101.86.49 443]
E: Репозиторий «https://apt.releases.hashicorp.com focal InRelease» больше не подписан.
N: Обновление из этого репозитория нельзя выполнить безопасным способом, поэтому по умолчанию он отключён.
N: Информацию о создании репозитория и настройках пользователя смотрите в справочной странице apt-secure(8).
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «https://swupdate.openvpn.net/community/openvpn3/repos focal InRelease» не поддерживает архитектуру «i386»
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
N: Пропускается получение настроенного файла «main/binary-i386/Packages», так как репозиторий «https://dl.google.com/linux/chrome/deb stable InRelease» не поддерживает архитектуру «i386»
W: Цель Packages (main/binary-amd64/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Packages (main/binary-all/Packages) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru_RU) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-ru) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель Translations (main/i18n/Translation-en) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-amd64.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11 (main/dep11/Components-all.yml) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-small (main/dep11/icons-48x48.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons (main/dep11/icons-64x64.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель DEP-11-icons-hidpi (main/dep11/icons-64x64@2.tar) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-amd64) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
W: Цель CNF (main/cnf/Commands-all) настроена несколько раз: в /etc/apt/sources.list.d/google-chrome.list:3 и в /etc/apt/sources.list.d/google.list:1
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# apt install openvpn3
Чтение списков пакетов… Готово
Построение дерева зависимостей       
Чтение информации о состоянии… Готово
Следующие пакеты устанавливались автоматически и больше не требуются:
  ieee-data python3-argcomplete python3-dnspython python3-jinja2 python3-kerberos python3-libcloud python3-netaddr python3-ntlm-auth python3-requests-kerberos python3-requests-ntlm python3-selinux
  python3-winrm python3-xmltodict
Для их удаления используйте «apt autoremove».
Будут установлены следующие дополнительные пакеты:
  libjsoncpp1 libtinyxml2-6a
Следующие НОВЫЕ пакеты будут установлены:
  libjsoncpp1 libtinyxml2-6a openvpn3
Обновлено 0 пакетов, установлено 3 новых пакетов, для удаления отмечено 0 пакетов, и 42 пакетов не обновлено.
Необходимо скачать 1 646 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 7 450 kB.
Хотите продолжить? [Д/н] y
Пол:1 http://ru.archive.ubuntu.com/ubuntu focal/universe amd64 libtinyxml2-6a amd64 7.0.0+dfsg-1build1 [28,4 kB]
Пол:2 http://ru.archive.ubuntu.com/ubuntu focal/main amd64 libjsoncpp1 amd64 1.7.4-3.1ubuntu2 [75,6 kB] 
Пол:3 https://swupdate.openvpn.net/community/openvpn3/repos focal/main amd64 openvpn3 amd64 17~beta2+focal [1 542 kB]
Получено 1 646 kB за 0с (4 509 kB/s)                                           
Выбор ранее не выбранного пакета libtinyxml2-6a:amd64.
(Чтение базы данных … на данный момент установлено 266845 файлов и каталогов.)
Подготовка к распаковке …/libtinyxml2-6a_7.0.0+dfsg-1build1_amd64.deb …
Распаковывается libtinyxml2-6a:amd64 (7.0.0+dfsg-1build1) …
Выбор ранее не выбранного пакета libjsoncpp1:amd64.
Подготовка к распаковке …/libjsoncpp1_1.7.4-3.1ubuntu2_amd64.deb …
Распаковывается libjsoncpp1:amd64 (1.7.4-3.1ubuntu2) …
Выбор ранее не выбранного пакета openvpn3.
Подготовка к распаковке …/openvpn3_17~beta2+focal_amd64.deb …
Распаковывается openvpn3 (17~beta2+focal) …
Настраивается пакет libtinyxml2-6a:amd64 (7.0.0+dfsg-1build1) …
Настраивается пакет libjsoncpp1:amd64 (1.7.4-3.1ubuntu2) …
Настраивается пакет openvpn3 (17~beta2+focal) …
openvpn3-autoload.service is a disabled or a static unit, not starting it.
Обрабатываются триггеры для man-db (2.9.1-1) …
Обрабатываются триггеры для dbus (1.12.16-2ubuntu2.1) …
Обрабатываются триггеры для libc-bin (2.31-0ubuntu9.7) …
```

```
root@PC-Ubuntu:~# openvpn3 session-start
session-start: ** ERROR ** Either --config or --config-path must be provided
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 
Missing command.  See 'openvpn3 help' for details
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 help
openvpn3: OpenVPN 3
          Command line interface to manage OpenVPN 3 configurations and sessions

  Available commands: 
    help              - This help screen
    shell-completion  - Helper function to provide shell completion data
    version           - Show program version information
    config-import     - Import configuration profiles
    config-manage     - Manage configuration properties
    config-acl        - Manage access control lists for configurations
    config-dump       - Show/dump a configuration profile
    config-remove     - Remove an available configuration profile
    configs-list      - List all available configuration profiles
    session-start     - Start a new VPN session
    session-manage    - Manage VPN sessions
    session-auth      - Interact with on-going session authentication requests
    session-acl       - Manage access control lists for sessions
    session-stats     - Show session statistics
    sessions-list     - List available VPN sessions
    log               - Receive log events as they occur

For more information, run: openvpn3 <command> --help

root@PC-Ubuntu:~# openvpn3 session-auth
No sessions requires authentication interaction
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 session-start --config ${CONFIGURATION_OPENVPN}
openvpn3/session-start: option '--config' requires an argument
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 session-start
session-start: ** ERROR ** Either --config or --config-path must be provided
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# pwd
/root
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# mc
```

* Со страницы пользователя OpenVPN был скачан файл профиля `profile-3.ovpn`
```
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# ls -l
итого 252912
-rw-r--r--  1 tcpdump tcpdump      1223 янв 15 14:04  001.pcap
-rw-r--r--  1 tcpdump tcpdump     48438 янв 15 14:05  002.pcap
drwxr-xr-x  3 root    root         4096 фев 18 21:40  ansible-learning
drwxr-xr-x  3 root    root         4096 янв 13 17:30  devops-netology
drwx------  3 root    root         4096 мар 13 20:27  Downloads
drwxr-xr-x  3 root    root         4096 янв 13 22:39  go
drwxr-xr-x  2 root    root         4096 дек 23 11:36  log
-rw-rw-r--  1 maestro maestro      1700 янв  5 12:21  my-key.pem
drwxr-xr-x 15 root    root         4096 фев  5 08:43  netology-project
-rw-r--r--  1 root    root    198578061 мар 13 22:10  openjdk-14_linux-x64_bin.tar.gz
-rw-rw-r--  1 maestro maestro     10136 мар 26 21:12  profile-3.ovpn
drwxr-xr-x  3 root    root         4096 янв 13 21:40  PycharmProjects
drwxr-xr-x  7 root    root         4096 янв 23 15:41  scripts
drwxr-xr-x  5 root    root         4096 мар 18 11:12  snap
drwxr-xr-x 16 root    root         4096 мар 14 11:29  TEMP
-rwxrwxr-x  1 root    root     45353856 мая 23  2019  terraform
-rw-r--r--  1 root    root     14907580 дек 19 16:54  terraform_0.12.0_linux_amd64.zip
drwxr-xr-x  3 root    root         4096 янв 21 20:44  terraform-provider-aws
-rwxr-xr-x  1 root    root         2483 дек 25 21:56  test-services-2
drwxr-xr-x  3 root    root         4096 янв 15 12:29  testssl
drwxr-xr-x  6 root    root         4096 мар  3 22:42  vagrant-project
drwx------  7 root    root         4096 фев  6 08:24 'VirtualBox VMs'
drwxr-xr-x  4 root    root         4096 дек  9 16:49  yandex-cloud
root@PC-Ubuntu:~# pwd
/root
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# mc
```
* Запуск сессии на основании файла-конфигураци пользователя 
```

root@PC-Ubuntu:~# openvpn3 session-start --config profile-3.ovpn 
Using configuration profile from file: profile-3.ovpn
Session path: /net/openvpn/v3/sessions/f4a2e5f6sa286s439cs9fc7sc39ecbdca540
Auth User name: agent-vasya     # Вводим имя пользователя
Auth Password:                  # Вводим пароль пользователя
Connected
root@PC-Ubuntu:~# 
```
* Проверка доступности ресурсов
```
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# curl https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.14.0-x86_64.rpm
Warning: Binary output can mess up your terminal. Use "--output -" to tell 
Warning: curl to output it to your terminal anyway, or consider "--output 
Warning: <FILE>" to save to a file.
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 sessions-list
-----------------------------------------------------------------------------
        Path: /net/openvpn/v3/sessions/f4a2e5f6sa286s439cs9fc7sc39ecbdca540
     Created: Sat Mar 26 21:16:31 2022                  PID: 170527
       Owner: root                                   Device: tun0
 Config name: profile-3.ovpn  (Config not available)
Session name: 3.82.174.127
      Status: Connection, Client connected
-----------------------------------------------------------------------------
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# ls -lha
итого 248M
drwx------ 30 root    root    4,0K мар 26 21:14  .
drwxr-xr-x 20 root    root    4,0K янв 17 17:34  ..
-rw-r--r--  1 tcpdump tcpdump 1,2K янв 15 14:04  001.pcap
-rw-r--r--  1 tcpdump tcpdump  48K янв 15 14:05  002.pcap
drwxr-xr-x  6 root    root    4,0K фев 20 20:38  .ansible
drwxr-xr-x  3 root    root    4,0K фев 18 21:40  ansible-learning
drwxr-xr-x  2 root    root    4,0K янв  4 11:00  .aws
-rw-------  1 root    root     37K мар 21 21:56  .bash_history
-rw-r--r--  1 root    root    3,9K фев  5 17:16  .bashrc
drwx------ 10 root    root    4,0K фев  6 08:36  .cache
drwx------ 12 root    root    4,0K янв 17 17:34  .config
drwx------  3 root    root    4,0K янв  3 18:03  .dbus
drwxr-xr-x  3 root    root    4,0K янв 13 17:30  devops-netology
drwx------  3 root    root    4,0K мар 13 20:27  Downloads
-rw-r--r--  1 root    root      62 дек  9 15:45  .gitconfig
drwxr-xr-x  3 root    root    4,0K янв 13 22:39  go
drwxr-xr-x  4 root    root    4,0K янв 13 21:31  .java
-rw-------  1 root    root     131 фев 26 17:56  .lesshst
drwx------  3 root    root    4,0K дек  5 14:22  .local
drwxr-xr-x  2 root    root    4,0K дек 23 11:36  log
drwxr-xr-x  3 root    root    4,0K мар 14 10:39  .m2
-rw-rw-r--  1 maestro maestro 1,7K янв  5 12:21  my-key.pem
drwxr-xr-x 15 root    root    4,0K фев  5 08:43  netology-project
-rw-r--r--  1 root    root    190M мар 13 22:10  openjdk-14_linux-x64_bin.tar.gz
-rw-r--r--  1 root    root     161 дек  5  2019  .profile
-rw-rw-r--  1 maestro maestro 9,9K мар 26 21:12  profile-3.ovpn
drwxr-xr-x  3 root    root    4,0K янв 13 21:40  PycharmProjects
-rw-------  1 root    root    2,4K дек 25 12:52  .python_history
drwxr-xr-x  7 root    root    4,0K янв 23 15:41  scripts
-rw-r--r--  1 root    root      72 дек  9 19:58  .selected_editor
drwxr-xr-x  5 root    root    4,0K мар 18 11:12  snap
drwxr-xr-x  4 root    root    4,0K мар 13 18:54  .sonar
drwx------  2 root    root    4,0K мар 16 21:13  .ssh
drwxr-xr-x 16 root    root    4,0K мар 14 11:29  TEMP
-rwxrwxr-x  1 root    root     44M мая 23  2019  terraform
-rw-r--r--  1 root    root     15M дек 19 16:54  terraform_0.12.0_linux_amd64.zip
drwxr-xr-x  2 root    root    4,0K мар 22 20:14  .terraform.d
drwxr-xr-x  3 root    root    4,0K янв 21 20:44  terraform-provider-aws
-rwxr-xr-x  1 root    root    2,5K дек 25 21:56  test-services-2
drwxr-xr-x  3 root    root    4,0K янв 15 12:29  testssl
drwxr-xr-x  7 root    root    4,0K мар 26 10:55  .vagrant.d
drwxr-xr-x  6 root    root    4,0K мар  3 22:42  vagrant-project
-rw-------  1 root    root     38K мар 26 09:05  .viminfo
drwx------  7 root    root    4,0K фев  6 08:24 'VirtualBox VMs'
-rw-r--r--  1 root    root     173 дек  5 13:41  .wget-hsts
drwxr-xr-x  4 root    root    4,0K дек  6 21:37  .wine
drwxr-xr-x  4 root    root    4,0K дек  9 16:49  yandex-cloud
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# openvpn3 sessions-manage
openvpn3: Unknown command 'sessions-manage'
root@PC-Ubuntu:~# 
```

```
root@PC-Ubuntu:~# openvpn3 session-manage
session-manage: ** ERROR ** One of --pause, --resume, --restart, --disconnect, --cleanup or --log-level must be present
root@PC-Ubuntu:~# 
root@PC-Ubuntu:~# 

```

#### Подключение клиента к серверу
#### Отключение клиента от сервера
