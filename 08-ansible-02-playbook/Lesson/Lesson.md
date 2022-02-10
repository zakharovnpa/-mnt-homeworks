### Ход выполнения ДЗ по теме "08.02 Работа с Playbook"

## Подготовка к выполнению
1. Создайте свой собственный (или используйте старый) публичный репозиторий на github с произвольным именем.

Создан репозиторий для выполнения ДЗ [ansible-02-playbook](https://github.com/zakharovnpa/ansible-02-playbook)

2. Скачайте [playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

Выполнено

3. Подготовьте хосты в соотвтествии с группами из предподготовленного playbook. 



4. Скачайте дистрибутив [java](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html) и положите его в директорию `playbook/files/`. 

* Для скачивания пришлось создать УЗ на сайте Oracle npazakharov@gmail.com pass !+1
* Затем архив перенесен в Яндекс облако.
* Ссылка на скачивание была взята из панели разработчика браузера из кода ссылки на кнопке скачать
* Взятая ссылка была добавлена в ansible-playbook
```yml
---
- name: Check version Java
  hosts: localhost
  tasks:
    - name: Get Java
      ansible.builtin.get_url: 
        url: "https://s804sas.storage.yandex.net/rdisk/1.........Jr3yw5--6yZCSqDDextBgY"
        dest: "/tmp"
        mode: 0755

```

* Также архив был скачан по взятой с облака ссылке командой 
```ps
curl -O https://s804sas.storage.yandex.net/rdisk/139082549d55ac46f6a77591ecb08eb0a6906d0cbdcb3835c5e53c9eb23bc425/6204f0f5/duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A==?uid=34414669&filename=jdk-11.0.14_linux-x64_bin.tar.gz&disposition=attachment&hash=&limit=0&content_type=application%2Fx-gzip&owner_uid=34414669&fsize=168679847&hid=0fef40a053897309e30543619d23226c&media_type=compressed&tknv=v2&etag=c2037b5f2e2a6ddcfbdfe1489bccfd63&rtoken=e7eIqFuC5HZY&force_default=yes&ycrid=na-3c5259ce3e65a7b6dbd193a5b311927b-downloader9h&ts=5d7a7e5b66740&s=0de7ebb3429f68eb20383eac62727d17cf25e161c2a0002a6999baa8a823e503&pb=U2FsdGVkX19pztWLYUf_22d2O81EXLpp5UmZMzfEl5RRL1Fqgz16R1Gmfxbb7NxvH4SRfEK7S94DqcstbEIB5Jr3yw5--6yZCSqDDextBgY
[1] 23125
[2] 23126
[3] 23127
[4] 23128
[5] 23129
[6] 23130
[7] 23131
[8] 23132
[9] 23133
[10] 23134
[11] 23135
[12] 23136
[13] 23137
[14] 23138
[15] 23139
[16] 23140
[17] 23141
[2]   Done                    filename=jdk-11.0.14_linux-x64_bin.tar.gz
[3]   Done                    disposition=attachment
[4]   Done                    hash=
[5]   Done                    limit=0
[6]   Done                    content_type=application%2Fx-gzip
[7]   Done                    owner_uid=34414669
[8]   Done                    fsize=168679847
[9]   Done                    hid=0fef40a053897309e30543619d23226c
[10]   Done                    media_type=compressed
[11]   Done                    tknv=v2
[12]   Done                    etag=c2037b5f2e2a6ddcfbdfe1489bccfd63
[13]   Done                    rtoken=e7eIqFuC5HZY
[14]   Done                    force_default=yes
root@server1:~/TMP#   % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   188  100   188    0     0   1382      0 --:--:-- --:--:-- --:--:--  1382

[1]   Done                    curl -O https://s804sas.storage.yandex.net/rdisk/139082549d55ac46f6a77591ecb08eb0a6906d0cbdcb3835c5e53c9eb23bc425/6204f0f5/duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A==?uid=34414669
[15]   Done                    ycrid=na-3c5259ce3e65a7b6dbd193a5b311927b-downloader9h
[16]-  Done                    ts=5d7a7e5b66740
[17]+  Done                    s=0de7ebb3429f68eb20383eac62727d17cf25e161c2a0002a6999baa8a823e503

```

```ps
root@server1:/tmp# ls -lha
total 161M
drwxrwxrwt 11 root root 4.0K Feb 10 07:30  .
drwxr-xr-x 20 root root 4.0K Feb 10 07:26  ..
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
```

```ps
root@server1:/tmp# cp duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A== jdk-11.0.14_linux-x64_bin.tar.gz
root@server1:/tmp# 
root@server1:/tmp# 
root@server1:/tmp# ls -lha
total 322M
drwxrwxrwt 11 root root 4.0K Feb 10 07:37  .
drwxr-xr-x 20 root root 4.0K Feb 10 07:26  ..
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
-rwxr-xr-x  1 root root 161M Feb 10 07:37  jdk-11.0.14_linux-x64_bin.tar.gz


```

```ps
root@server1:/tmp# file jdk-11.0.14_linux-x64_bin.tar.gz
jdk-11.0.14_linux-x64_bin.tar.gz: gzip compressed data, last modified: Tue Dec  7 21:54:31 2021, from Unix, original size modulo 2^32 282060800 gzip compressed data, reserved method, ASCII, extra field, has comment, encrypted, from FAT filesystem (MS-DOS, OS/2, NT), original size modulo 2^32 282060800

```

```ps
root@server1:/tmp# tar -xvf jdk-11.0.14_linux-x64_bin.tar.gz
jdk-11.0.14/README.html
jdk-11.0.14/bin/jar
jdk-11.0.14/bin/jarsigner
jdk-11.0.14/bin/java
jdk-11.0.14/bin/javac
jdk-11.0.14/bin/javadoc
jdk-11.0.14/bin/javap
jdk-11.0.14/bin/jcmd
jdk-11.0.14/bin/jconsole
jdk-11.0.14/bin/jdb
jdk-11.0.14/bin/jdeprscan
jdk-11.0.14/bin/jdeps
jdk-11.0.14/bin/jfr
jdk-11.0.14/bin/jhsdb
jdk-11.0.14/bin/jimage
jdk-11.0.14/bin/jinfo
jdk-11.0.14/bin/jjs
jdk-11.0.14/bin/jlink
jdk-11.0.14/bin/jmap
jdk-11.0.14/bin/jmod
jdk-11.0.14/bin/jps
jdk-11.0.14/bin/jrunscript
jdk-11.0.14/bin/jshell
jdk-11.0.14/bin/jstack
jdk-11.0.14/bin/jstat
jdk-11.0.14/bin/jstatd
jdk-11.0.14/bin/keytool
jdk-11.0.14/bin/pack200
jdk-11.0.14/bin/rmic
jdk-11.0.14/bin/rmid
jdk-11.0.14/bin/rmiregistry
jdk-11.0.14/bin/serialver
jdk-11.0.14/bin/unpack200
jdk-11.0.14/conf/logging.properties
jdk-11.0.14/conf/management/jmxremote.access
jdk-11.0.14/conf/management/jmxremote.password.template
jdk-11.0.14/conf/management/management.properties
jdk-11.0.14/conf/net.properties
jdk-11.0.14/conf/security/java.policy
jdk-11.0.14/conf/security/java.security
jdk-11.0.14/conf/security/policy/README.txt
jdk-11.0.14/conf/security/policy/limited/default_US_export.policy
jdk-11.0.14/conf/security/policy/limited/default_local.policy
jdk-11.0.14/conf/security/policy/limited/exempt_local.policy
jdk-11.0.14/conf/security/policy/unlimited/default_US_export.policy
jdk-11.0.14/conf/security/policy/unlimited/default_local.policy
jdk-11.0.14/conf/sound.properties
jdk-11.0.14/include/classfile_constants.h
jdk-11.0.14/include/jawt.h
jdk-11.0.14/include/jdwpTransport.h
jdk-11.0.14/include/jni.h
jdk-11.0.14/include/jvmti.h
jdk-11.0.14/include/jvmticmlr.h
jdk-11.0.14/include/linux/jawt_md.h
jdk-11.0.14/include/linux/jni_md.h
jdk-11.0.14/jmods/java.base.jmod
jdk-11.0.14/jmods/java.compiler.jmod
jdk-11.0.14/jmods/java.datatransfer.jmod
jdk-11.0.14/jmods/java.desktop.jmod
jdk-11.0.14/jmods/java.instrument.jmod
jdk-11.0.14/jmods/java.logging.jmod
jdk-11.0.14/jmods/java.management.jmod
jdk-11.0.14/jmods/java.management.rmi.jmod
jdk-11.0.14/jmods/java.naming.jmod
jdk-11.0.14/jmods/java.net.http.jmod
jdk-11.0.14/jmods/java.prefs.jmod
jdk-11.0.14/jmods/java.rmi.jmod
jdk-11.0.14/jmods/java.scripting.jmod
jdk-11.0.14/jmods/java.se.jmod
jdk-11.0.14/jmods/java.security.jgss.jmod
jdk-11.0.14/jmods/java.security.sasl.jmod
jdk-11.0.14/jmods/java.smartcardio.jmod
jdk-11.0.14/jmods/java.sql.jmod
jdk-11.0.14/jmods/java.sql.rowset.jmod
jdk-11.0.14/jmods/java.transaction.xa.jmod
jdk-11.0.14/jmods/java.xml.crypto.jmod
jdk-11.0.14/jmods/java.xml.jmod
jdk-11.0.14/jmods/jdk.accessibility.jmod
jdk-11.0.14/jmods/jdk.attach.jmod
jdk-11.0.14/jmods/jdk.charsets.jmod
jdk-11.0.14/jmods/jdk.compiler.jmod
jdk-11.0.14/jmods/jdk.crypto.cryptoki.jmod
jdk-11.0.14/jmods/jdk.crypto.ec.jmod
jdk-11.0.14/jmods/jdk.dynalink.jmod
jdk-11.0.14/jmods/jdk.editpad.jmod
jdk-11.0.14/jmods/jdk.hotspot.agent.jmod
jdk-11.0.14/jmods/jdk.httpserver.jmod
jdk-11.0.14/jmods/jdk.internal.ed.jmod
jdk-11.0.14/jmods/jdk.internal.jvmstat.jmod
jdk-11.0.14/jmods/jdk.internal.le.jmod
jdk-11.0.14/jmods/jdk.internal.opt.jmod
jdk-11.0.14/jmods/jdk.internal.vm.ci.jmod
jdk-11.0.14/jmods/jdk.internal.vm.compiler.jmod
jdk-11.0.14/jmods/jdk.internal.vm.compiler.management.jmod
jdk-11.0.14/jmods/jdk.jartool.jmod
jdk-11.0.14/jmods/jdk.javadoc.jmod
jdk-11.0.14/jmods/jdk.jcmd.jmod
jdk-11.0.14/jmods/jdk.jconsole.jmod
jdk-11.0.14/jmods/jdk.jdeps.jmod
jdk-11.0.14/jmods/jdk.jdi.jmod
jdk-11.0.14/jmods/jdk.jdwp.agent.jmod
jdk-11.0.14/jmods/jdk.jfr.jmod
jdk-11.0.14/jmods/jdk.jlink.jmod
jdk-11.0.14/jmods/jdk.jshell.jmod
jdk-11.0.14/jmods/jdk.jsobject.jmod
jdk-11.0.14/jmods/jdk.jstatd.jmod
jdk-11.0.14/jmods/jdk.localedata.jmod
jdk-11.0.14/jmods/jdk.management.agent.jmod
jdk-11.0.14/jmods/jdk.management.jfr.jmod
jdk-11.0.14/jmods/jdk.management.jmod
jdk-11.0.14/jmods/jdk.naming.dns.jmod
jdk-11.0.14/jmods/jdk.naming.ldap.jmod
jdk-11.0.14/jmods/jdk.naming.rmi.jmod
jdk-11.0.14/jmods/jdk.net.jmod
jdk-11.0.14/jmods/jdk.pack.jmod
jdk-11.0.14/jmods/jdk.rmic.jmod
jdk-11.0.14/jmods/jdk.scripting.nashorn.jmod
jdk-11.0.14/jmods/jdk.scripting.nashorn.shell.jmod
jdk-11.0.14/jmods/jdk.sctp.jmod
jdk-11.0.14/jmods/jdk.security.auth.jmod
jdk-11.0.14/jmods/jdk.security.jgss.jmod
jdk-11.0.14/jmods/jdk.unsupported.desktop.jmod
jdk-11.0.14/jmods/jdk.unsupported.jmod
jdk-11.0.14/jmods/jdk.xml.dom.jmod
jdk-11.0.14/jmods/jdk.zipfs.jmod
jdk-11.0.14/legal/java.base/COPYRIGHT
jdk-11.0.14/legal/java.base/LICENSE
jdk-11.0.14/legal/java.base/aes.md
jdk-11.0.14/legal/java.base/asm.md
jdk-11.0.14/legal/java.base/c-libutl.md
jdk-11.0.14/legal/java.base/cldr.md
jdk-11.0.14/legal/java.base/icu.md
jdk-11.0.14/legal/java.base/public_suffix.md
jdk-11.0.14/legal/java.base/unicode.md
jdk-11.0.14/legal/java.compiler/COPYRIGHT
jdk-11.0.14/legal/java.compiler/LICENSE
jdk-11.0.14/legal/java.datatransfer/COPYRIGHT
jdk-11.0.14/legal/java.datatransfer/LICENSE
jdk-11.0.14/legal/java.desktop/COPYRIGHT
jdk-11.0.14/legal/java.desktop/LICENSE
jdk-11.0.14/legal/java.desktop/colorimaging.md
jdk-11.0.14/legal/java.desktop/giflib.md
jdk-11.0.14/legal/java.desktop/harfbuzz.md
jdk-11.0.14/legal/java.desktop/jpeg.md
jdk-11.0.14/legal/java.desktop/lcms.md
jdk-11.0.14/legal/java.desktop/libpng.md
jdk-11.0.14/legal/java.desktop/mesa3d.md
jdk-11.0.14/legal/java.desktop/xwd.md
jdk-11.0.14/legal/java.instrument/COPYRIGHT
jdk-11.0.14/legal/java.instrument/LICENSE
jdk-11.0.14/legal/java.logging/COPYRIGHT
jdk-11.0.14/legal/java.logging/LICENSE
jdk-11.0.14/legal/java.management.rmi/COPYRIGHT
jdk-11.0.14/legal/java.management.rmi/LICENSE
jdk-11.0.14/legal/java.management/COPYRIGHT
jdk-11.0.14/legal/java.management/LICENSE
jdk-11.0.14/legal/java.naming/COPYRIGHT
jdk-11.0.14/legal/java.naming/LICENSE
jdk-11.0.14/legal/java.net.http/COPYRIGHT
jdk-11.0.14/legal/java.net.http/LICENSE
jdk-11.0.14/legal/java.prefs/COPYRIGHT
jdk-11.0.14/legal/java.prefs/LICENSE
jdk-11.0.14/legal/java.rmi/COPYRIGHT
jdk-11.0.14/legal/java.rmi/LICENSE
jdk-11.0.14/legal/java.scripting/COPYRIGHT
jdk-11.0.14/legal/java.scripting/LICENSE
jdk-11.0.14/legal/java.se/COPYRIGHT
jdk-11.0.14/legal/java.se/LICENSE
jdk-11.0.14/legal/java.security.jgss/COPYRIGHT
jdk-11.0.14/legal/java.security.jgss/LICENSE
jdk-11.0.14/legal/java.security.sasl/COPYRIGHT
jdk-11.0.14/legal/java.security.sasl/LICENSE
jdk-11.0.14/legal/java.smartcardio/COPYRIGHT
jdk-11.0.14/legal/java.smartcardio/LICENSE
jdk-11.0.14/legal/java.smartcardio/pcsclite.md
jdk-11.0.14/legal/java.sql.rowset/COPYRIGHT
jdk-11.0.14/legal/java.sql.rowset/LICENSE
jdk-11.0.14/legal/java.sql/COPYRIGHT
jdk-11.0.14/legal/java.sql/LICENSE
jdk-11.0.14/legal/java.transaction.xa/COPYRIGHT
jdk-11.0.14/legal/java.transaction.xa/LICENSE
jdk-11.0.14/legal/java.xml.crypto/COPYRIGHT
jdk-11.0.14/legal/java.xml.crypto/LICENSE
jdk-11.0.14/legal/java.xml.crypto/santuario.md
jdk-11.0.14/legal/java.xml/COPYRIGHT
jdk-11.0.14/legal/java.xml/LICENSE
jdk-11.0.14/legal/java.xml/bcel.md
jdk-11.0.14/legal/java.xml/dom.md
jdk-11.0.14/legal/java.xml/jcup.md
jdk-11.0.14/legal/java.xml/xalan.md
jdk-11.0.14/legal/java.xml/xerces.md
jdk-11.0.14/legal/jdk.accessibility/COPYRIGHT
jdk-11.0.14/legal/jdk.accessibility/LICENSE
jdk-11.0.14/legal/jdk.attach/COPYRIGHT
jdk-11.0.14/legal/jdk.attach/LICENSE
jdk-11.0.14/legal/jdk.charsets/COPYRIGHT
jdk-11.0.14/legal/jdk.charsets/LICENSE
jdk-11.0.14/legal/jdk.compiler/COPYRIGHT
jdk-11.0.14/legal/jdk.compiler/LICENSE
jdk-11.0.14/legal/jdk.crypto.cryptoki/COPYRIGHT
jdk-11.0.14/legal/jdk.crypto.cryptoki/LICENSE
jdk-11.0.14/legal/jdk.crypto.cryptoki/pkcs11cryptotoken.md
jdk-11.0.14/legal/jdk.crypto.cryptoki/pkcs11wrapper.md
jdk-11.0.14/legal/jdk.crypto.ec/COPYRIGHT
jdk-11.0.14/legal/jdk.crypto.ec/LICENSE
jdk-11.0.14/legal/jdk.crypto.ec/ecc.md
jdk-11.0.14/legal/jdk.dynalink/COPYRIGHT
jdk-11.0.14/legal/jdk.dynalink/LICENSE
jdk-11.0.14/legal/jdk.dynalink/dynalink.md
jdk-11.0.14/legal/jdk.editpad/COPYRIGHT
jdk-11.0.14/legal/jdk.editpad/LICENSE
jdk-11.0.14/legal/jdk.hotspot.agent/COPYRIGHT
jdk-11.0.14/legal/jdk.hotspot.agent/LICENSE
jdk-11.0.14/legal/jdk.httpserver/COPYRIGHT
jdk-11.0.14/legal/jdk.httpserver/LICENSE
jdk-11.0.14/legal/jdk.internal.ed/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.ed/LICENSE
jdk-11.0.14/legal/jdk.internal.jvmstat/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.jvmstat/LICENSE
jdk-11.0.14/legal/jdk.internal.le/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.le/LICENSE
jdk-11.0.14/legal/jdk.internal.le/jline.md
jdk-11.0.14/legal/jdk.internal.opt/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.opt/LICENSE
jdk-11.0.14/legal/jdk.internal.opt/jopt-simple.md
jdk-11.0.14/legal/jdk.internal.vm.ci/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.vm.ci/LICENSE
jdk-11.0.14/legal/jdk.internal.vm.compiler.management/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.vm.compiler.management/LICENSE
jdk-11.0.14/legal/jdk.internal.vm.compiler/COPYRIGHT
jdk-11.0.14/legal/jdk.internal.vm.compiler/LICENSE
jdk-11.0.14/legal/jdk.jartool/COPYRIGHT
jdk-11.0.14/legal/jdk.jartool/LICENSE
jdk-11.0.14/legal/jdk.javadoc/COPYRIGHT
jdk-11.0.14/legal/jdk.javadoc/LICENSE
jdk-11.0.14/legal/jdk.javadoc/jquery.md
jdk-11.0.14/legal/jdk.javadoc/jqueryUI.md
jdk-11.0.14/legal/jdk.javadoc/jszip.md
jdk-11.0.14/legal/jdk.javadoc/pako.md
jdk-11.0.14/legal/jdk.jcmd/COPYRIGHT
jdk-11.0.14/legal/jdk.jcmd/LICENSE
jdk-11.0.14/legal/jdk.jconsole/COPYRIGHT
jdk-11.0.14/legal/jdk.jconsole/LICENSE
jdk-11.0.14/legal/jdk.jdeps/COPYRIGHT
jdk-11.0.14/legal/jdk.jdeps/LICENSE
jdk-11.0.14/legal/jdk.jdi/COPYRIGHT
jdk-11.0.14/legal/jdk.jdi/LICENSE
jdk-11.0.14/legal/jdk.jdwp.agent/COPYRIGHT
jdk-11.0.14/legal/jdk.jdwp.agent/LICENSE
jdk-11.0.14/legal/jdk.jfr/COPYRIGHT
jdk-11.0.14/legal/jdk.jfr/LICENSE
jdk-11.0.14/legal/jdk.jlink/COPYRIGHT
jdk-11.0.14/legal/jdk.jlink/LICENSE
jdk-11.0.14/legal/jdk.jshell/COPYRIGHT
jdk-11.0.14/legal/jdk.jshell/LICENSE
jdk-11.0.14/legal/jdk.jsobject/COPYRIGHT
jdk-11.0.14/legal/jdk.jsobject/LICENSE
jdk-11.0.14/legal/jdk.jstatd/COPYRIGHT
jdk-11.0.14/legal/jdk.jstatd/LICENSE
jdk-11.0.14/legal/jdk.localedata/COPYRIGHT
jdk-11.0.14/legal/jdk.localedata/LICENSE
jdk-11.0.14/legal/jdk.localedata/cldr.md
jdk-11.0.14/legal/jdk.localedata/thaidict.md
jdk-11.0.14/legal/jdk.management.agent/COPYRIGHT
jdk-11.0.14/legal/jdk.management.agent/LICENSE
jdk-11.0.14/legal/jdk.management.jfr/COPYRIGHT
jdk-11.0.14/legal/jdk.management.jfr/LICENSE
jdk-11.0.14/legal/jdk.management/COPYRIGHT
jdk-11.0.14/legal/jdk.management/LICENSE
jdk-11.0.14/legal/jdk.naming.dns/COPYRIGHT
jdk-11.0.14/legal/jdk.naming.dns/LICENSE
jdk-11.0.14/legal/jdk.naming.ldap/COPYRIGHT
jdk-11.0.14/legal/jdk.naming.ldap/LICENSE
jdk-11.0.14/legal/jdk.naming.rmi/COPYRIGHT
jdk-11.0.14/legal/jdk.naming.rmi/LICENSE
jdk-11.0.14/legal/jdk.net/COPYRIGHT
jdk-11.0.14/legal/jdk.net/LICENSE
jdk-11.0.14/legal/jdk.pack/COPYRIGHT
jdk-11.0.14/legal/jdk.pack/LICENSE
jdk-11.0.14/legal/jdk.rmic/COPYRIGHT
jdk-11.0.14/legal/jdk.rmic/LICENSE
jdk-11.0.14/legal/jdk.scripting.nashorn.shell/COPYRIGHT
jdk-11.0.14/legal/jdk.scripting.nashorn.shell/LICENSE
jdk-11.0.14/legal/jdk.scripting.nashorn/COPYRIGHT
jdk-11.0.14/legal/jdk.scripting.nashorn/LICENSE
jdk-11.0.14/legal/jdk.scripting.nashorn/double-conversion.md
jdk-11.0.14/legal/jdk.scripting.nashorn/joni.md
jdk-11.0.14/legal/jdk.sctp/COPYRIGHT
jdk-11.0.14/legal/jdk.sctp/LICENSE
jdk-11.0.14/legal/jdk.security.auth/COPYRIGHT
jdk-11.0.14/legal/jdk.security.auth/LICENSE
jdk-11.0.14/legal/jdk.security.jgss/COPYRIGHT
jdk-11.0.14/legal/jdk.security.jgss/LICENSE
jdk-11.0.14/legal/jdk.unsupported.desktop/COPYRIGHT
jdk-11.0.14/legal/jdk.unsupported.desktop/LICENSE
jdk-11.0.14/legal/jdk.unsupported/COPYRIGHT
jdk-11.0.14/legal/jdk.unsupported/LICENSE
jdk-11.0.14/legal/jdk.xml.dom/COPYRIGHT
jdk-11.0.14/legal/jdk.xml.dom/LICENSE
jdk-11.0.14/legal/jdk.zipfs/COPYRIGHT
jdk-11.0.14/legal/jdk.zipfs/LICENSE
jdk-11.0.14/lib/classlist
jdk-11.0.14/lib/ct.sym
jdk-11.0.14/lib/jexec
jdk-11.0.14/lib/jfr/default.jfc
jdk-11.0.14/lib/jfr/profile.jfc
jdk-11.0.14/lib/jli/libjli.so
jdk-11.0.14/lib/jrt-fs.jar
jdk-11.0.14/lib/jspawnhelper
jdk-11.0.14/lib/jvm.cfg
jdk-11.0.14/lib/libattach.so
jdk-11.0.14/lib/libawt.so
jdk-11.0.14/lib/libawt_headless.so
jdk-11.0.14/lib/libawt_xawt.so
jdk-11.0.14/lib/libdt_socket.so
jdk-11.0.14/lib/libextnet.so
jdk-11.0.14/lib/libfontmanager.so
jdk-11.0.14/lib/libinstrument.so
jdk-11.0.14/lib/libj2gss.so
jdk-11.0.14/lib/libj2pcsc.so
jdk-11.0.14/lib/libj2pkcs11.so
jdk-11.0.14/lib/libjaas.so
jdk-11.0.14/lib/libjava.so
jdk-11.0.14/lib/libjavajpeg.so
jdk-11.0.14/lib/libjawt.so
jdk-11.0.14/lib/libjdwp.so
jdk-11.0.14/lib/libjimage.so
jdk-11.0.14/lib/libjsig.so
jdk-11.0.14/lib/libjsound.so
jdk-11.0.14/lib/liblcms.so
jdk-11.0.14/lib/libmanagement.so
jdk-11.0.14/lib/libmanagement_agent.so
jdk-11.0.14/lib/libmanagement_ext.so
jdk-11.0.14/lib/libmlib_image.so
jdk-11.0.14/lib/libnet.so
jdk-11.0.14/lib/libnio.so
jdk-11.0.14/lib/libprefs.so
jdk-11.0.14/lib/librmi.so
jdk-11.0.14/lib/libsaproc.so
jdk-11.0.14/lib/libsctp.so
jdk-11.0.14/lib/libsplashscreen.so
jdk-11.0.14/lib/libsunec.so
jdk-11.0.14/lib/libunpack.so
jdk-11.0.14/lib/libverify.so
jdk-11.0.14/lib/libzip.so
jdk-11.0.14/lib/modules
jdk-11.0.14/lib/psfont.properties.ja
jdk-11.0.14/lib/psfontj2d.properties
jdk-11.0.14/lib/security/blocked.certs
jdk-11.0.14/lib/security/cacerts
jdk-11.0.14/lib/security/default.policy
jdk-11.0.14/lib/security/public_suffix_list.dat
jdk-11.0.14/lib/server/Xusage.txt
jdk-11.0.14/lib/server/libjsig.so
jdk-11.0.14/lib/server/libjvm.so
jdk-11.0.14/lib/src.zip
jdk-11.0.14/lib/tzdb.dat
jdk-11.0.14/man/man1/jaccessinspector.1
jdk-11.0.14/man/man1/jaccesswalker.1
jdk-11.0.14/man/man1/jar.1
jdk-11.0.14/man/man1/jarsigner.1
jdk-11.0.14/man/man1/java.1
jdk-11.0.14/man/man1/javac.1
jdk-11.0.14/man/man1/javadoc.1
jdk-11.0.14/man/man1/javap.1
jdk-11.0.14/man/man1/jcmd.1
jdk-11.0.14/man/man1/jconsole.1
jdk-11.0.14/man/man1/jdb.1
jdk-11.0.14/man/man1/jdeprscan.1
jdk-11.0.14/man/man1/jdeps.1
jdk-11.0.14/man/man1/jhsdb.1
jdk-11.0.14/man/man1/jinfo.1
jdk-11.0.14/man/man1/jjs.1
jdk-11.0.14/man/man1/jlink.1
jdk-11.0.14/man/man1/jmap.1
jdk-11.0.14/man/man1/jmod.1
jdk-11.0.14/man/man1/jps.1
jdk-11.0.14/man/man1/jrunscript.1
jdk-11.0.14/man/man1/jstack.1
jdk-11.0.14/man/man1/jstat.1
jdk-11.0.14/man/man1/jstatd.1
jdk-11.0.14/man/man1/keytool.1
jdk-11.0.14/man/man1/kinit.1
jdk-11.0.14/man/man1/klist.1
jdk-11.0.14/man/man1/ktab.1
jdk-11.0.14/man/man1/pack200.1
jdk-11.0.14/man/man1/rmic.1
jdk-11.0.14/man/man1/rmid.1
jdk-11.0.14/man/man1/rmiregistry.1
jdk-11.0.14/man/man1/serialver.1
jdk-11.0.14/man/man1/unpack200.1
jdk-11.0.14/release

```

```ps
root@server1:/tmp# ls -lha
-rwxr-xr-x  1 root root 161M Feb 10 07:30 'duT1q6E6kpFTxT3aaITPD9fzKCHXRnJahRxxCO9rinnARF4SWV8lcZbveeI0IzUwOHHrDSYYB7as2-XzzorW-A=='
drwxr-xr-x  9 root root 4.0K Feb 10 07:39  jdk-11.0.14
-rwxr-xr-x  1 root root 161M Feb 10 07:37  jdk-11.0.14_linux-x64_bin.tar.gz


```
```ps
root@server1:/tmp/jdk-11.0.14# ls -lha
total 44K
drwxr-xr-x  9 root  root  4.0K Feb 10 07:39 .
drwxrwxrwt 12 root  root  4.0K Feb 10 07:39 ..
drwxr-xr-x  2 root  root  4.0K Feb 10 07:39 bin
drwxr-xr-x  4 root  root  4.0K Feb 10 07:39 conf
drwxr-xr-x  3 root  root  4.0K Feb 10 07:39 include
drwxr-xr-x  2 root  root  4.0K Feb 10 07:39 jmods
drwxr-xr-x 72 root  root  4.0K Feb 10 07:39 legal
drwxr-xr-x  6 root  root  4.0K Feb 10 07:39 lib
drwxr-xr-x  3 root  root  4.0K Feb 10 07:39 man
-r--r--r--  1 10668 10668  160 Dec  7 21:54 README.html
-rw-r--r--  1 10668 10668 1.3K Dec  7 21:54 release

```
Затем архив перенесен в директорию /files

## Основная часть
1. Приготовьте свой собственный inventory файл `prod.yml`.

**Ответ:**

2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.

**Ответ:**

3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.

**Ответ:**

4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.

**Ответ:**

5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

**Ответ:**

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.

**Ответ:**

7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

**Ответ:**

8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

**Ответ:**

9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

**Ответ:**

10. Готовый playbook выложите в свой репозиторий, в ответ предоставьте ссылку на него.

**Ответ:**
