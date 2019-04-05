---
title: 保护异常处理
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- code security, exception handling
- security [.NET Framework], exception handling
- secure coding, exception handling
- exception handling, security
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
author: mairaw
ms.author: mairaw
ms.openlocfilehash: c406edcef393d3c2b9e4cf6dbeee9d572c0951f4
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54679378"
---
# <a name="securing-exception-handling"></a>保护异常处理
在 Visual c + + 和 Visual Basic 中，筛选器表达式进一步在堆栈中向上之前运行**最后**语句。 **捕获**与关联的块之后运行该筛选器**最后**语句。 有关详细信息，请参阅[使用用户筛选异常](../../../docs/standard/exceptions/using-user-filtered-exception-handlers.md)。 本部分中检查此顺序的安全隐患。 请考虑下面的伪代码示例说明了哪些筛选器语句中的顺序，并**最后**运行的语句。  
  
```cpp  
void Main()   
{  
    try   
    {  
        Sub();  
    }   
    except (Filter())   
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()   
{  
    try   
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }   
    finally   
    {  
        Console.WriteLine("finally");  
    }  
}                        
```  
  
 此代码将打印以下。  
  
```  
Throw  
Filter  
Finally  
Catch  
```  
  
 筛选器之前运行**最后**语句，因此安全问题可能会造成的任何内容会使更改在其中执行其他代码无法充分利用状态。 例如：  
  
```cpp  
try   
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and   
    // so on) that could be exploited if malicious   
    // code ran before state is restored.  
    Do_some_work();  
}   
finally   
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 此伪代码允许运行任意代码的堆栈较高的筛选器。 将具有类似的效果的操作的其他示例包括临时模拟另一标识，绕过某些安全检查，内部标志设置或更改区域性与线程关联。 建议的解决方案是引入了一个异常处理程序，以隔离到线程的状态从向调用方的筛选器块的代码的更改。 但是，很重要的异常处理程序必须正确地引入或将不会修复此问题。 下面的示例切换的 UI 区域性，但无法类似的方式公开任何类型的线程状态更改。  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",   
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 正确的解决方法在这种情况下是包装现有**尝试**/**最后**块中**尝试**/**捕获**块。 只需引入**catch throw**到现有的子句**尝试**/**最后**块不能解决此问题，如下面的示例中所示。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try   
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally   
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 此操作未修复问题，因为**最后**以前未运行语句`FilterFunc`获取控件。  
  
 下面的示例通过确保修复此问题**最后**子句已提供异常向调用方的异常筛选器块之前执行。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try    
    {  
        try   
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally   
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## <a name="see-also"></a>请参阅
- [安全编码准则](../../../docs/standard/security/secure-coding-guidelines.md)
