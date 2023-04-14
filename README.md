
# <div align="center">mi3m实验室硬件演示</div>


## 1.全景相机推拉流
全景相机网线连CPE DHCP，头显也连CPE（只要网络连通在不在同一局域网都可，不在同一子网时拉流地址为CPE的WAN IP）</br>

（1）推流</br>
开全景相机第三个按钮（横向），reday，向下模式选择 “4k 30Hz” ,不要选带3D的，会出现两个画面，选择直到出现计时画面为止。
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017623-48db9cd4-3932-483e-9b10-430aa0e15b69.png" width="400"></div>

 
也可在电脑上用insta pro软件推流。

（2）修改配置文件</br>
头显连接数据线连电脑，电脑连CPE WIFI，然后修改配置文件，添加一个应用，改name uri id即可，另存为然后复制进去
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017907-e9808156-752c-426d-8929-78fc6412baba.png" width="400"></div>

<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017973-722e5a6e-a8b4-4f00-a4de-ddf4fe3a4755.png" width="400"></div>

（3）头显拉流</br>
打开头显  应用  点开对应应用名称（图中为星地）

（4）手机、电脑拉流</br>
连CPE，打开Insta360Player，在线观看，输入配置文件中的地址

## 2. VONR电话

实验室3个华为手机中有2个有VONR功能,首先要保证开启了IMS服务，一般都开了，详见英文pdf文档</br>
(1) 手机开启VONR功能</br>
开发者选项->VONR高清通话，开启后信号处会显示HD
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022702-53f682ab-96a8-4691-a769-60c5f975e1b8.png" width="400"></div>

(2)	手机号码</br>
在核心网数据库: /ltemme-linux-2021-03-25/config文件夹下的ue_db-ims.cfg文件中（tel或imsi都行）
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232022893-6da5b948-98d0-4079-8c1f-b22033cc28d0.png" width="400"></div>


 </br>
(3)直接用拨号软件打电话
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232023098-111d04a4-de8b-40eb-9c8e-220fe7e1b099.png" width="400"></div>
 
注：烧卡时MSISDN为电话号码（要和核心网数据库对应）
<div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/VONR.png" width="800"></div>

## 3.AR


**注意：AR和ALVR不能同时开，否则会连不上。**
unreal engine会自动加载steamvr，steamvr会自动唤醒ALVR，需要在steamvr中：
设置->管理加载项->禁用ALVR

运行登月的新项目：

AR头显和服务器主机连同一子网（CPE），主机ping不通头显是正常的，ping要支持icmp协议（头显估计不能）
进入编译后的文件夹，运行可执行文件连接AR头显（不用打开unreal）
 
```
MissionAR.exe -vr -HoloLensRemoting=192.168.8.114(AR头显IP)
```
 <div align="center"><img src="https://github.com/dragonstrong/mi3m/blob/main/AR.png" width="800"></div>

 
[官网指南](https://docs.microsoft.com/en-us/windows/mixed-reality/develop/unreal/unreal-streaming?tabs=wmr)
 

