---
title: x:Uid 指令
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], localizable content attribute
- XAML [XAML Services], x:Uid attribute
- x:Uid attribute [XAML Services]
- Uid attribute [XAML Services]
ms.assetid: 81defade-483b-4a89-b76d-9b25bba34010
ms.openlocfilehash: 6e946c63227a06b2032ce27e61899c1b8f05ec9f
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58042969"
---
# <a name="xuid-directive"></a>x:Uid 指令
提供的标记元素的唯一标识符。 在许多情况下，此唯一标识符将使用 XAML 本地化流程和工具。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性用法  
  
```xaml  
<object x:Uid="identifier"... />  
```  
  
## <a name="xaml-values"></a>XAML 值  
  
|||  
|-|-|  
|`identifier`|手动创建或自动生成的字符串应该是唯一的文件中来进行解释时`x:Uid`使用者。|  
  
## <a name="remarks"></a>备注  
 在 [MS-XAML]`x:Uid`定义为一个指令。 有关详细信息，请参阅[ \[MS XAML\]部分 5.3.6](https://go.microsoft.com/fwlink/?LinkId=114525)。  
  
 `x:Uid` 是从离散`x:Name`同时由于规定的 XAML 本地化方案以便用于本地化的标识符没有任何依赖关系的编程模型含义`x:Name`。 此外，`x:Name`受 XAML 名称范围; 但是，`x:Uid`不受任何 XAML 语言定义的概念的强制唯一性。 在广义上讲 （不是本地化流程的一部分的处理器） 中的 XAML 处理器不会强制实施唯一性的`x:Uid`值。 该职责的发起方的值是从概念上讲。 唯一性的假定条件下`x:Uid`单一 XAML 源中的值是合理的值，例如专门的全球化进程或工具的使用者。 典型的唯一性模型是`x:Uid`值内是唯一的表示 XAML 的 XML 编码的文件。  
  
 具有特定的 XAML 架构的重要知识的工具可以选择将应用`x:Uid`仅为 true 可本地化的字符串，而不是所有情况下，在标记中遇到一个文本字符串值。  
  
 框架可以指定特定的属性在其对象模型中为别名`x:Uid`通过将特性应用<xref:System.Windows.Markup.UidPropertyAttribute>到定义的类型。 如果框架指定特定属性，它不是同时指定`x:Uid`和别名成员在同一个对象。 如果这两个`x:Uid`并指定别名成员，.NET Framework XAML 服务 API 通常会引发<xref:System.Xaml.XamlDuplicateMemberException>这种情况下。  
  
## <a name="wpf-usage-notes"></a>WPF 用法说明  
 有关角色的详细信息`x:Uid`WPF 在本地化过程中以及 XAML 的 BAML 形式中，请参阅[WPF 的全球化](../wpf/advanced/globalization-for-wpf.md)或 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A>
- <xref:Microsoft.Build.Tasks.Windows.UidManager>
- [WPF 全球化](../wpf/advanced/globalization-for-wpf.md)
