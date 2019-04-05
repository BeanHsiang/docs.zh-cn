---
title: 如何：创建具有访问键和文本换行的控件
ms.date: 03/30/2017
helpviewer_keywords:
- access keys [WPF], control for
- controls [WPF], text wrapping
- wrapping text [WPF]
- keys [WPF], control for
- controls [WPF], access keys
- text wrapping [WPF]
ms.assetid: 205099d9-2551-4302-a25e-a15af9f67e04
ms.openlocfilehash: e410b92f90f775471ef5d89365549ccd5bb7f085
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57361897"
---
# <a name="how-to-create-a-control-that-has-an-access-key-and-text-wrapping"></a>如何：创建具有访问键和文本换行的控件
此示例演示如何创建具有访问键且支持文本换行的控件。 该示例使用<xref:System.Windows.Controls.Label>控件来说明这些概念。  
  
## <a name="example"></a>示例  
 **将文本换行添加到标签**  
  
 <xref:System.Windows.Controls.Label>控件不支持文本换行。 如果需要一个多次换行的标签，可以嵌套其他支持文本换行的元素，并将该元素放在标签内。 下面的示例演示如何使用<xref:System.Windows.Controls.TextBlock>进行包装若干行文本的标签。  
  
 [!code-xaml[LabelSnippet#5](~/samples/snippets/csharp/VS_Snippets_Wpf/LabelSnippet/CS/Pane1.xaml#5)]  
  
 **将访问键和文本换行添加到标签**  
  
 如果你需要<xref:System.Windows.Controls.Label>具有访问键 （助记键），请使用<xref:System.Windows.Controls.AccessText>内元素<xref:System.Windows.Controls.Label>。  
  
 控件，如<xref:System.Windows.Controls.Label>， <xref:System.Windows.Controls.Button>， <xref:System.Windows.Controls.RadioButton>， <xref:System.Windows.Controls.CheckBox>， <xref:System.Windows.Controls.MenuItem>， <xref:System.Windows.Controls.TabItem>， <xref:System.Windows.Controls.Expander>，和<xref:System.Windows.Controls.GroupBox>具有默认控件模板。 这些模板包含<xref:System.Windows.Controls.ContentPresenter>。 您可以设置的属性之一<xref:System.Windows.Controls.ContentPresenter>是<xref:System.Windows.Controls.ContentPresenter.RecognizesAccessKey%2A>="true"，这可用于指定控件的访问密钥。  
  
 下面的示例演示如何创建<xref:System.Windows.Controls.Label>的具有访问键且支持文本换行。 若要启用文本换行，该示例设置<xref:System.Windows.Controls.AccessText.TextWrapping%2A>属性，并使用下划线字符指定访问密钥。 （紧跟下划线字符后面的字符就是访问键。）  
  
 [!code-xaml[LabelSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/LabelSnippet/CS/Pane1.xaml#4)]  
  
## <a name="see-also"></a>请参阅
- [如何：设置标签的目标属性](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms752101(v=vs.90))
