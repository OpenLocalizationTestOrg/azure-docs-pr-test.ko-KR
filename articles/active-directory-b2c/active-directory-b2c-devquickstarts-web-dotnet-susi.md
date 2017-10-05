---
title: Azure Active Directory B2C | Microsoft Docs
description: "Azure Active Directory B2C를 사용하여 등록/로그인, 프로필 편집 및 암호 다시 설정을 포함하는 웹 응용 프로그램을 빌드하는 방법입니다."
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="d0fd5-103">Azure Active Directory B2C 등록, 로그인, 프로필 편집 및 암호 재설정을 사용하여 ASP.NET 웹앱 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="d0fd5-104">이 자습서에서는 다음을 수행하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d0fd5-105">웹앱에 Azure AD B2C ID 기능 추가</span><span class="sxs-lookup"><span data-stu-id="d0fd5-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="d0fd5-106">Azure AD B2C 디렉터리에 웹앱 등록</span><span class="sxs-lookup"><span data-stu-id="d0fd5-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="d0fd5-107">웹앱에 대한 사용자 등록/로그인, 프로필 편집 및 암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0fd5-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d0fd5-108">Prerequisites</span></span>

- <span data-ttu-id="d0fd5-109">Azure 계정에 B2C 테넌트를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="d0fd5-110">[여기](https://azure.microsoft.com/en-us/)에서 Azure 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="d0fd5-111">샘플 코드를 보고 수정하기 위해 [Microsoft Visual Studio](https://www.visualstudio.com/) 또는 비슷한 프로그램이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="d0fd5-112">Azure AD B2C 디렉터리 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="d0fd5-113">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="d0fd5-114">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="d0fd5-115">아직 없는 경우 B2C 디렉터리를 만든 후에 이 가이드를 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="d0fd5-116">Azure 구독에 B2C 테넌트를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="d0fd5-117">**만들기**를 선택한 후 **Azure 구독에 기존 Azure AD B2C 테넌트 연결** 옵션을 선택한 다음 **Azure AD B2C 테넌트** 드롭다운에서 연결하려는 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="d0fd5-118">응용 프로그램 만들기 및 등록</span><span class="sxs-lookup"><span data-stu-id="d0fd5-118">Create and register an application</span></span>

<span data-ttu-id="d0fd5-119">다음으로 B2C 디렉터리에서 앱을 만들고 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="d0fd5-120">Azure AD B2C가 앱과 안전하게 통신하는 데 필요한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="d0fd5-121">완료되면 응용 프로그램 설정에 API 및 네이티브 응용 프로그램 모두를 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="d0fd5-122">B2C 테넌트에 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="d0fd5-123">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d0fd5-124">이 코드 샘플은 **등록 및 로그인**, **프로필 편집** 및 **암호 재설정**의 세 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="d0fd5-125">[정책 참조 문서](active-directory-b2c-reference-policies.md)에서 설명한 대로 각 형식에 하나의 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d0fd5-126">각 정책의 경우 표시 이름 특성 또는 클레임을 선택하고 나중에 사용할 정책 이름을 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="d0fd5-127">ID 공급자 추가</span><span class="sxs-lookup"><span data-stu-id="d0fd5-127">Add your identity providers</span></span>

<span data-ttu-id="d0fd5-128">설정에서 **ID 공급자**를 선택하고 사용자 이름 등록 또는 전자 메일 등록을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="d0fd5-129">등록 및 로그인 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="d0fd5-130">프로필 편집 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="d0fd5-131">암호 재설정 정책 만들기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="d0fd5-132">정책을 만들었다면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="d0fd5-133">샘플 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="d0fd5-133">Download the sample code</span></span>

<span data-ttu-id="d0fd5-134">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="d0fd5-135">다음을 실행하여 샘플을 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="d0fd5-136">샘플 코드를 다운로드한 후 Visual Studio .sln 파일을 열어 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="d0fd5-137">이제 솔루션에는 `TaskWebApp`과 `TaskService`, 2개의 프로젝트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="d0fd5-138">`TaskWebApp`은 사용자와 상호 작용하는 MVC 웹 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="d0fd5-139">`TaskService` 는 각 사용자의 할 일 모음을 저장하는 앱의 백 엔드 Web API입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="d0fd5-140">이 문서에서는 `TaskWebApp` 응용 프로그램만을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="d0fd5-141">Azure AD B2C를 사용하여 `TaskService`을 구축하는 방법을 알아보려면 [.NET 웹 API 자습서](active-directory-b2c-devquickstarts-api-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="d0fd5-142">테넌트 및 정책을 사용하는 코드 업데이트</span><span class="sxs-lookup"><span data-stu-id="d0fd5-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="d0fd5-143">샘플은 데모 테넌트의 정책 및 클라이언트 ID를 사용하도록 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="d0fd5-144">자신의 테넌트에 연결하려면 `TaskWebApp` 프로젝트에서 `web.config`를 열고 다음 값을 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="d0fd5-145">`ida:Tenant`를 테넌트 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="d0fd5-146">`ida:ClientId`를 웹앱 응용 프로그램 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="d0fd5-147">`ida:ClientSecret`을 웹앱 비밀 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="d0fd5-148">`ida:SignUpSignInPolicyId`를 "등록 또는 로그인" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="d0fd5-149">`ida:EditProfilePolicyId`를 "프로필 편집" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="d0fd5-150">`ida:ResetPasswordPolicyId`를 "암호 재설정" 정책 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="d0fd5-151">앱 시작</span><span class="sxs-lookup"><span data-stu-id="d0fd5-151">Launch the app</span></span>
<span data-ttu-id="d0fd5-152">Visual Studio 내에서 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="d0fd5-153">할 일 목록 탭으로 이동합니다. URl는 https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="d0fd5-154">메일 주소 또는 사용자 이름을 사용하여 앱에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="d0fd5-155">로그아웃한 다음 다시 로그인하고 프로필을 편집하거나 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="d0fd5-156">로그아웃했다가 다른 사용자로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="d0fd5-157">소셜 IDP 추가</span><span class="sxs-lookup"><span data-stu-id="d0fd5-157">Add social IDPs</span></span>

<span data-ttu-id="d0fd5-158">현재 앱은 **로컬 계정**을 사용하여 사용자 등록 및 로그인을 지원합니다. 사용자 이름 및 암호를 사용하는 B2C 디렉터리에 저장된 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="d0fd5-159">Azure AD B2C를 사용하면 코드를 변경하지 않고도 다른 **IDP(ID 공급자)** 에 대한 지원을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="d0fd5-160">소셜 IDP를 앱에 추가하려면 이 문서 중에서 상세한 지침을 수행하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="d0fd5-161">지원하려는 각 IDP의 경우 해당 시스템에서 응용 프로그램을 등록하고 클라이언트 ID를 얻어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="d0fd5-162">Facebook을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fd5-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="d0fd5-163">Google을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fd5-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="d0fd5-164">Amazon을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fd5-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="d0fd5-165">LinkedIn을 IDP로 설정</span><span class="sxs-lookup"><span data-stu-id="d0fd5-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="d0fd5-166">B2C 디렉터리에 ID 공급자를 추가한 후 [정책 참조 문서](active-directory-b2c-reference-policies.md)에서 설명한 대로 새 IDP를 포함하도록 세 가지 정책을 각각 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="d0fd5-167">정책을 저장한 후 앱을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="d0fd5-168">ID 환경 각각에서 로그인 및 등록으로 추가된 새 IDP가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="d0fd5-169">정책을 실험하고 샘플 앱에서 영향을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="d0fd5-170">IDP를 추가 또는 제거하거나 응용 프로그램 클레임을 조작하거나 등록 특성을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="d0fd5-171">어떻게 정책, 인증 요청 및 OWIN을 모두 함께 연결하는지 확인할 수 있을 때까지 실험해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="d0fd5-172">샘플 코드 연습</span><span class="sxs-lookup"><span data-stu-id="d0fd5-172">Sample code walkthrough</span></span>
<span data-ttu-id="d0fd5-173">다음 섹션에서는 샘플 응용 프로그램 코드를 구성하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="d0fd5-174">이후 앱 개발에서 지침으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="d0fd5-175">인증 지원 추가</span><span class="sxs-lookup"><span data-stu-id="d0fd5-175">Add authentication support</span></span>

<span data-ttu-id="d0fd5-176">이제 Azure AD B2C를 사용하여 앱을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="d0fd5-177">앱은 OpenID Connect 인증 요청을 보내 Azure AD B2C와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="d0fd5-178">요청은 앱에서 정책을 지정하여 실행하려는 사용자 경험을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="d0fd5-179">Microsoft의 OWIN 라이브러리를 사용하여 해당 요청을 보내고, 정책을 실행하고, 사용자의 세션을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="d0fd5-180">OWIN 설치</span><span class="sxs-lookup"><span data-stu-id="d0fd5-180">Install OWIN</span></span>

<span data-ttu-id="d0fd5-181">시작하려면 Visual Studio 패키지 관리자 콘솔을 사용하여 OWIN 미들웨어 NuGet 패키지를 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="d0fd5-182">OWIN 시작 클래스 추가</span><span class="sxs-lookup"><span data-stu-id="d0fd5-182">Add an OWIN startup class</span></span>

<span data-ttu-id="d0fd5-183">`Startup.cs`라는 API에 OWIN 시작 클래스를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="d0fd5-184">프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** 및 **새 항목**을 선택한 다음 OWIN을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="d0fd5-185">OWIN 미들웨어는 앱이 시작되면 `Configuration(…)` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="d0fd5-186">이 샘플에서는 `public partial class Startup`에 대한 클래스 선언을 변경하고 `App_Start\Startup.Auth.cs`에서 클래스의 다른 부분을 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="d0fd5-187">`Configuration` 메서드 내에서 `ConfigureAuth`에 호출을 추가했습니다. 이는 `Startup.Auth.cs`에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="d0fd5-188">수정 후에 `Startup.cs`는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="d0fd5-189">인증 미들웨어 구성</span><span class="sxs-lookup"><span data-stu-id="d0fd5-189">Configure the authentication middleware</span></span>

<span data-ttu-id="d0fd5-190">`App_Start\Startup.Auth.cs` 파일을 열고 `ConfigureAuth(...)` 메서드를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="d0fd5-191">`OpenIdConnectAuthenticationOptions`에 제공하는 매개 변수는 앱이 Azure AD B2C와 통신하기 위한 좌표로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="d0fd5-192">특정 매개 변수를 지정하지 않으면 기본값이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="d0fd5-193">예를 들어 샘플에 `ResponseType`을 지정하지 않으므로 기본값 `code id_token`이 Azure AD B2C로 보내는 각 요청에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="d0fd5-194">쿠키 인증도 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="d0fd5-195">무엇보다도 OpenID Connect 미들웨어는 사용자 세션을 유지하기 위해 쿠키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="d0fd5-196">위의 `OpenIdConnectAuthenticationOptions`에서 OpenID Connect 미들웨어에서 수신되는 특정 알림에 대한 콜백 함수 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="d0fd5-197">이러한 동작은 `OpenIdConnectAuthenticationNotifications` 개체를 사용하여 정의되고 `Notifications` 변수에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="d0fd5-198">샘플에서는 이벤트에 따라 서로 다른 3개의 콜백을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="d0fd5-199">다른 정책 사용</span><span class="sxs-lookup"><span data-stu-id="d0fd5-199">Using different policies</span></span>

<span data-ttu-id="d0fd5-200">Azure AD B2C에 대한 요청이 만들어질 때마다 `RedirectToIdentityProvider` 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="d0fd5-201">콜백 함수 `OnRedirectToIdentityProvider`에서 다른 정책을 사용하려는 경우 나가는 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="d0fd5-202">암호 재설정 또는 프로필 편집을 수행하려면 기본 "등록 또는 로그인" 정책 대신 암호 재설정 정책과 같은 해당 정책을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="d0fd5-203">샘플에서는 사용자가 암호를 재설정하거나 프로필을 편집하려고 하는 경우 OWIN 컨텍스트로 사용하려는 정책을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="d0fd5-204">다음을 수행하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="d0fd5-205">다음을 수행하여 콜백 함수 `OnRedirectToIdentityProvider`를 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="d0fd5-206">권한 부여 코드 처리</span><span class="sxs-lookup"><span data-stu-id="d0fd5-206">Handling authorization codes</span></span>

<span data-ttu-id="d0fd5-207">권한 부여 코드를 받을 때 `AuthorizationCodeReceived` 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="d0fd5-208">OpenID Connect 미들웨어는 액세스 토큰에 대한 코드 교환을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="d0fd5-209">콜백 함수에서 토큰에 대한 코드를 수동으로 교환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="d0fd5-210">자세한 내용은 방법을 설명하는 [설명서](active-directory-b2c-devquickstarts-web-api-dotnet.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="d0fd5-211">오류 처리</span><span class="sxs-lookup"><span data-stu-id="d0fd5-211">Handling errors</span></span>

<span data-ttu-id="d0fd5-212">인증이 실패한 경우 `AuthenticationFailed` 알림이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="d0fd5-213">해당 콜백 메서드에서 원하는 대로 오류를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="d0fd5-214">그러나 오류 코드 `AADB2C90118`에 대한 확인을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="d0fd5-215">“등록 또는 로그인” 정책 실행 동안 사용자에게 **암호를 잊으셨나요?** 링크를 선택할 기회가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="d0fd5-216">이 이벤트에서 Azure AD B2C는 앱에 암호 재설정 정책을 대신 사용하여 요청을 만들어야 한다는 것을 나타내는 해당 오류 코드를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="d0fd5-217">Azure AD로 인증 요청 보내기</span><span class="sxs-lookup"><span data-stu-id="d0fd5-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="d0fd5-218">이제 앱은 OpenID Connect 인증 프로토콜을 사용하여 Azure AD B2C와 통신하도록 올바르게 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="d0fd5-219">OWIN은 인증 메시지를 작성하고, Azure AD B2C에서 토큰의 유효성을 검사하고, 사용자 세션을 유지 관리하는 세부 과정을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="d0fd5-220">이제 각 사용자 흐름을 시작하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="d0fd5-221">사용자가 웹앱에서 **등록/로그인**, **프로필 편집** 또는 **암호 재설정**을 선택하는 경우 연결된 작업이 `Controllers\AccountController.cs`에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="d0fd5-222">또한 앱에서 사용자를 로그아웃하는 데 OWIN을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="d0fd5-223">`Controllers\AccountController.cs`에서 다음을 가집니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="d0fd5-224">정책을 명시적으로 호출하는 것 외에도 사용자가 로그인하지 않은 경우 정책을 실행할 컨트롤러에서 `[Authorize]` 태그를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="d0fd5-225">`Controllers\HomeController.cs`를 열고 클레임 컨트롤러에 `[Authorize]` 태그를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="d0fd5-226">OWIN은 `[Authorize]` 태그를 눌렀을 때 구성되는 마지막 정책을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="d0fd5-227">사용자 정보 표시</span><span class="sxs-lookup"><span data-stu-id="d0fd5-227">Display user information</span></span>

<span data-ttu-id="d0fd5-228">OpenID Connect를 사용하여 사용자를 인증할 때 Azure AD B2C는 **클레임**을 포함하는 ID 토큰을 앱에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="d0fd5-229">이는 사용자에 대한 어설션입니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-229">These are assertions about the user.</span></span> <span data-ttu-id="d0fd5-230">클레임을 사용하여 앱 개인 설정을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="d0fd5-231">`Controllers\HomeController.cs` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="d0fd5-232">`ClaimsPrincipal.Current` 보안 주체 개체를 통해 컨트롤러의 사용자 클레임에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="d0fd5-233">동일한 방식으로 응용 프로그램에서 수신하는 클레임을 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="d0fd5-234">앱이 수신하는 모든 클레임 목록은 **클레임** 페이지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0fd5-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
