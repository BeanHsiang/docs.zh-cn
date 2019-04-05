---
title: 使用 WCF 开发工具
ms.date: 03/30/2017
ms.assetid: 054adb87-c244-4d5a-83d1-0b2b44bd454b
ms.openlocfilehash: e9a398ac6914582d299658e3e45d17ea5468917d
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54712085"
---
# <a name="using-the-wcf-development-tools"></a>使用 WCF 开发工具
本部分介绍可以帮助您开发 WCFservice 的 Visual Studio 开发工具。  
  
 您可以使用作为基础的 Visual Studio 模板快速生成你自己的服务，然后使用 WCF 服务自动主机和 WCF 测试客户端来调试和测试你的服务。 通过一起使用这些工具，可以快速完美地完成调试和测试过程，无需在早期阶段提交给承载模型。  
  
## <a name="the-wcf-developer-tools"></a>WCF 开发人员工具  
 [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)  
  
 可以使用 Visual Studio 中的预定义的 Visual Studio 项目和项模板快速生成 WCF 服务和周边应用程序。  
  
 [WCF 服务主机 (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)  
  
 WCF 服务自动主机 (WcfSvcHost.exe) 允许您启动 Visual Studio 调试器 (F5) 以自动承载和测试已实现的服务。 然后，您可以测试使用 WCF 测试客户端 (wcfTestClient.exe) 或自己的客户端查找并解决任何潜在错误的服务。  
  
 [WCF 测试客户端 (WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)  
  
 WCF 测试客户端 (WcfTestClient.exe) 是一个 GUI 工具，您可以输入任意类型的参数，将该服务，以及查看发回响应服务输入提交。 它提供了完美的服务测试体验与 WCF 服务自动主机结合使用时。  
  
 [通过 XML 生成数据类型类](../../../docs/framework/wcf/generating-data-type-classes-from-xml.md)  
  
 可将存储在剪贴板中的 XML 数据粘贴到代码页中。 数据中定义的类将被转换为代码类型。  
  
## <a name="using-the-tools-without-administrator-privilege"></a>在无管理员权限的情况下使用工具  
 若要使不具有管理员权限的用户能够开发 WCF 服务，ACL （访问控制列表） 创建命名空间"http://+:8731/Design_Time_Addresses"在 Visual Studio 安装的过程。 该 ACL 被设置为“(UI)”，这将包括登录到此计算机的所有交互用户。 管理员可以在此 ACL 中添加或移除用户，或者打开其他端口。此 ACL 支持 WCF 或 WF 模板以其各自的默认配置发送和接收数据。 它还使用户能够使用 WCF 服务自动主机 (wcfSvcHost.exe) 而无需向其授予管理员权限。  
  
 可以使用提升的管理员帐户在 [!INCLUDE[wv](../../../includes/wv-md.md)] 中通过 Netsh.exe 工具来修改访问权限。 下面是使用 Netsh.exe 的示例。  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 有关 Netsh.exe 的详细信息，请参阅[如何使用 Netsh.exe 工具和命令行开关](https://go.microsoft.com/fwlink/?LinkId=97877)。  
  
## <a name="see-also"></a>请参阅
- [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)
- [WCF 服务主机 (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
- [WCF 测试客户端 (WcfTestClient.exe)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)
