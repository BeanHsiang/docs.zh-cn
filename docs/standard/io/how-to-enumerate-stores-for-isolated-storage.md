---
title: 如何：枚举独立存储的存储区
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enumerating stores
- data storage using isolated storage, enumerating stores
- storing data using isolated storage, enumerating stores
- stores, enumerating
- isolated storage, enumerating stores
- data stores, enumerating
ms.assetid: 0fcf279a-f241-48f0-8034-2e3d331f1fcb
author: mairaw
ms.author: mairaw
ms.openlocfilehash: f14259afe4ee296d930b042d9e9ef069a81e65f9
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54591755"
---
# <a name="how-to-enumerate-stores-for-isolated-storage"></a>如何：枚举独立存储的存储区
您可以使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=nameWithType> 静态方法枚举当前用户的所有独立存储区。 该方法采用 <xref:System.IO.IsolatedStorage.IsolatedStorageScope> 值并且返回 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 枚举器。 若要枚举存储区，您必须具有指定<xref:System.Security.Permissions.IsolatedStorageFilePermission> 值的 <xref:System.Security.Permissions.IsolatedStorageContainment.AdministerIsolatedStorageByUser> 权限。 如果调用采用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> 值的 <xref:System.IO.IsolatedStorage.IsolatedStorageScope.User> 方法，它将返回一组为当前用户定义的 <xref:System.IO.IsolatedStorage.IsolatedStorageFile> 对象。  
  
## <a name="example"></a>示例  
 下面的代码示例使用 <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A> 方法获取按用户和程序集隔离的存储区，创建一些文件，并检索这些文件。  
  
 [!code-csharp[Conceptual.IsolatedStorage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.isolatedstorage/cs/source2.cs#2)]
 [!code-vb[Conceptual.IsolatedStorage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.isolatedstorage/vb/source2.vb#2)]  
  
## <a name="see-also"></a>请参阅

- <xref:System.IO.IsolatedStorage.IsolatedStorageFile>
- [独立存储](../../../docs/standard/io/isolated-storage.md)
