# Demo on supervisor

## Installation
To install supervisor on CentOS, please run the following commands in the console:
```bash
sudo su -
yum install python-setuptools
easy_install supervisor

supervisord -version
```

## Configure supervisord in your environment
```bash
echo_supervisord_conf  >  /etc/supervisord.conf
vi /etc/supervisord.conf
mkdir -p /etc/supervisor/conf.d/
vi /etc/supervisor/conf.d/block_parser.ini
(user - centos: mkdir -p /data/block-parser/logs)

vi /usr/lib/systemd/system/supervisord.service
# https://www.jianshu.com/p/e1c3e6fbae80
systemctl enable supervisord.service
```

## Start & stop supervisord
```bash
systemctl start supervisord.service
systemctl status supervisord.service
systemctl stop supervisord.service
```

## Supervisorctl
Switch to root user `sudo su -`
```bash
# help
supervisorctl help
# status
supervisorctl status
# reload & update
supervisorctl reload
supervisorctl update
# start, stop & restart
supervisorctl start <your_program_name>
supervisorctl stop <your_program_name>
supervisorctl restart <your_program_name>
```

## Other commands
1. after update /etc/supervisord.conf file, do the following to reload the latest configuration:
```bash
sudo service supervisord reload
```
2. 如果修改了supervisor.service文件，可以通过reload命令来重新加载配置文件
```bash
systemctl reload supervisord.service
```