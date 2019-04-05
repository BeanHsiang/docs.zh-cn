---
title: 如何：指定通道安全凭据
ms.date: 03/30/2017
ms.assetid: f8e03f47-9c4f-4dd5-8f85-429e6d876119
ms.openlocfilehash: dac85a31a3194af3dff8a14461591d0f1a97399f
ms.sourcegitcommit: d9a0071d0fd490ae006c816f78a563b9946e269a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55066189"
---
# <a name="how-to-specify-channel-security-credentials"></a>如何：指定通道安全凭据
Windows Communication Foundation (WCF) 服务标记允许 COM 应用程序可以调用 WCF 服务。 大多数 WCF 服务需要客户端指定要用于身份验证和授权的凭据。 在从 WCF 客户端调用 WCF 服务，可以指定这些凭据，在托管代码或应用程序配置文件中。 在 COM 应用程序中调用 WCF 服务，可以使用<xref:System.ServiceModel.ComIntegration.IChannelCredentials>接口指定凭据。 本主题将介绍使用 <xref:System.ServiceModel.ComIntegration.IChannelCredentials> 接口指定凭据的各种方法。  
  
> [!NOTE]
>  <xref:System.ServiceModel.ComIntegration.IChannelCredentials> 是一种基于 IDispatch 的接口，在 Visual Studio 环境中使用它将无法获取 IntelliSense 功能。  
  
 本文将使用 WCF 服务中定义[消息安全示例](../../../../docs/framework/wcf/samples/message-security-sample.md)。  
  
### <a name="to-specify-a-client-certificate"></a>指定客户端证书  
  
1.  在消息安全目录中运行 Setup.bat 文件以创建和安装所需的测试证书。  
  
2.  打开消息安全项目。  
  
3.  添加`[ServiceBehavior(Namespace="http://Microsoft.ServiceModel.Samples")]`到`ICalculator`接口定义。  
  
4.  添加`bindingNamespace="http://Microsoft.ServiceModel.Samples"`到服务 App.config 中的终结点标记。  
  
5.  生成消息安全示例并运行 Service.exe。 使用 Internet Explorer 并浏览到服务的 URI (http://localhost:8000/ServiceModelSamples/Service)以确保服务正在运行。  
  
6.  打开 Visual Basic 6.0 并创建一个新的 Standard .exe 文件。 在窗体中添加一个按钮并双击该按钮，以将以下代码添加到 Click 处理程序中：  
  
    ```  
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
        monString = monString + ", binding=BasicHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
        Set monikerProxy = GetObject(monString)  
  
        'Set the Service Certificate.  
     monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetDefaultServiceCertificateFromStore "CurrentUser", "TrustedPeople", "FindBySubjectName", "localhost"  
  
        'Set the Client Certificate.  
        monikerProxy.ChannelCredentials.SetClientCertificateFromStoreByName "CN=client.com", "CurrentUser", "My"  
        MsgBox monikerProxy.Add(3, 4)  
    ```  
  
7.  运行 Visual Basic 应用程序并验证结果。  
  
     Visual Basic 应用程序将显示一个消息框，其中包含调用 Add(3, 4) 的结果。 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromFile%28System.String%2CSystem.String%2CSystem.String%29> 或 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStoreByName%28System.String%2CSystem.String%2CSystem.String%29> 也可以用于代替 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetClientCertificateFromStore%28System.String%2CSystem.String%2CSystem.String%2CSystem.Object%29> 设置客户端证书：  
  
    ```  
    monikerProxy.ChannelCredentials.SetClientCertificateFromFile "C:\MyClientCert.pfx", "password", "DefaultKeySet"  
    ```  
  
> [!NOTE]
>  为使此调用生效，客户端证书在运行该客户端的计算机上应该是受信任的。  
  
> [!NOTE]
>  如果标记格式不正确，或如果服务不可用，则对 `GetObject` 的调用将返回一个错误，指示“语法无效”。 如果您收到此错误，请确保所使用的标记正确无误且服务可用。  
  
### <a name="to-specify-user-name-and-password"></a>指定用户名和密码  
  
1.  修改服务的 App.config 文件以使用 `wsHttpBinding`。 验证用户名和密码时需要如此：  
  
  
  
2.  将 `clientCredentialType` 设置为 UserName：  
  
  
  
3.  打开 Visual Basic 6.0 并创建一个新的 Standard .exe 文件。 在窗体中添加一个按钮并双击该按钮，以将以下代码添加到 Click 处理程序中：  
  
    ```  
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
  
    Set monikerProxy = GetObject(monString)  
  
    monikerProxy.ChannelCredentials.SetServiceCertificateAuthentication "CurrentUser", "NoCheck", "PeerOrChainTrust"  
    monikerProxy.ChannelCredentials.SetUserNameCredential "username", "password"  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
4.  运行 Visual Basic 应用程序并验证结果。 Visual Basic 应用程序将显示一个消息框，其中包含调用 Add(3, 4) 的结果。  
  
    > [!NOTE]
    >  在本示例中，服务标记中指定的绑定已更改为 WSHttpBinding_ICalculator。 另外请注意，在调用 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetUserNameCredential%28System.String%2CSystem.String%29> 时，必须提供有效的用户名和密码。  
  
### <a name="to-specify-windows-credentials"></a>指定 Windows 凭据  
  
1.  在服务的 App.config 文件中将 `clientCredentialType` 设置为 Windows：  
  
  
  
2.  打开 Visual Basic 6.0 并创建一个新的 Standard .exe 文件。 在窗体中添加一个按钮并双击该按钮，以将以下代码添加到 Click 处理程序中：  
  
    ```  
    monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
    monString = monString + ", address=http://localhost:8000/ServiceModelSamples/Service"  
    monString = monString + ", contract=ICalculator, contractNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", binding=WSHttpBinding_ICalculator, bindingNamespace=http://Microsoft.ServiceModel.Samples"  
    monString = monString + ", upnidentity=domain\userID"  
  
    Set monikerProxy = GetObject(monString)  
     monikerProxy.ChannelCredentials.SetWindowsCredential "domain", "userID", "password", 1, True  
  
    MsgBox monikerProxy.Add(3, 4)  
    ```  
  
3.  运行 Visual Basic 应用程序并验证结果。 Visual Basic 应用程序将显示一个消息框，其中包含调用 Add(3, 4) 的结果。  
  
    > [!NOTE]
    >  您必须使用有效值替换“domain”、“userID”和“password”。  
  
### <a name="to-specify-an-issue-token"></a>指定颁发令牌  
  
1.  颁发令牌仅用于使用联合安全的应用程序。 有关联合安全的详细信息，请参阅[联合身份验证和颁发令牌](../../../../docs/framework/wcf/feature-details/federation-and-issued-tokens.md)并[联合身份验证示例](../../../../docs/framework/wcf/samples/federation-sample.md)。  
  
     下面的 Visual Basic 代码示例演示如何调用 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29> 方法：  
  
    ```  
        monString = "service:mexAddress=http://localhost:8000/ServiceModelSamples/Service?wsdl"  
        monString = monString + ", address=http://localhost:8000/SomeService/Service"  
        monString = monString + ", contract=ICalculator, contractNamespace=http://SomeService.Samples"  
        monString = monString + ", binding=WSHttpBinding_ISomeContract, bindingNamespace=http://SomeService.Samples"  
  
        Set monikerProxy = GetObject(monString)  
    monikerProxy.SetIssuedToken("http://somemachine/sts", "bindingType", "binding")  
    ```  
  
     有关用于此方法的参数的更多信息，请参见 <xref:System.ServiceModel.ComIntegration.IChannelCredentials.SetIssuedToken%28System.String%2CSystem.String%2CSystem.String%29>。  
  
## <a name="see-also"></a>请参阅
- [联合](../../../../docs/framework/wcf/feature-details/federation.md)
- [如何：联合身份验证服务上配置凭据](../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)
- [如何：创建联合客户端](../../../../docs/framework/wcf/feature-details/how-to-create-a-federated-client.md)
- [消息安全性](../../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)
- [绑定与安全](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)
