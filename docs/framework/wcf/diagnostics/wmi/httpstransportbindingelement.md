---
title: HttpsTransportBindingElement
ms.date: 03/30/2017
ms.assetid: e78aa8c6-b53b-4105-a900-d3e7a39670f2
ms.openlocfilehash: be4d78867081dbe511b83d39b5e07e06b689cc09
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54537759"
---
# <a name="httpstransportbindingelement"></a>HttpsTransportBindingElement
HttpsTransportBindingElement  
  
## <a name="syntax"></a>语法  
  
```csharp  
class HttpsTransportBindingElement : HttpTransportBindingElement  
{  
  boolean RequireClientCertificate;  
};  
```  
  
## <a name="methods"></a>方法  
 HttpsTransportBindingElement 类未定义任何方法。  
  
## <a name="properties"></a>属性  
 HttpsTransportBindingElement 类具有下列属性：  
  
### <a name="requireclientcertificate"></a>RequireClientCertificate  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示是否需要进行 SSL 客户端身份验证。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>
