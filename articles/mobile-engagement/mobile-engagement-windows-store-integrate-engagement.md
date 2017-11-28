---
title: "aaaWindows 유니버설 앱 Engagement SDK 통합"
description: "어떻게 tooIntegrate Windows 유니버설 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="b445c-103">Windows 유니버설 앱 Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="b445c-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b445c-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="b445c-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="b445c-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b445c-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="b445c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b445c-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="b445c-107">Android</span><span class="sxs-lookup"><span data-stu-id="b445c-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="b445c-108">이 절차에서는 hello 가장 간단한 방법은 tooactivate Engagement의 분석 및 Windows 유니버설 응용 프로그램의 함수 모니터링을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="b445c-109">단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="b445c-110">hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) 이후 이 통계는 종속 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="b445c-111">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="b445c-111">Supported versions</span></span>
<span data-ttu-id="b445c-112">hello Mobile Engagement SDK에 대 한 Windows 유니버설 앱 Windows 런타임 및 대상으로 하는 유니버설 Windows 플랫폼 응용 프로그램에 통합할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="b445c-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="b445c-113">Windows 8</span></span>
* <span data-ttu-id="b445c-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b445c-114">Windows 8.1</span></span>
* <span data-ttu-id="b445c-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b445c-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="b445c-116">Windows 10(데스크톱 및 모바일 제품군)</span><span class="sxs-lookup"><span data-stu-id="b445c-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="b445c-117">Windows Phone Silverlight 대상으로 하는 다음이 toohello 참조 [Windows Phone Silverlight 통합 절차](mobile-engagement-windows-phone-integrate-engagement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="b445c-118">Hello Mobile Engagement 유니버설 앱 SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="b445c-119">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="b445c-119">All platforms</span></span>
<span data-ttu-id="b445c-120">Mobile Engagement SDK에 대 한 Windows 유니버설 앱 hello 라는 Nuget 패키지로 사용할 수는 *MicrosoftAzure.MobileEngagement*합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="b445c-121">Hello Visual Studio Nuget 패키지 관리자에서에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="b445c-122">Windows 8.x 및 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b445c-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="b445c-123">NuGet hello의 hello SDK 리소스를 자동으로 배포 `Resources` 응용 프로그램 프로젝트의 hello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="b445c-124">Windows 10 유니버설 Windows 플랫폼 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="b445c-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="b445c-125">NuGet은 아직 UWP 응용 프로그램의 hello SDK 리소스를 자동으로 배포 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="b445c-126">NuGet에서 리소스 배포 때까지 수동으로 다시 발생 toodo를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="b445c-127">파일 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="b445c-128">Toohello 수정할 수 있는 위치를 이동 (**x.x.x** 은 설치 하는 계약의 hello 버전): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="b445c-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="b445c-129">끌어서 놓기 hello **리소스** hello Visual Studio에서 프로젝트의 파일 탐색기 toohello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="b445c-130">Visual Studio에서 프로젝트를 선택 하 고 hello 활성화 **모두 표시 파일** hello 위에 아이콘 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="b445c-131">일부 파일 hello 프로젝트에 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-131">Some files are not included in hello project.</span></span> <span data-ttu-id="b445c-132">에 한 번에 마우스 오른쪽 단추로 클릭 hello tooimport **리소스** 폴더 **프로젝트에서 제외** hello에 다른 마우스 오른쪽 단추로 클릭 한 다음 **리소스** 폴더 **포함 프로젝트에서** toore-hello 전체 폴더를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="b445c-133">Hello에서 모든 파일을 **리소스** 폴더는 이제 프로젝트에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="b445c-134">Hello 기능 추가</span><span class="sxs-lookup"><span data-stu-id="b445c-134">Add hello capabilities</span></span>
<span data-ttu-id="b445c-135">hello Engagement SDK 순서 toowork에 hello Windows SDK의 일부 기능을 제대로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="b445c-136">열기 프로그램 `Package.appxmanifest` 파일 및 기능에 따라 해당 hello 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="b445c-137">Hello Engagement SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="b445c-138">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="b445c-138">Engagement configuration</span></span>
<span data-ttu-id="b445c-139">hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="b445c-140">이 파일 toospecify를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="b445c-141">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="b445c-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="b445c-142">런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:</span><span class="sxs-lookup"><span data-stu-id="b445c-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="b445c-143">응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="b445c-144">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="b445c-144">Engagement initialization</span></span>
<span data-ttu-id="b445c-145">새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="b445c-146">이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="b445c-147">사용 되는 tooinitialize hello Engagement SDK도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="b445c-148">Hello 수정 `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="b445c-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="b445c-149">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="b445c-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="b445c-150">모든 호출에 대해 한 번씩 메서드 tooshare hello Engagement 초기화를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="b445c-151">호출 `InitEngagement` hello에 `OnLaunched` 메서드:</span><span class="sxs-lookup"><span data-stu-id="b445c-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="b445c-152">다른 응용 프로그램이 나 hello 명령줄 hello 다음 사용자 지정 체계를 사용 하 여 응용 프로그램이 시작 되 면 `OnActivated` 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="b445c-153">앱이 활성화 될 때에 tooinitiate hello Engagement SDK가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="b445c-154">toodo 따라서 재정의 `OnActivated` 메서드:</span><span class="sxs-lookup"><span data-stu-id="b445c-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="b445c-155">강력 하 게 하면 tooadd hello Engagement 초기화를 응용 프로그램의 다른 장소에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="b445c-156">기본 보고</span><span class="sxs-lookup"><span data-stu-id="b445c-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="b445c-157">권장 방법: `Page` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="b445c-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="b445c-158">Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `Page` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="b445c-159">방법의 예로 toodo 응용 프로그램의 페이지에 대 한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="b445c-160">할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="b445c-161">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="b445c-161">C# Source file</span></span>
<span data-ttu-id="b445c-162">페이지 `.xaml.cs` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="b445c-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="b445c-163">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="b445c-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="b445c-164">`Page` 및 `EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="b445c-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="b445c-165">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="b445c-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="b445c-166">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="b445c-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="b445c-167">페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="b445c-168">그렇지 않으면 hello 활동 보고 되지 것입니다 (hello `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드).</span><span class="sxs-lookup"><span data-stu-id="b445c-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="b445c-169">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="b445c-169">XAML file</span></span>
<span data-ttu-id="b445c-170">페이지 `.xaml` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="b445c-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="b445c-171">Tooyour 네임 스페이스 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="b445c-172">`Page` 및 `engagement:EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="b445c-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="b445c-173">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="b445c-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="b445c-174">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="b445c-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="b445c-175">Hello 기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="b445c-175">Override hello default behaviour</span></span>
<span data-ttu-id="b445c-176">기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="b445c-177">Hello 클래스 hello "페이지" 접미사를 사용 하는 경우 서비스 에서도 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="b445c-178">Hello 이름에 대 한 toooverride hello 기본 동작을 원하는 경우이 tooyour 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="b445c-179">원하는 tooreport 몇 가지 추가 정보를 작업과이 tooyour 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="b445c-180">Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.</span><span class="sxs-lookup"><span data-stu-id="b445c-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="b445c-181">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="b445c-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="b445c-182">처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `Page` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="b445c-183">Toocall 권장 `StartActivity` 내부의 프로그램 `OnNavigatedTo` 페이지의 메서드.</span><span class="sxs-lookup"><span data-stu-id="b445c-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="b445c-184">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="b445c-185">hello를 자동으로 호출 하는 Windows 유니버설 SDK hello `EndActivity` hello 응용 프로그램을 닫으면 메서드.</span><span class="sxs-lookup"><span data-stu-id="b445c-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="b445c-186">즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드에서이 메서드는 전송 tooEngagement 서버가 현재 사용자에 게 leave hello 응용 프로그램, 이렇게 설정이 하면 모든 응용 프로그램 로그에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="b445c-187">고급 보고</span><span class="sxs-lookup"><span data-stu-id="b445c-187">Advanced reporting</span></span>
<span data-ttu-id="b445c-188">필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="b445c-189">hello Engagement API Engagement의 고급 기능을 모두 toouse 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="b445c-190">자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="b445c-191">고급 구성</span><span class="sxs-lookup"><span data-stu-id="b445c-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="b445c-192">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="b445c-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="b445c-193">Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="b445c-194">이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="b445c-195">이 기능은 toodisable을 계획할 경우 처리 되지 않은 충돌, 응용 프로그램에서 발생 한 경우 Engagement hello 크래시 보내지 것입니다 주의 해야 **AND** hello 세션 및 작업을 닫지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="b445c-196">방금 toodisable 자동 충돌 보고에 선언한 hello 방식에 따라 구성을 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="b445c-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="b445c-197">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="b445c-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="b445c-198">보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="b445c-199">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="b445c-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="b445c-200">보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="b445c-201">버스트 모드</span><span class="sxs-lookup"><span data-stu-id="b445c-201">Burst mode</span></span>
<span data-ttu-id="b445c-202">기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="b445c-203">더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우는 일반 기본 시간 ("버스트 모드" hello 라는)에서 한 번에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="b445c-204">따라서 toodo hello 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="b445c-205">hello 인수에는 **밀리초**합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="b445c-206">언제 든 지 tooreactivate hello 실시간 로깅 하려는 경우만 hello 메서드 hello 0 값 또는 모든 매개 변수 없이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="b445c-207">hello 버스트 모드 약간 증가 hello 배터리 수명 하지만 영향을 주 hello Engagement 모니터: 모든 세션 및 작업 기간 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 둥근된 toohello 버스트 임계값도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="b445c-208">toouse 30000 (30 초) 보다 버스트 임계값 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="b445c-209">Toobe 제한 too300 항목이 저장 된 로그를 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="b445c-210">보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="b445c-211">hello 버스트 임계값 1 s 보다 tooa 기간을 구성할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="b445c-212">따라서 toodo를 시도 하면 hello SDK hello 오류와 함께 추적 표시 되며가 자동으로 다시 toohello 기본 값, 즉, 0을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="b445c-213">이렇게 하면 hello SDK tooreport hello 로그를 실시간으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="b445c-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

