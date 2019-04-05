---
title: 如何：使用双工协定访问服务
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 746a9d64-f21c-426c-b85d-972e916ec6c5
ms.openlocfilehash: 366fd9d6aa220bcbec1ee8fb2a04d1b84755800a
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57678678"
---
# <a name="how-to-access-services-with-a-duplex-contract"></a>如何：使用双工协定访问服务

Windows Communication Foundation (WCF) 的一个功能是能够创建使用双工消息模式的服务。 此模式允许服务通过回调与客户端进行通信。 本主题演示创建 WCF 客户端实现回调接口的客户端类中的步骤。

双向绑定向服务公开客户端的 IP 地址。 客户端应使用安全来确保仅连接到自己信任的服务。

有关创建基本 WCF 服务和客户端的教程，请参阅[入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)。

## <a name="to-access-a-duplex-service"></a>访问双工服务

1. 创建包含两个接口的服务。 第一个接口用于服务，第二个接口用于回调。 有关创建双工服务的详细信息，请参阅[如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)。

2. 运行服务。

3. 使用[ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)为客户端生成协定 （接口）。 有关如何执行此操作的信息，请参阅[如何：创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。

4. 在客户端类中实现回调接口，如下面的示例所示。

    ```csharp
    public class CallbackHandler : ICalculatorDuplexCallback
    {
        public void Result(double result)
        {
            Console.WriteLine("Result ({0})", result);
        }
        public void Equation(string equation)
        {
            Console.WriteLine("Equation({0})", equation);
        }
    }
    ```

    ```vb
    Public Class CallbackHandler
    Implements ICalculatorDuplexCallback
       Public Sub Result (ByVal result As Double)
          Console.WriteLine("Result ({0})", result)
       End Sub
        Public Sub Equation(ByVal equation As String)
            Console.WriteLine("Equation({0})", equation)
        End Sub
    End Class
    ```

5. 创建 <xref:System.ServiceModel.InstanceContext> 类的一个实例。 构造函数需要客户端类的一个实例。

    ```csharp
    InstanceContext site = new InstanceContext(new CallbackHandler());
    ```

    ```vb
    Dim site As InstanceContext = New InstanceContext(new CallbackHandler())
    ```

6. 创建的 WCF 客户端使用需要的构造函数实例<xref:System.ServiceModel.InstanceContext>对象。 该构造函数的第二个参数是配置文件中找到的终结点的名称。

    ```csharp
    CalculatorDuplexClient wcfClient = new CalculatorDuplexClient(site, "default");
    ```

    ```vb
    Dim wcfClient As New CalculatorDuplexClient(site, "default")
    ```

7. 调用 WCF 客户端所需的方法。

## <a name="example"></a>示例

下面的代码示例演示如何创建一个访问双工协定的客户端类。

[!code-csharp[S_DuplexClients#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_duplexclients/cs/client.cs#1)]
[!code-vb[S_DuplexClients#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_duplexclients/vb/client.vb#1)]

## <a name="see-also"></a>请参阅

- [入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)
- [如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)
- [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)
- [如何：创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
- [如何：考虑使用 ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)
