#视频控件安装配置手册
##1. 环境需求

###OCX运行环境
1. 操作系统： windows XP，windows 7,windows 8, windows 10
2. 运行时环境：.NET framework 3.5及以上
3. 浏览器：IE 8，IE 9,IE 10,IE 11

###AIC配置
1. AIC版本: AIC7.2以上
2. 修改SDK配置，打开UUI，UCID和自定义速录数据传递
3. 添加离席原因code
4. 修改AIC的TS服务中的高级选项中勾选 Enable Reason Code

###Jtapi 服务配置
####需求
1. CentOS 6以上 64位 
2. JDK1.7环境

####配置
1. 修改conf/Config.ini 文件,设置以下内容：

~~~
	AES_IP              =  AES服务器IP地址
	AES_PORT            =  AES上tsapi服务port（默认为450）
	AES_LOGINID         =  AES上tsapi服务用户名
	AES_PWD             =  AES上tsapi服务用户密码
	AES_LINK            =  AES上tsapilink串
	AES_STATIONS        =  CM分配的虚拟分机号码
	# 分机间用逗号隔开，连续分机可以首尾分机用“-”连接。
例如：	
	AES_IP              =  8.8.8.8
	AES_PORT            =  450
	AES_LOGINID         =  xxx
	AES_PWD             =  xxx
	AES_LINK            =  AVAYA#CM#CSTA#xxx-AES
	AES_STATIONS        =  7001-7003,7010,7015
~~~

####运行
1. 将jserver_xxxx.zip压缩包里的文件解压
2. 安装成服务：执行 bin/startup64.sh install
3. 启动 bin/startup64.sh

##2. 控件安装
###安装包说明
1. videoPhoneSetup.exe  -- A端控件安装包
2. vtmPhoneSetup.exe  --C端控件安装包

###安装步骤
双击安装包，按默认提示安装即可

##3. 控件配置
###1）A端控件配置
* 修改安装目录下的App.config文件

~~~
<?xml version="1.0"?><configuration>  <appSettings>    <add key="serverConfig" value="http://192.168.22.149:9700/icsdk"/>    <add key="station" value="8004"/>    <add key="vidyoPortalURL" value="http://bj.vidyo.com/" />  <add key="httptimeout" value="15000" />  <add key="alertingTimeout" value="5" />  <add key="ringFileName" value="ring.wav" />    <add key="keepAlive" value="6000" />  </appSettings></configuration>
~~~
**关键配置：**

1. **serverConfig:**`AIC SDK 接入地址`
2. **station:**`座席桌面上的分机的号码`
3. **vidyoPortalURL:**`vidyo port的地址`
4. **其他默认即可**

###2）C端控件配置
* 修改安装目录下的App.config文件

~~~
<?xml version="1.0"?><configuration>  <appSettings>    <add key="jtapi_host_port" value="192.168.22.132:9500" />    <!--webCTI_host_port：WebCTI服务的地址和端口-->    <add key="vidyoPortalURL" value="http://bj.vidyo.com/" />    <!--vidyoPortalURL：vidyo的Portal地址-->    <add key="station" value="8005"/>    <add key="httptimeout" value="25000" />    <!--httptimeout:调用VMS接口时http请求的超时时长，单位：毫秒-->    <add key="calltimeout" value="5000" />    <!--calltimeout:每次呼叫请求的超时时长，单位：毫秒-->    <add key="callcount" value="3" />    <!--callcount:尝试呼叫次数-->      </appSettings>    </configuration>
~~~
**关键配置：**

1. **jtapi_host_port:**`JTAPI接入服务器的接入地址、端口`
2. **station:**`用来发起虚拟呼叫的虚呼叫分机号码`
3. **vidyoPortalURL:**`vidyo port的地址`
4. **其他默认即可**

