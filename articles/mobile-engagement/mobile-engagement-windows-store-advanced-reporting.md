---
title: "aaaWindows MobileApps Engagement와 유니버설 고급 보고"
description: "어떻게 tooIntegrate Windows 유니버설 앱과 함께 Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="280df-103">Hello Windows 유니버설 앱 Engagement SDK와의 고급 보고</span><span class="sxs-lookup"><span data-stu-id="280df-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="280df-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="280df-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="280df-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="280df-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="280df-106">iOS</span><span class="sxs-lookup"><span data-stu-id="280df-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="280df-107">Android</span><span class="sxs-lookup"><span data-stu-id="280df-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="280df-108">이 항목에서는 Windows 유니버설 응용 프로그램에서 추가 보고 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="280df-109">이러한 시나리오 tooapply toohello hello에서 만든 응용 프로그램을 선택할 수 있는 옵션을 포함할 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="280df-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="280df-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="280df-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="280df-111">이 자습서를 시작 하기 전에 먼저 완료 해야 hello [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서는 의도적으로 직접와 단순입니다.</span><span class="sxs-lookup"><span data-stu-id="280df-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="280df-112">이 자습서에서는 선택할 수 있는 추가 옵션에 관해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="280df-113">런타임에 Engagement 구성 지정</span><span class="sxs-lookup"><span data-stu-id="280df-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="280df-114">hello에 hello Engagement 구성 한 곳에서 `Resources\EngagementConfiguration.xml` hello에 지정 된 위치는 프로젝트의 파일 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="280df-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="280df-115">런타임 시 지정할 수도 있지만: hello 다음 hello Engagement 에이전트를 초기화 하기 전에 메서드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="280df-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="280df-116">권장 방법: `Page` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="280df-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="280df-117">모든 확인 Engagement toocompute 사용자, 세션, 활동, 충돌 및 기술 통계에 필요한 모든 hello 로그 tooactivate hello 보고 프로그램 `Page` hello에서 하위 클래스 상속 `EngagementPage` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="280df-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="280df-118">아래에는 응용 프로그램 페이지에 대한 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="280df-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="280df-119">할 수 있는 응용 프로그램의 모든 페이지에 대해 동일한 작업 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="280df-120">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="280df-120">C# Source file</span></span>
<span data-ttu-id="280df-121">페이지 `.xaml.cs` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="280df-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="280df-122">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="280df-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="280df-123">`Page` 및 `EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="280df-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="280df-124">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="280df-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="280df-125">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="280df-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="280df-126">페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="280df-127">그렇지 않으면 hello 활동 보고 되지 않습니다 (hello `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드).</span><span class="sxs-lookup"><span data-stu-id="280df-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="280df-128">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="280df-128">XAML file</span></span>
<span data-ttu-id="280df-129">페이지 `.xaml` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="280df-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="280df-130">Tooyour 네임 스페이스 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="280df-131">`Page` 및 `engagement:EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="280df-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="280df-132">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="280df-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="280df-133">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="280df-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="280df-134">Hello 기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="280df-134">Override hello default behaviour</span></span>
<span data-ttu-id="280df-135">기본적으로 hello 페이지의 hello 클래스 이름은 추가 된 hello 활동 이름으로 보고 됩니다.</span><span class="sxs-lookup"><span data-stu-id="280df-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="280df-136">Hello 클래스 hello "페이지" 접미사를 사용 하면 계약으로 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="280df-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="280df-137">이 코드를 추가 하는 hello 이름에 대 한 toooverride hello 기본 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="280df-138">tooreport이이 코드를 추가 하 여 활동을 사용 하 여 추가 정보:</span><span class="sxs-lookup"><span data-stu-id="280df-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="280df-139">Hello 내에서 이러한 메서드를 호출 `OnNavigatedTo` 페이지의 메서드.</span><span class="sxs-lookup"><span data-stu-id="280df-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="280df-140">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="280df-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="280df-141">처리할 수 없거나 toooverload 하지 않을 경우 프로그램 `Page` 클래스, 호출 하 여 작업을 시작 대신 `EngagementAgent` 메서드를 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="280df-142">페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`를 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="280df-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="280df-143">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="280df-144">hello를 자동으로 호출 하는 Windows 유니버설 SDK hello `EndActivity` hello 응용 프로그램을 닫으면 메서드.</span><span class="sxs-lookup"><span data-stu-id="280df-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="280df-145">즉, **항상** toocall hello 권장 `StartActivity` hello 사용자의 hello 활동 변경 될 때마다 메서드 및 너무**NEVER** 호출 hello `EndActivity` 메서드.</span><span class="sxs-lookup"><span data-stu-id="280df-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="280df-146">이 메서드 hello 현재 사용자에는 모든 응용 프로그램 로그에 영향을 주는 hello 응용 프로그램 없어진 hello Engagement 서버를에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="280df-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="280df-147">고급 보고</span><span class="sxs-lookup"><span data-stu-id="280df-147">Advanced reporting</span></span>
<span data-ttu-id="280df-148">필요에 따라 tooreport 응용 프로그램별 이벤트, 오류 및 작업, toodo를 지금 사용할 수 있습니다, 사용 하 여 hello hello에서 메서드를 찾을 다른 `EngagementAgent` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="280df-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="280df-149">hello Engagement API 모든 Engagement의 고급 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="280df-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="280df-150">자세한 내용은 참조 하십시오. [어떻게 toouse hello 고급 API Windows 유니버설 앱에 태그 지정 Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="280df-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

