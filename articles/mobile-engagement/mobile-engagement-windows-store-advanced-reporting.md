---
title: "MobileApps Engagement를 사용한 Windows 유니버설 고급 보고"
description: "Windows 유니버설 앱과 Azure 모바일 Engagement를 통합하는 방법"
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
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="528bb-103">Windows 유니버설 앱 Engagement SDK의 고급 보고</span><span class="sxs-lookup"><span data-stu-id="528bb-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="528bb-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="528bb-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="528bb-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="528bb-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="528bb-106">iOS</span><span class="sxs-lookup"><span data-stu-id="528bb-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="528bb-107">Android</span><span class="sxs-lookup"><span data-stu-id="528bb-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="528bb-108">이 항목에서는 Windows 유니버설 응용 프로그램에서 추가 보고 시나리오를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="528bb-109">이러한 시나리오에서는 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서에서 만든 앱에 적용하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="528bb-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="528bb-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="528bb-111">이 자습서를 시작하기 전에 먼저 직접적이고 간단한 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 자습서를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="528bb-112">이 자습서에서는 선택할 수 있는 추가 옵션에 관해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="528bb-113">런타임에 Engagement 구성 지정</span><span class="sxs-lookup"><span data-stu-id="528bb-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="528bb-114">Engagement 구성은 [시작](mobile-engagement-windows-store-dotnet-get-started.md) 항목에서 지정한 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 중앙 집중식으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="528bb-115">그렇지만 런타임에 구성을 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="528bb-116">권장 방법: `Page` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="528bb-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="528bb-117">Engagement에서 사용자, 세션, 활동, 작동 중단 및 기술 통계를 계산하는 데 필요한 모든 로그의 보고를 활성화하려는 경우 모든 `Page` 서브클래스가 `EngagementPage` 클래스에서 상속하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="528bb-118">아래에는 응용 프로그램 페이지에 대한 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="528bb-119">응용 프로그램의 모든 페이지에 대해 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="528bb-120">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="528bb-120">C# Source file</span></span>
<span data-ttu-id="528bb-121">페이지 `.xaml.cs` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="528bb-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="528bb-122">`using` 구문에 추가:</span><span class="sxs-lookup"><span data-stu-id="528bb-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="528bb-123">`Page` 및 `EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="528bb-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="528bb-124">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="528bb-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="528bb-125">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="528bb-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="528bb-126">페이지가 `OnNavigatedTo` 메서드를 재정의하는 경우에는 `base.OnNavigatedTo(e)`을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="528bb-127">그렇지 않으면 활동이 보고되지 않습니다. `EngagementPage`는 `OnNavigatedTo` 메서드 내에서 `StartActivity`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="528bb-128">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="528bb-128">XAML file</span></span>
<span data-ttu-id="528bb-129">페이지 `.xaml` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="528bb-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="528bb-130">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="528bb-131">`Page` 및 `engagement:EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="528bb-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="528bb-132">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="528bb-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="528bb-133">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="528bb-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="528bb-134">기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="528bb-134">Override the default behaviour</span></span>
<span data-ttu-id="528bb-135">기본적으로 페이지의 클래스 이름은 extra 없이 활동 이름으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="528bb-136">클래스에서 "Page" 접미사를 사용하는 경우에는 해당 접미사가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="528bb-137">이름에 대한 기본 동작을 재정의하려면 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="528bb-138">사용자 활동에 대한 추가 정보를 보고하려면 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="528bb-139">페이지의 `OnNavigatedTo` 메서드 내에서 이러한 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="528bb-140">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="528bb-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="528bb-141">`Page` 클래스를 오버로드할 수 없거나 오버로드하지 않으려는 경우 `EngagementAgent` 메서드를 직접 호출하여 활동을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="528bb-142">페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`를 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="528bb-143">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="528bb-144">응용 프로그램을 닫을 때 Windows 유니버설 SDK는 `EndActivity` 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="528bb-145">따라서 사용자 활동이 변경될 때마다 `StartActivity` 메서드를 호출하는 것이 **상당히** 좋으며 `EndActivity` 메서드는 호출하지 **않는** 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="528bb-146">이 메서드는 현재 사용자가 응용 프로그램을 떠났음을 Engagement 서버에 알립니다. 이는 모든 응용 프로그램 로그에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="528bb-147">고급 보고</span><span class="sxs-lookup"><span data-stu-id="528bb-147">Advanced reporting</span></span>
<span data-ttu-id="528bb-148">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고할 수 있습니다. 이렇게 하려면 `EngagementAgent` 클래스에 포함된 다른 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="528bb-149">Engagement API에서는 Engagement의 모든 고급 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="528bb-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="528bb-150">자세한 내용은 [Windows 유니버설 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-windows-store-use-engagement-api.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="528bb-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

