---
title: 争用 ETW 事件-.NET
ms.date: 03/30/2017
helpviewer_keywords:
- contention events [.NET Framework]
- ETW, contention events (CLR)
ms.assetid: 6933e753-2f2a-425b-ae84-42138c957d76
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 95f56a6c8b51c58ed36d5d0de428bf57b728009c
ms.sourcegitcommit: 5dcfeb59179e81071f54840d4902cbe00b184294
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2019
ms.locfileid: "54857640"
---
# <a name="contention-etw-events"></a>争用 ETW 事件

只要运行时使用的 <xref:System.Threading.Monitor?displayProperty=nameWithType> 锁或本机锁出现争用情况，就会引发争用事件。 一个线程等待的锁被另一线程占有时将发生争用。

下表显示了引发争用事件的关键字以及事件的级别。 有关详细信息，请参阅[CLR ETW 关键字和级别](clr-etw-keywords-and-levels.md)。

|引发事件的关键字|级别|
|-----------------------------------|-----------|
|`ContentionKeyword` (0x4000)|信息性 (4)|

下表显示了事件信息：

|事件|事件 ID|在发生以下情况时引发|
|-----------|--------------|-----------------|
|`ContentionStart_V1`|81|争用开始。 此事件不包括线程等待获取锁之前的旋转时间；仅在线程等待获取锁时引发此事件。|
|`ContentionStop`|91|争用结束。|

下表显示了事件数据：

|字段名|数据类型|描述|
|----------------|---------------|-----------------|
|Flags|win:UInt8|0 表示托管；1 表示本机。|
|ClrInstanceID|win:UInt16|CLR 实例的唯一 ID。|

## <a name="see-also"></a>请参阅

- [CLR ETW 事件](clr-etw-events.md)
