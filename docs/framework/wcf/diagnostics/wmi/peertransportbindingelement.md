---
title: PeerTransportBindingElement
ms.date: 03/30/2017
ms.assetid: 40bf6be2-8087-4cb3-a66c-408d53eb9269
ms.openlocfilehash: 437ccc0446e3cc05596ab12b7908177b7f78e431
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54670649"
---
# <a name="peertransportbindingelement"></a>PeerTransportBindingElement
PeerTransportBindingElement  
  
## <a name="syntax"></a>语法  
  
```csharp
class PeerTransportBindingElement : TransportBindingElement  
{  
  string ListenIPAddress;  
  sint32 Port;  
  PeerSecuritySettings Security;  
};  
```  
  
## <a name="methods"></a>方法  
 PeerTransportBindingElement 类未定义任何方法。  
  
## <a name="properties"></a>Properties  
 PeerTransportBindingElement 类具有以下属性：  
  
### <a name="listenipaddress"></a>ListenIPAddress  
 数据类型：String  
  
 访问类型：只读  
  
 对等节点在其上侦听消息的 IP 地址。  
  
### <a name="port"></a>端口  
 数据类型：sint32  
  
 访问类型：只读  
  
 网络接口端口，此绑定在该端口上处理对等通道消息。  
  
### <a name="security"></a>安全性  
 数据类型：PeerSecuritySettings  
  
 访问类型：只读  
  
 对等传输安全设置。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Channels.PeerTransportBindingElement>
