---
title: 如何：将应用程序图标添加到使用 Windows 窗体 NotifyIcon 组件任务栏
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- TrayIcon
helpviewer_keywords:
- status area icons
- icons [Windows Forms], adding to taskbar
- NotifyIcon component
- taskbar [Windows Forms], adding icons
ms.assetid: d28c0fe6-aaf2-4df7-ad74-928d861a8510
ms.openlocfilehash: 04f6b98a2206371a2838b3a6952feeafcd788309
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57714250"
---
# <a name="how-to-add-application-icons-to-the-taskbar-with-the-windows-forms-notifyicon-component"></a>如何：将应用程序图标添加到使用 Windows 窗体 NotifyIcon 组件任务栏
Windows 窗体<xref:System.Windows.Forms.NotifyIcon>组件在任务栏的状态通知区域显示一个图标。 若要在状态区域中显示多个图标，必须有多个<xref:System.Windows.Forms.NotifyIcon>窗体上的组件。 若要设置控件显示的图标，使用<xref:System.Windows.Forms.NotifyIcon.Icon%2A>属性。 此外可以编写代码<xref:System.Windows.Forms.NotifyIcon.DoubleClick>事件处理程序，以便当用户双击该图标出现该问题。 例如，您能够为用户配置后台进程的图标表示显示一个对话框。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.NotifyIcon>组件用于通知目的，警告用户操作或事件已发生或已在某种类型的状态更改。 应与应用程序的标准交互使用菜单、 工具栏和其他用户界面元素。  
  
### <a name="to-set-the-icon"></a>若要设置图标  
  
1.  将一个值赋给<xref:System.Windows.Forms.NotifyIcon.Icon%2A>属性。 值必须属于类型`System.Drawing.Icon`和可以从.ico 文件加载。 在代码中，或单击省略号按钮，可以指定图标文件 (![VisualStudioEllipsesButton 屏幕快照](../media/vbellipsesbutton.png "vbEllipsesButton")) 旁边<xref:System.Windows.Forms.NotifyIcon.Icon%2A>中的属性**属性**窗口中，，然后选择中的文件**打开**出现的对话框。  
  
2.  将 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性设置为 `true`。  
  
3.  设置<xref:System.Windows.Forms.NotifyIcon.Text%2A>属性设置为一个合适的工具提示字符串。  
  
     在下面的代码示例中，将路径设置图标的位置是**我的文档**文件夹。 使用此位置是因为您可以假定大多数运行 Windows 操作系统的计算机将包含该文件夹。 选择此位置，用户还可以具有最少的系统访问级别来安全地运行应用程序。 下面的示例要求具有的窗体<xref:System.Windows.Forms.NotifyIcon>已添加的控件。 它还需要一个名为的图标文件`Icon.ico`。  
  
    ```vb  
    ' You should replace the bold icon in the sample below  
    ' with an icon of your own choosing.  
    NotifyIcon1.Icon = New _   
       System.Drawing.Icon(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Icon.ico")  
    NotifyIcon1.Visible = True  
    NotifyIcon1.Text = "Antivirus program"  
    ```  
  
    ```csharp  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    notifyIcon1.Icon =   
       new System.Drawing.Icon (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Icon.ico");  
    notifyIcon1.Visible = true;  
    notifyIcon1.Text = "Antivirus program";  
    ```  
  
    ```cpp  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    notifyIcon1->Icon = gcnew   
       System::Drawing::Icon(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Icon.ico"));  
    notifyIcon1->Visible = true;  
    notifyIcon1->Text = "Antivirus program";  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.NotifyIcon>
- <xref:System.Windows.Forms.NotifyIcon.Icon%2A>
- [如何：使用 Windows 窗体 NotifyIcon 组件关联快捷菜单](how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component.md)
- [NotifyIcon 组件](notifyicon-component-windows-forms.md)
- [NotifyIcon 组件概述](notifyicon-component-overview-windows-forms.md)
