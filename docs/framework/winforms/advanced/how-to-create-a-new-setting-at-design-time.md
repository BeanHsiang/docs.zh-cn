---
title: 如何：在设计时创建新的设置
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], design time
- application settings [Windows Forms], creating
ms.assetid: c5d60a66-6507-462f-a81f-e3bc0a804e16
ms.openlocfilehash: 54f64de8cdd47b7fd451d266cca3b7577e9e1d78
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57702771"
---
# <a name="how-to-create-a-new-setting-at-design-time"></a>如何：在设计时创建新的设置
使用设置设计器，可以在设计时创建一个新的设置。 设置设计器是一个网格样式接口，可用于创建新的设置，并指定这些设置的属性。 必须指定名称、 值、 类型和新的设置的作用域。 一旦创建了设置，就可在代码中访问。  
  
### <a name="to-create-a-new-setting-at-design-time-in-c"></a>若要在设计时在 C 中创建新的设置\#
  
1.  在中**解决方案资源管理器**，展开**属性**在项目节点。  
  
2.  双击想要添加新设置.settings 文件。 此文件的默认名称是 Settings.settings。  
  
3.  在设置设计器中，设置名称、 值、 类型和您的设置的作用域。 每行代表单个设置。  
  
### <a name="to-create-a-new-setting-at-design-time-in-visual-basic"></a>若要在设计时在 Visual Basic 中创建一个新的设置  
  
1.  在中**解决方案资源管理器**，右键单击项目节点并选择**属性**。  
  
2.  在中**属性**页上，选择**设置**选项卡。  
  
3.  在设置设计器中，设置名称、 值、 类型和您的设置的作用域。 每行代表单个设置。  
  
## <a name="see-also"></a>请参阅
- [使用应用程序设置和用户设置](using-application-settings-and-user-settings.md)
- [应用程序设置概述](application-settings-overview.md)
- [如何：在设计时的现有设置的值更改](how-to-change-the-value-of-an-existing-setting-at-design-time.md)
