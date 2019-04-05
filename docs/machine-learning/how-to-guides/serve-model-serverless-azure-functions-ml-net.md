---
title: 将 ML.NET 模型部署到 Azure Functions
description: 使用 Azure Functions 通过 Internet 提供 ML.NET 情绪分析机器学习模型进行预测
ms.date: 03/08/2019
ms.custom: mvc,how-to
ms.openlocfilehash: db29e37660665b02ab93a07b37418f0c4c20a608
ms.sourcegitcommit: 5d9f4b805787f890ca6e0dc7ea30a43018bc9cbb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2019
ms.locfileid: "57788635"
---
# <a name="how-to-use-mlnet-model-in-azure-functions"></a>操作说明：在 Azure Functions 中使用 ML.NET 模型

本操作说明介绍了如何在无服务器环境（如 Azure Functions）中通过 Internet 使用预生成的 ML.NET 机器学习模型进行各个预测。

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET 简介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)。

此操作说明和相关示例目前使用的是 ML.NET 版本 0.10。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

## <a name="prerequisites"></a>系统必备

- 安装了“.NET Core 跨平台开发”工作负载和“Azure 开发”的 [Visual Studio 2017 15.6 或更高版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 
- [Azure Functions 工具](/azure/azure-functions/functions-develop-vs#check-your-tools-version)
- Powershell
- 预先定型的模型。 
    - 根据 [ML.NET 情绪分析教程](../tutorials/sentiment-analysis.md)生成你自己的模型。
    - 下载此[预先定型的情绪分析机器学习模型](https://github.com/dotnet/samples/blob/master/machine-learning/models/sentimentanalysis/sentiment_model.zip)

## <a name="create-azure-functions-project"></a>创建 Azure Functions 项目

1. 打开 Visual Studio 2017。 从菜单栏中选择“文件” > “新建” > “项目”。 在“新项目”对话框中，依次选择“Visual C#”节点和“云”节点。 然后，选择“Azure Functions”项目模板。 在“名称”文本框中，键入“SentimentAnalysisFunctionsApp”，再选择“确定”按钮。
1. 在“新项目”对话框中，打开项目选项上方的下拉列表，并选择“Azure Functions v2 (.NET Core)”。 然后，依次选择“Http 触发器”项目和“确定”按钮。
1. 在项目中创建“MLModels”目录，用于保存模型：

    在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新文件夹”。 键入“MLModels”，再按 Enter。

1. 安装“Microsoft.ML NuGet 包”：

    在“解决方案资源管理器”中，右键单击项目，然后选择“管理 NuGet 包”。 将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Microsoft.ML”，在列表中选择该包，然后选择“安装”按钮。 选择“预览更改”对话框上的“确定”按钮，如果你同意所列包的许可条款，则选择“接受许可”对话框上的“我接受”按钮。

## <a name="add-pre-built-model-to-project"></a>将预生成的模型添加到项目

1. 将预生成的模型复制到 MLModels 文件夹。
1. 在“解决方案资源管理器”中，右键单击预生成的模型文件，并选择“属性”。 在“高级”下，将“复制到输出目录”的值更改为“如果较新则复制”。

## <a name="create-function-to-analyze-sentiment"></a>创建情绪分析函数

创建情绪预测类。 向项目添加一个新类：

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新项”。

1. 在“添加新项”对话框中，选择“Azure 函数”，并将“名称”字段更改为“AnalyzeSentiment.cs”。 然后，选择“添加”按钮。

1. 在“新 Azure 函数”对话框中，选择“Http 触发器”。 然后，选择“确定”按钮。

    此时，AnalyzeSentiment.cs 文件在代码编辑器中打开。 将下面的 `using` 语句添加到 GitHubIssueData.cs 的顶部：

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
using Microsoft.ML;
using Microsoft.ML.Core.Data;
using Microsoft.ML.Data;
using MLNETServerless.DataModels;
```

### <a name="create-data-models"></a>创建数据模型

需要为输入数据和预测创建一些类。 向项目添加一个新类：

1. 在项目中创建“DataModels”目录，用于保存数据模型：在“解决方案资源管理器”中，右键单击项目，并依次选择“添加”>“新文件夹”。 键入“DataModels”，再按 Enter。
2. 在“解决方案资源管理器”中，右键单击“DataModels”目录，再依次选择“添加”>“新项”。
3. 在“添加新项”对话框中，选择“类”并将“名称”字段更改为“SentimentData.cs”。 然后，选择“添加”按钮。 “SentimentData.cs”文件随即在代码编辑器中打开。 将以下 using 语句添加到 SentimentData.cs 顶部：

```csharp
using Microsoft.ML.Data;
```

删除现有类定义，并将以下代码添加到 SentimentData.cs 文件：

```csharp
public class SentimentData
{
    [LoadColumn(0)]
    public bool Label { get; set; }
    [LoadColumn(1)]
    public string Text { get; set; }
}
```

4. 在“解决方案资源管理器”中，右键单击“DataModels”目录，再依次选择“添加”>“新项”。
5. 在“添加新项”对话框中，选择“类”，并将“名称”字段更改为“SentimentPrediction.cs”。 然后，选择“添加”按钮。 此时，SentimentPrediction.cs 文件在代码编辑器中打开。 将以下 using 语句添加到 SentimentPrediction.cs 顶部：

```csharp
using Microsoft.ML.Data;
```

删除现有类定义，并将以下代码添加到 SentimentPrediction.cs 文件：

```csharp
public class SentimentPrediction
{
    [ColumnName("PredictedLabel")]
    public bool Prediction { get; set; }
}
```

### <a name="add-prediction-logic"></a>添加预测逻辑

将 AnalyzeSentiment 类中 Run 方法的现有实现替换为以下代码：

```csharp
    public static async Task<IActionResult> Run(
        [HttpTrigger(AuthorizationLevel.Function,"post", Route = null)] HttpRequest req,
        ILogger log)
    {
        log.LogInformation("C# HTTP trigger function processed a request.");

        //Create Context
        MLContext mlContext = new MLContext();

        //Load Model
        using (var fs = File.OpenRead("MLModels/sentiment_model.zip"))
        {
            model = mlContext.Model.Load(fs);
        }

        //Parse HTTP Request Body
        string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        SentimentData data = JsonConvert.DeserializeObject<SentimentData>(requestBody);

        //Create Prediction Engine
        PredictionEngine<SentimentData, SentimentPrediction> predictionEngine = model.CreatePredictionEngine<SentimentData, SentimentPrediction>(mlContext);

        //Make Prediction
        SentimentPrediction prediction = predictionEngine.Predict(data);

        //Convert prediction to string
        string isToxic = Convert.ToBoolean(prediction.Prediction) ? "Toxic" : "Not Toxic";

        //Return Prediction
        return (ActionResult)new OkObjectResult(isToxic);
    }
}
```

## <a name="test-locally"></a>本地测试

至此，已完成所有设置，是时候测试应用程序了：

1. 运行此应用程序
1. 打开 PowerShell，并在提示符中输入代码（其中，PORT 是应用程序运行所在的端口）。 端口通常是 7071。 

```powershell
Invoke-RestMethod "http://localhost:<PORT>/api/AnalyzeSentiment" -Method Post -Body (@{Text="This is a very rude movie"} | ConvertTo-Json) -ContentType "application/json"
```

如果成功，输出文本应如下所示：

```powershell
Toxic
```

祝贺你！ 你已成功使用 Azure Functions 通过 Internet 提供模型进行预测。

## <a name="next-steps"></a>后续步骤

- [部署到 Azure](/azure/azure-functions/functions-develop-vs#publish-to-azure)