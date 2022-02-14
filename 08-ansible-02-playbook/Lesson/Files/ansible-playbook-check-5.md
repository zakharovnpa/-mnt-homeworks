```ps
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-playbook 5-site.yml -i inventory/5-prod.yml --check -vvv
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
host_list declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/5-prod.yml as it did not pass its verify_file() method
script declined parsing /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/5-prod.yml as it did not pass its verify_file() method
Parsed /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/inventory/5-prod.yml inventory source with yaml plugin
Skipping callback 'default', as we already have a stdout callback.
Skipping callback 'minimal', as we already have a stdout callback.
Skipping callback 'oneline', as we already have a stdout callback.

PLAYBOOK: 5-site.yml *****************************************************************************************************************************************************************************************
2 plays in 5-site.yml

PLAY [Install Java] ******************************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:2
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265 `" && echo ansible-tmp-1644806577.0461833-62173-214741144864265="` echo /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265 `" ) && sleep 0\'']
<ubuntu> Attempting python interpreter discovery
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'echo PLATFORM; uname; echo FOUND; command -v \'"\'"\'python3.10\'"\'"\'; command -v \'"\'"\'python3.9\'"\'"\'; command -v \'"\'"\'python3.8\'"\'"\'; command -v \'"\'"\'python3.7\'"\'"\'; command -v \'"\'"\'python3.6\'"\'"\'; command -v \'"\'"\'python3.5\'"\'"\'; command -v \'"\'"\'/usr/bin/python3\'"\'"\'; command -v \'"\'"\'/usr/libexec/platform-python\'"\'"\'; command -v \'"\'"\'python2.7\'"\'"\'; command -v \'"\'"\'python2.6\'"\'"\'; command -v \'"\'"\'/usr/bin/python\'"\'"\'; command -v \'"\'"\'python\'"\'"\'; echo ENDFOUND && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3.6 && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpowh00mc0 TO /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265/AnsiballZ_setup.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265/ /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806577.0461833-62173-214741144864265/ > /dev/null 2>&1 && sleep 0'"]
ok: [ubuntu]
META: ran handlers

TASK [Set facts for Java 11 vars] ****************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:6
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
ok: [ubuntu] => {
    "ansible_facts": {
        "java_home": "/opt/jdk/11.0.14"
    },
    "changed": false
}

TASK [Upload .tar.gz file containing binaries from local storage] ********************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:10
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537 `" && echo ansible-tmp-1644806581.1891565-62432-28791105999537="` echo /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmp2_js1ffb TO /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/ /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_stat.py && sleep 0'"]
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpmtfc1f7j TO /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_file.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/ /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806581.1891565-62432-28791105999537/ > /dev/null 2>&1 && sleep 0'"]
ok: [ubuntu] => {
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
            "mode": null,
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
    "mode": "0644",
    "owner": "root",
    "path": "/tmp/jdk-11.0.14.tar.gz",
    "size": 168679847,
    "state": "file",
    "uid": 0
}

TASK [Ensure installation dir exists] ************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:18
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393 `" && echo ansible-tmp-1644806586.0240912-62670-254553346651393="` echo /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpmju8cmj0 TO /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393/AnsiballZ_file.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393/ /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-rtedxepubxecbwlkrkipmraosksyebmn ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806586.0240912-62670-254553346651393/ > /dev/null 2>&1 && sleep 0'"]
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

TASK [Extract java in the installation directory] ************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:24
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806588.335092-62843-166537947324662 `" && echo ansible-tmp-1644806588.335092-62843-166537947324662="` echo /root/.ansible/tmp/ansible-tmp-1644806588.335092-62843-166537947324662 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-rcvsndoazwhhnkyfjvscqchisggsnefq ; test -e /opt/jdk/11.0.14/bin/java\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806588.335092-62843-166537947324662/ > /dev/null 2>&1 && sleep 0'"]
skipping: [ubuntu] => {
    "changed": false,
    "msg": "skipped, since /opt/jdk/11.0.14/bin/java exists"
}

TASK [Export environment variables] **************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:35
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009 `" && echo ansible-tmp-1644806589.5737114-62969-153918710395009="` echo /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpqidm7kc_ TO /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/ /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-bwtuxqyaawabfvuoukdlegestwhgnvxe ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmp81hrvx4c TO /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_file.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/ /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-abdfcckqeqneorhwurhitqsgjhjepvjb ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/AnsiballZ_file.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806589.5737114-62969-153918710395009/ > /dev/null 2>&1 && sleep 0'"]
ok: [ubuntu] => {
    "changed": false,
    "checksum": "1bfb427e4e2b292bd03ad784d0b35096b20a6a9c",
    "dest": "/etc/profile.d/jdk.sh",
    "diff": {
        "after": {
            "path": "/etc/profile.d/jdk.sh"
        },
        "before": {
            "path": "/etc/profile.d/jdk.sh"
        }
    },
    "gid": 0,
    "group": "root",
    "invocation": {
        "module_args": {
            "_diff_peek": null,
            "_original_basename": "jdk.sh.j2",
            "access_time": null,
            "access_time_format": "%Y%m%d%H%M.%S",
            "attributes": null,
            "dest": "/etc/profile.d/jdk.sh",
            "follow": true,
            "force": false,
            "group": null,
            "mode": null,
            "modification_time": null,
            "modification_time_format": "%Y%m%d%H%M.%S",
            "owner": null,
            "path": "/etc/profile.d/jdk.sh",
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
    "mode": "0644",
    "owner": "root",
    "path": "/etc/profile.d/jdk.sh",
    "size": 186,
    "state": "file",
    "uid": 0
}
META: ran handlers
META: ran handlers

PLAY [Install Elasticsearch] *********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:42
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200 `" && echo ansible-tmp-1644806592.6861663-63213-52866114952200="` echo /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/setup.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpe2tj6dfj TO /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200/AnsiballZ_setup.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200/ /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200/AnsiballZ_setup.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806592.6861663-63213-52866114952200/ > /dev/null 2>&1 && sleep 0'"]
ok: [ubuntu]
META: ran handlers

TASK [Upload tar.gz Elasticsearch from remote URL] ***********************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:46
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415 `" && echo ansible-tmp-1644806595.498492-63398-4168010246415="` echo /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/get_url.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmps12umrf1 TO /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/AnsiballZ_get_url.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/ /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/AnsiballZ_get_url.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/AnsiballZ_get_url.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/ > /dev/null 2>&1 && sleep 0'"]
changed: [ubuntu] => {
    "attempts": 1,
    "changed": true,
    "checksum_dest": null,
    "checksum_src": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "dest": "/tmp/elasticsearch-7.10.1-linux-x86_64.tar.gz",
    "elapsed": 0,
    "invocation": {
        "module_args": {
            "attributes": null,
            "backup": false,
            "checksum": "",
            "client_cert": null,
            "client_key": null,
            "dest": "/tmp/elasticsearch-7.10.1-linux-x86_64.tar.gz",
            "force": true,
            "force_basic_auth": false,
            "group": null,
            "headers": null,
            "http_agent": "ansible-httpget",
            "mode": 493,
            "owner": null,
            "selevel": null,
            "serole": null,
            "setype": null,
            "seuser": null,
            "sha256sum": "",
            "timeout": 60,
            "tmp_dest": null,
            "unredirected_headers": [],
            "unsafe_writes": false,
            "url": "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.1-linux-x86_64.tar.gz",
            "url_password": null,
            "url_username": null,
            "use_gssapi": false,
            "use_proxy": true,
            "validate_certs": false
        }
    },
    "msg": "OK (318801277 bytes)",
    "src": "/root/.ansible/tmp/ansible-tmp-1644806595.498492-63398-4168010246415/tmpzbu9pude",
    "url": "https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.10.1-linux-x86_64.tar.gz"
}

TASK [Create directrory for Elasticsearch] *******************************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:57
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424 `" && echo ansible-tmp-1644806598.672579-63569-23131965212424="` echo /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424 `" ) && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/file.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpln0ho7np TO /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424/AnsiballZ_file.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424/ /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c '/usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424/AnsiballZ_file.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806598.672579-63569-23131965212424/ > /dev/null 2>&1 && sleep 0'"]
changed: [ubuntu] => {
    "changed": true,
    "diff": {
        "after": {
            "path": "/opt/elastic/7.10.1",
            "state": "directory"
        },
        "before": {
            "path": "/opt/elastic/7.10.1",
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
            "path": "/opt/elastic/7.10.1",
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
    "path": "/opt/elastic/7.10.1"
}

TASK [Extract Elasticsearch in the installation directory] ***************************************************************************************************************************************************
task path: /root/learning-ansible/Lesson-ansible-02/ansible-02-playbook/5-site.yml:62
redirecting (type: connection) ansible.builtin.docker to community.docker.docker
<ubuntu> ESTABLISH DOCKER CONNECTION FOR USER: root
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'echo ~ && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'( umask 77 && mkdir -p "` echo /root/.ansible/tmp `"&& mkdir "` echo /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526 `" && echo ansible-tmp-1644806600.5749075-63736-227612841799526="` echo /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526 `" ) && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-qwtfooyiimjbehdmpcmbgrqcwsplirzm ; test -e /opt/elastic/7.10.1/bin/elasticsearch\'"\'"\' && sleep 0\'']
Using module file /usr/local/lib/python3.8/dist-packages/ansible/modules/stat.py
<ubuntu> PUT /root/.ansible/tmp/ansible-local-62168hxax2bnp/tmpcqbbxh4k TO /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526/AnsiballZ_stat.py
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'chmod u+x /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526/ /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526/AnsiballZ_stat.py && sleep 0'"]
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', '/bin/sh -c \'sudo -H -S -n  -u root /bin/sh -c \'"\'"\'echo BECOME-SUCCESS-vdnsqbrtywizxejnjkoyduktfgfeqkwd ; /usr/bin/python3 /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526/AnsiballZ_stat.py\'"\'"\' && sleep 0\'']
<ubuntu> EXEC ['/usr/bin/docker', b'exec', b'-i', 'ubuntu', '/bin/sh', '-c', "/bin/sh -c 'rm -f -r /root/.ansible/tmp/ansible-tmp-1644806600.5749075-63736-227612841799526/ > /dev/null 2>&1 && sleep 0'"]
The full traceback is:
NoneType: None
fatal: [ubuntu]: FAILED! => {
    "changed": false,
    "msg": "dest '/opt/elastic/7.10.1' must be an existing dir"
}

PLAY RECAP ***************************************************************************************************************************************************************************************************
ubuntu                     : ok=8    changed=2    unreachable=0    failed=1    skipped=1    rescued=0    ignored=0  
```
