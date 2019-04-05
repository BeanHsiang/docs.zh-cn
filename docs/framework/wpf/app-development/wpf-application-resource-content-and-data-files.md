---
title: WPF 应用程序资源、内容和数据文件
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WPF application [WPF], files
- loose resources [WPF]
- content files [WPF]
- Site of Origin files [WPF]
- resource files [WPF]
- remote files [WPF]
- embedded resources [WPF]
- files [WPF]
- referencing application files [WPF]
- application development [WPF], files
- application management [WPF]
ms.assetid: 7ad2943b-3961-41d3-8fc6-1582d43f5d99
ms.openlocfilehash: f9fd936c15454a81058d42825800a388c5c90a40
ms.sourcegitcommit: 0c48191d6d641ce88d7510e319cf38c0e35697d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57379193"
---
# <a name="wpf-application-resource-content-and-data-files"></a>WPF 应用程序资源、内容和数据文件
[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 应用程序通常依赖包含不可执行的数据，如文件[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]，图像、 视频和音频。 Windows Presentation Foundation (WPF) 提供了配置、 确定，并使用这些类型的数据文件，称为应用程序数据文件的特殊支持。 这种支持主要针对一组特定的应用程序数据文件类型，包括：  
  
-   **资源文件**:数据文件编译为可执行文件或库的[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]程序集。  
  
-   **内容文件**:与可执行文件的显式关联的独立数据文件[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]程序集。  
  
-   **源站点文件**:没有与可执行文件关联的独立数据文件[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]程序集。  
  
 这三种类型的文件之间的一个重要区别是：资源文件和内容文件在生成时即为程序集所知；程序集明确知道它们的存在。 为源站点文件，但是，程序集可能完全不了解它们，或者通过 pack[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]引用; 的后一种情况下不能保证被引用的源站点文件实际存在。  
  
 若要引用应用程序数据文件，Windows Presentation Foundation (WPF) 可使用包[!INCLUDE[TLA#tla_uri](../../../../includes/tlasharptla-uri-md.md)]方案，它在详细信息中所述[WPF 中的 Pack Uri](pack-uris-in-wpf.md))。  
  
 本主题介绍如何配置和使用应用程序数据文件。  
  
  
<a name="Resource_Files"></a>   
## <a name="resource-files"></a>资源文件  
 如果应用程序数据文件必须始终可供某个应用程序使用，那么保证可用性的唯一方法是将其编译到应用程序的主可执行程序集内，或者它所引用的程序集内。 此类型的应用程序数据文件称为*资源文件*。  
  
 应在以下情况下使用资源文件：  
  
-   将资源文件编译到程序集内之后，无需更新资源文件的内容。  
  
-   希望通过减少文件依赖项的数量来简化应用程序分发的复杂性。  
  
-   在应用程序数据文件必须是可本地化 (请参阅[WPF 全球化和本地化概述](../advanced/wpf-globalization-and-localization-overview.md))。  
  
> [!NOTE]
>  在本部分中所述的资源文件是不同的资源文件中所述[XAML 资源](../advanced/xaml-resources.md)和不同于嵌入或链接的资源中所述[管理应用程序资源 (.NET)](/visualstudio/ide/managing-application-resources-dotnet).  
  
### <a name="configuring-resource-files"></a>配置资源文件  
 在中[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]，资源文件是包含在一个文件[!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)]项目用作`Resource`项。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Resource Include="ResourceFile.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在中[!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]，通过将文件添加到项目和设置创建一个资源文件及其`Build Action`到`Resource`。  
  
 当生成项目时，[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]将资源编译为程序集。  
  
### <a name="using-resource-files"></a>使用资源文件  
 若要加载资源文件，可以调用<xref:System.Windows.Application.GetResourceStream%2A>方法<xref:System.Windows.Application>类，并传入一个包[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]标识所需的资源文件。 <xref:System.Windows.Application.GetResourceStream%2A> 返回<xref:System.Windows.Resources.StreamResourceInfo>对象，该资源文件作为公开<xref:System.IO.Stream>并描述其内容类型。  
  
 例如，下面的代码演示如何使用<xref:System.Windows.Application.GetResourceStream%2A>加载<xref:System.Windows.Controls.Page>资源文件，并将其设置为的内容<xref:System.Windows.Controls.Frame>(`pageFrame`):  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadapageresourcefilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageResourceFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadapageresourcefilemanuallycode)]  
  
 虽然通过调用<xref:System.Windows.Application.GetResourceStream%2A>可以让您访问<xref:System.IO.Stream>，您需要执行额外的工作来将其转换为将要设置其属性的类型。 相反，您可以让[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]负责打开和转换<xref:System.IO.Stream>通过加载资源文件直接到使用代码的类型的属性。  
  
 下面的示例演示如何加载<xref:System.Windows.Controls.Page>直接<xref:System.Windows.Controls.Frame>(`pageFrame`) 使用的代码。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.cs#loadpageresourcefilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml.vb#loadpageresourcefilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageResourceFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetResourceStreamSnippetWindow.xaml#loadpageresourcefilefromxaml)]  
  
### <a name="application-code-files-as-resource-files"></a>作为资源文件的应用程序代码文件  
 一组特殊[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]可以使用包引用应用程序代码文件[!INCLUDE[TLA2#tla_uri#plural](../../../../includes/tla2sharptla-urisharpplural-md.md)]，包括 windows、 页、 流文档和资源字典。 例如，可以设置<xref:System.Windows.Application.StartupUri%2A?displayProperty=nameWithType>与包属性[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]引用的窗口或你想要在应用程序启动时加载的页面。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#SetApplicationStartupURI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/App.xaml#setapplicationstartupuri)]  
  
 您可以执行操作时采用此[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]文件包含在[!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)]项目用作`Page`项。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Page Include="MainWindow.xaml" />  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在中[!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]，添加一个新<xref:System.Windows.Window>， <xref:System.Windows.Navigation.NavigationWindow>， <xref:System.Windows.Controls.Page>， <xref:System.Windows.Documents.FlowDocument>，或<xref:System.Windows.ResourceDictionary>到项目，`Build Action`的标记文件将默认为`Page`。  
  
 使用的项目时`Page`编译项目，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]项转换为二进制格式，并将其编译到关联的程序集。 因此，可以像使用典型的资源文件一样使用这些文件。  
  
> [!NOTE]
>  如果[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]作为配置文件`Resource`项，并且没有代码隐藏文件，则原始[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]编译到程序集而不是原始的二进制版本[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]。  
  
<a name="Content_Files"></a>   
## <a name="content-files"></a>内容文件  
 一个*的内容文件*作为松散文件与可执行程序集一起分发。 虽然它们不编译到程序集内，但编译程序集时所使用的元数据建立了与每个内容文件的关联。  
  
 如果应用程序需要一组特定的应用程序数据文件，并且你希望能够更新这些文件，而无需重新编译使用它们的程序集，应使用内容文件。  
  
### <a name="configuring-content-files"></a>配置内容文件  
 若要将内容文件添加到项目中，应用程序数据文件必须是作为包含`Content`项。 此外，因为内容文件不直接编译为程序集，您需要设置[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]`CopyToOutputDirectory`要指定内容文件复制到的位置相对于生成程序集的元数据元素。 如果所需资源复制到生成输出文件夹每次生成项目，则设置`CopyToOutputDirectory`元数据元素与`Always`值。 否则，可以确保，仅资源的最新版本复制到生成输出文件夹使用`PreserveNewest`值。  
  
 下面演示的是一个配置为内容文件的文件，此内容文件只有在将新版本的资源添加到项目时才会复制到生成输出文件夹。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <ItemGroup>  
    <Content Include="ContentFile.xaml">  
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>  
    </Content>  
  </ItemGroup>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在[!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]，通过将文件添加到项目和设置创建一个内容文件，其`Build Action`到`Content`，并设置其`Copy to Output Directory`到`Copy always`(与相同`Always`) 和`Copy if newer`(与相同`PreserveNewest`)。  
  
 当生成项目时，<xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>属性编译到程序集的每个内容文件的元数据。  
  
 `[assembly: AssemblyAssociatedContentFile("ContentFile.xaml")]`  
  
 值<xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>意味着相对于其位置在项目中的内容文件的路径。 例如，如果内容文件位于项目子文件夹中，附加路径信息将合并到<xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>值。  
  
 `[assembly: AssemblyAssociatedContentFile("Resources/ContentFile.xaml")]`  
  
 <xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>值也是生成输出文件夹中的内容文件的路径的值。  
  
### <a name="using-content-files"></a>使用内容文件  
 若要加载的内容文件，可以调用<xref:System.Windows.Application.GetContentStream%2A>方法<xref:System.Windows.Application>类，并传入一个包[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]，它标识所需的内容文件。 <xref:System.Windows.Application.GetContentStream%2A> 返回<xref:System.Windows.Resources.StreamResourceInfo>对象，该文件内容作为公开<xref:System.IO.Stream>并描述其内容类型。  
  
 例如，下面的代码演示如何使用<xref:System.Windows.Application.GetContentStream%2A>加载<xref:System.Windows.Controls.Page>内容文件，并将其设置为的内容<xref:System.Windows.Controls.Frame>(`pageFrame`)。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadapagecontentfilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageContentFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadapagecontentfilemanuallycode)]  
  
 虽然通过调用<xref:System.Windows.Application.GetContentStream%2A>可以让您访问<xref:System.IO.Stream>，您需要执行额外的工作来将其转换为将要设置其属性的类型。 相反，您可以让[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]负责打开和转换<xref:System.IO.Stream>通过加载资源文件直接到使用代码的类型的属性。  
  
 下面的示例演示如何加载<xref:System.Windows.Controls.Page>直接<xref:System.Windows.Controls.Frame>(`pageFrame`) 使用的代码。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.cs#loadpagecontentfilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageContentFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml.vb#loadpagecontentfilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageContentFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/ApplicationGetContentStreamSnippetWindow.xaml#loadpagecontentfilefromxaml)]  
  
<a name="Site_of_Origin_Files"></a>   
## <a name="site-of-origin-files"></a>源站点文件  
 资源文件有显式关系与它们一起分发的程序集由定义<xref:System.Windows.Resources.AssemblyAssociatedContentFileAttribute>。 但是，有些情况下可能需要在程序集和应用程序数据文件之间建立隐式关系或不存在的关系，这些情况包括：  
  
-   在编译时不存在的文件。  
  
-   在运行之前不知道程序集将需要哪些文件。  
  
-   希望能够更新文件，无需重新编译与这些文件关联的程序集。  
  
-   应用程序使用大型数据文件（如音频和视频），并且你希望仅在用户选择下载时才下载这些文件。  
  
 可以加载这些类型的文件使用的传统[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]方案，如 file:/// 和 http:// 方案。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#AbsolutePackUriFileHttpReferenceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/AbsolutePackUriPage.xaml#absolutepackurifilehttpreferencexaml)]  
  
 但是，file:/// 和 http:// 方案要求应用程序具有完全信任。 如果应用程序是[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]启动从 Internet 或 intranet，并请求仅的允许从这些位置启动的应用程序的松散文件只能从原点 （应用程序的站点加载的权限集启动位置）。 此类文件称为*源站点的*文件。  
  
 虽然源站点文件并不仅限于部分信任应用程序，但这些文件是部分信任应用程序的唯一选择。 完全信任应用程序可能仍然需要加载它们在生成时所不知道的应用程序数据文件；但是完全信任应用程序可以使用 file:///，应用程序数据文件很可能将安装在该应用程序程序集所在的文件夹或其子文件夹中。 在此情况下，使用源站点引用比使用 file:/// 更加容易，因为使用 file:/// 需要找出文件的完整路径。  
  
> [!NOTE]
>  文件不会缓存使用的源站点的[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]客户端计算机，而内容文件却上。 因此，只有在专门请求下载源站点文件时，才会下载它们。 如果[!INCLUDE[TLA#tla_xbap](../../../../includes/tlasharptla-xbap-md.md)]应用程序具有大型媒体文件，因为源站点文件意味着初始应用程序启动速度更快，并且文件只会按需下载配置它们。  
  
### <a name="configuring-site-of-origin-files"></a>配置源站点文件  
 如果在源站点文件在编译时是不存在或未知，则需要使用传统部署机制，用于确保所需的文件都可以在运行时，包括使用`XCopy`命令行程序或[!INCLUDE[TLA#tla_wininstall](../../../../includes/tlasharptla-wininstall-md.md)].  
  
 如果您知道在编译时将如要放置于源站点的但仍想要避免显式依赖的文件，则可以添加到这些文件[!INCLUDE[TLA#tla_msbuild](../../../../includes/tlasharptla-msbuild-md.md)]项目用作`None`项。 因为与内容文件，您需要设置[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]`CopyToOutputDirectory`属性来指定源站点文件复制到的位置相对于生成的程序集，通过指定`Always`值或`PreserveNewest`值。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
  ...  
  <None Include="PageSiteOfOriginFile.xaml">  
    <CopyToOutputDirectory>Always</CopyToOutputDirectory>  
  </None>  
  ...  
</Project>  
```  
  
> [!NOTE]
>  在中[!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]，你创建原始文件的一个站点将文件添加到项目并设置其`Build Action`到`None`。  
  
 当生成项目时，[!INCLUDE[TLA2#tla_msbuild](../../../../includes/tla2sharptla-msbuild-md.md)]将指定的文件复制到生成输出文件夹。  
  
### <a name="using-site-of-origin-files"></a>使用源站点文件  
 若要加载源站点文件，可以调用<xref:System.Windows.Application.GetRemoteStream%2A>方法<xref:System.Windows.Application>类，并传入一个包[!INCLUDE[TLA2#tla_uri](../../../../includes/tla2sharptla-uri-md.md)]标识的原始文件所需的站点。 <xref:System.Windows.Application.GetRemoteStream%2A> 返回<xref:System.Windows.Resources.StreamResourceInfo>对象，它提供了源站点文件作为<xref:System.IO.Stream>并描述其内容类型。  
  
 例如，下面的代码演示如何使用<xref:System.Windows.Application.GetRemoteStream%2A>加载<xref:System.Windows.Controls.Page>源站点的文件，并将其设置为的内容<xref:System.Windows.Controls.Frame>(`pageFrame`)。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadapagesoofilemanuallycode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadAPageSOOFileManuallyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadapagesoofilemanuallycode)]  
  
 虽然通过调用<xref:System.Windows.Application.GetRemoteStream%2A>可以让您访问<xref:System.IO.Stream>，您需要执行额外的工作来将其转换为将要设置其属性的类型。 相反，您可以让[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]负责打开和转换<xref:System.IO.Stream>通过加载资源文件直接到使用代码的类型的属性。  
  
 下面的示例演示如何加载<xref:System.Windows.Controls.Page>直接<xref:System.Windows.Controls.Frame>(`pageFrame`) 使用的代码。  
  
 [!code-csharp[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml.cs#loadpagesoofilefromcode)]
 [!code-vb[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/VisualBasic/ResourcesSample/SOOPage.xaml.vb#loadpagesoofilefromcode)]  
  
 下面的示例是与上例等效的标记。  
  
 [!code-xaml[WPFAssemblyResourcesSnippets#LoadPageSOOFileFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAssemblyResourcesSnippets/CSharp/ResourcesSample/SOOPage.xaml#loadpagesoofilefromxaml)]  
  
<a name="Rebuilding_after_Changing_Build_Type"></a>   
## <a name="rebuilding-after-changing-build-type"></a>更改生成类型后重新生成  
 在更改应用程序数据文件的生成类型后，需要重新生成整个应用程序以确保应用这些更改。 如果只生成应用程序，则不会应用更改。  
  
## <a name="see-also"></a>请参阅
- [WPF 中的 Pack URI](pack-uris-in-wpf.md)
