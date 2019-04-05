---
title: 如何：创建 MDI 父窗体
ms.date: 03/30/2017
helpviewer_keywords:
- parent forms
- MDI [Windows Forms], creating forms
ms.assetid: 12c71221-2377-4bb6-b10b-7b4b300fd462
ms.openlocfilehash: 5da7f1a53412cf30a5898fec096aaa01e3aa65d2
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57722979"
---
# <a name="how-to-create-mdi-parent-forms"></a>如何：创建 MDI 父窗体
> [!IMPORTANT]
>  该话题使用 <xref:System.Windows.Forms.MainMenu> 控制（已由 <xref:System.Windows.Forms.MenuStrip> 控制取代）。 如果你选择的话，就会保留 <xref:System.Windows.Forms.MainMenu> 控制以便实现后向兼容性和未来使用。  有关创建 MDI 父窗体的使用<xref:System.Windows.Forms.MenuStrip>，请参阅[如何：使用 MenuStrip 创建 MDI 窗口列表](../controls/how-to-create-an-mdi-window-list-with-menustrip-windows-forms.md)。  
  
 多文档界面 (MDI) 应用程序的基础为 MDI 父窗体。 这是包含 MDI 子窗口（用户与 MDI 应用程序交流所在的子窗口）的窗口。 在“Windows 窗体设计器”中采用编程方式可轻松创建一个 MDI 父窗体。  
  
### <a name="to-create-an-mdi-parent-form-at-design-time"></a>要在设计时创建 MDI 父窗体  
  
1.  创建一个 Windows 应用程序项目。  
  
2.  在中**属性**窗口中，将<xref:System.Windows.Forms.Form.IsMdiContainer%2A>属性设置为**true**。  
  
     这将该表单指定为适合子窗口的 MDI 容器。  
  
    > [!NOTE]
    >  在“属性”窗口中设置属性时，如果你喜欢的话，也可以将 `WindowState` 属性设置为“最大化”，因为父窗体最大化时最容易操作 MDI 子窗口。 此外，注意 MDI 父窗体的边缘将获得系统颜色（在 Windows“系统控制面板”中进行设置），而非你使用 <xref:System.Windows.Forms.Control.BackColor%2A?displayProperty=nameWithType> 属性设置的背景颜色。  
  
3.  从“工具箱”中，将“MenuStrip”控件拖到窗体上。 创建一个顶级菜单项，将“Text”属性设置为“&File”，其中包含名为“&New”和“&Close”的子菜单项。 另创建一个名为“&Window”的顶级菜单项。  
  
     第一个菜单将在运行时创建并隐藏菜单项，第二个菜单将跟踪打开的 MDI 子窗口。 这时，你已经创建了一个 MDI 父窗口。  
  
4.  按 **F5** 运行该应用程序。 有关创建 MDI 子窗口的 MDI 父窗体内运行的信息，请参阅[如何：创建 MDI 子窗体](how-to-create-mdi-child-forms.md)。  
  
## <a name="see-also"></a>请参阅
- [多文档界面 (MDI) 应用程序](multiple-document-interface-mdi-applications.md)
- [如何：创建 MDI 子窗体](how-to-create-mdi-child-forms.md)
- [如何：确定活动的 MDI 子窗体](how-to-determine-the-active-mdi-child.md)
- [如何：将数据发送到活动的 MDI 子窗体](how-to-send-data-to-the-active-mdi-child.md)
- [如何：排列 MDI 子窗体](how-to-arrange-mdi-child-forms.md)
