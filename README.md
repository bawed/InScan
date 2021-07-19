# InScan开源扫描器
## 简介
本工具只可用于安全测试，勿用于非法用途！
### 工具定位
边界打点后的自动化内网工具，完全与服务端脱离。服务端只用于生成poc，网段信息等配置。
### 内网渗透痛点
目前已有的扫描器，依赖库较多，体积过于庞大，在内网渗透中，很多极端情况无法安装扫描器，使用socks4/socks5代理扫描的话，时间久，效率低。
### InScan优点
* 多平台，单一的二进制文件，免依赖;
* 支持自动可视化多级隧道，通过后台按钮开关即可穿越多层网络;
* 支持ipv6的扫描器;
* 快速直观查看多网卡机器，方便快速定位能穿多层网络机器;
* 通过已知密码生成社工字典，快速横向内网;
* 内网B/S架构系统自动化爆破，验证码自动识别;
* 快速资产识别，站点截图;
* 通过扫描到的资产自动化进行网站目录扫描；

### InScan支持平台
全平台支持，一个二进制文件，开箱即用。
命令行启动
```
  -pocPort int
        rpc端口，默认：8009 (default 8009)
  -rpcPort int
        rpc端口，默认：8008 (default 8008)
  -sysTime int
        系统信息上报时间，默认：15秒 (default 15)
  -webPort int
        web端口，默认：8080 (default 8080)
```
#### Windows使用
推荐管理员权限打开cmd，在cmd界面执行inscan.exe（管理员权限可支持icmp快速探测存活）
#### Linux使用
赋予文件执行权限
```
chmod +x inscan
```
后台执行
```
./inscan &
```
#### Android近源攻击
破解WiFi密码，手机安装Termux.apk，打开终端。  （不要勾选icmp探测存活）

```
wget 后台生成的arm架构程序
```
赋予文件执行权限
```
chmod +x inscan
```
后台执行
```
./inscan &
```
Termux切后台，使用手机浏览器访问 即可开始扫描。 

### 横向移动生成器
填写ip地址段或者与域名，开启自动化目录扫描、爆破、字典生成等功能。    
ip地址逗号分隔或换行分隔    
示例：
```
192.168.1.1/16,172.16.0.0/8
```
或
```
192.168.1.1/16
172.16.0.0/8
```
![-w1219](images/001.jpeg)

**弱口令字典生成**
![-w1145](images/002.jpeg)

**poc选择**
![-w1149](images/003.jpeg)

#### 精准的扫描方式
InScan首先做端口扫描，然后把状态为打开的TCP或UDP的IP+端口传递给服务识别模块，这些IP+端口会并行做服务探测。一旦连接建立成功，InScan会尝试超时等待，一些常见的服务，例如FTP、SSH、SMTP、Telnet、POP3、IMAP服务会对建立的连接发送一些欢迎的banner信息，这个过程没有发送任何的数据(也就是只经过了TCP的三次握手)，在等待的时间内如果收到了数据，InScan会将收到的banner信息和空探针的上千个指纹库进行匹配，假如服务和版本信息完全识别了，那么这个端口的服务识别就结束了。假如InScan探测到的端口为存活，但是没有获得banner数据，那么InScan会根据对应端口和优先级动态调整数据探针指纹策略继续进行扫描，直到完全识别到服务和版本。


![扫描原理流程](images/004.png)


### 扫描结果
**多网卡流量监控**
![-w1208](images/005.jpeg)

**操作系统详情**
![-w1213](images/006.jpeg)

**网卡、cpu、内存详情**
![-w1215](images/022.jpeg)

**可视化扫描进度**
![-w1190](images/007.jpeg)

**banner详情**
![-w861](images/023.jpeg)

**banner详情**

![-w1146](images/008.jpeg)

**可视化网卡识别，精准定位多网卡机器。**
![-w999](images/009.jpeg)

**poc漏洞验证**
![-w1280](images/010.jpeg)



#### web管理ssh
爆破成功后的ssh通过网页操作。    
开发中,近期上线............
#### rdp管理
爆破成功后的rdp，通过网页操作。    
开发中,近期上线............
#### 数据库管理
web界面实现数据库的增删改查功能，以及打包下载。    
开发中,近期上线............
#### web目录扫描
开发中,近期上线............
#### web登陆框自动爆破
机器学习的验证码识别库，自动爆破内网可登陆的web系统。        
开发中,近期上线............
### poc管理
#### 提交格式
目前支持xray、nuclei等模板，后续支持更多。
![-w1186](images/011.jpeg)
![-w1199](images/012.jpeg)


### cms指纹管理
**操作系统指纹、CMS指纹等。**
![-w1407](images/013.jpeg)

![-w1333](images/014.jpeg)
![-w1069](images/015.jpeg)

![-w1275](images/016.jpeg)
![-w1416](images/017.jpeg)
![-w1185](images/018.jpeg)

### 可视化隧道节点管理
使用隧道功能后，poc获取控制权限或爆破成功，自动化传输隧道agent，通过后台开关即可控制节点。
![-w1183](images/019.jpeg)

### DNSLOG
直接生成域名即可。
### shellcode自动化免杀
1. 采用国密算法加密的shellcode，可过大部分杀软，满足后渗透的需求。
2. 如编译好的exe文件，也可以使用该功能进行混淆捆版。
![-w1185](images/020.jpeg)

### 提权辅助
windows自动采集补丁信息，如当前非管理员权限，可自动化进行简单提权，同时也会列出可提权exp，进行手工提权。同时也可粘贴其他地方的systeminfo进行提权查询。
![-w768](images/021.jpeg)


### 提交反馈
如有好的建议，以及发现BUG。    
GitHub issue: https://github.com/inbug-team/InScan/issues

**官网(生成扫描器)：**
https://www.inbug.org

同时也可通过公众号联系：
![-w784](images/InBug.png)
