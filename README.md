
目录
=================

* [1\.全景相机推拉流](#1全景相机推拉流)
* [2\. VONR电话](#2-vonr电话)
* [3\.AR](#3ar)

# 1.Amari基站
包含核心网和基站（一体化）
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/icon.jpg" width="200"></div>

## 1.1 基站核心网启动
</br>不打VONR电话无需配置```/home/sdr/2021-03-25/ltemme-linux-2021-03-25/config/ims.cfg```
### 1.1.1 Amari基站连Amari核心网
(1) 修改基站配置文件```/home/sdr/2021-03-25/lteenb-linux-2021-03-25/config/v3best-gnb-sa.cfg```中:
- ```amf_addr：核心网IP```
- ```gtp_addr：基站IP```
</br>Amari网口闲置时两个地址都设成本地```127.0.1.X```。
</br>另一配置方法是：在amari后接一根网线，基于物理网卡起一个虚拟IP，分别作为```amf_addr```和```gtp_addr```。

(2) 修改核心网配置文件```/home/sdr/2021-03-25/ltemme-linux-2021-03-25/config/mme-ims.cfg```中:
- ```gtp_addr：和基站配置文件中的amf_addr相同```


### 1.1.2 Amari基站连其他核心网
</br>Amari只开基站，用网线将它和核心网主机连起来，两个设成同一网段的静态IP，假设为```192.168.1.210```和```192.168.1.211```（子网掩码24位）
- ```amf_addr:核心网主机IP  192.168.1.211```
- ```gtp_addr:基站IP 192.168.1.210```

</br>核心网
- ```gtp_addr: 核心网所在主机IP 192.168.1.211```








# 1.全景相机推拉流
全景相机网线连```CPE DHCP```，头显也连```CPE```（只要网络连通在不在同一局域网都可，不在同一子网时拉流地址为CPE的WAN IP）</br>

（1）推流</br>
开全景相机第三个按钮（横向），reday，向下模式选择 “4k 30Hz” ,不要选带3D的，会出现两个画面，选择直到出现计时画面为止。
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017623-48db9cd4-3932-483e-9b10-430aa0e15b69.png" width="400"></div>


也可在电脑上用```insta pro```软件推流。

（2）修改配置文件</br>
头显数据线连电脑，电脑连CPE WIFI，修改配置文件：添加一个应用，改name uri id即可，另存为然后复制进去
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017907-e9808156-752c-426d-8929-78fc6412baba.png" width="400"></div>

<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017973-722e5a6e-a8b4-4f00-a4de-ddf4fe3a4755.png" width="400"></div>

（3）头显拉流</br>
打开头显  应用  点开对应应用名称（图中为星地）

（4）手机、电脑拉流</br>
连CPE，使用```Insta360```在线观看，输入配置文件中的地址。或者```potplayer、vlc```拉流。

# 2. VONR电话

- 实验室3个华为手机中有2个```VONR```功能正常（背后标了VONR）,首先要保证开启了```IMS```服务，一般都开了，详见英文```pdf```文档</br>
- 手机连不上基站检查```apn```(和核心网里的要一致，大基站配置的```internet```)，5G模式选择：```SA+NSA``` 飞行模式
- 连上不显示HD或者经常断：```ims.cfg```文件配置不正确

(1) IMS服务配置
</br>除正常修改基站配置文件```/home/sdr/2021-03-25/lteenb-linux-2021-03-25/config/v3best-gnb-sa.cfg```和核心网配置文件```/home/sdr/2021-03-25/ltemme-linux-2021-03-25/config/mme-ims.cfg```外，还要配置IMS服务，```/home/sdr/2021-03-25/ltemme-linux-2021-03-25/config/ims.cfg```中修改：
- ```cx_server_addr：与基站配置文件中amf_addr相同```
- ```sctp_addr、cx_bind_addr：与基站配置文件中gtp_addr相同```

(2) 手机开启```VONR```功能</br>
开发者选项->```VONR```高清通话，开启后信号处会显示```HD```（没有```HD```则是```IMS```配置错误）
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022702-53f682ab-96a8-4691-a769-60c5f975e1b8.png" width="400"></div>

(3)	手机号码</br>
在核心网数据库: ```/ltemme-linux-2021-03-25/config/ue_db-ims.cfg```文件中（tel或imsi都行），核心网```mme```界面输命令```ue```可看到```imsi```。
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022893-6da5b948-98d0-4079-8c1f-b22033cc28d0.png" width="400"></div>


 </br>
(4)直接用拨号软件打电话
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232023098-111d04a4-de8b-40eb-9c8e-220fe7e1b099.png" width="400"></div>

注：烧卡时MSISDN为电话号码（要和核心网数据库对应）
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/VONR.png" width="800"></div>

# 3.AR

**注意：AR和ALVR不能同时开，否则会连不上。**</br>
```unreal engine```会自动加载```steamvr，steamvr```会自动唤醒```ALVR```，需要在```steamvr```中：
设置->管理加载项->禁用ALVR

AR服务器连接AR头显：</br>
AR头显和服务器主机连同一子网（CPE），主机ping不通头显是正常的，ping要支持icmp协议（头显估计不能）
</br>
法1：</br>
打开```unreal```虚幻引擎,编辑->项目设置->搜索"holo",在AR头显中运行```HoloLens graphic Remoting```，将显示的IP地址填入3，然后点连接，显示```connected```为连接成功 。若不成功一般是没有在steamvr加载项中禁用ALVR。连上之后点运行即可在头显中开始游戏。
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/AR2.png" width="800"></div>

</br>
法2：</br>
运行登月项目：进入编译后的文件夹，cmd运行可执行文件连接AR头显（不用打开unreal）:

```
MissionAR.exe -vr -HoloLensRemoting=192.168.8.114(AR头显IP)
```
 <div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/AR.png" width="800"></div>


[官网指南](https://docs.microsoft.com/en-us/windows/mixed-reality/develop/unreal/unreal-streaming?tabs=wmr)

