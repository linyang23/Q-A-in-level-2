### how to create wordpress

##### 购买域名，我买了一个WindAlso.top(当然，可以不用域名访问，直接通过阿里云服务器ip也可以)
step1: 打开这个网站[阿里万网域名注册](https://wanwang.aliyun.com/domain)，里面有1元的域名可以购买(比如.top,.work等)  
step2: 注册自己中意的域名，买之前查询好是否已被注册，然后购买即可，购买中间需要登记个人信息，验证邮箱和身份证（需要审核照片）  
step3: 支付宝扫码付款，购买完成，照片未审核完的购买后状态如图![windalso](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/windalso.png)  

##### 域名解析到ip
step1: 打开[阿里云](https://homenew.console.aliyun.com/)  
step2: 点击左上角三条线，选择域名，打开域名解析控制台  
step3: 找到自己购买的域名，选择操作下方的解析，选择添加记录，在记录值中写下之前ecs服务器实例的公网ip[公网ip](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/explainip.png),主机记录填写www  
下面是如果没有备案的情况下用域名访问的情况，也就是说如果没有备案域名，就只能通过阿里服务器的ip才能访问搭建的wordpress博客  
![备案](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/beian.png)  

##### 登录云服务器
step1: 点击实例中远程连接旁边的管理，点击左边本实例安全组，点击其中正在使用的那条右边的配置规则按钮  
step2: 点击手动添加，目的写80/80（因为wordpress需要80端口才能访问到），源为0.0.0.0/0   
step3: 实例创建3个月后，就可以对域名进行备案了，不然无法直接访问  
step4: win+x,选择windows powershell（管理员）  
step5：输入ssh -V，如下图显示，则说明已经装好了ssh工具，若没有安装，可以下载安装OpenSSH  
![ssh工具](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/ssh.png)  
step6: 输入命令**ssh root@xxx.xxx.xxx.xxxx**（此处为你的公网ip）  
注: 也可以不需要4、5步，后续所有步骤在workbench[见此页面](https://github.com/linyang23/Q-A-in-level-2/blob/master/doc/0003_vscode%E9%85%8D%E7%BD%AE%E9%98%BF%E9%87%8C%E4%BA%91.md)的终端中跑  

##### 安装Apache HTTP服务
step7: 输入命令，安装Apache服务和扩展包，**yum -y install httpd httpd-manual mod_ssl mod_perl mod_auth_mysql**.注：对于centos7.3以及之后的版本，可能mod_auth_mysql无法通过这种方式安装，不用担心，后续报错之后按照所说方式解决即可  
step8: 使用**systemctl start httpd.service**启动Apache服务  
step9: 在浏览器访问你的IP地址 **http://<云服务器公网地址>**，测试Apache服务是否安装成功，如果测试也页能打开，说明安装成功  

##### 安装 MySQL 数据库
step10: 下载并安装MySQL官方的Yum Repository,命令如下  
**wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm  
yum -y install mysql57-community-release-el7-10.noarch.rpm  
yum -y install mysql-community-server**  
如果运行完显示**Unable to find a match: mysql-community-server**（这是因为yum源安装mysql查找失败，需要yum源配置mysql，实现下载），则继续执行以下命令：  
先执行：**yum module disable mysql**，弹出选择yes  
再执行：**yum -y install mysql-community-server**  
step11: 启动 MySQL 数据库,命令为**systemctl start mysqld.service**  
step12: 查看下MySQL运行状态（显示为绿色的active则表示已经开启）,命令为**systemctl status mysqld.service**  
step13: 查看一下MySQL初始密码，用于后续登录。命令为**grep "password" /var/log/mysqld.log**,注意是英文的双引号  
step14:登录数据库,命令为**mysql -uroot -p**，输入上面初始密码（不会明文显示）  
step15：修改默认密码为**NewPassWord1.**(注意有个英语句号)，命令为**ALTER USER 'root'@'localhost' IDENTIFIED BY 'NewPassWord1.';**(注意命令有分号,且引号为英语单引号，按crtl+z可以退出该模式)  
step16： 创建WordPress数据库，命令为**create database xx;(注意命令有分号)**，xx由自己决定，这里我们使用**create database wordpress;**  
step17: 查看数据库创建情况，命令为**show databases;**  
step18: 输入exit或者ctrl+z退出数据库  

##### 安装PHP语言环境
step19: 安装php环境，命令为**yum -y install php php-mysql gd php-gd gd-devel php-xml php-common php-mbstring php-ldap php-pear php-xmlrpc php-imap --skip-broken**
注：对于高版本的centos，需要添加yum源地址，命令如下  
**rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm**  
**rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-8.rpm**  
添加相关的库后，启用 PHP 7.4 的 Remi 模块并进行安装，命令为：**dnf -y install dnf-utils**  
然后安装php-74，命令为**：**yum install php74-php** 和 **yum install php-mysql gd php-gd gd-devel php-xml php-common php-mbstring php-ldap php-pear php-xmlrpc php-imap --skip-broken**  
step20: 创建PHP测试页面,命令为**echo "\<? php phpinfo(); ?>" > /var/www/html/phpinfo.php**  
step21: 打开浏览器，访问**http://<云服务器公网地址>/phpinfo.php**,如果页面显示很多内容，说明成功，如果只显示一行源代码，说明失败，这时候输入**service httpd restart**重启httpd服务即可，再刷新刚才的页面，会发现恢复正常了

##### Wordpress安装和配置
step22: **yum -y install wordpress**(安装wordpress) ，如果出错的话换成这步且步不进行step23和step26：先输入**cd ~**,然后输入**wget http://wordpress.org/latest.tar.gz**(做好下载特别慢的准备)，下载完之后解压**tar xzvf latest.tar.gz** ，拷贝到/var/www/html/wordpress目录**sudo rsync -avP ~/wordpress/ /var/www/html/wordpress/**，切换到wordpress目录**cd /var/www/html/wordpress**，复制wp-config.php文件**cp wp-config-sample.php wp-config.php**，编辑wp-config.php文件**sudo vim wp-config.php**，然后在配置文件里设置正确的值（如果提示已有文件，则按e进入，进去后按s或者i进入修改模式，修改完成后按esc推出编辑模式，然后按shift+:,输入x回车即可保存退出）：  
// ** MySQL settings - You can get this info from your web host ** //  
/** The name of the database for WordPress */  
define('DB_NAME', 'database_name_here');  
/** MySQL database username */  
define('DB_USER', 'username_here');  
/** MySQL database password */  
define('DB_PASSWORD', 'password_here');  
/** MySQL hostname */  
define('DB_HOST', 'localhost');  
设置值参考step26  
step23: **cd /usr/share/wordpress**（指到路径）,然后**ln -snf /etc/wordpress/wp-config.php wp-config.php**（修改路径），接着输入**ll**（查看修改后的目录结构）  
step24：**mkdir /var/www/html/wp-blog**（在Apache的根目录/var/www/html下，创建一个wp-blog文件夹，这个文件夹将会用来放你的WordPress网站程序）  
step25: **mv * /var/www/html/wp-blog/**(把当前目录wordpress下的文件全部移到/var/www/html/wp-blog下)  
step26: **sed -i ‘s/database_name_here/wordpress/’ /var/www/html/wp-blog/wp-config.php
sed -i ‘s/username_here/root/’ /var/www/html/wp-blog/wp-config.php  
sed -i ‘s/password_here/NewPassWord1./’ /var/www/html/wp-blog/wp-config.php**，（这三个命令是修改三个参数，database_name_here为之前步骤中创建的数据库名称，此例子是wordpress；username_here为数据库的用户名，此例子为root；password_here为数据库的登录密码，此例子为NewPassWord1.）  
step27: **cat -n /var/www/html/wp-blog/wp-config.php**(查看配置文件信息是否修改成功)  
step28: **systemctl restart httpd**(重启Apache服务)  

##### 使用WordPress
step29: 打开浏览器并访问**http://<云服务器的公网IP>/wp-blog/wp-admin/install.php**，输入自己想要的站点名称】用户名和密码，填写邮箱，然后登录愉快的使用吧.如果访问说Your PHP installation appears to be missing the MySQL extension which is required by WordPress.则说明php安装mysql相关不完整，可以添加命令：  
**yum install php74-php-pecl-mysql-xdevapi**  
**yum install php74-php-pecl-mysql**  
**yum install php74-php-mysqlnd**  
然后重复step28，就可以得到正常的网站显示了  
![wordpress](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/wordpress.png)  
注册后，登录好的wordpress管理界面如下：  
![wordpress](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/wordpresstop.png)   
这是外面访问的页面：  
![wordpress](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/wordpresscover.png)  


Q: 如何卸载php？  
A：输入命令，**rpm -qa|grep php**，查看安装的包有哪些，然后通过**rpm -e xx**分别删除，其中xx为包名，如果无法删除，则会提示其依赖于哪些包，先卸载这些被依赖的包，然后即可删除之前无法删除的包  
Q: 如何删除数据库？  
A：**drop database <数据库名>;**（输入此命令）  
Q: php如何显示安装了哪些模块？  
A：输入命令**php -m**  
