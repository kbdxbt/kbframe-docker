## kbframe-docker 
是一款基于docker为kbframe框架量身打造的环境安装程序

> 使用前希望能了解一定的docker使用基础

内置服务
- nginx
- mysql8 (5.X，支持主从配置)
- php7.4 (7.3,7.2,7.1,5.6,5.4)
- redis (一主两从三哨兵)
- mongodb
- rabbitmq

> elk (elasticsearch+logstash+kibana) ,由于elk对服务器配置要求较高，所以默认关闭，如需开启，编辑docker-compose.yml去掉相应的#号即可 


### 目录
- [安装docker](docs/install-docker.md)
- [安装kbframe](docs/kbframe-docker.md)
- [Mysql主从配置](docs/mysql-master-slave.md)
- [Redis一主两从三哨兵]()

> 本版本为kbframe专用版，修改了部分扩展和新增主从配置等，更多问题请访问源地址https://github.com/yeszao/dnmp

### License
MIT


