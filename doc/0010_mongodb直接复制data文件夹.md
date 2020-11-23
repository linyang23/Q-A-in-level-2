### 0010_mongodb直接复制data文件夹

如果mongodb的data文件夹是直接复制粘贴而非使用内部的导出接口，那么到时候就会出先在另一台主机上这个data文件夹根本无法使用的情况，这时候的解决方案：
- 删除data文件夹里面的storage.bson文件
- 删除data文件夹里面的mongod.lock文件
- 删除data文件夹里面的WiredTiger.lock文件
- 删除data文件夹里面的WiredTiger.lock文件
- 删除data文件夹里面的journal文件夹
- cd到mongodb的安装路径（.../bin）
- 输入命令：mongod --repair --dbpath /www/server/mongodb/data,后者路径为data文件夹路径
- 等待文件检验和生成，直到cmd无变化后ctrl+z退出
- 输入命令mongod --dbpath /www/server/mongodb/data，等待片刻
- 正常使用