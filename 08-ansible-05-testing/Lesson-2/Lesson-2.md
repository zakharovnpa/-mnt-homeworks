## Ход выполнения ДЗ по новому варианту по теме "08.05 Тестирование Roles"

### Директория выпонения ДЗ:

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles#

```




## Подготовка к выполнению
1. Установите molecule: `pip3 install "molecule==3.4.0"`

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# pip3 install "molecule==3.4.0"
Collecting molecule==3.4.0
  Downloading molecule-3.4.0-py3-none-any.whl (239 kB)
     |████████████████████████████████| 239 kB 1.3 MB/s 
Collecting Jinja2>=2.11.3
  Downloading Jinja2-3.1.2-py3-none-any.whl (133 kB)
     |████████████████████████████████| 133 kB 12.5 MB/s 
Collecting pluggy<1.0,>=0.7.1
  Downloading pluggy-0.13.1-py2.py3-none-any.whl (18 kB)
Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from molecule==3.4.0) (21.3)
Requirement already satisfied: setuptools>=42 in /usr/lib/python3/dist-packages (from molecule==3.4.0) (45.2.0)
Collecting click-help-colors>=0.9
  Downloading click_help_colors-0.9.1-py3-none-any.whl (5.5 kB)
Collecting subprocess-tee>=0.3.2
  Downloading subprocess_tee-0.3.5-py3-none-any.whl (8.0 kB)
Collecting cookiecutter>=1.7.3
  Downloading cookiecutter-1.7.3-py2.py3-none-any.whl (34 kB)
Requirement already satisfied: PyYAML<6,>=5.1 in /usr/lib/python3/dist-packages (from molecule==3.4.0) (5.3.1)
Requirement already satisfied: selinux; sys_platform == "linux" in /usr/lib/python3/dist-packages (from molecule==3.4.0) (3.0)
Collecting click<9,>=8.0
  Downloading click-8.1.3-py3-none-any.whl (96 kB)
     |████████████████████████████████| 96 kB 5.3 MB/s 
Collecting enrich>=1.2.5
  Downloading enrich-1.2.7-py3-none-any.whl (8.7 kB)
Collecting ansible-lint>=5.1.1
  Downloading ansible_lint-6.1.0-py3-none-any.whl (150 kB)
     |████████████████████████████████| 150 kB 11.6 MB/s 
Collecting rich>=9.5.1
  Downloading rich-12.4.1-py3-none-any.whl (231 kB)
     |████████████████████████████████| 231 kB 11.3 MB/s 
Requirement already satisfied: paramiko<3,>=2.5.0 in /usr/lib/python3/dist-packages (from molecule==3.4.0) (2.6.0)
Collecting cerberus!=1.3.3,!=1.3.4,>=1.3.1
  Downloading Cerberus-1.3.2.tar.gz (52 kB)
     |████████████████████████████████| 52 kB 1.4 MB/s 
Collecting MarkupSafe>=2.0
  Downloading MarkupSafe-2.1.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->molecule==3.4.0) (3.0.7)
Collecting binaryornot>=0.4.4
  Downloading binaryornot-0.4.4-py2.py3-none-any.whl (9.0 kB)
Collecting jinja2-time>=0.2.0
  Downloading jinja2_time-0.2.0-py2.py3-none-any.whl (6.4 kB)
Collecting poyo>=0.5.0
  Downloading poyo-0.5.0-py2.py3-none-any.whl (10 kB)
Collecting requests>=2.23.0
  Downloading requests-2.27.1-py2.py3-none-any.whl (63 kB)
     |████████████████████████████████| 63 kB 1.8 MB/s 
Requirement already satisfied: six>=1.10 in /usr/lib/python3/dist-packages (from cookiecutter>=1.7.3->molecule==3.4.0) (1.14.0)
Collecting python-slugify>=4.0.0
  Downloading python_slugify-6.1.2-py2.py3-none-any.whl (9.4 kB)
Collecting jsonschema>=4.5.1
  Downloading jsonschema-4.5.1-py3-none-any.whl (72 kB)
     |████████████████████████████████| 72 kB 1.5 MB/s 
Collecting ruamel.yaml<0.18,>=0.15.34
  Downloading ruamel.yaml-0.17.21-py3-none-any.whl (109 kB)
     |████████████████████████████████| 109 kB 13.6 MB/s 
Collecting pytest
  Downloading pytest-7.1.2-py3-none-any.whl (297 kB)
     |████████████████████████████████| 297 kB 12.8 MB/s 
Requirement already satisfied: ansible-core>=2.12.0 in /usr/local/lib/python3.8/dist-packages (from ansible-lint>=5.1.1->molecule==3.4.0) (2.12.2)
Collecting wcmatch>=7.0
  Downloading wcmatch-8.3-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 1.3 MB/s 
Collecting ansible-compat>=2.0.2
  Downloading ansible_compat-2.0.3-py3-none-any.whl (16 kB)
Collecting yamllint>=1.25.0
  Downloading yamllint-1.26.3.tar.gz (126 kB)
     |████████████████████████████████| 126 kB 12.5 MB/s 
Collecting commonmark<0.10.0,>=0.9.0
  Downloading commonmark-0.9.1-py2.py3-none-any.whl (51 kB)
     |████████████████████████████████| 51 kB 6.3 MB/s 
Collecting typing-extensions<5.0,>=4.0.0; python_version < "3.9"
  Downloading typing_extensions-4.2.0-py3-none-any.whl (24 kB)
Collecting pygments<3.0.0,>=2.6.0
  Downloading Pygments-2.12.0-py3-none-any.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 11.6 MB/s 
Requirement already satisfied: chardet>=3.0.2 in /usr/lib/python3/dist-packages (from binaryornot>=0.4.4->cookiecutter>=1.7.3->molecule==3.4.0) (3.0.4)
Collecting arrow
  Downloading arrow-1.2.2-py3-none-any.whl (64 kB)
     |████████████████████████████████| 64 kB 2.7 MB/s 
Collecting charset-normalizer~=2.0.0; python_version >= "3"
  Downloading charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Requirement already satisfied: idna<4,>=2.5; python_version >= "3" in /usr/lib/python3/dist-packages (from requests>=2.23.0->cookiecutter>=1.7.3->molecule==3.4.0) (2.8)
Requirement already satisfied: certifi>=2017.4.17 in /usr/lib/python3/dist-packages (from requests>=2.23.0->cookiecutter>=1.7.3->molecule==3.4.0) (2019.11.28)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /usr/lib/python3/dist-packages (from requests>=2.23.0->cookiecutter>=1.7.3->molecule==3.4.0) (1.25.8)
Collecting text-unidecode>=1.3
  Downloading text_unidecode-1.3-py2.py3-none-any.whl (78 kB)
     |████████████████████████████████| 78 kB 6.5 MB/s 
Collecting importlib-resources>=1.4.0; python_version < "3.9"
  Downloading importlib_resources-5.7.1-py3-none-any.whl (28 kB)
Collecting attrs>=17.4.0
  Downloading attrs-21.4.0-py2.py3-none-any.whl (60 kB)
     |████████████████████████████████| 60 kB 6.7 MB/s 
Collecting pyrsistent!=0.17.0,!=0.17.1,!=0.17.2,>=0.14.0
  Downloading pyrsistent-0.18.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (119 kB)
     |████████████████████████████████| 119 kB 11.6 MB/s 
Collecting ruamel.yaml.clib>=0.2.6; platform_python_implementation == "CPython" and python_version < "3.11"
  Downloading ruamel.yaml.clib-0.2.6-cp38-cp38-manylinux1_x86_64.whl (570 kB)
     |████████████████████████████████| 570 kB 12.1 MB/s 
Collecting iniconfig
  Downloading iniconfig-1.1.1-py2.py3-none-any.whl (5.0 kB)
Collecting py>=1.8.2
  Downloading py-1.11.0-py2.py3-none-any.whl (98 kB)
     |████████████████████████████████| 98 kB 6.1 MB/s 
Collecting tomli>=1.0.0
  Downloading tomli-2.0.1-py3-none-any.whl (12 kB)
Requirement already satisfied: resolvelib<0.6.0,>=0.5.3 in /usr/local/lib/python3.8/dist-packages (from ansible-core>=2.12.0->ansible-lint>=5.1.1->molecule==3.4.0) (0.5.4)
Requirement already satisfied: cryptography in /usr/lib/python3/dist-packages (from ansible-core>=2.12.0->ansible-lint>=5.1.1->molecule==3.4.0) (2.8)
Collecting bracex>=2.1.1
  Downloading bracex-2.2.1-py3-none-any.whl (12 kB)
Collecting pathspec>=0.5.3
  Downloading pathspec-0.9.0-py2.py3-none-any.whl (31 kB)
Requirement already satisfied: python-dateutil>=2.7.0 in /usr/lib/python3/dist-packages (from arrow->jinja2-time>=0.2.0->cookiecutter>=1.7.3->molecule==3.4.0) (2.7.3)
Collecting zipp>=3.1.0; python_version < "3.10"
  Downloading zipp-3.8.0-py3-none-any.whl (5.4 kB)
Building wheels for collected packages: cerberus, yamllint
  Building wheel for cerberus (setup.py) ... done
  Created wheel for cerberus: filename=Cerberus-1.3.2-py3-none-any.whl size=54335 sha256=185bc6a22189d0e61da04031ff051bac957be41ad2f23e20ea17c04a871bee69
  Stored in directory: /root/.cache/pip/wheels/ae/34/69/a4de22183e8aa2539ba66b3ed344dab74783d8d43fea2a5816
  Building wheel for yamllint (setup.py) ... done
  Created wheel for yamllint: filename=yamllint-1.26.3-py2.py3-none-any.whl size=60805 sha256=bda7ad2e2b86620f588fa3404429de641303331df5f9e6215cf7aba470041b28
  Stored in directory: /root/.cache/pip/wheels/50/32/52/83c64d29428fe60cf259c5d223364015072b97c37e2a1247cb
Successfully built cerberus yamllint
Installing collected packages: MarkupSafe, Jinja2, pluggy, click, click-help-colors, subprocess-tee, binaryornot, arrow, jinja2-time, poyo, charset-normalizer, requests, text-unidecode, python-slugify, cookiecutter, commonmark, typing-extensions, pygments, rich, enrich, zipp, importlib-resources, attrs, pyrsistent, jsonschema, ruamel.yaml.clib, ruamel.yaml, iniconfig, py, tomli, pytest, bracex, wcmatch, ansible-compat, pathspec, yamllint, ansible-lint, cerberus, molecule
  Attempting uninstall: MarkupSafe
    Found existing installation: MarkupSafe 1.1.0
    Not uninstalling markupsafe at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'MarkupSafe'. No files were found to uninstall.
  Attempting uninstall: Jinja2
    Found existing installation: Jinja2 2.10.1
    Not uninstalling jinja2 at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'Jinja2'. No files were found to uninstall.
  Attempting uninstall: click
    Found existing installation: Click 7.0
    Not uninstalling click at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'Click'. No files were found to uninstall.
  Attempting uninstall: requests
    Found existing installation: requests 2.22.0
    Not uninstalling requests at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'requests'. No files were found to uninstall.
  Attempting uninstall: pygments
    Found existing installation: Pygments 2.3.1
    Not uninstalling pygments at /usr/lib/python3/dist-packages, outside environment /usr
    Can't uninstall 'Pygments'. No files were found to uninstall.
Successfully installed Jinja2-3.1.2 MarkupSafe-2.1.1 ansible-compat-2.0.3 ansible-lint-6.1.0 arrow-1.2.2 attrs-21.4.0 binaryornot-0.4.4 bracex-2.2.1 cerberus-1.3.2 charset-normalizer-2.0.12 click-8.1.3 click-help-colors-0.9.1 commonmark-0.9.1 cookiecutter-1.7.3 enrich-1.2.7 importlib-resources-5.7.1 iniconfig-1.1.1 jinja2-time-0.2.0 jsonschema-4.5.1 molecule-3.4.0 pathspec-0.9.0 pluggy-0.13.1 poyo-0.5.0 py-1.11.0 pygments-2.12.0 pyrsistent-0.18.1 pytest-7.1.2 python-slugify-6.1.2 requests-2.27.1 rich-12.4.1 ruamel.yaml-0.17.21 ruamel.yaml.clib-0.2.6 subprocess-tee-0.3.5 text-unidecode-1.3 tomli-2.0.1 typing-extensions-4.2.0 wcmatch-8.3 yamllint-1.26.3 zipp-3.8.0

```
* Столкнулся с несовместимостью версий ansible-lint и molecule

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# molecule --verson
Traceback (most recent call last):
  File "/usr/local/bin/molecule", line 5, in <module>
    from molecule.__main__ import main
  File "/usr/local/lib/python3.8/dist-packages/molecule/__main__.py", line 22, in <module>
    from molecule.shell import main
  File "/usr/local/lib/python3.8/dist-packages/molecule/shell.py", line 29, in <module>
    from molecule import command, logger
  File "/usr/local/lib/python3.8/dist-packages/molecule/command/__init__.py", line 27, in <module>
    from molecule.command import base  # noqa
  File "/usr/local/lib/python3.8/dist-packages/molecule/command/base.py", line 31, in <module>
    from ansiblelint.prerun import prepare_environment
ModuleNotFoundError: No module named 'ansiblelint.prerun'

```
* Решение:
  - Уделена версия ansible-lint 6.1.0

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# pip3 uninstall ansible-lint 6.1.0
Found existing installation: ansible-lint 6.1.0
Uninstalling ansible-lint-6.1.0:
  Would remove:
    /usr/local/bin/ansible-lint
    /usr/local/lib/python3.8/dist-packages/ansible_lint-6.1.0.dist-info/*
    /usr/local/lib/python3.8/dist-packages/ansiblelint/*
Proceed (y/n)? y
  Successfully uninstalled ansible-lint-6.1.0
WARNING: Skipping 6.1.0 as it is not installed.

```
  - Установлена версия ansible-lint 5.4.0

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# pip install ansible-lint==5.4.0
Collecting ansible-lint==5.4.0
  Downloading ansible_lint-5.4.0-py3-none-any.whl (119 kB)
     |████████████████████████████████| 119 kB 1.3 MB/s 
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from ansible-lint==5.4.0) (5.3.1)
Collecting tenacity
  Downloading tenacity-8.0.1-py3-none-any.whl (24 kB)
Requirement already satisfied: rich>=9.5.1 in /usr/local/lib/python3.8/dist-packages (from ansible-lint==5.4.0) (12.4.1)
Requirement already satisfied: wcmatch>=7.0 in /usr/local/lib/python3.8/dist-packages (from ansible-lint==5.4.0) (8.3)
Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from ansible-lint==5.4.0) (21.3)
Requirement already satisfied: ruamel.yaml<1,>=0.15.37; python_version >= "3.7" in /usr/local/lib/python3.8/dist-packages (from ansible-lint==5.4.0) (0.17.21)
Requirement already satisfied: enrich>=1.2.6 in /usr/local/lib/python3.8/dist-packages (from ansible-lint==5.4.0) (1.2.7)
Requirement already satisfied: typing-extensions<5.0,>=4.0.0; python_version < "3.9" in /usr/local/lib/python3.8/dist-packages (from rich>=9.5.1->ansible-lint==5.4.0) (4.2.0)
Requirement already satisfied: pygments<3.0.0,>=2.6.0 in /usr/local/lib/python3.8/dist-packages (from rich>=9.5.1->ansible-lint==5.4.0) (2.12.0)
Requirement already satisfied: commonmark<0.10.0,>=0.9.0 in /usr/local/lib/python3.8/dist-packages (from rich>=9.5.1->ansible-lint==5.4.0) (0.9.1)
Requirement already satisfied: bracex>=2.1.1 in /usr/local/lib/python3.8/dist-packages (from wcmatch>=7.0->ansible-lint==5.4.0) (2.2.1)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->ansible-lint==5.4.0) (3.0.7)
Requirement already satisfied: ruamel.yaml.clib>=0.2.6; platform_python_implementation == "CPython" and python_version < "3.11" in /usr/local/lib/python3.8/dist-packages (from ruamel.yaml<1,>=0.15.37; python_version >= "3.7"->ansible-lint==5.4.0) (0.2.6)
Installing collected packages: tenacity, ansible-lint
Successfully installed ansible-lint-5.4.0 tenacity-8.0.1

```
* Результат:
```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# ansible --version
ansible [core 2.12.2]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.8/dist-packages/ansible
  ansible collection location = /root/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.8.10 (default, Mar 15 2022, 12:22:08) [GCC 9.4.0]
  jinja version = 3.1.2
  libyaml = True
```

```
root@PC-Ubuntu:~/ansible-learning/05-testing-roles# molecule --version
molecule 3.4.0 using python 3.8 
    ansible:2.12.2
    delegated:3.4.0 from molecule

```

2. Соберите локальный образ на основе [Dockerfile](./Dockerfile)

```
FROM rancher/dind:latest
ENV MOLECULE_NO_LOG false

RUN apt reinstall glibc-common -y
RUN apt update -y && apt install tar gcc make python3-pip zlib-devel openssl-devel yum-utils libffi-devel -y

ADD https://www.python.org/ftp/python/3.7.10/Python-3.7.10.tgz Python-3.7.10.tgz
RUN tar xf Python-3.7.10.tgz && cd Python-3.7.10/ && ./configure && make && make altinstall
ADD https://www.python.org/ftp/python/3.9.2/Python-3.9.2.tgz Python-3.9.2.tgz
RUN tar xf Python-3.9.2.tgz && cd Python-3.9.2/ && ./configure && make && make altinstall
RUN python3 -m pip install --upgrade pip && pip3 install tox selinux
RUN rm -rf Python-*
```
* Для разных дистрибуьтвов ОС использовать возможность определения типа ОС из Gathernig Facts - использовать переменну `ansible_facts.pkg_mgr`
```
  - import_tasks: "configure.yml"
  - include_tasks: "download {{ ansible_facts.pkg_mgr }}.yml"     # пока это пример
    tags: [always]
                                                               
  - include_tasks: "download_kibana_rpm.yml"    # пока это пример
    # when:
    #  - force_reinstall
    # tags: [install]
  - include_tasks: "install_kibana.yml"   # пока это пример
    # when:
    #  - skip_instal is undefinde
    #  - ansible_distributon in support_system
    tags: [install]
    
    tags: [config]
    
    
    tags: [service]

```


## Основная часть

Наша основная цель - настроить тестирование наших ролей. Задача: сделать сценарии тестирования для vector. Ожидаемый результат: все сценарии успешно проходят тестирование ролей.

### Molecule

1. Запустите  `molecule test -s centos7` внутри корневой директории clickhouse-role, посмотрите на вывод команды.
2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.
3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.
4. Добавьте несколько assert'ов в verify.yml файл для  проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска, etc). Запустите тестирование роли повторно и проверьте, что оно прошло успешно.
5. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

### Tox

1. Добавьте в директорию с vector-role файлы из [директории](./example)
2. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it <image_name> /bin/bash`, где path_to_repo - путь до корня репозитория с vector-role на вашей файловой системе.
3. Внутри контейнера выполните команду `tox`, посмотрите на вывод.
4. Добавьте файл `tox.ini` в корень репозитория каждой своей роли.
5. Создайте облегчённый сценарий для `molecule`. Проверьте его на исполнимость.
6. Пропишите правильную команду в `tox.ini` для того чтобы запускался облегчённый сценарий.
7. Запустите `docker` контейнер так, чтобы внутри оказались обе ваши роли.
8. Зайдти поочерёдно в каждую из них и запустите команду `tox`. Убедитесь, что всё отработало успешно.
9. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Ссылка на репозиторий являются ответами на домашнее задание. Не забудьте указать в ответе теги решений Tox и Molecule заданий.

## Необязательная часть

1. Проделайте схожие манипуляции для создания роли lighthouse.
2. Создайте сценарий внутри любой из своих ролей, который умеет поднимать весь стек при помощи всех ролей.
3. Убедитесь в работоспособности своего стека. Создайте отдельный verify.yml, который будет проверять работоспособность интеграции всех инструментов между ними.
4. Выложите свои roles в репозитории. В ответ приведите ссылки.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
