---
title: WS-AtomicTransaction 配置实用工具 (wsatConfig.exe)
ms.date: 03/30/2017
ms.assetid: 1c56cf98-3963-46d5-a4e1-482deae58c58
ms.openlocfilehash: b4c2bb2d9c81b6ab3afc783d1188de7664e01566
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54741413"
---
# <a name="ws-atomictransaction-configuration-utility-wsatconfigexe"></a>WS-AtomicTransaction 配置实用工具 (wsatConfig.exe)
WS-AtomicTransaction 配置实用工具用于配置基本的 WS-AtomicTransaction 支持设置。  
  
## <a name="syntax"></a>语法  
  
```  
wsatConfig [Options]  
```  
  
## <a name="remarks"></a>备注  
 只能使用此命令行工具在本地计算机中配置基本的 WS-AT 设置。 如果必须在本地和远程计算机上配置设置，则应如中所述来使用 MMC 管理单元[配置 Ws-atomic 事务支持](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)。  
  
 可以在 Windows SDK 安装位置中找到此命令行工具，具体位置为  
  
 %SystemRoot%\Microsoft.Net\Framework\v3.0\Windows Communication Foundation\wsatConfig.exe  
  
 如果运行的是 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 或 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]，您必须在运行 WsatConfig.exe 之前下载更新。 有关此更新的详细信息，请参阅[Commerce Server 2007 (KB912817) 更新](https://go.microsoft.com/fwlink/?LinkId=95340)并[可用性的 Windows XP COM + 修补程序汇总包 13](https://go.microsoft.com/fwlink/?LinkId=95341)。  
  
 下表显示了可用于 WS-AtomicTransaction 配置实用工具 (wsatConfig.exe) 的选项。  
  
> [!NOTE]
>  为选定端口设置 SSL 证书时，将覆盖与该端口关联的原始 SSL 证书（如果有）。  
  
|选项|描述|  
|-------------|-----------------|  
|-帐户：\<帐户 >|指定可参与 WS-AtomicTransaction 的帐户的逗号分隔列表。 不会检查这些帐户的有效性。|  
|-accountsCerts:\<thumb>&#124;"Issuer\SubjectName",>|指定可参与 WS-AtomicTransaction 的证书以逗号分隔的列表。 这些证书由指纹或“颁发者\主题名称”对指示。 如果主题名称为空，请为其使用 {EMPTY}。|  
|-endpointCert:<machine&#124;\<thumb>&#124;"Issuer\SubjectName">|使用由指纹或“颁发者\主题名称”对指定的计算机证书或另一个本地终结点证书。 如果主题名称为空，请为其使用 {EMPTY}。|  
|-maxTimeout:\<sec>|以秒为单位指定最大超时。 有效值为从 0 到 3600。|  
|-network:\<enable&#124;disable>|启用或禁用 WS-AtomicTransaction 网络支持。|  
|-端口：\<portNum >|为 WS-AtomicTransaction 设置 HTTPS 端口。<br /><br /> 如果在运行此工具之前已启用了防火墙，则会在例外列表中自动注册该端口。 如果在运行此工具之前防火墙处于禁用状态，将不会对防火墙进行任何其他配置。<br /><br /> 如果在配置 WS-AT 之后启用防火墙，您必须再次运行此工具并使用此参数提供端口号。 如果在配置之后禁用防火墙，WS-AT 将继续工作，而无需附加输入。|  
|超时：\<秒 >|以秒为单位指定默认超时。 有效值为 1 到 3600。|  
|-traceActivity:\<enable&#124;disable>|启用或禁用对活动事件的跟踪。|  
|-traceLevel:\<关闭&#124;错误&#124;关键&#124;警告&#124;信息&#124;详细&#124;所有 >}|指定跟踪级别。|  
|-tracePII:\<enable&#124;disable>|启用或禁用对个人身份信息的跟踪。|  
|-traceProp:\<enable&#124;disable>|启用或禁用对传播事件的跟踪。|  
|-restart|立即重新启动 MSDTC 以使更改生效。 如果不指定此选项，则更改将在 MSDTC 重新启动后生效。|  
|-show|显示当前的 WS-AtomicTransaction 协议设置。|  
|-virtualServer:\<virtualServer>|指定 DTC 资源群集名。|  
  
## <a name="see-also"></a>请参阅
- [使用 WS-AtomicTransaction](../../../docs/framework/wcf/feature-details/using-ws-atomictransaction.md)
- [配置 WS-Atomic 事务支持](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)
