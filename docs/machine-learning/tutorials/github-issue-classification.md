---
title: 在 GitHub 问题多类分类方案中使用 ML.NET
description: 了解如何在多类分类方案中使用 ML.NET 对 GitHub 问题进行分类，将其分配到给定区域。
ms.date: 03/12/2019
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 1031ac8a592c968e22745de4be966392733597dd
ms.sourcegitcommit: 16aefeb2d265e69c0d80967580365fabf0c5d39a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2019
ms.locfileid: "57846306"
---
# <a name="tutorial-use-mlnet-in-a-multiclass-classification-scenario-to-classify-github-issues"></a>教程：在多类分类场景中使用 ML.NET 对 GitHub 问题进行分类

此示例教程通过在 Visual Studio 2017 中使用 C# 的 .NET Core 控制台应用程序，演示如何使用 ML.NET 创建 GitHub 问题分类器。

在本教程中，你将了解：
> [!div class="checklist"]
> * 了解问题
> * 选择适当的机器学习算法
> * 准备数据
> * 转换数据
> * 定型模型
> * 评估模型
> * 使用训练的模型预测
> * 使用加载模型部署和预测

> [!NOTE]
> 本主题引用 ML.NET（目前处于预览状态），且材料可能会更改。 有关详细信息，请访问 [ML.NET 简介](https://www.microsoft.com/net/learn/apps/machine-learning-and-ai/ml-dotnet)。

此教程和相关示例目前使用的是 ML.NET 版本 0.11。 有关详细信息，请参阅 [dotnet/machinelearning GitHub 存储库](https://github.com/dotnet/machinelearning/tree/master/docs/release-notes)上的发行说明。

## <a name="github-issue-sample-overview"></a>GitHub 问题示例概述

该示例是使用 ML.NET 来定型模型的控制台应用，该模型对 GitHub 问题的 Area 标签进行分类和预测。 它还使用第二个数据集对模型进行评估，以进行质量分析。 问题数据集来自 dotnet/corefx GitHub 存储库。

可以在 [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/GitHubIssueClassification) 存储库中找到本教程的源代码。

## <a name="prerequisites"></a>系统必备

* 安装了“.NET Core 跨平台开发”工作负载的 [Visual Studio 2017 15.6 或更高版本](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

* [Github 问题制表符分隔文件 (issues_train.tsv)](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv)。
* [Github 问题测试制表符分隔文件 (issues_test.tsv)](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv)。

## <a name="machine-learning-workflow"></a>机器学习工作流

本教程后面介绍了机器学习工作流，使该过程能够有序地进行。

工作流阶段如下所示：

1. **了解问题**
2. **准备数据**
   * **加载数据**
   * **提取功能（转换数据）**
3. **生成并定型** 
   * **定型模型**
   * **评估模型**
4. **部署模型**
   * **使用模型来预测**

### <a name="understand-the-problem"></a>了解问题

首先需要了解问题，因此可以将其分解为能够支持构建和定型模型的几个部分。 通过分解问题，可以预测和评估结果。

本教程旨在探讨传入的 GitHub 问题属于哪个区域，目的是对其进行正确标记，从而确定优先级和进行计划安排。

可将问题划分为以下部分：

* 问题标题文本
* 问题说明文本
* 模型定型数据的区域值
* 一个可评估的预测区域值，评估后可在实际操作中使用该值

然后，需要确定区域，并借助此操作选择机器学习任务。

## <a name="select-the-appropriate-machine-learning-algorithm"></a>选择适当的机器学习算法

通过此问题，你将了解以下情况：

定型数据：

可以在几个区域（区域）中标记 GitHub 问题，如以下示例所示：

* area-System.Numerics
* area-System.Xml
* area-Infrastructure
* area-System.Linq
* area-System.IO

预测新 GitHub 问题的“区域”，如下例所示：

* Contract.Assert vs Debug.Assert
* Make fields readonly in System.Xml

分类机器学习算法最适合此方案。

### <a name="about-the-classification-learning-algorithm"></a>有关分类学习算法

分类是一项机器学习算法，它使用数据来确定某个项或数据行的类别、类型或类。 例如，可以使用分类：

* 识别情绪为正面还是负面。
* 将电子邮件分类为垃圾邮件或正常邮件。
* 确定患者的实验室样本是否癌变。
* 根据客户对销售活动的反应倾向对客户进行分类。

分类学习算法用例通常为以下类型之一：

* 二元：A 或 B。
* 多类：可以通过使用单个模型来预测多个类别。

对于此类问题，请使用多类分类学习算法，因为你的问题类别预测可能是多个类别（多类）而不是仅两个（二元）中的一个。

## <a name="create-a-console-application"></a>创建控制台应用程序

### <a name="create-a-project"></a>创建项目

1. 打开 Visual Studio 2017。 从菜单栏中选择“文件” > “新建” > “项目”。 在“新项目”对话框中，依次选择“Visual C#”和“.NET Core”节点。 然后，选择“控制台应用程序(.NET Core)”项目模板。 在“名称”文本框中，键入“GitHubIssueClassification”，然后选择“确定”按钮。

2. 在项目中创建一个名为“数据”的目录来保存数据集文件：

    在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新文件夹”。 键入“Data”，然后按 Enter。

3. 在项目中创建一个名为“模型”的目录来保存模型：

    在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新文件夹”。 键入“模型”，然后按 Enter。

4. 安装“Microsoft.ML NuGet 包”：

    在“解决方案资源管理器”中，右键单击项目，然后选择“管理 NuGet 包”。 将“nuget.org”选择为“包源”，选择“浏览”选项卡并搜索“Microsoft.ML”，在列表中选择该包，然后选择“安装”按钮。 选择“预览更改”对话框上的“确定”按钮，如果你同意所列包的许可条款，则选择“接受许可”对话框上的“我接受”按钮。

### <a name="prepare-your-data"></a>准备数据

1. 下载 [issues_train.tsv](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_train.tsv) 和 [issues_test.tsv](https://raw.githubusercontent.com/dotnet/samples/master/machine-learning/tutorials/GitHubIssueClassification/Data/issues_test.tsv) 数据集，并将它们保存到先前创建的“数据”文件夹。 第一个数据集定型机器学习模型，第二个数据集可用来评估模型的准确度。

2. 在“解决方案资源管理器”中，右键单击每个 \*.tsv 文件，然后选择“属性”。 在“高级”下，将“复制到输出目录”的值更改为“如果较新则复制”。

### <a name="create-classes-and-define-paths"></a>创建类和定义路径

将以下附加的 `using` 语句添加到“Program.cs”文件顶部：

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddUsings)]

创建 3 个全局字段，来保存最近下载的文件路径以及 `MLContext`、`DataView`、`PredictionEngine` 和 `TextLoader` 的全局变量：

* `_trainDataPath` 具有用于定型模型的数据集路径。
* `_testDataPath` 具有用于评估模型的数据集路径。
* `_modelPath` 具有在其中保存定型模型的路径。
* `_mlContext` 是用于提供处理上下文的 <xref:Microsoft.ML.MLContext>。
* `_trainingDataView` 是用于处理定型数据集的 <xref:Microsoft.Data.DataView.IDataView>。
* `_predEngine` 是用于单个预测的 <xref:Microsoft.ML.PredictionEngine%602>。
* `_reader` 是用于加载和转换数据集的 <xref:Microsoft.ML.Data.TextLoader>。

将以下代码添加到 `Main` 方法正上方的行中以指定这些路径和其他变量：

[!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DeclareGlobalVariables)]

为输入数据和预测创建一些类。 向项目添加一个新类：

1. 在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “新项”。

1. 在“添加新项”对话框中，选择“类”并将“名称”字段更改为“GitHubIssueData.cs”。 然后，选择“添加”按钮。

    “GitHubIssueData.cs”文件随即在代码编辑器中打开。 将下面的 `using` 语句添加到 GitHubIssueData.cs 的顶部：

[!code-csharp[AddUsings](../../../samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#AddUsings)]

删除现有类定义并向“GitHubIssueData.cs”文件添加以下代码，其中有两个类 `GitHubIssue` 和 `IssuePrediction`：

[!code-csharp[DeclareGlobalVariables](../../../samples/machine-learning/tutorials/GitHubIssueClassification/GitHubIssueData.cs#DeclareTypes)]

`GitHubIssue` 是输入数据集类，具有以下 <xref:System.String> 字段：

* `ID` 包含 GitHub 问题 ID 的值
* `Area` 包含 `Area` 标签的值
* `Title` 包含 GitHub 问题标题
* `Description` 包含 GitHub 问题说明

`IssuePrediction` 是在定型模型后用于预测的类。 它有一个 `string` (`Area`) 和一个 `PredictedLabel` `ColumnName` 属性。 `Label` 用于创建和定型模型，并且与第二个数据集结合使用来评估模型。 `PredictedLabel` 在预测和评估过程中使用。 对于计算，将使用带定型数据的输入、预测值和模型。

使用 ML.NET 构建模型时，首先要创建一个 <xref:Microsoft.ML.MLContext>。 `MLContext` 在概念上相当于在实体框架中使用 `DbContext`。 该环境为 ML 作业提供一个上下文，可以用于异常情况跟踪和日志记录。

### <a name="initialize-variables-in-main"></a>在 Main 中初始化变量

使用具有随机种子 (`seed: 0`) 的新实例 `MLContext` 初始化 `_mlContext` 全局变量，以获得跨多个定型的可重复/确定性结果。  用下面 `Main` 方法中的代码替换 `Console.WriteLine("Hello World!")` 行：

[!code-csharp[CreateMLContext](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateMLContext)]

## <a name="load-the-data"></a>加载数据

接下来，初始化 `_trainingDataView` <xref:Microsoft.Data.DataView.IDataView> 全局变量并使用 `_trainDataPath` 参数加载数据。

 作为 [`Transforms`](../basic-concepts-model-training-in-mldotnet.md#transformer) 的输入和输出，`DataView` 是基本的数据管道类型，与 `LINQ` 中的 `IEnumerable` 类似。

在 ML.NET 中，数据类似于 `SQL view`。 它是异源数据，会延迟计算并进行架构化。 该对象是管道的第一部分，并加载数据。 在本教程中，它会加载一个包含问题标题、说明和相应区域 GitHub 标签的数据集。 `DataView` 用于创建和定型模型。

由于先前创建的 `GitHubIssue` 数据模型类型与数据集架构相匹配，因此可以将初始化、映射和数据集加载合并到一行代码中。

使用 [LoadFromTextFile 方法](xref:Microsoft.ML.TextLoaderSaverCatalog.LoadFromTextFile%60%601%28Microsoft.ML.DataOperationsCatalog,System.String,System.Char,System.Boolean,System.Boolean,System.Boolean,System.Boolean%29)的 `MLContext.Data.LoadFromTextFile` 包装器加载数据。 它返回 <xref:Microsoft.Data.DataView.IDataView>，此接口通过 `GitHubIssue` 数据模型类型推断数据集架构，并使用数据集标头。 

之前在创建 `GitHubIssue` 类时定义了数据模式。 对于架构：

* 第一列 `ID`（GitHub 问题 ID）
* 第二列 `Area`（定型预测）
* 第三列 `Title`（GitHub 问题标题）是用于预测 `Area` 的第一个[特征](../resources/glossary.md##feature)
* 第四列 `Description` 是用于预测 `Area` 的第二个特征

要初始化并加载 `_trainingDataView` 全局变量以将其用于管道，请在 `mlContext` 初始化后添加以下代码：

[!code-csharp[LoadTrainData](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTrainData)]

将以下代码作为下一行代码添加到 `Main` 方法中：

[!code-csharp[CallProcessData](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallProcessData)]

`ProcessData` 方法执行以下任务：

* 提取并转换数据。
* 返回处理管道。

使用下面的代码紧随 `Main` 方法后创建 `ProcessData` 方法：

```csharp
public static IEstimator<ITransformer> ProcessData()
{

}
```

## <a name="extract-features-and-transform-the-data"></a>提取功能和转换数据

预处理和清除数据任务至关重要，需要首先执行才能将数据集有效地用于机器学习。 原始数据通常嘈杂不可靠，并且可能缺少值。 在没有这些建模任务的情况下使用数据会产生误导性结果。

ML.NET 的转换管道撰写一组自定义 `transforms` 集，要在定型或测试数据之前将其应用到数据。 转换的主要目的是为了[特征化](../resources/glossary.md#feature-engineering)数据。 机器学习算法理解[特征化](../resources/glossary.md#feature)数据，因此下一步是将文本数据转换为 ML 算法识别的格式。 该格式是[数值向量](../resources/glossary.md#numerical-feature-vector)。

在后续步骤中，按 `GitHubIssue` 类中定义的名称引用列。

定型和评估模型时，默认情况下，将“标签”列中的值视为要预测的正确值。 由于要预测 `GitHubIssue` 的区域 GitHub 标签，所以将 `Area` 列复制到“标签”列。 为此，请使用 `MLContext.Transforms.Conversion.MapValueToKey`，它是 <xref:Microsoft.ML.ConversionsExtensionsCatalog.MapValueToKey%2A> 转换类的包装器。  `MapValueToKey` 返回实际上是管道的 <xref:Microsoft.ML.Data.EstimatorChain%601>。 命名此 `pipeline`，因为你将把定型程序附加到 `EstimatorChain`。 添加下一个代码行：

[!code-csharp[MapValueToKey](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#MapValueToKey)]

 特征化将不同的数字键值分配给每列的不同值，供机器学习算法使用。 接下来，调用 `mlContext.Transforms.Text.FeaturizeText`，它将文本（`Title` 和 `Description`）列特征化为每个名为 `TitleFeaturized` 和 `DescriptionFeaturized` 的值的数字向量。 使用以下代码将两列的特征化附加到管道：

[!code-csharp[FeaturizeText](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#FeaturizeText)]

>[!WARNING]
> ML.NET 版本 0.10 已更改转换参数的顺序。 这在你构建之前不会错误输出。 使用用于转换的参数名称，如前面的代码片段中所示。

数据准备最后一步使用 `Concatenate` 转换类将所有功能列合并到“功能”列。 默认情况下，学习算法仅处理“特征”列的特征。 使用以下代码将此转换附加到管道：

[!code-csharp[Concatenate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Concatenate)]

 接下来，附加一个 <xref:Microsoft.ML.Data.EstimatorChain%601.AppendCacheCheckpoint%2A> 来缓存数据视图，以便在使用缓存多次循环访问数据时获得更好的性能，如下面的代码所示：

[!code-csharp[AppendCache](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AppendCache)]

> [!WARNING]
> 对小/中型数据集使用 AppendCacheCheckpoint 可以降低训练时间。 在处理大型数据集时不使用它（删除 .AppendCacheCheckpoint()）。

在 `ProcessData` 方法的末尾返回管道。

[!code-csharp[ReturnPipeline](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnPipeline)]

此步骤处理预处理/特征化。 使用 ML.NET 中可用的其他组件可以在使用模型时生成更佳结果。

## <a name="build-and-train-the-model"></a>生成和定型模型

将以下调用添加到 `BuildAndTrainModel` 方法作为 `Main` 方法的下一行代码：

[!code-csharp[CallBuildAndTrainModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallBuildAndTrainModel)]

`BuildAndTrainModel` 方法执行以下任务：

* 创建定型算法类。
* 定型模型。
* 根据定型数据预测区域。
* 将模型保存到 `.zip` 文件。
* 返回模型。

使用下面的代码紧随 `Main` 方法后创建 `BuildAndTrainModel` 方法：

```csharp
public static IEstimator<ITransformer> BuildAndTrainModel(IDataView trainingDataView, IEstimator<ITransformer> pipeline)
{

}
```

请注意，两个参数传递到 BuildAndTrainModel 方法；用于定性数据集 (`trainingDataView`) 的 `IDataView`，用于 ProcessData (`pipeline`) 中创建的处理管道的 <xref:Microsoft.ML.Data.EstimatorChain%601>。

 将以下代码添加为 `BuildAndTrainModel` 方法的首行：

### <a name="choose-a-learning-algorithm"></a>选择学习算法

要添加学习算法，请调用返回 <xref:Microsoft.ML.Trainers.SdcaMultiClassTrainer> 对象的 `mlContext.MulticlassClassification.Trainers.StochasticDualCoordinateAscent` 包装器方法。  `SdcaMultiClassTrainer` 追加到 `pipeline` 并接受特征化的 `Title` 和 `Description` (`Features`) 以及 `Label` 输入参数，以便从历史数据中学习。 还需要将标签映射到值以返回其原始可读状态。 使用以下代码执行这两个操作：

[!code-csharp[AddTrainer](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTrainer)]

### <a name="train-the-model"></a>定型模型

根据已加载和转换的数据集定型模型 <xref:Microsoft.ML.Data.TransformerChain%601>。 一旦定义了估算器，将使用 <xref:Microsoft.ML.Data.EstimatorChain%601.Fit%2A> 定型模型，同时提供已经加载的定型数据。 此方法会返回要用于预测的模型。 `trainingPipeline.Fit()` 定型管道，并返回基于传入的 `DataView` 的 `Transformer`。 在 `.Fit()` 方法运行之前不会执行此试验。

将以下代码添加到 `BuildAndTrainModel` 方法中：

[!code-csharp[TrainModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#TrainModel)]

虽然 `model` 是对多行数据进行操作的 `transformer`，但常见的生产场景是需要对单个示例进行预测。 <xref:Microsoft.ML.PredictionEngine%602> 是从 `CreatePredictionEngine` 方法返回的包装器。 让我们添加以下代码来创建 `PredictionEngine`，作为 `BuildAndTrainModel` 方法中的下一行：

[!code-csharp[CreatePredictionEngine1](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine1)]

### <a name="predict-with-the-trained-model"></a>使用训练的模型预测

通过创建一个 `GitHubIssue` 实例，在 `Predict` 方法中添加一个 GitHub 问题来测试定型模型的预测：

[!code-csharp[CreateTestIssue1](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreateTestIssue1)]

可以使用它来预测问题数据的单个实例的 `Area` 标签。 要获得预测，请对数据使用 <xref:Microsoft.ML.PredictionEngine%602.Predict%2A>。 输入数据是一个字符串，且模型包含特征化。 管道在定型和预测期间同步。 不必专门为预测编写预处理/特征化代码，并且相同 API 负责批处理和一次性预测。

[!code-csharp[Predict](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Predict)]

### <a name="using-the-model-prediction-results"></a>使用模型：预测结果

显示 `GitHubIssue` 和相应的 `Area` 标签预测以便共享结果，并采取相应措施。  使用以下 <xref:System.Console.WriteLine?displayProperty=nameWithType> 代码创建结果显示：

[!code-csharp[OutputPrediction](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#OutputPrediction)]

### <a name="return-the-model-trained-to-use-for-evaluation"></a>返回定型模型以用于评估

在 `BuildAndTrainModel` 方法末尾返回模型。

[!code-csharp[ReturnModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#ReturnModel)]

## <a name="evaluate-the-model"></a>评估模型

你已经创建和定型模型，现在需要使用不同的数据集对其进行评估以保证质量和进行验证。 在 `Evaluate` 方法中，将传入在 `BuildAndTrainModel` 中创建的模型以进行评估。 紧随 `BuildAndTrainModel` 后创建 `Evaluate` 方法，如以下代码所示：

```csharp
public static void Evaluate()
{

}
```

`Evaluate` 方法执行以下任务：

* 加载测试数据集。
* 创建多类评估程序。
* 评估模型并创建指标。
* 显示指标。

使用下面的代码，在 `BuildAndTrainModel` 方法调用的正下方，从 `Main` 方法中添加对新方法的调用：

[!code-csharp[CallEvaluate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallEvaluate)]

如同之前使用定型数据集执行的操作，可以将初始化、映射和测试数据集加载合并到一行代码中。 可以将此数据集作为质量检查来评估模型。 将以下代码添加到 `Evaluate` 方法中：

[!code-csharp[LoadTestDataset](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadTestDataset)]

`MulticlassClassificationContext.Evaluate` 是 <xref:Microsoft.ML.MulticlassClassificationCatalog.Evaluate%2A> 方法的包装器，它使用指定数据集计算模型的质量指标。 它返回 <xref:Microsoft.ML.Data.MultiClassClassifierMetrics> 对象，其中包含由多类分类计算器计算出的总体指标。
要显示指标来确定模型质量，需要先获取这些指标。
请注意使用机器学习 `_trainedModel` 全局变量（转换器）的 `Transform` 方法来输入要素和返回预测。 将以下代码作为下一行添加到 `Evaluate` 方法中：

[!code-csharp[Evaluate](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#Evaluate)]

针对多类分类评估以下指标：

* 微观准确性 - 每个“样本-类”对准确性指标的贡献度相同。  通常会希望微观准确性尽可能接近 1。

* 宏观准确性 - 每个类对准确性指标的贡献度相同。 占比较小的类与占比较大的类拥有同等的权重。 通常会希望宏准确性尽可能接近 1。

* 对数损失 - 请参阅[对数损失](../resources/glossary.md#log-loss)。 通常会希望对数损失尽可能接近 0。

* 对数损失减小 - 取值范围为 [-inf，100]，其中 100 表示非常精准的预测结果，0 表示准确性一般的预测。 通常会希望数损失减少尽可能接近零。

### <a name="displaying-the-metrics-for-model-validation"></a>显示用于模型验证的指标

使用下面的代码显示指标、共享结果，然后处理它们：

[!code-csharp[DisplayMetrics](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayMetrics)]

### <a name="save-the-trained-and-evaluated-model"></a>保存经过训练和评估的模型

此时，你具有可以集成到任何现有或新 .NET 应用程序的 <xref:Microsoft.ML.Data.TransformerChain%601> 类型模型。 要将已定型的模型保存为 .zip 文件，请添加以下代码作为 `BuildAndTrainModel` 中的下一行来调用 `SaveModelAsFile` 方法：

[!code-csharp[CallSaveModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallSaveModel)]

## <a name="save-the-model-as-a-zip-file"></a>将模型保存为 .zip 文件

使用下面的代码紧随 `Evaluate` 方法后创建 `SaveModelAsFile` 方法：

```csharp
private static void SaveModelAsFile(MLContext mlContext, ITransformer model)
{

}
```

`SaveModelAsFile` 方法执行以下任务：

* 将模型保存为 .zip 文件。

接下来，创建一个方法来保存模型，以便它可以在其他应用程序中重用和使用。 `ITransformer` 有一个在 `_modelPath` 全局字段中采用的 <xref:Microsoft.ML.Data.TransformerChain%601.SaveTo(Microsoft.ML.IHostEnvironment,System.IO.Stream)> 方法和一个 <xref:System.IO.Stream> 方法。 要将模型保存为 zip 文件，需在调用 `SaveTo` 方法之前立即创建 `FileStream`。 将以下代码作为下一行添加到 `SaveModelAsFile` 方法中：

[!code-csharp[SaveModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#SaveModel)]

还可以使用以下代码通过使用 `_modelPath` 编写控制台消息来显示文件的写入位置：

```csharp
Console.WriteLine("The model is saved to {0}", _modelPath);
```

## <a name="deploy-and-predict-with-a-loaded-model"></a>使用加载模型部署和预测

使用下面的代码，在 `Evaluate` 方法调用的正下方，从 `Main` 方法中添加对新方法的调用：

[!code-csharp[CallPredictIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CallPredictIssue)]

使用以下代码恰好在 `Evaluate` 方法的后面（恰在 `SaveModelAsFile` 方法之前）创建 `PredictIssue` 方法：

```csharp
private static void PredictIssue()
{

}
```

`PredictIssue` 方法执行以下任务：

* 创建测试数据的单个问题。
* 根据测试数据预测区域。
* 结合测试数据和预测进行报告。
* 显示预测结果。

首先，使用以下代码加载先前保存的模型：

[!code-csharp[LoadModel](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#LoadModel)]

通过创建一个 `GitHubIssue` 实例，在 `Predict` 方法中添加一个 GitHub 问题来测试定型模型的预测：

[!code-csharp[AddTestIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#AddTestIssue)]

[!code-csharp[CreatePredictionEngine](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#CreatePredictionEngine)]
  
现在已有一个模型，可以使用它来预测 GitHub 问题数据的单个实例的区域 GitHub 标签。 要获得预测，请对数据使用 <xref:Microsoft.ML.PredictionEngine%602.Predict%2A>。 输入数据是一个字符串，且模型包含特征化。 管道在定型和预测期间同步。 不必专门为预测编写预处理/特征化代码，并且相同 API 负责批处理和一次性预测。 在用于预测的 `PredictIssue` 方法中添加以下代码：

[!code-csharp[PredictIssue](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#PredictIssue)]

### <a name="using-the-loaded-model-for-prediction"></a>使用加载后的模型进行预测

显示 `Area` 以便对问题进行分类并对其进行相应操作。 使用以下 <xref:System.Console.WriteLine?displayProperty=nameWithType> 代码创建结果显示：

[!code-csharp[DisplayResults](../../../samples/machine-learning/tutorials/GitHubIssueClassification/Program.cs#DisplayResults)]

## <a name="results"></a>结果

结果应如下所示。 管道处理期间，会显示消息。 你可能会看到警告或处理消息。 为简便起见，已从以下结果中删除这些消息。

```console
=============== Single Prediction just-trained-model - Result: area-System.Net ===============
The model is saved to C:\Users\johalex\dotnet-samples\samples\machine-learning\tutorials\GitHubIssueClassification\bin\Debug\netcoreapp2.0\..\..\..\Models\model.zip
*************************************************************************************************************
*       Metrics for Multi-class Classification model - Test Data
*------------------------------------------------------------------------------------------------------------
*       MicroAccuracy:    0.74
*       MacroAccuracy:    0.687
*       LogLoss:          .932
*       LogLossReduction: 63.852
*************************************************************************************************************
=============== Single Prediction - Result: area-System.Data ===============
```

祝贺你！ 现在，已成功生成用于为 GitHub 问题分类和预测区域标签的机器学习模型。 可以在 [dotnet/samples](https://github.com/dotnet/samples/tree/master/machine-learning/tutorials/GitHubIssueClassification) 存储库中找到本教程的源代码。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：
> [!div class="checklist"]
> * 了解问题
> * 选择适当的机器学习算法
> * 准备数据
> * 转换数据
> * 定型模型
> * 评估模型
> * 使用训练的模型预测
> * 使用加载模型部署和预测

进入下一教程了解详细信息
> [!div class="nextstepaction"]
> [出租车费预测器](taxi-fare.md)
