#  Linux

## 一、Linux基础命令

1.Linux系统的目录结构

- Linux目录结构是一个树型结构
- Linux没有盘符，只有一个**根目录/**,所有文件都在它下面

2.Linux路径描述方式

- Linux系统中，路径之间的层级关系，使用：/来表示
- 出现在开头的/表示根目录，出现在后面的/表示层级关系

### 1.Linux命令入门

- 基础命令
  - command [-options] [parameter] 
  - command是命令本身，-options(可选)命令的一些选项，可以通过选项控制命令的行为细节
  - parameter：[可选]  命令的参数，多数用于命令的指向目标
  - 如：ls -l /home/yyue, ls是命令本身，-l是选项，/home/yyue是参数
    - 以列表的形式显示/home/yyue目录的内容
- ls命令入门
  - 列出目录下的内容
  - 语法：ls [-a -l -h] [Linux路径]
  - Home目录：每个用户在Linux系统的专属目录，默认在：/home/用户名
  - 当前工作目录：Linux命令在执行命令时，需要一个工作目录，打开命令行程序(终端)默认设置工作目录在用户的HOME目录
- ls命令的参数和选项
  - 当ls不使用参数，表示列出：当前工作目录的内容，即用户的HOME目录
  - 当使用参数，ls命令的参数表示：指定一个Linux路径，列出指定路径内容
  - -a选项，表示：all的意思，即列出全部文件（包含隐藏的文件/文件夹）。以.开头的表示Linux系统的隐藏文件
    - ![](D:\mybatis笔记\images\linux1.png)
  - -l选项，表示：以列表的形式展示内容，并展示更多信息
    - 语法中的选项是可以组合使用的，比如-a和-l可以组合应用
    - ls -l -a
    - ls -la
    - ls -al
  - -h选项，表示以易于阅读的形式，列出文件大小，如K,M,G
    - -h选项必须要搭配-l一起使用

### 2.目录切换相关命令（cd/pwd）

通过cd命令，更改当前所在的工作目录，cd:Change Directory 

语法：cd [Linux路径]

- cd命令无需选项，只有参数，表示切换到哪个目录下 

- cd命令直接执行，不写参数，表示回到用户的HOME目录

  pwd查看当前工作目录，查看当前所在的工作目录，pwd:Print Work Directory

- pwd命令，无选项，无参数，直接输入pwd

### 3.相对路径、绝对路径和特殊路径符

- 绝对路径：以根目录为起点，描述路径的一种写法，路径描述以/开头
- 相对路径：以当前目录为起点，描述路径的一种写法，路径描述无需以/开头
- 特殊路径符：
  - .  表示当前目录，比如cd ./Desktop表示切换到当前目录下的Desktop目录内，和cd Desktop效果一致
  - ..  表示上一级目录，比如cd ..即可切换到上一级目录或cd ../..切换到上两级目录
  - ~  表示HOME目录，比如cd ~ 即可切换到HOME目录或cd ~、Desktop，切换到HOME内的Desktop

### 4.创建目录命令（mkdir）

mkdir命令可以创建新的目录（文件夹）

语法：mkdir [-p] Linux路径

- 参数必填，表示Linux路径，即要创建的文件夹的路径，相对路径或绝对路径均可
-   -p选项可选，表示自动创建不存在的父目录，适用于创建连续多层级的目录
- **注：**创建文件夹需要修改权限，确保操作均在HOME目录内，不要在HOME外操作，涉及到权限问题，HOME外无法成功

### 5.文件操作命令（touch、cat、more）

1.touch命令：创建文件

 语法：touch Linux路径

- touch命令无选项，参数必填，表示要创建的文件路径，相对、绝对、特殊路径均可以使用

2.cat命令：查看文件内容

语法：cat Linux路径

ctrl+l清空屏幕

3.more命令：查看文件内容

​		与cat不同之处：cat是直接将内容全部显示出来，more支持翻页，如果文件内容过多，可以一页页的展示

语法：more Linux路径，，查看的过程中可以通过空格进行翻页，可以通过q退出查看

### 6.文件操作命令（cp、mv、rm）

1.cp命令：复制文件文件夹

语法：cp [-r] 参数1 参数2

- -r选项，用于**复制文件夹**使用，表示递归
- 参数1，Linux路径，表示被复制的文件或文件夹
- 参数2，Linux路径，表示要复制去的地方

2.mv命令：移动文件或文件夹

语法：mv 参数1 参数2

- 参数1，Linux路径，表示被移动的文件或者文件夹
- 参数2，表示要移动去的地方，如果目标不存在，则进行改名，确保目标存在

3.rm命令：删除文件、文件夹

语法：rm [-r -f] 参数1 参数2 ············

- 同cp命令，-r用于删除文件夹
- -f表示force，强制删除（不会弹出提示）
- 参数表示要删除的文件或文件夹

rm命令支持通配符*，用来做模糊匹配

- 符号*表示通配符，即匹配任意内容（包括空）
- 如：test*，表示匹配任何以test开头的内容
- *test，表示匹配任何以test结尾的内容
- \*test*表示匹配任何包含test的内容

###  7.查找命令（which、find）

1.which命令：查看所使用的一系列命令的程序文件存放的位置

语法：which 要查找的命令

如：which pwd

2.find命令：按文件名查找文件

语法：find 起始路径 -name “被查找文件”

被查找文件名，支持使用通配符*来做模糊查询

- 符号*表示通配符，即匹配任意内容（包括空）
- 如：test*，表示匹配任何以test开头的内容
- *test，表示匹配任何以test结尾的内容
- \*test*表示匹配任何包含test的内容

find命令：按文件大小查找文件

语法：find 起始路径 -size +|-n[kMG]

- +、-表示大于和小于
- n表示大小数字
- kMG表示大小单位，k(小写字母)表示kb，M表示MB，G表示GB
- 如：查找小于10KB的文件 ：find / -size -10k
- 查找大于100MB的文件：find / -size +100M
- 查找大于1GB的文件：find / -size +1G

### 8.grep、wc和管道符

1.grep命令：从文件中通过关键字过滤文件行

语法：grep [-n] 关键字 文件路径

- -n，表示在结果中显示匹配的行的行号
- 关键字：表示过滤的关键字，带有空格或者其他特殊字符，建议使用“”将关键字包围起来
- 文件路径：表示要过滤内容的文件，作为内容输入端口

2.wc命令：统计文件的行数、单词数量等

语法：wc [-c -m -l -w] 文件路径

- -c统计bytes数量
- -m统计字符数量
- -l统计行数
- -w统计单词数量
- 文件路径：被统计的文件，可作为内容输入端口

3.管道符：|

含义：将管道符左边命令的结果，作为右边命令的输入

如：cat yyue.txt | grep yyue     

- cat yyue.txt 的输出结果（文件内容） 
- 作为右边grep命令的输入（被过滤的文件）

### 9.echo、tail和重定向符

1.echo命令：在命令行内输出指定内容

语法：echo 输出的内容 

- 输出的内容，复杂内容可以用”“包围
- 如：在终端上显示：hello Linux   可以使用echo hello Linux 或者 echo "hello Linux"

2.反引号`

- echo pwd 输出的是pwd，本意想要输出当前的工作路径，但是被当作普通字符输出了
- 可以通过将命令用反引号将其包围，被反引号包围的内容，会被作为命令执行，而非普通字符.
- echo \`pwd\`

3.重定向符:>和>>

- \>将左侧命令的结果，覆盖写入到符号右侧指定的文件中
- \>>将左侧命令的结果，追加写入到符号右侧指定的文件中

如：echo "linux hello" > yyue.txt       ls >> yyue.txt    只要是能产生结果的就可以重定向到指定文件中

4.tail命令：查看文件尾部内容，跟踪文件的最新更改

语法：tail [-f -num] Linux路径

- linux路径表示被跟踪的文件路径
- -f表示持续跟踪
- -num表示查看尾部多少行，不填默认10行

### 10.vi编辑器

vi：Linux中最经典的文本编辑器

vim：vi的加强版本，兼容vi的所有指令，不仅能编辑文本，还具有shell程序编辑的功能，可以不同颜色的字体；来辨别语法的正确性。

三种工作模式：

- 命令模式：所敲的按键编辑器都理解为命令，以命令驱动执行不同的功能。此模型下，不能自由进行文本编辑
- 输入模式：即编辑模式、插入模式。此模式下，可以对文件内容进行自由编辑。
- 底线命令模式：以：开始，通常用于文件的保存、退出

命令模式：

- vi/vim 文件路径

- 若文件路径表示的文件不存在，那么此命令会用于编辑新文件

- 若文件路径表示的文件存在，此命令用于编辑已有文件

- 快捷键：

  - i：在当前光标位置进入输入模式
  - a：在当前光标位置之后进入输入模式
  - I：在当前行的开头，进入输入模式
  - A：在当前行的结尾，进入输入模式
  - o：在当前光标下一行进入输入模式
  - O：在当前光标上一行进入输入模式
  - esc：任何情况下输入esc都能回到命令模式
  - 键盘上、键盘k：向上移动光标
  - 键盘下、键盘j：向下移动光标
  - 键盘左、键盘h：向左移动光标
  - 键盘右、键盘l：向右
  - 0：移动光标到当前行的开头
  - $：移动光标到当前行的结尾
  - pageup(PageUp)：向上翻页
  - pagedown(PgDn)：向下翻页
  - /：进入搜索模式
  - n：向下继续搜索
  - N：向上继续搜索
  - dd：删除光标所在行的内容
  - ndd：n是数字，表示删除当前光标向下n行
  - yy：复制当前行
  - nyy：复制当前行和下面的n行
  - p：粘贴复制的内容
  - u：撤销修改
  - ctrl+r：反向撤销修改
  - gg：跳到首行
  - G：跳到行尾
  - dG：从当前行开始，向下全部删除
  - dgg：从当前行开始，向上全部删除
  - d$：从当前光标开始，删除到本行的结尾
  - d0：从当前光标开始，删除到本行的开头

  在命令模式内，输入：,即可进入底线命令模式

  - :wq  保存并退出
  - :q    仅退出
  - :q!   强制退出
  - :w   仅保存
  - :set nu  显示行号
  - :set paste  设置粘贴模式

## 二、Linux用户和权限

### 1.root用户

Linux系统中，拥有最大权限的是root

- 普通用户的权限，一般在其HOME目录内不受限
- 一旦出了HOME目录，大多数地方，普通用户仅有只读和执行权限，无修改权限

**su和exit命令**

- su命令：用于账户切换的系统命令
- 语法：su [-] [用户名]
- -可选：表示是否在切换用户后加载环境变量，建议带上
- 用户名：要切换的用户，可省，省略表示切换到root
- exit返回上一个用户，也可以ctrl+d
- 普通用户切换到其他用户需要输入密码，root用户切换到其他用户，无需密码。

**sudo命令**

- su命令切换到root得到最大权限
- 但不建议长期使用root命令，避免带来系统损坏
- 可以使用sudo命令，为普通的命令授权，临时以root身份执行
- 语法：sudo 其他命令
- 在其他命令之前，带上sudo，即可为这条命令临时赋予root授权
- 需要为普通用户配置sudo认证
  - 配置认证：切换到root用户，执行visudo命令，会自动通过vi编辑器打开：/etc/sudoers
  - 文件最后添加：yyue ALL=(ALL)    NOPASSWD:ALL        （centos7这样设置，Ubuntu好像不行）

### 2.用户、用户组管理

Linux系统中：

- 配置多个用户
- 配置多个用户组
- 用户可以加入多个用户组中

Linux中关于权限的管控级别：

- 针对用户的权限控制
- 针对用户组的权限控制 

用户组管理：

- 需root用户执行
- 创建用户组：groupadd 用户组名
- 删除用户组：groupdel 用户组名

用户管理：

- 创建用户：useradd [-g -d] 用户名
  - -g：指定用户的组，不指定-g，会创建同名组并自动加入，指定-g需要组已经存在
  - -d：指定用户HOME路径，不指定，HOME目录默认在：/home/用户名
- 删除用户：userdel [-r] 用户名
  - -r：删除用户的HOME目录，不使用-r，删除用户时，HOME目录保留
- 查看用户所属组：id [用户名]
  - 用户名：被查看的用户，如果不提供则查看自身
- 修改用户所属组：usermod -aG 用户组 用户名，将指定用户加入指定组

getent：查看当前系统中有哪些用户

- 语法：getent passwd
- 语法：getent group 查看当前系统中有哪些用户组

### 3.查看权限控制 

![](D:\mybatis笔记\images\l2.png)

- 序号1：表示文件、文件夹的权限控制信息
- 序号2：表示文件、文件夹所属用户
- 序号3：表示文件、文件夹所属用户组
- -或d或l：-表示文件，d表示文件夹，l表示软链接
- rwx：r表示读权限，w表示写权限，x表示执行权限
- 针对文件、文件夹不同，rwx含义不同
  - r针对文件可以查看文件内容，针对文件夹可以查看文件夹内容
  - w针对文件表示可以修改此文件，针对文件夹，可以在此文件夹内创建、删除、改名等操作
  - x针对文件表示可以将文件作为程序执行，针对文件夹，表示可以更改工作目录到此文件夹，即cd进入

### 4.修改权限控制-chmod

chmod命令：修改文件、文件夹的权限信息   **注：**只有文件、文件夹的所属用户或root用户可以修改

语法：chmod [-R] 权限 文件或文件夹

- -R:对文件夹内的全部内容应用同样的操作
- 如：chmod u=rwx,g=rx,o=x hello.txt,将文件权限修改为rwxr-x--x,其中u是所属用户权限，g是group组权限，o是other其他用户权限

权限可以用3位数字来表示（chmod 777 test.txt），第一位位用户权限，第二位表示用户组权限，第三位表示其他用户权限，r记为4，w记为2，x记为1，可以有

- 0：无任何权限，---
- 1：仅有w权限，--x
- 2：仅有w权限，-w-
- 3：有w，x权限，-wx
- 4：仅有r权限，r--
- 5：有rx权限，r-x
- 6：有rw权限，rw-
- 7：有rwx权限，rwx

### 5.修改权限控制-chown

chown命令：可以修改文件、文件夹的所属用户和用户组

**注：****普通用户无法修改所属为其他用户或组，此命令只适用于root用户执行**

语法：chown [-R] \[用户][:\][用户组] 文件或文件夹

- -R表示对文件夹内全部内容应用相同规则
- 用户：修改所属用户
- 用户组：修改所属用户组
- ：用于分隔用户和用户组

如：

- chown root hello.txt 将hello.txt所属用户修改为root
- chown :root hello.txt 将所属用户组修改为root
- chown root:yyue hello.txt将所属用户修改为root，用户组修改为yyue
- chown -R root test 将文件夹test的所属用户修改为root并对文件夹内全部内容应用同样规则

## 三、Linux实用操作

### 1.常用快捷键

- ctrl+c强制停止
- ctrl+d退出或登出（不能用于退出vi/vim）
- history：查看历史输入过的命令
- ！命令前缀：自动执行上一次匹配前缀的命令
- ctrl+r:输入内容匹配历史命令，若搜索到的内容是需要的，按回车执行，键盘左右键可以得到此命令（不执行）
- 光标移动快捷键：
  - ctrl+a：跳到命令开头
  - ctrl+e：跳到命令结尾
  - ctrl+键盘左键，向左跳一个单词
  - ctrl+键盘右键，向右跳一个单词
- 清屏：
  - ctrl+l，清空终端内容
  - clear命令

### 2.软件安装

**apt**

语法:apt [-y] [install | remove | search] 软件名称

(**注:需要root权限**)

- apt install wget,安装wget
- apt remove wget,移除
- apt search wget,搜索 

### 3.systemctl

systemctl命令:Linux系统支持使用systemctl命令控制:启动、停止、开机自启

被systemctl管理的软件,一般成为:服务

语法:systemctl start | stop | status | enabel | disable 服务名 （start启动、stop关闭、status查看状态、enable开启开机自启、disable关闭开机自启）  

系统内置的服务比较多,如:

- NetworkManager,主网络服务
- network,副网络服务
- ufw,防火墙服务
- sshd,ssh服务

### 4.软连接

ln命令：创建软连接，系统中创建软连接，可以将文件、文件夹链接到其他位置（类似于windows系统中的快捷方式）

语法：ln -s 参数1 参数2

- -s创建软连接
- 参数1：被链接的文件或文件夹
- 参数2：要链接去的目的地

### 5.日期、时区

1.date命令：查看系统时间

语法：date [-d] [+格式化字符串]

- -d按照给定的字符串显示日期，一般用于日期计算
- 格式化字符串：通过特定的字符串标记，来控制显示的日期格式
- %Y年，%y年份后两位(00-99)，%m月份，%d日，%H小时，%M分钟，%S秒，%s自1970-01-01 00:00:00 UTC到现在的秒数

例如：

- 使用date命令，无选项，直接查看时间
- ![](D:\mybatis笔记\images\l3.png)
- 按照2022-01-01的格式显示日期
- ![](D:\mybatis笔记\images\l4.png)
- 按照2022-01-01 10:00:00显示日期
- ![](D:\mybatis笔记\images\l.png)
- 如上：由于中间有空格，所以需要双引号包围格式化字符串，作为整体

2.date命令进行日期加减

- -d选项，可以按照给定的字符串显示日期，一般用于日期计算
-  date -d "+1 day" +%Y%m%d  # 显示后一天的日期
-  date -d "-1 day" +%Y%m%d   # 显示前一天日期
-  date -d "+1 month" +%Y%m%d # 显示后一个月的日期
- day | month | year | hour | minute | second

3.修改linux时区

- 使用root权限，执行以下命令，修改时区为东八时区
- rm -f /etc/localtime
- sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
- 将系统自带的localtiime文件删除，并将/usr/share/zoneinfo/Asia/Shanghai文件链接为localtime文件

4.ntp程序：自动校准系统时间

- 安装ntp:apt -y install ntp
- 启动并设置开机自启：
  - systemctl start npt
  - systemctl enable ntp
- 当ntp启动后会定期联网校准系统时间
- 也可以手动校准（需要root权限)：ntpdate -u ntp.aliyun.com

### 6.ip地址、主机名

#### 1.ip地址、主机名

IP地址：每个联网的计算机都会有一个地址

可以通过ifconfig查看本机的ip地址，若无法使用，可以安装：apt -y install net-tools

**特殊IP地址：**

- 127.0.0.1这个IP地址用于指代本机
- 0.0.0.0，特殊IP地址
  - 可以用于指代本机
  - 可以在端口绑定中用来确定绑定关系
  - 在一些IP地址限制中，表示所有IP的意思，如放行规则设置为0.0.0.0，表示允许任意IP访问

主机名：hostname可以查看Linux的主机名

**在linux中修改主机名：**

- 使用命令：hostname查看主机名
- 使用：hostnamectl set-hostname 主机名（需要root权限）
- 重新登录Finalshell即可查看到

**域名解析：**

- 访问www.baidu.com流程：访问www.baidu.com----》检查Windows系统：C:\Windows\System32\drivers\etc\hosts 文件   Linux系统：/etc/hosts 文件，是否有www.baidu.com的ip地址记录。-----》有，打开网站，没有就联网询问公开DNS服务器是否有记录www.baidu.com的IP地址
- 即：
  - 先查看本机的记录
  - 再联网去DNS服务器(如114.114.114.114,8.8.8.8等)询问

**配置主机名映射**

（由于ip地址过于长难记，所以可以将ip地址与主机名进行映射，使得可以直接通过访问主机名来访问该ip地址）

- 在windows系统的：C:\Windows\System32\drivers\etc\hosts文件中配置记录即可 
- 192.168.138.129 ubuntu 保存，则可以通过ubuntu进行连接

#### 2.虚拟机配置固定IP

2.1在VMware Workstation中配置固定IP

- 步骤：
  - 1.在VMware Workstation中配置IP地址网关和网段（IP地址的范围）
  - 2.在Linux系统中手动修改配置文件，固定IP（配置net8）
  - vim /etc/netplan/01-network-manager-all.yaml 
    - ![](D:\mybatis笔记\images\l5.png)
  - sudo netplan apply使配置生效

### 7.网络传输

1.ping命令：检查指定的网络服务器是否是可联通状态

语法：ping [-c num] ip或主机名

- -c:检查的次数，不使用-c选项，将无限次数持续检查
- ip或主机名：被检查的服务器的ip地址或主机名地址
- 如：ping www.baidu.com是否联通

2.wget命令

wget是非交互式的文件下载器，可以在命令行内下载网络文件

语法： wget [-b] url

- -b(可选):后台下载，会将日志写入到当前工作目录的wget-log文件
- url：下载链接
- 例如：wget  http://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz

3.curl命令：可以发送http网络请求，可用于：下载文件、获取信息等

语法：curl [-O] url

- -O：用于下载文件，当url是下载链接时，可以使用该选项保存文件
- url：要发起请求的网络   （相当于获取网页）
- 例如：
  - 向cip.cc发起网络请求：curl cip.cc
  - 也可以通过curl下载hadoop-3.3.0安装包，curl -O +url

4.端口：设备与外界通讯交流的出入口，可以分为物理端口和虚拟端口两类

物理端口：又称之为接口，是可见的端口，如USB接口

虚拟端口：计算机内部的端口，不可见，用来操作系统和外部进行交互使用

**Linux系统：**

- 公认端口：1~1023，通常用于一些系统内置或知名程序的预留使用，如SSH服务的22端口，HTTPS服务的443端口，非特殊要求不要占用
- 注册端口：1024~49151，通常可随意使用，用于松散的绑定一些程序\服务
- 动态端口：49152~65535，通常不会固定绑定程序，而且当程序对外进行网络链接时，用于临时使用

**查看端口占用：**可以通过Linux命令去查看端口的占用情况

- 使用nmap命令，安装nmap:apt -y install nmap
- 语法：nmap 被查看的IP地址
- nmap 127.0.0.1:查看本机端口被占用情况

**可以通过netstat命令**：查看指定端口的占用情况

- 语法：netstat -anp | grep 端口号 ，安装netstat：apt -y install net-tools
- 例如查看6000端口被哪个程序占用：netstat -anp | grep 6000

### 8.进程管理

进程：程序运行在操作系统中，是被操作系统所管理的。为管理运行的程序，每一个程序在运行时，被操作系统注册为系统中的一个进程，并为每一个进程分配一个独有的：进程ID

查看进程：ps [-e -f]

- -e:显示全部的进程
- -f：以完全格式化的形式展示信息
- 固定用法：ps -ef 列出全部进程的全部信息
- 查看指定进程：可以使用管道符配合grep来进行过滤：如ps -ef | grep tail即可准确的找到tail命令的信息
- （过滤不仅仅过滤名称，进程号，用户ID等）

关闭进程：kill [-9] 进程ID

- -9：表示强制关闭进程。不使用此选项会向进程发送信号要求其关闭，但是否关闭看进程自身的处理机制
- 可以先查看进程ID（搭配使用grep进行过滤查看）

### 9.主机状态

- 查看系统资源占用：top命令查看CPU、内存使用情况，类似Windows的任务管理器
- 语法：直接输入top，按q或ctrl+c退出
- ![](D:\mybatis笔记\images\l6.png)
- ![](D:\mybatis笔记\images\l7.png)

磁盘信息监控：使用df命令，可以查看硬盘使用情况

- 语法：df [-h]
- -h：以更加人性化的单位显示

iostat：查看CPU、磁盘的相关信息

- 语法：iostat [-x] [num1] [num2]
- -x：显示更多信息
- num1：数字，刷新间隔，num2：数字，刷新几次

网络状态监控：使用sar命令查看网络的相关统计

- 语法：sar -n DEV num1 num2
- -n，查看网络，DEV表示查看网络接口
- num1：刷新间隔，num2：查看次数

### 10.环境变量

env命令可查看当前系统中记录的环境变量

- 环境变量：PATH（无论当前工作目录是什么，都能执行/usr/bin/cd这个程序，就是因为借助环境变量中：PATH这个项目的值来做到的）

- ![](D:\mybatis笔记\images\l8.png)
- PATH记录了系统执行任何命令的搜索路径，当执行任何命令时，都会按照顺序，从上述路径中搜索要执行的程序的本体

$符号：被用于取”变量“的值

- 取环境变量的值就可以通过语法：$环境变量名 来取
- 如：echo $PATH

**自行设计环境变量**

- 临时设置，语法：export 变量名=变量值
- 永久设计
  - 针对当前用户生效，配置在当前用户的：~/.bashrc文件中
  - 针对所有用户生效，配置在系统的：/etc/profile文件中
  - 并通过语法：source配置文件，进行立刻生效，或重新登录生效

自定义环境变量PATH

- 可以将搜索路径自行添加到PATH中
- 测试：
  - 在当前HOME目录内创建文件夹，myenv，在文件夹内创建文件mkhaha
  - 通过vim编辑器，在mkhaha文件内写入：echo ===
  - 完成上述操作后，随意钱换工作目录，执行mkhaha命令，无法执行（要想其可执行，要写修改权限）
- 修改PATH的值
  - 临时修改PATH：export PATH = $PATH:/home/yyue/myenv,再次执行mkhaha，无论在那里都可以执行

### 11.上传、下载

rz,sz命令（可以通过apt -y install lrzsz安装）

- rz命令，进行上传，语法：直接输入rz即可
- sz命令，进行下载，语法：sz要下载的文件
- 文件会自动下载到桌面的fsdownload文件夹中

### 12.压缩、解压

压缩格式：

- zip格式：Linux等常用
- tar：Linux等常用
- gzip：Linux等常用

针对.tar  .gz这两种格式：使用tar命令均可以进行压缩和解压缩的操作

- 语法：tar [-c -v -x -f -z -C] 参数1 参数2 ````参数n
- -c：创建压缩文件，用于压缩模式
- -v：显示压缩、解压过程，用于查看进度
- -x：解压模式
- -f：要创建的文件，或要解压的文件，-f选项必须在所有选项中位置处于最后一个
- -z：gzip模式，不适用-z就是普通的tarball格式
- -C：选择解压的目的地，用于解压模式

tar命令压缩常用组合：

- tar -cvf test.tar 1.txt 2.txt 3.txt（将1.txt 2.txt 3.txt压缩到test.tar文件内）
- tar -zcvf test.tar.gz 1.txt 2.txt 3.txt（将1.txt 2.txt 3.txt压缩到test.tar.gz文件内，使用gzip模式）
- **注：**-z选项如果使用的话，一般处于选项位第一个，-f必须最后一个

tar解压命令常用组合：

- tar -xvf test.tar（解压test.tar，将文件解压至当前目录）
- tar -xvf test.tar -C /home/yyue（解压test.tar，将文件解压到指定目录/home/yyue下）

zip命令压缩文件

- 可以使用zip命令，压缩文件为zip压缩包
- 语法：zip [-r] 参数1 参数2 ····
- -r：被压缩的包含文件夹的时候，需要使用-r选项，和rm、cp等命令使用-r效果一样
- 示例：
  - zip test.zip a.txt b.txt c.txt（将abc压缩到test.zip文件内)
  - zip -r test.zip test a.txt(将test文件夹以及a.txt文件压缩到test.zip中)

unzip命令：解压zip压缩包

- 语法：unzip [-d] 参数
- -d：指定要解压去的位置
- 参数：被解压的zip压缩包文件
- 示例 
  - unzip test.zip
  - unzip test.zip -d /home/yyue

## 四、实战：在Linux上部署各类软件

###  1.mysql数据库管理系统安装部署

安装mysql5.7

1. 切换到root用户

   - ```
     sudo su - #切换到root用户
     ```

2. 下载apt仓库文件

   - ```
     #下载apt仓库的安装包，Ubuntu的安装包是.deb文件
     wget https://dev.mysql.com/get/mysql-apt-config_0.8.12-1_all.deb
     ```

3. 配置apt仓库

   - ```
     # 使用dpkg命令安装仓库
     dpkg -i mysql-apt-config_0.8.12-1_all.deb
     ```

4. 更新apt仓库的信息

   - ```
     # 首先导入仓库的密钥信息(否则不被信任)
     apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 467B942D3A79BD29
     # 更新仓库信息
     apt update
     ```

5. 检查是否成功配置Mysql的仓库

   - ```
     apt-cache policy mysql-server
     ```

6. 安装mysql5.7

   - ```
     # 使用apt安装mysql客户端和mysql服务器
     apt install -f -y mysql-client=5.7* mysql-community-server=5.7*
     ```

   - 弹出框输入root密码并选择ok

7. 启动mysql

   - ```
     /etc/init.d/mysql start # 启动
     /etc/init.d/msql stop # 停止
     /etc/init.d/mysql status # 查看状态
     ```

8. 对mysql进行初始化

   - ```
     # 执行如下命令，此命令是mysql安装后自带的配置程序
     mysql_secure_installation
     # 可以通过which命令查看到这个自带程序所在的位置
     which mysql_secure_installation
     /usr/bin/mysql_secure_installation
     ```

   - 输入密码

   - 是否开启密码验证插件，如果需要增强密码安全性，输入y并回车，不需要直接回车

   - 是否更改root密码，需要输入y回车，不需要直接回车

   - 是否移除匿名用户，移除输入y回车，不移除1直接回车

   - 是否禁止root用户远程登录，禁止输入y回车

   - 是否移除自带的测试数据库，移除y

   - 是否刷新权限，刷新输入y回车

9. 登录mysql

   - ```
     mysql -uroot -p
     # 输入密码即可登录成功
     ```
   
10. 开机自启

    - ```
      sudo update-rc.d -f mysql defaults
      reboot # 重启查看状态，是否启动
      ```

安装MySQL8.0版本

1. 若是安装过5.7，则需要写在仓库信息

   - ```
     # 卸载MySQL5.7
     apt remove -y mysql-client=5.7* mysql-community-server=5.7*
     # 卸载5.7的仓库信息
     dpkg -l | grep mysql | awk '{print $2}' | xargs dpkg -P
     ```

2. 更新apt仓库信息

   - ```
     apt update
     ```

3. 安装mysql

   - ```
     apt install -y mysql-server
     ```

4. 启动mysql

   - ```
     /etc/init.d/mysql start # 启动
     /etc/init.d/msql stop # 停止
     /etc/init.d/mysql status # 查看状态
     ```

5. 登录mysql设置密码

   - ```
     # 直接执行mysql 
     mysql
     ```

6. 设置密码

   - ```
     ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
     # 此处password修改成自己要设置的密码
     ```

7. 退出MySQL控制台

   - ```
     exit
     ```

8. 对mysql进行初始化

   - ```
     # 执行如下命令，此命令是mysql安装后自带的配置程序
     mysql_secure_installation
     # 可以通过which命令查看到这个自带程序所在的位置
     which mysql_secure_installation
     /usr/bin/mysql_secure_installation
     ```

   - 后续内容同5.7

### 2.Tomcat安装部署

Tomcat：一个web应用程序的托管平台，可以让用户编写的web应用程序，被tomcat所托管，并提供网站服务

安装两个步骤：

- 安装JDK环境
- 解压并安装Tomcat

安装JDK

1. 下载Linux的JDK8

2. 登录Linux系统，切换到root目录下

3. 上传下载好的JDK安装包

4. 创建文件夹，用来部署JDK，将JDK和Tomcat都安装部署到：/export/server内

   - ```
     mkdir -p /export/server
     ```

5. 解压缩JDK安装文件

   - ```
     tar -zxvf jdk-8u361-linux-x64.tar.gz -C /export/server/
     ```

6. 配置JDK的软链接

   - ```
     ln -s /export/server/jdk1.8.0_361 /export/server/jdk
     ```

7. 配置JAVA_HOME环境变量，以及将$JAVA_HOME/bin文件夹加入PATH环境变量中

   - ```
     # 编辑/etc/profile文件
     export JAVA_HOME=/opt/jdk/jdk-17.0.4.1
     export JRE_HOME=${JAVA_HOME}/jre
     export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib 
     export PATH=${JAVA_HOME}/bin:$PATH
     ```

8. 生效环境变量

   - ```
     source /etc/profile
     ```

安装Tomcat并部署

注：Tomcat建议使用非root用户安装并启动，可以创建一个用户：tomcat用以部署

1. 首先，放行tomcat需要使用的8080端口的外部访问权限

   - 放行有2中操作方式

     - 关闭防火墙
     - 配置防火墙规则，放行端口

   - ```
     # 以下两种方式选一即可
     #方式一：关闭防火墙
     systemctl stop ufw #关闭防火墙
     systemctl disable ufw # 停止防火墙开机自启
     
     #方式二：放行80 80端口的外部访问
     firewall-cmd --add-port=8080/tcp --permanent # --add-port=8080/tcp表示放行8080端口的tcp访问，--permanent表示永久生效
     firewall-cmd --reload #重新载入防火墙规则使其生效
     ```

2. 以root用户操作，创建tomcat用户

   - ```
     # 使用root用户操作
     useradd tomcat
     # 可选 为tomcat用户配置密码
     passwd tomcat
     ```

3. 下载Tomcat安装包

   - ```
     # 使用root用户操作
     wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.5/bin/apache-tomcat-10.1.5.tar.gz
     # 若出现https相关错误，可以使用--no-check-certificate选项
     wget --no-check-certificate https://dlcdn.apache.org/tomcat/tomcat-10/v10.1.5/bin/apache-tomcat-10.1.5.tar.gz
     ```

4. 解压Tomcat安装包

   - ```
     # 使用root用户操作，否则无权限解压到/export/server内，除非修改此文件夹权限
     tar -zxvf apache-tomcat-10.1.5.tar.gz -C /export/server
     ```

5. 创建Tomcat软链接

   - ```
     ln -s /export/server/apache-tomcat-10.1.5 /export/server/tomcat
     ```

6. 修改tomcat安装目录权限

   - ```
     # 使用root用户操作，同时对软连接和tomcat安装文件夹进行修改
     chown -R tomcat:tomcat tomcat
     chown -R tomcat:tomcat apache-tomcat-10.1.5
     ```

7. 切换到yyue用户

   - ```
     su - tomcat
     ```

8. 启动tomcat

   - ```
     /export/server/tomcat/bin/startup.sh
     ```


安装10失败，该安装了9，如链接所示[(235条消息) ubuntu 22.04 安装tomcat 9（最新实操）_ubuntu安装tomcat9_我有事我先走啦的博客-CSDN博客](https://blog.csdn.net/hahaqinyou/article/details/125656223)

### 3.Nginx安装部署

简介：Nginx：一个高性能的HTTP和反向代理web服务器，同时也提供了MAP/POP3/SMTP服务，同tomcat一样，Nginx可以托管用户编写的web应用程序成为可访问的网页服务，同时也可以作为流量代理服务器，控制流量的中转。

## 五、Ubuntu22.04配置MySQL，并远程连接

### 1.修改mysql配置文件

```
/etc/mysql/mysql.conf.d   下面的mysqld.cnf文件，注释掉bind-address = 127.0.0.1，加上port=3306.
```

2.重启mysql

```
service mysql stop
service mysql start
```

3.进入mysql配置mysql外部访问权限

```
update user set host='%' where user='root';
grant all privileges on *.* to 'root'@'%' identified by '你的root账户密码';   # 赋予权限
flush privileges; # 立即生效
```

## 记录：

### 1.ubuntu安装minio

1. 进入/opt目录，创建minio文件夹

   - ```
     cd /opt
     ```

   - ```
     mkdir minio
     ```

2. 下载安装包

   - ```
     wget https://dl.minio.io/server/minio/release/linux-amd64/minio
     ```

3. 在minio文件夹下创建log文件

   - ```
     cd /minio
     touch minio.log
     ```

4. 赋予minio文件执行权限

   - ```
     chmod 777 minio
     ```

5. 启动minio

   - ```
     ./minio server /opt/minio/data （/opt/minio/data 为你存放静态文件的目录）
     ```

6. 访问minio

   - ```
     #每次minio重新启动的时候端口会变
     # 所以启动可以使用
     ./minio server /opt/minio/data --console-address ":62222"
     ```

7. 设置minio后台启动

   - ```
     #创建启动文件
     vim start.sh
     ```

   - ```
     nohup /opt/minio/minio server  /opt/minio/data --console-address ":35555" > /opt/minio/minio.log 2>&1 &
     ```

8. 脚本运行minio

   - ```
     sh start.sh
     ```

9. 访问地址

   ```
   http://127.0.0.1:35555
   ```

   主机访问地址

   - ```
     http://192.168.88.128:9000
     ```

10. [(244条消息) Linux安装MinIO（图文解说详细版）_掉头发的王富贵的博客-CSDN博客](https://blog.csdn.net/csdnerM/article/details/121336618)

先搭建minio，然后用各自语言连上去

换镜像源：

- 首先先备份

- ```
  sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
  ```

- 修改该文件的源

- ```
  sudo vim /etc/apt/sources.list
  ```

- 更新源

- ```
  sudo apt-get update
  ```

  