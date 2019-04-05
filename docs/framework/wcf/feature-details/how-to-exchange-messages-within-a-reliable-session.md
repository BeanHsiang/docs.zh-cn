---
title: 如何：可靠会话内交换消息
ms.date: 03/30/2017
ms.assetid: 87cd0e75-dd2c-44c1-8da0-7b494bbdeaea
ms.openlocfilehash: 145224655d1ec76c9deb5afc3c1a8ec9a1975f4f
ms.sourcegitcommit: af0a22a4eb11bbcd33baec49150d551955b50a16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260681"
---
# <a name="how-to-exchange-messages-within-a-reliable-session"></a>如何：可靠会话内交换消息

本主题概述了使用系统提供的绑定之一来启用可靠会话所需的步骤。这些绑定支持可靠会话，但默认情况下不支持。 启用可靠会话使用代码以强制方式或配置文件中以声明方式。 此过程使用客户端和服务配置文件来启用可靠会话并规定消息到达其中发送顺序相同。

此过程的关键部分是终结点配置元素包含`bindingConfiguration`引用一个名为的绑定配置的属性`Binding1`。 [ **\<绑定 >** ](../../../../docs/framework/misc/binding.md)配置元素将引用此名称来启用可靠会话通过设置`enabled`属性的[ **\<reliableSession >** ](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731302(v=vs.100))元素`true`。 通过将 `ordered` 属性设置为 `true`，可为可靠会话指定有序传送保证。

此示例中的源副本，请参阅[WS 可靠会话](../../../../docs/framework/wcf/samples/ws-reliable-session.md)。

### <a name="configure-the-service-with-a-wshttpbinding-to-use-a-reliable-session"></a>将服务配置为使用 WSHttpBinding 使用可靠会话

1. 为该类型的服务定义服务协定。

   [!code-csharp[c_HowTo_UseReliableSession#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1121)]

1. 在服务类中实现该服务协定。 请注意，该服务的实现内部未指定地址或绑定信息。 您无需编写代码，以便从配置文件中检索的地址或绑定信息。

   [!code-csharp[c_HowTo_UseReliableSession#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1122)]

1. 创建*Web.config*文件以配置一个终结点`CalculatorService`，它使用<xref:System.ServiceModel.WSHttpBinding>与已启用并按序送达消息所需的可靠会话。

   [!code-xml[c_HowTo_UseReliableSession#2111](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/common/web.config#2111)]

1. 创建*Service.svc*包含行的文件：

   ```
   <%@ServiceHost language=c# Service="CalculatorService" %>
   ```

1.  位置*Service.svc* Internet 信息服务 (IIS) 虚拟目录中的文件。

### <a name="configure-the-client-with-a-wshttpbinding-to-use-a-reliable-session"></a>使用 WSHttpBinding 使用可靠会话配置客户端

1. 使用[ServiceModel Metadata Utility Tool (*Svcutil.exe*)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)从命令行以从服务元数据生成代码：

   ```console
   Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
   ```

1. 生成的客户端包含`ICalculator`定义客户端实现必须满足的服务协定的接口。

   [!code-csharp[C_HowTo_UseReliableSession#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1221)]

1. 生成的客户端应用程序还包含 `ClientCalculator` 的实现。 请注意，地址和绑定信息不内部，指定服务的实现。 您无需编写代码，以便从配置文件中检索的地址或绑定信息。

   [!code-csharp[C_HowTo_UseReliableSession#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1222)]

1. *Svcutil.exe*还会生成使用的客户端的配置<xref:System.ServiceModel.WSHttpBinding>类。 将配置文件名称*App.config*时使用 Visual Studio。

   [!code-xml[C_HowTo_UseReliableSession#2211](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/common/app.config#2211)]

1. 创建的实例`ClientCalculator`应用程序中，并调用服务操作。

   [!code-csharp[C_HowTo_UseReliableSession#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1223)]

1. 编译并运行客户端。

## <a name="example"></a>示例

默认情况下，有多种系统提供的绑定支持可靠会话。 这些问题包括：

- <xref:System.ServiceModel.WSDualHttpBinding>

- <xref:System.ServiceModel.NetNamedPipeBinding>

- <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>

有关如何创建支持可靠会话的自定义绑定的示例，请参阅[如何：使用 HTTPS 创建自定义可靠会话绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md)。

## <a name="see-also"></a>请参阅

- [可靠会话](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)
