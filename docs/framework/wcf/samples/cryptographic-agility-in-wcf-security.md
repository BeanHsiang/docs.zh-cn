---
title: WCF 安全中的加密灵活性
ms.date: 03/30/2017
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
ms.openlocfilehash: 64519e51b82780ce2b355251245d77bff0a9e73b
ms.sourcegitcommit: 14355b4b2fe5bcf874cac96d0a9e6376b567e4c7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/30/2019
ms.locfileid: "55273314"
---
# <a name="cryptographic-agility-in-wcf-security"></a>WCF 安全中的加密灵活性

此示例演示如何在要提供加密的敏捷实现 Windows Communication Foundation (WCF) 客户端和服务中的标准/自定义算法中指定。 该示例由下列项目组成：

**服务**

这是自承载的 WCF 服务，实现`ICalculator`接口，并保护终结点使用<xref:System.ServiceModel.WSHttpBinding>与安全会话和可靠会话被禁用。 该服务定义一个自定义 `SecurityAlgorithmSuite` 类，以指定要用于消息安全的加密算法。

**客户端**

这是 WCF 客户端身份验证成功后访问该服务。 该客户端调用由 `ICalculator` 接口公开并由服务实现的操作。 该客户端也定义相同的自定义 `SecurityAlgorithmSuite` 类，以指定要用于消息安全的加密算法。

## <a name="to-use-this-sample"></a>使用此示例

1. 在 Visual Studio 2012 中打开 CryptoAgility.sln 解决方案。

2. 按 Ctrl+Shift+B 生成解决方案。

3. 打开[!INCLUDE[fileExplorer](~/includes/fileexplorer-md.md)]并导航到 \WCF\Basic\Security\CryptoAgility\Service\bin 目录，并使用管理员特权运行 service.exe 文件，通过右击 service.exe 并选择**以管理员身份运行**。

4. 导航到 \WCF\Basic\Security\CryptoAgility\Client\bin 目录并正常运行 client.exe 文件。

> [!IMPORTANT]
> 您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> 如果此目录不存在，请转到[Windows Communication Foundation (WCF) 和.NET Framework 4 的 Windows Workflow Foundation (WF) 示例](https://go.microsoft.com/fwlink/?LinkId=150780)若要下载所有 Windows Communication Foundation (WCF) 和[!INCLUDE[wf1](../../../../includes/wf1-md.md)]示例。 此示例位于以下目录：
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`

## <a name="see-also"></a>请参阅

- [Windows Communication Foundation 安全性](../feature-details/security.md)