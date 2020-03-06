# 华为光猫破解教程
## 前言
### 破解光猫必备要求
- 有原光猫超密（最好要有，方便获取宽带信息）  
- 有宽带的loid（部分需要password）  
- 有宽带账号密码  
- 记下宽带的Vlan ID  
- 有宽带电话请记录清楚里面的配置
##### 在此diss【宽带论坛】【恩山无线】  
两大坑害换光猫用户的论坛  
各种资源全部被这两大论坛封锁，用户上传的固件教程被这些论坛管理员删除，拿去售卖  
把其他用户摸索出来后分享的教程，转身删除，拿去咸鱼售卖  
请问你们要脸吗？不！你们没有脸！  
你们只想着赚用户的钱，甚至还在论坛发着错误教程让别人变砖，还口口声声的在论坛说帮别人修砖不值得，不“浪费时间”  
现实是你们咸鱼的救砖交易量可观，随便帮忙“下发”一次收费就是三四十，这就是你们口中的“不浪费时间”修砖、“没空”，真可谓是滑天下之大稽  
#### 注意事项
##### 本教程以及其包含的固件、工具所有人可免费下载，完全开源，开源协议遵照“[CC-BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)”，  
[![image](https://github.com/2879597772/ONT/blob/master/images/CC.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.zh)
##### 其意思为“知识共享-署名-非商业性-相同方式共享，即此教程共享，转发必须注明作者本人-不允许以各种方法拿此教程获利，此共享协议对中国大陆有效，受中国法律保护！用本教程获利的人，我将保留依法追责的权力！
·此教程目的是为了避开【宽带论坛】【恩山无线】那些无良管理和商家，把一些简单问题，他人解决后分享的问题收费化  
·如果你也对折腾光猫有兴趣，有意发类似教程，有意分享您的换猫经验，手上有工具或固件愿意分享出来，请在“issues”发表出来，我将注明您的信息并发表出来  
·此教程可能看到、发现的人并不多，但是，一个人看到就可以帮助一个人！

### 本教程适用于华为光猫的破解，主要内容包括：
- [开启telnet](#开启telnet)
- [补全shell](#补全shell)
- [修改连接设备数量](#修改连接设备数量)
- [修改到原厂界面](#修改到原厂界面)
- [修改到电信界面](#修改到电信界面)
- [修改到联通界面](#修改到联通界面)
- [修改到移动界面](#修改到移动界面)
- [itms伪认证](#itms伪认证)
- [改E/G模式（部分可改双模）](#改E/G模式)  
- [救砖方法](#救砖方法)
- [相应工具的分享](#相应工具的分享)
## 正文
### 开启telnet
telnet，乃破解光猫必有的一项，开启后可通过telnet对光猫进行修改，如获取超密、修改界面、更改光模块运行模式等等。  
开启此模式前，请确保你的电脑开启了telnet功能，具体方法请自行百度。  
早期光猫可以使用“组播工具”使能方式开启光猫的telnet功能，随着华为升级光猫固件，这种方法在新光猫上已经失效，现给出目前已知的3种开启方案  
##### 1· 使用超密开启  
使用超密登录光猫后，进入“安全>ONT访问控制配置”，将“使能LAN侧PC通过TELNET访问设备”勾选，即可开启telnet（如下图）其他界面开启方式大同小异  
![image](https://github.com/2879597772/ONT/blob/master/images/open_telnet.jpg)
##### 2· 修改配置开启
部分光猫由于地区/固件影响，没有办法用上图方式开启telnet，但若在“管理>设备管理”中有“USB备份设置”的话，即可用此方法开启telnet  
·在“USB备份设置”中勾选“快速恢复”以便恢复配置  
·在光猫背面插入U盘后点击“备份配置”（插入U盘后刷新界面）  
![image](https://github.com/2879597772/ONT/blob/master/images/open_telnet2.jpg)  
· 拔出U盘，插入电脑，可以看见U盘目录下有“e8_Config_Backup”文件夹，内有一个*.cfg的文件，此文件就是我们要修改的文件  
· 此文件一般都被加密，请使用目录工具中的“华为配置文件解密工具”进行解密  
· 将配置文件`<X_HW_CLITelnetAccess`字段做如下修改： 
```   
<X_HW_CLITelnetAccess Access="1" TelnetPort="23" OutTelnetPort="23"/>  
```  
![image](https://github.com/2879597772/ONT/blob/master/images/open_telnet3.jpg)  
· 加密后插回光猫，将光猫断电重启，配置文件即可恢复，telnet开启  
##### 3· TTL修改参数
目前正在查询相关资料和测试
### 补全shell
全新光猫一般默认不带shell，telnet进入光猫后，输入su>shell>help查看可用命令，如果少的可怜，就需要补全shell  
华为光猫补全shell方法都大同小异，成功率不高的原因往往在于补全所需的文件，此类文件一般都由某些大神制作，很少外流，本人已将可找到的补全文件都放在工具中了，大家可以一个一个慢慢试验  
· 补全方式：打开使能工具，点升级，选网卡，浏览补全文件，最后点升启动。  
· 正常升级情况下，光猫面板所有的灯同时一闪一闪，如果灯没反应，使能点停止，不要关闭使能，光猫断电，光猫通电，光猫启动完成，点使能中的：启动。  
· 日常从帮别人补全，有发现连接不上光猫的情况，可尝试更换组播工具进行补全  
### 修改连接设备数量
由于不同人的不同需求，一台光猫可能同时连接数台设备，但光猫有个很变态的设置，限制了光猫的设备连接数量，本块内容在于解除光猫最大设备连接量  
· 修改配置法：下载配置文件，见[`开启telne`](#修改配置开启)`中的修改配置开启部分`，并对文件进行解密  
· 在配置文件中查找`<X_HW_AccessLimit`字段，并这样修改
```
TotalTerminalNumber="40"  
```  
![image](https://github.com/2879597772/ONT/blob/master/images/TotalTerminalNumber.jpg)   
其中`40`就是控制设备数量的关键，可以按照你的需求自行修改  
· 修改后进行加密，按照[`开启telne`](#修改配置开启)的方法恢复  
### 修改到原厂界面
### 修改到电信界面
### 修改到联通界面
### 修改到移动界面
### itms伪认证
`此条影响范围小，一般改回原厂界面都不需要这步操作，但总有例外，特别是运营商定制光猫，就算改回原厂，也容易出现OLT注册成功，ITMS注册失败导致“获取到ip地址、可以看iptv、ping外网ip可以通、光猫自检通过，但是局域网内打开任意网址自动跳转至光猫注册界面`  
此电信定制猫出现较多，本人多方查询后才找到，原因是此方法大都为论坛中楼中楼回复，搜索引擎收录较少！废话不多说，以下是详细教程：  
· 下载配置文件并解密，见[`开启telne部分`](#修改配置开启)  
· 搜索`<X_HW_UserInfo`字段
· 将  
```
<X_HW_UserInfo UserName="" UserId="" Status="99" Limit="5" Times="0" Result="99" X_HW_InformStatus="0" X_HW_AcsCnnctSatus="0" ForceSupport="1" SameWithPonInfo="1" X_HW_RegisterMode="1" />
<X_HW_ServiceManage FtpEnable="0"   FtpPort="21" FtpRoorDir="/mnt/ftproot/" FtpUserNum="0" />
```  
改为这样  
```
<X_HW_UserInfo UserName="" UserId="" Status="0" Limit="10" Times="0" Result="1" X_HW_InformStatus="0" X_HW_AcsCnnctSatus="0" ForceSupport="1" SameWithPonInfo="1" X_HW_RegisterMode="1" />
<X_HW_ServiceManage FtpEnable="0"   FtpPort="21" FtpRoorDir="/mnt/ftproot/" FtpUserNum="0" />
```  
· 其中主要修改的就是：`Status=" " Limit=" " Times=" " Result=" "`为itms认证配置  

### 改E/G模式
### 救砖方法
### 相应工具的分享

本人时间没有那么多，这些教程只会在有时间的时候写，请各位见谅