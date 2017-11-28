---
title: "Azure AD B2C: Node.js를 사용하여 Web API 보안 유지 | Microsoft Docs"
description: "B2C 테 넌 트의 토큰을 수락 하는 Node.js toobuild 웹 API 하는 방법"
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
ms.openlocfilehash: 47f5bae025a9ba2f486e36acef36aa37cfb43543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-secure-a-web-api-by-using-nodejs"></a><span data-ttu-id="6ab32-103">Azure AD B2C: Node.js를 사용하여 Web API 보안 유지</span><span class="sxs-lookup"><span data-stu-id="6ab32-103">Azure AD B2C: Secure a web API by using Node.js</span></span>
<!-- TODO [AZURE.INCLUDE [active-directory-b2c-devquickstarts-web-switcher](../../includes/active-directory-b2c-devquickstarts-web-switcher.md)]-->

<span data-ttu-id="6ab32-104">Azure AD(Azure Active Directory) B2C로 OAuth 2.0 액세스 토큰을 사용하여 Web API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-104">With Azure Active Directory (Azure AD) B2C, you can secure a web API by using OAuth 2.0 access tokens.</span></span> <span data-ttu-id="6ab32-105">이러한 토큰 Azure AD B2C tooauthenticate toohello API를 사용 하 여 클라이언트 앱을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-105">These tokens allow your client apps that use Azure AD B2C tooauthenticate toohello API.</span></span> <span data-ttu-id="6ab32-106">이 문서에서는 어떻게 toocreate "할 일 목록" API, 사용자가 허용 tooadd 및 목록 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-106">This article shows you how toocreate a "to-do list" API that allows users tooadd and list tasks.</span></span> <span data-ttu-id="6ab32-107">hello 웹 API는 Azure AD B2C를 사용 하 여 보안 처리 되며 toomanage 인증 된 사용자의 할 일 목록을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-107">hello web API is secured using Azure AD B2C and only allows authenticated users toomanage their to-do list.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab32-108">이 샘플을 사용 하 여 연결 toobe tooby 쓰여진 우리의 [iOS B2C 샘플 응용 프로그램](active-directory-b2c-devquickstarts-ios.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-108">This sample was written toobe connected tooby using our [iOS B2C sample application](active-directory-b2c-devquickstarts-ios.md).</span></span> <span data-ttu-id="6ab32-109">현재 단계를 먼저 hello 및 다음 예제를 따라가려면 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-109">Do hello current walk-through first, and then follow along with that sample.</span></span>
>
>

<span data-ttu-id="6ab32-110">**Passport** 는 Node.js에 대한 인증 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="6ab32-111">유연한 모듈식 Passport는 어떤 Express 기반 또는 Restify 웹 응용 프로그램에도 원활하게 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-111">Flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="6ab32-112">포괄적인 전략 모음이 사용자 이름 및 암호, Facebook, Twitter 등을 사용하는 인증을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-112">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6ab32-113">Microsoft는 Azure AD(Azure Active Directory)에 대한 전략을 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-113">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6ab32-114">이 모듈을 설치 하 고 다음 hello Azure AD 추가 `passport-azure-ad` 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-114">You install this module and then add hello Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="6ab32-115">toodo이이 샘플에서는 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-115">toodo this sample, you need to:</span></span>

1. <span data-ttu-id="6ab32-116">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-116">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="6ab32-117">사용자 응용 프로그램 toouse Passport의 설정 `azure-ad-passport` 플러그 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-117">Set up your application toouse Passport's `azure-ad-passport` plug-in.</span></span>
3. <span data-ttu-id="6ab32-118">클라이언트 응용 프로그램 toocall hello "할 일 목록" web API를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-118">Configure a client application toocall hello "to-do list" web API.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="6ab32-119">Azure AD B2C 디렉터리 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ab32-119">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="6ab32-120">Azure AD B2C를 사용하기 전에 디렉터리 또는 테넌트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-120">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="6ab32-121">디렉터리는 모든 사용자, 앱, 그룹 등을 위한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-121">A directory is a container for all users, apps, groups, and more.</span></span>  <span data-ttu-id="6ab32-122">디렉터리가 없는 경우 계속하기 전에 [B2C 디렉터리를 만듭니다](active-directory-b2c-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="6ab32-122">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="6ab32-123">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-123">Create an application</span></span>
<span data-ttu-id="6ab32-124">응용 프로그램과 함께 Azure AD 필요 하다 고 toosecurely 몇 가지 정보를 제공 하 여 B2C 디렉터리에 응용 프로그램 통신 toocreate을 다음으로, 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-124">Next, you need toocreate an app in your B2C directory that gives Azure AD some information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="6ab32-125">이 경우 hello 클라이언트 응용 프로그램 및 web API 모두 표시 됩니다는 단일 **응용 프로그램 ID**하나의 논리 앱 구성 되므로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-125">In this case, both hello client app and web API are represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="6ab32-126">응용 프로그램, 프로그램 toocreate 따라 [이러한 지침](active-directory-b2c-app-registration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-126">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="6ab32-127">다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-127">Be sure to:</span></span>

* <span data-ttu-id="6ab32-128">포함 된 **웹 응용 프로그램/웹 api** hello 응용 프로그램에서</span><span class="sxs-lookup"><span data-stu-id="6ab32-128">Include a **web app/web api** in hello application</span></span>
* <span data-ttu-id="6ab32-129">**회신 URL**로 `http://localhost/TodoListService`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-129">Enter `http://localhost/TodoListService` as a **Reply URL**.</span></span> <span data-ttu-id="6ab32-130">이 코드 샘플에 대 한 hello 기본 URL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-130">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="6ab32-131">응용 프로그램에 **응용 프로그램 암호** 를 만들고 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="6ab32-132">이 데이터가 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-132">You need this data later.</span></span> <span data-ttu-id="6ab32-133">이 값 toobe 필요 함을 참고 [XML 이스케이프](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) 사용 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="6ab32-133">Note that this value needs toobe [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
* <span data-ttu-id="6ab32-134">복사 hello **응용 프로그램 ID** 할당된 tooyour 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-134">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="6ab32-135">이 데이터가 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-135">You need this data later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="6ab32-136">정책 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-136">Create your policies</span></span>
<span data-ttu-id="6ab32-137">Azure AD B2C에서 모든 사용자 환경은 [정책](active-directory-b2c-reference-policies.md)에 의해 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6ab32-138">이 앱은 등록 및 로그인이라는 두 가지 ID 환경을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-138">This app contains two identity experiences: sign up and sign in.</span></span> <span data-ttu-id="6ab32-139">에 설명 된 대로 각 유형별로 하나의 정책 toocreate 필요는 [정책 참조 문서](active-directory-b2c-reference-policies.md#create-a-sign-up-policy)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-139">You need toocreate one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span>  <span data-ttu-id="6ab32-140">세 가지 정책을 만들 때 다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-140">When you create your three policies, be sure to:</span></span>

* <span data-ttu-id="6ab32-141">Hello 선택 **표시 이름** 및 등록 정책에 등록 기타 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-141">Choose hello **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="6ab32-142">Hello 선택 **표시 이름** 및 **개체 ID** 모든 정책에 대 한 응용 프로그램 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-142">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span>  <span data-ttu-id="6ab32-143">물론 다른 클레임을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-143">You can choose other claims as well.</span></span>
* <span data-ttu-id="6ab32-144">Hello 아래로 복사 **이름** 를 만든 후 각 정책의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-144">Copy down hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="6ab32-145">Hello 접두사 있어야 `b2c_1_`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-145">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="6ab32-146">이러한 정책 이름이 나중에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-146">You need those policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="6ab32-147">준비 toobuild 하 여 세 가지 정책을 만든 후 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-147">After you have created your three policies, you're ready toobuild your app.</span></span>

<span data-ttu-id="6ab32-148">toolearn Azure AD B2C의 정책 작동 방식에 대 한 hello로 시작 [.NET 웹 응용 프로그램 시작 자습서](active-directory-b2c-devquickstarts-web-dotnet.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-148">toolearn about how policies work in Azure AD B2C, start with hello [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="6ab32-149">Hello 코드 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ab32-149">Download hello code</span></span>
<span data-ttu-id="6ab32-150">이 자습서에 대 한 코드를 hello [GitHub에서 유지 관리 됩니다](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-150">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS).</span></span> <span data-ttu-id="6ab32-151">할 수 있습니다 때 toobuild hello 샘플으로 이동 [기본 프로젝트를.zip 파일로 다운로드](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip)합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-151">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="6ab32-152">Hello 구조를 복제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-152">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS.git
```

<span data-ttu-id="6ab32-153">완료 하는 hello 앱 이기도 [.zip 파일로 사용할](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) 컴퓨터나 hello `complete` hello의 분기 같은 리포지토리 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-153">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebAPI-NodeJS/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

## <a name="download-nodejs-for-your-platform"></a><span data-ttu-id="6ab32-154">사용자 플랫폼을 위한 Node.js 다운로드</span><span class="sxs-lookup"><span data-stu-id="6ab32-154">Download Node.js for your platform</span></span>
<span data-ttu-id="6ab32-155">이 샘플을 사용 하는 toosuccessfully Node.js 설치 중인을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-155">toosuccessfully use this sample, you need a working installation of Node.js.</span></span>

<span data-ttu-id="6ab32-156">[nodejs.org](http://nodejs.org)에서 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-156">Install Node.js from [nodejs.org](http://nodejs.org).</span></span>

## <a name="install-mongodb-for-your-platform"></a><span data-ttu-id="6ab32-157">사용자 플랫폼을 위한 MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="6ab32-157">Install MongoDB for your platform</span></span>
<span data-ttu-id="6ab32-158">이 샘플을 사용 하는 toosuccessfully를 MongoDB 설치 되어 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-158">toosuccessfully use this sample, you need a working installation of MongoDB.</span></span> <span data-ttu-id="6ab32-159">사용 MongoDB toomake 영구 REST API 서버 인스턴스에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-159">We use MongoDB toomake your REST API persistent across server instances.</span></span>

<span data-ttu-id="6ab32-160">[mongodb.org](http://www.mongodb.org)에서 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-160">Install MongoDB from [mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="6ab32-161">이 연습에서는 hello 기본 설치 및 서버 끝점을 사용 하 여이 문서 작성 시 hello는 MongoDB에 대 한 가정 `mongodb://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-161">This walk-through assumes that you use hello default installation and server endpoints for MongoDB, which at hello time of this writing is `mongodb://localhost`.</span></span>
>
>

## <a name="install-hello-restify-modules-in-your-web-api"></a><span data-ttu-id="6ab32-162">Web API에에서 hello Restify 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="6ab32-162">Install hello Restify modules in your web API</span></span>
<span data-ttu-id="6ab32-163">Restify toobuild REST API 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-163">We use Restify toobuild your REST API.</span></span> <span data-ttu-id="6ab32-164">Restify는 Express에서 파생된 유연한 최소 Node.js 응용 프로그램 프레임워크입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-164">Restify is a minimal and flexible Node.js application framework derived from Express.</span></span> <span data-ttu-id="6ab32-165">Connect 위에 REST API를 구축하기 위한 강력한 기능 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-165">It has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="6ab32-166">Restify 설치</span><span class="sxs-lookup"><span data-stu-id="6ab32-166">Install Restify</span></span>
<span data-ttu-id="6ab32-167">Hello 명령줄에서 디렉터리를 너무 변경`azuread`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-167">From hello command line, change your directory too`azuread`.</span></span> <span data-ttu-id="6ab32-168">경우 hello `azuread` 디렉터리 존재 하지 않습니다, 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-168">If hello `azuread` directory doesn't exist, create it.</span></span>

<span data-ttu-id="6ab32-169">`cd azuread` 또는 `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="6ab32-169">`cd azuread` or `mkdir azuread;`</span></span>

<span data-ttu-id="6ab32-170">Hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-170">Enter hello following command:</span></span>

`npm install restify`

<span data-ttu-id="6ab32-171">이 명령은 Restify를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-171">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="6ab32-172">오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="6ab32-172">Did you get an error?</span></span>
<span data-ttu-id="6ab32-173">일부 운영 체제에서 사용 하는 경우 `npm`, hello 오류가 발생할 수 있습니다 `Error: EPERM, chmod '/usr/local/bin/..'` 및 hello 계정 관리자 권한으로 실행 하는 요청입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-173">In some operating systems, when you use `npm`, you may receive hello error `Error: EPERM, chmod '/usr/local/bin/..'` and a request that you run hello account as an administrator.</span></span> <span data-ttu-id="6ab32-174">Hello를 사용 하 여 이러한 문제가 발생할 경우 `sudo` 명령 toorun `npm` 더 높은 권한 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-174">If this problem occurs, use hello `sudo` command toorun `npm` at a higher privilege level.</span></span>

#### <a name="did-you-get-a-dtrace-error"></a><span data-ttu-id="6ab32-175">DTrace 오류가 발생했나요?</span><span class="sxs-lookup"><span data-stu-id="6ab32-175">Did you get a DTrace error?</span></span>
<span data-ttu-id="6ab32-176">Restify를 설치할 때 다음 텍스트와 같은 내용이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-176">You may see something like this text when you install Restify:</span></span>

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

<span data-ttu-id="6ab32-177">Restify는 DTrace를 사용하여 REST 호출을 추적하는 강력한 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-177">Restify provides a powerful mechanism for tracing REST calls by using DTrace.</span></span> <span data-ttu-id="6ab32-178">그러나 대부분의 운영 체제에서는 DTrace를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-178">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="6ab32-179">이러한 오류는 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-179">You can safely ignore these errors.</span></span>

<span data-ttu-id="6ab32-180">hello hello 명령의 출력에는 비슷한 toothis 텍스트 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-180">hello output of hello command should appear similar toothis text:</span></span>

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

## <a name="install-passport-in-your-web-api"></a><span data-ttu-id="6ab32-181">Web API에 Passport 설치</span><span class="sxs-lookup"><span data-stu-id="6ab32-181">Install Passport in your web API</span></span>
<span data-ttu-id="6ab32-182">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="6ab32-182">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="6ab32-183">다음 명령을 hello를 사용 하 여 Passport를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-183">Install Passport using hello following command:</span></span>

`npm install passport`

<span data-ttu-id="6ab32-184">hello hello 명령의 출력에는 비슷한 toothis 텍스트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-184">hello output of hello command should be similar toothis text:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="add-passport-azuread-tooyour-web-api"></a><span data-ttu-id="6ab32-185">Passport를 azure ad tooyour 웹 API에 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-185">Add passport-azuread tooyour web API</span></span>
<span data-ttu-id="6ab32-186">다음으로 사용 하 여 hello OAuth 전략을 추가 `passport-azuread`, 제품군 Passport를 사용 하 여 Azure AD를 연결 하는 전략입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-186">Next, add hello OAuth strategy by using `passport-azuread`, a suite of strategies that connect Azure AD with Passport.</span></span> <span data-ttu-id="6ab32-187">이 전략을 사용 하 여 전달자 토큰 hello REST API 샘플에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-187">Use this strategy for bearer tokens in hello REST API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab32-188">OAuth2는 알려진 모든 토큰 유형이 발급될 수 있는 프레임워크를 제공하지만 특정 토큰 유형만 일반적으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-188">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained widespread use.</span></span> <span data-ttu-id="6ab32-189">끝점을 보호 하기 위한 hello 토큰은 bearer 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-189">hello tokens for protecting endpoints are bearer tokens.</span></span> <span data-ttu-id="6ab32-190">토큰의 이러한 유형은 hello OAuth2 가장 광범위 하 게 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-190">These types of tokens are hello most widely issued in OAuth2.</span></span> <span data-ttu-id="6ab32-191">여러 구현 전달자 토큰 발급 토큰의 형식만 hello 있다고 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-191">Many implementations assume that bearer tokens are hello only type of token issued.</span></span>
>
>

<span data-ttu-id="6ab32-192">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="6ab32-192">From hello command line, change your directory too`azuread`, if it's not already there.</span></span>

<span data-ttu-id="6ab32-193">Hello Passport 설치 `passport-azure-ad` hello 다음 명령을 사용 하 여 모듈:</span><span class="sxs-lookup"><span data-stu-id="6ab32-193">Install hello Passport `passport-azure-ad` module using hello following command:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="6ab32-194">hello hello 명령의 출력에는 비슷한 toothis 텍스트 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-194">hello output of hello command should be similar toothis text:</span></span>

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

## <a name="add-mongodb-modules-tooyour-web-api"></a><span data-ttu-id="6ab32-195">MongoDB 모듈 tooyour 웹 API에 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-195">Add MongoDB modules tooyour web API</span></span>
<span data-ttu-id="6ab32-196">이 샘플을 MongoDB를 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-196">This sample uses MongoDB as your data store.</span></span> <span data-ttu-id="6ab32-197">Mongoose 설치는 모델 및 스키마를 관리하는 데 널리 사용되는 플러그 인입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-197">For that install Mongoose, a widely used plug-in for managing models and schemas.</span></span>

* `npm install mongoose`

## <a name="install-additional-modules"></a><span data-ttu-id="6ab32-198">추가 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="6ab32-198">Install additional modules</span></span>
<span data-ttu-id="6ab32-199">다음으로, 필수 모듈 남은 hello를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-199">Next, install hello remaining required modules.</span></span>

<span data-ttu-id="6ab32-200">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-200">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-201">Hello 모듈의 설치 프로그램 `node_modules` 디렉터리:</span><span class="sxs-lookup"><span data-stu-id="6ab32-201">Install hello modules in your `node_modules` directory:</span></span>

* `npm install assert-plus`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install express`
* `npm install bunyan`

## <a name="create-a-serverjs-file-with-your-dependencies"></a><span data-ttu-id="6ab32-202">종속성을 적용하여 server.js 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-202">Create a server.js file with your dependencies</span></span>
<span data-ttu-id="6ab32-203">hello `server.js` 파일은 웹 API 서버에 대 한 hello 대부분의 hello 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-203">hello `server.js` file provides hello majority of hello functionality for your Web API server.</span></span>

<span data-ttu-id="6ab32-204">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-204">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-205">편집기에서 `server.js` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-205">Create a `server.js` file in an editor.</span></span> <span data-ttu-id="6ab32-206">Hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-206">Add hello following information:</span></span>

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

<span data-ttu-id="6ab32-207">Hello 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-207">Save hello file.</span></span> <span data-ttu-id="6ab32-208">Tooit를 나중에 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-208">You return tooit later.</span></span>

## <a name="create-a-configjs-file-toostore-your-azure-ad-settings"></a><span data-ttu-id="6ab32-209">Azure AD 설정 config.js 파일 toostore 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-209">Create a config.js file toostore your Azure AD settings</span></span>
<span data-ttu-id="6ab32-210">이 코드 파일에서 Azure AD 포털 toohello hello 구성 매개 변수를 전달 `Passport.js` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-210">This code file passes hello configuration parameters from your Azure AD Portal toohello `Passport.js` file.</span></span> <span data-ttu-id="6ab32-211">Hello 웹 API toohello 포털 hello hello 연습의 첫 번째 부분에 추가 될 때 이러한 구성 값을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-211">You created these configuration values when you added hello web API toohello portal in hello first part of hello walk-through.</span></span> <span data-ttu-id="6ab32-212">Hello 코드를 복사한 후 hello 값이 매개이 변수 중에서 어떤 tooput을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-212">We explain what tooput in hello values of these parameters after you copy hello code.</span></span>

<span data-ttu-id="6ab32-213">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-213">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-214">편집기에서 `config.js` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-214">Create a `config.js` file in an editor.</span></span> <span data-ttu-id="6ab32-215">Hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-215">Add hello following information:</span></span>

```Javascript
// Don't commit this file tooyour public repos. This config is for first-run
exports.creds = {
clientID: <your client ID for this Web API you created in hello portal>
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
audience: '<your audience URI>', // hello Client ID of hello application that is calling your API, usually a web API or native client
identityMetadata: 'https://login.microsoftonline.com/<tenant name>/.well-known/openid-configuration', // Make sure you add hello B2C tenant name in hello <tenant name> area
tenantName:'<tenant name>',
policyName:'b2c_1_<sign in policy name>' // This is hello policy you'll want toovalidate against in B2C. Usually this is your Sign-in policy (as users sign in toothis API)
passReqToCallback: false // This is a node.js construct that lets you pass hello req all hello way back tooany upstream caller. We turn this off as there is no upstream caller.
};

```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="required-values"></a><span data-ttu-id="6ab32-216">필요한 값</span><span class="sxs-lookup"><span data-stu-id="6ab32-216">Required values</span></span>
<span data-ttu-id="6ab32-217">`clientID`: hello Web API 응용 프로그램의 클라이언트 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-217">`clientID`: hello client ID of your Web API application.</span></span>

<span data-ttu-id="6ab32-218">`IdentityMetadata`: 여기에 `passport-azure-ad` hello id 공급자에 대 한 구성 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-218">`IdentityMetadata`: This is where `passport-azure-ad` looks for your configuration data for hello identity provider.</span></span> <span data-ttu-id="6ab32-219">Hello 키 toovalidate hello JSON 웹 토큰에 대 한도 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-219">It also looks for hello keys toovalidate hello JSON web tokens.</span></span>

<span data-ttu-id="6ab32-220">`audience`: hello 호출 응용 프로그램을 식별 하는 hello 포털에서 (URI) uniform resource identifier입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-220">`audience`: hello uniform resource identifier (URI) from hello portal that identifies your calling application.</span></span>

<span data-ttu-id="6ab32-221">`tenantName`: 해당 테넌트 이름입니다(예: **contoso.onmicrosoft.com**).</span><span class="sxs-lookup"><span data-stu-id="6ab32-221">`tenantName`: Your tenant name (for example, **contoso.onmicrosoft.com**).</span></span>

<span data-ttu-id="6ab32-222">`policyName`: hello tooyour 서버에서 들어오는 toovalidate hello 토큰을 원하는 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-222">`policyName`: hello policy that you want toovalidate hello tokens coming in tooyour server.</span></span> <span data-ttu-id="6ab32-223">이 정책은 되어야 로그인에 대 한 hello 클라이언트 응용 프로그램에서 사용 하는 동일한 정책을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-223">This policy should be hello same policy that you use on hello client application for sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="6ab32-224">지금은 사용 하 여 동일한 hello 정책을 통해 클라이언트와 서버 모두 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-224">For now, use hello same policies across both client and server setup.</span></span> <span data-ttu-id="6ab32-225">이미는 연습을 완료 하 고 이러한 정책을 만들고, 필요가 없으면 toodo 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-225">If you have already completed a walk-through and created these policies, you don't need toodo so again.</span></span> <span data-ttu-id="6ab32-226">Hello 연습을 완료 하기 때문에 필요는 없습니다 새 정책 tooset hello 사이트에서 클라이언트 연습에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-226">Because you completed hello walk-through, you shouldn't need tooset up new policies for client walk-throughs on hello site.</span></span>
>
>

## <a name="add-configuration-tooyour-serverjs-file"></a><span data-ttu-id="6ab32-227">구성 tooyour server.js 파일 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-227">Add configuration tooyour server.js file</span></span>
<span data-ttu-id="6ab32-228">hello tooread hello 값 `config.js` 사용자가 만든 파일에서 추가 hello `.config` 응용 프로그램에 필요한 리소스로 파일을 다음 hello 전역 변수 toothose hello 설정 `config.js` 문서.</span><span class="sxs-lookup"><span data-stu-id="6ab32-228">tooread hello values from hello `config.js` file you created, add hello `.config` file as a required resource in your application, and then set hello global variables toothose in hello `config.js` document.</span></span>

<span data-ttu-id="6ab32-229">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-229">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-230">열기 hello `server.js` 편집기에서에서 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-230">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6ab32-231">Hello 다음 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-231">Add hello following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="6ab32-232">너무 새 섹션 추가`server.js` hello 코드 다음에 포함 된:</span><span class="sxs-lookup"><span data-stu-id="6ab32-232">Add a new section too`server.js` that includes hello following code:</span></span>

```Javascript
// We pass these options in toohello ODICBearerStrategy.

var options = {
    // hello URL of hello metadata document for your app. We put hello keys for token validation from hello URL found in hello jwks_uri tag of hello in hello metadata.
    identityMetadata: config.creds.identityMetadata,
    clientID: config.creds.clientID,
    tenantName: config.creds.tenantName,
    policyName: config.creds.policyName,
    validateIssuer: config.creds.validateIssuer,
    audience: config.creds.audience,
    passReqToCallback: config.creds.passReqToCallback

};
```

<span data-ttu-id="6ab32-233">다음으로,이 호출 응용 프로그램에서 수신 하는 hello 사용자에 대 한 몇 가지 자리 표시자를 추가 해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-233">Next, let's add some placeholders for hello users we receive from our calling applications.</span></span>

```Javascript
// array toohold logged in users and hello current logged in user (owner)
var users = [];
var owner = null;
```

<span data-ttu-id="6ab32-234">계속해서 로거를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-234">Let's go ahead and create our logger too.</span></span>

```Javascript
// Our logger
var log = bunyan.createLogger({
    name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="add-hello-mongodb-model-and-schema-information-by-using-mongoose"></a><span data-ttu-id="6ab32-235">Mongoose를 사용 하 여 hello MongoDB 모델 및 스키마 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-235">Add hello MongoDB model and schema information by using Mongoose</span></span>
<span data-ttu-id="6ab32-236">hello 이전 준비 성과가 REST API 서비스에서 함께이 세 파일 bring 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-236">hello earlier preparation pays off as you bring these three files together in a REST API service.</span></span>

<span data-ttu-id="6ab32-237">이 연습에 대 한 사용 하 여 MongoDB toostore 작업 이전에 설명한 대로.</span><span class="sxs-lookup"><span data-stu-id="6ab32-237">For this walk-through, use MongoDB toostore your tasks, as discussed earlier.</span></span>

<span data-ttu-id="6ab32-238">Hello에 `config.js` 데이터베이스 라는 파일을 **tasklist \ / s**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-238">In hello `config.js` file, you called your database **tasklist**.</span></span> <span data-ttu-id="6ab32-239">해당 이름의 hello의 hello 끝에 두면 서버가 이기도 `mongoose_auth_local` 연결 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-239">That name was also what you put at hello end of hello `mongoose_auth_local` connection URL.</span></span> <span data-ttu-id="6ab32-240">이 데이터베이스 MongoDB에 미리 toocreate 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-240">You don't need toocreate this database beforehand in MongoDB.</span></span> <span data-ttu-id="6ab32-241">사용자에 대 한 hello 서버 응용 프로그램의 첫 번째 실행 시 hello 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-241">It creates hello database for you on hello first run of your server application.</span></span>

<span data-ttu-id="6ab32-242">MongoDB 데이터베이스 toouse는 hello 서버 이야기, 후 해야 toowrite 몇 가지 추가 코드 toocreate hello 모델 및 스키마 서버 작업에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-242">After you tell hello server which MongoDB database toouse, you need toowrite some additional code toocreate hello model and schema for your server tasks.</span></span>

### <a name="expand-hello-model"></a><span data-ttu-id="6ab32-243">Hello 모델 확장</span><span class="sxs-lookup"><span data-stu-id="6ab32-243">Expand hello model</span></span>
<span data-ttu-id="6ab32-244">이 스키마 모델은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-244">This schema model is simple.</span></span> <span data-ttu-id="6ab32-245">필요에 따라 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-245">You can expand it as required.</span></span>

<span data-ttu-id="6ab32-246">`owner`: 누가 toohello 작업을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-246">`owner`: Who is assigned toohello task.</span></span> <span data-ttu-id="6ab32-247">이 개체는 **문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-247">This object is a **string**.</span></span>  

<span data-ttu-id="6ab32-248">`Text`: hello 작업 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-248">`Text`: hello task itself.</span></span> <span data-ttu-id="6ab32-249">이 개체는 **문자열**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-249">This object is a **string**.</span></span>

<span data-ttu-id="6ab32-250">`date`: hello 날짜 hello 작업으로 인 한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-250">`date`: hello date that hello task is due.</span></span> <span data-ttu-id="6ab32-251">이 개체는 **날짜/시간**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-251">This object is a **datetime**.</span></span>

<span data-ttu-id="6ab32-252">`completed`: 경우 hello 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-252">`completed`: If hello task is complete.</span></span> <span data-ttu-id="6ab32-253">이 개체는 **부울**입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-253">This object is a **Boolean**.</span></span>

### <a name="create-hello-schema-in-hello-code"></a><span data-ttu-id="6ab32-254">Hello 코드에서 hello 스키마 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-254">Create hello schema in hello code</span></span>
<span data-ttu-id="6ab32-255">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-255">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-256">열기 hello `server.js` 편집기에서에서 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-256">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6ab32-257">Hello 다음 hello 구성 항목 아래에 정보를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-257">Add hello following information below hello configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 3000; // Note we are hosting our API on port 3000
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;

// Connect tooMongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');

// Here we create a schema toostore our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
    owner: String,
    Text: String,
    completed: Boolean,
    date: Date
});

// Use hello schema tooregister a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="6ab32-258">Hello 스키마를 처음 만들면 및 toostore hello 전체에서 데이터를 정의할 때 코드를 사용 하는 모델 개체를 만든 다음 프로그램 **경로**합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-258">You first create hello schema, and then you create a model object that you use toostore your data throughout hello code when you define your **routes**.</span></span>

## <a name="add-routes-for-your-rest-api-task-server"></a><span data-ttu-id="6ab32-259">REST API 작업 서버에 대한 경로 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-259">Add routes for your REST API task server</span></span>
<span data-ttu-id="6ab32-260">와 데이터베이스 모델 toowork를가지고 REST API 서버에 사용 하는 hello 경로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-260">Now that you have a database model toowork with, add hello routes you use for your REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="6ab32-261">Restify의 경로 정보</span><span class="sxs-lookup"><span data-stu-id="6ab32-261">About routes in Restify</span></span>
<span data-ttu-id="6ab32-262">경로 동일 하 게 작동 Restify에서 hello에 hello Express 스택을 사용할 때 작업 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-262">Routes work in Restify in hello same way that they work when they use hello Express stack.</span></span> <span data-ttu-id="6ab32-263">Hello hello 클라이언트 응용 프로그램 toocall 예상 되는 URI를 사용 하 여 경로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-263">You define routes by using hello URI that you expect hello client applications toocall.</span></span>

<span data-ttu-id="6ab32-264">Restify 경로의 일반적인 패턴:</span><span class="sxs-lookup"><span data-stu-id="6ab32-264">A typical pattern for a Restify route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep hello server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```

<span data-ttu-id="6ab32-265">Resitfy 및 Express는 응용 프로그램 유형 정의 및 여러 다른 끝점에서 복잡한 라우팅 수행 등의 훨씬 더 수준 높은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-265">Restify and Express can provide much deeper functionality, such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="6ab32-266">Hello 목적으로이 자습서에서는 이러한 경로 단순하게 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-266">For hello purposes of this tutorial, we keep these routes simple.</span></span>

#### <a name="add-default-routes-tooyour-server"></a><span data-ttu-id="6ab32-267">기본 경로 tooyour 서버 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-267">Add default routes tooyour server</span></span>
<span data-ttu-id="6ab32-268">이제의 hello 기본 CRUD 경로 추가할 **만들** 및 **목록** REST API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-268">You now add hello basic CRUD routes of **create** and **list** for our REST API.</span></span> <span data-ttu-id="6ab32-269">Hello에 다른 경로 찾을 수 `complete` hello 샘플의 분기 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-269">Other routes can be found in hello `complete` branch of hello sample.</span></span>

<span data-ttu-id="6ab32-270">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-270">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

<span data-ttu-id="6ab32-271">열기 hello `server.js` 편집기에서에서 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-271">Open hello `server.js` file in an editor.</span></span> <span data-ttu-id="6ab32-272">Hello 데이터베이스 항목 아래 위에 hello 다음 정보를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-272">Below hello database entries you made above add hello following information:</span></span>

```Javascript
/**
 *
 * APIs for our REST Task server
 */

// Create a task

function createTask(req, res, next) {

    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

    res.header("Access-Control-Allow-Origin", "*");
    res.header("Access-Control-Allow-Headers", "X-Requested-With");

    // Create a new task model, fill it up and save it tooMongodb
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
            req.log.warn(err, 'createTask: unable toosave');
            next(err);
        } else {
            res.send(201, _task);

        }
    });

    return next();

}
```

```Javascript
/// Simple returns hello list of TODOs that were loaded.

function listTasks(req, res, next) {
    // Resitify currently has a bug which doesn't allow you tooset default headers
    // This headers comply with CORS and allow us toomongodbServer our response tooany origin

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
            log.warn(err, "There is no tasks in hello database. Add one!");
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


#### <a name="add-error-handling-for-hello-routes"></a><span data-ttu-id="6ab32-273">오류 hello 경로 대 한 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-273">Add error handling for hello routes</span></span>
<span data-ttu-id="6ab32-274">뒤로 toohello 클라이언트 이해할 수 있는 방식으로 발생 한 모든 문제를 통신할 수 있도록 몇 가지 오류 처리를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-274">Add some error handling so that you can communicate any problems you encounter back toohello client in a way that it can understand.</span></span>

<span data-ttu-id="6ab32-275">Hello 코드 다음을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-275">Add hello following code:</span></span>

```Javascript
///--- Errors for communicating something interesting back toohello client
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


## <a name="create-your-server"></a><span data-ttu-id="6ab32-276">서버 만들기</span><span class="sxs-lookup"><span data-stu-id="6ab32-276">Create your server</span></span>
<span data-ttu-id="6ab32-277">이제 데이터베이스를 정의하고 경로를 적용했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-277">You have now defined your database and put your routes in place.</span></span> <span data-ttu-id="6ab32-278">hello toodo 있습니다에 대 한 마지막 항목은 통화를 관리 하는 tooadd hello 서버 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-278">hello last thing for you toodo is tooadd hello server instance that manages your calls.</span></span>

<span data-ttu-id="6ab32-279">Restify 및 Express REST API 서버에 대 한 세부적으로 사용자 지정을 제공 하지만 여기 hello 가장 기본적인 설치 프로그램에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-279">Restify and Express provide deep customization for a REST API server, but we use hello most basic setup here.</span></span>

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

// Allow 5 requests/second by IP, and burst too10
server.use(restify.throttle({
    burst: 10,
    rate: 5,
    ip: true,
}));

// Use hello common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
    mapParams: true
})); // Allows for JSON mapping tooREST
server.use(restify.authorizationParser()); // Looks for authorization headers

// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support


```
## <a name="add-hello-routes-toohello-server-without-authentication"></a><span data-ttu-id="6ab32-280">인증) (없이 hello 경로 toohello 서버 추가</span><span class="sxs-lookup"><span data-stu-id="6ab32-280">Add hello routes toohello server (without authentication)</span></span>
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
    consoleMessage += '\n Open your browser too%s/api/tasks\n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
    consoleMessage += '\n !!! why not try a $curl -isS %s | json tooget some ideas? \n';
    consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';

    //log.info(consoleMessage, server.name, server.url, server.url, server.url);

});

```

## <a name="add-authentication-tooyour-rest-api-server"></a><span data-ttu-id="6ab32-281">인증 tooyour REST API 서버를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-281">Add authentication tooyour REST API server</span></span>
<span data-ttu-id="6ab32-282">이제 실행 중인 REST API 서버가 있고 Azure AD에 대해 유용하게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-282">Now that you have a running REST API server, you can make it useful against Azure AD.</span></span>

<span data-ttu-id="6ab32-283">Hello 명령줄에서 디렉터리를 너무 변경`azuread`아직 없는 경우:</span><span class="sxs-lookup"><span data-stu-id="6ab32-283">From hello command line, change your directory too`azuread`, if it's not already there:</span></span>

`cd azuread`

### <a name="use-hello-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="6ab32-284">Passport azure ad에 포함 되어 있는 OIDCBearerStrategy hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="6ab32-284">Use hello OIDCBearerStrategy that is included with passport-azure-ad</span></span>
> [!TIP]
> <span data-ttu-id="6ab32-285">작성 하는 경우, Api hello 데이터 toosomething 사용자 hello hello 토큰에서 고유한 연결 항상 해야 스푸핑할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-285">When you write APIs, you should always link hello data toosomething unique from hello token that hello user can’t spoof.</span></span> <span data-ttu-id="6ab32-286">Hello 서버는 할 일 항목을 저장 하는 경우 수행 hello 바탕 **oid** hello "소유자" 필드에서 이동 하 hello 토큰 (token.oid 통해 라고 함)에서 hello 사용자의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-286">When hello server stores ToDo items, it does so based on hello **oid** of hello user in hello token (called through token.oid), which goes in hello “owner” field.</span></span> <span data-ttu-id="6ab32-287">이 값은 해당 사용자만 자신의 할 일 항목에 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-287">This value ensures that only that user can access their own ToDo items.</span></span> <span data-ttu-id="6ab32-288">가 없는 노출 "소유자"의 hello API에에서 인증 된 경우에 외부 사용자가 다른 사용자의 할 일 항목을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-288">There is no exposure in hello API of “owner,” so an external user can request others’ ToDo items even if they are authenticated.</span></span>
>
>

<span data-ttu-id="6ab32-289">를 사용 하 여 함께 제공 된 hello 전달자 전략 `passport-azure-ad`합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-289">Next, use hello bearer strategy that comes with `passport-azure-ad`.</span></span>

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
        log.info('verifying hello user');
        log.info(token, 'was hello token retreived');
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

<span data-ttu-id="6ab32-290">Passport는 모든 전략에 대 한 hello 같은 패턴을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-290">Passport uses hello same pattern for all its strategies.</span></span> <span data-ttu-id="6ab32-291">사용자는 이를 `token` 및 `done`을 매개 변수로 포함하는 `function()`에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-291">You pass it a `function()` that has `token` and `done` as parameters.</span></span> <span data-ttu-id="6ab32-292">hello 전략의 작업을 모두 수행한 후 tooyou 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-292">hello strategy comes back tooyou after it has done all of its work.</span></span> <span data-ttu-id="6ab32-293">그런 다음 저장 hello 사용자를 저장 한 hello 토큰에 대 한 tooask 다시 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-293">You should then store hello user and save hello token so that you don’t need tooask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ab32-294">위의 hello 코드는 모든 사용자에 게 tooauthenticate tooyour 서버 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-294">hello code above takes any user who happens tooauthenticate tooyour server.</span></span> <span data-ttu-id="6ab32-295">이 프로세스를 자동 등록이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-295">This process is known as autoregistration.</span></span> <span data-ttu-id="6ab32-296">프로덕션 서버에서 주저 하지 마시기 바랍니다 모든 사용자가 액세스 hello API에 먼저 않고도 등록 프로세스를 통해 하죠.</span><span class="sxs-lookup"><span data-stu-id="6ab32-296">In production servers, don't let in any users access hello API without first having them go through a registration process.</span></span> <span data-ttu-id="6ab32-297">이 프로세스는 일반적으로 Facebook을 사용 하 여 tooregister를 허용 하지만 다음 toofill 추가 정보를 요청 하는 소비자 앱에서 참조 하는 hello 패턴.</span><span class="sxs-lookup"><span data-stu-id="6ab32-297">This process is usually hello pattern you see in consumer apps that allow you tooregister by using Facebook but then ask you toofill out additional information.</span></span> <span data-ttu-id="6ab32-298">이 프로그램을 명령줄 프로그램을 없으면 우리 hello 토큰 개체를 반환 하 고 다음 사용자가 toofill 추가 정보를 요청 하는에서 hello 전자 메일을 추출 하 고 있을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-298">If this program wasn’t a command-line program, we could have extracted hello email from hello token object that is returned and then asked users toofill out additional information.</span></span> <span data-ttu-id="6ab32-299">샘플 이기 때문에 여기서 추가할 tooan 메모리 내 데이터베이스.</span><span class="sxs-lookup"><span data-stu-id="6ab32-299">Because this is a sample, we add them tooan in-memory database.</span></span>
>
>

## <a name="run-your-server-application-tooverify-that-it-rejects-you"></a><span data-ttu-id="6ab32-300">서버 응용 프로그램 tooverify 실행을 거부 하면</span><span class="sxs-lookup"><span data-stu-id="6ab32-300">Run your server application tooverify that it rejects you</span></span>
<span data-ttu-id="6ab32-301">사용할 수 있습니다 `curl` toosee 이제 끝점에 대 한 OAuth2 보호를 포함 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6ab32-301">You can use `curl` toosee if you now have OAuth2 protection against your endpoints.</span></span> <span data-ttu-id="6ab32-302">hello 헤더가 반환 되어야 충분 한 tootell hello 오른쪽 경로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-302">hello headers returned should be enough tootell you that you are on hello right path.</span></span>

<span data-ttu-id="6ab32-303">MongoDB 인스턴스가 실행되고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-303">Make sure that your MongoDB instance is running:</span></span>

    $sudo mongodb

<span data-ttu-id="6ab32-304">Toohello 디렉터리 및 실행된 hello 서버를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-304">Change toohello directory and run hello server:</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="6ab32-305">새 터미널 창에서 `curl`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-305">In a new terminal window, run `curl`</span></span>

<span data-ttu-id="6ab32-306">기본 POST를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-306">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:3000/api/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="6ab32-307">401 오류는 원하는 hello 응답입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-307">A 401 error is hello response you want.</span></span> <span data-ttu-id="6ab32-308">해당 hello Passport 레이어에서 tooredirect 시도 나타냅니다 toohello 권한 부여 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-308">It indicates that hello Passport layer is trying tooredirect toohello authorize endpoint.</span></span>

## <a name="you-now-have-a-rest-api-service-that-uses-oauth2"></a><span data-ttu-id="6ab32-309">이제 OAuth2를 사용하는 REST API 서비스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-309">You now have a REST API service that uses OAuth2</span></span>
<span data-ttu-id="6ab32-310">Restify 및 OAuth를 사용하여 REST API를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-310">You have implemented a REST API by using Restify and OAuth!</span></span> <span data-ttu-id="6ab32-311">이제 toodevelop 서비스를 계속 하 고이 예제에서 빌드할 수 있도록 충분 한 코드가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-311">You now have sufficient code so that you can continue toodevelop your service and build on this example.</span></span> <span data-ttu-id="6ab32-312">OAuth2 호환 클라이언트를 사용하지 않고 이 서버로 수행할 수 있는 작업은 모두 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-312">You have gone as far as you can with this server without using an OAuth2-compatible client.</span></span> <span data-ttu-id="6ab32-313">그 다음 단계에 대 한 같은 추가 단계를 사용 하 여 우리의 [tooa 웹 API B2C 함께 iOS를 사용 하 여 연결](active-directory-b2c-devquickstarts-ios.md) 연습 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-313">For that next step use an additional walk-through like our [Connect tooa web API by using iOS with B2C](active-directory-b2c-devquickstarts-ios.md) walkthrough.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ab32-314">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ab32-314">Next steps</span></span>
<span data-ttu-id="6ab32-315">이제와 같은 고급 toomore 항목을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ab32-315">You can now move toomore advanced topics, such as:</span></span>

[<span data-ttu-id="6ab32-316">웹 API tooa B2C 함께 iOS를 사용 하 여 연결</span><span class="sxs-lookup"><span data-stu-id="6ab32-316">Connect tooa web API by using iOS with B2C</span></span>](active-directory-b2c-devquickstarts-ios.md)
