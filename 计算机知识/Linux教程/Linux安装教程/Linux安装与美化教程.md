# Linux系统

相信大多数的同学在来到视觉组之前并没有使用过Linux系统，但是多半听说过Linux系统的名字，相较于Windows系统，Linux具有许多的优点。比如说在环境的搭建方面，在视觉组的工作中，需要配置大量的库，这些库在Linux系统中被统一的管理，安装或者编译的过程十分的简单，同时在使用的时候也更加的便捷。同时一些重要的库比如ros，对于Linux的支持很全面，同时因为Linux系统的一些特性，比如说对于串口的定义便于我们进行串口通信。综合以上的这些原因，所以在车辆的工控机上运行的是Linux系统，同时为了环境的同步以及自身的编程方便，我们也要求大家为自己的电脑安装Linux系统，对于有志于长期使用Linux的同学，将其作为日常使用的系统，我们推荐为Linux系统留出200GB，只将Linux作为在视觉组写程序使用，其中只安装编程所需环境，则需要留出30-50GB，值得一提的是，双系统的安装可以会有较小的风险，但是这种风险也是无法忽略的，笔者建议先对于电脑上的十分重要的数据进行备份再进行Linux系统的安装。当然，安装Linux的虚拟机也是一种不错的选择。

因为笔者将Linux系统作为日常使用，同时写作过相关的教程，以下给出，假如方案不同，请酌情参考(如Linux系统仅作为编程使用，在安装过程中的挂载点设置中不需要设置根目录与home目录的区别)，同时在安装的过程中建议在专业人士的陪同下进行，假如出现了问题，不要擅自操作。

## 阅读指南

### 目的

本文的写作目的在于帮助完全零基础的小白不理解原理而可以无脑安装Linux系统，同时也是为自己进行的一个整理，相较于网上大多数的教程，本教程将一些内容进行了整合与整理，加之本人在安装Ubuntu系统的时候听从学长的教导了解的内容，对于部分的网络常见的教程进行了部分的“优化”。

### 阅读建议

在过程中假如出现了与教程中情况不符合的情况，不建议自己根据自己的猜想进行操作，而是寻找身边的计算机大佬或者在网上进行求助，对于网上的教程也不要盲目的实施，而是查看网上教程针对的问题和自己所面对的是否是同一种问题。
同时为了一些篇幅的连贯性，一些操作的说明以及讲解放在了本文中Tips的部分，假如说看到了一些自己不太能理解的操作，而确实有理解的必要(毕竟本文本身以不需要理解的傻瓜式教程作为目的)，可以去Tips中看看有没有自己需要的内容。
不可否认的是，本篇中有大量的文字描述，一些诸如在安装系统过程中的截图，在事后本人才发现可以通过手机拍屏在通过扫描软件处理得到可以使用的图片，但是在当时由于没有备图，用自己的电脑反复重装系统又不太现实，还是希望阅读者可以耐心阅读文字部分，不要遗漏任何内容，若有无法理解请不要盲目尝试，而是找有技术的人寻求支持。
本文部分图片取自相关软件官网。

## 前置

### 什么是Linux系统

在安装Ubuntu系统之前，我们必须了解什么是Linux系统，简单来说：
Linux系统是一套免费使用和自由传播的类Unix操作系统，是一个基于POSIX和UNIX的多用户、多任务、支持多线程和多CPU的操作系统，其内核由林纳斯·本纳第克特·托瓦兹于1991年10月5日首次发布。它能运行主要 的Unix工具软件、应用程序和网络协议。它支持32位和64位硬件。Linux继承了Unix以网络为核心的设计 思想，是一个性能稳定的多用户网络操作系统。Linux有上百种不同的发行版，如基于社区开发的debian、archlinux，和基于商业开发的Red Hat Enterprise Linux、SUSE、Oracle Linux等。
而Ubuntu Desktop是由Canonical开发的Linux发行版(指由Linux内核开发的操作系统)，由于其易用性，它是最受欢迎的发行版之一。它也是刚开始使用Linux的人的首选之一。

### 为什么选择Ubuntu系统

对于阅读这篇教程的人来说，主要是因为需要使用ROS(Robotic Operating System)，而ROS只支持在Linux系统上安装部署，并且它的首选开发平台是Ubuntu。同时Ubuntu系统在日常的编程中因为一些指令的存在，对于配置依赖等也十分的便捷(相较于Windows简直便捷了无数倍)。

### 什么样的电脑可以装上Ubuntu系统

首先对于安装Ubuntu系统的电脑来说，根据本人个人经验，假如说是想配置一套可以长期使用的Ubuntu系统，电脑应当有一段完整的空白的空间位于某一分区的末尾，并且大小在100GB左右(假如说只是用于基础的编程，或许40GB左右就可以)。
注：众所周知分区的设置也是有讲究的，因为磁盘的存储本质上是有序的，可以理解为一条存储空间，假如说你的一个分区占用了其中的一部分，而且只在这部分的头和尾存了东西，中间确实有大片的空白，但是你并不能把它切出来，不然应该会有奇怪的现象，不过我没了解过，也没试过，你有兴趣可以了解，但是不建议尝试，除非你对于这个硬盘已经毫无留恋了。

### 选择双系统而非虚拟机

相较网上一部分的教学，关于虚拟机安装Ubuntu系统，我们更愿意选择使用双系统，虽然它需要重启才可以在不同的系统之间切换，但是这可以让Ubuntu系统发挥电脑的全部性能。

## 启动盘

在经过了前面的介绍，我们已经知道了什么是Ubuntu系统，并且我们要具备怎样的条件才能搭建Ubuntu系统了，接下来就来到了制作启动盘的步骤。

### 什么是启动盘

启动盘不像其名字一样，像是每次启动这个系统的时候都需要使用启动盘才可以启动一样，要是更加形象的形容，更像是一个放置系统的安装包的地方。比方说你从Windows系统下载了Ubuntu系统的系统文件(一般为iso文件，也就是光盘映像文件)，这个文件本身等于说是放在了Windows系统所属的存储空间中，你很难指望在一个系统里的文件能跳脱出这个系统而去在电脑中安装另一个系统，而假如说你将这个文件放到一个U盘中，虽然说U盘也可以在Windows系统中被识别，但是，值得注意的是，被识别。是的，U盘并不属于Windows系统，所以我们可以使用U盘进行安装，而这块U盘便被称为启动盘。

### 制作流程

现在网络上一般的教程都使用Rufus软件制作启动盘，但是这种方法无疑存在一种弊端，便是会“毁掉”你的U盘。在制作启动盘的过程中存在一步被称为“部署”的步骤，这一步会将iso文件放进你的U盘，但是使用Rufus之后，你的U盘将不能用于其他的用途。也就是说即使你有一个1TB大小的U盘，而iso文件一般只有不到4GB，你的U盘也不能再装进去任何东西，否则就无法进行后续的系统安装了，而假如你想用这个U盘安装其他的系统，制作成其他系统的启动盘，你则需要格式化这个U盘。
不过，技术总是在变革，在这里推荐软件[ventoy](https://www.ventoy.net/cn/index.html)，ventoy软件具有诸多的优势，此处让我们引用一段其官网的说明：“简单来说，ventoy是一个制作可启动U盘的开源工具。有了Ventoy你就无需反复地格式化U盘，你只需要把 ISO/WIM/IMG/VHD(x)/EFI 等类型的文件直接拷贝到U盘里面就可以启动了，无需其他操作。你可以一次性拷贝很多个不同类型的镜像文件，Ventoy 会在启动时显示一个菜单来供你进行选择”。
让我用通俗的流程来讲解一下，以下讲解下载并安装Ubuntu20.04.5：

1. 从清华源下载[ubuntu-20.04.5-desktop-amd64.iso](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/ubuntu-20.04.5-desktop-amd64.iso)(点一下直接下载，或者不行的话可以手动前往[清华源界面](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/)选择ubuntu-20.04.5-desktop-amd64.iso下载)。
2. 下载[ventoy-1.0.84](https://mirrors.nju.edu.cn/github-release/ventoy/Ventoy/Ventoy%201.0.85%20release/ventoy-1.0.85-windows.zip)(点一下直接下载，从GitHub下载需要科学上网，此处选择的链接源自南京大学镜像站)，或者不行的话手动前往其[官网](https://www.ventoy.net/cn/index.html)挑选下载。
3. 解压下载的ventoy压缩包，该压缩包开袋即食，进入解压后的文件夹，启动Ventoy2Disk.exe，应出现以下界面：

![[Ventoy2Disk启动界面.png]]

4. 在电脑上接入已经准备好的U盘(建议是空U盘，否则做好内容备份)，点击软件中“设备”右侧刷新图标，然后下拉设备菜单，选择你的U盘，之后点击安装，假如不出意外，可以看到你的U盘名字被改成了Ventoy，之后把你事先下载好的ubuntu-20.04.5-desktop-amd64.iso文件拷贝进U盘即可。在这里可以解释一下Ventoy的特性，这是一个可以制作多系统启动盘的软件，安装在你的U盘之后，一切被拷入的系统配置文件都会被自动配置，在重启并按照正常安装系统流程操作的过程中会出现一个菜单界面(下图)，供你选择你想要安装的系统，而同时这个U盘也可以用于常规的拷贝文件与储存。

![[Ventoy菜单界面.png]]

5. 到这里，你的启动盘已经制作完成了，貌似非常简单，接下来，将进入安装系统的步骤，请聚精会神，不要错过任何一个步骤。

## 安装系统

### 准备空间

首先，在安装系统之前，还记得我们之前说的吗？要保证你有空闲的100GB空间，当然，这前提是，你失去了这100GB空间之后，你的Windows系统的空间依然不会显得逼仄(尤其是C盘，Windows系统的文件会不断变大，假如说不知道缩减方法，不建议盲目删除一些东西，而也因此需要为C盘留下一定的空间余量)。
Windows+E打开资源管理器，右键单击此电脑，选择管理(Windows11需要先点击显示更多选项)，进入计算机管理页面。点击存储-->磁盘管理，会进入以下界面：

![[压缩卷.png]]

在这里找到你之前觉得有空余空间的磁盘，单击右键选择压缩卷，在页面中“输入压缩空间量”中输入你需要压缩的空间大小，若按照之前的要求100GB，你需要输入102400，然后点击压缩，等待完成即可。

![[输入压缩量.png]]

## 安装系统

插入制作好的启动盘，重启电脑，重启的过程中狂按F12，然后在出现的页面的左下角找到你的U盘(可以尝试辨别一下是哪个，或者先退出，然后去Windows里看看你的U盘的学名)即可进入上方给出过的Ventoy菜单界面，理论来说应该只有我们需要安装的Ubuntu20.04.5，按下Enter(回车)进行确认。

![[打开U盘.jpg|300]]

![[Ventoy选择Ubuntu.jpg]]

![[Ventoy选择模式.jpg]]

值得一提的是在大多数的非图形化页面中，并不存在光标这一物体，需要通过键盘的上下左右键(不是WASD)进行选择，用Enter键(回车键)进行确认。
可能出现选项，选择第一项Ubuntu即可，之后会显示正在检测文件。

![[选择Ubuntu安装.jpg]]

![[检查磁盘内容.jpg]]

等待一段时间，应该可以见到如下界面(暂时无需联网)：
1. 欢迎，在左侧栏选择Chinese，点击继续。

![[Ubuntu欢迎.jpg]]

2. 键盘布局，在左侧栏选择Chinese，右侧栏选择Chinese，点击继续。

![[Ubuntu键盘布局.jpg]]

3. 无线，在下方选择我现在不想链接wi-fi无线网络，点击继续。

![[Ubuntu无线.jpg]]

4. 更新和其他软件，选择最小安装，下方两个不勾选(因为没联网)，点击继续。

![[Ubuntu更新和其他软件.jpg]]

5. 安装类型，其他选项，点击继续。
6. 之后不出意外会看到一个界面，大致为一个表格：

| 设备           | 类型 | 挂载点 | 格式化? | 大小     | 已用 | 已装系统 |
| -------------- | ---- | ------ | ------- | -------- | ---- | -------- |
| /dev/nvme0n1p0 | ntfs |        |         | xxxx     | xxxx | xxxx     |
| /dev/nvme0n1p1 | ntfs |        |         | xxxx     | xxxx | xxxx     |
| /dev/nvme0n1p2 | ntfs |        |         | xxxx     | xxxx | xxxx     |
| 空闲           |      |        |         | 102400MB |      |          |

选择这个我们之前建立出来的102400MB的空闲，表格的左下角应有一个加号和一个减号，点击加号，会出现窗口“创建分区”，选择逻辑分区，空间起始位置，用于efi，不选择挂载点，大小为300MB。之后再创建三个分区，其中之一用于交换空间，其他不变，理论来说大小与你的内存大小一致，但是小一些设置个2GB也不是问题；其中之一用于btrfs，挂载点“/”，大小建议60GB左右，其他不变；其中之一，其中之一用于btrfs，挂载点“/home”，大小为剩余大小，其他不变。

![[Ubuntu安装类型.jpg]]

以上创建的分区，均在下方选择下方的安装启动器的设备，选择新建的efi对应的设备。之后继续继续继续继续。
配置完毕之后点击现在安装。
7. 您在什么地方，选择上海，点击继续。

![[Ubuntu您在什么地方.jpg]]

8. 您是谁？设置你的姓名、计算机名和用户名，值得一提的是密码可以设置的简短一些，因为在Ubuntu后续的操作中会使用sudo来获取root权限，这个过程需要输入密码，而sudo在你使用Ubuntu的时候经常出现。

![[Ubuntu您是谁.jpg]]

9. 重启你的电脑。会显示拔出你的U盘，拔出，然后按下Enter回车键。
10. 重启之后不会像之前一样直接进入Windows界面，而是进入Grub界面，也就是一个黑色的看上去很简陋的纯文字界面，在左上角会显示Ubuntu和Windows界面，通过上下键可以进行选择，按Enter回车键确定，此处选择Ubuntu。

### 独显直连与显卡驱动

虽然说这部分应该是一种“优化”，但是这两点没有充分配置，可能对于新手来说，这个Ubuntu系统和无法使用基本上没有区别，接下来依次讲解：

#### 源

点击左下角呼出应用列表，在软件与更新中：

![[软件与更新.png]]

找到“Ubuntu软件-可从互联网下载-源代码”，勾选，并在下方下拉列表选择其他，选择你心仪的源，这里本人选择`mirrors.huaweicloud.com`。中间一切操作询问许可均许可。

![[Ubuntu选择下载服务器.jpg]]

![[Ubuntu软件和更新更新缓存.jpg]]

#### 独显直连

假如说你的电脑同时拥有核显和独显，bios具备动态切换功能，那么在上述步骤重启之后你可能会遇到重启之后进入Ubuntu系统显示为黑屏的情况，此时需要修改为独显直连，首先先按下CTRL+ALT+DEL重启，然后狂按F2(此处视主板型号不同有所不同，可自己查询自己的电脑进入BIOS界面的方法)，然后在其中寻找“Hybrid Graphics/Advanced Optimus”，将ON改为OFF，此处的位置因不同BIOS不同而不同，请自行挨个寻找。之后点击下方APPLY CHANGES，OK，退出重启即可。

#### 显卡驱动

此时你已经可以再一次登入Ubuntu系统，这个奇怪的桌面陌生的环境让你非常的不适应，但是更重要的是，你感觉Ubuntu系统奇卡无比。还记得一开始选择双系统的初衷吗？就是为了让性能被完全发挥，但是事实上如今却没有这个效果，这是因为你没有安装显卡驱动，接下来介绍安装显卡驱动的方法，不过在此之前，简单介绍一下Linux系统的强大工具：终端。
由于本教程的目的是进行Ubuntu系统的安装配置与剩余的优化，并不是讲解Ubuntu系统的终端，所以此处会简单的介绍一下这个工具。在任何界面(大概)按下CTRL+ALT+T可以呼出终端，大多数的终端的操作只在这里进行就可以。而指令带有sudo的前缀意味着你使用ROOT权限进行，我们不去理解下面的命令，只需要进行复制粘贴就好，值得一提的是，在终端中，CTRL+C意味着退出当前进程，而复制粘贴在终端中则需要使用CTRL+SHIFT+C/V，不过在外面还是CTRL+C/V。
首先依次复制粘贴以下指令，按回车，假如说让输入密码就输入密码(输入密码的时候密码不会显示出来，这不是因为你没输入进去，输入完之后按下回车就好)，让输入Y/n的时候输入Y。

```zsh
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```

等待结束，在这个过程中可以看看窗外的风景什么的，cuda的源不太妙，所以下载的会比较慢。
下载完毕之后再次重启电脑即可，可以发现这一次进入系统会快上不少，此时我们已经完成了基本配置的全部内容了。

## Ubuntu常用依赖与美化

假如说想要长期住在Ubuntu，一些对于系统的美化，让系统的使用更加的顺手肯定是少不了的，尤其是对于我这种不使用动态桌面都浑身难受得人来说。
众所周知，.exe文件是Windows操作系统支持的，但是Ubuntu系统并不直接支持，这也就说明最常见的设置动态桌面的方法，从steam下载wallpaper engine已经行不通了，包括其他的诸多操作也是，所以我们将依次介绍对于一些事物的美化操作。

### 常用依赖的下载

我们需要下载一些常用的依赖，包括说git(用于github或者gitee相关的支持)、gcc、g++等一些熟悉的面孔以及zsh、curl之类的，使用方法还是在终端直接输入就好。

```zsh
sudo apt install git curl vim gcc g++ zsh chrome-gnome-shell
```

### GNOME

#### 什么是GNOME

GNOME是一套纯粹自由的计算机软件，运行在操作系统上，提供图形桌面环境。GNOME 包含了 Panel (用来启动此程式和显示目前的状态)、桌面 (应用程式和资料放置的地方)及一系列的标准桌面工具和应用程式，并且能让各个应用程式都能正常地运作。GNOME是Linux操作系统上最常用的图形桌面环境之一。

#### 设置GNOME与拓展

在你的Mozilla Firefox浏览器中的右上角，点击这个由三个横杠组成的图表，然后在下拉菜单中找到“拓展和主题”，点击进入。

![[拓展和主题.png]]

在上方的寻找更多附加组件中搜索“GNOME Shell 集成”，点进去，然后点击添加到Firefox，中间会有一个弹窗，选择“添加”。
之后会发现右上角有了这个脚掌形状的图表，若没有可以重启Firefox，点击进去，会进入“https://extensions.gnome.org/”。
在上方搜索栏中依次搜索“Caffeine”、“Dash to Panel”、“Prime Indicator”与“Tray Icons: Reloaded”，并且点击进去，将OFF的开关打开，会显示问你是否安装拓展，选择安装。

![[GNOME插件关.png]]

![[GNOME插件开.png]]

![[安装插件.png]]

简单介绍一下三个插件，Caffeine插件的作用是在你的任务栏的角落里增加一个咖啡的图标，点击一下会禁用自动挂起和屏幕保护程序，也就是禁止自动锁屏一类的操作。

![[Caffeine.png]]

Dash to Panel的作用是给予了你更改任务栏的能力，右键你的任务栏，选择Dash to Panel设置，你就可以在出现的窗口中决定任务栏的位置以及对齐方式了。

![[Dash to Panel.png]]

举个简单的例子来说，你不太习惯Ubuntu在左侧的任务栏，在面板屏幕位置中选择底部，任务栏就会来到底部，像是你曾经使用的Windows一样。

![[任务栏位置设置.png]]

而Tray Icons: Reloaded的功能我没有验证过，按照描述修改的也是图标。

![[Tray Icons.png]]

### VSCode

曾几何时我们不敢使用VSCode进行编程，虽然我们都知道VSCode的拓展性之高，但是却畏于其配置之复杂，一个配置C++环境就已经十分的麻烦，但是就像是一开始我说的那样，Linux系统提供了较为便捷的配置方法，就像是上述的g++与gcc，只需要一行代码即可，所以说让我们从[官网](https://code.visualstudio.com/)下载VSCode吧，选择deb，之后使用下方语句。

```zsh
sudo dpkg -i deb包的完整名称(包括后缀名)
# 此行为注释，上方如 sudo dpkg -i code_1.74.0-1670260027_amd64.deb 
```
之后进入VSCode，换成简体中文(插件，一般来说右下角会提示你安装并重启，否则你可以点击在左侧栏中的拓展图标(如下图)，并搜索Chinese (Simplified) (简体中文)，选择第一个，点击install)。

![[VSCode拓展.png]]

之后便是更加多的插件的选择，这些插件能让你的VSCode看上去更加顺眼，如下：

![[VSCode插件.png]]

#### CMake && CMake Tools

使用CMake编写CMakeList进行库与项目的关联是很重要的一环，当然，CMake还具有许多其他的强大功能。

#### C++

都写C++的程序了，自然也需要C++的插件，不过C++的“拓展插件”是否安装，看个人需求吧，本人没有安装。

#### SynthWave '84

一个外观美化的插件，但是其实，说到底，貌似，编程软件的外观也就那么回事，对吧......

#### background-cover

貌似可以替换壁纸，不过在使用的时候或许需要先在终端中输入一句`sudo chown -R $(whoami) /usr/share/code`，相关的这篇[教程](https://blog.csdn.net/qq_53627591/article/details/122528373)很不错，在过程中有什么问题可以看这个。

#### Doxygen Documentation Generator

强大的注释插件，可以看看插件的介绍，还是很好用的，对于规范的注释，以及在注释后快捷生成说明文档。

#### Material Icon Theme

图标的外观。

#### Todo Tree

安装之后在左侧栏会多出一个树一样的图标，同时在程序中的注释中的行首加上TODO或者FIXME字样后空格，可以点击树一样的图标之后可以显示全部该字样的地点以及该行内的内容，同时点击可以进行跳转，可以理解为一个记录目标的插件。

![[Todo Tree图标.png]]

![[TODO与FIXME.png]]

### 动态壁纸

在Ubuntu中拥有一个简单的壁纸是很简单的，就像在Windows一样选择图片进行切换即可，但是假如你是一个对这个你可能用一次电脑都见不到几秒钟的壁纸稍有追求的话，想必在Windows上已经对大名鼎鼎的Wallpaper Engine已经无比熟悉，但是在Ubuntu没有如此便捷的软件可以有一个创意工坊、更多的自定义选项，以及友好的操作来供你选择，不过好在Komorebi为你提供了剩余的选择：使用一个视频作为壁纸。
首先使用`sudo apt install `下载软件，此时呼出软件列表，应该可以发现多出了两个软件，分别为Komorebi和Wallpaper Creator，其中Komorebi是负责展现动态壁纸的软件，而Wallpaper Creator则可以制作动态壁纸。
那么现在，你需要一个素材，可以先回到Windows使用Wallpaper Engine寻找一下你喜欢的壁纸，一般来说Live2D感较低的动态壁纸更可能是上传者上传了一个纯视频，下载之后打开其在文件资源管理器的位置，即可看到后缀名为`.mp4`或者类似格式的视频文件，假如没有，就换一个吧。
然后按照Tips中的方法，回到Ubuntu之后找到你的这个视频文件，以及应该在同一文件夹下名为preview的预览图片，这二者缺一不可，然后打开Wallpaper Creator，按照要求填写壁纸名称，并选择你的Wallpaper是A video，之后选择你的视频地址，值得一提的是下面一栏中的thumbnail也要选择，选择你的预览图片，这一步骤必须进行，否则你可能最后找不到你的壁纸文件。最后点击Next，然后选择是否要添加一个时间图标到你的壁纸上，我一般选择不，再Next，然后不要关闭软件，复制软件上显示的以`sudo`开头的一句指令并在终端中执行，然后打开你的Komorebi，假如说最后面没有显示你新建的壁纸，或者点击壁纸之后桌面是纯黑，可能是因为你没有安装依赖，在终端中输入

```zsh
sudo apt-get install gstreamer1.0-libav
```

之后再打开Komorebi，假如没有显示，点击Quit关闭软件，再在软件列表中启动，应该点击壁纸并在桌面看到其动态。

### 字体

FiraCode是一款适合程序员的字体，支持很多的符号以及连字符，而且本身等宽，这里使用FiraCode Nerd Font，前往[官网](https://www.nerdfonts.com/font-downloads)，下拉找到FiraCode Nerd Font选择Download，下载并在本地解压，之后在终端使用指令`sudo mv 你的这个文件夹的绝对路径或相对路径 /usr/share/fonts`，这里的绝对路径可以进入你解压出来的文件夹，右键属性查看，在后面补全，使得路径以FiraCode结尾，相对路径同理，从当前终端位于的路径开始。这里的mv为move的意思，移动。
移动之后，输入`sudo fc-cache`之后就可以在终端或者VSCode中更换字体，如在终端中单击“三条杠”，选择配置文件首选项，然后点击配置文件下方的任一内容，一般为未命名，勾选自定义字体，点击选择，上拉，可选择为FiraCode Nerd Font Regular。而在VSCode中左下角齿轮-设置-Editor：Font Family，在下方文本框中最前面添加`'FiraCode Nerd Font',`，别忘了复制这个逗号，即可。之后在VSCode中搜索liga，选择Editor：Font Ligatures下方的在settings.json中编辑，将`"editor.fontLigatures": false`中的false改为true。这时候新建一个文本，输入!=，你就能看到连字符的效果了。
假如不行可以先重启一下。

### zsh

假如使用Ubuntu一开始自带的bash，终端界面应该非常的简陋，而zsh可以让你的终端更加美观，而且拥有更强大的补全功能。
在~目录下，假如没有.zshrc文件，创建一个，在其中输入：

```zsh
# Enable Powerlevel10k instant prompt. Should stay close to the top of ~/.zshrc.
# Initialization code that may require console input (password prompts, [y/n]
# confirmations, etc.) must go above this block; everything else may go below.
if [[ -r "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh" ]]; then
  source "${XDG_CACHE_HOME:-$HOME/.cache}/p10k-instant-prompt-${(%):-%n}.zsh"
fi


### Added by Zinit's installer
if [[ ! -f $HOME/.local/share/zinit/zinit.git/zinit.zsh ]]; then
    print -P "%F{33} %F{220}Installing %F{33}ZDHARMA-CONTINUUM%F{220} Initiative Plugin Manager (%F{33}zdharma-continuum/zinit%F{220})Ã¢ÂÂ¦%f"
    command mkdir -p "$HOME/.local/share/zinit" && command chmod g-rwX "$HOME/.local/share/zinit"
    command git clone https://github.com/zdharma-continuum/zinit "$HOME/.local/share/zinit/zinit.git" && \
        print -P "%F{33} %F{34}Installation successful.%f%b" || \
        print -P "%F{160} The clone has failed.%f%b"
fi

source "$HOME/.local/share/zinit/zinit.git/zinit.zsh"
autoload -Uz _zinit
(( ${+_comps} )) && _comps[zinit]=_zinit
### End of Zinit's installer chunk
# zinit
zinit light zsh-users/zsh-autosuggestions
zinit light zdharma/fast-syntax-highlighting
zinit snippet OMZ::lib/clipboard.zsh
zinit snippet OMZ::lib/completion.zsh
zinit snippet OMZ::lib/history.zsh
zinit snippet OMZ::lib/git.zsh
zinit snippet OMZ::lib/theme-and-appearance.zsh
zinit snippet OMZP::sudo/sudo.plugin.zsh
zinit ice depth"1" # git clone depth
zinit light romkatv/powerlevel10k

# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh

#proxy
alias setproxy="export ALL_PROXY=http://127.0.0.1:7890" 
alias unsetproxy="unset ALL_PROXY"
```

在一开始的基础配置的时候不难发现我们已经`apt-get install`了zsh，这时候在我们的终端直接输入zsh就会运行.zshrc中的配置，应该是正在下载一些东西，假如说下载并不是很顺利，可能需要通过代理解决网络问题，这里指路Clash，其他的在本教程中不进行介绍，绿色上网人人有责。
解决网络问题，成功现在之后，首先确认终端的字体已经更换为FiraCode，之后应该会有一个界面，让你确认是否显示出的图案是菱形等图案，假如是就没问题。然后按照上面的内容选择，一个个选择你想要的外观，选择完毕之后输入`chsh`，再输入`/bin/zsh`，结束，重启电脑就可以用上帅气的zsh了。
同时在zsh支持一种更加智能的补全，其会记录你曾经输入的指令，再次输入之后会有显示，但是不同于正常补全使用TAB键，而是按下“向右”键，即可进行补全。

### Firefox

![[Firefox插件.png]]

火狐浏览器同样存在许多的插件可供选择，而这里推荐GNOME Shell集成，不再介绍，可以看上文的内容。
同时对于英语水平不太好的人来说，可以和我一样选择一个诸如百度翻译的翻译插件，支持划译，还是挺好的。

### Grub

在每一次重启电脑的时候，我们会选择使用哪个系统，这个时候会进入的界面被称为Grub界面，假如说没有经过美化，这个界面的内容会是黑底白字，看上去非常的“极客”，不过假如说我们需要一个更加美观的看上去高端一些的Grub界面的话，GNOME也已经为我们找到了方法。
进入[gnome-look](https://www.gnome-look.org/browse/)网站，在左侧栏选择GRUB Themes，在页面中找到一个你喜欢的Grub界面，点进去，在右侧选择Download，你可以理解为有很多的页面里面其实都是一个合集，但是我们安装知识选取了其中的一个主题，所以在Download后出现的列表中选择一个下载并解压，在目录中可以找到一个install.sh的文件，在这里打开终端，输入指令`sudo ./install.sh`，即可，重启电脑，你就可以看到你的全新的Grub界面了。

## Tips

### 访问Windows中的文件

有的时候我们会遇到一些问题，比如说一个很简单的现象，你刚刚在Ubuntu系统安了家，结果发现自己把什么东西忘记在了Windows系统中，这时候使用重启去获取这个文件将是一件繁琐的事情，毕竟没有人想要天天重启，这时候打开Ubuntu系统的“文件”，在左侧一栏中找到其他位置，点进去就可以看到熟悉的你在Windows系统中设置的盘符了，同理想要进入Ubuntu系统根目录下的除home之外的文件夹(比如opt)，也可以通过这个方法进入。

![[其他位置.png]]

### 终端之自动补全

在未进行zsh的设置的时候，终端仅会有一个不智能的自动补全，在终端使用TAB进行补全，场景一般比如在输入一串本地地址的时候，有一个文件夹“dwajdawjlkjckajcheofca”名字非常的长，而在当前目录下仅有这一个文件夹开头三个字母为dwa，在输入dwa之后即可按下TAB进行补全。

## 附录

这里放一些其他的自己突然想到的内容，将来可能从中移除并单独作为新的教程。

### Ubuntu基本终端操作

#### sudo

在一切的指令前面添加sudo意味着使其获得根权限，即最高权限。使用sudo之后需要输入密码，假如在同一终端内连续使用sudo只需要第一次输入密码。

#### ls

输入之后可以查看当前文件夹下的内容。

#### mv、cp与rm

即move、copy与remove，移动、拷贝与删除。这三条指令分别用法为`mv/cp 想要移动的文件的相对或者绝对路径 目的的相对或者绝对路径`以及`rm 想要删除的文件的相对或者绝对路径`，值得一提的是假如要修改一些根目录下的内容，这些语句需要加上sudo前缀。

#### mkdir、gedit、torch与vim

`mkdir 文件夹名`用于创建文件夹；`touch 文件名.后缀名`用于创建文件，需要写上后缀；`gedit 文件名`与`vim 文件名`是两种文件编辑器，其中gedit的界面更加适合新手使用，而vim则有一套自己的操作方法，需要系统的学习，建议学习之后再使用，别乱点。

#### chmod

chmod一般用于修改文件的读写运行权限，其中读写与运行用二进制写出，并且分为三个用户组，大致如下：

![[chmod.jpg]]

使用修改文件权限的执行，必须要在根权限下才可以执行，虽然说有如此多的内容，但是一般来说，使用`chmod`只会使用`chmod 777 文件名`，也就是将该文件的权限完全开放，或者使用`chmod -x 文件名`，也就是将这个文件添加可执行权限。

### ros的安装

#### ros是什么

暂无整理介绍，可以自行上网搜索。

#### 安装指令

这里安装使用清华源，会快一些。
依次输入：

```zsh
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

sudo apt update

sudo apt install ros-noetic-desktop-full
```
安装结束，但是在每一个终端中使用ros的时候都需要手动source一个脚本：

```zsh
source /opt/ros/noetic/setup.bash
```

不过可以通过：

```zsh
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
```
在每次启动终端时自动source这个脚本，同时，假如正在使用的是zsh而非bash，将其中的bash字样改为zsh。

## CMake安装库

```zsh
# 进入下载好的文件夹，这个文件夹需要有一个CMakeList
mkdir build
cd build
cmake ..
make -j8
make test
# 若无误
sudo make install 
```

## 脚本

或许，假如不出以外的话，使用这个脚本可以完成一部分本文开头的操作。这里主要包含了安装ros与Ceres的脚本
脚本内容，再之后有使用方法：

```zsh
# 安装依赖的shell脚本
# 使用之前需要在软件和更新中选择“源文件”的“下载自”

cd ~

# 下载cuda显卡驱动
# 事后会在～目录下留一个cuda-keyring_1.0-1_all.deb，删不删除随你

wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda

# 安装一堆乱七八糟的依赖

sudo apt install git curl vim gcc g++ zsh chrome-gnome-shell cmake

# 安装ros，不想安装直接删除下面这一部分的全部东西就好

sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
sudo apt update
sudo apt install ros-noetic-desktop-full
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
echo "source /opt/ros/noetic/setup.zsh" >> ~/.zshrc
sudo apt install ros-noetic-serial

# 安装Ceres，不想安装直接删除下面这一部分的全部东西就好，确保home目录下没有名为clone的文件夹，若有，在下方手动删除一行 mkdir clone ，并保存。

sudo apt-get install libgoogle-glog-dev libgflags-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libeigen3-dev
sudo apt-get install libsuitesparse-dev
cd ~
mkdir clone
cd ~/clone
git clone https://gitee.com/undark/ceres-solver-1.14.0.git
cd ceres-solver-1.14.0
rm -rf .git
mkdir build
cd build
cmake ..
make -j8
make test
make install
```

在你喜欢的地方打开终端，输入：

```zsh
gedit setup.sh
# 在出现的窗口中输入上方的内容并保存、退出
chmod 777 setup.sh
# 使用之前依次检查是否满足脚本中注释对于文件夹创建的要求
./setup.sh
```
