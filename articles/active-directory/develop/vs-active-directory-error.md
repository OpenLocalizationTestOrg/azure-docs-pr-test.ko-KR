---
title: "Azure Active Directory 연결 마법사를 사용하여 오류를 진단하는 방법"
description: "Active Directory 연결 마법사에서 호환되지 않는 인증 유형 검색"
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
ms.openlocfilehash: 4f29f62b2996cae98b02c1ed5fcb59eca09301ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="55f70-103">Azure Active Directory 연결 마법사를 사용하여 오류 진단</span><span class="sxs-lookup"><span data-stu-id="55f70-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="55f70-104">이전 인증 코드를 검색하는 동안 마법사에서 호환되지 않는 인증 유형을 검색했습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="55f70-105">무엇을 확인합니까?</span><span class="sxs-lookup"><span data-stu-id="55f70-105">What is being checked?</span></span>
<span data-ttu-id="55f70-106">**참고:** 프로젝트에서 이전 인증 코드를 제대로 감지 하려면 프로젝트를 빌드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="55f70-107">이 오류가 발생했고 프로젝트에 이전 인증 코드가 없는 경우 다시 작성한 다음 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="55f70-108">프로젝트 형식</span><span class="sxs-lookup"><span data-stu-id="55f70-108">Project Types</span></span>
<span data-ttu-id="55f70-109">이 마법사는 프로젝트에 올바른 인증 논리를 삽입할 수 있도록 사용자가 개발 중인 프로젝트 형식을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="55f70-110">프로젝트의 `ApiController`에서 파생되는 컨트롤러가 있으면 프로젝트가 WebAPI 프로젝트로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="55f70-111">프로젝트의 `MVC.Controller`에서 파생되는 컨트롤러만 있으면 프로젝트가 MVC 프로젝트로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="55f70-112">다른 항목은 이 마법사에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="55f70-113">호환 가능한 인증 코드</span><span class="sxs-lookup"><span data-stu-id="55f70-113">Compatible Authentication Code</span></span>
<span data-ttu-id="55f70-114">또한 이 마법사에서는 이전에 이 마법사로 구성되었거나 이 마법사와 호환되는 인증 설정이 있는지도 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="55f70-115">모든 설정이 있는 경우 재진입 사례로 간주되고 마법사가 열릴 때 해당 설정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="55f70-116">설정이 일부만 있으면 오류 사례로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="55f70-117">MVC 프로젝트에서 이 마법사는 이전에 마법사를 사용한 결과에 따라 다음과 같은 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="55f70-118">또한 이 마법사는 이전에 마법사를 사용한 결과에 따라 다음과 같은 Web API 프로젝트 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="55f70-119">호환되지 않는 인증 코드</span><span class="sxs-lookup"><span data-stu-id="55f70-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="55f70-120">마지막으로, 이 마법사에서는 이전 버전의 Visual Studio를 사용하여 구성된 인증 코드의 버전을 감지하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="55f70-121">이 오류가 발생한 경우에는 프로젝트에 호환되지 않는 인증 코드가 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="55f70-122">마법사에서는 이전 버전의 Visual Studio에서 다음과 같은 인증 유형을 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="55f70-123">Windows 인증</span><span class="sxs-lookup"><span data-stu-id="55f70-123">Windows Authentication</span></span> 
* <span data-ttu-id="55f70-124">개별 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="55f70-124">Individual User Accounts</span></span> 
* <span data-ttu-id="55f70-125">조직 계정</span><span class="sxs-lookup"><span data-stu-id="55f70-125">Organizational Accounts</span></span> 

<span data-ttu-id="55f70-126">MVC 프로젝트에서 Windows 인증을 감지하기 위해 마법사는 사용자의 **web.config** 파일에서 `authentication` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="55f70-127">Web API 프로젝트에서 Windows 인증을 감지하기 위해 마법사는 사용자 프로젝트의 **.csproj** 파일에서 `IISExpressWindowsAuthentication` 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="55f70-128">개별 사용자 계정 인증을 감지하기 위해 마법사는 사용자의 **Packages.config** 파일에서 패키지 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="55f70-129">조직 계정 인증의 이전 양식을 감지하기 위해 마법사는 **web.config**에서 다음 요소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="55f70-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="55f70-130">인증 유형을 변경하려면 호환되지 않는 인증 유형을 제거하고 마법사를 다시 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="55f70-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="55f70-131">자세한 내용은 [Azure AD의 인증 시나리오](active-directory-authentication-scenarios.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="55f70-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="55f70-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="55f70-132">Next steps</span></span>
- [<span data-ttu-id="55f70-133">Azure AD의 인증 시나리오</span><span class="sxs-lookup"><span data-stu-id="55f70-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)