---
title: "알림 허브에 대한 보안"
description: "이 항목에서는 Azure 알림 허브 보안에 대해 설명합니다."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 7c3283799806135060bb8ca57ea398c93d1106bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="security"></a><span data-ttu-id="907e7-103">보안</span><span class="sxs-lookup"><span data-stu-id="907e7-103">Security</span></span>
## <a name="overview"></a><span data-ttu-id="907e7-104">개요</span><span class="sxs-lookup"><span data-stu-id="907e7-104">Overview</span></span>
<span data-ttu-id="907e7-105">이 항목에서는 Azure 알림 허브의 보안 모델에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-105">This topic describes the security model of Azure Notification Hubs.</span></span> <span data-ttu-id="907e7-106">알림 허브는 서비스 버스 엔터티이므로 서비스 버스와 동일한 보안 모델을 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-106">Because Notification Hubs are a Service Bus entity, they implement the same security model as Service Bus.</span></span> <span data-ttu-id="907e7-107">자세한 내용은 [서비스 버스 인증](https://msdn.microsoft.com/library/azure/dn155925.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e7-107">For more information, see the [Service Bus Authentication](https://msdn.microsoft.com/library/azure/dn155925.aspx) topics.</span></span>

## <a name="shared-access-signature-security-sas"></a><span data-ttu-id="907e7-108">SAS(공유 액세스 서명) 보안</span><span class="sxs-lookup"><span data-stu-id="907e7-108">Shared Access Signature Security (SAS)</span></span>
<span data-ttu-id="907e7-109">알림 허브는 SAS(공유 액세스 서명)라는 엔터티 수준 보안 체계를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-109">Notification Hubs implements an entity-level security scheme called SAS (Shared Access Signature).</span></span> <span data-ttu-id="907e7-110">이 체계를 통해 메시징 엔터티가 해당 엔터티에 대한 권한을 부여하는 설명에서 최대 12개의 권한 부여 규칙을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-110">This scheme enables messaging entities to declare up to 12 authorization rules in their description that grant rights on that entity.</span></span>

<span data-ttu-id="907e7-111">"보안 클레임" 섹션에 설명된 대로 각 규칙에는 이름, 키 값(공유 암호) 및 권한 집합이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-111">Each rule contains a name, a key value (shared secret), and a set of rights, as explained in the section “Security Claims.”</span></span> <span data-ttu-id="907e7-112">알림 허브를 만들 때 두 개의 규칙이 자동으로 만들어집니다. 즉, 클라이언트 앱에서 사용하는 수신 대기 권한이 있는 규칙과 앱 백 엔드에서 사용하는 모든 권한이 있는 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-112">When creating a Notification Hub, two rules are automatically created: one with Listen rights (that the client app uses) and one with all rights (that the app backend uses).</span></span>

<span data-ttu-id="907e7-113">클라이언트 앱에서 등록 관리를 수행할 때 날씨 업데이트와 같이 알림을 통해 보낸 정보가 중요하지 않으면 알림 허브에 액세스하는 일반적인 방법은 규칙 수신 대기 전용 액세스의 키 값을 클라이언트 앱에 부여하는 것과 규칙 모든 권한의 키 값을 앱 백 엔드에 부여하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-113">When performing registration management from client apps, if the information sent via notifications is not sensitive (for example, weather updates), a common way to access a Notification Hub is to give the key value of the rule Listen-only access to the client app, and to give the key value of the rule full access to the app backend.</span></span>

<span data-ttu-id="907e7-114">Windows 스토어 클라이언트 앱에 키 값을 포함하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-114">It is not recommended that you embed the key value in Windows Store client apps.</span></span> <span data-ttu-id="907e7-115">키 값을 포함하지 않는 방법은 클라이언트 앱이 시작할 때 앱 백 엔드에서 키 값을 검색하도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-115">A way to avoid embedding the key value is to have the client app retrieve it from the app backend at startup.</span></span>

<span data-ttu-id="907e7-116">수신 대기 액세스가 있는 키를 통해 클라이언트 앱이 모든 태그를 등록할 수 있음을 이해하는 것이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-116">It is important to understand that the key with Listen access allows a client app to register for any tag.</span></span> <span data-ttu-id="907e7-117">앱이 특정 클라이언트에 대한 특정 태그로 등록을 제한해야 하는 경우(예: 태그가 사용자 ID를 나타내는 경우) 앱 백 엔드가 등록을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-117">If your app must restrict registrations to specific tags to specific clients (for example, when tags represent user IDs), then your app backend must perform the registrations.</span></span> <span data-ttu-id="907e7-118">자세한 내용은 등록 관리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="907e7-118">For more information, see Registration Management.</span></span> <span data-ttu-id="907e7-119">이러한 방식으로 클라이언트 앱이 알림 허브에 직접 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-119">Note that in this way, the client app will not have direct access to Notification Hubs.</span></span>

## <a name="security-claims"></a><span data-ttu-id="907e7-120">보안 클레임</span><span class="sxs-lookup"><span data-stu-id="907e7-120">Security claims</span></span>
<span data-ttu-id="907e7-121">다른 엔터티와 마찬가지로 알림 허브 작업에 허용된 3가지 보안 클레임은 수신 대기, 전송 및 관리입니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-121">Similar to other entities, Notification Hub operations are allowed for three security claims: Listen, Send, and Manage.</span></span>

| <span data-ttu-id="907e7-122">클레임</span><span class="sxs-lookup"><span data-stu-id="907e7-122">Claim</span></span> | <span data-ttu-id="907e7-123">설명</span><span class="sxs-lookup"><span data-stu-id="907e7-123">Description</span></span> | <span data-ttu-id="907e7-124">허용되는 연산</span><span class="sxs-lookup"><span data-stu-id="907e7-124">Operations allowed</span></span> |
| --- | --- | --- |
| <span data-ttu-id="907e7-125">수신 대기</span><span class="sxs-lookup"><span data-stu-id="907e7-125">Listen</span></span> |<span data-ttu-id="907e7-126">단일 등록 만들기/업데이트, 읽기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="907e7-126">Create/Update, Read, and Delete single registrations</span></span> |<span data-ttu-id="907e7-127">등록 만들기/업데이트</span><span class="sxs-lookup"><span data-stu-id="907e7-127">Create/Update registration</span></span><br><br><span data-ttu-id="907e7-128">등록 읽기</span><span class="sxs-lookup"><span data-stu-id="907e7-128">Read registration</span></span><br><br><span data-ttu-id="907e7-129">핸들에 대한 모든 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="907e7-129">Read all registrations for a handle</span></span><br><br><span data-ttu-id="907e7-130">등록 삭제</span><span class="sxs-lookup"><span data-stu-id="907e7-130">Delete registration</span></span> |
| <span data-ttu-id="907e7-131">보내기</span><span class="sxs-lookup"><span data-stu-id="907e7-131">Send</span></span> |<span data-ttu-id="907e7-132">알림 허브에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="907e7-132">Send messages to the notification hub</span></span> |<span data-ttu-id="907e7-133">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="907e7-133">Send message</span></span> |
| <span data-ttu-id="907e7-134">관리</span><span class="sxs-lookup"><span data-stu-id="907e7-134">Manage</span></span> |<span data-ttu-id="907e7-135">알림 허브의 CRUD(PNS 자격 증명 및 보안 키 업데이트 포함) 및 태그 기준 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="907e7-135">CRUDs on Notification Hubs (including updating PNS credentials, and security keys), and read registrations based on tags</span></span> |<span data-ttu-id="907e7-136">알림 허브 만들기/업데이트/읽기/삭제</span><span class="sxs-lookup"><span data-stu-id="907e7-136">Create/Update/Read/Delete notification hubs</span></span><br><br><span data-ttu-id="907e7-137">태그별 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="907e7-137">Read registrations by tag</span></span> |

<span data-ttu-id="907e7-138">알림 허브는 Microsoft Azure 액세스 제어 토큰 및 알림 허브에서 직접 구성하는 공유 키로 생성된 서명 토큰에서 부여한 클레임을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="907e7-138">Notification Hubs accept claims granted by Microsoft Azure Access Control tokens, and by signature tokens generated with shared keys configured directly on the Notification Hub.</span></span>

