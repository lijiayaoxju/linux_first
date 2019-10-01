--Linux目录结构
--
	/ 根目录
	/bin 常用指令目录
	/sbin 管理员命令
	/usr/bin 用户常用命令
	/usr/sbin 超级用户常用命令

	/etc 系统配置文件目录，更改可能导致系统无法启动
	/boot 启动时Linux核心文件
	/lib 所用应用程序的动态库
	/sys 系统架构


	/opt 安装软件所在的文件
	/dev 设备目录
	/proc 内存中开辟的虚拟空间
	/home 用户的主目录
	/var 经常修改的文件所在的目录，包括日志等
	/srv 该目录存放这一些程序启动后需要提取的数据

--切换用户 sudo su <用户名>

--文件基本属性
--
	第一个字符表示文件类型：
		d:路径
		-:文件
		l:链接
	剩下的字符三个一组：
		ower,group,others
		r: 可读
		w: 可写
		x: 可执行
	eg: -rwxr-xr-- :一个所有者可读可写可执行，用户组可读可执行，其他人可读的文件
	改变用户组，拥有者：
		chown [-R] <用户名> <文件>
		chgrp [-R] <用户组> <文件>
		-R 为递归更改，将文件夹内所有文件属性更改
	改变读写执行权限：
		chmod [-R] xyz <文件> 
		xyz:对应权限的数字相加 x:拥有者 y:用户组 z:其他
		r:4 w:2 x:1   rwx:7 r-x:5

--文件目录管理
--
	ls [-lad]
	cd 
	pwd [-P]

	mkdir -m 777 -p <文件夹> ： -m:修改权限 -p: 递归创建
	目录的权限关系到是否可以在此目录新建文件
	rmdir -p <目录> 

	cp [-ipr] 源 目 -i:覆盖是否提示 -p:是否连同文件属性 -r：递归调用

	rm [-ir] < >    -i:删除前询问 -r:递归
	mv 文件名1 文件名2 ：将文件名1改为文件名2
	mv [-ui]   s1 s2 .. dir -i:覆盖提示 -u: s较新的时候才会覆盖

--
	cat [-AbEnTv] 文件
	tac 文件内容从最后一行察看
	nl -b STYLE -n FORMAT <file> 
	STYLE:a t(空行不显示行号)  FORMAT: ln:行号左侧显示 rn:行号右侧显示不加0 rz:行号右侧显示加0
	less <file>
	q:退出查看
	空格：像下翻页
	b:像上翻页
	/<str>： 查找字符串str
	n: 前一个搜寻 
	N: 后一个搜寻
	head [-n number] <flie>:从文件开始显示number行
	tail [-n number] <file>:从文件结尾开始显示number行

用户和用户组管理
--
	与用户用户组有关的文件：/etc/passwd /etc/group
	/etc/passwd中数据格式：
		用户名：口令：用户ID:用户组ID:说明：用户主目录：登陆shell
		口令：不是密码，出于安全考虑一般为x
		用户ID: 每个用户有一个不同的ID 0为root 1～499系统所有 500之后为普通用户所有
		用户组ID: 每个ID对应/etc/group中一条
		说明： 随意说明
		用户主目录：用户工作所在的目录
		登陆shell：用户登陆后所运行的shell
	/etc/group中数据格式：
		组名：口令：组织ID:组内用户列表
	 	口令：一般为x
--
	批量添加/删除用户
	newusers < users.txt 
	users.txt 中的数据为按照/etc/passwd的数据格式，口令空着，一行一个用户
	pwunconv
	chpasswd < passwd.txt 
	passwd.txt 中的数据格式为 用户名：密码 一个一个用户
	pwconv

	pwunconv是将加密密码转到/etc/passwd中，用来修改
	pwconv 将密码隐藏到shandow文件中（此文件只有root读写权限）

磁盘管理：
--
	查看磁盘用量：df -h 文件夹 
	这是用来显示该文件夹所在的文件系统的信息，而非该文件夹大小
	查看该文件/文件夹大小 df -sh 文件夹 -s作用为只列出该文件而不用列出该文件夹中下属文件/目录大小




