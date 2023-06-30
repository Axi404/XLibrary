# 序

很高兴你进入这一篇教程，了解这个在 Linux 众多系统中最为风靡的系统之一的安装方法。在开始动手操作之前，我建议你先了解 Ubuntu 系统的版本，你可以根据你的需要进行选择。

Ubuntu 的系统版本都会有对应的名称（以形容词+动物命名），看上去十分的有趣，同时图标（默认桌面）也会是这种动物。如下：

|Ubuntu 系统版本|名称|
|---|---|
|Ubuntu 4.10|Warty Warthog|
|Ubuntu 5.04|Hoary Hedgehog|
|Ubuntu 5.10|Breezy Badger|
|Ubuntu 6.06 LTS|Dapper Drake|
|Ubuntu 6.10|Edgy Eft|
|Ubuntu 7.04|Feisty Fawn|
|Ubuntu 7.10|Gutsy Gibbon|
|Ubuntu 8.04 LTS|Hardy Heron|
|Ubuntu 8.10|Intrepid Ibex|
|Ubuntu 9.04|Jaunty Jackalope|
|Ubuntu 9.10|Karmic Koala|
|Ubuntu 10.04 LTS|Lucid Lynx|
|Ubuntu 10.10|Maverick Meerkat|
|Ubuntu 11.04|Natty Narwhal|
|Ubuntu 11.10|Oneiric Ocelot|
|Ubuntu 12.04 LTS|Precise Pangolin|
|Ubuntu 12.10|Quantal Quetzal|
|Ubuntu 13.04|Raring Ringtail|
|Ubuntu 13.10|Saucy Salamander|
|Ubuntu 14.04 LTS|Trusty Tahr|
|Ubuntu 14.10|Utopic Unicorn|
|Ubuntu 15.04|Vivid Vervet|
|Ubuntu 15.10|Wily Werewolf|
|Ubuntu 16.04 LTS|Xenial Xerus|
|Ubuntu 16.10|Yakkety Yak|
|Ubuntu 17.04|Zesty Zapus|
|Ubuntu 17.10|Artful Aardvark|
|Ubuntu 18.04 LTS|Bionic Beaver|
|Ubuntu 18.10|Cosmic Cuttlefish|
|Ubuntu 19.04|Disco Dingo|
|Ubuntu 19.10|Eoan Ermine|
|Ubuntu 20.04 LTS|Focal Fossa|
|Ubuntu 20.10|Groovy Gorilla|
|Ubuntu 21.04|Hirsute Hippo|
|Ubuntu 21.10|Impish Indri|
|Ubuntu 22.04|Jammy Jellyfish|
|Ubuntu 22.10|Kinetic Kudu|

作为新手，我们建议你选择 LTS 的版本，也就是 Long Term Support，长时间支持，这种版本的维护周期在五年，可以支持更长时间的使用。当今市面上比较流行的版本是 20.04（也有部分人使用 22.04，但是需要切记，靠前的版本中伴随着更新的体验与更强大的功能的或许还有不完善的框架以及不稳定性），本教程也将以**讲解安装 Ubuntu 20.04** 为示范，但是值得注意的是，安装 Ubuntu 的过程大多大同小异，所以依照本教程进行操作也是可以考虑的。

# 注意事项

在安装 Linux 系统之前，需要注意的是，本教程讲解的是安装双系统，也就是在对于大多数人常用的 Windows 系统（也有部分是 MacOS）之外，在电脑中再安装一个系统。这种操作毫无疑问是**有风险**的，可能会导致硬盘数据的丢失（假如没有谨慎操作或者说出现的意外，尽管这种风险极低，但是依然有必要注意），所以请确保你至少有一位善于计算机的朋友可以为你提供线下面对面的支持，并且确保已经谨慎阅读了一切内容。

在安装系统之前请检查自己的重要文件并进行备份，参考并使用本教程为读者自愿行为，本教程概不为任何损失承担责任。

# 检查配置

在安装系统之前，需要检查你的电脑配置是否足以安装双系统，这里的配置并非如游戏配置一样的显卡与 CPU 参数等，而是你的电脑的磁盘是否有足够的空间，以及你的电脑的[[磁盘存储格式]]是否正确。

一般来说安装 Linux 系统的过程中，使用 GPT 格式的硬盘更为便于安装双系统，尤其是当你要将两个系统分别装在不同的硬盘中的时候，由于 MBR 硬盘存储格式对于分区数量的限制，加上双系统会要求进行一定的硬盘分区，所以使用 GPT 是更为安全的选择，假如说没有 GPT 格式的硬盘，也可以尝试使用 MBR 格式，但是为了一劳永逸，也建议将重要数据备份之后将硬盘转换存储格式。

一般来说安装 Linux 系统，假如说只是为了某种编程使用，建议预留 50 GB 的空间，假如说为了更加长期且舒适的体验，100~200 GB 是需要准备的，当然，假如说完全日常的使用需要考虑下载以及储存内容消耗的空间（比如说下载一些视频或者图片），所以上不封顶。

# 准备启动盘

## 启动盘

在经过了前面的介绍，我们已经知道了什么是 Ubuntu 系统，并且我们要具备怎样的条件才能搭建 Ubuntu 系统了，接下来就来到了制作启动盘的步骤。

### 什么是启动盘

启动盘不像其名字一样，像是每次启动这个系统的时候都需要使用启动盘才可以启动一样，要是更加形象的形容，更像是一个放置系统的安装包的地方。比方说你从 Windows 系统下载了 Ubuntu 系统的系统文件（一般为 iso 文件，也就是光盘映像文件），这个文件本身等于说是放在了 Windows 系统所属的存储空间中，你很难指望在一个系统里的文件能跳脱出这个系统而去在电脑中安装另一个系统，而假如说你将这个文件放到一个 U 盘中，虽然说 U 盘也可以在 Windows 系统中被识别，但是，值得注意的是，被识别。是的，U 盘并不属于 Windows 系统，所以我们可以使用 U 盘进行安装，而这块 U 盘便被称为启动盘。

### 制作流程

现在网络上一般的教程都使用 Rufus 软件制作启动盘，但是这种方法无疑存在一种弊端，便是会“毁掉”你的 U 盘。在制作启动盘的过程中存在一步被称为“部署”的步骤，这一步会将 ISO 文件放进你的 U 盘，但是使用 Rufus 之后，你的 U 盘将不能用于其他的用途。也就是说即使你有一个 1 TB 大小的 U 盘，而 iso 文件一般只有不到 4 GB，你的 U 盘也不能再装进去任何东西，否则就无法进行后续的系统安装了，而假如你想用这个 U 盘安装其他的系统，制作成其他系统的启动盘，你则需要格式化这个 U 盘。  

不过，技术总是在变革，在这里推荐软件 [ventoy](https://www.ventoy.net/cn/index.html)，ventoy 软件具有诸多的优势，此处让我们引用一段其官网的说明：“简单来说，ventoy 是一个制作可启动 U 盘的开源工具。有了 Ventoy 你就无需反复地格式化 U 盘，你只需要把 ISO/WIM/IMG/VHD/EFI 等类型的文件直接拷贝到 U 盘里面就可以启动了，无需其他操作。你可以一次性拷贝很多个不同类型的镜像文件，Ventoy 会在启动时显示一个菜单来供你进行选择”。  

让我用通俗的流程来讲解一下，以下讲解下载并安装 Ubuntu 20.04.5：

1. 从清华源下载 [ubuntu-20.04.5-desktop-amd64.iso](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/ubuntu-20.04.5-desktop-amd64.iso) （点一下直接下载，或者不行的话可以手动前往[清华源界面](https://mirrors.tuna.tsinghua.edu.cn/ubuntu-releases/20.04/)选择 ubuntu-20.04.5-desktop-amd 64. Iso 下载）。
2. 下载 [ventoy-1.0.84](https://mirrors.nju.edu.cn/github-release/ventoy/Ventoy/Ventoy%201.0.85%20release/ventoy-1.0.85-windows.zip) (点一下直接下载，从 GitHub 下载需要科学上网，此处选择的链接源自南京大学镜像站)，或者不行的话手动前往其[官网](https://www.ventoy.net/cn/index.html)挑选下载。
3. 解压下载的 ventoy 压缩包，该压缩包开袋即食，进入解压后的文件夹，启动 Ventoy 2 Disk. Exe，应出现以下界面：

![[Ventoy2Disk启动界面.png]]

4. 在电脑上接入已经准备好的 U 盘 (建议是空 U 盘，否则做好内容备份)，点击软件中“设备”右侧刷新图标，然后下拉设备菜单，选择你的 U 盘，之后点击安装，假如不出意外，可以看到你的 U 盘名字被改成了 Ventoy，之后把你事先下载好的 ubuntu-20.04.5-desktop-amd 64. Iso 文件拷贝进 U 盘即可。在这里可以解释一下 Ventoy 的特性，这是一个可以制作多系统启动盘的软件，安装在你的 U 盘之后，一切被拷入的系统配置文件都会被自动配置，在重启并按照正常安装系统流程操作的过程中会出现一个菜单界面 (下图)，供你选择你想要安装的系统，而同时这个 U 盘也可以用于常规的拷贝文件与储存。

![[Ventoy菜单界面.png]]

5. 到这里，你的启动盘已经制作完成了，貌似非常简单，接下来，将进入安装系统的步骤，请聚精会神，不要错过任何一个步骤。