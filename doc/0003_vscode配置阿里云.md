### 0003：how to use aliyun with vscode

##### 购买阿里云服务（此处为学生免费申请活动）
step1: 打开这个网站[免费领取6个月阿里云服务器](https://link.zhihu.com/?target=https%3A//developer.aliyun.com/adc/student)  
step2：登录支付宝，注册阿里云账号  
step3: 登录后，答题通过，然后点击领取，点击这个网站[阿里云服务器白嫖攻略](https://www.cnblogs.com/HGNET/p/12397741.html)查看题库

##### 阿里云ecs密钥配置
step1: 打开这个网站[阿里云ecs控制台](https://ecs.console.aliyun.com/)  
step2：点击左侧实例与镜像，选择实例，然后点击更多，选中密码/密钥中的重置实例密码，修改为想要的密码![重置密码](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/restartkey.png)  
step3: 重启实例
step4：点击远程链接![远程连接](https://github.com/linyang23/Q-A-in-level-2/blob/master/photo/farconnect.png)  
step5: 选择workbench的立即登录，会跳转一个网页  
step6: 填写密码，其他不用修改

##### vscode配置
step1: vscode下载安装remote-ssh插件  
step2: 在 vscode setting里搜索 remote.SSH.showLoginTerminal 配置项，并开启它（倘若此项没开启，连接服务器时将会一直停留在连接状态）  
step3：按Ctrl + Shift + P 打开命令查找，输入 Remote-SSH:Open Configuration File，选择打开 C:\Users\你的本机用户名\.ssh\config 文件，修改为(**记得删掉#和后面的内容**)：
// config 文件  
Host AliServer11  #AliServer11可以自己随意取    
    HostName XXX.XX.XX.XXX  #你的服务器公网IP，在之前的实例里面有  
    User root  #登陆服务器的用户名，一般是root  
step4: 再次打开命令查找，输入Remote-SSH:Connect Current Window to Host ，选择刚配置好的远程服务 AliServer11，等待连接  
step5: 连接成功在 vscode 的 TEMINAL （Ctrl + ` 可快速打开）中会提示输入登陆密码，回车即可  
