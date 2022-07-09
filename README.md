# i5-5200u-Opencore
##  硬件配置
详细配置请查看官网数据库：https://www.acer.com/datasheets/2014/4876/V3-371/NX.MPFCN.015.html   
硬盘 ： 三星870evo 250GB      
无线网卡（蓝牙及WIFI）：BCM943224PCIET2（**NGFF**转卡）（自行更换），我已经设置内核版本号来适配Monterey与旧的MacOS的蓝牙驱动     
## 驱动情况
已基本完美驱动
### 已驱动硬件
CPU（i5-5200u）   
GPU（Intel HD Graphics 5500）   
触控板及键盘（在OC引导页面有间歇性不可用）   
声卡 **ALC283**布局15可驱动（11存在杂音，详细内容见末尾），3.5mm耳机孔/扬声器/麦克风可用   
USB均可用   
网卡 MacOS12下可用，**双向**隔空传送/接力/随航/共享剪贴板可用。隔空传送速度20m/s左右。     
电池 循环次数，插电状态，电量均可用（插电功率检测可能存在问题，没影响）     
摄像头   
读卡器（速度未知）  
附：Fn键+方向键操作可用。（调节音量/亮度）
### 已知问题
休眠存在问题
全面禁用   
```
sudo pmset -a sleep 0;   
sudo pmset -a disablesleep 1;
```
取消禁用    
```
sudo pmset -a sleep 1;    
sudo pmset -a disablesleep 0;   
```
## 注意事项
这些解决方法一般只适用于一模一样的机型。
### 安装前注意事项
1.更新主板Bios至最新。  
[下载地址](https://www.acer.com.cn/support.html?type=1)  
2.修改主板设置。  
Boot-Boot Mode 改为**UEFI**（必要）  
Boot-Secure Boot 改为**Diskabled**（如果无法修改请先设置Bios密码） （必要）  
Main-F12 Boot menu 改为**Enabled**，便于临时修改引导项。 （非必要）  
### 引导OC时页面键鼠不可用
可以在引导界面时，按住下键并插拔有响应的USB设备（u盘·鼠标·iPhone）
### 跑完代码后黑屏
此时其实MacOS已经启动了，你需要闭合屏幕再打开（不要闭合太久否则系统会睡眠重启），如果背光暗着就点下键盘（任意键）。  
解决方法：（居然系统后）通过开启hidpi和注入eeid。  
推荐使用下面的项目：  
[xzhih/one-key-hidpi](https://github.com/xzhih/one-key-hidpi)
### Layout id
AppleAlc在2016.5.16发布的0.1.10中添加了V3-371驱动Alc283的layout id，但其存在耳机孔大量杂音及扬声器不使用时电流声的问题，在多次测试下，layout ID **15** 在扬声器，耳机孔，麦克风的工作中更加顺利，并且没有烦人的电流声。  
PS：目前我的MacOS工作在Layout id **15**的情况下没有任何异常。  
## 更新日志    
部分日志继承自[gatesx/Acer-v3-547H-OC-EFI-i5-5200u](https://github.com/gatesx/Acer-v3-371-547H-OC-EFI-i5-5200u)  
### 202.7.9
基于OpenCore 0.8.2完整重配
更新驱动
(MacOS12.4测试成功)
### 2022.3.26  
更新至OpenCore 0.8.0  
更新驱动  
(MacOS 12.3 测试完成)
### 2022.3.4  
更新了layout id 为 **15**  
删除了英文文档  
PS：OC0.7.8暂不更新。  
### 2022.1.22  
定制USB  
中文文档改为README.md（主要文档）  
### 2022.1.18  
OpenCore版本升级至 0.7.7 （稳定通道）  
### 2022.1.17  
添加了读卡器驱动，系统信息面板信息可以读取，但没有CD卡来让我测试。  

## 赞赏  

![Wechat](https://user-images.githubusercontent.com/84220224/149635235-3f295841-d2cf-4579-b2a7-00b5345ff77e.jpg)
![Alipay](https://user-images.githubusercontent.com/84220224/149635237-1d548a3f-12c8-4c4b-81a8-08b455b9801f.jpg)
