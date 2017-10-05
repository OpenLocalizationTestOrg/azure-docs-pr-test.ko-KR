---
title: "Windows 유니버설 앱 Azure Mobile Engagement 시작"
description: "Windows 유니버설 앱에 대해 분석 및 푸시 알림과 함께 Azure Mobile Engagement를 사용하는 방법을 알아봅니다."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="d701b-103">Windows 유니버설 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="d701b-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d701b-104">이 항목에서는 Azure Mobile Engagement를 사용하여 Windows 유니버설 응용 프로그램에서 구분된 사용자에게 푸시 알림을 보내고 앱 사용량을 파악하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="d701b-105">이 자습서에서는 Mobile Engagement를 사용하는 간단한 브로드캐스트 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="d701b-106">WNS(Windows 알림 서비스)를 사용하여 푸시 알림을 받고 기본적인 앱 사용 데이터를 수집하는 빈 Windows 유니버설 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="d701b-107">Azure Mobile Engagement 서비스는 2018년 3월에 사용 중지되며 현재 기존 고객에게만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d701b-108">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d701b-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d701b-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d701b-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="d701b-110">Windows 유니버설 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="d701b-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d701b-111"><a id="connecting-app"></a>Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d701b-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d701b-112">이 자습서에서는 데이터를 수집하고 푸시 알림을 보내는 데 필요한 최소 집합인 "기본 통합" 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="d701b-113">전체 통합 설명서는 [Mobile Engagement Windows 유니버설 SDK 통합](mobile-engagement-windows-store-sdk-overview.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="d701b-114">여기서는 통합을 시연하기 위해 Visual Studio를 사용하여 기본적인 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="d701b-115">Windows 유니버설 앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="d701b-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="d701b-116">다음 단계에서는 Visual Studio 2015를 사용한다고 가정하지만 이전 버전의 Visual Studio에서도 단계는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="d701b-117">Visual Studio를 시작하고 **홈** 화면에서 **새 프로젝트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="d701b-118">팝업에서 **Windows** -> **유니버설** -> **비어 있는 앱(유니버설 Windows)**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="d701b-119">앱 **이름** 및 **솔루션 이름**을 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="d701b-120">이제 다음에 Azure Mobile Engagement SDK를 통합할 Windows 유니버설 앱 프로젝트가 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d701b-121">Mobile Engagement 백 엔드에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d701b-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d701b-122">프로젝트에서 [MicrosoftAzure.MobileEngagement] Nuget 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="d701b-123">Windows와 Windows Phone 플랫폼을 모두 대상으로 하는 경우 두 프로젝트에 대해 이 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="d701b-124">Windows 8.x 및 Windows Phone 8.1에 대해 동일한 Nuget 패키지는 각 프로젝트에 올바른 플랫폼별 이진 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="d701b-125">**Package.appxmanifest**를 열고 다음 기능이 추가되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="d701b-126">이제 앞서 Mobile Engagement 앱에 대해 복사한 연결 문자열을 `Resources\EngagementConfiguration.xml` 파일의 `<connectionString>` 태그와 `</connectionString>` 태그 사이에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="d701b-127">앱이 Windows와 Windows Phone 플랫폼을 모두 대상으로 하는 경우 여전히 지원하는 각 플랫폼에 하나씩 두 개의 Mobile Engagement 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="d701b-128">두 개의 앱을 가지면 대상에 올바른 구분을 생성할 수 있고 각 플랫폼을 대상으로 하는 적절한 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d701b-129">NuGet이 아직 Windows 10 UWP 응용 프로그램에서 SDK 리소스를 자동으로 복사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="d701b-130">Nuget 패키지를 설치하는 경우 표시된 단계(readme.txt)를 따라 수동으로 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="d701b-131">파일 `App.xaml.cs`에서:</span><span class="sxs-lookup"><span data-stu-id="d701b-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="d701b-132">a.</span><span class="sxs-lookup"><span data-stu-id="d701b-132">a.</span></span> <span data-ttu-id="d701b-133">`using` 구문 추가:</span><span class="sxs-lookup"><span data-stu-id="d701b-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="d701b-134">b.</span><span class="sxs-lookup"><span data-stu-id="d701b-134">b.</span></span> <span data-ttu-id="d701b-135">Engagement를 초기화하는 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="d701b-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="d701b-136">c.</span><span class="sxs-lookup"><span data-stu-id="d701b-136">c.</span></span> <span data-ttu-id="d701b-137">**OnLaunched** 메서드에서 SDK 초기화:</span><span class="sxs-lookup"><span data-stu-id="d701b-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="d701b-138">c.</span><span class="sxs-lookup"><span data-stu-id="d701b-138">c.</span></span> <span data-ttu-id="d701b-139">**OnActivated** 메서드에 다음을 삽입하고 아직 없는 경우 해당 메서드 추가:</span><span class="sxs-lookup"><span data-stu-id="d701b-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="d701b-140"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="d701b-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="d701b-141">데이터 보내기를 시작하고 사용자가 활성 상태인지 확인하려면 Mobile Engagement 백 엔드에 화면(활동)을 하나 이상 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="d701b-142">**MainPage.xaml.cs**에서 다음 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="d701b-143">Microsoft.Azure.Engagement.Overlay; 사용</span><span class="sxs-lookup"><span data-stu-id="d701b-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="d701b-144">**MainPage**의 기본 클래스를 **Page**에서 **EngagementPageOverlay**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="d701b-145">파일 `MainPage.xaml`에서:</span><span class="sxs-lookup"><span data-stu-id="d701b-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="d701b-146">a.</span><span class="sxs-lookup"><span data-stu-id="d701b-146">a.</span></span> <span data-ttu-id="d701b-147">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="d701b-148">b.</span><span class="sxs-lookup"><span data-stu-id="d701b-148">b.</span></span> <span data-ttu-id="d701b-149">XML 태그 이름의 **Page**를 **engagement:EngagementPageOverlay**로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d701b-150">페이지가 `OnNavigatedTo` 메서드를 재정의하는 경우에는 `base.OnNavigatedTo(e)`을(를) 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="d701b-151">그렇지 않으면 활동이 보고되지 않습니다. `EngagementPage`은(는) `OnNavigatedTo` 메서드 내에서 `StartActivity`을(를) 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="d701b-152">이 작업은 기본 템플릿에 `OnNavigatedTo` 메서드가 있는 Windows Phone 프로젝트에서 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="d701b-153">**Windows 10 Universal 앱**의 경우 위에서 설명한 방법보다 [Windows 유니버설 앱 Engagement SDK의 고급 보고](mobile-engagement-windows-store-advanced-reporting.md)의 “권장 방법: Page 클래스 오버로드” 섹션에서 권장하는 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="d701b-154"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="d701b-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="d701b-155"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="d701b-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="d701b-156">Mobile Engagement에서는 캠페인 컨텍스트에서 푸시 알림 및 앱 내 메시징을 사용하여 사용자와 상호 작용하고 사용자에게 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="d701b-157">Mobile Engagement 포털에서는 이 모듈을 도달률이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="d701b-158">다음 섹션에서는 이러한 알림과 메시지를 받도록 앱을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="d701b-159">WNS 푸시 알림을 받도록 앱 설정</span><span class="sxs-lookup"><span data-stu-id="d701b-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="d701b-160">`Package.appxmanifest` 파일의 **응용 프로그램** 탭에서 **알림**에 있는 **알림 가능:**을 **예**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="d701b-161">도달률 SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="d701b-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="d701b-162">`App.xaml.cs`에서 에이전트 초기화 직후 **InitEngagement** 함수에서 **EngagementReach.Instance.Init(e);**를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="d701b-163">알림을 보낼 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-163">You're ready to send a toast.</span></span> <span data-ttu-id="d701b-164">그런 다음 이 기본 통합을 제대로 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="d701b-165">알림을 보내도록 Mobile Engagement 액세스 권한 부여</span><span class="sxs-lookup"><span data-stu-id="d701b-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="d701b-166">웹 브라우저에서 [Windows 스토어 개발자 센터]를 열어 로그인하고 필요한 경우 계정을 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="d701b-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="d701b-167">오른쪽 위 모서리에 있는 **대시보드**를 클릭한 다음 왼쪽 패널 메뉴에서 **새 앱 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="d701b-168">해당 이름을 예약하여 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="d701b-169">앱이 만들어지면 왼쪽 메뉴에서 **서비스 -> 푸시 알림**으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="d701b-170">푸시 알림 섹션에서 **Live 서비스 사이트** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="d701b-171">푸시 자격 증명 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="d701b-172">**앱 설정** 섹션에 있는지 확인한 다음 **패키지 SID** 및 **클라이언트 암호**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="d701b-173">Mobile Engagement 포털의 **설정**으로 이동하여 왼쪽의 **네이티브 푸시** 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="d701b-174">그런 다음 **편집** 단추를 클릭하여 다음과 같이 **패키지 SID(보안 식별자)** 및 **암호 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="d701b-175">마지막으로 Visual Studio 앱과 앱 스토어에 만들어진 이 앱이 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="d701b-176">Visual Studio의 **스토어에 앱 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="d701b-177"><a id="send"></a>앱에 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="d701b-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="d701b-178">앱이 실행 중인 경우 앱 내 알림이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="d701b-179">그렇지 않고 앱이 닫힌 경우 알림 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="d701b-180">앱 내 알림이 표시되지만 알림 메시지가 표시되지 않고 앱을 Visual Studio의 디버그 모드로 실행 중인 경우 도구 모음의 **수명 주기 이벤트 -> 일시 중단**을 사용하여 앱이 일시 중단되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="d701b-181">Visual Studio에서 응용 프로그램을 디버깅하는 동안 홈 단추를 클릭한 경우 일시 중단되지 않을 수 있으며, 앱 내 알림으로 표시되어 있는 동안에는 알림 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d701b-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="d701b-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="d701b-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="d701b-183">[Windows 스토어 개발자 센터]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="d701b-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
