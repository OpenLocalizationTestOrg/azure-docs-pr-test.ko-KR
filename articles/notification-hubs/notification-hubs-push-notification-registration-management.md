---
title: "등록 관리"
description: "이 항목에서는 푸시 알림을 받기 위해 알림 허브에 장치를 등록하는 방법에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="56418-103">등록 관리</span><span class="sxs-lookup"><span data-stu-id="56418-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="56418-104">개요</span><span class="sxs-lookup"><span data-stu-id="56418-104">Overview</span></span>
<span data-ttu-id="56418-105">이 항목에서는 푸시 알림을 받기 위해 알림 허브에 장치를 등록하는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="56418-106">먼저 높은 수준에서 등록을 설명한 다음 장치를 등록하는 두 가지 주 패턴, 즉 장치에서 알림 허브에 직접 등록 및 응용 프로그램 백 엔드를 통해 등록을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="56418-107">장치 등록이란?</span><span class="sxs-lookup"><span data-stu-id="56418-107">What is device registration</span></span>
<span data-ttu-id="56418-108">Notification Hub에 장치 등록은 **등록** 또는 **설치**를 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="56418-109">등록</span><span class="sxs-lookup"><span data-stu-id="56418-109">Registrations</span></span>
<span data-ttu-id="56418-110">등록은 태그 및 아마도 템플릿을 가진 장치에 대해 플랫폼 알림 서비스(PNS) 핸들을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="56418-111">PNS 핸들은 ChannelURI, 장치 토큰 또는 GCM 등록 ID일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="56418-112">태그는 장치 핸들의 정확한 집합에 알림을 올바른 장치 핸들 집합에 라우팅하기 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="56418-113">자세한 내용은 [라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="56418-114">템플릿은 등록당 변환을 구현하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="56418-115">자세한 내용은 [템플릿](notification-hubs-templates-cross-platform-push-messages.md)을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="56418-116">설치</span><span class="sxs-lookup"><span data-stu-id="56418-116">Installations</span></span>
<span data-ttu-id="56418-117">설치는 푸시 모음 관련 속성을 포함하고 있는 향상된 등록입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="56418-118">이는 장치 등록에 대한 최근의 가장 우수한 방식입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="56418-119">그러나 아직 클라이언트 쪽 .NET SDK([백 엔드 작업을 위한 알림 허브 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/))에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="56418-120">즉, 클라이언트 장치 자체에서 등록하는 경우 설치를 지원하기 위해 [알림 허브 REST API](https://msdn.microsoft.com/library/mt621153.aspx) 접근 방식을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="56418-121">백 엔드 서비스를 사용하는 경우 [백 엔드 작업을 위한 알림 허브 SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="56418-122">설치 사용의 몇 가지 주요 장점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="56418-123">설치 만들기 또는 업데이트가 완전히 멱등 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="56418-124">따라서 중복 등록을 걱정할 필요 없이 재시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="56418-125">설치 모델은 개별 푸시 - 특정 장치 대상 지정이 쉽게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="56418-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="56418-126">시스템 태그 **"$InstallationId:[installationId]"** 는 각 설치 기반 등록에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="56418-127">따라서 추가 코딩을 수행할 필요 없이 이 태그 보내기를 호출하여 특정 장치를 대상 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="56418-128">또한 설치를 사용하여 부분적인 등록 업데이트를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="56418-129">설치의 부분 업데이트는 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902)을 사용하여 PATCH 메서드에서 요청됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="56418-130">이는 등록 시 태그를 업데이트하려고 할 때 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="56418-131">전체 등록을 풀다운한 다음 모든 이전 태그를 다시 보낼 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="56418-132">설치는 다음과 같은 속성을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="56418-133">설치 속성의 전체 목록은 [REST API를 사용하여 설치 만들기 또는 덮어쓰기](https://msdn.microsoft.com/library/azure/mt621153.aspx) 또는 [설치 속성](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



<span data-ttu-id="56418-134">기본적으로 등록 및 설치는 더 이상 만료되지 않음에 유의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="56418-135">등록 및 설치는 각 장치/채널에 대한 유효한 PNS 핸들을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="56418-136">PNS 핸들은 장치의 클라이언트 앱에서만 획득할 수 있으므로 한 가지 패턴은 클라이언트 앱을 사용하여 해당 장치에서 직접 등록하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="56418-137">한편 태그와 관련된 보안 고려 사항 및 비즈니스 논리 때문에 앱 백 엔드에서 장치 등록을 관리해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="56418-138">템플릿</span><span class="sxs-lookup"><span data-stu-id="56418-138">Templates</span></span>
<span data-ttu-id="56418-139">[템플릿](notification-hubs-templates-cross-platform-push-messages.md)을 사용하려면 장치 설치에서 해당 장치와 연결된 모든 템플릿을 JSON 형식으로 유지합니다(위 샘플 참조).</span><span class="sxs-lookup"><span data-stu-id="56418-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="56418-140">템플릿 이름은는 동일한 장치에 대한 서로 다른 템플릿을 대상 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="56418-141">참고로 각 템플릿 이름은 템플릿 본문 및 선택적 태그 집합에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="56418-142">또한 각 플랫폼이 추가 템플릿 속성을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="56418-143">Windows 스토어(WNS 사용) 및 Windows Phone 8(MPNS 사용)의 경우 추가 헤더 집합이 템플릿의 일부일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="56418-144">APN의 경우 만료 속성을 상수 또는 템플릿 식으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="56418-145">설치 속성의 전체 목록은 [REST를 사용하여 설치 만들기 또는 덮어쓰기](https://msdn.microsoft.com/library/azure/mt621153.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="56418-146">Windows 스토어 앱용 보조 타일</span><span class="sxs-lookup"><span data-stu-id="56418-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="56418-147">Windows 스토어 클라이언트 응용 프로그램의 경우 보조 타일에 알림을 보내는 것은 기본 타일에 보내는 것과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="56418-148">이 기능은 설치에서도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-148">This is also supported in installations.</span></span> <span data-ttu-id="56418-149">참고로 보조 타일에는 클라이언트 앱의 SDK가 투명하게 처리하는 다른 ChannelUri가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="56418-150">SecondaryTiles 사전은 Windows 스토어 앱에서 SecondaryTiles 개체를 만드는 데 사용하는 것과 같은 TileId를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="56418-151">기본 ChannelUri와 마찬가지로 보조 타일의 ChannelUris도 언제든지 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="56418-152">알림 허브의 설치를 계속 업데이트되게 하려면 장치가 설치를 보조 타일의 현재 ChannelUris로 새로 고쳐야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="56418-153">장치에서 등록 관리</span><span class="sxs-lookup"><span data-stu-id="56418-153">Registration management from the device</span></span>
<span data-ttu-id="56418-154">클라이언트 앱에서 장치 등록을 관리하는 경우 백 엔드만는 알림을 보내기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="56418-155">클라이언트 앱은 PNS 핸들을 최신 상태로 유지하고 태그를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="56418-156">다음 그림은 이 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56418-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="56418-157">장치는 먼저 PNS에서 PNS 핸들을 검색한 다음 알림 허브에 직접 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="56418-158">등록이 성공한 후 앱 백 엔드는 해당 등록을 대상으로 지정하는 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="56418-159">알림을 보내는 방법에 대한 자세한 내용은 [라우팅 및 태그 식](notification-hubs-tags-segment-push-message.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="56418-160">참고로 이 경우 수신 권한만 사용하여 장치에서 사용자의 알림 허브에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="56418-161">자세한 내용은 [보안](notification-hubs-push-notification-security.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56418-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="56418-162">장치에서 등록은 가장 간단한 방법이지만 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="56418-163">첫 번째 단점은 클라이언트 앱이 활성 상태일 때에만 태그를 업데이트할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="56418-164">예를 들어 사용자가 스포츠 팀과 관련된 태그를 등록하는 장치 두 개를 가지고 있는 경우 첫 번째 장치가 추가 태그(예: Seahawks)에 대해 등록하면 두 번째 장치는 두 번째 장치의 앱이 두 번째로 실행될 때까지 Seahawks에 관한 알림을 받지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="56418-165">더 일반적으로 태그가 여러 장치의 영향을 받는 경우 백 엔드에서 태그 관리가 바람직한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="56418-166">클라이언트 앱에서 등록 관리의 두 번째 단점은 앱이 해킹을 당할 수 있으므로 “태그 수준 보안" 섹션에서 설명했듯이 특정 태그에 대한 등록을 보호하려면 좀 더 주의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="56418-167">설치를 사용하여 장치에서 알림 허브에 등록하는 예제 코드</span><span class="sxs-lookup"><span data-stu-id="56418-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="56418-168">현재 이 기능은 [알림 허브 REST API](https://msdn.microsoft.com/library/mt621153.aspx)를 사용해서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="56418-169">설치를 업데이트하는 경우 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902) 을 사용하여 PATCH 메서드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine the targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="56418-170">등록을 사용하여 장치에서 알림 허브에 등록하는 예제 코드</span><span class="sxs-lookup"><span data-stu-id="56418-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="56418-171">이러한 메서드는 호출되는 장치에 대한 등록을 만들거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="56418-172">즉, 핸들이나 태그를 업데이트하려면 전체 등록을 덮어써야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="56418-173">참고로 등록은 일시적이므로 언제나 특정 장치에 필요한 현재 태그와 함께 신뢰할 수 있는 저장소가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="56418-174">백 엔드에서 등록 관리</span><span class="sxs-lookup"><span data-stu-id="56418-174">Registration management from a backend</span></span>
<span data-ttu-id="56418-175">백 엔드에서 등록을 관리하려면 추가 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="56418-176">장치의 앱은 앱이 시작될 때마다 업데이트된 PNS 핸들을 백 엔드에 제공해야 하며(태그 및 템플릿과 함께), 백 엔드는 알림 허브에 대해 이 핸들을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="56418-177">다음 그림은 이 디자인을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="56418-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="56418-178">백 엔드에서 등록을 관리할 경우의 이점은 장치의 해당 앱이 비활성화되었을 때에도 등록에 대한 태그를 수정할 수 있고 태그를 등록에 추가하기 전에 클라이언트 앱을 인증할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="56418-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="56418-179">설치를 사용하여 백 엔드에서 알림 허브에 등록하는 예제 코드</span><span class="sxs-lookup"><span data-stu-id="56418-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="56418-180">클라이언트 장치는 여전히 해당 PNS 핸들 및 관련 설치 속성을 전과 같이 가져오며 등록을 수행하고 태그 등에 권한을 부여할 수 있는 백 엔드의 사용자 지정 API를 호출합니다. 백 엔드는 [백 엔드 작업용 Notification Hub SDK](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)를 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="56418-181">설치를 업데이트하는 경우 [JSON 패치 표준](https://tools.ietf.org/html/rfc6902) 을 사용하여 PATCH 메서드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="56418-182">등록 ID를 사용하여 장치에서 알림 허브에 등록하는 예제 코드</span><span class="sxs-lookup"><span data-stu-id="56418-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="56418-183">앱 백 엔드에서 등록에 대해 기본 CRUDS 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56418-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="56418-184">예:</span><span class="sxs-lookup"><span data-stu-id="56418-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


<span data-ttu-id="56418-185">백 엔드에서 등록 업데이트 간의 동시성을 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="56418-186">서비스 버스는 등록 관리를 위해 낙관적 동시성 제어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="56418-187">HTTP 수준에서 이 기능은 등록 관리 작업에 ETag를 사용하여 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="56418-188">이 기능은 동시성 문제로 인해 업데이트가 거부될 경우 예외를 throw하는 Microsoft SDK에 의해 투명하게 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="56418-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="56418-189">앱 백 엔드는 이러한 예외를 처리하고 필요한 경우 업데이트를 다시 시도하는 일을 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="56418-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

