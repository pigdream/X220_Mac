*This is a guide record about hack Mac installation, in case of re-installation.*

# X220黑苹果2k屏开启HiDPI-Windows双系统

**Author**: *Vincent* <u>Zhou</u>

## **重要：**

**<font color=red>换了2k屏后，安装完成后，不要运行驱动脚本全装驱动，会黑屏，使用dp线才行，不运行驱动脚本正常。</font>**

####  <font color=red face="微软雅黑"> 间歇性抽风或配置错误，黑屏 </font>

1. 用kextwizard重新安装驱动：

2. /Volumes/EFI/EFI删除APPLE文件夹

3. **重装发现不用装驱动，缺少什么驱动再单独装，运行驱动脚本全装驱动的话黑屏，硬盘区的EFI安装时也清空过的。结果安装完只修改重装了蓝牙的驱动  一切正常。hdpi只能开到1280X720,往上的话有出现黑屏。下次重装再完整试试。但是usb3.0插卡的地方发热，没有注意过是否是以前就发热，装个usb驱动试试？不全装驱动驱动后亮度，声音调节都正常（后面再装一次也不正常了，安装驱动的缘故？）。但是温度好像要比以前高，usb的缘故？还是以前就这么高？**

4. **记住安装系统时**断网**，修改时间，否则时间修改了，网络会自动调整为现在时间。**

   

5. istat menus要显示cpu温度等，需要单独增加sensor，利用HWSensors里的sensor安装。

6. 要解决Chrome中的屏幕闪烁问题，请打开Chrome浏览器，然后点击自定义并控制Chrome浏览器。 这只不过是浏览器页面最右侧可见的三个垂直点。

   现在，向下滚动到“设置”。 现在转到高级设置，然后转到系统，现在停用“可用时使用硬件加速”。

   在此之后，重新启动Chrome。 关闭“使用硬件加速时可用”选项后，检查Chrome中的屏幕闪烁问题是否已修复。------还是不行。

7. qv2ray，用iterm2 的profile功能设置远程ssh和带代理的终端模板  命令 ssh：ssh -p 26616 adam@65.49.215.236

   proxy: send text at start export https_proxy="http://127.0.0.1:8889";export http_proxy="http://127.0.0.1:8889"

    

   USB 3.0插卡可用

   GMYLE BC618T 54mm 2 Port USB 3.0 ExpressCard Adapter

    

   has been reported to work correctly in High Sierra on the X220 by taking the following steps:

   1. Rename *AppleUSBXHCIPCI.kext* located in */System/Library/Extensions/IOUSBHostFamily.kext/Contents/PlugIns* to *AppleUSBXHCIPCI.kext.bak*
   2. Download and install *[GenericUSBXHCI.kext](https://bitbucket.org/RehabMan/os-x-generic-usb3/downloads/)* using Kext Utility

   

----

## 1. 系统安装----X220及改过屏的X220

***关键词：*** *X220 MacOS 2K屏 黑苹果  屏幕 驱动  软件  蓝牙 DP线 音频 声卡*

​      *对于改过2K屏的，强烈建议买条DP口转HDMI或VGA口的线，可以用来接电视上或电脑显示器上，磁铁方式不一定管用，我的就是用磁铁没效果，这条线在进入不了系统，安装调试，开启HiDPI等试错等过程中作用巨大，当出错，进不了系统黑屏时这条线可能救回你的系统，简单直接，安装过程也有用，印象中装过几次，好像有时是不需要线就可以的，直接在2k屏上显示，可能跟安装前修改了config.plist有关*

*黑屏或没显示时可以尝试下Fn+F4键，但有<font color=red>**<u>DP线</u>**</font>在最保险*

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39ji7m1wj30wk0jojya.jpg" style="zoom:33%;" />

![](https://tva1.sinaimg.cn/large/008eGmZEly1gp38822wgkj31ha0u0npm.jpg)

![](https://tva1.sinaimg.cn/large/008eGmZEly1gp38730cq8j31hc0u0x6p.jpg)



<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39fakw4lj30wt0u0gvb.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39fakw4lj30wt0u0gvb.jpg" style="zoom:33%;" >



<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39fit17nj30wt0u079p.jpg" style="zoom:33%;" />

***Reference:***

1.  [THINKPAD X220 MACOS HIGH SIERRA 10.13 INSTALLATION GUIDE](http://x220.mcdonnelltech.com)

2. [DUAL BOOT MACOS AND WINDOWS FROM A SINGLE DRIVE ON THE THINKPAD X220](http://x220.mcdonnelltech.com/dual-boot-one-drive/ )
3. *其他，有些链接已经失效*

**前言**

​       电脑X220，2017年找网上换了2K屏，换后屏幕镜像显示，黑苹果不能进入，遂换回原装屏，2K屏一直放在一旁闲置，2018偶然发现***Reference***中第3个链接的参考，通过对比文中下载的Clover中的文件时间，发现修改了config.plist，通过diff命令对比两个config.plist，删减尝试不同部分启动，发现将以前，即***Reference***中英文1、2链接中的hack mac安装教程中的clover中的config.plist中的***\~\~VGA\~\~***描述部分删除就一切正常，**2K屏黑苹果正常**。

​       删除代码路径：***X220 macOS 10.13 Utility and Kext pack / EFI / CLOVER/ config.plist***,以下代码在config.plist中删除，如果系统已安装，在硬盘的***EFI**\*分区的***EFI / CLOVER/ config.plist**\*里删除修改。以下代码完全删除。

```xml
        <dict>
                <key>Comment</key>
                <string>Replace 4th port with VGA</string>
                <key>Find</key>
                <data>
                AQIEABAHAAAQBwAABQMAAAIAAAAwAAAAAgUAAAAEAAAH
                AAAAAwQAAAAEAAAJAAAABAYAAAAEAAAJAAAA
                </data>
                <key>Name</key>
                <string>AppleIntelSNBGraphicsFB</string>
                <key>Replace</key>
                <data>
                AQIEABITAAASEwAABQMAAAIAAAAwAAAAAgUAAAAEAAAH
                AAAAAwQAAAAEAAAJAAAABgIAABAAAAAJAAAA
                </data>
        </dict>
```

***已安装黑苹果的，要解决X220换2K屏黑苹果黑屏问题，有上面这个删除代码和DP线就可以了，进入系统选择镜像显示，可能已经自动为镜像显示了，需要详细操作黑苹果请看下面***

----

<p style="text-align:center;"><font size=6 color=blue><b>苍茫的天涯是我滴爱，绵绵的青山脚下花正开</b></font></p>

----

#### 1). 硬件准备及BIOS设置

##### **（1）移除BIOS白名单**

*以便安装其它硬件，如新的wifi模块，因为下载的BIOS包写入工具在Win 10中直接运行老是报错，所以采用了启动盘写入的方式，Win7 可以试试系统内运行：*

 ***Reference:****[THINKPAD X220 MODIFIED BIOS UPDATE FROM A BOOTABLE USB](http://x220.mcdonnelltech.com/bios/)*

在Windows中下载并安装[ Active@ Boot Disk 9.4 Demo](http://download.lsoft.net/BootDiskDemo9-Setup.exe)

1. 插入U盘，启动Active@ Boot Disk 9.4 Demo ，根据默认的设置制作PE启动盘

2. 下载[modified BIOS](http://www.mcdonnelltech.com/X220_v1.46_Modified_BIOS.zip), 解压放置一份到上面制作的PE启动U盘中

3. 确保PE启动盘插入X220，重启或启动X220，启动时F12选择PE盘引导启动进入PE系统

4. PE系统界面选择：*Start menu \> System \> Command Prompt (Cmd.exe)*打开cmd命令行，从命令行进入U盘中的modified BIOS目录，在cmd中输入*D:*，或*E:*, 回车，看是否有BIOS文件夹，根据各自电脑尝试正确的盘符。*cd BIOS目录*进入，输入*flash.bat*开始写入。完成后重启电脑

5. 重启电脑，启动时按F1，进入BIOS设置：

   \> – Config \> Power \> Power On with AC Attach \> ***Disabled*** 
   \> – Config \> Serial ATA (SATA) \> ***AHCI***
   \> – Security \> Memory protection \> Execution Prevention \> ***Enabled***
   \> – Startup \> UEFI/Legacy Boot \> ***Both***



##### **（2）硬件增配或替换**

1. 根据[参考1](http://x220.mcdonnelltech.com)的硬件推荐**Dell DW1510** – 802.11a/b/g/n 2.4 GHz & 5 GHz (Broadcom），淘宝上买了个BCM94322HM8L  MAC免驱，替换原有无线网卡，拆装过成参考百度.<u>***该网卡在Windows 10中无线WiFi不正常，网络速度很低，Win7 正常，可能因为网卡太老的原因***</u>

2. 淘宝联系X220 2K屏改装换屏，原屏保留

   <img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39fnut5lj30wk0n0jsw.jpg" style="zoom:33%;" />

3. 添置一块8G 内存条，总共10G，因为是集显，建议总共不少于8G

   <img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39frk2hyj30wk0e875u.jpg" style="zoom:33%;" />

4. 添置一块128G SSD，windows 与 mac都装在上面，ide硬盘用来放数据

5. 添置USB3.0 插卡，淘宝

*****

#### 2). 制作安装盘

​    ***前提条件，已有Mac系统，或已安装了个Mac虚拟机，在虚拟机的Mac OS里制作安装盘，在Windows下的制作方式未尝试过，可在网上查找方法，采用TransMac。vmware虚拟机安装mac跟下载的镜像很有关系，以前下过几个镜像，就一个能成功的，因为电脑已经在之前没换屏时黑苹果装过虚拟机mac了，电脑本身也有一个mac系统了，所以并未用过windows下的制作方式***

##### **（1）虚拟机系统安装**

1. Vmware安装虚拟机mac可以参考百度，虚拟机安装镜像下载 [百度网盘](https://pan.baidu.com/s/1cGU-E-H56rxe436ftAuT_w)  *密码: **c6al***，建议可以折腾下Windows下的制作方法，可以百度TransMac参考，或Etcher.

2. 安装虚拟机，安装unlock，否则虚拟机里建虚拟机时，没有Apple MacOs的选项，安装成功后可以选，多试试几个版本unlock，unlock版本一般会跟Vmware的版本相对应。

3. Windows上安装虚拟机安装Mac系统，安装过程中如果出现 ：

> “安装 macOS Sierra”应用程序副本已损坏，不能用来安装 macOS

这时先**断网**，并在安装界面的终端里面使用date命令修改时间，`date 032208102015.20`  按回车键确认03是月,22是日,08是时,10是分,2015是年,20是秒，秒可以不用输入。将时间修改回老时间，比如2015年，网上说在16年以前？可能由于联网安装包里的证书过期了，所以**断网并修改时间**安装。一定要**断网**！

##### （2）启动盘制作

1. 下载安装镜像10.13.6，10.14采用新的架构不兼容X220显示配置，懒得折腾，网上有折腾教程

   下载 [Install macOS High Sierra app][11][百度网盘](https://pan.baidu.com/s/1cGU-E-H56rxe436ftAuT_w)  *密码: **c6al***, 并解压放到系统的***应用文件夹***

2. 插入U盘,***应用启动台-其他-磁盘工具***，格式化U盘。***制作U盘，一定要先格式化苹果文件系统，不能直接用FAT32的U盘来运行U盘制作命令，没有格式化的话不会出现EFI分区在U盘上，就不能copy efi文件夹进去。同时注意左边栏左上角的显示选择和左侧的设备选择***

   <img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39n0i72yj31cc0u0q9l.jpg" style="zoom:33%;" />

   

   打开终端，复制输入以下命令：
   
   `sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ High\ Sierra.app --no interaction`

其中命令里的***/Volumes/USB***与格式化U盘时的名称***USB**\*保持一直。***Install\ macOS\ High\ Sierra.app**\*与下载的Mac系统镜像名称保持一致。输入密码，等待写入完成

下载 **ThinkPad X220 macOS 10.13 Utility and Kext Pack** [百度网盘](https://pan.baidu.com/s/1cGU-E-H56rxe436ftAuT_w)  *密码: **c6al***，解压并放入一份拷贝到上面做好的系统安装U盘中。

1. 从解压的**ThinkPad X220 macOS 10.13 Utility and Kext Pack**启动*Clover Configurator* ，点击*Mount EFI*，点击mount **U盘**的的EFI分区，挂在启动盘的EFI分区。退出*Clover Configurator* ，**留意是U盘的EFI分区**

   <img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39drwg8bj31hc0u01kx.jpg" style="zoom:33%;" />

2. 从解压的**ThinkPad X220 macOS 10.13 Utility and Kext Pack**复制整个EFI文件夹到U盘的EFI分区，如果EFI分区中已有EFI文件夹，删除已有的后再复制。



***重要：***

- 如果没有换过2k屏幕，使用电脑原来的屏幕，直接即可安装，不用修改config.plist
- 如果换过2k屏幕，此时2k屏幕是以镜像扩展显示器在工作的，需要修改config.plist，去掉***”Replace 4th port with VGA“***的那段代码，如前言中说明那样，删除clover中的config.plist中的**\~\~VGA\~\~**描述部分。修改完后再copy到U盘中。

另外可能需要修改的是蓝牙驱动里的VID和PID，最好也在安装前修改好，修改好后copy到U盘，如果安装时没修改，安装后也可修改。具体修改内容参考下面系统安装部分的蓝牙问题。

***Windows制作：TransMac，未尝试过，自行百度，windows制作后，同样copy一份Utility and Kext Pack进U盘***

*在Windows中修改建议用Sublime或VScode修改config.plist和蓝牙kext中的VID等，好像windows的文本编辑器保存会自动加上BOM，没试过，保险点*

***百度网盘上的里面的文件已经根据自己电脑上的信息修改过VGA和蓝牙ID。***

#### 3). 系统安装

重启电脑，BIOS设置U盘启动或F12选择U盘启动，U盘启动安装。

在Clover启动菜单选择*Boot OS X Install from Install macOS High Sierra*，选择磁盘工具，在磁盘工具中左上角下拉框中先选择***显示所有设备***，选中要安装的磁盘SSD。

##### **（1）格式化分区**

***重要：***

- 如果单块SSD就只安装Mac OS一个系统，直接选中磁盘，格式化：name 自己定，比如**Mac**，格式--扩展日志，分区--GUID

- 如果要在单块SSD上安装双系统，比如Mac OS+Windows，选中**硬盘**，点击分区，分为两个区，分区大小自己定，建议给苹果留多点，其中mac分区如上面格式化，另外Windows分区直接保留dos格式就行，或者不格式化，后面安装Windows过程中会再分区格式化。

- 安装过程中对硬盘格式化，再分区，一定要选左上角的查看**所有设备**再来格式化分区。

  
  
  <img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39chwf47j319c0u0h2q.jpg" style="zoom:33%;" />
  
  
  
  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp37d6tu7lj31400u0b2f.jpg" style="zoom:33%;" />





<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39m8tibzj30ne0c0taz.jpg" style="zoom:33%;" />



分区格式化完成后退出磁盘工具。



##### **（2）安装系统**

***改过2k屏的，如果安装过程黑屏了，或只有桌面显示，没有菜单（只显示扩展显示，因为2k屏幕改装是扩展镜像显示），可以用上面提到的DP线连接电脑跟电视或电脑显示器，印象中装过几次，好像有时是不需要线就可以的，可以尝试下Fn+F4键，但有DP线在最保险，改过config.plist的不用线也可以***

1. 选中安装Mac OS进行下一步，选中刚格式化的mac分区，进行安装，过程中可能会重启。

   **安装过程中如果出现 ：**

> “安装 macOS Sierra”应用程序副本已损坏，不能用来安装 macOS

这时先**断网**，并在安装界面的终端里面使用date命令修改时间，`date 032208102015.20`  按回车键确认03是月,22是日,08是时,10是分,2015是年,20是秒，秒可以不用输入。将时间修改回老时间，比如2015年，网上说在16年以前？可能由于联网安装包里的证书过期了，所以**断网并修改时间**安装。一定要**断网**！

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp37617dusj31400u0b2d.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp3775n3t0j31400u0npj.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp377ti2loj31400u0qvd.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39xg90s3j31400u0b2f.jpg" style="zoom:33%;" />



2. ***继续保持U盘插在电脑上，***因为此时的Clover引导是在U盘的EFI区的，硬盘上是没引导的，拔了就没引导了，重启时保证电脑还是从U盘启动（设置BIOS启动项或BIOS启动时F12选择），这样才能进入U盘的Clover引导菜单选择，此时重启后，菜单中应该多了一个图标选项：*Boot macOS Install from Mac**(你的硬盘分区名称)***，安装重启过程中始终选择这个选项继续安装。

3. 直到安装完成，此时Clover菜单应该多出另一个图标选项：***Boot macOS from Mac(你的硬盘分区名称)***，选择进入系统，进行初始化设置，直到此时还不能拔出U盘，还需要用到U盘的EFI来引导启动。

4. 进入系统后，打开终端，输入`sudo spctl --master-disable`允许任何源的app运行。

5. 将U盘中的[ThinkPad X220 macOS 10.13 Utility and Kext Pack][15] copy一份到电脑硬盘上，使用 *Clover Configurator*将**安装硬盘**的EFI分区挂载，挂载方法跟上面挂载U盘上的一样，注意不要选择挂载U盘的，而是挂载硬盘的，留意盘符描述文字的不同，此时方达里面可以看到EFI分区，进入，然后将[ThinkPad X220 macOS 10.13 Utility and Kext Pack][16]里的EFI文件夹copy一份到硬盘的EFI分区，如EFI分区已有EFI文件夹，删除后再复制。

***这步以后，就不用再靠U盘来引导启动了，直接硬盘可以Clover引导系统启动，可以拔出U盘了。***

----

#### 4). 驱动安装及安装后功能开启

##### （1）驱动安装

后面安装后不运行安装启动脚本好像还正常一些，蓝牙，屏幕都没事，以后安转不运行这个脚本，直接补上音频驱动即可。正常安装就可以，其实不用运行安装驱动的脚本，结果运行了脚本后重启，屏幕就出问题，只能接电视。不运行一切正常，音频不行。

~~打开*ThinkPad X220 macOS 10.13 Utility and Kext Pack \> EFI \> CLOVER \> kexts* ，运行脚本*\_kext-install.command*，直接右键，选择终端运行，输入密码，等待完成驱动安装，重启系统。。~~

 App Store上安装可用的系统更新，安装下载时可以完成其它部分。



##### （2）改善的电源管理

***新安装了下，好像这个命令运行不了了，难道不用了？直接运行之前下载的脚本也出错***，要翻墙才行，github被墙。利用ssdtPRGen.sh-Beta解压到~/Library中，改名ssdtPRGen，进入文件夹使用里面的脚本生产。

但好像本来就正常变频的，不需要弄了？

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp37m4z579j30u00x1k13.jpg" style="zoom:33%;" />

~~打开终端，copy以下命令输入：~~  要翻墙才行，github被墙。配置iterm profile翻墙

```shell
curl -o ~/ssdtPRGen.sh https://raw.githubusercontent.com/Piker-Alpha/ssdtPRGen.sh/master/ssdtPRGen.sh
chmod +x ~/ssdtPRGen.sh
./ssdtPRGen.sh
```

~~过程中提示是否copying and opening时输入**“N”**。一个针对这台电脑的 *SSDT.aml* 文件现在应该产生在 ***/Users/”你的用户名“/Library/ssdtPRGen***文件夹里了。~~

~~用 *Clover Configurator*将硬盘的EFI分区挂载，将上面生产的*SSDT.aml* 复制一份到*/Volumes/EFI/EFI/CLOVER/ACPI/patched/*目录下面，下次重启后即可。~~

~~先挂载EFI分区后输入：~~

~~`cp /Users/adam/Library/ssdtPRGen/SSDT.aml   /Volumes/EFI/EFI/CLOVER/ACPI/patched`~~



##### （3）开启HiDPI

建议只有2k屏开启，原装屏分辨率本来就低，开启后可视面积太少，没什么实用意义，HiDPI的本质就是4个像素充当一个像素来提高显示清晰度，所以2k能开启原生的1280X720P-HiDPI，正好是1280X2X720X2=2560X1440.

开启HiDPI----在终端运行下面的命令，这样开启后即可支撑2k屏能支撑的原生1280X720P-HiDPI

```shell
sudo defaults write /Library/Preferences/com.Apple.windowserver DisplayResolutionEnabled -bool YES

sudo defaults delete /Library/Preferences/com.apple.windowserver DisplayResolutionDisabled
```

运行后可进系统偏好设置--显示设置--缩放里面选择1280X720P-HiDPI，是不是字体什么的清晰很多了

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp381vzj5dj31hl0u0e87.jpg" style="zoom:33%;" />

1280X720P-HiDPI应该是最清晰的，但是字体有点偏大，可视面积有点少，所以可以选个折中的伪原生的1536X864 HiDPI，来支持更大的可视面积，但是清晰度会比1280X720P-HiDPI有所降低，但清晰度比没开HiDPI的1536X864 ，1600X900等要清晰。



##### （4）增加分辨率及HiDPI

* **增加1536X864，1920X1080分辨率**

```shell
ioreg -lw0 | grep IODisplayPrefsKey
```

会显示类似如下内容：

> "IODisplayPrefsKey" = "IOService:/AppleACPIPlatformExpert/PCI0@0/AppleACPIPCI/IGPU@2/AppleIntelFramebuffer@3/display0/AppleDisplay-**4d10**\-**142f**\"

记住***4d10***---**142f**这两个位置对应的**你自己电脑的16进制数字**，***以下命令都替换成自己电脑的数字再执行***

 其中**VendorID  4d10，ProductID  142f，**在百度找16进制转10进制网页，转换记录对应的10进制数。

```shell
sudo mkdir /System/Library/Displays/Contents/Resources/Overrides/DisplayVendorID-4d10

sudo vim /System/Library/Displays/Contents/Resources/Overrides/DisplayVendorID-4d10/DisplayProductID-142f
```

复制输入文件内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
        <key>DisplayProductName</key>
        <string>Lenovo x220 Display</string>
        <key>DisplayVendorID</key>
        <integer>19728</integer>
        <key>DisplayProductID</key>
        <integer>5167</integer>
        <key>scale-resolutions</key>
        <array>
                <data>AAAGAAAAA2A=</data>
                <data>AAAHgAAABDg=</data>
        </array>
</dict> 
</plist>
```

其中12516，54018用自己电脑的VendorID 和ProductID的16进制数对应的10进制数替换，保存退出

重启后应该就能在系统偏好设置--显示设置--缩放中看到1536 x 864 和 1920 x 1080的分辨率选择了。



+ **增加开启1536X864HiDPI**

  **新安装了后开启了这个分辨率的hidpi，黑屏，需要接线才行，不稳定，不要用**
  
  <img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp385gkrg7j316o0o1npe.jpg" style="zoom:33%;" />

~~增加1536X864 HiDPI支持，1600X900HiDPI开启后会有闪屏等不稳定出现，1536不稳定较少，1280最稳定但可视面积没有之前两个多，如果1600开启系统花屏等不能操作，重启，在clover界面按空格，选中security mode安全模式启动系统，调低分辨率，重启系统就好了。如黑屏等不能进如系统，可链接DP线接电视。~~

~~下载安装**SwitchResX 3.7 破解版**~~

~~在左侧点**Lenovo x220 Display**，与上面DisplayProductID-142文件中的DisplayProductName的名称一致。有一个有**Custom Resolutions**标签卡，在下面定义一个**3072×1728**的分辨率-（1536X2） X （864X2)，两倍关系，也可以把1600X900和1920X1080的两倍都增加上，但是能开启的实测1600X900HiDPI最高，还有些问题，最好降为1536X864HiDPI使用，偶尔有横线闪出，不影响使用，最稳定还是1280X720HiDPI，或不开HiDPI的分辨率。~~

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp38wt5qd2j314v0u0q8u.jpg" style="zoom:33%;" />



<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp38xnbdjyj314v0u0n3h.jpg" style="zoom:33%;" />

~~保存，重启，重新打开SwitchResX，就可以在现有分辨率里面找到1536×864 HiDPI，点最前面的小圆点启用它，好了，也可在里面选择其他的分辨率或其他HiDPI。~~

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp38ymry0lj314v0u0akg.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp38zwl76nj31280u0dms.jpg" style="zoom:33%;" />![](https://tva1.sinaimg.cn/large/008eGmZEgy1gp39yx89ihj31280u00zp.jpg)

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39zgu0q1j31280u00zp.jpg" style="zoom:33%;" />

~~还可以下载安装[RDM]()，用来选择分辨率的小工具~~

~~*DisplayProductID-142f文件在SwitchResX安装设置后会有变化，增加的scaled resolution会体现在该文件中，大牛也可以直接便捷该文件，使用RDM来选择使用*~~

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp38zma5fbj316o0o1npe.jpg" style="zoom:33%;" />

##### （5）音频驱动

先用kext wizard  把AppleHDA_20672.kext （跟 EFI驱动文件夹里的声卡驱动AppleHDA.kext ？） 都装到 S\L\E  目录下。 通过直接拉进kext wizard安装。

运行终端，先运行sudo -s 输入密码 免得一条一条的执行：

```
cd /System/Library/Extensions/AppleHDA_20672.kext/Contents/MacOS
sudo rm AppleHDA
sudo ln -s /System/Library/Extensions/AppleHDA.kext/Contents/MacOS/AppleHDA
sudo touch /System/Library/Extensions
```

**用kext wizard 修复权限&重建缓存 !!!**

**重启系统!!!**



##### （6）NTFS分区读写

**下面的方法不稳定，还是装个软件好些Tuxera？好像也写不了啊。**最好还是设立一个exFAT分区，Windows和Mac都正常读写，支持4G大文件。

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39ftniitj30wk0twgpl.jpg" style="zoom:33%;" />

~~Mac系统默认只读NTFS分区，读写FAT32分区，所以FAT32分区不用做任何操作，需开启读写NTFS分区，可用软件工具来实现，也可通过命令来实现，***建议重要数据分区和Windows系统安装分区不要开启读写，保留只读即可***，如果开启读写后，使用过程中突然不能读写或都不能读了，进入Window系统，在系统启动时如果提示硬盘分区检测修复，确认检测修复后即可恢复正常：~~

假如Temp分区为NTFS分区

```sh
diskutil info /Volumes/Temp | grep UUID
   Volume UUID:              2FE8D126-B66B-4A5E-8EAD-0BFCD70CD699
   Disk / Partition UUID:    53C1BA71-6834-4164-B58A-17D3AF2
echo "UUID=2FE8D126-B66B-4A5E-8EAD-0BFCD70CD699 none ntfs rw,auto,nobrowse" | sudo tee -a /etc/fstab
```

~~同理，移动硬盘等移动设备也可如此操作，**移动设备这样操作后，插上后不会在桌面显示图标了**，需要自行进入/Volumes才能看到盘符，可进入/Volumes后将对应盘符拉入左边访达的收藏里面，以后插入后直接鼠标点入即可。移动硬盘示例：~~

```sh
diskutil info /Volumes/Seagate\ Backup\ Plus\ Drive | grep UUID
echo "UUID=4F1B97F4-CD31-485C-AC8D-FCB1D95F36E8 none ntfs rw,aut,nobrowse" | sudo tee -a /etc/fstab
```

~~弹出硬盘时：`umount /Volumes/Seagate\ Backup\ Plus\ Drive`或直接点访达图标的弹出~~



##### （7）蓝牙问题

系统安装完，点击屏幕左上角苹果图标，关于本机-系统报告，查看各个硬件情况，点击蓝牙发现内容没有设备，如已经正常，则不用处理。通过修改蓝牙驱动解决，其实可以在安装过程中修改ThinkPad X220 macOS 10.13 Utility and Kext Pack中的驱动文件。

在Windows中查看蓝牙的VID和PID，具体方法如下：**系统window菜单，搜索-设备管理器-选种蓝牙设备-右键属性-详细信息-下拉列表里选种硬件ID**，里面列出了VID和PID16进制数字。百度16进制转10进制网页，记录VID和PID的16进制和对应的10进制数字。

***修改蓝牙驱动里的VID，PID：***

**制作安装U盘时修改**

修改文件路径:

`X220 macOS 10.13 Utility and Kext pack 10.28.2018 \ EFI \ CLOVER \ kexts \ Other \BlueTooth_Injector.kext \Contents\ Info.plist`

在Windows中直接进入文件夹一样进入即可，Mac里面到达BlueTooth\_Injector.kext 时，右键查看包内容。

在Windows中修改建议用Sublime修改，好像windows的文本编辑器保存会自动加上BOM，没试过，保险点

```xml
    <key>IOKitPersonalities</key>
    <dict>
        <key>PID 8575 0x217F VID 2652 0xA5C</key>
        <dict>
            <key>CFBundleIdentifier</key>                   <string>com.apple.iokit.BroadcomBluetoothHostControllerUSBTransport</string>
            <key>IOClass</key>
            <string>BroadcomBluetoothHostControllerUSBTransport</string>
            <key>IOProviderClass</key>
            <string>IOUSBHostDevice</string>
            <key>idProduct</key>
            <integer>8575</integer>
            <key>idVendor</key>
            <integer>2652</integer>
        </dict>
    </dict>
</dict>
</plist>
```

把其中的**PID 8575 0x217F VID 2652 0xA5C**与下面的**idProduct** **8575**，**idVendor** **2652**分别替换成上面查看的自己电脑的VID和PID的16进制和10进制数，保存。

修改后整个X220 macOS 10.13 Utility and Kext pack 10.28.2018复制进安装U盘，再启动安装。

**系统安装后修改：**

修改文件路径:

挂载磁盘EFI分区，进入EFI文件夹，`EFI \ CLOVER \ kexts \ Other \BlueTooth_Injector.kext \Contents\ Info.plist`修改，修改完后，用kext utility工具重新装一下驱动，将修改完的BlueTooth\_Injector.kext拉如kext utility，等待完成即可。



##### （8）亮度调节

**不装驱动亮度调节正常。再次证明了不要运行驱动暗转脚本**

不要删除/Library/ExtensionsAppleBacklightInjector.kext来调节亮度（参[考英文参考]()的方法），试过没用，还不能进系统了，接了DP线才能显示，电视与电脑同时显示。通过下载安装[Brightness slider]()来调节亮度，发现已经最亮了，可能磨砂屏的关系，所以其实不用管亮度调节了。



##### （9）USB 3.0插卡

```shell
cd /System/Library/Extensions/IOUSBHostFamily.kext/Contents/PlugIns
sudo mv AppleUSBXHCIPCI.kext bak.AppleUSBXHCIPCI.kext
```

下载 [*GenericUSBXHCI.kext*][21] 并用 ***Kext Utility***安装,在*ThinkPad X220 macOS 10.13 Utility and Kext Pack*中有此工具，打开工具，将下载的驱动拖入工具界面等待安装完成。好像依然是2.0，但是至少能用了，之前在windows下能用的3.0插卡，换mac系统就用不了。



##### （10）其他与SSD Trim

其他Night Shift（与macOS High Sierra Security Update 2018-002 10.13.6 (build 17G3025)及最新的一个更新不兼容，所以也没搞了），如果有兴趣的，安装完系统后，不要升级这个更新，可以启用。

```shell
xcode-select --install

cd /tmp; curl -s -o NightPatch.zip https://codeload.github.com/pookjw/NightPatch/zip/master; unzip -o -qq NightPatch.zip; cd NightPatch-master; chmod +x NightPatch.sh; ./NightPatch.sh
```

这个自己没试过

如果还想折腾其他的比如**Touchpad, TrackPoint and Tablet Input**d等等的，参考[英文参考1]()里面的**Notes and Suggestions**



**硬盘：SSD trim开启**

`sudo trimforce enable`



#### 5). Windows系统安装及双系统引导

##### （1）安装及引导调整

下载Windows系统镜像，下载的win10，win7用EFI安装。下载rufus，插入U盘制作启动磁盘。UEFI。正常安装安装系统，选择之前留下的另外一块分区安装，安装完成后应该直接进入Window系统了，没有Mac启动菜单了。

启动时进入BIOS设置-启动项-调整启动项的顺序，把Windows Boot Manager启动项和Mac OS X启动项移后，**移到Mac OS和系统安装硬盘的后面**，如下面的**ATA HDD2 LITEON**项后面，保存重新启动，Clover菜单又出来了，同时又有Windows的启动菜单在里面了。

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39tmjwmej31ca0u0agw.jpg" style="zoom:33%;" />

双系统安装完成。

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp394a7snlj31400u0qva.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEly1gp393xjhthj31400u0u13.jpg" style="zoom:33%;" />

<img src="https://tva1.sinaimg.cn/large/008eGmZEgy1gp39q2ygyfj31400u0npi.jpg" style="zoom:33%;" />

##### （2）双系统造成的时间错误

Mac和WIN双系统时间不对怎么办呢?有很多人装了Mac和Windows的双系统之后会发现进入苹果后，再重启进Windows就会出现时间不同步的问题，Windows下的时间比Mac下晚8小时，出现这个问题的主要原因是因为mac和win基准识别时间不同，那么这个问题该怎么解决呢?为大家带来一个有效的解决办法。

  步骤：打开C盘>Windows>System32，找到cmd.exe，右键以管理员的身份运行。 （或者使用WIN+R组合键后输入CMD）然后输入以下命令：
`Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1`
回车搞定！重启试试！

  命令的原理其实就是通过修改注册表让windows识别硬件时间为UTC-0而不是现在的UTC+8
也可以在注册表（WIN+R输入regedit）里直接操作HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\中添加一项数据类型为REG_DWORD,名称为RealTimeIsUniversal,值设为1即可。





#### 6). 其他问题

Wifi 突然经常断，和不能打开，什么问题？







----

<p style="text-align:center;"><font size=6 color=blue><b>什么样的节奏是最呀最摇摆，什么样的歌声才是最开怀</b></font></p>

----

## 2. Software Install

允许运行下载软件：sudo spctl --master-disable

### 1). 软件安装

	1. 下载软件包，直接解压拖进应用文件夹
	2. 双击软件包，把app图标拖进应用快捷方式
	3. 命令行安装，brew install

### 2). Brew install  需要iterm profile翻墙


```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

```shell
brew install wget
brew install iina
brew install bat
brew install iterm
```



### 3). oh my zsh 和插件    需要iterm profile翻墙

```shell
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

插件：

```shell
brew install zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

#编辑.zshrc
vim .zshrc

#将.zshrc里面的plugins段增加插件为：
 plugins=(
   git sublime web-search wd z zsh-autosuggestions 
 )

#主题字段修改为：
ZSH_THEME="random"

#文件末尾增加：
source /usr/local/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```



### 5). 其他软件

安装Go2Shell, TrashMe, Paste,Alfred,microsoft office,Typora,iStat Menu,百度网盘破解，ieaseMusic，Canary mail,音乐等软件。

**Go2Shell**：在文件夹中打开终端，安装时要调整方达设置

先安装，然后右键方达上方工具条自定义，将application里的go2shell拉入工具条上方，然后再点击，添加到方达，再删除之前拉进去的那个。





**iStat Menu**：系统状态信息实时显示,记住安装cup插件HWSensors才能监控温度

**Bartender**: 隐藏右上角多余的显示图标，避免拥挤，点一下可展开，好用，尤其是在hidip下

**QuickRes**：快捷切换分辨率显示，在720hidpi和1440全2k间点一下快速切换，相当方便

**Thor**：自己定制程序打开的快捷键，方便

**CheetSheet**：快捷键提示软件

**腾讯柠檬**：清理，卸载软件









******












