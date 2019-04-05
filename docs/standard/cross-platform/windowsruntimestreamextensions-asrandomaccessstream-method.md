---
title: WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream) 方法
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
api_name:
- System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream
api_location:
- System.Runtime.WindowsRuntime.dll
ms.assetid: dcc72283-caed-49ee-b45d-ccaf94e97129
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d5dd2829a9a00f869af3d7f370f99361979b8106
ms.sourcegitcommit: 01ea420eaa4bf76d5fc47673294c8881379b3369
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2019
ms.locfileid: "55758789"
---
# <a name="windowsruntimestreamextensionsasrandomaccessstreamsystemiostream-method"></a>WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream) 方法

[在 .NET Framework 4.5.1 和更高版本中受支持]

将指定的流转换为随机访问流。

**命名空间：**<xref:System.IO?displayProperty=nameWithType>
**程序集：** System.Runtime.WindowsRuntime （在 system.runtime.windowsruntime.dll 中）

## <a name="syntax"></a>语法

```csharp
[CLSCompliantAttribute(false)]
public static IRandomAccessStream AsRandomAccessStream(Stream stream)
```

```vb
'Declaration
<ExtensionAttribute> _
<CLSCompliantAttribute(False)> _
Public Shared Function AsRandomAccessStream ( _
        stream As Stream) As IRandomAccessStream
```

## <a name="parameters"></a>参数

`stream`

类型：<xref:System.IO.Stream?displayProperty=nameWithType>  
要转换的流。

## <a name="return-value"></a>返回值

类型：<xref:Windows.Storage.Streams.RandomAccessStream>  
一个[!INCLUDE[wrt](../../../includes/wrt-md.md)]随机访问流，表示已转换的流。

## <a name="exceptions"></a>Exceptions

|例外|条件|
|---------------|---------------|
|<xref:System.NotSupportedException>|要转换的流不支持查找。|

## <a name="remarks"></a>备注

此扩展方法仅在开发 Windows 应用商店应用时可用。 利用此方法，可以在 Windows 应用商店应用中轻松使用流。 要转换的 .NET Framework 流必须支持查找。 有关更多信息，请参见 <xref:System.IO.Stream.Seek%2A?displayProperty=nameWithType> 方法。

> [!IMPORTANT]
> 此 API 在 .NET Framework 4.5.1 和更高版本中受支持，但在 4.5 版中不受支持。

## <a name="version-information"></a>版本信息

**适用于 Windows 应用商店应用程序的.NET**

支持版本：Windows 8.1

## <a name="see-also"></a>请参阅

- [如何：在 .NET Framework 流和 Windows 运行时流之间进行转换](../io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)
