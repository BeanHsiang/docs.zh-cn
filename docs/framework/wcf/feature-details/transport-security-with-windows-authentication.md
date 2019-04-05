---
title: 通过 Windows 身份验证确保的传输安全
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 96dd26e2-46e7-4de0-9a29-4fcb05bf187b
ms.openlocfilehash: 96fce3cb56cf328e0fbb589113e3ac24519de557
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2019
ms.locfileid: "58125442"
---
# <a name="transport-security-with-windows-authentication"></a>通过 Windows 身份验证确保的传输安全
以下方案演示了 Windows Communication Foundation (WCF) 客户端和服务由 Windows 安全保护。 有关编程的详细信息，请参阅[如何：使用 Windows 凭据保护服务](../../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md)。  
  
 Intranet Web 服务显示了人力资源信息。 客户端是 Windows 窗体应用程序。 该应用程序部署在具有 Kerberos 控制器保护的域中。  
  
 ![使用 Windows 身份验证的传输安全性](./media/transport-security-with-windows-authentication/secured-windows-authentication.gif)  
  
|特征|描述|  
|--------------------|-----------------|  
|安全模式|传输|  
|互操作性|WCF 仅|  
|身份验证（服务器）<br /><br /> 身份验证（客户端）|是（使用 Windows 集成身份验证）<br /><br /> 是（使用 Windows 集成身份验证）|  
|完整性|是|  
|保密性|是|  
|传输|NET.TCP|  
|绑定|<xref:System.ServiceModel.NetTcpBinding>|  
  
## <a name="service"></a>服务  
 下面的代码和配置应独立运行。 执行下列操作之一：  
  
-   使用代码（而不使用配置）创建独立服务。  
  
-   使用提供的配置创建服务，但不定义任何终结点。  
  
### <a name="code"></a>代码  
 下面的代码演示如何创建使用 Windows 安全的服务终结点。  
  
 [!code-csharp[C_SecurityScenarios#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#3)]
 [!code-vb[C_SecurityScenarios#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#3)]  
  
### <a name="configuration"></a>配置  
 可以使用下面的配置代替代码来设置服务终结点：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <behaviors />  
    <services>  
      <service behaviorConfiguration="" name="ServiceModel.Calculator">  
        <endpoint address="net.tcp://localhost:8008/Calculator"   
                  binding="netTcpBinding"  
          bindingConfiguration="WindowsClientOverTcp"   
                  name="WindowsClientOverTcp"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <netTcpBinding>  
        <binding name="WindowsClientOverTcp">  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="client"></a>客户端  
 下面的代码和配置应独立运行。 执行下列操作之一：  
  
-   使用代码（和客户端代码）创建独立客户端。  
  
-   创建不定义任何终结点地址的客户端。 而使用将配置名称作为参数的客户端构造函数。 例如：  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### <a name="code"></a>代码  
 下面的代码创建客户端。 绑定配置为使用传输模式安全（采用 TCP 传输协议），并且客户端凭据类型设置为 Windows。  
  
 [!code-csharp[C_SecurityScenarios#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#4)]
 [!code-vb[C_SecurityScenarios#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#4)]  
  
### <a name="configuration"></a>配置  
 可以使用下面的配置代替代码来创建客户端。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <netTcpBinding>  
        <binding name="NetTcpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="Windows" />  
          </security>  
        </binding>  
      </netTcpBinding>  
    </bindings>  
    <client>  
      <endpoint address="net.tcp://localhost:8008/Calculator"   
                binding="netTcpBinding"            
                bindingConfiguration="NetTcpBinding_ICalculator"   
                contract="ICalculator"  
                name="NetTcpBinding_ICalculator">  
      </endpoint>  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>请参阅
- [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)
- [如何：使用 Windows 凭据保护服务](../../../../docs/framework/wcf/how-to-secure-a-service-with-windows-credentials.md)
- [Windows Server App Fabric 的安全模型](https://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)
