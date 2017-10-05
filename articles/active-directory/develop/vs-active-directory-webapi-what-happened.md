---
title: "Azure AD에 연결할 때의 WebApi 프로젝트 변경 내용 | Microsoft Docs"
description: "Visual Studio를 사용하여 Azure AD에 연결할 때 프로젝트 WebApi에서 변경되는 사항에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 086e5a9622cad681cd282345d97e0c28ee7de2fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="307f5-103">내 WebApi 프로젝트(Visual Studio Azure Active Directory 연결 서비스)의 변경 내용</span><span class="sxs-lookup"><span data-stu-id="307f5-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="307f5-104">시작</span><span class="sxs-lookup"><span data-stu-id="307f5-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="307f5-105">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="307f5-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="307f5-106">참조가 추가됨</span><span class="sxs-lookup"><span data-stu-id="307f5-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="307f5-107">NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="307f5-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="307f5-108">.NET 참조</span><span class="sxs-lookup"><span data-stu-id="307f5-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="307f5-109">코드 변경 내용</span><span class="sxs-lookup"><span data-stu-id="307f5-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="307f5-110">프로젝트에 코드 파일이 추가됨</span><span class="sxs-lookup"><span data-stu-id="307f5-110">Code files were added to your project</span></span>
<span data-ttu-id="307f5-111">Azure AD 인증에 대한 시작 논리가 포함된 인증 시작 클래스 **App_Start/Startup.Auth.cs**가 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="307f5-112">프로젝트에 시작 코드가 추가됨</span><span class="sxs-lookup"><span data-stu-id="307f5-112">Startup code was added to your project</span></span>
<span data-ttu-id="307f5-113">프로젝트에 시작 클래스가 이미 있는 경우 **Configuration** 메서드가 업데이트되어 `ConfigureAuth(app)`에 대한 호출이 해당 메서드에 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="307f5-114">그렇지 않으면 시작 클래스가 프로젝트에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="307f5-115">app.config 또는 web.config 파일에 새 구성 값이 추가됨</span><span class="sxs-lookup"><span data-stu-id="307f5-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="307f5-116">다음 구성 항목이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="307f5-117">Azure AD 앱이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="307f5-117">An Azure AD App was created</span></span>
<span data-ttu-id="307f5-118">마법사에서 선택한 디렉터리에 Azure AD 응용 프로그램이 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="307f5-119">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="307f5-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="307f5-120">*개별 사용자 계정 인증을 사용하지 않도록 설정*한 경우 내 프로젝트에 추가된 변경 내용은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="307f5-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="307f5-121">NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="307f5-122">프로젝트의 상태에 따라 수동으로 추가 참조 또는 파일을 제거하거나 적절하게 코드를 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="307f5-123">NuGet 패키지 참조가 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="307f5-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="307f5-124">코드 파일이 백업 및 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="307f5-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="307f5-125">다음 파일이 각각 프로젝트에서 백업 및 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="307f5-126">백업 파일은 프로젝트 디렉터리의 루트에 있는 'Backup' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="307f5-127">코드 파일이 백업됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="307f5-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="307f5-128">교체 전에 다음 파일이 각각 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="307f5-129">백업 파일은 프로젝트 디렉터리의 루트에 있는 'Backup' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="307f5-130">*디렉터리 데이터 읽기*를 선택한 경우 내 프로젝트에 추가된 변경 내용은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="307f5-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="307f5-131">app.config 또는 web.config에 변경 내용 추가됨</span><span class="sxs-lookup"><span data-stu-id="307f5-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="307f5-132">다음 추가 구성 항목이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="307f5-133">Azure Active Directory 앱이 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="307f5-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="307f5-134">Azure Active Directory 앱이 *디렉터리 데이터 읽기* 권한을 포함하도록 업데이트되었으며, 추가 키가 생성되어 `web.config` 파일에서 *ida:Password*로 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="307f5-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="307f5-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="307f5-135">Next steps</span></span>
- [<span data-ttu-id="307f5-136">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="307f5-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

