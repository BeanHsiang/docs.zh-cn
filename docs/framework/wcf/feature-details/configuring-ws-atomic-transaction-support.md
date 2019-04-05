---
title: 配置 WS-Atomic 事务支持
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF], configuring WS-Atomic Transaction
ms.assetid: cb9f1c9c-1439-4172-b9bc-b01c3e09ac48
ms.openlocfilehash: bc21cba7889652a8b485d101205b15d6f189d12d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54592427"
---
# <a name="configuring-ws-atomic-transaction-support"></a>配置 WS-Atomic 事务支持
本主题介绍如何通过 WS-AT 配置实用工具来配置 WS-AtomicTransaction (WS-AT) 支持。  
  
## <a name="using-the-ws-at-configuration-utility"></a>使用 WS-AT 配置实用工具  
 WS-AT 配置实用工具 (wsatConfig.exe) 用于配置 WS-AT 设置。 为了启用 WS-AT 协议服务，必须使用该配置实用工具为 WS-AT 配置 HTTPS 端口，将 X.509 证书绑定到该 HTTPS 端口，并通过指定证书主题名称或指纹来配置授权的合作伙伴证书。 通过该配置实用工具，还可以选择跟踪模式，设置默认的外发事务超时和最大传入事务超时。  
  
 使用“组件服务”管理控制台中的 Microsoft 管理控制台 (MMC) 属性页管理单元，或者在命令行窗口中，都可访问此工具的功能。 通过命令行窗口配置本地计算机上的 WS-AT 支持；使用 MMC 管理单元配置本地和远程计算机上的设置。  
  
 在 Windows SDK 安装位置“%WINDIR%\Microsoft.NET\Framework\v3.0\Windows Communication Foundation”中，可访问命令行窗口。  
  
 有关命令行工具的详细信息，请参阅[WS-AtomicTransaction 配置实用工具 (wsatConfig.exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)。  
  
 如果正在[!INCLUDE[wxp](../../../../includes/wxp-md.md)]或[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]，可以通过导航到访问 MMC 管理单元**控件面板 / 管理工具 / 组件服务**，右击**我的电脑**，和选择**属性**。 Microsoft 分布式事务处理协调器 (MSDTC) 也可以在这个位置配置。 选项可用于配置下进行分组**WS-AT**选项卡。如果运行的 Windows Vista 或[!INCLUDE[lserver](../../../../includes/lserver-md.md)]，MMC 管理单元可通过单击**启动**按钮，然后输入`dcomcnfg.exe`中**搜索**框。 当 MMC 打开后时，导航到**我 Computer\Distributed 事务 Coordinator\Local DTC**节点，右键单击并选择**属性**。 选项可用于配置下进行分组**WS-AT**选项卡。  
  
 有关管理单元的详细信息，请参阅[WS-AtomicTransaction 配置 MMC 管理单元](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)。  
  
 若要启用该工具的用户界面，必须首先注册 WsatUI.dll 文件，该文件位于以下路径下  
  
 %PROGRAMFILES%\Microsoft SDKs\Windows\v6.0\Bin  
  
 若要注册产品，请在“命令提示”窗口中执行以下命令：  
  
 `regasm.exe /codebase WsatUI.dll`  
  
## <a name="enabling-ws-at"></a>启用 WS-AT  
 若要使用端口 443 和带私钥的 X.509 证书（已安装在本地机器存储区中）在 MSDTC 内启用 WS-AT 协议服务，请使用 wsatConfig.exe 工具执行以下命令。  
  
 `WsatConfig.exe –network:enable –port:8443 –endpointCert:<machine|"Issuer\SubjectName"> -accountsCerts:<thumbprint|"Issuer\SubjectName"> -restart`  
  
 将相应的参数替换为与环境相关的值。  
  
 若要在 MSDTC 内禁用 WS-AT 协议服务，请使用 wsatConfig.exe 工具执行以下命令。  
  
 `WsatConfig.exe –network:disable -restart`  
  
## <a name="configuring-trust-between-two-machines"></a>在两台计算机之间配置信任  
 WS-AT 协议服务要求管理员显式授权各个帐户参与分布式事务。 如果您是两台计算机的管理员，可以按以下方式配置两台计算机以建立相互信任关系：在两台计算机之间交换正确的证书集，将这些证书安装到相应的证书存储区，然后使用 wsatConfig.exe 工具将每台计算机的证书添加到对方的授权参与者证书列表中。 若要在两台计算机之间使用 WS-AT 执行分布式事务，则必须执行此步骤。  
  
 下面的示例概述了在两台计算机 A 和 B 之间建立信任关系的步骤。  
  
### <a name="creating-and-exporting-certificates"></a>创建和导出证书  
 此过程需要使用 MMC“证书”管理单元。 打开“开始”/“运行”菜单，并在输入框中输入“mmc”，然后按“确定”可访问该管理单元。 然后，在**Console1**窗口中，导航到**文件/添加 / 删除**管理单元中，单击添加，然后选择**证书**从**不可单独使用管理单元**列表。 最后，选择**计算机帐户**来管理和单击**确定**。 **证书**节点会显示在管理单元控制台。  
  
 必须拥有必需的证书才能建立信任。 若要了解如何创建和安装新证书下面的步骤之前，请参阅[如何：创建并在开发过程中在 WCF 中安装临时客户端证书](https://go.microsoft.com/fwlink/?LinkId=158925)。  
  
1.  在计算机 A 上，使用 MMC“证书”管理单元将现有证书 (certA) 导入 LocalMachine\MY（“个人”节点）和 LocalMachine\ROOT 存储区（“受信任的根证书颁发机构”节点）。 若要将证书导入特定的节点，右键单击节点并选择**所有任务/导入**。  
  
2.  在计算机 B 上，使用 MMC“证书”管理单元创建或获取带私钥的证书 certB，并将其导入 LocalMachine\MY（“个人”节点）和 LocalMachine\ROOT 存储区（“受信任的根证书颁发机构”节点）。  
  
3.  如果 certA 的公钥还未导出到文件，则完成此操作。  
  
4.  如果 certB 的公钥还未导出到文件，则完成此操作。  
  
### <a name="establishing-mutual-trust-between-machines"></a>在两台计算机之间建立相互信任  
  
1.  在计算机 A 上，将 certB 的文件表示形式导入 LocalMachine\MY 和 LocalMachine\ROOT 存储区。 这表明计算机 A 信任 certB 与之通信。  
  
2.  在计算机 B 上，将 certA 的文件表示形式导入 LocalMachine\MY 和 LocalMachine\ROOT 存储区。 这表示计算机 B 信任 certA 与之通信。  
  
 完成这些步骤之后，即在两台计算机之间建立了信任，这时，就可以将它们配置为使用 WS-AT 相互通信。  
  
### <a name="configuring-msdtc-to-use-certificates"></a>配置 MSDTC 使用证书  
 由于 WS-AT 协议服务既作为客户端又作为服务器，因此它必须侦听传入连接和发起传出连接。 因此，需要对 MSDTC 进行配置，以使它知道在与外部各方通信时要使用哪个证书，在接受传入通信时要授权哪个证书。  
  
 可以使用 MMC WS-AT 管理单元进行这一配置。 有关此工具的详细信息，请参阅[WS-AtomicTransaction 配置 MMC 管理单元](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)主题。 下面的步骤介绍如何在运行 MSDTC 的两台计算机之间建立信任。  
  
1.  配置计算机 A 的设置。 对于"终结点证书"，选择 certA。 对于"授权的证书"，选择 certB。  
  
2.  配置计算机 B 的设置。 对于"终结点证书"，选择 certB。 对于"授权的证书"，选择 certA。  
  
> [!NOTE]
>  当一台计算机向另一台计算机发送消息时，发送方尝试验证接收方证书的主题名称和接收方计算机的名称是否匹配。 如果不匹配，则证书验证失败，并且两台计算机无法通信。  
>   
>  对于加入域的计算机，该名称为完全限定域名。 默认情况下，工作站中的计算机名称就是计算机的 NetBIOS 名称。 但是，对于两台计算机之间所用的连接，如果存在域名系统 (DNS) 后缀，则名称中还可包含 DNS 后缀。  
>   
>  如果计算机的名称更改，例如，当工作组计算机加入域时，必须重新颁发证书或手动配置 DNS 后缀。  
  
## <a name="security"></a>安全性  
 由于某些与 MSDTC 和 WS-AT 关联的设置分别存储在注册表的 HKLM\Software\Microsoft\MSDTC 和 HKLM\Software\Microsoft\WSAT 下面，因此，请确保这些注册表项得到了保护，只有管理员才能写入这些项。 在注册表编辑器工具中，右键单击你想要保护和选择的项**权限**设置适当的访问控制。 对于系统的安全性和完整性而言，重要的项对于低权限用户只读至关重要。  
  
 部署 MSDTC 时，管理员必须确保任何 MSDTC 数据交换都是安全的。 在工作组部署中，应将事务基础结构与恶意用户隔离；而在群集部署中，应保护群集注册表。  
  
## <a name="tracing"></a>跟踪  
 WS-AT 协议服务支持集成在一起，事务特定跟踪可以启用和使用托管[WS-AtomicTransaction 配置 MMC 管理单元](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)工具。  跟踪可包含指示以下内容的数据：特定事务的登记时间、事务达到其最终状态的时间、每个事务登记收到的结果。 可以使用查看所有跟踪[Service Trace Viewer Tool (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)工具。  
  
 通过 ETW 跟踪会话，WS-AT 协议服务还支持集成 ServiceModel 跟踪。 这样，除了现有事务跟踪之外，可提供更多特定于通信的详细跟踪。  若要启用这些附加跟踪，请按照以下步骤操作  
  
1.  打开**开始/运行**菜单中，输入框中键入"regedit"，然后选择**确定**。  
  
2.  在中**注册表编辑器**，导航到左侧窗格中，Hkey_Local_Machine\SOFTWARE\Microsoft\WSAT\3.0\ 上的以下文件夹  
  
3.  右键单击`ServiceModelDiagnosticTracing`右窗格中的值，然后选择**修改**。  
  
4.  在中**数值数据**输入框中，输入要指定你想要启用的跟踪级别的以下有效值之一。  
  
-   0：关闭  
  
-   1：严重  
  
-   3：错误。 这是默认值。  
  
-   7：警告  
  
-   15：信息  
  
-   31：详细  
  
## <a name="see-also"></a>请参阅
- [WS-AtomicTransaction 配置实用工具 (wsatConfig.exe)](../../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
- [WS-AtomicTransaction 配置 MMC 管理单元](../../../../docs/framework/wcf/ws-atomictransaction-configuration-mmc-snap-in.md)
