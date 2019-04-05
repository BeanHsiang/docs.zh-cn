---
title: 在应用中操作定型的机器学习模型 - ML.NET
description: 了解如何借助 ML.NET 在应用程序中使用定型和经过评估的机器学习模型
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: be6906c939b82d00067babaeebe809dae3de413a
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675129"
---
# <a name="operationalize-a-trained-machine-learning-model-in-apps---mlnet"></a>在应用中操作定型的机器学习模型 - ML.NET

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET 简介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)。

此操作说明和相关示例目前使用的是 ML.NET 版本 0.10。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明

当模型指标对你而言不错时，就到了“操作”模型的时候了。 可以在不同的环境中使用、保留和重用所生成的 `model` 对象，并在定型期间应用该对象“已学习”的相同步骤。

若要将模型保存到文件中，并重载它（可能在不同的上下文中），请使用以下示例：

```csharp
using (var stream = File.Create(modelPath))
{
    // Saving and loading happens to 'dynamic' models.
    mlContext.Model.Save(model, stream);
}

// Potentially, the lines below can be in a different process altogether.

// When you load the model, it's a transformer.
ITransformer loadedModel;
using (var stream = File.OpenRead(modelPath))
    loadedModel = mlContext.Model.Load(stream);
```
