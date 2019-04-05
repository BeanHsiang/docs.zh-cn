---
title: F# Interactive 选项
description: 了解有关支持的命令行选项F#交互式，fsi.exe。
ms.date: 05/16/2016
ms.openlocfilehash: cca1ef6671878acb1b837d6590139d5de7b7167d
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53128149"
---
# <a name="f-interactive-options"></a>F# Interactive 选项

> [!NOTE]
> 本文目前仅介绍适用于 Windows 的体验。  它将被重写。

本主题介绍支持的命令行选项F#Interactive， `fsi.exe`。 F#交互式接受很多与相同的命令行选项F#编译器，但还接受其他一些选项。

## <a name="using-f-interactive-for-scripting"></a>使用F#交互式用于脚本编写
F#交互式、 `fsi.exe`，可以通过交互方式，启动或从运行脚本的命令行启动它。 命令行语法

```
> fsi.exe [options] [ script-file [arguments] ]
```

文件扩展名为F#脚本文件是`.fsx`。

## <a name="table-of-f-interactive-options"></a>表的F#Interactive 选项
下表汇总了支持的选项F#交互。 在命令行上或通过 Visual Studio IDE，可以设置这些选项。 若要在 Visual Studio IDE 中设置这些选项，打开**工具**菜单中，选择**选项...**，然后展开**F#工具**节点，然后选择**F#交互**。

列表中出现的位置F#由分号分隔的参数交互选项，列表元素 (`;`)。

|选项|描述|
|------|-----------|
|**--**|用于指示F#Interactive 将其余参数视为命令行参数F#程序或脚本，可以使用列表在代码中访问**fsi.CommandLineArgs**。|
|**--checked**[**+**&#124;**-**]|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--codepage:&lt;int&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--consolecolors**[**+**&#124;**-**]|输出警告和错误消息的颜色。|
|**--crossoptimize**[**+**&#124;**-**]|启用或禁用跨模块优化。|
|**--debug**[**+**&#124;**-**]<br /><br />**-调试：**[**完整**&#124;**pdbonly**&#124;**可移植**&#124;**嵌入**]<br /><br />**-g**[**+**&#124;**-**]<br /><br />**-g:**[**完整**&#124;**pdbonly**&#124;**可移植**&#124;**嵌入**]|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--define:&lt;string&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--deterministic**[**+**&#124;**-**]|生成具有确定性的程序集 （包括模块版本 GUID 以及时间戳）。|
|**--exec**|指示F#交互式加载文件或运行命令行上给定的脚本文件后退出。|
|**--fullpaths**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--gui**[**+**&#124;**-**]|启用或禁用 Windows 窗体事件循环。 默认为已启用。|
|**--help**<br /><br />**-?**|用于显示命令行语法和每个选项的简短说明。|
|**-lib:&lt;文件夹列表&gt;**<br /><br />**-I:&lt;文件夹列表&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**-加载：&lt;文件名&gt;**|编译给定的源代码在启动时，将加载的已编译F#构造到会话。 如果目标源包含脚本指令，如 **#use**或 **#load**，则必须使用 **-使用**或者 **#use**而不是 **-加载**或 **#load**。|
|**--mlcompatibility**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--noframework**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)|
|**--nologo**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**-nowarn:&lt;警告列表&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--optimize**[**+**&#124;**-**]|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--preferreduilang:&lt;lang&gt;**| 指定首选的输出语言区域性名称 （例如，ES-ES，JA-JP）。 |
|**--quiet**|禁止显示F#交互窗口的输出传递给**stdout**流。|
|**--quotations-debug**|指定应派生自的表达式发出额外的调试信息F#的报价文本和反射的定义。 调试信息添加到自定义属性的F#表达式树节点。 请参阅[代码引用](code-quotations.md)并[Expr.CustomAttributes](https://msdn.microsoft.com/library/eb89943f-5f5b-474e-b125-030ca412edb3)。|
|**--readline**[**+**&#124;**-**]|启用或禁用在交互模式下的 tab 自动补全。|
|**-引用：&lt;文件名&gt;**<br /><br />**-:&lt;文件名&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--shadowcopyreferences**[**+**&#124;**-**]|阻止来自被锁定的引用F#交互进程。|
|**--simpleresolution**|使用基于目录的规则，而不是 MSBuild 解析的程序集引用进行解析。|
|**--tailcalls**[**+**&#124;**-**]|启用或禁用使用，尾 IL 指令将使得为尾递归函数重用堆栈帧。 默认情况下会启用此选项。|
|**-targetprofile:&lt;字符串&gt;**|指定此程序集的目标框架配置文件。 有效值为 mscorlib、 netcore 或 netstandard。  默认值为 mscorlib。|
|**-使用：&lt;文件名&gt;**|告知解释器使用给定的文件在启动时作为初始输入。|
|**--utf8output**|与 fsc.exe 编译器选项相同。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**-警告：&lt;警告级别&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--warnaserror**[**+**&#124;**-**]|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|
|**--warnaserror**[**+**&#124;**-**]:**&lt;int-list&gt;**|与相同**fsc.exe**编译器选项。 有关详细信息，请参阅[编译器选项](compiler-options.md)。|

## <a name="related-topics"></a>相关主题

|标题|描述|
|-----|-----------|
|[编译器选项](compiler-options.md)|介绍可用于命令行选项F#编译器**fsc.exe**。|
