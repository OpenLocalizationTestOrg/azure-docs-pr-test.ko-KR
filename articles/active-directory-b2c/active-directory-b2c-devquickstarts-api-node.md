---
title: "Azure AD B2C: Node.js를 사용하여 Web API 보안 유지 | Microsoft Docs"
description: "B2C 테넌트에서 토큰을 수락하는 Node.js Web API를 빌드하는 방법"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: fc2b9af8-fbda-44e0-962a-8b963449106a
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: xerners
ms.openlocfilehash: 6480be75c314ede1b786e959a79c0385dd2edea8
ms.sourcegitcommit: 73f159cdbc122ffe42f3e1f7a3de05f77b6a4725
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="bf550-103">Azure AD B2C: Node.js를 사용하여 Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="bf550-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="bf550-104">Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="bf550-105">이 토큰을 통해 클라이언트 앱이 Azure AD B2C를 사용하여 API에 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-105">These tokens allow your client apps that use Azure AD B2C to authenticate to the API.</span></span> <span data-ttu-id="bf550-106">이 문서에서는 사용자가 태스크를 추가하고 나열할 수 있는 "할 일 모음" API를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-106">This article shows you how to create a "to-do list" API that allows users to add and list tasks.</span></span> <span data-ttu-id="bf550-107">Web API는 Azure AD B2C를 사용하여 보호되며 사용자가 해당 할 일 목록을 관리하도록 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-107">The web API is secured using Azure AD B2C and only allows authenticated users to manage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="bf550-108">이 샘플은 [iOS B2C 샘플 응용 프로그램](active-directory-b2c-devquickstarts-ios.md)을 사용하여 연결되도록 작성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-108">This sample was written to be connected to by using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="bf550-109">현재 연습을 먼저 수행한 다음 해당 샘플도 함께 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="bf550-109">Do the current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="bf550-110">**Passport** 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="bf550-111">유연한 모듈식 Passport는 어떤 Express 기반 또는 Restify 웹 응용 프로그램에도 원활하게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="bf550-112">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="bf550-113">Microsoft는 Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bf550-114">여기서는 이 모듈을 설치하고 Azure AD `passport-azure-ad` 플러그 인에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-114">You install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="bf550-115">이 샘플을 수행하려면 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-115">To do this sample, you need to:</span></span>

1. <span data-ttu-id="bf550-116">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="bf550-117">Passport의 `azure-ad-passport` 플러그 인을 사용하도록 응용 프로그램을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-117">Set up your application to use Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="bf550-118">"to-do list" Web API를 호출하도록 클라이언트 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-118">Configure a client application to call the "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="bf550-119">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="bf550-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="bf550-120">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="bf550-121">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="bf550-122">디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="bf550-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="bf550-123">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-123">Create an application</span></span>
<span data-ttu-id="bf550-124">다음으로 B2C 디렉터리에 앱을 만들어야 하며 Azure AD가 앱과 안전하게 통신해야 한다는 일부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-124">Next, you need to create an app in your B2C directory that gives Azure AD some information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="bf550-125">이 경우 하나의 논리 앱을 구성하기 때문에 클라이언트 앱과 Web API 모두는 단일 **응용 프로그램 ID**에서 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-125">In this case, both the client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="bf550-126">앱을 만들려면 [다음 지침](active-directory-b2c-app-registration.md)에 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="bf550-127">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-127">Be sure to:</span></span>

* <span data-ttu-id="bf550-128">응용 프로그램에서 **웹앱/웹 API** 포함</span><span class="sxs-lookup"><span data-stu-id="bf550-128">Include a **web app/web api** in the application</span></span>
* <span data-ttu-id="bf550-129">**회신 URL**로 `http://localhost/TodoListService`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="bf550-130">이 코드 샘플에 대한 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-130">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="bf550-131">응용 프로그램에 **응용 프로그램 암호** 를 만들고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="bf550-132">이 데이터가 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-132">You need this data later.</span></span> <span data-ttu-id="bf550-133">참고로 이 값은 사용하기 전에 [XML 이스케이프](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="bf550-134">앱에 할당된 **응용 프로그램 ID** 를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="bf550-135">이 데이터가 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="bf550-136">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-136">Create your policies</span></span>
<span data-ttu-id="bf550-137">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="bf550-138">이 앱은 등록 및 로그인이라는 두 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="bf550-139">[정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)에서 설명한 대로 각 형식에 하나의 정책을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-139">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="bf550-140">세 가지 정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="bf550-141">등록 정책에서 **표시 이름** 및 다른 등록 특성을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="bf550-142">모든 정책에서 **표시 이름** 및 **개체 ID** 응용 프로그램 클레임을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="bf550-143">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="bf550-144">각 정책을 만든 후에 **이름** 을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-144">Copy down the **Name** of each policy after you create it.</span></span> <span data-ttu-id="bf550-145">접두사 `b2c_1_`이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="bf550-146">이러한 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="bf550-147">세 가지 정책을 만들었다면 앱을 빌드할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-147">After you have created your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="bf550-148">Azure AD B2C에서 정책 작동 방법을 알아보려면 [.NET 웹앱 시작 자습서](active-directory-b2c-devquickstarts-web-dotnet.md)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-148">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-the-code"></a><span data-ttu-id="bf550-149">코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="bf550-149">Download the code</span></span>
<span data-ttu-id="bf550-150">이 자습서에 대한 코드는 [GitHub에서 유지 관리됩니다](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="bf550-150">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="bf550-151">진행하면서 샘플을 빌드하기 위해 [골격 프로젝트를 .zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-151">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="bf550-152">구조를 복제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-152">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="bf550-153">완성된 앱도 [.zip 파일로 가능](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip)하거나 동일한 리포지토리의 `complete` 분기에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-153">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="bf550-154">사용자 플랫폼을 위한 Node.js 다운로드</span><span class="sxs-lookup"><span data-stu-id="bf550-154">Download Node.js for your platform</span></span>
<span data-ttu-id="bf550-155">이 샘플을 사용하려면 작동하는 Node.js 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-155">To successfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="bf550-156">[nodejs.org](http://nodejs.org)에서 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="bf550-157">사용자 플랫폼을 위한 MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="bf550-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="bf550-158">이 샘플을 사용하려면 작동하는 MongoDB 설치가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-158">To successfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="bf550-159">MongoDB를 사용하여 REST API가 서버 인스턴스 간에 지속되도록 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-159">We use MongoDB to make your REST API persistent across server instances.</span></span>

<span data-ttu-id="bf550-160">[mongodb.org](http://www.mongodb.org)에서 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="bf550-161">이 연습에서는 연습 과정을 작성할 때의 MongoDB에 대한 기본 설치 및 서버 끝점인 `mongodb://localhost`을(를) 사용한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-161">This walk-through assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-the-restify-modules-in-your-web-api"></a><span data-ttu-id="bf550-162">Web API에 Restify 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="bf550-162">Install the Restify modules in your web API</span></span>
<span data-ttu-id="bf550-163">REST API를 빌드하는 데 Restify를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-163">We use Restify to build your REST API.</span></span> <span data-ttu-id="bf550-164">Restify는 Express에서 파생된 유연한 최소 Node.js 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="bf550-165">Connect 위에 REST API를 구축하기 위한 강력한 기능 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="bf550-166">Restify 설치</span><span class="sxs-lookup"><span data-stu-id="bf550-166">Install Restify</span></span>
<span data-ttu-id="bf550-167">명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-167">From the command line, change your directory to `azuread`.</span></span> <span data-ttu-id="bf550-168">`azuread` 디렉터리가 존재하지 않는 경우 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-168">If the `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="bf550-169">`cd azuread` 또는 `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="bf550-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="bf550-170">다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-170">Enter the following command:</span></span>

`npm install restify`

<span data-ttu-id="bf550-171">이 명령은 Restify를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="bf550-172">오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="bf550-172">Did you get an error?</span></span>
<span data-ttu-id="bf550-173">일부 운영 체제에서 `npm`을 사용하는 경우 오류 `Error: EPERM, chmod '/usr/local/bin/..'` 및 관리자로 계정을 실행하는 요청을 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-173">In some operating systems, when you use `npm`, you may receive the error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run the account as an administrator.</span></span> <span data-ttu-id="bf550-174">이 문제가 발생하면 `sudo` 명령을 사용하여 더 높은 권한 수준으로 `npm`을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="bf550-174">If this problem occurs, use the `sudo` command to run `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="bf550-175">DTrace 오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="bf550-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="bf550-176">Restify를 설치할 때 다음 텍스트와 같은 내용이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="bf550-177">Restify는 DTrace를 사용하여 REST 호출을 추적하는 강력한 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="bf550-178">그러나 대부분의 운영 체제에서는 DTrace를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="bf550-179">이러한 오류는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="bf550-180">이 명령의 출력은 다음 텍스트와 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-180">The output of the command should appear similar to this text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="bf550-181">Web API에 Passport 설치</span><span class="sxs-lookup"><span data-stu-id="bf550-181">Install Passport in your web API</span></span>
<span data-ttu-id="bf550-182">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-182">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="bf550-183">다음 명령을 사용하여 Passport를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-183">Install Passport using the following command:</span></span>

`npm install passport`

<span data-ttu-id="bf550-184">이 명령의 출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-184">The output of the command should be similar to this text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-to-your-web-api"></a><span data-ttu-id="bf550-185">Web API에 passport-azuread 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-185">Add passport-azuread to your web API</span></span>
<span data-ttu-id="bf550-186">다음으로 Azure AD를 Passport와 함께 연결하는 전략 제품군인 `passport-azuread`를 사용하여 OAuth 전략을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-186">Next, add the OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="bf550-187">REST API 샘플에서는 이 전략을 전달자 토큰으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-187">Use this strategy for bearer tokens in the REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="bf550-188">OAuth2는 알려진 모든 토큰 유형이 발급될 수 있는 프레임워크를 제공하지만 특정 토큰 유형만 일반적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="bf550-189">끝점을 보호하기 위한 토큰이 전달자 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-189">The tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="bf550-190">전달자 토큰 형식은 OAuth2에서 가장 널리 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-190">These types of tokens are the most widely issued in OAuth2.</span></span> <span data-ttu-id="bf550-191">많은 구현에서 발급되는 유일한 토큰 유형이 전달자 토큰이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-191">Many implementations assume that bearer tokens are the only type of token issued.</span></span>
>
>

<span data-ttu-id="bf550-192">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-192">From the command line, change your directory to `azuread`, if it's not already there.</span></span>

<span data-ttu-id="bf550-193">다음 명령을 사용하여 Passport `passport-azure-ad` 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-193">Install the Passport `passport-azure-ad` module using the following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="bf550-194">이 명령의 출력은 다음 텍스트와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-194">The output of the command should be similar to this text:</span></span>

``
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
``

## <a name="add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="bf550-195">Web API에 MongoDB 모듈 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-195">Add MongoDB modules to your web API</span></span>
<span data-ttu-id="bf550-196">이 샘플을 MongoDB를 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="bf550-197">Mongoose 설치는 모델 및 스키마를 관리하는 데 널리 사용되는 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="bf550-198">추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="bf550-198">Install additional modules</span></span>
<span data-ttu-id="bf550-199">다음에는 나머지 필수 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-199">Next, install the remaining required modules.</span></span>

<span data-ttu-id="bf550-200">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-200">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-201">`node_modules` 디렉터리에 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-201">Install the modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="bf550-202">종속성을 적용하여 server.js 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="bf550-203">`server.js` 파일은 Web API 서버에 대한 대부분의 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-203">The `server.js` file provides the majority of the functionality for your Web API server.</span></span>

<span data-ttu-id="bf550-204">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-204">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-205">편집기에서 `server.js` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="bf550-206">다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-206">Add the following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var fs = require('fs');
var path = require('path');
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').BearerStrategy;
```

<span data-ttu-id="bf550-207">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-207">Save the file.</span></span> <span data-ttu-id="bf550-208">나중에 이 파일로 다시 돌아갈 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-208">You return to it later.</span></span>

## <a name="create-a-configjs-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="bf550-209">Azure AD 설정을 저장하기 위한 config.js 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-209">Create a config.js file to store your Azure AD settings</span></span>
<span data-ttu-id="bf550-210">이 코드 파일은 Azure AD 포털의 구성 매개 변수를 `Passport.js` 파일에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-210">This code file passes the configuration parameters from your Azure AD Portal to the `Passport.js` file.</span></span> <span data-ttu-id="bf550-211">이 연습의 첫 번째 부분에서 포털에 Web API를 추가했을 때 이러한 구성 값을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-211">You created these configuration values when you added the web API to the portal in the first part of the walk-through.</span></span> <span data-ttu-id="bf550-212">코드를 복사한 후에 이러한 매개 변수 값에 추가할 항목에 대해 설명할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-212">We explain what to put in the values of these parameters after you copy the code.</span></span>

<span data-ttu-id="bf550-213">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-213">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-214">편집기에서 `config.js` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="bf550-215">다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-215">Add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in the portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // the Client ID of the application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add the B2C tenant name in the <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is the policy you'll want to validate against in B2C. Usually this is your Sign-in policy (as users sign in to this API)
passReqToCallback: false // This is a node.js construct that lets you pass the req all the way back to any upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="bf550-216">필요한 값</span><span class="sxs-lookup"><span data-stu-id="bf550-216">Required values</span></span>
<span data-ttu-id="bf550-217">`clientID`: 웹 API 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-217">`clientID`: The client ID of your Web API application.</span></span>

<span data-ttu-id="bf550-218">`IdentityMetadata`: `passport-azure-ad`가 ID 공급자에 대한 구성 데이터를 찾는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for the identity provider.</span></span> <span data-ttu-id="bf550-219">JSON 웹 토큰의 유효성을 검사하는 키도 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-219">It also looks for the keys to validate the JSON web tokens.</span></span>

<span data-ttu-id="bf550-220">`audience`: 응용 프로그램 호출을 식별하는 포털의 URI(Uniform Resource Identifier)입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-220">`audience`: The uniform resource identifier (URI) from the portal that identifies your calling application.</span></span>

<span data-ttu-id="bf550-221">`tenantName`: 해당 테넌트 이름입니다(예: **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="bf550-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="bf550-222">`policyName`: 서버로 들어오는 토큰의 유효성을 검사하려는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-222">`policyName`: The policy that you want to validate the tokens coming in to your server.</span></span> <span data-ttu-id="bf550-223">이 정책은 클라이언트 응용 프로그램에서 로그인에 사용하는 것과 동일한 정책이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-223">This policy should be the same policy that you use on the client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="bf550-224">이제 클라이언트와 서버 설정 모두에서 동일한 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-224">For now, use the same policies across both client and server setup.</span></span> <span data-ttu-id="bf550-225">이미 연습 단계를 완료하고 이러한 정책을 만든 경우에는 다시 작업을 수행하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-225">If you have already completed a walk-through and created these policies, you don't need to do so again.</span></span> <span data-ttu-id="bf550-226">연습 단계를 완료했으므로 사이트에서 클라이언트 연습에 대해 새 정책을 설정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-226">Because you completed the walk-through, you shouldn't need to set up new policies for client walk-throughs on the site.</span></span>
>
>

## <a name="add-configuration-to-your-serverjs-file"></a><span data-ttu-id="bf550-227">server.js 파일에 구성 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-227">Add configuration to your server.js file</span></span>
<span data-ttu-id="bf550-228">만든 `config.js` 파일에서 값을 참고하려면 응용 프로그램에 필수 리소스로 `.config` 파일을 추가하고 전역 변수를 `config.js` 문서의 변수로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-228">To read the values from the `config.js` file you created, add the `.config` file as a required resource in your application, and then set the global variables to those in the `config.js` document.</span></span>

<span data-ttu-id="bf550-229">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-229">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-230">편집기에서 `server.js` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-230">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="bf550-231">다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-231">Add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="bf550-232">다음 코드를 포함하는 `server.js`에 새 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-232">Add a new section to `server.js` that includes the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.

var options = {
    // The URL of the metadata document for your app. We put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="bf550-233">다음으로 응용 프로그램 호출에서 수신한 사용자에 몇 가지 자리 표시자를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-233">Next, let's add some placeholders for the users we receive from our calling applications.</span></span>

```Javascript
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="bf550-234">계속해서 로거를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-the-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="bf550-235">Moongoose를 사용하여 MongoDB 모델 및 스키마 정보 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-235">Add the MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="bf550-236">REST API 서비스에서 이러한 세 파일을 함께 가져옴에 따라 이전 준비가 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-236">The earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="bf550-237">이 연습의 경우 앞에서 설명한 대로 MongoDB를 사용하여 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-237">For this walk-through, use MongoDB to store your tasks, as discussed earlier.</span></span>

<span data-ttu-id="bf550-238">`config.js` 파일에서 데이터베이스 **tasklist**를 호출했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-238">In the `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="bf550-239">해당 이름은 `mongoose_auth_local` 연결 URL의 끝에도 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-239">That name was also what you put at the end of the `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="bf550-240">MongoDB에서 이 데이터베이스를 미리 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-240">You don't need to create this database beforehand in MongoDB.</span></span> <span data-ttu-id="bf550-241">서버 응용 프로그램을 처음으로 실행할 경우 사용자에 대한 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-241">It creates the database for you on the first run of your server application.</span></span>

<span data-ttu-id="bf550-242">사용하려는 MongoDB 데이터베이스를 서버에 알린 후에는 일부 추가 코드를 작성하여 서버 작업에 대한 모델 및 스키마를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-242">After you tell the server which MongoDB database to use, you need to write some additional code to create the model and schema for your server tasks.</span></span>

### <a name="expand-the-model"></a><span data-ttu-id="bf550-243">모델 확장</span><span class="sxs-lookup"><span data-stu-id="bf550-243">Expand the model</span></span>
<span data-ttu-id="bf550-244">이 스키마 모델은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-244">This schema model is simple.</span></span> <span data-ttu-id="bf550-245">필요에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-245">You can expand it as required.</span></span>

<span data-ttu-id="bf550-246">`owner`: 작업에 할당된 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-246">`owner`: Who is assigned to the task.</span></span> <span data-ttu-id="bf550-247">이 개체는 **문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-247">This object is a **string**.</span></span>  

<span data-ttu-id="bf550-248">`Text`: 작업 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-248">`Text`: The task itself.</span></span> <span data-ttu-id="bf550-249">이 개체는 **문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-249">This object is a **string**.</span></span>

<span data-ttu-id="bf550-250">`date`: 작업이 만료되는 날짜입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-250">`date`: The date that the task is due.</span></span> <span data-ttu-id="bf550-251">이 개체는 **날짜/시간**입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-251">This object is a **datetime**.</span></span>

<span data-ttu-id="bf550-252">`completed`: 작업이 완료된 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-252">`completed`: If the task is complete.</span></span> <span data-ttu-id="bf550-253">이 개체는 **부울**입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-253">This object is a **Boolean**.</span></span>

### <a name="create-the-schema-in-the-code"></a><span data-ttu-id="bf550-254">코드에 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-254">Create the schema in the code</span></span>
<span data-ttu-id="bf550-255">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-255">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-256">편집기에서 `server.js` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-256">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="bf550-257">구성 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-257">Add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="bf550-258">먼저 스키마를 만든 후 **경로**를 정의할 때 코드 전체에 데이터를 저장하는 데 사용할 모델 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-258">You first create the schema, and then you create a model object that you use to store your data throughout the code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="bf550-259">REST API 작업 서버에 대한 경로 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="bf550-260">작업할 데이터베이스 모델이 준비되었으므로 REST API 서버에 사용할 경로를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-260">Now that you have a database model to work with, add the routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="bf550-261">Restify의 경로 정보</span><span class="sxs-lookup"><span data-stu-id="bf550-261">About routes in Restify</span></span>
<span data-ttu-id="bf550-262">경로는 Express 스택을 사용할 때 작업하는 것과 동일한 방식으로 Restify에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-262">Routes work in Restify in the same way that they work when they use the Express stack.</span></span> <span data-ttu-id="bf550-263">클라이언트 응용 프로그램이 호출할 것으로 예상하는 URI를 사용하여 경로를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-263">You define routes by using the URI that you expect the client applications to call.</span></span>

<span data-ttu-id="bf550-264">Restify 경로의 일반적인 패턴:</span><span class="sxs-lookup"><span data-stu-id="bf550-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="bf550-265">Resitfy 및 Express는 응용 프로그램 유형 정의 및 여러 다른 끝점에서 복잡한 라우팅 수행 등의 훨씬 더 수준 높은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="bf550-266">이 자습서의 목적에 따라 이러한 경로를 간단하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-266">For the purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-to-your-server"></a><span data-ttu-id="bf550-267">서버에 기본 경로 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-267">Add default routes to your server</span></span>
<span data-ttu-id="bf550-268">이제 REST API에 대한 **만들기** 및 **나열**이라는 기본 CRUD 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-268">You now add the basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="bf550-269">다른 경로는 샘플의 `complete` 분기에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-269">Other routes can be found in the `complete` branch of the sample.</span></span>

<span data-ttu-id="bf550-270">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-270">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="bf550-271">편집기에서 `server.js` 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-271">Open the `server.js` file in an editor.</span></span> <span data-ttu-id="bf550-272">위에서 작성한 데이터베이스 항목 아래에 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-272">Below the database entries you made above add the following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it to Mongodb
    var _task = new Task();

    if (!req.params.Text) {
        req.log.warn({
            params: req.params
        }, 'createTodo: missing task');
        next(new MissingTaskError());
        return;
    }

    _task.owner = owner;
    _task.Text = req.params.Text;
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
```

```Javascript
/// Simple returns the list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you to set default headers
    // This headers comply with CORS and allow us to mongodbServer our response to any origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    log.info("listTasks was called for: ", owner);

    Task.find({
        owner: owner
    }).limit(20).sort('date').exec(function(err, data) {

        if (err)
            return next(err);

        if (data.length > 0) {
            log.info(data);
        }

        if (!data.length) {
            log.warn(err, "There is no tasks in the database. Add one!");
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


#### <a name="add-error-handling-for-the-routes"></a><span data-ttu-id="bf550-273">경로에 대한 오류 처리 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-273">Add error handling for the routes</span></span>
<span data-ttu-id="bf550-274">일부 오류 처리를 추가하여 클라이언트에 다시 발생할 수 있는 문제를 이해할 수 있는 방식으로 통신할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-274">Add some error handling so that you can communicate any problems you encounter back to the client in a way that it can understand.</span></span>

<span data-ttu-id="bf550-275">다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-275">Add the following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
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


## <a name="create-your-server"></a><span data-ttu-id="bf550-276">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="bf550-276">Create your server</span></span>
<span data-ttu-id="bf550-277">이제 데이터베이스를 정의하고 경로를 적용했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="bf550-278">마지막으로 할 일은 호출을 관리할 서버 인스턴스를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-278">The last thing for you to do is to add the server instance that manages your calls.</span></span>

<span data-ttu-id="bf550-279">Restify 및 Express는 REST API 서버에 대한 세부적인 사용자 지정 기능을 제공하지만 여기서는 가장 기본적인 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-279">Restify and Express provide deep customization for a REST API server, but we use the most basic setup here.</span></span>

```Javascript

/**
 * Our Server
 */


var server = restify.createServer({
    name: "Microsoft Azure Active Directroy TODO Server",
    version: "2.0.1"
});

// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());

// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());

// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());

// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());

// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping to REST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-the-routes-to-the-server-without-authentication"></a><span data-ttu-id="bf550-280">서버에 경로 추가(인증 없이)</span><span class="sxs-lookup"><span data-stu-id="bf550-280">Add the routes to the server (without authentication)</span></span>
```Javascript
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), listTasks);
server.get('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.head('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), getTask);
server.post('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.post('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), createTask);
server.del('/api/tasks/:owner/:task', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks/:owner', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeTask);
server.del('/api/tasks', passport.authenticate('oauth-bearer', {
    session: false
}), removeAll, function respond(req, res, next) {
    res.send(204);
    next();
});


// Register a default '/' handler

server.get('/', function root(req, res, next) {
    var routes = [
        'GET     /',
        'POST    /api/tasks/:owner/:task',
        'POST    /api/tasks (for JSON body)',
        'GET     /api/tasks',
        'PUT     /api/tasks/:owner',
        'GET     /api/tasks/:owner',
        'DELETE  /api/tasks/:owner/:task'
    ];
    res.send(200, routes);
    next();
});
```

```Javascript

server.listen(serverPort, function() {

    var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
    consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
    consoleMessage += '\n %s server is listening at %s';
    consoleMessage += '\n Open your browser to %s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-to-your-rest-api-server"></a><span data-ttu-id="bf550-281">REST API 서버에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="bf550-281">Add authentication to your REST API server</span></span>
<span data-ttu-id="bf550-282">이제 실행 중인 REST API 서버가 있고 Azure AD에 대해 유용하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="bf550-283">아직 없는 경우 명령줄에서 해당 디렉터리를 `azuread`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-283">From the command line, change your directory to `azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="bf550-284">passport-azure-ad에 포함된 OIDCBearerStrategy 사용</span><span class="sxs-lookup"><span data-stu-id="bf550-284">Use the OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="bf550-285">API를 작성하는 경우 항상 사용자가 스푸핑할 수 없는 토큰의 고유한 항목에 데이터를 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-285">When you write APIs, you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="bf550-286">이 서버는 ToDo 항목을 저장할 때 "소유자" 필드에 넣은 토큰(token.oid를 통해 호출됨)에서 사용자의 **oid** 를 기준으로 항목을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-286">When the server stores ToDo items, it does so based on the **oid** of the user in the token (called through token.oid), which goes in the “owner” field.</span></span> <span data-ttu-id="bf550-287">이 값은 해당 사용자만 자신의 할 일 항목에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="bf550-288">API에 "owner"가 노출되지 않으므로 외부 사용자가 인증된 경우에도 다른 사용자의 ToDo 항목을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-288">There is no exposure in the API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="bf550-289">다음으로 `passport-azure-ad`와 함께 전달자 전략을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-289">Next, use the bearer strategy that comes with `passport-azure-ad`.</span></span>

```Javascript
var findById = function(id, fn) {
    for (var i = 0, len = users.length; i < len; i++) {
        var user = users[i];
        if (user.oid === id) {
            log.info('Found user: ', user);
            return fn(null, user);
        }
    }
    return fn(null, null);
};


var oidcStrategy = new OIDCBearerStrategy(options,
    function(token, done) {
        log.info('verifying the user');
        log.info(token, 'was the token retreived');
        findById(token.sub, function(err, user) {
            if (err) {
                return done(err);
            }
            if (!user) {
                // "Auto-registration"
                log.info('User was added automatically as they were new. Their sub is: ', token.oid);
                users.push(token);
                owner = token.oid;
                return done(null, token);
            }
            owner = token.sub;
            return done(null, user, token);
        });
    }
);

passport.use(oidcStrategy);
```

<span data-ttu-id="bf550-290">Passport는 모든 전략에 동일한 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-290">Passport uses the same pattern for all its strategies.</span></span> <span data-ttu-id="bf550-291">사용자는 이를 `token` 및 `done`을 매개 변수로 포함하는 `function()`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="bf550-292">전략은 모든 작업을 완료한 후에 사용자에게 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-292">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="bf550-293">그런 다음 사용자를 저장하고 다시 요청하지 않아도 되도록 토큰을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-293">You should then store the user and save the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf550-294">위 코드는 서버에 인증하는 모든 사용자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-294">The code above takes any user who happens to authenticate to your server.</span></span> <span data-ttu-id="bf550-295">이 프로세스를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-295">This process is known as autoregistration.</span></span> <span data-ttu-id="bf550-296">프로덕션 서버에서는 등록 프로세스를 먼저 통과하지 않으면 사용자에게 API 액세스를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-296">In production servers, don't let in any users access the API without first having them go through a registration process.</span></span> <span data-ttu-id="bf550-297">일반적으로 이 프로세스는 Facebook을 사용하여 등록할 수 있도록 하지만 추가 정보를 입력하도록 요구하는 소비자 앱에서 나타나는 패턴입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-297">This process is usually the pattern you see in consumer apps that allow you to register by using Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="bf550-298">이 프로그램이 명령줄 프로그램이 아니라면 반환된 토큰 개체에서 메일을 추출하고 사용자에게 추가 정보를 입력하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-298">If this program wasn’t a command-line program, we could have extracted the email from the token object that is returned and then asked users to fill out additional information.</span></span> <span data-ttu-id="bf550-299">샘플이기 때문에 메모리 내 데이터베이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-299">Because this is a sample, we add them to an in-memory database.</span></span>
>
>

## <a name="run-your-server-application-to-verify-that-it-rejects-you"></a><span data-ttu-id="bf550-300">서버 응용 프로그램을 실행하고 사용자를 거부하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-300">Run your server application to verify that it rejects you</span></span>
<span data-ttu-id="bf550-301">`curl`을 사용하여 끝점에 대해 OAuth2 보호가 적용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-301">You can use `curl` to see if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="bf550-302">반환되는 헤더는 올바른 경로에 있는지 알려줄 만큼 충분해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-302">The headers returned should be enough to tell you that you are on the right path.</span></span>

<span data-ttu-id="bf550-303">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="bf550-304">디렉터리로 변경하고 서버를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-304">Change to the directory and run the server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="bf550-305">새 터미널 창에서 `curl`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="bf550-306">기본 POST를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="bf550-307">401 오류는 원하는 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-307">A 401 error is the response you want.</span></span> <span data-ttu-id="bf550-308">Passport 계층이 권한 부여 끝점으로 리디렉션을 시도함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-308">It indicates that the Passport layer is trying to redirect to the authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="bf550-309">이제 OAuth2를 사용하는 REST API 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="bf550-310">Restify 및 OAuth를 사용하여 REST API를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="bf550-311">이제 충분한 코드가 있으므로 계속해서 서비스를 개발하고 이 예제를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-311">You now have sufficient code so that you can continue to develop your service and build on this example.</span></span> <span data-ttu-id="bf550-312">OAuth2 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="bf550-313">이를 위해 다음 단계에서는 [B2C를 포함한 iOS를 사용하여 웹 API에 연결](active-directory-b2c-devquickstarts-ios.md) 연습과 같은 추가 연습을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-313">For that next step use an additional walk-through like our [Connect to a web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf550-314">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf550-314">Next steps</span></span>
<span data-ttu-id="bf550-315">이제 다음과 같이 좀 더 고급 항목으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf550-315">You can now move to more advanced topics, such as:</span></span>

[<span data-ttu-id="bf550-316">B2C로 iOS를 사용하여 Web API에 연결</span><span class="sxs-lookup"><span data-stu-id="bf550-316">Connect to a web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
