---
title: "알림 허브에 대 한 aaaSecurity"
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
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a><span data-ttu-id="9082a-103">보안</span><span class="sxs-lookup"><span data-stu-id="9082a-103">Security</span></span>
## <a name="overview"></a><span data-ttu-id="9082a-104">개요</span><span class="sxs-lookup"><span data-stu-id="9082a-104">Overview</span></span>
<span data-ttu-id="9082a-105">이 항목에서는 Azure 알림 허브의 hello 보안 모델에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-105">This topic describes hello security model of Azure Notification Hubs.</span></span> <span data-ttu-id="9082a-106">Hello를 구현 하 고 알림 허브 서비스 버스 엔터티의 이기 때문에 서비스 버스와 동일한 보안 모델.</span><span class="sxs-lookup"><span data-stu-id="9082a-106">Because Notification Hubs are a Service Bus entity, they implement hello same security model as Service Bus.</span></span> <span data-ttu-id="9082a-107">자세한 내용은 참조 hello [서비스 버스 인증](https://msdn.microsoft.com/library/azure/dn155925.aspx) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-107">For more information, see hello [Service Bus Authentication](https://msdn.microsoft.com/library/azure/dn155925.aspx) topics.</span></span>

## <a name="shared-access-signature-security-sas"></a><span data-ttu-id="9082a-108">SAS(공유 액세스 서명) 보안</span><span class="sxs-lookup"><span data-stu-id="9082a-108">Shared Access Signature Security (SAS)</span></span>
<span data-ttu-id="9082a-109">알림 허브는 SAS(공유 액세스 서명)라는 엔터티 수준 보안 체계를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-109">Notification Hubs implements an entity-level security scheme called SAS (Shared Access Signature).</span></span> <span data-ttu-id="9082a-110">이 체계는 메시징 엔터티 toodeclare를 too12 엔터티에 대 한 권한을 부여 하는 설명에 권한 부여 규칙을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-110">This scheme enables messaging entities toodeclare up too12 authorization rules in their description that grant rights on that entity.</span></span>

<span data-ttu-id="9082a-111">"보안 클레임입니다." hello 섹션에서 설명한 대로 각 규칙 이름, 키 값 (공유 암호) 및 권한 집합이 포함</span><span class="sxs-lookup"><span data-stu-id="9082a-111">Each rule contains a name, a key value (shared secret), and a set of rights, as explained in hello section “Security Claims.”</span></span> <span data-ttu-id="9082a-112">알림 허브를 만들 때 두 개의 규칙이 자동으로 만들어집니다: Listen 권한 (클라이언트 응용 프로그램에서는 hello) 및 모든 권한 (앱 백 엔드 사용 하 여 hello)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-112">When creating a Notification Hub, two rules are automatically created: one with Listen rights (that hello client app uses) and one with all rights (that hello app backend uses).</span></span>

<span data-ttu-id="9082a-113">Hello 정보를 통해 전송 하는 경우 클라이언트 응용 프로그램에서 등록 관리를 수행할 때 알림 (예: 날씨 업데이트)는 중요 한를 일반적인 방식으로 tooaccess 알림 허브는 hello 규칙 수신 전용 액세스 toohello의 toogive hello 키 값 클라이언트 응용 프로그램 및 toogive hello hello 규칙 대 한 모든 권한 toohello 앱 백 엔드에서의 키 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-113">When performing registration management from client apps, if hello information sent via notifications is not sensitive (for example, weather updates), a common way tooaccess a Notification Hub is toogive hello key value of hello rule Listen-only access toohello client app, and toogive hello key value of hello rule full access toohello app backend.</span></span>

<span data-ttu-id="9082a-114">Windows 스토어 클라이언트 응용 프로그램에 hello 키 값을 포함 하는 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-114">It is not recommended that you embed hello key value in Windows Store client apps.</span></span> <span data-ttu-id="9082a-115">Hello 키 값을 포함 하는 방식으로 tooavoid은 toohave hello에 대 한 클라이언트 응용 프로그램에서에서 검색할 시작 시 hello 앱 백 엔드에서.</span><span class="sxs-lookup"><span data-stu-id="9082a-115">A way tooavoid embedding hello key value is toohave hello client app retrieve it from hello app backend at startup.</span></span>

<span data-ttu-id="9082a-116">반드시 수신 액세스 권한이 있는 키 hello toounderstand 앱 tooregister 모든 태그에 대 한 클라이언트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-116">It is important toounderstand that hello key with Listen access allows a client app tooregister for any tag.</span></span> <span data-ttu-id="9082a-117">앱 등록 toospecific 태그 toospecific 클라이언트 (예: 사용자 Id를 나타내는 태그)를 제한 해야 하는 경우 앱 백 hello 등록을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-117">If your app must restrict registrations toospecific tags toospecific clients (for example, when tags represent user IDs), then your app backend must perform hello registrations.</span></span> <span data-ttu-id="9082a-118">자세한 내용은 등록 관리를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9082a-118">For more information, see Registration Management.</span></span> <span data-ttu-id="9082a-119">이러한 방식으로 hello 클라이언트 응용 프로그램에는 하지도 직접 액세스 tooNotification 허브 참고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-119">Note that in this way, hello client app will not have direct access tooNotification Hubs.</span></span>

## <a name="security-claims"></a><span data-ttu-id="9082a-120">보안 클레임</span><span class="sxs-lookup"><span data-stu-id="9082a-120">Security claims</span></span>
<span data-ttu-id="9082a-121">알림 허브 작업은 세 가지 보안 클레임에 대 한 허용 비슷한 tooother 엔터티: 수신 대기, 전송 및 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-121">Similar tooother entities, Notification Hub operations are allowed for three security claims: Listen, Send, and Manage.</span></span>

| <span data-ttu-id="9082a-122">클레임</span><span class="sxs-lookup"><span data-stu-id="9082a-122">Claim</span></span> | <span data-ttu-id="9082a-123">설명</span><span class="sxs-lookup"><span data-stu-id="9082a-123">Description</span></span> | <span data-ttu-id="9082a-124">허용되는 연산</span><span class="sxs-lookup"><span data-stu-id="9082a-124">Operations allowed</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9082a-125">수신 대기</span><span class="sxs-lookup"><span data-stu-id="9082a-125">Listen</span></span> |<span data-ttu-id="9082a-126">단일 등록 만들기/업데이트, 읽기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="9082a-126">Create/Update, Read, and Delete single registrations</span></span> |<span data-ttu-id="9082a-127">등록 만들기/업데이트</span><span class="sxs-lookup"><span data-stu-id="9082a-127">Create/Update registration</span></span><br><br><span data-ttu-id="9082a-128">등록 읽기</span><span class="sxs-lookup"><span data-stu-id="9082a-128">Read registration</span></span><br><br><span data-ttu-id="9082a-129">핸들에 대한 모든 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="9082a-129">Read all registrations for a handle</span></span><br><br><span data-ttu-id="9082a-130">등록 삭제</span><span class="sxs-lookup"><span data-stu-id="9082a-130">Delete registration</span></span> |
| <span data-ttu-id="9082a-131">보내기</span><span class="sxs-lookup"><span data-stu-id="9082a-131">Send</span></span> |<span data-ttu-id="9082a-132">보낼 메시지 toohello 알림 허브</span><span class="sxs-lookup"><span data-stu-id="9082a-132">Send messages toohello notification hub</span></span> |<span data-ttu-id="9082a-133">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9082a-133">Send message</span></span> |
| <span data-ttu-id="9082a-134">관리</span><span class="sxs-lookup"><span data-stu-id="9082a-134">Manage</span></span> |<span data-ttu-id="9082a-135">알림 허브의 CRUD(PNS 자격 증명 및 보안 키 업데이트 포함) 및 태그 기준 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="9082a-135">CRUDs on Notification Hubs (including updating PNS credentials, and security keys), and read registrations based on tags</span></span> |<span data-ttu-id="9082a-136">알림 허브 만들기/업데이트/읽기/삭제</span><span class="sxs-lookup"><span data-stu-id="9082a-136">Create/Update/Read/Delete notification hubs</span></span><br><br><span data-ttu-id="9082a-137">태그별 등록 읽기</span><span class="sxs-lookup"><span data-stu-id="9082a-137">Read registrations by tag</span></span> |

<span data-ttu-id="9082a-138">알림 허브와 Microsoft Azure 액세스 제어 토큰 및 hello 알림 허브에서 직접 구성한 공유 키를 사용 하 여 생성 한 서명 토큰을 부여 하는 클레임을 수락 합니다.</span><span class="sxs-lookup"><span data-stu-id="9082a-138">Notification Hubs accept claims granted by Microsoft Azure Access Control tokens, and by signature tokens generated with shared keys configured directly on hello Notification Hub.</span></span>

