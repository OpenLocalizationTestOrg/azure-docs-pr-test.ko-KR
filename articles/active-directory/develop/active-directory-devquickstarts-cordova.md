---
title: "Azure AD Cordova 시작 | Microsoft 문서"
description: "로그인을 위해 Azure AD와 통합되고 OAuth를 사용하여 Azure AD로 보호되는 API를 호출하는 Cordova 응용 프로그램을 빌드하는 방법."
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="62a80-103">Azure AD를 Apache Cordova 앱에 통합</span><span class="sxs-lookup"><span data-stu-id="62a80-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="62a80-104">Apache Cordova를 사용하여 모든 기능이 갖춰진 네이티브 응용 프로그램으로 모바일 장치에서 실행될 수 있는 HTML5/JavaScript 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="62a80-105">Azure AD(Azure Active Directory)를 사용하면 Cordova 응용 프로그램에 엔터프라이즈급 인증 기능을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="62a80-106">Cordova 플러그 인은 iOS, Android, Windows 스토어 및 Windows Phone에서 Azure AD 네이티브 SDK를 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="62a80-107">해당 플러그 인을 사용하여 사용자의 Windows Server Active Directory 계정을 사용하는 로그인을 지원하고, Office 365 및 Azure API에 액세스하고, 사용자 고유의 사용자 지정 Web API에 대한 호출도 보호하도록 응용 프로그램을 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="62a80-108">이 자습서에서는 ADAL(Active Directory 인증 라이브러리)에 대한 Apache Cordova 플러그 인을 사용하고 다음 기능을 추가하여 간단한 앱을 개선해봅니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="62a80-109">단 몇 줄의 코드로, 사용자를 인증하고 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="62a80-110">해당 토큰을 사용하여 해당 디렉터리를 쿼리하고 결과를 표시하는 Graph API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="62a80-111">사용자에 대한 인증 프롬프트를 최소화하기 위해 ADAL 토큰 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="62a80-112">이러한 기능 개선을 위해서는 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="62a80-113">Azure AD에 응용 프로그램을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="62a80-114">앱에 토큰을 요청하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="62a80-115">해당 토큰을 사용하여 Graph API를 쿼리하고 결과를 표시하기 위한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="62a80-116">대상으로 지정할 모든 플랫폼 및 Cordova ADAL 플러그 인으로 Cordova 배포 프로젝트를 만들고 에뮬레이터에서 솔루션을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62a80-117">필수 조건</span><span class="sxs-lookup"><span data-stu-id="62a80-117">Prerequisites</span></span>
<span data-ttu-id="62a80-118">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="62a80-119">앱 개발 권한이 있는 계정이 있는 Azure AD 테넌트</span><span class="sxs-lookup"><span data-stu-id="62a80-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="62a80-120">Apache Cordova를 사용하도록 구성된 개발 환경.</span><span class="sxs-lookup"><span data-stu-id="62a80-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="62a80-121">위의 두 항목을 모두 설정한 경우 1단계를 바로 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="62a80-122">Azure AD 테넌트가 없는 경우 [여기에서 가져오는 방법에 대한 지침](active-directory-howto-tenant.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="62a80-123">컴퓨터에 Apache Cordova를 설정하지 않으려면 다음을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="62a80-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="62a80-124">Git</span><span class="sxs-lookup"><span data-stu-id="62a80-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="62a80-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="62a80-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="62a80-126">[Cordova CLI](https://cordova.apache.org/)(`npm install -g cordova` NPM 패키지 관리자를 통해 쉽게 설치 가능)</span><span class="sxs-lookup"><span data-stu-id="62a80-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="62a80-127">이전 설치는 PC와 Mac 둘 다에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="62a80-128">대상 플랫폼마다 필수 구성 요소가 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="62a80-129">Windows Tablet/PC 또는 Windows Phone을 빌드하여 실행하려면</span><span class="sxs-lookup"><span data-stu-id="62a80-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="62a80-130">[Windows용 Visual Studio 2013 업데이트 2 이상](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8)(Express 또는 다른 버전) 또는 [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="62a80-131">iOS에 대한 앱을 빌드하여 실행하려면</span><span class="sxs-lookup"><span data-stu-id="62a80-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="62a80-132">Xcode 6.x 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="62a80-133">[Apple 개발자 사이트](http://developer.apple.com/downloads) 또는 [Mac 앱 스토어](http://itunes.apple.com/us/app/xcode/id497799835?mt=12)에서 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="62a80-134">[ios-sim](https://www.npmjs.org/package/ios-sim)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="62a80-135">명령줄에서 iOS 시뮬레이터로 iOS 앱을 시작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="62a80-136">(터미널을 통해 쉽게 설치 가능: `npm install -g ios-sim`)</span><span class="sxs-lookup"><span data-stu-id="62a80-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="62a80-137">Android에 대한 앱을 빌드하여 실행하려면</span><span class="sxs-lookup"><span data-stu-id="62a80-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="62a80-138">[JDK(Java Development Kit) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) 이상을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="62a80-139">JDK 설치 경로(예: C:\Program Files\Java\jdk1.7.0_75)에 따라 `JAVA_HOME`(환경 변수)이 올바르게 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="62a80-140">[Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools)를 설치하고 `<android-sdk-location>\tools` 위치(예: C:\tools\Android\android-sdk\tools)를 `PATH` 환경 변수에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="62a80-141">Android SDK Manager를 열고(예를 들어 `android`터미널을 통해) 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="62a80-142">*Android 5.0.1(API 21)* 플랫폼 SDK</span><span class="sxs-lookup"><span data-stu-id="62a80-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="62a80-143">*Android SDK 빌드 도구* 버전 19.1.0 이상</span><span class="sxs-lookup"><span data-stu-id="62a80-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="62a80-144">*Android 지원 리포지토리* (기타)</span><span class="sxs-lookup"><span data-stu-id="62a80-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="62a80-145">Android SDK는 기본 에뮬레이터 인스턴스를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="62a80-146">에뮬레이터에서 Android 앱을 실행하려는 경우 터미널에서 `android avd`를 실행하고 **만들기**를 선택하여 에뮬레이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="62a80-147">API 수준 19 이상을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="62a80-148">Android 에뮬레이터 및 만들기 옵션에 대한 자세한 내용은 Android 사이트의 [AVD Manager](http://developer.android.com/tools/help/avd-manager.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62a80-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="62a80-149">1단계: Azure AD에 응용 프로그램 등록</span><span class="sxs-lookup"><span data-stu-id="62a80-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="62a80-150">이 단계는 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-150">This step is optional.</span></span> <span data-ttu-id="62a80-151">이 자습서는 자체 테넌트에서 프로비전을 수행하지 않고도 작동하는 샘플을 보는 데 사용할 수 있는 미리 프로비전된 값을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="62a80-152">그러나 자체 응용 프로그램을 만들 때 필요하므로 이 단계를 수행하고 프로세스에 익숙해지는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="62a80-153">Azure AD는 알려진 응용 프로그램으로만 토큰을 발급합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="62a80-154">앱에서 Azure AD를 사용하려면 먼저 테넌트에서 해당 항목을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="62a80-155">테넌트에 새 응용 프로그램을 등록하려면</span><span class="sxs-lookup"><span data-stu-id="62a80-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="62a80-156">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="62a80-157">위쪽 막대에서 계정을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-157">On the top bar, click your account.</span></span> <span data-ttu-id="62a80-158">**디렉터리** 목록에서 응용 프로그램을 등록할 Azure AD 테넌트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="62a80-159">왼쪽 창에서 **더 많은 서비스**를 클릭하고 **Azure Active Directory**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="62a80-160">**앱 등록**을 클릭하고 **추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="62a80-161">프롬프트에 따라 새 **네이티브 클라이언트 응용 프로그램**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="62a80-162">(Cordova 앱이 HTML 기반이기는 하지만 여기서는 네이티브 클라이언트 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="62a80-163">**네이티브 클라이언트 응용 프로그램** 옵션을 선택해야 하며 그렇지 않으면 응용 프로그램이 작동하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="62a80-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="62a80-164">**이름**은 사용자에게 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="62a80-165">**리디렉션 URI**는 앱에 토큰을 반환하는 데 사용되는 URI입니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="62a80-166">**http://MyDirectorySearcherApp**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="62a80-167">등록을 완료한 후에는 Azure AD가 사용자 앱에 고유한 응용 프로그램 ID를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="62a80-168">이 값은 다음 섹션에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="62a80-169">새로 만든 앱의 응용 프로그램 탭에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="62a80-170">`DirSearchClient Sample`을 실행하려면 새로 만든 앱에 Azure AD Graph API를 쿼리하는 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="62a80-171">**설정** 페이지에서 **필요한 사용 권한**, **추가**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="62a80-172">Azure Active Directory 응용 프로그램의 경우 API로 **Microsoft Graph**를 선택하고 **위임된 권한**에서 **로그인한 사용자로 디렉터리 액세스** 권한을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="62a80-173">이렇게 하면 응용 프로그램은 Graph API에서 사용자를 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="62a80-174">2단계: 샘플 앱 리포지토리 복제</span><span class="sxs-lookup"><span data-stu-id="62a80-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="62a80-175">셸 또는 명령줄에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="62a80-176">3단계: Cordova 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="62a80-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="62a80-177">여러 가지 방법으로 Cordova 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="62a80-178">이 자습서에서는 Cordova CLI(명령줄 인터페이스)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="62a80-179">셸 또는 명령줄에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="62a80-180">이 명령으로 Cordova 프로젝트에 대한 폴더 구조 및 스캐폴딩이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="62a80-181">새 DirSearchClient 폴더로 이동:</span><span class="sxs-lookup"><span data-stu-id="62a80-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="62a80-182">파일 관리자 또는 셸에서 다음 명령을 사용하여 www 하위 폴더에 시작 프로젝트의 콘텐츠를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="62a80-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="62a80-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="62a80-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="62a80-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="62a80-185">허용 목록 플러그 인을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="62a80-186">이 플러그 인은 Graph API를 호출하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="62a80-187">지원할 모든 플랫폼을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="62a80-188">작업 예제를 사용하려면 다음 명령 중 하나 이상을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="62a80-189">Windows에서는 iOS를, Mac에서는 Windows를 에뮬레이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="62a80-190">Cordova용 ADAL 플러그 인을 프로젝트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="62a80-191">4단계: 사용자를 인증하고 Azure AD에서 토큰을 가져오기 위한 코드 추가</span><span class="sxs-lookup"><span data-stu-id="62a80-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="62a80-192">이 자습서에서 개발 중인 응용 프로그램은 간단한 디렉터리 검색 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="62a80-193">그러면 사용자는 해당 디렉터리에 사용자의 별칭을 입력하고 몇 가지 기본 특성을 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="62a80-194">시작 프로젝트에는 앱의 기본 사용자 인터페이스 정의(www/index.html), 기본 앱 이벤트 주기를 연결하는 스캐폴딩의 정의, 사용자 인터페이스 바인딩 및 결과 표시 논리(www/js/index.js)가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="62a80-195">따라서 사용자는 ID 작업을 구현하는 논리만 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="62a80-196">코드에서 먼저 해야 할 작업은 앱 및 대상 리소스를 식별하기 위해 Azure AD에서 사용되는 프로토콜 값을 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="62a80-197">이러한 값은 나중에 토큰 요청을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="62a80-198">Index.js 파일의 맨 위에 다음 코드 조각을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="62a80-199">`redirectUri` 및 `clientId` 값은 Azure AD에서 앱을 설명하는 값과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="62a80-200">이 자습서 앞부분에 나오는 1단계에서 설명한 것처럼 Azure Portal의 **구성** 탭에서 이러한 값을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="62a80-201">사용자 고유의 테넌트에 새 앱을 등록하지 않도록 선택한 경우 미리 구성된 값을 그대로 붙여넣기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="62a80-202">프로덕션을 위해 계획된 앱에 대한 사용자 고유 항목을 항상 만들어야 하지만 샘플이 실행되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="62a80-203">다음으로 토큰 요청 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-203">Next, add the token request code.</span></span> <span data-ttu-id="62a80-204">`search` 및 `renderData` 정의 사이에 다음 코드 조각을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="62a80-205">두 주요 부분에서 분석하여 해당 함수를 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="62a80-206">이 샘플은 특정 테넌트에만 국한되지 않고 어떤 테넌트에서도 작동하도록 디자인되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="62a80-207">이 샘플은 인증 시에 사용자가 임의 계정을 입력하도록 하고 계정이 속하는 테넌트로 요청을 전달하는 "/common" 끝점을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="62a80-208">메서드의 첫 번째 부분은 ADAL 캐시를 검사하여 토큰이 이미 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="62a80-209">그렇다면 메서드는 ADAL을 다시 초기화하기 위해 토큰이 제공된 테넌트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="62a80-210">"/common"을 사용하면 항상 사용자에게 새 계정을 입력하라는 메시지가 표시되므로 불필요한 확인 메시지가 표시되지 않도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="62a80-211">이 메서드의 두 번째 부분에서는 적절한 토큰 요청을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="62a80-212">`acquireTokenSilentAsync` 메서드는 UX를 표시하지 않고 ADAL에 지정된 리소스에 대한 토큰의 반환을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="62a80-213">캐시에 이미 적합한 액세스 토큰이 저장되어 있거나 확인 메시지를 표시하지 않고 새 액세스 토큰을 가져오는 데 사용할 수 있는 새로 고침 토큰이 있는 경우 이러한 작업이 진행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="62a80-214">이 시도가 실패하면 사용자에게 인증을 요구하는 메시지를 표시하는 `acquireTokenAsync`로 대체할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="62a80-215">이제 토큰이 있으므로 마지막으로 Graph API를 호출하고 원하는 검색 쿼리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="62a80-216">`authenticate` 정의 아래에 다음 코드 조각을 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="62a80-217">시작점 파일은 텍스트 상자에 사용자의 별칭을 입력하기 위한 간단한 UX를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="62a80-218">이 메서드는 해당 값을 사용하여 쿼리를 생성하고, 액세스 토큰에 결합하고, Microsoft Graph로 보내고, 결과를 구문 분석합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="62a80-219">시작점 파일에 이미 있는 `renderData` 메서드는 결과를 시각화하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="62a80-220">5단계: 앱 실행</span><span class="sxs-lookup"><span data-stu-id="62a80-220">Step 5: Run the app</span></span>
<span data-ttu-id="62a80-221">이제 앱을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-221">Your app is finally ready to run.</span></span> <span data-ttu-id="62a80-222">작동은 간단합니다. 앱이 시작되면 텍스트 상자에 찾으려는 사용자의 별칭을 입력하고 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="62a80-223">인증을 위한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-223">You're prompted for authentication.</span></span> <span data-ttu-id="62a80-224">성공적으로 인증하고 검색하면 검색된 사용자의 특성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="62a80-225">이전에 가져온 토큰이 캐시에 있기 때문에 후속 실행은 프롬프트를 표시하지 않고 검색을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="62a80-226">앱을 실행하는 구체적인 단계는 플랫폼에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="62a80-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="62a80-227">Windows 10</span></span>
   <span data-ttu-id="62a80-228">태블릿/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="62a80-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="62a80-229">모바일(Windows 10 모바일 장치가 PC에 연결되어야 함): `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="62a80-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="62a80-230">처음 실행하는 동안 개발자 라이선스를 확인하기 위해 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="62a80-231">자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62a80-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="62a80-232">Windows 8.1 태블릿/PC</span><span class="sxs-lookup"><span data-stu-id="62a80-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="62a80-233">처음 실행하는 동안 개발자 라이선스를 확인하기 위해 로그인하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="62a80-234">자세한 내용은 [개발자 라이선스](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62a80-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="62a80-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="62a80-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="62a80-236">연결된 장치에서 실행하려면: `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="62a80-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="62a80-237">기본 에뮬레이터에서 실행하려면: `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="62a80-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="62a80-238">사용 가능한 모든 대상을 보려면 `cordova run windows --list -- --phone`을 사용하고, 특정 장치 또는 에뮬레이터에서 응용 프로그램을 실행하려면 `cordova run windows --target=<target_name> -- --phone`을 사용합니다(예: `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="62a80-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="62a80-239">Android</span><span class="sxs-lookup"><span data-stu-id="62a80-239">Android</span></span>
   <span data-ttu-id="62a80-240">연결된 장치에서 실행하려면: `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="62a80-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="62a80-241">기본 에뮬레이터에서 실행하려면: `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="62a80-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="62a80-242">이전에 "필수 조건" 섹션에서 설명한 대로 AVD Manager를 사용하여 에뮬레이터 인스턴스를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="62a80-243">사용 가능한 모든 대상을 보려면 `cordova run android --list`을 사용하고, 특정 장치 또는 에뮬레이터에서 응용 프로그램을 실행하려면 `cordova run android --target=<target_name>`을 사용합니다(예: `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="62a80-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="62a80-244">iOS</span><span class="sxs-lookup"><span data-stu-id="62a80-244">iOS</span></span>
   <span data-ttu-id="62a80-245">연결된 장치에서 실행하려면 `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="62a80-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="62a80-246">기본 에뮬레이터에서 실행하려면 `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="62a80-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="62a80-247">에뮬레이터에서 실행하려면 `ios-sim` 패키지가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="62a80-248">자세한 내용은 "필수 조건" 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="62a80-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="62a80-249">다음 단계</span><span class="sxs-lookup"><span data-stu-id="62a80-249">Next steps</span></span>
<span data-ttu-id="62a80-250">참조를 위해 완성된 샘플(사용자 구성 값 제외)이 [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient)에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="62a80-251">이제 좀 더 자세하고 좀 더 흥미로운 시나리오를 진행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="62a80-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="62a80-252">다음을 시도해 볼 수 있습니다. [Azure AD를 사용하여 Node.js Web API 보안 유지](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="62a80-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
