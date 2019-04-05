---
title: 虚拟目录设置说明
ms.date: 03/30/2017
ms.assetid: 3c62cab5-81a4-48b6-ac8c-9ce33a85a157
ms.openlocfilehash: 0f32fd6d65db529ba1015dedd98f99efd7f408c4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54588099"
---
# <a name="virtual-directory-setup-instructions"></a>虚拟目录设置说明
Windows Communication Foundation (WCF) 示例旨在共享公共虚拟目录，名为 servicemodelsamples 的将映射到 %SystemDrive%\inetpub\wwwroot\servicemodelsamples 文件夹。  
  
> [!NOTE]
>  %SystemDrive% 通常为 C: 或 D:，具体取决于安装 Internet 信息服务 (IIS) 的驱动器位置。  
  
 可以运行 Setupvroot.bat 和 Cleanupvroot.bat 文件[的 Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)创建虚拟目录。 如果宁愿手动创建虚拟目录，请使用下面的过程。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-create-a-virtual-directory-in-iis-70-or-75"></a>若要在 IIS 7.0 或 7.5 中创建虚拟目录  
  
1.  从**启动**菜单上，单击**运行**，然后键入**inetmgr**以打开 Internet 信息服务 (IIS) MMC 管理单元。  
  
2.  在左窗格中，展开包含计算机的名称的节点，然后展开**站点**节点。  
  
3.  右键单击**Default Web Site**，然后选择**添加应用程序**以打开**添加应用程序窗口**。  
  
4.  在窗口中，键入`servicemodelsamples`作为要创建的虚拟目录的别名。  
  
5.  创建以下目录：%SystemDrive%\inetpub\wwwroot\servicemodelsamples  
  
6.  将物理路径设置为 %SystemDrive%\inetpub\wwwroot\servicemodelsamples。  大多数 WCF 示例在生成后都将服务可执行文件复制到此位置。  
  
7.  单击 **“确定”**。 现在已为 WCF 示例创建 Web 应用程序。  
  
    > [!NOTE]
    >  因为所有 WCF 示例都使用相同的 servicemodelsamples Web 应用程序，必须只有一次执行此任务。  
  
    > [!NOTE]
    >  在本文档中，术语`virtual directory`和 `Web application`是同义词。  
  
     除了创建虚拟目录，还必须设置其属性以启用要运行 WCF 服务。 有关详细信息，请参见以下内容。  
  
#### <a name="to-create-a-virtual-directory-in-iis-51-or-60"></a>在 IIS 5.1 或 6.0 中创建虚拟目录  
  
1.  打开命令提示符窗口并键入`start inetmgr`以打开 Internet 信息服务 (IIS) MMC 管理单元。  
  
2.  在左窗格中，展开包含计算机的名称的节点，然后展开**网站**节点。  
  
3.  右键单击**Default Web Site** ，然后选择**新的、 虚拟目录**以打开虚拟目录创建向导。  
  
4.  在向导中，键入`servicemodelsamples`作为要创建的虚拟目录的别名。  
  
5.  将路径设置为 %SystemDrive%\inetpub\wwwroot\servicemodelsamples。 大多数 WCF 示例在生成后都将服务可执行文件复制到此位置。  
  
6.  单击 **“下一步”**。  
  
7.  默认情况下，已选中以下复选框：  
  
    -   **Read**  
  
    -   **运行脚本 （如 ASP)**  
  
8.  单击**下一步**，然后单击**完成**以完成向导。  
  
    > [!NOTE]
    >  因为所有 WCF 示例都使用相同的 servicemodelsamples 虚拟目录，必须一次执行此任务。  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-70-or-75"></a>若要设置附加虚拟目录属性在 IIS 7.0 或 7.5  
  
1.  单击 servicemodelsamples 节点。 窗口的底部列有两个视图。 选择**功能视图**如果尚未选择它。  
  
2.  双击的条目**目录浏览**。  
  
3.  在操作窗格中选择**启用**选项。 这样，您将能够使用 Internet Explorer 访问目录的目录，这在调试服务时将很有帮助。  
  
 最后，您必须设置 servicemodelsamples 文件夹的安全属性，以允许其他人访问该文件夹。 有关详细信息，请参见以下内容。  
  
#### <a name="to-set-additional-virtual-directory-properties-in-iis-51-or-60"></a>在 IIS 5.1 或 6.0 中设置附加虚拟目录属性  
  
1.  右击 servicemodelsamples 节点，然后单击**属性**。  
  
2.  默认情况下，已选中以下复选框：  
  
    -   **Read**  
  
    -   **日志访问**  
  
    -   **编制此资源的索引**  
  
3.  选择**目录浏览**复选框。 这样，您将能够使用 Internet Explorer 访问目录的目录，这在调试服务时将很有帮助。  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-70-or-75"></a>在 IIS 7.0 或 7.5 中设置文件夹的安全属性  
  
1.  定位到 %SystemDrive%\inetpub\wwwroot\servicemodelsamples。  
  
2.  右击 servicemodelsamples 文件夹，单击**共享**或**共享与**。  
  
3.  单击左侧的向下箭头**添加**按钮。  
  
4.  选择**查找**条目。 **选择用户或组**窗口随即打开。  
  
5.  单击 **“高级”**。  
  
6.  单击**位置**。 **位置**窗口随即打开。  
  
7.  选择对应于所使用计算机的项。 请务必选择本地计算机，而不是对应于所列出的任何域或网络的项。 选择计算机之后，单击**确定**。  
  
8.  单击**立即查找**。 此操作将用与本地计算机关联的对象填充搜索结果。  
  
9. 查找**IIS_IUSRS**中的条目**名称 （相对可分辨名称）** 列。 选择该条目，然后单击**确定**关闭搜索结果窗口。  
  
10. 单击**确定**以关闭**选择用户或组**窗口。  
  
11. 单击**共享**保存所做的更改。  
  
12. 若要启用共享的更改完成后，单击**完成**以关闭**文件共享**窗口。  
  
#### <a name="to-set-security-properties-of-the-folder-in-iis-51-or-60"></a>在 IIS 5.1 或 6.0 中设置文件夹的安全属性  
  
1.  定位到 %SystemDrive%\inetpub\wwwroot\servicemodelsamples。  
  
2.  右键单击**servicemodelsamples**文件夹，然后单击**共享和安全。**  
  
3.  单击 **“安全”** 选项卡。  
  
4.  如果在使用 IIS 6.0**组或用户名**框中，检查是否**Internet 来宾帐户**列出。  
  
     如果该帐户未列出：  
  
    1.  单击“开始”，然后单击“控制面板”。  
  
    2.  如果没有看到**用户帐户**图标，单击**切换到分类视图**。  
  
    3.  单击**用户帐户**图标。  
  
    4.  在"或选择一个控制面板图标，"单击**用户帐户**。  
  
    5.  在中**用户帐户**对话框中，单击**高级**选项卡。  
  
    6.  单击 **“高级”**。  
  
    7.  在中**本地用户和组**对话框中，单击此项可展开**用户**文件夹。  
  
    8.  在右窗格中，双击**Internet 来宾帐户**。  
  
    9. 在中**属性**名称对话框中，复制用作 Internet 来宾帐户。 默认情况下，该名称以“USR_”开头，后跟计算机的名称。  
  
    10. 关闭“属性”  对话框。  
  
    11. 关闭**本地用户和组**对话框。  
  
    12. 关闭**用户帐户**对话框。  
  
    13. 关闭另**用户帐户**对话框。  
  
    14. 在中**servicemodelsamples 属性**对话框中，在**安全**选项卡上，单击**添加**。  
  
    15. 键入一个反斜杠后, 跟计算机的名称，然后粘贴 Internet 用户帐户，例如，myMachineName\\%internetguestaccountname%  
  
    16. 单击**检查名称**验证所添加。 如果名称有效，名称将变为全大写并带下划线的形式。  
  
5.  对于 IIS 6.0，还检查网络服务列在**组或用户名**框。  
  
     如果“NETWORK SERVICE”未列出：  
  
    1.  单击 **添加**。  
  
    2.  在中**选择用户或组**对话框中，键入计算机的名称后跟反斜杠。  
  
    3.  类型**服务**后反斜杠 （没有空格）。  
  
    4.  单击**检查名称**。  
  
    5.  如果找到多个名称，选择**网络服务**然后单击**确定**。  
  
    6.  单击**确定**以关闭**选择用户或组**对话框。  
  
6.  如果使用带 IIS 5.1 的 Windows XP SP2，请检查中列出了 Internet 来宾帐户和 ASPNET**组或用户名**框。  
  
     请注意，ASPNET 用户可能属于内置**用户**安全组。 如果是这样，那么，如果**用户**组列在对话框中，不需要将其作为单独的项添加到许可用户的列表。  
  
     若要检查 ASPNET 是否属于**用户**安全组：  
  
    1.  上**启动**菜单上，单击**控制面板**。  
  
    2.  单击**用户帐户**图标。  
  
    3.  在中**组**列中，检查的值**ASPNET**是"用户。  
  
## <a name="see-also"></a>请参阅
- [Internet 信息服务承载说明](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)
