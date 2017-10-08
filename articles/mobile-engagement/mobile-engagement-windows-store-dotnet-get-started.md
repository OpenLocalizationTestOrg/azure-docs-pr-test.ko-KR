---
title: "Windows 범용 앱 Azure Mobile Engagement aaaGet 시작"
description: "자세한 내용은 방법 toouse Azure Mobile Engagement Windows 유니버설 앱에 대 한 분석 및 푸시 알림입니다."
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
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="00598-103">Windows 유니버설 앱용 Azure Mobile Engagement 시작</span><span class="sxs-lookup"><span data-stu-id="00598-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="00598-104">이 항목에서는 Azure Mobile Engagement toounderstand toouse 응용 프로그램 사용 및 송신 푸시 Windows 유니버설 응용 프로그램의 알림을 toosegmented 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="00598-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="00598-105">이 자습서에는 hello 간단한 브로드캐스트 시나리오를 Mobile Engagement를 사용 하 여 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="00598-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="00598-106">WNS(Windows 알림 서비스)를 사용하여 푸시 알림을 받고 기본적인 앱 사용 데이터를 수집하는 빈 Windows 유니버설 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00598-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="00598-107">hello Azure Mobile Engagement 서비스 년 3 월 2018 사용 중지 될 했으며 현재 사용 가능한 tooexisting 고객만 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="00598-108">자세한 내용은 [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00598-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00598-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00598-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="00598-110">Windows 유니버설 앱용 Mobile Engagement 설정</span><span class="sxs-lookup"><span data-stu-id="00598-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="00598-111"><a id="connecting-app"></a>응용 프로그램 toohello Mobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="00598-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="00598-112">이 자습서는 기본적인 "통합", 최소한의 hello 필요한 toocollect 데이터 설정 되 고 푸시 알림을 보내는 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="00598-113">hello에 hello 완벽 한 통합 설명서를 확인할 수 있습니다 [Mobile Engagement Windows 유니버설 SDK 통합](mobile-engagement-windows-store-sdk-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="00598-114">Visual Studio toodemonstrate hello 통합 된 기본 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00598-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="00598-115">Windows 유니버설 앱 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="00598-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="00598-116">hello 다음 단계에서는 가정 hello를 사용 하 여 Visual Studio 2015의 hello 단계는 이전 버전의 Visual Studio에서 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="00598-117">Visual Studio를 시작 및 hello **홈** 화면에서 **새 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="00598-118">Hello 팝업에 선택 **Windows** -> **유니버설** -> **비어 있는 앱 (유니버설 Windows)**합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="00598-119">Hello 앱 입력 **이름** 및 **솔루션 이름**, 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="00598-120">이제는 다음 hello Azure Mobile Engagement SDK가 통합 Windows 유니버설 앱 프로젝트를 작성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="00598-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="00598-121">응용 프로그램 tooMobile Engagement 백 엔드 연결</span><span class="sxs-lookup"><span data-stu-id="00598-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="00598-122">Hello 설치 [MicrosoftAzure.MobileEngagement] 프로젝트에서 Nuget 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="00598-123">Windows 및 Windows Phone 플랫폼을 대상으로 하는 경우 필요한 toodo이 두 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="00598-124">Windows 8.x 및 Windows Phone 8.1 hello 같은 Nuget 패키지 위치 hello 올바른 플랫폼별 바이너리 각 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00598-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="00598-125">열기 **Package.appxmanifest** 기능에 따라 해당 hello 있습니다 추가 되어 있는지 확인 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00598-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="00598-126">이제 Mobile Engagement 응용 프로그램에 대 한 앞에서 복사한 hello 연결 문자열을 복사 하 고 hello에 붙여 `Resources\EngagementConfiguration.xml` hello 간의 파일 `<connectionString>` 및 `</connectionString>` 태그:</span><span class="sxs-lookup"><span data-stu-id="00598-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="00598-127">앱이 Windows와 Windows Phone 플랫폼을 모두 대상으로 하는 경우 여전히 지원하는 각 플랫폼에 하나씩 두 개의 Mobile Engagement 응용 프로그램을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="00598-128">Hello 대상 그룹의 올바른 분할을 만들 수는 각 플랫폼에 대 한 대상된 적절 하 게 알림을 보낼 수를 두 응용 프로그램이 있으면이 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="00598-129">NuGet 자동으로 복사할 수 없습니다 hello SDK 리소스 Windows 10 UWP 응용 프로그램에서.</span><span class="sxs-lookup"><span data-stu-id="00598-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="00598-130">설정한 toodo hello Nuget 패키지가 설치 된 경우 (readme.txt)을 표시 하는 hello 단계를 수동으로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="00598-131">Hello에 `App.xaml.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="00598-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="00598-132">a.</span><span class="sxs-lookup"><span data-stu-id="00598-132">a.</span></span> <span data-ttu-id="00598-133">Hello 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="00598-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="00598-134">b.</span><span class="sxs-lookup"><span data-stu-id="00598-134">b.</span></span> <span data-ttu-id="00598-135">Hello Engagement 초기화 하는 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="00598-136">c.</span><span class="sxs-lookup"><span data-stu-id="00598-136">c.</span></span> <span data-ttu-id="00598-137">Hello에 SDK hello 초기화 **OnLaunched** 메서드:</span><span class="sxs-lookup"><span data-stu-id="00598-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="00598-138">c.</span><span class="sxs-lookup"><span data-stu-id="00598-138">c.</span></span> <span data-ttu-id="00598-139">Hello에 hello 다음 삽입 **OnActivated** 메서드 하 고 이미 존재 하지 않는 경우 hello 메서드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="00598-140"><a id="monitor"></a>실시간 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="00598-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="00598-141">데이터를 전송 하는 toostart 및는 hello 사용자가 활성화 되도록 하나 이상 화면 (활동) toohello Mobile Engagement 백 엔드를 전송 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="00598-142">Hello에 **MainPage.xaml.cs**, hello 다음 추가 `using` 문:</span><span class="sxs-lookup"><span data-stu-id="00598-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="00598-143">Microsoft.Azure.Engagement.Overlay; 사용</span><span class="sxs-lookup"><span data-stu-id="00598-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="00598-144">기본 클래스 hello 변경 **MainPage** 에서 **페이지** 너무**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="00598-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="00598-145">Hello에 `MainPage.xaml` 파일:</span><span class="sxs-lookup"><span data-stu-id="00598-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="00598-146">a.</span><span class="sxs-lookup"><span data-stu-id="00598-146">a.</span></span> <span data-ttu-id="00598-147">Tooyour 네임 스페이스 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="00598-148">b.</span><span class="sxs-lookup"><span data-stu-id="00598-148">b.</span></span> <span data-ttu-id="00598-149">Hello 대체 **페이지** hello XML 태그 이름에 **engagement: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="00598-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00598-150">페이지 hello를 재정의 하는 경우 `OnNavigatedTo` 메서드 수 있는지 toocall `base.OnNavigatedTo(e)`합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="00598-151">그렇지 않으면 hello 활동 보고 되지 않습니다 `EngagementPage` 호출 `StartActivity` 내 해당 `OnNavigatedTo` 메서드).</span><span class="sxs-lookup"><span data-stu-id="00598-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="00598-152">이 Windows Phone 프로젝트에서 특히 중요 hello 기본 서식 파일에 있는 한 `OnNavigatedTo` 메서드.</span><span class="sxs-lookup"><span data-stu-id="00598-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="00598-153">에 대 한 **Windows 10 유니버설 앱**, hello에서 권장 하는 hello 메서드를 사용 하 여 "권장 되는 방법: 페이지 클래스 오버 로드" 섹션의 [고급 hello Windows 유니버설 앱 Engagement SDK로 보고](mobile-engagement-windows-store-advanced-reporting.md) 위에서 설명한 하나는 hello 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="00598-154"><a id="monitor"></a>실시간 모니터링과 앱 연결</span><span class="sxs-lookup"><span data-stu-id="00598-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="00598-155"><a id="integrate-push"></a>푸시 알림 및 앱 내 메시징 사용</span><span class="sxs-lookup"><span data-stu-id="00598-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="00598-156">Mobile Engagement toointeract 있으며 푸시 알림과 앱 내 메시징을 캠페인의 hello 컨텍스트에서 사용자에 게 도달 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="00598-157">이 모듈에는 hello Mobile engagement 연결 포털에서 REACH를 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="00598-158">hello 다음 섹션에서는 앱 tooreceive를 속성을 설정.</span><span class="sxs-lookup"><span data-stu-id="00598-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="00598-159">사용자 응용 프로그램 tooreceive WNS 푸시 알림을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="00598-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="00598-160">Hello에 `Package.appxmanifest` 파일 hello에 **응용 프로그램** 탭의 **알림**설정, **알림 가능:** 너무**예**</span><span class="sxs-lookup"><span data-stu-id="00598-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="00598-161">REACH SDK hello를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="00598-162">`App.xaml.cs`, 호출 **EngagementReach.Instance.Init(e);** hello에 **InitEngagement** hello 에이전트 초기화 직후 함수:</span><span class="sxs-lookup"><span data-stu-id="00598-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="00598-163">준비 toosend 알림을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="00598-163">You're ready toosend a toast.</span></span> <span data-ttu-id="00598-164">그런 다음 이 기본 통합을 제대로 수행했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="00598-165">권한 부여 액세스 tooMobile Engagement toosend 알림</span><span class="sxs-lookup"><span data-stu-id="00598-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="00598-166">웹 브라우저에서 [Windows 스토어 개발자 센터]를 열어 로그인하고 필요한 경우 계정을 만드십시오.</span><span class="sxs-lookup"><span data-stu-id="00598-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="00598-167">클릭 **대시보드** hello 오른쪽 위 코너 한 다음 클릭 **새 앱 만들기** hello 왼쪽된 패널 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="00598-168">해당 이름을 예약하여 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00598-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="00598-169">Hello 응용 프로그램을 만든 후 너무 이동**서비스에 푸시 알림을->** hello 왼쪽된 메뉴에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="00598-170">Hello에 푸시 알림 섹션을 hello 클릭 **Live 서비스 사이트** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="00598-171">Toohello 푸시 자격 증명 섹션을 이동 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="00598-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="00598-172">Hello에 있는지 확인 **앱 설정** 섹션 및 다음 복사 프로그램 **패키지 SID** 및 **클라이언트 암호**</span><span class="sxs-lookup"><span data-stu-id="00598-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="00598-173">Toohello 이동 **설정** Mobile Engagement 포털의 hello를 클릭 하 고 **하 여 네이티브 푸시** hello 왼쪽에는 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="00598-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="00598-174">클릭 hello **편집** 단추 tooenter 프로그램 **패키지 보안 식별자 (SID)** 하였고 **비밀 키** 표시 된 것 처럼:</span><span class="sxs-lookup"><span data-stu-id="00598-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="00598-175">마지막으로 hello 앱 스토어에서이 작성된 된 앱과 Visual Studio 응용 프로그램에 연결 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="00598-176">Visual Studio의 **스토어에 앱 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="00598-177"><a id="send"></a>보낼 알림 tooyour 앱</span><span class="sxs-lookup"><span data-stu-id="00598-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="00598-178">Hello 앱이 실행 중인 앱 내 알림이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00598-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="00598-179">그렇지 않으면 hello 앱 닫혀 있는 경우에 알림 메시지 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="00598-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="00598-180">경우에 앱에서 알림을 하지만 하지 알림 메시지를 표시 하 고 hello 앱 Visual Studio에서 디버그 모드에서 실행 하는 **수명 주기 이벤트 Suspend->** hello 도구 모음 tooensure hello 이러한 앱이 중지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="00598-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="00598-181">Visual Studio에서 hello 응용 프로그램을 디버깅 하는 동안 hello 홈 단추를 클릭 한 경우 다음 해당 하지 않는 항상 일시 중단 하 고 알림 메시지로 표시 되지 hello 알림이 앱에 표시 하는 동안.</span><span class="sxs-lookup"><span data-stu-id="00598-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows 스토어 개발자 센터]: https://dev.windows.com
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
