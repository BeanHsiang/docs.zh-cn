---
title: 事件处理程序概述（Windows 窗体）
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, event handling
- event handling [Windows Forms], Windows Forms
- event handlers [Windows Forms], about event handlers
ms.assetid: 228112e1-1711-42ee-8ffa-ff3555bffe66
ms.openlocfilehash: 6dbcffadfd484dc33db2fcd3ee3f680dcc0740e5
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703382"
---
# <a name="event-handlers-overview-windows-forms"></a>事件处理程序概述（Windows 窗体）
事件处理程序是绑定到一个事件的方法。 当引发事件时，执行事件处理程序中的代码。 每个事件处理程序提供了两个参数，可用于正确地处理该事件。 下面的示例演示的事件处理程序<xref:System.Windows.Forms.Button>控件的<xref:System.Windows.Forms.Control.Click>事件。  
  
```vb  
Private Sub button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles button1.Click  
  
End Sub  
```  
  
```csharp  
private void button1_Click(object sender, System.EventArgs e)   
{  
  
}  
```  
  
```cpp  
private:  
  void button1_Click(System::Object ^ sender,  
    System::EventArgs ^ e)  
  {  
  
  }  
```  
  
 第一个参数，`sender`，提供对引发事件的对象的引用。 第二个参数， `e`，在上面的示例中，传递对象特定于正在处理的事件。 通过引用对象的属性 （和有时，其方法），您可以获取鼠标的鼠标事件或拖放事件中传输的数据的位置等信息。  
  
 通常，每个事件生成第二个参数的不同事件的对象类型的事件处理程序。 一些事件处理程序，如用于<xref:System.Windows.Forms.Control.MouseDown>和<xref:System.Windows.Forms.Control.MouseUp>事件，具有其第二个参数的相同对象类型。 对于这些类型的事件，可以使用相同的事件处理程序来处理这两个事件。  
  
 此外可以使用相同的事件处理程序来处理不同的控件的同一事件。 例如，如果有一组<xref:System.Windows.Forms.RadioButton>窗体上的控件，可以创建单个事件处理程序<xref:System.Windows.Forms.Control.Click>事件并且具有每个控件的<xref:System.Windows.Forms.Control.Click>事件绑定到单个事件处理程序。 有关详细信息，请参阅[如何：将多个事件连接到 Windows 窗体中的单个事件处理程序](how-to-connect-multiple-events-to-a-single-event-handler-in-windows-forms.md)。  
  
## <a name="see-also"></a>请参阅
- [在 Windows 窗体中创建事件处理程序](creating-event-handlers-in-windows-forms.md)
- [事件概述](events-overview-windows-forms.md)
