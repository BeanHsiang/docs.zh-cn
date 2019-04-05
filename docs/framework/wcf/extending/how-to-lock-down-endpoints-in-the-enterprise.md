---
title: 如何：在企业中的锁定终结点
ms.date: 03/30/2017
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
ms.openlocfilehash: 5392db25c0e3ae0051a892831dd013063389d863
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54663059"
---
# <a name="how-to-lock-down-endpoints-in-the-enterprise"></a>如何：在企业中的锁定终结点
大企业往往要求开发的应用程序符合企业安全策略。 以下主题讨论如何开发和安装客户端的终结点验证程序，它可以用来验证安装在计算机上的所有 Windows Communication Foundation (WCF) 客户端应用程序。  
  
 在这种情况下，验证程序是客户端验证程序，因为此终结点行为添加到客户端[ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) machine.config 文件中的部分。 WCF 加载公共终结点行为仅针对客户端应用程序，并加载常见服务行为仅用于服务应用程序。 若要为服务应用程序安装此相同验证程序，验证程序必须为服务行为。 有关详细信息，请参阅[ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)部分。  
  
> [!IMPORTANT]
>  服务或终结点行为未标有<xref:System.Security.AllowPartiallyTrustedCallersAttribute>特性 (APTCA) 添加到[ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)节的配置文件，则不运行应用程序在部分信任环境中运行时发生这种情况时引发的环境和任何异常。 若要强制运行公共行为（如验证程序），必须执行以下任一操作：  
>   
>  -- 使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性标记公共行为，使其可在部署为部分信任应用程序时运行。 请注意，可以在计算机上设置注册表项，以防运行标有 APTCA 的程序集。  
>   
>  -- 确保如果应用程序是作为完全受信任的应用程序部署的，则用户不能修改代码访问安全设置，从而无法在部分信任环境中运行该应用程序。 如果用户可以这样做，则自定义验证程序不会运行，且不引发任何异常。 若要确保这一点的一种方法，请参阅`levelfinal`选项使用[代码访问安全策略工具 (Caspol.exe)](https://go.microsoft.com/fwlink/?LinkId=248222)。  
>   
>  有关详细信息，请参阅[部分信任的最佳做法](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)并[Supported Deployment Scenarios](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)。  
  
### <a name="to-create-the-endpoint-validator"></a>创建终结点验证程序  
  
1.  使用 <xref:System.ServiceModel.Description.IEndpointBehavior> 方法中所需的验证步骤创建一个 <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A>。 下面的代码提供了一个示例。 (`InternetClientValidatorBehavior`取自[安全验证](../../../../docs/framework/wcf/samples/security-validation.md)示例。)  
  
     [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]  
  
2.  创建用于注册步骤 1 中创建的终结点验证程序的新 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>。 下面的代码示例演示了此过程。 (此示例中的原始代码位于[安全验证](../../../../docs/framework/wcf/samples/security-validation.md)示例。)  
  
     [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]  
  
3.  确保用强名称对编译的程序集签名。 有关详细信息，请参阅[强名称工具 (SN。EXE)](https://go.microsoft.com/fwlink/?LinkId=248217)和您的语言的编译器命令。  
  
### <a name="to-install-the-validator-into-the-target-computer"></a>将验证程序安装到目标计算机中  
  
1.  使用恰当的机制安装终结点验证程序。 在企业中，可以使用组策略和 Systems Management Server (SMS)。  
  
2.  强名称程序集安装到全局程序集缓存使用[Gacutil.exe （全局程序集缓存工具）](../../../../docs/framework/tools/gacutil-exe-gac-tool.md)。  
  
3.  使用 <xref:System.Configuration?displayProperty=nameWithType> 命名空间类型执行以下操作：  
  
    1.  将扩展名添加到[ \<behaviorExtensions >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviorextensions.md)部分使用完全限定的类型名称，并锁定该元素。  
  
         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]  
  
    2.  添加到的行为元素`EndpointBehaviors`的属性[ \<commonBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md)节并锁定该元素。 （若要在服务上安装验证程序，该验证程序必须是 <xref:System.ServiceModel.Description.IServiceBehavior>，并已添加到 `ServiceBehaviors` 属性。）下面的代码示例演示执行步骤 a. 和 b. 之后的适当配置，唯一例外是有没有强名称。  
  
         [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]  
  
    3.  保存 machine.config 文件。 下面的代码示例执行步骤 3 中的所有任务，但在本地保存已修改的 machine.config 文件的副本。  
  
         [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何将公共行为添加到 machine.config 文件并将副本保存到磁盘。 `InternetClientValidatorBehavior`取自[安全验证](../../../../docs/framework/wcf/samples/security-validation.md)示例。  
  
 [!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 您可能还需要对配置文件元素进行加密。 有关更多信息，请参见“另请参见”部分。  
  
## <a name="see-also"></a>请参阅
- [使用 DPAPI 加密配置文件元素](https://go.microsoft.com/fwlink/?LinkId=94954)
- [使用 RSA 加密配置文件元素](https://go.microsoft.com/fwlink/?LinkId=94955)
