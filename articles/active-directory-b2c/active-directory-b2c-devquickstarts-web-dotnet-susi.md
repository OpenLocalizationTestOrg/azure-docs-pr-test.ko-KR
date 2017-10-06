---
title: Active Directory B2C aaaAzure | Microsoft Docs
description: "어떻게 toobuild 웹 응용 프로그램 로그-up/로그인을 프로필 편집 및 Azure Active Directory B2C를 사용 하 여 다시 설정 하는 암호입니다."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="ffc34-103">Azure Active Directory B2C 등록, 로그인, 프로필 편집 및 암호 재설정을 사용하여 ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="ffc34-104">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ffc34-105">Azure AD B2C identity 기능 tooyour 웹 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="ffc34-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="ffc34-106">Azure AD B2C 디렉터리에 웹앱 등록</span><span class="sxs-lookup"><span data-stu-id="ffc34-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="ffc34-107">웹앱에 대한 사용자 등록/로그인, 프로필 편집 및 암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffc34-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ffc34-108">Prerequisites</span></span>

- <span data-ttu-id="ffc34-109">프로그램 B2C 테 넌 트 tooan Azure 계정을 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="ffc34-110">[여기](https://azure.microsoft.com/en-us/)에서 Azure 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="ffc34-111">필요한 [Microsoft Visual Studio](https://www.visualstudio.com/) 또는 유사한 tooview 프로그래밍 하 고 hello 샘플 코드를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="ffc34-112">Azure AD B2C 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="ffc34-113">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ffc34-114">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="ffc34-115">아직 없는 경우 B2C 디렉터리를 만든 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="ffc34-116">Tooconnect hello B2C 테 넌 트 tooyour Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="ffc34-117">선택한 후 **만들기**을 선택 hello **링크 기존 Azure AD B2C 테 넌 트 toomy Azure 구독** 옵션을 선택한 다음 hello **Azure AD B2C 테 넌 트** 드롭다운을 선택 hello tooassociate 원하는 테 넌 트.</span><span class="sxs-lookup"><span data-stu-id="ffc34-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="ffc34-118">응용 프로그램 만들기 및 등록</span><span class="sxs-lookup"><span data-stu-id="ffc34-118">Create and register an application</span></span>

<span data-ttu-id="ffc34-119">다음으로 toocreate 필요 하 고 B2C 디렉터리 hello 앱을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="ffc34-120">이렇게 하면 필요한 정보를 Azure AD B2C toosecurely 앱과 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="ffc34-121">완료되면 응용 프로그램 설정에 API 및 네이티브 응용 프로그램 모두를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="ffc34-122">B2C 테넌트에 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="ffc34-123">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ffc34-124">이 코드 샘플은 **등록 및 로그인**, **프로필 편집** 및 **암호 재설정**의 세 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="ffc34-125">Hello에 설명 된 대로 각 유형의 toocreate 하나의 정책이 필요한 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ffc34-126">각 정책에 대 한 tooselect hello 표시 이름 특성 또는 클레임 있으며 나중에 사용할 정책 hello 이름 아래로 toocopy 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="ffc34-127">ID 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="ffc34-127">Add your identity providers</span></span>

<span data-ttu-id="ffc34-128">설정에서 **ID 공급자**를 선택하고 사용자 이름 등록 또는 전자 메일 등록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="ffc34-129">등록 및 로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="ffc34-130">프로필 편집 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="ffc34-131">암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="ffc34-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="ffc34-132">준비 toobuild 하 여 정책을 만든 후 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="ffc34-133">Hello 샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="ffc34-133">Download hello sample code</span></span>

<span data-ttu-id="ffc34-134">이 자습서에 대 한 hello 코드에서 유지 관리 됩니다 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="ffc34-135">실행 하 여 hello 샘플을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="ffc34-136">Hello 샘플 코드를 다운로드 한 후 hello open Visual Studio.sln 파일 tooget 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="ffc34-137">hello 솔루션 파일에는 두 개의 프로젝트가 포함 되어: `TaskWebApp` 및 `TaskService`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="ffc34-138">`TaskWebApp`상호 작용 하는 hello 사용자 hello MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="ffc34-139">`TaskService`각 사용자의 할 일 목록에 저장 하는 hello 앱 백 엔드 웹 API입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="ffc34-140">이 문서에서는 hello 설명만 `TaskWebApp` 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="ffc34-141">toolearn 어떻게 toobuild `TaskService` Azure AD B2C를 사용 하 여 참조 [우리의.NET 웹 api 자습서](active-directory-b2c-devquickstarts-api-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="ffc34-142">테 넌 트 및 정책에 맞게 코드 toouse 업데이트</span><span class="sxs-lookup"><span data-stu-id="ffc34-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="ffc34-143">이 샘플은 구성 된 toouse hello 정책 및 클라이언트 ID 우리의 데모 테 넌 트입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="ffc34-144">tooconnect 것 tooyour 자체 테 넌 트 tooopen 해야 `web.config` hello에 `TaskWebApp` 프로젝트 및 다음 값에는 hello 바꾸기:</span><span class="sxs-lookup"><span data-stu-id="ffc34-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="ffc34-145">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="ffc34-146">`ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="ffc34-147">`ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="ffc34-148">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="ffc34-149">`ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="ffc34-150">`ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="ffc34-151">Hello 앱 시작</span><span class="sxs-lookup"><span data-stu-id="ffc34-151">Launch hello app</span></span>
<span data-ttu-id="ffc34-152">Visual Studio 내에서 hello 앱을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="ffc34-153">URl은 참고 hello 및 toohello 할 일 목록 탭 탐색: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id =* YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="ffc34-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="ffc34-154">전자 메일 주소 또는 사용자 이름을 사용 하 여 hello 앱 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="ffc34-155">로그 아웃 한 다음 다시 로그인 하 고 hello 프로필을 편집 하거나 hello 암호 다시 설정</span><span class="sxs-lookup"><span data-stu-id="ffc34-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="ffc34-156">로그아웃했다가 다른 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="ffc34-157">소셜 IDP 추가</span><span class="sxs-lookup"><span data-stu-id="ffc34-157">Add social IDPs</span></span>

<span data-ttu-id="ffc34-158">현재 hello 앱에서 등록 및 로그인 사용자만 사용 하 여 **로컬 계정**; 사용자 이름 및 암호를 사용 하는 계정을 B2C 디렉터리에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="ffc34-159">Azure AD B2C를 사용하면 코드를 변경하지 않고도 다른 **IDP(ID 공급자)** 에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="ffc34-160">tooadd 소셜 IDPs tooyour 응용 프로그램에 따라 hello 방법을 다음이 문서에 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="ffc34-161">에 대 한 각 IDP toosupport 5d; 응용 프로그램 tooregister 해당 시스템에 필요 하 고 클라이언트 ID를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="ffc34-162">Facebook을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="ffc34-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="ffc34-163">Google을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="ffc34-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="ffc34-164">Amazon을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="ffc34-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="ffc34-165">LinkedIn을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="ffc34-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="ffc34-166">Hello identity 공급자 tooyour B2C 디렉터리, 각 편집의 세 가지 정책 tooinclude hello에 설명 된 대로 새 IDPs hello 추가한 후 [정책 참조 문서](active-directory-b2c-reference-policies.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ffc34-167">정책을 저장 한 후 hello 앱을 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="ffc34-168">각 identity 경험 있는 로그인 및 등록 옵션으로 새 IDPs 추가 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="ffc34-169">정책을 테스트 하 여 및 샘플 앱에 hello 결과 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="ffc34-170">IDP를 추가 또는 제거하거나 응용 프로그램 클레임을 조작하거나 등록 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="ffc34-171">어떻게 정책, 인증 요청 및 OWIN을 모두 함께 연결하는지 확인할 수 있을 때까지 실험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ffc34-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="ffc34-172">샘플 코드 연습</span><span class="sxs-lookup"><span data-stu-id="ffc34-172">Sample code walkthrough</span></span>
<span data-ttu-id="ffc34-173">다음 섹션 hello hello 예제 응용 프로그램 코드 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="ffc34-174">이후 앱 개발에서 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="ffc34-175">인증 지원 추가</span><span class="sxs-lookup"><span data-stu-id="ffc34-175">Add authentication support</span></span>

<span data-ttu-id="ffc34-176">이제 Azure AD B2C 하 여 응용 프로그램 toouse를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="ffc34-177">앱은 OpenID Connect 인증 요청을 보내 Azure AD B2C와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="ffc34-178">hello 요청 사항이 hello 사용자 경험 앱 hello 정책을 지정 하 여 tooexecute 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="ffc34-179">이러한 요청을 Microsoft의 OWIN 라이브러리 toosend 사용 지정, 정책 실행, 사용자 세션을 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="ffc34-180">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="ffc34-180">Install OWIN</span></span>

<span data-ttu-id="ffc34-181">toobegin, hello Visual Studio 패키지 관리자 콘솔을 사용 하 여 hello OWIN 미들웨어 NuGet 패키지 toohello 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="ffc34-182">OWIN 시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="ffc34-182">Add an OWIN startup class</span></span>

<span data-ttu-id="ffc34-183">OWIN 시작 클래스 toohello API 호출 추가 `Startup.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="ffc34-184">Hello 프로젝트를 마우스 오른쪽 단추로 클릭 **추가** 및 **새 항목**, 한 다음 OWIN에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="ffc34-185">hello OWIN 미들웨어는 hello를 호출 하는 `Configuration(…)` 메서드 앱이 시작 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="ffc34-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="ffc34-186">이 예제에서는 변경 했습니다 hello 클래스 선언 너무`public partial class Startup` 구현에서 hello 클래스의 다른 부분을 hello `App_Start\Startup.Auth.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="ffc34-187">내부 hello `Configuration` 메서드를 호출 너무 추가`ConfigureAuth`에 정의 된 `Startup.Auth.cs`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="ffc34-188">Hello 수정한 다음 `Startup.cs` hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="ffc34-189">Hello 인증 미들웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="ffc34-190">파일 열기 hello `App_Start\Startup.Auth.cs` hello를 구현 하 고 `ConfigureAuth(...)` 메서드.</span><span class="sxs-lookup"><span data-stu-id="ffc34-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="ffc34-191">매개 변수가 hello `OpenIdConnectAuthenticationOptions` 좌표와 Azure AD B2C 앱 toocommunicate 프로그램에 대 한으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="ffc34-192">특정 매개 변수를 지정 하지 않으면 hello 기본값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="ffc34-193">예를 들어 hello를 지정 하지 않는 `ResponseType` hello 샘플에서 기본값 이므로 hello `code id_token` 각 나가는 요청 tooAzure AD B2C에에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="ffc34-194">Tooset 쿠키 인증을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="ffc34-195">hello OpenID Connect 미들웨어 무엇 보다도 쿠키 toomaintain 사용자 세션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="ffc34-196">`OpenIdConnectAuthenticationOptions` 위, hello OpenID Connect 미들웨어에서 수신 되는 특정 알림에 대 한 콜백 함수의 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="ffc34-197">이러한 동작은 사용 하 여 정의 됩니다는 `OpenIdConnectAuthenticationNotifications` 개체 및 hello에 저장 된 `Notifications` 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="ffc34-198">이 예제에서는 세 가지 콜백이 hello 이벤트에 따라 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="ffc34-199">다른 정책 사용</span><span class="sxs-lookup"><span data-stu-id="ffc34-199">Using different policies</span></span>

<span data-ttu-id="ffc34-200">hello `RedirectToIdentityProvider` tooAzure AD B2C은 요청 될 때마다 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="ffc34-201">Hello 콜백 함수에서 `OnRedirectToIdentityProvider`, 체크인 toouse 할까요 호출을 나가는 hello 다른 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="ffc34-202">순서 toodo 암호 다시 설정 또는 프로필을 편집할 hello 암호 재설정 정책 hello 기본 "등록 또는 로그인" 정책 대신 같은 toouse hello 해당 정책이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="ffc34-203">이 샘플에서는 사용자가 tooreset hello 암호 또는 hello 프로 파일을 편집 하는 경우에서는 추가 hello 정책 hello OWIN 컨텍스트로 toouse 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="ffc34-204">hello 다음을 수행 하 여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="ffc34-205">Hello 콜백 함수를 구현할 수 있습니다 및 `OnRedirectToIdentityProvider` hello 다음을 수행 하 여:</span><span class="sxs-lookup"><span data-stu-id="ffc34-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="ffc34-206">권한 부여 코드 처리</span><span class="sxs-lookup"><span data-stu-id="ffc34-206">Handling authorization codes</span></span>

<span data-ttu-id="ffc34-207">hello `AuthorizationCodeReceived` 인증 코드를 받을 때 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="ffc34-208">hello OpenID Connect 미들웨어 액세스 토큰에 대 한 교환 코드를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="ffc34-209">수동으로 hello 토큰에 콜백 함수에 대 한 hello 코드를 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="ffc34-210">자세한 내용은 참조 하십시오 hello [설명서](active-directory-b2c-devquickstarts-web-api-dotnet.md) 설명 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="ffc34-211">오류 처리</span><span class="sxs-lookup"><span data-stu-id="ffc34-211">Handling errors</span></span>

<span data-ttu-id="ffc34-212">hello `AuthenticationFailed` 인증이 실패 한 경우 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="ffc34-213">해당 콜백 메서드를 원하는 대로 hello 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="ffc34-214">그러나 추가할지를 묻는 hello 오류 코드에 대 한 확인 `AADB2C90118`합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="ffc34-215">"등록 또는 로그인" 정책 hello hello 실행 중 hello 사용자에 게 hello 기회 tooselect는 **암호를 잊으셨습니까?** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="ffc34-216">이 이벤트의 경우 Azure AD B2C는 응용 프로그램 응용 프로그램 대신 hello 암호 재설정 정책을 사용 하 여 요청을 수행 해야 해당 오류 코드가 나타내는 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="ffc34-217">인증 요청 tooAzure AD 보내기</span><span class="sxs-lookup"><span data-stu-id="ffc34-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="ffc34-218">이제 앱이 Azure AD B2C와 올바르게 구성 된 toocommunicate hello OpenID Connect 인증 프로토콜을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="ffc34-219">OWIN 인증 메시지를 만들어, Azure AD B2C에서 토큰의 유효성 검사 및 사용자 세션을 유지 관리의 hello 세부 정보를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="ffc34-220">나머지 각 사용자의 흐름 tooinitiate입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="ffc34-221">사용자가 선택할 때 **기호 위쪽/로그인**, **프로필 편집**, 또는 **암호 재설정** hello web app에서에 연결 된 hello 작업을 호출할 `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="ffc34-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="ffc34-222">OWIN toosign hello 앱에서 사용자 hello out를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="ffc34-223">`Controllers\AccountController.cs`에서 다음을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="ffc34-224">정책을 호출 또한 tooexplicitly를 사용할 수 있습니다는 `[Authorize]` hello 사용자가 로그인 되지 않은 경우 정책을 실행 하 여 컨트롤러에서 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="ffc34-225">열기 `Controllers\HomeController.cs` hello 추가 `[Authorize]` 태그 toohello 컨트롤러를 클레임 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="ffc34-226">Hello 마지막 정책 때 hello 구성를 선택 하는 OWIN `[Authorize]` 태그 적중 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="ffc34-227">사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="ffc34-227">Display user information</span></span>

<span data-ttu-id="ffc34-228">OpenID Connect를 사용 하 여 사용자를 인증 하는 경우 Azure AD B2C 반환을 포함 하는 ID 토큰 toohello 응용 프로그램 **클레임**합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="ffc34-229">이들은 hello 사용자에 대 한 어설션입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-229">These are assertions about hello user.</span></span> <span data-ttu-id="ffc34-230">앱 클레임 toopersonalize를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="ffc34-231">열기 hello `Controllers\HomeController.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="ffc34-232">사용자 클레임 hello 통해 컨트롤러에 액세스할 수 있습니다 `ClaimsPrincipal.Current` 보안 주체 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="ffc34-233">응용 프로그램 받는다고 hello에 동일한 클레임을 액세스할 수 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffc34-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="ffc34-234">Hello 앱 받는 모든 hello 클레임의 목록은 hello에 사용할 수 있습니다 **클레임** 페이지.</span><span class="sxs-lookup"><span data-stu-id="ffc34-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
