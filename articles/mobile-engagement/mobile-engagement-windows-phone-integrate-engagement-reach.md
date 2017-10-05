---
title: "Windows Phone 도달률 Engagement SDK 통합"
description: "Windows Phone Silverlight 앱에서 Azure Mobile Engagement 도달률을 통합하는 방법"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="6a653-103">Windows Phone 도달률 Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="6a653-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="6a653-104">이 가이드의 작업을 수행하기 전에 [Windows Phone Silverlight Engagement SDK 통합](mobile-engagement-windows-phone-integrate-engagement.md) 에 설명된 통합 절차를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="6a653-105">Windows Phone Silverlight 프로젝트에 Engagement 도달률 SDK 통합</span><span class="sxs-lookup"><span data-stu-id="6a653-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="6a653-106">별도로 추가할 항목은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-106">You do not have anything to add.</span></span> <span data-ttu-id="6a653-107">`EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="6a653-108">프로젝트의 `Resources` 폴더에 있는 이미지, 특히 기본적으로 Engagement 아이콘을 사용하는 브랜드 아이콘을 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="6a653-109">기능 추가</span><span class="sxs-lookup"><span data-stu-id="6a653-109">Add the capabilities</span></span>
<span data-ttu-id="6a653-110">Engagement 도달률 SDK에는 몇 가지 추가 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="6a653-111">`WMAppManifest.xml` 파일을 열고 다음 기능이 선언되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="6a653-112">첫 번째는 MPNS 서비스에 의해 사용되어 알림 메시지의 표시를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="6a653-113">두 번째는 SDK에 브라우저 작업을 포함하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="6a653-114">`WMAppManifest.xml` 파일을 편집하여 `<Capabilities />` 태그 내에 추가:</span><span class="sxs-lookup"><span data-stu-id="6a653-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="6a653-115">Microsoft 푸시 알림 서비스를 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="6a653-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="6a653-116">MPNS, 즉 **Microsoft 푸시 알림 서비스**를 사용하려면 `WMAppManifest.xml` 파일에 `Publisher` 특성이 프로젝트 이름으로 설정된 `<App />` 태그가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="6a653-117">Engagement 도달률 SDK 초기화</span><span class="sxs-lookup"><span data-stu-id="6a653-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="6a653-118">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="6a653-118">Engagement configuration</span></span>
<span data-ttu-id="6a653-119">Engagement 구성은 프로젝트의 `Resources\EngagementConfiguration.xml` 파일에서 중앙 집중식으로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="6a653-120">이 파일을 편집하여 도달률 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="6a653-121">*선택 사항으로*, 네이티브 푸시(MPNS)가 `<enableNativePush>` 및 `</enableNativePush>` 태그 간에 활성화되는지 여부를 나타냅니다(기본적으로 `true`).</span><span class="sxs-lookup"><span data-stu-id="6a653-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="6a653-122">*선택 사항으로*, `<channelName>` 및 `</channelName>` 태그 간의 푸시 채널 이름을 나타냅니다. 응용 프로그램이 현재 사용 중일 수 있는 동일 항목을 제공하거나 비워 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="6a653-123">대신 런타임에 구성을 지정하려는 경우에는 Engagement 에이전트 초기화 전에 다음 메서드를 호출하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="6a653-124">응용 프로그램의 MPNS 푸시 채널 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="6a653-125">기본적으로는 appId를 기준으로 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="6a653-126">Engagement 외부에서 푸시 채널을 사용하려는 경우를 제외하면 이름을 직접 지정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="6a653-127">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="6a653-127">Engagement initialization</span></span>
<span data-ttu-id="6a653-128">`App.xaml.cs`수정:</span><span class="sxs-lookup"><span data-stu-id="6a653-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="6a653-129">`using` 구문에 추가:</span><span class="sxs-lookup"><span data-stu-id="6a653-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="6a653-130">`Application_Launching`에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:</span><span class="sxs-lookup"><span data-stu-id="6a653-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="6a653-131">`Application_Activated` 메서드에 `EngagementReach.Instance.OnActivated` 삽입:</span><span class="sxs-lookup"><span data-stu-id="6a653-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="6a653-132">`EngagementReach.Instance.Init`은(는) 전용 스레드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="6a653-133">직접 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="6a653-134">앱 스토어 제출 고려 사항</span><span class="sxs-lookup"><span data-stu-id="6a653-134">App store submission considerations</span></span>
<span data-ttu-id="6a653-135">푸시 알림 사용 시에는 다음 규칙이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="6a653-136">Microsoft [응용 프로그램 정책] 설명서 2.9항에는 다음과 같은 규칙이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="6a653-137">사용자에게 푸시 알림 수신을 수락하도록 요청해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="6a653-138">그런 다음 설정에서 푸시 알림을 사용하지 않도록 설정할 방법을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="6a653-139">EngagementReach 개체는 옵트인(opt in) 및 옵트아웃(opt out)을 관리하기 위한 두 메서드인 `EnableNativePush()` 및 `DisableNativePush()`을(를) 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="6a653-140">예를 들어 MPNS를 사용하거나 사용하지 않는 토글을 사용하여 설정에서 옵션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="6a653-141">또한 Engagement 구성\<windows-phone-sdk-reach-configuration\>을 통해 MPNS를 비활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="6a653-142">2.9.1) 응용 프로그램은 먼저 제공할 알림을 설명하고 **사용자의 명시적 권한, 즉 옵트인(opt in)을 받아야 합니다**. 또한 **사용자가 푸시 알림 수신을 옵트아웃(opt out)할 수 있는 메커니즘도 제공해야 합니다**.</span><span class="sxs-lookup"><span data-stu-id="6a653-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="6a653-143">Microsoft 푸시 알림 서비스를 사용하여 제공하는 모든 알림은 사용자에게 제공되는 설명과 일치해야 하며 해당하는 모든 [응용 프로그램 정책][Content Policies] 및 [특정 응용 프로그램 유형에 대한 추가 요구 사항]을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="6a653-144">푸시 알림을 너무 많이 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-144">You should not use too many push notifications.</span></span> <span data-ttu-id="6a653-145">Engagement는 사용자에 대한 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="6a653-146">2.9.2) 응용 프로그램은, 그리고 해당 응용 프로그램이 Microsoft 푸시 알림 서비스를 사용할 때는 Microsoft 푸시 알림 서비스의 네트워크 용량이나 대역폭을 과도하게 사용해서는 안 되며, Microsoft의 합리적인 결정에 따라 과다한 푸시 알림으로 Windows Phone 또는 기타 Microsoft 장치나 서비스에 지나친 부담을 주어서는 안 됩니다. 또한 Microsoft 네트워크 또는 서버나 Microsoft 푸시 알림 서비스에 연결된 타사 서버 또는 네트워크를 손상시키거나 작동을 방해해서도 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="6a653-147">MPNS를 사용하여 중요한 정보를 보내지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6a653-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="6a653-148">Engagement에서는 MPNS를 사용하므로 이 규칙은 Engagement 프런트 엔드 내에서 만든 캠페인에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="6a653-149">2.9.3) Microsoft 푸시 알림 서비스를 사용하여 중요 업무용 알림 또는 생사에 영향을 줄 수 있는 알림을 보내서는 안 됩니다. 여기에는 의료 장치나 상태와 관련된 중요 알림을 비롯한 다수의 알림이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="6a653-150">Microsoft는 Microsoft 푸시 알림 서비스 또는 Microsoft 푸시 알림 서비스 알림 배달 기능을 중단/오류 없이 사용할 수 있거나 해당 기능이 실시간으로 제공된다는 어떤 보증도 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="6a653-151">**이러한 권장 사항을 지키지 않는 경우에는 응용 프로그램이 유효성 검사 프로세스를 통과한다고 보장할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="6a653-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="6a653-152">데이터 푸시 처리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="6a653-152">Handle data push (optional)</span></span>
<span data-ttu-id="6a653-153">응용 프로그램이 도달률 데이터 푸시를 수신할 수 있도록 하려면 EngagementReach 클래스의 두 이벤트를 구현해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="6a653-154">각 메서드의 콜백에서는 부울이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="6a653-155">Engagement에서는 데이터 푸시를 디스패치한 후 해당 백 엔드로 피드백을 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="6a653-156">콜백에서 false를 반환하면 `exit` 피드백이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="6a653-157">그렇지 않으면 `action`이(가) 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="6a653-158">이벤트에 대해 콜백이 설정되어 있지 않으면 `drop` 피드백이 Engagement에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="6a653-159">Engagement는 데이터 푸시에 대해 여러 피드백을 수신할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="6a653-160">이벤트에 대해 여러 처리기를 설정하려는 경우 피드백은 마지막으로 전송된 항목에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="6a653-161">이 경우에는 프런트 엔드에서 피드백을 혼동하지 않도록 항상 같은 값을 반환하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="6a653-162">UI 사용자 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="6a653-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="6a653-163">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="6a653-163">First step</span></span>
<span data-ttu-id="6a653-164">도달률 UI는 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="6a653-165">UI를 사용자 지정하려면 `EngagementReachHandler` 클래스의 서브클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="6a653-166">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="6a653-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="6a653-167">그런 다음 `Application_Launching` 메서드 내에서 `App.xaml.cs` 클래스의 사용자 지정 개체를 사용하여 `EngagementReach.Instance.Handler` 필드의 콘텐츠를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="6a653-168">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="6a653-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="6a653-169">Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="6a653-170">따라서 구현을 직접 작성할 필요는 없으며 직접 작성하더라도 모든 메서드를 재정의하지는 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="6a653-171">기본 동작에서는 Engagement 기준 개체가 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="6a653-172">레이아웃</span><span class="sxs-lookup"><span data-stu-id="6a653-172">Layouts</span></span>
<span data-ttu-id="6a653-173">도달률에서는 기본적으로 DLL의 포함된 리소스를 사용하여 알림과 페이지를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="6a653-174">그러나 원하는 리소스를 사용하여 이러한 구성 요소에 브랜드를 반영할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="6a653-175">서브클래스에서 `EngagementReachHandler` 메서드를 재정의하여 Engagement에서 특정 레이아웃을 사용하도록 명령할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="6a653-176">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="6a653-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="6a653-177">`CreateNotification` 메서드는 null을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="6a653-178">그러면 알림이 표시되지 않으며 도달률 캠페인이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="6a653-179">레이아웃 구현을 간소화할 수 있도록 코드의 기준으로 사용 가능한 자체 xaml도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="6a653-180">이 xaml은 Engagement SDK 보관 파일 위치(/src/reach/)에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="6a653-181">제공되는 원본은 Microsoft에서 사용하는 것과 정확하게 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="6a653-182">따라서 해당 원본을 직접 수정하는 경우에는 네임스페이스와 이름을 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="6a653-183">알림 위치</span><span class="sxs-lookup"><span data-stu-id="6a653-183">Notification position</span></span>
<span data-ttu-id="6a653-184">기본적으로 앱 내 알림은 응용 프로그램 왼쪽 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="6a653-185">이 동작은 `EngagementReachHandler` 개체의 `GetNotificationPosition` 메서드를 재정의하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="6a653-186">현재는 `BOTTOM`(기본값) 및 `TOP` 위치 중에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="6a653-187">시작 메시지</span><span class="sxs-lookup"><span data-stu-id="6a653-187">Launch message</span></span>
<span data-ttu-id="6a653-188">사용자가 시스템 알림(알림)을 클릭하면 앱이 시작되고 푸시 메시지의 내용이 로드되며 해당 캠페인의 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="6a653-189">응용 프로그램을 시작한 후부터 페이지가 표시될 때까지 네트워크 속도에 따라 지연이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="6a653-190">콘텐츠가 로드 중임을 사용자에게 알리려면 진행률 표시줄이나 진행률 표시기와 같은 시각적 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="6a653-191">Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="6a653-192">콜백을 구현하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-192">To implement the callback, do:</span></span>

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

<span data-ttu-id="6a653-193">콜백은 `App.xaml.cs` 파일의 `Application_Launching` 메서드에서 설정할 수 있으며 `EngagementReach.Instance.Init()` 호출 앞에 설정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="6a653-194">UI 스레드에서 각 처리기를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="6a653-195">따라서 MessageBox 또는 UI 관련 항목을 사용할 때는 별도의 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6a653-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="6a653-196">[응용 프로그램 정책]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="6a653-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="6a653-197">[특정 응용 프로그램 유형에 대한 추가 요구 사항]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="6a653-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

