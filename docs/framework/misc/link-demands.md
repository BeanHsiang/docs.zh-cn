---
title: 链接需求
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [.NET Framework], demands
- demanded permissions
- permissions [.NET Framework], demands
- granting permissions, demands
- code access security, demands
- user demands for permission
- caller security checks
- link demands
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2f55e282309d21b78c0aad9e7ada687f23628379
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54725670"
---
# <a name="link-demands"></a>链接需求
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 链接要求导致在实时编译过程中进行安全检查，并且只检查代码的直接调用程序集。 当代码绑定到类型引用（包括函数指针引用和方法调用）时发生链接。 如果调用程序集的权限不足以链接到代码，则加载并运行代码时将不允许该链接且将引发运行时异常。 可在继承自代码的类中重写链接要求。  
  
 请注意，不使用此类型的要求执行完整的堆栈审核，并且代码仍容易遭受引诱攻击。 例如，如果程序集 A 中的方法受链接要求，则程序集 B 中的直接调用方被评估基于程序集 B 的权限 但是，链接要求将不评估程序集 C 中的方法间接调用该方法在程序集中使用的方法在程序集 b。链接要求指定的权限仅直接中直接调用程序集的调用方必须具有链接到你的代码。 而不指定所有调用方为了运行你的代码所必须拥有的权限。  
  
 <xref:System.Security.CodeAccessPermission.Assert%2A>、<xref:System.Security.CodeAccessPermission.Deny%2A> 和 <xref:System.Security.CodeAccessPermission.PermitOnly%2A> 堆栈审核修饰符不影响链接要求计算。  由于链接要求不执行堆栈审核，所以堆栈审核修饰符对链接要求并无影响。  
  
 如果通过访问链接要求保护的方法[反射](../../../docs/framework/reflection-and-codedom/reflection.md)，则链接要求检查通过反射访问的代码的直接调用方。 对于使用反射执行的方法发现和方法调用都是如此。 例如，假设代码使用反射来返回<xref:System.Reflection.MethodInfo>对象，表示方法受链接要求，然后将其传递**MethodInfo**对使用该对象来调用原始方法的一些其他代码的对象。 在这种情况下链接请求检查会进行两次： 一次针对返回的代码**MethodInfo**对象，并对其进行调用的代码一次。  
  
> [!NOTE]
>  在静态类构造函数上执行的链接要求不保护构造函数，因为静态构造函数是在应用程序的代码执行路径外部由系统调用的。 因此，当链接要求应用于整个类时，它不能保护对静态构造函数的访问，尽管它确实保护类的其余部分。  
  
 下面的代码片段以声明方式指定链接到 `ReadData` 方法的任何代码必须具有 `CustomPermission` 权限。 此权限是假设的自定义权限，在 .NET Framework 中并不存在。 该请求通过传递**SecurityAction.LinkDemand**标记，用于`CustomPermissionAttribute`。  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function    
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## <a name="see-also"></a>请参阅
- [属性](../../../docs/standard/attributes/index.md)
- [代码访问安全性](../../../docs/framework/misc/code-access-security.md)
