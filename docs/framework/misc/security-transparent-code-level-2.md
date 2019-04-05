---
title: 安全透明的代码，级别 2
ms.date: 03/30/2017
helpviewer_keywords:
- transparency
- level 2 transparency
- security-transparent code
- security-critical code
ms.assetid: 4d05610a-0da6-4f08-acea-d54c9d6143c0
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8425b294328d4fc7546a372b329d8fa834a088d6
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54567017"
---
# <a name="security-transparent-code-level-2"></a>安全透明的代码，级别 2
<a name="top"></a>
[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 中引入了 2 级透明度。 此模型的三条原则是透明代码、安全可靠关键代码和安全关键代码。  
  
-   透明代码（包括以完全信任权限运行的代码）只能调用其他透明代码或安全可靠关键代码。 它只能执行域的部分信任权限集（如果存在）允许的操作。 透明代码不能：  
  
    -   执行 <xref:System.Security.CodeAccessPermission.Assert%2A> 或特权提升。  
  
    -   包含不安全或不可验证的代码。  
  
    -   直接调用关键代码。  
  
    -   调用本机代码或具有 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> 特性的代码。  
  
    -   调用受 <xref:System.Security.Permissions.SecurityAction.LinkDemand> 保护的成员。  
  
    -   从关键类型继承。  
  
     此外，透明方法不能重写关键虚拟方法或实现关键接口方法。  
  
-   可靠关键代码是完全信任的代码，且可被透明代码调用的代码。 它公开完全信任代码的有限外围应用；可靠关键代码中会进行准确性和安全性验证。  
  
-   安全关键代码可以调用完全信任的任何代码，但不能被透明代码调用。  
  
 本主题包含以下各节：  
  
-   [用法示例和行为](#examples)  
  
-   [重写模式](#override)  
  
-   [继承规则](#inheritance)  
  
-   [其他信息和规则](#additional)  
  
<a name="examples"></a>   
## <a name="usage-examples-and-behaviors"></a>用法示例和行为  
 若要指定 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 规则（ 2 级透明度），请对程序集使用以下批注：  
  
```  
[assembly: SecurityRules(SecurityRuleSet.Level2)]  
```  
  
 若要锁定至 .NET Framework 2.0 规则（1 级透明度），请使用以下批注：  
  
```  
[assembly: SecurityRules(SecurityRuleSet.Level1)]  
```  
  
 如果不对程序集进行批注，则默认使用 [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] 规则。 但是，建议的最佳做法是使用<xref:System.Security.SecurityRulesAttribute>特性而不是依赖默认值。  
  
### <a name="assembly-wide-annotation"></a>程序集范围的批注  
 以下规则适用于程序集级别的特性使用：  
  
-   没有属性：如果未指定任何属性，在运行时将所有代码解释为安全关键的除非安全关键违反继承规则 (例如，当重写或实现透明虚拟或接口方法)。 在这些情况下，方法是可靠关键方法。 指定无特性会导致公用语言运行时为你确定透明度规则。  
  
-   `SecurityTransparent`：所有代码都是透明的;整个程序集不会执行任何特权或不安全。  
  
-   `SecurityCritical`：由此类型引入此程序集的所有代码都是关键代码；其他所有代码都是透明的。 这种情况类似于不指定任何特性，但公共语言运行时不会自动确定透明度规则。 例如，如果重写虚拟方法或抽象方法或者实现接口方法，默认情况下，该方法是透明的。 你必须将方法显式批注为 `SecurityCritical` 或 `SecuritySafeCritical`；否则加载时将引发 <xref:System.TypeLoadException>。 当基类和派生类位于相同的程序集时，此规则也适用。  
  
-   `AllowPartiallyTrustedCallers` （级别 2 仅）：所有代码默认都是透明的。 但是，各个类型和成员可以有其他特性。  
  
 下表比较了 2 级与 1 级的程序集级别行为。  
  
|Assembly 特性|级别2|级别1|  
|------------------------|-------------|-------------|  
|部分信任的程序集上无特性|类型和成员默认是透明的，但可以是安全关键或安全可靠关键的。|所有类型和成员都是透明的。|  
|无特性|指定无特性会导致公用语言运行时为你确定透明度规则。 所有类型和成员都是安全关键的，除非安全关键违反继承规则。|在完全信任的程序集上（在全局程序缓集缓存或 `AppDomain` 中标识为完全信任的程序集中），所有类型都是透明的，所有成员都是安全可靠关键的。|  
|`SecurityTransparent`|所有类型和成员都是透明的。|所有类型和成员都是透明的。|  
|`SecurityCritical(SecurityCriticalScope.Everything)`|不适用。|所有类型和成员都是安全关键的。|  
|`SecurityCritical`|由此类型引入此程序集的所有代码都是关键代码；其他所有代码都是透明的。 如果重写虚拟方法或抽象方法或者实现接口方法，则必须将方法显式批注为 `SecurityCritical` 或 `SecuritySafeCritical`。|所有代码默认都是透明的。 但是，各个类型和成员可以有其他特性。|  
  
### <a name="type-and-member-annotation"></a>类型和成员批注  
 适用于安全类型的安全特性也适用于该类型引入的成员。 但是，这些规则不适用于基类或接口实现的虚拟或抽象重写。 以下规则适用于类型和成员级别的特性使用：  
  
-   `SecurityCritical`：类型或成员至关重要，可以通过完全信任代码调用。 安全关键类型中引入的方法是关键的。  
  
    > [!IMPORTANT]
    >  基类或接口中引入的以及安全关键类中重写或实现的虚拟和抽象方法默认是透明的。 这些方法必须标识为 `SecuritySafeCritical` 或 `SecurityCritical`。  
  
-   `SecuritySafeCritical`：类型或成员是可靠关键的。 但是，类型或成员可以从透明（部分信任的）代码调用，并且与任何其他关键代码一样。 必须审核代码的安全性。  
  
 [返回页首](#top)  
  
<a name="override"></a>   
## <a name="override-patterns"></a>重写模式  
 下表显示 2 级透明度允许的方法重写。  
  
|基虚拟/接口成员|重写/接口|  
|------------------------------------|-------------------------|  
|`Transparent`|`Transparent`|  
|`Transparent`|`SafeCritical`|  
|`SafeCritical`|`Transparent`|  
|`SafeCritical`|`SafeCritical`|  
|`Critical`|`Critical`|  
  
 [返回页首](#top)  
  
<a name="inheritance"></a>   
## <a name="inheritance-rules"></a>继承规则  
 在此部分中，基于访问权限和功能对 `Transparent`、`Critical` 和 `SafeCritical` 代码指定以下顺序：  
  
 `Transparent` < `SafeCritical` < `Critical`  
  
-   类型的规则：我们从左到右，访问变得更具限制性。 派生类型至少必须与基类型具有相同的受限访问权限。  
  
-   方法的规则：派生的方法不能从基方法更改可访问性。 对于默认行为，不带批注的所有派生方法都是 `Transparent`。 如果重写方法未显示批注为 `SecurityCritical`，则派生关键类型会导致引发异常。  
  
 下表显示允许的类型继承模式。  
  
|基类|派生类可以是|  
|----------------|--------------------------|  
|`Transparent`|`Transparent`|  
|`Transparent`|`SafeCritical`|  
|`Transparent`|`Critical`|  
|`SafeCritical`|`SafeCritical`|  
|`SafeCritical`|`Critical`|  
|`Critical`|`Critical`|  
  
 下表显示不允许的类型继承模式。  
  
|基类|派生类不可以是|  
|----------------|-----------------------------|  
|`SafeCritical`|`Transparent`|  
|`Critical`|`Transparent`|  
|`Critical`|`SafeCritical`|  
  
 下表显示允许的方法继承模式。  
  
|基方法|派生方法可以是|  
|-----------------|---------------------------|  
|`Transparent`|`Transparent`|  
|`Transparent`|`SafeCritical`|  
|`SafeCritical`|`Transparent`|  
|`SafeCritical`|`SafeCritical`|  
|`Critical`|`Critical`|  
  
 下表显示不允许的方法继承模式。  
  
|基方法|派生方法不可以是|  
|-----------------|------------------------------|  
|`Transparent`|`Critical`|  
|`SafeCritical`|`Critical`|  
|`Critical`|`Transparent`|  
|`Critical`|`SafeCritical`|  
  
> [!NOTE]
>  这些继承规则适用于 2 级类型和成员。 1 级程序集中的类型可以从 2 级安全关键类型和成员继承。 因此，2 级类型和成员必须与 1 级继承者具有不同的继承需求。  
  
 [返回页首](#top)  
  
<a name="additional"></a>   
## <a name="additional-information-and-rules"></a>其他信息和规则  
  
### <a name="linkdemand-support"></a>LinkDemand 支持  
 2 级透明度模型将 <xref:System.Security.Permissions.SecurityAction.LinkDemand> 替换为 <xref:System.Security.SecurityCriticalAttribute> 特性。 在遗留（1 级）代码中，<xref:System.Security.Permissions.SecurityAction.LinkDemand> 自动被视为 <xref:System.Security.Permissions.SecurityAction.Demand>。  
  
### <a name="reflection"></a>映像  
 调用关键方法或读取关键字段会触发对完全信任权限的要求（就像调用私有方法或字段一样）。 因此，完全信任的代码可以调用关键方法，而部分信任的代码则不能。  
  
 以下属性已添加到 <xref:System.Reflection> 命名空间，以确定类型、方法或字段是否为 `SecurityCritical``SecuritySafeCritical` 或 `SecurityTransparent`：<xref:System.Type.IsSecurityCritical%2A>、<xref:System.Reflection.MethodBase.IsSecuritySafeCritical%2A> 和 <xref:System.Reflection.MethodBase.IsSecurityTransparent%2A>。 使用这些属性可通过反射而非检查特性是否存在确定透明度。 透明度规则比较复杂，检查特性可能不够充分。  
  
> [!NOTE]
>  一个`SafeCritical`方法将返回`true`同时<xref:System.Type.IsSecurityCritical%2A>并<xref:System.Reflection.MethodBase.IsSecuritySafeCritical%2A>，这是因为`SafeCritical`事实上是关键的 （它具有相同的功能与关键代码，但它可以从透明代码调用）。  
  
 动态方法继承其附加到的模块的透明度；他们不继承类型的透明度（如果它们附加到一个类型）。  
  
### <a name="skip-verification-in-full-trust"></a>在完全信任的环境中跳过验证  
 你可以通过在 <xref:System.Security.SecurityRulesAttribute> 特性中将 <xref:System.Security.SecurityRulesAttribute.SkipVerificationInFullTrust%2A> 属性设置为 `true`，跳过完全信任的透明程序集的验证。  
  
 `[assembly: SecurityRules(SecurityRuleSet.Level2, SkipVerificationInFullTrust = true)]`  
  
 <xref:System.Security.SecurityRulesAttribute.SkipVerificationInFullTrust%2A> 属性默认为 `false`，因此该属性必须设置为 `true` 才能跳过验证。 只能出于优化目的跳过验证。 应确保在程序集中的透明代码是通过使用验证`transparent`选项[PEVerify 工具](../../../docs/framework/tools/peverify-exe-peverify-tool.md)。  
  
## <a name="see-also"></a>请参阅
- [安全透明代码，级别 1](../../../docs/framework/misc/security-transparent-code-level-1.md)
- [安全更改](../../../docs/framework/security/security-changes.md)
