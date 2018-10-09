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

## 命令行获取公网 IP

### curl ipinfo.io
```bash
$ curl ipinfo.io
```
    {
    "ip": "124.116.223.84",
    "city": "Xi'an",
    "region": "Shaanxi",
    "country": "CN",
    "loc": "34.2583,108.9286",
    "org": "AS4134 CHINANET-BACKBONE"
    }

### curl httpbin.org/ip
```bash
curl httpbin.org/ip
```

    {
    "origin": "124.116.223.84"
    }

### curl myip.ipip.net
```bash
$ curl myip.ipip.net
```
> 当前 IP：124.116.223.84  来自于：中国 陕西 宝鸡  电信

### curl ip.sb
```bash
$ curl ip.sb
```
    124.116.223.84

### curl -s ifcfg.cn/echo |python -m json.tool
```bash
$ curl -s ifcfg.cn/echo |python -m json.tool
```
    {
        "headers": {
            "ACCEPT": "*/*",
            "CONNECTION": "close",
            "HOST": "ifcfg.cn",
            "USER-AGENT": "curl/7.54.0"
        },
        "host": "ifcfg.cn",
        "ip": "124.116.223.84",
        "location": "\u4e2d\u56fd \u9655\u897f \u5b9d\u9e21",
        "method": "GET",
        "path": "/echo",
        "protocol": "http",
        "query_string": "",
        "url": "http://ifcfg.cn/echo",
        "user_agent": "curl/7.54.0"
    }

### curl ifconfig.me
```bash
$ curl ifconfig.me
```

    load: 2.35  cmd: curl 13313 waiting 0.00u 0.00s
    124.116.223.84

## 80端口被占用
```bash
$ lsof -i :80
```

## Telnet 测试开放端口
```bash
# quit 退出
$ telnet ip 端口
```

## 数据库
```bash
# 监听的端口列出来
netstat -anp|grep 3306
```

## Git
```git
# 提交日志
git log 
# 恢复文件
git checkout [file] 
# 与主干同步
git fetch origin
git rebase origin/master
# <username> 用户名称
git remote add origin git@github.com:<username>/larabbs.git 
# 过滤
git update-index --assume-unchanged config/pay.php 
```

## Editorconfig
```code
# coding styles between different editors and IDEs
# editorconfig.org

root = true

[*]

# Change these settings to your own preference
indent_style = space
indent_size = 4

# We recommend you to keep these unchanged
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = false

[*.{js,html,blade.php,css,scss}]
indent_style = space
indent_size = 4

[*.md]
trim_trailing_whitespace = false
```

## syncthing
```bash
# 查看服务器系统版本
cat /proc/version 

# 下载 syncthing
wget https://github.com/syncthing/syncthing/releases/download/v0.14.5/syncthing-linux-amd64-v0.14.5.tar.gz

# 解压
cd ~
tar xzvf syncthing-linux-amd64-v0.14.5
cd syncthing-linux-amd64-v0.14.51
./syncthing

# 修改配置文件，让其可远程访问
vim /root/.config/syncthing/config.xml

<gui enabled="true" tls="false" debugging="false">
    <address>127.0.0.1:8384</address>
    <user>administrator</user>
    <password>$2a$10$OGJCfTrVPHDmPwrBQHxubuaKyXvd6233rnPnuIQ9GCbNWxp5DiMMu</password>
    <apikey>xhgYWNrtQTjQe6jXAiioWWgZYxXKRSPn</apikey>
    <theme>default</theme>
</gui>

# 将 127.0.0.1:8384 修改为 0.0.0.0:8384
<address>127.0.0.1:8384</address>

# 放行 8384 端口 (注意：如若是阿里云的服务器需要填加例外规则)
/sbin/iptables -I INPUT -p tcp --dport 8384 -j ACCEPT
/etc/init.d/iptables save
service iptables restart

# bin
cp syncthing /usr/local/bin

# 后台执行
which syncthing 
nohup syncthing & 或者 nohup /usr/local/binsyncthing &
```