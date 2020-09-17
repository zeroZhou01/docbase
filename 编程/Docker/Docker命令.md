##Dcoker常用命令

####安装docker 
yum install docker ce

####修改镜像源
vim /etc/docker/daemon.json
添加
{
"registry-mirrors":["https://docker.mirrors.ustc.edu.cn"]
}

ustc清华镜像：https://docker.mirrors.ustc.edu.cn
docker中国社区：https://registry.docker-cn.com

####启动docker服务
systemctl start docker

#### 查看镜像
docker images

#### 查看所有容器
docker ps a

#### 查看正在运行的容器
docker ps 


#### 创建容器 
docker run -di --name=mytomcat -p 9000:8080 -v /usr/local/webapps:/usr/local/tomcat/webapps tomcat:7-jre7

-it 交互模式
-id 守护者模式
#### 进入容器
sudo docker exec -it 775c7c9ee1e1 /bin/bash 

#### 启动容器
docker start 

#### 停止容器
docker stop

#### 删除容器
docker rm 

#### 删除镜像
docker rmi

#### 查找镜像 
docker search mysql

####将文件拷贝进入容器
docker cp 文件 容器名：/路径

####将文件拷贝出来
docker cp 容器名：文件路径 宿主机路径

####目录挂载
docker run -dit -v 宿主机目录：容器目录


####Docker备份迁移
保存为镜像
docker commit mynginx mynginx_i

保存为文件
docker sava  -o mynginx.tar mynignx_I

恢复成镜像
docker load -i mynginx.tar


## 安装MySQL
#### 查看docker可用版本
方式1 https://hub.docker.com/_/mysql?tab=tags 
方式2 docker search

#### 拉取官方最新镜像
docker pull mysql:latest

#### 查看本地镜像是否已经有mysql镜像
docker images

#### 运行容器
docker run -itd --name mysql-test -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mima mysql

#### 查看是否已经安装
docker ps -a

#### 进入容器
docker exec -it mysql /bin/bash

#### 登录mysql
mysql -uroot -pmima

####修改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY 'mima'

####添加远程登录用户
CRATE USER 'name;@'%'IDENTIFIED WITH mysql_native_password BY 'mima' 
GRANT ALL PRIVILEGES ON *.* TO 'name'@'%';


---
## 安装Tomcat镜像
#### 查看镜像
方式一 https://hub.docker.com/_/tomcat?tab=tags
方式二 docker search tomcat

#### 拉取镜像
docker pull tomcat

#### 查看tomcat镜像
docker images|grep tomcat


####创建容器
docker run -dit --name mysql -p 8080:8080 -v /usr/locat/webapps:/usr/local/tomcat/webaspps tomcat

#### 查看当前容器运行情况
dcoer ps -a