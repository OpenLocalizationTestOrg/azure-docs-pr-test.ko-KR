---
title: "만든 aaaChanges tooa WebApi 프로젝트 tooAzure 광고를 연결 하는 경우 | Microsoft Docs"
description: "Visual Studio를 사용 하 여 AD tooAzure를 연결할 때 tooyour WebApi 프로젝트 결과 설명 합니다."
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
ms.openlocfilehash: 1ea77b6c75b2dc273219fa6c43f02c7a7c5312ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="what-happened-toomy-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="ff71f-103">어떤 발생 했습니다 toomy WebApi 프로젝트 (Visual Studio의 Azure Active Directory 서비스를 연결 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="ff71f-103">What happened toomy WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff71f-104">시작</span><span class="sxs-lookup"><span data-stu-id="ff71f-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="ff71f-105">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="ff71f-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="ff71f-106">참조가 추가됨</span><span class="sxs-lookup"><span data-stu-id="ff71f-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="ff71f-107">NuGet 패키지 참조</span><span class="sxs-lookup"><span data-stu-id="ff71f-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="ff71f-108">.NET 참조</span><span class="sxs-lookup"><span data-stu-id="ff71f-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="ff71f-109">코드 변경 내용</span><span class="sxs-lookup"><span data-stu-id="ff71f-109">Code changes</span></span>
### <a name="code-files-were-added-tooyour-project"></a><span data-ttu-id="ff71f-110">Tooyour 프로젝트에 추가 된 코드 파일이</span><span class="sxs-lookup"><span data-stu-id="ff71f-110">Code files were added tooyour project</span></span>
<span data-ttu-id="ff71f-111">인증 시작 클래스, **App_Start/Startup.Auth.cs** Azure AD 인증에 대 한 시작 논리를 포함 하는 tooyour 프로젝트에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added tooyour project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-tooyour-project"></a><span data-ttu-id="ff71f-112">시작 코드 tooyour 프로젝트에 추가 된</span><span class="sxs-lookup"><span data-stu-id="ff71f-112">Startup code was added tooyour project</span></span>
<span data-ttu-id="ff71f-113">프로젝트에서 시작 클래스 이미 설치한 경우 hello **구성** 메서드가 업데이트 된 tooinclude 호출 너무`ConfigureAuth(app)`합니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-113">If you already had a Startup class in your project, hello **Configuration** method was updated tooinclude a call too`ConfigureAuth(app)`.</span></span> <span data-ttu-id="ff71f-114">그렇지 않은 경우 시작 클래스 tooyour 프로젝트를 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-114">Otherwise, a Startup class was added tooyour project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="ff71f-115">app.config 또는 web.config 파일에 새 구성 값이 추가됨</span><span class="sxs-lookup"><span data-stu-id="ff71f-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="ff71f-116">구성 항목을 다음 hello 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-116">hello following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from hello new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="hello App ID Uri from hello wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="ff71f-117">Azure AD 앱이 만들어짐</span><span class="sxs-lookup"><span data-stu-id="ff71f-117">An Azure AD App was created</span></span>
<span data-ttu-id="ff71f-118">Azure AD 응용 프로그램은 hello 마법사에서 선택한 hello 디렉터리에서 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-118">An Azure AD Application was created in hello directory that you selected in hello wizard.</span></span>

[<span data-ttu-id="ff71f-119">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ff71f-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="ff71f-120">검사 하는 경우 *개별 사용자 계정 인증을 사용 하지 않도록 설정*, 추가 변경 내용을 toomy 프로젝트?</span><span class="sxs-lookup"><span data-stu-id="ff71f-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made toomy project?</span></span>
<span data-ttu-id="ff71f-121">NuGet 패키지 참조가 제거되고 파일이 제거 및 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="ff71f-122">프로젝트의 hello 상태에 따라 toomanually 추가 참조 또는 파일을 제거 하거나 적절 하 게 코드를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-122">Depending on hello state of your project, you may have toomanually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="ff71f-123">NuGet 패키지 참조가 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="ff71f-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="ff71f-124">코드 파일이 백업 및 제거됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="ff71f-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="ff71f-125">다음 파일의 각 백업 하 고 hello 프로젝트에서 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-125">Each of following files was backed up and removed from hello project.</span></span> <span data-ttu-id="ff71f-126">백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-126">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="ff71f-127">코드 파일이 백업됨(해당되는 경우)</span><span class="sxs-lookup"><span data-stu-id="ff71f-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="ff71f-128">교체 전에 다음 파일이 각각 백업되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="ff71f-129">백업 파일은 hello hello 프로젝트의 디렉터리 루트에 '백업' 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-129">Backup files are located in a 'Backup' folder at hello root of hello project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-toomy-project"></a><span data-ttu-id="ff71f-130">검사 하는 경우 *디렉터리 데이터 읽기*, 추가 변경 내용을 toomy 프로젝트?</span><span class="sxs-lookup"><span data-stu-id="ff71f-130">If I checked *Read directory data*, what additional changes were made toomy project?</span></span>
### <a name="additional-changes-were-made-tooyour-appconfig-or-webconfig"></a><span data-ttu-id="ff71f-131">Tooyour app.config 또는 web.config에 추가 변경 내용이 적용 된</span><span class="sxs-lookup"><span data-stu-id="ff71f-131">Additional changes were made tooyour app.config or web.config</span></span>
<span data-ttu-id="ff71f-132">hello 다음과 같은 추가 구성 항목 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-132">hello following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="ff71f-133">Azure Active Directory 앱이 업데이트됨</span><span class="sxs-lookup"><span data-stu-id="ff71f-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="ff71f-134">Azure Active Directory 앱이 업데이트 된 tooinclude hello *디렉터리 데이터 읽기* hello로 다음 사용 권한 및 추가 키를 만든 *ida: 암호* hello에 `web.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ff71f-134">Your Azure Active Directory App was updated tooinclude hello *Read directory data* permission and an additional key was created which was then used as hello *ida:Password* in hello `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff71f-135">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff71f-135">Next steps</span></span>
- [<span data-ttu-id="ff71f-136">Azure Active Directory에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="ff71f-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

