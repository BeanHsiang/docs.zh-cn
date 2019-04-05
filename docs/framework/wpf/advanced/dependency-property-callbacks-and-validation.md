---
title: 依赖项属性回调和验证
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dependency properties [WPF], validation
- coerce value callbacks [WPF]
- callbacks [WPF], validation
- dependency properties [WPF], callbacks
- validation of dependency properties [WPF]
ms.assetid: 48db5fb2-da7f-49a6-8e81-3540e7b25825
ms.openlocfilehash: ff7cbd995ba52f3cea712cb02b72f91d40422c33
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57363925"
---
# <a name="dependency-property-callbacks-and-validation"></a>依赖项属性回调和验证
本主题介绍如何使用与属性相关的功能（如验证确定、更改属性的有效值时调用的回调）的替代自定义实现，并重写对值确定的外部可能影响来创建依赖属性。 本主题还讨论使用这些技术扩展默认属性系统行为所适用的方案。  
  
  
  
<a name="prerequisites"></a>   
## <a name="prerequisites"></a>系统必备  
 本主题假定你了解实现依赖属性的基本方案，以及如何将元数据应用于自定义依赖属性。 有关上下文，请参阅[自定义依赖属性](custom-dependency-properties.md)和[依赖属性元数据](dependency-property-metadata.md)。  
  
<a name="Validation_Callbacks"></a>   
## <a name="validation-callbacks"></a>验证回叫  
 在首次注册依赖属性时，可以为其分配验证回叫。 验证回叫不属于属性元数据;是的直接输入<xref:System.Windows.DependencyProperty.Register%2A>方法。 因此，在为某个依赖属性创建验证回叫后，新实现无法重写该验证回叫。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 实现回叫，以便为其提供对象值。 如果提供的值对属性有效，回叫会返回 `true`；否则，回叫返回 `false`。 假定按照向属性系统注册的类型，属性的类型是正确的，因此通常不会在回叫内执行类型检查。 属性系统可在多种不同操作中使用回叫。 这包括按默认值的初始类型初始化、 以编程方式更改通过调用<xref:System.Windows.DependencyObject.SetValue%2A>，或尝试使用提供的新默认值重写元数据。 如果验证回叫是通过其中任何一种操作调用的，并且返回 `false`，则会引发异常。 应用程序编写器必须准备处理这些异常。 验证回叫常用于验证枚举值，或在属性设置的度量值必须大于等于零时约束整数值或双精度型值。  
  
 验证回叫专用作类验证程序，而不用作实例验证程序。 回叫参数不会与特定通信<xref:System.Windows.DependencyObject>上设置要验证的属性。 因此，验证回叫不能用来强制执行可能会影响属性值的“依赖项”，其中，某个属性特定于实例的值依赖于其他属性特定于实例的值或运行时状态等因素。  
  
 以下是非常简单的验证回叫方案的代码示例： 验证属性被类型化为<xref:System.Double>基元不是<xref:System.Double.PositiveInfinity>或<xref:System.Double.NegativeInfinity>。  
  
 [!code-csharp[DPCallbackOverride#ValidateValueCallback](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#validatevaluecallback)]
 [!code-vb[DPCallbackOverride#ValidateValueCallback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#validatevaluecallback)]  
  
<a name="Coerce_Value_Callbacks_and_Property_Changed_Events"></a>   
## <a name="coerce-value-callbacks-and-property-changed-events"></a>强制值回叫和属性更改事件  
 强制值回叫传递属性特定于<xref:System.Windows.DependencyObject>实例的属性，如执行<xref:System.Windows.PropertyChangedCallback>依赖项属性的值发生更改时由属性系统调用的实现。 通过将这两种回叫组合使用，可以对元素创建一系列属性，其中，一个属性的更改会对另一个属性实施强制或重新计算。  
  
 使用依赖属性链接的典型方案是：具有用户界面驱动属性，其中，元素为最小值和最大值分别保留一个属性，为实际值或当前值保留第三个属性。 此时，如果按照当前值超出新的最大值的方式调整最大值，则可能需要强制当前值不超过新的最大值，并对最小值与当前值强制类似的关系。  
  
 下面是一个非常简短的代码示例，仅针对阐释此关系的三个依赖属性之一。 该示例演示如何注册相关的 *Reading 属性的最小/最大/当前值集的 `CurrentReading` 属性。 它使用上一节中所示的验证。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 当前值的属性更改回叫用于将更改转发到其他依赖属性，方法是显式调用为这些属性注册的强制值回叫：  
  
 [!code-csharp[DPCallbackOverride#OnPCCurrent](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#onpccurrent)]
 [!code-vb[DPCallbackOverride#OnPCCurrent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#onpccurrent)]  
  
 强制值回叫会检查当前属性可能依赖的属性的值，并在必要时强制当前值：  
  
 [!code-csharp[DPCallbackOverride#CoerceCurrent](~/samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#coercecurrent)]
 [!code-vb[DPCallbackOverride#CoerceCurrent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#coercecurrent)]  
  
> [!NOTE]
>  不会强制属性的默认值。 如果属性值仍有其初始默认值，或通过清除使用其他值的属性值等于默认值可能会出现<xref:System.Windows.DependencyObject.ClearValue%2A>。  
  
 强制值回叫和属性更改回叫属于属性元数据的一部分。 因此，可以通过在类型上重写特定依赖属性的元数据来更改对该属性的回叫，因为其所在的类型派生自拥有该依赖属性的类型。  
  
<a name="Advanced"></a>   
## <a name="advanced-coercion-and-callback-scenarios"></a>高级强制和回叫方案  
  
### <a name="constraints-and-desired-values"></a>约束和所需的值  
 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A>回调将由属性系统来强制值根据所声明的逻辑，但强制转换后的本地设置值属性将仍会在内部保留"所需的值"。 如果约束基于可能会在应用程序生存期间动态更改的其他属性值，则强制约束也会进行动态更改，并且在给定新约束的情况下约束属性可更改其值以尽可能接近所需的值。 如果解除所有约束，该值会成为所需的值。 如果多个属性以循环方式相互依赖，则可能会引入某些相当复杂的依赖项方案。 例如，在最小/最大/当前值方案中，可以选择将最小值和最大值作为用户可设置的资源。 在这种情况下，可能需要强制最大值始终大于最小值，反之亦然。 但是，如果该强制处于活动状态，并且最大值强制为最小值，则会将当前值保留在不可设置的状态，因为它依赖于这二者，且被约束在这些值之间的范围内，即为零。 这样，如果调整最大值或最小值，当前值可能会“沿用”这些值之一，因为仍然存储了当前值所需的值，并且当前值会在放松约束时尝试接近所需的值。  
  
 复杂依赖项没有任何技术错误，但是，如果它们需要大量重新计算，则可能会略微降低性能，而且还可能导致用户混淆（如果直接影响 UI）。 请小心使用属性更改回叫和强制值回叫，确保尽可能地明确处理所尝试的强制，并且不会“过度约束”。  
  
### <a name="using-coercevalue-to-cancel-value-changes"></a>使用 CoerceValue 取消值更改  
 属性系统会将任何<xref:System.Windows.CoerceValueCallback>返回的值<xref:System.Windows.DependencyProperty.UnsetValue>作为一种特殊情况。 此特殊情况意味着，导致属性更改<xref:System.Windows.CoerceValueCallback>属性系统中，应会拒绝被调用，并且属性系统应改为报告该属性具有以前的任何值。 该机制可用于检查异步启动的属性更改对当前对象状态是否仍然有效，如果无效，则可取消这些更改。 另一个可能的方案是：可以根据负责所报告的值的属性值确定组件，有选择地取消该值。 若要执行此操作，可以使用<xref:System.Windows.DependencyProperty>回叫和属性标识符作为输入传递<xref:System.Windows.DependencyPropertyHelper.GetValueSource%2A>，然后处理<xref:System.Windows.ValueSource>。  
  
## <a name="see-also"></a>请参阅
- [依赖项属性概述](dependency-properties-overview.md)
- [依赖属性元数据](dependency-property-metadata.md)
- [自定义依赖属性](custom-dependency-properties.md)
