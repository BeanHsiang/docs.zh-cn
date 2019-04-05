---
title: DateTimePicker 控件概述（Windows 窗体）
ms.date: 03/30/2017
f1_keywords:
- DateTimePicker
helpviewer_keywords:
- DateTimePicker control [Windows Forms], about
- date and time picker controls
ms.assetid: 501af106-e9fc-4efc-b9b3-c9d8dcaf8c5c
ms.openlocfilehash: 1d2e286e3ce91c722be24f059a874b9db5f2ba82
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57703169"
---
# <a name="datetimepicker-control-overview-windows-forms"></a>DateTimePicker 控件概述（Windows 窗体）
Windows 窗体<xref:System.Windows.Forms.DateTimePicker>控件允许用户从日期或时间的列表中选择单个项。 当用于表示日期，它将显示在两个部分： 一下拉列表中的文本，并单击列表旁的向下箭头上时，将显示一个网格形式表示的日期。 网格看起来像<xref:System.Windows.Forms.MonthCalendar>控件，可用于选择多个日期。 有关详细信息<xref:System.Windows.Forms.MonthCalendar>控件，请参阅[MonthCalendar 控件概述](monthcalendar-control-overview-windows-forms.md)。  
  
## <a name="key-properties"></a>键属性  
 如果您想<xref:System.Windows.Forms.DateTimePicker>若要显示为选取或编辑而不是日期时间的控件，设置<xref:System.Windows.Forms.DateTimePicker.ShowUpDown%2A>属性设置为`true`并且<xref:System.Windows.Forms.DateTimePicker.Format%2A>属性设置为<xref:System.Windows.Forms.DateTimePickerFormat.Time>。 有关详细信息，请参阅[操作说明：使用 DateTimePicker 控件显示时间](how-to-display-time-with-the-datetimepicker-control.md)。  
  
 当<xref:System.Windows.Forms.DateTimePicker.ShowCheckBox%2A>属性设置为`true`，在控件中的选定日期旁边显示复选框。 选中复选框后，可以更新所选的日期时间值。 如果复选框为空，值显示为不可用。  
  
 控件的<xref:System.Windows.Forms.DateTimePicker.MaxDate%2A>和<xref:System.Windows.Forms.DateTimePicker.MinDate%2A>属性确定的日期和时间范围。 <xref:System.Windows.Forms.DateTimePicker.Value%2A>属性包含的当前日期和时间控件设置为。 有关详细信息，请参阅[如何：设置和返回日期与 Windows 窗体 DateTimePicker 控件](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)。 可以四种格式，通过设置中显示的值<xref:System.Windows.Forms.DateTimePicker.Format%2A>属性： <xref:System.Windows.Forms.DateTimePickerFormat.Long>， <xref:System.Windows.Forms.DateTimePickerFormat.Short>， <xref:System.Windows.Forms.DateTimePickerFormat.Time>，或<xref:System.Windows.Forms.DateTimePickerFormat.Custom>。 如果选择自定义格式，则必须设置<xref:System.Windows.Forms.DateTimePicker.CustomFormat%2A>属性设置为一个合适的字符串。 有关详细信息，请参阅[如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期](display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)。  
  
## <a name="see-also"></a>请参阅
- [如何：使用 Windows 窗体 DateTimePicker 控件以自定义格式显示日期](display-a-date-in-a-custom-format-with-wf-datetimepicker-control.md)
- [如何：使用 Windows 窗体 DateTimePicker 控件设置和返回日期](how-to-set-and-return-dates-with-the-windows-forms-datetimepicker-control.md)
