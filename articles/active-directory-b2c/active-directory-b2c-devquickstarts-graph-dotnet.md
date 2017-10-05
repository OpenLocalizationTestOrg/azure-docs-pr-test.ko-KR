---
title: "Azure Active Directory B2C: Graph API 사용 | Microsoft Docs"
description: "프로세스를 자동화하기 위해 응용 프로그램 ID를 사용하여 B2C 테넌트에 Graph API를 호출하는 방법입니다."
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
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="1520c-103">Azure AD B2C: Graph API 사용</span><span class="sxs-lookup"><span data-stu-id="1520c-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="1520c-104">Azure Active Directory(Azure AD) B2C 테넌트는 매우 큰 경향이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="1520c-105">즉, 많은 일반 테넌트 관리 작업을 프로그래밍 방식으로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="1520c-106">주요 예제는 사용자 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-106">A primary example is user management.</span></span> <span data-ttu-id="1520c-107">B2C 테넌트에 기존 사용자 저장소를 마이그레이션해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="1520c-108">고유한 페이지에서 사용자 등록을 호스팅하고 백그라운드에서 Azure AD B2C 디렉터리에 사용자 계정을 만들려고 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="1520c-109">이러한 형식의 태스크는 사용자 계정을 만들고 읽고 업데이트 및 삭제하는 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="1520c-110">Azure AD Graph API를 사용하여 이 태스크를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="1520c-111">B2C 테넌트의 경우 Graph API와 통신하는 두 가지 기본 모드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="1520c-112">대화형인 한 번 실행 작업의 경우 태스크를 수행할 때 B2C 테넌트에서 관리자 계정으로 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="1520c-113">이 모드에서는 관리자가 Graph API에 대한 호출을 수행할 수 있기 전에 해당 관리자가 자격 증명으로 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="1520c-114">자동화된 연속 작업의 경우 필요한 권한을 제공하는 일종의 서비스 계정을 사용하여 관리 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="1520c-115">Azure AD에서 응용 프로그램을 등록하고 Azure AD에 인증하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="1520c-116">**OAuth 2.0 클라이언트 자격 증명 부여** 를 사용하는 [응용 프로그램 ID](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api)를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="1520c-117">이 경우에 응용 프로그램은 사용자로서가 아닌 자체로서 Graph API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="1520c-118">이 기사에서는 자동화된 사용 사례를 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="1520c-119">이를 보여주려면 사용자 만들기, 읽기, 업데이트 및 삭제(CRUD) 작업을 수행하는 .NET 4.5 `B2CGraphClient`을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="1520c-120">클라이언트에는 다양한 메서드를 호출할 수 있도록 하는 Windows CLI(명령줄 인터페이스)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="1520c-121">그러나 코드를 비대화형이고 자동화된 방식으로 동작하도록 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="1520c-122">Azure AD B2C 테넌트 가져오기</span><span class="sxs-lookup"><span data-stu-id="1520c-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="1520c-123">응용 프로그램 또는 사용자를 만들거나 Azure AD와 상호 작용하려면 Azure AD B2C 테넌트 및 해당 테넌트의 전역 관리자 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="1520c-124">테넌트가 없는 경우 [Azure AD B2C를 시작](active-directory-b2c-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="1520c-125">테넌트에서 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="1520c-125">Register your application in your tenant</span></span>
<span data-ttu-id="1520c-126">B2C 테넌트를 설정한 후에 [Azure Portal](https://portal.azure.com)을 통해 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1520c-127">B2C 테넌트에서 Graph API를 사용하려면 Azure AD B2C *응용 프로그램* 블레이드가 **아닌** Azure Portal의 제네릭 *앱 등록*을 사용하여 전용 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="1520c-128">Azure AD B2C의 *응용 프로그램* 블레이드에 등록한 기존 B2C 응용 프로그램을 다시 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="1520c-129">[Azure Portal](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1520c-130">페이지의 오른쪽 위 모서리에서 계정을 선택하여 Azure AD B2C 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="1520c-131">왼쪽 탐색 창에서 **추가 서비스**를 선택하고 **앱 등록**을 클릭한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="1520c-132">프롬프트에 따라 새 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="1520c-133">응용 프로그램 형식에 **Web App/API**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="1520c-134">이 예제와 관련이 없지만 **모든 리디렉션 URI**(예: https://B2CGraphAPI )를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="1520c-135">이제 응용 프로그램은 응용 프로그램의 목록을 표시합니다. 이를 클릭하여 **응용 프로그램 ID**(클라이언트 ID라고도 함)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="1520c-136">이후 섹션에서 필요하므로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="1520c-137">설정 블레이드에서 **키**를 클릭하고 새 키(클라이언트 암호라고도 함)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="1520c-138">또한 뒤에 나오는 섹션에서 사용하기 위해 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="1520c-139">응용 프로그램에 대한 만들기, 읽기 및 업데이트 사용 권한 구성</span><span class="sxs-lookup"><span data-stu-id="1520c-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="1520c-140">이제 사용자를 만들기, 읽기, 업데이트 및 삭제하는 데 필요한 모든 권한을 가져오도록 응용 프로그램을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="1520c-141">Azure Portal의 [앱 등록] 블레이드에서 계속 진행하여 응용 프로그램을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="1520c-142">설정 블레이드에서 **필요한 사용 권한**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="1520c-143">필요한 사용 권한 블레이드에서 **Windows Azure Active Directory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="1520c-144">[액세스 사용] 블레이드에서 **응용 프로그램 사용 권한**의 **디렉터리 데이터 읽기 및 쓰기** 사용 권한을 선택하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="1520c-145">마지막으로 필요한 사용 권한 블레이드로 돌아가서 **사용 권한 부여** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="1520c-146">이제 B2C 테넌트에서 사용자를 만들기, 읽기 및 업데이트하는 권한을 가진 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="1520c-147">응용 프로그램에 대한 삭제 권한 구성</span><span class="sxs-lookup"><span data-stu-id="1520c-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="1520c-148">현재 *디렉터리 데이터 읽기 및 쓰기* 사용 권한에는 사용자를 삭제하는 등 모든 삭제 작업을 수행하는 기능이 포함되지 **않습니다**.</span><span class="sxs-lookup"><span data-stu-id="1520c-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="1520c-149">응용 프로그램에 사용자를 삭제하는 기능을 제공하려는 경우 PowerShell을 포함하는 이러한 추가 단계를 수행해야 합니다. 그렇지 않은 경우 다음 섹션으로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="1520c-150">우선 [Microsoft Online Services 로그인 도우미](http://go.microsoft.com/fwlink/?LinkID=286152)를 다운로드 및 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="1520c-151">그런 다음 [Windows PowerShell 용 64비트 Azure Active Directory 모듈](http://go.microsoft.com/fwlink/p/?linkid=236297)을 다운로드하고 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="1520c-152">PowerShell 모듈을 설치한 후에 PowerShell을 열고 B2C 테넌트에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="1520c-153">`Get-Credential`을 실행한 후에 사용자 이름 및 암호를 묻는 메시지가 표시되면 B2C 테넌트 관리자 계정의 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1520c-154">B2C 테넌트에 대해 **로컬**인 B2C 테넌트 관리자 계정을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="1520c-155">이러한 계정은 다음과 같습니다. myusername@myb2ctenant.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="1520c-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="1520c-156">이제 아래 스크립트에서 **응용 프로그램 ID**를 사용하여 응용 프로그램에 사용자를 삭제할 수 있는 사용자 계정 관리자 역할을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="1520c-157">이러한 역할은 잘 알려진 식별자로서 아래 스크립트에서 **응용 프로그램 ID**를 입력하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="1520c-158">이제 응용 프로그램에는 B2C 테넌트 사용자를 삭제하는 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="1520c-159">샘플 코드를 다운로드, 구성 및 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="1520c-160">우선 샘플 코드를 다운로드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="1520c-161">그런 다음 자세히 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="1520c-162">[샘플 코드를 .zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="1520c-163">사용자가 선택한 디렉터리에 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="1520c-164">Visual Studio에서 `B2CGraphClient\B2CGraphClient.sln` Visual Studio 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="1520c-165">`B2CGraphClient` 프로젝트에서 `App.config` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="1520c-166">세 개의 앱 설정을 다음과 같이 고유한 값으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="1520c-167">이제 `B2CGraphClient` 솔루션을 마우스 오른쪽 단추로 클릭하고 샘플을 다시 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="1520c-168">성공하는 경우 `B2C.exe` 실행 파일이 `B2CGraphClient\bin\Debug`에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="1520c-169">Graph API를 사용하여 사용자 CRUD 작업 작성</span><span class="sxs-lookup"><span data-stu-id="1520c-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="1520c-170">B2CGraphClient를 사용하려면 `cmd` Windows 명령 프롬프트를 열고 `Debug` 디렉터리로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="1520c-171">`B2C Help` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="1520c-172">각 명령에 대한 간략한 설명을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-172">This will display a brief description of each command.</span></span> <span data-ttu-id="1520c-173">이 명령 중 하나를 호출할 때마다 `B2CGraphClient` 은 Azure AD Graph API에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="1520c-174">액세스 토큰 가져오기</span><span class="sxs-lookup"><span data-stu-id="1520c-174">Get an access token</span></span>
<span data-ttu-id="1520c-175">Graph API에 대한 요청은 인증을 위한 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="1520c-176">`B2CGraphClient` 은 오픈 소스 ADAL(Active Directory 인증 라이브러리)를 사용하여 액세스 토큰을 획득할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="1520c-177">ADAL을 사용하면 간단한 API를 제공하고 액세스 토큰의 캐싱과 같은 중요한 일부 세부 정보를 처리하여 토큰을 쉽게 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="1520c-178">그러나 ADAL을 사용하여 토큰을 가져올 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="1520c-179">HTTP 요청을 선별하여 토큰을 가져올 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="1520c-180">이 코드 샘플에서는 Graph API와 통신하기 위해 ADAL v2를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="1520c-181">Azure AD Graph API와 함께 사용할 수 있는 액세스 토큰을 가져오기 위해 ADAL v2 또는 v3를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="1520c-182">`B2CGraphClient`가 실행되면 `B2CGraphClient` 클래스의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="1520c-183">이 클래스의 생성자는 ADAL 인증 스캐폴딩을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="1520c-184">`B2C Get-User` 명령을 예로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="1520c-185">`B2C Get-User`이 추가 입력 없이 호출되면 CLI가 `B2CGraphClient.GetAllUsers(...)` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="1520c-186">이 메서드는 `B2CGraphClient.SendGraphGetRequest(...)`를 호출하며 이는 Graph API에 HTTP GET 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="1520c-187">`B2CGraphClient.SendGraphGetRequest(...)` 가 가져오기 요청을 보내기 전에 먼저 ADAL을 사용하여 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="1520c-188">ADAL `AuthenticationContext.AcquireToken(...)` 메서드를 호출하여 Graph API에 대한 액세스 토큰을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="1520c-189">그러면 ADAL은 응용 프로그램의 ID를 나타내는 `access_token` 를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="1520c-190">사용자 읽기</span><span class="sxs-lookup"><span data-stu-id="1520c-190">Read users</span></span>
<span data-ttu-id="1520c-191">Graph API에서 사용자의 목록을 가져오거나 특정 사용자를 가져오려는 경우 `/users` 끝점에 HTTP `GET` 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="1520c-192">테넌트의 모든 사용자에 대한 요청은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="1520c-193">이 요청을 보려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="1520c-194">유의해야 할 두 가지 중요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-194">There are two important things to note:</span></span>

* <span data-ttu-id="1520c-195">ADAL을 통해 획득한 액세스 토큰은 `Bearer` 체계를 사용하여 `Authorization` 헤더에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="1520c-196">B2C 테넌트의 경우 쿼리 매개 변수 `api-version=1.6`를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="1520c-197">이러한 세부 사항은 모두 `B2CGraphClient.SendGraphGetRequest(...)` 메서드에서 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="1520c-198">소비자 사용자 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1520c-198">Create consumer user accounts</span></span>
<span data-ttu-id="1520c-199">B2C 테넌트에 사용자 계정을 만들 경우 `/users` 끝점에 HTTP `POST` 요청을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="1520c-200">이 요청의 이러한 대부분의 속성은 소비자 사용자를 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="1520c-201">자세히 알아보려면 [여기](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser)를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="1520c-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="1520c-202">`//` 메모는 그림에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="1520c-203">실제 요청에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="1520c-204">요청을 확인하려면 다음 명령 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="1520c-205">`Create-User` 명령은 .json 파일을 입력 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="1520c-206">이는 사용자 개체의 JSON 표현을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="1520c-207">샘플 코드에는 두 개의 샘플 .json 파일인 `usertemplate-email.json`과 `usertemplate-username.json`이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="1520c-208">필요에 따라 이러한 파일을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="1520c-209">위의 필수 필드 외에도 사용할 수 있는 여러 가지 선택적 필드가 이러한 파일에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="1520c-210">선택적 필드에 대한 세부 정보는 [Azure AD Graph API 엔터티 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="1520c-211">이 POST 요청이 `B2CGraphClient.SendGraphPostRequest(...)`에서 생성되는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="1520c-212">액세스 토큰을 요청의 `Authorization` 헤더에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="1520c-213">`api-version=1.6`을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="1520c-214">요청 본문에 JSON 사용자 개체를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="1520c-215">기존 사용자 저장소에서 마이그레이션하려는 계정에 [Azure AD B2C에 의해 적용되는 강력한 암호 강도](https://msdn.microsoft.com/library/azure/jj943764.aspx)보다 낮은 강도의 암호가 지정되어 있으면 `passwordPolicies` 속성의 `DisableStrongPassword` 값을 사용하여 강력한 암호 요구 사항을 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="1520c-216">예를 들어 다음과 같이 위에 제공된 사용자 만들기 요청을 수정할 수 있습니다. `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="1520c-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="1520c-217">소비자 사용자 계정 업데이트</span><span class="sxs-lookup"><span data-stu-id="1520c-217">Update consumer user accounts</span></span>
<span data-ttu-id="1520c-218">사용자 개체를 업데이트할 때 사용자 개체를 만드는 작업과 프로세스가 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="1520c-219">하지만 이 프로세스는 HTTP `PATCH` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="1520c-220">JSON 파일을 새 데이터로 업데이트하여 사용자를 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="1520c-221">`B2CGraphClient`을 사용하여 이러한 명령 중 하나를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="1520c-222">이 요청을 보내는 방법에 대한 세부 정보는 `B2CGraphClient.SendGraphPatchRequest(...)` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="1520c-223">사용자 검색</span><span class="sxs-lookup"><span data-stu-id="1520c-223">Search users</span></span>
<span data-ttu-id="1520c-224">여러 가지 방법으로 B2C 테넌트에서 사용자를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="1520c-225">하나는 사용자의 개체 ID를 사용하는 방법이고 다른 하나는 사용자의 로그인 식별자(예: `signInNames` 속성)를 사용하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="1520c-226">특정 사용자를 검색하려면 다음 명령 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="1520c-227">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="1520c-228">사용자 삭제</span><span class="sxs-lookup"><span data-stu-id="1520c-228">Delete users</span></span>
<span data-ttu-id="1520c-229">사용자를 삭제하는 과정은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="1520c-230">HTTP `DELETE` 메서드를 사용하고 올바른 개체 ID로 URL을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="1520c-231">예제를 보려면 이 명령을 입력하고 콘솔에 출력된 삭제 요청을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="1520c-232">이 요청을 보내는 방법에 대한 세부 정보는 `B2CGraphClient.SendGraphDeleteRequest(...)` 메서드를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="1520c-233">사용자 관리 외에도 Azure AD Graph API를 사용하여 다른 많은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="1520c-234">[Azure AD Graph API 참조](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) 는 샘플 요청과 함께 각 작업의 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="1520c-235">사용자 지정 특성 사용</span><span class="sxs-lookup"><span data-stu-id="1520c-235">Use custom attributes</span></span>
<span data-ttu-id="1520c-236">많은 소비자 응용 프로그램은 특정 유형의 사용자 지정 사용자 프로필 정보를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="1520c-237">이렇게 할 수 있는 한 가지 방법은 B2C 테넌트의 사용자 지정 특성을 정의하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="1520c-238">그런 다음 해당 특성을 사용자 개체의 다른 속성을 다룰 경우와 동일한 방식으로 다룰 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="1520c-239">특성을 업데이트 및 삭제하고 특성으로 쿼리하며 특성을 로그인 토큰에서 클레임으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="1520c-240">B2C 테넌트에서 사용자 지정 특성을 정의하려면 [B2C 사용자 지정 특성 참조](active-directory-b2c-reference-custom-attr.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1520c-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="1520c-241">`B2CGraphClient`를 사용하여 B2C 테넌트에 정의된 사용자 지정 특성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="1520c-242">이러한 함수의 출력은 각 사용자 지정 특성의 세부 정보를 다음과 같이 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="1520c-243">`extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`와 같은 전체 이름을 사용자 개체의 속성으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="1520c-244">.json 파일을 새 속성 및 속성에 대한 값으로 업데이트한 다음 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="1520c-245">`B2CGraphClient`를 사용하여 B2C 테넌트 사용자를 프로그래밍 방식으로 관리할 수 있는 서비스 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="1520c-246">`B2CGraphClient` 는 고유한 응용 프로그램 ID를 사용하여 Azure AD Graph API에 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="1520c-247">또한 클라이언트 암호를 사용하여 토큰을 획득합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="1520c-248">응용 프로그램에 이 기능을 통합할 때 B2C 앱에 대한 몇 가지 주요 사항을 기억해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="1520c-249">테넌트에서 응용 프로그램에 적절한 권한을 부여해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="1520c-250">이제 ADAL(MSAL 아님)을 사용하여 액세스 토큰을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="1520c-251">(또한 라이브러리를 사용하지 않고 직접 프로토콜 메시지를 보낼 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="1520c-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="1520c-252">Graph API를 호출할 때 `api-version=1.6`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="1520c-253">소비자 사용자를 만들고 업데이트하는 경우 위에서 설명한 대로 필수적인 몇 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1520c-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="1520c-254">B2C 테넌트의 Graph API를 사용하여 수행하려는 작업에 대한 질문이나 요청이 있는 경우 이 문서 또는 파일에 GitHub 코드 샘플 리포지토리의 문제에 대한 의견을 남겨주세요.</span><span class="sxs-lookup"><span data-stu-id="1520c-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

