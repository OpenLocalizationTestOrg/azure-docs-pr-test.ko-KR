---
title: "aaaAzure 알림 허브"
description: "Tooadd Azure 알림 허브와 알림 기능을 강제 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a><span data-ttu-id="0c983-103">Azure 알림 허브</span><span class="sxs-lookup"><span data-stu-id="0c983-103">Azure Notification Hubs</span></span>
## <a name="overview"></a><span data-ttu-id="0c983-104">개요</span><span class="sxs-lookup"><span data-stu-id="0c983-104">Overview</span></span>
<span data-ttu-id="0c983-105">Azure Notification Hubs는 사용하기 쉬운 다중 플랫폼의 확장된 푸시 엔진을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="0c983-106">단일 크로스 플랫폼 API 호출으로 모든 클라우드 또는 온-프레미스 백 엔드에서 대상으로 지정 된 개인 설정 된 푸시 알림 tooany 모바일 플랫폼을 쉽게 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications tooany mobile platform from any cloud or on-premises backend.</span></span>

<span data-ttu-id="0c983-107">Notification Hubs는 엔터프라이즈 시나리오 및 소비자 시나리오 모두에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-107">Notification Hubs works great for both enterprise and consumer scenarios.</span></span> <span data-ttu-id="0c983-108">다음은 고객이 Notification Hubs를 사용하는 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-108">Here are a few examples customers use Notification Hubs for:</span></span>

* <span data-ttu-id="0c983-109">최신 뉴스 알림 toomillions를 짧은 대기 시간으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-109">Send breaking news notifications toomillions with low latency.</span></span>
* <span data-ttu-id="0c983-110">Toointerested 사용자 세그먼트 위치 기반 쿠폰을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-110">Send location-based coupons toointerested user segments.</span></span>
* <span data-ttu-id="0c983-111">알림 이벤트와 관련 toousers 또는 미디어/스포츠/금융/게임 응용 프로그램에 대 한 그룹을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-111">Send event-related notifications toousers or groups for media/sports/finance/gaming applications.</span></span>
* <span data-ttu-id="0c983-112">프로 모션 내용을 tooapps tooengage 및 시장 toocustomers를 푸시하십시오.</span><span class="sxs-lookup"><span data-stu-id="0c983-112">Push promotional contents tooapps tooengage and market toocustomers.</span></span>
* <span data-ttu-id="0c983-113">새 메시지 및 작업 항목과 같은 엔터프라이즈 이벤트를 사용자에게 알립니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-113">Notify users of enterprise events like new messages and work items.</span></span>
* <span data-ttu-id="0c983-114">다단계 인증을 위한 코드를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-114">Send codes for multi-factor authentication.</span></span>

## <a name="what-are-push-notifications"></a><span data-ttu-id="0c983-115">푸시 알림이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0c983-115">What are Push Notifications?</span></span>
<span data-ttu-id="0c983-116">푸시 알림은 대개 팝업 또는 대화 상자에서 모바일 앱 사용자에게 원하는 특정 정보를 알리는 앱-사용자 통신의 한 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-116">Push notifications is a form of app-to-user communication where users of mobile apps are notified of certain desired information, usually in a pop-up or dialog box.</span></span> <span data-ttu-id="0c983-117">사용자가 선택 tooview 일반적으로 나 hello 메시지를 해제할 수 및 hello 알림을 통신 했 hello 모바일 응용 프로그램 선택 hello 전자 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-117">Users can generally choose tooview or dismiss hello message, and choosing hello former will open hello mobile app that had communicated hello notification.</span></span>

<span data-ttu-id="0c983-118">푸시 알림은 앱 참여와 사용량이 증가하는 소비자 앱과 최신 비즈니스 정보를 전달하는 엔터프라이즈 앱에 매우 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-118">Push notifications is vital for consumer apps in increasing app engagement and usage, and for enterprise apps in communicating up-to-date business information.</span></span> <span data-ttu-id="0c983-119">되었기 hello 최적의 사용자에 앱을 통신 에너지 효율적인 hello 알림 발신자에 대 한 유연 하 고 사용할 수 있는 모바일 장치에 대 한 해당 하는 앱이 활성화 되지 않은 상태인 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-119">It is hello best app-to-user communication because it is energy-efficient for  mobile devices, flexible for hello notifications senders, and available while corresponding apps are not active.</span></span>

<span data-ttu-id="0c983-120">인기 있는 몇 가지 플랫폼의 푸시 알림에 대한 자세한 내용은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0c983-120">For more information on push notifications for a few popular platforms:</span></span>
* [<span data-ttu-id="0c983-121">iOS</span><span class="sxs-lookup"><span data-stu-id="0c983-121">iOS</span></span>](https://developer.apple.com/notifications/)
* [<span data-ttu-id="0c983-122">Android</span><span class="sxs-lookup"><span data-stu-id="0c983-122">Android</span></span>](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [<span data-ttu-id="0c983-123">Windows</span><span class="sxs-lookup"><span data-stu-id="0c983-123">Windows</span></span>](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a><span data-ttu-id="0c983-124">푸시 알림 작동 방식</span><span class="sxs-lookup"><span data-stu-id="0c983-124">How Push Notifications Work</span></span>
<span data-ttu-id="0c983-125">푸시 알림은 *PNS(플랫폼 알림 시스템)*라는 플랫폼별 인프라를 통해 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-125">Push notifications are delivered through platform-specific infrastructures called *Platform Notification Systems* (PNSes).</span></span> <span data-ttu-id="0c983-126">베어본 푸시 기능으로 제공 된 toodelivery 메시지 tooa 장치를 처리 및 공통 인터페이스가 없습니다을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-126">They offer barebone push functionalities toodelivery message tooa device with a provided handle, and have no common interface.</span></span> <span data-ttu-id="0c983-127">알림 toosend tooall 고객 간에 hello iOS, Android 및 Windows 버전의 응용 프로그램에서는 hello 개발자 작업 해야 APNS (Apple Push Notification Service), (Firebase Cloud Messaging) FCM WNS (Windows 알림 서비스)와 일괄 처리 하는 동안 hello가 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-127">toosend a notification tooall customers across hello iOS, Android, and Windows versions of an app, hello developer must work with APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), and WNS (Windows Notification Service), while batching hello sends.</span></span>

<span data-ttu-id="0c983-128">높은 수준의 푸시 작동 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-128">At a high level, here is how push works:</span></span>

1. <span data-ttu-id="0c983-129">hello 클라이언트 응용 프로그램은 원하는 tooreceive 푸시 따라서 PNS tooretrieve에 해당 하는 연락처 hello 고유 하 고 임시 푸시 핸들을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-129">hello client app decides it wants tooreceive pushes hence contacts hello corresponding PNS tooretrieve its unique and temporary push handle.</span></span> <span data-ttu-id="0c983-130">hello 핸들 형식 (예: WNS Uri가 있는 반면 APNS 토큰) hello 시스템에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-130">hello handle type depends on hello system (e.g. WNS has URIs while APNS has tokens).</span></span>
2. <span data-ttu-id="0c983-131">hello 클라이언트 응용 프로그램 hello 앱 백 엔드에서 또는 공급자에서이 핸들을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-131">hello client app stores this handle in hello app back-end or provider.</span></span>
3. <span data-ttu-id="0c983-132">푸시 알림을 toosend hello 앱 백 엔드에서 hello 특정 클라이언트 앱 핸들 tootarget hello를 사용 하 여 PNS에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-132">toosend a push notification, hello app back-end contacts hello PNS using hello handle tootarget a specific client app.</span></span>
4. <span data-ttu-id="0c983-133">hello PNS 핸들 hello로 지정 된 hello 알림 toohello 장치를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-133">hello PNS forwards hello notification toohello device specified by hello handle.</span></span>

![][0]

## <a name="hello-challenges-of-push-notifications"></a><span data-ttu-id="0c983-134">hello 푸시 알림을 과제</span><span class="sxs-lookup"><span data-stu-id="0c983-134">hello Challenges of Push Notifications</span></span>
<span data-ttu-id="0c983-135">PNSes은 강력 하지만, 순서 tooimplement 일반적인 푸시 알림 등의 시나리오에서 브로드캐스트 또는 보내는 푸시 알림 toosegmented 사용자가 많은 작업 toohello 앱 개발자를 벗어나면 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-135">While PNSes are powerful, they leave much work toohello app developer in order tooimplement even common push notification scenarios, such as broadcasting or sending push notifications toosegmented users.</span></span>

<span data-ttu-id="0c983-136">푸시 중 하나입니다. 작업 관련 없는 toohello 응용 프로그램의 기본 비즈니스 논리는 복잡 한 인프라를 필요로 하기 때문에 가장 hello 모바일 클라우드 서비스 기능이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-136">Push is one of hello most requested features in mobile cloud services, because its working requires complex infrastructures that are unrelated toohello app's main business logic.</span></span> <span data-ttu-id="0c983-137">Hello 주요 과제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-137">Some of hello infrastructural challenges are:</span></span>

* <span data-ttu-id="0c983-138">**플랫폼 종속성**:</span><span class="sxs-lookup"><span data-stu-id="0c983-138">**Platform dependency**:</span></span> 

  * <span data-ttu-id="0c983-139">hello 백 엔드 PNSes 통합 되지 됩니다 toohave 복잡 하 고 유지 하드 플랫폼별 논리 toosend 알림 toodevices 다양 한 플랫폼에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-139">hello backend needs toohave complex and hard-to-maintain platform-dependent logic toosend notifications toodevices on various platforms as PNSes are not unified.</span></span>
* <span data-ttu-id="0c983-140">**크기 조정**:</span><span class="sxs-lookup"><span data-stu-id="0c983-140">**Scale**:</span></span>

  * <span data-ttu-id="0c983-141">PNS 지침에 따라 앱이 시작될 때마다 장치 토큰을 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-141">Per PNS guidelines, device tokens must be refreshed upon every app launch.</span></span> <span data-ttu-id="0c983-142">즉, 많은 양의 트래픽 처리 하는 hello 백 엔드 데이터베이스 액세스 최신 tookeep hello 토큰만.</span><span class="sxs-lookup"><span data-stu-id="0c983-142">This means hello backend is dealing with a large amount of traffic and database access just tookeep hello tokens up-to-date.</span></span> <span data-ttu-id="0c983-143">장치의 hello 수 toohundreds 및 수백만 이르면 hello를 만들고이 인프라를 유지 관리 비용은 대규모입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-143">When hello number of devices grows toohundreds and thousands of millions, hello cost of creating and maintaining this infrastructure is massive.</span></span>
  * <span data-ttu-id="0c983-144">대부분 PNSes 브로드캐스트 toomultiple 장치를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-144">Most PNSes do not support broadcast toomultiple devices.</span></span> <span data-ttu-id="0c983-145">이 의미 간단한 브로드캐스트 tooa는 백만 호출 toohello PNSes 백만 장치 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-145">This means a simple broadcast tooa million devices results in a million calls toohello PNSes.</span></span> <span data-ttu-id="0c983-146">최소 대기 시간으로 트래픽 양을 조정하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-146">Scaling this amount of traffic with minimal latency is nontrivial.</span></span>
* <span data-ttu-id="0c983-147">**라우팅**:</span><span class="sxs-lookup"><span data-stu-id="0c983-147">**Routing**:</span></span>
  
  * <span data-ttu-id="0c983-148">PNSes 방법을 toosend 메시지 toodevices을 제공 하지만 대부분의 앱 공지 사용자나 관심 그룹에 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-148">Though PNSes provide a way toosend messages toodevices, most apps notifications are targeted at users or interest groups.</span></span> <span data-ttu-id="0c983-149">즉, hello 백 엔드는 관심 그룹, 사용자가, 속성 등을 사용 하 여 레지스트리 tooassociate 장치는 유지 관리 해야 합니다. 이 오버 헤드는 응용 프로그램의 toohello 시간 toomarket 및 유지 관리 비용을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-149">This means hello backend must maintain a registry tooassociate devices with interest groups, users, properties, etc. This overhead adds toohello time toomarket and maintenance costs of an app.</span></span>

## <a name="why-use-notification-hubs"></a><span data-ttu-id="0c983-150">알림 허브를 사용하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="0c983-150">Why Use Notification Hubs?</span></span>
<span data-ttu-id="0c983-151">Notification Hubs는 사용자의 푸시 활성화와 관련된 모든 복잡성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-151">Notification Hubs eliminates all complexities associated with enabling push on your own.</span></span> <span data-ttu-id="0c983-152">다중 플랫폼의 확장된 푸시 알림 인프라는 푸시 관련 코드를 줄이고 백 엔드를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-152">Its multi-platform, scaled-out push notification infrastructure reduces push-related codes and simplifies your backend.</span></span> <span data-ttu-id="0c983-153">알림 허브와 장치는 hello 다음 그림에에서 나와 있는 것 처럼 hello 백 엔드 메시지 toousers 또는 관심 그룹에 보내는 동안는 허브는 PNS 핸들 등록만 담당 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-153">With Notification Hubs, devices are merely responsible for registering their PNS handles with a hub, while hello backend sends messages toousers or interest groups, as shown in hello following figure:</span></span>

![][1]

<span data-ttu-id="0c983-154">알림 허브는 다음 장점 hello로 즉시 사용할 푸시 엔진:</span><span class="sxs-lookup"><span data-stu-id="0c983-154">Notification hubs is your ready-to-use push engine with hello following advantages:</span></span>

* <span data-ttu-id="0c983-155">**플랫폼 간**</span><span class="sxs-lookup"><span data-stu-id="0c983-155">**Cross platforms**</span></span>

  * <span data-ttu-id="0c983-156">모든 주요 푸시 플랫폼(iOS, Android, Windows, Kindle 및 Baidu 포함) 지원</span><span class="sxs-lookup"><span data-stu-id="0c983-156">Support for all major push platforms including iOS, Android, Windows, and Kindle and Baidu.</span></span>
  * <span data-ttu-id="0c983-157">공용 인터페이스 toopush tooall 플랫폼에 특정 플랫폼 또는 플랫폼 독립적인 형식 아무 플랫폼 관련 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-157">A common interface toopush tooall platforms in platform-specific or platform-independent formats with no platform-specific work.</span></span>
  * <span data-ttu-id="0c983-158">한 곳에서 장치 핸들 관리</span><span class="sxs-lookup"><span data-stu-id="0c983-158">Device handle management in one place.</span></span>
* <span data-ttu-id="0c983-159">**백 엔드 간**</span><span class="sxs-lookup"><span data-stu-id="0c983-159">**Cross backends**</span></span>
  
  * <span data-ttu-id="0c983-160">클라우드 또는 온-프레미스</span><span class="sxs-lookup"><span data-stu-id="0c983-160">Cloud or on-premises</span></span>
  * <span data-ttu-id="0c983-161">.NET, Node.js, Java 등</span><span class="sxs-lookup"><span data-stu-id="0c983-161">.NET, Node.js, Java, etc.</span></span>
* <span data-ttu-id="0c983-162">**다양한 배달 패턴**</span><span class="sxs-lookup"><span data-stu-id="0c983-162">**Rich set of delivery patterns**:</span></span>

  * <span data-ttu-id="0c983-163">*여러 플랫폼 tooone 브로드캐스트*: 단일 API 호출 하 여 플랫폼 간에 장치의 toomillions 즉시 브로드캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-163">*Broadcast tooone or multiple platforms*: You can instantly broadcast toomillions of devices across platforms with a single API call.</span></span>
  * <span data-ttu-id="0c983-164">*Toodevice 푸시*: 알림을 tooindividual 장치 대상으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-164">*Push toodevice*: You can target notifications tooindividual devices.</span></span>
  * <span data-ttu-id="0c983-165">*Toouser 푸시*: 태그 및 템플릿을 기능 사용자의 모든 플랫폼 간 장치에 도달 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-165">*Push toouser*: Tags and templates features help you reach all cross-platform devices of a user.</span></span>
  * <span data-ttu-id="0c983-166">*동적 태그로 toosegment 푸시*: 태그 기능을 사용 하면 장치를 분할 하 고 tooone 세그먼트 또는 세그먼트 (예: 활성 AND 생활에서 새 사용자가 아닌 Seattle)의 식을 보내는 여부 toothem tooyour 요구에 따라을 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-166">*Push toosegment with dynamic tags*: Tags feature helps you segment devices and push toothem according tooyour needs, whether you are sending tooone segment or an expression of segments (e.g. active AND lives in Seattle NOT new user).</span></span> <span data-ttu-id="0c983-167">제한 된 toopub sub 않고 장치 태그 임의의 위치를 업데이트할 수 있습니다 및 언제 든 지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-167">Instead of being restricted toopub-sub, you can update device tags anywhere and anytime.</span></span>
  * <span data-ttu-id="0c983-168">*지역화된 푸시*: 템플릿 기능을 사용하면 백 엔드 코드에 영향을 미치지 않고도 지역화를 달성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-168">*Localized push*: Templates feature helps achieve localization without affecting backend code.</span></span>
  * <span data-ttu-id="0c983-169">*자동 푸시*: 특정 끌어오는 소스 나 작업이 toodevices 자동 알림을 보내고 toocomplete를 트리거하지 hello 푸시 풀 패턴을 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-169">*Silent push*: You can enables hello push-to-pull pattern by sending silent notifications toodevices and triggering them toocomplete certain pulls or actions.</span></span>
  * <span data-ttu-id="0c983-170">*푸시 예약*: 언제 든 지 알림을 toosend 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-170">*Scheduled push*: You can schedule toosend out notifications anytime.</span></span>
  * <span data-ttu-id="0c983-171">*직접 푸시*: 본사 서비스 및 직접 장치 핸들 목록이 푸시 tooa 일괄 처리를 사용 하 여 장치를 등록을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-171">*Direct push*: You can skip registering devices with our service and directly batch push tooa list of device handles.</span></span>
  * <span data-ttu-id="0c983-172">*개인 설정된 푸시*: 장치 푸시 변수를 사용하면 사용자 지정 키-값 쌍이 있는 장치별 개인 설정 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-172">*Personalized push*: Device push variables helps you send device-specific personalized push notifications with customized key-value pairs.</span></span>
* <span data-ttu-id="0c983-173">**다양한 원격 분석**</span><span class="sxs-lookup"><span data-stu-id="0c983-173">**Rich telemetry**</span></span>
  
  * <span data-ttu-id="0c983-174">일반 밀어넣기, 장치, 오류 및 작업 원격 분석은 hello Azure 포털에서에서 사용할 수 있는 방법과 프로그래밍 방식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-174">General push, device, error, and operation telemetry is available in hello Azure portal and programmatically.</span></span>
  * <span data-ttu-id="0c983-175">메시지 원격 분석 추적 당 hello 일괄 처리가 성공적으로 초기 요청 호출 tooour 서비스에서 각 푸시 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-175">Per Message Telemetry tracks each push from your initial request call tooour service successfully batching hello pushes out.</span></span>
  * <span data-ttu-id="0c983-176">플랫폼 알림 시스템 피드백 디버깅 tooassist 플랫폼 알림 시스템에서에서 모든 피드백을 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-176">Platform Notification System Feedback communicates all feedback from Platfom Notification Systems tooassist in debugging.</span></span>
* <span data-ttu-id="0c983-177">**확장성**</span><span class="sxs-lookup"><span data-stu-id="0c983-177">**Scalability**</span></span> 
  
  * <span data-ttu-id="0c983-178">빠른 메시지 toomillions 재설계 하거나 장치 분할 하지 않고도 장치를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-178">Send fast messages toomillions of devices without re-architecting or device sharding.</span></span>
* <span data-ttu-id="0c983-179">**보안**</span><span class="sxs-lookup"><span data-stu-id="0c983-179">**Security**</span></span>

  * <span data-ttu-id="0c983-180">SAS(Shared Access Secret) 또는 페더레이션 인증입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-180">Shared Access Secret (SAS) or federated authentication.</span></span>

## <a name="integration-with-app-service-mobile-apps"></a><span data-ttu-id="0c983-181">앱 서비스 모바일 앱과 통합</span><span class="sxs-lookup"><span data-stu-id="0c983-181">Integration with App Service Mobile Apps</span></span>
<span data-ttu-id="0c983-182">Azure 서비스 전반에 걸쳐 원활 하 고 통합 환경 toofacilitate [앱 서비스 모바일 앱] 푸시 알림을 알림 허브를 사용 하 여 기본적으로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-182">toofacilitate a seamless and unifying experience across Azure services, [App Service Mobile Apps] has built-in support for push notifications using Notification Hubs.</span></span> <span data-ttu-id="0c983-183">[앱 서비스 모바일 앱] 는 엔터프라이즈 개발자 및 시스템 통합자 toomobile 개발자가 다양 한 기능을 제공 하는 것에 대 한 확장성이 높은, 전역적으로 사용 가능한 모바일 응용 프로그램 개발 플랫폼을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-183">[App Service Mobile Apps] offers a highly scalable, globally available mobile application development platform for Enterprise Developers and System Integrators that brings a rich set of capabilities toomobile developers.</span></span>

<span data-ttu-id="0c983-184">모바일 앱 개발자가 워크플로 수행 하는 hello로 알림 허브를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-184">Mobile Apps developers can utilize Notification Hubs with hello following workflow:</span></span>

1. <span data-ttu-id="0c983-185">장치 PNS 핸들을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-185">Retrieve device PNS handle</span></span>
2. <span data-ttu-id="0c983-186">편리한 Mobile Apps 클라이언트 SDK 등록 API를 통해 장치를 Notification Hubs에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-186">Register device with Notification Hubs through convenient Mobile Apps Client SDK register API</span></span>
   * <span data-ttu-id="0c983-187">모바일 앱은 등록 시 보안을 목적으로 모든 태그를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-187">Note that Mobile Apps strips away all tags on registrations for security purposes.</span></span> <span data-ttu-id="0c983-188">장치와 tooassociate 태그 직접 알림 허브와 백 엔드에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-188">Work with Notification Hubs from your backend directly tooassociate tags with devices.</span></span>
3. <span data-ttu-id="0c983-189">알림 허브를 통해 앱 백 엔드에서 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-189">Send notifications from your app backend with Notification Hubs</span></span>

<span data-ttu-id="0c983-190">이 통합 toodevelopers 상태가 일부 편리 하며 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-190">Here are some conveniences brought toodevelopers with this integration:</span></span>

* <span data-ttu-id="0c983-191">**모바일 앱 클라이언트 Sdk**: 이러한 다중 플랫폼 Sdk 등록에 대 한 간단한 Api를 제공 하 고 자동으로 모바일 앱 hello 연결 toohello 알림 허브와 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-191">**Mobile Apps Client SDKs**: These multi-platform SDKs provide simple APIs for registration and talk toohello notification hub linked up with hello mobile app automatically.</span></span> <span data-ttu-id="0c983-192">개발자가 toodig 알림 허브 자격 증명을 통해 필요 하지 않으며 추가 서비스와 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-192">Developers do not need toodig through Notification Hubs credentials and work with an additional service.</span></span>

  * <span data-ttu-id="0c983-193">*Toouser 푸시*: hello Sdk에는 자동으로 모바일 앱 인증 된 사용자 ID tooenable 푸시 toouser 시나리오를 사용 하 여 장치를 지정 하는 hello 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-193">*Push toouser*: hello SDKs automatically tag hello given device with Mobile Apps authenticated User ID tooenable push toouser scenario.</span></span>
  * <span data-ttu-id="0c983-194">*Toodevice 푸시*: hello Sdk 개발자의 여러 서비스 Guid를 유지 관리 하는 데 문제가 hello 저장 되는 알림 허브와 GUID tooregister로 hello 모바일 앱 설치 ID를 자동으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-194">*Push toodevice*: hello SDKs automatically use hello Mobile Apps Installation ID as GUID tooregister with Notification Hubs, saving developers hello trouble of maintaining multiple service GUIDs.</span></span>
* <span data-ttu-id="0c983-195">**설치 모델**: 모바일 앱 알림 허브 최신 밀어넣기 모델 toorepresent 모든 푸시 쉽게 toouse 이며 푸시 알림 서비스에 맞게 조정 해야 하는 JSON 설치에서 장치에 연결 된 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-195">**Installation model**: Mobile Apps works with Notification Hubs' latest push model toorepresent all push properties associated with a device in a JSON Installation that aligns with Push Notification Services and is easy toouse.</span></span>
* <span data-ttu-id="0c983-196">**유연성**: 개발자 위치에 항상 hello 통합 된 경우에 알림 허브에 직접 toowork을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-196">**Flexibility**: Developers can always choose toowork with Notification Hubs directly even with hello integration in place.</span></span>
* <span data-ttu-id="0c983-197">**통합 된 환경에서 [Azure 포털]**: 푸시 기능을 모바일 앱에서 시각적으로 표현 됩니다와 모바일 앱을 통해 연결 된 알림 허브 hello와 개발자가 쉽게 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-197">**Integrated experience in [Azure portal]**: Push as a capability is represented visually in Mobile Apps and developers can easily work with hello associated notification hub through Mobile Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c983-198">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0c983-198">Next Steps</span></span>
<span data-ttu-id="0c983-199">다음 항목에서 알림 허브에 대한 자세한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0c983-199">You can find out more about Notification Hubs in these topics:</span></span>

* <span data-ttu-id="0c983-200">**[고객이 알림 허브를 사용하는 방법]**</span><span class="sxs-lookup"><span data-stu-id="0c983-200">**[How customers are using Notification Hubs]**</span></span>
* <span data-ttu-id="0c983-201">**[알림 허브 자습서 및 가이드]**</span><span class="sxs-lookup"><span data-stu-id="0c983-201">**[Notification Hubs tutorials and guides]**</span></span>
* <span data-ttu-id="0c983-202">**Notification Hubs 시작 자습서**: [iOS], [Android], [Windows 범용], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="0c983-202">**Notification Hubs Getting Started tutorials**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span></span>

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[고객이 알림 허브를 사용하는 방법]: http://azure.microsoft.com/services/notification-hubs
[알림 허브 자습서 및 가이드]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows 범용]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[앱 서비스 모바일 앱]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[Azure 포털]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
