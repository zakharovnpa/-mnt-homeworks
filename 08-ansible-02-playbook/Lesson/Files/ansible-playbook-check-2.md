```yml
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/2-prod.yml 2-site.yml --check

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
ok: [localhost]
[localhost] TASK: Gathering Facts (debug)> c
ok: [fedore]
ok: [ubuntu]
ok: [centos7]
[fedore] TASK: Gathering Facts (debug)> c
[ubuntu] TASK: Gathering Facts (debug)> c
[centos7] TASK: Gathering Facts (debug)> c

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
ok: [localhost]
[localhost] TASK: Set facts for Java 11 vars (debug)> c
ok: [centos7]
ok: [ubuntu]
ok: [fedore]
[centos7] TASK: Set facts for Java 11 vars (debug)> c
[ubuntu] TASK: Set facts for Java 11 vars (debug)> c
[fedore] TASK: Set facts for Java 11 vars (debug)> c

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
changed: [localhost]
[localhost] TASK: Upload .tar.gz file containing binaries from local storage (debug)> p task.args
{'dest': '/tmp/jdk-11.0.14.tar.gz',
 'mode': 493,
 'src': 'jdk-11.0.14_linux-x64_bin.tar.gz'}
[localhost] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c
changed: [ubuntu]
changed: [centos7]
changed: [fedore]
[ubuntu] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c
[centos7] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c
[fedore] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
changed: [localhost]
[localhost] TASK: Ensure installation dir exists (debug)> p task.args
{'_ansible_check_mode': True,
 '_ansible_debug': False,
 '_ansible_diff': False,
 '_ansible_keep_remote_files': False,
 '_ansible_module_name': 'file',
 '_ansible_no_log': False,
 '_ansible_remote_tmp': '~/.ansible/tmp',
 '_ansible_selinux_special_fs': ['fuse',
                                 'nfs',
                                 'vboxsf',
                                 'ramfs',
                                 '9p',
                                 'vfat'],
 '_ansible_shell_executable': '/bin/sh',
 '_ansible_socket': None,
 '_ansible_string_conversion_action': 'warn',
 '_ansible_syslog_facility': 'LOG_USER',
 '_ansible_tmpdir': '/root/.ansible/tmp/ansible-tmp-1644686532.3898444-38779-250307114659073/',
 '_ansible_verbosity': 0,
 '_ansible_version': '2.12.2',
 'path': '/opt/jdk/11.0.14',
 'state': 'directory'}
[localhost] TASK: Ensure installation dir exists (debug)> c
fatal: [centos7]: FAILED! => {"changed": false, "module_stderr": "/bin/sh: sudo: command not found\n", "module_stdout": "", "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error", "rc": 127}
ok: [ubuntu]
ok: [fedore]
[centos7] TASK: Ensure installation dir exists (debug)> p task.args
{'_ansible_check_mode': True,
 '_ansible_debug': False,
 '_ansible_diff': False,
 '_ansible_keep_remote_files': False,
 '_ansible_module_name': 'file',
 '_ansible_no_log': False,
 '_ansible_remote_tmp': '~/.ansible/tmp',
 '_ansible_selinux_special_fs': ['fuse',
                                 'nfs',
                                 'vboxsf',
                                 'ramfs',
                                 '9p',
                                 'vfat'],
 '_ansible_shell_executable': '/bin/sh',
 '_ansible_socket': None,
 '_ansible_string_conversion_action': 'warn',
 '_ansible_syslog_facility': 'LOG_USER',
 '_ansible_tmpdir': '/root/.ansible/tmp/ansible-tmp-1644686533.4941983-38776-61199116806871/',
 '_ansible_verbosity': 0,
 '_ansible_version': '2.12.2',
 'path': '/opt/jdk/11.0.14',
 'state': 'directory'}
[centos7] TASK: Ensure installation dir exists (debug)> c
[ubuntu] TASK: Ensure installation dir exists (debug)> p task.args
{'_ansible_check_mode': True,
 '_ansible_debug': False,
 '_ansible_diff': False,
 '_ansible_keep_remote_files': False,
 '_ansible_module_name': 'file',
 '_ansible_no_log': False,
 '_ansible_remote_tmp': '~/.ansible/tmp',
 '_ansible_selinux_special_fs': ['fuse',
                                 'nfs',
                                 'vboxsf',
                                 'ramfs',
                                 '9p',
                                 'vfat'],
 '_ansible_shell_executable': '/bin/sh',
 '_ansible_socket': None,
 '_ansible_string_conversion_action': 'warn',
 '_ansible_syslog_facility': 'LOG_USER',
 '_ansible_tmpdir': '/root/.ansible/tmp/ansible-tmp-1644686533.7043788-38777-558683818389/',
 '_ansible_verbosity': 0,
 '_ansible_version': '2.12.2',
 'path': '/opt/jdk/11.0.14',
 'state': 'directory'}
[ubuntu] TASK: Ensure installation dir exists (debug)> c
[fedore] TASK: Ensure installation dir exists (debug)> c

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
An exception occurred during task execution. To see the full traceback, use -vvv. The error was: NoneType: None
fatal: [localhost]: FAILED! => {"changed": false, "msg": "dest '/opt/jdk/11.0.14' must be an existing dir"}
[localhost] TASK: Extract java in the installation directory (debug)> p task.args
{'creates': '/opt/jdk/11.0.14/bin/java',
 'dest': '/opt/jdk/11.0.14',
 'extra_opts': ['--strip-components=1'],
 'mode': 493,
 'remote_src': True,
 'src': '/tmp/jdk-11.0.14.tar.gz'}
[localhost] TASK: Extract java in the installation directory (debug)> c
fatal: [ubuntu]: FAILED! => {"changed": false, "msg": "Source '/tmp/jdk-11.0.14.tar.gz' does not exist"}
fatal: [fedore]: FAILED! => {"changed": false, "msg": "Source '/tmp/jdk-11.0.14.tar.gz' does not exist"}
[ubuntu] TASK: Extract java in the installation directory (debug)> c
[fedore] TASK: Extract java in the installation directory (debug)> c

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
fedore                     : ok=4    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
localhost                  : ok=4    changed=2    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=4    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0 
```

```yml
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/2-prod.yml 2-site.yml --check -vvv
ansible-playbook [core 2.12.2]
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.8/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible-playbook
  python version = 3.8.10 (default, Nov 26 2021, 20:14:08) [GCC 9.3.0]
  jinja version = 3.0.3
  libyaml = True
No config file found; using defaults
host_list declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/2-prod.yml as it did not pass its verify_file() method
script declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/2-prod.yml as it did not pass its verify_file() method
Parsed /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/2-prod.yml inventory source with yaml plugin
Skipping callback 'default', as we already have a stdout callback.
Skipping callback 'minimal', as we already have a stdout callback.
Skipping callback 'oneline', as we already have a stdout callback.

PLAYBOOK: 2-site.yml *****************************************************************************************************************************************************************************************
1 plays in 2-site.yml

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/2-site.yml:2
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> ESTABLISH LOCAL CONNECTION FOR USER: root
<localhost> EXEC /bin/sh -c 'echo ~root && sleep 0'
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221 `" && echo ansible-tmp-1644686688.700845-39822-102570616653221="` echo /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221 `" ) && sleep 0'
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<fedore> ESTABLISH DOCKER CONNECTION FOR USER: root
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866 `" && echo ansible-tmp-1644686690.2889497-39819-44040197944866="` echo /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653 `" && echo ansible-tmp-1644686690.4250004-39820-119146005043653="` echo /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653 `" ) && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734 `" && echo ansible-tmp-1644686690.6770215-39824-45950093982734="` echo /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734 `" ) && sleep 0\'']
<centos7> Attempting python interpreter discovery
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<ubuntu> Attempting python interpreter discovery
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<fedore> Attempting python interpreter discovery
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<localhost> Attempting python interpreter discovery
<localhost> EXEC /bin/sh -c 'echo PLATFORM; uname; echo FOUND; command -v '"'"'python3.10'"'"'; command -v '"'"'python3.9'"'"'; command -v '"'"'python3.8'"'"'; command -v '"'"'python3.7'"'"'; command -v '"'"'python3.6'"'"'; command -v '"'"'python3.5'"'"'; command -v '"'"'/usr/bin/python3'"'"'; command -v '"'"'/usr/libexec/platform-python'"'"'; command -v '"'"'python2.7'"'"'; command -v '"'"'python2.6'"'"'; command -v '"'"'/usr/bin/python'"'"'; command -v '"'"'python'"'"'; echo ENDFOUND && sleep 0'
<localhost> EXEC /bin/sh -c '/usr/bin/python3.8 && sleep 0'
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<localhost> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpq3vs6v6w TO /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221/AnsiballZ_setup.py
<localhost> EXEC /bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221/ /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221/AnsiballZ_setup.py && sleep 0'
<localhost> EXEC /bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221/AnsiballZ_setup.py && sleep 0'
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3.6 && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/libexec/platform-python && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3.9 && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<centos7> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmp3_n9ww4g TO /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866/AnsiballZ_setup.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<fedore> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpp1p6za3r TO /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734/AnsiballZ_setup.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpo_xbdcog TO /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653/AnsiballZ_setup.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866/ /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653/ /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653/AnsiballZ_setup.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734/ /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734/AnsiballZ_setup.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653/AnsiballZ_setup.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734/AnsiballZ_setup.py && sleep 0'"]
<localhost> EXEC /bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686688.700845-39822-102570616653221/ > /dev/null 2>&1 && sleep 0'
ok: [localhost]
[localhost] TASK: Gathering Facts (debug)> <fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686690.6770215-39824-45950093982734/ > /dev/null 2>&1 && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686690.4250004-39820-119146005043653/ > /dev/null 2>&1 && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686690.2889497-39819-44040197944866/ > /dev/null 2>&1 && sleep 0'"]
c
ok: [fedore]
ok: [ubuntu]
ok: [centos7]
[fedore] TASK: Gathering Facts (debug)> c
[ubuntu] TASK: Gathering Facts (debug)> c
[centos7] TASK: Gathering Facts (debug)> c
META: ran handlers

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/2-site.yml:6
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
ok: [localhost] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}
[localhost] TASK: Set facts for Java 11 vars (debug)> redirecting (type: connection) ansible.builtin.docker to community.docker.docker
c
ok: [centos7] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}
ok: [ubuntu] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}
ok: [fedore] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}
[centos7] TASK: Set facts for Java 11 vars (debug)> c
[ubuntu] TASK: Set facts for Java 11 vars (debug)> c
[fedore] TASK: Set facts for Java 11 vars (debug)> c

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/2-site.yml:10
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> ESTABLISH LOCAL CONNECTION FOR USER: root
<localhost> EXEC /bin/sh -c 'echo ~root && sleep 0'
<localhost> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912 `" && echo ansible-tmp-1644686749.6063225-40681-79251447592912="` echo /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912 `" ) && sleep 0'
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<fedore> ESTABLISH DOCKER CONNECTION FOR USER: root
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109 `" && echo ansible-tmp-1644686750.9935234-40678-89580803126109="` echo /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799 `" && echo ansible-tmp-1644686751.2508042-40679-191467470672799="` echo /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799 `" ) && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383 `" && echo ansible-tmp-1644686751.5420136-40685-169063099035383="` echo /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<centos7> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmphvnapabi TO /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109/AnsiballZ_stat.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<localhost> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpk8vb14jc TO /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912/AnsiballZ_stat.py
<localhost> EXEC /bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912/ /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912/AnsiballZ_stat.py && sleep 0'
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<localhost> EXEC /bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912/AnsiballZ_stat.py && sleep 0'
<ubuntu> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmp66ymlpw5 TO /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799/AnsiballZ_stat.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<fedore> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpht1oxnes TO /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383/AnsiballZ_stat.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109/ /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799/ /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799/AnsiballZ_stat.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383/ /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383/AnsiballZ_stat.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799/AnsiballZ_stat.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383/AnsiballZ_stat.py && sleep 0'"]
<localhost> EXEC /bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686749.6063225-40681-79251447592912/ > /dev/null 2>&1 && sleep 0'
changed: [localhost] => {
    "attempts": 1,
    "changed": true,
    "diff": [],
    "invocation": {
        "dest": "/tmp/jdk-11.0.14.tar.gz",
        "mode": 493,
        "module_args": {
            "dest": "/tmp/jdk-11.0.14.tar.gz",
            "mode": 493,
            "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
        },
        "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
    }
}
[localhost] TASK: Upload .tar.gz file containing binaries from local storage (debug)> <centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686750.9935234-40678-89580803126109/ > /dev/null 2>&1 && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686751.2508042-40679-191467470672799/ > /dev/null 2>&1 && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686751.5420136-40685-169063099035383/ > /dev/null 2>&1 && sleep 0'"]
c
changed: [centos7] => {
    "attempts": 1,
    "changed": true,
    "diff": [],
    "invocation": {
        "dest": "/tmp/jdk-11.0.14.tar.gz",
        "mode": 493,
        "module_args": {
            "dest": "/tmp/jdk-11.0.14.tar.gz",
            "mode": 493,
            "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
        },
        "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
    }
}
changed: [ubuntu] => {
    "attempts": 1,
    "changed": true,
    "diff": [],
    "invocation": {
        "dest": "/tmp/jdk-11.0.14.tar.gz",
        "mode": 493,
        "module_args": {
            "dest": "/tmp/jdk-11.0.14.tar.gz",
            "mode": 493,
            "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
        },
        "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
    }
}
changed: [fedore] => {
    "attempts": 1,
    "changed": true,
    "diff": [],
    "invocation": {
        "dest": "/tmp/jdk-11.0.14.tar.gz",
        "mode": 493,
        "module_args": {
            "dest": "/tmp/jdk-11.0.14.tar.gz",
            "mode": 493,
            "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
        },
        "src": "jdk-11.0.14_linux-x64_bin.tar.gz"
    }
}
[centos7] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c
[ubuntu] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c
[fedore] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/2-site.yml:18
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> ESTABLISH LOCAL CONNECTION FOR USER: root
<localhost> EXEC /bin/sh -c 'echo ~root && sleep 0'
<localhost> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992 `" && echo ansible-tmp-1644686798.0016875-41196-22417957810992="` echo /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992 `" ) && sleep 0'
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<fedore> ESTABLISH DOCKER CONNECTION FOR USER: root
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069 `" && echo ansible-tmp-1644686799.3894074-41193-189882934325069="` echo /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948 `" && echo ansible-tmp-1644686799.5928528-41194-94798894181948="` echo /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948 `" ) && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908 `" && echo ansible-tmp-1644686799.9076934-41201-257906210255908="` echo /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<centos7> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpktjfewsz TO /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069/AnsiballZ_file.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<localhost> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpo5n84pqw TO /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992/AnsiballZ_file.py
<localhost> EXEC /bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992/ /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992/AnsiballZ_file.py && sleep 0'
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpf7dx9wve TO /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948/AnsiballZ_file.py
<localhost> EXEC /bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992/AnsiballZ_file.py && sleep 0'
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<fedore> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmplsvbuopt TO /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908/AnsiballZ_file.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069/ /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948/ /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948/AnsiballZ_file.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908/ /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908/AnsiballZ_file.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-saunmxsdvpiwqouligagkrgattqdwvvh ; /usr/bin/python /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-cksujrgtxzqidshtpyoowfnolpivpmvz ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-phyhvgzridvboczxaarqhgkaokgliuxd ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686799.3894074-41193-189882934325069/ > /dev/null 2>&1 && sleep 0'"]
<localhost> EXEC /bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686798.0016875-41196-22417957810992/ > /dev/null 2>&1 && sleep 0'
changed: [localhost] => {
    "changed": true,
    "diff": {
        "after": {
            "path": "/opt/jdk/11.0.14",
            "state": "directory"
        },
        "before": {
            "path": "/opt/jdk/11.0.14",
            "state": "absent"
        }
    },
    "invocation": {
        "module_args": {
            "_diff_peek": null,
            "_original_basename": null,
            "access_time": null,
            "access_time_format": "%Y%m%d%H%M.%S",
            "attributes": null,
            "follow": true,
            "force": false,
            "group": null,
            "mode": null,
            "modification_time": null,
            "modification_time_format": "%Y%m%d%H%M.%S",
            "owner": null,
            "path": "/opt/jdk/11.0.14",
            "recurse": false,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": null,
            "state": "directory",
            "unsafe_writes": false
        }
    },
    "path": "/opt/jdk/11.0.14"
}
[localhost] TASK: Ensure installation dir exists (debug)> <ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686799.5928528-41194-94798894181948/ > /dev/null 2>&1 && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686799.9076934-41201-257906210255908/ > /dev/null 2>&1 && sleep 0'"]
c
fatal: [centos7]: FAILED! => {
    "changed": false,
    "module_stderr": "/bin/sh: sudo: command not found\n",
    "module_stdout": "",
    "msg": "MODULE FAILURE\nSee stdout/stderr for the exact error",
    "rc": 127
}
ok: [ubuntu] => {
    "changed": false,
    "diff": {
        "after": {
            "path": "/opt/jdk/11.0.14"
        },
        "before": {
            "path": "/opt/jdk/11.0.14"
        }
    },
    "gid": 0,
    "group": "root",
    "invocation": {
        "module_args": {
            "_diff_peek": null,
            "_original_basename": null,
            "access_time": null,
            "access_time_format": "%Y%m%d%H%M.%S",
            "attributes": null,
            "follow": true,
            "force": false,
            "group": null,
            "mode": null,
            "modification_time": null,
            "modification_time_format": "%Y%m%d%H%M.%S",
            "owner": null,
            "path": "/opt/jdk/11.0.14",
            "recurse": false,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": null,
            "state": "directory",
            "unsafe_writes": false
        }
    },
    "mode": "0755",
    "owner": "root",
    "path": "/opt/jdk/11.0.14",
    "size": 4096,
    "state": "directory",
    "uid": 0
}
ok: [fedore] => {
    "changed": false,
    "diff": {
        "after": {
            "path": "/opt/jdk/11.0.14"
        },
        "before": {
            "path": "/opt/jdk/11.0.14"
        }
    },
    "gid": 0,
    "group": "root",
    "invocation": {
        "module_args": {
            "_diff_peek": null,
            "_original_basename": null,
            "access_time": null,
            "access_time_format": "%Y%m%d%H%M.%S",
            "attributes": null,
            "follow": true,
            "force": false,
            "group": null,
            "mode": null,
            "modification_time": null,
            "modification_time_format": "%Y%m%d%H%M.%S",
            "owner": null,
            "path": "/opt/jdk/11.0.14",
            "recurse": false,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": null,
            "state": "directory",
            "unsafe_writes": false
        }
    },
    "mode": "0755",
    "owner": "root",
    "path": "/opt/jdk/11.0.14",
    "size": 4096,
    "state": "directory",
    "uid": 0
}
[centos7] TASK: Ensure installation dir exists (debug)> c
[ubuntu] TASK: Ensure installation dir exists (debug)> c
[fedore] TASK: Ensure installation dir exists (debug)> c

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/2-site.yml:24
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> ESTABLISH LOCAL CONNECTION FOR USER: root
<localhost> EXEC /bin/sh -c 'echo ~root && sleep 0'
<localhost> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134 `" && echo ansible-tmp-1644686817.403411-41706-237112861451134="` echo /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134 `" ) && sleep 0'
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<localhost> EXEC /bin/sh -c 'test -e /opt/jdk/11.0.14/bin/java && sleep 0'
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<localhost> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpvrqbyah2 TO /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134/AnsiballZ_stat.py
<localhost> EXEC /bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134/ /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134/AnsiballZ_stat.py && sleep 0'
<localhost> EXEC /bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134/AnsiballZ_stat.py && sleep 0'
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<fedore> ESTABLISH DOCKER CONNECTION FOR USER: root
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403 `" && echo ansible-tmp-1644686818.5003085-41705-212581237012403="` echo /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403 `" ) && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058 `" && echo ansible-tmp-1644686818.777704-41708-261991294084058="` echo /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-xvsdxagumqoyfppxcwhjddfnmeedughh ; test -e /opt/jdk/11.0.14/bin/java\'"\'"\' && sleep 0\'']
<localhost> EXEC /bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686817.403411-41706-237112861451134/ > /dev/null 2>&1 && sleep 0'
The full traceback is:
NoneType: None
fatal: [localhost]: FAILED! => {
    "changed": false,
    "msg": "dest '/opt/jdk/11.0.14' must be an existing dir"
}
[localhost] TASK: Extract java in the installation directory (debug)> <fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-xhkmvqegeqxjvdlskfmpoezshciciqgy ; test -e /opt/jdk/11.0.14/bin/java\'"\'"\' && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpg3grvcmh TO /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_stat.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<fedore> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpmfnk3b6e TO /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/ /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_stat.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/ /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-gvdcibfpztkonsybsqgyypwddxnkrkqq ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-iidaeitafykjmcuzkuminwkzuinrsnwm ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/unarchive.py
<fedore> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmpm6fr1_4y TO /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_unarchive.py
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/unarchive.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-39814_amz8l1v/tmp4y63_gsd TO /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_unarchive.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/ /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_unarchive.py && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/ /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_unarchive.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-ewwrooitfcilgmnksvwljynmzpeegglc ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/AnsiballZ_unarchive.py\'"\'"\' && sleep 0\'']
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-pjoajiuehrcpkbrthlewriyqrstfftnm ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/AnsiballZ_unarchive.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686818.5003085-41705-212581237012403/ > /dev/null 2>&1 && sleep 0'"]
<fedore> EXEC ['/usr/bin/docker', b'exec', b'-i', 'fedore', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644686818.777704-41708-261991294084058/ > /dev/null 2>&1 && sleep 0'"]
c
fatal: [ubuntu]: FAILED! => {
    "changed": false,
    "invocation": {
        "module_args": {
            "attributes": null,
            "creates": "/opt/jdk/11.0.14/bin/java",
            "dest": "/opt/jdk/11.0.14",
            "exclude": [],
            "extra_opts": [
                "--strip-components=1"
            ],
            "group": null,
            "include": [],
            "keep_newer": false,
            "list_files": false,
            "mode": 493,
            "owner": null,
            "remote_src": true,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": "/tmp/jdk-11.0.14.tar.gz",
            "unsafe_writes": false,
            "validate_certs": true
        }
    },
    "msg": "Source '/tmp/jdk-11.0.14.tar.gz' does not exist"
}
fatal: [fedore]: FAILED! => {
    "changed": false,
    "invocation": {
        "module_args": {
            "attributes": null,
            "creates": "/opt/jdk/11.0.14/bin/java",
            "dest": "/opt/jdk/11.0.14",
            "exclude": [],
            "extra_opts": [
                "--strip-components=1"
            ],
            "group": null,
            "include": [],
            "keep_newer": false,
            "list_files": false,
            "mode": 493,
            "owner": null,
            "remote_src": true,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": "/tmp/jdk-11.0.14.tar.gz",
            "unsafe_writes": false,
            "validate_certs": true
        }
    },
    "msg": "Source '/tmp/jdk-11.0.14.tar.gz' does not exist"
}
[ubuntu] TASK: Extract java in the installation directory (debug)> c
[fedore] TASK: Extract java in the installation directory (debug)> c

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=3    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
fedore                     : ok=4    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
localhost                  : ok=4    changed=2    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
ubuntu                     : ok=4    changed=1    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   



```
