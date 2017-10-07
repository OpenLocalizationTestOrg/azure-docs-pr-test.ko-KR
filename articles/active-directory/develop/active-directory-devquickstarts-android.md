---
title: "시작 하는 AD Android aaaAzure | Microsoft Docs"
description: "어떻게 toobuild 로그인 및 Azure AD 호출에 대 한 Azure AD와 통합 하는 Android 응용 프로그램 OAuth를 사용 하 여 Api를 보호 합니다."
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="3a2ad-103">Android 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="3a2ad-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="3a2ad-104">새로운 우리의 hello 미리 보기를 사용 [개발자 포털](https://identity.microsoft.com/Docs/Android), 단 몇 분 후에 Azure AD와 실행 하는 데 도움이입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="3a2ad-105">hello 개발자 포털에서는 응용 프로그램을 등록 하 고 코드에 Azure AD 통합 hello 과정을 단계별로 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="3a2ad-106">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="3a2ad-107">데스크톱 응용 프로그램을 개발 하는 경우 Azure Active Directory (Azure AD) 하면 간단 하 고 간단 하 게 하면 tooauthenticate 사용자가 자신의 온-프레미스 Active Directory 계정을 사용 하 여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="3a2ad-108">응용 프로그램 toosecurely 해줍니다 모든 웹 Azure AD로 보호 되는 API를 사용와 같은 Office 365 Api hello 또는 Azure API를 환영 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="3a2ad-109">Azure AD tooaccess 보호 된 리소스를 필요로 하는 Android 클라이언트에 대 한 Active Directory 인증 라이브러리 (ADAL) hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="3a2ad-110">hello ADAL의 목적으로 toomake 사용자가 앱 tooget 액세스 토큰을 쉽게 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="3a2ad-111">toodemonstrate 하는 Android 할 일 목록 응용 프로그램을 작성할 것이 얼마나 쉬운지:</span><span class="sxs-lookup"><span data-stu-id="3a2ad-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="3a2ad-112">가져옵니다 hello를 사용 하 여 할 일 목록 API 호출에 대 한 토큰에 액세스 [OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="3a2ad-113">사용자의 할 일 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="3a2ad-114">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-114">Signs out users.</span></span>

<span data-ttu-id="3a2ad-115">시작 tooget, Azure AD 테 넌 트가 있습니다 수 있는 사용자를 만들와 응용 프로그램을 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="3a2ad-116">테 넌 트 아직 없는 경우 [자세한 방법을 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="3a2ad-117">1 단계: 다운로드 하 여 hello Node.js REST API TODO 샘플 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="3a2ad-118">hello Node.js REST API TODO 샘플에는 Azure AD에 대 한 단일-테 넌 트 할 일 REST API를 구축 하기 위한 기존 샘플에 대해 toowork 구체적으로 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="3a2ad-119">빠른 시작 hello에 대 한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="3a2ad-120">어떻게 tooset,이 기존 샘플 보기에 대 한 자세한 내용은 [Microsoft Azure Active Directory 샘플 REST API 서비스 Node.js 용](active-directory-devquickstarts-webapi-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="3a2ad-121">2단계: Azure AD 테넌트에 Web API 등록</span><span class="sxs-lookup"><span data-stu-id="3a2ad-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="3a2ad-122">Active Directory는 두 가지 유형의 응용 프로그램 추가를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="3a2ad-123">웹 서비스 toousers 제공 하는 Api</span><span class="sxs-lookup"><span data-stu-id="3a2ad-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="3a2ad-124">웹 Api 하는 것에 액세스 하는 응용 프로그램 (hello 웹 또는 장치에서 실행)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="3a2ad-125">이 단계에서는이 샘플 테스트를 위해 로컬로 실행 하는 hello 웹 API를 등록 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="3a2ad-126">일반적으로이 웹 API는 앱 tooaccess 원하는 기능을 제공 하는 REST 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="3a2ad-127">Azure AD는 끝점을 보호하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="3a2ad-128">Hello 앞서 참조 된 할 일 REST API를 등록 하는으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="3a2ad-129">하지만이 Azure Active Directory toohelp 보호 하려는 모든 웹 API에 대 한 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="3a2ad-130">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3a2ad-131">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-131">On hello top bar, click your account.</span></span> <span data-ttu-id="3a2ad-132">Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="3a2ad-133">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3a2ad-134">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3a2ad-135">Hello 응용 프로그램에 대 한 식별 이름을 입력 하세요 (예를 들어 **TodoListService**)을 선택 **웹 응용 프로그램 및/또는 Web API**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="3a2ad-136">Hello 로그온 URL에 대 한 hello 샘플에 대 한 hello 기준 URL을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="3a2ad-137">기본적으로 `https://localhost:8080`입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="3a2ad-138">클릭 **확인** toocomplete hello 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="3a2ad-139">Hello Azure 포털에서에서 tooyour 응용 프로그램 페이지를 이동 하 고 hello 응용 프로그램 ID 값을 찾아 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="3a2ad-140">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="3a2ad-141">Hello에서 **설정** -> **속성** 페이지, hello 앱 ID URI 업데이트-입력 `https://<your_tenant_name>/TodoListService`합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="3a2ad-142">대체 `<your_tenant_name>` Azure AD 테 넌 트의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="3a2ad-143">3 단계: hello 샘플 Android 네이티브 클라이언트 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="3a2ad-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="3a2ad-144">이 샘플에서는 웹 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-144">You must register your web application in this sample.</span></span> <span data-ttu-id="3a2ad-145">이렇게 하면 hello 적시에 등록 된 web API 응용 프로그램 toocommunicate를 프로그램 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="3a2ad-146">Azure AD는 거부 tooeven 등록 하지 않으면 로그인에 대 한 응용 프로그램 tooask 프로그램을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="3a2ad-147">Hello 모델의 hello 보안의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="3a2ad-148">앞서 참조 된 hello 샘플 응용 프로그램을 등록 하는으로 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="3a2ad-149">하지만 이 절차는 개발 중인 모든 앱에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="3a2ad-150">한 테넌트에 응용 프로그램과 Web API를 모두 배치하는 이유가 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="3a2ad-151">짐작할 수에 있는 것처럼 다른 테넌트에서 Azure AD에 등록된 외부 API에 액세스하는 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="3a2ad-152">이렇게 하면 고객 됩니다 tooconsent toohello hello 응용 프로그램에 API hello 사용 하 라는 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="3a2ad-153">iOS용 Active Directory 인증 라이브러리가 자동으로 동의 과정을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="3a2ad-154">고급 기능을 살펴볼 때 이것이 hello 작업 필요한 tooaccess hello 제품군에서 다른 서비스 공급자 뿐만 아니라 Azure 및 Office, Microsoft Api의 중요 한 부분이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="3a2ad-155">이제 web API와 hello 대상 응용 프로그램을 등록 하기 때문에 동일한 테 넌 트, 동의 프롬프트 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="3a2ad-156">이 경우 일반적으로 hello 자신의 회사 toouse에 대 한 응용 프로그램을 개발 하는 경우 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="3a2ad-157">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3a2ad-158">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-158">On hello top bar, click your account.</span></span> <span data-ttu-id="3a2ad-159">Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="3a2ad-160">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="3a2ad-161">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="3a2ad-162">Hello 응용 프로그램에 대 한 식별 이름을 입력 하세요 (예를 들어 **TodoListClient Android**)을 선택 **네이티브 클라이언트 응용 프로그램**를 클릭 하 고 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="3a2ad-163">Hello에 대 한 리디렉션 URI를 입력 `http://TodoListClient`합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="3a2ad-164">**마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-164">Click **Finish**.</span></span>
7. <span data-ttu-id="3a2ad-165">Hello 응용 프로그램 ID 값을 찾을 hello 응용 프로그램 페이지에서 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="3a2ad-166">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="3a2ad-167">Hello에서 **설정** 페이지에서 **필요한 권한** 선택 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="3a2ad-168">찾기 및 TodoListService 선택, 추가 hello **액세스 TodoListService** 에 따른 권한 **위임 된 권한**를 클릭 하 고 **수행**합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="3a2ad-169">Maven으로 toobuild, pom.xml hello 최상위 수준에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="3a2ad-170">선택한 디렉터리에 다음 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="3a2ad-171">Hello에 hello 단계를 따라 [Maven 환경을 Android 용 필수 구성 요소 tooset](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="3a2ad-172">Hello 에뮬레이터 SDK 19로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="3a2ad-173">Hello 리포지토리를 복제 toohello 루트 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="3a2ad-174">다음 명령을 실행합니다. `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="3a2ad-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="3a2ad-175">Hello 디렉터리 toohello 빠른 시작 예제를 변경 합니다.`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="3a2ad-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="3a2ad-176">다음 명령을 실행합니다. `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="3a2ad-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="3a2ad-177">Hello 응용 프로그램을 시작 하는 것이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="3a2ad-178">테스트 사용자 자격 증명 tootry를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="3a2ad-179">JAR 패키지 hello AAR 패키지 옆에 제출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="3a2ad-180">4 단계: Android ADAL hello를 다운로드 하 고 tooyour Eclipse 작업 공간 추가</span><span class="sxs-lookup"><span data-stu-id="3a2ad-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="3a2ad-181">만들었고 있습니다 toohave 쉽게 여러 옵션 toouse ADAL Android 프로젝트에서:</span><span class="sxs-lookup"><span data-stu-id="3a2ad-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="3a2ad-182">Eclipse 및 링크 tooyour 응용 프로그램으로 hello 소스 코드 tooimport이이 라이브러리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="3a2ad-183">Android Studio를 사용 하는 hello AAR 패키지 형식 및 참조 hello 바이너리를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="3a2ad-184">옵션 1: 소스 Zip 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a2ad-184">Option 1: Source Zip</span></span>
<span data-ttu-id="3a2ad-185">hello 소스 코드의 복사본 toodownload 클릭 **zip 파일 다운로드** hello hello 페이지의 오른쪽에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="3a2ad-186">또는 [GitHub에서 다운로드](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="3a2ad-187">옵션 2: Git를 통해 소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a2ad-187">Option 2: Source via Git</span></span>
<span data-ttu-id="3a2ad-188">tooget hello 소스 코드의 hello Git 통해 SDK를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="3a2ad-189">옵션 3: Gradle을 통해 이진 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a2ad-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="3a2ad-190">Hello Maven 중앙 리포지토리에서 hello 이진 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="3a2ad-191">Android Studio에서 프로젝트에 다음과 같이 hello AAR 패키지를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="3a2ad-192">옵션 4: Maven을 통해 AAR 가져오기</span><span class="sxs-lookup"><span data-stu-id="3a2ad-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="3a2ad-193">플러그 인 M2Eclipse hello를 사용 하 여 hello 종속성 pom.xml 파일에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="3a2ad-194">옵션 5: JAR 패키지 hello 라이브러리 폴더</span><span class="sxs-lookup"><span data-stu-id="3a2ad-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="3a2ad-195">Hello Maven 리포지토리에서 hello JAR 파일을 가져와서 하는 hello에 **libs** 프로젝트의 폴더에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="3a2ad-196">Toocopy hello 필요한 리소스 tooyour 프로젝트도 필요 하면 hello JAR 패키지에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="3a2ad-197">5 단계: 참조 tooAndroid ADAL tooyour 프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="3a2ad-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="3a2ad-198">참조 tooyour 프로젝트를 추가 하 고 Android 라이브러리로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="3a2ad-199">확실히 모르겠으면 어떻게 toodo이 hello에 대 한 자세한 정보를 얻을 수 있습니다 [Android Studio 사이트](http://developer.android.com/tools/projects/projects-eclipse.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="3a2ad-200">프로젝트 설정으로 디버깅을 위해 hello 프로젝트 종속성을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="3a2ad-201">프로젝트의 AndroidManifest.xml 파일 tooinclude를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="3a2ad-202">기본 활동에서 AuthenticationContext의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="3a2ad-203">이 호출의 hello 세부 정보는이 항목의 hello 범위 설명 하지만 좋은 시작 hello 확인 하 여 [Android Native Client 샘플](https://github.com/AzureADSamples/NativeClient-Android)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="3a2ad-204">다음 예제는 hello, SharedPreferences hello 기본 캐시 되며 기관에에서는 hello 형식의 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="3a2ad-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="3a2ad-205">Hello 사용자 자격 증명을 입력 하 고 인증 코드를 받은 후 AuthenticationActivity이 코드 블록 toohandle hello 끝을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="3a2ad-206">토큰에 대 한 tooask 콜백을 정의:</span><span class="sxs-lookup"><span data-stu-id="3a2ad-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="3a2ad-207">마지막으로 해당 콜백을 사용하여 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="3a2ad-208">Hello 매개 변수 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="3a2ad-209">*리소스* 는 필수 이며 tooaccess를 시도 하는 hello 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="3a2ad-210">*clientid*는 필수 항목이며 Azure AD에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="3a2ad-211">*RedirectUri* 필요한 toobe hello acquireToken 호출에 대 한 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="3a2ad-212">패키지 이름으로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="3a2ad-213">*PromptBehavior* tooask 자격 증명 tooskip hello 캐시 및 쿠키는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="3a2ad-214">*콜백* hello 권한 부여 코드는 토큰에 대해 교환 된 후에 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="3a2ad-215">여기에는 액세스 토큰, 만료 날짜 및 ID 토큰 정보를 포함하는 AuthenticationResult의 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="3a2ad-216">*acquireTokenSilent*는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="3a2ad-217">Toohandle 캐싱 및 새로 고침 토큰을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="3a2ad-218">또한 hello 동기화 버전을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-218">It also provides hello sync version.</span></span> <span data-ttu-id="3a2ad-219">*userId*가 매개 변수로 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="3a2ad-220">이 연습을 사용 하 여 어떤 필요한 toosuccessfully 통합 하면 Azure Active Directory에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="3a2ad-221">이 작업의 추가 예제에 대 한 방문 hello AzureADSamples / GitHub의 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="3a2ad-222">중요 정보</span><span class="sxs-lookup"><span data-stu-id="3a2ad-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="3a2ad-223">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="3a2ad-223">Customization</span></span>
<span data-ttu-id="3a2ad-224">응용 프로그램 리소스에서 라이브러리 프로젝트 리소스를 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="3a2ad-225">앱을 빌드할 때 이러한 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-225">This happens when your app is being built.</span></span> <span data-ttu-id="3a2ad-226">이러한 이유로 인증 활동 레이아웃 hello 원하는 방식으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="3a2ad-227">(WebView)를 사용 하 여 해당 ADAL hello 컨트롤의 ID가 있는지 tookeep hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="3a2ad-228">Broker</span><span class="sxs-lookup"><span data-stu-id="3a2ad-228">Broker</span></span>
<span data-ttu-id="3a2ad-229">Microsoft Intune 회사 포털 앱 hello hello broker 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="3a2ad-230">AccountManager에 hello 계정이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="3a2ad-231">hello 계정 형식이 "com.microsoft.workaccount."</span><span class="sxs-lookup"><span data-stu-id="3a2ad-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="3a2ad-232">AccountManager에서는 단일 SSO 계정만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="3a2ad-233">Hello 앱 중 하나에 대 한 hello 장치 챌린지를 완료 한 후 hello 사용자에 대 한 SSO 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="3a2ad-234">ADAL이이 인증자에 단일 사용자 계정을 만들어지고 tooskip 하지 않으려는 경우 hello 브로커 계정을 사용 하 여 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="3a2ad-235">사용 하는 hello 브로커 사용자를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="3a2ad-236">Broker 사용에 대 한 특별 한 RedirectUri tooregister를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="3a2ad-237">RedirectUri hello 형식으로 되어 `msauth://packagename/Base64UrlencodedSignature`합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="3a2ad-238">Hello 스크립트 brokerRedirectPrint.ps1 또는 hello API 호출 mContext.getBrokerRedirectUri 사용 하 여 앱에 대 한 프로그램 RedirectUri를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="3a2ad-239">hello 서명 인증서를 서명 하는 관련된 tooyour입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="3a2ad-240">hello 현재 브로커 모델 한 명의 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-240">hello current broker model is for one user.</span></span> <span data-ttu-id="3a2ad-241">AuthenticationContext은 hello API 메서드 tooget hello 브로커 사용자를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="3a2ad-242">응용 프로그램 매니페스트에서 사용 권한, toouse AccountManager 계정 다음 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="3a2ad-243">자세한 내용은 참조 hello [hello Android 사이트 AccountManager 정보](http://developer.android.com/reference/android/accounts/AccountManager.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="3a2ad-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="3a2ad-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="3a2ad-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="3a2ad-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="3a2ad-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="3a2ad-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="3a2ad-247">기관 URL 및 AD FS</span><span class="sxs-lookup"><span data-stu-id="3a2ad-247">Authority URL and AD FS</span></span>
<span data-ttu-id="3a2ad-248">Active Directory Federation Services (AD FS)의 인스턴스 검색 tooturn 필요 하 고 false hello AuthenticationContext 생성자에 전달 되므로 STS 프로덕션으로 인식 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="3a2ad-249">hello 기관 URL STS 인스턴스가 필요 하며 [테 넌 트 이름](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="3a2ad-250">캐시 항목 쿼리</span><span class="sxs-lookup"><span data-stu-id="3a2ad-250">Querying cache items</span></span>
<span data-ttu-id="3a2ad-251">ADAL은 일부 간단한 캐시 쿼리 함수를 사용하여 SharedPreferences에서 기본 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="3a2ad-252">사용 하 여 AuthenticationContext에서 hello 현재 캐시를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="3a2ad-253">Toocustomize 하려는 경우에 캐시 구현에 제공할 수 있습니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="3a2ad-254">프롬프트 동작</span><span class="sxs-lookup"><span data-stu-id="3a2ad-254">Prompt behavior</span></span>
<span data-ttu-id="3a2ad-255">ADAL 옵션 toospecify 프롬프트 동작을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="3a2ad-256">PromptBehavior.Auto는 hello 새로 고침 토큰이 유효 하지 않은 한 사용자 자격 증명이 필요한 경우 hello UI를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="3a2ad-257">PromptBehavior.Always를 건너뛰어 hello 캐시 사용량 항상 hello UI를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="3a2ad-258">캐시 및 새로 고침의 자동 토큰 요청</span><span class="sxs-lookup"><span data-stu-id="3a2ad-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="3a2ad-259">자동 토큰 요청 hello UI 팝업을 사용 하지 않는 및 활동 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="3a2ad-260">사용 가능한 경우 hello 캐시에서 토큰을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="3a2ad-261">Hello 토큰이 만료 된 경우이 메서드 toorefresh를 시도 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="3a2ad-262">Hello 새로 고침 토큰은 만료 또는 실패 한 경우 AuthenticationException 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="3a2ad-263">이 메서드를 사용하여 동기화를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="3a2ad-264">Null toocallback 설정 하거나 acquireTokenSilentSync를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="3a2ad-265">진단</span><span class="sxs-lookup"><span data-stu-id="3a2ad-265">Diagnostics</span></span>
<span data-ttu-id="3a2ad-266">다음은 문제를 진단 하는 것에 대 한 정보의 hello 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="3a2ad-267">예외</span><span class="sxs-lookup"><span data-stu-id="3a2ad-267">Exceptions</span></span>
* <span data-ttu-id="3a2ad-268">로그</span><span class="sxs-lookup"><span data-stu-id="3a2ad-268">Logs</span></span>
* <span data-ttu-id="3a2ad-269">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="3a2ad-269">Network traces</span></span>

<span data-ttu-id="3a2ad-270">상관 관계 Id는 hello 라이브러리에서 중앙 toohello 진단 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="3a2ad-271">Toocorrelate는 ADAL 요청 코드에서 다른 작업을 사용 하려는 경우에 요청 별로 상관 관계 Id를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="3a2ad-272">상관 관계 ID를 설정하지 않으면, ADAL에서 임의의 항목을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="3a2ad-273">모든 메시지를 로그 하 고 hello 상관 관계 id입니다. 그런 다음 네트워크 호출을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="3a2ad-274">hello 자체 ID도 변경 요청이 있을 때마다 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="3a2ad-275">예외</span><span class="sxs-lookup"><span data-stu-id="3a2ad-275">Exceptions</span></span>
<span data-ttu-id="3a2ad-276">예외 진단 먼저 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="3a2ad-277">Tooprovide 유용한 오류 메시지 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="3a2ad-278">유용하지 않은 오류 메시지가 표시되면 문제를 정리한 후 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="3a2ad-279">모델 및 SDK 번호와 같은 장치 정보도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="3a2ad-280">로그</span><span class="sxs-lookup"><span data-stu-id="3a2ad-280">Logs</span></span>
<span data-ttu-id="3a2ad-281">Hello 라이브러리 toogenerate를 구성할 수 있습니다 toohelp를 사용할 수 있는 로그 메시지 문제를 진단 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="3a2ad-282">Hello 다음 tooconfigure 생성 되는 ADAL toohand 각 로그 메시지에서 사용 되도록 하는 콜백을 호출 하 여 로깅을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="3a2ad-283">메시지는 hello 코드 다음에 표시 된 대로 tooa 사용자 지정 로그 파일을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="3a2ad-284">그러나 장치에서 로그를 얻는 표준 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="3a2ad-285">이 작업에 도움이 되는 몇 가지 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-285">There are some services that can help you with this.</span></span> <span data-ttu-id="3a2ad-286">와 같은 직접 보내는 hello 파일 tooa 서버를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="3a2ad-287">다음은 hello 로깅 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-287">These are hello logging levels:</span></span>
* <span data-ttu-id="3a2ad-288">오류(예외)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-288">Error (exceptions)</span></span>
* <span data-ttu-id="3a2ad-289">경고</span><span class="sxs-lookup"><span data-stu-id="3a2ad-289">Warn (warning)</span></span>
* <span data-ttu-id="3a2ad-290">정보(정보 제공용)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-290">Info (information purposes)</span></span>
* <span data-ttu-id="3a2ad-291">자세한 정보 표시(자세한 내용)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-291">Verbose (more details)</span></span>

<span data-ttu-id="3a2ad-292">다음과 같이 hello 로그 수준 설정:</span><span class="sxs-lookup"><span data-stu-id="3a2ad-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="3a2ad-293">모든 로그 메시지가 추가 tooany 사용자 지정 로그 콜백을 toologcat, 보내집니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="3a2ad-294">다음과 같이 로그 tooa 파일 logcat에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="3a2ad-295">Adb 명령에 대 한 자세한 참조 hello [hello Android 사이트 logcat 정보](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="3a2ad-296">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="3a2ad-296">Network traces</span></span>
<span data-ttu-id="3a2ad-297">ADAL을 생성 하는 다양 한 도구 toocapture hello HTTP 트래픽을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="3a2ad-298">Hello OAuth 프로토콜에 익숙한 경우 또는 tooprovide 진단 정보 tooMicrosoft 또는 기타 지원 채널을 필요한 경우 가장 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="3a2ad-299">Fiddler는 hello 쉬운 HTTP 추적 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="3a2ad-300">사용 하 여 hello 다음 링크 tooset toocorrectly 레코드 ADAL 네트워크 트래픽 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="3a2ad-301">Fiddler 또는 Charles toobe 유용한와 같은 추적 도구를 구성 해야 암호화 되지 않은 toorecord SSL 트래픽을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="3a2ad-302">이 방식으로 생성된 추적에는 액세스 토큰, 사용자 이름 및 암호와 같은 높은 권한이 필요한 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="3a2ad-303">프로덕션 계정을 사용하는 경우 이러한 추적 정보를 제3자와 공유하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="3a2ad-304">Toosupply 순서 tooget 지원의 추적 toosomeone 필요한 경우 공유 유의 하지 않는 사용자 이름 및 암호와 임시 계정을 사용 하 여 hello 문제를 재현 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="3a2ad-305">Hello Telerik 웹 사이트에서: [설정을를 Fiddler에 대 한 Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="3a2ad-306">GitHub: [ADAL에 대한 Fiddler 규칙 구성(영문)](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="3a2ad-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="3a2ad-307">대화 상자 모드</span><span class="sxs-lookup"><span data-stu-id="3a2ad-307">Dialog mode</span></span>
<span data-ttu-id="3a2ad-308">활동이 없는 hello acquireToken 메서드 확인 대화를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="3a2ad-309">암호화</span><span class="sxs-lookup"><span data-stu-id="3a2ad-309">Encryption</span></span>
<span data-ttu-id="3a2ad-310">ADAL은 hello 토큰 및 SharedPreferences에서 기본적으로 저장소를 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="3a2ad-311">Hello StorageHelper 클래스 toosee hello 세부 정보를 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="3a2ad-312">Android에서는 개인 키의 보안 저장소인 4.3(API 18)용 Android Keystore를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="3a2ad-313">ADAL은 API 18 이상에 이 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="3a2ad-314">더 낮은 SDK 버전에 대 한 ADAL toouse를 원하는 경우 tooprovide AuthenticationSettings.INSTANCE.setSecretKey에 비밀 키를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="3a2ad-315">OAuth2 전달자 챌린지</span><span class="sxs-lookup"><span data-stu-id="3a2ad-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="3a2ad-316">hello AuthenticationParameters 클래스 기능 tooget authorization_uri hello OAuth2 전달자 챌린지를에서 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="3a2ad-317">WebView의 세션 쿠키</span><span class="sxs-lookup"><span data-stu-id="3a2ad-317">Session cookies in WebView</span></span>
<span data-ttu-id="3a2ad-318">Android WebView hello 응용 프로그램을 닫은 후 세션 쿠키를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="3a2ad-319">다음 샘플 코드를 사용하여 이 문제를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="3a2ad-320">쿠키에 대 한 자세한 참조 hello [hello Android 사이트 CookieSyncManager 정보](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="3a2ad-321">리소스 재정의</span><span class="sxs-lookup"><span data-stu-id="3a2ad-321">Resource overrides</span></span>
<span data-ttu-id="3a2ad-322">hello ADAL 라이브러리 ProgressDialog 메시지에 대 한 영어 문자열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="3a2ad-323">지역화된 문자열을 사용하려는 경우 응용 프로그램이 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="3a2ad-324">NTLM 대화 상자</span><span class="sxs-lookup"><span data-stu-id="3a2ad-324">NTLM dialog box</span></span>
<span data-ttu-id="3a2ad-325">ADAL 버전 1.1.0 WebViewClient에서 hello onReceivedHttpAuthRequest 이벤트를 통해 처리 되는 NTLM 대화 상자를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="3a2ad-326">Hello 레이아웃과 hello 대화 상자에 대 한 문자열을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="3a2ad-327">앱 간 SSO</span><span class="sxs-lookup"><span data-stu-id="3a2ad-327">Cross-app SSO</span></span>
<span data-ttu-id="3a2ad-328">자세한 내용은 [어떻게 tooenable ADAL을 사용 하 여 android 응용 프로그램 간 SSO](active-directory-sso-android.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3a2ad-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
