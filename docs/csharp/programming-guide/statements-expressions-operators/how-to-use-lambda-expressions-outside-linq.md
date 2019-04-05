---
title: 如何：在 LINQ 外部使用 Lambda 表达式 - C# 编程指南
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [C#], outside LINQ
ms.assetid: 2b519274-6ee4-4455-ab2e-aed67dbfd07c
ms.openlocfilehash: c66dea393ad2351402f54b2391d424701208eba2
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54619812"
---
# <a name="how-to-use-lambda-expressions-outside-linq-c-programming-guide"></a>如何：在 LINQ 外部使用 Lambda 表达式（C# 编程指南）
Lambda 表达式并不只限于在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询中使用。 可以在需要委托值的任何地方（也就是在可以使用匿名方法的任何地方）使用这些表达式。 下面的示例演示如何在 Windows 窗体事件处理程序中使用 lambda 表达式。 请注意，输入的类型（<xref:System.Object> 和 <xref:System.Windows.Forms.MouseEventArgs>）由编译器推理，因此不必在 lambda 输入参数中显式给定。  
  
## <a name="example"></a>示例  
  
```csharp  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        // Use a lambda expression to define an event handler.  
       this.Click += (s, e) => { MessageBox.Show(((MouseEventArgs)e).Location.ToString());};  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅

- [Lambda 表达式](../../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
- [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)
- [语言集成查询 (LINQ))](../../../csharp/programming-guide/concepts/linq/index.md)
