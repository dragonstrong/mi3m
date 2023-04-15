
目录
=================

* [1\.全景相机推拉流](#1全景相机推拉流)
* [2\. VONR电话](#2-vonr电话)
* [3\.AR](#3ar)

# 1.Amari基站
一体化基站含核心网和基站
## 1.1 基站核心网启动
</br>不涉及打VONR电话只用改基站配置文件和核心网配置文件
### 1.1.1 Amari基站连Amari核心网
基站配置文件：
- amf_addr：核心网IP
- gtp_addr:基站IP
两个地址都可以设成本地127.0.1.X，也可以在基站后面接一根网线，基于物理网卡起一个虚拟网卡IP，分别作为amf_addr和gtp_addr。
</br>核心网配置文件
- gtp_addr：和基站配置文件中的amf_addr相同


### 1.1.2 Amari基站连其他核心网
</br>Amari只开基站，用网线将它和核心网主机连起来，两个设成同一网段的静态IP，假设为192.168.1.210和192.168.1.211（子网掩码24位）
- amf_addr:核心网主机IP  192.168.1.211
- gtp_addr:基站IP 192.168.1.210

</br>核心网
- gtp_addr: 设成核心网所在主机IP 192.168.1.211
开启核心网







# 1.全景相机推拉流
全景相机网线连CPE DHCP，头显也连CPE（只要网络连通在不在同一局域网都可，不在同一子网时拉流地址为CPE的WAN IP）</br>

（1）推流</br>
开全景相机第三个按钮（横向），reday，向下模式选择 “4k 30Hz” ,不要选带3D的，会出现两个画面，选择直到出现计时画面为止。
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017623-48db9cd4-3932-483e-9b10-430aa0e15b69.png" width="400"></div>


也可在电脑上用insta pro软件推流。

（2）修改配置文件</br>
头显数据线连电脑，电脑连CPE WIFI，修改配置文件：添加一个应用，改name uri id即可，另存为然后复制进去
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017907-e9808156-752c-426d-8929-78fc6412baba.png" width="400"></div>

<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017973-722e5a6e-a8b4-4f00-a4de-ddf4fe3a4755.png" width="400"></div>

（3）头显拉流</br>
打开头显  应用  点开对应应用名称（图中为星地）

（4）手机、电脑拉流</br>
连CPE，打开Insta360Player，在线观看，输入配置文件中的地址

# 2. VONR电话

实验室3个华为手机中有2个有VONR功能,首先要保证开启了IMS服务，一般都开了，详见英文pdf文档</br>
手机连不上基站检查apn(和核心网里的要一致，大基站配置的internet)，5G模式选择：SA+NSA 飞行模式
(1) 手机开启VONR功能</br>
开发者选项->VONR高清通话，开启后信号处会显示HD（没有HD则是IMS配置错误）
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022702-53f682ab-96a8-4691-a769-60c5f975e1b8.png" width="400"></div>

(2)	手机号码</br>
在核心网数据库: /ltemme-linux-2021-03-25/config文件夹下的ue_db-ims.cfg文件中（tel或imsi都行）
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022893-6da5b948-98d0-4079-8c1f-b22033cc28d0.png" width="400"></div>


 </br>
(3)直接用拨号软件打电话
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232023098-111d04a4-de8b-40eb-9c8e-220fe7e1b099.png" width="400"></div>

注：烧卡时MSISDN为电话号码（要和核心网数据库对应）
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/VONR.png" width="800"></div>

# 3.AR

**注意：AR和ALVR不能同时开，否则会连不上。**</br>
unreal engine会自动加载steamvr，steamvr会自动唤醒ALVR，需要在steamvr中：
设置->管理加载项->禁用ALVR

AR服务器连接AR头显：</br>
AR头显和服务器主机连同一子网（CPE），主机ping不通头显是正常的，ping要支持icmp协议（头显估计不能）
</br>
法1：</br>
打开unreal虚幻引擎,编辑->项目设置->搜索"holo",在AR头显中运行HoloLens graphic Remoting，将显示的IP地址填入3，然后点连接，显示connected为连接成功 。若不成功一般是没有在steamvr加载项中禁用ALVR。连上之后点运行即可在头显中开始游戏。
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/AR2.png" width="800"></div>

</br>
法2：</br>
运行登月项目：进入编译后的文件夹，cmd运行可执行文件连接AR头显（不用打开unreal）:

```
MissionAR.exe -vr -HoloLensRemoting=192.168.8.114(AR头显IP)
```
 <div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/AR.png" width="800"></div>


[官网指南](https://docs.microsoft.com/en-us/windows/mixed-reality/develop/unreal/unreal-streaming?tabs=wmr)

