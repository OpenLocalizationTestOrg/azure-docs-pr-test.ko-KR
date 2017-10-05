---
title: "Azure 알림 허브"
description: "Azure Notification Hubs에 푸시 알림 기능을 추가하는 방법을 알아봅니다."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: a1be0b13cd1feb582a23965df142e44d90ac6851
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs"></a><span data-ttu-id="04723-103">Azure 알림 허브</span><span class="sxs-lookup"><span data-stu-id="04723-103">Azure Notification Hubs</span></span>
## <a name="overview"></a><span data-ttu-id="04723-104">개요</span><span class="sxs-lookup"><span data-stu-id="04723-104">Overview</span></span>
<span data-ttu-id="04723-105">Azure Notification Hubs는 사용하기 쉬운 다중 플랫폼의 확장된 푸시 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="04723-106">단일 플랫폼 간 API 호출을 통해 클라우드 또는 온-프레미스 백 엔드에서 모든 모바일 플랫폼으로 개인 설정된 대상 푸시 알림을 쉽게 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

<span data-ttu-id="04723-107">Notification Hubs는 엔터프라이즈 시나리오 및 소비자 시나리오 모두에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-107">Notification Hubs works great for both enterprise and consumer scenarios.</span></span> <span data-ttu-id="04723-108">다음은 고객이 Notification Hubs를 사용하는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-108">Here are a few examples customers use Notification Hubs for:</span></span>

* <span data-ttu-id="04723-109">수백만 명의 사용자에게 대기 시간이 짧은 최신 뉴스 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-109">Send breaking news notifications to millions with low latency.</span></span>
* <span data-ttu-id="04723-110">관심 있는 사용자 세그먼트에 위치 기반 쿠폰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-110">Send location-based coupons to interested user segments.</span></span>
* <span data-ttu-id="04723-111">미디어/스포츠/금융/게임 응용 프로그램을 위해 사용자 또는 그룹에 이벤트 관련 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-111">Send event-related notifications to users or groups for media/sports/finance/gaming applications.</span></span>
* <span data-ttu-id="04723-112">프로모션 콘텐츠를 앱에 푸시하여 고객을 참여시키고 마케팅 활동을 전개합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-112">Push promotional contents to apps to engage and market to customers.</span></span>
* <span data-ttu-id="04723-113">새 메시지 및 작업 항목과 같은 엔터프라이즈 이벤트를 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="04723-113">Notify users of enterprise events like new messages and work items.</span></span>
* <span data-ttu-id="04723-114">다단계 인증을 위한 코드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-114">Send codes for multi-factor authentication.</span></span>

## <a name="what-are-push-notifications"></a><span data-ttu-id="04723-115">푸시 알림이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="04723-115">What are Push Notifications?</span></span>
<span data-ttu-id="04723-116">푸시 알림은 대개 팝업 또는 대화 상자에서 모바일 앱 사용자에게 원하는 특정 정보를 알리는 앱-사용자 통신의 한 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-116">Push notifications is a form of app-to-user communication where users of mobile apps are notified of certain desired information, usually in a pop-up or dialog box.</span></span> <span data-ttu-id="04723-117">사용자는 일반적으로 메시지를 보거나 해제할 수 있으며, 메시지를 보도록 선택하면 알림을 전달한 모바일 앱이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="04723-117">Users can generally choose to view or dismiss the message, and choosing the former will open the mobile app that had communicated the notification.</span></span>

<span data-ttu-id="04723-118">푸시 알림은 앱 참여와 사용량이 증가하는 소비자 앱과 최신 비즈니스 정보를 전달하는 엔터프라이즈 앱에 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-118">Push notifications is vital for consumer apps in increasing app engagement and usage, and for enterprise apps in communicating up-to-date business information.</span></span> <span data-ttu-id="04723-119">모바일 장치에는 에너지 효율이 높고, 알림 보낸 사람에게는 유연하며, 해당 앱이 활성화되어 있지 않을 때 사용할 수 있으므로 최상의 앱-사용자 통신입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-119">It is the best app-to-user communication because it is energy-efficient for  mobile devices, flexible for the notifications senders, and available while corresponding apps are not active.</span></span>

<span data-ttu-id="04723-120">인기 있는 몇 가지 플랫폼의 푸시 알림에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04723-120">For more information on push notifications for a few popular platforms:</span></span>
* [<span data-ttu-id="04723-121">iOS</span><span class="sxs-lookup"><span data-stu-id="04723-121">iOS</span></span>](https://developer.apple.com/notifications/)
* [<span data-ttu-id="04723-122">Android</span><span class="sxs-lookup"><span data-stu-id="04723-122">Android</span></span>](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [<span data-ttu-id="04723-123">Windows</span><span class="sxs-lookup"><span data-stu-id="04723-123">Windows</span></span>](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a><span data-ttu-id="04723-124">푸시 알림 작동 방식</span><span class="sxs-lookup"><span data-stu-id="04723-124">How Push Notifications Work</span></span>
<span data-ttu-id="04723-125">푸시 알림은 *PNS(플랫폼 알림 시스템)*라는 플랫폼별 인프라를 통해 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="04723-125">Push notifications are delivered through platform-specific infrastructures called *Platform Notification Systems* (PNSes).</span></span> <span data-ttu-id="04723-126">배달 메시지에 대한 베어본 푸시 기능을 제공되는 핸들이 있는 장치에 제공하며 공통 인터페이스가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-126">They offer barebone push functionalities to delivery message to a device with a provided handle, and have no common interface.</span></span> <span data-ttu-id="04723-127">iOS, Android 및 Windows 버전의 앱에서 모든 고객에게 알림을 보내려면 개발자는 보내기를 일괄 처리하는 동안 APNS(Apple Push Notification Service), FCM(Firebase Cloud Messaging) 및 WNS(Windows 알림 서비스)를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-127">To send a notification to all customers across the iOS, Android, and Windows versions of an app, the developer must work with APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), and WNS (Windows Notification Service), while batching the sends.</span></span>

<span data-ttu-id="04723-128">높은 수준의 푸시 작동 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-128">At a high level, here is how push works:</span></span>

1. <span data-ttu-id="04723-129">클라이언트 앱에서 푸시를 받도록 결정하면 해당 PNS에 연결하여 고유하고 일시적인 푸시 핸들을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-129">The client app decides it wants to receive pushes hence contacts the corresponding PNS to retrieve its unique and temporary push handle.</span></span> <span data-ttu-id="04723-130">핸들 형식은 시스템에 따라 다릅니다(예: WNS에는 URI가 있지만 APNS에는 토큰이 있음).</span><span class="sxs-lookup"><span data-stu-id="04723-130">The handle type depends on the system (e.g. WNS has URIs while APNS has tokens).</span></span>
2. <span data-ttu-id="04723-131">클라이언트 앱은 이 핸들을 백 엔드 또는 공급자에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-131">The client app stores this handle in the app back-end or provider.</span></span>
3. <span data-ttu-id="04723-132">푸시 알림을 보내기 위해 앱 백 엔드에서 핸들을 통해 PNS에 연결하여 특정 클라이언트 앱을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-132">To send a push notification, the app back-end contacts the PNS using the handle to target a specific client app.</span></span>
4. <span data-ttu-id="04723-133">PNS가 핸들에 의해 지정된 장치로 알림을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-133">The PNS forwards the notification to the device specified by the handle.</span></span>

![][0]

## <a name="the-challenges-of-push-notifications"></a><span data-ttu-id="04723-134">푸시 알림의 문제</span><span class="sxs-lookup"><span data-stu-id="04723-134">The Challenges of Push Notifications</span></span>
<span data-ttu-id="04723-135">PNS는 강력하지만 분할된 사용자에게 푸시 알림을 브로드캐스트하거나 보내는 것처럼 일반적인 푸시 알림 시나리오를 구현하기 위해 앱 개발자는 많은 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-135">While PNSes are powerful, they leave much work to the app developer in order to implement even common push notification scenarios, such as broadcasting or sending push notifications to segmented users.</span></span>

<span data-ttu-id="04723-136">푸시는 앱의 주요 비즈니스 논리와 관련이 없는 복잡한 인프라가 필요하기 때문에 모바일 클라우드 서비스에서 가장 많이 요구되는 기능 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-136">Push is one of the most requested features in mobile cloud services, because its working requires complex infrastructures that are unrelated to the app's main business logic.</span></span> <span data-ttu-id="04723-137">인프라 문제 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-137">Some of the infrastructural challenges are:</span></span>

* <span data-ttu-id="04723-138">**플랫폼 종속성**:</span><span class="sxs-lookup"><span data-stu-id="04723-138">**Platform dependency**:</span></span> 

  * <span data-ttu-id="04723-139">PNS가 통합되지 않기 때문에 다양한 플랫폼의 장치에 알림을 보내기 위해 복잡하고 유지하기가 힘든 플랫폼 종속 논리가 백 엔드에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-139">The backend needs to have complex and hard-to-maintain platform-dependent logic to send notifications to devices on various platforms as PNSes are not unified.</span></span>
* <span data-ttu-id="04723-140">**크기 조정**:</span><span class="sxs-lookup"><span data-stu-id="04723-140">**Scale**:</span></span>

  * <span data-ttu-id="04723-141">PNS 지침에 따라 앱이 시작될 때마다 장치 토큰을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-141">Per PNS guidelines, device tokens must be refreshed upon every app launch.</span></span> <span data-ttu-id="04723-142">즉 백 엔드에서 토큰을 최신 상태로 유지하는 데에만 대량의 트래픽과 데이터베이스 액세스를 처리하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-142">This means the backend is dealing with a large amount of traffic and database access just to keep the tokens up-to-date.</span></span> <span data-ttu-id="04723-143">장치의 수가 수억, 수십 억에 이르면 이 인프라를 만들고 유지 관리하는 비용이 엄청납니다.</span><span class="sxs-lookup"><span data-stu-id="04723-143">When the number of devices grows to hundreds and thousands of millions, the cost of creating and maintaining this infrastructure is massive.</span></span>
  * <span data-ttu-id="04723-144">대부분의 PNS는 여러 장치로의 브로드캐스트를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-144">Most PNSes do not support broadcast to multiple devices.</span></span> <span data-ttu-id="04723-145">즉 단순히 백만 개의 장치로 브로드캐스트하면 PNS를 백만 번 호출하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="04723-145">This means a simple broadcast to a million devices results in a million calls to the PNSes.</span></span> <span data-ttu-id="04723-146">최소 대기 시간으로 트래픽 양을 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-146">Scaling this amount of traffic with minimal latency is nontrivial.</span></span>
* <span data-ttu-id="04723-147">**라우팅**:</span><span class="sxs-lookup"><span data-stu-id="04723-147">**Routing**:</span></span>
  
  * <span data-ttu-id="04723-148">PNS에서 메시지를 장치로 보내는 방법을 제공하지만 대부분의 앱 알림은 사용자 또는 관심 그룹을 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-148">Though PNSes provide a way to send messages to devices, most apps notifications are targeted at users or interest groups.</span></span> <span data-ttu-id="04723-149">즉 백 엔드에서 관심 그룹, 사용자, 속성 등과 장치를 연결하는 레지스트리를 유지해야 합니다. 이러한 오버헤드로 인해 앱의 출시 기간 및 유지 관리 비용이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="04723-149">This means the backend must maintain a registry to associate devices with interest groups, users, properties, etc. This overhead adds to the time to market and maintenance costs of an app.</span></span>

## <a name="why-use-notification-hubs"></a><span data-ttu-id="04723-150">알림 허브를 사용하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="04723-150">Why Use Notification Hubs?</span></span>
<span data-ttu-id="04723-151">Notification Hubs는 사용자의 푸시 활성화와 관련된 모든 복잡성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-151">Notification Hubs eliminates all complexities associated with enabling push on your own.</span></span> <span data-ttu-id="04723-152">다중 플랫폼의 확장된 푸시 알림 인프라는 푸시 관련 코드를 줄이고 백 엔드를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-152">Its multi-platform, scaled-out push notification infrastructure reduces push-related codes and simplifies your backend.</span></span> <span data-ttu-id="04723-153">Notification Hubs를 사용하면 다음 그림과 같이 백 엔드에서 사용자 또는 관심 그룹에 메시지를 보내는 동안 장치는 PNS 핸들을 허브에 등록하는 역할만 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-153">With Notification Hubs, devices are merely responsible for registering their PNS handles with a hub, while the backend sends messages to users or interest groups, as shown in the following figure:</span></span>

![][1]

<span data-ttu-id="04723-154">Notification Hubs는 다음과 같은 장점으로 즉시 사용할 수 있는 푸시 엔진입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-154">Notification hubs is your ready-to-use push engine with the following advantages:</span></span>

* <span data-ttu-id="04723-155">**플랫폼 간**</span><span class="sxs-lookup"><span data-stu-id="04723-155">**Cross platforms**</span></span>

  * <span data-ttu-id="04723-156">모든 주요 푸시 플랫폼(iOS, Android, Windows, Kindle 및 Baidu 포함) 지원</span><span class="sxs-lookup"><span data-stu-id="04723-156">Support for all major push platforms including iOS, Android, Windows, and Kindle and Baidu.</span></span>
  * <span data-ttu-id="04723-157">플랫폼 특정 작업 없이 플랫폼별 또는 플랫폼 독립적 형식으로 모든 플랫폼에 푸시하는 공통 인터페이스</span><span class="sxs-lookup"><span data-stu-id="04723-157">A common interface to push to all platforms in platform-specific or platform-independent formats with no platform-specific work.</span></span>
  * <span data-ttu-id="04723-158">한 곳에서 장치 핸들 관리</span><span class="sxs-lookup"><span data-stu-id="04723-158">Device handle management in one place.</span></span>
* <span data-ttu-id="04723-159">**백 엔드 간**</span><span class="sxs-lookup"><span data-stu-id="04723-159">**Cross backends**</span></span>
  
  * <span data-ttu-id="04723-160">클라우드 또는 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="04723-160">Cloud or on-premises</span></span>
  * <span data-ttu-id="04723-161">.NET, Node.js, Java 등</span><span class="sxs-lookup"><span data-stu-id="04723-161">.NET, Node.js, Java, etc.</span></span>
* <span data-ttu-id="04723-162">**다양한 배달 패턴**</span><span class="sxs-lookup"><span data-stu-id="04723-162">**Rich set of delivery patterns**:</span></span>

  * <span data-ttu-id="04723-163">*하나 이상의 플랫폼에 브로드캐스트*: 단일 API 호출로 여러 플랫폼에서 수백만 개의 장치로 즉시 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-163">*Broadcast to one or multiple platforms*: You can instantly broadcast to millions of devices across platforms with a single API call.</span></span>
  * <span data-ttu-id="04723-164">*장치에 푸시*: 개별 장치에 알림을 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-164">*Push to device*: You can target notifications to individual devices.</span></span>
  * <span data-ttu-id="04723-165">*사용자에게 푸시*: 태그 및 템플릿 기능을 사용하면 사용자의 모든 플랫폼 간 장치에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-165">*Push to user*: Tags and templates features help you reach all cross-platform devices of a user.</span></span>
  * <span data-ttu-id="04723-166">*동적 태그를 사용하여 세그먼트로 푸시*: 태그 기능을 사용하면 하나의 세그먼트 또는 세그먼트의 식(예: 활성 AND 시애틀 거주 NOT 새 사용자)으로 보낼지 여부에 관계 없이 사용자의 요구에 따라 장치를 분류하고 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-166">*Push to segment with dynamic tags*: Tags feature helps you segment devices and push to them according to your needs, whether you are sending to one segment or an expression of segments (e.g. active AND lives in Seattle NOT new user).</span></span> <span data-ttu-id="04723-167">장치 태그를 pub-sub로 제한하는 대신 언제 어디서나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-167">Instead of being restricted to pub-sub, you can update device tags anywhere and anytime.</span></span>
  * <span data-ttu-id="04723-168">*지역화된 푸시*: 템플릿 기능을 사용하면 백 엔드 코드에 영향을 미치지 않고도 지역화를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-168">*Localized push*: Templates feature helps achieve localization without affecting backend code.</span></span>
  * <span data-ttu-id="04723-169">*자동 푸시*: 장치에 자동 알림을 보내고 특정 끌어오기 또는 작업을 완료하도록 이 알림을 트리거하여 push-to-pull(밀어넣기-끌어오기) 패턴을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-169">*Silent push*: You can enables the push-to-pull pattern by sending silent notifications to devices and triggering them to complete certain pulls or actions.</span></span>
  * <span data-ttu-id="04723-170">*예약된 푸시*: 언제든지 알림을 보내도록 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-170">*Scheduled push*: You can schedule to send out notifications anytime.</span></span>
  * <span data-ttu-id="04723-171">*직접 푸시*: 서비스를 통해 장치 등록을 건너뛰고 직접 장치 핸들 목록에 일괄적으로 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-171">*Direct push*: You can skip registering devices with our service and directly batch push to a list of device handles.</span></span>
  * <span data-ttu-id="04723-172">*개인 설정된 푸시*: 장치 푸시 변수를 사용하면 사용자 지정 키-값 쌍이 있는 장치별 개인 설정 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-172">*Personalized push*: Device push variables helps you send device-specific personalized push notifications with customized key-value pairs.</span></span>
* <span data-ttu-id="04723-173">**다양한 원격 분석**</span><span class="sxs-lookup"><span data-stu-id="04723-173">**Rich telemetry**</span></span>
  
  * <span data-ttu-id="04723-174">일반적인 푸시, 장치, 오류 및 작업 원격 분석은 Azure Portal에서 프로그래밍 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-174">General push, device, error, and operation telemetry is available in the Azure portal and programmatically.</span></span>
  * <span data-ttu-id="04723-175">메시지별 원격 분석은 초기 요청 호출에서 푸시 아웃 일괄 처리를 성공적으로 수행한 서비스에 대한 각 푸시를 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-175">Per Message Telemetry tracks each push from your initial request call to our service successfully batching the pushes out.</span></span>
  * <span data-ttu-id="04723-176">PNS(플랫폼 알림 시스템) 피드백은 디버깅을 지원하기 위해 PNS의 모든 피드백을 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-176">Platform Notification System Feedback communicates all feedback from Platfom Notification Systems to assist in debugging.</span></span>
* <span data-ttu-id="04723-177">**확장성**</span><span class="sxs-lookup"><span data-stu-id="04723-177">**Scalability**</span></span> 
  
  * <span data-ttu-id="04723-178">다시 설계하거나 장치를 분할하지 않고도 수백만 개의 장치로 빠른 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-178">Send fast messages to millions of devices without re-architecting or device sharding.</span></span>
* <span data-ttu-id="04723-179">**보안**</span><span class="sxs-lookup"><span data-stu-id="04723-179">**Security**</span></span>

  * <span data-ttu-id="04723-180">SAS(Shared Access Secret) 또는 페더레이션 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="04723-180">Shared Access Secret (SAS) or federated authentication.</span></span>

## <a name="integration-with-app-service-mobile-apps"></a><span data-ttu-id="04723-181">앱 서비스 모바일 앱과 통합</span><span class="sxs-lookup"><span data-stu-id="04723-181">Integration with App Service Mobile Apps</span></span>
<span data-ttu-id="04723-182">Azure 서비스 전반에서 원활하고 일관적인 사용 환경을 조성하기 위하여 알림 허브를 사용한 푸시 알림이 [앱 서비스 모바일 앱]에 기본적으로 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="04723-182">To facilitate a seamless and unifying experience across Azure services, [App Service Mobile Apps] has built-in support for push notifications using Notification Hubs.</span></span> <span data-ttu-id="04723-183">[앱 서비스 모바일 앱]은 엔터프라이즈 개발자 및 시스템 통합자를 위해 확장성이 크고 전 세계에서 사용 가능한 모바일 응용 프로그램 개발 플랫폼을 제공합니다. 이 플랫폼은 모바일 개발자에게 풍부한 기능 집합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-183">[App Service Mobile Apps] offers a highly scalable, globally available mobile application development platform for Enterprise Developers and System Integrators that brings a rich set of capabilities to mobile developers.</span></span>

<span data-ttu-id="04723-184">모바일 앱 개발자는 다음 워크플로에서 알림 허브를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-184">Mobile Apps developers can utilize Notification Hubs with the following workflow:</span></span>

1. <span data-ttu-id="04723-185">장치 PNS 핸들을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-185">Retrieve device PNS handle</span></span>
2. <span data-ttu-id="04723-186">편리한 Mobile Apps 클라이언트 SDK 등록 API를 통해 장치를 Notification Hubs에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-186">Register device with Notification Hubs through convenient Mobile Apps Client SDK register API</span></span>
   * <span data-ttu-id="04723-187">모바일 앱은 등록 시 보안을 목적으로 모든 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-187">Note that Mobile Apps strips away all tags on registrations for security purposes.</span></span> <span data-ttu-id="04723-188">백 엔드에서 알림 허브와 직접 작업하여 장치와 태그를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-188">Work with Notification Hubs from your backend directly to associate tags with devices.</span></span>
3. <span data-ttu-id="04723-189">알림 허브를 통해 앱 백 엔드에서 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-189">Send notifications from your app backend with Notification Hubs</span></span>

<span data-ttu-id="04723-190">이 통합으로 인해 개발자에게 다음과 같은 편리한 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="04723-190">Here are some conveniences brought to developers with this integration:</span></span>

* <span data-ttu-id="04723-191">**Mobile Apps 클라이언트 SDK**: 이러한 다중 플랫폼 SDK는 등록을 위한 간단한 API를 제공하며 모바일 앱과 자동으로 연결되는 알림 허브와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-191">**Mobile Apps Client SDKs**: These multi-platform SDKs provide simple APIs for registration and talk to the notification hub linked up with the mobile app automatically.</span></span> <span data-ttu-id="04723-192">개발자는 알림 허브 자격 증명을 심도있게 분석하고 추가 서비스로 작업할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-192">Developers do not need to dig through Notification Hubs credentials and work with an additional service.</span></span>

  * <span data-ttu-id="04723-193">*사용자에게 푸시*: SDK는 Mobile Apps 인증 사용자 ID로 지정된 장치에 태그를 자동으로 지정하여 사용자 시나리오에 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-193">*Push to user*: The SDKs automatically tag the given device with Mobile Apps authenticated User ID to enable push to user scenario.</span></span>
  * <span data-ttu-id="04723-194">*장치에 푸시*: SDK는 자동으로 Mobile Apps 설치 ID를 GUID로 사용하여 Notification Hubs에 등록하여 개발자가 여러 서비스 GUID를 유지 관리하는 문제를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="04723-194">*Push to device*: The SDKs automatically use the Mobile Apps Installation ID as GUID to register with Notification Hubs, saving developers the trouble of maintaining multiple service GUIDs.</span></span>
* <span data-ttu-id="04723-195">**설치 모델**: Mobile Apps는 Notification Hubs의 최신 푸시 모델과 함께 작동하여 푸시 알림 서비스와 일치하고 사용하기 쉬운 JSON 설치의 장치와 연결된 모든 푸시 속성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="04723-195">**Installation model**: Mobile Apps works with Notification Hubs' latest push model to represent all push properties associated with a device in a JSON Installation that aligns with Push Notification Services and is easy to use.</span></span>
* <span data-ttu-id="04723-196">**유연성**: 개발자는 통합되어 있더라도 Notification Hubs와 직접 작동하도록 언제든지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-196">**Flexibility**: Developers can always choose to work with Notification Hubs directly even with the integration in place.</span></span>
* <span data-ttu-id="04723-197">**[Azure Portal]에 통합된 환경**: 푸시 기능은 Mobile Apps에서 시각적으로 표현되므로 개발자가 Mobile Apps를 통해 연결된 알림 허브를 사용하여 쉽게 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-197">**Integrated experience in [Azure portal]**: Push as a capability is represented visually in Mobile Apps and developers can easily work with the associated notification hub through Mobile Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04723-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="04723-198">Next Steps</span></span>
<span data-ttu-id="04723-199">다음 항목에서 알림 허브에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="04723-199">You can find out more about Notification Hubs in these topics:</span></span>

* <span data-ttu-id="04723-200">**[고객이 알림 허브를 사용하는 방법]**</span><span class="sxs-lookup"><span data-stu-id="04723-200">**[How customers are using Notification Hubs]**</span></span>
* <span data-ttu-id="04723-201">**[알림 허브 자습서 및 가이드]**</span><span class="sxs-lookup"><span data-stu-id="04723-201">**[Notification Hubs tutorials and guides]**</span></span>
* <span data-ttu-id="04723-202">**Notification Hubs 시작 자습서**: [iOS], [Android], [Windows 범용], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="04723-202">**Notification Hubs Getting Started tutorials**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span></span>

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
<span data-ttu-id="04723-203">[고객이 알림 허브를 사용하는 방법]: http://azure.microsoft.com/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="04723-203">[How customers are using Notification Hubs]: http://azure.microsoft.com/services/notification-hubs</span></span>
<span data-ttu-id="04723-204">[알림 허브 자습서 및 가이드]: http://azure.microsoft.com/documentation/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="04723-204">[Notification Hubs tutorials and guides]: http://azure.microsoft.com/documentation/services/notification-hubs</span></span>
<span data-ttu-id="04723-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span></span>
<span data-ttu-id="04723-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span></span>
<span data-ttu-id="04723-207">[Windows 범용]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-207">[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span></span>
<span data-ttu-id="04723-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span></span>
<span data-ttu-id="04723-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span></span>
<span data-ttu-id="04723-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span></span>
<span data-ttu-id="04723-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="04723-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span></span>
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
<span data-ttu-id="04723-212">[앱 서비스 모바일 앱]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span><span class="sxs-lookup"><span data-stu-id="04723-212">[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span></span>
[templates]: notification-hubs-templates-cross-platform-push-messages.md
<span data-ttu-id="04723-213">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="04723-213">[Azure portal]: https://portal.azure.com</span></span>
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
