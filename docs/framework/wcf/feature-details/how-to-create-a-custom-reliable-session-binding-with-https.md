---
title: 如何：使用 HTTPS 创建自定义可靠会话绑定
ms.date: 03/30/2017
ms.assetid: fa772232-da1f-4c66-8c94-e36c0584b549
ms.openlocfilehash: f39325829cf4b548482a6a570a5aa1fd65e61a1d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54516676"
---
# <a name="how-to-create-a-custom-reliable-session-binding-with-https"></a>如何：使用 HTTPS 创建自定义可靠会话绑定

本主题演示如何对可靠会话使用安全套接字层 (SSL) 传输安全。 若要通过 HTTPS 使用可靠会话，必须创建使用可靠会话和 HTTPS 传输协议的自定义绑定。 使用代码以强制方式或配置文件中以声明方式启用可靠会话。 此过程使用客户端和服务配置文件来启用可靠会话和[  **\<httpsTransport >** ](../../../../docs/framework/configure-apps/file-schema/wcf/httpstransport.md)元素。

此过程的关键部分是**\<终结点 >** 配置元素包含`bindingConfiguration`引用一个名为的自定义绑定配置的属性`reliableSessionOverHttps`。 [ **\<绑定 >** ](../../../../docs/framework/misc/binding.md)配置元素将引用此名称来指定通过包括使用可靠会话和 HTTPS 传输 **\<reliableSession >** 并 **\<httpsTransport >** 元素。

此示例中的源副本，请参阅[自定义绑定可靠会话通过 HTTPS](../../../../docs/framework/wcf/samples/custom-binding-reliable-session-over-https.md)。

### <a name="configure-the-service-with-a-custombinding-to-use-a-reliable-session-with-https"></a>该服务使用 CustomBinding 配置为使用可靠会话与 HTTPS 一起使用

1. 为该类型的服务定义服务协定。

   [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1121)]

1. 在服务类中实现该服务协定。 请注意，该服务的实现内部未指定地址或绑定信息。 您无需编写代码，以便从配置文件中检索的地址或绑定信息。

   [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1122)]

1. 创建*Web.config*文件以配置一个终结点`CalculatorService`与名为的自定义绑定`reliableSessionOverHttps`使用可靠会话和 HTTPS 传输。

   [!code-xml[c_HowTo_CreateReliableSessionHTTPS#2111](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/web.config#2111)]

1. 创建*Service.svc*包含行的文件：

   ```
   <%@ServiceHost language=c# Service="CalculatorService" %>
   ```

1. 位置*Service.svc* Internet 信息服务 (IIS) 虚拟目录中的文件。

### <a name="configure-the-client-with-a-custombinding-to-use-a-reliable-session-with-https"></a>客户端使用 CustomBinding 配置为使用可靠会话与 HTTPS 一起使用

1. 使用[ServiceModel Metadata Utility Tool (*Svcutil.exe*)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)从命令行以从服务元数据生成代码。

   ```console
   Svcutil.exe <Metadata Exchange (MEX) address or HTTP GET address>
   ```

1. 生成的客户端包含`ICalculator`定义客户端实现必须满足的服务协定的接口。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1221)]

1. 生成的客户端应用程序还包含 `ClientCalculator` 的实现。 请注意，该服务的实现内部未指定地址和绑定信息。 您无需编写代码，以便从配置文件中检索的地址和绑定信息。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1222)]

1. 配置名为的自定义绑定`reliableSessionOverHttps`以使用 HTTPS 传输和可靠会话。

   [!code-xml[C_HowTo_CreateReliableSessionHTTPS#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/app.config#2211)]

1. 在应用程序中创建 `ClientCalculator` 的实例，然后调用服务操作。

   [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1223)]

1. 编译并运行客户端。  

## <a name="net-framework-security"></a>.NET Framework 安全性

因为此示例中使用的证书是使用创建的测试证书*Makecert.exe*，当您尝试访问 HTTPS 地址，例如，将出现安全警报`https://localhost/servicemodelsamples/service.svc`，从你的浏览器。

## <a name="see-also"></a>请参阅

- [可靠会话](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)
