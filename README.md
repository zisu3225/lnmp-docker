# lnmp-docker
php-fpm容器为工作容器，Dockerfile文件中已经通过脚本安装compose，并添加环境变量，若要启动laravel项目，需进入到此容器下  

`docker-compose exec php-fpm bash`  

进入容器后，通过compose手动安装laravel  

`compose global require "laravel/installer"`  

安装结束后，新建laravel工程  

`laravel new blog`  

修改laravel工程的.env文件，配置数据库参数，cache_driver以及session_driver修改为redis  

在/docker/nginx目录下修改nginx配置文件，指向新建工程的public目录  

运行以下命令启动docker  

`docker-compose up -d`
