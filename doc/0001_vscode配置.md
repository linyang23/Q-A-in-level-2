### 第一个问题：how to use vscode

#### vscode之安装篇
step1: 打开这个网址[vscode](https://code.visualstudio.com/download)  
step2: 下载对应系统的可安装执行文件  
step3: 打开该文件，路径自己决定，其他一路全选(也可以视情况决定)  
step4: 安装完成

Q：什么是将Code注册为受支持的文件类型的编辑器  
A：选中后，VScode支持的代码文件会被设定为默认用VScode打开，比如.txt和.py等后缀的文件  
Q: 什么是添加到Path  
A：选中后会自动配置环境变量，不用自己再操作，打开即用
#### vscode之插件篇
step1: 打开vscode  
step2: 找到左侧边栏，有一个由四个正方形构成的图标，点开即可使用插件商店  
step3: 选中搜索框，输入Chinese，出来的结果中有一个Chinese (Simplified) Language...，点击该栏右下角install，稍等片刻，整个软件右下角会弹出restart的按钮，点击该按钮  
step4: 此时界面变成中文，其他插件同上过程

Q：有哪些插件推荐  
A:   
编程支持: C/C++ | Code Runner | Language Support for Java| Python  
美化: background | Beautify | Bracket Pair Clorizer | Rainbow Csv | vscode-icons | Material Theme  
文件支持：Markdown Preview Enhanced | vscode-pdf  
刷题: Leetcode  
其他: Docker

#### vscode之C/C++配置篇
##### mingw安装配置
step1: 打开这个网址[mingw](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/)  
step2: 拉到页面下方，有一个Mingw-w64-install.exe，点击下载  
step3: 按照顺序从上往下，版本选最新版本；构架按照32位和64位来选择，一般选x86_64；线程部分选择win32，如果是Linux请选择posix；异常模型部分和最后一项选择默认  
step4: 路径自行选择，确保路径中不包含空格和中文字符，记住该路径，后续配置环境变量需要  
step5: 安装完成  
step6: 将上述路径添加到环境变量  
step7: win + r键，输入cmd，进去后输入gcc -v，如果弹出一堆字符，并且最后一行写有gcc的版本，说明配置成功
##### C/C++文件创建
step1: 打开vscode，安装插件: C/C++  
step2: 在文件管理器中创建一个专门用来写C/C++的文件夹  
step3: 使用vscode左上角的文件，点击打开文件夹按钮，将之前创建的文件夹打开  
step4: 左边侧栏两个文件叠加的图标，用于管理该文件夹，指针放在文件夹名上，会出现几个图标，点击其中创建文件图标，命名为xx.c或者xx.cpp，xx自行决定
##### C/C++运行环境配置
step1: 按快捷键Ctrl+Shift+P调出命令面板，输入C/C++，选择“Edit Configurations(UI)”进入配置。这里配置两个选项：   
（第一个选项）编译器路径：此处填写为上面mingw篇第6步的环境变量+gcc.exe或者g++.exe，比如C:/Program Files (x86)/mingw-w64/i686-8.1.0-win32-dwarf-rt_v6-rev0/mingw32/bin/g++.exe  
（第二个选项）IntelliSense 模式：gcc-x64  
step2: 配置完成后，发现项目中多了叫.vscode的一个文件夹，在其中新建launch.json和tasks.json  
step3：[launch.json](https://github.com/linyang23/Q-A-in-level-2/blob/master/.vscode/launch.json)如下(直接复制本文，其中所有的路径改成之前mingw的环境变量路径，gcc、g++、gdb保持不变)  
step4：[tasks.json](https://github.com/linyang23/Q-A-in-level-2/blob/master/.vscode/tasks.json)如下(直接复制本文，其中所有的路径改成之前mingw的环境变量路径，gcc、g++、gdb保持不变)  
step5: 点开c/cpp结尾的文件，编写c/c++代码，按f5运行，然后愉快的debug吧

#### vscode之python篇
##### anaconda安装配置
step1: 打开这个网站[anaconda](https://www.anaconda.com/download/)  
step2: 翻到最下面，下载对应的可执行安装文件  
step3: 点开下载好的该文件，全部默认同意并勾选(这样后续就不用添加环境变量了)，路径自选（尽量不要有空格和中文）  
注1：第四步和第五步根据需要执行，anaconda可以管理多个python版本，第四步和第五步是安装两个版本的过程，如果不需要就不需要执行  
注2：目前的anaconda自带环境为python3.8  
step4: 打开cmd，输入conda create -n python36 python=3.6  
step5: 打开cmd，输入conda create -n python27 python=2.7

Q: 如何查看安装了那些环境  
A: 打开cmd，输入conda env list  
Q: 如何进入指定环境并安装需要的包  
A: 打开cmd，输入conda activate py36(以python3.6为例)，然后输入pip install tensorflow==1.15(以与python3.6适配的tensorflow1.15版本为例)  
Q: 如何进入指定环境并安装需要的包  
A: 打开cmd，输入conda activate py36(以python3.6为例),输入pip list

##### nodejs安装配置
step1: 打开这个网站[nodejs](https://nodejs.org/en/download/)  
step2: 下载对应的可执行安装文件  
step3: 点开下载好的该文件，全部默认同意并勾选，路径自选（尽量不要有空格和中文）

##### Python运行环境配置
step1: 打开vscode，安装插件: Python  
step2: 在文件管理器中创建一个专门用来写Python的文件夹  
step3: 使用vscode左上角的文件，点击打开文件夹按钮，将之前创建的文件夹打开  
step4: 如果整个界面右下角弹出需要安装什么的信息，全部同意并等待安装  
step5：创建python文件，命名为xx.py，xx自行决定  
step6: 按f5，选择Python,然后愉快的debug吧

Q: 怎样使用不同的python版本  
A: 在vscode左下角可以选择使用的python版本
##### Jupyter Notebook配置（puthon进阶编程，可选）
step1: ctrl + shift + p,输入jupyter，选择Python: Create Blank New Jupyter Notebook」选项  
step2: 创建xx.ipynb文件，xx自行决定  
step3: 使用上述anaconda篇中安装包的方法，输入pip install jupyter，安装对应的包  
step4: 点开xx.ipynb文件，然后愉快的debug吧