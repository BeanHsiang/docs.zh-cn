---
title: 安全性和远程处理注意事项
ms.date: 03/30/2017
helpviewer_keywords:
- code security, remoting
- remoting, security
- security [.NET Framework], remoting
- secure coding, remoting
ms.assetid: 125d2ab8-55a4-4e5f-af36-a7d401a37ab0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 39b7bcec1196a59c47717ec2b5622ca8e0d3cdfc
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54591966"
---
# <a name="security-and-remoting-considerations"></a>安全性和远程处理注意事项
利用远程处理，你可以在应用程序域、进程或计算机之间设置透明的调用。 但是，代码访问安全堆栈审核不能跨越进程边界或计算机边界（它确实应用于同一进程的不同应用程序域之间）。  
  
 任何可远程处理的类（从 <xref:System.MarshalByRefObject> 类派生）都需要对安全负责。 要么只将代码用于封闭式安全环境中，在这种环境中可以隐式信任调用代码；要么相应地设计远程处理调用，以免这些调用会让受保护代码受到可能会被恶意使用的外部侵入的影响。  
  
 通常情况下，不应公开方法、 属性或受保护的声明性事件[LinkDemand](../../../docs/framework/misc/link-demands.md)和<xref:System.Security.Permissions.SecurityAction.InheritanceDemand>安全检查。 使用远程处理时，不会强制执行这些检查。 其他安全检查，如<xref:System.Security.Permissions.SecurityAction.Demand>， [Assert](../../../docs/framework/misc/using-the-assert-method.md)，依此类推，工作进程内的应用程序域之间，但在跨进程或跨计算机方案中不起作用。  
  
## <a name="protected-objects"></a>受保护的对象  
 某些对象自己保持安全状态。 不应将这些对象传递给不受信任的代码，否则这样的代码将会获得超越其自身权限的安全授权。  
  
 一个示例是创建 <xref:System.IO.FileStream> 对象。 在创建时将要求具有 <xref:System.Security.Permissions.FileIOPermission>，如果成功，则会返回该文件对象。 但是，如果将此对象引用传递给没有文件权限的代码，则该对象就可以读写此特定文件。  
  
 此类对象的最简单的防御措施就是请求同样**FileIOPermission**设法通过公共 API 元素获取对象引用的任何代码。  
  
## <a name="application-domain-crossing-issues"></a>跨应用程序域问题  
 若要隔离托管宿主环境中的代码，通常使用可以降低各种程序集的权限级别的显式策略来生成多个子应用程序域。 但是，这些程序集的策略在默认的应用程序域中保持不变。 如果其中一个子应用程序域可以强制默认的应用程序域加载一个程序集，则代码隔离就会失去作用，强制加载的程序集中的类型将能够以较高的信任级别运行代码。  
  
 一个应用程序域可以强制另一个应用程序域加载程序集，并通过调用托管在另一个应用程序域中的某个对象的代理来运行该程序集中所包含的代码。 若要获取跨应用程序域的代理，托管该对象的应用程序域必须通过方法调用参数来分发代理，或者是返回值。 或者，如果该应用程序域刚刚创建，则在默认情况下，创建者将具有 <xref:System.AppDomain> 对象的代理。 因此，为了避免破坏代码隔离，在具有较高信任级别的应用程序域中，不应将对引用封送对象的引用分发给信任级别较低的应用程序域，其中引用封送对象指从 <xref:System.MarshalByRefObject> 派生的类的实例。  
  
 通常，默认的应用程序域将创建子应用程序域，每一个子域中带有一个控件对象。 控件对象管理新的应用程序域，它有时从默认应用程序域接受命令，但实际上它不能直接与该域联系。 有时，默认的应用程序域将针对控件对象调用其代理。 但是，有时候控件对象可能需要回调到默认的应用程序域。 在这些情况下，默认的应用程序域向控件对象的构造函数传递一个引用封送回调对象。 控件对象负责保护此代理。 如果控件对象要在公共类的公共静态字段上放置此代理，或者以其他方式公开此代理，则会形成一种危险情形：其他代码将回调到默认的应用程序域。 因此，为使代理保持为私有的，总是隐式信任控件对象。  
  
## <a name="see-also"></a>请参阅
- [安全编码准则](../../../docs/standard/security/secure-coding-guidelines.md)
