```sh
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/3-prod.yml 3-site.yml --check -vvv
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
host_list declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/3-prod.yml as it did not pass its verify_file() method
script declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/3-prod.yml as it did not pass its verify_file() method
Parsed /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/3-prod.yml inventory source with yaml plugin
Skipping callback 'default', as we already have a stdout callback.
Skipping callback 'minimal', as we already have a stdout callback.
Skipping callback 'oneline', as we already have a stdout callback.

PLAYBOOK: 3-site.yml *****************************************************************************************************************************************************************************************
1 plays in 3-site.yml

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:2
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316 `" && echo ansible-tmp-1644758622.096062-53578-204979228459316="` echo /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316 `" ) && sleep 0\'']
<centos7> Attempting python interpreter discovery
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/libexec/platform-python && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<centos7> PUT /root/.ansible/tmp/ansible-local-53573tan_02z9/tmpb6067oxo TO /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316/AnsiballZ_setup.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316/ /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316/AnsiballZ_setup.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316/AnsiballZ_setup.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644758622.096062-53578-204979228459316/ > /dev/null 2>&1 && sleep 0'"]
ok: [centos7]
META: ran handlers

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:6
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
ok: [centos7] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:10
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078 `" && echo ansible-tmp-1644758627.245597-53830-35668284863078="` echo /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<centos7> PUT /root/.ansible/tmp/ansible-local-53573tan_02z9/tmpno3ai0ra TO /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_stat.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/ /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_stat.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_stat.py && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<centos7> PUT /root/.ansible/tmp/ansible-local-53573tan_02z9/tmp3jits2ys TO /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_file.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/ /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_file.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/AnsiballZ_file.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644758627.245597-53830-35668284863078/ > /dev/null 2>&1 && sleep 0'"]
ok: [centos7] => {
    "attempts": 1,
    "changed": false,
    "checksum": "8d114682158f9849e289ffc7b39a5b03f5558468",
    "dest": "/tmp/jdk-11.0.14.tar.gz",
    "diff": {
        "after": {
            "path": "/tmp/jdk-11.0.14.tar.gz"
        },
        "before": {
            "path": "/tmp/jdk-11.0.14.tar.gz"
        }
    },
    "gid": 0,
    "group": "root",
    "invocation": {
        "module_args": {
            "_diff_peek": null,
            "_original_basename": "jdk-11.0.14_linux-x64_bin.tar.gz",
            "access_time": null,
            "access_time_format": "%Y%m%d%H%M.%S",
            "attributes": null,
            "dest": "/tmp/jdk-11.0.14.tar.gz",
            "follow": true,
            "force": false,
            "group": null,
            "mode": 493,
            "modification_time": null,
            "modification_time_format": "%Y%m%d%H%M.%S",
            "owner": null,
            "path": "/tmp/jdk-11.0.14.tar.gz",
            "recurse": false,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "src": null,
            "state": "file",
            "unsafe_writes": false
        }
    },
    "mode": "0755",
    "owner": "root",
    "path": "/tmp/jdk-11.0.14.tar.gz",
    "size": 168679847,
    "state": "file",
    "uid": 0
}

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:18
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100 `" && echo ansible-tmp-1644758631.9378018-54054-137683124887100="` echo /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<centos7> PUT /root/.ansible/tmp/ansible-local-53573tan_02z9/tmpg_9br25y TO /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100/AnsiballZ_file.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100/ /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100/AnsiballZ_file.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100/AnsiballZ_file.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644758631.9378018-54054-137683124887100/ > /dev/null 2>&1 && sleep 0'"]
ok: [centos7] => {
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

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:24
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644758634.1425576-54215-237620428601234 `" && echo ansible-tmp-1644758634.1425576-54215-237620428601234="` echo /root/.ansible/tmp/ansible-tmp-1644758634.1425576-54215-237620428601234 `" ) && sleep 0\'']
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'test -e /opt/jdk/11.0.14/bin/java && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644758634.1425576-54215-237620428601234/ > /dev/null 2>&1 && sleep 0'"]
skipping: [centos7] => {
    "changed": false,
    "msg": "skipped, since /opt/jdk/11.0.14/bin/java exists"
}

TASK [Export environment variables] **************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/3-site.yml:35
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<centos7> ESTABLISH DOCKER CONNECTION FOR USER: root
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958 `" && echo ansible-tmp-1644758635.3480165-54334-194894850370958="` echo /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<centos7> PUT /root/.ansible/tmp/ansible-local-53573tan_02z9/tmp9jmui28o TO /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958/AnsiballZ_stat.py
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958/ /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958/AnsiballZ_stat.py && sleep 0'"]
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-uaudlfucthhaqsrgygohqodmzvywbusg ; /usr/bin/python /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
<centos7> EXEC ['/usr/bin/docker', b'exec', b'-i', 'centos7', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644758635.3480165-54334-194894850370958/ > /dev/null 2>&1 && sleep 0'"]
fatal: [centos7]: FAILED! => {
    "msg": "Failed to get information on remote file (/etc/profile.d/jdk.sh): /bin/sh: sudo: command not found\n"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
centos7                    : ok=4    changed=0    unreachable=0    failed=1    skipped=1    rescued=0    ignored=0  
```
