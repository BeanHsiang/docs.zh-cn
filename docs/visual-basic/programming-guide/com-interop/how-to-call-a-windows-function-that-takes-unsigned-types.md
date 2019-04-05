---
title: 如何：调用采用无符号的类型 (Visual Basic 中) 的 Windows 函数
ms.date: 07/20/2015
helpviewer_keywords:
- Windows functions [Visual Basic], calling
- unsigned data types [Visual Basic]
- UShort data type [Visual Basic], using
- functions [Visual Basic], calling Windows functions
- ULong data type [Visual Basic], using
- UInteger data type [Visual Basic], using
- data types [Visual Basic], using
- unsigned types [Visual Basic]
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types [Visual Basic], using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
ms.openlocfilehash: d1a679242f89c17e58a837ac2d356e1594972fb3
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57374552"
---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>如何：调用采用无符号的类型 (Visual Basic 中) 的 Windows 函数

如果您正在使用类、 模块或结构，它具有无符号的整数类型的成员，可以访问这些成员与 Visual Basic。

### <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>若要调用采用无符号的类型的 Windows 函数

1. 使用[Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)来判断 Visual Basic 的库包含该函数的什么其名称是在该库中，其调用的序列是什么，以及如何将字符串转换调用它时。

2. 在中`Declare`语句，使用`UInteger`， `ULong`， `UShort`，或`Byte`根据需要为每个参数使用一个无符号类型。

3. 要调用若要查找的名称和值的常量，它使用的 Windows 函数，请参阅文档。 其中许多 WinUser.h 文件中定义。

4. 声明在代码中的必要常量。 许多 Windows 常量是 32 位无符号的值，并应声明这些`As UInteger`。

5. 以正常方式调用函数。 下面的示例调用 Windows 函数`MessageBox`，其将无符号的整数自变量。

    ```vb
    Public Class windowsMessage
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (
            ByVal hWnd As Integer,
            ByVal lpText As String,
            ByVal lpCaption As String,
            ByVal uType As UInteger) As Integer
        Private Const MB_OK As UInteger = 0
        Private Const MB_ICONEXCLAMATION As UInteger = &H30
        Private Const IDOK As UInteger = 1
        Private Const IDCLOSE As UInteger = 8
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION
        Public Function messageThroughWindows() As String
            Dim r As Integer = mb(0, "Click OK if you see this!",
                "Windows API call", c)
            Dim s As String = "Windows API MessageBox returned " &
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"
            Return s
        End Function
    End Class
    ```

     你可以测试该函数`messageThroughWindows`用下面的代码。

    ```vb
    Public Sub consumeWindowsMessage()
        Dim w As New windowsMessage
        w.messageThroughWindows()
    End Sub
    ```

    > [!CAUTION]
    > `UInteger`， `ULong`， `UShort`，和`SByte`数据类型不属于[语言独立性和与语言无关的组件](../../../standard/language-independence-and-language-independent-components.md)(CLS)，因此符合 cls 的代码不能使用的组件，使用它们。

    > [!IMPORTANT]
    > Windows 应用程序编程接口 (API)，如在非托管代码调用公开您的代码与潜在的安全风险。

    > [!IMPORTANT]
    > 调用 Windows API 要求非托管的代码的权限，这可能会影响在部分信任情况下执行。 有关详细信息，请参阅<xref:System.Security.Permissions.SecurityPermission>并[代码访问权限](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h846e9b3(v=vs.100))。

## <a name="see-also"></a>请参阅

- [数据类型](../../../visual-basic/language-reference/data-types/index.md)
- [Integer 数据类型](../../../visual-basic/language-reference/data-types/integer-data-type.md)
- [UInteger 数据类型](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)
- [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)
- [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)
