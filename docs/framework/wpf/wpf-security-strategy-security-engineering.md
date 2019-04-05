---
title: WPF 安全策略 — 安全工程
ms.date: 03/30/2017
helpviewer_keywords:
- security [WPF], testing techniques
- Security Development Lifecycle (SDL), security analysis [WPF]
- Security Development Lifecycle (SDL), threat modeling
- Security Development Lifecycle (SDL), testing techniques
- Security Development Lifecycle (SDL), source analysis tools
- Security Development Lifecycle (SDL), critical code management
- threat modeling [WPF]
ms.assetid: 0fc04394-4e47-49ca-b0cf-8cd1161d95b9
ms.openlocfilehash: bddb9bb2cf9a601ce7796d17483c1ab8fa6d7aa1
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57378950"
---
# <a name="wpf-security-strategy---security-engineering"></a>WPF 安全策略 - 安全工程
可信计算是 Microsoft 为确保生成安全代码而首创的一项技术。 可信计算技术的一个关键元素是 [!INCLUDE[TLA#tla_sdl](../../../includes/tlasharptla-sdl-md.md)]。 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 是与标准工程过程一同用于简化提交安全代码的工程实践。 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 包含十个阶段，将规范化、可度量性和附加结构的最佳实践结合在一起，包括：  
  
-   安全设计分析  
  
-   基于工具的质量检查  
  
-   渗透测试  
  
-   最终安全评审  
  
-   发布后产品安全管理  
  
## <a name="wpf-specifics"></a>WPF 详细信息  
 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 工程团队可以应用和扩展 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)]，该产品组合包括以下主要方面：  
  
 [威胁建模](#threat_modeling)  
  
 [安全分析和编辑工具](#tools)  
  
 [测试技术](#techniques)  
  
 [关键代码管理](#critical_code)  
  
<a name="threat_modeling"></a>   
### <a name="threat-modeling"></a>威胁建模  
 威胁建模是 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)]的核心组件，用于分析系统，以确定潜在的安全漏洞。 一旦确定漏洞，威胁模型还可以确保采取适当的缓解措施。  
  
 我们以一个杂货店为例，说明威胁模型在高级别上所涉及的以下关键步骤：  
  
1.  **确定资产**。 杂货店的资产可能包括员工、保险箱、收银机和库存。  
  
2.  **枚举入口点**。 杂货店的入口点可能包括前门和后门、窗户、装货区和空调设备。  
  
3.  **使用入口点调查针对资产的攻击**。 可能进行的攻击包括通过空调入口点来对杂货店的保险箱资产进行攻击；有人可能会将空调设备拆掉，将保险箱通过空调处拉出杂货店。  
  
 威胁建模应用于整个 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]，包含以下各项：  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 分析器读取文件、将文本映射到相应的对象模型类并创建实际代码的方式。  
  
-   创建窗口句柄 (hWnd) 并通过其发送消息和呈现窗口内容的方式。  
  
-   数据绑定获取资源以及与系统交互的方式。  
  
 这些威胁模型对于在开发过程中确定安全设计需求以及缓解威胁非常重要。  
  
<a name="tools"></a>   
### <a name="source-analysis-and-editing-tools"></a>源分析和编辑工具  
 除 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 的手动安全代码评审元素外，[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 团队使用多个工具进行源分析和关联编辑，目的是减少安全漏洞。 使用了多种源工具，包括以下各项：  
  
-   **FXCop**:在托管代码中包括继承规则、 代码访问安全的使用情况以及安全地与非托管代码交互操作的方式查找常见安全问题。 请参阅[FXCop](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/bb429476%28v=vs.80%29)。  
  
-   **Prefix/Prefast**:例如缓冲区溢出、 格式字符串问题以及错误检查的非托管代码中查找安全漏洞和常见安全问题。  
  
-   **已禁止的 Api**:搜索源代码，以识别的函数的众所周知的而引发安全问题，如意外使用`strcpy`。 一旦识别出这些函数，将用更安全的替代函数来取代它们。  
  
<a name="techniques"></a>   
### <a name="testing-techniques"></a>测试技术  
 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 使用多种安全测试技术，包括：  
  
-   **白盒测试**:测试人员查看源代码，，然后生成攻击测试  
  
-   **黑盒测试**:测试人员尝试查找通过检查 API 和功能，安全，然后尝试对产品进行攻击。  
  
-   **从其他产品问题进行回归安全**:相关，来自相关产品的安全问题进行测试。 例如，对于 [!INCLUDE[TLA2#tla_ie](../../../includes/tla2sharptla-ie-md.md)]，已确定出大约六十个安全问题的相关变体，并已对它们在 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 上的适用性进行了测试。  
  
-   **借助文件模糊化执行基于工具的渗透测试**:文件模糊化执行是指利用文件读取器的输入范围的不同输入。 在 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 中的一个示例，使用此技术的一个示例就是检查图像解码代码的错误。  
  
<a name="critical_code"></a>   
### <a name="critical-code-management"></a>关键代码管理  
 有关[!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)]，[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]利用.NET Framework 支持标记和跟踪可提升特权的安全关键代码生成安全沙盒 (请参阅**安全关键方法**中[WPF安全策略-平台安全性](wpf-security-strategy-platform-security.md))。 考虑到对安全关键代码有较高的安全质量要求，因此需要对此类代码进行其他级别的源管理控制和安全审核。 大约有 5% 到 10% 的 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 由安全关键代码组成，这些代码由专门的审核团队进行审核。 通过跟踪安全关键代码和将每个关键实体（即，包含关键代码的方法）映射到其签署状态来对源代码和签入过程进行管理。 签署状态包括一个或多个审阅者的姓名。 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 的每个日常版本都将关键代码与前一版本中的该代码进行比较，以检查未经审批的更改。 如果工程师未经审核团队的批准而自行修改关键代码，则将识别并立即修复该代码。 通过这一过程，可以对 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 沙盒代码应用级别特高的审核并加以维护。  
  
## <a name="see-also"></a>请参阅
- [安全性](security-wpf.md)
- [WPF 部分信任安全](wpf-partial-trust-security.md)
- [WPF 安全策略 - 平台安全性](wpf-security-strategy-platform-security.md)
- [高信度计算](https://www.microsoft.com/mscorp/twc/default.mspx)
- [.NET 中的安全性](../../standard/security/index.md)
