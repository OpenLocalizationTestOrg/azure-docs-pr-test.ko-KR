---
title: "Azure AD Android 시작 | Microsoft Docs"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Android 응용 프로그램 빌드 방법입니다."
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="0cfd3-103">Android 앱에 Azure AD 통합</span><span class="sxs-lookup"><span data-stu-id="0cfd3-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="0cfd3-104">몇 분 안에 Azure AD를 실행할 수 있는 새로운 [개발자 포털](https://identity.microsoft.com/Docs/Android)의 미리 보기를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="0cfd3-105">개발자 포털은 앱을 등록하고 코드에 Azure AD를 통합하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="0cfd3-106">이 과정을 완료하면 테넌트에서 사용자를 인증할 수 있는 간단한 응용 프로그램 및 토큰을 수락하고 유효성 검사를 수행할 수 있는 백 엔드가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="0cfd3-107">데스크톱 응용 프로그램을 개발하는 경우 Azure AD(Azure Active Directory)를 사용하면 간단하고 편리하게 온-프레미스 Active Directory 계정을 사용하여 사용자를 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="0cfd3-108">또한 응용 프로그램에서 Office 365 API 또는 Azure API와 같이 Azure AD를 통해 보호되는 웹 API를 안전하게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="0cfd3-109">보호된 리소스에 액세스해야 하는 Android 클라이언트의 경우 Azure AD는 ADAL(Active Directory 인증 라이브러리)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="0cfd3-110">ADAL의 유일한 용도는 앱이 쉽게 액세스 토큰을 가져오도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="0cfd3-111">액세스 토큰을 얼마나 쉽게 가져올 수 있는지 보여 주기 위해 다음을 수행하는 Android 할 일 목록 응용 프로그램을 작성해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="0cfd3-112">[OAuth 2.0 인증 프로토콜](https://msdn.microsoft.com/library/azure/dn645545.aspx)을 사용하여 To-Do List API를 호출하기 위한 액세스 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="0cfd3-113">사용자의 할 일 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="0cfd3-114">사용자를 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-114">Signs out users.</span></span>

<span data-ttu-id="0cfd3-115">시작하려면 사용자를 만들고 응용 프로그램을 등록할 수 있는 Azure AD 테넌트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="0cfd3-116">테넌트가 아직 없는 경우 [얻는 방법을 알아보세요](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="0cfd3-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="0cfd3-117">1단계: Node.js REST API TODO 샘플 서버 다운로드 및 실행</span><span class="sxs-lookup"><span data-stu-id="0cfd3-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="0cfd3-118">Node.js REST API TODO 샘플은 Azure AD용 단일 테넌트 To-Do REST API를 빌드하기 위한 기존 샘플에서도 작동하도록 특수하게 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="0cfd3-119">다음은 빠른 시작을 위한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="0cfd3-120">설정 방법에 대한 자세한 내용은 [Node.js에 대한 Microsoft Azure Active Directory 샘플 REST API 서비스](active-directory-devquickstarts-webapi-nodejs.md)에 있는 기존의 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="0cfd3-121">2단계: Azure AD 테넌트에 Web API 등록</span><span class="sxs-lookup"><span data-stu-id="0cfd3-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="0cfd3-122">Active Directory는 두 가지 유형의 응용 프로그램 추가를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="0cfd3-123">사용자에게 서비스를 제공하는 Web API</span><span class="sxs-lookup"><span data-stu-id="0cfd3-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="0cfd3-124">해당 Web API에 액세스하는 응용 프로그램(웹 또는 장치에서 실행)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="0cfd3-125">이 단계에서는 이 샘플을 테스트하기 위해 로컬로 실행하는 Web API를 등록할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="0cfd3-126">일반적으로 이 Web API는 앱에서 액세스할 기능을 제공하는 REST 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="0cfd3-127">Azure AD는 끝점을 보호하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="0cfd3-128">앞에서 참조한 TODO REST API를 등록하는 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="0cfd3-129">하지만 Azure Active Directory에서 보호하려는 모든 Web API에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="0cfd3-130">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0cfd3-131">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-131">On the top bar, click your account.</span></span> <span data-ttu-id="0cfd3-132">**디렉터리** 목록에서 응용 프로그램을 등록할 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="0cfd3-133">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0cfd3-134">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="0cfd3-135">친숙한 응용 프로그램 이름(예:**TodoListService**)을 입력하고 **웹 응용 프로그램 및/또는 Web API**를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="0cfd3-136">로그온 URL에 대해서는 샘플의 기준 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="0cfd3-137">기본적으로 `https://localhost:8080`입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="0cfd3-138">등록을 완료하려면 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="0cfd3-139">Azure Portal에 있는 상태에서 응용 프로그램 페이지로 이동한 후 응용 프로그램 ID 값을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="0cfd3-140">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="0cfd3-141">**설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다(`https://<your_tenant_name>/TodoListService` 입력).</span><span class="sxs-lookup"><span data-stu-id="0cfd3-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="0cfd3-142">`<your_tenant_name>`을 Azure AD 테넌트의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="0cfd3-143">3단계: 샘플 Android 네이티브 클라이언트 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="0cfd3-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="0cfd3-144">이 샘플에서는 웹 응용 프로그램을 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-144">You must register your web application in this sample.</span></span> <span data-ttu-id="0cfd3-145">이렇게 하면 응용 프로그램이 방금 등록한 Web API와 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="0cfd3-146">등록되지 않은 응용 프로그램의 경우 로그인을 요청하더라도 Azure AD에서 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="0cfd3-147">이것은 모델 보안의 한 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-147">That's part of the security of the model.</span></span>

<span data-ttu-id="0cfd3-148">앞에서 참조한 응용 프로그램 예제를 등록하는 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="0cfd3-149">하지만 이 절차는 개발 중인 모든 앱에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="0cfd3-150">한 테넌트에 응용 프로그램과 Web API를 모두 배치하는 이유가 궁금할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="0cfd3-151">짐작할 수에 있는 것처럼 다른 테넌트에서 Azure AD에 등록된 외부 API에 액세스하는 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="0cfd3-152">이렇게 하면 응용 프로그램에서 API 사용에 동의할지 묻는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="0cfd3-153">iOS용 Active Directory 인증 라이브러리가 자동으로 동의 과정을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="0cfd3-154">고급 기능을 좀 더 살펴보게 되면 다른 서비스 공급자는 물론 Azure 및 Office에서 Microsoft API 모음에 액세스하는 데 필요한 작업의 중요한 부분이라는 것을 알 수 있게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="0cfd3-155">이제 Web API와 응용 프로그램을 동일한 테넌트에서 등록했으므로 동의를 묻는 메시지는 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="0cfd3-156">일반적으로 회사를 위해서만 응용 프로그램을 개발하는 경우가 여기에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="0cfd3-157">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0cfd3-158">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-158">On the top bar, click your account.</span></span> <span data-ttu-id="0cfd3-159">**디렉터리** 목록에서 응용 프로그램을 등록할 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="0cfd3-160">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0cfd3-161">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="0cfd3-162">응용 프로그램의 이름(예: **TodoListClient-Android**)을 입력하고 **네이티브 클라이언트 응용 프로그램**을 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="0cfd3-163">리디렉션 URI로 `http://TodoListClient`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="0cfd3-164">**Finish**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-164">Click **Finish**.</span></span>
7. <span data-ttu-id="0cfd3-165">응용 프로그램 페이지에서 응용 프로그램 ID 값을 찾아 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="0cfd3-166">나중에 이 응용 프로그램을 구성하는 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="0cfd3-167">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="0cfd3-168">TodoListService를 찾은 후 선택하고 **위임된 사용 권한**에서 **TodoListService 액세스** 사용 권한을 추가하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="0cfd3-169">Maven으로 빌드하려면 최상위 수준에서 pom.xml을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="0cfd3-170">선택한 디렉터리에 다음 리포지토리를 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="0cfd3-171">[Android용 Maven 환경을 설정하기 위한 필수 조건 섹션](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android)의 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="0cfd3-172">SDK 19로 에뮬레이터를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="0cfd3-173">리포지토리를 복제한 루트 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="0cfd3-174">다음 명령을 실행합니다. `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="0cfd3-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="0cfd3-175">빠른 시작 샘플 `cd samples\hello`로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="0cfd3-176">다음 명령을 실행합니다. `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="0cfd3-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="0cfd3-177">앱이 시작되는 것을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-177">You should see the app starting.</span></span>
8. <span data-ttu-id="0cfd3-178">테스트 사용자 자격 증명을 입력하여 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="0cfd3-179">AAR 패키지 외에 JAR 패키지가 제출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="0cfd3-180">4단계: Android ADAL을 다운로드한 후 Eclipse 작업 영역에 추가</span><span class="sxs-lookup"><span data-stu-id="0cfd3-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="0cfd3-181">사용자가 Android 프로젝트에서 ADAL을 사용하기 위한 여러 옵션을 사용할 수 있도록 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="0cfd3-182">소스 코드를 사용하여 Eclipse에 이 라이브러리를 가져온 후 응용 프로그램에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="0cfd3-183">Android Studio를 사용하는 경우 AAR 패키지 형식을 사용하고 이진 파일을 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="0cfd3-184">옵션 1: 소스 Zip 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cfd3-184">Option 1: Source Zip</span></span>
<span data-ttu-id="0cfd3-185">소스 코드의 복사본을 다운로드하려면 페이지 오른쪽에서 **ZIP 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="0cfd3-186">또는 [GitHub에서 다운로드](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="0cfd3-187">옵션 2: Git를 통해 소스 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cfd3-187">Option 2: Source via Git</span></span>
<span data-ttu-id="0cfd3-188">Git를 통해 SDK 원본 코드를 가져오려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="0cfd3-189">옵션 3: Gradle을 통해 이진 파일 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cfd3-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="0cfd3-190">Maven 중앙 리포지토리에서 이진 파일을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="0cfd3-191">AAR 패키지는 Android Studio의 프로젝트에 다음과 같이 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="0cfd3-192">옵션 4: Maven을 통해 AAR 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cfd3-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="0cfd3-193">M2Eclipse 플러그 인을 사용하는 경우 pom.xml 파일에 대한 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="0cfd3-194">옵션 5: libs 폴더 안에 JAR 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="0cfd3-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="0cfd3-195">maven 리포지토리에서 JAR 파일을 가져와 프로젝트의 **libs** 폴더에 놓을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="0cfd3-196">JAR 패키지에는 필수 리소스가 들어 있지 않으므로 이러한 필수 리소스를 프로젝트에도 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="0cfd3-197">5단계: 프로젝트에 Android ADAL에 대한 참조 추가</span><span class="sxs-lookup"><span data-stu-id="0cfd3-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="0cfd3-198">프로젝트에 대한 참조를 추가하고 Android 라이브러리로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="0cfd3-199">작업을 수행하는 방법을 잘 모르는 경우 [Android Studio 사이트](http://developer.android.com/tools/projects/projects-eclipse.html)에서 자세한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="0cfd3-200">디버깅하기 위해 프로젝트 종속성을 프로젝트 설정에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="0cfd3-201">다음을 포함하도록 프로젝트의 AndroidManifest.xml 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="0cfd3-202">기본 활동에서 AuthenticationContext의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="0cfd3-203">이 호출의 세부 정보는 이 항목에서 다루지 않지만 [Android 네이티브 클라이언트 샘플](https://github.com/AzureADSamples/NativeClient-Android)에서 유용한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="0cfd3-204">다음 예제에서 SharedPreferences는 기본 캐시이며 권한은 `https://login.microsoftonline.com/yourtenant.onmicrosoft.com` 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="0cfd3-205">사용자가 자격 증명을 입력하고 권한 부여 코드를 받은 후에 AuthenticationActivity의 끝을 처리하도록 이 코드 블록을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="0cfd3-206">토큰을 요청하려면 콜백을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="0cfd3-207">마지막으로 해당 콜백을 사용하여 토큰을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="0cfd3-208">매개 변수에 대한 설명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="0cfd3-209">*resource*는 필수 항목이며 액세스하려는 리소스를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="0cfd3-210">*clientid*는 필수 항목이며 Azure AD에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="0cfd3-211">*RedirectUri*는 acquireToken 호출의 경우에는 제공하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="0cfd3-212">패키지 이름으로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="0cfd3-213">*PromptBehavior*는 자격 증명을 요청하여 캐시 및 쿠키를 건너뛰는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="0cfd3-214">권한 부여 코드가 토큰과 교환되면 *callback*이 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="0cfd3-215">여기에는 액세스 토큰, 만료 날짜 및 ID 토큰 정보를 포함하는 AuthenticationResult의 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="0cfd3-216">*acquireTokenSilent*는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="0cfd3-217">호출하여 캐싱 및 토큰 새로 고침을 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="0cfd3-218">동기화 버전도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-218">It also provides the sync version.</span></span> <span data-ttu-id="0cfd3-219">*userId*가 매개 변수로 수락됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="0cfd3-220">이 연습 과정을 사용하여 Azure Active Directory에 성공적으로 통합하는 데 필요한 기술과 지식을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="0cfd3-221">이 작업의 추가 예제를 보려면 GitHub의 AzureADSamples/ 리포지토리를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="0cfd3-222">중요 정보</span><span class="sxs-lookup"><span data-stu-id="0cfd3-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="0cfd3-223">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="0cfd3-223">Customization</span></span>
<span data-ttu-id="0cfd3-224">응용 프로그램 리소스에서 라이브러리 프로젝트 리소스를 덮어쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="0cfd3-225">앱을 빌드할 때 이러한 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-225">This happens when your app is being built.</span></span> <span data-ttu-id="0cfd3-226">이러한 이유로 인증 활동 레이아웃 원하는 방식으로 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="0cfd3-227">ADAL이 사용하는 컨트롤의 ID(WebView)를 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="0cfd3-228">Broker</span><span class="sxs-lookup"><span data-stu-id="0cfd3-228">Broker</span></span>
<span data-ttu-id="0cfd3-229">Microsoft Intune의 회사 포털 앱은 broker 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="0cfd3-230">AccountManager에서 계정이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-230">The account is created in AccountManager.</span></span> <span data-ttu-id="0cfd3-231">계정 형식은 "com.microsoft.workaccount"입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="0cfd3-232">AccountManager에서는 단일 SSO 계정만 허용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="0cfd3-233">앱 중 하나에 대한 장치 챌린지를 완료한 후에 이 사용자에 대한 SSO 쿠키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="0cfd3-234">이 인증자에서 사용자 계정이 하나 만들어지고 해당 계정을 건너뛰지 않도록 선택한 경우 ADAL은 broker 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="0cfd3-235">다음과 같이 broker 사용자를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="0cfd3-236">broker 사용을 위해 특수한 RedirectUri를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="0cfd3-237">RedirectUri는 `msauth://packagename/Base64UrlencodedSignature` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="0cfd3-238">스크립트 brokerRedirectPrint.ps1 또는 API 호출 mContext.getBrokerRedirectUri를 사용하여 앱에 대한 RedirectUri를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="0cfd3-239">서명은 인증서 서명과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="0cfd3-240">현재 broker 모델은 단일 사용자에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-240">The current broker model is for one user.</span></span> <span data-ttu-id="0cfd3-241">AuthenticationContext는 broker 사용자를 가져오기 위한 API 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="0cfd3-242">앱 매니페스트에는 AccountManager 계정을 사용할 수 있는 다음 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="0cfd3-243">자세한 내용은 [Android 사이트에서 AccountManager 정보](http://developer.android.com/reference/android/accounts/AccountManager.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="0cfd3-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="0cfd3-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="0cfd3-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="0cfd3-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="0cfd3-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="0cfd3-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="0cfd3-247">기관 URL 및 AD FS</span><span class="sxs-lookup"><span data-stu-id="0cfd3-247">Authority URL and AD FS</span></span>
<span data-ttu-id="0cfd3-248">AD FS(Active Directory Federation Services)는 프로덕션 STS로 인식되지 않으므로 인스턴스 검색을 해제하고 AuthenticationContext 생성자에 false를 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="0cfd3-249">기관 URL에는 STS 인스턴스 및 [테넌트 이름](https://login.microsoftonline.com/yourtenant.onmicrosoft.com)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="0cfd3-250">캐시 항목 쿼리</span><span class="sxs-lookup"><span data-stu-id="0cfd3-250">Querying cache items</span></span>
<span data-ttu-id="0cfd3-251">ADAL은 일부 간단한 캐시 쿼리 함수를 사용하여 SharedPreferences에서 기본 캐시를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="0cfd3-252">다음을 사용하여 AuthenticationContext에서 현재 캐시를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="0cfd3-253">사용자 지정하려는 경우 캐시 구현을 제공할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="0cfd3-254">프롬프트 동작</span><span class="sxs-lookup"><span data-stu-id="0cfd3-254">Prompt behavior</span></span>
<span data-ttu-id="0cfd3-255">ADAL은 프롬프트 동작을 지정하기 위한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="0cfd3-256">새로 고침 토큰이 올바르지 않고 사용자 자격 증명이 필요한 경우 PromptBehavior.Auto가 UI를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="0cfd3-257">PromptBehavior.Always는 캐시 사용을 건너뛰고 항상 UI를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="0cfd3-258">캐시 및 새로 고침의 자동 토큰 요청</span><span class="sxs-lookup"><span data-stu-id="0cfd3-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="0cfd3-259">자동 토큰 요청은 UI 팝업을 사용하지 않으며 작업이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="0cfd3-260">사용 가능한 경우 캐시에서 토큰을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="0cfd3-261">토큰이 만료되면 이 메서드는 새로 고침을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="0cfd3-262">새로 고침 토큰이 만료되거나 실패하면 AuthenticationException이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="0cfd3-263">이 메서드를 사용하여 동기화를 호출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="0cfd3-264">callback에 대해 null을 설정하거나 acquireTokenSilentSync를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="0cfd3-265">진단</span><span class="sxs-lookup"><span data-stu-id="0cfd3-265">Diagnostics</span></span>
<span data-ttu-id="0cfd3-266">다음은 문제를 진단하기 위한 정보의 기본 출처입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="0cfd3-267">예외</span><span class="sxs-lookup"><span data-stu-id="0cfd3-267">Exceptions</span></span>
* <span data-ttu-id="0cfd3-268">로그</span><span class="sxs-lookup"><span data-stu-id="0cfd3-268">Logs</span></span>
* <span data-ttu-id="0cfd3-269">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="0cfd3-269">Network traces</span></span>

<span data-ttu-id="0cfd3-270">라이브러리에 포함된 상관 관계 ID가 진단에 핵심적이라는 점도 알아두세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="0cfd3-271">ADAL을 코드의 다른 작업과 상호 연관 지으려면 요청별로 상관 관계 ID를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="0cfd3-272">상관 관계 ID를 설정하지 않으면, ADAL에서 임의의 항목을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="0cfd3-273">모든 로그 메시지 및 네트워크 호출은 상관 관계 ID로 스탬프 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="0cfd3-274">자체 생성된 ID는 요청마다 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="0cfd3-275">예외</span><span class="sxs-lookup"><span data-stu-id="0cfd3-275">Exceptions</span></span>
<span data-ttu-id="0cfd3-276">예외는 첫 번째 진단입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="0cfd3-277">저희는 유용한 오류 메시지를 제공하기 위해 노력하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="0cfd3-278">유용하지 않은 오류 메시지가 표시되면 문제를 정리한 후 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="0cfd3-279">모델 및 SDK 번호와 같은 장치 정보도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="0cfd3-280">로그</span><span class="sxs-lookup"><span data-stu-id="0cfd3-280">Logs</span></span>
<span data-ttu-id="0cfd3-281">문제를 진단하는 데 도움을 주기 위해 사용할 수 있는 로그 메시지를 생성하도록 라이브러리를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="0cfd3-282">다음을 호출하여 ADAL에서 생성되는 각 로그 메시지를 전달하는 데 사용하는 콜백을 구성하도록 로깅을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="0cfd3-283">다음 코드와 같이 사용자 지정 로그 파일에 메시지를 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="0cfd3-284">그러나 장치에서 로그를 얻는 표준 방법은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="0cfd3-285">이 작업에 도움이 되는 몇 가지 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-285">There are some services that can help you with this.</span></span> <span data-ttu-id="0cfd3-286">또한 서버에 파일을 보내는 것과 같은 자체 방법을 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="0cfd3-287">다음은 로깅 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-287">These are the logging levels:</span></span>
* <span data-ttu-id="0cfd3-288">오류(예외)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-288">Error (exceptions)</span></span>
* <span data-ttu-id="0cfd3-289">경고</span><span class="sxs-lookup"><span data-stu-id="0cfd3-289">Warn (warning)</span></span>
* <span data-ttu-id="0cfd3-290">정보(정보 제공용)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-290">Info (information purposes)</span></span>
* <span data-ttu-id="0cfd3-291">자세한 정보 표시(자세한 내용)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-291">Verbose (more details)</span></span>

<span data-ttu-id="0cfd3-292">다음과 같이 로그 수준을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="0cfd3-293">모든 로그 메시지는 사용자 지정 로그 콜백 외에 logcat으로도 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="0cfd3-294">다음과 같이 logcat에서 파일로 로그를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="0cfd3-295">adb 명령에 대한 자세한 내용은 [Android 사이트에서 logcat 정보](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="0cfd3-296">네트워크 추적</span><span class="sxs-lookup"><span data-stu-id="0cfd3-296">Network traces</span></span>
<span data-ttu-id="0cfd3-297">ADAL이 생성하는 HTTP 트래픽을 캡처하기 위해 다양한 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="0cfd3-298">OAuth 프로토콜을 잘 알고 있거나 Microsoft 또는 기타 지원 채널에 진단 정보를 제공해야 할 경우에 이러한 도구를 사용하면 아주 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="0cfd3-299">Fiddler는 가장 쉬운 HTTP 추적 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="0cfd3-300">다음 링크에서 ADAL 네트워크 트래픽을 올바르게 기록하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="0cfd3-301">Fiddler 또는 Charles와 같은 추적 도구가 도움이 되려면, 암호화되지 않은 SSL 트래픽을 기록하도록 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="0cfd3-302">이 방식으로 생성된 추적에는 액세스 토큰, 사용자 이름 및 암호와 같은 높은 권한이 필요한 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="0cfd3-303">프로덕션 계정을 사용하는 경우 이러한 추적 정보를 제3자와 공유하지 않도록 하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="0cfd3-304">지원을 얻기 위해 누군가에게 추적 정보를 제공해야 하는 경우 공유해도 괜찮은 사용자 이름 및 암호를 사용한 임시 계정을 사용하여 문제를 재현하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="0cfd3-305">Telerik 웹 사이트: [Android용 Fiddler 설정(영문)](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="0cfd3-306">GitHub: [ADAL에 대한 Fiddler 규칙 구성(영문)](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span><span class="sxs-lookup"><span data-stu-id="0cfd3-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="0cfd3-307">대화 상자 모드</span><span class="sxs-lookup"><span data-stu-id="0cfd3-307">Dialog mode</span></span>
<span data-ttu-id="0cfd3-308">활동 없는 acquireToken 메서드는 대화 상자 프롬프트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="0cfd3-309">암호화</span><span class="sxs-lookup"><span data-stu-id="0cfd3-309">Encryption</span></span>
<span data-ttu-id="0cfd3-310">ADAL은 기본적으로 토큰을 암호화한 후 SharedPreferences에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="0cfd3-311">StorageHelper 클래스를 확인하여 세부 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="0cfd3-312">Android에서는 개인 키의 보안 저장소인 4.3(API 18)용 Android Keystore를 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="0cfd3-313">ADAL은 API 18 이상에 이 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="0cfd3-314">더 낮은 SDK 버전에 ADAL을 사용하려는 경우 AuthenticationSettings.INSTANCE.setSecretKey에서 비밀 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="0cfd3-315">OAuth2 전달자 챌린지</span><span class="sxs-lookup"><span data-stu-id="0cfd3-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="0cfd3-316">AuthenticationParameters 클래스는 OAuth2 전달자 챌린지에서 authorization_uri를 가져오기 위한 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="0cfd3-317">WebView의 세션 쿠키</span><span class="sxs-lookup"><span data-stu-id="0cfd3-317">Session cookies in WebView</span></span>
<span data-ttu-id="0cfd3-318">앱이 닫힌 후에 Android WebView가 세션 쿠키를 지우지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="0cfd3-319">다음 샘플 코드를 사용하여 이 문제를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="0cfd3-320">쿠키에 대한 자세한 내용은 [Android 사이트에서 CookieSyncManager 정보](http://developer.android.com/reference/android/webkit/CookieSyncManager.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="0cfd3-321">리소스 재정의</span><span class="sxs-lookup"><span data-stu-id="0cfd3-321">Resource overrides</span></span>
<span data-ttu-id="0cfd3-322">ADAL 라이브러리에는 ProgressDialog 메시지에 대한 영어 문자열이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="0cfd3-323">지역화된 문자열을 사용하려는 경우 응용 프로그램이 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="0cfd3-324">NTLM 대화 상자</span><span class="sxs-lookup"><span data-stu-id="0cfd3-324">NTLM dialog box</span></span>
<span data-ttu-id="0cfd3-325">ADAL 버전 1.1.0은 WebViewClient의 onReceivedHttpAuthRequest 이벤트를 통해 처리되는 NTLM 대화 상자를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="0cfd3-326">대화 상자에 대한 레이아웃 및 문자열을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="0cfd3-327">앱 간 SSO</span><span class="sxs-lookup"><span data-stu-id="0cfd3-327">Cross-app SSO</span></span>
<span data-ttu-id="0cfd3-328">[ADAL을 사용하여 Android에서 앱 간 SSO를 사용하도록 설정하는 방법](active-directory-sso-android.md)을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0cfd3-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
