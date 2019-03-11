
目前纯google机器翻译，只为方便更多人, 如果你感觉“这翻译的神马玩意儿，让我来“， 轻点击 https://www.transifex.com/lightningcn/raspiblitz/translate/#zh_CN/readmemd开始翻译

# RaspiBlitz
*让自己的闪电节点运行-在一个漂亮的 lcd 在 raspberrypi 上运行。*

` 1.0 版, 带有lnd 0.5.2-beta和比特币0.17.0.1  和litecoin0.16.3。`

![RaspiBlitz](pictures/raspiblitz.jpg)

** raspibblitz 是一个全开关-上闪电节点基于 lnd 运行与一个比特币-或 litecoin-fullnode 在 raspberrypi3-与1tb 硬盘和一个很好的显示, 方便设置和监控. **

它主要用于学习如何运行您自己的节点分散从家里。通过成为闪电网络的一部分, 发现和发展闪电网络不断增长的生态系统。

## 功能概述

这是一个快速查看 ssh 主菜单 (一旦 raspiblitz 是设置):

![MainMenu-A](pictures/mainmenu.png)

还有其他可以打开的服务：

![MainMenu-Services](pictures/mainmenu-services.png)

作为SSH菜单的并行替代方案，还提供了RTL WebUI（LND API覆盖率为57％）：

![RTL-preview](pictures/RTL-dashboard.png)

请参阅[功能文档]（＃feature-documentation）中的更多详细信息，当然您拥有所有[Fullnode API]（#interface--apis）。

## 设置RaspiBlitz的时间估计

RaspiBlitz针对在hackday或会议的研讨会期间进行了优化。当它与最新的同步区块链组装在一起时，它可以在大约2到3个小时内准备就绪 - 大多数是等待时间。

如果你从家里开始订购亚马逊的零件（参见下面的购物清单），那么它是一个周末项目，有很多下载和同步时间，你可以在不断检查进度的同时做其他事情。

## 需要硬件

RaspiBlitz由以下部分构建：

* RaspBerryPi 3 B +
* 1TB硬盘
* 液晶显示器
* Micro SD卡16GB
* Powersupply>= 3A（大而稳定）
* 便宜的套管

**全部低于150美元/ 130欧元（取决于国家和商店）**

## 亚马逊购物清单

这些是基于国家/地区的社区限制购物清单：

* [德国]（shoppinglist_de.md）*（参考购物清单）*
* [美国](shoppinglist_usa.md)
* [联合王国](shoppinglist_uk.md)
* [瑞士](shoppinglist_ch.md)
* [法国](shoppinglist_fr.md)
* [中国](shoppinglist_cn.md)
* [澳大利亚](shoppinglist_au.md)
* [捷克](shoppinglist_cz.md)

*您甚至可以通过[Bitrefill]（https://blog.bitrefill.com/its-here-buy-amazon-vouchers-with-bitcoin-on-bitrefill-bb2a4449724a）向比特币和闪电支付您的RaspiBlitz亚马逊购物。*

* [我还有哪些其他案例选择？](FAQ.md#what-other-case-options-do-i-have)

## 组装你的RaspiBlitz

如果您的RaspiBlitz尚未组装，请将RaspberryPi板放入盒中并添加如下图所示的显示：

![LCD](pictures/lcdassm.png)

*购物清单中的某些案例包含较小显示的顶部 - 您可以忽略该顶部。*

将HDD连接到其中一个USB端口。最后你的RaspiBlitz应该是这样的：

![HardwareSetup](pictures/hardwaresetup.jpg)

* [如何将RaspberryPi连接到硬盘？](FAQ.md#how-to-attach-the-raspberrypi-to-the-hdd)

## 安装软件

您的SD卡需要包含RaspiBlitz软件。您可以通过[自己构建SD卡图像]（＃build-the-sd-card-image）或使用已准备好的SD卡图像来走很长的路：

1. 下载SD卡图像 -  **版本1.0 **：

HTTP：http：//wiki.fulmo.org/downloads/raspiblitz-v1.0-2019-02-18.img.gz

Torrent：https：//github.com/rootzoll/raspiblitz/raw/master/raspiblitz-v1.0-2019-02-18.torrent

SHA-256：99ca96d214657388305ca117e2343ead45f9d907f185bef36c712a9a3e75568f

2. 将SD卡映像写入SD卡 - 如果需要详细信息，请参见此处：
https://www.raspberrypi.org/documentation/installation/installing-images/README.md

## 启动你的RaspiBlitz

插入SD卡并连接电源插头。

* 此时，请务必将覆盆子与LAN电缆连接到互联网。
* 确保您的笔记本电脑和树莓在同一个本地网络上。

**疑难解答：**

* [我的笔记本电脑上没有LAN端口 - 如何连接到我的RaspiBlitz？](FAQ.md#i-dont-have-a-lan-port-on-my-laptop---how-to-connect-to-my-raspiblitz)
* [是否可以通过Wifi连接Blitz而不是使用LAN电缆？](FAQ.md#is-it-possible-to-connect-the-blitz-over-wifi-instead-of-using-a-lan-cable)
* [我可以直接将RaspiBlitz连接到笔记本电脑吗？](FAQ.md#can-i-directly-connect-the-raspiblitz-with-my-laptop)
* [我连接了我的硬盘但它仍然在显示屏上显示“连接硬盘”？](FAQ.md#i-connected-my-hdd-but-it-still-says-connect-hdd-on-the-display)

当一切正常启动时，您应该在LCD面板上看到RaspiBlitz的本地IP地址。

![LCD0](pictures/lcd0-welcome.png)

现在打开终端（[OSX]（https://www.youtube.com/watch?v=5XgBd6rjuDQ）/ [Win10]（https://www.youtube.com/watch?v=xIfzZXHaCzQ））并连接通过SSH与RaspiBlitz显示的命令：

`ssh admin @ [YOURIP]`→使用密码：`raspiblitz`

**现在按照终端中的拨号键进行操作。这可能需要一些时间（准备一些咖啡） - 但最后你应该在你的RaspberryPi上有一个正在运行的Lightning节点，你可以开始学习和攻击。**

## 支持

如果您遇到问题或仍有疑问，请按照以下步骤获取支持。另请查看[setup documentation]（＃setup-process-detailed-documentation）了解详细信息。

1. 如果你能找到对这个问题/问题的回答，请查看[FAQ]（FAQ.md）。

2. 请确定您的问题/问题是关于RaspiBlitz还是例如LND。例如，如果您在打开LND问题/问题的渠道时无法路由付款或收到错误，则最好由LND开发社区回答：https：//dev.lightning.community

3. 转到RaspiBlitz的GitHub问题：https：//github.com/rootzoll/raspiblitz/issues在那里搜索。还可以通过从过滤器/搜索框中删除“is：open”来检查已关闭的问题。

4. 如果你还没找到答案，请在RaspiBlitz GitHub上打开一个新问题。您可能需要在GitHub上注册一个帐户。如果它是RaspiBlitz的错误，请在您的问题中添加（复制+粘贴）调试报告（参见[FAQ]（FAQ.md）如何生成）和/或添加一些屏幕截图/照片，以便社区更深入地了解你的问题。

## 设置过程（详细文档）

*目标是，所需的所有信息都是在设置过程中与RaspiBlitz本身的交互中提供的。本章中的文档仅供背景，教育工作者评论和提及边缘案例。*

### 在里面

每次SSH登录后自动作为管理员登录RaspiBlitz，用户可以选择RaspiBlitz是否应该使用Lightning运行比特币或Litecoin：

![SSH0](pictures/ssh0-welcome2.png)

设置Raspi是目前唯一的选择，所以我们选择OK。

*此菜单由脚本`00mainMenu.sh`显示，并在管理员`.bashrc`的每次登录时自动启动。如果您想在登录后进入正常的终端提示，请使用CTRL-c或CANCEL。要从终端返回主菜单，您可以使用命令`raspiblitz`。*

首先要设置的是为RaspiBlitz命名：

![SSH2](pictures/ssh2-passwords.png)

此名称作为本地网络中的主机名提供给RaspiBlitz，稍后也提供给闪电节点的别名。

然后用户被要求思考并写下4个密码：

![SSH1](pictures/ssh1-name.png)

*密码A，B，C＆D构思直接基于[RaspiBolt Guide Preperations]（https://github.com/Stadicus/guides/blob/master/raspibolt/raspibolt_20_pi.md#write-down-your-密码） - 查看更多背景信息。*

然后要求用户输入密码A：

![SSH3a](pictures/ssh3a-password.png)

这是此屏幕后每个SSH登录必须使用的新密码。它还为用户现有用户设置：root，bitcoin＆pi。

*比特币和闪电服务稍后将在后台运行（作为守护进程）并出于安全原因使用单独的用户“比特币”。此用户没有管理员权限，无法更改系统配置。*

然后要求用户输入密码B：

![SSH3b](pictures/ssh3b-password.png)

*稍后将需要其他密码C＆D。它们将在闪电钱包设置期间使用。*

在此之后，设置过程将需要一些时间，用户将看到许多控制台输出：

![SSH4](pictures/ssh4-scripts.png)

*背景：在用户交互之后，启动以下脚本以自动设置RaspiBlitz：*

### 获得区块链

*如果你有一个带有准备好的区块链的硬盘（例如ready2go-set或你在车间），你可以跳到[下一章]（＃setup-lightning）。如果您开始使用空硬盘 - 您将看到以下屏幕：*

要获得区块链的副本，RaspiBlitz提供以下选项：

<img src =“pictures / ssh5-blockchain2.png”alt =“blockchain-options”width =“600”>

选项 - 以及何时选择 - 将在这里解释：

#### 洪流

这是下载RaspiBlitz的区块链数据的默认方式。如果您选择它将显示以下屏幕：

![DOWNLOAD1](pictures/download-torrent.png)

*这可能需要一段时间 - 通常情况下，如果你让它保持运行一夜，应该这样做，但有些用户报告说它需要长达3天。如果它花费的时间超过了这个时间，或者在您开始选择后超过一个小时看不到任何进度（下载开始），请考虑取消下载并选择FTP下载选项。*

在RaspiBlitz进行Torrent下载时关闭终端窗口（关闭笔记本电脑）是安全的。要检查进度并继续设置，您需要再次ssh。

您可以通过按住键`x`来取消torrent下载。然后下载将停止，系统将询问您是否要保持目前为止的进度。如果您需要关闭RaspiBlitz并且想要稍后继续或者想要尝试其他下载选项但是如果其他选项较慢或不能正常工作而希望保留选项继续使用，则这是有意义的。

* [如何避免使用准备好的区块链并验证自己？](FAQ.md#how-can-i-avoid-using-a-prepared-blockchain-and-validate-myself)
* [为什么我的区块链的洪流下载这么久？]（）

#### 2. FTP下载

如果torrent选项不适合你，你应该尝试FTP下载。请注意，我们将文件托管在中央服务器上，并且不保证正常运行时间和带宽。如果你启动它，你应该看到以下屏幕：

![DOWNLOAD1](pictures/download-ftp.png)

在RaspiBlitz进行FTP下载时关闭终端窗口（关闭笔记本电脑）是安全的。要检查进度并继续设置，您需要再次ssh。

您可以通过按住键`x`来取消FTP下载。然后下载将停止，系统将询问您是否要保持目前为止的进度。如果您需要关闭RaspiBlitz并且想要稍后继续或想要尝试其他下载选项但是如果其他选项较慢或不能正常工作，则希望保持选项继续进行FTP下载，这是有意义的。

#### 4.从另一台计算机复制

如果您有另一台可用的计算机（笔记本电脑，台式机或其他raspiblitz）已运行工作区块链（txindex = 1），您可以使用此选项将其复制到RaspiBlitz。这将通过SCP（SSH文件传输）在本地网络上完成。选择此选项并按照给定的说明操作。

如果您不想使用第三方准备好的区块链运行RaspiBlitz，这也是最佳选择。然后在更强大的计算机上安装比特币核心，自己同步+验证区块链（使用txindex = 1），然后通过本地网络将其复制。

更多细节：[我在另一台计算机上有完整的区块链。如何将其复制到RaspiBlitz？]（FAQ.md #i-have-the-blockchain-on-another-computer-how-do-copy-it-to-the raspiblitz）

#### 5.从第二个HDD克隆

如果通过网络复制不起作用，则是从另一台计算机转移区块链的备份方式。关于设置的更多细节可以在[这里]找到（FAQ.md＃how-do-i-clone-the-blockchain-from-a-2nd-hdd）。

#### 6.从比特币网络同步

这是万不得已的后备。 RaspberryPi具有非常低功耗的CPU，并且直接与peer2peer网络同步和验证区块链可能需要数周时间 - 这就是为什么上面发明的其他选项的原因。

### 设置闪电

如果您看到此屏幕，则会安装Lightning并等待您的设置。

![SSH7](pictures/ssh7-lndinit.png)

RaspiBlitz为您调用LND钱包创建命令：

![SSH8](pictures/ssh8-wallet.png)

首先，它会要求您设置您的钱包解锁密码 - 在此处使用您选择的PASSWORD C并通过再次输入来确认。

其次，它会问你是否有一个现有的“密码种子助记符” - 如果这是你的第一个RaspiBlitz / LND只是ansere`n`。

*“密码种子助记符”是包含私钥备份的单词列表。如果你没有以前的RaspiBlitz设置，它将为你创建。如果你想在旧的LND钱包上重新收集，那就是设置中输入它的点。*

第三，它会询问您是否要使用其他密码保护备份单词列表。你可以简单地将它保持为空，只需按ENTER继续。如果您想要获得额外保护，请在此处使用您的chossen PASSWORD D.

LND现在将为您生成一个新的密码种子（单词列表）。在你继续之前写下这个 - 没有你限制你在硬件故障等情况下收回资金的机会。如果你只是想尝试/试验RaspiBlitz，至少要用你的智能手机拍照以防万一。如果您计划在尝试后将RaspiBlitz保持运行，请将此单词列表离线存储或保存在密码保存中。完成后按ENTER键。

它现在将确保您的钱包正确初始化，并可能要求您使用刚刚设置的PASSWORD C解锁它。

![SSH9c](pictures/ssh9c-unlock.png)

*每次重新启动/重新启动RaspiBlitz时，LND钱包都需要解锁。*

RaspiBlitz现在将进行最终设置配置，如安装工具，将SWAP文件移动到HDD或激活防火墙。在此屏幕上，您将看到一些文本在屏幕上移动：

![SSH9b](pictures/ssh9b-reboot.png)

基本设置已经完成 - 很好......但是在此之后仍然需要等待很长时间才能使用新的RaspiBlitz。按“确定”重新启动。您的终端会话将断开连接，并且raspberry pi将重新启动。

### 第一次开始：同步和扫描

重启完成后，所有服务都需要一段时间才能启动 - 等到你在液晶显示器/显示器上看到LND钱包需要解锁时。然后使用与开头相同的命令再次使用SSH（检查LCD /显示），但这次（以及每次后续登录）都使用您的PASSWORD A.

终端登录后，LND会询问您（如每次启动/重新启动时）再次解锁钱包 - 请使用PASSWORD C：

![SSH9c](pictures/ssh9c-unlock.png)

现在第一次开始你将有更长的等待时间（1小时到2-3天，取决于你的初始设置）......但是没关系，只需让RaspiBlitz运行直到完成。您甚至可以立即关闭终端并关闭笔记本电脑并稍后重新开机。您将在Blitz LCD /显示屏上看到它已准备就绪，当蓝色背景屏幕消失时您会看到状态屏幕，如下图所示。

要了解花了这么长时间......它有两件事：

1. 区块链同步

![SSH9d1](pictures/ssh9d-blockchainsync.png)

硬盘驱动器上的区块链不是绝对最新的。根据你如何将它转移到你的RaspiBlitz，它将落后几小时，几天甚至几周。现在，RaspiBlitz需要通过直接与peer-2-peer网络同步来追赶其余部分，直到它几乎达到100％。但即使你在开始时看到99.8％这可能需要时间 - 获得1％可能长达4小时（取决于网络速度）。所以请耐心点。

* [为什么我的“最终同步”需要这么长时间？](FAQ.md#why-is-my-final-sync-taking-so-long)

2. LND扫描

![SSH9d2](pictures/ssh9d-lndscan.png)

如果Blockchain Sync完成，LND将自动开始扫描区块链并收集信息。如果达到这一点，通常只需要大约1小时，直到等待时间结束。

完成所有操作后，您应该在RaspiBlitz LCD /显示屏上看到此状态屏幕：

![SSH9dz](pictures/ssh9z-ready.png)

### 主菜单

如果您现在通过SSH在RaspiBlitz中登录（或者您仍然登录），您将进入主菜单：

![SSH9e1](pictures/mainmenu1.png)

如果你向下滚动..你会看到更多的选择。主菜单的所有选项将在功能文档中进行说明。

*好的..所以从这里开始你的RaspiBlitz就可以玩了。*

如果您需要了解Lightning最基本的后续步骤是：

* 基金连锁钱包
* 打开一个频道
* 进行付款

如果您喜欢从带有仪表板UI的Web浏览器而不是SSH终端执行此操作，请转到  `SERVICES`, 激活 `RTL Web接口` ，然后在webbrowser中重新启动：http：// [LOCAL-IP- OF-YOU-NODE]：3000（密码B是你的RPC密码）。

玩得开心，骑着闪电：D

* BTW总是喜欢在twitter @ rootzoll上看到新的RaspBlitzes的照片添加到网络上*

* [我怎样才能获得进一步的帮助/支持？](#support)

### 功能文档

这些是通过RaspiBlitz SSH主菜单和服务提供的功能。他们的目标是为您提供一些基本/后备功能和配置。更复杂或用户友好的任务最好通过[API]（#interface  -  apis）连接到Lightning节点的钱包，应用程序和脚本来完成 - 因为你在RaspiBlitz上有一个完整的比特币和闪电节点。

让我们来看看SSH主菜单（向下滚动3页）：

![MainMenu-A](pictures/mainmenu1.png)

#### 信息：Raspiblitz状态屏幕

这是显示在LCD /显示屏上的屏幕。如果您旁边没有RaspiBlitz，那么从SSH调用远程情况很有用。但是如果你想复制+粘贴你的nodeID或制作截图。

![SSH9dz](pictures/ssh9z-ready.png)

*它不会自动更新。它只是一次性信息。*

* [为什么显示屏上的比特币IP是红色的？](FAQ.md#why-is-my-bitcoin-ip-on-the-display-red)
* [为什么显示屏上的节点地址为红色？](FAQ.md#why-is-my-node-address-on-the-display-red)
* [为什么我的节点在显示屏上的地址为黄色（不是绿色）？](FAQ.md#why-is-my-node-address-on-the-display-yellow-not-green)

#### 资金：为您的连锁钱包提供资金

在您打开其他节点的频道之前，您需要将一些硬币放到您的LND链式钱包上。使用此选项可生成发送资金的地址。

*提醒：RaspiBlitz和LND仍然是实验性软件。通过为您的LND节点提供资金，您可以承担失去资金的风险。因此，只需少量玩 - 当时20欧元/美元的区域应足以让您获得第一次体验。*

#### CONNECT：连接到对等方

在您可以使用网络上的另一个节点打开通道之前，您需要将此节点作为对等方连接到您的节点。

与对等方打开一个频道只是可选的。让另一个节点成为对等节点可以帮助您的节点通过八卦协议接收有关网络的信息。它将帮助您的节点通过网络找到更好的路由。

#### CHANNEL：用Peer打开一个频道

要使用其他节点打开付款渠道，您可以使用此选项。

在[1ML.com]（https://1ml.com/）等在线目录中查找有用节点以打开频道。

*这只是一个非常基本的shell脚本。要获得更多可用性，请尝试使用RTL Web界面（在“服务”下）或使用RaspiBlitz连接（移动）钱包。*

#### 发送：支付发票/付款请求

通过闪电支付发票。

*这只是一个非常基本的shell脚本。要获得更多可用性，请尝试使用RTL Web界面（在“服务”下）或使用RaspiBlitz连接（移动）钱包。*

#### RECEIVE：创建Invoice / PaymentRequest

创建发票以发送给通过lightnig支付的某人或服务。

*这只是一个非常基本的shell脚本。要获得更多可用性，请尝试使用RTL Web界面（在“服务”下）或使用RaspiBlitz连接（移动）钱包。*

![MainMenu-B](pictures/mainmenu2.png)

#### 服务：激活/停用服务

![MainMenu-Services](pictures/mainmenu-services.png)

##### 频道自动驾驶仪

自动驾驶仪是LND的一项功能，您可以打开它。它会自动使用大约一半的连锁资金（如果有的话）打开其他闪电节点的频道，自动驾驶员认为这对改善您的支付路线非常有用。

##### Testnet

如果您想尝试一下并玩免费测试硬币，您可以从区块链的主网切换到测试网。

请注意，可能需要一些时间来同步测试区块链，并且您需要在此过程中设置新的lnd testnet钱包。

##### 动态DNS

这是一种使您的RaspiBlitz可以从互联网公开访问的方式，以便其他节点可以与您打开频道，您可以从本地网络外部连接您的移动钱包。

为此，您可以在freedns.afraid.org等DynamicDomain服务上注册并转发TCP端口......

* 8333（比特币/主网）
* 9735（LND节点）
* 10009（LND RPC）

...从您的互联网路由器到RaspiBlitz的本地IP，然后激活unter“服务”“DynamicDNS”选项。

系统将要求您提供动态域名，例如“mynode.crabdance.org”，您还可以选择设置一个定期调用的URL，以使用动态域服务更新您的路由器IP。在freedns.afraid.org上，一旦添加了一个URL，就会在“动态DNS”菜单下将此URL称为“直接URL”。

##### 在TOR后面跑

您可以将比特币和Lightning节点作为TOR隐藏服务运行 - 用.onion-address替换您的IP

![tor1](pictures/tor1.png)

这有一些好处：

* 您不发布运行节点的IP，因此更难以解析您的真实姓名和位置。
* 您通过路由器的NAT隧道，并使比特币和闪电可以到达所有其他TOR节点。
* 通过使用TOR地址，可以将节点移动到不同的IPv4地址，并保持现有（=非常开放和资助）的通道功能。

但这也带来以下副作用：

* 移动钱包不支持连接TOR
* 没有运行TOR的闪电节点无法到达你（就像在NAT后面）

要尝试一下，只需打开服务 - 如果它不适合您，您可以稍后停用。

TOR集成是实验性的，目前无法再次关闭TOR。

##### RTL Web界面

RTL Web界面是一个LND控制仪表板，您可以在浏览器中使用一个漂亮的GUI运行它 - 它提供了比RaspiBlitu SSH菜单更多的Lightning节点控制。建议试一试。

![RTL](pictures/RTL-dashboard.png)

RTL程序员欢迎反馈：https：//github.com/ShahanaFarooqui/RTL

##### LND自动解锁

此功能基于https://github.com/Stadicus/guides/blob/master/raspibolt/raspibolt_6A_auto-unlock.md

它可以在“服务” - >“自动解锁LND”下激活。建议在使用DynamicDNS时打开它。因为在路由器的公共IP更改时，LND会自动重启，如果没有自动解锁，它将保持非活动状态/未达到状态，直到您手动解锁它为止。

* [使用自动解锁时，我会失去多少安全保障？](FAQ.md#when-using-auto-unlock-how-much-security-do-i-lose)

#### MOBILE：连接手机钱包

此功能可以帮助您将RaspiBlitz连接到智能手机上的手机钱包。

<img src =“pictures / mobile.png”alt =“mobile-wallets”>

目前[ZAP（iOS）]（https://github.com/LN-Zap/zap-iOS）和[Shango（iOS / Android）]（https://github.com/neogeno/shango-lightning-钱包）可用。

请记住，如果您还想通过RaspiBlitz从外部（通过LTE，3G，...）连接到智能手机，您可能需要在路由器上打开/转发端口，并应查看DynamicDNS功能来处理改变我们的家庭DSL的IP。

* [如何缩小QR码以连接我的Shango / Zap手机？](FAQ.md#how-do-i-shrink-the-qr-code-for-connecting-my-shangozap-mobile-phone)

#### 出口：蛋白杏仁饼干和TLS.cert

提供以下选项以使Macaroon和TLS文件可用于其他应用和钱包。

* Macaroons：允许在LND节点上执行某些命令的访问令牌。*

* TLS：用于保护/加密与LND节点的通信的证书。*

<img src =“pictures / export.png”alt =“export”>

##### 十六进制字符串

Macaroons和TLS.cert文件可以从RaspiBlitz复制+粘贴为Hex-Strings到任何其他支持它的应用程序。如果选择此选项，RaspiBlitz将以Hex-String为您打印所有文件。

建议将此方法导出到：
* [焦耳浏览器钱包](https://lightningjoule.com)

##### SSH下载

SCP是一个类似SSH的命令来传输文件。如果能够通过SSH连接到RaspiBlitz，SCP也可以传输文件。如果您选择这些选项，RaspiBlitz将打印准备好的SCP命令，您可以复制+粘贴以在第二个终端中运行。

建议将此方法导出到：
* [Zap桌面钱包](https://github.com/LN-Zap/zap-desktop)

##### 下载浏览器

打开临时网络服务器，以便您可以通过浏览器下载本地网络中的文件。

*这是传输这些文件的最不安全的方式 - 本地网络中的每个人都可以在下载期间访问这些文件。请记住，使用Admin-Macaroon，有人可以接管您的节点并花掉所有资金。只需使用作为最后一个后备。*

##### 更新蛋白杏仁饼干和TLS

如果要使先前导出的Macaroons和TLS文件无效，请使用 - 例如丢了手机钱包。

#### 名称：更改节点的名称/别名

更改节点的名称。

#### 密码：更改密码

更改密码以确保安全性。

![MainMenu-C](pictures/mainmenu3.png)

#### CHASHOUT：从链条钱包中删除资金

如果想要从RaspiBlitz中删除所有资金，请使用。

#### lnbalance：详细的钱包余额

<img src="pictures/bonus-lnbalance.png" alt="bonus-lnbalance" width="600">

#### lnchannels：闪电频道列表

<img src="pictures/bonus-lnchannels.png" alt="bonus-lnchannels" width="600">

#### OFF：PowerOff RaspiBlitz

关闭RaspiBlitz的安全方法。如果需要重启/重启 - 取消/重新插入电源。

#### X：控制台终端

关闭SSH主菜单并退出到终端 - 用户可以直接利用CLI客户端`bitcoin-cli`和`lncli`来使用比特币和Lightningnode。

使用命令`raspiblitz`，可以返回主菜单。

## 接口/ API

要开发自己的脚本/应用程序并将其他服务/应用程序连接到RaspiBlitz，您可以使用多个接口/ API：

### 比特币

* 终端上的`bitcoin-cli`命令行界面
* `bitcoind`在8333端口运行（公共）
* 端口8332（本地）上运行的`JSON-RPC` [DOC]（https://en.bitcoin.it/wiki/API_reference_%28JSON-RPC%29）

### LND闪电

* 终端上的`lncli`命令行界面[DOC]（https://api.lightning.community/）
* `lnd`在9735端口运行（公共）
* 在端口10009上运行`gRPC`（公共）[DOC]（https://api.lightning.community/）
* 在端口8080上运行`REST`（公共）[DOC]（https://api.lightning.community/rest/index.html）

## 更新到新版本

如果你的RaspiBlitz比较旧，那么verison 0.98请[见这里]（FAQ.md）。

如果您有RaspiBlitz版本0.98或更新版本，请执行以下操作：

* 主菜单> OFF
* 断电
* 删除SD卡

现在下载新的RaspiBlitz SD卡映像并将其写入SD卡。是的，您只需覆盖旧的SD卡即可，RaspiBlitz将您的所有个人数据存储在硬盘上。查看有关最新SD卡图像的详细信息[此处]（#instain-the-software）。

*如果您已对系统进行了手动更改（已安装的软件包，添加的脚本等），则可能需要在覆盖SD卡之前做一些准备工作 - 请参阅[FAQ]（FAQ.md＃why-do-i-need-to -RE烧-MY-SD卡换一个更新）。*

如果成功完成，只需将SD卡插入RaspiBlitz并再次打开电源即可。然后按照显示屏上的说明操作......别担心，您不需要再次重新下载区块链。

* [为什么我需要重新刻录SD卡才能进行更新？](FAQ.md#why-do-i-need-to-re-burn-my-sd-card-for-an-update)

## 构建SD卡映像

RaspberryPi的RaspiBlitz即用型SD卡图像由我们下载，以便让所有人快速启动（见上文）。但如果您想自己构建该图像 - 这是一个快速指南：

* 使用DESKTOP卡图片获得新的Rasbian RASPBIAN STRETCH：[下载]（https://www.raspberrypi.org/downloads/raspbian/）
* 将图像写入SD卡：[TUTORIAL]（https://www.raspberrypi.org/documentation/installation/installing-images/README.md）
* 安装时，将名为`ssh`的文件添加到SD卡的根目录以启用SSH登录
* 在Raspi中启动卡并使用`ssh pi @ [IP-OF-YOUR-RASPI]登录每个SSH的密码是`raspberry`

现在您已准备好启动SD卡构建脚本 - 将以下命令复制到终端并执行：

`wget https://raw.githubusercontent.com/rootzoll/raspiblitz/master/build_sdcard.sh&& sudo bash build_sdcard.sh`

正如您在URL中看到的那样，您可以在`build_sdcard.sh`下找到此Git仓库中的构建脚本 - 您可以在其中查看已详细安装和配置的内容。随意拉动请求发布改进。

整个构建过程需要一段时间。最后安装LCD驱动程序并重新启动。在此过程中创建用户`admin`。请记住，默认密码现在是`raspiblitz`。您可以再次使用SSH登录 - 这次使用admin：`ssh admin @ [IP-OF-YOUR-RASPI]`。 SD卡映像的安装程序应自动启动。如果您此时不想继续安装并使用此SD卡作为模板来设置多个RaspiBlitze，请单击“取消”并运行`/ home / admin / XXprepareRelease.sh`。一旦您看到LCD变白并且pi的活动LED开始变暗，您可以拔掉电源并取出SD卡。您现在已经构建了自己的RaspiBlitz SD卡映像。

*注意：如果您打算将自构建SD卡用作MASTER副本来备份映像并进行分发。使用较小的8GB卡。这样就可以确保它适用于后来推荐用于RaspiBlitz的每张16 GB卡。*

* [我可以在RaspberryPi以外的其他计算机上运行RaspiBlitz吗？](FAQ.md#can-i-run-raspiblitz-on-other-computers-than-raspberrypi)
* [如何在主分支之外构建SD卡？](FAQ.md#how-can-i-build-an-sd-card-other-then-the-master-branch)
* [如何从我的分叉GitHub Repo构建SD卡？](常问问题.md#how-can-i-build-an-sd-card-from-my-forked-github-repo)

## FAQ

以下是一些常见问题的简短选择：

* [如何备份我的Lightning节点？](FAQ.md#how-to-backup-my-lightning-node)
* [如何从失败的RaspiBlitz中恢复我的硬币？](FAQ.md#how-can-i-recover-my-coins-from-a-failing-raspiblitz)
* [那些“欠压检测”警告是否有问题？](FAQ.md#are-those-under-voltage-detected-warnings-a-problem)
* [我可以在RaspberryPi以外的其他电脑板上运行RaspiBlitz吗？](FAQ.md#can-i-run-raspiblitz-on-other-computers-than-raspberrypi)

你还有更多问题吗？检查[RaspiBlitz-FAQ-Archive]（FAQ.md）。

## 社区发展

欢迎大家加入，改进和扩展RaspiBlitz--这是一项正在进行的工作。 [检查问题]（https://github.com/rootzoll/raspiblitz/issues）如果你想帮忙或添加新的想法。您可以在`/ home / admin`或子文件`home.admin`中的git repo中找到用于RaspiBlitz交互的脚本。

还可以通过原始的“[RaspiBolt]（https://github.com/Stadicus/guides/tree/master/raspibolt）”教程深入了解如何在RaspberryPi上构建闪电节点的基础知识RaspiBlitz的开发工作 - 对斯塔迪库斯来说太多了:)

加入我的推特[@rootzoll]（https://twitter.com/rootzoll），在upcomming [#lightninghackday]（https://twitter.com/hashtag/LightningHackday?src=hash）访问我们或查看我们在柏林的比特币聚会...每隔一个星期四晚上一个月在房间的77吧 - 随意给我买一个带闪电的啤酒:)

* [我怎样才能获得进一步的帮助/支持？](#support)

Freenode上的IRC频道`irc：// irc.freenode.net / raspiblitz`（unmoderated）
