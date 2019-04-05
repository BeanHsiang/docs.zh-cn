---
title: 如何：向应用程序中添加多组设置C#
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], multiple sets
- application settings [Windows Forms], C#
ms.assetid: 45007ac6-cf07-4be7-bc38-3f0ef962faf9
ms.openlocfilehash: 43402d8a1b0b1ca26e656be1424a5fa341ac4728
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57719645"
---
# <a name="how-to-add-multiple-sets-of-settings-to-your-application-in-c"></a>如何：将多组设置添加到你在 C 中的应用程序\#
在某些情况下，你可能想要的应用程序中有多组设置。 例如，如果你正在开发的应用设置的特定组的地方频繁进行更改，可能会比较明智的做法其全都分成单个文件，以便可以成批，替换该文件保持不受影响的其他设置。 Visual Studio，可将多组设置添加到你的项目。 可以通过 Properties.Settings 对象访问更多组设置。  
  
### <a name="to-add-an-additional-set-of-setting-to-your-application"></a>若要将一组额外的设置添加到你的应用程序  
  
1.  从“项目”菜单中选择“添加新项”。 此时将打开“添加新项”对话框。  
  
2.  在中**添加新项**对话框中，选择**设置文件**，键入该文件的名称，然后单击**添加**将新的设置文件添加到你的解决方案。  
  
3.  在中**解决方案资源管理器**，将为新的设置文件拖放**属性**文件夹。 这允许你设置可在代码中使用新设置。  
  
4.  添加和使用此文件中的设置，也可以是任何其他设置文件。 您可以访问此组通过 Properties.Settings 对象的设置。  
  
## <a name="see-also"></a>请参阅
- [使用应用程序设置和用户设置](using-application-settings-and-user-settings.md)
- [应用程序设置概述](application-settings-overview.md)
