---
title: 客户端验证
ms.date: 03/30/2017
ms.assetid: f0c1f805-1a81-4d0d-a112-bf5e2e87a631
ms.openlocfilehash: b033695065dfeb130f041563909704acb84bb3be
ms.sourcegitcommit: 0069cb3de8eed4e92b2195d29e5769a76111acdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2019
ms.locfileid: "56333295"
---
# <a name="client-validation"></a>客户端验证
服务通常发布元数据以启用客户端代理类型的自动生成和配置。 如果服务不受信任，客户端应用程序应该验证元数据是否符合客户端应用程序有关安全性、事务、服务协定类型等方面的策略。 下面的示例演示如何编写一个客户端终结点行为，用于验证服务终结点以确保可以安全地使用该服务终结点。  
  
 服务公开四个终结点。 第一个终结点使用 WSDualHttpBinding，第二个终结点使用 NTLM 身份验证，第三个终结点启用事务流，第四个终结点使用基于证书的身份验证。  
  
 客户端使用 <xref:System.ServiceModel.Description.MetadataResolver> 类来检索服务的元数据。 客户端强制实施禁用双工绑定、NTLM 身份验证和使用验证行为的事务流的策略。 每个<xref:System.ServiceModel.Description.ServiceEndpoint>从服务的元数据，客户端应用程序导入的实例将添加的实例`InternetClientValidatorBehavior`到终结点行为<xref:System.ServiceModel.Description.ServiceEndpoint>然后再尝试使用 Windows Communication Foundation (WCF) 客户端连接到终结点。 在调用服务上的任何操作之前，会运行该行为的 `Validate` 方法，并通过引发 `InvalidOperationExceptions` 强制实施客户端的策略。  
  
### <a name="to-build-the-sample"></a>生成示例  
  
1.  若要生成解决方案，请按照中的说明[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)。  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>在同一计算机上运行示例  
  
1.  使用管理员特权打开 Visual Studio 开发人员命令提示并从示例安装文件夹运行 Setup.bat。 这将安装运行示例所需的所有证书。  
  
2.  从 \service\bin\Debug 运行服务应用程序。  
  
3.  从 \client\bin\Debug 运行客户端应用程序。 客户端活动将显示在客户端控制台应用程序上。  
  
4.  如果客户端和服务能够进行通信，请参见[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
5.  在运行完该示例后运行 Cleanup.bat 移除证书。 其他安全示例使用相同的证书。  
  
### <a name="to-run-the-sample-across-computers"></a>跨计算机运行示例  
  
1.  在服务器上，在使用管理员特权运行 Visual Studio 的开发人员命令提示符键入`setup.bat service`。 运行`setup.bat`与`service`参数与计算机的名称的完全限定域名创建一个服务证书并将服务证书导出到名为 Service.cer 的文件。  
  
2.  在服务器上，编辑 App.config 以反映新证书名称。 也就是说，更改`findValue`中的属性[ \<serviceCertificate >](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)元素名称的计算机的完全限定域名。  
  
3.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
4.  在客户端上打开开发人员命令提示用于 Visual Studio 使用管理员特权，并且类型`setup.bat client`。 运行`setup.bat`与`client`参数创建一个名为 Client.com 的客户端证书，并将客户端证书导出到名为 Client.cer 的文件。  
  
5.  在 client.cs 文件中更改 MEX 终结点的地址值和用于设置默认服务器证书的 `findValue` 以与服务的新地址相匹配。 通过使用服务器的完全限定域名替换 localhost 来执行此操作。 请重新生成。  
  
6.  将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
7.  在客户端上运行 ImportServiceCert.bat 在开发人员命令提示符下使用管理员特权打开 Visual Studio。 这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
8.  在服务器上，运行 ImportClientCert.bat 在开发人员命令提示符下使用管理员特权打开 Visual Studio。 这会将 Client.cer 文件中的客户端证书导入 LocalMachine - TrustedPeople 存储区。  
  
9. 在服务计算机上，在 Visual Studio 中生成服务项目并运行 service.exe。  
  
10. 在客户端计算机上，运行 client.exe。  
  
    1.  如果客户端和服务能够进行通信，请参见[WCF 示例的故障排除提示](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))。  
  
### <a name="to-clean-up-after-the-sample"></a>运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
    > [!NOTE]
    >  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。 如果您运行在计算机之间使用的证书，请确保清除已安装在 CurrentUser-的服务证书的 WCF 示例 TrustedPeople 存储。 为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>. For example: certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## <a name="see-also"></a>请参阅
- [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)
