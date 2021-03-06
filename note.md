### 常用快捷键
| 按键 | 作用 |
| ---- | ---- |
| Ctrl + c | 退出当前进程 |
| Ctrl + s | 暂停当前进程，按任意键继续 |
| Ctrl + a | 光标移至输入行头，等同于Home |
| Ctrl + e | 光标移至输入行末，等同于End |
| Ctrl + k | 删除从光标所在位置到行末 |

### 创建文件
> touch filename.filetype

> touch love{1..10}.txt 创建多个文件

### Shell 常用通配符
| 字符 | 含义 |
| --- | --- |
| * | 匹配 0 或多个字符 |
| ? | 匹配任意一个字符 |
| [list] | 匹配 list 中的任意单一字符, 如 ls [12345].txt 能匹配到 1.txt 2.txt ... 5.txt |
| [^list] | 匹配 除 list 中的任意单一字符以外的字符 |
[c1-c2] | 匹配 c1-c2 中的任意单一字符 如：[0-9][a-z] |
| {  } | 大括号可以用于批量创建文件，[ ]不行 |
{ string1, string2 } | 匹配 string1 或 string2 (或更多)其一字符串 |
{ c1..c2 } | 匹配 c1-c2 中全部字符 如{1..10}, 如 touch {1..10}.txt 创建 1.txt ... 10.txt |

### 用户

| 命令 | 含义 |
| --- | --- |
| who am i | 查看当前登录到终端的用户, 即对应 ssh _username_@ip |
| whoami | 查看当前登录的用户，和 who am i 不一样，如 su -l _username_ |
| sudo adduser _user_ | 添加用户，sudo 表示 root权限 |
| sudo passwd _user_ | 给用户设置密码 |
| su -l _user_ | 登录用户 |
| exit 或 Ctrl + D| 退出当前用户，不是退出终端 |

### 用户组
| 命令 | 含义 |
| ---  | ---  |
| groups _user_ | 查看某个用户所属的组 |
| cat /etc/group | 查看所有的组 |
| groupadd <组名> | 创建一个新组 |
| groupdel <组名> | 删除组 |
| sudo usermod -G <组> <用户> | 将用户添加到某个组 |
| sudo usermod -G sudo或wheel(centos) <用户> | 将用户添加到 sudo组 |
| sudo deluser或userdel _user_ --remove-home | 将用户从某个组删除 |

> 将用户添加到 sudo 组的好处就是不用切换用户环境就可以使用 sudo 权限。

### 权限相关
权限种类

| 权限 | 含义 |
| --- | --- |
| r | 读的权限，如 cat 命令查看文件内容 |
| w | 写的权限，vi 编辑文件或修改 |
| x | 执行权限，通常指可以运行的二进制程序文件或脚本文件|
  

> 记住，一个目录同时具有读权限和执行权限才可以打开并查看内部文件，而一个目录要有写权限才允许在其中创建其它文件，这是因为目录文件实际保存着该目录里面的文件的列表等信息。

> 权限按权限者分，可以分为 当前用户、所属用户组、其他用户。rwx为三位的二进制数，为1时即有权限，为0则无。所以其对应的十进制的数取值范围为 0~7，比如 7 = 1 * 2<sup>2</sup> + 1 * 2<sup>1</sup> + 1 * 2<sup>0</sup> 其对应的权限为 rwx，比如 2 = 0 * 2<sup>2</sup> + 1 * 2<sup>1</sup> + 0 * 2<sup>0</sup>,其对应的权限为 -r-

与权限有关的命令
| 命令 | 含义 |
| --- | --- |
| ls -l | 查看当前目录所有文件（夹），不包括隐藏文件的详细信息 |
| ls -lh | 更直观的看到文件的大小 |
| ls <目录名> 其他参数 | 查看某个目录下的文件 |
| ls -a | 查看当前目录的所有文件，包括隐藏的，linux中以 .开头的文件为隐藏文件 |
| ls -dl <目录名> | 查看某一个目录的完整属性，而不是显示目录里面的文件属性|
| ls -asSh(s为显示文件大小，S为按文件大小排序) | 显示所有文件大小，并以普通人类能看懂的方式呈现|
| sudo chown <用户> <文件> | 修改文件的所有者为指定用户  |
| chmod <三位权限数字> <文件> | 修改文件的权限所属| 

> ls -l 命令展示的文件详细信息含义如下图：
> ![](./ls.png)

### 目录结构及文件基本操作
符号对应的目录如下表 

| 符号 | 含义 |
| --- | --- |
| pwd | 显示当前路径 |
| cd（change directory） | 改变目录，配合下面的符号使用  |
| / | 根目录 |
| . | 当前目录 |
| .. | 上一级目录 |
| - | 上一次所在的目录 |
| ~ | 当前用户的 home 目录 |
> 可以用 Tab 进行路径补全

文件命令

| 命令 | 含义 |
| ---  | --- |
| mkdir <文件(夹)> | 创建文件(夹) |
| mkdir -p <文件路径> | 同时创建父目录 | 
| cp <目标文件> <新目录> | 将目标文件复制到新目录 |
| cp <目标文件> <新目录> -r | 将目标文件夹及后代复制到新目录 |
| rm <文件> -f(强制) -r(删除整个目录) | 删除一个文件(夹) |
| mv <目标文件(夹)> <新目录> | 移动目标文件到新目录，如果目标文件和新目录都是文件，则会进行改名 |
| rename <处理表达式> <匹配表达式> | 批量重命名文件 |
| cat <文件名> -n(显示行号) | 快速查看文件内容 |
| more <文件名> | 分页查看文件（space 滚动一页，enter滚动一行，q退出）|
| tail <文件名> -n <数字>(查看指定行数) | 查看文件内容的倒数指定几行 | 
| head <文件名> -n <数字>(查看指定行数) | 查看文件内容的正数指定几行 |
| file <文件名> | 查看文件类型 |


> mkdir 重复创建文件会报错，但是使用 touch 不会，touch 会改变文件或文件夹的时间戳，如果没有那个文件则会创建一个文件（不是文件夹）

### 环境变量
创建一个变量：
> name=dangchuanwen  

打印一个变量：
> echo $name

| 命令 | 说明 |
| ---  | --- |
| set | 显示当前 Shell 程序的所有变量，包括 env 和 export |
| env | 显示与当前用户相关的环境变量，包括 export |
| export | 显示从Shell中导出成环境变量的变量 |

> 使用 vimdiff 查看三者的区别，命令如下：
> 1. name=dangnima
> 2. export temp_name=dcw
> 3. env|sort>env.txt
> 4. export|sort>export.txt
> 5. set|sort>set.txt
> 6. vimdiff env.txt export.txt set.txt

> 结果可以看到三个变量的区别，如果使用 export 定义变量，则在 set 和 env 变量中可以看到，也就是说 export 是 set 和 env 的子集，而 set 又是 env 的子集。

> 但是这样定义变量关闭当前的 shell 进程后，就会消失，按照生命周期可以将变量分为下面两种：

| 变量类型 | 说明 |
| --- | --- |
| 永久的 | 需要修改配置文件，变量永久生效 |
| 临时的 | 使用 export 命令行声明即可，变量在关闭 shell 时失效 |

> 为了使变量永久生效，下面介绍两个重要保存变量的文件：

| 文件名 | 说明 |
| --- | --- |
| /etc/bashrc | 存放永久的shell变量 |
| /etc/profile | 存放永久的环境变量 |
| 用户目录/.profile | 只对当前用户生效的环境变量 |

> user/.profile 只对当前用户永久生效。因为它保存在当前用户的 Home 目录下，当切换用户时，工作目录可能一并被切换到对应的目录中，这个文件就无法生效。而写在 /etc/profile 里面的是对所有用户永久生效，所以如果想要添加一个永久生效的环境变量，只需要打开 /etc/profile，在最后加上你想添加的环境变量就好啦。

### 环境变量 PATH
PATH变量保存了各种 bin 目录，当输入一个可执行程序的命令时，计算机会遍历这个PATH变量中的所有 bin 目录，去查找有没有相关的命令。先查到先得到。可以尝试着输入以下命令查看：
> echo $PATH

下面是个练习小例子:

> 1.在用户根目录创建一个 mybin 文件夹

> 2.在mybin下创建一个 hello.c 文件，然后输入以下代码：

    #include<stdio.h>
    int main() {
      printf("hello wolrd");
    }

> 3.输入以下命令编译该 c 文件

    gcc -o hello hello.c

> 4.将编译后的 hello 文件移动到 mybin 目录

    mv hello mybin

> 5.在PATH变量后面追加写入mybin文件夹的目录

    PATH=$PATH:/home/user/mybin
  
> 6.此时即可在任何目录中执行 hello 命令执行 hello 程序

> 但是如果关闭 shell 终端后，hello命令就会失效。在每个用户的 home 目录中有一个 Shell 每次启动时会默认执行一个配置脚本，以初始化环境，包括添加一些用户自定义环境变量等等。实验楼的环境使用的 Shell 是 zsh，它的配置文件是 .zshrc，相应的如果使用的 Shell 是 Bash，则配置文件为 .bashrc。它们在 etc 下还都有一个或多个全局的配置文件，不过我们一般只修改用户目录下的配置文件。Shell 的种类有很多，可以使用 cat /etc/shells 命令查看当前系统已安装的 Shell。我们可以简单地使用下面命令直接添加内容到 .zshrc 中：

    echo "PATH=$PATH:/home/shiyanlou/mybin" >> .zshrc

### 变量的修改方式
| 变量设置方式 | 说明 |
| --- | --- |
| ${变量名#匹配字串} | 从头向后开始匹配，删除符合匹配字串的最短数据 |
| ${变量名##匹配字串} | 从头向后开始匹配，删除符合匹配字串的最长数据 |
| ${变量名%匹配字串} | 从尾向前开始匹配，删除符合匹配字串的最短数据 |
| ${变量名%%匹配字串} | 从尾向前开始匹配，删除符合匹配字串的最长数据 |
| ${变量名/旧的字串/新的字串} | 将符合旧字串的第一个字串替换为新的字串 |
| ${变量名//旧的字串/新的字串} | 将符合旧字串的全部字串替换为新的字串 |

> 前面我们在 Shell 中修改了一个配置脚本文件之后（比如 zsh 的配置文件 home 目录下的 .zshrc），每次都要退出终端重新打开甚至重启主机之后其才能生效，很是麻烦，我们可以使用 source 命令来让其立即生效，如：

    cd /home/shiyanlou
    source .zshrc

### 搜索文件
下面是关于搜索文件的三个命令：

| 命令 | 说明 |
| --- | --- |
| whereis <文件路径匹配符>| 搜索二进制文件，man帮助文件和源代码文件 |
| locate <文件路径匹配符>| 搜索全部类型的文件，它是直接读取的数据库所以很快，但是有些新文件并没有插入到数据库，需要在之前手动更新数据库 | 
| which <程序名>| 用来确定是否安装了某个指定的程序，它只从PATH环境变量的路径中去搜索, 也就说可以看到某个程序的执行文件在哪个地方|
| find <路径><-参数> | 最强大的搜索命令，如 find /etc -name "*.txt" |

### 文件打包和文件压缩
linux下压缩文件格式

| 文件名后缀 | 说明 |
| --- | --- |
| *.zip | zip 程序打包压缩的文件 |
| *.rar | rar 程序压缩的文件 |
| *.7z | 7zip 程序压缩的文件 |
| *.tar | tar 程序打包，未压缩的文件 |
| *.gz | gzip 程序（GNU zip）压缩的文件 |
| *.xz | xz 程序压缩的文件 |
| *.bz2 | bzip2 程序压缩的文件 |
| *.tar.gz | tar 打包，gzip 程序压缩的文件 |
| *.tar.xz | tar 打包，xz 程序压缩的文件 |
| *tar.bz2 | tar 打包，bzip2 程序压缩的文件 |
| *.tar.7z | tar 打包，7z 程序压缩的文件 |

zip压缩命令
> zip -<参数> <打包后的文件名> <需要打包的文件>

> 参数说明

| 参数 | 说明 |
| --- | --- |
| -r | 递归打包目录下的所有文件 |
| -q | 安静模式，不向屏幕输出信息 |
| -o | 表示输出文件，后面跟打包后的文件名 |
| -[1-9] | 表示压缩速度和压缩大小的程度，越小压缩越块，体积越大 |

zip解压命令
> unzip 压缩的文件 -<参数>

> 参数说明

| 参数 | 说明 |
| --- | --- |
| -q | 安静模式 |
| -d | 输出到指定文件夹，没有会创建 |
| -l | 不解压，查看压缩包内容 |
| -O | 指定编码类型，windows上创建的压缩文件中文编码为GBK，而linux默认为 UTF-8，所以 "-O GBK" |

tar 压缩命令
> tar 只是一个打包工具，集成了 7z、gzip、xz、bzip2 等工具。

> tar -P -cf shiyanlou.tar /home/shiyanlou/Desktop

> 参数说明

| 参数 | 说明 |
| --- | --- |
| -P | 保留绝对路径符 |
| -c | 表示创建一个tar包文件 |
| -f | 用于指定创建的文件名，文件名要紧跟 -f 后面 |
| -v | 以可视化的形式输出打包后的文件 |
| -z | 压缩文件格式为 *.tar.gz |
| -J | 压缩文件格式为 *.tar.xz |
| -j | 压缩文件格式为 *.tar.bz2 |

tar 解压缩命令
> tar -xf shiyanlou.tar -C tardir

> 参数说明

| 参数 | 说明 |
| --- | --- |
| -f | 指定的文件，可以放到其他参数后面连起来 |
| -x | 后面跟需要解压的tar文件 |
| -C | 到指定的已存在目录 |
| -t | 只查看不解包文件 |
| -p | 保留文件属性，比如软连接 |
| -h | 保留备份连接执行的源文件而不是链接本身|
| -z | 解压缩文件格式为 *.tar.gz |
| -J | 解压缩文件格式为 *.tar.xz |
| -j | 解压缩文件格式为 *.tar.bz2 |

常用总结

| 命令 | 打包命令 | 解包命令 | 指定路径命令 |
| --- | --- | --- | --- |
| zip | zip something.zip somthing (目录加 r 参数) | unzip something.zip | -d 参数 |
| tar | tar -cf something.tar something | tar -xf something.tar | -C 参数 |






