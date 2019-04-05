---
title: PeerCustomResolverBindingElement
ms.date: 03/30/2017
ms.assetid: 9ccc2770-a20e-4dff-9970-f56ad8aec2b5
ms.openlocfilehash: 37984fb51fd19eb1f6c249852f120cc59b99adc2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54613930"
---
# <a name="peercustomresolverbindingelement"></a>PeerCustomResolverBindingElement
PeerCustomResolverBindingElement  
  
## <a name="syntax"></a>语法  
```csharp
class PeerCustomResolverBindingElement : PeerResolverBindingElement
{  
    string Address;
    string Binding;
};
```  
  
## <a name="methods"></a>方法  
 PeerCustomResolverBindingElement 类不定义任何方法。  
  
## <a name="properties"></a>Properties  
 PeerCustomResolverBindingElement 类具有下列属性：  
  
### <a name="address"></a>Address  
 数据类型：String  
  
 访问类型：只读  
  
 对等自定义解析程序的地址。  
  
### <a name="binding"></a>绑定  
 数据类型：String  
  
 访问类型：只读  
  
 绑定的配置名称。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Channels.PeerCustomResolverBindingElement>
