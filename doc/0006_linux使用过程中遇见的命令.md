### linux使用过程中常用的命令

##### yum install xx(xx可以自定义，为名字)
下载安装xx文件或者包
##### wget xx(xx可以自定义，为链接)
下载xx所指向的文件或者包
##### ll
查看当前目录下的文件情况
##### cd xx(xx可以自定义，为路径)
跳转到xx路径
##### mv xx1 xx2 xx3 ... dir
把文件xx1、xx2、xx3 ... 移动到目录dir中
##### mv xx1 xx2
把文件xx1重命名为xx2
##### rm -f file
删除文件file,在真正删除之前会询问是否进行该操作
##### ps
显示当前进程运行情况
##### jobs
查看当前任务
##### file xx
显示xx的文件类型，比如文件夹、文本等
##### chmod xxx xx
将xx文件的权限更改为xxx
##### su xx(xx为用户名)
切换到xx用户
##### useradd admin -d /home/admin
##### passwd admin
新建用户admin，并更改密码（密码在输入以上命令后会提示输入，重复两次）
##### curl ipinfo.io
获取本机的IP信息
##### ctrl+z
终止当前命令
##### sudo
管理员模式运行命令
##### vim xx
对xx文件进行修改，若xx不存在，则创建一个新文件
##### kill -9 xx(xx为PID号，通过ps命令可以查看正在运行的进程和其PID号码)
强制关闭xx进程
##### whereis xx
查看xx的安装路径
##### mkdir xx
创建文件夹xx
##### pwd
显示当前目录的完整路径
##### ./xx
执行该文件
