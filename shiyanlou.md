## 挑战：备份日志
---
小明是一个服务器管理员，他需要每天备份论坛数据（这里我们用 ```alternatives.log``` 日志替代），备份当天的日志并删除之前的日志。而且备份之后文件名是 年-月-日 的格式。```alternatives.log``` 在 ```/var/log/``` 下面
### 目标
---
- 为 shiyanlou 用户添加计划任务
- 每天凌晨 3 点的时候定时备份 ```alternatives.log``` 到 ```/home/- shiyanlou/tmp/``` 目录
- 命名格式为 年-月-日，比如今天是 2017 年 4 月 1 日，那么文件名为 ```2017-04-01```
  ```shell
  $ sudo apt-get install -y rsyslog //下载rsyslog
  $ sudo service rsyslog start  //启动rsyslog服务
  $ sudo cron -f &  //启动crontab
  $ crontab -e //打开crontab，添加一个计划任务
  //文件内输入
  0 3 * * * sudo cp /var/log/alternatives.log /home/shiyanlou/tmp/$(date '+%Y-%m-%d')
  ```

### 提示语
- date
  ```shell
  $ date '+%Y-%m-%d'  //按自己的格式显示年月日
  2021-05-14  
  ```
- crontab
- cp 命令
- 用一条命令写在crontab里面即可，不用写脚本

注意 crontab 的计划任务设定的用户：
```shell
$ crontab -e 表示为当前用户添加计划任务
$ sudo crontab -e 表示为root用户添加计划任务
```