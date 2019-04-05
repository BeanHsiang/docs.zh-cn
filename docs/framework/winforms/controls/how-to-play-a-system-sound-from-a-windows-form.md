---
title: 如何：从 Windows 窗体播放系统声音
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], playing for system events
- playing sounds [Windows Forms], Windows Forms
- system sounds [Windows Forms], playing from Windows Forms
- playing sounds [Windows Forms], system
- SoundPlayer class [Windows Forms], system sounds
- sounds [Windows Forms], playing
- examples [Windows Forms], sounds
ms.assetid: afb206ff-4824-4804-a8d4-185bf5ad8e7c
ms.openlocfilehash: b2ac6c4f2e3334a9b4c5ff4d2a6e31b6b9bf3673
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57711212"
---
# <a name="how-to-play-a-system-sound-from-a-windows-form"></a>如何：从 Windows 窗体播放系统声音
下面的代码示例在运行时播放 `Exclamation` 系统声音。 有关系统声音的详细信息，请参阅<xref:System.Media.SystemSounds>。  
  
## <a name="example"></a>示例  
  
```vb  
Public Sub PlayExclamation()  
    SystemSounds.Exclamation.Play()  
End Sub  
```  
  
```csharp  
public void playExclamation()  
{  
    SystemSounds.Exclamation.Play();  
}  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 <xref:System.Media?displayProperty=nameWithType> 命名空间的引用。  
  
## <a name="see-also"></a>请参阅
- <xref:System.Media.SoundPlayer>
- <xref:System.Media.SystemSounds>
- [如何：从 Windows 窗体中播放提示音](how-to-play-a-beep-from-a-windows-form.md)
- [如何：从 Windows 窗体播放声音](how-to-play-a-sound-from-a-windows-form.md)
