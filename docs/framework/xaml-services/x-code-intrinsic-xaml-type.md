---
title: x:Code 内部 XAML 类型
ms.date: 03/30/2017
f1_keywords:
- Code
- x:Code
- xCode
helpviewer_keywords:
- Code directive in XAML [XAML Services]
- x:Code XAML directive element [XAML Services]
- XAML [XAML Services], x:Code directive element
ms.assetid: 87986b13-1a2e-4830-ae36-15f9dc5629e8
ms.openlocfilehash: 8d0dbc03bb5eaedd89d5a6ce97d625a51507e820
ms.sourcegitcommit: 5c1abeec15fbddcc7dbaa729fabc1f1f29f12045
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2019
ms.locfileid: "58050600"
---
# <a name="xcode-intrinsic-xaml-type"></a>x:Code 内部 XAML 类型
允许放置 XAML 生产中的代码。 此类代码也可以通过编译 XAML 或由运行时中以备后用，例如解释 XAML 生产留下任何 XAML 处理器实现编译。  
  
## <a name="xaml-object-element-usage"></a>XAML 对象元素用法  
  
```  
<x:Code>  
   // code instructions, usually enclosed by CDATA...  
</x:Code>  
```  
  
## <a name="remarks"></a>备注  
 中的代码`x:Code`XAML 指令元素是仍在常规 XML 命名空间中解释和提供的 XAML 命名空间。 因此，它是通常只需要使用的代码放入`x:Code`内`CDATA`段。  
  
 `x:Code` 不允许的 XAML 生产的所有可能的部署机制。 在特定的框架 (如 WPF) 必须编译代码。 在其他框架`x:Code`可能通常不允许使用情况。  
  
 允许托管的框架`x:Code`内容，正确的语言编译器用于`x:Code`内容由设置和用于编译应用程序的包含项目的目标。  
  
## <a name="wpf-usage-notes"></a>WPF 用法说明  
 代码中声明`x:Code`WPF 有几个值得注意的限制：  
  
-   `x:Code`指令元素必须是 XAML 生产的根元素的直接子元素。  
  
-   [X:class 指令](x-class-directive.md)必须提供父根元素上。  
  
-   该代码放在`x:Code`将被视为由编译为已经对此 XAML 页创建的分部类的作用域内。 因此您定义的所有代码必须都是该分部类的成员或变量。  
  
-   不能定义其他类，比由嵌套在分部类的类 （允许嵌套，但它不是典型因为嵌套的类不能在 XAML 中引用）。 不能定义或添加到用于现有的分部类的命名空间之外的 CLR 命名空间。  
  
-   必须完全限定所有的分部类的 CLR 命名空间之外的代码实体的引用。 如果所声明的成员是重写的分部类可重写成员，这必须指定与特定于语言的 override 关键字。 如果在中声明成员`x:Code`作用域与带 XAML 创建的分部类的成员冲突，这样，编译器会报告冲突，XAML 文件无法编译或加载。  
  
## <a name="see-also"></a>请参阅
- [x:Class 指令](x-class-directive.md)
- [WPF 中的代码隐藏和 XAML](../wpf/advanced/code-behind-and-xaml-in-wpf.md)
- [XAML 概述 (WPF)](../wpf/advanced/xaml-overview-wpf.md)
