# linux安装python3.9.10版本

https://www.cnblogs.com/lhongsen/p/16273032.html

### 安装依赖环境

```mipsasm
sudo yum install -y gcc make cmake zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel xz xz-devel libffi-devel
```

（1）Ubuntu/Debian下需安装的依赖：

```mipsasm
sudo apt-get install -y gcc make cmake build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
```

（2）Fedora/CentOS/RHEL(aws ec2)下需安装的依赖：

```mipsasm
sudo yum install gcc make cmake zlib-devel bzip2 bzip2-devel readline-devel sqlite sqlite-devel openssl-devel xz xz-devel libffi-devel
```

### 安装python

1. 下载Python3安装包

```ruby
wget https://www.python.org/ftp/python/3.9.10/Python-3.9.10.tgz
```

\2. 创建安装目录
个人习惯安装在/usr/local/python3

```bash
mkdir -p /usr/local/python3
```

1. 解压安装包

```undefined
tar -zxvf Python-3.9.10.tgz
```

1. 进入解压后的目录，编译安装（编译安装前需要安装编译器 sudo apt install gcc）
   （1）进入解压后的目录
   （2）执行./configure

```bash
cd /Python-3.9.10
./configure --prefix=/usr/local/python3   #/usr/local/python3为安装目录
```

执行完configure命令后，configure 命令执行完之后，会生成一个 Makefile 文件，这个 Makefile主要是被下一步的 make 命令所使用（ Linux 需要按照Makefile 所指定的顺序来构建 (build) 程序组件）。

（3）执行make指令

```go
make
```

make实际就是编译源代码，并生成执行文件。

（4）再执行make install 命令

```go
make install
```

make install实际上是把生成的执行文件拷贝到之前configure命令指定的目录/usr/local/python3下。

到这里安装已经结束，下面是配置环境。

1. 建立python3的软链

```bash
rm -rf /usr/bin/python3 # 删除原有的软链
ln -s /usr/local/python3/bin/python3.9 /usr/bin/python3
```

1. 将/usr/local/python3/Python-3.7.2/bin加入PATH

```bash
sudo vim /etc/profile
```

然后在文件末尾添加

```ruby
export PATH=$PATH:/usr/local/python3/bin
```

按ESC，输入:wq回车退出。

修改完后，还需要让这个环境变量在配置信息中生效，执行命令：

```bash
source /etc/profile
```

可以让profile文件立即生效。

1. 测试是否安装成功

```bash
$ python3 -V
Python 3.7.2
$ pip3 -V
pip 18.1 from /usr/local/python3/lib/python3.7/site-packages/pip (python 3.7)
```

如果输出如上，证明已成功安装！

如果pip3 -V找不到，可以尝试创建一下pip3的软链接：

```bash
rm -rf /usr/bin/pip3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
```
