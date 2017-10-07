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
# <a name="what-happened-toomy-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="72a23-103">어떤 발생 했습니다 toomy MVC 프로젝트 (Visual Studio의 Azure Active Directory 서비스를 연결 하는 데 사용)?</span><span class="sxs-lookup"><span data-stu-id="72a23-103">What happened toomy MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72a23-104">시작</span><span class="sxs-lookup"><span data-stu-id="72a23-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="72a23-105">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="72a23-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="72a23-106">참조가 추가됨</span><span class="sxs-lookup"><span data-stu-id="72a23-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="72a23-107">NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="72a23-107">NuGet package references</span></span>
* <span data-ttu-id="72a23-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="72a23-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="72a23-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="72a23-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="72a23-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="72a23-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="72a23-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="72a23-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="72a23-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="72a23-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="72a23-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="72a23-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="72a23-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="72a23-114">**Owin**</span></span>
* <span data-ttu-id="72a23-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="72a23-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="72a23-116">.NET 참조</span><span class="sxs-lookup"><span data-stu-id="72a23-116">.NET references</span></span>
* <span data-ttu-id="72a23-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="72a23-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="72a23-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="72a23-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="72a23-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="72a23-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="72a23-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="72a23-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="72a23-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="72a23-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="72a23-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="72a23-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="72a23-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="72a23-123">**Owin**</span></span>
* <span data-ttu-id="72a23-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="72a23-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="72a23-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="72a23-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="72a23-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="72a23-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="72a23-127">코드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="72a23-127">Code has been added</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="72a23-128">Tooyour 프로젝트에 추가 된 코드 파일이</span><span class="sxs-lookup"><span data-stu-id="72a23-128">Code files were added tooyour project</span></span>
<span data-ttu-id="72a23-129">인증 시작 클래스, **App_Start/Startup.Auth.cs** Azure AD 인증에 대 한 시작 논리를 포함 하는 tooyour 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="72a23-130">또한 **SignIn()** 및 **SignOut()** 메서드를 포함하는 컨트롤러 클래스 Controllers/AccountController.cs가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="72a23-131">마지막으로 SignIn/SignOut에 대한 작업 링크를 포함하는 부분 뷰 **Views/Shared/_LoginPartial.cshtml**이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="72a23-132">시작 코드 tooyour 프로젝트에 추가 된</span><span class="sxs-lookup"><span data-stu-id="72a23-132">Startup code was added tooyour project</span></span>
<span data-ttu-id="72a23-133">프로젝트에서 시작 클래스 이미 설치한 경우 hello **구성** 메서드가 업데이트 된 tooinclude 호출 너무**ConfigureAuth(app)**합니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-133">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too**ConfigureAuth(app)**.</span></span> <span data-ttu-id="72a23-134">그렇지 않은 경우 시작 클래스 tooyour 프로젝트를 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-134">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="72a23-135">app.config 또는 web.config에 새 구성 값이 추가됨</span><span class="sxs-lookup"><span data-stu-id="72a23-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="72a23-136">구성 항목을 다음 hello 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-136">hello following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="hello selected Azure AD Domain" />
        <add key="ida:TenantId" value="hello Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="72a23-137">Azure AD(Active Directory) 앱이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="72a23-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="72a23-138">Azure AD 응용 프로그램은 hello 마법사에서 선택한 hello 디렉터리에서 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-138">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="72a23-139">검사 하는 경우 *개별 사용자 계정 인증을 사용 하지 않도록 설정*, 추가 변경 내용을 toomy 프로젝트?</span><span class="sxs-lookup"><span data-stu-id="72a23-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="72a23-140">NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="72a23-141">프로젝트의 hello 상태에 따라 toomanually 추가 참조 또는 파일을 제거 하거나 적절 하 게 코드를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-141">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="72a23-142">NuGet 패키지 참조가 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="72a23-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="72a23-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="72a23-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="72a23-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="72a23-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="72a23-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="72a23-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="72a23-146">코드 파일이 백업 및 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="72a23-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="72a23-147">다음 파일의 각 백업 하 고 hello 프로젝트에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-147">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="72a23-148">백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-148">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="72a23-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="72a23-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="72a23-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="72a23-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="72a23-153">코드 파일이 백업됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="72a23-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="72a23-154">교체 전에 다음 파일이 각각 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="72a23-155">백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-155">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* <span data-ttu-id="72a23-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-156">**Startup.cs**</span></span>
* <span data-ttu-id="72a23-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="72a23-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="72a23-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="72a23-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="72a23-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="72a23-160">검사 하는 경우 *디렉터리 데이터 읽기*, 추가 변경 내용을 toomy 프로젝트?</span><span class="sxs-lookup"><span data-stu-id="72a23-160">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="72a23-161">추가 참조가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="72a23-162">추가 NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="72a23-162">Additional NuGet package references</span></span>
* <span data-ttu-id="72a23-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="72a23-163">**EntityFramework**</span></span>
* <span data-ttu-id="72a23-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="72a23-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="72a23-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="72a23-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="72a23-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="72a23-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="72a23-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="72a23-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="72a23-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="72a23-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="72a23-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="72a23-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="72a23-170">추가 .NET 참조</span><span class="sxs-lookup"><span data-stu-id="72a23-170">Additional .NET references</span></span>
* <span data-ttu-id="72a23-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="72a23-171">**EntityFramework**</span></span>
* <span data-ttu-id="72a23-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="72a23-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="72a23-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="72a23-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="72a23-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="72a23-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="72a23-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="72a23-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="72a23-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="72a23-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="72a23-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="72a23-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="72a23-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="72a23-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="72a23-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="72a23-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-tooyour-project"></a><span data-ttu-id="72a23-180">추가 코드 파일 tooyour 프로젝트에 추가 된</span><span class="sxs-lookup"><span data-stu-id="72a23-180">Additional Code files were added tooyour project</span></span>
<span data-ttu-id="72a23-181">두 개의 파일을 추가한 toosupport 토큰 캐싱: **Models\ADALTokenCache.cs** 및 **Models\ApplicationDbContext.cs**합니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-181">Two files were added toosupport token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="72a23-182">추가 컨트롤러와 뷰 Azure graph Api를 사용 하 여 사용자 프로필 정보에 액세스 하는 tooillustrate를 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-182">An additional controller and view were added tooillustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="72a23-183">해당 파일은 **Controllers\UserProfileController.cs** 및 **Views\UserProfile\Index.cshtml**입니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-tooyour-project"></a><span data-ttu-id="72a23-184">추가 시작 코드가 tooyour 프로젝트에 추가 된</span><span class="sxs-lookup"><span data-stu-id="72a23-184">Additional Startup code was added tooyour project</span></span>
<span data-ttu-id="72a23-185">Hello에 **startup.auth.cs** 파일을 새 **OpenIdConnectAuthenticationNotifications** 개체가 toohello 추가 되었으면 **알림** hello 소속  **OpenIdConnectAuthenticationOptions**합니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-185">In hello **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added toohello **Notifications** member of hello **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="72a23-186">이 hello OAuth 코드를 받아 액세스 토큰에 대 한 교환 tooenable입니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-186">This is tooenable receiving hello OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="72a23-187">Tooyour app.config 또는 web.config에 추가 변경 내용이 적용 된</span><span class="sxs-lookup"><span data-stu-id="72a23-187">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="72a23-188">hello 다음과 같은 추가 구성 항목 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-188">hello following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="72a23-189">hello 다음 구성 섹션 및 연결 문자열 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-189">hello following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="72a23-190">Azure Active Directory 앱이 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="72a23-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="72a23-191">Azure Active Directory 앱이 업데이트 된 tooinclude hello *디렉터리 데이터 읽기* hello로 다음 사용 권한 및 추가 키를 만든 *ida: ClientSecret* hello에  **web.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="72a23-191">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:ClientSecret* in hello **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="72a23-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="72a23-192">Next steps</span></span>
- [<span data-ttu-id="72a23-193">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="72a23-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

