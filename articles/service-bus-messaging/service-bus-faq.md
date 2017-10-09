---
title: "서비스 버스 질문과 대답 (FAQ) aaaAzure | Microsoft Docs"
description: "Azure Service Bus에 대한 일부 자주 묻는 질문을 답변합니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a><span data-ttu-id="60e29-103">Service Bus FAQ</span><span class="sxs-lookup"><span data-stu-id="60e29-103">Service Bus FAQ</span></span>
<span data-ttu-id="60e29-104">이 문서는 Microsoft Azure Service Bus에 대한 일부 자주 묻는 질문을 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-104">This article answers some frequently asked questions about Microsoft Azure Service Bus.</span></span> <span data-ttu-id="60e29-105">Hello를 방문할 수도 [Azure 지원 Faq](http://go.microsoft.com/fwlink/?LinkID=185083) 일반적인 Azure 가격 책정 및 지원 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-105">You can also visit hello [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span>

## <a name="general-questions-about-azure-service-bus"></a><span data-ttu-id="60e29-106">Azure Service Bus에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="60e29-106">General questions about Azure Service Bus</span></span>
### <a name="what-is-azure-service-bus"></a><span data-ttu-id="60e29-107">Azure Service Bus란?</span><span class="sxs-lookup"><span data-stu-id="60e29-107">What is Azure Service Bus?</span></span>
<span data-ttu-id="60e29-108">[Azure 서비스 버스](service-bus-messaging-overview.md) 는 분리 된 시스템 간에 toosend 데이터 수 있는 비동기 메시징 클라우드 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-108">[Azure Service Bus](service-bus-messaging-overview.md) is an asynchronous messaging cloud platform that enables you toosend data between decoupled systems.</span></span> <span data-ttu-id="60e29-109">Microsoft는 하면 필요 하지 않고 toohost 순서 toouse의 고유한 하드웨어 중 하나 이므로 서비스로이 기능을 제공 하기.</span><span class="sxs-lookup"><span data-stu-id="60e29-109">Microsoft offers this feature as a service, which means that you do not need toohost any of your own hardware in order toouse it.</span></span>

### <a name="what-is-a-service-bus-namespace"></a><span data-ttu-id="60e29-110">Service Bus 네임스페이스란?</span><span class="sxs-lookup"><span data-stu-id="60e29-110">What is a Service Bus namespace?</span></span>
<span data-ttu-id="60e29-111">[네임스페이스](service-bus-create-namespace-portal.md)는 응용 프로그램 내에서 Service Bus 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-111">A [namespace](service-bus-create-namespace-portal.md) provides a scoping container for addressing Service Bus resources within your application.</span></span> <span data-ttu-id="60e29-112">하나를 만들면 필요한 toouse 서비스 버스 이며 hello 중 하나로 시작의 첫 번째 단계 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-112">Creating one is necessary toouse Service Bus and will be one of hello first steps in getting started.</span></span>

### <a name="what-is-an-azure-service-bus-queue"></a><span data-ttu-id="60e29-113">Azure Service Bus 큐란?</span><span class="sxs-lookup"><span data-stu-id="60e29-113">What is an Azure Service Bus queue?</span></span>
<span data-ttu-id="60e29-114">[Service Bus 큐](service-bus-queues-topics-subscriptions.md)는 메시지가 저장되는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-114">A [Service Bus queue](service-bus-queues-topics-subscriptions.md) is an entity in which messages are stored.</span></span> <span data-ttu-id="60e29-115">큐는 여러 응용 프로그램이 나 서로 toocommunicate 해야 하는 분산된 응용 프로그램의 여러 부분이 있는 경우에 특히 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-115">Queues are particularly useful when you have multiple applications, or multiple parts of a distributed application that need toocommunicate with each other.</span></span> <span data-ttu-id="60e29-116">hello 큐는 비슷한 tooa 배포 센터 여러 제품 (메시지)를 수신 하 고 해당 위치에서 전송 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-116">hello queue is similar tooa distribution center in that multiple products (messages) are received and then sent from that location.</span></span>

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a><span data-ttu-id="60e29-117">Azure Service Bus 토픽 및 구독이란?</span><span class="sxs-lookup"><span data-stu-id="60e29-117">What are Azure Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="60e29-118">토픽은 큐로 시각화할 수 있고 여러 구독을 사용하는 경우 더 풍부한 메시징 모델이 되며 기본적으로는 일대다 통신 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-118">A topic can be visualized as a queue and when using multiple subscriptions, it becomes a richer messaging model; essentially a one-to-many communication tool.</span></span> <span data-ttu-id="60e29-119">이 게시/등록 모델 (또는 *pub/sub*)을 여러 구독 toohave 포함 하는 메시지 tooa 항목 여러 응용 프로그램에서 받은 메시지를 보내는 응용 프로그램을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-119">This publish/subscribe model (or *pub/sub*) enables an application that sends a message tooa topic with multiple subscriptions toohave that message received by multiple applications.</span></span>

### <a name="what-is-a-partitioned-entity"></a><span data-ttu-id="60e29-120">분할된 엔터티란?</span><span class="sxs-lookup"><span data-stu-id="60e29-120">What is a partitioned entity?</span></span>
<span data-ttu-id="60e29-121">일반적인 큐 또는 항목은 단일 메시지 broker에서 처리되며 하나의 메시징 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-121">A conventional queue or topic is handled by a single message broker and stored in one messaging store.</span></span> <span data-ttu-id="60e29-122">[분할된 큐 또는 토픽](service-bus-partitioning.md)은 여러 메시지 broker에 의해 처리되고 여러 메시징 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-122">A [partitioned queue or topic](service-bus-partitioning.md) is handled by multiple message brokers and stored in multiple messaging stores.</span></span> <span data-ttu-id="60e29-123">이 즉, 분할 된 큐 또는 항목의 전체 처리량을 hello 더 이상 단일 메시지 브로커 또는 메시징 저장소의 hello 성능을 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-123">This means that hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="60e29-124">또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 항목을 계속 렌더링할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-124">In addition, a temporary outage of a messaging store does not render a partitioned queue or topic unavailable.</span></span>

<span data-ttu-id="60e29-125">분할 엔터티를 사용하는 경우 순서는 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-125">Note that ordering is not ensured when using partitioning entities.</span></span> <span data-ttu-id="60e29-126">파티션을 사용할 수 없다는 hello 이벤트에서 수 여전히 보내고 다른 파티션에 hello에서 메시지를 수신 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-126">In hello event that a partition is unavailable, you can still send and receive messages from hello other partitions.</span></span>

## <a name="best-practices"></a><span data-ttu-id="60e29-127">모범 사례</span><span class="sxs-lookup"><span data-stu-id="60e29-127">Best practices</span></span>
### <a name="what-are-some-azure-service-bus-best-practices"></a><span data-ttu-id="60e29-128">일부 Azure Service Bus 모범 사례는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="60e29-128">What are some Azure Service Bus best practices?</span></span>
* <span data-ttu-id="60e29-129">[서비스 버스를 사용 하 여 성능 향상에 대 한 유용한] [ Best practices for performance improvements using Service Bus] -이 문서에서는 메시지를 교환할 때 toooptimize 성능 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-129">[Best practices for performance improvements using Service Bus][Best practices for performance improvements using Service Bus] – this article describes how toooptimize performance when exchanging messages.</span></span>

### <a name="what-should-i-know-before-creating-entities"></a><span data-ttu-id="60e29-130">엔터티를 만들기 전에 무엇을 알아야 하나요?</span><span class="sxs-lookup"><span data-stu-id="60e29-130">What should I know before creating entities?</span></span>
<span data-ttu-id="60e29-131">다음과 같은 큐와 항목의 속성 hello는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-131">hello following properties of a queue and topic are immutable.</span></span> <span data-ttu-id="60e29-132">새 대체 엔터티를 만들지 않고 엔터티를 프로비전하는 경우 다음 항목을 수정할 수 없다는 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-132">Please take this into account when you provision your entities as this cannot be modified, without creating a new replacement entity.</span></span>

* <span data-ttu-id="60e29-133">크기</span><span class="sxs-lookup"><span data-stu-id="60e29-133">Size</span></span>
* <span data-ttu-id="60e29-134">분할</span><span class="sxs-lookup"><span data-stu-id="60e29-134">Partitioning</span></span>
* <span data-ttu-id="60e29-135">세션</span><span class="sxs-lookup"><span data-stu-id="60e29-135">Sessions</span></span>
* <span data-ttu-id="60e29-136">중복 검색</span><span class="sxs-lookup"><span data-stu-id="60e29-136">Duplicate detection</span></span>
* <span data-ttu-id="60e29-137">Express 엔터티</span><span class="sxs-lookup"><span data-stu-id="60e29-137">Express entity</span></span>

## <a name="pricing"></a><span data-ttu-id="60e29-138">가격</span><span class="sxs-lookup"><span data-stu-id="60e29-138">Pricing</span></span>
<span data-ttu-id="60e29-139">이 섹션 hello 서비스 버스 가격 구조에 대 한 몇 가지 자주 묻는 질문에 답변 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-139">This section answers some frequently-asked questions about hello Service Bus pricing structure.</span></span>

<span data-ttu-id="60e29-140">hello [서비스 버스 가격 및 요금 청구](service-bus-pricing-billing.md) 참조, 문서 설명 하 고 서비스 버스 가격 옵션에 대 한 정보에 대 한 서비스 버스의 hello 과금 단위 [서비스 버스 가격 정보](https://azure.microsoft.com/pricing/details/service-bus/)합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-140">hello [Service Bus pricing and billing](service-bus-pricing-billing.md) article explains hello billing meters in Service Bus, and for information about Service Bus pricing options, see [Service Bus pricing details](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>

<span data-ttu-id="60e29-141">Hello를 방문할 수도 [Azure 지원 Faq](http://go.microsoft.com/fwlink/?LinkID=185083) 일반 Azure 가격 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-141">You can also visit hello [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing information.</span></span> 

### <a name="how-do-you-charge-for-service-bus"></a><span data-ttu-id="60e29-142">Service Bus 요금을 어떻게 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="60e29-142">How do you charge for Service Bus?</span></span>
<span data-ttu-id="60e29-143">Service Bus 가격 책정에 대한 전체 내용은 [Service Bus 가격 책정 세부 정보][Pricing overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e29-143">For complete information about Service Bus pricing, please see [Service Bus pricing details][Pricing overview].</span></span> <span data-ttu-id="60e29-144">또한 toohello 가격 설명이 없는 한, 응용 프로그램 프로 비전 되는 hello 데이터 센터 외부의 수신을 위해 연결 된 데이터 전송에 대 한 요금이 청구 됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-144">In addition toohello prices noted, you are charged for associated data transfers for egress outside of hello data center in which your application is provisioned.</span></span>

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a><span data-ttu-id="60e29-145">서비스 버스의 어떤 사용은 주체 toodata 전송?</span><span class="sxs-lookup"><span data-stu-id="60e29-145">What usage of Service Bus is subject toodata transfer?</span></span> <span data-ttu-id="60e29-146">어떤 경우에 대상이 아닌가요?</span><span class="sxs-lookup"><span data-stu-id="60e29-146">What is not?</span></span>
<span data-ttu-id="60e29-147">지정된 Azure 지역 내에서 데이터 전송은 비용뿐만 아니라 인바운드 데이터 전송 없이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-147">Any data transfer within a given Azure region is provided at no charge, as well as any inbound data transfer.</span></span> <span data-ttu-id="60e29-148">해당 지역 외부의 데이터 전송 속도가 찾을 수 있는 제목 tooegress 요금 [여기](https://azure.microsoft.com/pricing/details/bandwidth/)합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-148">Data transfer outside a region is subject tooegress charges which can be found [here](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="does-service-bus-charge-for-storage"></a><span data-ttu-id="60e29-149">Service Bus는 저장소에 대한 요금을 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="60e29-149">Does Service Bus charge for storage?</span></span>
<span data-ttu-id="60e29-150">아니요, Service Bus는 저장소에 대한 요금을 청구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-150">No, Service Bus does not charge for storage.</span></span> <span data-ttu-id="60e29-151">그러나 한 할당량 제한 hello 최대 데이터 양을 큐/항목당 지속 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-151">However, there is a quota limiting hello maximum amount of data that can be persisted per queue/topic.</span></span> <span data-ttu-id="60e29-152">Hello 다음 FAQ를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="60e29-152">See hello next FAQ.</span></span>

## <a name="quotas"></a><span data-ttu-id="60e29-153">할당량</span><span class="sxs-lookup"><span data-stu-id="60e29-153">Quotas</span></span>

<span data-ttu-id="60e29-154">서비스 버스 제한 및 할당량 목록, 참조 hello [서비스 버스 할당량 개요][Quotas overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-154">For a list of Service Bus limits and quotas, see hello [Service Bus quotas overview][Quotas overview].</span></span>

### <a name="does-service-bus-have-any-usage-quotas"></a><span data-ttu-id="60e29-155">Service Bus는 사용 할당량이 있나요?</span><span class="sxs-lookup"><span data-stu-id="60e29-155">Does Service Bus have any usage quotas?</span></span>
<span data-ttu-id="60e29-156">기본적으로 모든 클라우드 서비스의 경우 Microsoft는 모든 고객의 구독에 대해 계산되는 월별 사용 할당량을 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-156">By default, for any cloud service Microsoft sets an aggregate monthly usage quota that is calculated across all of a customer's subscriptions.</span></span> <span data-ttu-id="60e29-157">이러한 제한 보다 사용자의 필요가 많을 수도 있다는 것을 이해하기 때문에 사용자의 요구를 이해하고 이러한 제한을 적절하게 조정할 수 있도록 언제든지 서비스에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="60e29-157">Because we understand that you may need more than these limits, please contact customer service at any time so that we can understand your needs and adjust these limits appropriately.</span></span> <span data-ttu-id="60e29-158">서비스 버스에 대 한 hello 집계 사용 할당량은 매달 5 십억 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-158">For Service Bus, hello aggregate usage quota is 5 billion messages per month.</span></span>

<span data-ttu-id="60e29-159">Hello 오른쪽 toodisable를 지정된 된 달에 사용 할당량을 초과한 고객 계정, 보유 하지만 전자 메일 알림을 제공 하 고 작업을 수행 하기 전에 여러 시도 toocontact 고객을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-159">While we do reserve hello right toodisable a customer account that has exceeded its usage quotas in a given month, we will provide e-mail notification and make multiple attempts toocontact a customer before taking any action.</span></span> <span data-ttu-id="60e29-160">이러한 할당량을 초과 하는 고객 hello 할당량을 초과 하는 요금에 대 한 지불 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-160">Customers exceeding these quotas will still be responsible for charges that exceed hello quotas.</span></span>

<span data-ttu-id="60e29-161">Azure에서 다른 서비스와 마찬가지로 서비스 버스 리소스의 공정한 사용 인지 특정 할당량 tooensure의 집합을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-161">As with other services on Azure, Service Bus enforces a set of specific quotas tooensure that there is fair usage of resources.</span></span> <span data-ttu-id="60e29-162">Hello에서 이러한 할당량에 대 한 자세한 정보를 찾을 수 있습니다 [서비스 버스 할당량 개요][Quotas overview]합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-162">You can find more details about these quotas in hello [Service Bus quotas overview][Quotas overview].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="60e29-163">문제 해결</span><span class="sxs-lookup"><span data-stu-id="60e29-163">Troubleshooting</span></span>
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a><span data-ttu-id="60e29-164">일부 Azure 서비스 버스 Api 및 해당 권장된 동작에서 생성 된 hello 예외 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="60e29-164">What are some of hello exceptions generated by Azure Service Bus APIs and their suggested actions?</span></span>
<span data-ttu-id="60e29-165">가능한 Service Bus 예외의 목록은 [예외 개요][Exceptions overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="60e29-165">For a list of possible Service Bus exceptions, see [Exceptions overview][Exceptions overview].</span></span>

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a><span data-ttu-id="60e29-166">공유 액세스 서명이란 무엇이고 어떤 언어가 서명 생성을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="60e29-166">What is a Shared Access Signature and which languages support generating a signature?</span></span>
<span data-ttu-id="60e29-167">공유 액세스 서명은 SHA – 256 보안 해시 또는 URI에 따른 인증 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-167">Shared Access Signatures are an authentication mechanism based on SHA – 256 secure hashes or URIs.</span></span> <span data-ttu-id="60e29-168">방법에 대 한 내용은 toogenerate 노드, PHP, Java 및 C의 고유한 서명을\#, hello 참조 [공유 액세스 서명] [ Shared Access Signatures] 문서.</span><span class="sxs-lookup"><span data-stu-id="60e29-168">For information about how toogenerate your own signatures in Node, PHP, Java and C\#, see hello [Shared Access Signatures][Shared Access Signatures] article.</span></span>

## <a name="subscription-and-namespace-management"></a><span data-ttu-id="60e29-169">구독 및 네임스페이스 관리</span><span class="sxs-lookup"><span data-stu-id="60e29-169">Subscription and namespace management</span></span>
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a><span data-ttu-id="60e29-170">네임 스페이스 tooanother Azure 구독을 마이그레이션하는 방법</span><span class="sxs-lookup"><span data-stu-id="60e29-170">How do I migrate a namespace tooanother Azure subscription?</span></span>

<span data-ttu-id="60e29-171">Hello 중 하나를 사용 하 여 하나의 Azure 구독 tooanother에서 네임 스페이스를 이동할 수 있습니다 [Azure 포털](https://portal.azure.com) 또는 PowerShell 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-171">You can move a namespace from one Azure subscription tooanother, using either hello [Azure portal](https://portal.azure.com) or PowerShell commands.</span></span> <span data-ttu-id="60e29-172">Tooexecute hello 작업 순서에서에서 hello 네임 스페이스 이미 여야 활성화 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-172">In order tooexecute hello operation, hello namespace must already be active.</span></span> <span data-ttu-id="60e29-173">hello 명령을 실행 하는 hello 사용자는 모두 hello 소스의 관리자 여야 하 고 대상 구독 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-173">hello user executing hello commands must be an administrator on both hello source and target subscriptions.</span></span>

#### <a name="portal"></a><span data-ttu-id="60e29-174">포털</span><span class="sxs-lookup"><span data-stu-id="60e29-174">Portal</span></span>

<span data-ttu-id="60e29-175">Azure 포털 toomigrate 서비스 버스 네임 스페이스 tooanother 구독 toouse hello hello 지시에 따라 [여기](../azure-resource-manager/resource-group-move-resources.md#use-portal)합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-175">toouse hello Azure portal toomigrate Service Bus namespaces tooanother subscription, follow hello directions [here](../azure-resource-manager/resource-group-move-resources.md#use-portal).</span></span> 

#### <a name="powershell"></a><span data-ttu-id="60e29-176">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60e29-176">PowerShell</span></span>

<span data-ttu-id="60e29-177">hello 다음의 PowerShell 명령 순서는 네임 스페이스에서에서 이동 하나의 Azure 구독 tooanother 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-177">hello following sequence of PowerShell commands moves a namespace from one Azure subscription tooanother.</span></span> <span data-ttu-id="60e29-178">tooexecute이이 작업을 hello 네임 스페이스 이미 활성 상태 여야 하 고 hello PowerShell 명령을 실행 하는 hello 사용자 두 hello 원본 및 대상 구독에서 관리자 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="60e29-178">tooexecute this operation, hello namespace must already be active, and hello user running hello PowerShell commands must be an administrator on both hello source and target subscriptions.</span></span>

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a><span data-ttu-id="60e29-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60e29-179">Next steps</span></span>
<span data-ttu-id="60e29-180">서비스 버스에 대 한 자세한 toolearn hello 다음 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="60e29-180">toolearn more about Service Bus, see hello following topics.</span></span>

* [<span data-ttu-id="60e29-181">Azure Service Bus 프리미엄 소개(블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="60e29-181">Introducing Azure Service Bus Premium (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="60e29-182">Azure Service Bus 프리미엄 소개(Channel9)</span><span class="sxs-lookup"><span data-stu-id="60e29-182">Introducing Azure Service Bus Premium (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="60e29-183">Service Bus 개요</span><span class="sxs-lookup"><span data-stu-id="60e29-183">Service Bus overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="60e29-184">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="60e29-184">Azure Service Bus architecture overview</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="60e29-185">Service Bus 큐 시작</span><span class="sxs-lookup"><span data-stu-id="60e29-185">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
