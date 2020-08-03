# docker-compose.yml 通过docker搭建lnmp环境
php7.4(redis swoole) 
maraidb10.4 
nginx1.16 
redis5.0.7

#### 1.先安装docker和docker-compose
安装方法这里不进行描述
#### 2.先到php目录下执行构建镜像的代码
`docker build -t hwphp:7.4 .`

构建镜像完成后~执行启动容器命令

`docker run -d --name hwphp-fpm hwphp:7.4`

进入容器

`docker exec -it hwphp-fpm /bin/bash`

进入 /usr/local/etc/php 目录会有php.ini-development （开发环境用）与php.ini-production（生产环境用）两个文件

`cp php.ini-production php.ini`

然后退出容器，从容器里面拷文件到宿主机

`docker cp hwphp-fpm:/usr/local/etc/php/php.ini /data/lnmp/php/php.ini`

`docker cp hwphp-fpm:/usr/local/etc/php-fpm.d/www.conf /data/lnmp/php/www.conf`

#### nginx下创建配置文件
/data/lnmp/nginx/nginx.conf
/data/lnmp/nginx/conf.d/default.conf

#### docker-compose.yml文件内容请参考

执行 `docker-compose up -d` 安装文件和启动服务

docker-compose ps  查看运行情况，State全部为Up时，这说明服务都启动成功

然后到www/demo.com/ 目录下新建几个php文件进行测试吧~~ 
