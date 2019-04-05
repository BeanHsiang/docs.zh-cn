---
title: 如何：创建未签名的友元程序集 (C#)
ms.date: 07/20/2015
ms.assetid: 78cbc4f0-b021-4141-a4ff-eb4edbd814ca
ms.openlocfilehash: 5b376266581def9bdd4315ccbee04b71b7c8bc08
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57365056"
---
# <a name="how-to-create-unsigned-friend-assemblies-c"></a>如何：创建未签名的友元程序集 (C#)
本示例演示如何将友元程序集和未签名的程序集一起使用。  
  
### <a name="to-create-an-assembly-and-a-friend-assembly"></a>创建程序集和友元程序集  
  
1.  打开命令提示。  
  
2.  创建一个名为 `friend_unsigned_A.` 的 C# 文件，其中包含以下代码。 该代码使用 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性将 friend_unsigned_B 声明为友元程序集。  
  
    ```csharp  
    // friend_unsigned_A.cs  
    // Compile with:   
    // csc /target:library friend_unsigned_A.cs  
    using System.Runtime.CompilerServices;  
    using System;  
  
    [assembly: InternalsVisibleTo("friend_unsigned_B")]  
  
    // Type is internal by default.  
    class Class1  
    {  
        public void Test()  
        {  
            Console.WriteLine("Class1.Test");  
        }  
    }  
  
    // Public type with internal member.  
    public class Class2  
    {  
        internal void Test()  
        {  
            Console.WriteLine("Class2.Test");  
        }  
    }  
    ```  
  
3.  使用以下命令编译 friend_unsigned_A 并为其签名。  
  
    ```csharp  
    csc /target:library friend_unsigned_A.cs  
    ```  
  
4.  创建一个名为 `friend_unsigned_B` 的 C# 文件，其中包含以下代码。 由于 friend_unsigned_A 将 friend_unsigned_B 指定为友元程序集，因此 friend_unsigned_B 中的代码可以访问 friend_unsigned_A 中的 `internal` 类型和成员。  
  
    ```csharp  
    // friend_unsigned_B.cs  
    // Compile with:   
    // csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    public class Program  
    {  
        static void Main()  
        {  
            // Access an internal type.  
            Class1 inst1 = new Class1();  
            inst1.Test();  
  
            Class2 inst2 = new Class2();  
            // Access an internal member of a public type.  
            inst2.Test();  
  
            System.Console.ReadLine();  
        }  
    }  
    ```  
  
5.  使用以下命令编译 friend_unsigned_B。  
  
    ```csharp  
    csc /r:friend_unsigned_A.dll /out:friend_unsigned_B.exe friend_unsigned_B.cs  
    ```  
  
     编译器生成的程序集的名称必须与传递给 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性的友元程序集的名称匹配。 必须使用 `/out` 编译器选项显式指定输出程序集（.exe 或 .dll）的名称。 有关详细信息，请参阅 [/out（C# 编译器选项）](../../../../csharp/language-reference/compiler-options/out-compiler-option.md)。  
  
6.  运行 friend_unsigned_B.exe 文件。  
  
     该程序将输出两个字符串：“Class1.Test”和“Class2.Test”。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性和 <xref:System.Security.Permissions.StrongNameIdentityPermission> 类之间具有相似之处。 主要区别是，<xref:System.Security.Permissions.StrongNameIdentityPermission> 可以要求安全权限来运行一段特定代码，而 <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> 属性控制 `internal` 类型和成员的可见性。  
  
## <a name="see-also"></a>请参阅

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [.NET 中的程序集](../../../../standard/assembly/index.md)
- [友元程序集](../../../../standard/assembly/friend-assemblies.md)
- [如何：创建签名的友元程序集 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/how-to-create-signed-friend-assemblies.md)
- [C# 编程指南](../../../../csharp/programming-guide/index.md)
