---
title: "hello Azure Active Directory 연결 마법사를 사용 하 여 aaaHow toodiagnose 오류"
description: "hello active directory 연결 마법사가 호환 되지 않는 인증 유형 검색"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a><span data-ttu-id="fcc1c-103">Hello Azure Active Directory 연결 마법사를 사용 하 여 오류 진단</span><span class="sxs-lookup"><span data-stu-id="fcc1c-103">Diagnosing errors with hello Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="fcc1c-104">이전 인증 코드를 검색 하는 동안 hello 마법사에는 호환 되지 않는 인증 형식을 검색 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-104">While detecting previous authentication code, hello wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="fcc1c-105">무엇을 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="fcc1c-105">What is being checked?</span></span>
<span data-ttu-id="fcc1c-106">**참고:** toocorrectly 프로젝트에서 이전 인증 코드를 검색할 hello 프로젝트를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-106">**Note:** toocorrectly detect previous authentication code in a project, hello project must be built.</span></span>  <span data-ttu-id="fcc1c-107">이 오류가 발생했고 프로젝트에 이전 인증 코드가 없는 경우 다시 작성한 다음 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="fcc1c-108">프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="fcc1c-108">Project Types</span></span>
<span data-ttu-id="fcc1c-109">hello 마법사 hello 형식의 hello 프로젝트로 hello 오른쪽 인증 논리를 삽입할 수 있으므로 개발 하는 프로젝트를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-109">hello wizard checks hello type of project you’re developing so it can inject hello right authentication logic into hello project.</span></span>  <span data-ttu-id="fcc1c-110">파생 되는 컨트롤러가 `ApiController` hello 프로젝트 hello 프로젝트에 WebAPI 프로젝트도 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-110">If there is any controller that derives from `ApiController` in hello project, hello project is considered a WebAPI project.</span></span>  <span data-ttu-id="fcc1c-111">파생 되는 컨트롤러에만 있는 경우 `MVC.Controller` hello 프로젝트 hello 프로젝트에 MVC 프로젝트도 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-111">If there are only controllers that derive from `MVC.Controller` in hello project, hello project is considered an MVC project.</span></span>  <span data-ttu-id="fcc1c-112">그 외 모든 hello 마법사에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-112">Anything else is not supported by hello wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="fcc1c-113">호환 가능한 인증 코드</span><span class="sxs-lookup"><span data-stu-id="fcc1c-113">Compatible Authentication Code</span></span>
<span data-ttu-id="fcc1c-114">또한 hello 마법사 hello 마법사로 이전에 구성 된 또는 hello 마법사와 호환 되는 인증 설정을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-114">hello wizard also checks for authentication settings that have been previously configured with hello wizard or are compatible with hello wizard.</span></span>  <span data-ttu-id="fcc1c-115">모든 설정이 있으면 재진입용 경우 것으로 간주 됩니다 및 hello 마법사가 열리고 hello 설정을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-115">If all settings are present, it is considered a re-entrant case, and hello wizard opens display hello settings.</span></span>  <span data-ttu-id="fcc1c-116">Hello 설정의 일부 값이 있는 경우에 오류 사례를 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-116">If only some of hello settings are present, it is considered an error case.</span></span>

<span data-ttu-id="fcc1c-117">MVC 프로젝트에서 hello 마법사 hello 설정을 hello 마법사의 이전 사용 결과로 생성 되는 다음 중 하나에 대 한 확인:</span><span class="sxs-lookup"><span data-stu-id="fcc1c-117">In an MVC project, hello wizard checks for any of hello following settings, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="fcc1c-118">또한 hello 마법사 hello hello 마법사의 이전 사용 결과로 생성 되는 설정은 웹 API 프로젝트에서 다음 중 하나에 대 한 확인:</span><span class="sxs-lookup"><span data-stu-id="fcc1c-118">In addition, hello wizard checks for any of hello following settings in a Web API project, which result from previous use of hello wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="fcc1c-119">호환되지 않는 인증 코드</span><span class="sxs-lookup"><span data-stu-id="fcc1c-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="fcc1c-120">마지막으로, hello 마법사는 이전 버전의 Visual Studio로 구성 된 toodetect 버전의 인증 코드를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-120">Finally, hello wizard attempts toodetect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="fcc1c-121">이 오류가 발생한 경우에는 프로젝트에 호환되지 않는 인증 코드가 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="fcc1c-122">hello 마법사 hello를 유형의 인증 이전 버전의 Visual Studio에서 다음을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-122">hello wizard detects hello following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="fcc1c-123">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="fcc1c-123">Windows Authentication</span></span> 
* <span data-ttu-id="fcc1c-124">개별 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="fcc1c-124">Individual User Accounts</span></span> 
* <span data-ttu-id="fcc1c-125">조직 계정</span><span class="sxs-lookup"><span data-stu-id="fcc1c-125">Organizational Accounts</span></span> 

<span data-ttu-id="fcc1c-126">hello에 대 한 MVC 프로젝트에 Windows 인증을 toodetect, hello 마법사에서는 `authentication` 요소에서 사용자 **web.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-126">toodetect Windows Authentication in an MVC project, hello wizard looks for hello `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="fcc1c-127">hello에 대 한 웹 API 프로젝트에 Windows 인증을 toodetect, hello 마법사에서는 `IISExpressWindowsAuthentication` 프로젝트의 요소 **.csproj** 파일:</span><span class="sxs-lookup"><span data-stu-id="fcc1c-127">toodetect Windows Authentication in a Web API project, hello wizard looks for hello `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="fcc1c-128">hello 패키지 요소에 대 한 toodetect 개별 사용자 계정 인증 hello 마법사에서는 프로그램 **Packages.config** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-128">toodetect Individual User Accounts authentication, hello wizard looks for hello package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="fcc1c-129">요소 다음에 오는 hello에 대 한 오래 된 형태의 조직 계정 인증 toodetect hello 마법사에서는 **web.config**:</span><span class="sxs-lookup"><span data-stu-id="fcc1c-129">toodetect an old form of Organizational Account authentication, hello wizard looks for hello following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="fcc1c-130">toochange hello 인증 유형을 hello 호환 되지 않는 인증 유형을 제거 하 고 hello 마법사를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-130">toochange hello authentication type, remove hello incompatible authentication type and run hello wizard again.</span></span>

<span data-ttu-id="fcc1c-131">자세한 내용은 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fcc1c-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="fcc1c-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="fcc1c-132">Next steps</span></span>
- [<span data-ttu-id="fcc1c-133">Azure AD의 인증 시나리오</span><span class="sxs-lookup"><span data-stu-id="fcc1c-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)