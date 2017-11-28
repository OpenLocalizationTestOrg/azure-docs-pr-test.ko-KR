---
title: "알림 허브-aaaAzure 진단 지침"
description: "Azure 알림 허브와 toodiagnose 공통 발급 하는 방법에 대 한 지침입니다."
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
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a><span data-ttu-id="f7089-103">Azure 알림 허브 - 진단 지침</span><span class="sxs-lookup"><span data-stu-id="f7089-103">Azure Notification Hubs - Diagnosis guidelines</span></span>
## <a name="overview"></a><span data-ttu-id="f7089-104">개요</span><span class="sxs-lookup"><span data-stu-id="f7089-104">Overview</span></span>
<span data-ttu-id="f7089-105">Azure 알림 허브 고객의 도움을 주신 hello 가장 일반적인 질문 중 하나는 해당 응용 프로그램 백 엔드에서 보낸 알림의 표시 되지 않는 이유 아웃 toofigure hello 클라이언트 장치에 표시 되는 방식을 알림은 삭제 된 위치와 이유 및 방법 toofix이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-105">One of hello most common questions we hear from Azure Notification Hubs customers is how toofigure out why they don’t see a notification sent from their application backend appear on hello client device - where and why notifications were dropped and how toofix this.</span></span> <span data-ttu-id="f7089-106">이 문서에서 살펴보겠습니다 hello 알림을 삭제 되거나 끝나지 않는 이유는 다양 한 이유로 hello 장치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-106">In this article we will go through hello various reasons why notifications may get dropped or do not end up on hello devices.</span></span> <span data-ttu-id="f7089-107">또한 분석 하 고 hello 근본 원인을 알아낼 수 있는 방법을 통해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-107">We will also look through ways in which you can analyze and figure out hello root cause.</span></span> 

<span data-ttu-id="f7089-108">우선,는 중요 한 toounderstand 알림 toohello 장치 Azure 알림 허브를 푸시하는 방법</span><span class="sxs-lookup"><span data-stu-id="f7089-108">First of all, it is critical toounderstand how Azure Notification Hubs pushes out notifications toohello devices.</span></span>
![][0]

<span data-ttu-id="f7089-109">Hello에서 일반적인 송신 알림 흐름 hello 메시지를 보내 **응용 프로그램 백 엔드** 너무**Azure 알림 허브 (NH)** 차례로 고려 하는 모든 hello 등록에 약간의 처리를 수행 하는 계정 hello 즉, 모든 hello 등록 tooreceive hello 푸시 알림이 필요로 하는 태그 및 태그 식 toodetermine "대상 으로" 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-109">In a typical send notification flow, hello message is sent from hello **application backend** too**Azure Notification Hub (NH)** which in turn does some processing on all hello registrations taking into account hello configured tags & tag expressions toodetermine "targets" i.e. all hello registrations that need tooreceive hello push notification.</span></span> <span data-ttu-id="f7089-110">이러한 등록은 지원되는 일부 또는 모든 플랫폼(iOS, Google, Windows, Windows Phone, Kindle 및 중국 Android용 Baidu)에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-110">These registrations can span across any or all of our supported platforms - iOS, Google, Windows, Windows Phone, Kindle and Baidu for China Android.</span></span> <span data-ttu-id="f7089-111">NH 다음 푸시 알림을, 등록, 특정 toohello 장치 플랫폼의 여러 일괄 처리에서 분할 hello 대상, 설정 되 면 **푸시 알림 서비스 (PNS)** -Apple의 APNS, GCM Google 등에 대 한 예입니다. NH는 hello 알림 허브 구성 페이지에서 hello Azure 클래식 포털에서에서 설정 하는 hello 자격 증명을 기반으로 하는 각 PNS hello로 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-111">Once hello targets are established, NH then pushes out notifications, split across multiple batch of registrations, toohello device platform specific **Push Notification Service (PNS)** - e.g. APNS for Apple, GCM for Google etc. NH authenticates with hello respective PNS based on hello credentials you set in hello Azure Classic Portal on hello Configure Notification Hub page.</span></span> <span data-ttu-id="f7089-112">hello PNS에는 다음 각 hello 알림을 toohello 전달 **클라이언트 장치**합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-112">hello PNS then forwards hello notifications toohello respective **client devices**.</span></span> <span data-ttu-id="f7089-113">이것은 hello 플랫폼 toodeliver 푸시 알림 방법 및 참고는 hello 알림 배달의 최종 레그 hello 플랫폼 PNS 및 hello 장치 간에 발생 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-113">This is hello platform recommended way toodeliver push notifications and note that hello final leg of notification delivery takes place between hello platform PNS and hello device.</span></span> <span data-ttu-id="f7089-114">따라서 4가지 주요 구성 요소(*클라이언트*, *응용 프로그램 백 엔드*, *Azure Notification Hubs(NH)* 및 *푸시 알림 서비스(PNS)*)가 있으며 이러한 알림은 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-114">Therefore we have four major components - *client*, *application backend*, *Azure Notification Hubs (NH)* and *Push Notification Services (PNS)* and any of these may cause notifications getting dropped.</span></span> <span data-ttu-id="f7089-115">이 아키텍처에 대한 자세한 내용은 [Notification Hubs 개요]에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-115">More details on this architecture is available on [Notification Hubs Overview].</span></span>

<span data-ttu-id="f7089-116">오류 toodeliver 알림을 테스트/준비 단계 또는 구성 문제를 나타낼 수 있는의 일부 또는 모두이 알림을 hello 프로덕션 환경에서 발생할 수 있습니다 hello 초기 하는 동안 발생할 수 있습니다 가져오기 끊길 깊은 일부 응용 프로그램을 나타내는 또는 메시징 패턴 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-116">Failure toodeliver notifications may happen during hello initial test/staging phase which may indicate a configuration issue or it may happen in production where either all or some of hello notifications may be getting dropped indicating some deeper application or messaging pattern issue.</span></span> <span data-ttu-id="f7089-117">Hello 섹션에서 아래 살펴보겠습니다 다양 한 삭제 알림 시나리오에서 일반적인 toohello 드문 종류 중 일부를 사용할 수 있습니다 명백한 및 일부 다른 많은 양의 하지 사이의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-117">In hello section, below we will look at various dropped notifications scenarios ranging from common toohello rarer kind, some of which you may find obvious and some others not so much.</span></span> 

## <a name="azure-notifications-hub-mis-configuration"></a><span data-ttu-id="f7089-118">Azure 알림 허브의 잘못된 구성</span><span class="sxs-lookup"><span data-stu-id="f7089-118">Azure Notifications Hub mis-configuration</span></span>
<span data-ttu-id="f7089-119">Azure 알림 허브가 필요한 tooauthenticate 자체 hello 컨텍스트에서 hello 개발자 응용 프로그램 toobe 수 toosuccessfully 송신 알림 toohello의 각 PNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-119">Azure Notification Hubs needs tooauthenticate itself in hello context of hello developer's application toobe able toosuccessfully send notifications toohello respective PNS.</span></span> <span data-ttu-id="f7089-120">이 가능 hello 개발자 hello 각 플랫폼 (예: Google, 사과, Windows 등)와 개발자 계정을 만들고 다음 알림에서 hello 포털에서 구성할 toobe 필요한 자격 증명을 받게 응용 프로그램을 등록 하 여 허브 구성 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-120">This is made possible by hello developer creating a developer account with hello respective platform (Google, Apple, Windows etc) and then registering their application where they get credentials which need toobe configured in hello portal under Notification Hubs configuration section.</span></span> <span data-ttu-id="f7089-121">경우 알림이 표시 되지 않습니다는 hello 올바른 자격 증명 hello hello 응용 프로그램과 일치 하는 알림 허브에에서 구성 된 tooensure 아래 만들어야 플랫폼 특정 개발자 계정으로, 첫 번째 단계를 통해 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-121">If no notifications are making through, first step should be tooensure that hello correct credentials are configured in hello Notification Hub matching them with hello application created under their platform specific developer account.</span></span> <span data-ttu-id="f7089-122">있습니다.이 [시작 자습서] 단계별 방식으로이 프로세스를 보다 유용 toogo 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-122">You will find our [Getting Started Tutorials] useful toogo over this process in a step by step manner.</span></span> <span data-ttu-id="f7089-123">다음은 잘못된 구성의 몇가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-123">Here are some common mis-configurations:</span></span>

1. <span data-ttu-id="f7089-124">**일반**</span><span class="sxs-lookup"><span data-stu-id="f7089-124">**General**</span></span>
   
    <span data-ttu-id="f7089-125">) 동일 하면 알림 허브 이름 (입력 오류) 없이 hello는 있는지:</span><span class="sxs-lookup"><span data-stu-id="f7089-125">a) Make sure that your notification hub name (without typos) is hello same:</span></span>
   
   * <span data-ttu-id="f7089-126">Hello 클라이언트에서 등록 하는</span><span class="sxs-lookup"><span data-stu-id="f7089-126">Where you are registering from hello client,</span></span> 
   * <span data-ttu-id="f7089-127">Hello 백 엔드에서 알림을 보내는 위치</span><span class="sxs-lookup"><span data-stu-id="f7089-127">Where you are sending notifications from hello backend,</span></span>  
   * <span data-ttu-id="f7089-128">Hello PNS 자격 증명을 구성한 및</span><span class="sxs-lookup"><span data-stu-id="f7089-128">Where you have configured hello PNS credentials and</span></span> 
   * <span data-ttu-id="f7089-129">에 구성 된 SAS 자격 증명에는 클라이언트와 hello 백 엔드를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-129">Whose SAS credentials you have configured on hello client and hello backend.</span></span> 
     
     <span data-ttu-id="f7089-130">b) hello 클라이언트와 응용 프로그램 백 엔드 hello에서 올바른 SAS 구성 문자열 hello를 사용 하 고 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-130">b) Make sure that you are using hello correct SAS configuration strings on hello client and hello application backend.</span></span> <span data-ttu-id="f7089-131">으로 규칙을 사용 해야 hello **DefaultListenSharedAccessSignature** hello 클라이언트 및 **DefaultFullSharedAccessSignature** (주는 권한 toobe hello 응용 프로그램 백 엔드에 수 toosend 알림 toohello NH)</span><span class="sxs-lookup"><span data-stu-id="f7089-131">As a rule of thumb, you must be using hello **DefaultListenSharedAccessSignature** on hello client and **DefaultFullSharedAccessSignature** on hello application backend (which gives permission toobe able toosend notification toohello NH)</span></span>
2. <span data-ttu-id="f7089-132">**Apple 푸시 알림 서비스(APNS) 구성**</span><span class="sxs-lookup"><span data-stu-id="f7089-132">**Apple Push Notification Service (APNS) configuration**</span></span>
   
    <span data-ttu-id="f7089-133">서로 다른 2개의 허브를 유지해야 하는데, 하나는 프로덕션에 다른 하나는 테스트 목적으로 유지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-133">You must maintain two different hubs - one for production and another for testing purpose.</span></span> <span data-ttu-id="f7089-134">즉, 샌드박스 환경 tooa 별도 허브 및 프로덕션 tooa 별도 허브에서 toouse 보아야 hello 인증서 toouse 보아야 hello 인증서를 업로드 하는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-134">This means uploading hello certificate you are going toouse in sandbox environment tooa separate hub and hello certificate you are going toouse in production tooa separate hub.</span></span> <span data-ttu-id="f7089-135">Tooupload 다양 한 유형의 인증서 toohello 마십시오으로 동일한 허브는 hello 줄 아래로 알림 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-135">Do not try tooupload different types of certificates toohello same hub as it may cause notification failures down hello line.</span></span> <span data-ttu-id="f7089-136">여기서 다양 한 유형의 인증서 toohello 실수로 업로드 한 위치에서 직접 찾을 같은 허브 것이 좋습니다 toodelete hello 허브 및 새로 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-136">If you do find yourself in a position where you have inadvertently uploaded different types of certificate toohello same hub, it is recommended toodelete hello hub and start fresh.</span></span> <span data-ttu-id="f7089-137">어떤 이유로 든 원하는 경우에 없는 hello에 다음 수 toodelete hello 허브 매우 이상, hello 허브에서 모든 hello 기존 등록을 삭제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-137">If for some reason, you are not able toodelete hello hub then at hello very least, you must delete all hello existing registrations from hello hub.</span></span> 
3. <span data-ttu-id="f7089-138">**메시징 GCM(Google Cloud) 구성**</span><span class="sxs-lookup"><span data-stu-id="f7089-138">**Google Cloud Messaging (GCM) configuration**</span></span> 
   
    <span data-ttu-id="f7089-139">a) 클라우드 프로젝트에서 "Android용 Google 클라우드 메시징"을 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-139">a) Make sure that you are enabling "Google Cloud Messaging for Android" under your cloud project.</span></span> 
   
    ![][2]
   
    <span data-ttu-id="f7089-140">b)을 만들어야 합니다 "서버 키" 어떤 NH hello 자격 증명을 가져올 GCM과 tooauthenticate 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-140">b) Make sure that you create a "Server Key" while obtaining hello credentials which NH will use tooauthenticate with GCM.</span></span> 
   
    ![][3]
   
    <span data-ttu-id="f7089-141">c) hello 클라이언트 hello 대시보드에서 얻을 수 있는 완전히 숫자 엔터티는 "프로젝트 ID"를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-141">c) Make sure that you have configured "Project ID" on hello client which is an entirely numerical entity that you can obtain from hello dashboard:</span></span>
   
    ![][1]

## <a name="application-issues"></a><span data-ttu-id="f7089-142">응용 프로그램 문제</span><span class="sxs-lookup"><span data-stu-id="f7089-142">Application issues</span></span>
1) <span data-ttu-id="f7089-143">**태그/태그 식**</span><span class="sxs-lookup"><span data-stu-id="f7089-143">**Tags/ Tag expressions**</span></span>

<span data-ttu-id="f7089-144">태그 또는 태그 식 toosegment 대상 그룹을 사용할 경우 있기 항상 hello 알림을 보낼 때 한지 대상이 송신 호출에서 지정 하는 hello 태그/태그 식을 기반으로 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-144">If you are using tags or tag expressions toosegment your audience, it is always possible that when you are sending hello notification, there is no target being found based on hello tags/tag expressions you are specifying in your send call.</span></span> <span data-ttu-id="f7089-145">이 가장 좋습니다 tooreview는 사용자 등록 tooensure 태그가 있는 일치 알림을 전송 하 고 다음 해당 등록으로 hello 클라이언트 에서만에서 hello 알림을 확인 메일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-145">It is best tooreview your registrations tooensure that there are tags which match when you send notification and then verify hello notification receipt only from hello clients with those registrations.</span></span> <span data-ttu-id="f7089-146">예:</span><span class="sxs-lookup"><span data-stu-id="f7089-146">E.g.</span></span> <span data-ttu-id="f7089-147">태그 "정치" 말 NH 있는 프로그램 등록 작업을 완료 된 모든 태그와 알림 "스포츠" 보내는 경우이 전송 되지 않습니다 tooany 장치입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-147">if all your registrations with NH were done with say tag "Politics" and you are sending a notification with tag "Sports", it will not be sent tooany device.</span></span> <span data-ttu-id="f7089-148">복잡한 경우에는 "태그 A" 또는 "태그 B"로만 등록한 태그 식뿐만 아니라 "태그 A && 태그 B"를 대상으로 알림을 보내는 경우도 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-148">A complex case could involve tag expressions where you only registered with "Tag A" OR "Tag B" but while sending notifications, you are targeting "Tag A && Tag B".</span></span> <span data-ttu-id="f7089-149">Hello에 자체 팁 섹션 아래의 진단, 가지가 서로 hello 태그와 함께 사용자 등록을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-149">In hello self-diagnose tips section below, there are ways in which you can review your registrations along with hello tags they have.</span></span> 

2) <span data-ttu-id="f7089-150">**템플릿 문제**</span><span class="sxs-lookup"><span data-stu-id="f7089-150">**Template issues**</span></span>

<span data-ttu-id="f7089-151">템플릿을 사용 하는 다음에 설명 된 hello 지침을 따르는 확인 [템플릿 지침]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-151">If you are using templates then ensure that you are following hello guidelines described at [Template guidance].</span></span> 

3) <span data-ttu-id="f7089-152">**잘못된 등록**</span><span class="sxs-lookup"><span data-stu-id="f7089-152">**Invalid registrations**</span></span>

<span data-ttu-id="f7089-153">알림 허브가 올바르게 구성 된 hello 및 모든 태그/태그 식을 올바르게 hello 찾기 toowhich hello 알림을 toobe 전송 해야 하는 유효한 대상의 발생을 사용한 경우 NH를 발생 시킵니다 동시-각 일괄 처리에에서 여러 개의 처리 일괄 처리 등록 tooa 집합 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-153">Assuming hello Notification Hub was configured correctly and any tags/tag expressions were used correctly resulting in hello find of valid targets toowhich hello notifications need toobe sent, NH fires off several processing batches in parallel - each batch sending messages tooa set of registrations.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7089-154">병렬에서 처리 hello지 않습니다 것, 이후 hello 순서는 hello 알림을 배달할 수를 보장 하지는 않습니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-154">Since we do hello processing in parallel, we don’t guarantee hello order in which hello notifications will be delivered.</span></span> 
> 
> 

<span data-ttu-id="f7089-155">이제 Azure 알림 허브는 "최대 한 번의" 메시지 전달 모델에 대해 최적화되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-155">Now Azure Notifications Hub is optimized for an "at-most once" message delivery model.</span></span> <span data-ttu-id="f7089-156">즉,를 알림이 없는 두 번 이상 tooa 장치 배달 되는 중복 제거를 시도 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-156">This means that we attempt a de-duplication so that no notifications are delivered more than once tooa device.</span></span> <span data-ttu-id="f7089-157">tooensure hello 등록 전체를 검사 하 고 하나의 메시지만 확인이 실제로 보내는 hello 메시지 toohello PNS 하기 전에 장치 식별자 당 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-157">tooensure this we look through hello registrations and make sure that only one message is sent per device identifier before actually sending hello message toohello PNS.</span></span> <span data-ttu-id="f7089-158">을 각 일괄 처리 toohello PNS에서 수락 하는 다시 전송 되 고 hello 등록 유효성 검사, 있기 hello PNS 해당 일괄 처리에서 하나 이상의 hello 등록 오류가 검색 오류 tooAzure NH 반환 하 고 있으므로 삭제 하는 처리를 중지합니다 완전히 일괄 처리입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-158">As each batch is sent toohello PNS, which in turn is accepting and validating hello registrations, it is possible that hello PNS detects an error with one or more of hello registrations in a batch, returns an error tooAzure NH and stops processing thereby dropping that batch completely.</span></span> <span data-ttu-id="f7089-159">TCP 스트림 프로토콜을 사용하는 APNS와 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-159">This is especially true with APNS which uses a TCP stream protocol.</span></span> <span data-ttu-id="f7089-160">한 번 대부분에 대 한 최적화 된 것 이지만 배달 주소를 제거 하는이 경우의 hello 우리의 데이터베이스와 다음 해당 일괄 처리에서 hello 장치 hello 나머지 부분에 대 한 알림 배달을 다시 시도에서 오류가 있는 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-160">Although we are optimized for at-most once delivery, in this case we remove hello faulting registration from our database and then retry notification delivery for hello rest of hello devices in that batch.</span></span>

<span data-ttu-id="f7089-161">Hello Azure 알림 허브 REST Api를 사용 하 여 등록에 대 한 배달 실패 시도 hello에 대 한 오류 정보를 가져올 수 있습니다: [메시지 원격 분석: 알림 메시지 원격 분석 가져오기](https://msdn.microsoft.com/library/azure/mt608135.aspx) 및 [PNS 피드백](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span><span class="sxs-lookup"><span data-stu-id="f7089-161">You can get error information for hello failed delivery attempt against a registration using hello Azure Notification Hubs REST APIs: [Per Message Telemetry: Get Notification Message Telemetry](https://msdn.microsoft.com/library/azure/mt608135.aspx) and [PNS Feedback](https://msdn.microsoft.com/library/azure/mt705560.aspx).</span></span> <span data-ttu-id="f7089-162">Hello 참조 [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) 예를 들어 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-162">See hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) for example code.</span></span>

## <a name="pns-issues"></a><span data-ttu-id="f7089-163">PNS 문제</span><span class="sxs-lookup"><span data-stu-id="f7089-163">PNS issues</span></span>
<span data-ttu-id="f7089-164">hello 알림 메시지를 받은 후 해당 책임 toodeliver hello 알림 toohello 장치는 해당 PNS hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-164">Once hello notification message has been received by hello respective PNS then it is its responsibility toodeliver hello notification toohello device.</span></span> <span data-ttu-id="f7089-165">Azure 알림 허브가 hello 그림을 추가 벗어나 hello 알림을 toobe toohello 장치 배달 될 경우는 제어 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-165">Azure Notification Hubs is out of hello picture here and has no control on when or if hello notification is going toobe delivered toohello device.</span></span> <span data-ttu-id="f7089-166">Hello 플랫폼 알림 서비스와 매우 강력한 되므로 알림은 hello PNS에서에서 tooreach hello 장치를 몇 초 후에 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-166">Since hello platform notification services are pretty robust, notifications do tend tooreach hello devices in a few seconds from hello PNS.</span></span> <span data-ttu-id="f7089-167">그러나 Hello PNS에서 조정 하는 경우 다음 Azure 알림 허브가 적용 된 지 수 백오프 전략 있고, hello PNS 30 분에 연결할 수 없는 유지 되는 정책에서 tooexpire 놓고 이러한 메시지를 영구적으로 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-167">If hello PNS however is throttling then Azure Notification Hubs does apply an exponential back off strategy and if hello PNS remains unreachable for 30 min then we have a policy in place tooexpire and drop those messages permanently.</span></span> 

<span data-ttu-id="f7089-168">PNS toodeliver 알림을 시도 하는 경우 hello 장치가 오프 라인이 hello 알림 시간 제한 된 기간에 대 한 hello PNS에서 저장 되 고 toohello 장치를 사용할 수 있을 때 배달 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-168">If a PNS attempts toodeliver a notification but hello device is offline, hello notification is stored by hello PNS for a limited period of time, and delivered toohello device when it becomes available.</span></span> <span data-ttu-id="f7089-169">특정 앱에 대한 최근 알림 하나만 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-169">Only one recent notification for a particular app is stored.</span></span> <span data-ttu-id="f7089-170">각 새로운 알림이 hello 장치가 오프 라인 상태인 동안 여러 알림을 보내기 하면 hello 사전 통지 toobe 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-170">If multiple notifications are sent while hello device is offline, each new notification causes hello prior notification toobe discarded.</span></span> <span data-ttu-id="f7089-171">Hello 최신 알림만 유지 합니다.이 동작은 APNS에서 알림을 통합 하 고 축소 (축소 키를 사용 하 여)는 GCM에서 참조 된 tooas 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-171">This behavior of keeping only hello newest notification is referred tooas coalescing notifications in APNS and collapsing in GCM (which uses a collapsing key).</span></span> <span data-ttu-id="f7089-172">오랜 시간 동안 hello 장치가 오프 라인 상태인 경우에 대 한 목록만 저장 하는 모든 알림이 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-172">If hello device remains offline for a long time, any notifications that were being stored for it are discarded.</span></span> <span data-ttu-id="f7089-173">소스 - [APNS 지침] & [GCM 지침]</span><span class="sxs-lookup"><span data-stu-id="f7089-173">Source - [APNS guidance] & [GCM guidance]</span></span>

<span data-ttu-id="f7089-174">Azure 알림 허브-와 결합 키 hello 제네릭을 사용 하 여 HTTP 헤더를 통해 전달할 수 있습니다 `SendNotification` API (예: –.NET SDK에 대 한 `SendNotificationAsync`) toohello은으로 전달 되는 HTTP 헤더를 사용 하 해당 PNS 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-174">With Azure Notification Hubs - you can pass a coalescing key via an HTTP header using hello generic `SendNotification` API (e.g. for .NET SDK – `SendNotificationAsync`) which also takes HTTP headers which are passed as is toohello respective PNS.</span></span> 

## <a name="self-diagnose-tips"></a><span data-ttu-id="f7089-175">자체 진단 팁</span><span class="sxs-lookup"><span data-stu-id="f7089-175">Self-diagnose tips</span></span>
<span data-ttu-id="f7089-176">여기에 살펴보겠습니다 hello 다양 한 수단 toodiagnose 및 모든 알림 허브 문제 원인:</span><span class="sxs-lookup"><span data-stu-id="f7089-176">Here we will examine hello various avenues toodiagnose and root cause any Notification Hub issues:</span></span>

### <a name="verify-credentials"></a><span data-ttu-id="f7089-177">자격 증명 확인</span><span class="sxs-lookup"><span data-stu-id="f7089-177">Verify credentials</span></span>
1. <span data-ttu-id="f7089-178">**PNS 개발자 포털**</span><span class="sxs-lookup"><span data-stu-id="f7089-178">**PNS developer portal**</span></span>
   
    <span data-ttu-id="f7089-179">Hello 해당 PNS 개발자 포털 (APNS, GCM, WNS 등)을 사용 하 여 정보를 확인할 우리의 [시작 자습서]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-179">Verify them at hello respective PNS developer portal (APNS, GCM, WNS etc) using our [Getting Started Tutorials].</span></span>
2. <span data-ttu-id="f7089-180">**Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="f7089-180">**Azure Classic portal**</span></span>
   
    <span data-ttu-id="f7089-181">구성 탭 tooreview toohello 이동한 다음 hello PNS 개발자 포털에서 가져온 설정과 hello 자격 증명과 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-181">Go toohello Configure tab tooreview and match hello credentials with those obtained from hello PNS developer portal.</span></span> 
   
    ![][4]

### <a name="verify-registrations"></a><span data-ttu-id="f7089-182">등록 확인</span><span class="sxs-lookup"><span data-stu-id="f7089-182">Verify registrations</span></span>
1. <span data-ttu-id="f7089-183">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="f7089-183">**Visual Studio**</span></span>
   
    <span data-ttu-id="f7089-184">개발을 위한 Visual Studio를 사용 하는 경우 Azure tooMicrosoft 뷰와 연결할 고 "서버 탐색기" 알림 허브를 포함 한 Azure 서비스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-184">If you use Visual Studio for development then you can connect tooMicrosoft Azure and view and manage a bunch of Azure services including Notifications Hub from "Server Explorer".</span></span> <span data-ttu-id="f7089-185">개발/테스트 환경에서 주로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-185">This is primarily useful for your dev/test environment.</span></span> 
   
    ![][9]
   
    <span data-ttu-id="f7089-186">보고 하 고 플랫폼, 네이티브 또는 템플릿 등록, 태그, PNS 식별자, 등록 id와 hello 만료 날짜에 대 한 분류 원활 하 게 되는 허브의 모든 hello 등록을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-186">You can view and manage all hello registrations in your hub which are nicely categorized for platform, native or template registration, any tags, PNS identifier, registration id and hello expiration date.</span></span> <span data-ttu-id="f7089-187">또한 hello 신속 하 게-tooedit는 태그를 원하는 경우에 예를 들어 유용 등록을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-187">You can also edit a registration on hello fly - which is useful say if you want tooedit any tags.</span></span> 
   
    ![][8]
   
   > [!NOTE]
   > <span data-ttu-id="f7089-188">Visual Studio 기능 tooedit 등록은 등록의 수가 적은 개발/테스트 중에 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-188">Visual Studio functionality tooedit registrations should only be used during dev/test with limited number of registrations.</span></span> <span data-ttu-id="f7089-189">대량, 사용자 등록 고려 발생 필요 toofix 있을 경우 여기에서 설명 하는 hello 내보내기/가져오기 등록 기능을 사용 하 여 [내보내기/가져오기 등록](https://msdn.microsoft.com/library/dn790624.aspx)</span><span class="sxs-lookup"><span data-stu-id="f7089-189">If there arises a need toofix your registrations in bulk, consider using hello Export/Import registration functionality described here - [Export/Import Registrations](https://msdn.microsoft.com/library/dn790624.aspx)</span></span>
   > 
   > 
2. <span data-ttu-id="f7089-190">**서비스 버스 탐색기**</span><span class="sxs-lookup"><span data-stu-id="f7089-190">**Service Bus explorer**</span></span>
   
    <span data-ttu-id="f7089-191">많은 고객이 ServiceBus 탐색기에 설명된 [ServiceBus 탐색기]를 사용하여 알림 허브를 보고 관리합니다</span><span class="sxs-lookup"><span data-stu-id="f7089-191">Many customers use ServiceBus explorer described here - [ServiceBus Explorer] for viewing and managing their notification hub.</span></span> <span data-ttu-id="f7089-192">Code.microsoft.com - [ServiceBus 탐색기 코드]에서 사용할 수 있는 공개 소스 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-192">It is an open source project available from code.microsoft.com - [ServiceBus Explorer code]</span></span>

### <a name="verify-message-notifications"></a><span data-ttu-id="f7089-193">알림 메시지 확인</span><span class="sxs-lookup"><span data-stu-id="f7089-193">Verify message notifications</span></span>
1. <span data-ttu-id="f7089-194">**Azure 클래식 포털**</span><span class="sxs-lookup"><span data-stu-id="f7089-194">**Azure Classic Portal**</span></span>
   
    <span data-ttu-id="f7089-195">실행 되 고 모든 서비스 백 엔드를 필요로 하지 않고 toohello "디버그" 탭 toosend 테스트 알림을 tooyour 클라이언트를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-195">You can go toohello "Debug" tab toosend test notifications tooyour clients without needing any service backend up and running.</span></span> 
   
    ![][7]
2. <span data-ttu-id="f7089-196">**Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="f7089-196">**Visual Studio**</span></span>
   
    <span data-ttu-id="f7089-197">Hello comforts의 Visual Studio에서 테스트 알림을 보낼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-197">You can also send test notifications from hello comforts of Visual Studio:</span></span>
   
    ![][10]
   
    <span data-ttu-id="f7089-198">더 많은 on hello Visual Studio 알림 허브 Azure 탐색기 기능 여기-읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-198">You can read more on hello Visual Studio Notification Hub Azure explorer functionality here -</span></span> 
   
   * <span data-ttu-id="f7089-199">[VS 서버 탐색기 개요]</span><span class="sxs-lookup"><span data-stu-id="f7089-199">[VS Server Explorer Overview]</span></span>
   * <span data-ttu-id="f7089-200">[VS 서버 탐색기 블로그 게시물 - 1]</span><span class="sxs-lookup"><span data-stu-id="f7089-200">[VS Server Explorer Blog post - 1]</span></span>
   * <span data-ttu-id="f7089-201">[VS 서버 탐색기 블로그 게시물 - 2]</span><span class="sxs-lookup"><span data-stu-id="f7089-201">[VS Server Explorer Blog post - 2]</span></span>

### <a name="debug-failed-notifications-review-notification-outcome"></a><span data-ttu-id="f7089-202">실패한 알림 디버그/알림 결과 검토</span><span class="sxs-lookup"><span data-stu-id="f7089-202">Debug failed notifications/ Review notification outcome</span></span>
<span data-ttu-id="f7089-203">**EnableTestSend 속성**</span><span class="sxs-lookup"><span data-stu-id="f7089-203">**EnableTestSend property**</span></span>

<span data-ttu-id="f7089-204">알림 허브를 통해 알림을 보낼 때 처음 것 바로 가져옵니다 큐에서 대기 NH toodo 모든 대상 아웃 toofigure 처리에 대 한 코드를 다음 결국 NH 보냅니다 toohello PNS.</span><span class="sxs-lookup"><span data-stu-id="f7089-204">When you send a notification via Notification Hubs, initially it just gets queued up for NH toodo processing toofigure out all its targets and then eventually NH sends it toohello PNS.</span></span> <span data-ttu-id="f7089-205">이 REST API 또는 hello 클라이언트 SDK 중 하나를 사용 하는 경우 hello hello 메시지를 송신 호출 유일한 수단의 반환이 성공적 이면 성공적으로 큐에 대기 되었습니다 알림 허브를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-205">This means that when you are using REST API or any of hello client SDK, hello successful return of your send call only means that hello message has been successfully queued up with Notification Hub.</span></span> <span data-ttu-id="f7089-206">NH는 결국 toosend hello 메시지 tooPNS 가져왔습니다 때 무슨 상황이 통찰력을 제공 하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-206">It doesn’t give an insight into what happened when NH eventually got toosend hello message tooPNS.</span></span> <span data-ttu-id="f7089-207">알림이 하지 hello PNS에서 허용 하는 hello 최대값을 초과 하는 가능성이 있는지 NH toodeliver hello 메시지 tooPNS 시도 하면 오류가 발생 했습니다 예를 들어 hello 페이로드 크기는 hello 클라이언트 장치에 도착, 또는 hello 자격 증명 NH에 구성 된 경우 hello PNS 오류에 대 한 정보는 잘못 된 등 tooget, 라는 속성이 도입 되었습니다 [EnableTestSend 기능]합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-207">If your notification is not arriving at hello client device, there is a possibility that when NH tried toodeliver hello message tooPNS, there was an error e.g. hello payload size exceeded hello maximum allowed by hello PNS or hello credentials configured in NH are invalid etc. tooget an insight into hello PNS errors, we have introduced a property called [EnableTestSend feature].</span></span> <span data-ttu-id="f7089-208">이 속성을 테스트 hello 포털 또는 Visual Studio 클라이언트에서 메시지 및 되므로 세부 toosee 가능 보낼 때 사용할 자동으로 정보를 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-208">This property is automatically enabled when you send test messages from hello portal or Visual Studio client and therefore allows you toosee detailed debugging information.</span></span> <span data-ttu-id="f7089-209">가능한 경우 이제.NET SDK hello의 hello 예제를 수행 하는 Api를 통해이 사용할 수 있습니다 및 결국 추가 tooall 클라이언트 Sdk를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-209">You can use this via APIs taking hello example of hello .NET SDK where it is available now and will be added tooall client SDKs eventually.</span></span> <span data-ttu-id="f7089-210">toouse hello REST 호출으로이 간단 하 게 추가할 송신 호출의 hello 끝에 예를 들어 "test" 라는 쿼리 문자열 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f7089-210">toouse this with hello REST call, simply append a querystring parameter called "test" at hello end of your send call e.g.</span></span> 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

<span data-ttu-id="f7089-211">*예(.NET SDK)*</span><span class="sxs-lookup"><span data-stu-id="f7089-211">*Example (.NET SDK)*</span></span>

<span data-ttu-id="f7089-212">.NET SDK toosend 알림 기본 메시지를 사용 하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-212">Suppose you are using .NET SDK toosend a native toast notification:</span></span>

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

<span data-ttu-id="f7089-213">`result.State`단순히 상태 `Enqueued` hello 실행 기능에 대 한 모든 한 정보 없이 hello 끝나기 전에 tooyour 푸시 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-213">`result.State` will simply state `Enqueued` at hello end of hello execution without any insight into what happened tooyour push.</span></span> <span data-ttu-id="f7089-214">Hello를 사용 하 여 수 `EnableTestSend` hello를 초기화 하는 동안 부울 속성 `NotificationHubClient` hello 알림을 전송 하는 동안 발생 하는 hello PNS 오류에 대 한 자세한 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-214">Now you can use hello `EnableTestSend` boolean property while initializing hello `NotificationHubClient` and can get detailed status about hello PNS errors encountered while sending hello notification.</span></span> <span data-ttu-id="f7089-215">여기에 hello 송신 호출 NH hello 알림 tooPNS toodetermine hello 결과가 전달한 후만 반환 하기 때문에 시간이 추가로 tooreturn을 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-215">hello send call here will take additional time tooreturn because it is only returning after NH has delivered hello notification tooPNS toodetermine hello outcome.</span></span> 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

<span data-ttu-id="f7089-216">*샘플 출력*</span><span class="sxs-lookup"><span data-stu-id="f7089-216">*Sample Output*</span></span>

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

<span data-ttu-id="f7089-217">이 메시지는 hello 알림 허브에 잘못 된 자격 증명 구성 또는 hello 허브 및 hello에 hello 등록 문제가 권장 과정 toodelete이이 등록 되 고 hello 클라이언트 hello를 보내기 전에 다시 나타냅니다. 메시지.</span><span class="sxs-lookup"><span data-stu-id="f7089-217">This message indicates either invalid credentials are configured in hello notification hub or an issue with hello registrations on hello hub and hello recommended course would be toodelete this registration and let hello client recreate it before sending hello message.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7089-218">Hello를 사용 하 여가이 속성의 스로틀 과도 하 게 되 고 따라서만 사용 해야이 제한 된 집합이 등록 된 개발/테스트 환경에서 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-218">Note that hello use of this property is heavily throttled and so you must only use this in dev/test environment with limited set of registrations.</span></span> <span data-ttu-id="f7089-219">디버그 알림을 too10 장치만 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-219">We only send debug notifications too10 devices.</span></span> <span data-ttu-id="f7089-220">처리 분당 디버그 보냅니다 toobe 10 개로 제한을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-220">We also have a limit of processing debug sends toobe 10 per minute.</span></span> 
> 
> 

### <a name="review-telemetry"></a><span data-ttu-id="f7089-221">원격 분석 검토</span><span class="sxs-lookup"><span data-stu-id="f7089-221">Review telemetry</span></span>
1. <span data-ttu-id="f7089-222">**Azure 클래식 포털 사용**</span><span class="sxs-lookup"><span data-stu-id="f7089-222">**Use Azure Classic Portal**</span></span>
   
    <span data-ttu-id="f7089-223">hello 포털을 통해 알림 허브의 모든 hello 작업의 간략 한 개요 tooget 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-223">hello portal enables you tooget a quick overview of all hello activity on your Notification Hub.</span></span> 
   
    <span data-ttu-id="f7089-224">a) hello "대시보드" 탭에서에서 플랫폼 마다 오류 뿐 아니라 hello 등록, 알림의 집계 보기를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-224">a) From hello "dashboard" tab you can view an aggregated view of hello registrations, notifications as well as errors per platform.</span></span> 
   
    ![][5]
   
    <span data-ttu-id="f7089-225">hello "모니터 임계값" 탭 tootake NH toosend hello 알림 toohello PNS가 반환한 PNS 특정 오류에 특히에서 여러 다른 플랫폼 특정 메트릭을 추가할 수도 b).</span><span class="sxs-lookup"><span data-stu-id="f7089-225">b) You can also add many other platform specific metrics from hello "Monitor" tab tootake a deeper look particularly at any PNS specific errors returned when NH tries toosend hello notification toohello PNS.</span></span> 
   
    ![][6]
   
    <span data-ttu-id="f7089-226">검토 hello로 시작 해야 c) **들어오는 메시지**, **등록 작업**, **알림 성공** tooper 플랫폼 탭 tooreview hello를 이동 합니다 PNS 특정 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-226">c) You should start with reviewing hello **Incoming Messages**, **Registration Operations**, **Successful Notifications** and then go tooper platform tab tooreview hello PNS specific errors.</span></span> 
   
    <span data-ttu-id="f7089-227">d) 있는 경우 hello 알림 허브 잘못 구성 된 hello 인증 설정을 사용 하 여 다음 있습니다 PNS 인증 오류가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-227">d) If you have hello notification hub misconfigured with hello authentication settings then you will see PNS Authentication Error.</span></span> <span data-ttu-id="f7089-228">상태 toocheck hello PNS 자격 증명입니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-228">This is a good indication toocheck hello PNS credentials.</span></span> 

2) <span data-ttu-id="f7089-229">**프로그래밍 방식 액세스**</span><span class="sxs-lookup"><span data-stu-id="f7089-229">**Programmatic access**</span></span>

<span data-ttu-id="f7089-230">자세한 내용은 다음 참조</span><span class="sxs-lookup"><span data-stu-id="f7089-230">More details here -</span></span> 

* <span data-ttu-id="f7089-231">[프로그래밍 방식 원격 분석 액세스]</span><span class="sxs-lookup"><span data-stu-id="f7089-231">[Programmatic Telemetry Access]</span></span>
* <span data-ttu-id="f7089-232">[API 샘플을 통한 원격 분석 액세스]</span><span class="sxs-lookup"><span data-stu-id="f7089-232">[Telemetry Access via APIs sample]</span></span> 

> [!NOTE]
> <span data-ttu-id="f7089-233">**등록 내보내기/가져오기**, **API를 통한 원격 분석 액세스** 등의 여러 원격 분석 관련 기능은 표준 계층에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-233">Several telemetry related features like **Export/Import Registrations**, **Telemetry Access via APIs** etc are only available in Standard tier.</span></span> <span data-ttu-id="f7089-234">Toouse 사용 하려는 경우 이러한 기능에 있는 경우 무료 또는 기본 계층 다음 있습니다 hello REST Api에서 직접 사용 하 여 hello SDK 및 HTTP 403 (금지 됨)를 사용 하는 동안 예외 메시지 toothis 영향을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-234">If you attempt toouse these features if you are in Free or Basic tier then you will get exception message toothis effect while using hello SDK and an HTTP 403 (Forbidden) when using them directly from hello REST APIs.</span></span> <span data-ttu-id="f7089-235">Azure 클래식 포털을 통해 tooStandard 계층을 이동 했다고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7089-235">Make sure that you have moved up tooStandard tier via Azure Classic Portal.</span></span>  
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
[Notification Hubs 개요]: notification-hubs-push-notification-overview.md
[시작 자습서]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[템플릿 지침]: https://msdn.microsoft.com/library/dn530748.aspx 
[APNS 지침]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[GCM 지침]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[ServiceBus 탐색기]: http://msdn.microsoft.com/library/dn530751.aspx
[ServiceBus 탐색기 코드]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[VS 서버 탐색기 개요]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[VS 서버 탐색기 블로그 게시물 - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[VS 서버 탐색기 블로그 게시물 - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend 기능]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[프로그래밍 방식 원격 분석 액세스]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[API 샘플을 통한 원격 분석 액세스]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

