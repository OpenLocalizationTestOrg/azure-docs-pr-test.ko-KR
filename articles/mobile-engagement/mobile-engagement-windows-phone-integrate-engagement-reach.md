---
title: "aaaWindows 전화 Silverlight SDK 통합에 도달"
description: "어떻게 tooIntegrate Azure Mobile Engagement는 Windows Phone Silverlight 앱을 도달합니다"
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
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="fcc94-103">Windows Phone 도달률 Engagement SDK 통합</span><span class="sxs-lookup"><span data-stu-id="fcc94-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="fcc94-104">Hello에 설명 된 hello 통합 절차를 따라야 [Windows Phone Silverlight Engagement SDK 통합](mobile-engagement-windows-phone-integrate-engagement.md) 이 가이드를 수행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="fcc94-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="fcc94-105">Windows Phone Silverlight 프로젝트에 hello Engagement Reach SDK 포함</span><span class="sxs-lookup"><span data-stu-id="fcc94-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="fcc94-106">아무 것도 않아도 tooadd 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-106">You do not have anything tooadd.</span></span> <span data-ttu-id="fcc94-107">`EngagementReach` 참조 및 리소스가 이미 프로젝트에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="fcc94-108">Hello에 있는 이미지를 사용자 지정할 수 있습니다 `Resources` 특히 hello 브랜드 아이콘 (해당 기본 toohello Engagement 아이콘) 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="fcc94-109">Hello 기능 추가</span><span class="sxs-lookup"><span data-stu-id="fcc94-109">Add hello capabilities</span></span>
<span data-ttu-id="fcc94-110">hello Engagement Reach SDK에는 일부 유용한 기능이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="fcc94-111">열기 프로그램 `WMAppManifest.xml` 파일 및 기능에 따라 해당 hello 선언 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="fcc94-112">hello 하나는에서 처음 사용할 알림 메시지의 hello MPNS 서비스 tooallow hello 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="fcc94-113">hello 두 번째 메서드는 사용 되는 tooembed 브라우저 작업 hello SDK 나눕니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="fcc94-114">Hello 편집 `WMAppManifest.xml` hello 내에 추가 하 고 파일 `<Capabilities />` 태그:</span><span class="sxs-lookup"><span data-stu-id="fcc94-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="fcc94-115">Hello Microsoft 푸시 알림 서비스를 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="fcc94-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="fcc94-116">순서 toouse hello에 **Microsoft 푸시 알림 서비스** (MPNS 라고 함)에 `WMAppManifest.xml` 파일 있어야는 `<App />` 사용 하 여 태그는 `Publisher` 특성이 toohello 프로젝트 이름을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="fcc94-117">Hello Engagement Reach SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="fcc94-118">Engagement 구성</span><span class="sxs-lookup"><span data-stu-id="fcc94-118">Engagement configuration</span></span>
<span data-ttu-id="fcc94-119">hello에 곳에서 hello Engagement 구성 `Resources\EngagementConfiguration.xml` 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="fcc94-120">이 파일 toospecify reach 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="fcc94-121">*선택적*, 또는 여부를 나타냅니다 (MPNS) hello 네이티브 푸시가 활성화 사이 있지 않음 `<enableNativePush>` 및 `</enableNativePush>` 태그 (`true` 기본적으로).</span><span class="sxs-lookup"><span data-stu-id="fcc94-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="fcc94-122">*선택적*, 간의 hello 푸시 채널의 hello 이름을 표시 `<channelName>` 및 `</channelName>` hello를 제공 하는 태그를 동일한 응용 프로그램 수 현재 사용 하거나 비워 두세요.</span><span class="sxs-lookup"><span data-stu-id="fcc94-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="fcc94-123">런타임 시 대신 있습니다 호출할 수 있는 hello 다음 toospecify 하려는 경우 hello Engagement 에이전트를 초기화 하기 전에 메서드:</span><span class="sxs-lookup"><span data-stu-id="fcc94-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="fcc94-124">응용 프로그램의 hello MPNS 푸시 채널의 hello 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="fcc94-125">기본적으로 Engagement hello appId를 기반으로 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="fcc94-126">없는 필요 toospecify hello 이름이 있는, 직접 Engagement 외부 toouse hello 푸시 채널을 계획 하는 경우를 제외 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="fcc94-127">Engagement 초기화</span><span class="sxs-lookup"><span data-stu-id="fcc94-127">Engagement initialization</span></span>
<span data-ttu-id="fcc94-128">Hello 수정 `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="fcc94-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="fcc94-129">추가 tooyour `using` 문:</span><span class="sxs-lookup"><span data-stu-id="fcc94-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="fcc94-130">`Application_Launching`에서 `EngagementAgent.Instance.Init` 바로 다음에 `EngagementReach.Instance.Init` 삽입:</span><span class="sxs-lookup"><span data-stu-id="fcc94-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="fcc94-131">삽입 `EngagementReach.Instance.OnActivated` hello에 `Application_Activated` 메서드:</span><span class="sxs-lookup"><span data-stu-id="fcc94-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="fcc94-132">hello `EngagementReach.Instance.Init` 전용된 스레드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="fcc94-133">Toodo 없는 것 직접 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="fcc94-134">앱 스토어 제출 고려 사항</span><span class="sxs-lookup"><span data-stu-id="fcc94-134">App store submission considerations</span></span>
<span data-ttu-id="fcc94-135">Microsoft hello 푸시 알림을 사용 하는 경우 몇 가지 규칙을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="fcc94-136">Microsoft hello에서 [응용 프로그램 정책] 설명서, 2.9 섹션:</span><span class="sxs-lookup"><span data-stu-id="fcc94-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="fcc94-137">Hello 사용자 tooaccept tooreceive 푸시 알림을 요청 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="fcc94-138">설정에서 방법을 toodisable hello 푸시 알림을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="fcc94-139">hello EngagementReach 개체 제공 두 메서드 toomanage hello opt-에/옵트아웃을 `EnableNativePush()` 및 `DisableNativePush()`합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="fcc94-140">수, 예를 들어, 옵션 설정/해제 toodisable 사용 하 여 hello 설정에서 만들거나 MPNS를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="fcc94-141">Hello Engagement 구성을 통해 MPNS toodeactivate 결정할 수도 있습니다\<windows-phone-sdk-reach-구성\>합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="fcc94-142">2.9.1) hello 응용 프로그램에 제공 하는 hello 알림을 toobe 설명 먼저 해야 및 **(옵트인) hello 사용자의 명시적인 가져올**, 및 **사용자 수신 하지 않을 수 있는 hello를 통해 메커니즘을 제공 해야 푸시 알림**합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="fcc94-143">Hello Microsoft 푸시 알림 서비스를 사용 하 여 제공 하는 모든 알림 hello 설명이 제공 toohello 사용자와 일치 해야 하 고 모두 준수 해야 해당 [응용 프로그램 정책] [ Content Policies]및 [특정 응용 프로그램 종류에 대 한 추가 요구 사항이]합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="fcc94-144">푸시 알림을 너무 많이 사용해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-144">You should not use too many push notifications.</span></span> <span data-ttu-id="fcc94-145">Engagement는 사용자에 대한 알림을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="fcc94-146">2.9.2) hello 응용 프로그램 및 해당 Microsoft 푸시 알림 서비스 hello 사용 하지 과도 하 게 사용 해야 네트워크 용량 또는 hello Microsoft 푸시 알림 서비스의 대역폭 하거나 그렇지 않으면 백업용 부담을 Windows Phone 또는 다른 Microsoft 장치 또는 서비스 과도 한와 Microsoft의 합리적 판단에 따른 푸시 알림, 및를 손상 하거나 안 모든 Microsoft 네트워크 또는 서버 또는 모든 제 3 자 서버 또는 네트워크 연결 된 toohello Microsoft 푸시 알림 서비스에 방해가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="fcc94-147">MPNS toosend criticals 정보에 의존 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="fcc94-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="fcc94-148">Engagement MPNS를 사용 하 여이 규칙 hello Engagement 내에 프런트 엔드 만들어진 hello 캠페인에 대 한도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="fcc94-149">2.9.3) 수명 또는 사망, 제한 중요 한 알림 관련된 tooa 의료 장비 또는 조건을 포함 하 여 중요 한 영향을 줄 수 hello Microsoft 푸시 알림 서비스에는 업무에 중요 해 지거나 다른 방법 사용된 toosend 알림이 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="fcc94-150">MICROSOFT 명시적으로 부인 ANY 보증은 hello 사용의 hello MICROSOFT 푸시 알림 서비스 또는 배달의 MICROSOFT 푸시 알림 서비스 알림 됩니다 수 중지 되지 않고 오류 무료 tooOCCUR ON A 실시간으로 또는 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="fcc94-151">**응용 프로그램은 이러한 권장 사항을 고려 하지 않는 경우 hello 유효성 검사 프로세스를 전달 보장할 수 없습니다.**</span><span class="sxs-lookup"><span data-stu-id="fcc94-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="fcc94-152">데이터 푸시 처리(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="fcc94-152">Handle data push (optional)</span></span>
<span data-ttu-id="fcc94-153">응용 프로그램 toobe 수 tooreceive Reach 데이터 푸시를 원하는 tooimplement 두 이벤트의 hello EngagementReach 클래스 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="fcc94-154">각 메서드가 반환 되는 부울 값의 해당 hello 콜백에 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="fcc94-155">서비스는 hello 데이터 푸시 디스패치 후 피드백 tooits 백 엔드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="fcc94-156">Hello 콜백이 false를 반환 하면 hello `exit` 피드백 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="fcc94-157">그렇지 않으면 `action`이(가) 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="fcc94-158">콜백이 없는 hello 이벤트에 대 한을 설정 하는 경우 hello `drop` 피드백 tooEngagement 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="fcc94-159">데이터 푸시에 대 한 여러 개의 차트 피드백 수 tooreceive engagement이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="fcc94-160">Tooset 여러 처리기는 이벤트를 하려는 경우에 hello 피드백은 모니터는 toohello 보낸 마지막 트랜잭션이 주의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="fcc94-161">이 경우 tooalways 권장 반환 hello 혼동 피드백 hello 프런트 엔드에 있는 동일한 값 tooavoid 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="fcc94-162">UI 사용자 지정(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="fcc94-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="fcc94-163">첫 번째 단계</span><span class="sxs-lookup"><span data-stu-id="fcc94-163">First step</span></span>
<span data-ttu-id="fcc94-164">Toocustomize hello reach UI을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="fcc94-165">toodo 따라서 해야 toocreate hello의 서브 클래스 `EngagementReachHandler` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="fcc94-166">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="fcc94-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="fcc94-167">다음의 hello hello 콘텐츠를 설정 `EngagementReach.Instance.Handler` 필드에 사용자 지정 개체와 프로그램 `App.xaml.cs` hello 내 클래스 `Application_Launching` 메서드.</span><span class="sxs-lookup"><span data-stu-id="fcc94-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="fcc94-168">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="fcc94-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="fcc94-169">Engagement는 기본적으로 자체 `EngagementReachHandler` 구현을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="fcc94-170">Toocreate 없는 고유한, 이렇게 하면 없는 toooverride 모든 메서드에 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="fcc94-171">hello 기본 동작은 tooselect hello Engagement 기준 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="fcc94-172">레이아웃</span><span class="sxs-lookup"><span data-stu-id="fcc94-172">Layouts</span></span>
<span data-ttu-id="fcc94-173">기본적으로 도달 범위는 hello DLL toodisplay hello 알림과 페이지의 hello 포함 리소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="fcc94-174">그러나 결정할 수 있습니다 toouse 고유한 리소스 tooreflect 브랜드 이러한 구성 요소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="fcc94-175">재정의할 수 `EngagementReachHandler` 프로그램 하위 클래스 tootell Engagement toouse 메서드 레이아웃이:</span><span class="sxs-lookup"><span data-stu-id="fcc94-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="fcc94-176">**샘플 코드:**</span><span class="sxs-lookup"><span data-stu-id="fcc94-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="fcc94-177">hello `CreateNotification` 메서드에서 null을 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="fcc94-178">hello 알림이 표시 되지 않습니다 및 hello reach 캠페인에 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="fcc94-179">toosimplify 레이아웃 구현에 제공 하 고 코드에 대 한 기초로 사용 될 수 있는 고유한 xaml입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="fcc94-180">Hello Engagement SDK 보관 파일에 있는 (/ src/reach /).</span><span class="sxs-lookup"><span data-stu-id="fcc94-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="fcc94-181">동일 hello 정확 하 게 사용 하는 제공 하는 hello 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="fcc94-182">따라서 toomodify을를 직접 없습니다 toochange hello 네임 스페이스를 제거 하 고 이름을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="fcc94-183">알림 위치</span><span class="sxs-lookup"><span data-stu-id="fcc94-183">Notification position</span></span>
<span data-ttu-id="fcc94-184">기본적으로 앱 내 알림이 hello 아래쪽 hello 응용 프로그램의 왼쪽에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="fcc94-185">Hello를 재정의 하 여이 동작을 변경할 수 `GetNotificationPosition` hello 방식의 `EngagementReachHandler` 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="fcc94-186">Hello를 선택할 수 있으며 현재 `BOTTOM` (기본값) 및 `TOP` 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="fcc94-187">시작 메시지</span><span class="sxs-lookup"><span data-stu-id="fcc94-187">Launch message</span></span>
<span data-ttu-id="fcc94-188">사용자가 시스템 알림 (알림)를 클릭 하면 서비스를 실행 하는 hello 응용 프로그램, 부하 hello 내용의 hello 메시지를 푸시하고 캠페인에 해당 하는 hello에 대 한 hello 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="fcc94-189">Hello 시작 되지 않도록 (에 따라 네트워크의 속도 hello) hello 페이지의 hello 응용 프로그램 및 hello 표시 사이의 지연 시간이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="fcc94-190">로드 하는 문제가 tooindicate toohello 사용자, 진행률 표시줄 또는 진행률 표시기 등의 시각적 정보를 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="fcc94-191">Engagement에서 이 과정을 직접 처리할 수는 없으며, 처리에 사용할 수 있는 몇 가지 처리기를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="fcc94-192">tooimplement 콜백 hello을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="fcc94-193">Hello 콜백에서 설정할 수 있습니다 프로그램 `Application_Launching` 방식의 프로그램 `App.xaml.cs` hello 전에 가급적 파일 `EngagementReach.Instance.Init()` 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="fcc94-194">각 처리기는 UI 스레드 hello에 의해 호출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fcc94-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="fcc94-195">않아도 tooworry MessageBox 또는 다른 UI 관련를 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="fcc94-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[응용 프로그램 정책]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[특정 응용 프로그램 종류에 대 한 추가 요구 사항이]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

