---
title: "Windows Phone Silverlight Engagement SDK 통합"
description: "Windows Phone Silverlight 앱에서 Azure Mobile Engagement를 통합하는 방법"
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
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="2b5f3-103">Windows Phone Silverlight Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="2b5f3-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2b5f3-104">Windows 범용</span><span class="sxs-lookup"><span data-stu-id="2b5f3-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="2b5f3-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2b5f3-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="2b5f3-106">iOS</span><span class="sxs-lookup"><span data-stu-id="2b5f3-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="2b5f3-107">Android</span><span class="sxs-lookup"><span data-stu-id="2b5f3-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="2b5f3-108">이 절차에서는 Windows Phone Silverlight 응용 프로그램에서 Azure Mobile Engagement의 분석 및 모니터링 기능을 활성화하는 가장 간단한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="2b5f3-109">다음 단계만 수행하면 사용자, 세션, 활동, 작동 중단 및 기술과 관련된 모든 통계를 계산하는 데 필요한 로그 보고를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="2b5f3-110">이벤트, 오류, 작업 등의 기타 통계는 응용 프로그램별로 다르므로, 해당 통계를 계산하는 데 필요한 로그 보고는 Engagement API를 사용하여 수동으로 수행해야 합니다. 관련 설명은 아래의 [Windows Phone Silverlight 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-windows-phone-use-engagement-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="2b5f3-111">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="2b5f3-111">Supported versions</span></span>
<span data-ttu-id="2b5f3-112">Windows Silverlight용 Mobile Engagement SDK는 다음을 대상으로 하는 응용 프로그램에만 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="2b5f3-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="2b5f3-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="2b5f3-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="2b5f3-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="2b5f3-115">Windows Phone 8.1(비 Silverlight)을 대상으로 하는 경우 [Windows 범용](mobile-engagement-windows-store-integrate-engagement.md)통합 절차를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="2b5f3-116">Mobile Engagement Silverlight SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="2b5f3-117">Windows Silverlight용 Mobile Engagement SDK는 *MicrosoftAzure.MobileEngagement*로 불리는 Nuget 패키지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="2b5f3-118">Visual Studio Nuget 패키지 관리자에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="2b5f3-119">기능 추가</span><span class="sxs-lookup"><span data-stu-id="2b5f3-119">Add the capabilities</span></span>
<span data-ttu-id="2b5f3-120">Engagement SDK가 올바르게 작동하려면 Windows Phone Silverlight SDK의 일부 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="2b5f3-121">먼저 `WMAppManifest.xml` 파일을 열고 다음 기능이 `Capabilities` 패널에 선언되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="2b5f3-122">Engagement SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="2b5f3-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="2b5f3-123">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="2b5f3-123">Engagement configuration</span></span>
<span data-ttu-id="2b5f3-124">Engagement 구성은 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 중앙 집중식으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="2b5f3-125">이 파일을 편집하여 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-125">Edit this file to specify :</span></span>

* <span data-ttu-id="2b5f3-126">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="2b5f3-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="2b5f3-127">이 문자열을 런타임에 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="2b5f3-128">응용 프로그램의 연결 문자열은 Azure 클래식 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="2b5f3-129">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="2b5f3-129">Engagement initialization</span></span>
<span data-ttu-id="2b5f3-130">새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="2b5f3-131">이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="2b5f3-132">Engagement SDK를 초기화할 때도 이 클래스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="2b5f3-133">`App.xaml.cs`파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="2b5f3-134">`using` 구문에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="2b5f3-135">`EngagementAgent.Instance.Init`을(를) `Application_Launching` 메서드에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="2b5f3-136">`EngagementAgent.Instance.OnActivated`을(를) `Application_Activated` 메서드에 삽입합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="2b5f3-137">응용 프로그램의 다른 위치에는 Engagement 초기화를 추가하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="2b5f3-138">그러나 `EngagementAgent.Instance.Init` 메서드는 UI 스레드가 아닌 전용 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="2b5f3-139">기본 보고</span><span class="sxs-lookup"><span data-stu-id="2b5f3-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="2b5f3-140">권장 방법: `PhoneApplicationPage` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="2b5f3-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="2b5f3-141">Engagement에서 사용자, 세션, 활동, 작동 중단 및 기술 통계를 계산하는 데 필요한 모든 로그의 보고를 활성화하려는 경우 모든 `PhoneApplicationPage` 서브클래스가 `EngagementPage` 클래스에서 상속하도록 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="2b5f3-142">아래에는 응용 프로그램 페이지에 대해 이 작업을 수행하는 방법의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="2b5f3-143">응용 프로그램의 모든 페이지에 대해 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="2b5f3-144">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="2b5f3-144">C# Source file</span></span>
<span data-ttu-id="2b5f3-145">페이지 `.xaml.cs` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="2b5f3-146">`using` 구문에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="2b5f3-147">`PhoneApplicationPage`을(를) `EngagementPage`(으)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="2b5f3-148">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="2b5f3-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="2b5f3-149">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="2b5f3-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="2b5f3-150">페이지가 `OnNavigatedTo` 메서드에서 상속하는 경우에는 `base.OnNavigatedTo(e)` 호출을 허용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="2b5f3-151">그렇지 않으면 활동이 보고되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="2b5f3-152">실제로 `EngagementPage`은(는) `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="2b5f3-153">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="2b5f3-153">XAML file</span></span>
<span data-ttu-id="2b5f3-154">페이지 `.xaml` 파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="2b5f3-155">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="2b5f3-156">`phone:PhoneApplicationPage`을(를) `engagement:EngagementPage`(으)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="2b5f3-157">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="2b5f3-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="2b5f3-158">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="2b5f3-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="2b5f3-159">기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="2b5f3-159">Override the default behavior</span></span>
<span data-ttu-id="2b5f3-160">기본적으로 페이지의 클래스 이름은 extra 없이 활동 이름으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="2b5f3-161">클래스에서 "Page" 접미사를 사용하는 경우에는 해당 접미사도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="2b5f3-162">이름의 기본 동작을 재정의하려면 코드에 다음 코드 조각만 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="2b5f3-163">활동과 함께 추가 정보를 보고하려는 경우에는 코드에 다음 코드 조각을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="2b5f3-164">페이지의 `OnNavigatedTo` 메서드 내에서 이러한 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="2b5f3-165">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="2b5f3-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="2b5f3-166">`PhoneApplicationPage` 클래스를 오버로드할 수 없거나 오버로드하지 않으려는 경우 `EngagementAgent` 메서드를 직접 호출하여 활동을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="2b5f3-167">PhoneApplicationPage 페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="2b5f3-168">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="2b5f3-169">응용 프로그램이 닫힐 때 SDK에서 `EndActivity` 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="2b5f3-170">따라서 사용자 활동이 변경될 때마다 `StartActivity` 메서드를 호출하는 것이 **상당히** 좋으며 `EndActivity` 메서드는 호출하지 **않는** 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="2b5f3-171">이 메서드는 현재 사용자가 응용 프로그램을 떠난 Engagement 서버에 메시지를 보내며 이는 모든 응용 프로그램 로그에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="2b5f3-172">고급 보고</span><span class="sxs-lookup"><span data-stu-id="2b5f3-172">Advanced reporting</span></span>
<span data-ttu-id="2b5f3-173">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고할 수 있습니다. 이렇게 하려면 `EngagementAgent` 클래스에 포함된 다른 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="2b5f3-174">Engagement API에서는 Engagement의 모든 고급 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="2b5f3-175">자세한 내용은 [Windows Phone Silverlight 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-windows-phone-use-engagement-api.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="2b5f3-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="2b5f3-176">고급 구성</span><span class="sxs-lookup"><span data-stu-id="2b5f3-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="2b5f3-177">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="2b5f3-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="2b5f3-178">Engagement의 자동 작동 중단 보고를 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="2b5f3-179">이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="2b5f3-180">이 기능을 사용하지 않도록 설정하려는 경우 앱에서 처리되지 않은 작동 중단이 발생해도 Engagement에서 작동 중단을 전송하지 않으며 **또한** 세션 및 작업도 닫지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="2b5f3-181">자동 작동 중단 보고를 사용하지 않도록 설정하려면 구성을 선언한 방식에 따라 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="2b5f3-182">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="2b5f3-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="2b5f3-183">`<reportCrash>` 및 `</reportCrash>` 태그 간의 작동 중단 보고를 `false`(으)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="2b5f3-184">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="2b5f3-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="2b5f3-185">EngagementConfiguration 개체를 사용하여 작동 중단 보고를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="2b5f3-186">버스트 모드</span><span class="sxs-lookup"><span data-stu-id="2b5f3-186">Burst mode</span></span>
<span data-ttu-id="2b5f3-187">기본적으로 Engagement 서비스는 로그를 실시간으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="2b5f3-188">응용 프로그램이 로그를 매우 자주 보고하는 경우에는 로그를 버퍼링한 다음 정기적으로 한꺼번에 보고하는 것이 보다 효율적입니다. 이러한 방식을 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="2b5f3-189">이 방식을 사용하려면 다음 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="2b5f3-190">인수는 **밀리초**단위의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="2b5f3-191">언제든지 실시간 로깅을 다시 활성화하려면 매개 변수를 포함하지 않거나 값을 0으로 설정하여 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="2b5f3-192">버스트 모드를 사용하는 경우 배터리 수명은 약간 길어지지만 Engagement 모니터에 영향을 주게 됩니다. 모든 세션 및 작업 기간이 버스트 임계값으로 반올림되므로 버스트 임계값보다 짧은 세션과 작업은 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="2b5f3-193">30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="2b5f3-194">저장된 로드는 300개 항목으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="2b5f3-195">보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="2b5f3-196">1초보다 짧은 기간으로 버스트 임계값을 구성할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="2b5f3-197">버스트 임계값을 1초보다 짧게 구성하면 SDK에는 오류가 포함된 추적이 표시되며, 값은 자동으로 기본값인 0초로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="2b5f3-198">그러면 SDK에서 실시간 로그 보고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b5f3-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

