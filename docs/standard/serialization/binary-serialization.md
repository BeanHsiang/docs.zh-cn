---
title: 二进制序列化
ms.date: 01/02/2018
helpviewer_keywords:
- binary serialization
- serialization, about serialization
- deserialization
- binary serialization, about serialization
- binary serialization, .net core serialization
- serialization, cross-framework
ms.assetid: 2b1ea3be-1152-4032-b2b3-07794054c405
author: ViktorHofer
ms.author: mairaw
ms.openlocfilehash: 81d79ec0add7f8b73cced5c64a470fa9d699063c
ms.sourcegitcommit: 40364ded04fa6cdcb2b6beca7f68412e2e12f633
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2019
ms.locfileid: "56972399"
---
# <a name="binary-serialization"></a>二进制序列化

可以将序列化定义为一个将对象状态存储到存储介质的过程。 在这个过程中，对象的公共字段和私有字段以及类（包括含有该类的程序集）的名称，将转换成字节流，而字节流接着将写入数据流。 随后对该对象进行反序列化时，将创建原始对象的准确克隆。

在面向对象的环境中实现序列化机制时，必须多在易用性与灵活性之间做出权衡。 很大程度上，这个过程可以自动完成，但前提是您对该过程拥有足够的控制权。 例如，如果简单的二进制序列化不足，或者可能有特定原因决定需要对类中的哪些字段进行序列化，可能就会出现这种情况。 以下章节验证了随 .NET Framework 一起提供的可靠序列化机制，并强调了根据需要自定义该过程所能使用的一些重要功能。

> [!NOTE]
> 如果使用不同的 .NET Framework 版本序列化和反序列化以 UTF-8 或 UTF-7 编码的对象，则不保留该对象的状态。

[!INCLUDE [binary-serialization-warning](../../../includes/binary-serialization-warning.md)]

由于二进制序列化的性质允许在对象内修改私有成员，因此若要更改其状态，建议使用其他序列化框架，如在公共 API 曲面上操作的 JSON.NET。

## <a name="binary-serialization-in-net-core"></a>.NET Core 中的二进制序列化

.NET Core 支持带有类型子集的二进制序列化。 可在[可序列化类型部分](#serializable-types)查看受支持的类型列表。 一组已定义的类型是完全可以在 .NET Framework 4.5.1 及更高版本之间和 .NET Core 2.0 及更高版本之间进行序列化的。 其他 .NET 实现（如 Mono）并未正式得到支持，但应该也能使用。

### <a name="serializable-types"></a>可序列化类型

- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:Microsoft.CSharp.RuntimeBinder.RuntimeBinderInternalCompilerException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.AccessViolationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.AggregateException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.AppDomainUnloadedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ApplicationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ArgumentException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ArgumentNullException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ArgumentOutOfRangeException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ArithmeticException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Array?displayProperty=nameWithType>
- <xref:System.ArraySegment%601?displayProperty=nameWithType>
- <xref:System.ArrayTypeMismatchException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.BadImageFormatException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Boolean?displayProperty=nameWithType>
- <xref:System.Byte?displayProperty=nameWithType>
- <xref:System.CannotUnloadAppDomainException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Char?displayProperty=nameWithType>
- <xref:System.Collections.ArrayList?displayProperty=nameWithType>
- <xref:System.Collections.BitArray?displayProperty=nameWithType>
- <xref:System.Collections.Comparer?displayProperty=nameWithType>
- <xref:System.Collections.DictionaryEntry?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Comparer%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.EqualityComparer%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.HashSet%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.KeyNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Collections.Generic.KeyValuePair%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.LinkedList%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.List%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Queue%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedList%602?displayProperty=nameWithType>
- <xref:System.Collections.Generic.SortedSet%601?displayProperty=nameWithType>
- <xref:System.Collections.Generic.Stack%601?displayProperty=nameWithType>
- <xref:System.Collections.Hashtable?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.Collection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.KeyedCollection%602?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ObservableCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601?displayProperty=nameWithType>
- <xref:System.Collections.Queue?displayProperty=nameWithType>
- <xref:System.Collections.SortedList?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.HybridDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.ListDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.OrderedDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.StringCollection?displayProperty=nameWithType>
- <xref:System.Collections.Specialized.StringDictionary?displayProperty=nameWithType>
- <xref:System.Collections.Stack?displayProperty=nameWithType>
- `System.Collections.Generic.NonRandomizedStringEqualityComparer` （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.BindingList%601?displayProperty=nameWithType>
- <xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.Design.CheckoutException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.InvalidAsynchronousStateException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.InvalidEnumArgumentException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.LicenseException?displayProperty=nameWithType> （在.NET Core 2.0.4 和更高版本中可用，从.NET Framework 到.NET Core 不支持序列化）
- <xref:System.ComponentModel.WarningException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ComponentModel.Win32Exception?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.ConfigurationErrorsException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.ConfigurationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.Provider.ProviderException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.SettingsPropertyIsReadOnlyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.SettingsPropertyNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Configuration.SettingsPropertyWrongTypeException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ContextMarshalException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DBNull?displayProperty=nameWithType> （适用于.NET Core 2.0.2 和更高版本）
- <xref:System.Data.Common.DbException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.ConstraintException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.DBConcurrencyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.DataException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.DataSet?displayProperty=nameWithType>
- <xref:System.Data.DataTable?displayProperty=nameWithType> （除非 RemotingFormat 设 SerializationFormat.Binary 这种情况下它可以仅与交换.NET Core 2.1 和更高版本。）
- <xref:System.Data.DeletedRowInaccessibleException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.DuplicateNameException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.EvaluateException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.InRowChangingEventException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.InvalidConstraintException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.InvalidExpressionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.MissingPrimaryKeyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.NoNullAllowedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.Odbc.OdbcException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.OperationAbortedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.PropertyCollection?displayProperty=nameWithType>
- <xref:System.Data.ReadOnlyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.RowNotInTableException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SqlClient.SqlException?displayProperty=nameWithType> （在.NET Core 2.0.4 和更高版本中可用，从.NET Framework 到.NET Core 不支持序列化）
- <xref:System.Data.SqlTypes.SqlAlreadyFilledException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SqlTypes.SqlBoolean?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlByte?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlDateTime?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlDouble?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlGuid?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt16?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt32?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlInt64?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlNotFilledException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SqlTypes.SqlNullValueException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SqlTypes.SqlString?displayProperty=nameWithType>
- <xref:System.Data.SqlTypes.SqlTruncateException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SqlTypes.SqlTypeException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.StrongTypingException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.SyntaxErrorException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Data.VersionNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DataMisalignedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DateTime?displayProperty=nameWithType>
- <xref:System.DateTimeOffset?displayProperty=nameWithType>
- <xref:System.Decimal?displayProperty=nameWithType>
- `System.Diagnostics.Contracts.ContractException` （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Diagnostics.Tracing.EventSourceException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.DirectoryNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.MultipleMatchesException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.NoMatchingPrincipalException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.PasswordException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.PrincipalException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.PrincipalExistsException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.PrincipalOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.AccountManagement.PrincipalServerDownException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectExistsException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryObjectNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.ActiveDirectoryServerDownException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.ForestTrustCollisionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.ActiveDirectory.SyncFromAllServersOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.DirectoryServicesCOMException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.Protocols.BerConversionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.Protocols.DirectoryException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.Protocols.DirectoryOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.Protocols.LdapException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DirectoryServices.Protocols.TlsOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DivideByZeroException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.DllNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Double?displayProperty=nameWithType>
- <xref:System.Drawing.Color?displayProperty=nameWithType>
- <xref:System.Drawing.Point?displayProperty=nameWithType>
- <xref:System.Drawing.PointF?displayProperty=nameWithType>
- <xref:System.Drawing.Rectangle?displayProperty=nameWithType>
- <xref:System.Drawing.RectangleF?displayProperty=nameWithType>
- <xref:System.Drawing.Size?displayProperty=nameWithType>
- <xref:System.Drawing.SizeF?displayProperty=nameWithType>
- <xref:System.DuplicateWaitObjectException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.EntryPointNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Enum?displayProperty=nameWithType>
- <xref:System.EventArgs?displayProperty=nameWithType> （适用于.NET Core 2.0.6 和更高版本）
- <xref:System.Exception?displayProperty=nameWithType>
- <xref:System.ExecutionEngineException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.FieldAccessException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.FormatException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Globalization.CompareInfo?displayProperty=nameWithType>
- <xref:System.Globalization.CultureNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Globalization.SortVersion?displayProperty=nameWithType>
- <xref:System.Guid?displayProperty=nameWithType>
- `System.IO.Compression.ZLibException` （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.DriveNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.EndOfStreamException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.FileFormatException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.FileLoadException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.FileNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.IOException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.InternalBufferOverflowException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.InvalidDataException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.IsolatedStorage.IsolatedStorageException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IO.PathTooLongException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.IndexOutOfRangeException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.InsufficientExecutionStackException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.InsufficientMemoryException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Int16?displayProperty=nameWithType>
- <xref:System.Int32?displayProperty=nameWithType>
- <xref:System.Int64?displayProperty=nameWithType>
- <xref:System.IntPtr?displayProperty=nameWithType>
- <xref:System.InvalidCastException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.InvalidOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.InvalidProgramException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.InvalidTimeZoneException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MemberAccessException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MethodAccessException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MissingFieldException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MissingMemberException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MissingMethodException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.MulticastNotSupportedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.Cookie?displayProperty=nameWithType>
- <xref:System.Net.CookieCollection?displayProperty=nameWithType>
- <xref:System.Net.CookieContainer?displayProperty=nameWithType>
- <xref:System.Net.CookieException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.HttpListenerException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.Mail.SmtpException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.Mail.SmtpFailedRecipientException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.Mail.SmtpFailedRecipientsException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.NetworkInformation.NetworkInformationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.NetworkInformation.PingException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.ProtocolViolationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.Sockets.SocketException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.WebException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Net.WebSockets.WebSocketException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.NotFiniteNumberException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.NotImplementedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.NotSupportedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.NullReferenceException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Numerics.BigInteger?displayProperty=nameWithType>
- <xref:System.Numerics.Complex?displayProperty=nameWithType>
- <xref:System.Object?displayProperty=nameWithType>
- <xref:System.ObjectDisposedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.OperationCanceledException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.OutOfMemoryException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.OverflowException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.PlatformNotSupportedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.RankException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.AmbiguousMatchException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.CustomAttributeFormatException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.InvalidFilterCriteriaException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.ReflectionTypeLoadException?displayProperty=nameWithType> （在.NET Core 2.0.4 和更高版本中可用，从.NET Framework 到.NET Core 不支持序列化）
- <xref:System.Reflection.TargetException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.TargetInvocationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Reflection.TargetParameterCountException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Resources.MissingManifestResourceException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Resources.MissingSatelliteAssemblyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.CompilerServices.RuntimeWrappedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.COMException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.ExternalException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.InvalidComObjectException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.InvalidOleVariantTypeException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.MarshalDirectiveException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.SEHException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.SafeArrayRankMismatchException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.InteropServices.SafeArrayTypeMismatchException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.Serialization.InvalidDataContractException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Runtime.Serialization.SerializationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.SByte?displayProperty=nameWithType>
- <xref:System.Security.AccessControl.PrivilegeNotHeldException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Authentication.AuthenticationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Authentication.InvalidCredentialException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Cryptography.CryptographicException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Cryptography.CryptographicUnexpectedOperationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- `System.Security.Cryptography.Xml.CryptoSignedXmlRecursionException` （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.HostProtectionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Policy.PolicyException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.Principal.IdentityNotMappedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.SecurityException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本、 有限的序列化数据）
- <xref:System.Security.VerificationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Security.XmlSyntaxException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ServiceProcess.TimeoutException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Single?displayProperty=nameWithType>
- <xref:System.StackOverflowException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.String?displayProperty=nameWithType>
- <xref:System.StringComparer?displayProperty=nameWithType>
- <xref:System.SystemException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Text.DecoderFallbackException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Text.EncoderFallbackException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Text.RegularExpressions.RegexMatchTimeoutException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Text.StringBuilder?displayProperty=nameWithType>
- <xref:System.Threading.AbandonedMutexException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.BarrierPostPhaseException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.LockRecursionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.SemaphoreFullException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.SynchronizationLockException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.Tasks.TaskCanceledException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.Tasks.TaskSchedulerException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.ThreadAbortException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.ThreadInterruptedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.ThreadStartException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.ThreadStateException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Threading.WaitHandleCannotBeOpenedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.TimeSpan?displayProperty=nameWithType>
- <xref:System.TimeZoneInfo.AdjustmentRule?displayProperty=nameWithType>
- <xref:System.TimeZoneInfo?displayProperty=nameWithType>
- <xref:System.TimeZoneNotFoundException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.TimeoutException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Transactions.TransactionAbortedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Transactions.TransactionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Transactions.TransactionInDoubtException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Transactions.TransactionManagerCommunicationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Transactions.TransactionPromotionException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Tuple?displayProperty=nameWithType>
- <xref:System.TypeAccessException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.TypeInitializationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.TypeLoadException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.TypeUnloadedException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.UInt16?displayProperty=nameWithType>
- <xref:System.UInt32?displayProperty=nameWithType>
- <xref:System.UInt64?displayProperty=nameWithType>
- <xref:System.UIntPtr?displayProperty=nameWithType>
- <xref:System.UnauthorizedAccessException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Uri?displayProperty=nameWithType>
- <xref:System.UriFormatException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.ValueTuple?displayProperty=nameWithType> （不能序列化在.NET Framework 4.7 和更早版本）
- <xref:System.ValueType?displayProperty=nameWithType>
- <xref:System.Version?displayProperty=nameWithType>
- <xref:System.WeakReference%601?displayProperty=nameWithType>
- <xref:System.WeakReference?displayProperty=nameWithType>
- <xref:System.Xml.Schema.XmlSchemaException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.Schema.XmlSchemaInferenceException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.Schema.XmlSchemaValidationException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.XPath.XPathException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.XmlException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.Xsl.XsltCompileException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）
- <xref:System.Xml.Xsl.XsltException?displayProperty=nameWithType> （适用于.NET Core 2.0.4 和更高版本）

## <a name="in-this-section"></a>本节内容

- [序列化概念](../../../docs/standard/serialization/serialization-concepts.md)\
讨论序列化在其中有用的两种方案：在将数据保持到存储中以及在跨应用程序域传递对象时。

- [基本序列化](../../../docs/standard/serialization/basic-serialization.md)\
描述如何使用二进制格式化程序和 SOAP 格式化程序来序列化对象。

- [选择性的序列化](../../../docs/standard/serialization/selective-serialization.md)\
描述如何防止序列化某些类成员。

- [自定义序列化](../../../docs/standard/serialization/custom-serialization.md)\
描述如何使用 <xref:System.Runtime.Serialization.ISerializable> 接口自定义类的序列化。

- [序列化过程中的步骤](../../../docs/standard/serialization/steps-in-the-serialization-process.md)\
描述对格式化程序调用 <xref:System.Runtime.Serialization.Formatter.Serialize%2A> 方法时序列化采取操作的过程。

- [版本容错序列化](../../../docs/standard/serialization/version-tolerant-serialization.md)\
介绍如何创建可序列化类型。在不导致应用程序引发异常的情况下，可以在以后对这样的类型进行修改。

- [序列化准则](../../../docs/standard/serialization/serialization-guidelines.md)\
提供一些通用准则，用于确定何时序列化对象。

## <a name="reference"></a>参考

- <xref:System.Runtime.Serialization>\
包含可用于序列化和反序列化对象的类。

## <a name="related-sections"></a>相关章节

- [XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)\
描述随公共语言运行库一起提供的 XML 序列化机制。

- [安全和序列化](../../../docs/framework/misc/security-and-serialization.md)\
描述写入执行序列化的代码时需要遵循的安全编码原则。

- [.NET 远程处理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/72x4h507(v=vs.100))\
描述 .NET Framework 中为远程通信提供的多种通信方法。

- [使用 ASP.NET 和 XML Web 服务客户端创建的 XML Web Services](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/7bkzywba(v=vs.100))\
提供一些主题，描述并解释如何对使用 ASP.NET 创建的 XML Web services 进行编程。