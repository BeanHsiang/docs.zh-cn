---
title: WCF 所要求的操作系统资源
ms.date: 03/30/2017
ms.assetid: cdd9a331-53fe-4e0d-bdfe-782264aec5c9
ms.openlocfilehash: 759ab099066e300484860cf3f91d6d084ba1d339
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54527076"
---
# <a name="operating-system-resources-required-by-wcf"></a>WCF 所要求的操作系统资源
Windows Communication Foundation (WCF) 取决于提供的函数将操作系统的多个资源。 下表列出了这些资源。  
  
|资源|描述|  
|--------------|-----------------|  
|Microsoft 分布式事务协调器 (MSDTC)|支持 OleTx 事务所必需。|  
|Internet 信息服务 (IIS)|如果希望使用 IIS 来承载应用程序，则是必需的。|  
|Windows 进程激活服务 (WAS)|如果希望使用 WAS 来承载应用程序，则是必需的。|  
  
## <a name="see-also"></a>请参阅
- [系统要求](../../../docs/framework/wcf/wcf-system-requirements.md)
