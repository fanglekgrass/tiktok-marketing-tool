# DMIT VPS使用指南：购买、流量计费、设置Root密码及快照管理

DMIT 的全新管理后台采用了现代化的 UI 设计，使后台操作更加便捷。用户可以轻松完成 VPS 的重装系统、Root 密码设置、SSH 密钥管理、查看流量情况以及服务器续费等操作。本文将为您详细讲解这些功能的使用步骤。

## 1、DMIT 官网

👉 [【推荐收藏】2025年 DMIT 最新优惠活动整理汇总 - 每日更新可用优惠套餐](https://bit.ly/dmit_coupon)

DMIT 的官网提供了统一的入口，用户可使用官网访问管理后台，进行多种操作。请确保使用最新版本的浏览器以获得最佳体验。

## 2、关于流量计费政策

DMIT 针对部分套餐（如 HKG.T1 和 SJC.T1）实施了单向流量计费策略，该策略正式启用，并将根据流入（IN）和流出（OUT）流量的最大值(MAXBANDWIDTH)进行计费。

### 官方解释：
- 流入流量 (IN) 和流出流量 (OUT) 将实时统计；
- 系统会从两个数值中取最大值，作为实际计费流量；
- 如果出现流量统计偏差，请不要担心，该策略不会减少您的可用额度；
- 超额流量用户将根据对应套餐的策略（降速或暂停）调整服务。

以下是主要套餐的流量计费特点：
1. **PVM.HKG.T1.STARTER套餐**：采用单向流量计费，流量超额后降速。
2. **PVM.LAX.sPro.CREATOR套餐**：双向流量计费，流量不足将暂停服务。
3. **PVM.HKG.Pro套餐**：双向计费，流量超量后同样会暂停服务。

> 提示：每个套餐可能有不同的计费细则，请登录后台了解套餐详情。

## 3、SSH 密钥及 Root 密码设置教程

DMIT 提供了便捷的 Root 密码设置和 SSH 密钥管理功能。无论是您偏爱通过密钥登录还是密码登录，以下是设置步骤的详细说明。

### 密钥登录官方文档
DMIT 提供了相应的官方教程：[查看官方文档](https://www.dmit.io/knowledgebase.php)。

### 如何设置 Root 密码
#### 方法 1：命令行操作
1. 使用 `passwd` 命令设置新密码。
2. 修改 SSH 配置，允许 Root 密码登录：
   bash
   sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/g' /etc/ssh/sshd_config
   sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/g' /etc/ssh/sshd_config
   sudo service sshd restart
   
3. 重新启动服务器：
   bash
   reboot
   

#### 方法 2：编辑配置文件
1. 切换至 Root 身份（DMIT VPS 默认以 Root 身份登录）。
2. 编辑 SSH 配置文件：
   bash
   nano /etc/ssh/sshd_config
   
3. 确保以下两行未被注释，并设置为 `yes`：
   
   PermitRootLogin yes
   PasswordAuthentication yes
   
4. 保存变更后，重新启动 SSH 服务并重启服务器。

> 注意：服务器默认 Root 密码仅用于控制台登录。若需 SSH 登录，请完成上述配置，并重启完成生命周期。

## 4、快照功能

DMIT 目前为每台 VPS 提供 1 个免费的快照功能。您可以通过后台随时创建快照，用于数据备份或系统状态的还原。这一功能非常适合在重大配置更改或软件更新前使用。

## 5、如何重装系统

在管理后台，DMIT 提供了多种系统模板（如 Linux 发行版和 Windows 版本），以满足用户的不同需求。例如，您可以选择 Debian、Ubuntu、CentOS 等主流系统。

操作步骤：
1. 登录后台管理界面；
2. 选择服务器，点击“重装系统”；
3. 从可用列表中选择所需系统版本并确认；
4. 等待系统安装完成。

> 提示：重装系统会清除当前所有数据，请提前备份重要资料。

## 6、账单续费指南

如果需要恢复或续费您的服务器租期，在后台账单管理处可以一键完成续费操作：
1. 登录后台，进入账单页面；
2. 找到需续费的服务器服务项；
3. 点击“恢复续费”按钮完成操作。

## 7、洛杉矶 PVM.LAX.Pro 套餐线路特点

DMIT 的洛杉矶 CN2 GIA 专业套餐提供了高速稳定的中国大陆优化线路，非常适合对网络延迟要求较高的用户。其线路优化配置如下：
- **电信线路**：去程 GIA(AS4809)，三网回程均为 GIA。
- **联通线路**：去程直连 AS4837。
- **移动线路**：去程连接香港移动 AS58453。

这一网络配置可以最大限度地减少延迟，为用户提供更好的使用体验。