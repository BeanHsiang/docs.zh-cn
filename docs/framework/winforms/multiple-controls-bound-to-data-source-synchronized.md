---
title: 如何：确保多个控件绑定到相同的数据源保持同步
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], binding multiple
- controls [Windows Forms], synchronizing with data source
ms.assetid: c2f0ecc6-11e6-4c2c-a1ca-0759630c451e
ms.openlocfilehash: 01cec80c85beb64975648b2250c914fe04d3ac95
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57721380"
---
# <a name="how-to-ensure-multiple-controls-bound-to-the-same-data-source-remain-synchronized"></a>如何：确保多个控件绑定到相同的数据源保持同步
通常在使用 Windows 窗体中的数据绑定，多个控件绑定到同一数据源。 在某些情况下，可能需要采取额外步骤来确保控件的绑定的属性保持同步以及数据源。 这些步骤是在两种情况下需要：  
  
-   如果数据源不实现<xref:System.ComponentModel.IBindingList>，并因此生成<xref:System.ComponentModel.IBindingList.ListChanged>类型的事件<xref:System.ComponentModel.ListChangedType.ItemChanged>。  
  
-   如果数据源实现<xref:System.ComponentModel.IEditableObject>。  
  
 在前一种情况，你可以使用<xref:System.Windows.Forms.BindingSource>将数据源绑定到控件。 在后一种情况，您使用<xref:System.Windows.Forms.BindingSource>和处理<xref:System.Windows.Forms.BindingSource.BindingComplete>事件，并调用<xref:System.Windows.Forms.BindingManagerBase.EndCurrentEdit%2A>关联<xref:System.Windows.Forms.BindingManagerBase>。  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何将三个控件绑定 — 两个文本框控件和一个<xref:System.Windows.Forms.DataGridView>控件 — 对中的同一列<xref:System.Data.DataSet>使用<xref:System.Windows.Forms.BindingSource>组件。 此示例演示如何处理<xref:System.Windows.Forms.BindingSource.BindingComplete>事件，并确保一个文本框中的文本值更改时，另一个文本框和<xref:System.Windows.Forms.DataGridView>控件更新为正确的值。  
  
 该示例使用<xref:System.Windows.Forms.BindingSource>绑定数据源和控件。 或者，可以将控件绑定到数据源并检索<xref:System.Windows.Forms.BindingManagerBase>从窗体的绑定<xref:System.Windows.Forms.Control.BindingContext%2A>，然后处理<xref:System.Windows.Forms.BindingManagerBase.BindingComplete>事件<xref:System.Windows.Forms.BindingManagerBase>。 有关如何执行此操作的示例，了解帮助页<xref:System.Windows.Forms.BindingManagerBase.BindingComplete>事件的<xref:System.Windows.Forms.BindingManagerBase>。  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleControls#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleControls#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
  
-   此代码示例需要  
  
-   对 <xref:System><xref:System.Windows.Forms> 和 <xref:System.Drawing> 程序集的引用。  
  
-   一个具有窗体<xref:System.Windows.Forms.Form.Load>处理事件和调用`InitializeControlsAndDataSource`从窗体的示例中的方法<xref:System.Windows.Forms.Form.Load>事件处理程序。  
  
## <a name="see-also"></a>请参阅
- [如何：使用 BindingSource 组件跨窗体共享绑定数据](./controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)
- [Windows 窗体数据绑定中的更改通知](change-notification-in-windows-forms-data-binding.md)
- [与数据绑定相关的接口](interfaces-related-to-data-binding.md)
- [Windows 窗体数据绑定](windows-forms-data-binding.md)
