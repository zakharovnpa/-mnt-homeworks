# Домашнее задание к занятию "08.01 Введение в Ansible" - Захаров Сергей Николаевич

## Подготовка к выполнению
1. Установите ansible версии 2.10 или выше.
2. Создайте свой собственный публичный репозиторий на github с произвольным именем.
3. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть
1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте какое значение имеет факт `some_fact` для указанного хоста при выполнении playbook'a.

**Ответ:**
```ps
root@PC-Ubuntu:~/netology-project/mnt-homeworks-1/mnt-homeworks/08-ansible-01-base/playbook# ansible-playbook -i inventory/test.yml site.yml

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": 12
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

2. Найдите файл с переменными (group_vars) в котором задаётся найденное в первом пункте значение и поменяйте его на 'all default fact'.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01# grep -r "some_fact" group_vars
group_vars/el/examp.yml:  some_fact: "el default fact"
group_vars/deb/examp.yml:  some_fact: "deb default fact"
group_vars/all/examp.yml:  some_fact:12

```

```ps
root@PC-Ubuntu:~/netology-project/mnt-homeworks-1/mnt-homeworks/08-ansible-01-base/playbook/group_vars/all#ls -l
итого 4
-rw-r--r-- 1 root root 19 фев  4 17:03 examp.yml

```
Содержимое файла изначальное
```yml
---
  some_fact: 12
```
Содержимое файла после замены
```yml
---
  some_fact: all default fact
```

3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.

**Ответ:**
```ps
root@server1:~# docker run -d --name ubuntu ba6acccedd29 sleep 60000000
c028217942579e6001eae90aa8bd8ce3d35f9c2896da4ccba94fb2c8c3558821
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE          COMMAND            CREATED         STATUS         PORTS     NAMES
c02821794257   ba6acccedd29   "sleep 60000000"   7 seconds ago   Up 6 seconds             ubuntu
root@server1:~# 
root@server1:~# docker run -d --name centos7 eeb6ee3f44bd sleep 60000000
6a83d9d628c2bb2d008c1cb61932a05067691f7828c14df5bde8cee844728d37
root@server1:~# 
root@server1:~# 
```

```ps
root@server1:~# docker ps
CONTAINER ID   IMAGE          COMMAND            CREATED          STATUS          PORTS     NAMES
6a83d9d628c2   eeb6ee3f44bd   "sleep 60000000"   3 seconds ago    Up 2 seconds              centos7
c02821794257   ba6acccedd29   "sleep 60000000"   54 seconds ago   Up 53 seconds             ubuntu

```

4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.

**Ответ:**
File ` prod.yml `
```yml
---
  el:
    hosts:
      centos7:
        ansible_connection: docker
  deb:
    hosts:
      ubuntu:
        ansible_connection: docker

```
Вывод ` PLAY [Print os facts] ` 
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/hosts.yml site.yml 

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "deb"
}
ok: [centos7] => {
    "msg": "el"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```


5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились следующие значения: для `deb` - 'deb default fact', для `el` - 'el default fact'.

**Ответ:**
File group_vars/deb/example.yml
```yml
---
  some_fact: "deb default fact"

```
File group_vars/el/example.yml
```yml
---
  some_fact: "el default fact"

```

6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-vault encrypt group_vars/deb/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful
```
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-vault encrypt group_vars/el/examp.yml
New Vault password: 
Confirm New Vault password: 
Encryption successful

```

8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/hosts.yml site.yml 

PLAY [Print os facts] ****************************************************************************************************************************************************************************************
ERROR! Attempting to decrypt but no vault secrets found

```
Запускаем плейбук с запросом пароля
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password: 

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.

**Ответ:**
control node – хост с предустановленным ansible. 
Найдем список плагинов для подключений.
```ps
root@server1:/usr/local/lib/python3.8/dist-packages/ansible/plugins/connection# ansible-doc -t connection -l
[WARNING]: Collection frr.frr does not support Ansible version 2.12.2
[WARNING]: Collection ibm.qradar does not support Ansible version 2.12.2
[WARNING]: Collection splunk.es does not support Ansible version 2.12.2
ansible.netcommon.httpapi      Use httpapi to run command on network appliances  
ansible.netcommon.libssh       (Tech preview) Run tasks using libssh for ssh connection 
ansible.netcommon.napalm       Provides persistent connection using NAPALM    
ansible.netcommon.netconf      Provides a persistent connection using the netconf protocol 
ansible.netcommon.network_cli  Use network_cli to run command on network appliances     
ansible.netcommon.persistent   Use a persistent unix socket for connection   
community.aws.aws_ssm          execute via AWS Systems Manager          
community.docker.docker        Run tasks in docker containers    
community.docker.docker_api    Run tasks in docker containers    
community.docker.nsenter       execute on host running controller container  
community.general.chroot       Interact with local chroot      
community.general.funcd        Use funcd to connect to target    
community.general.iocage       Run tasks in iocage jails        
community.general.jail         Run tasks in jails     
community.general.lxc          Run tasks in lxc containers via lxc python library  
community.general.lxd          Run tasks in lxc containers via lxc CLI         
community.general.qubes        Interact with an existing QubesOS AppVM      
community.general.saltstack    Allow ansible to piggyback on salt minions   
community.general.zone         Run tasks in a zone instance  
community.libvirt.libvirt_lxc  Run tasks in lxc containers via libvirt   
community.libvirt.libvirt_qemu Run tasks on libvirt/qemu virtual machines   
community.okd.oc               Execute tasks in pods running on OpenShift   
community.vmware.vmware_tools  Execute tasks inside a VM via VMware Tools   
containers.podman.buildah      Interact with an existing buildah container   
containers.podman.podman       Interact with an existing podman container    
kubernetes.core.kubectl        Execute tasks in pods running on Kubernetes   
local                          execute on controller                       
paramiko_ssh                   Run tasks via python ssh (paramiko)      
psrp                           Run tasks over Microsoft PowerShell Remoting Protocol   
ssh                            connect via SSH client binary    
winrm                          Run tasks over Microsoft's WinRM 
```
Наиболее подходящий плагин
```ps
local                          execute on controller    

```
Посмотреть описание плагина
```ps
ansible-doc -t connection local
```

10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.

**Ответ:**
Для добавления новой группы хостов в файле ` inventory/prod.yml ` добавлено:
```yml
  local:
    hosts:
      localhost:
        ansible_connection: local

```
Создана новая директория ` group_vars/local `
А в файле ` group_vars/local/examp.yml ` добавлено:
```yml
---
  some_fact: "local default fact"

```

11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь что факты `some_fact` для каждого из хостов определены из верных `group_vars`.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/prod.yml site.yml

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "local default fact"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.

Файл `README.md` заполнен. Ссылка на репозиторий с измененным `playbook`: [Ansible-netology](https://github.com/zakharovnpa/Ansible-netology)

## Необязательная часть

1. При помощи `ansible-vault` расшифруйте все зашифрованные файлы с переменными.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-vault decrypt group_vars/deb/examp.yml
Vault password: 
Decryption successful
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# 
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-vault decrypt group_vars/el/examp.yml
Vault password: 
Decryption successful

```

2. Зашифруйте отдельное значение `PaSSw0rd` для переменной `some_fact` паролем `netology`. Добавьте полученное значение в `group_vars/all/exmp.yml`.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-vault encrypt_string
New Vault password: 
Confirm New Vault password: 
Reading plaintext input from stdin. (ctrl-d to end input, twice if your content does not already have a newline)
PaSSw0rd
!vault |
          $ANSIBLE_VAULT;1.1;AES256
          64643330363533656635636332643634323932653539303466326233386536383666396338306665
          3465623835666661663433303439346635303662326130300a333239663231666339646464653638
          63616565303434376664383737323731626538363530343866636432623838333338613139346464
          6635316338306263350a623864653266653630636532663961336134646261643662393465383537
          3238
Encryption successful
```
Добавляем полученное значение в `group_vars/all/exmp.yml`
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# cat group_vars/all/examp.yml 
---
  some_fact: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          64643330363533656635636332643634323932653539303466326233386536383666396338306665
          3465623835666661663433303439346635303662326130300a333239663231666339646464653638
          63616565303434376664383737323731626538363530343866636432623838333338613139346464
          6635316338306263350a623864653266653630636532663961336134646261643662393465383537
          3238

```

3. Запустите `playbook`, убедитесь, что для нужных хостов применился новый `fact`.

**Ответ:**
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password: 

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "PaSSw0rd"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```

4. Добавьте новую группу хостов `fedora`, самостоятельно придумайте для неё переменную. В качестве образа можно использовать [этот](https://hub.docker.com/r/pycontribs/fedora).

**Ответ:**
Запускаем новый контейнер fedore
```ps
root@server1:~# docker run -d --name fedore c31790496329 sleep 60000000
f44a0ef7cfe40e0933865ad73fc0007e9c5bdefc2525096cb46acddfaab98ee6
root@server1:~# 
root@server1:~# 
root@server1:~# docker ps
CONTAINER ID   IMAGE          COMMAND            CREATED         STATUS         PORTS     NAMES
f44a0ef7cfe4   c31790496329   "sleep 60000000"   3 seconds ago   Up 3 seconds             fedore
d81342e16c99   42a4e3b21923   "sleep 60000000"   21 hours ago    Up 21 hours              ubuntu
6a83d9d628c2   eeb6ee3f44bd   "sleep 60000000"   34 hours ago    Up 34 hours              centos7
```

Добавлена новая группа ` fed ` в ` inventory/prod.yml `
```yml
  fed:
    hosts:
      fedore:
        ansible_connection: docker
```
Добавлена новая переменная ` fed default fact ` в ` group_vars/fed/examp.yml `
```yml
---
  some_fact: "fed default fact"
```
Запускаем playbook
```ps
root@server1:~/learning-ansible/Lesson-ansible-01/playbook# ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass
Vault password: 

PLAY [Print os facts] ****************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]
ok: [fedore]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] **********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [fedore] => {
    "msg": "Fedora"
}

TASK [Print fact] ********************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "PaSSw0rd"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [fedore] => {
    "msg": "fed default fact"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
fedore                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

5. Напишите скрипт на bash: автоматизируйте поднятие необходимых контейнеров, запуск ansible-playbook и остановку контейнеров.

**Ответ:**
Составлен план действий скрипта:
- выполнить команду запуска контейнера ` centos7 `
- независимо от результата выполнения выполнить команду запуска контейнера ` ubuntu `
- независимо от результата выполнения выполнить команду запуска контейнера ` fedore `
- выдержать паузу 10 секунд
- выполнить команду запуска ` ansible-playbook `
- вывести в терминал список запущеных контейнеров.
- дождаться окончания выполнения команды запуска ` ansible-playbook `
- вывести в файл логов вывод команды ` ansible-playbook `
- выполнить команду остановки контейнера ` centos7 `
- независимо от результата выполнения выполнить команду остановки контейнера ` ubuntu `
- независимо от результата выполнения выполнить команду остановки контейнера ` fedore `
- вывести в терминал список запущеных контейнеров.

```bash
#!/usr/bin/env bash
#
# Скрипт для запуска контейнеров docker и запуска ansible-playbook

date >> ansible.log &&		# Запись даты выполнения скрипта
docker run -d --rm --name centos7 eeb6ee3f44bd sleep 60000000 && 	# Старт нового контейнера с именем centos7 на основе образа eeb6ee3f44bd
docker run -d --rm --name fedore c31790496329 sleep 60000000 &&		# Аналогично для fedore
docker run -d --rm --name ubuntu 42a4e3b21923 sleep 60000000 &&		# Аналогично для ubuntu

	sleep 3 &&				# Выполнить остановку скрипта на 3 секунды
	docker ps | grep 'Up' && 		# Вывод на терминал контейнеров, которые запустились
	sleep 10 &&				# Выполнить остановку скрипта на 10 секунд

ansible-playbook -i inventory/prod.yml site.yml --ask-vault-pass >> ansible.log && 	# Запуск playbook с запросом пароля на расшифровку файлов 
											# и запись результатов в файл ansible.log

docker stop centos7 &&		# Остановка и удаление уонтейнера с именем centos7
docker stop fedore &&		# Аналогично для fedore
docker stop ubuntu &&		# Аналогично для ubuntu

docker ps		# Вывод на терминал контейнеров, которые запустились

```

Листинг файла ` ansible.log `
```ps
Tue 08 Feb 2022 12:41:34 PM UTC

PLAY [Print os facts] **********************************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]
ok: [fedore]
ok: [ubuntu]
ok: [centos7]

TASK [Print OS] ****************************************************************
ok: [localhost] => {
    "msg": "Ubuntu"
}
ok: [centos7] => {
    "msg": "CentOS"
}
ok: [ubuntu] => {
    "msg": "Ubuntu"
}
ok: [fedore] => {
    "msg": "Fedora"
}

TASK [Print fact] **************************************************************
ok: [localhost] => {
    "msg": "PaSSw0rd"
}
ok: [centos7] => {
    "msg": "el default fact"
}
ok: [ubuntu] => {
    "msg": "deb default fact"
}
ok: [fedore] => {
    "msg": "fed default fact"
}

PLAY RECAP *********************************************************************
centos7                    : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
fedore                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
localhost                  : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   


```

6. Все изменения должны быть зафиксированы и отправлены в вашей личный репозиторий.

**Ответ:**
Измененный ` playbook ` отправлен в репозиторий [Ansible-netology](https://github.com/zakharovnpa/Ansible-netology)

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
