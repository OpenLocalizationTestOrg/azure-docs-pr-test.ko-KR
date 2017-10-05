---
title: "Windows 유니버설 앱 Engagement SDK 통합"
description: "Windows 유니버설 앱과 Azure 모바일 Engagement를 통합하는 방법"
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
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="bf3aa-103">Windows 유니버설 앱 Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="bf3aa-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf3aa-104">유니버설 Windows</span><span class="sxs-lookup"><span data-stu-id="bf3aa-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="bf3aa-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="bf3aa-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="bf3aa-106">iOS</span><span class="sxs-lookup"><span data-stu-id="bf3aa-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="bf3aa-107">Android</span><span class="sxs-lookup"><span data-stu-id="bf3aa-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="bf3aa-108">이 절차에서는 Windows 유니버설 응용 프로그램에서 Engagement의 분석 및 모니터링 기능을 활성화하는 가장 간단한 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="bf3aa-109">다음 단계만 수행하면 사용자, 세션, 활동, 작동 중단 및 기술과 관련된 모든 통계를 계산하는 데 필요한 로그 보고를 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="bf3aa-110">이벤트, 오류, 작업 등의 기타 통계는 응용 프로그램별로 다르므로, 해당 통계를 계산하는 데 필요한 로그 보고는 Engagement API를 사용하여 수동으로 수행해야 합니다. 관련 설명은 [Windows 유니버설 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-windows-store-use-engagement-api.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="bf3aa-111">지원되는 버전</span><span class="sxs-lookup"><span data-stu-id="bf3aa-111">Supported versions</span></span>
<span data-ttu-id="bf3aa-112">Windows 유니버설 앱용 Mobile Engagement SDK는 다음을 대상으로 하는 Windows 런타임 및 유니버설 Windows 플랫폼 응용 프로그램에만 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="bf3aa-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="bf3aa-113">Windows 8</span></span>
* <span data-ttu-id="bf3aa-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bf3aa-114">Windows 8.1</span></span>
* <span data-ttu-id="bf3aa-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="bf3aa-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="bf3aa-116">Windows 10(데스크톱 및 모바일 제품군)</span><span class="sxs-lookup"><span data-stu-id="bf3aa-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="bf3aa-117">Windows Phone Silverlight를 대상으로 하는 경우 [Windows Phone Silverlight 통합 절차](mobile-engagement-windows-phone-integrate-engagement.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-117">If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="bf3aa-118">Mobile Engagement 유니버설 Apps SDK 설치</span><span class="sxs-lookup"><span data-stu-id="bf3aa-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="bf3aa-119">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="bf3aa-119">All platforms</span></span>
<span data-ttu-id="bf3aa-120">Windows 유니버설 앱용 Mobile Engagement SDK는 *MicrosoftAzure.MobileEngagement*로 불리는 Nuget 패키지로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="bf3aa-121">Visual Studio Nuget 패키지 관리자에서 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="bf3aa-122">Windows 8.x 및 Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="bf3aa-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="bf3aa-123">NuGet은 응용 프로그램 프로젝트의 루트에 있는 `Resources` 폴더에서 SDK 리소스를 자동으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="bf3aa-124">Windows 10 유니버설 Windows 플랫폼 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="bf3aa-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="bf3aa-125">NuGet이 아직 UWP 응용 프로그램에서 SDK 리소스를 자동으로 배포하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="bf3aa-126">NuGet에서 리소스 배포가 다시 도입될 때까지 수동으로 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="bf3aa-127">파일 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="bf3aa-128">*%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81* 위치로 이동합니다(**x.x.x**는 설치하는 Engagement 버전임).</span><span class="sxs-lookup"><span data-stu-id="bf3aa-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="bf3aa-129">파일 탐색기에서 **Resources** 폴더를 Visual Studio의 프로젝트 루트에 끌어다 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="bf3aa-130">Visual Studio에서 프로젝트를 선택하고 **솔루션 탐색기** 맨 위에서 **모든 파일 표시** 아이콘을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="bf3aa-131">일부 파일이 프로젝트에 포함되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-131">Some files are not included in the project.</span></span> <span data-ttu-id="bf3aa-132">한 번에 가져오려면 **Resources** 폴더를 마우스 오른쪽 단추로 클릭하고 **프로젝트에서 제외**를 클릭한 다음 **Resources** 폴더를 다시 한 번 마우스 오른쪽 단추로 클릭하고 **프로젝트에 포함**을 다시 클릭하여 전체 폴더를 다시 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="bf3aa-133">이제 **Resources** 폴더의 모든 파일이 프로젝트에 포함되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="bf3aa-134">기능 추가</span><span class="sxs-lookup"><span data-stu-id="bf3aa-134">Add the capabilities</span></span>
<span data-ttu-id="bf3aa-135">Engagement SDK가 올바르게 작동하려면 Windows SDK의 일부 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="bf3aa-136">`Package.appxmanifest` 파일을 열고 다음 기능이 선언되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="bf3aa-137">Engagement SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="bf3aa-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="bf3aa-138">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="bf3aa-138">Engagement configuration</span></span>
<span data-ttu-id="bf3aa-139">Engagement 구성은 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 중앙 집중식으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="bf3aa-140">이 파일을 편집하여 다음을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-140">Edit this file to specify:</span></span>

* <span data-ttu-id="bf3aa-141">`<connectionString>` 및 `<\connectionString>` 태그 사이의 응용 프로그램 연결 문자열</span><span class="sxs-lookup"><span data-stu-id="bf3aa-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="bf3aa-142">이 문자열을 런타임에 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="bf3aa-143">응용 프로그램의 연결 문자열은 Azure 클래식 포털에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="bf3aa-144">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="bf3aa-144">Engagement initialization</span></span>
<span data-ttu-id="bf3aa-145">새 프로젝트를 만들 때는 `App.xaml.cs` 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="bf3aa-146">이 클래스는 `Application` 에서 상속하며, 여러 중요 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="bf3aa-147">Engagement SDK를 초기화할 때도 이 클래스가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="bf3aa-148">`App.xaml.cs`파일을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="bf3aa-149">`using` 구문에 추가:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="bf3aa-150">모든 호출에 대해 한 번씩 Engagement 초기화를 공유하도록 메서드를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="bf3aa-151">`OnLaunched` 메서드에서 `InitEngagement`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="bf3aa-152">사용자 지정 체계, 다른 응용 프로그램 또는 명령줄을 사용하여 응용 프로그램을 시작하면 `OnActivated` 메서드가 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="bf3aa-153">또한 앱을 활성화할 때 Engagement SDK를 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="bf3aa-154">이렇게 하려면 `OnActivated` 메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="bf3aa-155">응용 프로그램의 다른 위치에는 Engagement 초기화를 추가하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-155">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="bf3aa-156">기본 보고</span><span class="sxs-lookup"><span data-stu-id="bf3aa-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="bf3aa-157">권장 방법: `Page` 클래스 오버로드</span><span class="sxs-lookup"><span data-stu-id="bf3aa-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="bf3aa-158">Engagement에서 사용자, 세션, 활동, 작동 중단 및 기술 통계를 계산하는 데 필요한 모든 로그의 보고를 활성화하려는 경우 모든 `Page` 서브클래스가 `EngagementPage` 클래스에서 상속하도록 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="bf3aa-159">아래에는 응용 프로그램 페이지에 대해 이 작업을 수행하는 방법의 예제가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="bf3aa-160">응용 프로그램의 모든 페이지에 대해 동일한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="bf3aa-161">C# 소스 파일</span><span class="sxs-lookup"><span data-stu-id="bf3aa-161">C# Source file</span></span>
<span data-ttu-id="bf3aa-162">페이지 `.xaml.cs` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="bf3aa-163">`using` 구문에 추가:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="bf3aa-164">`Page` 및 `EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="bf3aa-165">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="bf3aa-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="bf3aa-166">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="bf3aa-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="bf3aa-167">페이지가 `OnNavigatedTo` 메서드를 재정의하는 경우에는 `base.OnNavigatedTo(e)`을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-167">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="bf3aa-168">그렇지 않으면 활동이 보고되지 않습니다. `EngagementPage`은(는) `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-168">Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="bf3aa-169">XAML 파일</span><span class="sxs-lookup"><span data-stu-id="bf3aa-169">XAML file</span></span>
<span data-ttu-id="bf3aa-170">페이지 `.xaml` 파일 수정:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="bf3aa-171">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="bf3aa-172">`Page` 및 `engagement:EngagementPage` 교체:</span><span class="sxs-lookup"><span data-stu-id="bf3aa-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="bf3aa-173">**Engagement 사용 안 함:**</span><span class="sxs-lookup"><span data-stu-id="bf3aa-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="bf3aa-174">**Engagement 사용:**</span><span class="sxs-lookup"><span data-stu-id="bf3aa-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="bf3aa-175">기본 동작 재정의</span><span class="sxs-lookup"><span data-stu-id="bf3aa-175">Override the default behaviour</span></span>
<span data-ttu-id="bf3aa-176">기본적으로 페이지의 클래스 이름은 extra 없이 활동 이름으로 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="bf3aa-177">클래스에서 "Page" 접미사를 사용하는 경우에는 해당 접미사도 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="bf3aa-178">이름의 기본 동작을 재정의하려면 코드에 다음 코드 조각만 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="bf3aa-179">활동과 함께 추가 정보를 보고하려는 경우에는 코드에 다음 코드 조각을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="bf3aa-180">페이지의 `OnNavigatedTo` 메서드 내에서 이러한 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="bf3aa-181">대체 메서드: 수동으로 `StartActivity()` 호출</span><span class="sxs-lookup"><span data-stu-id="bf3aa-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="bf3aa-182">`Page` 클래스를 오버로드할 수 없거나 오버로드하지 않으려는 경우 `EngagementAgent` 메서드를 직접 호출하여 활동을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="bf3aa-183">페이지의 `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="bf3aa-184">세션을 올바르게 종료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="bf3aa-185">응용 프로그램을 닫을 때 Windows 유니버설 SDK는 `EndActivity` 메서드를 자동으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-185">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="bf3aa-186">따라서 사용자 활동이 변경될 때마다 `StartActivity` 메서드를 호출하는 것이 **상당히** 좋으며 `EndActivity` 메서드는 호출하지 **않는** 것이 좋습니다. 이 메서드는 현재 사용자가 응용 프로그램을 떠난 Engagement 서버에 보내며 이는 모든 응용 프로그램 로그에 영향을 미칩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-186">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="bf3aa-187">고급 보고</span><span class="sxs-lookup"><span data-stu-id="bf3aa-187">Advanced reporting</span></span>
<span data-ttu-id="bf3aa-188">필요에 따라 응용 프로그램 관련 이벤트, 오류 및 작업을 보고할 수 있습니다. 이렇게 하려면 `EngagementAgent` 클래스에 포함된 다른 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="bf3aa-189">Engagement API에서는 Engagement의 모든 고급 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="bf3aa-190">자세한 내용은 [Windows 유니버설 앱에서 고급 Mobile Engagement 태깅 API를 사용하는 방법](mobile-engagement-windows-store-use-engagement-api.md)을 참조하세요</span><span class="sxs-lookup"><span data-stu-id="bf3aa-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="bf3aa-191">고급 구성</span><span class="sxs-lookup"><span data-stu-id="bf3aa-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="bf3aa-192">자동 작동 중단 보고를 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="bf3aa-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="bf3aa-193">Engagement의 자동 작동 중단 보고를 사용하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="bf3aa-194">이렇게 하면 처리되지 않은 예외 발생 시 Engagement에서 아무런 작업도 수행하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="bf3aa-195">이 기능을 사용하지 않도록 설정하려는 경우 앱에서 처리되지 않은 작동 중단이 발생해도 Engagement에서 작동 중단을 전송하지 않으며 **또한** 세션 및 작업도 닫지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-195">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="bf3aa-196">자동 작동 중단 보고를 사용하지 않도록 설정하려면 구성을 선언한 방식에 따라 사용자 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="bf3aa-197">`EngagementConfiguration.xml` 파일에서</span><span class="sxs-lookup"><span data-stu-id="bf3aa-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="bf3aa-198">`<reportCrash>` 및 `</reportCrash>` 태그 간의 작동 중단 보고를 `false`(으)로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="bf3aa-199">런타임에 `EngagementConfiguration` 개체에서</span><span class="sxs-lookup"><span data-stu-id="bf3aa-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="bf3aa-200">EngagementConfiguration 개체를 사용하여 작동 중단 보고를 false로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="bf3aa-201">버스트 모드</span><span class="sxs-lookup"><span data-stu-id="bf3aa-201">Burst mode</span></span>
<span data-ttu-id="bf3aa-202">기본적으로 Engagement 서비스는 로그를 실시간으로 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="bf3aa-203">응용 프로그램이 로그를 매우 자주 보고하는 경우에는 로그를 버퍼링한 다음 정기적으로 한꺼번에 보고하는 것이 보다 효율적입니다. 이러한 방식을 "버스트 모드"라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="bf3aa-204">이 방식을 사용하려면 다음 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="bf3aa-205">인수는 **밀리초**단위의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="bf3aa-206">언제든지 실시간 로깅을 다시 활성화하려면 매개 변수를 포함하지 않거나 값을 0으로 설정하여 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="bf3aa-207">버스트 모드를 사용하는 경우 배터리 수명은 약간 길어지지만 Engagement 모니터에 영향을 주게 됩니다. 모든 세션 및 작업 기간이 버스트 임계값으로 반올림되므로 버스트 임계값보다 짧은 세션과 작업은 표시되지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="bf3aa-208">30000(30초) 이하의 버스트 임계값을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="bf3aa-209">저장된 로드는 300개 항목으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="bf3aa-210">보내는 로그가 너무 길면 일부 로그가 손실될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="bf3aa-211">1초보다 짧은 기간으로 버스트 임계값을 구성할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-211">The burst threshold cannot be configured to a period lesser than 1s.</span></span> <span data-ttu-id="bf3aa-212">버스트 임계값을 1초보다 짧게 구성하면 SDK에는 오류가 포함된 추적이 표시되며, 값은 자동으로 기본값인 0초로 다시 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-212">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s.</span></span> <span data-ttu-id="bf3aa-213">그러면 SDK에서 실시간 로그 보고가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf3aa-213">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

