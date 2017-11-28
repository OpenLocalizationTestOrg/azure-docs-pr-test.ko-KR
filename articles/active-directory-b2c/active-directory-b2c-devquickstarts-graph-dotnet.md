---
title: "Azure Active Directory B2C: 사용 하 여 hello Graph API | Microsoft Docs"
description: "어떻게 toocall hello Graph API B2C 테 넌 트에 대 한 응용 프로그램 identity tooautomate hello 프로세스를 사용 하 여 합니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="986fa-103">Azure AD B2C: hello Graph API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="986fa-104">Azure (Azure AD) Active Directory B2C 테 넌 트에 매우 큰 toobe는 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="986fa-105">즉, 여러 가지 일반적인 테 넌 트 관리 작업 toobe 프로그래밍 방식으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="986fa-106">주요 예제는 사용자 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-106">A primary example is user management.</span></span> <span data-ttu-id="986fa-107">기존 사용자 저장소 tooa B2C 테 넌 트 toomigrate를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="986fa-108">사용자 등록 toohost 고유한 페이지에서 원하는 수 고 hello 백그라운드 Azure AD B2C 디렉터리에 사용자 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="986fa-109">이러한 유형의 작업 필요 hello 기능 toocreate, 읽기, 업데이트 및 사용자 계정을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="986fa-110">Hello Azure AD Graph API를 사용 하 여 이러한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="986fa-111">B2C 테 넌 트의 두 가지 기본 방식 hello Graph API와의 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="986fa-112">대화형, 한 번 실행 작업에 대 한 hello 작업을 수행할 때 hello B2C 테 넌 트의 관리자 계정으로 작동 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="986fa-113">이 모드는 해당 관리자는 모든 호출 toohello Graph API를 수행 하려면 먼저 자격 증명을 사용 하는 관리자 toosign이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="986fa-114">자동화 되 고 연속 작업에 대 한 hello 필요한 권한 tooperform 관리 작업과 일부 사용자가 제공한 서비스 계정 유형에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="986fa-115">Azure AD 응용 프로그램을 등록 및 tooAzure AD를 인증 하 여이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="986fa-116">사용 하 여 이렇게는 **응용 프로그램 ID** hello를 사용 하 여 [OAuth 2.0 클라이언트 자격 증명 부여](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="986fa-117">이 경우 hello 응용 프로그램 역할을 사용자가 아니라 자체 toocall hello Graph API 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="986fa-118">이 문서의 내용에 대해 설명 합니다 방법을 tooperform hello 자동화 된 사용 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="986fa-119">.NET 4.5 빌드합니다 toodemonstrate, `B2CGraphClient` 을 수행 하지 않는 사용자 만들기, 읽기, 업데이트 및 삭제 (CRUD) 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="986fa-120">클라이언트 hello tooinvoke 수 있는 Windows 명령줄 인터페이스 (CLI) 다양 한 메서드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="986fa-121">그러나 hello 코드 toobehave는 비 대화형, 자동화 된 방식으로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="986fa-122">Azure AD B2C 테넌트 가져오기</span><span class="sxs-lookup"><span data-stu-id="986fa-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="986fa-123">응용 프로그램 또는 사용자를 만들거나 전혀 Azure AD와 상호 작용할 수 있습니다, 전에 hello 테 넌 트의 전역 관리자 계정 및 Azure AD B2C 테 넌 트가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="986fa-124">테넌트가 없는 경우 [Azure AD B2C를 시작](active-directory-b2c-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="986fa-125">테넌트에서 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="986fa-125">Register your application in your tenant</span></span>
<span data-ttu-id="986fa-126">B2C 테 넌 트를 만든 후 필요한 tooregister hello 통해 응용 프로그램 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="986fa-127">B2C 테 넌 트와 toouse hello Graph API를 해야 tooregister 전용된 응용 프로그램을 제네릭 hello를 사용 하 여 *앱 등록* hello Azure 포털에에서 블레이드 **하지** Azure AD B2C  *응용 프로그램* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="986fa-128">Hello 기존의 B2C 응용 프로그램을 Azure AD B2C hello에 등록을 다시 사용할 수 없습니다 *응용 프로그램* 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="986fa-129">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="986fa-130">Hello hello 페이지의 맨 위 오른쪽 모서리에서 사용자 계정을 선택 하 여 Azure AD B2C 테 넌 트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="986fa-131">Hello 왼쪽의 탐색 창에서 선택 **더 서비스**, 클릭 **앱 등록**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="986fa-132">Hello 화면에 따라 수행 하 고 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="986fa-133">선택 **웹 응용 프로그램 / API** 응용 프로그램 종류 hello으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="986fa-134">이 예제와 관련이 없지만 **모든 리디렉션 URI**(예: https://B2CGraphAPI )를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="986fa-135">hello 응용 프로그램이 지금 표시, 응용 프로그램의 hello 목록에서 클릭 하 여 조치 tooobtain hello **응용 프로그램 ID** (클라이언트 ID 라고도 함).</span><span class="sxs-lookup"><span data-stu-id="986fa-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="986fa-136">이후 섹션에서 필요하므로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="986fa-137">Hello 설정 블레이드에서 클릭 **키** 고 (클라이언트 비밀 라고도 함) 새 키를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="986fa-138">또한 뒤에 나오는 섹션에서 사용하기 위해 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="986fa-139">응용 프로그램에 대한 만들기, 읽기 및 업데이트 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="986fa-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="986fa-140">모든 hello 프로그램 응용 프로그램 tooget 필요한 사용 권한을 toocreate tooconfigure 필요한 이제, 읽기, 업데이트 및 사용자를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="986fa-141">계속 Azure 포털의 응용 프로그램 등록 블레이드 hello, 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="986fa-142">Hello 설정 블레이드에서 클릭 **필요한 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="986fa-143">Hello 필요한 사용 권한이 블레이드에서 클릭 **Windows Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="986fa-144">Hello 액세스 사용 블레이드에서 hello 선택 **디렉터리 데이터 읽기 및 쓰기** 선점을 **응용 프로그램 사용 권한** 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="986fa-145">마지막으로 다시 hello 필요한 사용 권한이 블레이드 클릭 hello **사용 권한 부여** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="986fa-146">B2C 테 넌 트에서 사용 toocreate, 읽기 및 업데이트 사용자는 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="986fa-147">응용 프로그램에 대한 삭제 권한 구성</span><span class="sxs-lookup"><span data-stu-id="986fa-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="986fa-148">현재 hello *디렉터리 데이터 읽기 및 쓰기* 권한 않습니다 **하지** hello 기능 toodo 사용자를 삭제 하는 등 모든 삭제 항목을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="986fa-149">응용 프로그램 hello 기능 toodelete 사용자가 toogive 하려는 toodo PowerShell와 관련 된 다음 추가 단계 필요 합니다, 그리고 그렇지 않으면 toohello 다음 섹션을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="986fa-150">먼저 다운로드 하 여 hello 설치 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="986fa-151">다운로드 하 고 hello 설치 [Windows PowerShell 용 Azure Active Directory 모듈을 64 비트](http://go.microsoft.com/fwlink/p/?linkid=236297)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="986fa-152">Hello PowerShell 모듈을 설치한 후 PowerShell을 열고 tooyour B2C 테 넌 트를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="986fa-153">실행 한 후 `Get-Credential`, 사용자 이름 및 암호, Enter hello 사용자 이름 및 B2C 테 넌 트 관리자 계정의 암호를 묻는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="986fa-154">Toouse는 B2C 테 넌 트 관리자 계정으로 필요한 **로컬** toohello B2C 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="986fa-155">이러한 계정은 다음과 같습니다. myusername@myb2ctenant.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="986fa-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="986fa-156">Hello에서는 이제 **응용 프로그램 ID** hello 스크립트 tooassign hello 응용 프로그램 hello 사용자 계정 관리자 역할 toodelete 사용자 있게 해 주는 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="986fa-157">이러한 역할 없으므로 잘 알려진 식별자를 입력 하기만 하면 toodo 프로그램 **응용 프로그램 ID** hello 스크립트 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="986fa-158">이제 응용 프로그램 B2C 테 넌 트에서 toodelete 사용자 사용 권한에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="986fa-159">다운로드, 구성 및 hello 샘플 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="986fa-160">먼저, hello 샘플 코드를 다운로드 하 고 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="986fa-161">그런 다음 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="986fa-162">있습니다 수 [hello 샘플 코드를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="986fa-163">사용자가 선택한 디렉터리에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="986fa-164">열기 hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio에서 Visual Studio 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="986fa-165">Hello에 `B2CGraphClient` 프로젝트, 열기 hello 파일 `App.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="986fa-166">Hello 세 가지 응용 프로그램 설정이 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="986fa-167">그런 다음 마우스 오른쪽 단추로 클릭 hello `B2CGraphClient` hello 샘플 솔루션 및 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="986fa-168">성공하는 경우 `B2C.exe` 실행 파일이 `B2CGraphClient\bin\Debug`에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="986fa-169">Hello Graph API를 사용 하 여 사용자 CRUD 작업 작성</span><span class="sxs-lookup"><span data-stu-id="986fa-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="986fa-170">toouse hello B2CGraphClient를 열고는 `cmd` Windows 명령 메시지를 표시 하 고 디렉터리 toohello 변경 `Debug` 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="986fa-171">그러고 나 서 hello `B2C Help` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="986fa-172">각 명령에 대한 간략한 설명을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-172">This will display a brief description of each command.</span></span> <span data-ttu-id="986fa-173">이러한 명령 중 하나를 호출할 때마다 `B2CGraphClient` 요청 toohello Azure AD Graph API를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="986fa-174">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="986fa-174">Get an access token</span></span>
<span data-ttu-id="986fa-175">모든 요청 toohello Graph API 인증에는 액세스 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="986fa-176">`B2CGraphClient`사용 하 여 hello 오픈 소스 Active Directory 인증 라이브러리 (ADAL) toohelp 액세스 토큰을 획득 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="986fa-177">ADAL을 사용하면 간단한 API를 제공하고 액세스 토큰의 캐싱과 같은 중요한 일부 세부 정보를 처리하여 토큰을 쉽게 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="986fa-178">그러나 toouse ADAL tooget 토큰 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="986fa-179">HTTP 요청을 선별하여 토큰을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="986fa-180">이 코드에에서 사용 하 여 ADAL v2 hello Graph API가 있는 주문 toocommunicate 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="986fa-181">Hello Azure AD Graph API와 함께 사용할 수 있는 순서 tooget 액세스 토큰에 v3 또는 v 2 ADAL을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="986fa-182">때 `B2CGraphClient` 실행 hello의 인스턴스를 만들고 `B2CGraphClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="986fa-183">이 클래스에 대 한 hello 생성자는 ADAL 인증 스 캐 폴딩 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="986fa-184">Hello에서는 `B2C Get-User` 예를 들어 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="986fa-185">때 `B2C Get-User` 추가 입력을 hello CLI 호출 hello 없이 호출 `B2CGraphClient.GetAllUsers(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="986fa-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="986fa-186">이 메서드를 호출 `B2CGraphClient.SendGraphGetRequest(...)`, Graph API는 HTTP GET 요청 toohello를 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="986fa-187">전에 `B2CGraphClient.SendGraphGetRequest(...)` 보냅니다 GET 요청을 hello를 먼저 가져옵니다 액세스 토큰 ADAL을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="986fa-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="986fa-188">있습니다 수 액세스 토큰 가져오기 ADAL hello 호출 하 여 hello Graph API에 대 한 `AuthenticationContext.AcquireToken(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="986fa-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="986fa-189">ADAL 다음 반환 된 `access_token` hello 응용 프로그램의 id를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="986fa-190">사용자 읽기</span><span class="sxs-lookup"><span data-stu-id="986fa-190">Read users</span></span>
<span data-ttu-id="986fa-191">HTTP를 보낼 수 tooget 사용자의 목록을 원하는 또는 hello Graph API에서에서 특정 사용자를 가져올 때 `GET` toohello 요청 `/users` 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="986fa-192">모든 테 넌 트에 사용자가 hello에 대 한 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="986fa-193">toosee이이 요청을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="986fa-194">중요 한 사항이 toonote 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-194">There are two important things toonote:</span></span>

* <span data-ttu-id="986fa-195">hello ADAL을 통해 획득 하는 액세스 토큰은 추가 toohello `Authorization` hello를 사용 하 여 헤더 `Bearer` 구성표입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="986fa-196">B2C 테 넌 트의 hello 쿼리 매개 변수를 사용 해야 `api-version=1.6`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="986fa-197">Hello에서 처리 되는 이러한 세부 정보 중 둘 다 `B2CGraphClient.SendGraphGetRequest(...)` 메서드:</span><span class="sxs-lookup"><span data-stu-id="986fa-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="986fa-198">소비자 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="986fa-198">Create consumer user accounts</span></span>
<span data-ttu-id="986fa-199">HTTP를 보낼 수 B2C 테 넌 트의 사용자 계정을 만들면 `POST` toohello 요청 `/users` 끝점:</span><span class="sxs-lookup"><span data-stu-id="986fa-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="986fa-200">이 요청에서 이러한 속성 중 대부분은 필요한 toocreate 소비자 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="986fa-201">toolearn 더 클릭 [여기](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="986fa-202">해당 hello 참고 `//` 주석 예시용 포함 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="986fa-203">실제 요청에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="986fa-204">hello 다음 명령 중 하나를 실행 toosee hello 요청:</span><span class="sxs-lookup"><span data-stu-id="986fa-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="986fa-205">hello `Create-User` 명령은 입력된 매개 변수로.json 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="986fa-206">이는 사용자 개체의 JSON 표현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="986fa-207">Hello 샘플 코드에서 두 개의 샘플.json 파일 없는: `usertemplate-email.json` 및 `usertemplate-username.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="986fa-208">이러한 파일 toosuit 요구에 맞게 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="986fa-209">또한 toohello 필요한 위의 필드, 사용할 수 있는 여러 가지 선택적 필드는 이러한 파일에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="986fa-210">Hello에 hello 선택적 필드에 대 한 내용은 있습니다 [Azure AD Graph API 엔터티 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="986fa-211">Hello POST 요청에 생성 되는 방식을 볼 수 `B2CGraphClient.SendGraphPostRequest(...)`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="986fa-212">액세스 토큰 toohello 첨부 `Authorization` hello 요청의 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="986fa-213">`api-version=1.6`을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="986fa-214">Hello hello 요청 본문에 hello JSON 사용자 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="986fa-215">기존 사용자 저장소에서 toomigrate hello 보다 낮은 암호 강도 하려는 경우는 hello 계정 [Azure AD B2C에 의해 적용 하는 강력한 암호 강도](https://msdn.microsoft.com/library/azure/jj943764.aspx), hello를사용하여hello강력한암호요구사항을사용하지않도록설정할`DisableStrongPassword`hello 값 `passwordPolicies` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="986fa-216">Hello를 수정할 수는 예를 들어, 다음과 같이 위에 제공 된 사용자 요청 만들기: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="986fa-217">소비자 사용자 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="986fa-217">Update consumer user accounts</span></span>
<span data-ttu-id="986fa-218">사용자 개체를 업데이트할 때 hello 프로세스는 비슷한 toohello toocreate 사용자 개체를 사용 하는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="986fa-219">이 프로세스는 hello HTTP를 사용 하지만 `PATCH` 메서드:</span><span class="sxs-lookup"><span data-stu-id="986fa-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="986fa-220">JSON 파일을 새 데이터로 업데이트 하면 tooupdate 사용자를 시도 하십시오.</span><span class="sxs-lookup"><span data-stu-id="986fa-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="986fa-221">사용할 수 있습니다 `B2CGraphClient` toorun 이러한 명령 중 하나:</span><span class="sxs-lookup"><span data-stu-id="986fa-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="986fa-222">Hello 검사 `B2CGraphClient.SendGraphPatchRequest(...)` 메서드는 방법에 대 한 자세한 내용은 toosend이이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="986fa-223">사용자 검색</span><span class="sxs-lookup"><span data-stu-id="986fa-223">Search users</span></span>
<span data-ttu-id="986fa-224">여러 가지 방법으로 B2C 테넌트에서 사용자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="986fa-225">Hello 사용자의 개체 ID 또는 hello 사용자의 로그인 식별자를 사용 하 여 2를 사용 하 여 하나 (예: hello `signInNames` 속성).</span><span class="sxs-lookup"><span data-stu-id="986fa-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="986fa-226">Hello 특정 사용자에 대 한 명령을 toosearch 다음 중 하나를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="986fa-227">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="986fa-228">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="986fa-228">Delete users</span></span>
<span data-ttu-id="986fa-229">사용자를 삭제 하기 위한 hello 과정은 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="986fa-230">사용 하 여 hello HTTP `DELETE` hello로 hello URL 구문 및 메서드는 개체 ID를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="986fa-231">예를 들어 toosee이 명령과 보기 hello delete 요청을 인쇄 toohello 콘솔 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="986fa-232">Hello 검사 `B2CGraphClient.SendGraphDeleteRequest(...)` 메서드는 방법에 대 한 자세한 내용은 toosend이이 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="986fa-233">또한 toouser 관리 hello Azure AD Graph API 사용 하 여 다른 여러 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="986fa-234">[Azure AD Graph API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 는 샘플 요청과 함께 각 작업의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="986fa-235">사용자 지정 특성 사용</span><span class="sxs-lookup"><span data-stu-id="986fa-235">Use custom attributes</span></span>
<span data-ttu-id="986fa-236">대부분의 소비자 응용 프로그램 특정 유형의 사용자 지정 사용자 프로필 정보를 toostore 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="986fa-237">이렇게 하려면 한 가지 방법은 toodefine B2C 테 넌 트의 사용자 지정 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="986fa-238">그런 다음 해당 특성 hello를 처리할 수 있습니다 동일한 방식으로 사용자 개체에 다른 속성을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="986fa-239">Hello 특성을 업데이트할 수 있습니다 hello 특성별 쿼리 hello 속성 삭제 로그인 토큰 등을 클레임으로 hello 특성을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="986fa-240">toodefine B2C 테 넌 트의 사용자 지정 특성 참조 hello [B2C 사용자 지정 특성 참조](active-directory-b2c-reference-custom-attr.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="986fa-241">사용 하 여 B2C 테 넌 트에 정의 된 hello 사용자 지정 특성을 볼 수 있습니다 `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="986fa-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="986fa-242">이러한 함수의 hello 출력 각 사용자 지정 특성의 hello 세부 정보를 같은 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="986fa-243">Hello와 같은 전체 이름에 사용할 수 있습니다 `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, 사용자 개체의 속성으로.</span><span class="sxs-lookup"><span data-stu-id="986fa-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="986fa-244">Hello 새 속성 및 hello 속성에 대 한 값을 가진.json 파일을 업데이트 하 고 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="986fa-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="986fa-245">`B2CGraphClient`를 사용하여 B2C 테넌트 사용자를 프로그래밍 방식으로 관리할 수 있는 서비스 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="986fa-246">`B2CGraphClient`자체 응용 프로그램 identity tooauthenticate toohello Azure AD Graph API를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="986fa-247">또한 클라이언트 암호를 사용하여 토큰을 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="986fa-248">응용 프로그램에 이 기능을 통합할 때 B2C 앱에 대한 몇 가지 주요 사항을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="986fa-249">Toogrant hello 응용 프로그램 hello 적절 한 사용 권한이 필요 hello 테 넌 트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="986fa-250">지금은 toouse ADAL (하지 MSAL) tooget 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="986fa-251">(또한 라이브러리를 사용하지 않고 직접 프로토콜 메시지를 보낼 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="986fa-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="986fa-252">Hello Graph API를 호출할 때 사용 하 여 `api-version=1.6`합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="986fa-253">소비자 사용자를 만들고 업데이트하는 경우 위에서 설명한 대로 필수적인 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="986fa-254">한 질문이 나 원하는 tooperform hello Graph API에서 사용 하 여 작업에 대 한 요청에 있는 경우 B2C 테 넌 트에이 문서에 남길 또는 hello GitHub 코드 샘플 저장소에서 문제를 제출 합니다.</span><span class="sxs-lookup"><span data-stu-id="986fa-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

