---
title: 类型成员的名称
ms.date: 10/22/2008
ms.technology: dotnet-standard
helpviewer_keywords:
- events [.NET Framework], names
- methods [.NET Framework], names
- type members
- properties [.NET Framework], names
- fields, names
- field names
- names [.NET Framework], type members
- members [.NET Framework], type
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
author: KrzysztofCwalina
ms.openlocfilehash: 7cf98b8ed1957352f357c7a9d580b4fd567a1634
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54576936"
---
# <a name="names-of-type-members"></a>类型成员的名称
类型的成员包括：方法、属性、事件、构造函数和字段。 以下各部分介绍各类型成员的命名准则。  
  
## <a name="names-of-methods"></a>方法的名称  
 由于方法是操作执行的途径，所以设计准则要求方法名称是谓词或谓词短语。 通过遵循这一准则，还可将方法名称与属性和类型名称（即名词或形容词短语）区分开来。  
  
 **✓ 务必**使用谓词或谓词短语作为方法名称。  
  
```  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
```  
  
## <a name="names-of-properties"></a>属性的名称  
 与其他成员不同，属性名称须为名词短语或形容词。 这是因为属性引用数据，且属性名称反映了这一点。 应始终为属性名称使用 PascalCasing。  
  
 **✓ 务必**使用名词、名词短语或形容词来命名属性。  
  
 **X 不要**设立与 "Get" 方法名称匹配的属性，如下例所示：  
  
 `public string TextWriter { get {...} set {...} }`  
 `public string GetTextWriter(int value) { ... }`  
  
 此模式通常表明该属性实际上应是一种方法。  
  
 **✓ 务必**使用用于描述集合中项目的复数形式短语来命名集合属性，而不是使用后跟 "List" 或 "Collection" 的单数形式短语来命名。   
  
 **✓ 务必**使用肯定语气的短语（`CanSeek` 而不是 `CantSeek`）来命名布尔型属性。 或者，还可以为布尔型属性使用前缀 "Is"、"Can" 或 "Has"，但仅在适用时使用。   
  
 **✓ 考虑**使用属性的类型的名称为属性命名。  
  
 例如，以下属性正确获取并设置了名为 `Color` 的枚举值，因此该属性名为 `Color`：  
  
```  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## <a name="names-of-events"></a>事件的名称  
 事件始终是指某个操作，这个操作可能正在发生，也可能已经发生。 因此与方法一样，事件用谓词命名，谓词时态用于指示事件引发的时间。   
  
 **✓ 务必**使用谓词或谓词短语来命名事件。  
  
 示例：`Clicked`、`Painting`、`DroppedDown` 等。  
  
 **✓ 务必**通过使用现在时态和过去时态，让事件名称含有时间先后的概念。  
  
 例如，窗口关闭之前引发的事件称为 `Closing`，窗口关闭之后引发的事件称为 `Closed`。  
  
 X 请勿使用 “Before” 或 “After” 前缀和后缀来指示事件之前或之后。 应按前述使用现在时态和过去时态。  
  
 ✓ 请使用 “EventHandler” 后缀来命名事件处理程序（用作事件类型的委托），如以下示例所示：  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ 务必**在事件处理程序中使用两个名为 `sender` 和 `e` 的参数。  
  
 sender 参数表示引发事件的对象。 sender 参数的类型通常是 `object`，且可能会使用更具体的类型。   
  
 **✓ 务必**使用“EventArgs”后缀来命名事件参数类。   
  
## <a name="names-of-fields"></a>字段的名称  
 字段命名准则适用于静态公共字段和受保护字段。 准则不适用于内部字段和专用字段，[成员设计准则](../../../docs/standard/design-guidelines/member.md)不允许使用公共或受保护的实例字段。  
  
  ✓ 请在字段名称中使用 PascalCasing。    
  
  ✓ 请使用名词、名词短语或形容词来命名字段。    
  
  X 请勿在字段名称中使用前缀。    
  
 例如，不要使用 "g_" 或 "s_" 来指示静态字段。  
  
 *部分版权 © 2005, 2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [命名规则](../../../docs/standard/design-guidelines/naming-guidelines.md)
