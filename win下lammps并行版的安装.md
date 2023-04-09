# win下lammps并行版的安装

首先去看[官网教程](https://packages.lammps.org/windows.html)

先通读一遍，捋清思路

辗转问到的需求是*安装并行的2021或2020版本，直接安装在win上*

虚拟机的部分就不用你们考虑了，我抽空给你们做个镜像

## 安装包下载

[mpich(64位)](https://www.mpich.org/static/downloads/1.4.1p1/mpich2-1.4.1p1-win-x86-64.msi)

[lammps(全版本下载页)](https://rpm.lammps.org/windows/64bit/)

我选择的是[2021年9月29日的MPI版本](https://rpm.lammps.org/windows/64bit/LAMMPS-64bit-29Sep2021-MPI.exe)

## 安装过程

[mpich的含义等](https://www.mpich.org/)自行查看官网链接

### .NET Framework的启用

按一下`win`键，输入“控制面板”，打开。右上角角搜索栏输入“Windows功能”，单击`启用或关闭Windows功能`

![avatar](/pic/win/1.png)

若.NET3.5前为黑色实心填充，双击两次`黑色实心填充`，使之变成黑色勾即可。（中间会弹出消息框，确认即可）

![avatar](/pic/win/2.png)

如下图，已安装好。单击`确认`，退出控制面板，完成安装。

![avatar](/pic/win/3.png)

> 笔者之前有安装过solidworks，所以.NET3.5 4.8都已经开过并安装好，这一步可能会有疏漏

### MPICH的安装

找到上文的安装包，右击，选择`安装`

依次选择`Next`，`Next`，`Next`，`I agree`，`Next`

下图需要设置密码（或口令），个人使用的是笔记本锁屏密码（默认也可以）

![avatar](/pic/win/4.png)

建议默认路径，记住默认路径的位置，否则需要手动修改环境变量，点击`为Everyone安装`

![avatar](/pic/win/5.png)

一开始安装进程不会动，要注意下方任务栏有一个请求权限的提示，允许就好了，很快的

单击`close`完成安装

![avatar](/pic/win/6.png)

使用组合键`win+R`调出运行窗口，输入cmd（short for command）并回车

![avatar](/pic/win/7.png)

在左下角搜索栏输入cmd，选择用管理员身份运行

![avatar](/pic/win/8.png)

```cmd
cmd可以理解为纯文本界面的计算机系统，就是通过命令行（文本）的形式进行你想要的操作
这里列出几个常见的cmd命令：
#表示更换驱动器，D可以替换成C、E……看你分了几个盘
D:
#change dictionary的简写，表示更改当前路径，xxxx即为要更改的文件夹（只有当前路径下有xxxx才可以直接进入）。
#cd ..表示退回到当前路径的母文件夹
cd xxxx
#列出当前目录下所有文件和文件夹
dir
#where用于查找环境变量
#where xxxx
#后续有很多操作都是基于cmd，最好理解清楚
```

组合使用`cd`和`dir`命令，进入mpich的安装路径下的`bin`文件夹

![avatar](/pic/win/9.png)

输入`smpd.exe -install`，并回车，将mpich集成到系统中

![avatar](/pic/win/10.png)

输出如下即为安装完成：

![avatar](/pic/win/11.png)

#### 注册mpich

管理员身份打开cmd，进入mpich下的bin目录，输入`mpiexec -remove`

![avatar](/pic/win/12.png)

报错也不用管，输入`mpiexec -register`，回车。

会需要注册账户：用户名选择DESKTOP-xxxx\xxxx，密码自己设置（为了防止泄露，密码不会显示）

输入完成了回车一下就可以运行下一行了

![avatar](/pic/win/13.png)

输入`mpiexec -validate`，返回“SUCCESS”表示安装成功

![avatar](/pic/win/14.png)

输入`smpd -status`，显示如下表示安装成功

![avatar](/pic/win/15.png)

### lammps本体的安装

双击lammps安装包

![avatar](/pic/win/16.png)

单击`更多信息`，然后单击`仍要运行`

![avatar](/pic/win/17.png)

单击`I agree`，更改安装目录

![avatar](/pic/win/18.png)

单击`install`开始安装，单击`close`完成安装并退出

### 测试安装情况

启动cmd，进入lammps安装路径，进入LAMMPS 64-bit 29Sep2021-MPI下的Examples目录

![avatar](/pic/win/19.png)

进入第一个文件夹`airebo`，使用`dir`命令看一下有哪些in文件（输入文件）。在cmd里输入命令`mpiexec -np 16 lmp -in in.airebo.lmp`，回车。等待一会若无报错代码即表明安装完成。如图：

![avatar](/pic/win/20.png)