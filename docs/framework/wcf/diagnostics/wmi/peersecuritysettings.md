---
title: PeerSecuritySettings
ms.date: 03/30/2017
ms.assetid: 24ae0d35-f3a3-419b-afd6-686e22aae27b
ms.openlocfilehash: 761ed0e30c6acca8c910c5dc97dfbae46c1f89bb
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54564833"
---
# <a name="peersecuritysettings"></a>PeerSecuritySettings
PeerSecuritySettings  
  
## <a name="syntax"></a>语法  
  
```csharp
class PeerSecuritySettings  
{  
  string Mode;  
  PeerTransportSecuritySettings Transport;  
};  
```  
  
## <a name="methods"></a>方法  
 PeerSecuritySettings 类不定义任何方法。  
  
## <a name="properties"></a>Properties  
 PeerSecuritySettings 类具有下列属性：  
  
### <a name="mode"></a>模式  
 数据类型：String  
  
 访问类型：只读  
  
 配置有绑定的终结点是否使用消息级别和传输级别安全。  
  
### <a name="transport"></a>传输  
 数据类型：PeerTransportSecuritySettings  
  
 访问类型：只读  
  
 传输安全设置。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.PeerSecuritySettings>
