---
title: RelativeSource MarkupExtension
ms.date: 03/30/2017
f1_keywords:
- RelativeSource
helpviewer_keywords:
- RelativeSource markup extensions [WPF]
- XAML [WPF], RelativeSource markup extension
ms.assetid: 26be4721-49b5-4717-a92e-7d54ad0d3a81
ms.openlocfilehash: a6a7d615a3a54fbc75bb86b295fdf80433a31dc5
ms.sourcegitcommit: 5137208fa414d9ca3c58cdfd2155ac81bc89e917
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57476329"
---
# <a name="relativesource-markupextension"></a>RelativeSource MarkupExtension

指定的属性<xref:System.Windows.Data.RelativeSource>绑定源中使用[绑定标记扩展](binding-markup-extension.md)，或设置时<xref:System.Windows.Data.Binding.RelativeSource%2A>属性<xref:System.Windows.Data.Binding>建立在 XAML 中的元素。

## <a name="xaml-attribute-usage"></a>XAML 属性用法

```xml
<Binding RelativeSource="{RelativeSource modeEnumValue}" .../>
```

## <a name="xaml-attribute-usage-nested-within-binding-extension"></a>XAML 属性用法（嵌套在 Binding 扩展内）

```xml
<object property="{Binding RelativeSource={RelativeSource modeEnumValue} ...}" .../>
```

## <a name="xaml-object-element-usage"></a>XAML 对象元素用法

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource Mode="modeEnumValue"/>
  </Binding.RelativeSource>
</Binding>
```

或

```xml
<Binding>
  <Binding.RelativeSource>
    <RelativeSource
      Mode="FindAncestor"
      AncestorType="{x:Type typeName}"
      AncestorLevel="intLevel"
    />
  </Binding.RelativeSource>
</Binding>
```

## <a name="xaml-values"></a>XAML 值

|||
|-|-|
|`modeEnumValue`|以下项之一：<br /><br /> 字符串标记`Self`; 对应于<xref:System.Windows.Data.RelativeSource>创建具有其<xref:System.Windows.Data.RelativeSource.Mode%2A>属性设置为<xref:System.Windows.Data.RelativeSourceMode.Self>。<br />字符串标记`TemplatedParent`; 对应于<xref:System.Windows.Data.RelativeSource>创建具有其<xref:System.Windows.Data.RelativeSource.Mode%2A>属性设置为<xref:System.Windows.Data.RelativeSourceMode.TemplatedParent>。<br />字符串标记`PreviousData`; 对应于<xref:System.Windows.Data.RelativeSource>创建具有其<xref:System.Windows.Data.RelativeSource.Mode%2A>属性设置为<xref:System.Windows.Data.RelativeSourceMode.PreviousData>。<br />-请参阅下面的信息有关`FindAncestor`模式。|
|`FindAncestor`|字符串标记 `FindAncestor`。 使用此标记可输入一个模式，以便 `RelativeSource` 指定上级类型和可选的上级级别。 它对应于通过将 <xref:System.Windows.Data.RelativeSource> 属性设置为 <xref:System.Windows.Data.RelativeSource.Mode%2A> 而创建的 <xref:System.Windows.Data.RelativeSourceMode.FindAncestor>。|
|`typeName`|对于 `FindAncestor` 模式是必需的。 类型的名称，用于填充 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 属性。|
|`intLevel`|对于 `FindAncestor` 模式是可选的。 上级级别（在逻辑树中向父级方向计算）。|

## <a name="remarks"></a>备注

`{RelativeSource TemplatedParent}` 绑定用法是一项关键技术的一大概念的控件的用户界面和控件的逻辑分离。 这可以实现从模板定义内绑定到模板化父级（在其中应用模板的运行时对象实例）。 这种情况下， [TemplateBinding 标记扩展](templatebinding-markup-extension.md)实际上是以下绑定表达式的简写形式： `{Binding RelativeSource={RelativeSource TemplatedParent}}`。 `TemplateBinding` 或`{RelativeSource TemplatedParent}`用法都仅定义了一个模板 XAML 内部适用。 有关详细信息，请参阅[TemplateBinding 标记扩展](templatebinding-markup-extension.md)

`{RelativeSource FindAncestor}` 主要用于控件模板或可预测的自包含的 UI 组合，其中一个控件始终应位于某个上级类型的可视树的情况。 例如，项控件的项可能使用 `FindAncestor` 用法绑定到其项控件父级/祖先级。 或者，属于模板中控件组合一部分的元素可使用 `FindAncestor` 绑定到同一组合结构中的父元素。

在 XAML 语法章节显示的 `FindAncestor` 模式的对象元素语法中，第二个对象元素语法专门用于 `FindAncestor` 模式。 `FindAncestor` 模式需要 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 值。 必须设置<xref:System.Windows.Data.RelativeSource.AncestorType%2A>作为属性使用[X:type 标记扩展](../../xaml-services/x-type-markup-extension.md)要查找的上级节点的类型引用。 当在运行时处理绑定请求时，将会用到 <xref:System.Windows.Data.RelativeSource.AncestorType%2A> 值。

对于 `FindAncestor` 模式，当元素树中可能存在多个该类型的上级时，可以使用可选属性 <xref:System.Windows.Data.RelativeSource.AncestorLevel%2A> 帮助消除上级查找的歧义。

有关如何使用 `FindAncestor` 模式的详细信息，请参阅 <xref:System.Windows.Data.RelativeSource>。

`{RelativeSource Self}` 适用于方案这两个属性之间的一个实例属性应依赖于同一个实例，并 （如强制） 任何一般依赖属性关系的另一个属性的值已存在。 虽然很少见，对象上存在两个属性值可以说完全相同 （并以相同方式键入），您还可以应用`Converter`具有一个绑定到参数`{RelativeSource Self}`，并使用此转换器转换源之间和目标类型。 另一方案`{RelativeSource Self}`作为的一部分是<xref:System.Windows.MultiDataTrigger>。

例如，以下 XAML 定义了一个 <xref:System.Windows.Shapes.Rectangle> 元素，以便无论为 <xref:System.Windows.FrameworkElement.Width%2A> 输入什么值，都确保 <xref:System.Windows.Shapes.Rectangle> 始终是一个方形：`<Rectangle Width="200" Height="{Binding RelativeSource={RelativeSource Self}, Path=Width}" .../>`

`{RelativeSource PreviousData}` 数据模板中或在其中绑定将使用集合作为数据源的情况下非常有用。 可以使用`{RelativeSource PreviousData}`以突出显示集合中相邻数据项之间的关系。 相关技术是在数据源中的当前项和前一个项之间建立 <xref:System.Windows.Data.MultiBinding>，并使用此绑定上的转换器来确定这两个项及其属性的差异。

在下面的示例中，项目模板中的第一个 <xref:System.Windows.Controls.TextBlock> 可显示当前编号。 第二个<xref:System.Windows.Controls.TextBlock>绑定<xref:System.Windows.Data.MultiBinding>，名义上有两个<xref:System.Windows.Data.Binding>构成部分： 当前记录，并刻意采用前一个数据记录使用的绑定`{RelativeSource PreviousData}`。 然后，<xref:System.Windows.Data.MultiBinding> 上的转换器将计算差异，并将其返回到绑定。

```xml
<ListBox Name="fibolist">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
            <TextBlock Text="{Binding}"/>
            <TextBlock>, difference = </TextBlock>
                <TextBlock>
                    <TextBlock.Text>
                        <MultiBinding Converter="{StaticResource DiffConverter}">
                            <Binding/>
                            <Binding RelativeSource="{RelativeSource PreviousData}"/>
                        </MultiBinding>
                    </TextBlock.Text>
                </TextBlock>
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
```

数据绑定概念未在此处，请参阅[数据绑定概述](../data/data-binding-overview.md)。

在中[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]XAML 处理器实现中，对此标记扩展的处理由定义<xref:System.Windows.Data.RelativeSource>类。

`RelativeSource` 是标记扩展。 当要求转义特性值应为非文本值或非处理程序名称时，通常会实现标记扩展，相对于只在某些类型或属性上放置类型转换器而言，此需求更具有全局性。 在 XAML 使用的所有标记扩展`{`和`}`约定所依据的 XAML 处理器识别标记扩展必须处理该属性其特性语法中的字符。 有关详细信息，请参阅[标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)。

## <a name="see-also"></a>请参阅

- <xref:System.Windows.Data.Binding>
- [样式设置和模板化](../controls/styling-and-templating.md)
- [XAML 概述 (WPF)](xaml-overview-wpf.md)
- [标记扩展和 WPF XAML](markup-extensions-and-wpf-xaml.md)
- [数据绑定概述](../data/data-binding-overview.md)
- [绑定声明概述](../data/binding-declarations-overview.md)
- [x:Type 标记扩展](../../xaml-services/x-type-markup-extension.md)
