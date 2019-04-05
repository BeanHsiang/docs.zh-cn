---
title: 如何：中显示控件选择工具箱项对话框
ms.date: 03/30/2017
helpviewer_keywords:
- global assembly cache [Windows Forms], Choose Toolbox Items dialog box
- AssemblyFoldersEx [Windows Forms], Choose Toolbox Items dialog box
- controls [Windows Forms], display in Choose Toolbox Items dialog box
- assembly folder registration [Windows Forms], Choose Toolbox Items dialog box
- Choose Toolbox Items dialog box [Windows Forms], display control
ms.assetid: 01ef6eba-d044-40f0-951d-78eff7ebd9a9
ms.openlocfilehash: 191a0848d01eb043420866052b64e2284eb92b49
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720129"
---
# <a name="how-to-display-a-control-in-the-choose-toolbox-items-dialog-box"></a>如何：中显示控件选择工具箱项对话框
在开发和分发控件，您可能希望出现在这些控件**选择工具箱项**对话框中，右键单击时显示**工具箱**，然后选择**选择项**。 可以使控件能够显示在此对话框中的使用 AssemblyFoldersEx 注册过程。  
  
### <a name="to-display-your-control-in-the-choose-toolbox-items-dialog-box"></a>若要在选择工具箱项对话框中显示控件  
  
-   在控件程序集安装到全局程序集缓存中。 有关详细信息，请参阅[如何：将程序集安装到全局程序集缓存](../../app-domains/how-to-install-an-assembly-into-the-gac.md)  
  
     或  
  
-   使用 AssemblyFoldersEx 注册过程中注册您的控件和其关联的设计时程序集。 AssemblyFoldersEx 是框架的第三方供应商在其中存储每个版本，它们支持的路径的注册表位置。 设计时间解析度可以查看在此注册表位置，以查找引用程序集。 注册表脚本可以指定你想要显示在工具箱中的控件。 有关详细信息，请参阅[部署自定义控件和设计时程序集](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ee849818(v=vs.100))。  
  
## <a name="see-also"></a>请参阅
- [“选择工具箱项”对话框 (Visual Studio)](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/dyca0t6t(v=vs.100))
- [部署自定义控件和设计时程序集](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ee849818(v=vs.100))
- [设计时开发 Windows 窗体控件](developing-windows-forms-controls-at-design-time.md)
- [如何：将程序集安装到全局程序集缓存](../../app-domains/how-to-install-an-assembly-into-the-gac.md)
- [演练：自动填充工具箱与自定义组件](walkthrough-automatically-populating-the-toolbox-with-custom-components.md)
