---
title: 关于GPU驱动的安装方法
date: 2026-06-03 21:20:21
tags:
    - 搞机日常
categories:
    - 教程分享
top_img: /img/GPU Driver Banner.jpeg
---

# 关于GPU驱动的安装方法

众所周知 安装新版本的gpu驱动能够大幅降低游戏功耗（心虚）提高跑分一般性的安装方法就是直接刷制作好的gpu的面具模块,或者是在第三方rec中刷入驱动卡刷包。这两者都缺陷与优点，前者方便，但是在配合shamiko模块使用时，一些被排除的应用会出现极其频繁的花屏、闪屏现象，虽然能使用但是还是废了点眼睛😵）而且momo还会报“找到被magisk模块修改的文件”  
（这你能忍？😡执着于环境隐藏的小伙伴们估计要急得睡不着了）

<figure style="text-align: center;">
  <img src="/img/momo检测环境异常.jpg" alt="momo检测环境异常" width="400">
  <figcaption>图1：momo检测环境异常</figcaption>
</figure>

而且在一些奇奇怪怪的情况下会发生奇怪的bug，比如有一天晚上我犯病了，手欠频繁的打开关闭驱动模块（不知道是Magisk问题还是模块bug）我手机的驱动直接就掉了😫开机及花屏，当时我就慌的不行了，好在我有第三方Rec twrp，在里面重装了一次驱动模块才给救回来（🐮魔的当时真给我吓死，大家真的不要在晚上搞机😭）好在面具刷入不需要解锁vendor分区

后者从第三方rec刷入卡刷包，好处是更稳定，前提是要做好备份，momo也不会报错，毕竟这相当于也是更新系统了，它测不出这个。但是但是，如果你不解锁分区，等到的结果就是白白重启一次😂

<figure style="text-align: center;">
  <img src="/img/twrp提示vendor is not mounted.jpg" alt="twrp提示vendor is not mounted" width="400">
  <figcaption>图2：twrp提示vendor is not mounted</figcaption>   
</figure>

这也有缺点，那也有缺点，这时候可能就有小伙伴门要问了“驻波驻波我们有没有什么办法不用解锁分区就能够刷入呢🤔”，那自然就是有的，简单来说就是把vendor分区提取出来，出来然后将驱动文件覆盖进去

首先我们要准备好一台电脑（没有也没事），数据线，勤劳的双手和你的耐心

首先就是提取出我们的vendor分区，准备好我们的刷机包，如果是线刷包就直接解压找到super.img和boot.img这俩个文件
如果是卡刷包的话你就只会看见`payload.bin`这个文件  
那么我们就把`payload.bin`这个单独文件解压出来

打开dna这个软件，有手机版和电脑端的，如果手机内存不够可以上电脑里搞

首先是电脑端  
用管理员权限运行这个程序

<figure style="text-align: center;">
  <img src="/img/PC-DNA.jpg" alt="PC-DNA" width="400">
  <figcaption>图3：电脑端DNA界面</figcaption>   
</figure>

我们先输入0来新建一个工程，并且按照它的要求来给我们的工程取个名字，这里以我的机型命名k60pro

新建完后你就会发现文件夹里出现了这个名字的工程文件夹

我们来打开它，发现里面只有这仨个文件夹，第一个文件夹要放我们要处理的文件，第二个是它的输出文件夹，第三个我们还用不到

<figure style="text-align: center;">
  <img src="/img/DNA文件夹.jpg" alt="DNA文件夹" width="400">
  <figcaption>图4：DNA文件夹</figcaption>   
</figure>

如果你是卡刷包  
我们将之前得到的payload.bin文件放进去  
如果你是线刷包，已经有了`super.img`和`vbmeta.img` 那就把这俩放入第一个文件夹中  
重新运行dna，选择我们的工程 然后输入3来分解我们的`payload.bin` 输入1来选择指定镜像 我们将`vbmeta.img`和vendor分区提取出来,像这样

<figure style="text-align: center;">
  <img src="/img/提取vbmeta和vendor.jpg" alt="提取vbmeta和vendor" width="400">
  <figcaption>图5：提取vbmeta和vendor</figcaption>   
</figure>

然后按回车，提取好后它提示我们是否要继续分解，我们输入1，这样我们就会发现工程文件中多出了vendor这个文件夹（vbmeta是不能继续分解的）这就是我们提取出来的文件  
如果你是线刷包那就在工程界面输入1直接选择分解img，无需上面这些操作

***

现在来到手机端  
我们新建好工程后把要分解的东西放入这个路径下

<figure style="text-align: center;">
  <img src="/img/放入自己建的工程文件夹下 我的是k60pro.jpg" alt="放入自己建的工程文件夹下 我的是k60pro" width="400">
  <figcaption>图6：放入自己建的工程文件夹下 我的是k60pro</figcaption>   
</figure>

`payload.bin`的分解bin，得到img的分解img

<figure style="text-align: center;">
  <img src="/img/手机端DNA工程菜单.jpg" alt="手机端DNA工程菜单" width="400">
  <figcaption>图7：手机端DNA工程菜单</figcaption>   
</figure>

分解好的文件夹在下面这个路径中

<figure style="text-align: center;">
  <img src="/img/分解路径.jpg" alt="分解路径" width="400">
  <figcaption>图8：/data/DNA/NA_K60pro/</figcaption>   
</figure>

然后准备好我们的驱动文件 下图是模块内容

<figure style="text-align: center;">
  <img src="/img/模块内容.jpg" alt="模块内容" width="400">
  <figcaption>图9：其它的文件不用管</figcaption>   
</figure>

打开system文件夹 把里面的vendor文件夹覆盖到先前分解好的vendor文件夹中

如果是卡刷包的则将这几个文件覆盖进先前分解好的vendor文件夹中

<figure style="text-align: center;">
  <img src="/img/模块内容2.jpg" alt="模块内容2" width="400">
  <figcaption>图10：脚本和卡刷包必备格式文件夹不用管</figcaption>   
</figure>

***

回到dna  
电脑端  
我们先输入9进入其它功能 输入2去除vbmeta验证 如果你早已去除那么就不需要管这步了

<figure style="text-align: center;">
  <img src="/img/PC-去除vbmeta验证.jpg" alt="PC-去除vbmeta验证" width="400">
  <figcaption>图11：PC-去除vbmeta验证</figcaption>   
</figure>

接下来回到上级输入2合成img将vendor合成.img格式

<figure style="text-align: center;">
  <img src="/img/PC-合成img.jpg" alt="PC-合成img" width="400">
  <figcaption>图12：PC-合成img</figcaption>   
</figure>

如果你闪退了 那就把工程文件夹中的config给删了重新搞一遍

***

手机端  
选择合成img-dat-br  
选择vendor  
打包格式选择线刷格式  
打开最下面的开关打包为erofs

<figure style="text-align: center;">
  <img src="/img/手机端合成img.jpg" alt="手机端合成img" width="400">
  <figcaption>图13：手机端合成img</figcaption>   
</figure>

其它的不用管直接确定  
合成好的文件在

<figure style="text-align: center;">
  <img src="/img/手机输出路径.jpg" alt="手机输出路径" width="400">
  <figcaption>图14：/sdcard/DNA/NA_k60pro/out/</figcaption>   
</figure>

这个文件夹中

***

接下来将手机进入fastboot模式  
输入以下命令  
`fastboot reboot fastboot` （进入fastbootd模式不然刷不了动态分区中的vendor分区）

进入后  
`fastboot flash vendor 文件路径` （刷入vendor）  
`fastboot flash vbmeta 文件路径` （刷入vbmeta）  
然后你就大功告成啦🤓👆  
如果你是手机端打包的没去验证 那么你要把刷入vbmeta的那个命令改为  
`fastboot --disable-verity --disable-verification flash vbmeta 文件路径`   
这样我们就大功告成辣🥰🥰🥰  
让我们重启来看看生效没

<figure style="text-align: center;">
  <img src="/img/驱动版本查询.jpg" alt="驱动版本查询" width="400">
  <figcaption>图15：看到驱动版本已经变0744.16了</figcaption>   
</figure>

小跑个分

<figure style="text-align: center;">
  <img src="/img/跑分前.jpg" alt="跑分前" width="400">
  <figcaption>图16：刷之前</figcaption>   
</figure>

<figure style="text-align: center;">
  <img src="/img/刷之后.jpg" alt="刷之后" width="400">
  <figcaption>图17：刷之后</figcaption>   
</figure>

大概是我的gpu体质不够好吧，我看有些人提升挺大的😂  
相关工具到时候我会发在评论区  
第一次写图文 写的乱七八糟请大家见谅

捏妈妈的手打的累死了😫

***

相关文件

电脑端  
https://www.lanzouw.com/iCCNG1pmcryh  
密码:bb8p

手机端  
https://www.lanzouw.com/iT31w1qlszmj  
密码:fe0m

8gen2 gpu驱动https://www.lanzouw.com/iFAJx1pmdgha  
投币领取哦