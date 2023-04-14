
# <div align="center">mi3m实验室硬件演示</div>


## 1、全景相机推拉流
全景相机网线连CPE DHCP，头显也连CPE（在不在一个局域网都可以，只要网络连通即可，当不在同一子网时，拉流地址为CPE的WAN IP）
（1）推流
开全景相机第三个按钮（横向），reday，向下模式选择 “4k 30Hz” ,不要选带3D的，会出现两个画面，选择直到出现计时画面为止。
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017623-48db9cd4-3932-483e-9b10-430aa0e15b69.png" width="400"></div>

 
也可在电脑上用insta pro软件推流。
（2）修改配置文件
头显连接数据线连电脑，电脑连CPE WIFI，然后修改配置文件，添加一个应用，改name uri id即可，另存为然后复制进去
<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017907-e9808156-752c-426d-8929-78fc6412baba.png" width="400"></div>

<div align="center"><img src="https://user-images.githubusercontent.com/32926995/232017973-722e5a6e-a8b4-4f00-a4de-ddf4fe3a4755.png" width="400"></div>



（3）头显拉流
打开头显  应用  点开对应应用名称（图中为星地）
（4）手机、电脑拉流
连CPE，打开Insta360Player，在线观看，输入配置文件中的地址

