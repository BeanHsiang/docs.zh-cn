---
title: 在 ML.NET 中使用排列功能的重要性来确定模型功能的重要性
description: 在 ML.NET 中使用排列功能的重要性来理解模型功能的重要性
ms.date: 03/05/2019
ms.custom: mvc,how-to
ms.openlocfilehash: b0457bc07168579403e5a00383864c5612e1d17f
ms.sourcegitcommit: 58fc0e6564a37fa1b9b1b140a637e864c4cf696e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2019
ms.locfileid: "57675545"
---
# <a name="determine-the-feature-importance-of-models-with-permutation-feature-importance-in-mlnet"></a>在 ML.NET 中使用排列功能的重要性来确定模型功能的重要性

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET 简介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)。

此操作说明和相关示例目前使用的是 ML.NET 版本 0.10。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

在创建机器学习模型时，仅仅进行预测通常是不够的。 机器学习开发人员、决策者以及受模型影响的人员通常需要了解机器学习模型如何做出决策，以及哪些特性有助于提高其性能。 `Permutation Feature Importance` (PFI) 是一项在 Microsoft 内部使用的模型可解释性工具，帮助机器学习开发人员更好地理解模型功能的重要性。

PFI 是一种在定型的机器学习模型中确定全局功能重要性的技术，由 Breiman 在[“随机林”论文的第 10 节](https://www.stat.berkeley.edu/~breiman/randomforest2001.pdf)中提出。 PFI 通过以下问题来衡量功能的重要性，“如果一项功能的值被设置为随机值，会对模型有什么影响？”。 PFI 方法的优点是它与模型无关，它适用于任何可进行评估的模型，并且可以使用任何数据集（而不仅仅是定型集）来计算功能的重要性。 可以按此方法使用 PFI 来生成如下图所示的功能重要性：

![排列功能重要性关系图](./media/determine-global-feature-importance-in-model/pfi-graph.png)

```csharp
// Compute the feature importance using PFI
var permutationMetrics = mlContext.Regression.PermutationFeatureImportance(model.LastTransformer, model.Transform(data), "MedianHomeValue");

// Get the feature names from the training set
var featureNames =
    data.Schema.AsEnumerable()
    .Select(column => column.Name) // Get the column names
    .Where(name => name != "MedianHomeValue") // Drop the Label
    .ToArray();

// Write out the feature names and their importance to the model's Mean R-squared value
for (int i = 0; i < featureNames.Length;i++)
{
    Console.WriteLine($"{featureNames[i]}\t{permutationMetrics[i].RSquared.Mean:G4}");
}
```

有关使用 PFI 来分析模型功能重要性的示例，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/samples/Microsoft.ML.Samples/Dynamic/PermutationFeatureImportance)。

/* 其实并不是完全随机的，而是在一组示例中排列。
