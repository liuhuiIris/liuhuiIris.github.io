---
title: centos7-nginx-php
date: 2017-11-30 23:08:13
tags: php
---

# 1.系统环境

阿里云服务器 centos7

nginx version: nginx/1.12.2

# 2.一键php
安装并验证

```bash
yum install -y php

php -v
```

显示以下内容则安装成功
```bash
PHP 5.4.16 (cli) (built: Nov 15 2017 16:33:54)
Copyright (c) 1997-2013 The PHP Group
Zend Engine v2.4.0, Copyright (c) 1998-2013 Zend Technologies
```

启动php--很重要,被这个命令卡了一晚上

```bash
systemctl start php-fpm
```

验证是否成功
```bash
[root@liuhuiiris php_wx]# ps -ef | grep php-fpm

root     31847     1  0 23:02 ?        00:00:00 php-fpm: master process (/etc/php-fpm.conf)
apache   31849 31847  0 23:02 ?        00:00:00 php-fpm: pool www
apache   31850 31847  0 23:02 ?        00:00:00 php-fpm: pool www
apache   31851 31847  0 23:02 ?        00:00:00 php-fpm: pool www
apache   31852 31847  0 23:02 ?        00:00:00 php-fpm: pool www
apache   31853 31847  0 23:02 ?        00:00:00 php-fpm: pool www
root     31855 31234  0 23:02 pts/1    00:00:00 grep --color=auto php-fpm
```

# 3. 配置nginx
配置好相应路径即可，127.0.0.1:9000不要擅自修改
```bash
location / {
    root   /opt/workspace/php_wx;
    index  index.html index.htm index.php;
}

location ~ \.php$ {
    #root           /opt/workspace/php_wx;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    fastcgi_param  SCRIPT_FILENAME  /opt/workspace/php_wx$fastcgi_script_name;
    include        fastcgi_params;
}
```

配置好nginx后reload
```bash
nginx -s reload
```

测试php
```bash
vim /opt/workspace/php_wx/info.php

<?php phpinfo(); ?>
```

在浏览器中打开 IP/info.php,如下图所示
![php](https://liuhuiiris.github.io/img/php/php.png)


大功告成！

