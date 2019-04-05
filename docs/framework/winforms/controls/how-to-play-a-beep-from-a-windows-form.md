---
title: 如何：从 Windows 窗体中播放提示音
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sounds [Windows Forms], beep
- Windows Forms, sounds
- sounds [Windows Forms], playing
- forms [Windows Forms], sounds
- examples [Windows Forms], sounds
ms.assetid: 7ea5cded-4888-4f35-8f28-5cab1a55c973
ms.openlocfilehash: d04bf4bd45aa6ba5dfe231d5f69c2b2a13765373
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57710428"
---
# <a name="how-to-play-a-beep-from-a-windows-form"></a>如何：从 Windows 窗体中播放提示音
本示例在运行时播放提示音。  
  
## <a name="example"></a>示例  
  
```vb  
Public Sub OnePing()  
    Beep()  
End Sub  
```  
  
```csharp  
public void onePing()  
{  
    SystemSounds.Beep.Play();  
}  
```  
  
> [!NOTE]
>  中播放的声音C#代码示例由<xref:System.Media.SystemSounds.Beep%2A>系统声音设置决定。 有关详细信息，请参阅 <xref:System.Media.SystemSounds>。  
  
## <a name="compiling-the-code"></a>编译代码  
 有关C#，此示例需要引用<xref:System.Media?displayProperty=nameWithType>命名空间。  
  
## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualBasic.Interaction.Beep%2A>
- <xref:System.Media.SoundPlayer>
- [如何：从 Windows 窗体播放系统声音](how-to-play-a-system-sound-from-a-windows-form.md)
- [如何：从 Windows 窗体播放声音](how-to-play-a-sound-from-a-windows-form.md)
