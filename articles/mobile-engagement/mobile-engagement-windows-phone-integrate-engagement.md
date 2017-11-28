---
title: "aaaWindows 전화 Silverlight Engagement SDK 통합"
description: "어떻게 tooIntegrate Windows Phone Silverlight 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="337e5-103">Windows Phone Silverlight Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="337e5-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="337e5-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="337e5-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="337e5-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="337e5-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="337e5-106">iOS</span><span class="sxs-lookup"><span data-stu-id="337e5-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="337e5-107">Android</span><span class="sxs-lookup"><span data-stu-id="337e5-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="337e5-108">이 절차에서는 hello 가장 간단한 방법은 tooactivate Azure Mobile Engagement의 분석 및 Windows Phone Silverlight 응용 프로그램의 함수 모니터링을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="337e5-109">단계를 수행 하는 hello 사용자, 세션, 활동, 충돌 및 Technicals에 대 한 모든 통계 toocompute 필요한 충분 한 tooactivate hello 보고서의 로그 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="337e5-110">hello 로그의 필요한 보고서 toocompute 다른 통계 이벤트, 오류 및 작업 수행 해야 hello Engagement API를 사용 하 여 수동으로 처럼 (참조 [어떻게 toouse hello 고급 Windows Phone Silverlight 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md) 아래) 이후이 통계는 응용 프로그램에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="337e5-111">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="337e5-111">Supported versions</span></span>
<span data-ttu-id="337e5-112">hello Windows Silverlight에 대 한 Mobile Engagement SDK 대상으로 응용 프로그램에 통합할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="337e5-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="337e5-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="337e5-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="337e5-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="337e5-115">Windows Phone 8.1 (Silverlight가 아닌) 대상으로 하는 다음이 toohello 참조 [Windows 유니버설 통합 절차](mobile-engagement-windows-store-integrate-engagement.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="337e5-116">Hello Mobile Engagement Silverlight SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="337e5-117">Windows Silverlight에 대 한 Mobile Engagement SDK hello 라는 Nuget 패키지로 사용할 수는 *MicrosoftAzure.MobileEngagement*합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="337e5-118">Hello Visual Studio Nuget 패키지 관리자에서에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="337e5-119">Hello 기능 추가</span><span class="sxs-lookup"><span data-stu-id="337e5-119">Add hello capabilities</span></span>
<span data-ttu-id="337e5-120">hello Engagement SDK 순서 toowork에 hello Windows Phone Silverlight SDK의 일부 기능을 제대로 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="337e5-121">Open 프로그램 `WMAppManifest.xml` 파일 및 기능에 따라 해당 hello hello에 선언 해야 `Capabilities` 패널:</span><span class="sxs-lookup"><span data-stu-id="337e5-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="337e5-122">Hello Engagement SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="337e5-123">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="337e5-123">Engagement configuration</span></span>
<span data-ttu-id="337e5-124">hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="337e5-125">이 파일 toospecify를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="337e5-126">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="337e5-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="337e5-127">런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:</span><span class="sxs-lookup"><span data-stu-id="337e5-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="337e5-128">응용 프로그램에 대 한 연결 문자열 hello hello Azure 클래식 포털에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="337e5-129">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="337e5-129">Engagement initialization</span></span>
<span data-ttu-id="337e5-130">새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="337e5-131">이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="337e5-132">사용 되는 tooinitialize hello Engagement SDK도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="337e5-133">Hello 수정 `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="337e5-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="337e5-134">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="337e5-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="337e5-135">삽입 `EngagementAgent.Instance.Init` hello에 `Application_Launching` 메서드:</span><span class="sxs-lookup"><span data-stu-id="337e5-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="337e5-136">삽입 `EngagementAgent.Instance.OnActivated` hello에 `Application_Activated` 메서드:</span><span class="sxs-lookup"><span data-stu-id="337e5-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="337e5-137">강력 하 게 하면 tooadd hello Engagement 초기화를 응용 프로그램의 다른 장소에 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="337e5-138">그러나 해당 hello `EngagementAgent.Instance.Init` hello UI 스레드가 아닌는 전용된 스레드와 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="337e5-139">기본 보고</span><span class="sxs-lookup"><span data-stu-id="337e5-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="337e5-140">권장 방법: `PhoneApplicationPage` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="337e5-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="337e5-141">Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 순서 tooactivate hello 보고서에서 만들 수 있습니다 모든 프로그램 `PhoneApplicationPage` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="337e5-142">방법의 예로 toodo 응용 프로그램의 페이지에 대 한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="337e5-143">할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="337e5-144">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="337e5-144">C# Source file</span></span>
<span data-ttu-id="337e5-145">페이지 `.xaml.cs` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="337e5-146">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="337e5-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="337e5-147">`PhoneApplicationPage`을(를) `EngagementPage`(으)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="337e5-148">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="337e5-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="337e5-149">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="337e5-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="337e5-150">페이지 hello에서 상속 하는 경우 `OnNavigatedTo` 메서드를 신중 하 게 toolet hello 수 `base.OnNavigatedTo(e)` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="337e5-151">그렇지 않으면 hello 활동 보고 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="337e5-152">실제로, hello `EngagementPage` 호출 하는 중 `StartActivity` hello 내 `OnNavigatedTo` 메서드.</span><span class="sxs-lookup"><span data-stu-id="337e5-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="337e5-153">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="337e5-153">XAML file</span></span>
<span data-ttu-id="337e5-154">페이지 `.xaml` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="337e5-155">Tooyour 네임 스페이스 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="337e5-156">`phone:PhoneApplicationPage`을(를) `engagement:EngagementPage`(으)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="337e5-157">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="337e5-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="337e5-158">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="337e5-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="337e5-159">Hello 기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="337e5-159">Override hello default behavior</span></span>
<span data-ttu-id="337e5-160">기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="337e5-161">Hello 클래스 hello "페이지" 접미사를 사용 하는 경우 서비스 에서도 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="337e5-162">Hello 이름에 대 한 toooverride hello 기본 동작을 수행 하는 경우이 tooyour 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="337e5-163">원하는 tooreport 추가적인 정보를 작업과이 tooyour 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="337e5-164">Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.</span><span class="sxs-lookup"><span data-stu-id="337e5-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="337e5-165">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="337e5-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="337e5-166">처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `PhoneApplicationPage` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="337e5-167">PhoneApplicationPage 페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="337e5-168">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="337e5-169">hello를 자동으로 호출 하는 hello SDK `EndActivity` hello 응용 프로그램을 닫으면 메서드.</span><span class="sxs-lookup"><span data-stu-id="337e5-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="337e5-170">즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드.</span><span class="sxs-lookup"><span data-stu-id="337e5-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="337e5-171">이 메서드는 현재 사용자 hello 남아 서 hello 응용 프로그램 및 모든 응용 프로그램 로그에 영향을 주는 메시지 toohello Engagement 서버를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="337e5-172">고급 보고</span><span class="sxs-lookup"><span data-stu-id="337e5-172">Advanced reporting</span></span>
<span data-ttu-id="337e5-173">필요에 따라 tooreport 응용 프로그램에 대 한 특정 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="337e5-174">hello Engagement API Engagement의 고급 기능을 모두 toouse 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="337e5-175">자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 Windows Phone Silverlight 응용 프로그램에서 API 태그를 지정 하는 Mobile Engagement](mobile-engagement-windows-phone-use-engagement-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="337e5-176">고급 구성</span><span class="sxs-lookup"><span data-stu-id="337e5-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="337e5-177">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="337e5-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="337e5-178">Hello 자동 충돌 보고 서비스의 기능을 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="337e5-179">이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="337e5-180">이 기능은 toodisable을 계획할 경우 처리 되지 않은 충돌, 응용 프로그램에서 발생 한 경우 Engagement hello 크래시 보내지 것입니다 주의 해야 **AND** hello 세션 및 작업 닫히지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="337e5-181">방금 toodisable 자동 충돌 보고에 선언한 hello 방식에 따라 구성을 사용자 지정:</span><span class="sxs-lookup"><span data-stu-id="337e5-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="337e5-182">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="337e5-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="337e5-183">보고서를 너무 충돌 설정`false` 사이 `<reportCrash>` 및 `</reportCrash>` 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="337e5-184">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="337e5-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="337e5-185">보고서 크래시 toofalse EngagementConfiguration 개체를 사용 하 여 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="337e5-186">버스트 모드</span><span class="sxs-lookup"><span data-stu-id="337e5-186">Burst mode</span></span>
<span data-ttu-id="337e5-187">기본적으로 hello Engagement 서비스 보고서는 실시간으로 기록 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="337e5-188">더 나은 toobuffer hello 로그 및 tooreport은 응용 프로그램 로그를 자주 보고 하는 경우는 일반 기본 시간 ("버스트 모드" hello 라는)에서 한 번에 모두 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="337e5-189">따라서 toodo hello 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="337e5-190">hello 인수에는 **밀리초**합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="337e5-191">언제 든 지 tooreactivate hello 실시간 로깅 하려는 경우만 hello 메서드 hello 0 값 또는 모든 매개 변수 없이 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="337e5-192">hello 버스트 모드 약간 증가 hello 배터리 수명 하지만 영향을 주 hello Engagement 모니터: 모든 세션 및 작업 기간 (따라서 세션 및 작업 hello 버스트 임계값 표시 되지 않는 보다 짧은) 둥근된 toohello 버스트 임계값도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="337e5-193">toouse 30000 (30 초) 보다 버스트 임계값 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="337e5-194">Toobe 제한 too300 항목이 저장 된 로그를 인식 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="337e5-195">보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="337e5-196">hello 버스트 임계값을 구성할 수 없습니다 tooa 기간이 더 적은 보다 1 초입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="337e5-197">Hello SDK hello 오류와 함께 추적 표시 되며가 자동으로 toohello 기본값 다시 설정 하므로 toodo를 시도 하면, 즉 0 초입니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="337e5-198">이렇게 하면 hello SDK tooreport hello 로그를 실시간으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="337e5-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

