---
title: OneWayBindingElement
ms.date: 03/30/2017
ms.assetid: 5c7e17c3-39b9-4214-ae08-9e6141734305
ms.openlocfilehash: d84184febd6db3f233aae6fe558b8e0f50a9cb82
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54608831"
---
# <a name="onewaybindingelement"></a>OneWayBindingElement
OneWayBindingElement  
  
## <a name="syntax"></a>语法  
  
```csharp
class OneWayBindingElement : BindingElement  
{  
  ChannelPoolSettings ChannelPoolSettings;  
  sint32 MaxAcceptedChannels;  
  boolean PacketRoutable;  
};  
```  
  
## <a name="methods"></a>方法  
 OneWayBindingElement 类未定义任何方法。  
  
## <a name="properties"></a>Properties  
 OneWayBindingElement 类具有以下属性：  
  
### <a name="channelpoolsettings"></a>ChannelPoolSettings  
 数据类型：ChannelPoolSettings  
  
 访问类型：只读  
  
 通道池设置。  
  
### <a name="maxacceptedchannels"></a>MaxAcceptedChannels  
 数据类型：sint32  
  
 访问类型：只读  
  
 接受的最大通道数。  
  
### <a name="packetroutable"></a>PacketRoutable  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，该值指示数据包是否可路由。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Channels.OneWayBindingElement>
