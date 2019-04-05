---
title: 如何：使用传输安全性和消息凭据
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TransportWithMessageCredentials
ms.assetid: 6cc35346-c37a-4859-b82b-946c0ba6e68f
ms.openlocfilehash: 7af670210b39da93e9f3efb37a0bfddce84ed2a2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54731863"
---
# <a name="how-to-use-transport-security-and-message-credentials"></a>如何：使用传输安全性和消息凭据
保护具有传输和消息凭据的服务使用的传输和消息安全模式的最佳 Windows Communication Foundation (WCF) 中。 总之，传输层安全提供了完整性和机密性，而消息层安全则提供了严格的传输安全机制所不可能提供的多种凭据。 本主题演示使用 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.NetTcpBinding> 绑定通过消息凭据实现传输的基本步骤。 有关设置安全模式的详细信息，请参阅[如何：将安全模式设置](../../../../docs/framework/wcf/how-to-set-the-security-mode.md)。  
  
 在将安全模式设置为 `TransportWithMessageCredential` 时，传输会确定实际提供传输级安全的机制。 对于 HTTP，该机制为基于 HTTP 的安全套接字层 (SSL)（SSL over HTPP，或 HTTPS）；对于 TCP，该机制为 SSL over TCP 或 Windows。  
  
 如果传输为 HTTP（使用 <xref:System.ServiceModel.WSHttpBinding>），则由 SSL over HTTP 提供传输级安全。 在这种情况下，必须使用绑定到某个端口的 SSL 证书来配置承载服务的计算机，如本主题稍后所示。  
  
 如果传输为 TCP（使用 <xref:System.ServiceModel.NetTcpBinding>），则默认情况下提供的传输级安全为 Windows 安全，即 SSL over TCP。 使用 SSL over TCP 时，必须使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 方法指定证书，如本主题稍后所示。  
  
### <a name="to-use-the-wshttpbinding-with-a-certificate-for-transport-security-in-code"></a>使用 WSHttpBinding 和证书来获得传输安全（在代码中）  
  
1.  使用 HttpCfg.exe 工具将 SSL 证书绑定到计算机上的某个端口。 有关详细信息，请参阅[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
2.  创建 <xref:System.ServiceModel.WSHttpBinding> 类的一个实例，并将 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A> 属性设置为 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>。  
  
3.  将 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> 属性设置为适当的值。 (有关详细信息，请参阅[选择凭据类型](../../../../docs/framework/wcf/feature-details/selecting-a-credential-type.md)。)下面的代码使用 <xref:System.ServiceModel.MessageCredentialType.Certificate> 值。  
  
4.  用适当的基址创建 <xref:System.Uri> 类的一个实例。 请注意，该地址必须使用“HTTPS”方案，且必须包含计算机的实际名称以及 SSL 证书绑定到的端口号。 （也可以在配置中设置基址。）  
  
5.  使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法添加一个服务终结点。  
  
6.  创建 <xref:System.ServiceModel.ServiceHost> 的实例并调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#7)]
     [!code-vb[c_SettingSecurityMode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#7)]  
  
### <a name="to-use-the-nettcpbinding-with-a-certificate-for-transport-security-in-code"></a>使用 NetTcpBinding 和证书来获得传输安全（在代码中）  
  
1.  创建 <xref:System.ServiceModel.NetTcpBinding> 类的一个实例，并将 <xref:System.ServiceModel.NetTcpSecurity.Mode%2A> 属性设置为 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>。  
  
2.  将 <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A> 设置为适当的值。 下面的代码使用 <xref:System.ServiceModel.MessageCredentialType.Certificate> 值。  
  
3.  用适当的基址创建 <xref:System.Uri> 类的一个实例。 请注意，该地址必须使用“net.tcp”方案。 （也可以在配置中设置基址。）  
  
4.  创建 <xref:System.ServiceModel.ServiceHost> 类的实例。  
  
5.  使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 类的 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 方法显式设置服务的 X.509 证书。  
  
6.  使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法添加一个服务终结点。  
  
7.  调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#8)]
     [!code-vb[c_SettingSecurityMode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#8)]  
  
### <a name="to-use-the-nettcpbinding-with-windows-for-transport-security-in-code"></a>使用 NetTcpBinding 和 Windows 来获得传输安全（在代码中）  
  
1.  创建 <xref:System.ServiceModel.NetTcpBinding> 类的一个实例，并将 <xref:System.ServiceModel.NetTcpSecurity.Mode%2A> 属性设置为 <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential>。  
  
2.  将传输安全设置为使用 Windows，方法是将 <xref:System.ServiceModel.TcpTransportSecurity.ClientCredentialType%2A> 设置为 <xref:System.ServiceModel.TcpClientCredentialType.Windows>。 （请注意，这是默认值。）  
  
3.  将 <xref:System.ServiceModel.MessageSecurityOverTcp.ClientCredentialType%2A> 设置为适当的值。 下面的代码使用 <xref:System.ServiceModel.MessageCredentialType.Certificate> 值。  
  
4.  用适当的基址创建 <xref:System.Uri> 类的一个实例。 请注意，该地址必须使用“net.tcp”方案。 （也可以在配置中设置基址。）  
  
5.  创建 <xref:System.ServiceModel.ServiceHost> 类的实例。  
  
6.  使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 类的 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 方法显式设置服务的 X.509 证书。  
  
7.  使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法添加一个服务终结点。  
  
8.  调用 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#9)]
     [!code-vb[c_SettingSecurityMode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#9)]  
  
## <a name="using-configuration"></a>使用配置  
  
#### <a name="to-use-the-wshttpbinding"></a>使用 WSHttpBinding  
  
1.  使用绑定到某个端口的 SSL 证书配置计算机。 (有关详细信息，请参阅[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md))。 不需要设置 <`transport`> 使用此配置元素的值。  
  
2.  指定消息级安全的客户端凭据类型。 下面的示例设置`clientCredentialType`属性的 <`message`> 元素`UserName`。  
  
    ```xml  
    <wsHttpBinding>  
    <binding name="WsHttpBinding_ICalculator">  
            <security mode="TransportWithMessageCredential" >  
               <message clientCredentialType="UserName" />  
            </security>  
    </binding>  
    </wsHttpBinding>  
    ```  
  
#### <a name="to-use-the-nettcpbinding-with-a-certificate-for-transport-security"></a>使用 NetTcpBinding 和证书来获得传输安全  
  
1.  对于 SSL over TCP，必须在 `<behaviors>` 元素中显式指定证书。 下面的示例指定一个证书，该证书由其颁发机构存储在默认存储位置（本地计算机和个人存储）。  
  
    ```xml  
    <behaviors>  
     <serviceBehaviors>  
       <behavior name="mySvcBehavior">  
           <serviceCredentials>  
             <serviceCertificate findValue="contoso.com"  
                                 x509FindType="FindByIssuerName" />  
           </serviceCredentials>  
       </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
2.  添加[ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)到绑定节  
  
3.  添加一个绑定元素，并将 `name` 属性设置为适当的值。  
  
4.  添加 <`security`> 元素，并将设置`mode`属性为`TransportWithMessageCredential`。  
  
5.  添加 <`message>`元素，并将设置`clientCredentialType`属性为适当的值。  
  
    ```xml  
    <bindings>  
    <netTcpBinding>  
      <binding name="myTcpBinding">  
        <security mode="TransportWithMessageCredential" >  
           <message clientCredentialType="Windows" />  
        </security>  
      </binding>  
    </netTcpBinding>  
    </bindings>  
    ```  
  
#### <a name="to-use-the-nettcpbinding-with-windows-for-transport-security"></a>使用 NetTcpBinding 和 Windows 来获得传输安全  
  
1.  添加[ \<netTcpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)到绑定节  
  
2.  添加 <`binding`> 元素，并设置`name`属性为适当的值。  
  
3.  添加 <`security`> 元素，并将设置`mode`属性为`TransportWithMessageCredential`。  
  
4.  添加 <`transport`> 元素，并设置`clientCredentialType`属性为`Windows`。  
  
5.  添加 <`message`> 元素，并设置`clientCredentialType`属性为适当的值。 下面的代码将该值设置为一个证书。  
  
    ```xml  
    <bindings>  
    <netTcpBinding>  
      <binding name="myTcpBinding">  
        <security mode="TransportWithMessageCredential" >  
           <transport clientCredentialType="Windows" />  
           <message clientCredentialType="Certificate" />  
        </security>  
      </binding>  
    </netTcpBinding>  
    </bindings>  
    ```  
  
## <a name="see-also"></a>请参阅
- [如何：将安全模式设置](../../../../docs/framework/wcf/how-to-set-the-security-mode.md)
- [保护服务](../../../../docs/framework/wcf/securing-services.md)
- [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)
