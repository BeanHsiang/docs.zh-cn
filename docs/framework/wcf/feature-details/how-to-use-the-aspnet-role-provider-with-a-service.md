---
title: 如何：与服务一起使用 ASP.NET 角色提供程序
ms.date: 03/30/2017
ms.assetid: 88d33a81-8ac7-48de-978c-5c5b1257951e
ms.openlocfilehash: 0ad581a6967c759095d85d946a8557b47a075355
ms.sourcegitcommit: 6b308cf6d627d78ee36dbbae8972a310ac7fd6c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/23/2019
ms.locfileid: "54658229"
---
# <a name="how-to-use-the-aspnet-role-provider-with-a-service"></a>如何：与服务一起使用 ASP.NET 角色提供程序
[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供程序（与 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格提供程序一起提供）是一种可供 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 开发人员创建网站的功能，这些网站允许用户通过网站创建帐户并向用户分配用于授权的角色。 借助此功能，任何用户都可以通过网站建立帐户，并登录以获取该网站及其服务的独占访问权。 这与要求用户在 Windows 域中具有帐户的 Windows 安全完全不同。 所有提供凭据（用户名/密码组合）的用户都可以使用该站点及其服务。  
  
 示例应用程序，请参阅[成员资格和角色提供程序](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)。 有关详细信息[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]成员资格提供程序功能，请参阅[如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)。  
  
 角色提供程序功能使用 SQL Server 数据库存储用户信息。 Windows Communication Foundation (WCF) 开发人员可以利用这些功能实现安全性。 当集成到 WCF 应用程序，用户必须提供用户名/密码组合到 WCF 客户端应用程序。 若要启用 WCF 以使用的数据库，必须创建的实例<xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>类中，设置其<xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A>属性设置为<xref:System.ServiceModel.Description.PrincipalPermissionMode.UseAspNetRoles>，并将该实例添加到行为集合<xref:System.ServiceModel.ServiceHost>的承载服务。  
  
### <a name="to-configure-the-role-provider"></a>配置角色提供程序  
  
1.  在 Web.config 文件中，在 <`system.web`> 元素中，添加 <`roleManager`> 元素，并设置其`enabled`属性为`true`。  
  
2.  将 `defaultProvider` 属性设置为 `SqlRoleProvider`。  
  
3.  子级作为 <`roleManager`> 元素中，添加 <`providers`> 元素。  
  
4.  子级作为 <`providers`> 元素中，添加 <`add`> 元素具有以下属性设置为适当的值： `name`， `type`， `connectionStringName`，并`applicationName`，如以下示例所示。  
  
    ```xml  
    <!-- Configure the Sql Role Provider. -->  
    <roleManager enabled ="true"   
     defaultProvider ="SqlRoleProvider" >  
       <providers>  
         <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
       </providers>  
    </roleManager>  
    ```  
  
### <a name="to-configure-the-service-to-use-the-role-provider"></a>将服务配置为使用角色提供程序  
  
1.  在 Web.config 文件中，添加[ \<system.serviceModel >](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)元素。  
  
2.  添加[\<行为 >](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)元素 <`system.ServiceModel`> 元素。  
  
3.  添加[ \<serviceBehaviors >](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)到 <`behaviors`> 元素。  
  
4.  添加[\<行为 >](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)元素，并设置`name`属性为适当的值。  
  
5.  添加[ \<serviceAuthorization >](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)到 <`behavior`> 元素。  
  
6.  将 `principalPermissionMode` 属性设置为 `UseAspNetRoles`。  
  
7.  将 `roleProviderName` 属性设置为 `SqlRoleProvider`。 下面的示例演示此配置的一个片段。  
  
    ```xml  
    <behaviors>  
     <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
       <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                             roleProviderName ="SqlRoleProvider" />  
      </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
## <a name="see-also"></a>请参阅
- [成员资格和角色提供程序](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)
- [如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)
