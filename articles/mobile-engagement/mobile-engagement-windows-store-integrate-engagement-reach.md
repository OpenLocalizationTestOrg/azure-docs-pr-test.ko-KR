---
title: "Windows 유니버설 앱 도달률 SDK 통합"
description: "Windows 유니버설 앱과 Azure 모바일 Engagement 도달률을 통합하는 방법"
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="b2abb-103">Windows 유니버설 앱 도달률 SDK 통합</span><span class="sxs-lookup"><span data-stu-id="b2abb-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="b2abb-104">이 가이드의 작업을 수행하기 전에 [Windows 유니버설 Engagement SDK 통합](mobile-engagement-windows-store-integrate-engagement.md) 에 설명된 통합 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="b2abb-105">Windows 유니버설 프로젝트에 Engagement 도달률 SDK 포함</span><span class="sxs-lookup"><span data-stu-id="b2abb-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="b2abb-106">별도로 추가할 항목은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-106">You do not have anything to add.</span></span> <span data-ttu-id="b2abb-107">`EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="b2abb-108">프로젝트의 `Resources` 폴더에 있는 이미지, 특히 기본적으로 Engagement 아이콘을 사용하는 브랜드 아이콘을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="b2abb-109">유니버설 앱에서 공유 프로젝트의 `Resources` 폴더를 이동하여 앱 사이의 콘텐츠를 공유할 수도 있지만 플랫폼에 종속된 기본 위치에 `Resources\EngagementConfiguration.xml` 파일을 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="b2abb-110">Windows 알림 서비스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="b2abb-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="b2abb-111">Windows 8.x 및 Windows Phone 8.1만 해당</span><span class="sxs-lookup"><span data-stu-id="b2abb-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="b2abb-112">`Application UI`의 `Package.appxmanifest` 파일에서 **Windows 알림 서비스**(WNS라고 함)를 사용하려면 왼쪽 아래 박스에서 `All Image Assets`을(를) 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="b2abb-113">`Notifications`의 오른쪽 상자에서 `toast capable`을(를) `(not set)`에서 `(Yes)`(으)로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="b2abb-114">모든 플랫폼</span><span class="sxs-lookup"><span data-stu-id="b2abb-114">All platforms</span></span>
<span data-ttu-id="b2abb-115">Microsoft 계정 및 Engagement 플랫폼에 앱을 동기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="b2abb-116">이를 위해 계정을 만들거나 [Windows 개발자 센터](https://dev.windows.com)에 로그온해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="b2abb-117">그다음에 새 응용 프로그램을 만들고 SID 및 암호 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="b2abb-118">Engagement 프런트 엔드에서 `native push` 의 앱 설정으로 이동하여 자격 증명을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="b2abb-119">그런 다음 프로젝트를 마우스 오른쪽 단추로 클릭하고 `store` 및 `Associate App with the Store...`을(를) 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="b2abb-120">동기화하기 전에 만든 응용 프로그램을 선택하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="b2abb-121">Engagement 도달률 SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="b2abb-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="b2abb-122">`App.xaml.cs` 수정:</span><span class="sxs-lookup"><span data-stu-id="b2abb-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="b2abb-123">`InitEngagement` 메서드에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:</span><span class="sxs-lookup"><span data-stu-id="b2abb-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="b2abb-124">`EngagementReach.Instance.Init`은(는) 전용 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="b2abb-125">직접 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="b2abb-126">응용 프로그램의 다른 곳에서 푸시 알림을 사용 중인 경우 Engagement 도달률에 [푸시 채널을 공유](#push-channel-sharing) 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="b2abb-127">통합</span><span class="sxs-lookup"><span data-stu-id="b2abb-127">Integration</span></span>
<span data-ttu-id="b2abb-128">Engagement는 도달률 앱 내 배너와 알림 및 설문 조사에 대한 중간 보기를 응용 프로그램에 추가하는 두 가지 방법(오버레이 통합 및 웹 보기 수동 통합)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="b2abb-129">동일한 페이지에서 두 가지 방법을 결합할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="b2abb-130">두 가지 통합 간의 선택은 다음과 같은 방식으로 요약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="b2abb-131">이미 페이지가 에이전트 `EngagementPage`에서 상속된 경우 오버레이 통합을 선택할 수 있으며 이는 페이지에서 `EngagementPage`를 `EngagementPageOverlay`로 바꾸고 `xmlns:engagement="using:Microsoft.Azure.Engagement"`를 `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"`로 바꾸는 정도의 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="b2abb-132">페이지에서 도달률 UI를 정확히 배치하거나 페이지에 다른 상속 수준을 추가하지 않으려는 경우 웹 보기 수동 통합을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="b2abb-133">오버레이 통합</span><span class="sxs-lookup"><span data-stu-id="b2abb-133">Overlay integration</span></span>
<span data-ttu-id="b2abb-134">Engagement 오버레이는 페이지에서 도달률 캠페인을 표시하는 데 사용되는 UI 요소를 동적으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="b2abb-135">오버레이가 레이아웃에 적합하지 않은 경우 대신 웹 보기 수동 통합을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="b2abb-136">.xaml 파일에서 `EngagementPage` 참조를 `EngagementPageOverlay`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="b2abb-137">다음 줄을 네임스페이스 선언에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="b2abb-138">`engagement:EngagementPage` 및 `engagement:EngagementPageOverlay` 교체:</span><span class="sxs-lookup"><span data-stu-id="b2abb-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="b2abb-139">**EngagementPage를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="b2abb-140">**EngagementPageOverlay를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="b2abb-141">그런 다음 .cs 파일에서 `EngagementPage` 대신 `EngagementPageOverlay`로 페이지에 태그를 지정하고 `Microsoft.Azure.Engagement.Overlay`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="b2abb-142">`EngagementPage` 및 `EngagementPageOverlay` 교체:</span><span class="sxs-lookup"><span data-stu-id="b2abb-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="b2abb-143">**EngagementPage를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="b2abb-144">**EngagementPageOverlay를 사용하는 경우:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="b2abb-145">Engagement 오버레이는 레이아웃에 구성된 페이지 맨 위에 `Grid` 요소 및 두 개의 `WebView` 요소(하나는 배너용이고 나머지 하나는 중간 보기용)를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="b2abb-146">`EngagementPageOverlay.cs` 파일에서 직접 오버레이 요소를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="b2abb-147">웹 보기 수동 통합</span><span class="sxs-lookup"><span data-stu-id="b2abb-147">Web views manual integration</span></span>
<span data-ttu-id="b2abb-148">도달률은 페이지에서 배너 및 중간 보기의 표시를 담당할 두 개의 `WebView` 요소를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="b2abb-149">두 개의 `WebView` 요소를 페이지의 임의 위치에 추가하기만 하면 되며 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="b2abb-150">이 예제에서 `WebView` 요소는 화면 회전 또는 창 크기를 변경할 때 자동으로 크기를 조정하는 컨테이너에 맞게 확장됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="b2abb-151">`WebView` 요소에 동일한 이름 지정 `engagement_notification_content` 및 `engagement_announcement_content`를 유지하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="b2abb-152">도달률은 요소를 이름으로 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="b2abb-153">datapush 처리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2abb-153">Handle datapush (optional)</span></span>
<span data-ttu-id="b2abb-154">응용 프로그램이 도달률 데이터 푸시를 수신할 수 있도록 하려면 EngagementReach 클래스의 두 이벤트를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="b2abb-155">App.xaml.cs의 App() 생성자에서 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="b2abb-156">각 메서드의 콜백에서는 부울이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="b2abb-157">Engagement에서는 데이터 푸시를 디스패치한 후 해당 백 엔드로 피드백을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="b2abb-158">콜백에서 false를 반환하면 `exit` 피드백이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="b2abb-159">그렇지 않으면 `action`이(가) 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="b2abb-160">이벤트에 대해 콜백이 설정되어 있지 않으면 `drop` 피드백이 Engagement에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="b2abb-161">Engagement는 데이터 푸시에 대해 여러 피드백을 수신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="b2abb-162">이벤트에 대해 여러 처리기를 설정하려는 경우 피드백은 마지막으로 전송된 항목에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="b2abb-163">이 경우에는 프런트 엔드에서 피드백을 혼동하지 않도록 항상 같은 값을 반환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="b2abb-164">UI 사용자 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b2abb-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="b2abb-165">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="b2abb-165">First step</span></span>
<span data-ttu-id="b2abb-166">도달률 UI는 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="b2abb-167">UI를 사용자 지정하려면 `EngagementReachHandler` 클래스의 서브클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="b2abb-168">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="b2abb-169">그런 다음 `App()` 메서드 내에서 `App.xaml.cs` 클래스의 사용자 지정 개체를 사용하여 `EngagementReach.Instance.Handler` 필드의 콘텐츠를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="b2abb-170">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="b2abb-171">Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="b2abb-172">따라서 구현을 직접 작성할 필요는 없으며 직접 작성하더라도 모든 메서드를 재정의하지는 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="b2abb-173">기본 동작에서는 Engagement 기준 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="b2abb-174">웹 보기</span><span class="sxs-lookup"><span data-stu-id="b2abb-174">Web View</span></span>
<span data-ttu-id="b2abb-175">도달률에서는 기본적으로 DLL의 포함된 리소스를 사용하여 알림과 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="b2abb-176">전체 사용자 지정 기능을 제공하기 위해 웹 보기만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="b2abb-177">레이아웃을 사용자 지정하려면 리소스 파일 `EngagementAnnouncement.html` 및 `EngagementNotification.html`을(를) 직접 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="b2abb-178">Engagement가 제대로 실행하려면 `<body></body>` 에 모든 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="b2abb-179">그러나 `engagement_webview_area`외부에 태그를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="b2abb-180">원하는 리소스를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="b2abb-181">서브클래스에서 `EngagementReachHandler` 메서드를 재정의하여 Engagement에서 레이아웃을 사용하도록 명령할 수 있습니다. 단, 포함된 Engagement 메커니즘을 사용할 때는 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="b2abb-182">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="b2abb-182">**Sample Code :**</span></span>

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


<span data-ttu-id="b2abb-183">기본적으로 AnnouncementHTML은 `ms-appx-web:///Resources/EngagementAnnouncement.html`입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="b2abb-184">푸시 메시지(텍스트 알림, 웹 알림, 설문 조사 알림)의 내용을 디자인하는 html 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="b2abb-185">AnnouncementName은 `engagement_announcement_content`입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="b2abb-186">xaml 페이지의 웹 보기 디자인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="b2abb-187">NotfificationHTML은 `ms-appx-web:///Resources/EngagementNotification.html`입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="b2abb-188">푸시 메시지의 알림을 디자인하는 html 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="b2abb-189">NotfificationName은 `engagement_notification_content`입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="b2abb-190">xaml 페이지의 웹 보기 디자인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="b2abb-191">사용자 지정</span><span class="sxs-lookup"><span data-stu-id="b2abb-191">Customization</span></span>
<span data-ttu-id="b2abb-192">Engagement 개체를 보존하는 경우 원하는 알림 및 공지 웹 보기를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="b2abb-193">세 번에 걸쳐 설명되는 webview에 주의합니다. 첫 번째는 xaml에서, 두 번째는 "setwebview()" 메서드의 .cs 파일에서, 세 번째는 html 파일에서 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="b2abb-194">xaml에 현재 그래픽 레이아웃 webview 구성 요소를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="b2abb-195">.cs 파일에는 알림(notification 및 announcement)의 두 웹 보기 크기를 설정하는 "setwebview()"를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="b2abb-196">응용 프로그램의 크기를 조정할 때 매우 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="b2abb-197">Engagement html 파일에는 웹 보기 내용, 디자인 및 웹 보기 간의 요소 위치에 대한 설명을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="b2abb-198">시작 메시지</span><span class="sxs-lookup"><span data-stu-id="b2abb-198">Launch message</span></span>
<span data-ttu-id="b2abb-199">사용자가 시스템 알림(알림)을 클릭하면 응용 프로그램이 시작되고 푸시 메시지의 내용이 로드되며 해당 캠페인의 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="b2abb-200">응용 프로그램을 시작한 후부터 페이지가 표시될 때까지 네트워크 속도에 따라 지연이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="b2abb-201">콘텐츠가 로드 중임을 사용자에게 알리려면 진행률 표시줄이나 진행률 표시기와 같은 시각적 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="b2abb-202">Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="b2abb-203">콜백을 구현하려면 App.xaml.cs의 "Public App(){}"에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="b2abb-204">`App.xaml.cs` 파일의 "Public App(){}" 메서드에서 콜백을 설정할 수 있으며 `EngagementReach.Instance.Init()` 호출 앞에 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="b2abb-205">UI 스레드에서 각 처리기를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="b2abb-206">따라서 MessageBox 또는 UI 관련 항목을 사용할 때는 별도의 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="b2abb-207"><a id="push-channel-sharing"></a> 푸시 채널 공유</span><span class="sxs-lookup"><span data-stu-id="b2abb-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="b2abb-208">응용 프로그램에서 푸시 알림을 다른 용도로 사용 하는 경우 Engagement SDK의 푸시 채널 공유 기능을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="b2abb-209">이는 푸시 누락을 방지하기 위함입니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="b2abb-210">Engagement 도달률 초기화에 푸시 채널을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="b2abb-211">SDK는 새 항목을 요청하는 대신 이것을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="b2abb-212">`App.xaml.cs` 파일의 `InitEngagement` 메서드에서 푸시 채널을 사용한 Engagement 도달률 초기화를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="b2abb-213">또한, 도달률 초기화 후 푸시 채널을 사용하려는 경우 Engagement 도달률에 콜백을 설정하여 푸시 채널을 SDK에 의해 생성하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="b2abb-214">도달률 초기화 **후** 모든 위치에서 콜백을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="b2abb-215">사용자 지정 체계 팁</span><span class="sxs-lookup"><span data-stu-id="b2abb-215">Custom scheme tip</span></span>
<span data-ttu-id="b2abb-216">사용자 지정 체계 사용법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-216">We provide custom scheme use.</span></span> <span data-ttu-id="b2abb-217">Engagement 응용 프로그램에서 사용할 여러 URI 유형을 Engagement 프런트 엔드에서 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="b2abb-218">`http, ftp, ...` 와(과) 같은 기본 체계는 Windows에서 관리되며 장치에 기본 응용 프로그램이 설치되어 있지 않으면 해당 메시지가 포함된 창이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="b2abb-219">또한 응용 프로그램에 대해 사용자 지정 체계를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="b2abb-220">응용 프로그램에서 사용자 지정 체계를 간편하게 설정하는 방법은 `Package.appxmanifest`을(를) 열고 `Declarations` 패널로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="b2abb-221">사용 가능한 선언 스크롤 상자에서 `Protocol` 을(를) 선택하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="b2abb-222">새 프로토콜의 원하는 이름을 입력하여 `Name` 필드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="b2abb-223">이제 이 프로토콜을 사용하려면 `App.xaml.cs`을(를) `OnActivated` 메서드로 편집하고 여기서 Engagement를 초기화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2abb-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

