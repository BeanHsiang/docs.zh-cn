---
title: 依赖项属性
ms.date: 10/22/2008
ms.technology: dotnet-standard
ms.assetid: 212cfb1e-cec4-4047-94a6-47209b387f6f
author: KrzysztofCwalina
ms.openlocfilehash: 52d7a69a3f52c67ebff3f3db1daf0790e995913a
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54721906"
---
# <a name="dependency-properties"></a>依赖项属性
依赖项属性 (DP) 是一种常规属性，它将其值存储在属性存储中而不是其他位置（例如类型变量（字段））中。  
  
 附加依赖项属性是一种建模为静态 Get 和 Set 方法的依赖项属性，表示那些描述对象及其容器之间关系的“属性”（例如，`Panel` 容器中 `Button` 对象的位置）。  
  
 **✓ 务必**提供依赖项属性，如果需要属性 WPF 功能，例如样式、触发器、数据绑定、动画、动态资源和继承。  
  
## <a name="dependency-property-design"></a>依赖项属性设计  
 **✓ 务必**在实现依赖属性时继承自 <xref:System.Windows.DependencyObject> 或其子类型之一。 该类型提供了一个非常有效的属性存储实现，并且自动支持 WPF 数据绑定。  
  
 **✓ 务必**提供常规 CLR 属性和公共的静态只读字段，用于存储每个依赖属性的 <xref:System.Windows.DependencyProperty?displayProperty=nameWithType> 的实例。  
  
 **✓ 务必**通过调用实例方法 <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=nameWithType> 和 <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=nameWithType> 来实现依赖属性。  
  
 **✓ 务必** 在为依赖属性静态字段命名时以 “Property” 作为属性名称的后缀。  
  
 **X 切忌**在代码中显式设置依赖项属性的默认值; 而是在元数据中设置它们。  
  
 如果显式设置属性默认值，则可能会阻止通过某些隐式方法（例如样式）设置该属性。  
  
 **X 切忌**为了访问静态字段而将标准代码以外的代码放在属性访问器中。  
  
 如果属性是通过隐式方式（例如样式）设置的，则该代码不会执行，因为样式直接使用静态字段。  
  
 **X 切忌**使用依赖属性存储安全数据。 即使私有依赖属性也可以公开访问。  
  
## <a name="attached-dependency-property-design"></a>附加依赖项属性设计  
 上一部分中描述的依赖项属性表示声明类型的内在属性；例如，`Text` 属性是 `TextButton` 的一个属性，用来声明它。 一种特殊的依赖项属性是附加依赖项属性。  
  
 附加属性的典型示例是 <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=nameWithType> 属性。 该属性表示 Button（而不是 Grid）的列位置，但仅当 Button 包含在 Grid 中时才生效，因此它是被 Grid“附加”到 Button 的。  
  
```xaml
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition />  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
  
    <Button Grid.Column="0">Click</Button>  
    <Button Grid.Column="1">Clack</Button>  
</Grid>  
```  
  
 附加属性的定义看起来大致类似于常规的依赖项属性，除了访问器由静态 Get 和 Set 方法表示：  
  
```csharp
public class Grid {  
  
    public static int GetColumn(DependencyObject obj) {  
        return (int)obj.GetValue(ColumnProperty);  
    }  
  
    public static void SetColumn(DependencyObject obj, int value) {  
        obj.SetValue(ColumnProperty,value);  
    }  
  
    public static readonly DependencyProperty ColumnProperty =  
        DependencyProperty.RegisterAttached(  
            "Column",  
            typeof(int),  
            typeof(Grid)  
    );  
}  
```  
  
## <a name="dependency-property-validation"></a>依赖项属性验证  
 属性通常会实施所谓的验证。 尝试更改属性的值时，系统会执行验证逻辑。  
  
 遗憾的是，依赖项属性访问器不能包含任意验证代码， 相反，只能在属性注册期间指定依赖项属性的验证逻辑。  
  
 **X 切忌**将依赖属性验证逻辑放入属性访问器。 相反，应将验证回叫传递到 `DependencyProperty.Register` 方法。  
  
## <a name="dependency-property-change-notifications"></a>依赖属性更改通知  
 **X 切忌**在依赖属性访问器中实现更改通知逻辑。 依赖属性具有一个内置更改通知功能，必须通过向 <xref:System.Windows.PropertyMetadata> 提供更改通知回叫才能使用该功能。  
  
## <a name="dependency-property-value-coercion"></a>依赖项属性值强制转换  
 在实际修改属性存储之前，如果赋给属性 setter 的值被 setter 修改，则会发生属性强制转换。  
  
 **X 切忌**在依赖属性访问器中实现强制逻辑。  
  
 依赖项属性有一个内置的强制转换功能，可以通过向 `PropertyMetadata` 提供强制回调来使用它。  
  
 *部分版权 © 2005、2009 Microsoft Corporation。保留所有权利。*  
  
 *经 Pearson Education, Inc 授权，转载自[框架设计准则：可重用的 .NET 库的约定、习惯用语和模式，第 2 版](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 作者：Krzysztof Cwalina 和 Brad Abrams，由 Addison Wesley Professional 于 2008 年 10 月 22 日印发，作为 Microsoft Windows 开发系列的一部分。*  
  
## <a name="see-also"></a>请参阅

- [框架设计指南](../../../docs/standard/design-guidelines/index.md)
- [常用设计模型](../../../docs/standard/design-guidelines/common-design-patterns.md)
