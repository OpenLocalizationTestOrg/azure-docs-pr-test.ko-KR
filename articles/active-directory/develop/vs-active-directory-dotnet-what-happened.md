---
title: "Azure AD에 연결할 때의 MVC 프로젝트 변경 내용 | Microsoft Docs"
description: "Visual Studio 연결된 서비스를 사용하여 Azure AD에 연결할 때 MVC 프로젝트의 변경 내용을 설명합니다."
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
ms.openlocfilehash: 095411a7fc854f4dce11921adb0f57c5389a8e13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="394ea-103">내 MVC 프로젝트(Visual Studio Azure Active Directory 연결된 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="394ea-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="394ea-104">시작</span><span class="sxs-lookup"><span data-stu-id="394ea-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="394ea-105">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="394ea-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="394ea-106">참조가 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="394ea-107">NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="394ea-107">NuGet package references</span></span>
* <span data-ttu-id="394ea-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="394ea-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="394ea-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="394ea-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="394ea-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="394ea-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="394ea-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="394ea-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="394ea-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="394ea-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="394ea-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="394ea-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="394ea-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="394ea-114">**Owin**</span></span>
* <span data-ttu-id="394ea-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="394ea-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="394ea-116">.NET 참조</span><span class="sxs-lookup"><span data-stu-id="394ea-116">.NET references</span></span>
* <span data-ttu-id="394ea-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="394ea-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="394ea-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="394ea-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="394ea-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="394ea-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="394ea-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="394ea-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="394ea-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="394ea-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="394ea-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="394ea-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="394ea-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="394ea-123">**Owin**</span></span>
* <span data-ttu-id="394ea-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="394ea-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="394ea-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="394ea-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="394ea-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="394ea-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="394ea-127">코드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="394ea-128">프로젝트에 코드 파일이 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-128">Code files were added to your project</span></span>
<span data-ttu-id="394ea-129">Azure AD 인증에 대한 시작 논리가 포함된 인증 시작 클래스 **App_Start/Startup.Auth.cs**가 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="394ea-130">또한 **SignIn()** 및 **SignOut()** 메서드를 포함하는 컨트롤러 클래스 Controllers/AccountController.cs가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="394ea-131">마지막으로 SignIn/SignOut에 대한 작업 링크를 포함하는 부분 뷰 **Views/Shared/_LoginPartial.cshtml**이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="394ea-132">프로젝트에 시작 코드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-132">Startup code was added to your project</span></span>
<span data-ttu-id="394ea-133">프로젝트에 시작 클래스가 이미 있는 경우 **Configuration** 메서드가 업데이트되어 **ConfigureAuth(app)**에 대한 호출이 해당 메서드에 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="394ea-134">그렇지 않으면 시작 클래스가 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="394ea-135">app.config 또는 web.config에 새 구성 값이 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="394ea-136">다음 구성 항목이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="394ea-137">Azure AD(Active Directory) 앱이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="394ea-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="394ea-138">마법사에서 선택한 디렉터리에 Azure AD 응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="394ea-139">*개별 사용자 계정 인증을 사용하지 않도록 설정*한 경우 내 프로젝트에 추가된 변경 내용은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="394ea-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="394ea-140">NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="394ea-141">프로젝트의 상태에 따라 수동으로 추가 참조 또는 파일을 제거하거나 적절하게 코드를 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="394ea-142">NuGet 패키지 참조가 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="394ea-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="394ea-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="394ea-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="394ea-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="394ea-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="394ea-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="394ea-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="394ea-146">코드 파일이 백업 및 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="394ea-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="394ea-147">다음 파일이 각각 프로젝트에서 백업 및 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="394ea-148">백업 파일은 프로젝트 디렉터리의 루트에 있는 'Backup' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="394ea-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="394ea-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="394ea-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="394ea-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="394ea-153">코드 파일이 백업됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="394ea-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="394ea-154">교체 전에 다음 파일이 각각 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="394ea-155">백업 파일은 프로젝트 디렉터리의 루트에 있는 'Backup' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="394ea-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-156">**Startup.cs**</span></span>
* <span data-ttu-id="394ea-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="394ea-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="394ea-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="394ea-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="394ea-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="394ea-160">*디렉터리 데이터 읽기*를 선택한 경우 내 프로젝트에 추가된 변경 내용은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="394ea-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="394ea-161">추가 참조가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="394ea-162">추가 NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="394ea-162">Additional NuGet package references</span></span>
* <span data-ttu-id="394ea-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="394ea-163">**EntityFramework**</span></span>
* <span data-ttu-id="394ea-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="394ea-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="394ea-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="394ea-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="394ea-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="394ea-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="394ea-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="394ea-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="394ea-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="394ea-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="394ea-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="394ea-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="394ea-170">추가 .NET 참조</span><span class="sxs-lookup"><span data-stu-id="394ea-170">Additional .NET references</span></span>
* <span data-ttu-id="394ea-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="394ea-171">**EntityFramework**</span></span>
* <span data-ttu-id="394ea-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="394ea-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="394ea-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="394ea-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="394ea-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="394ea-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="394ea-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="394ea-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="394ea-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="394ea-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="394ea-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="394ea-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="394ea-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="394ea-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="394ea-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="394ea-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="394ea-180">프로젝트에 추가 코드 파일이 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="394ea-181">토큰 캐싱을 지원하기 위해 두 파일 **Models\ADALTokenCache.cs** 및 **Models\ApplicationDbContext.cs**가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="394ea-182">추가 컨트롤러와 뷰는 Azure graph API를 사용하여 액세스 사용자 프로필 정보를 설명하기 위해 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="394ea-183">해당 파일은 **Controllers\UserProfileController.cs** 및 **Views\UserProfile\Index.cshtml**입니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="394ea-184">프로젝트에 추가 시작 코드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="394ea-185">**startup.auth.cs** 파일에서 **OpenIdConnectAuthenticationOptions**의 **Notifications** 멤버에 **OpenIdConnectAuthenticationNotifications** 개체가 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="394ea-186">이를 통해 OAuth 코드를 받고 액세스 토큰에 대해 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="394ea-187">app.config 또는 web.config에 변경 내용 추가됨</span><span class="sxs-lookup"><span data-stu-id="394ea-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="394ea-188">다음 추가 구성 항목이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="394ea-189">다음 구성 섹션 및 연결 문자열이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-189">The following configuration sections and connection string have been added.</span></span>

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


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="394ea-190">Azure Active Directory 앱이 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="394ea-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="394ea-191">Azure Active Directory 앱이 *디렉터리 데이터 읽기* 권한을 포함하도록 업데이트되었으며, 추가 키가 생성되어 **web.config** 파일에서 *ida:ClientSecret*으로 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="394ea-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="394ea-192">다음 단계</span><span class="sxs-lookup"><span data-stu-id="394ea-192">Next steps</span></span>
- [<span data-ttu-id="394ea-193">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="394ea-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

