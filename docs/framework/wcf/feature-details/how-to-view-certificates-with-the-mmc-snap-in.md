---
title: 如何：使用 MMC 管理单元查看证书
ms.date: 02/25/2019
helpviewer_keywords:
- certificates [WCF], viewing with the MMC snap-in
ms.assetid: 2b8782aa-ebb4-4ee7-974b-90299e356dc5
ms.openlocfilehash: 6ec86ffca9ae84a9c3276a3dd6de676919dcd2e0
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57200281"
---
# <a name="how-to-view-certificates-with-the-mmc-snap-in"></a>如何：使用 MMC 管理单元查看证书
当您创建安全的客户端或服务时，可以使用[证书](working-with-certificates.md)作为凭据。 例如，常见的凭据类型是 X.509 证书，创建具有<xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=nameWithType>方法。 

有三种不同类型的可以检查 Windows 系统上使用 Microsoft 管理控制台 (MMC) 的证书存储：

- 本地计算机：存储是在设备本地和全局上设备的所有用户。

- 当前用户：在存储区是本地的设备上的当前用户帐户。

- 服务帐户：在存储区是本地的设备上的特定服务。

  
## <a name="view-certificates-in-the-mmc-snap-in"></a>在 MMC 管理单元中查看证书 

下面的过程演示如何检查本地设备以查找相应的证书上的存储区： 
  
1. 选择**运行**从**启动**菜单中，然后输入*mmc*。 

    将显示在 MMC。 
  
2. 从**文件**菜单中，选择**添加/删除管理单元**。 
    
    **添加或删除管理单元**窗口会显示。
  
3. 从**可用的管理单元**列表中，选择**证书**，然后选择**添加**。  

    ![添加证书管理单元](./media/mmc-add-certificate-snap-in.png)
  
4. 在中**管理单元中的证书**窗口中，选择**计算机帐户**，然后选择**下一步**。 
  
    或者，您可以选择**我的用户帐户**当前用户或**服务帐户**针对特定服务。 

    > [!NOTE]
    > 如果您不管理员为你的设备，你可以仅对你的用户帐户的管理证书。
  
5. 在中**选择计算机**窗口中，保留**本地计算机**选择，并选择**完成**。  
  
6. 在中**管理单元中添加或删除**窗口中，选择**确定**。  
  
    ![添加证书管理单元](./media/mmc-certificate-snap-in-selected.png)

7. 可选：从**文件**菜单中，选择**保存**或**另存为**保存 MMC 控制台文件以供将来使用。  

8. 若要查看你的证书 MMC 管理单元中，选择**控制台根节点**在左窗格中，然后展开**证书 （本地计算机）**。

    将显示每种类型的证书的目录的列表。 从每个证书目录中，可以查看、 导出、 导入，并删除其证书。
  

## <a name="view-certificates-with-the-certificate-manager-tool"></a>使用证书管理器工具查看证书

您还可以查看、 导出、 导入，和使用证书管理器工具中删除证书。

### <a name="to-view-certificates-for-the-local-device"></a>若要查看本地设备的证书

1. 选择**运行**从**启动**菜单中，然后输入*certlm.msc*。 

    将显示本地设备的证书管理器工具。 
  
2. 若要查看您的证书，在**证书-本地计算机**在左窗格中，展开你想要查看的证书的类型的目录。

### <a name="to-view-certificates-for-the-current-user"></a>若要查看当前用户证书

1. 选择**运行**从**启动**菜单中，然后输入*certmgr.msc*。 

    当前用户的证书管理器工具会显示。 
  
2. 若要查看您的证书，在**证书-当前用户**在左窗格中，展开你想要查看的证书的类型的目录。

  
## <a name="see-also"></a>请参阅
- [使用证书](working-with-certificates.md)
- [如何：创建开发期间使用的临时证书](how-to-create-temporary-certificates-for-use-during-development.md)
- [如何：检索证书的指纹](how-to-retrieve-the-thumbprint-of-a-certificate.md)
