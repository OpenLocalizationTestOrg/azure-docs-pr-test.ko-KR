---
title: "aaaWindows 유니버설 앱 SDK 통합에 도달"
description: "어떻게 tooIntegrate Azure Mobile Engagement는 Windows 유니버설 앱을 도달합니다"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="12ae6-103">Windows 유니버설 앱 도달률 SDK 통합</span><span class="sxs-lookup"><span data-stu-id="12ae6-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="12ae6-104">Hello에 설명 된 hello 통합 절차를 따라야 [Windows 유니버설 Engagement SDK 통합](mobile-engagement-windows-store-integrate-engagement.md) 이 가이드를 수행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="12ae6-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="12ae6-105">Windows 유니버설 프로젝트로 hello Engagement Reach SDK 포함</span><span class="sxs-lookup"><span data-stu-id="12ae6-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="12ae6-106">아무 것도 않아도 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-106">You do not have anything tooadd.</span></span> <span data-ttu-id="12ae6-107">`EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="12ae6-108">Hello에 있는 이미지를 사용자 지정할 수 있습니다 `Resources` 특히 hello 브랜드 아이콘 (해당 기본 toohello Engagement 아이콘) 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="12ae6-109">유니버설 앱에서 이동할 수도 있습니다 hello `Resources` 폴더에 해당 콘텐츠 사이의 수 있지만 응용 프로그램, 갖습니다 프로그램 공유 프로젝트 tooshare tookeep hello `Resources\EngagementConfiguration.xml` 종속 플랫폼의 기본 위치에서의 파일.</span><span class="sxs-lookup"><span data-stu-id="12ae6-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="12ae6-110">Hello Windows 알림 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="12ae6-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="12ae6-111">Windows 8.x 및 Windows Phone 8.1만 해당</span><span class="sxs-lookup"><span data-stu-id="12ae6-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="12ae6-112">순서 toouse hello에 **Windows 알림 서비스** (WNS 라고 함)에서 프로그램 `Package.appxmanifest` 파일 크기가 `Application UI` 클릭 `All Image Assets` hello bot 왼쪽된 상자에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="12ae6-113">Hello 상자 오른쪽의 hello에 `Notifications`, 변경 `toast capable` 에서 `(not set)` 너무`(Yes)`합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="12ae6-114">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="12ae6-114">All platforms</span></span>
<span data-ttu-id="12ae6-115">Toosynchronize 앱 tooyour Microsoft 계정과 toohello engagement 플랫폼을 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="12ae6-116">이 계정을 toocreate 하거나 여러 로그온 [windows 개발자 센터](https://dev.windows.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="12ae6-117">새 응용 프로그램을 만들고 찾을 있는 후 hello SID 및 비밀 키입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="12ae6-118">Hello engagement 프런트엔드에서의 응용 프로그램 설정에 이동 `native push` 자격 증명을 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="12ae6-119">그런 다음 프로젝트를 마우스 오른쪽 단추로 클릭하고 `store` 및 `Associate App with hello Store...`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="12ae6-120">하기만 tooselect hello 응용 프로그램 사용자에 게 작성 toosynchronize 전에 것입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="12ae6-121">Hello Engagement Reach SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="12ae6-122">Hello 수정 `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="12ae6-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="12ae6-123">`InitEngagement` 메서드에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:</span><span class="sxs-lookup"><span data-stu-id="12ae6-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="12ae6-124">hello `EngagementReach.Instance.Init` 전용된 스레드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="12ae6-125">Toodo 없는 것 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="12ae6-126">응용 프로그램에서 푸시 알림을 다른 곳에서 사용 중인 경우 너무 있는[푸시 채널 공유](#push-channel-sharing) Engagement Reach와 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="12ae6-127">통합</span><span class="sxs-lookup"><span data-stu-id="12ae6-127">Integration</span></span>
<span data-ttu-id="12ae6-128">공지 및 설문 조사의 응용 프로그램에서 두 가지 방법으로 tooadd hello Reach 앱 내 배너 및 중간 뷰를 제공 하는 engagement: hello 통합 및 hello 웹 보기 수동 통합 오버레이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="12ae6-129">두 접근 방식을 hello에 결합할 수 없습니다 동일한 페이지.</span><span class="sxs-lookup"><span data-stu-id="12ae6-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="12ae6-130">hello hello 두 통합 중에 선택 이러한 방식으로 요약 될 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="12ae6-131">Hello 에이전트에서에서 페이지를 이미 상속 하는 경우에 hello 오버레이 통합을 선택할 수도 있습니다 `EngagementPage`, 대체 단순히는 `EngagementPage` 하 여 `EngagementPageOverlay` 및 `xmlns:engagement="using:Microsoft.Azure.Engagement"` 여 `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` 페이지에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="12ae6-132">선택할 수 있습니다 hello 웹 보기 수동 통합 tooprecisely 위치 hello 도달 UI 페이지 내에서 하려는 경우 또는 tooadd 않도록 다른 상속 수준 tooyour 페이지.</span><span class="sxs-lookup"><span data-stu-id="12ae6-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="12ae6-133">오버레이 통합</span><span class="sxs-lookup"><span data-stu-id="12ae6-133">Overlay integration</span></span>
<span data-ttu-id="12ae6-134">hello Engagement 오버레이 hello UI 요소 toodisplay Reach 캠페인 페이지에 사용 되는 동적으로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="12ae6-135">Hello 오버레이 레이아웃에 적합 하지 않는 경우 고려해 야 hello 웹 보기 수동 통합 대신.</span><span class="sxs-lookup"><span data-stu-id="12ae6-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="12ae6-136">.Xaml 파일 변경에 `EngagementPage` 너무 참조`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="12ae6-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="12ae6-137">Tooyour 네임 스페이스 선언을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="12ae6-138">`engagement:EngagementPage` 및 `engagement:EngagementPageOverlay` 교체:</span><span class="sxs-lookup"><span data-stu-id="12ae6-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="12ae6-139">**EngagementPage를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="12ae6-140">**EngagementPageOverlay를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="12ae6-141">그런 다음 .cs 파일에서 `EngagementPage` 대신 `EngagementPageOverlay`로 페이지에 태그를 지정하고 `Microsoft.Azure.Engagement.Overlay`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="12ae6-142">`EngagementPage` 및 `EngagementPageOverlay` 교체:</span><span class="sxs-lookup"><span data-stu-id="12ae6-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="12ae6-143">**EngagementPage를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="12ae6-144">**EngagementPageOverlay를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="12ae6-145">hello Engagement 오버레이 추가 `Grid` 페이지 맨 위에 요소 레이아웃 및 hello 두 구성 `WebView` hello에 대 한 요소 하나 배너와 hello hello 중간 보기에 대 한 다른 하나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="12ae6-146">Hello에서 직접 hello 오버레이 요소를 사용자 지정할 수 있습니다 `EngagementPageOverlay.cs` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="12ae6-147">웹 보기 수동 통합</span><span class="sxs-lookup"><span data-stu-id="12ae6-147">Web views manual integration</span></span>
<span data-ttu-id="12ae6-148">검색 두 hello에 대 한 페이지 도달 하는 `WebView` 요소 hello 배너와 hello 중간 보기를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="12ae6-149">toodo 있는 점은 tooadd만 hello 그 두 `WebView` 요소 위치 페이지에서 다음은 예제:</span><span class="sxs-lookup"><span data-stu-id="12ae6-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="12ae6-150">이 예제에서는 hello에 `WebView` 요소는 늘어난된 toofit 자동으로 화면 회전 또는 창 크기 변경이 발생 한 경우 다시 크기의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="12ae6-151">동일한 명명 tookeep hello 반드시 `engagement_notification_content` 및 `engagement_announcement_content` hello에 대 한 `WebView` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="12ae6-152">도달률은 요소를 이름으로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="12ae6-153">datapush 처리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="12ae6-153">Handle datapush (optional)</span></span>
<span data-ttu-id="12ae6-154">응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 원하는 tooimplement 두 이벤트의 hello EngagementReach 클래스 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="12ae6-155">App.xaml.cs hello App() 생성자에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="12ae6-156">각 메서드가 반환 되는 부울 값의 해당 hello 콜백에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="12ae6-157">서비스는 hello 데이터 푸시 디스패치 후 피드백 tooits 백 엔드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="12ae6-158">Hello 콜백이 false를 반환 하면 hello `exit` 피드백 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="12ae6-159">그렇지 않으면 `action`이(가) 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="12ae6-160">콜백이 없는 hello 이벤트에 대 한을 설정 하는 경우 hello `drop` 피드백 tooEngagement 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="12ae6-161">데이터 푸시에 대 한 여러 개의 차트 피드백 수 tooreceive engagement이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="12ae6-162">Tooset 여러 처리기는 이벤트를 하려는 경우에 hello 피드백은 모니터는 toohello 보낸 마지막 트랜잭션이 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="12ae6-163">이 경우 tooalways 권장 반환 hello 혼동 피드백 hello 프런트 엔드에 있는 동일한 값 tooavoid 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="12ae6-164">UI 사용자 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="12ae6-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="12ae6-165">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="12ae6-165">First step</span></span>
<span data-ttu-id="12ae6-166">Toocustomize hello reach UI을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="12ae6-167">toodo 따라서 해야 toocreate hello의 서브 클래스 `EngagementReachHandler` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="12ae6-168">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="12ae6-169">다음의 hello hello 콘텐츠를 설정 `EngagementReach.Instance.Handler` 필드에 사용자 지정 개체와 프로그램 `App.xaml.cs` hello 내 클래스 `App()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="12ae6-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="12ae6-170">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="12ae6-171">Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="12ae6-172">Toocreate 없는 고유한, 이렇게 하면 없는 toooverride 모든 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="12ae6-173">hello 기본 동작은 tooselect hello Engagement 기준 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="12ae6-174">웹 보기</span><span class="sxs-lookup"><span data-stu-id="12ae6-174">Web View</span></span>
<span data-ttu-id="12ae6-175">기본적으로 도달 범위는 hello DLL toodisplay hello 알림과 페이지의 hello 포함 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="12ae6-176">tooprovide 전체 사용자 지정 가능한 웹 보기만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="12ae6-177">Toocustomize 레이아웃을 하려는 경우 재정의 직접 hello 리소스 파일 `EngagementAnnouncement.html` 및 `EngagementNotification.html`합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="12ae6-178">계약의 모든 코드를 필요한 `<body></body>` toorun 정확 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="12ae6-179">그러나 `engagement_webview_area`외부에 태그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="12ae6-180">그러나 리소스 toouse를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="12ae6-181">재정의할 수 `EngagementReachHandler` 메서드 프로그램 하위 클래스 tootell Engagement toouse에 레이아웃, 보험 tooembedded hello engagement 메커니즘 하지만 변수:</span><span class="sxs-lookup"><span data-stu-id="12ae6-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="12ae6-182">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="12ae6-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="12ae6-183">기본적으로 AnnouncementHTML은 `ms-appx-web:///Resources/EngagementAnnouncement.html`입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="12ae6-184">Hello html 파일을 (텍스트 알림, 웹 anoucement 및 설문 조사 알림)는 푸시 메시지의 hello 내용 디자인을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="12ae6-185">AnnouncementName은 `engagement_announcement_content`입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="12ae6-186">Xaml 페이지에서 hello webview 디자인의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="12ae6-187">NotfificationHTML은 `ms-appx-web:///Resources/EngagementNotification.html`입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="12ae6-188">푸시 메시지에 대 한 hello 알림을 디자인 hello html 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="12ae6-189">NotfificationName은 `engagement_notification_content`입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="12ae6-190">Xaml 페이지에서 hello webview 디자인의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="12ae6-191">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="12ae6-191">Customization</span></span>
<span data-ttu-id="12ae6-192">Engagement 개체를 보존하는 경우 원하는 알림 및 공지 웹 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="12ae6-193">웹 보기 개체 설명 하는 세 번-hello xaml에서는 처음으로 hello "setwebview()" 메서드에서.cs 파일에서 시간이 두 번째 및 세 번째 시간 hello html 파일에 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="12ae6-194">Xaml hello 현재 그래픽 레이아웃 webview 구성 요소에 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="12ae6-195">.Cs 파일에서 "setwebview()" hello 두 webview (알림, 알림)의 hello 차원 설정한를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="12ae6-196">Hello 응용 프로그램의 크기를 조정할 때 매우 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="12ae6-197">Hello Engagement html 파일에서는 hello webview 콘텐츠, 디자인에 설명 하 고 hello 서로 사이의 요소 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="12ae6-198">시작 메시지</span><span class="sxs-lookup"><span data-stu-id="12ae6-198">Launch message</span></span>
<span data-ttu-id="12ae6-199">사용자가 시스템 알림 (알림)를 클릭 하면 Engagement hello 응용 프로그램을 시작, 부하 hello 내용의 hello 메시지를 푸시하고 hello 해당 캠페인에 대 한 hello 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="12ae6-200">Hello 시작 되지 않도록 (에 따라 네트워크의 속도 hello) hello 페이지의 hello 응용 프로그램 및 hello 표시 사이의 지연 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="12ae6-201">로드 하는 문제가 tooindicate toohello 사용자, 진행률 표시줄 또는 진행률 표시기 등의 시각적 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="12ae6-202">Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="12ae6-203">"공용 App() {}" App.xaml.cs에서 tooimplement hello 콜백을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="12ae6-204">Hello 콜백 "공개 App() {}"는 방법을 설정할 수 있습니다 프로그램 `App.xaml.cs` hello 전에 가급적 파일 `EngagementReach.Instance.Init()` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="12ae6-205">각 처리기는 UI 스레드 hello에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="12ae6-206">않아도 tooworry MessageBox 또는 다른 UI 관련를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="12ae6-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="12ae6-207"><a id="push-channel-sharing"></a> 푸시 채널 공유</span><span class="sxs-lookup"><span data-stu-id="12ae6-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="12ae6-208">경우 푸시 알림을 응용 프로그램에서 다른 용도로 사용 하는 이름을 제공 해야 toouse hello 푸시 채널 hello Engagement SDK의 기능을 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="12ae6-209">이 누락 tooavoid 푸시입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="12ae6-210">사용자 고유의 푸시 채널 toohello Engagement Reach 초기화를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="12ae6-211">hello SDK 한 새 요청 하는 대신 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="12ae6-212">Hello에 푸시 채널 hello Engagement Reach 초기화 업데이트로 `InitEngagement` hello 메서드에서 `App.xaml.cs` 파일:</span><span class="sxs-lookup"><span data-stu-id="12ae6-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="12ae6-213">또는 원하는 경우 tooconsume hello 푸시 채널 hello Reach 초기화 된 후 hello SDK에서 만들어지면 콜백을 Engagement Reach tooget hello 푸시 채널에 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="12ae6-214">콜백은 모든 위치에서 설정 **후** Reach 초기화 hello:</span><span class="sxs-lookup"><span data-stu-id="12ae6-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="12ae6-215">사용자 지정 체계 팁</span><span class="sxs-lookup"><span data-stu-id="12ae6-215">Custom scheme tip</span></span>
<span data-ttu-id="12ae6-216">사용자 지정 체계 사용법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-216">We provide custom scheme use.</span></span> <span data-ttu-id="12ae6-217">engagement 프런트 엔드 toobe engagement 응용 프로그램에서 사용 되는 다른 종류의 URI 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="12ae6-218">`http, ftp, ...` 와(과) 같은 기본 체계는 Windows에서 관리되며 장치에 기본 응용 프로그램이 설치되어 있지 않으면 해당 메시지가 포함된 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="12ae6-219">또한 응용 프로그램에 대해 사용자 지정 체계를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="12ae6-220">hello 간단한 방법을 tooset 응용 프로그램에서 사용자 지정 체계는 tooopen 프로그램 `Package.appxmanifest` 에서 이동 `Declarations` 패널입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="12ae6-221">선택 `Protocol` hello 사용 가능한 선언 스크롤 상자 영역을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="12ae6-222">Hello 편집 `Name` 필드에 새 프로토콜에 필요한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="12ae6-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="12ae6-223">이제 toouse이이 프로토콜을 편집 하면 `App.xaml.cs` hello로 `OnActivated` 메서드를도 tooinitialize engagement 여기 유념 하십시오:</span><span class="sxs-lookup"><span data-stu-id="12ae6-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

