---
title: CLR 探查器和 Windows 应用商店应用程序
ms.date: 03/30/2017
dev_langs:
- csharp
applies_to:
- Windows 10
- Windows 8
helpviewer_keywords:
- profiling API
- profiling API [.NET Framework]
- profiling managed code
- profiling managed code [Windows Store Apps]
ms.assetid: 1c8eb2e7-f20a-42f9-a795-71503486a0f5
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 93344e1c5aa62e86d29a0110a9d8cffc3cea66ff
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57358543"
---
# <a name="clr-profilers-and-windows-store-apps"></a>CLR 探查器和 Windows 应用商店应用程序

本主题讨论你需要想办法编写诊断工具分析的管理 Windows 应用商店应用程序内运行的代码时。 它还提供了指导原则来修改现有的开发工具，以使它们继续工作时对 Windows 应用商店应用程序运行它们。 若要了解此信息，最好是如果您熟悉使用公共语言运行时分析 API，已针对 Windows 桌面应用程序，并且您正确运行现在感兴趣修改该工具的诊断工具中使用此 API若要针对 Windows 应用商店应用程序正确运行。

## <a name="introduction"></a>介绍

如果过去的介绍性段落中做它，然后您熟悉 CLR 分析 API。 编写了一个诊断工具，还针对托管桌面应用程序。 现在，您想要执行的操作，以便所需的工具适用于托管的 Windows 应用商店应用程序。 可能已尝试进行这项工作，并发现它不是简单的任务。 实际上，有一些可能不太明显的所有工具开发人员的注意事项。 例如：

- 具有严重降低的权限的上下文中运行 Windows 应用商店应用程序。

- Windows 元数据文件具有唯一特征相比传统的托管模块时。

- Windows 应用商店应用程序具有交互性出现故障时挂起自己的习惯。

- 进程间通信机制可能由于各种原因而无法继续工作。

本主题列出了需要注意的事项，以及如何正确处理它们。

如果您熟悉 CLR 分析 API，请跳到本主题末尾处的资源，可找到更好地介绍性信息。

提供有关特定 Windows Api 使用方式的详细信息也是本主题的讨论范围内。 请考虑本主题的起点，并参考 MSDN，了解有关此处引用的任何 Windows Api 的详细信息。

## <a name="architecture-and-terminology"></a>体系结构和术语

通常，一种诊断工具的体系结构，如下面的插图中所示。 它使用术语"探查器，"但许多此类工具远不止于典型性能或内存分析为领域，如代码覆盖率，模拟对象框架、 时程调试应用程序监视，依此类推。 为简单起见，本主题将继续引用所有这些工具为探查器。

在本主题中使用了以下术语：

**应用程序**

这是探查器分析的应用程序。 通常情况下，此应用程序的开发人员现在使用探查器可帮助您诊断与应用程序的问题。 传统上，此应用程序是 Windows 桌面应用程序，但在本主题中，我们正在寻找 Windows 应用商店应用程序。

**Profiler DLL**

这是将加载到应用程序所分析的进程空间的组件。 此组件，也称为探查器"代理，"将实现[ICorProfilerCallback](icorprofilercallback-interface.md)[ICorProfilerCallback 接口](icorprofilercallback-interface.md)(2，3，等等) 接口，并在使用[ICorProfilerInfo](icorprofilerinfo-interface.md)(2，3，等等) 接口，以便收集有关已分析的应用程序和可能的数据修改应用程序的行为的各个方面。

**Profiler UI**

这是探查器用户与之交互的桌面应用程序。 它负责向用户显示应用程序状态以及可让用户控制的已分析的应用程序的行为的方法。 此组件始终在其自身进程空间，独立于应用程序所分析的进程空间中运行。 Profiler UI 也可用作"附加触发器，"该调用进程[iclrprofiling:: Attachprofiler](iclrprofiling-attachprofiler-method.md)方法，使分析应用程序中，若要加载在这些情况下，探查器 DLL 没有 Profiler DLL在启动时加载。

> [!IMPORTANT]
> Profiler UI 应保持 Windows 桌面应用程序，即使它所应用到控件和 Windows 应用商店应用程序的报表。 不希望能够打包和交付您在 Windows 应用商店中的诊断工具。 需要执行操作的 Windows 应用商店应用程序不能这样做，并提供其中的许多驻留在 Profiler UI 所需的工具。

在本文档的示例代码假定：

- Profiler DLL 是用 c + +，因为它必须是本机 DLL，根据 CLR 分析 API 的要求。

- Profiler UI 是用 C# 编写的。 这不是有必要，但因为没有任何要求 Profiler UI 的过程语言，为什么不选择一种语言的简洁和简单？

### <a name="windows-rt-devices"></a>Windows RT 设备

Windows RT 设备相当已锁定。 只需第三方探查器无法加载此类设备上。 本文档重点介绍 Windows 8 Pc。

## <a name="consuming-windows-runtime-apis"></a>使用 Windows 运行时 Api

在以下各节所述的方案很多，Profiler UI 桌面应用程序需要使用一些新的 Windows 运行时 Api。 您需要请查阅文档以了解可以从桌面应用程序使用的 Windows 运行时 Api 和它们的行为不同时是否调用从桌面应用程序和 Windows 应用商店应用。

如果 Profiler UI 用托管代码编写的将有几个步骤都需要执行的操作进行使用这些简单的 Windows 运行时 Api。 请参阅[托管桌面应用程序和 Windows 运行时](https://go.microsoft.com/fwlink/?LinkID=271858)文章了解详细信息。

## <a name="loading-the-profiler-dll"></a>正在加载 Profiler DLL

本部分介绍如何 Profiler UI 将导致 Windows 应用商店应用程序加载 Profiler DLL。 在本部分中所讨论的代码位于 Profiler UI 桌面应用程序，并因此涉及到使用安全的桌面应用程序，但不一定是安全的 Windows 应用商店应用程序的 Windows Api。

Profiler UI 可能会导致你 Profiler DLL 被加载到应用程序的进程空间中通过两种方式：

- 在应用程序启动时，如控制的环境变量。

- 通过将附加到应用程序启动完成后通过调用[iclrprofiling:: Attachprofiler](iclrprofiling-attachprofiler-method.md)方法。

第一个障碍之一将获取启动负载和附加负载的 Profiler DLL 与 Windows 应用商店应用程序一起正常工作。 加载这两种形式共享公用的特殊注意事项，因此，让我们开始使用它们。

### <a name="common-considerations-for-startup-and-attach-loads"></a>常见注意事项启动和附加的负载

**签名在 Profiler DLL**

当 Windows 尝试加载 Profiler DLL 时，它验证 Profiler DLL 已正确签名。 如果没有，则加载默认情况下会失败。 有两种方法可以实现此目的：

- 请确保您 Profiler 的 DLL 进行签名。

- 告诉您的用户，他们必须安装开发人员许可证在其 Windows 8 计算机上使用所需的工具之前。 这可以从 Visual Studio 或手动从命令提示符处自动完成。 有关详细信息，请参阅[获取开发人员许可证](https://docs.microsoft.com/previous-versions/windows/apps/hh974578(v=win.10))。

**文件系统权限**

Windows 应用商店应用程序必须有权加载并从它的文件系统上的位置执行 Profiler DLL residesBy 默认情况下，Windows 应用商店应用程序不具备在大多数目录和任何失败的尝试加载 Profiler DLL 上的此类权限将生成如下所示的 Windows 应用程序事件日志中的条目：

```Output
NET Runtime version 4.0.30319.17929 - Loading profiler failed during CoCreateInstance.  Profiler CLSID: '{xxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}'.  HRESULT: 0x80070005.  Process ID (decimal): 4688.  Message ID: [0x2504].
```

通常情况下，Windows 应用商店应用程序只允许访问一组有限的磁盘上的位置。 每个 Windows 应用商店应用程序可以为其所有 Windows 应用商店应用程序被都授予访问权限的文件系统中访问其自己的应用程序数据文件夹，以及其他几个方面。 最好是安装 Profiler DLL Program Files 或 Program Files (x86) 下的某个位置及其依赖项，因为所有 Windows 应用商店应用程序具有读取和执行权限默认情况下。

### <a name="startup-load"></a>启动负载

通常情况下，在桌面应用中，Profiler UI 会提示你 Profiler DLL 启动负载通过初始化包含所需的 CLR 分析 API 的环境变量的环境块 (即`COR_PROFILER`， `COR_ENABLE_PROFILING`，和`COR_PROFILER_PATH`)，并然后使用该环境块创建一个新的进程。 同样适用于 Windows 应用商店应用程序，但机制不同。

**不会运行提升的权限**

如果进程尝试生成 Windows 应用商店应用程序进程 B 进程 A 应运行在中等完整性级别，不能在高完整性级别 （即，未提升的权限）。 这意味着应在中等完整性级别运行 Profiler UI，或它必须生成在中等完整性级别启动 Windows 应用商店应用程序，需要注意的另一个桌面进程。

**选择 Windows 应用商店应用到配置文件**

首先，你将想要让探查器用户启动的 Windows 应用商店应用程序。 对于桌面应用，可能会显示文件浏览对话框中，然后用户会查找并选择.exe 文件。 但 Windows 应用商店应用程序是不同的并使用一个浏览对话框没有任何意义。 相反，它是更好地向用户显示的 Windows 应用商店应用程序已安装了该用户就可以从选择列表。

可以使用<xref:Windows.Management.Deployment.PackageManager>类来生成此列表。 `PackageManager` 适用于桌面应用的 Windows 运行时类，实际上它是*仅*适用于桌面应用。

下面的代码示例假设 Profiler UI 编写桌面应用程序中为从C#使用`PackageManager`生成的 Windows 应用的列表：

```csharp
string currentUserSID = WindowsIdentity.GetCurrent().User.ToString();
IAppxFactory appxFactory = (IAppxFactory) new AppxFactory();
PackageManager packageManager = new PackageManager();
IEnumerable<Package> packages = packageManager.FindPackagesForUser(currentUserSID);
```

**指定的自定义的环境块**

新的 COM 接口， [IPackageDebugSettings](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)，可用于自定义为了简化某些形式的诊断的 Windows 应用商店应用的执行行为。 其方法之一[EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)，可以将环境块传递给 Windows 应用商店应用程序时它已启动，以及其他有用的效果，例如禁用自动进程挂起。 环境块很重要，因为这是您需要指定环境变量 (`COR_PROFILER`， `COR_ENABLE_PROFILING`，和`COR_PROFILER_PATH)`) 使用 CLR 加载 Profiler DLL。

请思考以下代码片段：

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, debuggerCommandLine,
                                                                 (IntPtr)fixedEnvironmentPzz);
```

有几个项都需要得到正确结果：

- `packageFullName` 可循环访问包，然后抓取时确定`package.Id.FullName`。

- `debuggerCommandLine` 更有趣的是。 若要将自定义的环境块传递给 Windows 应用商店应用程序，需要编写您自己，简单的虚拟调试器。 Windows 会生成 Windows 应用商店应用程序挂起，然后将调试器附加通过启动您的调试器在此示例中类似的命令行：

    ```Output
    MyDummyDebugger.exe -p 1336 -tid 1424
    ```

     其中`-p 1336`意味着 Windows 应用商店应用程序具有进程 ID 1336 和`-tid 1424`表示线程 ID 1424 是线程处于挂起状态。 虚拟调试器会分析从命令行 ThreadID，恢复该线程，然后退出。

     下面是一些示例来执行此操作的 c + + 代码 （请确保添加错误检查 ！）：

    ```cpp
    int wmain(int argc, wchar_t* argv[])
    {
        // …
        // Parse command line here
        // …

        HANDLE hThread = OpenThread(THREAD_SUSPEND_RESUME,
                                                                  FALSE /* bInheritHandle */, nThreadID);
        ResumeThread(hThread);
        CloseHandle(hThread);
        return 0;
    }
    ```

     将需要安装的一部分在诊断工具，为部署此虚拟调试器，然后指定的路径中此调试器`debuggerCommandLine`参数。

**启动 Windows 应用商店应用程序**

启动 Windows 应用商店应用的时刻终于到来了。 如果您已尝试过做自己，您可能已经注意到， [CreateProcess](/windows/desktop/api/processthreadsapi/nf-processthreadsapi-createprocessa)是不创建 Windows 应用商店应用程序进程。 相反，你将需要使用[IApplicationActivationManager::ActivateApplication](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-iapplicationactivationmanager-activateapplication)方法。 为此，你将需要获取要启动的 Windows 应用商店应用的应用程序用户模型 ID。 这意味着您将需要执行一个小获知清单。

时循环访问你的程序包 (请参阅中的"选择 Windows 应用商店应用到配置文件"[启动负载](#startup-load)前面部分)，可能想要获取当前包清单中包含的应用程序的一：

```csharp
string manifestPath = package.InstalledLocation.Path + "\\AppxManifest.xml";

AppxPackaging.IStream manifestStream;
SHCreateStreamOnFileEx(
                    manifestPath,
                    0x00000040,     // STGM_READ | STGM_SHARE_DENY_NONE
                    0,              // file creation attributes
                    false,          // fCreate
                    null,           // reserved
                    out manifestStream);

IAppxManifestReader manifestReader = appxFactory.CreateManifestReader(manifestStream);

IAppxManifestApplicationsEnumerator appsEnum = manifestReader.GetApplications();
```

是的一个包可以有多个应用程序，并且每个应用程序具有其自己的应用程序用户模型 id。 因此你将想要提出你的用户的应用程序到配置文件，并获取该特定应用程序中的应用程序用户模型 ID:

```csharp
while (appsEnum.GetHasCurrent() != 0)
{
    IAppxManifestApplication app = appsEnum.GetCurrent();
    string appUserModelId = app.GetAppUserModelId();
    //...
}
```

最后，您现在有您需要启动 Windows 应用商店应用程序：

```csharp
IApplicationActivationManager appActivationMgr = new ApplicationActivationManager();
appActivationMgr.ActivateApplication(appUserModelId, appArgs, ACTIVATEOPTIONS.AO_NONE, out pid);
```

**请记住要调用 DisableDebugging**

当调用[IPackageDebugSettings::EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)，所做的承诺，您将清理后自行通过调用[IPackageDebugSettings::DisableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging)方法，因此请确保执行操作分析会话时通过。

### <a name="attach-load"></a>附加负载

当 Profiler UI 想要将其 Profiler DLL 附加到已开始运行的应用程序时，它使用[iclrprofiling:: Attachprofiler](iclrprofiling-attachprofiler-method.md)。 同样适用于 Windows 应用商店应用。 但除了前面列出的常见注意事项，请确保目标 Windows 应用商店应用程序不会挂起。

**EnableDebugging**

通过启动负载，如调用[IPackageDebugSettings::EnableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-enabledebugging)方法。 您不需要它传递的环境块，但您需要其他功能之一： 禁用自动进程挂起。 否则为当 Profiler UI 调用[AttachProfiler](iclrprofiling-attachprofiler-method.md)，目标 Windows 应用商店应用程序可能会挂起。 实际上，这可能是如果用户现在使用 Profiler UI，进行交互，并且 Windows 应用商店应用程序未在任何用户的屏幕上处于活动状态。 如果应用已挂起 Windows 应用商店，它也不能以响应任何发出信号，CLR 会向它发送附加 Profiler DLL。

因此您会希望执行如下操作：

```csharp
IPackageDebugSettings pkgDebugSettings = new PackageDebugSettings();
pkgDebugSettings.EnableDebugging(packageFullName, null /* debuggerCommandLine */,
                                                                 IntPtr.Zero /* environment */);
```

这是在相同的调用，但未指定调试器命令行或环境块为启动加载的情况下，可能会使。

**DisableDebugging**

与往常一样，不要忘记调用[IPackageDebugSettings::DisableDebugging](/windows/desktop/api/shobjidl_core/nf-shobjidl_core-ipackagedebugsettings-disabledebugging)完成分析会话的。

## <a name="running-inside-the-windows-store-app"></a>在 Windows 应用商店应用程序内部运行

因此 Windows 应用商店应用程序已最后加载 Profiler DLL。 现在必须如何通过不同的规则所需的 Windows 应用商店应用程序播放让 Profiler DLL，包括允许哪些 Api 以及如何使用运行较少的权限。

### <a name="stick-to-the-windows-store-app-apis"></a>坚持使用 Windows 应用商店应用 Api

当您浏览 Windows API 时，您会注意到不会成为适用于桌面应用程序、 Windows 应用商店应用程序，或同时记录了每个 API。 例如，**要求**的文档部分[InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount)函数指示该函数，适用于桌面应用程序。 与此相反， [InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex)函数是可用于桌面应用程序和 Windows 应用商店应用程序。

在开发 Profiler DLL 时，将它视为如同它是 Windows 应用商店应用程序，并只使用记录到 Windows 应用商店应用程序为可用的 Api。 分析依赖项 (例如，可以运行`link /dump /imports`针对 Profiler DLL 审核)，然后搜索文档，请参阅哪些依赖项是确定，这不是。 在大多数情况下，可以通过只需将它们替换为用于记录为安全的 API 的较新窗体修复您的违规 (例如，替换[InitializeCriticalSectionAndSpinCount](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionandspincount)与[InitializeCriticalSectionEx](/windows/desktop/api/synchapi/nf-synchapi-initializecriticalsectionex))。

您可能注意到 Profiler DLL 调用适用于桌面应用程序，某些 Api 和它们看上去尚未处理甚至 Profiler DLL 加载 Windows 应用商店应用程序内。 请注意，它是有风险，若要使用 Profiler DLL 时加载到 Windows 应用商店应用程序进程中的 Windows 应用商店应用程序与使用未记录任何 API:

- 此类 Api 不保证能够在 Windows 应用商店应用程序中运行的唯一上下文中调用时。

- 从不同的 Windows 应用商店应用程序进程中调用时，此类 Api 可能不一致地工作。

- 此类 Api 可能看起来可以从当前版本的 Windows 中的 Windows 应用商店应用程序正常工作，但可能会中断或在 Windows 的未来版本中禁用。

最佳建议是解决所有冲突，并避免风险。

你可能会发现您绝对不能缺少特定的 API 和找不到替代适用于 Windows 应用商店应用程序。 这种情况下，最小值：

- 测试、 测试、 测试生活 daylights 超出该 API 的使用情况。

- 了解 API 可能会突然中断或消失如果调用从在 Windows 应用商店应用在将来的版本的 Windows。 这不会由 Microsoft、 被视为一个兼容性问题和支持它的使用情况不会具有优先级。

### <a name="reduced-permissions"></a>降低的权限

它位于本主题列出 Windows 应用商店应用程序权限不同于桌面应用程序的所有方式的范围之外。 但当然行为将每次尝试访问的任何资源 Profiler DLL （时加载到与桌面应用程序相比的 Windows 应用商店应用） 时不同。 文件系统是最常见的例子。 存在但在给定的 Windows 应用商店应用程序有权访问的磁盘上放置几个 (请参阅[文件的访问和权限 (Windows 运行时应用](https://docs.microsoft.com/previous-versions/windows/apps/hh967755(v=win.10)))，并且您 Profiler 的 DLL 将相同的限制。 进行全面测试您的代码。

### <a name="inter-process-communication"></a>进程间通信

在本白皮书开头图中所示，Profiler DLL （加载到 Windows 应用商店应用程序进程空间） 可能需要与你 Profiler 的 UI （在单独的桌面应用程序进程空间中运行） 通过你自己自定义进程间通信通信 (IPC) 通道。 Profiler UI 将信号发送到要修改其行为的 Profiler DLL 和 Profiler DLL 将数据从已分析 Windows 应用商店应用发送回用于后续处理和向探查器用户显示的 Profiler UI。

大多数探查器需要处理这种方式，但您的 IPC 机制为选择限制更多 Profiler DLL 加载到 Windows 应用商店应用程序时。 例如，命名的管道不属于 Windows 应用商店应用程序 SDK，因此不能使用它们。

但毫无疑问，文件仍在中，但以限制更多的方式。 此外，还提供事件。

**通过文件进行通信**

大部分数据将通过文件可能传递 Profiler DLL 和 Profiler UI 之间。 关键是要选取你 Profiler DLL （在 Windows 应用商店应用的上下文中） 和 Profiler UI 具有读取的文件位置和写入访问权限。 例如，临时文件夹的路径是一个位置，可以访问您的 Profiler DLL 和 Profiler UI，但没有其他 Windows 应用商店应用程序包可以访问 （从而避免登录其他 Windows 应用商店应用包中的任何信息）。

在 Profiler UI 和 Profiler DLL 可以独立地确定此路径。 在 Profiler 用户界面，它循环访问所有为当前用户安装的包 （请参阅前面的示例代码），获取的访问权限`PackageId`类，类似于此代码段中的代码与派生的临时文件夹路径。 （与往常一样，错误检查省略了为简洁起见。）

```csharp
// C# code for the Profiler UI.
ApplicationData appData =
    ApplicationDataManager.CreateForPackageFamily(
        packageId.FamilyName);

tempDir = appData.TemporaryFolder.Path;
```

同时，Profiler DLL 可以执行基本上是相同的操作，但它可以更多轻松地访问<xref:Windows.Storage.ApplicationData>通过使用类[ApplicationData.Current](xref:Windows.Storage.ApplicationData.Current%2A)属性。

**通过事件进行通信**

如果你想在 Profiler UI 和 Profiler DLL 之间的简单信号语义，可以使用 Windows 应用商店应用程序，以及桌面应用程序内的事件。

从 Profiler DLL，只需调用[CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa)函数以使用任何喜欢的名称创建命名的事件。 例如：

```cpp
// Profiler DLL in Windows Store app (C++).
CreateEventEx(
    NULL,  // Not inherited
    "MyNamedEvent"
    CREATE_EVENT_MANUAL_RESET, /* explicit ResetEvent() required; leave initial state unsignaled */
    EVENT_ALL_ACCESS);
```

Profiler UI 然后需要查找 Windows 应用商店应用程序的命名空间下该命名的事件。 例如，可以调用 Profiler UI [CreateEventEx](/windows/desktop/api/synchapi/nf-synchapi-createeventexa)，指定为事件名称

`AppContainerNamedObjects\<acSid>\MyNamedEvent`

`<acSid>` 为 Windows 应用商店应用程序的 AppContainer SID。 本主题前面部分介绍了如何循环访问当前用户安装的包。 从该示例代码中，你可以获取包 Id。 你可以从包 Id，获取和`<acSid>`，类似于以下代码：

```csharp
IntPtr acPSID;
DeriveAppContainerSidFromAppContainerName(packageId.FamilyName, out acPSID);

string acSid;
ConvertSidToStringSid(acPSID, out acSid);

string acDir;
GetAppContainerFolderPath(acSid, out acDir);
```

### <a name="no-shutdown-notifications"></a>没有关闭通知

运行时在 Windows 应用商店应用程序内，Profiler DLL 不应依赖于任一[icorprofilercallback:: Shutdown](icorprofilercallback-shutdown-method.md)甚至[DllMain](/windows/desktop/Dlls/dllmain) (使用`DLL_PROCESS_DETACH`) 正在调用以通知 Profiler DLL正在退出 Windows 应用商店应用程序。 事实上，应该会永远不会调用。 从历史上看，许多 Profiler Dll 使用这些通知作为方便的位置以刷新缓存磁盘、 关闭文件，将通知发送回的 Profiler UI，等等。但现在需要稍有不同组织 Profiler DLL。

Profiler DLL 时对其应为日志记录信息。 出于性能原因，你可能想要批处理在内存中的信息，然后刷新到磁盘大小超过某个阈值批处理随着。 但假设尚未刷新到磁盘的任何信息可能会丢失。 这意味着您需要明智地，选取你的阈值，Profiler UI 需要强制应对编写的 Profiler DLL 的信息不完整。

## <a name="windows-runtime-metadata-files"></a>Windows 运行时元数据文件

它是深入介绍本文档的讨论范围内哪些 Windows 运行时元数据 (WinMD) 文件。 本部分仅限于 CLR 分析 API 在 WinMD 文件加载的 Profiler DLL 分析 Windows 应用商店应用程序时的反应。

### <a name="managed-and-non-managed-winmds"></a>托管和非托管 Winmd

如果开发人员使用 Visual Studio 创建新的 Windows 运行时组件项目，该项目的生成过程生成 WinMD 文件，描述由开发人员编写的元数据 （类、 接口等的类型说明）。 如果此项目是用 C# 或 VB 编写的托管的语言项目，该相同的 WinMD 文件还包含这些类型 （它包含所有从开发人员的源代码编译的 IL 的含义） 的实现。 此类文件称为托管 WinMD 文件。 它们是有趣，因为它们包含 Windows 运行时元数据和基础实现。

与此相反，如果开发人员的 c + + 创建 Windows 运行时组件项目，生成该项目生成包含仅元数据的 WinMD 文件，并实现编译为单独的本机 DLL。 同样，在 Windows SDK 中提供的 WinMD 文件包含仅元数据编译到单独的本机 Dll 作为 Windows 的一部分提供的实现。

下面的信息适用于包含元数据和实现，这两个托管 Winmd 和非托管 Winmd，其中包含仅元数据。

### <a name="winmd-files-look-like-clr-modules"></a>WinMD 文件看起来像 CLR 模块

CLR 是而言，所有 WinMD 文件都是模块。 在 Profiler DLL 时加载 WinMD 文件和其 Moduleid 中有哪些，其他托管模块时一样，因此能够告知 CLR 分析 API。

Profiler DLL 可以通过调用从其他模块区分 WinMD 文件[ICorProfilerInfo3::GetModuleInfo2](icorprofilerinfo3-getmoduleinfo2-method.md)方法，并检查`pdwModuleFlags`输出参数[COR_PRF_MODULE_WINDOWS_运行时](cor-prf-module-flags-enumeration.md)标志。 （是设置当且仅当 ModuleID 表示 WinMD。）

### <a name="reading-metadata-from-winmds"></a>从 Winmd 读取元数据

WinMD 文件，类似于常规模块包含可通过读取的元数据[元数据 Api](../../../../docs/framework/unmanaged-api/metadata/index.md)。 但是，CLR 将 Windows 运行时类型到.NET Framework 类型时它会读取 WinMD 文件，以便开发人员可以在托管代码中进行编程和使用 WinMD 文件可以更自然的编程体验。 有关这些映射的一些示例，请参阅[.NET Framework 支持的 Windows 应用商店应用程序和 Windows 运行时](../../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)。

因此哪种视图在探查器时，将看到它使用元数据 Api： 原始的 Windows 运行时视图或映射的.NET Framework 视图？  答案： 完全取决于您。

当您调用[icorprofilerinfo:: Getmodulemetadata](icorprofilerinfo-getmodulemetadata-method.md)方法获取元数据接口，例如 WinMD [IMetaDataImport](../../../../docs/framework/unmanaged-api/metadata/imetadataimport-interface.md)，你可以选择设置[ofNoTransform](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md)中`dwOpenFlags`参数来关闭此映射。 否则，默认情况下将启用此映射。 通常情况下，探查器将保持启用，该映射，以便从 WinMD 元数据 （例如，类型的名称） 获取 Profiler DLL 的字符串看起来熟悉和自然向探查器用户。

### <a name="modifying-metadata-from-winmds"></a>修改从 Winmd 元数据

不支持修改中 Winmd 元数据。 如果您调用[icorprofilerinfo:: Getmodulemetadata](icorprofilerinfo-getmodulemetadata-method.md)方法的 WinMD 文件，并指定[ofWrite](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md)中`dwOpenFlags`参数或可写元数据接口提出，例如[IMetaDataEmit](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)， [GetModuleMetaData](icorprofilerinfo-getmodulemetadata-method.md)将失败。 这是于 IL 重写的探查器需要修改元数据以支持其检测 （例如，若要添加 AssemblyRefs 或新的方法） 尤其重要。 因此，应检查[COR_PRF_MODULE_WINDOWS_RUNTIME](cor-prf-module-flags-enumeration.md)首先 （如在上一节中讨论） 并避免在要求可写元数据接口提供对此类模块。

### <a name="resolving-assembly-references-with-winmds"></a>解析与 Winmd 的程序集引用

对于许多探查器需要解析元数据引用手动以帮助检测或类型检查。 此类探查器需要了解的 CLR 如何解析指向 Winmd，程序集引用，因为在标准的程序集引用完全不同的方式解析这些引用。

## <a name="memory-profilers"></a>内存探查器

垃圾回收器和托管的堆不完全不同的 Windows 应用商店应用和桌面应用程序中。 但是，有一些细微的差异，探查器作者需要注意。

### <a name="forcegc-creates-a-managed-thread"></a>ForceGC 创建托管的线程

Profiler DLL 时执行操作的内存分析，通常创建一个单独的线程从其调用[ForceGC 方法](icorprofilerinfo-forcegc-method.md)方法。 这是什么新鲜事物。 但什么可能会感到惊讶是执行垃圾回收中的 Windows 应用商店应用的行为可能会将你的线程转换为托管线程 （例如，分析 API ThreadID 将为该线程创建）。

若要了解这一后果，务必了解同步和异步调用之间的差异，由 CLR 分析 API 定义。 请注意，这是从 Windows 应用商店应用中的异步调用的概念非常不同。 请参阅博客文章[我们使用了 CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](https://blogs.msdn.microsoft.com/davbr/2008/12/23/why-we-have-corprof_e_unsupported_call_sequence/)有关详细信息。

相关的问题是，由探查器创建的线程上进行的调用，总是会考虑同步的即使这些调用都是从外部的 Profiler DLL 的一个实现[ICorProfilerCallback](icorprofilercallback-interface.md)方法。 至少，它用于出现这种情况。 现在，CLR 已启用探查器的线程到托管线程对的调用由于[ForceGC 方法](icorprofilerinfo-forcegc-method.md)，线程将不再被视为探查器的线程。 在这种情况下，CLR 强制实施更严格的什么限定为该线程同步定义 — 即的调用必须源自的 Profiler DLL 的一个[ICorProfilerCallback](icorprofilercallback-interface.md)限定为同步的方法。

在实践中，这意味着什么？ 大多数[ICorProfilerInfo](icorprofilerinfo-interface.md)仅安全地同步，调用方法，否则将立即失败。 因此，如果 Profiler DLL 重用您[ForceGC 方法](icorprofilerinfo-forcegc-method.md)探查器创建的线程通常由其他调用的线程 (例如，若[RequestProfilerDetach](icorprofilerinfo3-requestprofilerdetach-method.md)， [RequestReJIT](icorprofilerinfo4-requestrejit-method.md)，或[RequestRevert](icorprofilerinfo4-requestrevert-method.md))，您会遇到问题。 甚至如异步安全函数[DoStackSnapshot](icorprofilerinfo2-dostacksnapshot-method.md)已从托管线程中调用时的特殊规则。 (请参阅博客文章[Profiler 堆栈遍历：基础知识及更高版本](https://blogs.msdn.microsoft.com/davbr/2005/10/06/profiler-stack-walking-basics-and-beyond/)有关详细信息。)

因此，我们建议您 Profiler 的 DLL 创建，以便在调用任何线程[ForceGC 方法](icorprofilerinfo-forcegc-method.md)应使用*仅*为了触发 Gc，然后响应 GC 回调。 它不应调用到分析 API 来执行其他任务，例如采样或分离的堆栈。

### <a name="conditionalweaktablereferences"></a>ConditionalWeakTableReferences

从.NET Framework 4.5 开始，还有一个新的 GC 回调[ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md)，其中给出了探查器有关的更完整信息*依赖句柄*。 这些句柄有效地将引用从源对象添加到以进行 GC 生存期管理的目标对象。 依赖句柄是什么新鲜事物，并在托管代码中进行编程的开发人员就能够通过创建其自己的依赖句柄<xref:System.Runtime.CompilerServices.ConditionalWeakTable%602?displayProperty=nameWithType>甚至在 Windows 8 和.NET Framework 4.5 之前的类。

但是，托管的 XAML Windows 应用商店应用程序现在进行大量使用依赖句柄。 具体而言，CLR 使用它们来帮助管理托管的对象和非托管的 Windows 运行时对象之间的引用循环。 这意味着它是比更重要现在前所未有的内存探查器，以了解这些依赖句柄，以便它们可以可视化，其余部分的堆关系图中的边缘。 应使用 Profiler DLL [RootReferences2](icorprofilercallback2-rootreferences2-method.md)， [ObjectReferences](icorprofilercallback-objectreferences-method.md)，并[ConditionalWeakTableElementReferences](icorprofilercallback5-conditionalweaktableelementreferences-method.md)一起以形成一个完整的堆关系图视图.

## <a name="conclusion"></a>结束语

就可以使用 CLR 分析 API 来分析 Windows 应用商店应用程序内运行的托管的代码。 事实上，可以执行你正在开发的现有探查器并进行一些特定的更改，以便它可以针对 Windows 应用商店应用程序。 Profiler UI 应使用新的 Api 来激活 Windows 应用商店应用程序在调试模式下。 请确保你 Profiler DLL 使用适用于 Windows 应用商店应用程序的这些 Api。 与 Windows 应用商店应用 API 限制记住和意识的现有 Windows 应用商店应用程序的受限权限，则应编写 Profiler DLL 和 Profiler UI 之间的通信机制。 Profiler DLL 必须了解 CLR 如何处理 Winmd，以及垃圾回收器的行为与托管线程不同。

## <a name="resources"></a>资源

**公共语言运行时**

- [分析 （非托管的 API 参考）](index.md)

- [元数据 （非托管 API 参考）](../metadata/index.md)

**与 Windows 运行时的 CLR 的交互**

- [.NET Framework 对 Windows 应用商店应用和 Windows 运行时的支持情况](../../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)

**Windows 应用商店应用**

- [文件访问和权限 （Windows 运行时应用](https://docs.microsoft.com/previous-versions/windows/apps/hh967755%28v=win.10%29)

- [获取开发人员许可证](https://docs.microsoft.com/previous-versions/windows/apps/hh974578%28v=win.10%29)

- [IPackageDebugSettings 接口](/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ipackagedebugsettings)
