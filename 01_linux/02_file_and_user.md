# 文件和用户管理

## 文件系统

以.开头的文件为隐藏文件

### 增删改查

#### 创建

创建文件 touch

```shell
touch {filename1} {filename2} ... # 创建多个文件
```
创建文件夹 mkdir

```shell
mkdir -p 1/2/3/4/5 # 如果不存在，递归创建

mkdir ~/{dir1,dir2,...} # 创建多个文件夹

mkdir -vp 1/2/3/4/5/6 # -v 打印
mkdir: created directory '1'
mkdir: created directory '1/2'
mkdir: created directory '1/2/3'
mkdir: created directory '1/2/3/4'
mkdir: created directory '1/2/3/4/5'
mkdir: created directory '1/2/3/4/5/6'
```

#### 删除

删除 rm

- rm \[path\]/* # 不会删除隐藏文件

#### 修改
拷贝 cp
- r - 递归
- f - 强制：例如打开的文件复制走
- n - 不提示

移动 mv

文本内容修改 vim

#### 查询

##### 文件夹查询

子文件查询 ls
```shell
ls -l # 长格式显示详细内容
ls -d
```

工作目录查询 pwd

##### 文件查询

全部查询 cat

全部翻页 more

头几行 head

```shell
head -c12 # 输出12字节内容
head -n12 # 输出12行内容
head -q {filename} # 不输出文件路径（默认）
==> {file path} <==
head -v # 输出文件路径

➜  ~ head -q Downloads/Anaconda3-2023.09-0-Linux-x86_64.sh 
#!/bin/sh
#
# Created by constructor 3.4.5
#
# NAME:  Anaconda3
# VER:   2023.09-0
# PLAT:  linux-64
# MD5:   d2bf41ff259832a949671f4f6cdf6dea

set -eu
➜  ~ head -v Downloads/Anaconda3-2023.09-0-Linux-x86_64.sh
==> Downloads/Anaconda3-2023.09-0-Linux-x86_64.sh <==
#!/bin/sh
#
# Created by constructor 3.4.5
#
# NAME:  Anaconda3
# VER:   2023.09-0
# PLAT:  linux-64
# MD5:   d2bf41ff259832a949671f4f6cdf6dea

set -eu


```

尾几行 tail

内容过滤 grep

### 文件编辑

#### 重定向

\> 和 \>\>

#### 文件编辑器
gedit, vi 和 vim

##### vi的基础操作
vi 分为命令模式，编辑模式末行模式和视图模式：
- ESC - 命令模式输入命令
- : - 末行模式在命令模式下通过:进入，输入命令
- ioaA - 命令模式下进入输入模式
- v, V, \^v - 命令模式下进入视图模式

最常用的命令：
- i - 进入编辑模式
- o - 在下面插入新的行并进入编辑模式
- :wq - 保存并退出
- :q - 退出不保存
- :q! - 强制退出不保存
- yy - 复制行
- p - 粘贴
- dd - 删除行
- u - 撤销上一步操作
- :set nu - 显示行号
- v - 进入视图模式

进入编辑模式：
- o - 下一行插入
- i - 当前光标插入
- a - 光标下一个位置插入
- A - 行末插入

复制粘贴删除等文本操作：
- y - 复制（cop**y**），进入视图模式选取完按y可以直接复制指定内容
- yy - 复制行
- y^ y$ - 复制当前光标到行头/行尾内容
- ygg yG - 复制当前光标到文件头/文件尾的内容
- y\[num\]G - 从当前光标开始复制\[num\]行
- yw, y\[num\]w - 复制一个/\[num\]个单词
- d - 删除
- dd - 删除行
- p - 粘贴
- u - 撤销
- \[num\]u - 撤销\[num\]次操作
- ctrl + r - 恢复
- \[num\]ctrl + r - 恢复\[num\]次操作

光标定位：
- hjkl 左下上右
- 0 $ 行首行尾
- gg G 页首页尾
- \[num\]G 进入第\[num\]行
- /\[str\] 查找字符串\[str\]，enter后，使用n/N查找下一个/上一个

文件保存退出：
- :q - 退出
- :w - 保存
- :w \[filename\] - 另存为\[filename\]
- :wq - 保存并退出

查找替换：
- /\[str\] - 查找字符串\[str\]，enter后，使用n/N查找下一个/上一个
- :\[l1\],\[l2\] s/\[raw_str\]/\[new_str\]/g - 范围替换，从\[l1\]-\[l2\]行，将\[raw_str\]替换成\[new_str\]，在末行模式下进行，不要忽略冒号

设置环境：
- :set nu - 显示行号
- :set nonu - 取消显示行号
- :set list - 显示控制字符

## 用户管理


### 用户信息存储

- /etc/passwd - 用户基本信息文件
- /etc/shadow - 用户密码信息文件
- /etc/group - 组信息文件

#### passwd

用户信息保存在 /etc/passwd 文件中，共七列：
```shell
root:x:0:0:root:/root:/bin/bash
# 用户名:x密码占位符:uid:gid:描述:home路径:shell
ether:x:1000:1000:Ether,,,:/home/ether:/usr/bin/zsh
```

- 用户名
- x - 密码占位符，具体密码不在此
- uid：user id，0为特权用户，1～499为系统用户，1000+是普通用户
- gid: 用户所在组别
- 描述
- home路径
- 登陆shell

IDC（internet database center）互联网数据中心

#### shadow

/etc/shadow 保存了加密后的用户密码，总共九列

```shell
# 用户名：密码的密文：最后修改时间：？：？：？：？：？：？
root:$y$j9T$3XBWxxxx/SbixxxxZrw/$4Lxx.GlbpPTxxxLo.Bx/Xixx:198xx:0:99999:7:::
ether:$y$j9Txxx.NE44Dxxx.MUGszEZ1$TZxxx/X6BeExxx/DWixxx:197xx:0:99999:7:::

user:password:time:?:?:?:?:?
```

1. 用户名
2. 密码的密文，如果为"!!"则说明密码过期
3. 最后一次修改时间，从1970/01/01开始，到修改密码的天数
4. 密码修改最小时间间隔，两次修改密码之间的最小天数，0表示随时可以更改
5. 密码有效最大时间间隔，密码有效期，单位为天，99999代表永久有效
6. 警告时间，在密码到期前n天提醒用户修改密码
7. 不活动时间，n天不登陆系统，禁用该用户
8. 失效时间，账户有效期为n天，过期账号就失效
9. 保留

#### group

组信息文件保存在/etc/group，创建用户时很可能创建一个同名组

```shell
# 组名：组密码：组id：组成成员
root:x:0:
adm:x:4:syslog,ether
sudo:x:27:ether
```

#### shell

shell是命令解释器
- 定义命令
- 接收命令
- 执行命令

常用shell
- /bin/bash
- /bin/sh
- /usr/sbin/nologin


### 用户管理命令

增删改查
- useradd - 增加用户
- id - 查询用户
- who/whoami - 当前用户信息
- passwd - 修改密码
- userdel - 删除用户
- usermode - 修改用户

#### useradd
```shell
useradd [name] -u [id] -d [home_path] -g [基本组] -G [附加组]
```

#### userdel
```shell
userdel -r [name] # 删除用户和用户的home文件夹
```

#### passwd
```shell
passwd # 修改当前账户密码
passwd [user] # 修改别人的密码，只有 super user 可以用
```

#### usermode
```shell
usermode -s /sbin/nologin [user] #  修改默认shell
```

### 用户组管理命令

 - groupadd
 - groupdel
 - groupmems
 - groupmod
 - groups

用户所加入的组分为基本组和附加组，这是对某一个用户来说的概念：
- 基本组：随用户创建的组，如果未指定，组名和用户名相同，/etc/passwd里面记录的唯一组别就是基本组
  - useradd -g 设定用户的基本组
- 附加组：加入的其他组，/etc/group中记录的组别就是附加组
- 用户与未加入的组不构成其他关系

### 提权

- 永久提权：su，转成任意账户
- 临时提权：sudo，像管理员一样执行命令，完成部分特权指令
  - 可以使用sudo的用户记录在 /etc/sudoers

#### su

```shell
su - [username] # -会切变量
su [username] # 不会切变量
```

#### sudo

/etc/sudoers

```shell
# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```