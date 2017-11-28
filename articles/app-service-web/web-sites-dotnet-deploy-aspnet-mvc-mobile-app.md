---
title: "Azure 앱 서비스의 ASP.NET MVC 5 aaaDeploy 모바일 웹 앱"
description: "앱 서비스 모바일을 사용 하는 웹 응용 프로그램 tooAzure toodeploy 기능이 방법 in ASP.NET MVC 5 웹 응용 프로그램에 설명 하는 자습서입니다."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="e7190-103">Azure 앱 서비스에 ASP.NET MVC 5 모바일 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="e7190-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="e7190-104">이 자습서에서는 어떻게 toobuild ASP.NET MVC 5 웹 모바일에서 잘 작동 되는 앱의 기본 사항을 hello 및 tooAzure 앱 서비스 배포에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="e7190-105">이 자습서에서는 필요한 [Visual Studio Express 2013 for Web] [ Visual Studio Express 2013] 또는 hello professional 버전의 Visual Studio가 이미 있는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="e7190-106">사용할 수 있습니다 [Visual Studio 2015] hello 스크린 샷이 달라질 수 있고 hello ASP.NET 4.x 서식 파일을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="e7190-107">만들 내용</span><span class="sxs-lookup"><span data-stu-id="e7190-107">What You'll Build</span></span>
<span data-ttu-id="e7190-108">이 자습서에서는 hello에 모바일 기능 toohello 간단한 목록 회의 응용 프로그램 제공 되는 추가 합니다 [시작 프로젝트][StarterProject]합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="e7190-109">hello 다음 스크린샷은 hello ASP.NET 세션 완료 hello 응용 프로그램에서는 hello 브라우저 에뮬레이터 Internet Explorer 11 F12 개발자 도구에서와 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e7190-110">Hello Internet Explorer 11 F12 개발자 도구 및 hello를 사용할 수 있습니다 [Fiddler 도구] [ Fiddler] toohelp 응용 프로그램을 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="e7190-111">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="e7190-111">Skills You'll Learn</span></span>
<span data-ttu-id="e7190-112">다음 내용을 학습하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="e7190-113">어떻게 toouse Visual Studio 2013 toopublish 웹 응용 프로그램의 Azure 앱 서비스 웹 앱 직접 tooa 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="e7190-114">ASP.NET MVC 5 hello 템플릿을 모바일 장치에 표시를 개선 하기 위해 hello CSS 부트스트랩 프레임 워크를 사용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="e7190-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="e7190-115">모바일 전용 toocreate tootarget 특정 모바일 브라우저의 경우 hello iPhone 및 Android와 같은 보는 방법</span><span class="sxs-lookup"><span data-stu-id="e7190-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="e7190-116">어떻게 toocreate 응답 뷰 (toodifferent 브라우저 장치에서 응답 하는 뷰)</span><span class="sxs-lookup"><span data-stu-id="e7190-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="e7190-117">Hello 개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="e7190-117">Set up hello development environment</span></span>
<span data-ttu-id="e7190-118">Hello Azure SDK for.NET 2.5.1 설치 하 여 개발 환경을 설정 이상.</span><span class="sxs-lookup"><span data-stu-id="e7190-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="e7190-119">Azure SDK for.NET을 tooinstall hello 아래 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="e7190-120">Visual Studio 2013을 아직 설치를 설정 하지 않은 hello 링크를 통해 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="e7190-121">이 자습서를 완료하려면 Visual Studio 2013이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="e7190-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="e7190-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="e7190-123">Hello 웹 플랫폼 설치 관리자 창에서 클릭 **설치** hello 설치를 진행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="e7190-124">모바일 브라우저 에뮬레이터도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="e7190-125">Hello 다음 중 하나라도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-125">Any of hello following will work:</span></span>

* <span data-ttu-id="e7190-126">[Internet Explorer 11 F12 개발자 도구][EmulatorIE11]의 브라우저 에뮬레이터(모바일 브라우저 스크린샷에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="e7190-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="e7190-127">Windows Phone 8, Windows Phone 7 및 Apple iPad를 위한 사용자 에이전트 문자열 기본 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="e7190-128">[Google Chrome DevTools][EmulatorChrome]의 브라우저 에뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="e7190-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="e7190-129">Apple iPhone, Apple iPad, Amazon Kindle Fire 등 여러 Android 장치에 대한 기본 설정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="e7190-130">터치 이벤트도 에뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-130">It also emulates touch events.</span></span>
* <span data-ttu-id="e7190-131">[Opera Mobile Emulator][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="e7190-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="e7190-132">Visual Studio 프로젝트를 C\# 소스 코드는 사용할 수 있는 tooaccompany이이 항목:</span><span class="sxs-lookup"><span data-stu-id="e7190-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="e7190-133">[시작 프로젝트 다운로드][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="e7190-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="e7190-134">[완성된 프로젝트 다운로드][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="e7190-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="e7190-135"><a name="bkmk_DeployStarterProject"></a>Hello 시작 프로젝트 tooan Azure 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e7190-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="e7190-136">Hello 회의 목록 응용 프로그램을 다운로드 [시작 프로젝트][StarterProject]합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="e7190-137">그런 다음 Windows 탐색기에서 hello 다운로드 한 ZIP 파일을 오른쪽 단추로 클릭 하 고 선택 *속성*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="e7190-138">Hello에 **속성** 대화 상자에서 선택 하는 hello **차단 해제** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="e7190-139">(Toouse 하려고 할 때 발생 하는 보안 경고가 표시 되지 않도록 차단 해제는 *.zip* hello 웹에서 다운로드 한 파일입니다.)</span><span class="sxs-lookup"><span data-stu-id="e7190-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="e7190-140">Hello ZIP 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **압축 풀기** hello 파일 압축을 풀입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="e7190-141">Visual Studio에서 열고 hello *C#\Mvc5Mobile.sln* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="e7190-142">솔루션 탐색기에서 hello 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="e7190-143">웹 게시에서 **Microsoft Azure 앱 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="e7190-144">Azure에 아직 로그인하지 않은 경우 **계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="e7190-145">Azure 계정에 표시 되는 메시지 toolog을 hello를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="e7190-146">hello 응용 프로그램 서비스 대화 상자 이제 표시 하면 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="e7190-147">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="e7190-148">Hello에 **웹 응용 프로그램 이름** 필드에서 고유한 응용 프로그램 이름 접두사를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="e7190-149">정규화된 웹앱 이름은 *&lt;prefix>*.azurewebsites.net입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="e7190-150">또한 **리소스 그룹**에서 새 리소스 그룹 이름을 선택하거나 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="e7190-151">클릭 **새로** toocreate 새 앱 서비스 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="e7190-152">Hello 새 앱 서비스 계획을 구성 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="e7190-153">Hello 응용 프로그램 서비스 만들기 대화 상자에서 다시 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="e7190-154">Hello Azure 리소스를 만든 후 새 응용 프로그램에 대 한 hello 설정을 사용 하 여 hello 웹 게시 대화가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="e7190-155">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="e7190-156">Visual Studio 프로젝트 toohello Azure 웹 앱에 대 한 게시의 hello 스타터 완료 되 면 hello 데스크톱 브라우저 toodisplay hello 라이브 웹 앱을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="e7190-157">모바일 브라우저 에뮬레이터를 시작, hello 회의 응용 프로그램에 대 한 hello URL 복사 (*<prefix>*. azurewebsites.net) hello 에뮬레이터에 한 다음 오른쪽 단추를 누르고 선택 **태그별찾아보기**.</span><span class="sxs-lookup"><span data-stu-id="e7190-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="e7190-158">Internet Explorer 11 hello 기본 브라우저로 사용 하는 경우 하기만 하면 tootype `F12`, 다음 `Ctrl+8`, 다음 너무 hello 브라우저 프로필을 변경 하 고**Windows Phone**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="e7190-159">아래 이미지에는 나와 hello *AllTags* 세로 모드로 보기 (에서 선택 **태그에 의해 찾아보기**).</span><span class="sxs-lookup"><span data-stu-id="e7190-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="e7190-160">Visual Studio 내에서 MVC 5 응용 프로그램을 디버그할 수, 하는 동안 웹 앱 tooAzure 게시할 수 있습니다 다시 tooverify hello 라이브 웹 앱 모바일 브라우저 또는 브라우저 에뮬레이터에서 앱에서 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="e7190-161">모바일 장치에서 읽을 수 있는 매우은 hello 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="e7190-162">또한 이미 hello 부트스트랩 CSS 프레임 워크에 의해 적용 된 hello 시각 효과 중 일부를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="e7190-163">Hello 클릭 **ASP.NET** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="e7190-164">hello ASP.NET 태그 보기는 확대/축소 맞추는 toohello 화면을 자동으로 부트스트랩을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="e7190-165">그러나이 toobetter 짝패 hello 모바일 브라우저 보기를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="e7190-166">예를 들어 hello **날짜** 열을 읽기가 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="e7190-167">Hello 자습서의 뒷부분에 나오는 hello 변경 *AllTags* toomake 볼 것 모바일에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="e7190-168"><a name="bkmk_bootstrap"></a> 부트스트랩 CSS 프레임워크</span><span class="sxs-lookup"><span data-stu-id="e7190-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="e7190-169">새로운 MVC 5 hello에 서식 파일은 기본적으로 부트스트랩 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="e7190-170">어떻게 응용 프로그램에서 서로 다른 뷰 hello 즉시 향상 이미 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="e7190-171">예를 들어 hello 브라우저 너비 작은 경우 hello 위쪽 탐색 모음 hello을 자동으로 축소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="e7190-172">Hello 데스크톱 브라우저에 hello 브라우저 창 크기를 다시 조정 하 고 hello 탐색 모음에서 디자인을 변경 하는 방법을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="e7190-173">부트스트랩에 제공 된 hello 응답성이 뛰어난 웹 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="e7190-174">toosee hello 웹 앱, 부트스트랩 없이 표시 되는 방법 열고 *앱\_시작\\BundleConfig.cs* 포함 하는 hello 줄을 주석 *bootstrap.js* 및 *bootstrap.css*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="e7190-175">hello 다음 코드를 보여 줍니다 hello hello에 마지막 두 개의 문을 `RegisterBundles` 메서드 hello 변경 후:</span><span class="sxs-lookup"><span data-stu-id="e7190-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="e7190-176">키를 눌러 `Ctrl+F5` toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="e7190-177">Hello 축소 가능한 탐색 창을 일반 순서가 지정 되지 않은 목록 방금 이제 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="e7190-178">**태그로 찾아보기**를 다시 클릭하고 **ASP.NET**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="e7190-179">Hello 모바일 에뮬레이터 뷰에서 확대/축소 맞추는 toohello 화면은 더 이상 고 스크롤해야 옆으로 hello 테이블의 순서 toosee hello 오른쪽 면에서 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="e7190-180">변경 내용을 실행 취소 hello 모바일에서 잘 작동 디스플레이 복원 된 hello 모바일 브라우저 tooverify 새로 고 치세요.</span><span class="sxs-lookup"><span data-stu-id="e7190-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="e7190-181">부트스트랩 특정 tooASP.NET MVC 5 아니며 모든 웹 응용 프로그램에서 이러한 기능을 활용을 취할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="e7190-182">하지만 이제는 ASP.NET MVC 5 프로젝트 템플릿에 기본 제공되므로 MVC 5 웹 응용 프로그램은 Bootstrap을 기본적으로 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="e7190-183">부트스트랩에 대 한 자세한 내용을 보려면 이동 toothe [부트스트랩] [ BootstrapSite] 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="e7190-184">Hello 다음 섹션에 표시 됩니다 어떻게 tooprovide mobile 브라우저에 대 한 특정 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="e7190-185"><a name="bkmk_overrideviews"></a>Hello 뷰, 레이아웃 및 부분 뷰를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="e7190-186">일반적인 모바일 브라우저, 개별 모바일 브라우저 또는 특정 브라우저용 뷰(레이아웃 및 부분 뷰 포함)를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="e7190-187">tooprovide 모바일 전용 보기, 뷰 파일을 복사 하 고 추가 *합니다. 모바일* toohello 파일 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="e7190-188">예를 들어 toocreate 모바일 *인덱스* 뷰를 복사할 수는 있지만 *뷰\\홈\\Index.cshtml* 를 *뷰\\홈\\ Index.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="e7190-189">이 섹션에서는 모바일 전용 레이아웃 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="e7190-190">toostart, 복사 *뷰\\Shared\\\_Layout.cshtml* 를 *뷰\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="e7190-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="e7190-191">열기  *\_Layout.Mobile.cshtml* 에서 hello 제목을 변경 하 고 **m v c 5 응용 프로그램** 너무**m v c 5 응용 프로그램 (모바일)**합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="e7190-192">각 `Html.ActionLink` hello 탐색 모음에 대 한 호출, "찾아보기 기준" 각 링크에 제거 *ActionLink*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="e7190-193">hello 다음 보여 주는 코드를 완료 하는 hello `<ul class="nav navbar-nav">` hello 모바일 레이아웃 파일의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="e7190-194">복사 hello *뷰\\홈\\AllTags.cshtml* 파일을 *뷰\\홈\\AllTags.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="e7190-195">Hello 새 파일을 열고 변경는 `<h2>` "Tags"에서 요소 너무 "태그 (M)":</span><span class="sxs-lookup"><span data-stu-id="e7190-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="e7190-196">데스크톱 브라우저 및 모바일 브라우저 에뮬레이터를 사용 하 여 toohello 태그 페이지를 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="e7190-197">hello 모바일 브라우저 에뮬레이터 hello를 두 개의 변경 내용을 표시 (에서 제목 hello  *\_Layout.Mobile.cshtml* 와 hello 제목 *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e7190-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="e7190-198">반면, 바탕 화면 hello 변경 되지 않은 (에서 제목이  *\_Layout.cshtml* 및 *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e7190-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="e7190-199"><a name="bkmk_browserviews"></a> 브라우저 전용 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e7190-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="e7190-200">또한 toomobile 및 데스크톱 관련 뷰, 개별 브라우저에 대 한 보기를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="e7190-201">예를 들어 hello iPhone 또는 Android 브라우저 hello에만 사용 되는 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="e7190-202">이 섹션에서는 hello iPhone 버전과 hello iPhone 브라우저에 대 한 레이아웃 만듭니다 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="e7190-203">열기 hello *Global.asax* 파일 및 코드 toohello 맨 뒤 hello 추가 `Application_Start` 메서드.</span><span class="sxs-lookup"><span data-stu-id="e7190-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="e7190-204">이 코드는 각 수신 요청에 맞출 "iPhone"이라는 새로운 디스플레이 모드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="e7190-205">(즉, 포함 되 면 hello 사용자 에이전트 hello "iPhone")를 정의 된 조건과 일치 하는 hello 들어오는 요청을 하면 ASP.NET MVC는 이름이 "iPhone" 접미사를 포함 하는 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="e7190-206">때 모바일 브라우저 전용 추가 디스플레이 모드와 같은 iPhone 및 Android에 대 한 있는지 tooset hello 첫 번째 인수를 너무 수`0` (hello hello 목록 위쪽에서의 삽입) toomake 있는지 hello 브라우저 전용 모드를 사용 하는 우선 순위가 hello 모바일 서식 파일 (*. Mobile.cshtml)입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="e7190-207">이면 hello 모바일 템플릿 hello 목록의 위쪽에 hello 대신 의도 한 디스플레이 모드를 통해 선택할 수 있습니다 (첫 번째 일치 wins hello 및 모든 모바일 브라우저 일치 하는 hello 모바일 템플릿이).</span><span class="sxs-lookup"><span data-stu-id="e7190-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="e7190-208">Hello 코드에서 마우스 오른쪽 단추로 클릭 `DefaultDisplayMode`, 선택 **해결**를 선택한 후 `using System.Web.WebPages;`합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="e7190-209">참조 toothe 추가 `System.Web.WebPages` 에 네임 스페이스는 `DisplayModeProvider` 및 `DefaultDisplayMode` 형식은 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="e7190-210">또는 다음 줄 toothe hello만 수동으로 추가할 수 `using` hello 파일의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="e7190-211">Hello 변경 내용을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-211">Save hello changes.</span></span> <span data-ttu-id="e7190-212">*Views\\Shared\\\_Layout.Mobile.cshtml* 파일을 *Views\\Shared\\\_Layout.iPhone.cshtml*에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="e7190-213">Hello 새 파일을 열고 hello 제목을 변경 `MVC5 Application (Mobile)` 를 `MVC5 Application (iPhone)`합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="e7190-214">복사 hello *뷰\\홈\\AllTags.Mobile.cshtml* 파일을 *뷰\\홈\\AllTags.iPhone.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="e7190-215">Hello 새 파일에서 변경 hello `<h2>` 요소에서 "태그 (M)" "태그가 너무 (iPhone)"입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="e7190-216">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-216">Run hello application.</span></span> <span data-ttu-id="e7190-217">모바일 브라우저 에뮬레이터에서 앱 실행, 해당 사용자 에이전트 너무 설정 되어 있는지 확인 "iPhone" toohello 찾아보기 및 *AllTags* 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="e7190-218">Hello 에뮬레이터 Internet Explorer 11 F12 개발자 도구를 사용 하는 경우 에뮬레이션 toohello 다음을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="e7190-219">브라우저 프로필 = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="e7190-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="e7190-220">사용자 에이전트 문자열 = **Custom**</span><span class="sxs-lookup"><span data-stu-id="e7190-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="e7190-221">사용자 지정 문자열 = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="e7190-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="e7190-222">hello 다음 스크린샷은 hello *AllTags* (iPhone 5 C 사용자 에이전트 문자열은) 보기 사용자 지정 사용자 에이전트 문자열 hello와 Internet Explorer 11 F12 개발자 도구에서 에뮬레이터에 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="e7190-223">모바일 브라우저 hello 선택 hello **스피커** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="e7190-224">모바일 보기 없기 때문에 (*AllSpeakers.Mobile.cshtml*), hello 기본 스피커 볼 (*AllSpeakers.cshtml*) hello 모바일 레이아웃 보기를 사용 하 여 렌더링 됩니다 ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e7190-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="e7190-225">Hello 제목 아래와 같이 **m v c 5 응용 프로그램 (모바일)** 에 정의 된  *\_Layout.Mobile.cshtml*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="e7190-226">전역으로 설정 하 여 렌더링 모바일 레이아웃 내에서 기본 (비모바일) 뷰를 비활성화할 수 있습니다 `RequireConsistentDisplayMode` 를 `true` hello에 *뷰\\\_ViewStart.cshtml* 다음과 같이 파일:</span><span class="sxs-lookup"><span data-stu-id="e7190-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="e7190-227">때 `RequireConsistentDisplayMode` 너무 설정`true`, hello 모바일 레이아웃 (*\_Layout.Mobile.cshtml*) 모바일 보기에만 사용 됩니다 (즉, 파일 보기 경우 hello 폼의  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="e7190-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="e7190-228">Tooset 경우가 `RequireConsistentDisplayMode` 너무`true` 모바일 레이아웃 비모바일 보기와 잘 작동 하지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="e7190-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="e7190-229">hello에서는 아래 스크린샷에서 방법을 hello *스피커* 페이지를 렌더링 하는 경우 `RequireConsistentDisplayMode` 너무 설정`true` (없이 hello 문자열 hello hello 위쪽 탐색 모음에서 "(모바일)").</span><span class="sxs-lookup"><span data-stu-id="e7190-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="e7190-230">설정 하 여 특정 보기에서 일관 된 표시 모드를 해제할 수 `RequireConsistentDisplayMode` 너무`false` hello 보기 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="e7190-231">Hello에 다음 태그 *뷰\\홈\\AllSpeakers.cshtml* 파일 집합 `RequireConsistentDisplayMode` 너무`false`:</span><span class="sxs-lookup"><span data-stu-id="e7190-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="e7190-232">이 섹션에서 살펴본 어떻게 toocreate 모바일 레이아웃, 뷰 및 toocreate 레이아웃, 보기와 같은 특정 장치에 대 한 iPhone hello 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="e7190-233">그러나 hello 부트스트랩 CSS 프레임 워크의 주요 이점은 hello는 반응 형 레이아웃 즉, 데스크톱, 휴대폰 및 태블릿 브라우저 toocreate 일관 된 모양과 느낌에는 단일 스타일 시트를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="e7190-234">Hello 다음 섹션에 표시 tooleverage 부트스트랩 toocreate 모바일에서 잘 작동 하는 방법 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="e7190-235"><a name="bkmk_Improvespeakerslist"></a>Hello 스피커 목록 개선</span><span class="sxs-lookup"><span data-stu-id="e7190-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="e7190-236">Hello, 본 것 처럼 *스피커* 보기를 읽을 수는 하지만 어려운 tootap 모바일 장치에는 작은 hello 링크 이며 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="e7190-237">이 섹션에서는 할 hello *AllSpeakers* 스피커를 찾을 큰, tap 쉬운 링크를 표시 하 고 검색 상자 tooquickly를 포함 하는 뷰의 모바일에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="e7190-238">부트스트랩 hello를 사용할 수 있습니다 [연결된 리스트 그룹] [ linked list group] hello를 개선 하기 위해 스타일 지정 *스피커* 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="e7190-239">*뷰\\홈\\AllSpeakers.cshtml*, hello Razor 파일의 내용을 hello 아래 hello 코드로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="e7190-240">hello `class="list-group"` hello에 대 한 특성 `<div>` 태그 적용 부트스트랩 목록 스타일 및 hello `class="input-group-item"` 부트스트랩 목록 항목 스타일 지정 tooeach 링크 특성을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="e7190-241">Hello 모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="e7190-242">hello 업데이트 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="e7190-243">부트스트랩 hello [연결된 리스트 그룹] [ linked list group] 스타일 지정 hello 전체 각 링크를 클릭할 수 있는 상자는 훨씬 더 나은 사용자 환경을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="e7190-244">Toothe 바탕 화면 보기를 전환 하 고 hello 일관 된 모양과 느낌을 관찰 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="e7190-245">Hello 모바일 브라우저 보기 기능이 향상 되기는 하지만 스피커 hello 긴 목록을 탐색 하 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="e7190-246">부트스트랩은 바로 사용 가능한 검색 필터 기능을 제공하지 않지만, 코드 몇 줄을 사용하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="e7190-247">먼저 추가 검색 상자 toohello 보기에서는 다음 hello hello 필터 함수에 대 한 JavaScript 코드와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="e7190-248">*뷰\\홈\\AllSpeakers.cshtml*, 추가 \<양식\> hello 직후 태그 \<h2\> 아래와 같이 태그:</span><span class="sxs-lookup"><span data-stu-id="e7190-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="e7190-249">해당 hello 확인 `<form>` 및 `<input>` 태그는 모두 hello 부트스트랩 스타일이 적용 toothem 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="e7190-250">hello `<span>` 요소 추가 부트스트랩 [glyphicon] [ glyphicon] toothe 검색 상자입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="e7190-251">Hello에 *스크립트* 폴더 이라는 JavaScript 파일을 추가 *filter.js*합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="e7190-252">Hello 파일을 열고 hello에 코드를 다음을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="e7190-253">에 등록 된 번들의 있어야 tooinclude filter.js 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="e7190-254">열기 *앱\_시작\\BundleConfig.cs* hello 첫 번째 번들을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="e7190-255">첫 번째 변경 `bundles.Add` 문 (hello에 대 한 **jquery** 번들) tooinclude *스크립트\\filter.js*, 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="e7190-256">hello **jquery** 번들 hello 기본적으로 이미 렌더링  *\_레이아웃* 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="e7190-257">Hello를 사용 하는 나중 같은 JavaScript 코드 tooapply 필터 기능 tooother 목록 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="e7190-258">Hello 모바일 브라우저를 새로 고치고 toohello 이동 *AllSpeakers* 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="e7190-259">검색 상자에 "sc"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-259">In the search box, type "sc".</span></span> <span data-ttu-id="e7190-260">이제 tooyour 검색 문자열에 따라 hello 스피커 목록을 필터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="e7190-261"><a name="bkmk_improvetags"></a>Hello 태그 목록 개선</span><span class="sxs-lookup"><span data-stu-id="e7190-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="e7190-262">Hello 처럼 *스피커* 를 보려면 hello *태그* 보기를 읽을 수는 있지만 hello 링크는 모바일 장치에서 작은 어렵고 tootap 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="e7190-263">Hello를 해결할 수 *태그* 보기 hello 동일 hello를 수정 하는 방식으로 *스피커* hello 다음 하지만 앞에서 설명한 hello 코드 변경 내용을 사용 하는 경우 보고 `Html.ActionLink` 에 메서드 구문을  *뷰\\홈\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e7190-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="e7190-264">hello는 다음과 같이 데스크톱 브라우저 검색 새로 고침:</span><span class="sxs-lookup"><span data-stu-id="e7190-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="e7190-265">하 고 다음과 같이 새로 고칠 모바일 브라우저 찾습니다 hello:</span><span class="sxs-lookup"><span data-stu-id="e7190-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="e7190-266">Hello 원래 목록 형식 지정 하는 경우 중인 아직 중지 되지 않은 모바일 브라우저 hello 및 발생 했습니다 tooyour 좋은 부트스트랩 스타일 있는지 잘 이해가 가지, 이전 동작 toocreate 모바일 특정 보기에 대 한 아티팩트입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="e7190-267">그러나 이제 hello 부트스트랩 CSS 프레임 워크 toocreate 응답성이 뛰어난 웹 디자인을 사용 하는 서을 이러한 모바일 전용 뷰 및 hello 모바일 전용 레이아웃 보기를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="e7190-268">그렇게 않은 모바일 브라우저를 새로 고친된 hello hello 부트스트랩 스타일이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="e7190-269"><a name="bkmk_improvedates"></a>Hello 날짜 목록 개선</span><span class="sxs-lookup"><span data-stu-id="e7190-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="e7190-270">Hello를 향상 시킬 수 있습니다 *날짜* hello 향상 처럼 볼 *스피커* 및 *태그* hello 코드 변경 내용을 따라 hello 하지만 앞에서 설명한 를사용하는경우뷰`Html.ActionLink` 에 메서드 구문을 *뷰\\홈\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="e7190-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="e7190-271">새로 고친 모바일 브라우저 뷰는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="e7190-272">Hello 속도가 더욱 향상 *날짜* 날짜별으로 hello 날짜 및 시간 값을 구성 하 여 보기.</span><span class="sxs-lookup"><span data-stu-id="e7190-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="e7190-273">부트스트랩 hello로이 작업을 수행할 수 있습니다 [패널] [ panels] 스타일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="e7190-274">Hello hello 내용 바꾸기 *뷰\\홈\\AllDates.cshtml* 를 다음 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="e7190-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="e7190-275">이 코드에서는 별도 `<div class="panel panel-primary">` hello 목록 및 사용 하 여 hello에 고유한 각 날짜에 대 한 태그 [연결된 리스트 그룹] [ linked list group] 각각에 대 한 이전 처럼를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="e7190-276">이 코드를 실행할 때 처럼 보이지만 어떤 hello 모바일 브라우저는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="e7190-277">Toohello 데스크톱 브라우저를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="e7190-278">다시, 참고 hello 일관성 있는 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="e7190-279"><a name="bkmk_improvesessionstable"></a>Hello SessionsTable 보기 개선</span><span class="sxs-lookup"><span data-stu-id="e7190-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="e7190-280">이 섹션에서는 할 hello *SessionsTable* 보려면 자세한 모바일에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="e7190-281">이 변경은 더 광범위 한 hello 이전 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="e7190-282">Hello 모바일 브라우저에서 hello 누릅니다 **태그** 입력 한 다음 단추를 `asp` 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="e7190-283">Hello 누릅니다 **ASP.NET** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="e7190-284">볼 수 있듯이 hello 표시로 디자인 된 현재 toobe hello 데스크톱 브라우저에 표시 되는 테이블에 형식 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="e7190-285">그러나 모바일 브라우저에 약간 어려울 tooread 되기 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="e7190-286">toofix이,이 오픈 *뷰\\홈\\SessionsTable.cshtml* 파일의 내용을 hello 코드 다음 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="e7190-287">hello 코드에서는 3 가지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-287">hello code does 3 things:</span></span>

* <span data-ttu-id="e7190-288">사용 하 여 hello 부트스트랩 [연결 된 목록 사용자 지정 그룹] [ custom linked list group] tooformat hello 세션 정보 세로 방향으로,이 모든 정보는 (사용 하 여 클래스와 같은 모바일 브라우저에서 읽을 수 있도록 목록 그룹-항목-텍스트)</span><span class="sxs-lookup"><span data-stu-id="e7190-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="e7190-289">hello 적용 [그리드 시스템] [ grid system] toothe 레이아웃 하므로 해당 hello 세션 항목 hello 데스크톱 브라우저에서 가로 및 세로로 hello 모바일 브라우저 (hello col md 4 클래스 사용)에서 흐름</span><span class="sxs-lookup"><span data-stu-id="e7190-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="e7190-290">사용 하 여 hello [응답 유틸리티] [ responsive utilities] hello 세션 태그 (hello xs 숨겨진 클래스를 사용 하 여) hello 모바일 브라우저에서 볼 때를 숨기려면</span><span class="sxs-lookup"><span data-stu-id="e7190-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="e7190-291">또한 제목 링크 toogo toohello 해당 세션을 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="e7190-292">아래 hello 이미지 hello 코드 변경 내용을 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e7190-293">자동으로 적용 하는 hello 부트스트랩 그리드 시스템 hello 모바일 브라우저 세션을 세로로 정렬 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="e7190-294">또한 사라졌는지 hello 태그는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="e7190-295">Toohello 데스크톱 브라우저를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="e7190-296">Hello 데스크톱 브라우저에서 hello 태그는 이제 표시를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="e7190-297">또한 hello 부트스트랩 그리드 시스템 적용 한 경우 두 열에 hello 세션 항목을 정렬 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="e7190-298">브라우저를 확대 하면 hello 정렬을 toothree 열 변경 되는지 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="e7190-299"><a name="bkmk_improvesessionbycode"></a>Hello SessionByCode 보기 개선</span><span class="sxs-lookup"><span data-stu-id="e7190-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="e7190-300">Hello를 마지막으로 수정 합니다 *SessionByCode* toomake 볼 것 모바일에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="e7190-301">Hello 모바일 브라우저에서 hello 누릅니다 **태그** 입력 한 다음 단추를 `asp` 검색 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="e7190-302">Hello 누릅니다 **ASP.NET** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="e7190-303">Hello ASP.NET 태그에 대 한 세션이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="e7190-304">Hello 선택 **ASP.NET 및 AngularJS 단일 페이지 응용 프로그램 빌드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="e7190-305">hello 기본 바탕 화면 보기 하지만, 일부 부트스트랩 GUI 구성 요소를 사용 하 여 hello 모양의 쉽게 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="e7190-306">열기 *뷰\\홈\\SessionByCode.cshtml* hello 내용을 태그 뒤 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="e7190-307">hello 새 태그 tooimprove hello 모바일 보기의 스타일을 지정 하는 부트스트랩 패널을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="e7190-308">Hello 모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="e7190-309">hello 다음 이미지 반영 방금 만든 hello 코드 변경 내용:</span><span class="sxs-lookup"><span data-stu-id="e7190-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="e7190-310">요약 및 검토</span><span class="sxs-lookup"><span data-stu-id="e7190-310">Wrap Up and Review</span></span>
<span data-ttu-id="e7190-311">이 자습서에서는 살펴보았습니다 어떻게 웹 응용 프로그램 toouse ASP.NET MVC 5 toodevelop 모바일에서 잘 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="e7190-312">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7190-312">These include:</span></span>

* <span data-ttu-id="e7190-313">ASP.NET MVC 5 응용 프로그램 tooan 앱 서비스 웹 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="e7190-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="e7190-314">MVC 5 응용 프로그램에서 부트스트랩 toocreate 응답성이 뛰어난 웹 레이아웃을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e7190-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="e7190-315">모든 뷰에 대해 그리고 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰 재정의</span><span class="sxs-lookup"><span data-stu-id="e7190-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="e7190-316">`RequireConsistentDisplayMode` 속성을 사용하여 레이아웃 및 부분 재정의 작업 제어</span><span class="sxs-lookup"><span data-stu-id="e7190-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="e7190-317">Hello iPhone 브라우저와 같은 특정 브라우저를 대상으로 하는 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e7190-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="e7190-318">Razor 코드에서 Boostrap 스타일 적용</span><span class="sxs-lookup"><span data-stu-id="e7190-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="e7190-319">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e7190-319">See Also</span></span>
* [<span data-ttu-id="e7190-320">반응형 웹 디자인의 9가지 기본 원칙</span><span class="sxs-lookup"><span data-stu-id="e7190-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="e7190-321">[부트스트랩][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="e7190-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="e7190-322">[공식 부트스트랩 블로그][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="e7190-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="e7190-323">[Tutorial Republic의 Twitter 부트스트랩 자습서][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="e7190-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="e7190-324">[부트스트랩 Playground hello][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="e7190-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="e7190-325">[W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="e7190-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="e7190-326">[미디어 쿼리에 대한 W3C 권장 사항][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="e7190-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e7190-327">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="e7190-327">What's changed</span></span>
* <span data-ttu-id="e7190-328">웹 사이트 tooApp 서비스에서에서 변경 사항 참조 가이드 toohello: [기존 Azure 서비스에 대 한 해당 영향 및 Azure 앱 서비스](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e7190-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

