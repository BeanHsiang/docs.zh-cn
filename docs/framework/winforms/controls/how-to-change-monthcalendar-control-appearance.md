---
title: 如何：更改 Windows 窗体 MonthCalendar 控件的外观
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], calendar controls
- MonthCalendar control [Windows Forms], formatting display
ms.assetid: d09b95c9-e108-4608-9b31-b9100c0677bf
ms.openlocfilehash: 2e26f7a9db8e19b584000089f99e99aab7c25a32
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57716369"
---
# <a name="how-to-change-the-windows-forms-monthcalendar-controls-appearance"></a>如何：更改 Windows 窗体 MonthCalendar 控件的外观
Windows 窗体<xref:System.Windows.Forms.MonthCalendar>让您可以自定义在很多方面的日历的外观。 例如，可以设置配色方案，并选择要显示或隐藏周数和当前日期。  
  
### <a name="to-change-the-month-calendars-color-scheme"></a>若要更改月日历的配色方案  
  
-   设置属性，如<xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>，<xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A>和<xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>。 <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>属性还为每周天数中确定的字体颜色。 <xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>属性确定的日期之前和之后显示的月或几个月的颜色。  
  
    ```vb  
    MonthCalendar1.TitleBackColor = System.Drawing.Color.Blue  
    MonthCalendar1.TrailingForeColor = System.Drawing.Color.Red  
    MonthCalendar1.TitleForeColor = System.Drawing.Color.Yellow  
    ```  
  
    ```csharp  
    monthCalendar1.TitleBackColor = System.Drawing.Color.Blue;  
    monthCalendar1.TrailingForeColor = System.Drawing.Color.Red;  
    monthCalendar1.TitleForeColor = System.Drawing.Color.Yellow;  
    ```  
  
    ```cpp  
    monthCalendar1->TitleBackColor = System::Drawing::Color::Blue;  
    monthCalendar1->TrailingForeColor = System::Drawing::Color::Red;  
    monthCalendar1->TitleForeColor = System::Drawing::Color::Yellow;  
    ```  
  
    > [!NOTE]
    >  从开始使用 Windows Vista，具体取决于主题，设置某些属性可能会更改日历的外观。 例如，如果 Windows 设置为使用 Aero 主题，则将设置<xref:System.Windows.Forms.MonthCalendar.BackColor%2A>， <xref:System.Windows.Forms.MonthCalendar.TitleBackColor%2A>， <xref:System.Windows.Forms.MonthCalendar.TitleForeColor%2A>，或<xref:System.Windows.Forms.MonthCalendar.TrailingForeColor%2A>属性不起作用。 这是因为该日历的更新的版本呈现在运行时派生自当前操作系统主题的外观。 如果你想要使用这些属性，并启用日历的早期版本，则可以为应用程序禁用视觉样式。 禁用视觉样式，可能会影响的外观和行为的应用程序中的其他控件。 若要禁用在 Visual Basic 中的视觉样式，请打开项目设计器，并取消选中**启用 XP 视觉样式**复选框。 若要禁用视觉样式在 C# 中的，打开 Program.cs，并注释掉`Application.EnableVisualStyles();`。 视觉样式的详细信息，请参阅[启用视觉样式](/windows/desktop/controls/cookbook-overview)。  
  
### <a name="to-display-the-current-date-at-the-bottom-of-the-control"></a>若要在控件的底部显示当前日期  
  
-   将 <xref:System.Windows.Forms.MonthCalendar.ShowToday%2A> 属性设置为 `true`。 下面的示例显示和省略双击窗体之后今天的日期之间切换。  
  
    ```vb  
    Private Sub Form1_DoubleClick(ByVal sender As Object, _  
    ByVal e As System.EventArgs) Handles MyBase.DoubleClick  
       ' Toggle between True and False.  
       MonthCalendar1.ShowToday = Not MonthCalendar1.ShowToday  
    End Sub  
    ```  
  
    ```csharp  
    private void Form1_DoubleClick(object sender, System.EventArgs e)  
    {  
       // Toggle between True and False.  
       monthCalendar1.ShowToday = !monthCalendar1.ShowToday;  
    }  
    ```  
  
    ```cpp  
    private:  
       System::Void Form1_DoubleClick(System::Object ^  sender,  
          System::EventArgs ^  e)  
       {  
          // Toggle between True and False.  
          monthCalendar1->ShowToday = !monthCalendar1->ShowToday;  
       }  
    ```  
  
     (Visual C#， [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]) 将以下代码放在窗体的构造函数，以注册事件处理程序。  
  
    ```csharp  
    this.DoubleClick += new System.EventHandler(this.Form1_DoubleClick);  
    ```  
  
    ```cpp  
    this->DoubleClick += gcnew System::EventHandler(this,  
       &Form1::Form1_DoubleClick);  
    ```  
  
### <a name="to-display-week-numbers"></a>若要显示周数  
  
-   将 <xref:System.Windows.Forms.MonthCalendar.ShowWeekNumbers%2A> 属性设置为 `true`。 在代码中或在属性窗口中，可以设置此属性。  
  
     在左侧的一周的第一天到一个单独的列中显示周数。  
  
    ```vb  
    MonthCalendar1.ShowWeekNumbers = True  
    ```  
  
    ```csharp  
    monthCalendar1.ShowWeekNumbers = true;  
    ```  
  
    ```cpp  
    monthCalendar1->ShowWeekNumbers = true;  
    ```  
  
## <a name="see-also"></a>请参阅
- [MonthCalendar 控件](monthcalendar-control-windows-forms.md)
- [如何：在 Windows 窗体 MonthCalendar 控件中选择日期范围](how-to-select-a-range-of-dates-in-the-windows-forms-monthcalendar-control.md)
- [如何：特定以粗体的显示日期与 Windows 窗体 MonthCalendar 控件](display-specific-days-in-bold-with-wf-monthcalendar-control.md)
- [如何：在 Windows 窗体 MonthCalendar 控件中显示多个月份](display-more-than-one-month-wf-monthcalendar-control.md)
