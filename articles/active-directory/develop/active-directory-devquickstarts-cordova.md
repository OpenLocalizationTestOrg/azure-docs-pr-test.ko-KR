---
title: "aaaAzure AD Cordova 시작 | Microsoft Docs"
description: "Toobuild Cordova 응용 프로그램 하는 로그인에 대 한 Azure AD와 통합 되어 방법과 OAuth를 사용 하 여 Azure AD로 보호 된 Api를 호출 합니다."
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="49a9e-103">Azure AD를 Apache Cordova 앱에 통합</span><span class="sxs-lookup"><span data-stu-id="49a9e-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="49a9e-104">완전 한 네이티브 응용 프로그램으로 모바일 장치에서 실행할 수 있는 Apache Cordova toodevelop HTML5/JavaScript 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="49a9e-105">Azure Active Directory (Azure AD)와 기업 간 인증 기능 tooyour Cordova 응용 프로그램을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="49a9e-106">Cordova 플러그 인은 iOS, Android, Windows 스토어 및 Windows Phone에서 Azure AD 네이티브 SDK를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="49a9e-107">플러그 인을 향상 시킬 수 있습니다 응용 프로그램을 사용 하 여 사용자의 Windows Server Active Directory 계정, 이득 액세스 tooOffice 365 및 Azure Api를 사용 하 여 로그인 하 고 심지어 toosupport 호출 tooyour 고유의 사용자 지정 웹 API를 보호할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="49a9e-108">이 자습서에서는 Apache Cordova 플러그 인 hello Active Directory 인증 라이브러리 (ADAL) tooimprove 간단한 응용 프로그램에 대 한 hello 같은 기능을 추가 하 여:</span><span class="sxs-lookup"><span data-stu-id="49a9e-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="49a9e-109">단 몇 줄의 코드로, 사용자를 인증하고 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="49a9e-110">해당 토큰 tooinvoke hello Graph API tooquery 해당 디렉터리를 사용 하 고 hello 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="49a9e-111">Hello ADAL 토큰 캐시 toominimize 인증 사용 hello 사용자에 게 묻습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="49a9e-112">toomake를 해야 이러한 향상 된 기능:</span><span class="sxs-lookup"><span data-stu-id="49a9e-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="49a9e-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="49a9e-114">코드 tooyour 앱 toorequest 토큰을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="49a9e-115">Hello Graph API를 쿼리 하기 위한 코드 toouse hello 토큰을 추가 하 고 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="49a9e-116">Hello Cordova 배포 프로젝트 만들기 모든 hello 플랫폼과 tootarget, 추가 hello Cordova ADAL 플러그 인을 에뮬레이터의 hello 솔루션을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49a9e-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="49a9e-117">Prerequisites</span></span>
<span data-ttu-id="49a9e-118">toocomplete 해야이 자습서에서는:</span><span class="sxs-lookup"><span data-stu-id="49a9e-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="49a9e-119">앱 개발 권한이 있는 계정이 있는 Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="49a9e-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="49a9e-120">가 toouse Apache Cordova를 구성 하는 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="49a9e-121">둘 다 이미 있는 경우 설정, 직접 toostep 1 계속 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="49a9e-122">Azure AD 테 넌 트를 설정 하지 않은 경우 사용 하 여 hello [방법은 하나 tooget](active-directory-howto-tenant.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="49a9e-123">사용자 컴퓨터에 설치 하는 Apache Cordova를 설정 하지 않은 경우에 hello 다음을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="49a9e-124">Git</span><span class="sxs-lookup"><span data-stu-id="49a9e-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="49a9e-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="49a9e-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="49a9e-126">[Cordova CLI](https://cordova.apache.org/)(`npm install -g cordova` NPM 패키지 관리자를 통해 쉽게 설치 가능)</span><span class="sxs-lookup"><span data-stu-id="49a9e-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="49a9e-127">앞에 설치 하는 hello Mac. hello 및 hello PC에서 모두 작동 해야</span><span class="sxs-lookup"><span data-stu-id="49a9e-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="49a9e-128">대상 플랫폼마다 필수 구성 요소가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="49a9e-129">toobuild 및 Windows 태블릿/PC 또는 Windows Phone 앱 실행:</span><span class="sxs-lookup"><span data-stu-id="49a9e-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="49a9e-130">[Windows용 Visual Studio 2013 업데이트 2 이상](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8)(Express 또는 다른 버전) 또는 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="49a9e-131">toobuild 및 iOS 용 앱 실행:</span><span class="sxs-lookup"><span data-stu-id="49a9e-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="49a9e-132">Xcode 6.x 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="49a9e-133">Hello에서 다운로드 [Apple 개발자 사이트](http://developer.apple.com/downloads) 또는 hello [Mac 앱 스토어](http://itunes.apple.com/us/app/xcode/id497799835?mt=12)합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="49a9e-134">[ios-sim](https://www.npmjs.org/package/ios-sim)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="49a9e-135">사용할 수 있습니다 toostart iOS 앱 hello 명령줄에서 ios 시뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="49a9e-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="49a9e-136">(Hello 터미널을 통해 쉽게 설치할 수 있습니다: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="49a9e-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="49a9e-137">toobuild 및 Android 용 앱 실행:</span><span class="sxs-lookup"><span data-stu-id="49a9e-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="49a9e-138">[JDK(Java Development Kit) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="49a9e-139">확인 `JAVA_HOME` toohello JDK 설치 경로 (예를 들어 C:\Program Files\Java\jdk1.7.0_75)에 따라 (환경 변수) 올바르게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="49a9e-140">설치 [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) hello 추가 `<android-sdk-location>\tools` 위치 (예를 들어 C:\tools\Android\android-sdk\tools) tooyour `PATH` 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="49a9e-141">Android SDK Manager를 엽니다 (예를 들어 hello 터미널을 통해: `android`) 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="49a9e-142">*Android 5.0.1(API 21)* 플랫폼 SDK</span><span class="sxs-lookup"><span data-stu-id="49a9e-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="49a9e-143">*Android SDK 빌드 도구* 버전 19.1.0 이상</span><span class="sxs-lookup"><span data-stu-id="49a9e-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="49a9e-144">*Android 지원 리포지토리* (기타)</span><span class="sxs-lookup"><span data-stu-id="49a9e-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="49a9e-145">hello Android SDK는 모든 기본 에뮬레이터 인스턴스를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="49a9e-146">실행 하 여 만드세요 `android avd` 터미널 hello 및 다음을 선택 하 **만들기**toorun 에뮬레이터의 hello Android 앱을 사용 하려는 경우.</span><span class="sxs-lookup"><span data-stu-id="49a9e-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="49a9e-147">API 수준 19 이상을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="49a9e-148">Hello Android 에뮬레이터 및 만들기 옵션에 대 한 자세한 내용은 참조 [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) hello Android 사이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="49a9e-149">1단계: Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="49a9e-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="49a9e-150">이 단계는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-150">This step is optional.</span></span> <span data-ttu-id="49a9e-151">이 자습서 toosee를 사용할 수 있는 미리 프로 비전된 값 자신의 테 넌 트의 모든 프로 비전을 수행 하지 않고도 작업에 대 한 샘플 hello를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="49a9e-152">그러나이 단계를 수행 하 고 될 수 있으므로 필요한 응용 프로그램을 만들 때 hello 프로세스에 잘 수행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="49a9e-153">Azure AD 응용 프로그램을 알려진 토큰 tooonly를 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="49a9e-154">Azure AD에서 앱을 사용 하려면 먼저 toocreate 항목에 대 한 테 넌 트에 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="49a9e-155">tooregister 테 넌 트에 새 응용 프로그램:</span><span class="sxs-lookup"><span data-stu-id="49a9e-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="49a9e-156">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="49a9e-157">Hello 위쪽 막대에서 계정을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-157">On hello top bar, click your account.</span></span> <span data-ttu-id="49a9e-158">Hello에 **디렉터리** 목록 tooregister 원하는 hello Azure AD 테 넌 트 응용 프로그램을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="49a9e-159">클릭 **더 서비스** 에 hello 왼쪽된 창에서 선택한 후 **Azure Active Directory**합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="49a9e-160">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="49a9e-161">만들고 hello 지시에 따라 한 **네이티브 클라이언트 응용 프로그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="49a9e-162">(Cordova 앱이 HTML 기반이기는 하지만 여기서는 네이티브 클라이언트 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="49a9e-163">hello **네이티브 클라이언트 응용 프로그램** 옵션을 선택 해야 합니다 또는 hello 응용 프로그램에서 작동 하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="49a9e-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="49a9e-164">**이름** 응용 프로그램 toousers에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="49a9e-165">**리디렉션 URI** 는 hello tooreturn 토큰 tooyour 응용 프로그램을 사용 하는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="49a9e-166">**http://MyDirectorySearcherApp**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="49a9e-167">등록을 완료 한 후 Azure AD는 고유한 응용 프로그램 ID tooyour 응용 프로그램에 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="49a9e-168">Hello 다음 섹션의이 값이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="49a9e-169">응용 프로그램을 새로 만든 hello hello 응용 프로그램 탭에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="49a9e-170">toorun `DirSearchClient Sample`, hello 새로 만든 응용 프로그램 권한 tooquery hello Azure AD Graph API 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="49a9e-171">Hello에서 **설정** 페이지에서 **필요한 권한**를 선택한 후 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="49a9e-172">Hello Azure Active Directory 응용 프로그램에 대 한 선택 **Microsoft Graph** 으로 hello를 더하고 API hello **hello 로그인 한 사용자로 디렉터리에 액세스 hello** 에 따른 권한 **위임 된 사용 권한**합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="49a9e-173">이 통해 사용자에 대 한 프로그램 응용 프로그램 tooquery hello Graph API.</span><span class="sxs-lookup"><span data-stu-id="49a9e-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="49a9e-174">2 단계: hello 샘플 앱 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="49a9e-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="49a9e-175">셸 또는 명령줄에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="49a9e-176">3 단계: hello Cordova 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="49a9e-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="49a9e-177">여러 가지 방법 toocreate Cordova 응용 프로그램이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="49a9e-178">이 자습서에서는 hello Cordova CLI (명령줄 인터페이스)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="49a9e-179">셸 또는 명령줄에서 다음 명령을 hello를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="49a9e-180">해당 명령은 hello 폴더 구조 및 hello Cordova 프로젝트에 대 한 스 캐 폴딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="49a9e-181">Toohello 새 DirSearchClient 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="49a9e-182">파일 관리자 또는 hello 다음 셸에서에서 명령을 사용 하 여 hello www 하위 폴더에 hello 시작 프로젝트의 hello 콘텐츠를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="49a9e-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="49a9e-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="49a9e-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="49a9e-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="49a9e-185">Hello 허용 목록 플러그 인을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="49a9e-186">이 hello Graph API를 호출 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="49a9e-187">Toosupport 원하는 모든 hello 플랫폼을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="49a9e-188">작업 예제 toohave hello 명령 뒤의 tooexecute 하나 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="49a9e-189">참고 수 windows 수 tooemulate iOS 또는 mac에서 Windows를 에뮬레이트하 없습니다</span><span class="sxs-lookup"><span data-stu-id="49a9e-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="49a9e-190">Cordova 플러그 인 tooyour 프로젝트에 대 한 ADAL hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="49a9e-191">4 단계: 코드 tooauthenticate 사용자를 추가 하 고 Azure AD에서 토큰을 얻어</span><span class="sxs-lookup"><span data-stu-id="49a9e-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="49a9e-192">이 자습서에서 개발 중인 응용 프로그램으로 hello 간단한 디렉터리 검색 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="49a9e-193">hello 사용자 수 하 한 다음, hello 디렉터리에 있는 모든 사용자의 hello 별칭을 입력 하 고, 몇 가지 기본 특성을 시각화 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="49a9e-194">(에 www/index.html) hello 응용 프로그램의 hello 기본 사용자 인터페이스의 hello 정의 포함 하는 hello 시작 프로젝트 및 기본 응용 프로그램 이벤트를 연결 하는 hello 스 캐 폴딩 주기, 사용자 인터페이스 바인딩 (www/js/index.js)에서 디스플레이 논리 조정은 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="49a9e-195">hello 유일한 작업 엔은 identity 작업을 구현 하는 tooadd hello 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="49a9e-196">hello 먼저 toodo 코드에서 필요한 것은 Azure AD 앱을 식별 하는 데 사용 하는 hello 프로토콜 값을 소개 하며 hello 리소스 대상</span><span class="sxs-lookup"><span data-stu-id="49a9e-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="49a9e-197">이러한 값에는 나중에 사용 되는 tooconstruct hello 토큰 요청 게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="49a9e-198">Hello 다음 hello 위쪽 hello index.js 파일의 코드 조각 삽입:</span><span class="sxs-lookup"><span data-stu-id="49a9e-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="49a9e-199">hello `redirectUri` 및 `clientId` 값에는 Azure AD에서 앱을 설명 하는 hello 값과 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="49a9e-200">Hello에서 찾을 수 있습니다 **구성** 이 자습서의 앞부분에 나오는 1 단계에 설명 된 대로 hello Azure 포털을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="49a9e-201">하지 자신의 테 넌 트에 새 앱을 등록 하기 위한를 선택한 경우 hello 미리 구성 된 값은 단순히 붙여넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="49a9e-202">그런 다음 프로덕션 환경에는 앱에 대 한 항목을 직접를 항상 만들어야 하지만 hello 샘플 실행을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="49a9e-203">다음으로 hello 토큰 요청 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-203">Next, add hello token request code.</span></span> <span data-ttu-id="49a9e-204">코드 조각 hello 사이 다음 hello 삽입 `search` 및 `renderData` 정의:</span><span class="sxs-lookup"><span data-stu-id="49a9e-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="49a9e-205">두 주요 부분에서 분석하여 해당 함수를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="49a9e-206">이 샘플 디자인 된 toowork 모든 테 넌 트와는 달리 toobeing 연결 tooa 특정 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="49a9e-207">Hello를 사용 하 여 인증 시에 계정이 hello 사용자 tooenter 수 있도록 하 고 속하는 hello 요청 toohello 테 넌 트를 안내 하는 "/ 일반적인" 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="49a9e-208">이 첫 번째 부분에서는 hello 메서드 토큰이 이미 저장 되어 있는 경우 hello ADAL 캐시 toosee를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="49a9e-209">이 경우 hello 메서드가 hello 테 넌 트 hello 토큰에서 ADAL을 다시 초기화 하기 위한 있었던 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="49a9e-210">이 이므로 필요한 tooavoid 추가 프롬프트 hello 사용 "/ 일반적인"의 hello 사용자 tooenter 새 계정을 묻는에 항상 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="49a9e-211">hello 메서드의 두 번째 부분은 hello hello 적절 한 토큰 요청을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="49a9e-212">hello `acquireTokenSilentAsync` 메서드 요청 ADAL tooreturn 토큰을 지정 하는 hello에 대 한 모든 사용자 환경 표시 하지 않고 리소스</span><span class="sxs-lookup"><span data-stu-id="49a9e-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="49a9e-213">Hello 캐시에 저장 하 고, 적합 한 액세스 토큰을 이미 있는 경우에 발생할 수 있습니다 새로 고침 토큰 수 있는지 또는 모든 프롬프트를 표시 하지 않고 tooget 새 액세스 토큰을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="49a9e-214">이 시도가 실패 하면, 우리에서 대체 `acquireTokenAsync`-hello 사용자 tooauthenticate 물어봅니다 시각적으로 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="49a9e-215">이제 hello 토큰 했으므로 म 수 마지막 hello Graph API 호출과 원하는 hello 검색 쿼리를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="49a9e-216">Hello 다음 hello 아래 코드 조각 삽입 `authenticate` 정의:</span><span class="sxs-lookup"><span data-stu-id="49a9e-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="49a9e-217">텍스트 상자에 사용자의 별칭을 입력 하기 위한 간단한 UX를 제공 하는 hello 시작점 파일.</span><span class="sxs-lookup"><span data-stu-id="49a9e-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="49a9e-218">이 메서드를 사용 하 고 그 값 tooconstruct 쿼리, hello 액세스 토큰으로 결합, tooMicrosoft 그래프를 보낼 hello 결과 구문 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="49a9e-219">hello `renderData` hello 결과 시각화 하는 hello 시작점 파일에 이미 있는 메서드를 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="49a9e-220">5 단계: hello 앱 실행</span><span class="sxs-lookup"><span data-stu-id="49a9e-220">Step 5: Run hello app</span></span>
<span data-ttu-id="49a9e-221">응용 프로그램에 마지막으로 준비 toorun입니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="49a9e-222">작동 하는 것은 간단: hello 앱이 시작 되 면, toolook 원하는 hello 사용자의 hello 별칭을 입력 하 고 hello 단추를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="49a9e-223">인증을 위한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-223">You're prompted for authentication.</span></span> <span data-ttu-id="49a9e-224">성공적으로 인증 및 검색 시 검색 hello 사용자의 hello 특성이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="49a9e-225">후속 실행 모든 프롬프트를 표시 하지 않고 hello 검색을 수행 합니다 이면 고마워요 hello toohello 있으면 이전에 캐시에서 토큰.</span><span class="sxs-lookup"><span data-stu-id="49a9e-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="49a9e-226">hello 앱을 실행 하기 위한 구체적인 단계 hello 플랫폼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="49a9e-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="49a9e-227">Windows 10</span></span>
   <span data-ttu-id="49a9e-228">태블릿/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="49a9e-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="49a9e-229">모바일 (Windows 10 Mobile 장치 연결 tooa PC 필요):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="49a9e-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="49a9e-230">먼저 실행 하 여 hello, 하는 동안 메시지가 나타날 수 있습니다에 toosign 개발자 라이선스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="49a9e-231">자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49a9e-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="49a9e-232">Windows 8.1 태블릿/PC</span><span class="sxs-lookup"><span data-stu-id="49a9e-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="49a9e-233">먼저 실행 하 여 hello, 하는 동안 메시지가 나타날 수 있습니다에 toosign 개발자 라이선스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="49a9e-234">자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="49a9e-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="49a9e-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="49a9e-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="49a9e-236">연결된 된 장치에서 toorun:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="49a9e-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="49a9e-237">hello 기본 에뮬레이터에 toorun:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="49a9e-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="49a9e-238">사용 하 여 `cordova run windows --list -- --phone` toosee 모든 사용 가능한 대상 및 `cordova run windows --target=<target_name> -- --phone` 특정 장치 또는 에뮬레이터에서 toorun hello 응용 프로그램 (예를 들어 `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="49a9e-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="49a9e-239">Android</span><span class="sxs-lookup"><span data-stu-id="49a9e-239">Android</span></span>
   <span data-ttu-id="49a9e-240">연결된 된 장치에서 toorun:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="49a9e-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="49a9e-241">hello 기본 에뮬레이터에 toorun:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="49a9e-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="49a9e-242">만든 에뮬레이터 인스턴스가 AVD Manager를 사용 하 여 hello "전제 조건" 섹션에서에서 설명한 대로 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="49a9e-243">사용 하 여 `cordova run android --list` toosee 모든 사용 가능한 대상 및 `cordova run android --target=<target_name>` 특정 장치 또는 에뮬레이터에서 toorun hello 응용 프로그램 (예를 들어 `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="49a9e-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="49a9e-244">iOS</span><span class="sxs-lookup"><span data-stu-id="49a9e-244">iOS</span></span>
   <span data-ttu-id="49a9e-245">연결된 된 장치에서 toorun:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="49a9e-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="49a9e-246">hello 기본 에뮬레이터에 toorun:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="49a9e-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="49a9e-247">Hello 했는지 확인 `ios-sim` hello 에뮬레이터에서 toorun 패키지가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="49a9e-248">자세한 내용은 hello "전제 조건"을 참조 하세요. 섹션.</span><span class="sxs-lookup"><span data-stu-id="49a9e-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="49a9e-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="49a9e-249">Next steps</span></span>
<span data-ttu-id="49a9e-250">구성 값) (없이 hello 완료 샘플은에서 사용할 수 있는 참조를 위해 [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient)합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="49a9e-251">이제 고급 toomore (및 기타 흥미로운)에 이동 시나리오 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="49a9e-252">Tootry 할 수 있습니다: [Azure AD 사용 하 여 Node.js 웹 API 보안](active-directory-devquickstarts-webapi-nodejs.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="49a9e-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
