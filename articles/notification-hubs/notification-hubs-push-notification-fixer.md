---
title: "Azure 알림 허브 - 진단 지침"
description: "Azure 알림 허브의 일반적인 문제를 진단하는 방법에 대한 지침입니다."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 32e3a2e6f840afd865375a622cfae0d33ba65090
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a><span data-ttu-id="89d91-103">Azure 알림 허브 - 진단 지침</span><span class="sxs-lookup"><span data-stu-id="89d91-103">Azure Notification Hubs - Diagnosis guidelines</span></span>
## <a name="overview"></a><span data-ttu-id="89d91-104">개요</span><span class="sxs-lookup"><span data-stu-id="89d91-104">Overview</span></span>
<span data-ttu-id="89d91-105">Azure 알림 허브 고객으로부터 가장 많이 듣는 질문 중 하나는 클라이언트 장치에 나타나는 고객의 응용 프로그램 백엔드에서 보낸 알림을 보지 못하는 이유와 알림이 삭제되는 위치와 이유 그리고 이 문제를 해결하는 방법에 대한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-105">One of the most common questions we hear from Azure Notification Hubs customers is how to figure out why they don’t see a notification sent from their application backend appear on the client device - where and why notifications were dropped and how to fix this.</span></span> <span data-ttu-id="89d91-106">이 문서에서는 장치에서 알림이 삭제되거나 끝나지 않는 다양한 이유에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-106">In this article we will go through the various reasons why notifications may get dropped or do not end up on the devices.</span></span> <span data-ttu-id="89d91-107">또한 근본 원인을 분석하여 해결책을 찾아낼 수 있는 방법도 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-107">We will also look through ways in which you can analyze and figure out the root cause.</span></span> 

<span data-ttu-id="89d91-108">먼저, Azure 알림 허브에서 장치로 알림을 푸시하는 방법을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-108">First of all, it is critical to understand how Azure Notification Hubs pushes out notifications to the devices.</span></span>
![][0]

<span data-ttu-id="89d91-109">일반적인 보내기 알림 흐름에서 메시지는 **응용 프로그램 백 엔드**에서 **Azure Notification Hub(NH)**로 전송됩니다. 이어서 "대상"(예: 푸시 알림을 받아야 하는 모든 등록)을 결정하기 위해 구성된 태그 및 태그 식을 고려하는 모든 등록에 대해 일부 처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-109">In a typical send notification flow, the message is sent from the **application backend** to **Azure Notification Hub (NH)** which in turn does some processing on all the registrations taking into account the configured tags & tag expressions to determine "targets" i.e. all the registrations that need to receive the push notification.</span></span> <span data-ttu-id="89d91-110">이러한 등록은 지원되는 일부 또는 모든 플랫폼(iOS, Google, Windows, Windows Phone, Kindle 및 중국 Android용 Baidu)에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-110">These registrations can span across any or all of our supported platforms - iOS, Google, Windows, Windows Phone, Kindle and Baidu for China Android.</span></span> <span data-ttu-id="89d91-111">대상이 설정되면 NH에서 여러 등록 일괄 처리로 분할된 알림을 특정 장치 플랫폼 **푸시 알림 서비스(PNS** - Apple용 APNS, Google용 GCM 등)로 푸시합니다. NH는 구성 알림 허브 페이지의 Azure 클래식 포털에서 설정한 자격 증명을 기반으로 개별 PNS를 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-111">Once the targets are established, NH then pushes out notifications, split across multiple batch of registrations, to the device platform specific **Push Notification Service (PNS)** - e.g. APNS for Apple, GCM for Google etc. NH authenticates with the respective PNS based on the credentials you set in the Azure Classic Portal on the Configure Notification Hub page.</span></span> <span data-ttu-id="89d91-112">그런 다음 PNS는 해당 알림을 개별 **클라이언트 장치**로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-112">The PNS then forwards the notifications to the respective **client devices**.</span></span> <span data-ttu-id="89d91-113">이 방법은 푸시 알림을 전달하기 위한 플랫폼 권장 방식이며 최종 알림 레그는 플랫폼 PNS와 장치에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-113">This is the platform recommended way to deliver push notifications and note that the final leg of notification delivery takes place between the platform PNS and the device.</span></span> <span data-ttu-id="89d91-114">따라서 4가지 주요 구성 요소(*클라이언트*, *응용 프로그램 백 엔드*, *Azure Notification Hubs(NH)* 및 *푸시 알림 서비스(PNS)*)가 있으며 이러한 알림은 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-114">Therefore we have four major components - *client*, *application backend*, *Azure Notification Hubs (NH)* and *Push Notification Services (PNS)* and any of these may cause notifications getting dropped.</span></span> <span data-ttu-id="89d91-115">이 아키텍처에 대한 자세한 내용은 [Notification Hubs 개요]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-115">More details on this architecture is available on [Notification Hubs Overview].</span></span>

<span data-ttu-id="89d91-116">알림을 전달하지 못하는 현상은 초기 테스트/준비 단계에서 구성에 문제가 있어서 발생할 수 있고 응용 프로그램이 심층적이거나 패턴 문제가 있어서 전체 또는 일부 알림이 삭제될 수 있는 프로덕션에서 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-116">Failure to deliver notifications may happen during the initial test/staging phase which may indicate a configuration issue or it may happen in production where either all or some of the notifications may be getting dropped indicating some deeper application or messaging pattern issue.</span></span> <span data-ttu-id="89d91-117">이 섹션에서는 일반적인 경우에서 매우 드문 경우까지 다양한 알림 삭제 시나리오에 대해 살펴보도록 하겠습니다. 이 중에는 확실하다고 느끼는 것도 있고 심하지 않다고 생각되는 것도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-117">In the section, below we will look at various dropped notifications scenarios ranging from common to the rarer kind, some of which you may find obvious and some others not so much.</span></span> 

## <a name="azure-notifications-hub-mis-configuration"></a><span data-ttu-id="89d91-118">Azure 알림 허브의 잘못된 구성</span><span class="sxs-lookup"><span data-stu-id="89d91-118">Azure Notifications Hub mis-configuration</span></span>
<span data-ttu-id="89d91-119">Azure 알림 허브는 각 PNS에 알림을 성공적으로 보낼 수 있도록 개발자의 응용 프로그램 컨텍스트에서 자신을 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-119">Azure Notification Hubs needs to authenticate itself in the context of the developer's application to be able to successfully send notifications to the respective PNS.</span></span> <span data-ttu-id="89d91-120">이렇게 하려면 개발자가 각 플랫폼(Google, Apple, Windows 등)에서 개발자 계정을 만든 다음 포털의 알림 허브 구성 섹션에서 구성해야 하는 자격 증명을 얻는 응용 프로그램을 등록하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-120">This is made possible by the developer creating a developer account with the respective platform (Google, Apple, Windows etc) and then registering their application where they get credentials which need to be configured in the portal under Notification Hubs configuration section.</span></span> <span data-ttu-id="89d91-121">알림을 만들지 않은 경우 먼저 특정 플랫폼 개발자 계정에서 생성한 응용 프로그램과 일치하는 알림 허브에 올바른 자격 증명이 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-121">If no notifications are making through, first step should be to ensure that the correct credentials are configured in the Notification Hub matching them with the application created under their platform specific developer account.</span></span> <span data-ttu-id="89d91-122">[자습서 시작하기] 는 단계별 방식으로 이 프로세스를 이해하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-122">You will find our [Getting Started Tutorials] useful to go over this process in a step by step manner.</span></span> <span data-ttu-id="89d91-123">다음은 잘못된 구성의 몇가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-123">Here are some common mis-configurations:</span></span>

1. <span data-ttu-id="89d91-124">**일반**</span><span class="sxs-lookup"><span data-stu-id="89d91-124">**General**</span></span>
   
    <span data-ttu-id="89d91-125">a) 알림 허브 이름(오타 없이)이 다음과 동일한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-125">a) Make sure that your notification hub name (without typos) is the same:</span></span>
   
   * <span data-ttu-id="89d91-126">클라이언트에서 등록하는 위치</span><span class="sxs-lookup"><span data-stu-id="89d91-126">Where you are registering from the client,</span></span> 
   * <span data-ttu-id="89d91-127">백엔드에서 알림을 보내는 위치</span><span class="sxs-lookup"><span data-stu-id="89d91-127">Where you are sending notifications from the backend,</span></span>  
   * <span data-ttu-id="89d91-128">PNS 자격 증명 구성한 위치</span><span class="sxs-lookup"><span data-stu-id="89d91-128">Where you have configured the PNS credentials and</span></span> 
   * <span data-ttu-id="89d91-129">클라이언트와 백엔드에서 SAS 자격 증명을 구성한 사람</span><span class="sxs-lookup"><span data-stu-id="89d91-129">Whose SAS credentials you have configured on the client and the backend.</span></span> 
     
     <span data-ttu-id="89d91-130">b) 클라이언트와 응용 프로그램 백엔드에서 올바른 SAS 구성 문자열을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-130">b) Make sure that you are using the correct SAS configuration strings on the client and the application backend.</span></span> <span data-ttu-id="89d91-131">경험으로 보아, 클라이언트에서는 **DefaultListenSharedAccessSignature**를 사용해야 하며 응용 프로그램 백 엔드에서는 **DefaultFullSharedAccessSignature**를 사용해야 합니다.(NH에 알림을 보낼 수 있도록 권한을 제공)</span><span class="sxs-lookup"><span data-stu-id="89d91-131">As a rule of thumb, you must be using the **DefaultListenSharedAccessSignature** on the client and **DefaultFullSharedAccessSignature** on the application backend (which gives permission to be able to send notification to the NH)</span></span>
2. <span data-ttu-id="89d91-132">**Apple 푸시 알림 서비스(APNS) 구성**</span><span class="sxs-lookup"><span data-stu-id="89d91-132">**Apple Push Notification Service (APNS) configuration**</span></span>
   
    <span data-ttu-id="89d91-133">서로 다른 2개의 허브를 유지해야 하는데, 하나는 프로덕션에 다른 하나는 테스트 목적으로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-133">You must maintain two different hubs - one for production and another for testing purpose.</span></span> <span data-ttu-id="89d91-134">즉, 샌드박스 환경에서 사용하려는 인증서를 별도의 허브에 업로드하고 프로덕션에서 사용하려는 인증서를 별도의 허브에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-134">This means uploading the certificate you are going to use in sandbox environment to a separate hub and the certificate you are going to use in production to a separate hub.</span></span> <span data-ttu-id="89d91-135">알림을 보내는 데 완전히 실패할 수 있기 때문에 동일한 허브에 다른 종류의 인증서를 업로드하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="89d91-135">Do not try to upload different types of certificates to the same hub as it may cause notification failures down the line.</span></span> <span data-ttu-id="89d91-136">실수로 동일한 허브에 다른 종류의 인증서를 업로드한 위치를 직접 찾으려면 허브를 삭제하고 새로 고침하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-136">If you do find yourself in a position where you have inadvertently uploaded different types of certificate to the same hub, it is recommended to delete the hub and start fresh.</span></span> <span data-ttu-id="89d91-137">어떤 이유로 최소한 허브를 삭제할 수 없는 경우 허브에서 기존의 모든 등록을 삭제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-137">If for some reason, you are not able to delete the hub then at the very least, you must delete all the existing registrations from the hub.</span></span> 
3. <span data-ttu-id="89d91-138">**메시징 GCM(Google Cloud) 구성**</span><span class="sxs-lookup"><span data-stu-id="89d91-138">**Google Cloud Messaging (GCM) configuration**</span></span> 
   
    <span data-ttu-id="89d91-139">a) 클라우드 프로젝트에서 "Android용 Google 클라우드 메시징"을 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-139">a) Make sure that you are enabling "Google Cloud Messaging for Android" under your cloud project.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="89d91-140">b) NH가 GCM을 인증하는 데 사용할 자격 증명을 가져오는 동안 "서버 키"를 만들었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-140">b) Make sure that you create a "Server Key" while obtaining the credentials which NH will use to authenticate with GCM.</span></span> 
   
    ![][3]
   
    <span data-ttu-id="89d91-141">c) 대시보드에서 얻을 수 있는 완전히 숫자 엔터티인 클라이언트에서 "프로젝트 ID"를 구성했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-141">c) Make sure that you have configured "Project ID" on the client which is an entirely numerical entity that you can obtain from the dashboard:</span></span>
   
    ![][1]

## <a name="application-issues"></a><span data-ttu-id="89d91-142">응용 프로그램 문제</span><span class="sxs-lookup"><span data-stu-id="89d91-142">Application issues</span></span>
1) <span data-ttu-id="89d91-143">**태그/태그 식**</span><span class="sxs-lookup"><span data-stu-id="89d91-143">**Tags/ Tag expressions**</span></span>

<span data-ttu-id="89d91-144">태그 또는 태그 식을 사용하여 청중을 분할하는 경우 알림을 보낼 때 보내기 호출에서 지정하는태그/태그 식을 기반으로 찾을 수 있는 대상은 항상 없습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-144">If you are using tags or tag expressions to segment your audience, it is always possible that when you are sending the notification, there is no target being found based on the tags/tag expressions you are specifying in your send call.</span></span> <span data-ttu-id="89d91-145">알림을 보낸 다음 해당 등록을 가진 클라이언트에서만 알림 수신을 확인할 경우 일치하는 태그가 있는지 확인하기 위해 등록을 검토하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-145">It is best to review your registrations to ensure that there are tags which match when you send notification and then verify the notification receipt only from the clients with those registrations.</span></span> <span data-ttu-id="89d91-146">예:</span><span class="sxs-lookup"><span data-stu-id="89d91-146">E.g.</span></span> <span data-ttu-id="89d91-147">NH에서 한 모든 등록이 "Politics"를 말하는 태그로 완료되었고 "Sports" 태그로 알림을 보내는 경우 어떤 장치로도 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-147">if all your registrations with NH were done with say tag "Politics" and you are sending a notification with tag "Sports", it will not be sent to any device.</span></span> <span data-ttu-id="89d91-148">복잡한 경우에는 "태그 A" 또는 "태그 B"로만 등록한 태그 식뿐만 아니라 "태그 A && 태그 B"를 대상으로 알림을 보내는 경우도 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-148">A complex case could involve tag expressions where you only registered with "Tag A" OR "Tag B" but while sending notifications, you are targeting "Tag A && Tag B".</span></span> <span data-ttu-id="89d91-149">아래의 자체 진단 팁 섹션에는 사용자 등록을 등록에 포함된 태그와 함께 검토할 수 있는 방법을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-149">In the self-diagnose tips section below, there are ways in which you can review your registrations along with the tags they have.</span></span> 

2) <span data-ttu-id="89d91-150">**템플릿 문제**</span><span class="sxs-lookup"><span data-stu-id="89d91-150">**Template issues**</span></span>

<span data-ttu-id="89d91-151">템플릿을 사용하는 경우 [템플릿 지침]에 설명된 지침을 따르는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-151">If you are using templates then ensure that you are following the guidelines described at [Template guidance].</span></span> 

3) <span data-ttu-id="89d91-152">**잘못된 등록**</span><span class="sxs-lookup"><span data-stu-id="89d91-152">**Invalid registrations**</span></span>

<span data-ttu-id="89d91-153">알림 허브가 올바르게 구성되었고 모든 태그/태그 식이 올바르게 사용되어 알림을 보내야 하는 유효한 대상을 찾았다고 가정하고 NH는 여러 일괄 처리를 병렬로 시작하며 각 일괄 처리는 등록 집합에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-153">Assuming the Notification Hub was configured correctly and any tags/tag expressions were used correctly resulting in the find of valid targets to which the notifications need to be sent, NH fires off several processing batches in parallel - each batch sending messages to a set of registrations.</span></span> 

> [!NOTE]
> <span data-ttu-id="89d91-154">병렬로 처리했기 때문에 알림이 전달되는 순서는 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-154">Since we do the processing in parallel, we don’t guarantee the order in which the notifications will be delivered.</span></span> 
> 
> 

<span data-ttu-id="89d91-155">이제 Azure 알림 허브는 "최대 한 번의" 메시지 전달 모델에 대해 최적화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-155">Now Azure Notifications Hub is optimized for an "at-most once" message delivery model.</span></span> <span data-ttu-id="89d91-156">즉, 장치에 알림이 두 번 이상 전달되지 않도록 중복 제거를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-156">This means that we attempt a de-duplication so that no notifications are delivered more than once to a device.</span></span> <span data-ttu-id="89d91-157">이렇게 하려면 등록을 확인하고 실제로 PNS에 메시지를 보내기 전에 장치 식별자당 하나의 메시지만 보냈는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-157">To ensure this we look through the registrations and make sure that only one message is sent per device identifier before actually sending the message to the PNS.</span></span> <span data-ttu-id="89d91-158">각 일괄 처리는 PNS로 보내지고 이어서 등록을 수락하고 유효성을 검사하기 때문에 일괄 처리에 있는 하나 이상의 등록에서 오류를 탐지하여 이 오류를 Azure NH로 반환한 다음 처리를 중지시켜 일괄 처리가 완전히 삭제되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-158">As each batch is sent to the PNS, which in turn is accepting and validating the registrations, it is possible that the PNS detects an error with one or more of the registrations in a batch, returns an error to Azure NH and stops processing thereby dropping that batch completely.</span></span> <span data-ttu-id="89d91-159">TCP 스트림 프로토콜을 사용하는 APNS와 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-159">This is especially true with APNS which uses a TCP stream protocol.</span></span> <span data-ttu-id="89d91-160">최대 한 번의 배달에 최적화되어 있지만 이 경우에는 데이터베이스에서 오류가 발생한 등록을 제거한 다음 해당 배치의 나머지 장치에 대해 알림 배달을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-160">Although we are optimized for at-most once delivery, in this case we remove the faulting registration from our database and then retry notification delivery for the rest of the devices in that batch.</span></span>

<span data-ttu-id="89d91-161">Azure Notification Hubs REST API를 사용하는 등록 시 실패한 배달 시도에 대해 오류 정보를 확인할 수 있습니다. [메시지별 원격 분석: 알림 메시지 원격 분석 가져오기](https://msdn.microsoft.com/library/azure/mt608135.aspx) 및 [PNS 피드백](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span><span class="sxs-lookup"><span data-stu-id="89d91-161">You can get error information for the failed delivery attempt against a registration using the Azure Notification Hubs REST APIs: [Per Message Telemetry: Get Notification Message Telemetry](https://msdn.microsoft.com/library/azure/mt608135.aspx) and [PNS Feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span></span> <span data-ttu-id="89d91-162">예제 코드는 [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89d91-162">See the [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) for example code.</span></span>

## <a name="pns-issues"></a><span data-ttu-id="89d91-163">PNS 문제</span><span class="sxs-lookup"><span data-stu-id="89d91-163">PNS issues</span></span>
<span data-ttu-id="89d91-164">각 PNS에서 알림 메시지를 받으면 해당 알림을 장치로 보내는 것은 PNS의 책임입니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-164">Once the notification message has been received by the respective PNS then it is its responsibility to deliver the notification to the device.</span></span> <span data-ttu-id="89d91-165">Azure 알림 허브는 여기에 관여하지 않으며 알림이 장치로 전달되는 동안에는 제어하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-165">Azure Notification Hubs is out of the picture here and has no control on when or if the notification is going to be delivered to the device.</span></span> <span data-ttu-id="89d91-166">플랫폼 알림 서비스는 꽤 경고하므로 알림은 PNS로부터 몇 초 이내에 장치에 도달하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-166">Since the platform notification services are pretty robust, notifications do tend to reach the devices in a few seconds from the PNS.</span></span> <span data-ttu-id="89d91-167">그러나 PNS가 제한하는 경우 Azure 알림 허브는 기하급수적인 백오프 전략을 적용하고 PNS가 30분 안에 도달할 수 없을 경우 해당 메시지를 영구적으로 만료하여 삭제하기 위한 정책을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-167">If the PNS however is throttling then Azure Notification Hubs does apply an exponential back off strategy and if the PNS remains unreachable for 30 min then we have a policy in place to expire and drop those messages permanently.</span></span> 

<span data-ttu-id="89d91-168">PNS가 알림을 전달하려고 하지만 장치가 오프라인일 경우 PNS가 일정 시간 동안 알림을 저장했다가 사용할 수 있을 때 장치로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-168">If a PNS attempts to deliver a notification but the device is offline, the notification is stored by the PNS for a limited period of time, and delivered to the device when it becomes available.</span></span> <span data-ttu-id="89d91-169">특정 앱에 대한 최근 알림 하나만 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-169">Only one recent notification for a particular app is stored.</span></span> <span data-ttu-id="89d91-170">장치가 오프라인일 때 여러 알림을 전송하는 경우 각 새 알림이 이전 알림을 삭제하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-170">If multiple notifications are sent while the device is offline, each new notification causes the prior notification to be discarded.</span></span> <span data-ttu-id="89d91-171">가장 최신 알림만 유지하는 이 동작은 APNS에서는 결합 알림 그리고 GCM에서는 축소 알림(축소 키 사용)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-171">This behavior of keeping only the newest notification is referred to as coalescing notifications in APNS and collapsing in GCM (which uses a collapsing key).</span></span> <span data-ttu-id="89d91-172">장치가 오랫동안 오프라인 상태일 경우 저장된 모든 알림이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-172">If the device remains offline for a long time, any notifications that were being stored for it are discarded.</span></span> <span data-ttu-id="89d91-173">소스 - [APNS 지침] & [GCM 지침]</span><span class="sxs-lookup"><span data-stu-id="89d91-173">Source - [APNS guidance] & [GCM guidance]</span></span>

<span data-ttu-id="89d91-174">Azure 알림 허브를 사용하면 일반 `SendNotification` API(예: .NET SDK용 `SendNotificationAsync`)를 사용하여 HTTP 헤더를 통해 결합 키를 전달할 수 있고 각 PNS에 그대로 전달하는 HTTP 헤더를 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-174">With Azure Notification Hubs - you can pass a coalescing key via an HTTP header using the generic `SendNotification` API (e.g. for .NET SDK – `SendNotificationAsync`) which also takes HTTP headers which are passed as is to the respective PNS.</span></span> 

## <a name="self-diagnose-tips"></a><span data-ttu-id="89d91-175">자체 진단 팁</span><span class="sxs-lookup"><span data-stu-id="89d91-175">Self-diagnose tips</span></span>
<span data-ttu-id="89d91-176">여기에서는 모든 알림 허브 문제를 진단하여 근본 원인을 알아내기 위한 다양한 방안을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-176">Here we will examine the various avenues to diagnose and root cause any Notification Hub issues:</span></span>

### <a name="verify-credentials"></a><span data-ttu-id="89d91-177">자격 증명 확인</span><span class="sxs-lookup"><span data-stu-id="89d91-177">Verify credentials</span></span>
1. <span data-ttu-id="89d91-178">**PNS 개발자 포털**</span><span class="sxs-lookup"><span data-stu-id="89d91-178">**PNS developer portal**</span></span>
   
    <span data-ttu-id="89d91-179">해당 PNS 개발자 포털(APNS, GCM WNS 등)에서 당사의 [자습서 시작하기]를 사용하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-179">Verify them at the respective PNS developer portal (APNS, GCM, WNS etc) using our [Getting Started Tutorials].</span></span>
2. <span data-ttu-id="89d91-180">**Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="89d91-180">**Azure Classic portal**</span></span>
   
    <span data-ttu-id="89d91-181">구성 탭으로 이동하여 자격 증명을 검토하고 PNS 개발자 포털에서 얻은 자격 증명과 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-181">Go to the Configure tab to review and match the credentials with those obtained from the PNS developer portal.</span></span> 
   
    ![][4]

### <a name="verify-registrations"></a><span data-ttu-id="89d91-182">등록 확인</span><span class="sxs-lookup"><span data-stu-id="89d91-182">Verify registrations</span></span>
1. <span data-ttu-id="89d91-183">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="89d91-183">**Visual Studio**</span></span>
   
    <span data-ttu-id="89d91-184">개발에 Visual Studio를 사용하는 경우 Microsoft Azure에 연결한 다음 "서버 탐색기"에서 알림 허브를 포함한 다양한 Azure 서비스를 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-184">If you use Visual Studio for development then you can connect to Microsoft Azure and view and manage a bunch of Azure services including Notifications Hub from "Server Explorer".</span></span> <span data-ttu-id="89d91-185">개발/테스트 환경에서 주로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-185">This is primarily useful for your dev/test environment.</span></span> 
   
    ![][9]
   
    <span data-ttu-id="89d91-186">허브에서 플랫폼, 네이티브 또는 템플릿 등록, 태그, PNS 식별자, 등록 id 및 만료 날짜별로 보기 좋게 분류된 모든 등록을 보고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-186">You can view and manage all the registrations in your hub which are nicely categorized for platform, native or template registration, any tags, PNS identifier, registration id and the expiration date.</span></span> <span data-ttu-id="89d91-187">또한 즉석에서 등록을 편집할 수도 있는데, 태그를 편집하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-187">You can also edit a registration on the fly - which is useful say if you want to edit any tags.</span></span> 
   
    ![][8]
   
   > [!NOTE]
   > <span data-ttu-id="89d91-188">등록을 편집할 수 있는 visual Studio 기능은 제한된 수의 등록을 가진 개발/테스트 동안에만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-188">Visual Studio functionality to edit registrations should only be used during dev/test with limited number of registrations.</span></span> <span data-ttu-id="89d91-189">등록을 대량으로 수정해야 할 경우 [등록 내보내기/가져오기](https://msdn.microsoft.com/library/dn790624.aspx)</span><span class="sxs-lookup"><span data-stu-id="89d91-189">If there arises a need to fix your registrations in bulk, consider using the Export/Import registration functionality described here - [Export/Import Registrations](https://msdn.microsoft.com/library/dn790624.aspx)</span></span>
   > 
   > 
2. <span data-ttu-id="89d91-190">**서비스 버스 탐색기**</span><span class="sxs-lookup"><span data-stu-id="89d91-190">**Service Bus explorer**</span></span>
   
    <span data-ttu-id="89d91-191">많은 고객이 ServiceBus 탐색기에 설명된 [ServiceBus 탐색기]를 사용하여 알림 허브를 보고 관리합니다</span><span class="sxs-lookup"><span data-stu-id="89d91-191">Many customers use ServiceBus explorer described here - [ServiceBus Explorer] for viewing and managing their notification hub.</span></span> <span data-ttu-id="89d91-192">Code.microsoft.com - [ServiceBus 탐색기 코드]에서 사용할 수 있는 공개 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-192">It is an open source project available from code.microsoft.com - [ServiceBus Explorer code]</span></span>

### <a name="verify-message-notifications"></a><span data-ttu-id="89d91-193">알림 메시지 확인</span><span class="sxs-lookup"><span data-stu-id="89d91-193">Verify message notifications</span></span>
1. <span data-ttu-id="89d91-194">**Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="89d91-194">**Azure Classic Portal**</span></span>
   
    <span data-ttu-id="89d91-195">"디버그" 탭으로 이동하여 모든 서비스를 백엔드 및 실행하지 않고 클라이언트에 테스트 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-195">You can go to the "Debug" tab to send test notifications to your clients without needing any service backend up and running.</span></span> 
   
    ![][7]
2. <span data-ttu-id="89d91-196">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="89d91-196">**Visual Studio**</span></span>
   
    <span data-ttu-id="89d91-197">또한 Visual Studio의 comforts에서 테스트 알림을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-197">You can also send test notifications from the comforts of Visual Studio:</span></span>
   
    ![][10]
   
    <span data-ttu-id="89d91-198">자세한 내용은 다음 Visual Studio 알림 허브 Azure 탐색기 기능에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-198">You can read more on the Visual Studio Notification Hub Azure explorer functionality here -</span></span> 
   
   * <span data-ttu-id="89d91-199">[VS 서버 탐색기 개요]</span><span class="sxs-lookup"><span data-stu-id="89d91-199">[VS Server Explorer Overview]</span></span>
   * <span data-ttu-id="89d91-200">[VS 서버 탐색기 블로그 게시물 - 1]</span><span class="sxs-lookup"><span data-stu-id="89d91-200">[VS Server Explorer Blog post - 1]</span></span>
   * <span data-ttu-id="89d91-201">[VS 서버 탐색기 블로그 게시물 - 2]</span><span class="sxs-lookup"><span data-stu-id="89d91-201">[VS Server Explorer Blog post - 2]</span></span>

### <a name="debug-failed-notifications-review-notification-outcome"></a><span data-ttu-id="89d91-202">실패한 알림 디버그/알림 결과 검토</span><span class="sxs-lookup"><span data-stu-id="89d91-202">Debug failed notifications/ Review notification outcome</span></span>
<span data-ttu-id="89d91-203">**EnableTestSend 속성**</span><span class="sxs-lookup"><span data-stu-id="89d91-203">**EnableTestSend property**</span></span>

<span data-ttu-id="89d91-204">알림 허브를 통해 알림을 보내면 처음에는 NH에서 처리하여 모든 대상을 파악하기를 기다리기만 했다가 결국에는 NH가 PNS로 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-204">When you send a notification via Notification Hubs, initially it just gets queued up for NH to do processing to figure out all its targets and then eventually NH sends it to the PNS.</span></span> <span data-ttu-id="89d91-205">즉, REST API 또는 클라이언트 SDK 중 하나를 사용하는 경우 송신 호출의 성공적으로 반환은 메시지가 알림 허브에 성공적으로 대기한다는 것만을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-205">This means that when you are using REST API or any of the client SDK, the successful return of your send call only means that the message has been successfully queued up with Notification Hub.</span></span> <span data-ttu-id="89d91-206">NH가 결국 PNS로 메시지를 보냈을 때 어떤 일이 발생하는지에 대한 통찰력을 제공하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-206">It doesn’t give an insight into what happened when NH eventually got to send the message to PNS.</span></span> <span data-ttu-id="89d91-207">사용자 알림이 클라이언트 장치에 도착하지 않을 경우 NH가 PNS로 메시지를 보내려고 시도했을 때 오류가 발생했을 수 있습니다. 예를 들어, 페이로드 크기가 PNS에서 허용되는 최대값을 초과했거나 NH에서 구성된 자격 증명이 잘못되는 등의 가능성이 있습니다. PNS 오류에 대한 통찰력을 얻기 위해 [EnableTestSend 기능]이라는 속성을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-207">If your notification is not arriving at the client device, there is a possibility that when NH tried to deliver the message to PNS, there was an error e.g. the payload size exceeded the maximum allowed by the PNS or the credentials configured in NH are invalid etc. To get an insight into the PNS errors, we have introduced a property called [EnableTestSend feature].</span></span> <span data-ttu-id="89d91-208">이 속성은 포털 또는 Visual Studio 클라이언트에서 테스트 메시지를 보낼 때 자동으로 활성화되기 때문에 자세한 디버깅 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-208">This property is automatically enabled when you send test messages from the portal or Visual Studio client and therefore allows you to see detailed debugging information.</span></span> <span data-ttu-id="89d91-209">현재 사용할 수 있는 .NET SDK의 예를 수행하는 API를 통해 이를 사용할 수 있고 결국 모든 클라이언트 SDK에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-209">You can use this via APIs taking the example of the .NET SDK where it is available now and will be added to all client SDKs eventually.</span></span> <span data-ttu-id="89d91-210">이를 REST 호출과 함께 사용하려면 예를 들어, 송신 호출 끝에 "test"라는 쿼리 문자열 매개변수를 추가 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-210">To use this with the REST call, simply append a querystring parameter called "test" at the end of your send call e.g.</span></span> 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

<span data-ttu-id="89d91-211">*예(.NET SDK)*</span><span class="sxs-lookup"><span data-stu-id="89d91-211">*Example (.NET SDK)*</span></span>

<span data-ttu-id="89d91-212">.NET SDK를 사용하여 네이티브 토스트 알림을 보낸다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-212">Suppose you are using .NET SDK to send a native toast notification:</span></span>

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

<span data-ttu-id="89d91-213">`result.State`는 푸시에서 발생하는 일에 대한 이해 없이 실행 끝에서 `Enqueued` 상태를 나타내기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-213">`result.State` will simply state `Enqueued` at the end of the execution without any insight into what happened to your push.</span></span> <span data-ttu-id="89d91-214">이제 `NotificationHubClient`을(를) 초기화하는 동안 `EnableTestSend` 부울 속성을 사용할 수 있고 알림을 보내는 동안 발생한 PNS 오류에 대한 자세한 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-214">Now you can use the `EnableTestSend` boolean property while initializing the `NotificationHubClient` and can get detailed status about the PNS errors encountered while sending the notification.</span></span> <span data-ttu-id="89d91-215">보내기 호출을 반환할 때는 NH가 PNS로 알림을 전달하여 결과를 결정한 후에만 반환하기 때문에 시간이 추가로 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-215">The send call here will take additional time to return because it is only returning after NH has delivered the notification to PNS to determine the outcome.</span></span> 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

<span data-ttu-id="89d91-216">*샘플 출력*</span><span class="sxs-lookup"><span data-stu-id="89d91-216">*Sample Output*</span></span>

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    The Token obtained from the Token Provider is wrong

<span data-ttu-id="89d91-217">이 메시지는 알림 허브에 잘못된 자격 증명이 구성되었거나 허브에 있는 등록에 문제가 있다는 것을 나타내며 메시지를 보내기 전에 이 구성을 삭제하고 클라이언트가 다시 만들도록 하려면 권장된 코스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-217">This message indicates either invalid credentials are configured in the notification hub or an issue with the registrations on the hub and the recommended course would be to delete this registration and let the client recreate it before sending the message.</span></span> 

> [!NOTE]
> <span data-ttu-id="89d91-218">이 속성의 사용은 엄격하게 제한되므로 제한된 등록 집합을 가진 개발/테스트 환경에서만 이 속성을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-218">Note that the use of this property is heavily throttled and so you must only use this in dev/test environment with limited set of registrations.</span></span> <span data-ttu-id="89d91-219">10개의 장치에만 디버그 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-219">We only send debug notifications to 10 devices.</span></span> <span data-ttu-id="89d91-220">분당 10개의 디버그 보내기만 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-220">We also have a limit of processing debug sends to be 10 per minute.</span></span> 
> 
> 

### <a name="review-telemetry"></a><span data-ttu-id="89d91-221">원격 분석 검토</span><span class="sxs-lookup"><span data-stu-id="89d91-221">Review telemetry</span></span>
1. <span data-ttu-id="89d91-222">**Azure 클래식 포털 사용**</span><span class="sxs-lookup"><span data-stu-id="89d91-222">**Use Azure Classic Portal**</span></span>
   
    <span data-ttu-id="89d91-223">포털을 사용하면 알림 허브의 모든 활동에 대한 간략한 개요를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-223">The portal enables you to get a quick overview of all the activity on your Notification Hub.</span></span> 
   
    <span data-ttu-id="89d91-224">a) "대시보드" 탭에서 등록, 알림뿐만 아니라 플랫폼별 오류에 대한 집계 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-224">a) From the "dashboard" tab you can view an aggregated view of the registrations, notifications as well as errors per platform.</span></span> 
   
    ![][5]
   
    <span data-ttu-id="89d91-225">b) 또한 "모니터" 탭에서 다른 많은 플랫폼 특정 메트릭을 추가하여 특히 NH에서 PNS로 알림을 보내려고 할 때 반환된 PNS 특정 오류를 더 자세히 살펴볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-225">b) You can also add many other platform specific metrics from the "Monitor" tab to take a deeper look particularly at any PNS specific errors returned when NH tries to send the notification to the PNS.</span></span> 
   
    ![][6]
   
    <span data-ttu-id="89d91-226">c) **들어오는 메시지**, **등록 작업**, **성공한 알림** 검토를 시작으로 플랫폼별 탭으로 이동하여 PNS 특정 오류를 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-226">c) You should start with reviewing the **Incoming Messages**, **Registration Operations**, **Successful Notifications** and then go to per platform tab to review the PNS specific errors.</span></span> 
   
    <span data-ttu-id="89d91-227">d) 인증 설정에서 알림 허브를 잘못 구성한 경우 PNS 인증 오류가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-227">d) If you have the notification hub misconfigured with the authentication settings then you will see PNS Authentication Error.</span></span> <span data-ttu-id="89d91-228">이것은 PNS 자격 증명을 확인하는 좋은 표시입니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-228">This is a good indication to check the PNS credentials.</span></span> 

2) <span data-ttu-id="89d91-229">**프로그래밍 방식 액세스**</span><span class="sxs-lookup"><span data-stu-id="89d91-229">**Programmatic access**</span></span>

<span data-ttu-id="89d91-230">자세한 내용은 다음 참조</span><span class="sxs-lookup"><span data-stu-id="89d91-230">More details here -</span></span> 

* <span data-ttu-id="89d91-231">[프로그래밍 방식 원격 분석 액세스]</span><span class="sxs-lookup"><span data-stu-id="89d91-231">[Programmatic Telemetry Access]</span></span>
* <span data-ttu-id="89d91-232">[API 샘플을 통한 원격 분석 액세스]</span><span class="sxs-lookup"><span data-stu-id="89d91-232">[Telemetry Access via APIs sample]</span></span> 

> [!NOTE]
> <span data-ttu-id="89d91-233">**등록 내보내기/가져오기**, **API를 통한 원격 분석 액세스** 등의 여러 원격 분석 관련 기능은 표준 계층에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-233">Several telemetry related features like **Export/Import Registrations**, **Telemetry Access via APIs** etc are only available in Standard tier.</span></span> <span data-ttu-id="89d91-234">무료 또는 기본 계층에 있을 때 이러한 기능을 사용하려고 하면 REST API에서 직접 사용하는 경우 SDK 및 HTTP 403(금지됨)을 사용하는 동안 이 효과에 대한 예외 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-234">If you attempt to use these features if you are in Free or Basic tier then you will get exception message to this effect while using the SDK and an HTTP 403 (Forbidden) when using them directly from the REST APIs.</span></span> <span data-ttu-id="89d91-235">Azure 클래식 포털을 통해 표준 계층으로 이동했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="89d91-235">Make sure that you have moved up to Standard tier via Azure Classic Portal.</span></span>  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
<span data-ttu-id="89d91-236">[Notification Hubs 개요]: notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="89d91-236">[Notification Hubs Overview]: notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="89d91-237">[자습서 시작하기]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="89d91-237">[Getting Started Tutorials]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="89d91-238">[템플릿 지침]: https://msdn.microsoft.com/library/dn530748.aspx </span><span class="sxs-lookup"><span data-stu-id="89d91-238">[Template guidance]: https://msdn.microsoft.com/library/dn530748.aspx </span></span>
<span data-ttu-id="89d91-239">[APNS 지침]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4</span><span class="sxs-lookup"><span data-stu-id="89d91-239">[APNS guidance]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4</span></span>
<span data-ttu-id="89d91-240">[GCM 지침]: http://developer.android.com/google/gcm/adv.html</span><span class="sxs-lookup"><span data-stu-id="89d91-240">[GCM guidance]: http://developer.android.com/google/gcm/adv.html</span></span>
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
<span data-ttu-id="89d91-241">[ServiceBus 탐색기]: http://msdn.microsoft.com/library/dn530751.aspx</span><span class="sxs-lookup"><span data-stu-id="89d91-241">[ServiceBus Explorer]: http://msdn.microsoft.com/library/dn530751.aspx</span></span>
<span data-ttu-id="89d91-242">[ServiceBus 탐색기 코드]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a</span><span class="sxs-lookup"><span data-stu-id="89d91-242">[ServiceBus Explorer code]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a</span></span>
<span data-ttu-id="89d91-243">[VS 서버 탐색기 개요]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx </span><span class="sxs-lookup"><span data-stu-id="89d91-243">[VS Server Explorer Overview]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx </span></span>
<span data-ttu-id="89d91-244">[VS 서버 탐색기 블로그 게시물 - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs </span><span class="sxs-lookup"><span data-stu-id="89d91-244">[VS Server Explorer Blog post - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs </span></span>
<span data-ttu-id="89d91-245">[VS 서버 탐색기 블로그 게시물 - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ </span><span class="sxs-lookup"><span data-stu-id="89d91-245">[VS Server Explorer Blog post - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ </span></span>
<span data-ttu-id="89d91-246">[EnableTestSend 기능]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx</span><span class="sxs-lookup"><span data-stu-id="89d91-246">[EnableTestSend feature]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx</span></span>
<span data-ttu-id="89d91-247">[프로그래밍 방식 원격 분석 액세스]: http://msdn.microsoft.com/library/azure/dn458823.aspx</span><span class="sxs-lookup"><span data-stu-id="89d91-247">[Programmatic Telemetry Access]: http://msdn.microsoft.com/library/azure/dn458823.aspx</span></span>
<span data-ttu-id="89d91-248">[API 샘플을 통한 원격 분석 액세스]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel</span><span class="sxs-lookup"><span data-stu-id="89d91-248">[Telemetry Access via APIs sample]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel</span></span>

