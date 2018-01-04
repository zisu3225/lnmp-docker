# lnmp-docker 测试方法

下载本项目后，启动docker  
`docker-compose up -d`  
php-fpm容器为工作容器，Dockerfile文件中已经通过脚本安装compose，并添加环境变量，若要启动laravel项目，需进入到此容器下   
`docker-compose exec php-fpm bash`  

进入容器后，通过compose手动安装laravel    
`compose global require "laravel/installer"`    

安装结束后，进入到容器内的www目录，新建laravel工程   
`cd /var/www`  
`laravel new blog`   
`exit`  
此时新工程的目录已经与docker中www目录同步，因docker中未安装vim，因此需退出php-fpm容器修改./www/blog/.env文件  

修改laravel工程的.env文件，配置数据库参数，cache_driver以及session_driver修改为redis   
#### 修改mysql配置
DB_HOST=mysql  
DB_DATABASE=blog  
DB_USERNAME=root  
DB_PASSWORD=123456  

#### 修改redis配置
CACHE_DRIVER=redis  
SESSION_DRIVER=redis  

REDIS_HOST=redis  
REDIS_PASSWORD=123456  

在/docker/nginx目录下修改nginx配置文件，根目录指向新建工程的public目录，本项目默认指向blog工程的public目录
若需修改配置文件，需重新启动docker

`docker-compose up -d`

再次进入到php-fpm容器  
`docker-compose exec php-fpm bash`  
`cd /var/www/blog`  
`php artisan make:Auth`  
`php artisan migrate`  
*laravel 工程启动时若报错Predis\Client找不到，请执行compose require "preids/predis"*  

#### 反向代理测试
反向代理利用nginx开放的81端口，反向代理到www.baidu.com

