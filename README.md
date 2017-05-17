# 纪录自己不常用的 Linux 命令及脚本

## iptables 

```bash
封单个IP的命令：iptables -I INPUT -s 124.115.0.199 -j DROP
　
封IP段的命令：iptables -I INPUT -s 124.115.0.0/16 -j DROP　后二位

封整个段的命令：iptables -I INPUT -s 194.42.0.0/8 -j DROP　后三位

封几个段的命令：iptables -I INPUT -s 61.37.80.0/24 -j DROP　后一位

只封80端口：iptables -I INPUT -p tcp –dport 80 -s 124.115.0.0/24 -j DROP
列出屏蔽Ip条目：iptables -L INPUT --line-numbers

解封：iptables -F

清空：iptables -D INPUT 数字

列出 INPUT链 所有的规则：iptables -L INPUT --line-numbers

保存:service iptables save

重启:service iptables restart
```

## find
```bash
查找当前目录下以tar.gz结尾的文件：find . -name '*tar.gz'

查找当前目录及子目录下所有以.txt和.pdf结尾的文件：find . -name "*.txt" -o -name "*.pdf"

查找当前目录下不以txt结尾的文件：find . ! -name "*.txt"

查找当前目录下以.txt结尾的文件并删除：find . -type f -name "*.txt" -delete

查找当前目录下权限不是644的php文件：find . -type f -name "*.php" ! -perm 644

查找长度为0的文件：find . -empty
```

## trace
```bash
MAC追踪路由：traceroute weibo.com

Win追踪路由：tracert weibo.com
```

## chown
```bash
改变拥有者：chown -R 用户名称 文件目录

```
## chgrp
```bash
改变拥有者：chgrp -R 用户名称 文件目录

```