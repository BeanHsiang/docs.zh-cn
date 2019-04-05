---
title: 如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DateTimePicker control [Windows Forms], display styles
- examples [Windows Forms], DateTimePicker control
- dates [Windows Forms], displaying in DateTimePicker control
ms.assetid: 39767691-2d2b-46b6-a663-b7901e581a6e
ms.openlocfilehash: c201455acaa9bde521afd623424d0cfc403b1bff
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57705865"
---
# <a name="how-to-display-a-date-in-a-custom-format-with-the-windows-forms-datetimepicker-control"></a>如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期
Windows 窗体<xref:System.Windows.Forms.DateTimePicker>控制可以让你灵活地设置日期和时间控件中的显示格式。 <xref:System.Windows.Forms.DateTimePicker.Format%2A>属性，可选择从中列出的预定义格式<xref:System.Windows.Forms.DateTimePickerFormat>。 如果这些都不能充分满足您需求，则可以创建您自己使用中列出的格式字符的格式样式<xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A>。  
  
### <a name="to-display-a-custom-format"></a>若要显示的自定义格式  
  
1.  将 <xref:System.Windows.Forms.DateTimePicker.Format%2A> 属性设置为 `DateTimePickerFormat.Custom`。  
  
2.  设置<xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A>属性设置为格式字符串。  
  
    ```vb  
    DateTimePicker1.Format = DateTimePickerFormat.Custom  
    ' Display the date as "Mon 27 Feb 2012".  
    DateTimePicker1.CustomFormat = "ddd dd MMM yyyy"  
    ```  
  
    ```csharp  
    dateTimePicker1.Format = DateTimePickerFormat.Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1.CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
    ```cpp  
    dateTimePicker1->Format = DateTimePickerFormat::Custom;  
    // Display the date as "Mon 27 Feb 2012".  
    dateTimePicker1->CustomFormat = "ddd dd MMM yyyy";  
    ```  
  
### <a name="to-add-text-to-the-formatted-value"></a>若要将文本添加到带格式的值  
  
1.  使用单引号括起来不像"M"的格式字符或分隔符等任何字符":"。 例如，下面的格式字符串显示当前日期，格式以"今天是：05:30:31 星期五年 3 月 02，2012"英语 （美国） 区域性中。  
  
    ```vb  
    DateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy"  
    ```  
  
    ```csharp  
    dateTimePicker1.CustomFormat = "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
    ```cpp  
    dateTimePicker1->CustomFormat =  
       "'Today is:' hh:mm:ss dddd MMMM dd, yyyy";  
    ```  
  
     具体取决于的区域性设置，可能会更改任何未括在单引号内字符。 例如，上面的格式字符串显示当前日期，格式以"今天是：05:30:31 星期五年 3 月 02，2012"英语 （美国） 区域性中。 请注意，第一个冒号括在单引号中，因为它不是因为它处于"hh: mm:"为分隔字符。 在另一个区域性格式可能显示为"现在是：05.30.31 星期五年 3 月 02，2012"。  
  
## <a name="see-also"></a>请参阅
- [DateTimePicker 控件](datetimepicker-control-windows-forms.md)
- [如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)
