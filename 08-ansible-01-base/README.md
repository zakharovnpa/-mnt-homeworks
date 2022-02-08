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

9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.

**Ответ:**

10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.

**Ответ:**

11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь что факты `some_fact` для каждого из хостов определены из верных `group_vars`.

**Ответ:**

12. Заполните `README.md` ответами на вопросы. Сделайте `git push` в ветку `master`. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым `playbook` и заполненным `README.md`.

## Необязательная часть

1. При помощи `ansible-vault` расшифруйте все зашифрованные файлы с переменными.

**Ответ:**

2. Зашифруйте отдельное значение `PaSSw0rd` для переменной `some_fact` паролем `netology`. Добавьте полученное значение в `group_vars/all/exmp.yml`.

**Ответ:**

3. Запустите `playbook`, убедитесь, что для нужных хостов применился новый `fact`.

**Ответ:**

4. Добавьте новую группу хостов `fedora`, самостоятельно придумайте для неё переменную. В качестве образа можно использовать [этот](https://hub.docker.com/r/pycontribs/fedora).

**Ответ:**

5. Напишите скрипт на bash: автоматизируйте поднятие необходимых контейнеров, запуск ansible-playbook и остановку контейнеров.

**Ответ:**

6. Все изменения должны быть зафиксированы и отправлены в вашей личный репозиторий.

**Ответ:**

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
