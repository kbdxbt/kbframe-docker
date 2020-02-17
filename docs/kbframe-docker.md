### 安装 kbframe-docker
1.安装git
```
yum -y install git
```
2.git clone项目：
```
git clone https://github.com/kbdxbt/kbframe-docker
```
3.如果不是root用户，还需将当前用户加入docker用户组：
```
sudo gpasswd -a ${USER} docker
```
4.拷贝并命名配置文件（Windows系统请用copy命令），启动：
```
cd kbframe-docker                                 # 进入项目目录
cp env.sample .env                                # 复制环境变量文件
cp docker-compose.sample.yml docker-compose.yml   # 复制 docker-compose 配置文件。默认启动3个服务：
docker-compose up -d                              # 启动
```
#### composer和php 命令配置
参考bash.alias.sample示例文件，将对应 php composer 函数拷贝到主机的 ~/.bashrc文件
```
vi ~/.bashrc
source ~/.bashrc
php -v #查看php命令
composer -v #查看composer命令
```
#### 安装kbframe
1.git clone项目
```
cd www
git clone https://github.com/kbdxbt/kbframe
```
2.安装kbframe
```
cp .env.example .env 
//编辑env文件，配置好相应的配置信息，数据库必须配置
composer install
php artisan app:init
```
3.测试应用
访问 ip+/backend/login
账号：root
密码：123456