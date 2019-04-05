---
title: 如何：创建和初始化跟踪侦听器
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- initializing trace listeners
- trace listeners, creating
- trace listeners, initializing
- tracing [.NET Framework], trace listeners
- logs, trace listeners
ms.assetid: 21726de1-61ee-4fdc-9dd0-3be49324d066
author: mairaw
ms.author: mairaw
ms.openlocfilehash: ee0ad6b34e30b03ec42ff793e37d0e13b448cbfe
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54583098"
---
# <a name="how-to-create-and-initialize-trace-listeners"></a>如何：创建和初始化跟踪侦听器
<xref:System.Diagnostics.Debug?displayProperty=nameWithType> 和 <xref:System.Diagnostics.Trace?displayProperty=nameWithType> 类向接收和处理消息的对象（成为侦听器）中发送消息。 在启用跟踪或调试后将自动创建并初始化一个如上所述的侦听器 <xref:System.Diagnostics.DefaultTraceListener?displayProperty=nameWithType>。 如果要将 <xref:System.Diagnostics.Trace> 或 <xref:System.Diagnostics.Debug> 输出定向到任何其他源，则必须创建并初始化其他跟踪侦听器。  
  
 所创建的侦听器应反映应用程序的需要。 例如，如果想要获取所有跟踪输出的文本记录，则创建 <xref:System.Diagnostics.TextWriterTraceListener> 侦听器；启用后，它会将所有输出都写入新的文本文件中。 另一方面，如果想要仅在应用程序执行过程中查看输出，则创建 <xref:System.Diagnostics.ConsoleTraceListener> 侦听器，以便将所有输出定向到控制台窗口。 <xref:System.Diagnostics.EventLogTraceListener> 可以将跟踪输出定向到事件日志。 有关详细信息，请参阅[跟踪侦听器](../../../docs/framework/debug-trace-profile/trace-listeners.md)。  
  
 可以在[应用程序配置文件](../../../docs/framework/configure-apps/index.md)或代码中创建跟踪侦听器。 我们建议使用应用程序配置文件，因为它们可在不更改代码的情况下添加、修改或删除跟踪侦听器。  
  
### <a name="to-create-and-use-a-trace-listener-by-using-a-configuration-file"></a>若要使用配置文件创建和初始化跟踪侦听器  
  
1.  请声明应用程序配置文件中的跟踪侦听器。 如果创建的侦听器需要的任何其他对象，请同时对它们进行声明。 下面的示例演示如何创建名为 `myListener` 的侦听器，它将写入到文本文件 `TextWriterOutput.log` 中。  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <trace autoflush="false" indentsize="4">  
          <listeners>  
            <add name="myListener" type="System.Diagnostics.TextWriterTraceListener" initializeData="TextWriterOutput.log" />  
            <remove name="Default" />  
          </listeners>  
        </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
2.  在代码中使用 <xref:System.Diagnostics.Trace> 类以将消息写入到跟踪侦听器中。  
  
    ```vb  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
### <a name="to-create-and-use-a-trace-listener-in-code"></a>若要在代码中创建和使用跟踪侦听器  
  
-   请将跟踪侦听器添加到 <xref:System.Diagnostics.Trace.Listeners%2A> 集合并将跟踪信息发送到侦听器。  
  
    ```vb  
    Trace.Listeners.Add(New TextWriterTraceListener("TextWriterOutput.log", "myListener"))  
    Trace.TraceInformation("Test message.")  
    ' You must close or flush the trace to empty the output buffer.  
    Trace.Flush()  
    ```  
  
    ```csharp  
    Trace.Listeners.Add(new TextWriterTraceListener("TextWriterOutput.log", "myListener"));  
    Trace.TraceInformation("Test message.");  
    // You must close or flush the trace to empty the output buffer.  
    Trace.Flush();  
    ```  
  
     - 或 -  
  
-   如果不希望侦听器接收跟踪输出，则不要将其添加到 <xref:System.Diagnostics.Trace.Listeners%2A> 集合。 可以通过调用侦听器自己的输出方法由独立于 <xref:System.Diagnostics.Trace.Listeners%2A> 集合的侦听器发出输出。 下面的示例演示如何向不在 <xref:System.Diagnostics.Trace.Listeners%2A> 集合中的侦听器写入代码行。  
  
    ```vb  
    Dim myListener As New TextWriterTraceListener("TextWriterOutput.log", "myListener")  
    myListener.WriteLine("Test message.")  
    ' You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush()  
    ```  
  
    ```csharp  
    TextWriterTraceListener myListener = new TextWriterTraceListener("TextWriterOutput.log", "myListener");  
    myListener.WriteLine("Test message.");  
    // You must close or flush the trace listener to empty the output buffer.  
    myListener.Flush();  
    ```  
  
## <a name="see-also"></a>请参阅
- [跟踪侦听器](../../../docs/framework/debug-trace-profile/trace-listeners.md)
- [跟踪开关](../../../docs/framework/debug-trace-profile/trace-switches.md)
- [如何：将跟踪语句添加到应用程序代码](../../../docs/framework/debug-trace-profile/how-to-add-trace-statements-to-application-code.md)
- [跟踪应用程序和在应用程序中插入检测点](../../../docs/framework/debug-trace-profile/tracing-and-instrumenting-applications.md)
