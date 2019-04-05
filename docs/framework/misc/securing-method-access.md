---
title: 保护方法访问
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- code security, method access
- secure coding, method access
- security [.NET Framework], method access
- method access security
ms.assetid: f7c2d6ec-3b18-4e0e-9991-acd97189d818
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8ad7c9aba84a769cb4ea16a2d288b1a9b4f17ca5
ms.sourcegitcommit: d9a0071d0fd490ae006c816f78a563b9946e269a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2019
ms.locfileid: "55066007"
---
# <a name="securing-method-access"></a>保护方法访问
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 某些方法可能不适用于允许任意不受信任的代码进行调用。 此类方法会带来几种风险：该方法可能会提供一些受限制的信息;它可能信任传递给它; 的任何信息它可能不会执行错误检查的参数;或使用错误的参数，它可能会出现故障或执行某些有害操作。 应该注意这些情况，并采取措施以帮助保护这类方法。  
  
 在某些情况下，可能需要限制并不打算用于公共用途但仍须为公共方法的方法。 例如，可能有一个需在你自己的 DLL 间调用（从而必须为公共接口）的接口，但你不希望将其以公共方式公开，以防止客户使用它，或防止恶意代码利用入口点进入组件中。 限制不打算用于公共用途（但必须为公共方法）的方法的另一个常见理由是：为了避免不得不记录和支持可能是内部接口的接口。  
  
 托管代码提供几种方法来限制方法访问：  
  
-   如果可以信任类、程序集或派生类，则限制它们的可访问性的范围。 这是限制方法访问的最简单的方法。 请注意，派生类的可信度通常可低于其从中派生的类，尽管在某些情况下它们共享父类的标识。 具体而言，不推断从关键字**保护**，这不一定使用的安全上下文中。  
  
-   限制对指定的标识-从根本上讲，任何特定的调用方的方法访问[证据](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7y5x1hcd%28v=vs.100%29)选择 （强名称、 发布服务器、 区域等）。  
  
-   限制对具有你选择的任何权限的调用方的方法访问。  
  
 同样，声明性安全使你可以控制类的继承。 可以使用**InheritanceDemand**来执行以下操作：  
  
-   要求派生类具有指定的标识或权限。  
  
-   要求重写特定方法的派生类具有指定的标识或权限。  
  
 下面的示例演示如何通过要求使用特定强名称对调用方进行签名来帮助保护具有有限访问权限的公共类。 此示例使用<xref:System.Security.Permissions.StrongNameIdentityPermissionAttribute>与**需**为强名称。 有关如何为程序集具有强名称签名的基于任务的信息，请参阅[创建和使用具有强名称程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)。  
  
```vb  
<StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey := "…hex…", Name := "App1", Version := "0.0.0.0")>  _  
Public Class Class1  
End Class  
```  
  
```csharp  
[StrongNameIdentityPermissionAttribute(SecurityAction.Demand, PublicKey="…hex…", Name="App1", Version="0.0.0.0")]  
public class Class1  
{  
  
}   
```  
  
## <a name="excluding-classes-and-members-from-use-by-untrusted-code"></a>防止不受信任的代码使用类和成员  
 使用本节中所示的声明来防止部分受信任的代码使用特定的类、方法以及属性和事件。 将这些声明应用到类，即可对类的所有方法、属性和事件应用保护；但请注意，字段访问不受声明性安全影响。 也请注意，链接要求仅帮助不受直接调用方的攻击，可能仍会受到引诱攻击。  
  
> [!NOTE]
>  [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中引入了新的透明度模型。 [安全透明的代码，级别 2](../../../docs/framework/misc/security-transparent-code-level-2.md)模型标识安全代码与<xref:System.Security.SecurityCriticalAttribute>属性。 安全关键代码需要调用方和继承者均完全受信任。 在早期 .NET Framework 版本中的代码访问安全性规则下运行的程序集可以调用级别 2 程序集。 在这种情况下，安全关键属性将被视为完全信任的链接要求。  
  
 在强名称的程序集中[LinkDemand](../../../docs/framework/misc/link-demands.md)应用于所有可以访问的方法、 属性和其中到完全受信任调用方限制其使用的事件。 若要禁用此功能，必须应用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 特性。 因此，仅未签名的程序集或具有此特性的程序集需要显式标记类以排除不受信任调用方；可以使用这些声明来标记其中并不打算用于不受信任的调用方的类型子集。  
  
 下面的示例说明如何防止不受信任的代码使用类和成员。  
  
 对于公共非密封类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _   
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
Public Class CanDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public class CanDeriveFromMe  
{  
}  
```  
  
 对于公共密封类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
NotInheritable Public Class CannotDeriveFromMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public sealed class CannotDeriveFromMe  
{  
}  
```  
  
 对于公共抽象类：  
  
```vb  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name := "FullTrust"), _  
System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name := "FullTrust")>  _  
MustInherit Public Class CannotCreateInstanceOfMe_CanCastToMe  
End Class  
```  
  
```csharp  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
public abstract class CannotCreateInstanceOfMe_CanCastToMe {}  
```  
  
 对于公共虚拟函数：  
  
```vb  
Class Base1   
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overridable Sub CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Base1  
```  
  
```csharp  
class Base1   
{  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name="FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]  
    public virtual void CanOverrideOrCallMe() {}  
}  
```  
  
 对于公共抽象函数：  
  
```vb  
MustInherit Class Base2  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Sub MustOverrideMe()  
    End Sub  
End Class 'Base2  
```  
  
```csharp  
abstract class Base2 {  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(  
System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
public abstract void MustOverrideMe();  
}  
```  
  
 对于基类不要求完全信任的公共重写函数：  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe  
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 对于基类要求完全信任的公共重写函数：  
  
```vb  
Class Derived  
    Inherits Base1  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust")> _  
    Public Overrides Sub CanOverrideOrCallMe()  
        MyBase.CanOverrideOrCallMe()  
    End Sub 'CanOverrideOrCallMe   
End Class 'Derived  
```  
  
```csharp  
class Derived : Base1  
{     
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name="FullTrust")]      
    public override void CanOverrideOrCallMe()   
    {  
        base.CanOverrideOrCallMe();  
    }  
}  
```  
  
 对于公共接口：  
  
```vb  
Public Interface ICanCastToMe  
    <System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
    Sub CanImplementMe()  
End Interface 'ICanCastToMe  
<System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name:="FullTrust"), System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name:="FullTrust")> _  
Class Implemented  
    Implements ICanCastToMe  
    Public Sub CanImplementMe()  
    End Sub 'CanImplementMe  
```  
  
```csharp  
public interface ICanCastToMe   
{  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
void CanImplementMe();  
}  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
[System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.InheritanceDemand, Name = "FullTrust")]  
class Implemented : ICanCastToMe  
{  
    public void CanImplementMe()  
    {  
    }  
}  
```  
  
## <a name="virtual-internal-overrides-or-overloads-overridable-friend"></a>Virtual Internal 重写或 Overloads Overridable Friend  
  
> [!NOTE]
>  本部分中的安全问题时将方法声明为同时发出警告`virtual`并`internal`(`Overloads` `Overridable` `Friend`在 Visual Basic 中)。 此警告仅适用于.NET framework 1.0 和 1.1 版，不适用于更高版本。  
  
 在.NET framework 1.0 和 1.1 版中，您必须注意类型系统可访问性的细微差别时确认你的代码对其他程序集不可用。 声明的方法**虚拟**并**内部**(**Overloads Overridable Friend**在 Visual Basic 中) 可以重写父类的 vtable 条目，并可以仅通过使用在同一程序集中因为它是内部。 但是，由重写的可访问性**虚拟**关键字，并且可以覆盖从另一个程序集，只要该代码有权访问类本身。 如果重写可能会出现问题，使用声明性安全来解决问题，或删除**虚拟**如果不是绝对必需的关键字。  
  
 请注意，即使语言编译器通过编译错误防止这些重写，使用其他编译器编写的代码也可能发生重写。  
  
## <a name="see-also"></a>请参阅
- [安全编码准则](../../../docs/standard/security/secure-coding-guidelines.md)
