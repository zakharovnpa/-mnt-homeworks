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

Доустановка ` ansible-lint `
```ps
root@server1:/tmp# pip3 install ansible-lint
Collecting ansible-lint
  Downloading ansible_lint-5.3.2-py3-none-any.whl (115 kB)
     |████████████████████████████████| 115 kB 1.4 MB/s 
Collecting tenacity
  Downloading tenacity-8.0.1-py3-none-any.whl (24 kB)
Requirement already satisfied: packaging in /usr/local/lib/python3.8/dist-packages (from ansible-lint) (21.3)
Collecting ruamel.yaml<1,>=0.15.37; python_version >= "3.7"
  Downloading ruamel.yaml-0.17.20-py3-none-any.whl (109 kB)
     |████████████████████████████████| 109 kB 12.5 MB/s 
Requirement already satisfied: pyyaml in /usr/lib/python3/dist-packages (from ansible-lint) (5.3.1)
Collecting enrich>=1.2.6
  Downloading enrich-1.2.7-py3-none-any.whl (8.7 kB)
Collecting wcmatch>=7.0
  Downloading wcmatch-8.3-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 1.3 MB/s 
Collecting rich>=9.5.1
  Downloading rich-11.2.0-py3-none-any.whl (217 kB)
     |████████████████████████████████| 217 kB 7.1 MB/s 
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /usr/local/lib/python3.8/dist-packages (from packaging->ansible-lint) (3.0.7)
Collecting ruamel.yaml.clib>=0.2.6; platform_python_implementation == "CPython" and python_version < "3.11"
  Downloading ruamel.yaml.clib-0.2.6-cp38-cp38-manylinux1_x86_64.whl (570 kB)
     |████████████████████████████████| 570 kB 9.0 MB/s 
Collecting bracex>=2.1.1
  Downloading bracex-2.2.1-py3-none-any.whl (12 kB)
Collecting commonmark<0.10.0,>=0.9.0
  Downloading commonmark-0.9.1-py2.py3-none-any.whl (51 kB)
     |████████████████████████████████| 51 kB 5.2 MB/s 
Collecting pygments<3.0.0,>=2.6.0
  Downloading Pygments-2.11.2-py3-none-any.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 8.6 MB/s 
Requirement already satisfied: colorama<0.5.0,>=0.4.0 in /usr/lib/python3/dist-packages (from rich>=9.5.1->ansible-lint) (0.4.3)
Installing collected packages: tenacity, ruamel.yaml.clib, ruamel.yaml, commonmark, pygments, rich, enrich, bracex, wcmatch, ansible-lint
Successfully installed ansible-lint-5.3.2 bracex-2.2.1 commonmark-0.9.1 enrich-1.2.7 pygments-2.11.2 rich-11.2.0 ruamel.yaml-0.17.20 ruamel.yaml.clib-0.2.6 tenacity-8.0.1 wcmatch-8.3

```

```ps
root@server1:/tmp# type ansible-lint
ansible-lint is /usr/local/bin/ansible-lint
root@server1:/tmp# 
root@server1:/tmp# which ansible-lint
/usr/local/bin/ansible-lint


```

## Основная часть
1. Приготовьте свой собственный inventory файл `prod.yml`.

**Ответ:**

В лекции "8.3. Использование Yandex Cloud" описано 

использование фактов хостов: 01:12:30
создание инвентори: 01:13:50
Создание в Яндекс.Облаке ВМ: 01:18:00
и запуск playbook:01:21:00



В соответствии с тем, что у нас есть
``` yml
el:
   hosts:
     centos7:
        ansible_connection: docker

```


```yml
---
centos7:
  hosts:
    localhost:
      ansible_connection: ssh
      ansible_user: root

```

2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает kibana.
Точно также как настривать эластик. Все рубль- в рубль.
скачать тар-гз
сделать тимплейт с-ашника
разархивировать тар-гз
создать директорию


**Ответ:**
```
Kibana – тиражируемая свободная программная панель визуализации данных. В процессе использования программы информация, 
проиндексированная в кластере Elasticsearch, представляется в виде диаграмм различных видов, таких как:
- столбчатые,
- линейные,
- точечные,
- круговые,
- а также возможна визуализация данных в привязке к географическим картам.

Как правило, Kibana используется для мониторинга и анализа ИТ-инфраструктуры в составе Elastic Stack (ранее ELK Stack), 
в который помимо нее входят Elasticsearch и Logstash. Logstash отвечает за логирование и поставляет входящий поток данных 
в Elasticsearch для хранения, классификации и поиска. Kibana, в свою очередь, получает доступ к данным Elasticsearch для 
их визуализации в различных визуальных форматах, например – в виде информационных панелей (dashboards) с различными видами диаграмм.
```


Находим в википедии ссылку на [сайт кибаны](https://www.elastic.co/kibana/) 
Находим ссылку на скачивание кибаны [https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz](https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz)

Дописываем playbook 
```yml
---
name: Install Kibana
  hosts: ubuntu
  ansible_connext: docker
    tasks: Download kibana
      - name:Get Kibana
        get_url: "https://artifacts.elastic.co/downloads/kibana/kibana-8.0.0-linux-x86_64.tar.gz"

```
```yml
- name: Install Java
  hosts: all
  tasks:
    - name: Set facts for Java 11 vars
      set_fact:
        java_home: "/opt/jdk/{{ java_jdk_version }}"
      tags: java
    - name: Upload .tar.gz file containing binaries from local storage
      copy:
        src: "{{ java_oracle_jdk_package }}"
        dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
      register: download_java_binaries
      until: download_java_binaries is succeeded
      tags: java
    - name: Ensure installation dir exists
      become: true
      file:
        state: directory
        path: "{{ java_home }}"
      tags: java
    - name: Extract java in the installation directory
      become: true
      unarchive:
        copy: false
        src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
        dest: "{{ java_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ java_home }}/bin/java"
      tags:
        - java
    - name: Export environment variables
      become: true
      template:
        src: jdk.sh.j2
        dest: /etc/profile.d/jdk.sh
      tags: java

```

3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.

**Ответ:**

```yml
- name: Install Kibana
  hosts: all
  tasks:
    - name: Set facts for Kibana 11 vars
      set_fact:
        java_home: "/opt/jdk/{{ java_jdk_version }}"
      tags: kibana
    - name: Upload .tar.gz file containing binaries from local storage
      copy:
        src: "{{ java_oracle_jdk_package }}"
        dest: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
      register: download_java_binaries
      until: download_java_binaries is succeeded
      tags: java
    - name: Ensure installation dir exists
      become: true
      file:
        state: directory
        path: "{{ java_home }}"
      tags: java
    - name: Extract java in the installation directory
      become: true
      unarchive:
        copy: false
        src: "/tmp/jdk-{{ java_jdk_version }}.tar.gz"
        dest: "{{ java_home }}"
        extra_opts: [--strip-components=1]
        creates: "{{ java_home }}/bin/java"
      tags:
        - java
    - name: Export environment variables
      become: true
      template:
        src: jdk.sh.j2
        dest: /etc/profile.d/jdk.sh
      tags: java


```

4. Tasks должны: скачать нужной версии дистрибутив, выполнить распаковку в выбранную директорию, сгенерировать конфигурацию с параметрами.

**Ответ:**

```yml

```

5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

**Ответ:**
Проверка идет на таком окружении: локалхост и три различных докер-контейнера.
Линтер собщает о том, что не установлены права доступа к файлам в следующих тасках:
  - Upload .tar.gz file containing binaries from local storage
  - Ensure installation dir exists
  - Extract java in the installation directory

Данные директории еще не созданы

```yml
root@server1:~/learning-ansible/Lesson-ansible-02/ansible-02-playbook# ansible-lint 2-site.yml 
WARNING  Overriding detected file kind 'yaml' with 'playbook' for given positional argument: 2-site.yml
WARNING  Listing 3 violation(s) that are fatal
risky-file-permissions: File permissions unset or incorrect
2-site.yml:10 Task/Handler: Upload .tar.gz file containing binaries from local storage

risky-file-permissions: File permissions unset or incorrect
2-site.yml:17 Task/Handler: Ensure installation dir exists

risky-file-permissions: File permissions unset or incorrect
2-site.yml:33 Task/Handler: Export environment variables

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - experimental  # all rules tagged as experimental

Finished with 0 failure(s), 3 warning(s) on 1 files.
```

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.
 Он может не запуститься. Это нормально. Попытаться сделать так, чтобы с чеком отработал.

**Ответ:**

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

7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

Также можно зайти на систему и там посмотреть
**Ответ:**

```yml

```

8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

**Ответ:**

```yml

```

9. Подготовьте README.md файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

**Ответ:**

10. Готовый playbook выложите в свой репозиторий, в ответ предоставьте ссылку на него.

**Ответ:**
