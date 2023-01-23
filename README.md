# i5-5200u-Opencore
注意⚠️：本文档正在修改，已发布pre-release版本，更改内容过多相关文档未能跟进，如果有建议可以开issues
##  警告
MacOS 13删除了大量的驱动，升级后核显将无法被系统正常驱动驱动，可以使用**OpenCore-Legacy-Patcher**驱动，见结尾。
##  硬件配置
详细配置请查看官网数据库：https://www.acer.com/datasheets/2014/4876/V3-371/NX.MPFCN.015.html   
硬盘 ： 三星870evo 250GB      
无线网卡（蓝牙及WIFI）：BCM943224PCIET2（**NGFF**转卡）（自行更换），如需使用BigSur及以下系统，需要修改驱动，见结尾。
## 驱动情况
已基本完美驱动
### 已驱动硬件
CPU（i5-5200u）   
GPU（Intel HD Graphics 5500）   
键盘（在OC引导页面有间歇性不可用）   
声卡 **ALC283**布局15可驱动（11存在杂音，详细内容见末尾），3.5mm耳机孔/扬声器/麦克风可用   
USB均可用   
网卡 MacOS12下可用，**双向**隔空传送/接力/随航/共享剪贴板可用。隔空传送速度20m/s左右。     
电池 循环次数，插电状态，电量均可用（插电功率检测可能存在问题，无影响）     
摄像头   
读卡器（速度未知）  
附：Fn键+方向键操作可用。（调节音量/亮度/功能键）
### 已知问题
#### 休眠存在问题（休眠详细见末尾）  
可以全面禁用   
```
sudo pmset -a sleep 0;   
sudo pmset -a disablesleep 1;
```
取消禁用    
```
sudo pmset -a sleep 1;    
sudo pmset -a disablesleep 0;   
```
#### 触控板
由于未知的原因，触控板无法识别出四指及以上，但三指以下手势正常。    
## 注意事项
这些解决方法一般只适用于一模一样或者近似的机型。
### 安装前注意事项
1.更新主板Bios至最新。  
[下载地址](https://www.acer.com.cn/support.html?type=1)  
2.修改主板设置。  
Boot-Boot Mode 改为**UEFI**（必要）  
Boot-Secure Boot 改为**Disabled**（如果无法修改请先设置Bios密码） （必要）  
Main-F12 Boot menu 改为**Enabled**，便于临时修改引导项。 （非必要）  
### 引导OC时页面键鼠不可用
可以在引导界面时，按住下键并插拔有响应的USB设备（u盘·鼠标·iPhone）
### 跑完代码后黑屏
此时其实MacOS已经启动了，你需要闭合屏幕再打开（不要闭合太久否则系统会睡眠重启），如果背光暗着就点下键盘（任意键）。  
解决方法：（进入系统后）通过开启hidpi和注入eeid。  
推荐使用下面的项目：  
[xzhih/one-key-hidpi](https://github.com/xzhih/one-key-hidpi)
### Layout id
AppleAlc在2016.5.16发布的0.1.10中添加了V3-371驱动Alc283的layout id，但其存在耳机孔大量杂音及扬声器不使用时电流声的问题，在多次测试下，layout ID **15** 在扬声器，耳机孔，麦克风的工作中更加顺利，并且没有烦人的电流声。  
PS：目前我的MacOS工作在Layout id **15**的情况下没有任何异常。  
## 更新日志    
部分日志继承自[gatesx/Acer-v3-547H-OC-EFI-i5-5200u](https://github.com/gatesx/Acer-v3-371-547H-OC-EFI-i5-5200u)  
### 2023.1.24
更新至OpenCore0.8.7   
完成MacOS12/13中测试
添加plug-xcpm.aml，将EC重命名，若机型不同需删除自行配置，方法可在Google搜索，我将在博客中编写教程。    
重新使用SSDT-Time配置了ACPI（包括IQR）   
更新驱动     
重新配置Config    
添加了FeatureUnlock.kext已解锁通用控制等   
使用设备路径的方法代替acid的方法   
添加了启动声音
更改机型为Mac Mini（个人喜好，因为这样性能释放可能会好一点，文档中有机型推荐）   
启用了sata trim，如果影响开机请详细内容参考 (大头蔡Cass的视频)[https://www.bilibili.com/video/BV1HB4y1m7nJ/?spm_id_from=333.337.search-card.all.click]      
#### 讲一下为什么拖了这么久
距离我上次更新已经半年了，其实对于这台笔记本来说也到了寿终正寝的时间了，但我别无选择，我半年来一直研究黑苹果，认识了DSDT，ACPI，睡眠，很多新的知识，但是睡眠问题仍然未能解决，尽管尝试过Win11，但最后还是回到MacOS，因为Apple生态确实优秀，我觉得折腾也挺好，我没有上传到Github的原因有两个，第一是我觉得自己的引导并没有到那种程度，可以让别人参考，第二是我半年来我没有找到别人和我使用同一款机型，甚至连Star都没有。但最近我心情不太好，觉得找点事做，想起来还有这个我唯一发布的“项目”，就来更新了，半年了，变化好大，我上一次更新中考还没放榜，现在都高一寒假了。
### 2022.7.9
基于OpenCore 0.8.2完整重配  
更新驱动  
(MacOS12.4测试成功)  
### 2022.3.26  
更新至OpenCore 0.8.0   
更新驱动   
(MacOS 12.3 测试完成)   
完善Readme.md使其符合Markdown标准
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
![Wechat](https://user-images.githubusercontent.com/108464559/178111133-1902d02d-3d43-4bdb-b88f-2d3d695f7d70.JPG)   
![Alipay](https://user-images.githubusercontent.com/108464559/178111152-2ab9e2f5-d49c-4de9-95e7-e781cab4e712.JPG)
