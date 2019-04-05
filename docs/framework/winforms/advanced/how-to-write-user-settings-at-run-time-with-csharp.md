---
title: 如何：在运行时编写用户设置C#
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], run time
- application settings [Windows Forms], writing user settings
- application settings [Windows Forms], C#
ms.assetid: 9d061c7d-b33b-470f-a36d-edccb1d6f9a3
ms.openlocfilehash: 264fa9706f9255d7324cad6d02c36cc424e28995
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56981590"
---
# <a name="how-to-write-user-settings-at-run-time-with-c"></a>如何：在使用 C 运行时编写用户设置\#

应用程序范围的设置是只读的，只能在设计时更改，或通过在应用程序会话之间更改 .config 文件进行更改。 但用户范围的设置可以在运行时写入，就像更改任何属性值一样。 新值在应用程序会话的持续时间内始终存在。 可以通过调用 Save 方法在应用程序会话之间保留对设置的更改。  
  
## <a name="how-to-write-and-persist-user-settings-at-run-time-with-c"></a>如何：编写并使用 C 运行时保存用户设置\#
  
1. 访问设置并向其分配新值，如本示例中所示：  
  
   ```csharp
   Properties.Settings.Default.myColor = Color.AliceBlue;  
   ```  
  
2. 如果想要到在应用程序会话之间保留对设置的更改，请调用 Save 方法，如本示例中所示：  
  
    ```csharp
    Properties.Settings.Default.Save();  
    ```  
  
用户设置保存在用户的本地应用程序数据文件夹（隐藏）中子文件夹下的文件内。  
  
## <a name="see-also"></a>请参阅

- [使用应用程序设置和用户设置](using-application-settings-and-user-settings.md)
- [如何：在运行时读取设置C#](how-to-read-settings-at-run-time-with-csharp.md)
- [应用程序设置概述](application-settings-overview.md)
