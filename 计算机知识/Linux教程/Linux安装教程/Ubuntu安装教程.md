# 序

很高兴你进入这一篇教程，了解这个在Linux众多系统中最为风靡的系统之一的安装方法。在开始动手操作之前，我建议你先了解Ubuntu系统的版本，你可以根据你的需要进行选择。

Ubuntu的系统版本都会有对应的名称(以形容词+动物命名)，看上去十分的有趣，同时图标(默认桌面)也会是这种动物。如下：

|Ubuntu系统版本|名称|
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

作为新手，我们建议你选择LTS的版本，也就是Long Term Support，长时间支持，这种版本的维护周期在五年，可以支持更长时间的使用。当今市面上比较流行的版本是20.04(也有部分人使用22.04，但是需要切记，靠前的版本中伴随着更新的体验与更强大的功能的或许还有不完善的框架以及不稳定性)，本教程也将以**讲解安装Ubuntu20.04**为示范，但是值得注意的是，安装Ubuntu的过程大多大同小异，所以依照本教程进行操作也是可以考虑的。

# 注意事项

在安装Linux系统之前，需要注意的是，本教程讲解的是安装双系统，也就是在对于大多数人常用的Windows系统(也有部分是MacOS)之外，在电脑中再安装一个系统。这种操作毫无疑问是**有风险**的，可能会导致硬盘数据的丢失(假如没有谨慎操作或者说出现的意外，尽管这种风险极低，但是依然有必要注意)，所以请确保你至少有一位善于计算机的朋友可以为你提供线下面对面的支持，并且确保已经谨慎阅读了一切内容。

在安装系统之前请检查自己的重要文件并进行备份，参考并使用本教程为读者自愿行为，本教程概不为任何损失承担责任。

# 检查配置

在安装系统之前，需要检查你的电脑配置是否足以安装双系统，这里的配置并非如游戏配置一样的显卡与CPU参数等，而是你的电脑的磁盘是否有足够的空间，以及你的电脑的[[磁盘存储格式]]是否正确。

一般来说安装Linux系统的过程中，使用GPT格式的硬盘更为便于安装双系统，尤其是当你要将两个系统分别装在不同的硬盘中的时候，由于MBR硬盘存储格式对于分区数量的限制，加上双系统会要求进行一定的硬盘分区，所以使用GPT是更为安全的选择，假如说没有GPT格式的硬盘，也可以尝试使用MBR格式，但是为了一劳永逸，也建议将重要数据备份之后将硬盘转换存储格式。

一般来说安装Linux系统，假如说只是为了某种编程使用，建议预留50GB的空间，假如说为了更加长期且舒适的体验，100~200GB是需要准备的，当然，假如说完全日常的使用需要考虑下载以及储存内容消耗的空间(比如说下载一些视频或者图片)，所以上不封顶。