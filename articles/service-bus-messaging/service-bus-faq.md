---
title: Azure Service Bus FAQ | Microsoft Docs
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
ms.openlocfilehash: 1403184d96388cb03b2c767c4da342ec1c6fe236
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-faq"></a><span data-ttu-id="24121-103">Service Bus FAQ</span><span class="sxs-lookup"><span data-stu-id="24121-103">Service Bus FAQ</span></span>
<span data-ttu-id="24121-104">이 문서는 Microsoft Azure Service Bus에 대한 일부 자주 묻는 질문을 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-104">This article answers some frequently asked questions about Microsoft Azure Service Bus.</span></span> <span data-ttu-id="24121-105">또한 일반적인 Azure 가격 책정 및 지원 정보는 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-105">You can also visit the [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span>

## <a name="general-questions-about-azure-service-bus"></a><span data-ttu-id="24121-106">Azure Service Bus에 대한 일반적인 질문</span><span class="sxs-lookup"><span data-stu-id="24121-106">General questions about Azure Service Bus</span></span>
### <a name="what-is-azure-service-bus"></a><span data-ttu-id="24121-107">Azure Service Bus란?</span><span class="sxs-lookup"><span data-stu-id="24121-107">What is Azure Service Bus?</span></span>
<span data-ttu-id="24121-108">[Azure Service Bus](service-bus-messaging-overview.md)는 분리된 시스템 간에 데이터를 보낼 수 있도록 하는 비동기 메시지 클라우드 플랫폼입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-108">[Azure Service Bus](service-bus-messaging-overview.md) is an asynchronous messaging cloud platform that enables you to send data between decoupled systems.</span></span> <span data-ttu-id="24121-109">Microsoft에서 이 기능을 서비스로 제공하므로 이를 사용하기 위해 고유한 하드웨어 중 하나를 호스트할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-109">Microsoft offers this feature as a service, which means that you do not need to host any of your own hardware in order to use it.</span></span>

### <a name="what-is-a-service-bus-namespace"></a><span data-ttu-id="24121-110">Service Bus 네임스페이스란?</span><span class="sxs-lookup"><span data-stu-id="24121-110">What is a Service Bus namespace?</span></span>
<span data-ttu-id="24121-111">[네임스페이스](service-bus-create-namespace-portal.md)는 응용 프로그램 내에서 Service Bus 리소스의 주소를 지정하기 위한 범위 컨테이너를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-111">A [namespace](service-bus-create-namespace-portal.md) provides a scoping container for addressing Service Bus resources within your application.</span></span> <span data-ttu-id="24121-112">네임스페이스를 만드는 작업은 Service Bus를 사용하는 데 필요하고 Service Bus를 시작하는 첫 번째 단계 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-112">Creating one is necessary to use Service Bus and will be one of the first steps in getting started.</span></span>

### <a name="what-is-an-azure-service-bus-queue"></a><span data-ttu-id="24121-113">Azure Service Bus 큐란?</span><span class="sxs-lookup"><span data-stu-id="24121-113">What is an Azure Service Bus queue?</span></span>
<span data-ttu-id="24121-114">[Service Bus 큐](service-bus-queues-topics-subscriptions.md)는 메시지가 저장되는 엔터티입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-114">A [Service Bus queue](service-bus-queues-topics-subscriptions.md) is an entity in which messages are stored.</span></span> <span data-ttu-id="24121-115">큐는 서로 통신해야 하는 여러 응용 프로그램 또는 분산된 응용 프로그램의 여러 부분이 있는 경우에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-115">Queues are particularly useful when you have multiple applications, or multiple parts of a distributed application that need to communicate with each other.</span></span> <span data-ttu-id="24121-116">큐는 여러 제품(메시지)를 해당 위치에서 받고 보내는 배포 센터와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-116">The queue is similar to a distribution center in that multiple products (messages) are received and then sent from that location.</span></span>

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a><span data-ttu-id="24121-117">Azure Service Bus 토픽 및 구독이란?</span><span class="sxs-lookup"><span data-stu-id="24121-117">What are Azure Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="24121-118">토픽은 큐로 시각화할 수 있고 여러 구독을 사용하는 경우 더 풍부한 메시징 모델이 되며 기본적으로는 일대다 통신 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-118">A topic can be visualized as a queue and when using multiple subscriptions, it becomes a richer messaging model; essentially a one-to-many communication tool.</span></span> <span data-ttu-id="24121-119">이 게시/구독 모델(또는 *pub/sub*)을 사용하면 여러 응용 프로그램에서 받은 메시지를 여러 구독을 사용하여 토픽에 메시지를 전송하는 응용 프로그램을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-119">This publish/subscribe model (or *pub/sub*) enables an application that sends a message to a topic with multiple subscriptions to have that message received by multiple applications.</span></span>

### <a name="what-is-a-partitioned-entity"></a><span data-ttu-id="24121-120">분할된 엔터티란?</span><span class="sxs-lookup"><span data-stu-id="24121-120">What is a partitioned entity?</span></span>
<span data-ttu-id="24121-121">일반적인 큐 또는 항목은 단일 메시지 broker에서 처리되며 하나의 메시징 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="24121-121">A conventional queue or topic is handled by a single message broker and stored in one messaging store.</span></span> <span data-ttu-id="24121-122">[분할된 큐 또는 토픽](service-bus-partitioning.md)은 여러 메시지 broker에 의해 처리되고 여러 메시징 저장소에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="24121-122">A [partitioned queue or topic](service-bus-partitioning.md) is handled by multiple message brokers and stored in multiple messaging stores.</span></span> <span data-ttu-id="24121-123">즉, 분할된 큐 또는 항목의 전체 처리량은 단일 메시지 broker 또는 메시징 저장소의 성능으로 제한되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-123">This means that the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="24121-124">또한 메시징 스토어가 일시적으로 중단된 경우에도 분할된 큐 또는 항목을 계속 렌더링할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-124">In addition, a temporary outage of a messaging store does not render a partitioned queue or topic unavailable.</span></span>

<span data-ttu-id="24121-125">분할 엔터티를 사용하는 경우 순서는 보장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-125">Note that ordering is not ensured when using partitioning entities.</span></span> <span data-ttu-id="24121-126">파티션을 사용할 수 없는 이벤트에서도 여전히 메세지를 보내고 다른 파티션에서 메시지를 수신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-126">In the event that a partition is unavailable, you can still send and receive messages from the other partitions.</span></span>

## <a name="best-practices"></a><span data-ttu-id="24121-127">모범 사례</span><span class="sxs-lookup"><span data-stu-id="24121-127">Best practices</span></span>
### <a name="what-are-some-azure-service-bus-best-practices"></a><span data-ttu-id="24121-128">일부 Azure Service Bus 모범 사례는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="24121-128">What are some Azure Service Bus best practices?</span></span>
* <span data-ttu-id="24121-129">[Service Bus를 사용한 성능 향상에 대한 모범 사례][Best practices for performance improvements using Service Bus] - 이 문서에서는 메시지를 교환할 때 성능을 최적화하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-129">[Best practices for performance improvements using Service Bus][Best practices for performance improvements using Service Bus] – this article describes how to optimize performance when exchanging messages.</span></span>

### <a name="what-should-i-know-before-creating-entities"></a><span data-ttu-id="24121-130">엔터티를 만들기 전에 무엇을 알아야 하나요?</span><span class="sxs-lookup"><span data-stu-id="24121-130">What should I know before creating entities?</span></span>
<span data-ttu-id="24121-131">큐 및 토픽에서 다음 속성을 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-131">The following properties of a queue and topic are immutable.</span></span> <span data-ttu-id="24121-132">새 대체 엔터티를 만들지 않고 엔터티를 프로비전하는 경우 다음 항목을 수정할 수 없다는 점을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-132">Please take this into account when you provision your entities as this cannot be modified, without creating a new replacement entity.</span></span>

* <span data-ttu-id="24121-133">크기</span><span class="sxs-lookup"><span data-stu-id="24121-133">Size</span></span>
* <span data-ttu-id="24121-134">분할</span><span class="sxs-lookup"><span data-stu-id="24121-134">Partitioning</span></span>
* <span data-ttu-id="24121-135">세션</span><span class="sxs-lookup"><span data-stu-id="24121-135">Sessions</span></span>
* <span data-ttu-id="24121-136">중복 검색</span><span class="sxs-lookup"><span data-stu-id="24121-136">Duplicate detection</span></span>
* <span data-ttu-id="24121-137">Express 엔터티</span><span class="sxs-lookup"><span data-stu-id="24121-137">Express entity</span></span>

## <a name="pricing"></a><span data-ttu-id="24121-138">가격</span><span class="sxs-lookup"><span data-stu-id="24121-138">Pricing</span></span>
<span data-ttu-id="24121-139">이 섹션은 Service Bus 가격 책정 구조에 대한 일부 자주 묻는 질문을 답변합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-139">This section answers some frequently-asked questions about the Service Bus pricing structure.</span></span>

<span data-ttu-id="24121-140">[Service Bus 가격 책정 및 청구](service-bus-pricing-billing.md) 문서에서는 Service Bus의 청구 미터에 대해 설명합니다. Service Bus 가격 책정 옵션에 대한 자세한 내용은 [Service Bus 가격 책정 정보](https://azure.microsoft.com/pricing/details/service-bus/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-140">The [Service Bus pricing and billing](service-bus-pricing-billing.md) article explains the billing meters in Service Bus, and for information about Service Bus pricing options, see [Service Bus pricing details](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>

<span data-ttu-id="24121-141">또한 일반적인 Azure 가격 책정 정보는 [Azure 지원 FAQ](http://go.microsoft.com/fwlink/?LinkID=185083)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-141">You can also visit the [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing information.</span></span> 

### <a name="how-do-you-charge-for-service-bus"></a><span data-ttu-id="24121-142">Service Bus 요금을 어떻게 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="24121-142">How do you charge for Service Bus?</span></span>
<span data-ttu-id="24121-143">Service Bus 가격 책정에 대한 전체 내용은 [Service Bus 가격 책정 세부 정보][Pricing overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-143">For complete information about Service Bus pricing, please see [Service Bus pricing details][Pricing overview].</span></span> <span data-ttu-id="24121-144">언급된 가격 외에도 응용 프로그램이 프로비전되는 데이터 센터의 외부에서 송신을 위해 연결된 데이터 전송에 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="24121-144">In addition to the prices noted, you are charged for associated data transfers for egress outside of the data center in which your application is provisioned.</span></span>

### <a name="what-usage-of-service-bus-is-subject-to-data-transfer-what-is-not"></a><span data-ttu-id="24121-145">Service Bus를 어떻게 사용하면 데이터가 전송의 대상이 되나요?</span><span class="sxs-lookup"><span data-stu-id="24121-145">What usage of Service Bus is subject to data transfer?</span></span> <span data-ttu-id="24121-146">어떤 경우에 대상이 아닌가요?</span><span class="sxs-lookup"><span data-stu-id="24121-146">What is not?</span></span>
<span data-ttu-id="24121-147">지정된 Azure 지역 내에서 데이터 전송은 비용뿐만 아니라 인바운드 데이터 전송 없이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="24121-147">Any data transfer within a given Azure region is provided at no charge, as well as any inbound data transfer.</span></span> <span data-ttu-id="24121-148">지역 외부의 데이터 전송은 [여기](https://azure.microsoft.com/pricing/details/bandwidth/)에서 찾을 수 있는 송신 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="24121-148">Data transfer outside a region is subject to egress charges which can be found [here](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="does-service-bus-charge-for-storage"></a><span data-ttu-id="24121-149">Service Bus는 저장소에 대한 요금을 청구하나요?</span><span class="sxs-lookup"><span data-stu-id="24121-149">Does Service Bus charge for storage?</span></span>
<span data-ttu-id="24121-150">아니요, Service Bus는 저장소에 대한 요금을 청구하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-150">No, Service Bus does not charge for storage.</span></span> <span data-ttu-id="24121-151">하지만 큐/항목 당 지속될 수 있는 데이터의 최대 크기를 제한하는 할당량이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-151">However, there is a quota limiting the maximum amount of data that can be persisted per queue/topic.</span></span> <span data-ttu-id="24121-152">다음 FAQ를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-152">See the next FAQ.</span></span>

## <a name="quotas"></a><span data-ttu-id="24121-153">할당량</span><span class="sxs-lookup"><span data-stu-id="24121-153">Quotas</span></span>

<span data-ttu-id="24121-154">Service Bus 제한 및 할당량 목록은 [Service Bus 할당량 개요][Quotas overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-154">For a list of Service Bus limits and quotas, see the [Service Bus quotas overview][Quotas overview].</span></span>

### <a name="does-service-bus-have-any-usage-quotas"></a><span data-ttu-id="24121-155">Service Bus는 사용 할당량이 있나요?</span><span class="sxs-lookup"><span data-stu-id="24121-155">Does Service Bus have any usage quotas?</span></span>
<span data-ttu-id="24121-156">기본적으로 모든 클라우드 서비스의 경우 Microsoft는 모든 고객의 구독에 대해 계산되는 월별 사용 할당량을 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-156">By default, for any cloud service Microsoft sets an aggregate monthly usage quota that is calculated across all of a customer's subscriptions.</span></span> <span data-ttu-id="24121-157">이러한 제한 보다 사용자의 필요가 많을 수도 있다는 것을 이해하기 때문에 사용자의 요구를 이해하고 이러한 제한을 적절하게 조정할 수 있도록 언제든지 서비스에 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-157">Because we understand that you may need more than these limits, please contact customer service at any time so that we can understand your needs and adjust these limits appropriately.</span></span> <span data-ttu-id="24121-158">Service Bus의 경우 집계 사용 할당량은 매월 5십억 개의 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-158">For Service Bus, the aggregate usage quota is 5 billion messages per month.</span></span>

<span data-ttu-id="24121-159">지정된 달에 사용 할당량을 초과하는 고객의 계정을 사용하지 않도록 설정하는 권한을 보유하지만 메일 알림을 제공하며 조치를 취하기 전에 고객에게 연락을 여러 번 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-159">While we do reserve the right to disable a customer account that has exceeded its usage quotas in a given month, we will provide e-mail notification and make multiple attempts to contact a customer before taking any action.</span></span> <span data-ttu-id="24121-160">이러한 할당량을 초과하는 고객은 할당량을 초과하는 요금을 지불해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-160">Customers exceeding these quotas will still be responsible for charges that exceed the quotas.</span></span>

<span data-ttu-id="24121-161">Azure에서 다른 서비스와 마찬가지로 Service Bus는 리소스의 공정한 사용을 보장하기 위해 특정한 할당량 집합을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-161">As with other services on Azure, Service Bus enforces a set of specific quotas to ensure that there is fair usage of resources.</span></span> <span data-ttu-id="24121-162">[Service Bus 할당량 개요][Quotas overview]에서 이러한 할당량에 대한 자세한 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-162">You can find more details about these quotas in the [Service Bus quotas overview][Quotas overview].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="24121-163">문제 해결</span><span class="sxs-lookup"><span data-stu-id="24121-163">Troubleshooting</span></span>
### <a name="what-are-some-of-the-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a><span data-ttu-id="24121-164">Azure Service Bus API 및 해당 제안된 작업에 의해 생성된 일부 예외는 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="24121-164">What are some of the exceptions generated by Azure Service Bus APIs and their suggested actions?</span></span>
<span data-ttu-id="24121-165">가능한 Service Bus 예외의 목록은 [예외 개요][Exceptions overview]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-165">For a list of possible Service Bus exceptions, see [Exceptions overview][Exceptions overview].</span></span>

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a><span data-ttu-id="24121-166">공유 액세스 서명이란 무엇이고 어떤 언어가 서명 생성을 지원하나요?</span><span class="sxs-lookup"><span data-stu-id="24121-166">What is a Shared Access Signature and which languages support generating a signature?</span></span>
<span data-ttu-id="24121-167">공유 액세스 서명은 SHA – 256 보안 해시 또는 URI에 따른 인증 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="24121-167">Shared Access Signatures are an authentication mechanism based on SHA – 256 secure hashes or URIs.</span></span> <span data-ttu-id="24121-168">노드, PHP, Java 및 C\#에서 직접 서명을 생성하는 방법에 대한 내용은 [공유 액세스 서명][Shared Access Signatures] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-168">For information about how to generate your own signatures in Node, PHP, Java and C\#, see the [Shared Access Signatures][Shared Access Signatures] article.</span></span>

## <a name="subscription-and-namespace-management"></a><span data-ttu-id="24121-169">구독 및 네임스페이스 관리</span><span class="sxs-lookup"><span data-stu-id="24121-169">Subscription and namespace management</span></span>
### <a name="how-do-i-migrate-a-namespace-to-another-azure-subscription"></a><span data-ttu-id="24121-170">다른 Azure 구독으로 네임스페이스를 마이그레이션하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="24121-170">How do I migrate a namespace to another Azure subscription?</span></span>

<span data-ttu-id="24121-171">[Azure Portal](https://portal.azure.com) 또는 PowerShell 명령을 사용하여 Azure 구독 간에 네임스페이스를 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="24121-171">You can move a namespace from one Azure subscription to another, using either the [Azure portal](https://portal.azure.com) or PowerShell commands.</span></span> <span data-ttu-id="24121-172">작업을 실행하기 위해 네임스페이스가 활성화되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-172">In order to execute the operation, the namespace must already be active.</span></span> <span data-ttu-id="24121-173">명령을 실행하는 사용자는 원본 및 대상 구독에 대한 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-173">The user executing the commands must be an administrator on both the source and target subscriptions.</span></span>

#### <a name="portal"></a><span data-ttu-id="24121-174">포털</span><span class="sxs-lookup"><span data-stu-id="24121-174">Portal</span></span>

<span data-ttu-id="24121-175">Azure Portal을 사용하여 Service Bus 네임스페이스를 다른 구독으로 마이그레이션하려면 [여기](../azure-resource-manager/resource-group-move-resources.md#use-portal)에 있는 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="24121-175">To use the Azure portal to migrate Service Bus namespaces to another subscription, follow the directions [here](../azure-resource-manager/resource-group-move-resources.md#use-portal).</span></span> 

#### <a name="powershell"></a><span data-ttu-id="24121-176">PowerShell</span><span class="sxs-lookup"><span data-stu-id="24121-176">PowerShell</span></span>

<span data-ttu-id="24121-177">다음 PowerShell 명령 시퀀스는 네임스페이스를 Azure 구독 간에 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-177">The following sequence of PowerShell commands moves a namespace from one Azure subscription to another.</span></span> <span data-ttu-id="24121-178">이 작업을 실행하려면 네임스페이스 이미 활성 상태여야 하며 PowerShell 명령을 실행하는 사용자는 원본 및 대상 구독의 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="24121-178">To execute this operation, the namespace must already be active, and the user running the PowerShell commands must be an administrator on both the source and target subscriptions.</span></span>

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription to target subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a><span data-ttu-id="24121-179">다음 단계</span><span class="sxs-lookup"><span data-stu-id="24121-179">Next steps</span></span>
<span data-ttu-id="24121-180">Service Bus에 대한 자세한 내용은 다음 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="24121-180">To learn more about Service Bus, see the following topics.</span></span>

* [<span data-ttu-id="24121-181">Azure Service Bus 프리미엄 소개(블로그 게시물)</span><span class="sxs-lookup"><span data-stu-id="24121-181">Introducing Azure Service Bus Premium (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="24121-182">Azure Service Bus 프리미엄 소개(Channel9)</span><span class="sxs-lookup"><span data-stu-id="24121-182">Introducing Azure Service Bus Premium (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="24121-183">Service Bus 개요</span><span class="sxs-lookup"><span data-stu-id="24121-183">Service Bus overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="24121-184">Azure Service Bus 아키텍처 개요</span><span class="sxs-lookup"><span data-stu-id="24121-184">Azure Service Bus architecture overview</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="24121-185">Service Bus 큐 시작</span><span class="sxs-lookup"><span data-stu-id="24121-185">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
