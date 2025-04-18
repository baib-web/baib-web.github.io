最近看到一份文章 让我有了折腾的兴致：
[使用洋葱（Tor）创建隐藏的 IRC 服务器](https://infosecwriteups.com/create-a-hidden-irc-server-with-the-onion-router-tor-c839e3a81d78)
# Onion IRC是什么呢 
我们先拆开来看 
- Tor 网络 (Onion Network): 一种通过多层加密和匿名服务器路由网络流量 以隐藏用户身份和位置的技术
- IRC: 一种实时的文本聊天协议
- Onion IRC: 将 IRC 的实时聊天功能与 Tor 网络的匿名性相结合，提供匿名和安全的聊天环境 
- Onion IRC是世界最大黑客组织匿名者推荐的通讯聊天方式
# 搭建Onion IRC服务
## 前置条件
- 一台境外的VPS且搭载了Ubuntu系统
## 安装inspircd和tor
`sudo apt install -y inspircd tor`
## 更改您的标题 如果您很懒的话 只需从我的标题中复制即可
`nano /etc/inspircd/inspircd.motd`
```
--------------------------------------
隐私是一项人权 在这里畅所欲言吧
--------------------------------------
```
nano编辑器的保存步骤： ctrl x + Y + 回车
## 编辑Tor配置文件
`nano /etc/tor/torrc`
## 按如下示例添加配置选项
定义Tor 管理服务身份和加密材料的位置
`HiddenServiceDir /var/lib/tor/my_hidden_service/hostname`
IP保持127.0.0.1 6667为inspircd端口
`HiddenServicePort 6667 127.0.0.1:6667`
指定obfs4proxy 将下面示例的/path/to/obfs4proxy替换为他实际在的路径 找不到路径可以键入`whereis obfs4proxy`看看
`ClientTransport obfs4 exec /path/to/obfs4proxy`
输入网桥 （网桥有时效性 建议经常更换）获取网桥可以在电报上发消息给[GetBridgesBot](https://t.me/GetBridgesBot) 或是发邮件至bridges@torproject.org 或是访问[该网站](https://bridges.torproject.org/)网桥格式如下
```
Bridge [IP address]:[Port] [fingerprint]
Bridge 192.0.2.10:9001 AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA
Bridge 203.0.113.42:443 BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB
```
使用UseBridges 1配置让Tor通过网桥访问
`UseBridges 1`
## 按如下示例修改配置选项
去除类似下面行的注释（删除#号即删除注释）
`SocksPort 9050 # Default: Bind to localhost:9050 for local connections.
`
## 启动Tor服务（可以使用Nyx工具查看连接状态）
`sudo service tor start`
## 启动inspircd并查看状态
`sudo service inspircd start && sudo service inspircd status`
## 查看onion域名并记住
`cat /var/lib/tor/my_hidden_service/hostname/hostname`
# 访问Onion IRC
## 前置条件
- 可以魔法上网
- 在你要访问Onion IRC的设备上下载[Tor专家软件包](https://www.torproject.org/zh-CN/download/tor/)或[TOR浏览器](https://www.torproject.org/zh-CN/download/)
- 在你要访问Onion IRC的设备上安装[HexChat](https://hexchat.github.io/)
## 添加TOR配置文件
找到"`C:\Users\baibl\AppData\Roaming\tor`"目录创建一个txt文件 命名为torrc 即tor配置文件 不保留缀名
在配置文件中写入：
如果你是Tor浏览器：`ClientTransport obfs4 exec ./PluggableTransports/lyrebird.exe`
如果你是Tor专家软件包：`ClientTransport obfs4 exec ./pluggable_transports/lyrebird.exe`
网桥配置同上
```
Bridge [IP address]:[Port] [fingerprint]
Bridge 192.0.2.10:9001 AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA AAAA
Bridge 203.0.113.42:443 BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB BBBB
```
同上
`UseBridges 1`
## 启动客户端上的Tor服务
- 如果你是Tor浏览器 右击找到程序的路径 `...\Tor Browser\Browser`然后再进入`...\Tor Browser\Browser\TorBrowser\Tor `里面应该有一个tor.exe文件
- 如果你是Tor专家软件包 到达文件的/tor目录 里面应该有一个tor.exe文件
- 添加一个txt文件 编辑输入文本`tor` 保存并重命名为`start.bat` 点击便可快捷启动Tor服务
- 或者在当前目录右击选择在终端打开 键入`tor`指令待输出状态进度到达100%显示done即已连接到TOR路由
## 配置SOCKS5代理
打开Hexchat
先配置个人信息
点Add添加 填入onion域名 配置只勾最后一个选项
依次找到`Settings>Preferences>Network setup>Proxy Server`按如下方式配置
```
Hostname： 127.0.0.1
Port：9050
Type：SOCKS5
Use proxy for ： All connections
```
连接成功后会弹出一个窗口 这时选择创建或加入一个频道 比如#tor 这样就可以开始聊天了
教程到此结束 现在像一个真正的黑客一样 开始你的隐匿聊天吧












