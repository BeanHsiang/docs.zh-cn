---
title: Binding2
ms.date: 03/30/2017
ms.assetid: 09511c6c-5749-4bb0-874e-0f0be36bfe04
ms.openlocfilehash: aaf0dd9d6918f2c248942cee3773eee8332adda9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54552835"
---
# <a name="binding"></a>绑定
wmi Binding  
  
## <a name="syntax"></a>语法  
  
```csharp
class Binding  
{  
  BindingElement BindingElements[];  
  datetime CloseTimeout;  
  string Name;  
  string Namespace;  
  datetime OpenTimeout;  
  datetime ReceiveTimeout;  
  string Scheme;  
  datetime SendTimeout;  
};  
```  
  
## <a name="methods"></a>方法  
 Binding 类未定义任何方法。  
  
## <a name="properties"></a>Properties  
 Binding 类具有以下属性。  
  
### <a name="bindingelements"></a>BindingElements  
 数据类型：BindingElement 数组  
  
 访问类型：只读  
  
 由绑定实现的绑定元素的集合。  
  
### <a name="closetimeout"></a>CloseTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 为完成关闭操作提供的时间间隔。  
  
### <a name="name"></a>name  
 数据类型：String  
  
 访问类型：只读  
  
 绑定的名称。  
  
### <a name="namespace"></a>命名空间  
 数据类型：String  
  
 访问类型：只读  
  
 绑定的 XML 命名空间。  
  
### <a name="opentimeout"></a>OpenTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 为完成打开操作提供的时间间隔。  
  
### <a name="receivetimeout"></a>ReceiveTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 为完成接收操作提供的时间间隔。  
  
### <a name="scheme"></a>方案  
 数据类型：String  
  
 访问类型：只读  
  
 绑定建立的通道和侦听器工厂所使用的 URI 传输方案。  
  
### <a name="sendtimeout"></a>SendTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 为完成发送操作提供的时间间隔。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Channels.Binding>
