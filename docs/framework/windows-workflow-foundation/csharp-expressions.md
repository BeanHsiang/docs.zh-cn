---
title: C# 表达式
ms.date: 03/30/2017
ms.assetid: 29110be7-f4e3-407e-8dbe-78102eb21115
ms.openlocfilehash: 2ffc380d9c65ec398084bfcbeadfe0fd2c3d6720
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57720574"
---
# <a name="c-expressions"></a>C# 表达式
从开始[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]，Windows Workflow Foundation (WF) 中支持 C# 表达式。 新的 C# 工作流项目中创建 Visual Studio 2012 面向[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]使用 C# 表达式和 Visual Basic 工作流项目使用 Visual Basic 表达式。 现有使用 Visual Basic 表达式的 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 工作流项目可以不受项目语言限制而迁移到 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]，并得到支持。 本主题概述了 [!INCLUDE[wf1](../../../includes/wf1-md.md)] 中的 C# 表达式。

## <a name="using-c-expressions-in-workflows"></a>在工作流中使用 C# 表达式

-   [在工作流设计器中使用 C# 表达式](csharp-expressions.md#WFDesigner)

    -   [向后兼容性](csharp-expressions.md#BackwardCompat)

-   [在代码工作流中使用 C# 表达式](csharp-expressions.md#CodeWorkflows)

-   [在 XAML 工作流中使用 C# 表达式](csharp-expressions.md#XamlWorkflows)

    -   [编译的 Xaml](csharp-expressions.md#CompiledXaml)

    -   [松散 Xaml](csharp-expressions.md#LooseXaml)

-   [在 XAMLX 工作流服务中使用 C# 表达式](csharp-expressions.md#WFServices)

### <a name="WFDesigner"></a> 在工作流设计器中使用 C# 表达式
 从开始[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]，Windows Workflow Foundation (WF) 中支持 C# 表达式。 C# 工作流项目中创建 Visual Studio 2012 面向[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]使用 C# 表达式，而 Visual Basic 工作流项目使用 Visual Basic 表达式。 若要指定所需的 C# 表达式，它在框中键入标有**输入 C# 表达式**。 该标签显示在属性窗口中（当在设计器中选中活动时），或显示在工作流设计器的活动上。 下例中，在 `WriteLine` 范围内，一个 `Sequence` 中包含了两个 `NoPersistScope` 活动。

 ![自动创建的序列活动](./media/autosurround2.png "AutoSurround2")

> [!NOTE]
>  C# 表达式仅在 Visual Studio 中支持和不支持在重新承载的工作流设计器中。 在重新承载设计器中支持的新 WF45 功能的详细信息，请参阅[重新承载工作流设计器中新 Workflow Foundation 4.5 功能的支持](wf-features-in-the-rehosted-workflow-designer.md)。

#### <a name="BackwardCompat"></a> 向后兼容性
 在现有已迁移到 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 的 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] C# 工作流项目中使用的 Visual Basic 表达式是得到支持的。 现有的 Visual Basic 表达式的文本时可以在工作流设计器中查看 Visual Basic 表达式，将替换**值在 XAML 中设置**，除非 Visual Basic 表达式是有效的 C# 语法。 如果 Visual Basic 表达式符合 C# 语法则予以显示。 若要将 Visual Basic 表达式更新为 C#，可在工作流设计器中编辑这些表达式，指定等效的 C# 表达式。 将 Visual Basic 表达式更新为 C# 不是必须的，但一旦在工作流设计器中进行更新，这些表达式即转换成 C# 并不可重新转换为 Visual Basic。

### <a name="CodeWorkflows"></a> 在代码工作流中使用 C# 表达式
 基于 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 代码的工作流支持 C# 表达式，但 C# 表达式须用 <xref:System.Activities.XamlIntegration.TextExpressionCompiler.Compile%2A?displayProperty=nameWithType> 进行编译，然后才能调用工作流。 工作流作者可以用 `CSharpValue` 表示表达式的右值，用 `CSharpReference` 表示表达式的左值。 在下例中，用一个 `Assign` 活动以及 `WriteLine` 活动中所包含的 `Sequence` 活动创建了一个工作流。 为 `CSharpReference` 的 `To` 参数指定了一个 `Assign`，用来表示表达式的左值。 为 `CSharpValue` 的 `Value` 参数和 `Assign` 的 `Text` 参数指定了一个 `WriteLine`，用于表示这两个表达式的右值。

```csharp
Variable<int> n = new Variable<int>
{
    Name = "n"
};

Activity wf = new Sequence
{
    Variables = { n },
    Activities =
    {
        new Assign<int>
        {
            To = new CSharpReference<int>("n"),
            Value = new CSharpValue<int>("new Random().Next(1, 101)")
        },
        new WriteLine
        {
            Text = new CSharpValue<string>("\"The number is \" + n")
        }
    }
};

CompileExpressions(wf);

WorkflowInvoker.Invoke(wf);
```

 工作流构造完毕后，通过调用 `CompileExpressions` 帮助器方法编译了 C# 表达式，随后调用工作流。 下面的示例为 `CompileExpressions` 方法。

```csharp
static void CompileExpressions(Activity activity)
{
    // activityName is the Namespace.Type of the activity that contains the
    // C# expressions.
    string activityName = activity.GetType().ToString();

    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name
    // to represent the new type that represents the compiled expressions.
    // Take everything after the last . for the type name.
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";
    // Take everything before the last . for the namespace.
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());

    // Create a TextExpressionCompilerSettings.
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings
    {
        Activity = activity,
        Language = "C#",
        ActivityName = activityType,
        ActivityNamespace = activityNamespace,
        RootNamespace = null,
        GenerateAsPartialClass = false,
        AlwaysGenerateSource = true,
        ForImplementation = false
    };

    // Compile the C# expression.
    TextExpressionCompilerResults results =
        new TextExpressionCompiler(settings).Compile();

    // Any compilation errors are contained in the CompilerMessages.
    if (results.HasErrors)
    {
        throw new Exception("Compilation failed.");
    }

    // Create an instance of the new compiled expression type.
    ICompiledExpressionRoot compiledExpressionRoot =
        Activator.CreateInstance(results.ResultType,
            new object[] { activity }) as ICompiledExpressionRoot;

    // Attach it to the activity.
    CompiledExpressionInvoker.SetCompiledExpressionRoot(
        activity, compiledExpressionRoot);
}
```

> [!NOTE]
>  如果C#表达式未编译，<xref:System.NotSupportedException>使用类似于以下的消息调用工作流时，将引发：`Expression Activity type 'CSharpValue`1 需要编译才能运行。  请确保已编译工作流。

 如果基于自定义代码的工作流使用 `DynamicActivity`，则需要对 `CompileExpressions` 方法作一些修改，如下列代码示例所示。

```csharp
static void CompileExpressions(DynamicActivity dynamicActivity)
{
    // activityName is the Namespace.Type of the activity that contains the
    // C# expressions. For Dynamic Activities this can be retrieved using the
    // name property , which must be in the form Namespace.Type.
    string activityName = dynamicActivity.Name;

    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name
    // to represent the new type that represents the compiled expressions.
    // Take everything after the last . for the type name.
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";
    // Take everything before the last . for the namespace.
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());

    // Create a TextExpressionCompilerSettings.
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings
    {
        Activity = dynamicActivity,
        Language = "C#",
        ActivityName = activityType,
        ActivityNamespace = activityNamespace,
        RootNamespace = null,
        GenerateAsPartialClass = false,
        AlwaysGenerateSource = true,
        ForImplementation = true
    };

    // Compile the C# expression.
    TextExpressionCompilerResults results =
        new TextExpressionCompiler(settings).Compile();

    // Any compilation errors are contained in the CompilerMessages.
    if (results.HasErrors)
    {
        throw new Exception("Compilation failed.");
    }

    // Create an instance of the new compiled expression type.
    ICompiledExpressionRoot compiledExpressionRoot =
        Activator.CreateInstance(results.ResultType,
            new object[] { dynamicActivity }) as ICompiledExpressionRoot;

    // Attach it to the activity.
    CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation(
        dynamicActivity, compiledExpressionRoot);
}
```

 在动态活动中编译 C# 表达式的 `CompileExpressions` 重载中有几处不同。

-   `CompileExpressions` 的参数是一个 `DynamicActivity`。

-   通过使用 `DynamicActivity.Name` 属性检索类型名称和命名空间。

-   将 `TextExpressionCompilerSettings.ForImplementation` 设置为 `true`。

-   调用 `CompiledExpressionInvoker.SetCompiledExpressionRootForImplementation` 而非 `CompiledExpressionInvoker.SetCompiledExpressionRoot`。

 有关使用在代码中使用表达式的详细信息，请参阅[编写工作流、 活动和表达式使用命令性代码](authoring-workflows-activities-and-expressions-using-imperative-code.md)。

### <a name="XamlWorkflows"></a> 在 XAML 工作流中使用 C# 表达式
 XAML 工作流支持 C# 表达式。 编译型 XAML 工作流被编译到类型中，而宽松型 XAML 工作流由运行时加载，并在工作流执行时编译到活动树中。

-   [编译的 Xaml](csharp-expressions.md#CompiledXaml)

-   [松散 Xaml](csharp-expressions.md#LooseXaml)

#### <a name="CompiledXaml"></a> 编译的 Xaml
 编译型 XAML 工作流支持 C# 表达式，此种工作流编译成类型，作为面向 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] 的 C# 工作流项目的组成部分。 已编译的 XAML 是在 Visual Studio 中，工作流创作的默认类型和 C# 工作流项目中创建 Visual Studio 面向[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]使用 C# 表达式。

#### <a name="LooseXaml"></a> 松散 Xaml
 宽松型 XAML 工作流支持 C# 表达式。 加载并调用宽松型 XAML 工作流的工作流宿主程序必须面向 [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]，而<xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 必须设为 `true`（默认值为 `false`）。 要将 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 设置为 `true`，请创建一个 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> 实例，创建时将其 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> 属性设为 `true`，并作为参数传递给 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=nameWithType>。 如果`CompileExpressions`未设置为`true`、<xref:System.NotSupportedException>将引发类似于以下消息：`Expression Activity type 'CSharpValue`1 需要编译才能运行。  请确保已编译工作流。

```csharp
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings
{
    CompileExpressions = true
};

DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;
```

 有关使用 XAML 工作流的详细信息，请参阅[序列化工作流和活动与 XAML](serializing-workflows-and-activities-to-and-from-xaml.md)。

### <a name="WFServices"></a> 在 XAMLX 工作流服务中使用 C# 表达式
 XAMLX 工作流服务支持 C# 表达式。 当工作流服务承载于 IIS 或 WAS 中时，无须执行任何额外步骤，但如果 XAML 工作流服务是自承载的，则 C# 表达式必须经过编译。 若要编译 C# 表达式在自承载的 XAMLX 工作流服务中，首先将 XAMLX 文件加载到`WorkflowService`，然后将传递`Body`的`WorkflowService`到`CompileExpressions`中前面所述方法[使用 C#代码工作流中的表达式](csharp-expressions.md#CodeWorkflows)部分。 下例加载一个 XAMLX 工作流服务，编译 C# 表达式，随后打开该工作流服务并等待请求。

```csharp
// Load the XAMLX workflow service.
WorkflowService workflow1 =
    (WorkflowService)XamlServices.Load(xamlxPath);

// Compile the C# expressions in the workflow by passing the Body to CompileExpressions.
CompileExpressions(workflow1.Body);

// Initialize the WorkflowServiceHost.
var host = new WorkflowServiceHost(workflow1, new Uri("http://localhost:8293/Service1.xamlx"));

// Enable Metadata publishing/
ServiceMetadataBehavior smb = new ServiceMetadataBehavior();
smb.HttpGetEnabled = true;
smb.MetadataExporter.PolicyVersion = PolicyVersion.Policy15;
host.Description.Behaviors.Add(smb);

// Open the WorkflowServiceHost and wait for requests.
host.Open();
Console.WriteLine("Press enter to quit");
Console.ReadLine();
```

 如果 C# 表达式未编译，那么，虽然 `Open` 操作会成功执行，但工作流在调用时将失败。 以下`CompileExpressions`方法是从上一个方法一样[代码工作流中的使用 C# 表达式](csharp-expressions.md#CodeWorkflows)部分。

```csharp
static void CompileExpressions(Activity activity)
{
    // activityName is the Namespace.Type of the activity that contains the
    // C# expressions.
    string activityName = activity.GetType().ToString();

    // Split activityName into Namespace and Type.Append _CompiledExpressionRoot to the type name
    // to represent the new type that represents the compiled expressions.
    // Take everything after the last . for the type name.
    string activityType = activityName.Split('.').Last() + "_CompiledExpressionRoot";
    // Take everything before the last . for the namespace.
    string activityNamespace = string.Join(".", activityName.Split('.').Reverse().Skip(1).Reverse());

    // Create a TextExpressionCompilerSettings.
    TextExpressionCompilerSettings settings = new TextExpressionCompilerSettings
    {
        Activity = activity,
        Language = "C#",
        ActivityName = activityType,
        ActivityNamespace = activityNamespace,
        RootNamespace = null,
        GenerateAsPartialClass = false,
        AlwaysGenerateSource = true,
        ForImplementation = false
    };

    // Compile the C# expression.
    TextExpressionCompilerResults results =
        new TextExpressionCompiler(settings).Compile();

    // Any compilation errors are contained in the CompilerMessages.
    if (results.HasErrors)
    {
        throw new Exception("Compilation failed.");
    }

    // Create an instance of the new compiled expression type.
    ICompiledExpressionRoot compiledExpressionRoot =
        Activator.CreateInstance(results.ResultType,
            new object[] { activity }) as ICompiledExpressionRoot;

    // Attach it to the activity.
    CompiledExpressionInvoker.SetCompiledExpressionRoot(
        activity, compiledExpressionRoot);
}
```
