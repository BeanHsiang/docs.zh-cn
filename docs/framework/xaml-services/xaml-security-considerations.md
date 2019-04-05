---
title: XAML 安全注意事项
ms.date: 03/30/2017
helpviewer_keywords:
- security [XAML Services], .NET XAML services
- XAML security [XAML Services]
ms.assetid: 544296d4-f38e-4498-af49-c9f4dad28964
ms.openlocfilehash: 6cd09295f9dac26011652d6b0a33318841b04072
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54648357"
---
# <a name="xaml-security-considerations"></a>XAML 安全注意事项
本主题介绍在应用程序中安全性的最佳做法，当您使用 XAML 和.NET Framework XAML 服务 API。  
  
## <a name="untrusted-xaml-in-applications"></a>在应用程序中不受信任的 XAML  
 在最常规的意义上，不受信任的 XAML 是你的应用程序不是专门未包括或发出任何 XAML 源。  
  
 XAML 是编译为或存储为`resx`-类型受信任且经过签名的程序集内的资源不是本质上是不受信任。 为您信任的程序集作为一个整体，您可以信任 XAML。 在大多数情况下，你是只关心松散 XAML，这是从流或其他 I/O 加载的 XAML 源的信任方面。 松散 XAML 不是特定的组件或功能的部署和打包基础结构的应用程序模型。 但是，程序集可能会实现涉及加载松散 XAML 的行为。  
  
 有关不受信任的 XAML，您应该像通常相同，就好像不受信任的代码。 使用沙盒或其他形式来阻止访问受信任的代码可能不受信任的 XAML。  
  
 XAML 功能的特性提供 XAML 构造对象和设置其属性的权限。 这些功能还包括访问映射和访问应用程序域中的程序集使用标记扩展的类型转换器`x:Code`块，依次类推。  
  
 除了其语言级别功能，XAML 用于用户界面定义中的许多技术。 正在加载不受信任的 XAML 可能意味着加载恶意电子欺骗用户界面。  
  
## <a name="sharing-context-between-readers-and-writers"></a>共享读取器和编写器之间的上下文  
 XAML 读取器和 XAML 编写器的.NET Framework XAML 服务体系结构通常要求共享到 XAML 编写器或共享的 XAML 架构上下文的 XAML 读取器。 如果你正在编写 XAML 节点循环逻辑，或者提供自定义保存路径可能需要共享的对象或上下文。 不应共享 XAML 读取器实例、 非默认 XAML 架构上下文或受信任和不受信任代码之间的 XAML 读取器/编写器类的设置。  
  
 大多数方案和涉及 XAML 对象编写的基于 CLR 的类型支持的操作可以只使用默认 XAML 架构上下文。 默认 XAML 架构上下文未显式包含可能会危害完全信任的设置。 因此，它是安全地共享受信任和不受信任的 XAML 读取器/编写器组件之间的上下文。 但是，如果执行此操作时，它仍是最佳的做法是尽量在单独的此类的阅读器和编写器<xref:System.AppDomain>作用域，使用专用于/进行沙盒处理以部分信任的其中之一。  
  
## <a name="xaml-namespaces-and-assembly-trust"></a>XAML 命名空间和程序集信任  
 受信任和不受信任程序集加载到应用程序域之间没有区别的基本的非限定的语法和 XAML 如何解释到程序集的自定义 XAML 命名空间映射的定义。 因此，它是从技术上讲可能不受信任的程序集以欺骗受信任的程序集的预期的 XAML 命名空间映射，并捕获 XAML 源的声明的对象和属性信息。 如果你有安全需求，从而避免这种情况下，应当生成预期的 XAML 命名空间映射，使用以下方法之一：  
  
-   具有强名称，在任何 XAML 命名空间映射中所做的应用程序的 XAML 中使用完全限定的程序集的名称。  
  
-   限制程序集映射到一组固定的引用程序集，通过构造特定<xref:System.Xaml.XamlSchemaContext>在 XAML 读取器和 XAML 对象编写器。 请参阅 <xref:System.Xaml.XamlSchemaContext.%23ctor%28System.Collections.Generic.IEnumerable%7BSystem.Reflection.Assembly%7D%29>。  
  
## <a name="xaml-type-mapping-and-type-system-access"></a>XAML 类型映射和类型系统访问  
 XAML 支持其自己的类型系统，这在许多方面与 CLR 如何实现基本的 CLR 类型系统对等。 但是，您将基于其类型信息的类型的信任决定的类型意识的某些方面，您应延迟到 CLR 后备类型中的类型信息。 这是因为某些 XAML 类型系统的特定报告功能均保持打开状态作为虚拟方法，因此，不完全受控制的原始的.NET Framework XAML 服务实现。 这些扩展点存在，因为 XAML 类型系统是可扩展的使之与 XAML 本身的可扩展性和与使用默认 CLR 支持实现和默认 XAML 架构上下文及其可能的替代类型映射策略。 详细信息，请参阅特定说明多个的属性上<xref:System.Xaml.XamlType>和<xref:System.Xaml.XamlMember>。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Xaml.Permissions.XamlAccessLevel>
