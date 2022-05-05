# Ход выполненя Домашнее задание к занятию "09.05 Teamcity"

## Подготовка к выполнению

1. В Ya.Cloud создайте новый инстанс (4CPU4RAM) на основе образа `jetbrains/teamcity-server`
2. Дождитесь запуска teamcity, выполните первоначальную настройку
3. Создайте ещё один инстанс(2CPU4RAM) на основе образа `jetbrains/teamcity-agent`. Пропишите к нему a окружения `SERVER_URL: "http://<teamcity_url>:8111"`
4. Авторизуйте агент
5. Сделайте fork [репозитория](https://github.com/aragastmatb/example-teamcity)
6. Создать VM для Nexus (2CPU4RAM) и запустить playook (./infrastructure)

* Запускем `ansible-playbook ./infrastructure/site.yml -i ./infrastructure/inventory/cicd/hosts.yml`
```
root@PC-Ubuntu:~/ansible-learning/yandex-cloud/Lambda/ansible# ansible-playbook ./infrastructure/site.yml -i ./infrastructure/inventory/cicd/hosts.yml 
[WARNING]: Found both group and host with same name: nexus

PLAY [Get Nexus installed] ***********************************************************************************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************************************************************************************************
The authenticity of host '51.250.88.80 (51.250.88.80)' can't be established.
ECDSA key fingerprint is SHA256:snjHfBoLYlGdxMlGh34ex7BAski6uP63bJZKoKAd1kE.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
ok: [nexus]

TASK [Create Nexus group] ************************************************************************************************************************************************************************************
changed: [nexus]

TASK [Create Nexus user] *************************************************************************************************************************************************************************************
changed: [nexus]

TASK [Install JDK] *******************************************************************************************************************************************************************************************
changed: [nexus]

TASK [Create Nexus directories] ******************************************************************************************************************************************************************************
changed: [nexus] => (item=/home/nexus/log)
changed: [nexus] => (item=/home/nexus/sonatype-work/nexus3)
changed: [nexus] => (item=/home/nexus/sonatype-work/nexus3/etc)
changed: [nexus] => (item=/home/nexus/pkg)
changed: [nexus] => (item=/home/nexus/tmp)

TASK [Download Nexus] ****************************************************************************************************************************************************************************************
[WARNING]: Module remote_tmp /home/nexus/.ansible/tmp did not exist and was created with a mode of 0700, this may cause issues when running as another user. To avoid this, create the remote_tmp dir with
the correct permissions manually
changed: [nexus]

TASK [Unpack Nexus] ******************************************************************************************************************************************************************************************
changed: [nexus]

TASK [Link to Nexus Directory] *******************************************************************************************************************************************************************************
changed: [nexus]

TASK [Add NEXUS_HOME for Nexus user] *************************************************************************************************************************************************************************
changed: [nexus]

TASK [Add run_as_user to Nexus.rc] ***************************************************************************************************************************************************************************
changed: [nexus]

TASK [Raise nofile limit for Nexus user] *********************************************************************************************************************************************************************
changed: [nexus]

TASK [Create Nexus service for SystemD] **********************************************************************************************************************************************************************
changed: [nexus]

TASK [Ensure Nexus service is enabled for SystemD] ***********************************************************************************************************************************************************
changed: [nexus]

TASK [Create Nexus vmoptions] ********************************************************************************************************************************************************************************
changed: [nexus]

TASK [Create Nexus properties] *******************************************************************************************************************************************************************************
changed: [nexus]

TASK [Lower Nexus disk space threshold] **********************************************************************************************************************************************************************
skipping: [nexus]

TASK [Start Nexus service if enabled] ************************************************************************************************************************************************************************
changed: [nexus]

TASK [Ensure Nexus service is restarted] *********************************************************************************************************************************************************************
skipping: [nexus]

TASK [Wait for Nexus port if started] ************************************************************************************************************************************************************************
ok: [nexus]

PLAY RECAP ***************************************************************************************************************************************************************************************************
nexus                      : ok=17   changed=15   unreachable=0    failed=0    skipped=2    rescued=0    ignored=0   

```
* Вход на сервер Nexus `http://51.250.88.80:8081`








## Основная часть

1. Создайте новый проект в teamcity на основе fork
- 01:10

- Создан проект `netology-teamcity`
- Проброшен ключ SSH с измененными правами для пользователя не root и такой же группы
- Выполнено подключение к репозиторию по этой ссылке: `https://github.com/zakharovnpa/example-teamcity`
- С таким подключением работает запуск сборки при изменении в репозитории.

- Затем ссылка на VCS root была заменена на `git@github.com:zakharovnpa/example-teamcity.git`
- Teamcity принял ссылку, подключение успешное.


2. Сделайте autodetect конфигурации

- autodetect сообщил, что BuildSteps (шаги сборки) не найдены и просит вручную их настроить.

3. Сохраните необходимые шаги, запустите первую сборку master'a
- Выполнить предварительнуб настройку TeamCity

- 01:32:00 - Build Feature - здесь настраивается параметр, по которому начинается сборка при изменини в репозитории?????

4. Поменяйте условия сборки: если сборка по ветке `master`, то должен происходит `mvn clean deploy`, иначе `mvn clean test`. Это все про Maven.
- 02:22:00 - Делаем сборку по условию задачи. Пояснение: если в имя ветки не входит слово `master`, то мы делаем просто тесты, если входит, то делаем полную нормальную сборку.
- 02:24:15 - пример

В настройках `Build` в шаге `Execute step` выбираем `Always, even build stop ... ` добавляем параметр `teamcity.build.brunc`, Conditions: `does not contain`, Value `master` - указываем конкретную ветку
- 02:23:18 - если слово master не входит в имя ветки, то мы делаем просто тесты, если входит, то делаем полную нормальную сборку.
- 02:23:50 - настройка второго шага сборки. 
  - Execute step: `Always, even if build stop command was issued`
  - Add Conditions:
    - Parameter Name: `teamcity.build.branch`, 
    - Conditions: `contains`, 
    - Value: `master`
  - Goals: `clean deploy ` - будет создавать файлы `.jar` и подготоваливать их к деплою в Nexus
- Поменять в файле `pom.xml` ip address servers Nexus

```xml
<distributionManagement>
		<repository>
				<id>nexus</id>
				<url>http://51.250.79.202:8081/repository/maven-releases</url>
		</repository>
	</distributionManagement>
```

- Зайти на сервер Nexus `http://51.250.88.80:8081` - 02:25:00

5. Для deploy (загрузки артифактов на сревер Nexus) будет необходимо загрузить [settings.xml](./09-ci-05-teamcity/teamcity/settings.xml) в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus. Креды - это Credentionals - параметры авторизации на сервере - логин и пароль
- 02:29:30 - про необходимость загрузки настройки Nexus через загрузку файла `settings.xml` с загрузкой кредов
- 02:30:20 - показано содержимое файла `settings.xml` и секция с логином и паролем
- 02:31:00 - показано где настройки для загрузки файла конфигурации `settings.xml`

```xml
  <servers>
    <!-- server
     | Specifies the authentication information to use when connecting to a particular server, identified by
     | a unique name within the system (referred to by the 'id' attribute below).
     |
     | NOTE: You should either specify username/password OR privateKey/passphrase, since these pairings are
     |       used together.
     |
    <server>
      <id>deploymentRepo</id>
      <username>repouser</username>
      <password>repopwd</password>
    </server>
    -->
    <server>
      <id>nexus</id>
      <username>admin</username>
      <password>admin123</password>
    </server>
    <!-- Another sample, using keys to authenticate.
    <server>
      <id>siteServer</id>
      <privateKey>/path/to/private/key</privateKey>
      <passphrase>optional; leave empty if not used.</passphrase>
    </server>
    -->
  </servers>
```



* Порядок загрузки файла конфигураци:
- В меню проекта, в пункт `Maven Settings` --> `Uplad Settings File`

* Для начала использования файла конфигурации:
- Зайти в меню сборки `Beald` --> `Beald steps` --> `User setings selection` --> `netology` (<project_name>) --> `Save`
- Еще раз запустить сборку.

* Как выкладывать в артифакты:
- 02:33:20 - пояснение
- В меню сборки `Build` --> `General Setting` в пункте `Artifact paths` записать `+:target/*.jar` и тогда все `.jar` артифакта сборки непосредственно были бы под кнопкой `Artifacts` (крайняя справа в виде стопочки бумаг) в общем списке проведенных сборок в меню `Build`--> `History`
![screen-teamcity-build-history](/09-ci-05-teamcity/Files/screen-teamcity-build-history.png)

- 02:33:45 - что присходит в это время в Nexus
  - В директории `maven-release` появились папки с plaindoll и с версиями файлов
- 02:34:00 - повторный запуск сборки не забампив новую версию. !!! Что такое забампив???, то призойдет ошибка из-за того, что номер релиза не изменился (не увеличился). Две одинаковые репозитории в релизной ветке выложить нельзя.

Забапмить - в ПО для работы с файлами (VisualStudio) есть команда `bump version` для синхронизации изменений в файлах с файлами в удаленной репозитории

Что нужно сделать:
- 02:35:10 - в файле `pom.xml` изменить version для jar
```xml
.
.
<packing>jar</packing>
<version>0.2.5</version> - удалить
<version>0.2.6</version> - добавить
``` 
- После того, как изменения синхронизированы с удаленым репозиторием, автоматически запустится новая сборка.

- 02:37:15 - про то, что в файл `pom.xml` всталяются парметры версионирования. Каждая новая сборка апплоадит новую версию артифакта.
В правильной сборке никто бампить версию не станет.
Был показан самый простой способ доставки из CI в  CD.

TeamCity - инструмент более для CI, чем для CD.

6. В pom.xml необходимо поменять ссылки на репозиторий и nexus
- 02:14 - про Nexus. Как установить на новой ВМ и про сбор артифактов
- 02:28:20 - Nexus

* Как выкладывать в артифакты:
- 02:33:20 - пояснение
- В меню сборки `Build` --> `General Setting` в пункте `Artifact paths` записать `+:target/*.jar` и тогда все `.jar` артифакта сборки непосредственно были бы под кнопкой `Artifacts` (крайняя справа в виде стопочки бумаг) в общем списке проведенных сборок в меню `Build`--> `History`
![screen-teamcity-build-history](/09-ci-05-teamcity/Files/screen-teamcity-build-history.png)
- 02:35:15 - меняет номер версии в файле `pom.xml`
- 02:36:45 - пояснение про то как teamcity можно версионировать. Делать Build Number, который потом можно использовать как параметр. В правильной версии никто бампить не станет.

7. Запустите сборку по master, убедитесь что всё прошло успешно, артефакт появился в nexus
- 02:27:50 - про PullRequest и Merge в ветку master
- 02:33:20 - как настроить путь для выгрузки артифактов
- 02:33:50 - проверка артифакта в Nexus
- 02:37:40 - проверка артифакта в Nexus. Самый простой способ доставки артфактов из CI в CD
- 02:22:00 - Делаем сборку

8. Мигрируйте `build configuration` в репозиторий
- 02:50:10 - пояснение 

- Обязательно должно быть подключение к VCS git по ssh
- Это настраивается в меню проекта
  - `Version settins`  --> `Sinchronization enable` --> выбираем репозиторий. Формат - `Kotlin` --> Apply
- Начинается сборка проекта в виде Котлина, связывается с репозиторием, пушит по ssh в мастер ветку.   
- 02:52:15 - готовность синхронизации
- 02:52:20 - в репозитории появляется директория `./teamcity`. В ней лежит `pom.xml`, `settings.kts` - файл с настройками проекта и файл `netology` в директории `./teamcity/pluginData/_Self/mavenSettings/netology` Это файл настроек Maven в формате `.xml` - тот самый   
- 02:52:55 - пояснение по файлу настроек Maven в формате `.xml` для проекта. В этом файле можно менять настройки, потом пушить в репозиторий. TeamCity вычитывает этот репозиторий иесли мы здесь все наприсали правильно, все компилируется и все хорошо, то он будет вносить эти изменения в свою конфигурацию и работать с ними. Если в этом файле будет какая-то ошибка и файл не будет компилироваться, то тогда будет применяться последняя успешная конфигурация .
- 02:56:55 - Важно то, что результатом выгрузки является директория `./teamcity/pluginData/_Self/mavenSettings/`, а в ней `settings.kts`, `pom.xml` будут выложены.                                                                       

9. Создайте отдельную ветку `feature/add_reply` в репозитории
- 02:08:10 - пример


* Не удалось создать новую ветку по команде `git checkout -b feature/add_reply `
```
root@PC-Ubuntu:~/netology-project/example-teamcity# git checkout -b feature/add_reply
fatal: cannot lock ref 'refs/heads/feature/add_reply': 'refs/heads/feature' exists; cannot create 'refs/heads/feature/add_reply'

```
* Создана новая ветка `git checkout -b feature`

```
root@PC-Ubuntu:~/netology-project/example-teamcity# git checkout -b feature
Переключено на новую ветку «feature»
root@PC-Ubuntu:~/netology-project/example-teamcity# 
root@PC-Ubuntu:~/netology-project/example-teamcity# git log --graph --oneline
* 2cfadd3 (HEAD -> feature, origin/main, origin/HEAD, main) Adding change in README.md
* c2f6429 Create WelcomerTest.java
* cde289c Create Welcomer.java
* 2d283da Create HelloPlayer.java
* aeb3180 Create pom.xml
* d08e247 Create .project
* fd1eba4 Create .gitignore
* 79e6a2f Create .classpath
* 0d8bb7c Create Welcomer.java
* 06d6cc9 Create HelloPlayer.java
* 2514cbe Create settings.kts
* 1805795 Create pom.xml
* 8a81fb2 Create netology
* e8b255f Create org.eclipse.jdt.core.prefs
* 04d499b Create org.eclipse.jdt.apt.core.prefs
* bf577d1 Initial commit

```


10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово `hunter`
- 01:07 - показан прмер
- 02:08 - пример

* Вносим изменения в файл `sec/main/java/plaindoll/Welcomer.java`

```

```

11. Дополните тест для нового метода на поиск слова `hunter` в новой реплике
- 02:09:20 - пример

12. Сделайте push всех изменений в новую ветку в репозиторий
- 02:11 - пример

13. Убедитесь что сборка самостоятельно запустилась, тесты прошли успешно
- 02:06:35 - показаны где смотреть результаты тестов

[netology_Build_3-tests.csv](/09-ci-05-teamcity/Files/netology_Build_3-tests.csv)

```
Order#,Test Name,Status,Duration(ms)
1,plaindoll.WelcomerTest.welcomerSaysFarewell,OK,6
2,plaindoll.WelcomerTest.welcomerSaysHunter,OK,0
3,plaindoll.WelcomerTest.welcomerSaysStatus,OK,0
4,plaindoll.WelcomerTest.welcomerSaysWelcome,OK,0

```

14. Внесите изменения из произвольной ветки `feature/add_reply` в `master` через `Merge`
- 02:08:00 - пример



15. Убедитесь, что нет собранного артифакта в сборке по ветке `master`
- 01:57:45
- 02:14 - про Nexus. Как установить на новой ВМ и про сбор артифактов

16. Настройте конфигурацию так, чтобы она собирала `.jar` в артефакты сборки
- 02:33

17. Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны
18. Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity
19. В ответ предоставьте ссылку на репозиторий

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
