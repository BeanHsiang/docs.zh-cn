---
title: ClientCredentials
ms.date: 03/30/2017
ms.assetid: 41dffd6b-8f14-4fed-aefb-2a1bb168efb3
ms.openlocfilehash: 410a133ae3041db00ecb7a17677afe6538ef1f4f
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54632733"
---
# <a name="clientcredentials"></a>ClientCredentials
ClientCredentials  
  
## <a name="syntax"></a>语法  
  
```csharp
class ClientCredentials : Behavior  
{  
  string ClientCertificate;  
  string HttpDigest;  
  string IssuedToken;  
  string Peer;  
  string ServiceCertificate;  
  boolean SupportInteractive;  
  string UserName;  
  string Windows;  
};  
```  
  
## <a name="methods"></a>方法  
 ClientCredentials 类未定义任何方法。  
  
## <a name="properties"></a>Properties  
 ClientCredentials 类具有以下属性：  
  
### <a name="clientcertificate"></a>ClientCertificate  
 数据类型：String  
  
 访问类型：只读  
  
 客户端用来向服务验证身份的 X.509 证书。  
  
### <a name="httpdigest"></a>HttpDigest  
 数据类型：String  
  
 访问类型：只读  
  
 当前 Http Digest 凭据。  
  
### <a name="issuedtoken"></a>IssuedToken  
 数据类型：String  
  
 访问类型：只读  
  
 用于联系本地安全令牌服务的终结点地址和绑定。  
  
### <a name="peer"></a>对等  
 数据类型：String  
  
 访问类型：只读  
  
 对等节点用来向网格中的其他节点验证其自身身份的凭据。  
  
### <a name="servicecertificate"></a>ServiceCertificate  
 数据类型：String  
  
 访问类型：只读  
  
 服务的 X.509 证书。  
  
### <a name="supportinteractive"></a>SupportInteractive  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定凭据是否支持交互式协商。  
  
### <a name="username"></a>UserName  
 数据类型：String  
  
 访问类型：只读  
  
 客户端用来向服务验证其自身身份的用户名和密码。  
  
### <a name="windows"></a>Windows  
 数据类型：String  
  
 访问类型：只读  
  
 客户端用来向服务验证其自身身份的 Windows 凭据。  
  
## <a name="requirements"></a>要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|-----------------------------------|  
|命名空间|已在 root\ServiceModel 中定义|  
  
## <a name="see-also"></a>请参阅
- <xref:System.ServiceModel.Description.ClientCredentials>
