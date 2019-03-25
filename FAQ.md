# 常见问题 - 常见问题解答

## 如何生成调试报告？

如果您的RaspiBlitz工作不正常并且您希望从社区获得帮助，那么提供更多调试信息是好的，因此其他人可以更好地诊断您的问题 - 请按照以下步骤生成调试报告：

- 使用您的密码A以管理员用户身份ssh进入您的raspiblitz
- 如果看到菜单 - 使用CTRL + C进入终端
- 要生成调试报告，请运行：`./ XXdebugLogs.sh`
- 然后复制以`*** RASPIBLITZ LOGS ***'开头的所有输出并分享

*请注意：此日志可能包含私人信息（如IP，节点ID，......） - 只需公开分享您的感觉。*

## 如何更新我的RaspiBlitz（AFTER版本0.98）？

准备RaspiBlitz更新：

- 主菜单>关闭
- 移除电源
- 删除SD卡

现在下载新的RaspiBlitz SD卡映像并将其写入SD卡。是的，您只需覆盖旧的SD卡即可，所有个人数据都在HDD上（如果您没有对系统进行任何手动更改） 。有关最新SD卡图像的详细信息，请访问：https：//github.com/rootzoll/raspiblitz#scenario-2-start-at-home

如果成功完成，只需将SD卡插入RaspiBlitz并再次打开电源即可。然后按照显示屏上的说明操作......别担心，您不需要再次重新下载区块链。

## 如何更新旧的RaspiBlitz（BEFORE版本0.98）？

如果您的旧版RaspiBlitz版本为0.98或更高版本，请按照自述文件中的更新说明进行操作。

如果您运行早于0.98的版本，您基本上需要设置一个新的RaspiBlitz来更新 - 但您可以将区块链数据保留在HDD上，因此您不需要再等待很长时间：

1. 关闭所有打开的闪电通道（`lncli closeallchannels --force`）或使用菜单选项'CLOSE ALL'（如果可用）。等到所有结账交易完成。

2. 将所有链上资金转移到raspiblitz外的钱包（`lncli --conf_target 3 sendcoins [ADDRESS]`）或使用菜单选项'CHASH OUT'（如果有的话）

3. 通过运行脚本`/ home / admin / XXcleanHDD.sh`为新设置准备硬盘（区块链将保留在硬盘上）

4. 然后关闭RaspiBlitz（`sudo shutdown now`），用新图像刷SD卡，重做RaspiBlitz的全新设置，重新调入你的资金，重新打开你的频道

## 为什么我需要重新刻录SD卡才能进行更新？

我知道只运行一个更新脚本会更好，你准备好了。但是这些脚本需要以更复杂的方式编写，以便能够使用任何版本的LND和Bitcoind（它们已经足够复杂并且具有所有边缘情况）并且测试将变得比它更耗时。现在已经。这不是单个开发人员可以提供的。

对于某些人来说，通过重新刻录新的SD卡进行更新可能是一个痛点 - 特别是如果您添加了自己的脚本或对系统进行了更改 - 但这是设计的。这是一种在每次更新时强制执行“干净状态”的方法 - 与我测试和开发脚本的状态相同。这种痛苦的原因：我根本无法编写和支持在每个修改过的系统上永久运行的脚本 - 这简直太过分了。

使用SD卡更新机制，我降低了复杂性，我提供了一个“干净状态”操作系统，LND / Bitcoind和脚本紧密捆绑在一起的依赖/组合，就像我测试它们一样，它更容易重现错误报告并提供支持办法。

当然，人们应该修改系统，添加自己的脚本等...但是如果你想要获得RaspiBlitz更新的好处，你有两种方法可以做到：

1. 将您的更改作为拉取请求返回到主项目，以便它们成为下一次更新的一部分 - 下一个SD卡版本。

2. 进行更改，以便他们能够轻松更新SD卡 - 将所有脚本和额外数据放入HDD和文档中，以便在更新后如何再次激活它们。甚至可以编写一个小的shell脚本（存储在硬盘上）安装和配置所有附加软件包，软件和脚本。

* BTW使用新的SD卡进行更新时会产生有益的副作用：您还可以摆脱过去发生的任何恶意软件或系统膨胀。你从一个新系统开始：）*

## 如何避免使用准备好的区块链并验证自己？

torrent和FTP下载使用准备好的区块链来启动RaspiBlitz。如果您想要自我验证，您可以在另一台功能更强大的计算机上执行此操作，然后将您自己经过验证的区块链转移到RaspiBlitz。有关详细信息，请查看[自述文件]（README.md）中所述的“从另一台计算机复制”和“从第二台硬盘克隆”选项。

## 我在另一台计算机上有完整的区块链。如何将其复制到RaspiBlitz？

从另一台计算机（例如您的笔记本电脑）复制已经同步的区块链可以快速启动RaspiBlitz或用新的区块链替换损坏的区块链。另外，您自己同步并验证了区块链，并且不信任RaspiBlitz FTP / Torrent下载（不信任，验证）。

一个要求是区块链来自另一个比特币核心客户端，其版本大于或等于0.17.1且事务索引已打开（`bitcoin.conf`中的`txindex = 1`）。

但我们不会通过USB将数据复制到设备，因为硬盘需要在EXT4中格式化，而Windows或Mac计算机通常无法读取/写入。所以我将解释一种通过本地网络复制数据的方法。这应该可以在Windows，Mac，Linux甚至另一个已经同步的RaspiBlitz中使用。

两台计算机（您的RaspberryPi和其他具有完整区块链的计算机）需要连接到同一本地网络。确保比特币在包含区块链的计算机上停止运行。如果您的区块链源是在终端`sudo systemctl stop bitcoind`上运行的另一个RaspiBlitz，然后转到区块链数据所在的目录`cd / mnt / hdd / bitcoin`  - 稍后复制/传输时重新启动RaspiBlitz源用`sudo shutdown -r now`。

如果准备好以上所有内容，请使用新的SD卡开始设置新的RaspiBlitz（如自述文件中所述） - 可以确定硬盘上没有区块链数据 - 只需按照设置进行操作即可。当你到达设置点“获取区块链”时，选择COPY选项。从RaspiBlitz的1.0版本开始，这将为您提供有关如何将区块链数据传输到RaspiBlitz的更详细说明。简而言之：在具有区块链数据源的计算机上，您将执行SCP命令，该命令将通过本地网络将数据复制到RaspiBlitz。

一旦你完成了所有的转移，Raspiblitz将对数据进行快速检查 - 但这并不能保证传输中的所有细节都可以。如果您遇到困难或查看价值低于90％的最终同步，请进一步查看常见问题解答。

**如果你想用这种方式替换损坏的区块链：** *转到终端 - 也许用CTRL + c。然后调用`/ home / admin / 50copyHDD.sh`使用显示的SCP命令复制新的区块链。全部复制后按ENTER键，脚本可以快速检查数据。然后重新启动`sudo shutdown -r now` *

## 如何从第二个硬盘克隆区块链？

在设置过程中，当您从空HDD开始时，您需要获得区块链的副本。可用的一个选项是将第二个HDD连接到RaspiBlitz，该RaspiBlitz已包含区块链数据并开始复制/克隆。

如果选择此选项，控制台会要求您连接第二个HDD并自动检测它：

！[SSH6b（图片/ ssh6b-copy.png）

您可以简单地使用另一台RaspiBlitz的硬盘驱动器，或者您自己准备一台硬盘驱动器：

* 使用exFAT格式化第二个硬盘（Windows和Mac上的availbale）
* 将索引的区块链复制到根文件夹“比特币”
* 当您的硬盘准备就绪时，您的文件夹比特币的内容应如下所示：

```
/比特币/块
/比特币/ chainstate
/比特币/索引
```

可选您还可以添加testnet数据：

```
/比特币/ testnet3 /块
/比特币/ testnet3 / chainstate
/比特币/ testnet3 /索引
```

要将第二个HDD连接到RaspiBlitz，建议使用Y电缆提供额外的电源（请参阅可选购物清单）。因为RaspiBlitz无法在没有额外电源的情况下运行2个HDD。如需额外电源，您可以使用电池组（如下图所示）或选择带有自己电源的外置硬盘。

！[ExtraPower（图片/ extrapower.png）

## 为什么我的“最终同步”需要这么长时间？

首先，如果你看到最终同步超过90％，你可以不时看到小幅增加 - 你应该没问题......这可能需要一些时间来赶上网络。只有当您在“获取区块链”中激活地选择“SYNC”选项时，最终同步低于90％才可以。如果你做了一个torrent，一个FTP或来自另一台计算机的副本，看到90％以下的东西出错了，设置过程忽略了你准备好的Blockchain并进行完全同步 - 这几乎可以永远在raspberryPi上。

因此，如果出现问题（如上所述），请从头开始重试。您需要重新启动硬盘才能重新启动：以管理员用户身份登录。使用CTRL + c中止最终同步信息以进入终端。运行`sudo /home/admin/XXcleanHDD.sh -all`并按照脚本删除HDD中的所有数据。当'sudo shutdown now`的时候finsihed掉电。然后从图像中制作一张新的SD卡，这次尝试另一种方法来获取区块链。如果您第二次遇到麻烦，请在GitHub上报告问题。

## 如何备份我的Lightning节点？

注意：如果备份不是最新的通道状态，则恢复备份可能会导致丢失所有通道资金。目前还没有针对闪电节点的完美备份解决方案 - 社区正在开发此主题。

但有一种安全的方法可以开始：将您的LND钱包种子（创建钱包时的单词列表）存放在安全的地方。它是恢复对您的连锁资金的访问权的关键 - 您的硬币不受活跃渠道的约束。

恢复活动通道中的硬币有点复杂。因为您必须确保您确实拥有频道状态数据的最新备份。问题是：如果您将频道的旧状态发布到网络，这看起来像是作弊的尝试，并且您的频道合作伙伴可以获得频道中的所有资金。

要真正拥有可靠的备份，这些功能需要成为LND软件的一部分。几乎所有其他解决方案都不会是完美的。这就是为什么RaspiBlitz目前不试图提供备份功能的原因。

但您可以尝试备份，风险自负。您的所有Lightning节点数据都在`/ mnt / hdd / lnd`目录中。只需在lnd服务停止时运行该数据的备份 - >`sudo systemctl stop lnd`然后在您的笔记本电脑上，您将终端放入要存储备份的目录中，并使用以下SCP命令下载：

`scp -r bitcoin @ [LOCAL-IP-OF-RASPIBLITZ]：/ mnt / hdd / lnd /./`使用你的密码A

如果你想恢复LND备份状态。制作一个新的RaspiBlitz（新的SD卡图像和一个干净的HDD），将其设置为准备好（你在LCD上看到状态屏幕）然后转到终端，用`sudo systemctl stop lnd`停止lnd服务删除内容使用`sudo rm -rf / mnt / hdd / lnd / *`的lnd数据目录。然后，在您的笔记本电脑位于同一目录中的终端中，您进行了备份（在那里列出了备份的lnd目录）运行以下SCP命令：

`scp -r ./lnd/* bitcoin @ [LOCAL-IP-OF-RASPIBLITZ]：/ mnt / hdd / lnd /`使用密码A

没有运行重启：`sudo shutdown -r now` ...重启后LND可能需要更长时间的重新扫描，但是你应该看到旧的通道和余额。

**请注意，如果备份是几个小时/几天，通道可能已被另一方关闭，可能需要一些时间，直到您看到资金回到链上。如果备份时间稍长，则频道对方可能已使用您的离线时间欺骗您使用旧状态。如果你的备份不是最新状态而且LND正在关闭频道，那么你也可能发生了一个旧的频道状态（被视为作弊），并且该频道的资金会因为惩罚而丢失。所以再次..这种备份方法可能有风险，请谨慎使用。**

## 这个助记符种子单词列表是什么？

通过LND在钱包创建时为您提供的24字列表，您可以恢复您的私钥（BIP 39）。你应该把它写下来并存放在保存的地方。

有关助记符种子的更多背景，请参阅此视频：https：//www.youtube.com/watch？v = wWCIQFNf_8g

## PASSWORD D如何影响种子这个词？

在钱包创建时，系统会询问您是否要使用其他密码保护您的单词种子列表。如果您选择这样，RaspiBlitz建议您此时使用您的PASSWORD D.

为种子单词使用附加密码是可选的。如果您选择这样，您将需要密码才能从您的种子词中恢复您的私钥。如果没有此密码，您的私钥将无法从种子词中恢复。因此，如果有人找到您写下的单词列表，密码会增加额外的安全层。

## 如何从失败的RaspiBlitz中恢复我的硬币？

您可能会遇到硬件出现故障或软件开始出现故障的情况。因此，您决定设置一个新的RaspiBlitz，就像上面“更新到新的SD卡发布”中的章节一样 - 但关闭频道和兑现不再有效。关于你在失败的设置中已有的资金怎么样？

还没有完美的方法来备份/恢复您的硬币，但您可以尝试以下方法来充分利用这种情况：

### 1）从钱包种子中恢复

还记得你在设置过程中写下的那24个单词吗？这就是你的“密码种子” - 现在这句话对于收回你的钱包非常重要。如果你不再拥有它们：跳过本章并阅读选项2.如果你仍然有密码：好，但请仔细阅读以下内容：

使用密码种子，您可以恢复LND为您管理的比特币钱包 - 但它不包含您打开的频道的所有详细信息 - 它只是您资金钱包的关键。如果您能够关闭所有频道或从未打开任何频道，那么一切正常，您可以继续。如果您在那里有资金的开放渠道，则需要考虑以下因素：

* 您现在依靠通道计数器部件强制关闭通道。如果他们这样做，硬币将在未来的某一点再次用于您的资金钱包 - 在强制关闭延迟之后。
* 如果您的频道反对部分从不强行关闭频道（因为它们也处于离线状态），您的频道资金可以永久冻结。

因此，以这种方式存在一个小风险，您将无法收回您的资金。但通常情况下，如果您的频道反对部分仍在线，请注意您不会再回到网上，并且他们在频道方面拥有一些资金：他们有动力强制关闭频道再次使用他们的资金。

所以如果你想用RaspiBlitz“从钱包种子中恢复”，这就是todo：

- 设置一个新的RaspiBlitz（新鲜的SD卡图像和干净的硬盘）。
- 在新的SetUp中，您可以创建LND钱包（请参见下图）。

！[SSH8（图片/钱包recover.png）

- 当你被问到“你有一个现有的密码钱包”这次回答“你好”时。
- 输入密码种子 - 一行中的所有单词用空格分隔
- 如果在最后询问密码D以加密您的密码种子，请使用与上次相同的密码。如果您最后一次没有输入，请再次按Enter键。
- 当被问及“地址预见”号码时 - 使用“250000”代替默认值！

然后给LND一些时间重新扫描区块链。最后，您将恢复您的资金钱包。您可能需要等待旧的通道计数器部件强制关闭旧通道，直到您看到显示的硬币。

*重要提示：如果您在从种子恢复后看到连锁资金的零余额...请参阅[此处]（https://github.com/rootzoll/raspiblitz/issues/278）讨论的详细信息 - 您可以尝试设置新鲜这次有更大的前瞻数字。*

### 2）LND信道状态备份

第二种选择风险非常大，可能导致资金全部流失。如果你仍然可以访问失败的RaspiBlitz的硬盘内容，它就可以工作了。只有在您丢失了上述选项的密码种子，忘记了密码种子加密密码或者您的旧频道计数器部分也处于脱机状态时，才应该使用它。

你做的是原则：
- 制作HDD目录`/ mnt / hdd / lnd`的副本
- 设置一个新的RaspiBlitz
- 用`sudo systemctl stop lnd`停止LND
- 用你的备份版本替换新的`/ mnt / hdd / lnd`
- 确保`/ mnt / hdd / lnd`中的所有内容都归比特币所有：比特币
- 重新启动RaspiBlitz

这是高度实验性的。并再次说明：如果您使用不代表最新频道状态的备份恢复LND，这将触发闪电“惩罚”机制 - 允许您的频道计数器部分从频道获取所有资金。它是万不得已的措施。但如果它为你工作，请告诉我们。

## 如何更改闪电节点的名称/别名

使用主菜单中的“更改节点的名称/别名”选项。 RaspiBlitz将在此之后重新启动。

## 在SSH上做什么我看到“警告：远程主机识别已经改变！”

这意味着，RaspiBlitz的公共ssh密钥已更改为您在该IP下最后一次登录的密钥。

在更新期间发生这种情况是可以的 - 当您更改SD卡图像时。如果它真的发生了 - 请检查您的本地网络设置一秒钟。也许您的RaspiBlitz的本地IP发生了变化？是否连接了第二个RaspiBlitz？这是一个安全警告，所以至少需要一些时间来检查是否有什么奇怪的。但也不要惊慌 - 当它在你的本地网络中时，通常它是一些网络的东西 - 而不是入侵者。

要解决此问题并且能够再次使用SSH登录，您必须从本地客户端计算机中删除该IP的旧公钥。只需运行以下命令（使用RaspiBlitz的替换IP）：`ssh-keygen -R IP-OF-YOUR-RASPIBLITZ`或从known_hosts文件中手动删除此IP的行（请参阅该文件的路径）警告信息）。

之后，您应该能够再次使用SSH登录。

## 使用自动解锁时，我会失去多少安全保障？

一般来说，“钱包锁定”的想法是您的私钥/种子/钱包以加密的方式存储在您的硬盘上。每次重启时，您必须手动输入密码（解锁钱包），以便LND可以再次读取和写入加密的钱包。如果您的RaspiBlitz被盗或被带走，这会提高您的安全性 - 它会断电，然后您的钱包就安全了 - 攻击者无法访问您的钱包。

当您激活RaspiBlitz的“自动解锁”功能时，钱包的密码将存储在RaspiBlitz上。因此，如果攻击者在物理上窃取RaspiBlitz，现在他们可以找到密码并解锁钱包。

## 我连接了我的硬盘但它仍然在显示屏上显示“连接硬盘”？

您的硬盘可能还没有分区。以管理员身份SSH进入RaspiBlitz（请参阅显示的命令和密码），您应该可以选择创建分区。如果不是这样的话：

检查/更换USB电缆。将HDD连接到另一台计算机并检查它是否完全显示。

OSX：https：//www.howtogeek.com/212836/how-to-use-your-macs-disk-utility-to-partition-wipe-repair-restore-and-copy-drives/

Windows：https：//www.lifewire.com/how-to-open-disk-management-2626080

Linux / Ubuntu（桌面）：https：//askubuntu.com/questions/86724/how-do-i-open-the-disk-utility-in-unity

Linux / Raspbian（命令行）：https：//www.addictivetips.com/ubuntu-linux-tips/manually-partition-a-hard-drive-command-line-linux/

## 如何缩小QR码以连接我的Shango / Zap手机？

使字体变小，直到QR码适合您的（全屏）终端。在OSX中使用`CMD` +`-`键。在LINUX中使用`CTRL` +`-`键。在WINDOWS Putty上进入设置并更改字体大小：https：//globedrill.com/change-font-size-putty

## 为什么显示屏上的比特币IP是红色的？

当RaspiBlitz检测到它无法从外部到达比特币节点的端口时，比特币IP为红色。这意味着比特币节点可以与其他比特币节点对等，但其他比特币节点无法启动与您的对等。别担心，您不需要可公开访问的比特币节点来运行（公共）闪电节点。但是，如果要更改此设置，则需要将路由器上的端口8333转发到RaspiBlitz。如何做到这一点在每个路由器上都是不同的。

## 为什么显示屏上的节点地址为红色？

当RaspiBlitz检测到它无法从外部到达LND节点的端口时 - 当设备位于路由器的NAT或防火墙后面时，节点地址为红色。您的节点无法公开访问。这意味着您可以与其他公共节点对等+ openChannel，但其他节点不能与您对等+ openChannel。要更改此设置，您需要将路由器上的端口9735转发到RaspiBlitz。如何做到这一点在每个路由器上都是不同的。

## 为什么我的节点在显示屏上的地址为黄色（不是绿色）？

黄色没关系。 RaspiBlitz可以检测到它可以到达公共IP的端口9735上的服务 - 这在大多数情况下是RaspiBlitz的LND。但RaspiBlitz无法100％肯定地检测到这是该端口上自己的LND服务 - 这就是为什么它只是黄色而不是绿色。

## 我可以将RaspiBlitz作为BTCPayServer的Backend运行吗？

BTCPay服务器是您自己的支付处理器的解决方案，可以为您的在线商店接受Lightning Payments：https：//github.com/btcpayserver/btcpayserver

您可以在此处找到实验设置的设置说明：https：//goo.gl/KnTzLu

感谢@RobEdb（在Twitter上询问更多详情）与RaspiBlitz一起运行他的演示商店：https：//store.edberg.eu  - 买一张[他和安德烈亚斯]的照片（https://store.edberg.eu/produkt / jag-andreas /）:)

## 我的笔记本电脑上没有LAN端口 - 如何连接到我的RaspiBlitz？

只要您可以通过WLAN连接到RaspiBlitz连接到的同一个LAN路由器/交换机，您就不需要笔记本电脑上的LAN端口。您在同一个本地网络上。

## 是否可以通过Wifi连接Blitz而不是使用LAN电缆？

建议使用LAN电缆，因为它可以减少网络连接端可能出现的错误来源。但是，当您没有LAN-Router / Switch时，如何设置WLAN，请参见此处：
https://github.com/Stadicus/guides/blob/master/raspibolt/raspibolt_20_pi.md#prepare-wifi

## 我可以直接将RaspiBlitz连接到笔记本电脑吗？

如果您的笔记本电脑上有LAN端口 - 或者您有USB-LAN适配器，则可以直接将RaspiBlitz（没有路由器/交换机）连接到笔记本电脑并共享WIFI Internet连接。您可以按照[OSX指南]（https://medium.com/@tzhenghao/how-to-ssh-into-your-raspberry-pi-with-a-mac-and-ethernet-cable-636a197d055）进行操作。

简而言之，OSX：

* 确保所有VPN都关闭（可能会干扰本地LAN）
* 直接连接局域网
* 设置>共享/ Freigaben>激活从WLAN到以太网的“互联网共享”
* 设置>网络>以太网适配器>设置为DHCP
* 在终端>`ifconfig`那里你应该是bridge100的IP
* 在终端>`arp -a`中检查客户端到网桥的IP
* 在终端> ssh admin @ [clientIP]

如果有人在Linux / Win中执行此操作，请分享。

## 如何在没有SSH的情况下安全地拔出/关闭

如果硬盘正好在写入过程中，那么从RaspiBlitz断电可能会导致数据损坏。最安全的方法是始终通过SSH连接到RaspiBlitz并使用主菜单中的“POWER OFF”选项。

但是，如果无法使用SSH登录并且您需要先关闭电源，至少先拆除局域网电缆（网络连接）一段时间（大约10-30秒 - 直到您看不到硬盘上没有闪烁的灯光），然后拔下电源线。如果在这种情况下数据损坏，这应该将风险降至最低。

## 如何在主分支之外构建SD卡？

开发中可能还有一个尚未发布的新功能尚未在主分支中 - 但您想尝试一下。

要从另一个分支而不是主分支构建SD卡映像，请按照README中的[构建SD卡映像]（README.md＃build-the-sd-card-image），但从另一个分支执行构建脚本，将该分支的名称添加为构建脚本的参数。

例如，如果要从“dev”分支进行构建，请执行以下命令：

`wget https://raw.githubusercontent.com/rootzoll/raspiblitz/dev/build_sdcard.sh&& sudo bash build_sdcard.sh'dev'`

## 如何从我的分叉GitHub Repo构建SD卡？

如果您分叉RaspiBlitz repo（非常欢迎）并且您希望在RaspiBlitz上运行该代码，有两种方法可以做到这一点：

* 快速方法：对于脚本中的小变化，在运行的RaspiBlitz上转到`/ home / admin`，用`sudo rm -r raspiblitz`删除旧的git然后用你的代码`git clone [YOURREPO]`替换它。 /家/管理/ XXsyncScripts.sh`

* 好的方法：如果您想安装/删除/更改服务和系统配置，您需要使用自己的代码构建SD卡。从README中的[Build the SD Card Image]（README.md＃build-the-sd-card-image）中进行准备，但最后运行命令：

`wget https://raw.githubusercontent.com/[GITHUB-USERNAME]/raspiblitz/[BRANCH]/build_sdcard.sh&& sudo bash build_sdcard.sh [BRANCH] [GITHUB-USERNAME]

如果您正在使用forked repo并希望使用最新的repo更改更新RaspiBlitz上的脚本，请运行`/ home / admin / XXsyncScripts.sh`  - 只要您不对sd卡构建进行更改即可脚本 - 然后你需要再次从你的仓库建立一个新的SD卡。

## 如何将RaspberryPi连接到硬盘？

有多种方法可以做到 - 只要记住它应该很容易到达SD卡插槽以移除和更换卡。

以下是使用[Hook-and-loop fastener]（https://en.wikipedia.org/wiki/Hook-and-loop_fastener）磁带的示例：

！[ExtraPower（图片/ befestigung.jpg）

## 我还有哪些其他案例选择？

您可以使用名为“Lightning Shell”的RaspiBlitz打印的自定义3D替换购物清单中的通用案例 -  @CryptoCloaks的精彩作品

https://thecryptocloak.com/product/lightningshell/

！[LightningShell（图片/ lightningshell.png）

此回购中还有第一个免费的3D开源文件，位于`case.3dprint`目录中，您可以进行自我打印。那些比'Lightning Shell'简单得多，还没有完成。但随意尝试和改进 -  PullRequests欢迎。

## 那些“欠压检测”警告是否有问题？

当用于RaspiBlitz的USB电源适配器功率过低时，显示屏上会很快显示“欠压检测”（欠压）信息。如果你看到那些只有一两次不合适，但可以在宽容的窗口。不过请确保您的USB电源适配器至少可以提供3A。如果您仍然看到这些警告，可能只为HDD提供第二个USB电源适配器并通过Y型电缆为HDD供电 - 请参阅https://en.wikipedia.org/wiki/Y-cable#USB

## 为什么我们需要下载区块链而不同步它？

RaspiBlitz由RaspberryPi提供支持。 SingleBoardComputer的处理能力太低，无法在设置过程（验证）期间从比特币对等网络快速同步区块链。要同步和索引完整的区块链可能需要数周甚至更长时间。这就是RaspiBlitz需要从其他来源下载准备好的区块链的原因。

## 使用perpared SD卡图像是否安全？

使用预先构建的软件几乎总是将信任转移到制作二进制文件的人身上。但是如果下载的图像真的是GitHub Repo提供的图像，那么至少你可以在下载后检查SHA校验和。为此，请快速检查您的浏览器是否确实位于正确的GiutHub页面中，并且您的GitHub页面的HTTPS是否由“DigiCert”签名。然后将SHA-256字符串（总是在README上图像的下载链接旁边）与命令`shasum -a 256 [DOWNLOADED-FILE-TO-CHECK]`（Mac / Linux）的结果进行比较。这仍然不是最优的，如果社区中至少有一些人要求它，我会考虑将下载作为未来的作者签名。

最好的方法是自己制作SD卡。你使用脚本`build_sdcard.sh`。花几分钟时间检查一下您是否在该构建脚本中看到任何可疑内容，然后按照[README]（README.md＃build-the-sd-card-image）进行操作。

## 从第三方下载区块链是否安全？

从第三方（torrent / ftp）下载区块链并不是最佳选择，对于未来的廉价和强大的SingleBoardComputers，我们可以摆脱这个“补丁”。

下载的区块链已预先编入索引并预先验证。这应该是足够安全的，因为如果用户获得“操纵”的区块链，它将在设置后不起作用。下载的区块链的开头需要适合创世块（在bitcoind软件中），并且下载的区块链的末端不需要与比特币网络状态的其余部分匹配 - 在对等2网络网络中需要分配的新区块的哈希值匹配下载的区块链头。因此，如果你下载了一个被操纵的区块链，它只是在实践中不起作用。只要你没有处于一个完全敌对的环境中，有人能够伪造整个同行和矿工的网络 - 这足以安全地运行一个资金不足的完整节点来试用闪电网络。

如果您不相信下载或者您希望在更多生产环境中运行RaspiBlitz（风险自负），请不要使用torrent / ftp下载并选择从更强大的计算机复制区块链数据的选项（笔记本电脑或台式机）您可以自己同步，验证和索引区块链 - 有关详细信息，请参阅[自述文件]（README.md＃4-copies-from-another-computer）。

## 什么是“基础洪流文件”？

受网站getbitcoinblockchain.com的启发，我们使用他们的一个基本torrent文件来拥有一组基本的块 - 这些将来不会改变。此torrent包含大部分数据（大文件），我们不需要长时间更改torrent。通过这种方式，洪流可以建立广泛的播种种子，洪流网络可以承受沉重的负担。

目前（Baseiteration = 1）这只是比特币blk和rev文件到数字：
- / blocks：01390
- / testnet3 / blocks：00152

对于litecoin（Baseiteration = 1），它的blk和rev文件最多为数字：
- / blocks：00124

基本torrent文件应始终具有以下命名方案：

`raspiblitz- [CHAINNETWORK] [BASEITERATIONNUMBER]  -  [YEAR]  -  [月]  -  [DAY] -base.torrent`

因此，例如，在2018-10-31创建的Litecoin基础洪流的第二个版本将具有此名称：raspiblitz-litecoin2-2018-10-31-base.torrent

## 什么是“更新Torrent文件”以及如何创建它？

所有其余文件都打包成第二个torrent文件。此文件将更频繁地更新。播种预计不会那么好，下载可能会慢一点，但这没关系，因为它是一个小得多的文件。

这样就可以在良好的播种和最新的区块链之间取得良好的平衡。

要创建Update Torrent文件，请执行以下步骤...

在RaspiBlitz上有一个几乎100％同步的bitcoind MAINNET，txindex = 1
（从此节点中删除所有资金 - 因为区块链被搞乱了）

停止bitcoind：
```
sudo systemctl停止bitcoind
```

删除基础洪流blk文件：
```
sudo rm /mnt/hdd/bitcoin/blocks/blk00*.dat
sudo rm /mnt/hdd/bitcoin/blocks/blk0{1000..1390}.dat
```

删除基本种子rev文件：
```
sudo rm /mnt/hdd/bitcoin/blocks/rev00*.dat
sudo rm /mnt/hdd/bitcoin/blocks/rev0{1000..1390}.dat
```

现在更改到您打包torrent文件的计算机，并将三个目录转移到torrent基目录（应该是您当前的工作目录）：
```
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / blocks ./blocks
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / chainstate ./chainstate
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / indexes ./indexes
```

在RaspiBlitz上还有一个几乎100％同步的bitcoind TESTNET，txindex = 1

停止bitcoind：
```
sudo systemctl停止bitcoind
```

删除基础洪流blk文件：
```
sudo rm /mnt/hdd/bitcoin/testnet3/blocks/blk000*.dat
sudo rm /mnt/hdd/bitcoin/testnet3/blocks/blk00{100..152}.dat
```

删除基本种子rev文件：
```
sudo rm /mnt/hdd/bitcoin/testnet3/blocks/rev000*.dat
sudo rm /mnt/hdd/bitcoin/testnet3/blocks/rev00{100..152}.dat
```

现在再次更改到您的计算机，在那里打包torrent文件并将三个目录传输到torrent基目录（应该是您当前的工作目录）：
```
mkdir testnet3
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / testnet3 / blocks ./testnet3/blocks
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / testnet3 / chainstate ./testnet3/chainstate
scp -r bitcoin @ [RaspiBlitzIP]：/ mnt / hdd / bitcoin / testnet3 / indexes ./testnet3/indexes
```

（重新）将“torrent base directory”命名为与torrent UPDATE文件本身相同的名称（没有.torrent结尾）。更新torrent文件应始终具有以下命名方案：

`raspiblitz- [CHAINNETWORK] [BASEITERATIONNUMBER]  -  [YEAR]  -  [月]  -  [DAY] -update.torrent`

*例如，在2018-12-24为litecoin创建的更新torrent是对第二个基本torrent版本的更新将具有此名称：raspiblitz-litecoin2-2018-12-24-update.torrent *

现在打开你的torrent客户端（例如qTorrent for OSX）并创建一个新的torrent文件，将新重命名的“torrent base directory”作为源目录。

将此跟踪器列表添加到您的torrent并开始播种（在三个单个跟踪器之间保持空闲/空行）：
```
UDP：//tracker.justseed.it：1337

UDP：//tracker.coppersurfer.tk：6969 /公布

UDP：//open.demonii.si：1337 /公布

UDP：//denis.stalker.upeer.me：6969 /公布
```

成功创建torrent文件后：
* 复制到`/ home.admin / assets`
* 推动掌握
* 更改`50torrentHDD.sh script`
* 添加到Torrent- [RSS]（https://github.com/rootzoll/raspiblitz/issues/285#issuecomment-457796120）
* 种子在家里和像justseed.it这样的服务
* 更新[问题]（https://github.com/rootzoll/raspiblitz/issues/285#issuecomment-457796120）并在twitter上询问有关播种的帮助

## 创建新的SD卡映像的过程是什么？

生成新SD卡映像的过程的工作节点：

* 在构建计算机上从USB记忆棒启动`Ubuntu LIVE`（启动时按F12键）
* 连接安全WIFI（硬件开关）
* 从[raspberrypi.org]（https://www.raspberrypi.org/downloads/raspbian/）下载最新的Raspbian Desktop（无推荐软件）到NTFS格式的数据U盘
* 打开终端并比较校验和`shasum -a 256 / media / ubuntu / ... [DOWNLOADED-RASPBIAN]
* 在NTFS U盘上使用文件管理器上下文`extract here`解压缩
* 使用8GB SD卡连接SD卡读卡器
* 在img文件`write image`上的文件管理器上下文中使用写入sd卡
* 在`boot`驱动器可用空间`在终端`中打开文件管理器上下文中使用
* 运行命令`touch ssh`
* 关闭终端并弹出`boot`
* 将RaspiBlitz（无硬盘）连接到网络，插入SD卡并打开电源
* 如果RaspiBlitz（arp -a或检查路由器）找到IP
* 在终端`ssh pi @ [IP-OF-RASPIBLITZ]`
* 密码是`raspberry`
* `wget https://raw.githubusercontent.com/rootzoll/raspiblitz/master/build_sdcard.sh&& sudo bash build_sdcard.sh`
* 检查输出是否有警告/错误 - 安装LCD
* 使用`ssh admin @ [IP-OF-RASPIBLITZ]`（pw：raspiblitz）登录并运行`./ XXprepareRelease.sh`
* 在构建笔记本电脑上关闭Wifi（硬件关闭）并关闭
* 删除`Ubuntu LIVE` USB记忆棒并替换为`Ubuntu AIRGAP`
* PowerOn Build Laptop（按F12键启动菜单）
* 削减RaspiBlitz的力量，删除SD卡并与SD卡读卡器连接以构建笔记本电脑
* 在Filemenager NTFS中连接并打开 - 白色scace上的上下文 - >打开终端
* 运行`df`来检查SD卡读卡器设备名称
* `sudo dd if = / dev / [sdcarddevice] | gzip> ./ raspiblitz-vX.X -YEAR-MONTH-DAY.img.gz`
* 从NTFS删除所有IMG文件（只保留zips / gzs）
* 白色空间上下文，`在终端打开`，运行`shasum -a 256 [NEW-ZIP]> sha256.txt`
* [未来的作者在这里使用airgap build machine的工具签名]
* 关机构建计算机
* 将NTFS USB记忆棒连接到MacOS（只读它）
* 检查文件是否可以在OSX上解压缩
* 使用新图像运行测试
* 将新图像上传到下载服务器
* 将SHA256-String复制到GutHub README并更新downloadlink

## 我可以在RaspberryPi以外的其他计算机上运行RaspiBlitz吗？

这个GitHub中有一个实验部分试图为其他SingleBoardComputers构建。随意尝试并分享您的经验：[dietpi / README.md]（dietpi / README.md）

## 我可以翻转屏幕吗？

对于默认的3.5“LCD，您需要编辑/boot/config.txt。运行`sudo nano / boot / config.txt`
到最后寻找“dtoverlay = tft35a：rotate = 270”这一行。要以180度翻转屏幕，将线路更改为“dtoverlay = tft35a：rotate = 90”并使用“sudo reboot”重新启动。参考：https：//github.com/goodtft/LCD-show/issues/34

## 如何设置新鲜/清除/重置而不进入恢复模式？

当您使用新的/干净的RaspiBlitz映像放入SD卡时，RaspiBlitz将进入恢复模式，因为它检测到HDD上的旧数据并假设您只想继续使用此数据。

但是可能有些情况下你想从一开始就开始一个完全新鲜/干净的RaspiBlitz。为此，您需要从HDD中删除旧数据。您可以通过在另一台计算机上格式化（例如使用FAT并将其命名为“NEW”）来完成此操作。或者，当您可以在终端上运行脚本“/home/admin/XXcleanHD.sh -all”时。

当硬盘清洁时，然后刷新一个新的RaspiBlitz SD卡，你的设置应该重新开始。

## 我的区块链数据已损坏 - 我该怎么办？

您可以尝试重新编制索引，但这可能需要很长时间 - 多天甚至数周。但还有其他选择：

1. 从另一台计算机复制区块链

您可以删除旧区块链并获取新区块链。请参阅常见问题解答：[我在另一台计算机上拥有完整的区块链。如何将其复制到RaspiBlitz？]（FAQ.md #i-have-the-blockchain-on-another-computer-how-do-copy-it-to-raspiblitz）。即使您无法删除数据，也请先重命名不可删除的文件夹，然后按照说明进行操作。

2. Re-Torrent下载准备好的Blockchain

你也可以开始一个新的Torrent-Download并在完成后用新的下载替换旧的区块链。转到终端并运行脚本`/ mnt / hdd / 50torrentHDD.sh`

3. 备份LND数据，制作新的闪电战，重播LND数据

您可以备份您的频道和钱包数据，制作一个完整的新RaspiBlitz，然后在设置之后，用旧的替换LND数据。还要确保再次检查电源 - 它需要提供等于或大于3A的电流，并且应提供稳定的电流。如果您认为您的硬盘或SD卡质量下降 - 也许这是更换的好时机。请参阅常见问题解答：[如何从失败的RaspiBlitz中恢复我的硬币？]（FAQ.md＃how-can-i-recover-my-coins-from-a-failed-raspiblitz）*
