---
title: "만든 aaaChanges tooa MVC 프로젝트 tooAzure 광고를 연결 하는 경우 | Microsoft Docs"
description: "Visual Studio가 연결 되어 서비스를 사용 하 여 tooAzure AD를 연결할 때 tooyour MVC 프로젝트 결과 설명 합니다."
services: active-directory
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 5e6d4ce5331eacca5fc83429017ae454fadcc8e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a>어떤 발생 했습니다 toomy MVC 프로젝트 (Visual Studio의 Azure Active Directory 서비스를 연결 하는 데 사용)?
> [!div class="op_single_selector"]
> * [시작](vs-active-directory-dotnet-getting-started.md)
> * [변경된 내용](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>참조가 추가됨
### <a name="nuget-package-references"></a>NuGet 패키지 참조
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>.NET 참조
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>코드가 추가됨
### <a name="code-files-were-added-tooyour-project"></a>Tooyour 프로젝트에 추가 된 코드 파일이
인증 시작 클래스, **App_Start/Startup.Auth.cs** Azure AD 인증에 대 한 시작 논리를 포함 하는 tooyour 프로젝트에 추가 되었습니다. 또한 **SignIn()** 및 **SignOut()** 메서드를 포함하는 컨트롤러 클래스 Controllers/AccountController.cs가 추가되었습니다. 마지막으로 SignIn/SignOut에 대한 작업 링크를 포함하는 부분 뷰 **Views/Shared/_LoginPartial.cshtml**이 추가되었습니다.

### <a name="startup-code-was-added-tooyour-project"></a>시작 코드 tooyour 프로젝트에 추가 된
프로젝트에서 시작 클래스 이미 설치한 경우 hello **구성** 메서드가 업데이트 된 tooinclude 호출 너무**ConfigureAuth(app)**합니다. 그렇지 않은 경우 시작 클래스 tooyour 프로젝트를 추가 되었습니다.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>app.config 또는 web.config에 새 구성 값이 추가됨
구성 항목을 다음 hello 추가 되었습니다.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>Azure AD(Active Directory) 앱이 만들어짐
Azure AD 응용 프로그램은 hello 마법사에서 선택한 hello 디렉터리에서 만들어졌습니다.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a>검사 하는 경우 *개별 사용자 계정 인증을 사용 하지 않도록 설정*, 추가 변경 내용을 toomy 프로젝트?
NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다. 프로젝트의 hello 상태에 따라 toomanually 추가 참조 또는 파일을 제거 하거나 적절 하 게 코드를 수정 해야 합니다.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet 패키지 참조가 제거됨(해당되는 경우)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>코드 파일이 백업 및 제거됨(해당되는 경우)
다음 파일의 각 백업 하 고 hello 프로젝트에서 제거 되었습니다. 백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>코드 파일이 백업됨(해당되는 경우)
교체 전에 다음 파일이 각각 백업되었습니다. 백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a>검사 하는 경우 *디렉터리 데이터 읽기*, 추가 변경 내용을 toomy 프로젝트?
추가 참조가 추가되었습니다.

### <a name="additional-nuget-package-references"></a>추가 NuGet 패키지 참조
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>추가 .NET 참조
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-tooyour-project"></a>추가 코드 파일 tooyour 프로젝트에 추가 된
두 개의 파일을 추가한 toosupport 토큰 캐싱: **Models\ADALTokenCache.cs** 및 **Models\ApplicationDbContext.cs**합니다.  추가 컨트롤러와 뷰 Azure graph Api를 사용 하 여 사용자 프로필 정보에 액세스 하는 tooillustrate를 추가 되었습니다.  해당 파일은 **Controllers\UserProfileController.cs** 및 **Views\UserProfile\Index.cshtml**입니다.

### <a name="additional-startup-code-was-added-tooyour-project"></a>추가 시작 코드가 tooyour 프로젝트에 추가 된
Hello에 **startup.auth.cs** 파일을 새 **OpenIdConnectAuthenticationNotifications** 개체가 toohello 추가 되었으면 **알림** hello 소속  **OpenIdConnectAuthenticationOptions**합니다.  이 hello OAuth 코드를 받아 액세스 토큰에 대 한 교환 tooenable입니다.

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a>Tooyour app.config 또는 web.config에 추가 변경 내용이 적용 된
hello 다음과 같은 추가 구성 항목 추가 되었습니다.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

hello 다음 구성 섹션 및 연결 문자열 추가 되었습니다.

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a>Azure Active Directory 앱이 업데이트됨
Azure Active Directory 앱이 업데이트 된 tooinclude hello *디렉터리 데이터 읽기* hello로 다음 사용 권한 및 추가 키를 만든 *ida: ClientSecret* hello에  **web.config** 파일입니다.

## <a name="next-steps"></a>다음 단계
- [Azure Active Directory에 대한 자세한 정보](https://azure.microsoft.com/services/active-directory/)

