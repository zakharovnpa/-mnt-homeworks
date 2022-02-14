```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook -i inventory/4-prod.yml 4-site.yml --check -vvv
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
host_list declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/4-prod.yml as it did not pass its verify_file() method
script declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/4-prod.yml as it did not pass its verify_file() method
Parsed /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/4-prod.yml inventory source with yaml plugin
Skipping callback 'default', as we already have a stdout callback.
Skipping callback 'minimal', as we already have a stdout callback.
Skipping callback 'oneline', as we already have a stdout callback.

PLAYBOOK: 4-site.yml *****************************************************************************************************************************************************************************************
1 plays in 4-site.yml

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/4-site.yml:2
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941 `" && echo ansible-tmp-1644759912.2022412-54769-34476908806941="` echo /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941 `" ) && sleep 0\'']
<ubuntu> Attempting python interpreter discovery
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3.6 && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-54764ulspjw2h/tmpd062cbpy TO /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941/AnsiballZ_setup.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941/ /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644759912.2022412-54769-34476908806941/ > /dev/null 2>&1 && sleep 0'"]
ok: [ubuntu]
[ubuntu] TASK: Gathering Facts (debug)> p task.args
{'gather_subset': ['all'], 'gather_timeout': 10}
[ubuntu] TASK: Gathering Facts (debug)> c
META: ran handlers

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/4-site.yml:6
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
ok: [ubuntu] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}
[ubuntu] TASK: Set facts for Java 11 vars (debug)> p task.args
{'java_home': '/opt/jdk/11.0.14'}
[ubuntu] TASK: Set facts for Java 11 vars (debug)> c

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/4-site.yml:10
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272 `" && echo ansible-tmp-1644760000.3441153-55034-132028915601272="` echo /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-54764ulspjw2h/tmpk_a7soaa TO /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272/ /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644760000.3441153-55034-132028915601272/ > /dev/null 2>&1 && sleep 0'"]
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
[ubuntu] TASK: Upload .tar.gz file containing binaries from local storage (debug)> p task.args
{'dest': '/tmp/jdk-11.0.14.tar.gz',
 'mode': 493,
 'src': 'jdk-11.0.14_linux-x64_bin.tar.gz'}
[ubuntu] TASK: Upload .tar.gz file containing binaries from local storage (debug)> c

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/4-site.yml:18
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971 `" && echo ansible-tmp-1644760102.1834598-55203-206685477522971="` echo /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-54764ulspjw2h/tmps686_tv8 TO /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/AnsiballZ_file.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/ /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-lnpywciewoewaqwvvyriuvnubvagbyvy ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/ > /dev/null 2>&1 && sleep 0'"]
changed: [ubuntu] => {
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
 '_ansible_tmpdir': '/root/.ansible/tmp/ansible-tmp-1644760102.1834598-55203-206685477522971/',
 '_ansible_verbosity': 3,
 '_ansible_version': '2.12.2',
 'path': '/opt/jdk/11.0.14',
 'state': 'directory'}
[ubuntu] TASK: Ensure installation dir exists (debug)> c

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/4-site.yml:24
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628 `" && echo ansible-tmp-1644760135.7167094-55378-153206419318628="` echo /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-yvshauzzctifrxcmhbcvknenieqqzzzl ; test -e /opt/jdk/11.0.14/bin/java\'"\'"\' && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-54764ulspjw2h/tmpltf3bb1i TO /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628/ /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-jgegyknjzufxmumpuvmeiyzexsaustkr ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644760135.7167094-55378-153206419318628/ > /dev/null 2>&1 && sleep 0'"]
The full traceback is:
NoneType: None
fatal: [ubuntu]: FAILED! => {
    "changed": false,
    "msg": "dest '/opt/jdk/11.0.14' must be an existing dir"
}
[ubuntu] TASK: Extract java in the installation directory (debug)> p task.args
{'creates': '/opt/jdk/11.0.14/bin/java',
 'dest': '/opt/jdk/11.0.14',
 'extra_opts': ['--strip-components=1'],
 'mode': 493,
 'remote_src': True,
 'src': '/tmp/jdk-11.0.14.tar.gz'}
[ubuntu] TASK: Extract java in the installation directory (debug)> 
{'creates': '/opt/jdk/11.0.14/bin/java',
 'dest': '/opt/jdk/11.0.14',
 'extra_opts': ['--strip-components=1'],
 'mode': 493,
 'remote_src': True,
 'src': '/tmp/jdk-11.0.14.tar.gz'}
[ubuntu] TASK: Extract java in the installation directory (debug)> c

PLAY RECAP ***************************************************************************************************************************************************************************************************
ubuntu                     : ok=4    changed=2    unreachable=0    failed=1    skipped=0    rescued=0    ignored=0   
```
