---
title: 控制 WCF 服务主机的自动启动
ms.date: 03/30/2017
f1_keywords:
- WcfOptions
ms.assetid: 6abe5d34-519b-4cef-8f02-3c0a7f125585
ms.openlocfilehash: f7f58a684449819fe945ad1ba5bff12f425c8294
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712387"
---
# <a name="controlling-auto-launching-of-wcf-service-host"></a>控制 WCF 服务主机的自动启动
在调试包含多个项目在同一 Visual Studio 解决方案中的另一个项目时可以控制 WCF 服务库项目中，Windows Communication Foundation (WCF) 服务主机 (WcfSvcHost.exe) 的自动启动功能。  
  
 为此，请右键单击 WCF 服务项目中**解决方案资源管理器**，选择**属性**，然后单击**WCF 选项**选项卡。**启动 WCF 服务主机在调试同一解决方案中的另一个项目时**默认情况下启用复选框。 您可以清除的框，以便在同一解决方案中调试另一个项目时，就不会启动此特定项目的 WCF 服务主机。  
  
 此行为不会影响 F5 调试或此项目的“添加服务引用”功能。  
  
 该选项可用于以下项目：  
  
-   WCF 服务库项目。  
  
-   顺序工作流服务库项目。  
  
-   状态机工作流服务库项目。  
  
-   联合服务库项目。  
  
## <a name="see-also"></a>请参阅
- [WCF 服务主机 (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
