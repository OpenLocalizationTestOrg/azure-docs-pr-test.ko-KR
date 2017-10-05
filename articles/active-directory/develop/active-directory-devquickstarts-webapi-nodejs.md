---
title: "Azure AD Node.js 시작 | Microsoft Docs"
description: "인증을 위해 Azure AD와 통합되는 Node.js REST Web API를 빌드하는 방법."
services: active-directory
documentationcenter: nodejs
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 4f58177f540c14172d7ece8b4bc8c8a2b9787f8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-web-apis-for-nodejs"></a><span data-ttu-id="7f348-103">Node.js용 web API 시작</span><span class="sxs-lookup"><span data-stu-id="7f348-103">Get started with web APIs for Node.js</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7f348-104">*Passport* 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-104">*Passport* is authentication middleware for Node.js.</span></span> <span data-ttu-id="7f348-105">유연한 모듈식 Passport는 어떤 Express 기반 또는 Resitify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-105">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7f348-106">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-106">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="7f348-107">Microsoft는 Microsoft Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-107">We have developed a strategy for Microsoft Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7f348-108">여기서는 이 모듈을 설치하고 Microsoft Azure Active Directory `passport-azure-ad` 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-108">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="7f348-109">이렇게 하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-109">To do this, you need to:</span></span>

1. <span data-ttu-id="7f348-110">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-110">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="7f348-111">Passport의 `passport-azure-ad` 플러그 인을 사용하도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-111">Set up your app to use Passport's `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="7f348-112">To Do List web API를 호출하도록 클라이언트 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-112">Configure a client application to call the To Do List web API.</span></span>

<span data-ttu-id="7f348-113">이 자습서에 대한 코드는 [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi)에서 유지 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-113">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-node-webapi).</span></span>

> [!NOTE]
> <span data-ttu-id="7f348-114">이 문서에서는 Azure AD B2C를 사용하여 로그인, 등록 및 프로필 관리를 구현하는 방법을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-114">This article doesn't cover how to implement sign-in, sign-up, or profile management with Azure AD B2C.</span></span> <span data-ttu-id="7f348-115">사용자를 인증한 후에 Web API를 호출하는 데 집중합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-115">It focuses on calling web APIs after the user is already authenticated.</span></span>  <span data-ttu-id="7f348-116">[Azure Active Directory와 통합하는 방법 문서](active-directory-how-to-integrate.md)를 시작하여 Azure Active Directory의 기본 사항에 대해 알아보시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-116">We recommend that you start with [How to integrate with Azure Active Directory document](active-directory-how-to-integrate.md) to learn about the basics of Azure Active Directory.</span></span>
>
>

<span data-ttu-id="7f348-117">Microsoft는 이 실행 예제의 모든 소스 코드를 GitHub의 MIT 라이선스에 출시했으므로 자유롭게 복제(및 분기)하고 피드백을 제공하고 요청을 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-117">We've released all the source code for this running example in GitHub under an MIT license, so feel free to clone (or even better, fork), and provide feedback and pull requests.</span></span>

## <a name="about-nodejs-modules"></a><span data-ttu-id="7f348-118">Node.js 모듈 정보</span><span class="sxs-lookup"><span data-stu-id="7f348-118">About Node.js modules</span></span>
<span data-ttu-id="7f348-119">이 연습에서는 Node.js 모듈을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-119">We use Node.js modules in this walkthrough.</span></span> <span data-ttu-id="7f348-120">모듈은 응용 프로그램의 특정 기능을 제공하는 로드 가능한 JavaScript 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-120">Modules are loadable JavaScript packages that provide specific functionality for your application.</span></span> <span data-ttu-id="7f348-121">일반적으로 NPM 설치 디렉터리에서 Node.js NPM 명령줄 도구를 사용하여 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-121">You usually install modules by using the Node.js an NPM command-line tool in the NPM installation directory.</span></span> <span data-ttu-id="7f348-122">그러나 HTTP 모듈과 같은 일부 모듈은 코어 Node.js 패키지에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-122">However, some modules, such as the HTTP module, are included in the core Node.js package.</span></span>

<span data-ttu-id="7f348-123">설치된 모듈은 Node.js 설치 디렉터리의 루트에 있는 **node_modules** 디렉터리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-123">Installed modules are saved in the **node_modules** directory at the root of your Node.js installation directory.</span></span> <span data-ttu-id="7f348-124">**node_modules** 디렉터리의 각 모듈은 종속되는 모듈이 포함된 고유한 **node_modules** 디렉터리를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-124">Each module in the **node_modules** directory maintains its own **node_modules** directory that contains any modules that it depends on.</span></span> <span data-ttu-id="7f348-125">또한 각 필수 모듈에는 **node_modules** 디렉터리가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-125">Also, each required module has a **node_modules** directory.</span></span> <span data-ttu-id="7f348-126">이러한 반복되는 디렉터리 구조는 종속성 체인을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-126">This recursive directory structure represents the dependency chain.</span></span>

<span data-ttu-id="7f348-127">이와 같은 종속성 체인 구조로 인해 응용 프로그램 공간이 커집니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-127">This dependency chain structure results in a larger application footprint.</span></span> <span data-ttu-id="7f348-128">하지만 모든 종속성이 충족되고 개발에 사용되는 모듈 버전이 프로덕션에도 사용되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-128">But it also guarantees that all dependencies are met and that the version of the modules that's used in development is also used in production.</span></span> <span data-ttu-id="7f348-129">따라서 프로덕션 앱 동작을 예측하기 쉬워지고 사용자에게 영향을 줄 수 있는 버전 문제도 방지됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-129">This makes the production app behavior more predictable and prevents versioning problems that might affect users.</span></span>

## <a name="step-1-register-an-azure-ad-tenant"></a><span data-ttu-id="7f348-130">1단계: Azure AD 등록</span><span class="sxs-lookup"><span data-stu-id="7f348-130">Step 1: Register an Azure AD tenant</span></span>
<span data-ttu-id="7f348-131">이 샘플을 사용하려면 Azure Active Directory 테넌트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-131">To use this sample, you need an Azure Active Directory tenant.</span></span> <span data-ttu-id="7f348-132">테넌트가 무엇인지 또는 어떻게 가져오는지 잘 모를 경우 [Azure AD 테넌트를 가져오는 방법](active-directory-howto-tenant.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7f348-132">If you're not sure what a tenant is or how to get one, see [How to get an Azure AD tenant](active-directory-howto-tenant.md).</span></span>

## <a name="step-2-create-an-application"></a><span data-ttu-id="7f348-133">2단계: 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="7f348-133">Step 2: Create an application</span></span>
<span data-ttu-id="7f348-134">다음으로 Azure AD가 앱과 안전하게 통신해야 한다는 정보를 제공하는 앱을 디렉터리에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-134">Next you create an app in your directory that gives Azure AD information that it needs to securely communicate with your app.</span></span>  <span data-ttu-id="7f348-135">이 경우 클라이언트 앱과 web API가 하나의 논리 앱을 구성하기 때문에 둘 다 단일 **응용 프로그램 ID**로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-135">Both the client app and web API are represented by a single **Application ID** in this case, because they comprise one logical app.</span></span>  <span data-ttu-id="7f348-136">앱을 만들려면 [다음 지침](active-directory-how-applications-are-added.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-136">To create an app, follow [these instructions](active-directory-how-applications-are-added.md).</span></span> <span data-ttu-id="7f348-137">기간 업무 앱을 빌드하는 경우 [이 추가 지침이 유용할 수 있습니다](../active-directory-applications-guiding-developers-for-lob-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7f348-137">If you are building a line-of-business app, [these additional instructions might be useful](../active-directory-applications-guiding-developers-for-lob-applications.md).</span></span>

<span data-ttu-id="7f348-138">응용 프로그램을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="7f348-138">To create an application:</span></span>

1. <span data-ttu-id="7f348-139">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-139">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7f348-140">상단 메뉴에서 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-140">On the top menu, select your account.</span></span> <span data-ttu-id="7f348-141">그런 다음 **디렉터리** 목록에서 응용 프로그램을 등록할 Active Directory 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-141">Then, under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="7f348-142">왼쪽 메뉴에서 **추가 서비스**를 선택한 후 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-142">In the menu on the left, select **More Services**, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="7f348-143">**앱 등록**을 선택하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-143">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="7f348-144">프롬프트에 따라 새 **웹 응용 프로그램 및/또는 WebAPI**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-144">Follow the prompts to create a **Web Application and/or WebAPI**.</span></span>

      * <span data-ttu-id="7f348-145">응용 프로그램의 **이름**은 최종 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-145">The **name** of the application describes your application to end users.</span></span>

      * <span data-ttu-id="7f348-146">**로그온 URL** 은 앱의 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-146">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="7f348-147">샘플 코드의 기본 URL은 `https://localhost:8080`입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-147">The default URL of the sample code is `https://localhost:8080`.</span></span>

6. <span data-ttu-id="7f348-148">등록 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-148">After you register, Azure AD assigns your app a unique Application ID.</span></span> <span data-ttu-id="7f348-149">이 값은 다음 섹션에서 필요하므로 응용 프로그램 페이지에서 이 값을 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-149">You need this value in the next sections, so copy it from the application page.</span></span>

7. <span data-ttu-id="7f348-150">응용 프로그램에 대한 **설정** -> **속성** 페이지에서 앱 ID URI를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-150">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="7f348-151">**앱 ID URI** 는 응용 프로그램의 고유 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-151">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="7f348-152">규칙은 `https://<tenant-domain>/<app-name>`(예: `https://contoso.onmicrosoft.com/my-first-aad-app`)을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-152">The convention is to use `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="7f348-153">**설정** 페이지에서 응용 프로그램의 **키**를 만들고 편한 위치에 복사해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-153">Create a **Key** for your application from the **Settings** page, and then copy it somewhere.</span></span> <span data-ttu-id="7f348-154">곧 이 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-154">You'll need it shortly.</span></span>

## <a name="step-3-download-nodejs-for-your-platform"></a><span data-ttu-id="7f348-155">3단계: 사용자 플랫폼을 위한 Node.js 다운로드</span><span class="sxs-lookup"><span data-stu-id="7f348-155">Step 3: Download Node.js for your platform</span></span>
<span data-ttu-id="7f348-156">이 샘플을 사용하려면 작동하는 Node.js 설치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-156">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="7f348-157">[http://nodejs.org](http://nodejs.org)에서 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-157">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="step-4-install-mongodb-on-your-platform"></a><span data-ttu-id="7f348-158">4단계: 플랫폼에 MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="7f348-158">Step 4: Install MongoDB on your platform</span></span>
<span data-ttu-id="7f348-159">이 샘플을 사용하려면 작동하는 MongoDB 설치가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-159">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="7f348-160">MongoDB를 사용하여 REST API가 서버 인스턴스에서 지속되도록 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-160">You use MongoDB to make the REST API persistent across server instances.</span></span>

<span data-ttu-id="7f348-161">[http://mongodb.org](http://www.mongodb.org)에서 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-161">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="7f348-162">이 연습에서는 MongoDB의 기본 설치 및 mongodb://localhost 서버 끝점(현재 문성 작성 시점 기준)을 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-162">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is mongodb://localhost.</span></span>
>
>

## <a name="step-5-install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="7f348-163">5단계: web API에 Restify 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="7f348-163">Step 5: Install the Restify modules in your web API</span></span>
<span data-ttu-id="7f348-164">Resitfy를 사용하여 REST API를 작성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-164">We are using Restify to build our REST API.</span></span> <span data-ttu-id="7f348-165">Restify는 Express에서 파생된 작고 유연한 Node.js 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-165">Restify is a minimal and flexible Node.js application framework that's derived from Express.</span></span> <span data-ttu-id="7f348-166">Connect 위에 REST API를 구축하기 위한 강력한 기능 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-166">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="7f348-167">Restify 설치</span><span class="sxs-lookup"><span data-stu-id="7f348-167">Install Restify</span></span>
1. <span data-ttu-id="7f348-168">명령줄에서 디렉터리를 **azuread** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-168">From the command line, change directories to the **azuread** directory.</span></span> <span data-ttu-id="7f348-169">**azuread** 디렉터리가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-169">If the **azuread** directory does not exist, create it.</span></span>

        `cd azuread - or- mkdir azuread; cd azuread`

2. <span data-ttu-id="7f348-170">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-170">Type the following command:</span></span>

    `npm install restify`

    <span data-ttu-id="7f348-171">이 명령은 Restify를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="7f348-172">오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="7f348-172">Did you get an error?</span></span>
<span data-ttu-id="7f348-173">일부 운영 체제에서 NPM 매개 변수를 사용하면 **오류: EPERM, chmod '/usr/local/bin/..'** 오류 메시지와</span><span class="sxs-lookup"><span data-stu-id="7f348-173">When you use NPM on some operating systems, you might receive an error that says **Error: EPERM, chmod '/usr/local/bin/..'**</span></span> <span data-ttu-id="7f348-174">관리자 계정으로 실행하라는 제안이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-174">and a suggestion that you try running the account as an administrator.</span></span> <span data-ttu-id="7f348-175">이런 경우 sudo 명령을 사용하여 더 높은 권한 수준으로 NPM을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="7f348-175">If this occurs, use the sudo command to run NPM at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="7f348-176">DTRACE 관련 오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="7f348-176">Did you get an error regarding DTRACE?</span></span>
<span data-ttu-id="7f348-177">Restify를 설치할 때 다음과 같은 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-177">You might see an error like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```
<span data-ttu-id="7f348-178">Restify는 DTrace를 사용하여 REST 호출을 추적하는 강력한 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-178">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="7f348-179">그러나 DTrace가 없는 운영 체제가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-179">However, many operating systems do not have DTrace.</span></span> <span data-ttu-id="7f348-180">이러한 오류는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-180">You can safely ignore these errors.</span></span>

<span data-ttu-id="7f348-181">이 명령의 출력은 다음 출력과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-181">The output of this command should look similar to the following output:</span></span>

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0 (mv@0.0.5)


## <a name="step-6-install-passportjs-in-your-web-api"></a><span data-ttu-id="7f348-182">6단계: web API에 Passport.js 설치</span><span class="sxs-lookup"><span data-stu-id="7f348-182">Step 6: Install Passport.js in your web API</span></span>
<span data-ttu-id="7f348-183">[Passport](http://passportjs.org/) 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-183">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="7f348-184">유연한 모듈식 Passport는 어떤 Express 기반 또는 Resitify 웹 응용 프로그램에도 원활하게 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-184">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Restify web application.</span></span> <span data-ttu-id="7f348-185">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-185">A comprehensive set of strategies support authentication with a username and password, Facebook, Twitter, and more.</span></span>

<span data-ttu-id="7f348-186">Microsoft는 Azure Active Directory에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-186">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="7f348-187">여기서는 이 모듈을 설치하고 Azure Active Directory 전략 플러그 인을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-187">We install this module and then add the Azure Active Directory strategy plug-in.</span></span>

1. <span data-ttu-id="7f348-188">명령줄에서 디렉터리를 **azuread** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-188">From the command line, change directories to the **azuread** directory.</span></span>

2. <span data-ttu-id="7f348-189">passport.js를 설치하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-189">To install passport.js, enter the following command :</span></span>

    `npm install passport`

    <span data-ttu-id="7f348-190">이 명령의 출력은 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-190">The output of the command should look similar to the following:</span></span>

``
        passport@0.1.17 node_modules\passport
        ├── pause@0.0.1
        └── pkginfo@0.2.3
``

## <a name="step-7-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="7f348-191">7단계: web API에 Passport-Azure-AD 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-191">Step 7: Add Passport-Azure-AD to your web API</span></span>
<span data-ttu-id="7f348-192">다음으로 Azure Active Directory를 Passport에 연결하는 전략 제품군인 `passport-azure-ad`를 사용하여 OAuth 전략을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-192">Next we add the OAuth strategy by using `passport-azure-ad`, a suite of strategies that connect Azure Active Directory to Passport.</span></span> <span data-ttu-id="7f348-193">이 REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-193">We use this strategy for bearer tokens in this REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="7f348-194">OAuth2는 알려진 모든 토큰 유형을 발급할 수 있는 프레임워크를 제공하지만 일반적으로 특정 토큰 유형만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-194">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types are commonly used.</span></span> <span data-ttu-id="7f348-195">전달자 토큰은 끝점 보호에 가장 일반적으로 사용되는 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-195">Bearer tokens are the most commonly used tokens for protecting endpoints.</span></span> <span data-ttu-id="7f348-196">전달자 토큰은 OAuth2에서 가장 널리 발급되는 토큰 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-196">They are the most widely issued type of token in OAuth2.</span></span> <span data-ttu-id="7f348-197">많은 구현에서 발급되는 유일한 토큰 유형이 전달자 토큰이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-197">Many implementations assume that bearer tokens are the only type of tokens that are issued.</span></span>
>
>

<span data-ttu-id="7f348-198">명령줄에서 디렉터리를 **azuread** 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-198">From the command line, change directories to the **azuread** directory.</span></span>

<span data-ttu-id="7f348-199">다음 명령을 입력하여 Passport.js `passport-azure-ad module`을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-199">Type the following command to install the Passport.js `passport-azure-ad module`:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="7f348-200">이 명령의 출력은 다음 출력과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-200">The output of the command should look similar to the following output:</span></span>


    passport-azure-ad@1.0.0 node_modules/passport-azure-ad
    ├── xtend@4.0.0
    ├── xmldom@0.1.19
    ├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
    ├── underscore@1.8.3
    ├── async@1.3.0
    ├── jsonwebtoken@5.0.2
    ├── xml-crypto@0.5.27 (xpath.js@1.0.6)
    ├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
    ├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
    ├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
    └── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)



## <a name="step-8-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="7f348-201">8단계: web API에 MongoDB 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-201">Step 8: Add MongoDB modules to your web API</span></span>
<span data-ttu-id="7f348-202">데이터 저장소로 MongoDB를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-202">We use MongoDB as our datastore.</span></span> <span data-ttu-id="7f348-203">따라서 모델 및 스키마를 관리에 널리 사용되는 Mongoose라고 하는 플러그 인을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-203">For that reason, we need to install the widely used plug-in called Mongoose to manage models and schemas.</span></span> <span data-ttu-id="7f348-204">MongoDB용 데이터베이스 드라이버(MongoDB)도 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-204">We also need to install the database driver for MongoDB (which is also called MongoDB).</span></span>

 `npm install mongoose`

## <a name="step-9-install-additional-modules"></a><span data-ttu-id="7f348-205">9단계: 추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="7f348-205">Step 9: Install additional modules</span></span>
<span data-ttu-id="7f348-206">다음으로 나머지 필수 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-206">Next we install the remaining required modules.</span></span>

1. <span data-ttu-id="7f348-207">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-207">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-208">다음 명령을 입력하여 **node_modules** 디렉터리에 다음 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-208">Enter the following commands to install these modules in your **node_modules** directory:</span></span>

    * `npm install assert-plus`
    * `npm install bunyan`
    * `npm update`

## <a name="step-10-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="7f348-209">10단계: 종속성을 적용하여 server.js 만들기</span><span class="sxs-lookup"><span data-stu-id="7f348-209">Step 10: Create a server.js with your dependencies</span></span>
<span data-ttu-id="7f348-210">server.js 파일은 web API 서버에 대한 대부분의 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-210">The server.js file provides most of the functionality for our web API server.</span></span> <span data-ttu-id="7f348-211">이 파일에 대부분의 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-211">We add most of our code to this file.</span></span> <span data-ttu-id="7f348-212">프로덕션을 위해, 기능을 별도의 경로 및 컨트롤러와 같은 좀 더 작은 파일로 리팩터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-212">For production purposes, we recommend that you refactor the functionality into smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="7f348-213">이 데모에서는 이 기능에 server.js를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-213">In this demo, we use server.js for this functionality.</span></span>

1. <span data-ttu-id="7f348-214">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-214">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-215">즐겨 사용하는 편집기에서 `server.js` 파일을 만들고 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-215">Create a `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
        'use strict';

        /**
         * Module dependencies.
         */

        var fs = require('fs');
        var path = require('path');
        var util = require('util');
        var assert = require('assert-plus');
        var bunyan = require('bunyan');
        var getopt = require('posix-getopt');
        var mongoose = require('mongoose/');
        var restify = require('restify');
        var passport = require('passport');
      var BearerStrategy = require('passport-azure-ad').BearerStrategy;
    ```

3. <span data-ttu-id="7f348-216">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-216">Save the file.</span></span> <span data-ttu-id="7f348-217">잠시 후에 이 파일로 다시 돌아갈 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-217">We'll return to it shortly.</span></span>

## <a name="step-11-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="7f348-218">11단계: Azure AD 설정을 저장하기 위한 구성 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="7f348-218">Step 11: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="7f348-219">이 코드 파일은 Azure Active Directory 포털의 구성 매개 변수를 Passport.js에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-219">This code file passes the configuration parameters from your Azure Active Directory portal to Passport.js.</span></span> <span data-ttu-id="7f348-220">이 연습의 첫 번째 부분에서 포털에 web API를 추가할 때 이러한 구성 값을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-220">You created these configuration values when you added the web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="7f348-221">코드를 복사한 후에 이러한 매개 변수 값에 추가할 항목에 대해 설명할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-221">We explain what to put in the values of these parameters after you copy the code.</span></span>

1. <span data-ttu-id="7f348-222">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-222">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-223">즐겨 사용하는 편집기에서 `config.js` 파일을 만들고 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-223">Create a `config.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
         exports.creds = {
             mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
             clientID: 'your client ID',
             audience: 'your application URL',
            // you cannot have users from multiple tenants sign in to your server unless you use the common endpoint
          // example: https://login.microsoftonline.com/common/.well-known/openid-configuration
             identityMetadata: 'https://login.microsoftonline.com/<your tenant id>/.well-known/openid-configuration',
             validateIssuer: true, // if you have validation on, you cannot have users from multiple tenants sign in to your server
             passReqToCallback: false,
             loggingLevel: 'info' // valid are 'info', 'warn', 'error'. Error always goes to stderr in Unix.

         };
    ```
3. <span data-ttu-id="7f348-224">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-224">Save the file.</span></span>

## <a name="step-12-add-configuration-values-to-your-serverjs-file"></a><span data-ttu-id="7f348-225">12단계: server.js 파일에 구성 값 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-225">Step 12: Add configuration values to your server.js file</span></span>
<span data-ttu-id="7f348-226">응용 프로그램에서 방금 만든 .config 파일로부터 이러한 값을 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-226">We need to read these values from the .config file that you created across our application.</span></span> <span data-ttu-id="7f348-227">이 작업을 수행하기 위해 응용 프로그램에서 .config 파일을 필수 리소스로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-227">To do this, we add the .config file as a required resource in our application.</span></span> <span data-ttu-id="7f348-228">그런 다음 config.js 문서의 변수와 일치하도록 전역 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-228">Then we set the global variables to match the variables in the config.js document.</span></span>

1. <span data-ttu-id="7f348-229">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-229">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-230">즐겨 사용하는 편집기에서 `server.js` 파일을 열고 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-230">Open your `server.js` file in your favorite editor, and then add the following information:</span></span>

    ```Javascript
    var config = require('./config');
    ```
3. <span data-ttu-id="7f348-231">그 후 다음 코드를 사용하여 `server.js`에 새 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-231">Then add a new section to `server.js` with the following code:</span></span>

    ```Javascript
    var options = {
        // The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
        identityMetadata: config.creds.identityMetadata,
        clientID: config.creds.clientID,
        validateIssuer: config.creds.validateIssuer,
        audience: config.creds.audience,
        passReqToCallback: config.creds.passReqToCallback,
        loggingLevel: config.creds.loggingLevel

    };

    // Array to hold logged in users and the current logged in user (owner).
    var users = [];
    var owner = null;

    // Our logger.
    var log = bunyan.createLogger({
        name: 'Azure Active Directory Bearer Sample',
             streams: [
            {
                stream: process.stderr,
                level: "error",
                name: "error"
            },
            {
                stream: process.stdout,
                level: "warn",
                name: "console"
            }, ]
    });

      // If the logging level is specified, switch to it.
      if (config.creds.loggingLevel) { log.levels("console", config.creds.loggingLevel); }

    // MongoDB setup.
    // Set up some configuration.
    var serverPort = process.env.PORT || 8080;
    var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
    ```

4. <span data-ttu-id="7f348-232">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-232">Save the file.</span></span>

## <a name="step-13-add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="7f348-233">13단계: Moongoose를 사용하여 MongoDB 모델 및 스키마 정보 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-233">Step 13: Add The MongoDB Model and schema information by using Mongoose</span></span>
<span data-ttu-id="7f348-234">이제 이러한 세 파일을 하나의 REST API 서비스에 통합하면 모든 준비 과정이 마무리됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-234">Now all this preparation is going to start paying off as we combine these three files into a REST API service.</span></span>

<span data-ttu-id="7f348-235">이 연습에서는 4단계에서 설명한 대로 MongoDB를 사용하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-235">For this walkthrough, we use MongoDB to store our tasks as discussed in Step 4.</span></span>

<span data-ttu-id="7f348-236">11단계에서 만든 `config.js` 파일에서는 `tasklist` 데이터베이스를 호출했습니다. **mogoose_auth_local** 연결 URL의 마지막에 추가한 데이터베이스이기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-236">In the `config.js` file that we created in Step 11, we called our database `tasklist`, because that was what we put at the end of our **mogoose_auth_local** connection URL.</span></span> <span data-ttu-id="7f348-237">MongoDB에서 이 데이터베이스를 미리 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-237">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="7f348-238">그 대신 서버 응용 프로그램이 처음으로 실행될 때 MongoDB가 이 데이터베이스를 자동으로 만듭니다(아직 데이터베이스가 없다고 가정).</span><span class="sxs-lookup"><span data-stu-id="7f348-238">Instead, MongoDB creates this for us on the first run of our server application (assuming that the database doesn't already exist).</span></span>

<span data-ttu-id="7f348-239">사용하려는 MongoDB 데이터베이스를 서버에 알렸으므로 일부 추가 코드를 작성하여 서버 작업에 대한 모델 및 스키마를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-239">Now that we've told the server which MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's tasks.</span></span>

### <a name="discussion-of-the-model"></a><span data-ttu-id="7f348-240">모델에 대한 논의</span><span class="sxs-lookup"><span data-stu-id="7f348-240">Discussion of the model</span></span>
<span data-ttu-id="7f348-241">Microsoft의 스키마 모델은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-241">Our schema model is simple.</span></span> <span data-ttu-id="7f348-242">필요에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-242">You expand it as required.</span></span>

<span data-ttu-id="7f348-243">NAME: 작업에 할당된 사람의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-243">NAME: The name of the person who is assigned to the task.</span></span> <span data-ttu-id="7f348-244">**문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-244">A **String**.</span></span>

<span data-ttu-id="7f348-245">TASK: 작업 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-245">TASK: The task itself.</span></span> <span data-ttu-id="7f348-246">**문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-246">A **String**.</span></span>

<span data-ttu-id="7f348-247">DATE: 작업이 만료되는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-247">DATE: The date that the task is due.</span></span> <span data-ttu-id="7f348-248">**DATETIME**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-248">A **DATETIME**.</span></span>

<span data-ttu-id="7f348-249">COMPLETED: 작업의 완료 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-249">COMPLETED: If the task has been completed or not.</span></span> <span data-ttu-id="7f348-250">**부울**입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-250">A **BOOLEAN**.</span></span>

### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="7f348-251">코드에 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="7f348-251">Creating the schema in the code</span></span>
1. <span data-ttu-id="7f348-252">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-252">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-253">즐겨 사용하는 편집기에서 `server.js` 파일을 열고 구성 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-253">Open your `server.js` file in your favorite editor, and then add the following information below the configuration entry:</span></span>

    ```Javascript
    // Connect to MongoDB.
    global.db = mongoose.connect(serverURI);
    var Schema = mongoose.Schema;
    log.info('MongoDB Schema loaded');

    // Here we create a schema to store our tasks and users. It's a fairly simple schema for now.
    var TaskSchema = new Schema({
        owner: String,
        task: String,
        completed: Boolean,
        date: Date
    });

    // Use the schema to register a model.
    mongoose.model('Task', TaskSchema);
    var Task = mongoose.model('Task');
    ```
<span data-ttu-id="7f348-254">코드를 보면 알 수 있듯이, 먼저 스키마를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-254">As you can tell from the code, we create our schema first.</span></span> <span data-ttu-id="7f348-255">그런 다음 **경로**를 정의할 때 코드 전체에서 데이터를 저장하는 데 사용할 모델 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-255">Then we create a model object that we use to store our data throughout the code when we define our **Routes**.</span></span>

## <a name="step-14-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="7f348-256">14단계: Task REST API 서버에 대한 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-256">Step 14: Add our routes for our task REST API server</span></span>
<span data-ttu-id="7f348-257">작업할 데이터베이스 모델이 준비되었으므로 REST API 서버에 사용할 경로를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-257">Now that we have a database model to work with, let's add the routes we are going use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="7f348-258">Restify의 경로 정보</span><span class="sxs-lookup"><span data-stu-id="7f348-258">About routes in Restify</span></span>
<span data-ttu-id="7f348-259">경로는 Express 스택을 사용할 때와 동일한 방식으로 Restify에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-259">Routes work in Restify the same way they do in the Express stack.</span></span> <span data-ttu-id="7f348-260">클라이언트 응용 프로그램이 호출할 것으로 예상하는 URI를 사용하여 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-260">You define routes by using the URI that you expect the client applications to call.</span></span> <span data-ttu-id="7f348-261">일반적으로 경로는 별도 파일에 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-261">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="7f348-262">여기서는 경로를 server.js 파일에 저장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-262">For our purposes, we put our routes in the server.js file.</span></span> <span data-ttu-id="7f348-263">프로덕션 사용을 위해서는 자체 파일에서 이러한 경로를 팩터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-263">We recommend that you factor these routes into their own file for production use.</span></span>

<span data-ttu-id="7f348-264">Restify 경로의 일반적인 패턴은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-264">A typical pattern for a Restify route is as follows:</span></span>

```Javascript
function createObject(req, res, next) {

// Do work on object.

 _object.name = req.params.object; // passed value is in req.params under object

 ///...

return next(); // Keep the server going.
}

....

server.post('/service/:add/:object', createObject); // Calls createObject on routes that match this.

```


<span data-ttu-id="7f348-265">가장 기본적인 수준의 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-265">This is the pattern at its most basic level.</span></span> <span data-ttu-id="7f348-266">Resitfy(및 Express)는 응용 프로그램 유형을 정의하고, 여러 끝점에 복잡한 라우팅을 제공하는 등 훨씬 수준 높은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-266">Restify (and Express) provide much deeper functionality, such as defining application types and providing complex routing across different endpoints.</span></span> <span data-ttu-id="7f348-267">여기서는 이러한 경로를 간단하게 유지하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-267">For our purposes, we are keeping these routes simple.</span></span>

### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="7f348-268">서버에 기본 경로 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-268">Add default routes to our server</span></span>
<span data-ttu-id="7f348-269">이제 만들기, 검색, 업데이트 및 삭제의 기본 CRUD 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-269">We now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

1. <span data-ttu-id="7f348-270">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-270">From the command line, change directories to the **azuread** folder if you're not already there:</span></span>

    `cd azuread`

2. <span data-ttu-id="7f348-271">즐겨 사용하는 편집기에서 `server.js` 파일을 열고 앞에서 만든 데이터베이스 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-271">Open the `server.js` file in your favorite editor, and then add the following information below the previous database entries that you made:</span></span>

```Javascript

/**
 *
 * APIs for our REST Task server.
 */

// Create a task.

function createTask(req, res, next) {

    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it, and save it to Mongodb.
    var _task = new Task();

    if (!req.params.task) {
        req.log.warn('createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.task = req.params.task;
    _task.date = new Date();

    _task.save(function(err) {
        if (err) {
            req.log.warn(err, 'createTask: unable to save');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}


// Delete a task by name.

function removeTask(req, res, next) {

    Task.remove({
        task: req.params.task,
        owner: owner
    }, function(err) {
        if (err) {
            req.log.warn(err,
                'removeTask: unable to delete %s',
                req.params.task);
            next(err);
        } else {
            log.info('Deleted task:', req.params.task);
            res.send(204);
            next();
        }
    });
}

// Delete all tasks.

function removeAll(req, res, next) {
    Task.remove();
    res.send(204);
    return next();
}


// Get a specific task based on name.

function getTask(req, res, next) {

    log.info('getTask was called for: ', owner);
    Task.find({
        owner: owner
    }, function(err, data) {
        if (err) {
            req.log.warn(err, 'get: unable to read %s', owner);
            next(err);
            return;
        }

        res.json(data);
    });

    return next();
}

/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Restify currently has a bug which doesn't allow you to set default headers.
    // These headers comply with CORS and allow us to mongodbServer our response to any origin.

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err) {
            return next(err);
        }

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in the database. Did you initialize the database as stated in the README?");
        }

        if (!owner) {
            log.warn(err, "You did not pass an owner when listing tasks.");
        } else {

            res.json(data);

        }
    });

    return next();
}

```

### <a name="add-error-handling-in-our-apis"></a><span data-ttu-id="7f348-272">API에서 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-272">Add error handling in our APIs</span></span>
```

///--- Errors for communicating something interesting back to the client.

function MissingTaskError() {
    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'MissingTask',
        message: '"task" is a required parameter',
        constructorOpt: MissingTaskError
    });

    this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);


function TaskExistsError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 409,
        restCode: 'TaskExists',
        message: owner + ' already exists',
        constructorOpt: TaskExistsError
    });

    this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);


function TaskNotFoundError(owner) {
    assert.string(owner, 'owner');

    restify.RestError.call(this, {
        statusCode: 404,
        restCode: 'TaskNotFound',
        message: owner + ' was not found',
        constructorOpt: TaskNotFoundError
    });

    this.name = 'TaskNotFoundError';
}

util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="step-15-create-your-server"></a><span data-ttu-id="7f348-273">15단계: 서버 만들기</span><span class="sxs-lookup"><span data-stu-id="7f348-273">Step 15: Create your server</span></span>
<span data-ttu-id="7f348-274">데이터베이스를 정의했으며 경로가 정위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-274">We have defined our database and our routes are in place.</span></span> <span data-ttu-id="7f348-275">마지막으로 할 일은 호출을 관리할 서버 인스턴스를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-275">The last thing to do is add the server instance that manages our calls.</span></span>

<span data-ttu-id="7f348-276">Restify(및 Express)에서 REST API 서버에 대해 여러 사용자 지정 작업을 수행할 수 있지만 여기서는 가장 기본적인 설정만 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-276">In Restify (and Express) you can do a lot of customization for a REST API server, but again we are going to use the most basic setup for our purposes.</span></span>

```Javascript
/**
 * Our server.
 */


var server = restify.createServer({
    name: "Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads.
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//.
server.pre(restify.pre.sanitizePath());

// Handle annoying user agents (curl).
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in).
server.use(restify.requestLogger());

// Allow five requests per second by IP, and burst to 10.
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want.
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allow for JSON mapping to REST.
```

## <a name="step-16-add-the-routes-to-the-server-without-authentication-for-now"></a><span data-ttu-id="7f348-277">16단계: 서버에 경로 추가(지금은 인증 없이)</span><span class="sxs-lookup"><span data-stu-id="7f348-277">Step 16: Add the routes to the server (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD.
/**
/*
/* Each of these handlers is protected by our OIDCBearerStrategy by invoking 'oidc-bearer'.
/* In the pasport.authenticate() method. We set 'session: false' because REST is stateless and
/* we don't need to maintain session state. You can experiment with removing API protection
/* by removing the passport.authenticate() method as follows:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler.
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```

## <a name="step-17-run-the-server-before-adding-oauth-support"></a><span data-ttu-id="7f348-278">17단계: 서버 실행(OAuth 지원을 추가하기 전에)</span><span class="sxs-lookup"><span data-stu-id="7f348-278">Step 17: Run the server (before adding OAuth support)</span></span>
<span data-ttu-id="7f348-279">인증을 추가하기 전에 서버를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-279">Test out your server before we add authentication.</span></span>

<span data-ttu-id="7f348-280">서버를 테스트하는 가장 쉬운 방법은 명령줄에서 curl을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-280">The easiest way to test your server is by using curl in a command line.</span></span> <span data-ttu-id="7f348-281">이 작업을 수행하기 전에 JSON처럼 출력을 구문 분석할 수 있는 유틸리티가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-281">Before we do that, we need a utility that allows us to parse output as JSON.</span></span>

1. <span data-ttu-id="7f348-282">다음 JSON 도구를 설치합니다(이제부터 나오는 모든 예제에서 이 도구가 사용됨).</span><span class="sxs-lookup"><span data-stu-id="7f348-282">Install the following JSON tool (all the following examples use this tool):</span></span>

    `$npm install -g jsontool`

    <span data-ttu-id="7f348-283">이렇게 하면 JSON 도구가 전역적으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-283">This installs the JSON tool globally.</span></span> <span data-ttu-id="7f348-284">작업이 완료되었으니 서버 작업을 진행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-284">Now that we’ve accomplished that, let’s play with the server:</span></span>

2. <span data-ttu-id="7f348-285">먼저 mongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-285">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

3. <span data-ttu-id="7f348-286">그런 다음 해당 디렉터리로 변경하고 curl을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-286">Then, change to the directory and start curling:</span></span>

    <span data-ttu-id="7f348-287">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7f348-287">`$ cd azuread` `$ node server.js`</span></span>

    `$ curl -isS http://127.0.0.1:8080 | json`

    ```Shell
    HTTP/1.1 200 OK
    Connection: close
    Content-Type: application/json
    Content-Length: 171
    Date: Tue, 14 Jul 2015 05:43:38 GMT
    [
    "GET /",
    "POST /tasks/:owner/:task",
    "POST /tasks (for JSON body)",
    "GET /tasks",
    "PUT /tasks/:owner",
    "GET /tasks/:owner",
    "DELETE /tasks/:owner/:task"
    ]
    ```

4. <span data-ttu-id="7f348-288">그런 다음 다음과 같은 방식으로 작업을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-288">Then, we can add a task this way:</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    <span data-ttu-id="7f348-289">응답은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-289">The response should be:</span></span>

        ```Shell
        HTTP/1.1 201 Created
        Connection: close
        Access-Control-Allow-Origin: *
        Access-Control-Allow-Headers: X-Requested-With
        Content-Type: application/x-www-form-urlencoded
        Content-Length: 5
        Date: Tue, 04 Feb 2014 01:02:26 GMT
        Hello
        ```
    <span data-ttu-id="7f348-290">또한 다음 방식으로 Brandon에 대한 작업을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-290">And we can list tasks for Brandon this way:</span></span>

        `$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="7f348-291">이 모든 작업이 끝나면 REST API 서버에 OAuth를 추가할 준비가 완료된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-291">If all this works, we're ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="7f348-292">MongoDB를 사용하는 REST API 서버가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-292">You have a REST API server with MongoDB!</span></span>

## <a name="step-18-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="7f348-293">18단계: REST API 서버에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="7f348-293">Step 18: Add authentication to our REST API server</span></span>
<span data-ttu-id="7f348-294">이제 REST API가 실행되고 있으니 Azure AD를 사용하여 더욱 유용하게 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-294">Now that we have a running REST API, let's start making it useful with Azure AD.</span></span>

<span data-ttu-id="7f348-295">아직 디렉터리를 변경하지 않았으면 명령줄에서 디렉터리를 **azuread** 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-295">From the command line, change directories to the **azuread** folder if you're not already there.</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="7f348-296">passport-azure-ad에 포함된 OIDCBearerStrategy 사용</span><span class="sxs-lookup"><span data-stu-id="7f348-296">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="7f348-297">지금까지 권한 부여 없이 일반적인 REST TODO 서버를 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-297">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="7f348-298">이 지점에서 통합 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-298">This is where we start putting that together.</span></span>

1. <span data-ttu-id="7f348-299">먼저, Passport를 사용하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-299">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="7f348-300">다른 서버 구성 바로 뒤에 이 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-300">Put this right after your other server configuration:</span></span>

    ```Javascript
            // Let's start using Passport.js.

            server.use(passport.initialize()); // Starts passport.
            server.use(passport.session()); // Provides session support.
    ```
    > [!TIP]
    > <span data-ttu-id="7f348-301">API를 작성할 때 항상 사용자가 스푸핑할 수 없는 토큰의 고유한 항목에 데이터를 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-301">When you write APIs, we recommend that you always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="7f348-302">이 서버는 TODO 항목을 저장할 때 "owner" 필드에 넣은 토큰(token.oid를 통해 호출됨)의 사용자 개체 ID를 기준으로 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-302">When this server stores TODO items, it stores them based on the object ID of the user in the token (called through token.oid), which we put in the “owner” field.</span></span> <span data-ttu-id="7f348-303">이렇게 하면 해당 사용자만 자신의 TODO 항목에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-303">This ensures that only that user can access their TODOs.</span></span> <span data-ttu-id="7f348-304">API에 "owner"가 노출되지 않으므로 외부 사용자가 인증된 경우에도 다른 사용자의 TODO 항목을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-304">There is no exposure in the API of “owner,” so an external user can request the TODOs of others even if they are authenticated.</span></span>                    

2. <span data-ttu-id="7f348-305">다음으로 `passport-azure-ad`와 함께 제공되는 전달자 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-305">Next let’s use the bearer strategy that comes with `passport-azure-ad`.</span></span> <span data-ttu-id="7f348-306">지금은 코드만 살펴보고 나머지는 잠시 후에 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-306">Look at the code for now and we'll explain the rest shortly.</span></span> <span data-ttu-id="7f348-307">위에서 붙여넣은 코드 뒤에 이 코드를 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-307">Put this after what you pasted above:</span></span>

```Javascript
    /**
    /*
    /* Calling the OIDCBearerStrategy and managing users.
    /*
    /* Passport pattern provides the need to manage users and info tokens
    /* with a FindorCreate() method that must be provided by the implementor.
    /* Here we just auto-register any user and implement a FindById().
    /* You'll want to do something smarter.
    **/

    var findById = function(id, fn) {
        for (var i = 0, len = users.length; i < len; i++) {
            var user = users[i];
            if (user.sub === id) {
                log.info('Found user: ', user);
                return fn(null, user);
            }
        }
        return fn(null, null);
    };


    var bearerStrategy = new BearerStrategy(options,
        function(token, done) {
            log.info('verifying the user');
            log.info(token, 'was the token retreived');
            findById(token.sub, function(err, user) {
                if (err) {
                    return done(err);
                }
                if (!user) {
                    // "Auto-registration"
                    log.info('User was added automatically as they were new. Their sub is: ', token.sub);
                    users.push(token);
                    owner = token.sub;
                    return done(null, token);
                }
                owner = token.sub;
                return done(null, user, token);
            });
        }
    );

    passport.use(bearerStrategy);
```

<span data-ttu-id="7f348-308">Passport는 모든 전략 작성자가 준수하는 유사한 패턴을 모든 전략(Twitter, Facebook 등)에 대해 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-308">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="7f348-309">전략을 보면 토큰 및 완료가 매개 변수로 포함된 함수가 전달되는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-309">Looking at the strategy, you see we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="7f348-310">전략은 작업을 완료한 후에 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-310">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="7f348-311">전략이 돌아오면 토큰을 다시 요청할 필요가 없도록 사용자를 저장하고 토큰을 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-311">After it does, we store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f348-312">이전 코드는 서버에 인증하는 모든 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-312">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="7f348-313">이를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-313">This is known as auto-registration.</span></span> <span data-ttu-id="7f348-314">프로덕션 서버에서는 사용자가 결정한 등록 프로세스를 통과하지 않은 사람에게는 액세스를 허용하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-314">In production servers, you we recommend that you don't let anyone in without first having them go through a registration process that you decide on.</span></span> <span data-ttu-id="7f348-315">이것은 Facebook에 등록할 수 있도록 허용하지만 추가 정보를 입력하도록 요구하는 소비자 앱에서 주로 나타나는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-315">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="7f348-316">명령줄 프로그램이 아니라면 반환된 토큰 개체에서 메일을 추출하고 사용자에게 추가 정보를 입력하도록 요구할 수 있었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-316">If this wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="7f348-317">테스트 서버이므로 메모리 내 데이터베이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-317">Because this is a test server, we simply add them to the in-memory database.</span></span>
>
>

### <a name="protect-some-endpoints"></a><span data-ttu-id="7f348-318">일부 끝점 보호</span><span class="sxs-lookup"><span data-stu-id="7f348-318">Protect some endpoints</span></span>
<span data-ttu-id="7f348-319">사용하려는 프로토콜을 통해 `passport.authenticate()` 호출을 지정하여 끝점을 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-319">You protect endpoints by specifying the `passport.authenticate()` call with the protocol that you want to use.</span></span>

<span data-ttu-id="7f348-320">서버 코드에서 좀 더 흥미로운 작업을 수행하도록 경로를 편집해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-320">To make our server code do something more interesting, let’s edit the route.</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oauth-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="step-19-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="7f348-321">19단계: 서버 응용 프로그램을 다시 실행하고 사용자를 거부하는지 확인</span><span class="sxs-lookup"><span data-stu-id="7f348-321">Step 19: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="7f348-322">`curl`을 다시 사용하여 끝점에 대해 OAuth2 보호가 적용되는지 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-322">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="7f348-323">이 끝점에 대해 클라이언트 SDK 중 하나를 실행하기 전에 이 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-323">We do this test before running any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="7f348-324">반환되는 헤더는 현재 우리가 올바른 경로에 있는지 알려줄 만큼 충분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-324">The headers that are returned should be enough to tell us if we're going down the right path.</span></span>

1. <span data-ttu-id="7f348-325">먼저 mongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-325">First, make sure that your mongoDB instance is running:</span></span>

    `$sudo mongod`

2. <span data-ttu-id="7f348-326">그런 다음 해당 디렉터리로 변경하고 curl을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-326">Then, change to the directory and start curling.</span></span>

      <span data-ttu-id="7f348-327">`$ cd azuread` `$ node server.js`</span><span class="sxs-lookup"><span data-stu-id="7f348-327">`$ cd azuread` `$ node server.js`</span></span>

3. <span data-ttu-id="7f348-328">기본 POST를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-328">Try a basic POST.</span></span>

    `$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

    ```Shell
    HTTP/1.1 401 Unauthorized
    Connection: close
    WWW-Authenticate: Bearer realm="Users"
    Date: Tue, 14 Jul 2015 05:45:03 GMT
    Transfer-Encoding: chunked
    ```

<span data-ttu-id="7f348-329">여기서 우리가 찾는 응답은 401입니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-329">A 401 is the response you are looking for here.</span></span> <span data-ttu-id="7f348-330">이 응답은 Passport 계층이 인증된 끝점으로 리디렉션을 시도하고 있음을 나타냅니다. 정확하게 우리가 원하는 대로 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-330">This response indicates that the Passport layer is trying to redirect to the authorized endpoint, which is exactly what you want.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f348-331">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7f348-331">Next steps</span></span>
<span data-ttu-id="7f348-332">OAuth2 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-332">You've gone as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="7f348-333">이제 추가 연습 과정을 진행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-333">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="7f348-334">Restify 및 OAuth2를 사용하여 REST API를 구현하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-334">You've now learned how to implement a REST API by using Restify and OAuth2.</span></span> <span data-ttu-id="7f348-335">또한 계속해서 서비스를 개발하고 이 예제를 바탕으로 구축하는 데 도움이 되는 코드를 충분히 제공해 드렸습니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-335">You also have more than enough code to keep developing your service and learning how to build on this example.</span></span>

<span data-ttu-id="7f348-336">ADAL 과정의 다음 단계에 관심이 있는 경우 여기서 권장하는 지원되는 ADAL 클라이언트로 계속 진행하세요.</span><span class="sxs-lookup"><span data-stu-id="7f348-336">If you are interested in the next steps in your ADAL journey, here are some supported ADAL clients we recommend that you  keep working with.</span></span>

<span data-ttu-id="7f348-337">개발자 컴퓨터에 복제하고 연습에 설명된 대로 구성하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f348-337">Clone down to your developer machine and configure as described in the walkthrough.</span></span>

[<span data-ttu-id="7f348-338">iOS용 ADAL(영문)</span><span class="sxs-lookup"><span data-stu-id="7f348-338">ADAL for iOS</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)

[<span data-ttu-id="7f348-339">Android용 ADAL(영문)</span><span class="sxs-lookup"><span data-stu-id="7f348-339">ADAL for Android</span></span>](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
