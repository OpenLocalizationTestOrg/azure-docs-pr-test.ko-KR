---
title: "Azure 앱 서비스에 ASP.NET MVC 5 모바일 웹 앱 배포"
description: "ASP.NET MVC 5 웹 응용 프로그램에서 모바일 기능을 사용하여 Azure 앱 서비스에 웹 앱을 배포하는 방법에 대해 설명하는 자습서입니다."
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
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="1062c-103">Azure 앱 서비스에 ASP.NET MVC 5 모바일 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="1062c-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="1062c-104">이 자습서에서는 모바일 친화적인 ASP.NET MVC 5 웹 앱을 만들고 Azure 앱 서비스에 배포하는 방법에 대한 기초적인 내용을 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="1062c-105">이 자습서를 사용하려면 [Visual Studio Express 2013 for Web][Visual Studio Express 2013] 또는 이미 보유하고 있는 Visual Studio의 Professional 버전이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="1062c-106">[Visual Studio 2015] 를 사용할 수 있지만 스크린샷이 달라지게 되고 ASP.NET 4.x 템플릿을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="1062c-107">만들 내용</span><span class="sxs-lookup"><span data-stu-id="1062c-107">What You'll Build</span></span>
<span data-ttu-id="1062c-108">이 자습서에서는 [시작 프로젝트][StarterProject]에 제공된 간단한 회의 목록 응용 프로그램에 모바일 기능을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="1062c-109">다음 스크린샷은 완료된 응용 프로그램에서의 ASP.NET 세션을 보여 줍니다. Internet Explorer 11 F12 개발자 도구에 있는 브라우저 에뮬레이터에서 이러한 세션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1062c-110">Internet Explorer 11 F12 개발자 도구 및 [Fiddler 도구][Fiddler]를 사용하여 응용 프로그램을 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="1062c-111">학습할 기술</span><span class="sxs-lookup"><span data-stu-id="1062c-111">Skills You'll Learn</span></span>
<span data-ttu-id="1062c-112">다음 내용을 학습하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="1062c-113">Visual Studio 2013을 사용하여 웹 응용 프로그램을 Azure 앱 서비스의 웹 앱에 직접 게시하는 방법</span><span class="sxs-lookup"><span data-stu-id="1062c-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="1062c-114">모바일 장치의 디스플레이를 향상하기 위해 ASP.NET MVC 5 템플릿에서 CSS 부트스트랩 프레임워크를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="1062c-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="1062c-115">iPhone 및 Android 등 특정 모바일 브라우저를 대상으로 모바일 전용 뷰를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1062c-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="1062c-116">반응형 뷰(장치 간의 서로 다른 브라우저에 반응하는 뷰)를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="1062c-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="1062c-117">개발 환경 설정</span><span class="sxs-lookup"><span data-stu-id="1062c-117">Set up the development environment</span></span>
<span data-ttu-id="1062c-118">Azure SDK for .NET 2.5.1 이상을 설치하여 개발 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="1062c-119">Azure SDK for .NET을 설치하려면 아래 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="1062c-120">Visual Studio 2013가 아직 설치되어 있지 않은 경우 링크를 통해 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="1062c-121">이 자습서를 완료하려면 Visual Studio 2013이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="1062c-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="1062c-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="1062c-123">웹 플랫폼 설치 관리자 창에서 **설치** 를 클릭하여 설치를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="1062c-124">모바일 브라우저 에뮬레이터도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="1062c-125">다음을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-125">Any of the following will work:</span></span>

* <span data-ttu-id="1062c-126">[Internet Explorer 11 F12 개발자 도구][EmulatorIE11]의 브라우저 에뮬레이터(모바일 브라우저 스크린샷에 사용됨).</span><span class="sxs-lookup"><span data-stu-id="1062c-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="1062c-127">Windows Phone 8, Windows Phone 7 및 Apple iPad를 위한 사용자 에이전트 문자열 기본 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="1062c-128">[Google Chrome DevTools][EmulatorChrome]의 브라우저 에뮬레이터.</span><span class="sxs-lookup"><span data-stu-id="1062c-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="1062c-129">Apple iPhone, Apple iPad, Amazon Kindle Fire 등 여러 Android 장치에 대한 기본 설정이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="1062c-130">터치 이벤트도 에뮬레이트합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-130">It also emulates touch events.</span></span>
* <span data-ttu-id="1062c-131">[Opera Mobile Emulator][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="1062c-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="1062c-132">C\# 소스 코드를 사용하는 Visual Studio 프로젝트를 다음 항목과 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="1062c-133">[시작 프로젝트 다운로드][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="1062c-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="1062c-134">[완성된 프로젝트 다운로드][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="1062c-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="1062c-135"><a name="bkmk_DeployStarterProject"></a>Azure 웹 앱에 시작 프로젝트 배포</span><span class="sxs-lookup"><span data-stu-id="1062c-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="1062c-136">회의 목록 응용 프로그램 [시작 프로젝트][StarterProject]를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="1062c-137">그런 다음 Windows 탐색기에서 다운로드한 ZIP 파일을 마우스 오른쪽 단추로 클릭하고 *속성*을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="1062c-138">**속성** 대화 상자에서 **차단 해제** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="1062c-139">(차단 해제는 웹에서 다운로드한 *.zip* 파일을 사용하려고 할 때 발생하는 보안 경고를 막습니다.)</span><span class="sxs-lookup"><span data-stu-id="1062c-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="1062c-140">ZIP 파일을 마우스 오른쪽 단추로 클릭하고 **모두 압축 풀기** 를 선택하여 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="1062c-141">Visual Studio에서 *C#\Mvc5Mobile.sln* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="1062c-142">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="1062c-143">웹 게시에서 **Microsoft Azure 앱 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="1062c-144">Azure에 아직 로그인하지 않은 경우 **계정 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="1062c-145">표시되는 메시지에 따라 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="1062c-146">이제 앱 서비스 대화 상자가 로그인한 것으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="1062c-147">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="1062c-148">**웹앱 이름** 필드에서 고유한 앱 이름 접두사를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="1062c-149">정규화된 웹앱 이름은 *&lt;prefix>*.azurewebsites.net입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="1062c-150">또한 **리소스 그룹**에서 새 리소스 그룹 이름을 선택하거나 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="1062c-151">그런 다음 **새로 만들기** 를 클릭하여 새 앱 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="1062c-152">새 앱 서비스 계획을 구성하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="1062c-153">다시 앱 서비스 만들기 대화 상자에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="1062c-154">Azure 리소스가 만들어진 후 웹 게시 대화 상자에 새 앱의 설정이 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="1062c-155">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="1062c-156">Visual Studio에서 시작 프로젝트를 Azure 웹 앱에 게시하는 것이 완료된 후에는 데스크톱 브라우저가 열려서 라이브 웹 앱을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="1062c-157">모바일 브라우저 에뮬레이터를 시작하고 회의 응용 프로그램(*<prefix>*.azurewebsites.net)의 URL을 에뮬레이터에 복사한 다음 오른쪽 위에 있는 단추를 클릭하고 **태그로 찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="1062c-158">Internet Explorer 11을 기본 브라우저로 사용 중인 경우에는 `F12` 및 `Ctrl+8`을 입력한 후에 브라우저 프로필을 **Windows Phone**으로 변경하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="1062c-159">아래 이미지는 *AllTags* 뷰를 세로 모드로 보여 줍니다( **태그로 찾아보기**선택 시).</span><span class="sxs-lookup"><span data-stu-id="1062c-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="1062c-160">Visual Studio 내에서 MVC 5 응용 프로그램을 디버깅할 수도 있고, 웹 앱을 Azure에 다시 게시하여 모바일 브라우저나 브라우저 에뮬레이터에서 라이브 웹 앱을 직접 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="1062c-161">이 화면은 모바일 장치에서 가독성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="1062c-162">이미 부트스트랩 CSS 프레임워크에 의해 적용된 시각 효과 중 일부를 알고 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="1062c-163">**ASP.NET** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="1062c-164">ASP.NET 태그 뷰는 화면에 맞게 크기가 조정되어 있습니다. 크기 조정은 Bootstrap에서 자동으로 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="1062c-165">하지만 모바일 브라우저에 더 알맞게 이 뷰를 향상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="1062c-166">예를 들어 **Date** 열은 읽기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="1062c-167">이 자습서 뒷부분에서 *AllTags* 뷰를 모바일 친화적으로 변경해 볼 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="1062c-168"><a name="bkmk_bootstrap"></a> 부트스트랩 CSS 프레임워크</span><span class="sxs-lookup"><span data-stu-id="1062c-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="1062c-169">MVC 5 템플릿의 새로운 점은 기본 제공 Bootstrap 지원입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="1062c-170">이것이 응용 프로그램에서 여러 가지 뷰를 즉시 향상하는 것을 이미 확인한 바 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="1062c-171">예를 들어 맨 위에 있는 탐색 표시줄은 브라우저 너비가 좁아질 때 자동으로 축소될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="1062c-172">데스크톱 브라우저에서 브라우저 창의 크기를 조정하여 탐색 표시줄의 모양과 느낌이 어떻게 변하는지 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1062c-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="1062c-173">이것이 Bootstrap에 기본 제공되는 반응형 웹 디자인입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="1062c-174">Bootstrap을 사용하지 않을 때 웹앱이 어떻게 보이는지를 확인하려면 *App\_Start\\BundleConfig.cs*를 열고 *bootstrap.js* 및 *bootstrap.css*가 들어 있는 줄을 주석으로 처리하세요.</span><span class="sxs-lookup"><span data-stu-id="1062c-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="1062c-175">다음 코드는 변경한 후 `RegisterBundles` 메서드의 마지막 두 문을 보여 줍니다</span><span class="sxs-lookup"><span data-stu-id="1062c-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="1062c-176">`Ctrl+F5` 를 눌러 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="1062c-177">축소 가능한 탐색 표시줄이 이제 일반적인 순서 없는 목록일 뿐인 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="1062c-178">**태그로 찾아보기**를 다시 클릭하고 **ASP.NET**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="1062c-179">모바일 에뮬레이터 뷰에서 이제 더 이상 화면에 맞게 크기가 조정되지 않는 것을 볼 수 있으며, 표의 오른쪽을 보려면 옆쪽으로 스크롤해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="1062c-180">변경 내용을 실행 취소하고 모바일 브라우저를 새로 고쳐, 모바일 친화적인 디스플레이가 복원되었는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="1062c-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="1062c-181">Bootstrap은 ASP.NET MVC 5 전용이 아니므로 어떤 웹 응용 프로그램에서나 이 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="1062c-182">하지만 이제는 ASP.NET MVC 5 프로젝트 템플릿에 기본 제공되므로 MVC 5 웹 응용 프로그램은 Bootstrap을 기본적으로 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="1062c-183">부트스트랩에 대한 자세한 내용을 보려면 [부트스트랩][BootstrapSite] 사이트로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="1062c-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="1062c-184">다음 섹션에서는 모바일 브라우저 전용 뷰를 제공하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="1062c-185"><a name="bkmk_overrideviews"></a> 뷰, 레이아웃 및 부분 뷰 재정의</span><span class="sxs-lookup"><span data-stu-id="1062c-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="1062c-186">일반적인 모바일 브라우저, 개별 모바일 브라우저 또는 특정 브라우저용 뷰(레이아웃 및 부분 뷰 포함)를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="1062c-187">모바일 전용 뷰를 제공하기 위해 뷰 파일을 복사하여 파일 이름에 *.Mobile* 을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="1062c-188">예를 들어, 모바일 *인덱스* 뷰를 만들려면 *Views\\Home\\Index.cshtml*을 *Views\\Home\\Index.Mobile.cshtml*로 복사하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="1062c-189">이 섹션에서는 모바일 전용 레이아웃 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="1062c-190">시작하려면 *Views\\Shared\\\_Layout.cshtml*을 *Views\\Shared\\\_Layout.Mobile.cshtml*로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="1062c-191">*\_Layout.Mobile.cshtml*을 열고 제목을 **MVC5 응용 프로그램**에서 **MVC5 응용 프로그램(모바일)**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="1062c-192">탐색 모음에 대한 각 `Html.ActionLink` 호출에서 각 링크 *ActionLink*에서 "Browse by"를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="1062c-193">다음 코드는 모바일 레이아웃 파일의 완성된 `<ul class="nav navbar-nav">` 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="1062c-194">*Views\\Home\\AllTags.cshtml* 파일을 *Views\\Home\\AllTags.Mobile.cshtml*로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="1062c-195">새 파일을 열고 `<h2>` 요소를 "Tags"에서 "Tags (M)"으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="1062c-196">데스크톱 브라우저와 모바일 브라우저 에뮬레이터를 사용하여 태그 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="1062c-197">모바일 브라우저 에뮬레이터에 두 가지 변경 내용이 표시됩니다(*\_Layout.Mobile.cshtml*에서 변경된 제목 및 *AllTags.Mobile.cshtml*에서 변경된 제목).</span><span class="sxs-lookup"><span data-stu-id="1062c-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="1062c-198">반대로 데스크톱 화면은 변경되지 않았습니다(*\_Layout.cshtml* 및 *AllTags.cshtml*의 제목 그대로).</span><span class="sxs-lookup"><span data-stu-id="1062c-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="1062c-199"><a name="bkmk_browserviews"></a> 브라우저 전용 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="1062c-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="1062c-200">모바일 전용 및 데스크톱 전용 뷰 외에도 개별 브라우저를 위한 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="1062c-201">예를 들어 iPhone 또는 Android 브라우저 전용의 뷰를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="1062c-202">이 섹션에서는 iPhone 브라우저를 위한 레이아웃과 iPhone 버전의 *AllTags* 뷰를 만들어 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="1062c-203">*Global.asax* 파일을 열고 `Application_Start` 메서드의 맨 아래에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="1062c-204">이 코드는 각 수신 요청에 맞출 "iPhone"이라는 새로운 디스플레이 모드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="1062c-205">수신 요청이 정의된 조건과 일치하는 경우(즉, 사용자 에이전트가 "iPhone" 문자열을 포함하는 경우) ASP.NET MVC는 이름에 "iPhone" 접미사가 들어 있는 뷰를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="1062c-206">iPhone 및 Android와 같은 모바일 브라우저 전용 디스플레이 모드를 추가할 때는 브라우저 전용 모드가 모바일 템플릿(*.Mobile.cshtml)보다 우선적으로 적용되도록 첫 번째 인수를 `0`으로 설정해야 합니다(목록 맨 위에 삽입).</span><span class="sxs-lookup"><span data-stu-id="1062c-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="1062c-207">반대로 모바일 템플릿이 목록의 맨 위에 있으면 의도한 디스플레이 모드가 아니라 해당 모바일 템플릿이 선택됩니다(첫 번째 일치 항목이 적용되는데 모바일 템플릿은 모든 모바일 브라우저와 일치함).</span><span class="sxs-lookup"><span data-stu-id="1062c-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="1062c-208">코드에서 `DefaultDisplayMode`를 마우스 오른쪽 단추로 클릭하고 **확인**을 선택한 다음 `using System.Web.WebPages;`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="1062c-209">그러면 `System.Web.WebPages` 네임스페이스에 참조가 추가되고, 여기에서 `DisplayModeProvider` 및 `DefaultDisplayMode` 유형이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="1062c-210">또는 파일의 `using` 섹션에 다음 줄을 직접 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="1062c-211">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-211">Save the changes.</span></span> <span data-ttu-id="1062c-212">*Views\\Shared\\\_Layout.Mobile.cshtml* 파일을 *Views\\Shared\\\_Layout.iPhone.cshtml*에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="1062c-213">새 파일을 연 후에 제목을 `MVC5 Application (Mobile)`에서 `MVC5 Application (iPhone)`으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="1062c-214">*Views\\Home\\AllTags.Mobile.cshtml* 파일을 *Views\\Home\\AllTags.iPhone.cshtml*로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="1062c-215">새 파일에서 `<h2>` 요소를 "Tags (M)"에서 "Tags (iPhone)"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="1062c-216">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-216">Run the application.</span></span> <span data-ttu-id="1062c-217">모바일 브라우저 에뮬레이터를 실행하고, 사용자 에이전트가 "iPhone"으로 설정되었는지 확인하고, *AllTags* 뷰로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="1062c-218">Internet Explorer 11 F12 개발자 도구에서 에뮬레이터를 사용 중인 경우 에뮬레이션을 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="1062c-219">브라우저 프로필 = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="1062c-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="1062c-220">사용자 에이전트 문자열 = **Custom**</span><span class="sxs-lookup"><span data-stu-id="1062c-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="1062c-221">사용자 지정 문자열 = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="1062c-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="1062c-222">다음 스크린샷은 Internet Explorer 11 F12 개발자 도구에서 에뮬레이터에 렌더링된 *AllTags* 뷰와 사용자 지정 사용자 에이전트 문자열(iPhone 5C 사용자 에이전트 문자열임)을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="1062c-223">모바일 브라우저에서 **Speakers** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="1062c-224">모바일 뷰(*AllSpeakers.Mobile.cshtml*)가 없으므로 기본 발표자 뷰(*AllSpeakers.cshtml*)는 모바일 레이아웃 뷰(*\_Layout.Mobile.cshtml*)를 사용하여 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="1062c-225">아래와 같이 **MVC5 응용 프로그램(모바일)**이라는 제목이 *\_Layout.Mobile.cshtml*에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="1062c-226">다음과 같이 *Views\\\_ViewStart.cshtml* 파일에서 `RequireConsistentDisplayMode`를 `true`로 설정하여 모바일 레이아웃 내에서 기본(모바일 아님) 뷰가 렌더링되지 않도록 전체적으로 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="1062c-227">`RequireConsistentDisplayMode`이(가) `true`(으)로 설정되면 모바일 레이아웃(*\_Layout.Mobile.cshtml*)이 모바일 뷰에 대해서만 사용됩니다(예: 뷰 파일이 ***ViewName**.Mobile.cshtml* 형식일 때).</span><span class="sxs-lookup"><span data-stu-id="1062c-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="1062c-228">모바일 뷰가 아닌 뷰에서 모바일 레이아웃이 제대로 작동하지 않을 때 `RequireConsistentDisplayMode`를 `true`로 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="1062c-229">아래의 스크린샷은 `RequireConsistentDisplayMode`가 `true`로 설정되어 있을 때 *발표자* 페이지가 어떻게 렌더링되는 지를 보여줍니다(맨 위의 탐색 표시줄에 "(Mobile)" 문자열이 없음).</span><span class="sxs-lookup"><span data-stu-id="1062c-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="1062c-230">뷰 파일에서 `RequireConsistentDisplayMode`를 `false`로 설정하여 특정 뷰의 일관된 디스플레이 모드를 비활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="1062c-231">*Views\\Home\\AllSpeakers.cshtml* 파일의 다음 태그는 `RequireConsistentDisplayMode`를 `false`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="1062c-232">이 섹션에서는 모바일 레이아웃 및 뷰를 만드는 방법과 iPhone과 같은 특정 장치용의 레이아웃 및 뷰를 만드는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="1062c-233">그러나 부트스트랩 CSS 프레임워크의 주요 이점은 반응형 레이아웃입니다. 이 레이아웃을 통해 데스크톱, 전화 및 태블릿 브라우저에 걸쳐 단일 스타일 시트를 적용하여 일관된 모양과 느낌을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="1062c-234">다음 섹션에서는 Bootstrap을 활용하여 모바일 친화적인 뷰를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="1062c-235"><a name="bkmk_Improvespeakerslist"></a> 발표자 목록 개선</span><span class="sxs-lookup"><span data-stu-id="1062c-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="1062c-236">방금 본 것처럼 *발표자* 뷰는 가독성은 있지만 링크가 작고 모바일 장치에서 누르기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="1062c-237">이 섹션에서는 *AllSpeakers* 뷰를 모바일 친화적으로 만듭니다. 크고 누르기 쉬운 링크를 표시하고 발표자를 빨리 찾을 수 있는 검색 상자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="1062c-238">부트스트랩 [연결된 목록 그룹][linked list group] 스타일을 사용하여 *발표자* 뷰를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="1062c-239">*Views\\Home\\AllSpeakers.cshtml*에서 Razor 파일의 내용을 아래의 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

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

<span data-ttu-id="1062c-240">`<div>` 태그의 `class="list-group"` 속성은 Bootstrap 목록 항목 스타일을 적용하고 `class="input-group-item"` 속성은 각 링크에 Bootstrap 목록 스타일을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="1062c-241">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-241">Refresh the mobile browser.</span></span> <span data-ttu-id="1062c-242">업데이트된 뷰는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="1062c-243">부트스트랩 [연결된 목록 그룹][linked list group] 스타일은 각 링크의 전체 상자를 클릭 가능한 상태로 만들어서 사용자 환경을 더욱 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="1062c-244">데스크톱 뷰로 전환해도 일관된 모양과 느낌이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="1062c-245">모바일 브라우저 뷰가 개선되기는 했지만 긴 발표자 목록을 탐색하기가 힘듭니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="1062c-246">부트스트랩은 바로 사용 가능한 검색 필터 기능을 제공하지 않지만, 코드 몇 줄을 사용하여 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="1062c-247">먼저 검색 상자를 뷰에 추가한 후에 JavaScript 코드를 연결하여 필터 기능을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="1062c-248">*Views\\Home\\AllSpeakers.cshtml*에서 다음과 같이 \<form\> 태그를 \<h2\> 태그 바로 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="1062c-249">`<form>` 및 `<input>` 태그 모두에 Bootstrap 스타일이 적용되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="1062c-250">`<span>` 요소는 Bootstrap [glyphicon][glyphicon]을 검색 상자에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="1062c-251">*Scripts* 폴더에서 *filter.js*라는 JavaScript 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="1062c-252">파일을 열고 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
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

<span data-ttu-id="1062c-253">또한 등록된 번들에 filter.js를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="1062c-254">*App\_Start\\BundleConfig.cs*를 열고 첫 번째 번들을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="1062c-255">첫 번째 `bundles.Add` 문(**jquery** 번들에 해당)을 변경하여 다음과 같이 *Scripts\\filter.js*를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="1062c-256">**jquery** 번들은 이미 기본 *\_Layout* 뷰에 렌더링되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="1062c-257">나중에 같은 JavaScript 코드를 활용하여 필터 기능을 다른 목록 뷰에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="1062c-258">모바일 브라우저를 새로 고치고 *AllSpeakers* 뷰로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="1062c-259">검색 상자에 "sc"를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-259">In the search box, type "sc".</span></span> <span data-ttu-id="1062c-260">이제 검색 문자열에 따라 발표자 목록을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="1062c-261"><a name="bkmk_improvetags"></a> 태그 목록 개선</span><span class="sxs-lookup"><span data-stu-id="1062c-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="1062c-262">*발표자* 뷰처럼 *태그* 뷰도 가독성은 있지만 링크가 작고 모바일 장치에서 누르기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="1062c-263">*발표자* 뷰를 수정한 것과 같은 방법으로 *태그* 뷰를 수정할 수 있습니다. 앞에서 설명한 대로 코드를 변경하되 *Views\\Home\\AllTags.cshtml*에서 다음 `Html.ActionLink` 메서드 구문을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="1062c-264">새로 고친 데스크톱 브라우저는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="1062c-265">그리고 새로 고친 모바일 브라우저는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="1062c-266">모바일 브라우저에서 원래의 목록 형식이 그대로 있고, 보기 좋았던 Bootstrap 스타일이 사라진 것이 눈에 띌 것입니다. 이것은 앞서 모바일 전용 뷰를 만들었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="1062c-267">하지만 이제는 부트스트랩 CSS 프레임워크를 사용하여 반응형 웹 디자인을 만드는 것이기 때문에 모바일 전용 뷰와 모바일 전용 레이아웃 뷰를 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="1062c-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="1062c-268">그러면 새로 고친 모바일 브라우저에 Bootstrap 스타일이 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="1062c-269"><a name="bkmk_improvedates"></a> 날짜 목록 개선</span><span class="sxs-lookup"><span data-stu-id="1062c-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="1062c-270">*스피커* 및 *태그* 뷰를 개선한 것과 같이 *날짜* 뷰를 개선할 수 있습니다. 앞에서 설명한 대로 코드를 변경하되 *Views\\Home\\AllDates.cshtml*에서 다음 `Html.ActionLink` 메서드 구문을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="1062c-271">새로 고친 모바일 브라우저 뷰는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="1062c-272">날짜-시간 값을 날짜별로 정리함으로써 *날짜* 뷰를 더욱 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="1062c-273">부트스트랩 [패널][panels] 스타일을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="1062c-274">*Views\\Home\\AllDates.cshtml* 파일 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="1062c-275">이 코드는 목록에 있는 각 개별 날짜에 대해 별도의 `<div class="panel panel-primary">` 태그를 만들고 앞서와 마찬가지로 해당 링크에 [연결된 목록 그룹][linked list group]을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="1062c-276">이 코드를 실행하면 모바일 브라우저가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="1062c-277">데스크톱 브라우저로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-277">Switch to the desktop browser.</span></span> <span data-ttu-id="1062c-278">이번에도 일관된 모양을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="1062c-279"><a name="bkmk_improvesessionstable"></a> SessionsTable 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="1062c-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="1062c-280">이 섹션에서는 *SessionsTable* 뷰를 보다 모바일 친화적으로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="1062c-281">앞서의 경우보다 변화의 폭이 더 큽니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="1062c-282">모바일 브라우저에서 **태그** 단추를 누르고 검색 상자에 `asp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="1062c-283">**ASP.NET** 링크를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="1062c-284">보시다시피 표 형태로 표시됩니다. 현재는 데스크톱 브라우저에서 보도록 디자인된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="1062c-285">하지만 모바일 브라우저에서는 읽기가 약간 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="1062c-286">이를 수정하기 위해 *Views\\Home\\SessionsTable.cshtml*을 열고 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

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

<span data-ttu-id="1062c-287">이 코드는 세 가지 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-287">The code does 3 things:</span></span>

* <span data-ttu-id="1062c-288">부트스트랩 [사용자 지정 연결된 목록 그룹][custom linked list group]을 사용하여 세션 정보를 세로 형태로 정리하여 이 모든 정보를 모바일 브라우저에서 읽을 수 있게 됩니다(list-group-item-text 등의 클래스 사용).</span><span class="sxs-lookup"><span data-stu-id="1062c-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="1062c-289">[그리드 시스템][grid system]을 레이아웃에 적용하여 세션 항목이 데스크톱 브라우저에서 가로 방향으로 흐르고 모바일 브라우저에서는 세로 방향으로 흐르도록 합니다(col-md-4 클래스 사용).</span><span class="sxs-lookup"><span data-stu-id="1062c-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="1062c-290">모바일 브라우저에서 볼 때 [응답성이 뛰어난 유틸리티][responsive utilities]를 사용하여 세션 태그를 숨깁니다(hidden-xs 클래스 사용).</span><span class="sxs-lookup"><span data-stu-id="1062c-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="1062c-291">제목 링크를 눌러 해당 세션으로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="1062c-292">아래 이미지는 코드 변경 내용이 반영된 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1062c-293">자동으로 적용한 Bootstrap 그리드 시스템은 모바일 브라우저에서 세션을 세로로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="1062c-294">또한 태그가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="1062c-295">데스크톱 브라우저로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="1062c-296">데스크톱 브라우저에서는 태그가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="1062c-297">또한 적용한 부트스트랩 그리드 시스템이 세션 항목을 두 개의 열로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="1062c-298">브라우저를 확대하면 세 개의 열로 정렬되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="1062c-299"><a name="bkmk_improvesessionbycode"></a> SessionByCode 뷰 개선</span><span class="sxs-lookup"><span data-stu-id="1062c-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="1062c-300">마지막으로, *SessionByCode* 뷰를 모바일 친화적으로 수정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="1062c-301">모바일 브라우저에서 **태그** 단추를 누르고 검색 상자에 `asp`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="1062c-302">**ASP.NET** 링크를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="1062c-303">ASP.NET 태그의 세션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="1062c-304">**ASP.NET 및 AngularJS로 단일 페이지 응용 프로그램 만들기** 링크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="1062c-305">기본 데스크톱 뷰도 좋지만 몇 가지 Bootstrap GUI 구성 요소를 사용하여 이 뷰를 쉽게 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="1062c-306">*Views\\Home\\SessionByCode.cshtml*을 열고 내용을 다음 태그로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

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

<span data-ttu-id="1062c-307">새 태그는 Bootstrap 패널 스타일을 사용하여 모바일 뷰를 개선합니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="1062c-308">모바일 브라우저를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-308">Refresh the mobile browser.</span></span> <span data-ttu-id="1062c-309">다음 이미지는 방금 변경한 코드가 반영된 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="1062c-310">요약 및 검토</span><span class="sxs-lookup"><span data-stu-id="1062c-310">Wrap Up and Review</span></span>
<span data-ttu-id="1062c-311">이 자습서에서는 ASP.NET MVC 5를 사용하여 모바일 친화적인 웹 응용 프로그램을 개발하는 방법을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="1062c-312">내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1062c-312">These include:</span></span>

* <span data-ttu-id="1062c-313">앱 서비스 웹 앱에 ASP.NET MVC 5 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="1062c-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="1062c-314">MVC 5 응용 프로그램에서 Bootstrap을 사용하여 반응형 웹 레이아웃 만들기</span><span class="sxs-lookup"><span data-stu-id="1062c-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="1062c-315">모든 뷰에 대해 그리고 개별 뷰에 대해 레이아웃, 뷰 및 부분 뷰 재정의</span><span class="sxs-lookup"><span data-stu-id="1062c-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="1062c-316">`RequireConsistentDisplayMode` 속성을 사용하여 레이아웃 및 부분 재정의 작업 제어</span><span class="sxs-lookup"><span data-stu-id="1062c-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="1062c-317">iPhone 브라우저 등 특정 브라우저를 대상으로 하는 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="1062c-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="1062c-318">Razor 코드에서 Boostrap 스타일 적용</span><span class="sxs-lookup"><span data-stu-id="1062c-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="1062c-319">참고 항목</span><span class="sxs-lookup"><span data-stu-id="1062c-319">See Also</span></span>
* [<span data-ttu-id="1062c-320">반응형 웹 디자인의 9가지 기본 원칙</span><span class="sxs-lookup"><span data-stu-id="1062c-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="1062c-321">[부트스트랩][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="1062c-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="1062c-322">[공식 부트스트랩 블로그][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="1062c-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="1062c-323">[Tutorial Republic의 Twitter 부트스트랩 자습서][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="1062c-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="1062c-324">[부트스트랩 실습][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="1062c-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="1062c-325">[W3C 권장 사항 모바일 웹 응용 프로그램 모범 사례][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="1062c-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="1062c-326">[미디어 쿼리에 대한 W3C 권장 사항][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="1062c-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1062c-327">변경된 내용</span><span class="sxs-lookup"><span data-stu-id="1062c-327">What's changed</span></span>
* <span data-ttu-id="1062c-328">웹 사이트에서 앱 서비스로의 변경에 대한 지침은 [Azure 앱 서비스와 이 서비스가 기존 Azure 서비스에 미치는 영향](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1062c-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

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
[The Bootstrap Playground]: http://www.bootply.com/
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

