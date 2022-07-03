---
layout: post
title: Linuxの特権昇格
published : true
tags: CTF Common cheatsheet linux 特権昇格 Privesc "privilage escaration"
---
## 列挙
### SUID
```sh
find / -perm -4000 2>/dev/null
```

### sudo
```sh
sudo -l
```

### プロセス
```sh
ps awxww
```

### サービス
```sh
ss -antul
```

### apache2 config
```
/etc/apache2/sites-enabled
```

## ssh-keygen プロンプトなし。(RCEでリモートマシン上にssh-keygenするときに使う)
```sh
ssh-keygen -t rsa -f /home/matt/.ssh/id_rsa'
```

## SSH port forwerding
```sh
ssh daniel@panda.htb -L 9999:localhost:80
```

## cron
```sh
cat /etc/cron.d/*
```
and
```sh
cat /var/spool/cron/crontabs/*                cat: '/var/spool/cron/crontabs/*': Permission denied
```

## 監査ログ
- ユーザがadmグループにいるとき、監査ログが確認できる。その他/ver/logの確認も。


```sh
cry0l1t3@academy:/$ id
uid=1002(cry0l1t3) gid=1002(cry0l1t3) groups=1002(cry0l1t3),4(adm)

cry0l1t3@academy:/$ aureport --tty

TTY Report
===============================================
# date time event auid term sess comm data
===============================================
Error opening config file (Permission denied)
NOTE - using built-in logs:
/var/log/audit/audit.log
1. 08/12/2020 02:28:10 83 0 ? 1 sh "su mrb3n",<nl>
2. 08/12/2020 02:28:13 84 0 ? 1 su "mrb3n_Ac@d3my!",<nl>
3. 08/12/2020 02:28:24 89 0 ? 1 sh "whoami",<nl>
4. 08/12/2020 02:28:28 90 0 ? 1 sh "exit",<nl>
5. 08/12/2020 02:28:37 93 0 ? 1 sh "/bin/bash -i",<nl>
```