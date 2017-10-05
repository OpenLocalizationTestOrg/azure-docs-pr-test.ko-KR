---
title: "Azure Service Bus 요청-응답 기간 작업에서 AMQP 1.0 | Microsoft Docs"
description: "Microsoft Azure Service Bus 요청/응답 기반 작업 목록입니다."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: 756565b3da6e0a818d1ee3d5e17f942d96be14f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a><span data-ttu-id="6ae71-103">Microsoft Azure Service Bus에서 AMQP 1.0: Microsoft Azure Service Bus 요청/응답 기반 작업</span><span class="sxs-lookup"><span data-stu-id="6ae71-103">AMQP 1.0 in Microsoft Azure Service Bus: request-response-based operations</span></span>

<span data-ttu-id="6ae71-104">이 항목에서는 Microsoft Azure Service Bus 요청/응답 기반 작업 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-104">This topic defines the list of Microsoft Azure Service Bus request/response-based operations.</span></span> <span data-ttu-id="6ae71-105">이 정보는 AMQP Management Version 1.0 초안을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-105">This information is based on the AMQP Management Version 1.0 working draft.</span></span>  
  
<span data-ttu-id="6ae71-106">Service Bus가 OASIS AMQP 기술 사양을 구현하고 빌드하는 방법을 설명하는 자세한 유선 수준 AMQP 1.0 프로토콜 가이드는 [Azure Service Bus 및 Event Hubs 프로토콜 가이드의 AMQP 1.0](service-bus-amqp-protocol-guide.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6ae71-106">For a detailed wire-level AMQP 1.0 protocol guide, which explains how Service Bus implements and builds on the OASIS AMQP technical specification, see the [AMQP 1.0 in Azure Service Bus and Event Hubs protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="concepts"></a><span data-ttu-id="6ae71-107">개념</span><span class="sxs-lookup"><span data-stu-id="6ae71-107">Concepts</span></span>  
  
### <a name="entity-description"></a><span data-ttu-id="6ae71-108">엔터티 설명</span><span class="sxs-lookup"><span data-stu-id="6ae71-108">Entity description</span></span>  

<span data-ttu-id="6ae71-109">엔터티 설명은 Service Bus [QueueDescription Class](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription Class](/dotnet/api/microsoft.servicebus.messaging.topicdescription) 또는 [SubscriptionDescription Class](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-109">An entity description refers to either a Service Bus [QueueDescription Class](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription Class](/dotnet/api/microsoft.servicebus.messaging.topicdescription), or [SubscriptionDescription Class](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) object.</span></span>  
  
### <a name="brokered-message"></a><span data-ttu-id="6ae71-110">broker 저장 메시지</span><span class="sxs-lookup"><span data-stu-id="6ae71-110">Brokered message</span></span>  

<span data-ttu-id="6ae71-111">AMQP 메시지에 매핑되는 Service Bus의 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-111">Represents a message in Service Bus, which is mapped to an AMQP message.</span></span> <span data-ttu-id="6ae71-112">이 매핑은 [Service Bus AMQP 프로토콜 가이드](service-bus-amqp-protocol-guide.md)에서 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-112">The mapping is defined in the [Service Bus AMQP protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="attach-to-entity-management-node"></a><span data-ttu-id="6ae71-113">엔터티 관리 노드에 연결</span><span class="sxs-lookup"><span data-stu-id="6ae71-113">Attach to entity management node</span></span>  

<span data-ttu-id="6ae71-114">이 문서에 설명된 모든 작업은 요청/응답 패턴을 따르며 엔터티로 범위가 지정되며 엔터티 관리 노드에 연결되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-114">All the operations described in this document follow a request/response pattern, are scoped to an entity, and require attaching to an entity management node.</span></span>  
  
### <a name="create-link-for-sending-requests"></a><span data-ttu-id="6ae71-115">요청 전송을 위한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="6ae71-115">Create link for sending requests</span></span>  

<span data-ttu-id="6ae71-116">요청 전송을 위해 관리 노드에 대한 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-116">Creates a link to the management node for sending requests.</span></span>  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a><span data-ttu-id="6ae71-117">응답 수신을 위한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="6ae71-117">Create link for receiving responses</span></span>  

<span data-ttu-id="6ae71-118">관리 노드에서 응답 수신을 위한 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-118">Creates a link for receiving responses from the management node.</span></span>  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a><span data-ttu-id="6ae71-119">요청 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="6ae71-119">Transfer a request message</span></span>  

<span data-ttu-id="6ae71-120">요청 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-120">Transfers a request message.</span></span>  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a><span data-ttu-id="6ae71-121">응답 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="6ae71-121">Receive a response message</span></span>  

<span data-ttu-id="6ae71-122">응답 링크에서 응답 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-122">Receives the response message from the response link.</span></span>  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
<span data-ttu-id="6ae71-123">응답 메시지는 다음 형식으로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-123">The response message is in the following form:</span></span>
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a><span data-ttu-id="6ae71-124">Service Bus 엔터티 주소</span><span class="sxs-lookup"><span data-stu-id="6ae71-124">Service Bus entity address</span></span>  

<span data-ttu-id="6ae71-125">Service Bus 엔터티 주소는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-125">Service Bus entities must be addressed as follows:</span></span>  
  
|<span data-ttu-id="6ae71-126">엔터티 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-126">Entity type</span></span>|<span data-ttu-id="6ae71-127">주소</span><span class="sxs-lookup"><span data-stu-id="6ae71-127">Address</span></span>|<span data-ttu-id="6ae71-128">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-128">Example</span></span>|  
|-----------------|-------------|-------------|  
|<span data-ttu-id="6ae71-129">큐</span><span class="sxs-lookup"><span data-stu-id="6ae71-129">queue</span></span>|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|<span data-ttu-id="6ae71-130">토픽</span><span class="sxs-lookup"><span data-stu-id="6ae71-130">topic</span></span>|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|<span data-ttu-id="6ae71-131">subscription</span><span class="sxs-lookup"><span data-stu-id="6ae71-131">subscription</span></span>|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a><span data-ttu-id="6ae71-132">메시지 작업</span><span class="sxs-lookup"><span data-stu-id="6ae71-132">Message operations</span></span>  
  
### <a name="message-renew-lock"></a><span data-ttu-id="6ae71-133">메시지 갱신 잠금</span><span class="sxs-lookup"><span data-stu-id="6ae71-133">Message Renew Lock</span></span>  

<span data-ttu-id="6ae71-134">엔터티 설명에 지정된 시간까지 메시지 잠금을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-134">Extends the lock of a message by the time specified in the entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-135">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-135">Request</span></span>  

<span data-ttu-id="6ae71-136">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-136">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-137">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-137">Key</span></span>|<span data-ttu-id="6ae71-138">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-138">Value Type</span></span>|<span data-ttu-id="6ae71-139">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-139">Required</span></span>|<span data-ttu-id="6ae71-140">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-140">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-141">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-141">operation</span></span>|<span data-ttu-id="6ae71-142">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-142">string</span></span>|<span data-ttu-id="6ae71-143">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-143">Yes</span></span>|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-144">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-144">uint</span></span>|<span data-ttu-id="6ae71-145">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-145">No</span></span>|<span data-ttu-id="6ae71-146">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-146">Operation server timeout in milliseconds.</span></span>|  
  
 <span data-ttu-id="6ae71-147">요청 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 amqp-value 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-147">The request message body must consist of an amqp-value section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-148">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-148">Key</span></span>|<span data-ttu-id="6ae71-149">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-149">Value Type</span></span>|<span data-ttu-id="6ae71-150">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-150">Required</span></span>|<span data-ttu-id="6ae71-151">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-151">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|<span data-ttu-id="6ae71-152">uuid의 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-152">array of uuid</span></span>|<span data-ttu-id="6ae71-153">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-153">Yes</span></span>|<span data-ttu-id="6ae71-154">갱신할 메시지 잠금 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-154">Message lock tokens to renew.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-155">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-155">Response</span></span>  

<span data-ttu-id="6ae71-156">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-156">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-157">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-157">Key</span></span>|<span data-ttu-id="6ae71-158">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-158">Value Type</span></span>|<span data-ttu-id="6ae71-159">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-159">Required</span></span>|<span data-ttu-id="6ae71-160">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-160">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-161">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-161">statusCode</span></span>|<span data-ttu-id="6ae71-162">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-162">int</span></span>|<span data-ttu-id="6ae71-163">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-163">Yes</span></span>|<span data-ttu-id="6ae71-164">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-164">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-165">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-165">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="6ae71-166">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-166">statusDescription</span></span>|<span data-ttu-id="6ae71-167">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-167">string</span></span>|<span data-ttu-id="6ae71-168">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-168">No</span></span>|<span data-ttu-id="6ae71-169">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-169">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-170">응답 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 amqp-value 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-170">The response message body must consist of an amqp-value section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-171">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-171">Key</span></span>|<span data-ttu-id="6ae71-172">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-172">Value Type</span></span>|<span data-ttu-id="6ae71-173">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-173">Required</span></span>|<span data-ttu-id="6ae71-174">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-174">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-175">만료</span><span class="sxs-lookup"><span data-stu-id="6ae71-175">expirations</span></span>|<span data-ttu-id="6ae71-176">타임 스탬프 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-176">array of timestamp</span></span>|<span data-ttu-id="6ae71-177">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-177">Yes</span></span>|<span data-ttu-id="6ae71-178">요청 잠금 토큰에 해당하는 메시지 잠금 토큰 새 만료입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-178">Message lock token new expiration corresponding to the request lock tokens.</span></span>|  
  
### <a name="peek-message"></a><span data-ttu-id="6ae71-179">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="6ae71-179">Peek Message</span></span>  

<span data-ttu-id="6ae71-180">잠그지 않고 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-180">Peeks messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-181">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-181">Request</span></span>  

<span data-ttu-id="6ae71-182">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-182">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-183">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-183">Key</span></span>|<span data-ttu-id="6ae71-184">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-184">Value Type</span></span>|<span data-ttu-id="6ae71-185">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-185">Required</span></span>|<span data-ttu-id="6ae71-186">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-186">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-187">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-187">operation</span></span>|<span data-ttu-id="6ae71-188">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-188">string</span></span>|<span data-ttu-id="6ae71-189">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-189">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-190">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-190">uint</span></span>|<span data-ttu-id="6ae71-191">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-191">No</span></span>|<span data-ttu-id="6ae71-192">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-192">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-193">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-193">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-194">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-194">Key</span></span>|<span data-ttu-id="6ae71-195">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-195">Value Type</span></span>|<span data-ttu-id="6ae71-196">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-196">Required</span></span>|<span data-ttu-id="6ae71-197">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-197">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|<span data-ttu-id="6ae71-198">long</span><span class="sxs-lookup"><span data-stu-id="6ae71-198">long</span></span>|<span data-ttu-id="6ae71-199">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-199">Yes</span></span>|<span data-ttu-id="6ae71-200">보기를 시작할 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-200">Sequence number from which to start peek.</span></span>|  
|`message-count`|<span data-ttu-id="6ae71-201">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-201">int</span></span>|<span data-ttu-id="6ae71-202">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-202">Yes</span></span>|<span data-ttu-id="6ae71-203">보려는 최대 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-203">Maximum number of messages to peek.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-204">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-204">Response</span></span>  

<span data-ttu-id="6ae71-205">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-205">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-206">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-206">Key</span></span>|<span data-ttu-id="6ae71-207">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-207">Value Type</span></span>|<span data-ttu-id="6ae71-208">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-208">Required</span></span>|<span data-ttu-id="6ae71-209">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-209">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-210">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-210">statusCode</span></span>|<span data-ttu-id="6ae71-211">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-211">int</span></span>|<span data-ttu-id="6ae71-212">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-212">Yes</span></span>|<span data-ttu-id="6ae71-213">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-213">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-214">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="6ae71-214">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="6ae71-215">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="6ae71-215">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="6ae71-216">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-216">statusDescription</span></span>|<span data-ttu-id="6ae71-217">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-217">string</span></span>|<span data-ttu-id="6ae71-218">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-218">No</span></span>|<span data-ttu-id="6ae71-219">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-219">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-220">응답 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-220">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-221">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-221">Key</span></span>|<span data-ttu-id="6ae71-222">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-222">Value Type</span></span>|<span data-ttu-id="6ae71-223">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-223">Required</span></span>|<span data-ttu-id="6ae71-224">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-224">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-225">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="6ae71-225">messages</span></span>|<span data-ttu-id="6ae71-226">맵 목록</span><span class="sxs-lookup"><span data-stu-id="6ae71-226">list of maps</span></span>|<span data-ttu-id="6ae71-227">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-227">Yes</span></span>|<span data-ttu-id="6ae71-228">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-228">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="6ae71-229">메시지를 나타내는 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-229">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-230">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-230">Key</span></span>|<span data-ttu-id="6ae71-231">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-231">Value Type</span></span>|<span data-ttu-id="6ae71-232">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-232">Required</span></span>|<span data-ttu-id="6ae71-233">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-233">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-234">message</span><span class="sxs-lookup"><span data-stu-id="6ae71-234">message</span></span>|<span data-ttu-id="6ae71-235">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-235">array of byte</span></span>|<span data-ttu-id="6ae71-236">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-236">Yes</span></span>|<span data-ttu-id="6ae71-237">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-237">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="schedule-message"></a><span data-ttu-id="6ae71-238">메시지 예약</span><span class="sxs-lookup"><span data-stu-id="6ae71-238">Schedule Message</span></span>  

<span data-ttu-id="6ae71-239">메시지를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-239">Schedules messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-240">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-240">Request</span></span>  

<span data-ttu-id="6ae71-241">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-241">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-242">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-242">Key</span></span>|<span data-ttu-id="6ae71-243">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-243">Value Type</span></span>|<span data-ttu-id="6ae71-244">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-244">Required</span></span>|<span data-ttu-id="6ae71-245">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-245">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-246">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-246">operation</span></span>|<span data-ttu-id="6ae71-247">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-247">string</span></span>|<span data-ttu-id="6ae71-248">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-248">Yes</span></span>|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-249">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-249">uint</span></span>|<span data-ttu-id="6ae71-250">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-250">No</span></span>|<span data-ttu-id="6ae71-251">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-251">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-252">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-252">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-253">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-253">Key</span></span>|<span data-ttu-id="6ae71-254">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-254">Value Type</span></span>|<span data-ttu-id="6ae71-255">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-255">Required</span></span>|<span data-ttu-id="6ae71-256">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-256">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-257">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="6ae71-257">messages</span></span>|<span data-ttu-id="6ae71-258">맵 목록</span><span class="sxs-lookup"><span data-stu-id="6ae71-258">list of maps</span></span>|<span data-ttu-id="6ae71-259">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-259">Yes</span></span>|<span data-ttu-id="6ae71-260">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-260">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="6ae71-261">메시지를 나타내는 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-261">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-262">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-262">Key</span></span>|<span data-ttu-id="6ae71-263">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-263">Value Type</span></span>|<span data-ttu-id="6ae71-264">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-264">Required</span></span>|<span data-ttu-id="6ae71-265">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-265">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-266">message-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-266">message-id</span></span>|<span data-ttu-id="6ae71-267">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-267">string</span></span>|<span data-ttu-id="6ae71-268">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-268">Yes</span></span>|<span data-ttu-id="6ae71-269">string으로 `amqpMessage.Properties.MessageId`</span><span class="sxs-lookup"><span data-stu-id="6ae71-269">`amqpMessage.Properties.MessageId` as string</span></span>|  
|<span data-ttu-id="6ae71-270">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-270">session-id</span></span>|<span data-ttu-id="6ae71-271">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-271">string</span></span>|<span data-ttu-id="6ae71-272">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-272">Yes</span></span>|`amqpMessage.Properties.GroupId as string`|  
|<span data-ttu-id="6ae71-273">파티션 키</span><span class="sxs-lookup"><span data-stu-id="6ae71-273">partition-key</span></span>|<span data-ttu-id="6ae71-274">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-274">string</span></span>|<span data-ttu-id="6ae71-275">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-275">Yes</span></span>|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|<span data-ttu-id="6ae71-276">message</span><span class="sxs-lookup"><span data-stu-id="6ae71-276">message</span></span>|<span data-ttu-id="6ae71-277">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-277">array of byte</span></span>|<span data-ttu-id="6ae71-278">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-278">Yes</span></span>|<span data-ttu-id="6ae71-279">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-279">AMQP 1.0 wire-encoded message.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-280">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-280">Response</span></span>  

<span data-ttu-id="6ae71-281">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-281">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-282">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-282">Key</span></span>|<span data-ttu-id="6ae71-283">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-283">Value Type</span></span>|<span data-ttu-id="6ae71-284">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-284">Required</span></span>|<span data-ttu-id="6ae71-285">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-285">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-286">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-286">statusCode</span></span>|<span data-ttu-id="6ae71-287">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-287">int</span></span>|<span data-ttu-id="6ae71-288">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-288">Yes</span></span>|<span data-ttu-id="6ae71-289">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-289">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-290">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-290">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="6ae71-291">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-291">statusDescription</span></span>|<span data-ttu-id="6ae71-292">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-292">string</span></span>|<span data-ttu-id="6ae71-293">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-293">No</span></span>|<span data-ttu-id="6ae71-294">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-294">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-295">응답 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-295">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-296">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-296">Key</span></span>|<span data-ttu-id="6ae71-297">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-297">Value Type</span></span>|<span data-ttu-id="6ae71-298">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-298">Required</span></span>|<span data-ttu-id="6ae71-299">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-299">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-300">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="6ae71-300">sequence-numbers</span></span>|<span data-ttu-id="6ae71-301">long 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-301">array of long</span></span>|<span data-ttu-id="6ae71-302">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-302">Yes</span></span>|<span data-ttu-id="6ae71-303">예약된 메시지의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-303">Sequence number of scheduled messages.</span></span> <span data-ttu-id="6ae71-304">시퀀스 번호는 취소하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-304">Sequence number is used to cancel.</span></span>|  
  
### <a name="cancel-scheduled-message"></a><span data-ttu-id="6ae71-305">예약된 메시지 취소</span><span class="sxs-lookup"><span data-stu-id="6ae71-305">Cancel Scheduled Message</span></span>  

<span data-ttu-id="6ae71-306">예약된 메시지를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-306">Cancels scheduled messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-307">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-307">Request</span></span>  

<span data-ttu-id="6ae71-308">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-308">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-309">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-309">Key</span></span>|<span data-ttu-id="6ae71-310">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-310">Value Type</span></span>|<span data-ttu-id="6ae71-311">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-311">Required</span></span>|<span data-ttu-id="6ae71-312">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-312">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-313">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-313">operation</span></span>|<span data-ttu-id="6ae71-314">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-314">string</span></span>|<span data-ttu-id="6ae71-315">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-315">Yes</span></span>|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-316">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-316">uint</span></span>|<span data-ttu-id="6ae71-317">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-317">No</span></span>|<span data-ttu-id="6ae71-318">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-318">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-319">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-319">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-320">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-320">Key</span></span>|<span data-ttu-id="6ae71-321">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-321">Value Type</span></span>|<span data-ttu-id="6ae71-322">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-322">Required</span></span>|<span data-ttu-id="6ae71-323">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-323">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-324">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="6ae71-324">sequence-numbers</span></span>|<span data-ttu-id="6ae71-325">long 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-325">array of long</span></span>|<span data-ttu-id="6ae71-326">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-326">Yes</span></span>|<span data-ttu-id="6ae71-327">취소할 예약된 메시지의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-327">Sequence numbers of scheduled messages to cancel.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-328">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-328">Response</span></span>  

<span data-ttu-id="6ae71-329">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-329">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-330">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-330">Key</span></span>|<span data-ttu-id="6ae71-331">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-331">Value Type</span></span>|<span data-ttu-id="6ae71-332">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-332">Required</span></span>|<span data-ttu-id="6ae71-333">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-333">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-334">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-334">statusCode</span></span>|<span data-ttu-id="6ae71-335">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-335">int</span></span>|<span data-ttu-id="6ae71-336">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-336">Yes</span></span>|<span data-ttu-id="6ae71-337">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-337">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-338">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-338">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="6ae71-339">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-339">statusDescription</span></span>|<span data-ttu-id="6ae71-340">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-340">string</span></span>|<span data-ttu-id="6ae71-341">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-341">No</span></span>|<span data-ttu-id="6ae71-342">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-342">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-343">응답 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-343">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-344">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-344">Key</span></span>|<span data-ttu-id="6ae71-345">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-345">Value Type</span></span>|<span data-ttu-id="6ae71-346">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-346">Required</span></span>|<span data-ttu-id="6ae71-347">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-347">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-348">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="6ae71-348">sequence-numbers</span></span>|<span data-ttu-id="6ae71-349">long 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-349">array of long</span></span>|<span data-ttu-id="6ae71-350">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-350">Yes</span></span>|<span data-ttu-id="6ae71-351">예약된 메시지의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-351">Sequence number of scheduled messages.</span></span> <span data-ttu-id="6ae71-352">시퀀스 번호는 취소하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-352">Sequence number is used to cancel.</span></span>|  
  
## <a name="session-operations"></a><span data-ttu-id="6ae71-353">세션 작업</span><span class="sxs-lookup"><span data-stu-id="6ae71-353">Session Operations</span></span>  
  
### <a name="session-renew-lock"></a><span data-ttu-id="6ae71-354">세션 갱신 잠금</span><span class="sxs-lookup"><span data-stu-id="6ae71-354">Session Renew Lock</span></span>  

<span data-ttu-id="6ae71-355">엔터티 설명에 지정된 시간까지 메시지 잠금을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-355">Extends the lock of a message by the time specified in the entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-356">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-356">Request</span></span>  

<span data-ttu-id="6ae71-357">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-357">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-358">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-358">Key</span></span>|<span data-ttu-id="6ae71-359">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-359">Value Type</span></span>|<span data-ttu-id="6ae71-360">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-360">Required</span></span>|<span data-ttu-id="6ae71-361">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-361">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-362">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-362">operation</span></span>|<span data-ttu-id="6ae71-363">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-363">string</span></span>|<span data-ttu-id="6ae71-364">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-364">Yes</span></span>|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-365">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-365">uint</span></span>|<span data-ttu-id="6ae71-366">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-366">No</span></span>|<span data-ttu-id="6ae71-367">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-367">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-368">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-368">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-369">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-369">Key</span></span>|<span data-ttu-id="6ae71-370">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-370">Value Type</span></span>|<span data-ttu-id="6ae71-371">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-371">Required</span></span>|<span data-ttu-id="6ae71-372">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-372">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-373">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-373">session-id</span></span>|<span data-ttu-id="6ae71-374">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-374">string</span></span>|<span data-ttu-id="6ae71-375">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-375">Yes</span></span>|<span data-ttu-id="6ae71-376">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="6ae71-376">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-377">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-377">Response</span></span>  

<span data-ttu-id="6ae71-378">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-378">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-379">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-379">Key</span></span>|<span data-ttu-id="6ae71-380">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-380">Value Type</span></span>|<span data-ttu-id="6ae71-381">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-381">Required</span></span>|<span data-ttu-id="6ae71-382">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-382">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-383">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-383">statusCode</span></span>|<span data-ttu-id="6ae71-384">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-384">int</span></span>|<span data-ttu-id="6ae71-385">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-385">Yes</span></span>|<span data-ttu-id="6ae71-386">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-386">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-387">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="6ae71-387">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="6ae71-388">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="6ae71-388">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="6ae71-389">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-389">statusDescription</span></span>|<span data-ttu-id="6ae71-390">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-390">string</span></span>|<span data-ttu-id="6ae71-391">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-391">No</span></span>|<span data-ttu-id="6ae71-392">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-392">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-393">응답 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-393">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-394">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-394">Key</span></span>|<span data-ttu-id="6ae71-395">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-395">Value Type</span></span>|<span data-ttu-id="6ae71-396">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-396">Required</span></span>|<span data-ttu-id="6ae71-397">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-397">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-398">expiration</span><span class="sxs-lookup"><span data-stu-id="6ae71-398">expiration</span></span>|<span data-ttu-id="6ae71-399">timestamp</span><span class="sxs-lookup"><span data-stu-id="6ae71-399">timestamp</span></span>|<span data-ttu-id="6ae71-400">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-400">Yes</span></span>|<span data-ttu-id="6ae71-401">새 만료.</span><span class="sxs-lookup"><span data-stu-id="6ae71-401">New expiration.</span></span>|  
  
### <a name="peek-session-message"></a><span data-ttu-id="6ae71-402">세션 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="6ae71-402">Peek Session Message</span></span>  

<span data-ttu-id="6ae71-403">잠그지 않고 세션 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-403">Peeks session messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-404">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-404">Request</span></span>  

<span data-ttu-id="6ae71-405">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-405">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-406">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-406">Key</span></span>|<span data-ttu-id="6ae71-407">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-407">Value Type</span></span>|<span data-ttu-id="6ae71-408">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-408">Required</span></span>|<span data-ttu-id="6ae71-409">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-409">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-410">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-410">operation</span></span>|<span data-ttu-id="6ae71-411">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-411">string</span></span>|<span data-ttu-id="6ae71-412">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-412">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-413">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-413">uint</span></span>|<span data-ttu-id="6ae71-414">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-414">No</span></span>|<span data-ttu-id="6ae71-415">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-415">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-416">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-416">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-417">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-417">Key</span></span>|<span data-ttu-id="6ae71-418">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-418">Value Type</span></span>|<span data-ttu-id="6ae71-419">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-419">Required</span></span>|<span data-ttu-id="6ae71-420">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-420">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-421">from-sequence-number</span><span class="sxs-lookup"><span data-stu-id="6ae71-421">from-sequence-number</span></span>|<span data-ttu-id="6ae71-422">long</span><span class="sxs-lookup"><span data-stu-id="6ae71-422">long</span></span>|<span data-ttu-id="6ae71-423">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-423">Yes</span></span>|<span data-ttu-id="6ae71-424">보기를 시작할 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-424">Sequence number from which to start peek.</span></span>|  
|<span data-ttu-id="6ae71-425">message-count</span><span class="sxs-lookup"><span data-stu-id="6ae71-425">message-count</span></span>|<span data-ttu-id="6ae71-426">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-426">int</span></span>|<span data-ttu-id="6ae71-427">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-427">Yes</span></span>|<span data-ttu-id="6ae71-428">보려는 최대 메시지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-428">Maximum number of messages to peek.</span></span>|  
|<span data-ttu-id="6ae71-429">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-429">session-id</span></span>|<span data-ttu-id="6ae71-430">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-430">string</span></span>|<span data-ttu-id="6ae71-431">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-431">Yes</span></span>|<span data-ttu-id="6ae71-432">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="6ae71-432">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-433">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-433">Response</span></span>  

<span data-ttu-id="6ae71-434">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-434">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-435">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-435">Key</span></span>|<span data-ttu-id="6ae71-436">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-436">Value Type</span></span>|<span data-ttu-id="6ae71-437">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-437">Required</span></span>|<span data-ttu-id="6ae71-438">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-438">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-439">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-439">statusCode</span></span>|<span data-ttu-id="6ae71-440">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-440">int</span></span>|<span data-ttu-id="6ae71-441">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-441">Yes</span></span>|<span data-ttu-id="6ae71-442">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-442">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-443">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="6ae71-443">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="6ae71-444">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="6ae71-444">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="6ae71-445">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-445">statusDescription</span></span>|<span data-ttu-id="6ae71-446">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-446">string</span></span>|<span data-ttu-id="6ae71-447">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-447">No</span></span>|<span data-ttu-id="6ae71-448">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-448">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-449">응답 메시지 본문은 다음 엔터티와 함께 맵을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-449">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-450">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-450">Key</span></span>|<span data-ttu-id="6ae71-451">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-451">Value Type</span></span>|<span data-ttu-id="6ae71-452">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-452">Required</span></span>|<span data-ttu-id="6ae71-453">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-453">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-454">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="6ae71-454">messages</span></span>|<span data-ttu-id="6ae71-455">맵 목록</span><span class="sxs-lookup"><span data-stu-id="6ae71-455">list of maps</span></span>|<span data-ttu-id="6ae71-456">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-456">Yes</span></span>|<span data-ttu-id="6ae71-457">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-457">List of messages in which every map represents a message.</span></span>|  
  
 <span data-ttu-id="6ae71-458">메시지를 나타내는 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-458">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-459">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-459">Key</span></span>|<span data-ttu-id="6ae71-460">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-460">Value Type</span></span>|<span data-ttu-id="6ae71-461">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-461">Required</span></span>|<span data-ttu-id="6ae71-462">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-462">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-463">message</span><span class="sxs-lookup"><span data-stu-id="6ae71-463">message</span></span>|<span data-ttu-id="6ae71-464">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-464">array of byte</span></span>|<span data-ttu-id="6ae71-465">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-465">Yes</span></span>|<span data-ttu-id="6ae71-466">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-466">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="set-session-state"></a><span data-ttu-id="6ae71-467">세션 상태 설정</span><span class="sxs-lookup"><span data-stu-id="6ae71-467">Set Session State</span></span>  

<span data-ttu-id="6ae71-468">세션 상태를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-468">Sets the state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-469">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-469">Request</span></span>  

<span data-ttu-id="6ae71-470">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-470">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-471">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-471">Key</span></span>|<span data-ttu-id="6ae71-472">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-472">Value Type</span></span>|<span data-ttu-id="6ae71-473">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-473">Required</span></span>|<span data-ttu-id="6ae71-474">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-474">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-475">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-475">operation</span></span>|<span data-ttu-id="6ae71-476">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-476">string</span></span>|<span data-ttu-id="6ae71-477">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-477">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-478">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-478">uint</span></span>|<span data-ttu-id="6ae71-479">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-479">No</span></span>|<span data-ttu-id="6ae71-480">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-480">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-481">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-481">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-482">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-482">Key</span></span>|<span data-ttu-id="6ae71-483">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-483">Value Type</span></span>|<span data-ttu-id="6ae71-484">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-484">Required</span></span>|<span data-ttu-id="6ae71-485">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-485">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-486">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-486">session-id</span></span>|<span data-ttu-id="6ae71-487">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-487">string</span></span>|<span data-ttu-id="6ae71-488">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-488">Yes</span></span>|<span data-ttu-id="6ae71-489">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="6ae71-489">Session ID.</span></span>|  
|<span data-ttu-id="6ae71-490">session-state</span><span class="sxs-lookup"><span data-stu-id="6ae71-490">session-state</span></span>|<span data-ttu-id="6ae71-491">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-491">array of bytes</span></span>|<span data-ttu-id="6ae71-492">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-492">Yes</span></span>|<span data-ttu-id="6ae71-493">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="6ae71-493">Opaque binary data.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-494">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-494">Response</span></span>  

<span data-ttu-id="6ae71-495">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-495">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-496">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-496">Key</span></span>|<span data-ttu-id="6ae71-497">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-497">Value Type</span></span>|<span data-ttu-id="6ae71-498">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-498">Required</span></span>|<span data-ttu-id="6ae71-499">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-499">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-500">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-500">statusCode</span></span>|<span data-ttu-id="6ae71-501">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-501">int</span></span>|<span data-ttu-id="6ae71-502">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-502">Yes</span></span>|<span data-ttu-id="6ae71-503">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-503">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-504">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-504">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-505">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-505">statusDescription</span></span>|<span data-ttu-id="6ae71-506">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-506">string</span></span>|<span data-ttu-id="6ae71-507">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-507">No</span></span>|<span data-ttu-id="6ae71-508">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-508">Description of the status.</span></span>|  
  
### <a name="get-session-state"></a><span data-ttu-id="6ae71-509">세션 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="6ae71-509">Get Session State</span></span>  

<span data-ttu-id="6ae71-510">세션 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-510">Gets the state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-511">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-511">Request</span></span>  

<span data-ttu-id="6ae71-512">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-512">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-513">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-513">Key</span></span>|<span data-ttu-id="6ae71-514">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-514">Value Type</span></span>|<span data-ttu-id="6ae71-515">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-515">Required</span></span>|<span data-ttu-id="6ae71-516">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-516">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-517">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-517">operation</span></span>|<span data-ttu-id="6ae71-518">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-518">string</span></span>|<span data-ttu-id="6ae71-519">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-519">Yes</span></span>|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-520">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-520">uint</span></span>|<span data-ttu-id="6ae71-521">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-521">No</span></span>|<span data-ttu-id="6ae71-522">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-522">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-523">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-523">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-524">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-524">Key</span></span>|<span data-ttu-id="6ae71-525">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-525">Value Type</span></span>|<span data-ttu-id="6ae71-526">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-526">Required</span></span>|<span data-ttu-id="6ae71-527">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-527">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-528">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-528">session-id</span></span>|<span data-ttu-id="6ae71-529">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-529">string</span></span>|<span data-ttu-id="6ae71-530">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-530">Yes</span></span>|<span data-ttu-id="6ae71-531">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="6ae71-531">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-532">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-532">Response</span></span>  

<span data-ttu-id="6ae71-533">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-533">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-534">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-534">Key</span></span>|<span data-ttu-id="6ae71-535">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-535">Value Type</span></span>|<span data-ttu-id="6ae71-536">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-536">Required</span></span>|<span data-ttu-id="6ae71-537">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-537">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-538">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-538">statusCode</span></span>|<span data-ttu-id="6ae71-539">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-539">int</span></span>|<span data-ttu-id="6ae71-540">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-540">Yes</span></span>|<span data-ttu-id="6ae71-541">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-541">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-542">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-542">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-543">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-543">statusDescription</span></span>|<span data-ttu-id="6ae71-544">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-544">string</span></span>|<span data-ttu-id="6ae71-545">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-545">No</span></span>|<span data-ttu-id="6ae71-546">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-546">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-547">응답 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-547">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-548">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-548">Key</span></span>|<span data-ttu-id="6ae71-549">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-549">Value Type</span></span>|<span data-ttu-id="6ae71-550">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-550">Required</span></span>|<span data-ttu-id="6ae71-551">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-551">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-552">session-state</span><span class="sxs-lookup"><span data-stu-id="6ae71-552">session-state</span></span>|<span data-ttu-id="6ae71-553">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-553">array of bytes</span></span>|<span data-ttu-id="6ae71-554">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-554">Yes</span></span>|<span data-ttu-id="6ae71-555">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="6ae71-555">Opaque binary data.</span></span>|  
  
### <a name="enumerate-sessions"></a><span data-ttu-id="6ae71-556">세션 열거</span><span class="sxs-lookup"><span data-stu-id="6ae71-556">Enumerate Sessions</span></span>  

<span data-ttu-id="6ae71-557">메시지 엔터티에서 세션을 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-557">Enumerates sessions on a messaging entity.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-558">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-558">Request</span></span>  

<span data-ttu-id="6ae71-559">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-559">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-560">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-560">Key</span></span>|<span data-ttu-id="6ae71-561">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-561">Value Type</span></span>|<span data-ttu-id="6ae71-562">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-562">Required</span></span>|<span data-ttu-id="6ae71-563">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-563">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-564">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-564">operation</span></span>|<span data-ttu-id="6ae71-565">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-565">string</span></span>|<span data-ttu-id="6ae71-566">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-566">Yes</span></span>|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-567">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-567">uint</span></span>|<span data-ttu-id="6ae71-568">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-568">No</span></span>|<span data-ttu-id="6ae71-569">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-569">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-570">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-570">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-571">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-571">Key</span></span>|<span data-ttu-id="6ae71-572">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-572">Value Type</span></span>|<span data-ttu-id="6ae71-573">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-573">Required</span></span>|<span data-ttu-id="6ae71-574">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-574">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-575">last-updated-time</span><span class="sxs-lookup"><span data-stu-id="6ae71-575">last-updated-time</span></span>|<span data-ttu-id="6ae71-576">timestamp</span><span class="sxs-lookup"><span data-stu-id="6ae71-576">timestamp</span></span>|<span data-ttu-id="6ae71-577">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-577">Yes</span></span>|<span data-ttu-id="6ae71-578">지정된 시간 이후 업데이트된 세션만 포함하도록 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-578">Filter to include only sessions updated after a given time.</span></span>|  
|<span data-ttu-id="6ae71-579">skip</span><span class="sxs-lookup"><span data-stu-id="6ae71-579">skip</span></span>|<span data-ttu-id="6ae71-580">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-580">int</span></span>|<span data-ttu-id="6ae71-581">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-581">Yes</span></span>|<span data-ttu-id="6ae71-582">세션 수를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-582">Skip a number of sessions.</span></span>|  
|<span data-ttu-id="6ae71-583">top</span><span class="sxs-lookup"><span data-stu-id="6ae71-583">top</span></span>|<span data-ttu-id="6ae71-584">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-584">int</span></span>|<span data-ttu-id="6ae71-585">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-585">Yes</span></span>|<span data-ttu-id="6ae71-586">최대 세션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-586">Maximum number of sessions.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-587">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-587">Response</span></span>  

<span data-ttu-id="6ae71-588">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-588">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-589">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-589">Key</span></span>|<span data-ttu-id="6ae71-590">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-590">Value Type</span></span>|<span data-ttu-id="6ae71-591">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-591">Required</span></span>|<span data-ttu-id="6ae71-592">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-592">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-593">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-593">statusCode</span></span>|<span data-ttu-id="6ae71-594">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-594">int</span></span>|<span data-ttu-id="6ae71-595">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-595">Yes</span></span>|<span data-ttu-id="6ae71-596">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-596">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-597">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="6ae71-597">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="6ae71-598">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="6ae71-598">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="6ae71-599">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-599">statusDescription</span></span>|<span data-ttu-id="6ae71-600">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-600">string</span></span>|<span data-ttu-id="6ae71-601">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-601">No</span></span>|<span data-ttu-id="6ae71-602">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-602">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-603">응답 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-603">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-604">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-604">Key</span></span>|<span data-ttu-id="6ae71-605">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-605">Value Type</span></span>|<span data-ttu-id="6ae71-606">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-606">Required</span></span>|<span data-ttu-id="6ae71-607">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-607">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-608">skip</span><span class="sxs-lookup"><span data-stu-id="6ae71-608">skip</span></span>|<span data-ttu-id="6ae71-609">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-609">int</span></span>|<span data-ttu-id="6ae71-610">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-610">Yes</span></span>|<span data-ttu-id="6ae71-611">상태 코드가 200인 경우 건너뛴 세션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-611">Number of skipped sessions if status code is 200.</span></span>|  
|<span data-ttu-id="6ae71-612">sessions-ids</span><span class="sxs-lookup"><span data-stu-id="6ae71-612">sessions-ids</span></span>|<span data-ttu-id="6ae71-613">문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-613">array of strings</span></span>|<span data-ttu-id="6ae71-614">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-614">Yes</span></span>|<span data-ttu-id="6ae71-615">상태 코드가 200인 경우 세션 ID 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-615">Array of session IDs if status code is 200.</span></span>|  
  
## <a name="rule-operations"></a><span data-ttu-id="6ae71-616">규칙 작업</span><span class="sxs-lookup"><span data-stu-id="6ae71-616">Rule operations</span></span>  
  
### <a name="add-rule"></a><span data-ttu-id="6ae71-617">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="6ae71-617">Add Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-618">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-618">Request</span></span>  

<span data-ttu-id="6ae71-619">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-619">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-620">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-620">Key</span></span>|<span data-ttu-id="6ae71-621">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-621">Value Type</span></span>|<span data-ttu-id="6ae71-622">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-622">Required</span></span>|<span data-ttu-id="6ae71-623">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-623">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-624">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-624">operation</span></span>|<span data-ttu-id="6ae71-625">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-625">string</span></span>|<span data-ttu-id="6ae71-626">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-626">Yes</span></span>|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-627">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-627">uint</span></span>|<span data-ttu-id="6ae71-628">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-628">No</span></span>|<span data-ttu-id="6ae71-629">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-629">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-630">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-630">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-631">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-631">Key</span></span>|<span data-ttu-id="6ae71-632">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-632">Value Type</span></span>|<span data-ttu-id="6ae71-633">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-633">Required</span></span>|<span data-ttu-id="6ae71-634">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-634">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-635">rule-name</span><span class="sxs-lookup"><span data-stu-id="6ae71-635">rule-name</span></span>|<span data-ttu-id="6ae71-636">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-636">string</span></span>|<span data-ttu-id="6ae71-637">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-637">Yes</span></span>|<span data-ttu-id="6ae71-638">구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-638">Rule name, not including subscription and topic names.</span></span>|  
|<span data-ttu-id="6ae71-639">rule-description</span><span class="sxs-lookup"><span data-stu-id="6ae71-639">rule-description</span></span>|<span data-ttu-id="6ae71-640">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-640">map</span></span>|<span data-ttu-id="6ae71-641">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-641">Yes</span></span>|<span data-ttu-id="6ae71-642">다음 섹션에 지정된 대로 규칙 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-642">Rule description as specified in next section.</span></span>|  
  
<span data-ttu-id="6ae71-643">**rule-description** 맵은 다음 엔터티를 포함해야 합니다. 여기서 **sql-filter** 및 **correlation-filter**는 상호 배타적입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-643">The **rule-description** map must include the following entries, where **sql-filter** and **correlation-filter** are mutually exclusive:</span></span>  
  
|<span data-ttu-id="6ae71-644">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-644">Key</span></span>|<span data-ttu-id="6ae71-645">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-645">Value Type</span></span>|<span data-ttu-id="6ae71-646">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-646">Required</span></span>|<span data-ttu-id="6ae71-647">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-647">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-648">sql-filter</span><span class="sxs-lookup"><span data-stu-id="6ae71-648">sql-filter</span></span>|<span data-ttu-id="6ae71-649">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-649">map</span></span>|<span data-ttu-id="6ae71-650">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-650">Yes</span></span>|<span data-ttu-id="6ae71-651">다음 섹션에 지정된 대로 `sql-filter`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-651">`sql-filter`, as specified in the next section.</span></span>|  
|<span data-ttu-id="6ae71-652">correlation-filter</span><span class="sxs-lookup"><span data-stu-id="6ae71-652">correlation-filter</span></span>|<span data-ttu-id="6ae71-653">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-653">map</span></span>|<span data-ttu-id="6ae71-654">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-654">Yes</span></span>|<span data-ttu-id="6ae71-655">다음 섹션에 지정된 대로 `correlation-filter`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-655">`correlation-filter`, as specified in the next section.</span></span>|  
|<span data-ttu-id="6ae71-656">sql-rule-action</span><span class="sxs-lookup"><span data-stu-id="6ae71-656">sql-rule-action</span></span>|<span data-ttu-id="6ae71-657">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-657">map</span></span>|<span data-ttu-id="6ae71-658">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-658">Yes</span></span>|<span data-ttu-id="6ae71-659">다음 섹션에 지정된 대로 `sql-rule-action`입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-659">`sql-rule-action`, as specified in the next section.</span></span>|  
  
<span data-ttu-id="6ae71-660">sql-filter 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-660">The sql-filter map must include the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-661">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-661">Key</span></span>|<span data-ttu-id="6ae71-662">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-662">Value Type</span></span>|<span data-ttu-id="6ae71-663">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-663">Required</span></span>|<span data-ttu-id="6ae71-664">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-664">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-665">식</span><span class="sxs-lookup"><span data-stu-id="6ae71-665">expression</span></span>|<span data-ttu-id="6ae71-666">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-666">string</span></span>|<span data-ttu-id="6ae71-667">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-667">Yes</span></span>|<span data-ttu-id="6ae71-668">Sql 필터 식.</span><span class="sxs-lookup"><span data-stu-id="6ae71-668">Sql filter expression.</span></span>|  
  
<span data-ttu-id="6ae71-669">**correlation-filter** 맵은 다음 항목을 하나 이상 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-669">The **correlation-filter** map must include at least one of the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-670">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-670">Key</span></span>|<span data-ttu-id="6ae71-671">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-671">Value Type</span></span>|<span data-ttu-id="6ae71-672">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-672">Required</span></span>|<span data-ttu-id="6ae71-673">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-673">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-674">correlation-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-674">correlation-id</span></span>|<span data-ttu-id="6ae71-675">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-675">string</span></span>|<span data-ttu-id="6ae71-676">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-676">No</span></span>||  
|<span data-ttu-id="6ae71-677">message-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-677">message-id</span></span>|<span data-ttu-id="6ae71-678">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-678">string</span></span>|<span data-ttu-id="6ae71-679">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-679">No</span></span>||  
|<span data-ttu-id="6ae71-680">to</span><span class="sxs-lookup"><span data-stu-id="6ae71-680">to</span></span>|<span data-ttu-id="6ae71-681">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-681">string</span></span>|<span data-ttu-id="6ae71-682">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-682">No</span></span>||  
|<span data-ttu-id="6ae71-683">reply-to</span><span class="sxs-lookup"><span data-stu-id="6ae71-683">reply-to</span></span>|<span data-ttu-id="6ae71-684">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-684">string</span></span>|<span data-ttu-id="6ae71-685">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-685">No</span></span>||  
|<span data-ttu-id="6ae71-686">label</span><span class="sxs-lookup"><span data-stu-id="6ae71-686">label</span></span>|<span data-ttu-id="6ae71-687">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-687">string</span></span>|<span data-ttu-id="6ae71-688">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-688">No</span></span>||  
|<span data-ttu-id="6ae71-689">session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-689">session-id</span></span>|<span data-ttu-id="6ae71-690">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-690">string</span></span>|<span data-ttu-id="6ae71-691">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-691">No</span></span>||  
|<span data-ttu-id="6ae71-692">reply-to-session-id</span><span class="sxs-lookup"><span data-stu-id="6ae71-692">reply-to-session-id</span></span>|<span data-ttu-id="6ae71-693">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-693">string</span></span>|<span data-ttu-id="6ae71-694">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-694">No</span></span>||  
|<span data-ttu-id="6ae71-695">content-type</span><span class="sxs-lookup"><span data-stu-id="6ae71-695">content-type</span></span>|<span data-ttu-id="6ae71-696">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-696">string</span></span>|<span data-ttu-id="6ae71-697">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-697">No</span></span>||  
|<span data-ttu-id="6ae71-698">properties</span><span class="sxs-lookup"><span data-stu-id="6ae71-698">properties</span></span>|<span data-ttu-id="6ae71-699">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-699">map</span></span>|<span data-ttu-id="6ae71-700">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-700">No</span></span>|<span data-ttu-id="6ae71-701">Service Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-701">Maps to Service Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).</span></span>|  
  
<span data-ttu-id="6ae71-702">**sql-rule-action** 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-702">The **sql-rule-action** map must include the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-703">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-703">Key</span></span>|<span data-ttu-id="6ae71-704">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-704">Value Type</span></span>|<span data-ttu-id="6ae71-705">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-705">Required</span></span>|<span data-ttu-id="6ae71-706">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-706">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-707">식</span><span class="sxs-lookup"><span data-stu-id="6ae71-707">expression</span></span>|<span data-ttu-id="6ae71-708">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-708">string</span></span>|<span data-ttu-id="6ae71-709">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-709">Yes</span></span>|<span data-ttu-id="6ae71-710">Sql 작업 식.</span><span class="sxs-lookup"><span data-stu-id="6ae71-710">Sql action expression.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-711">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-711">Response</span></span>  

<span data-ttu-id="6ae71-712">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-712">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-713">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-713">Key</span></span>|<span data-ttu-id="6ae71-714">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-714">Value Type</span></span>|<span data-ttu-id="6ae71-715">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-715">Required</span></span>|<span data-ttu-id="6ae71-716">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-716">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-717">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-717">statusCode</span></span>|<span data-ttu-id="6ae71-718">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-718">int</span></span>|<span data-ttu-id="6ae71-719">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-719">Yes</span></span>|<span data-ttu-id="6ae71-720">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-720">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-721">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-721">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-722">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-722">statusDescription</span></span>|<span data-ttu-id="6ae71-723">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-723">string</span></span>|<span data-ttu-id="6ae71-724">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-724">No</span></span>|<span data-ttu-id="6ae71-725">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-725">Description of the status.</span></span>|  
  
### <a name="remove-rule"></a><span data-ttu-id="6ae71-726">규칙 제거</span><span class="sxs-lookup"><span data-stu-id="6ae71-726">Remove Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-727">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-727">Request</span></span>  

<span data-ttu-id="6ae71-728">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-728">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-729">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-729">Key</span></span>|<span data-ttu-id="6ae71-730">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-730">Value Type</span></span>|<span data-ttu-id="6ae71-731">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-731">Required</span></span>|<span data-ttu-id="6ae71-732">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-732">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-733">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-733">operation</span></span>|<span data-ttu-id="6ae71-734">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-734">string</span></span>|<span data-ttu-id="6ae71-735">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-735">Yes</span></span>|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-736">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-736">uint</span></span>|<span data-ttu-id="6ae71-737">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-737">No</span></span>|<span data-ttu-id="6ae71-738">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-738">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-739">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-739">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-740">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-740">Key</span></span>|<span data-ttu-id="6ae71-741">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-741">Value Type</span></span>|<span data-ttu-id="6ae71-742">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-742">Required</span></span>|<span data-ttu-id="6ae71-743">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-743">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-744">rule-name</span><span class="sxs-lookup"><span data-stu-id="6ae71-744">rule-name</span></span>|<span data-ttu-id="6ae71-745">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-745">string</span></span>|<span data-ttu-id="6ae71-746">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-746">Yes</span></span>|<span data-ttu-id="6ae71-747">구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-747">Rule name, not including subscription and topic names.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-748">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-748">Response</span></span>  

<span data-ttu-id="6ae71-749">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-749">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-750">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-750">Key</span></span>|<span data-ttu-id="6ae71-751">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-751">Value Type</span></span>|<span data-ttu-id="6ae71-752">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-752">Required</span></span>|<span data-ttu-id="6ae71-753">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-753">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-754">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-754">statusCode</span></span>|<span data-ttu-id="6ae71-755">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-755">int</span></span>|<span data-ttu-id="6ae71-756">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-756">Yes</span></span>|<span data-ttu-id="6ae71-757">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-757">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-758">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-758">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-759">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-759">statusDescription</span></span>|<span data-ttu-id="6ae71-760">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-760">string</span></span>|<span data-ttu-id="6ae71-761">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-761">No</span></span>|<span data-ttu-id="6ae71-762">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-762">Description of the status.</span></span>|  
  
## <a name="deferred-message-operations"></a><span data-ttu-id="6ae71-763">지연된 메시지 작업</span><span class="sxs-lookup"><span data-stu-id="6ae71-763">Deferred message operations</span></span>  
  
### <a name="receive-by-sequence-number"></a><span data-ttu-id="6ae71-764">시퀀스 번호로 받기</span><span class="sxs-lookup"><span data-stu-id="6ae71-764">Receive by sequence number</span></span>  

<span data-ttu-id="6ae71-765">시퀀스 번호로 지연된 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-765">Receives deferred messages by sequence number.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-766">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-766">Request</span></span>  

<span data-ttu-id="6ae71-767">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-767">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-768">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-768">Key</span></span>|<span data-ttu-id="6ae71-769">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-769">Value Type</span></span>|<span data-ttu-id="6ae71-770">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-770">Required</span></span>|<span data-ttu-id="6ae71-771">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-771">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-772">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-772">operation</span></span>|<span data-ttu-id="6ae71-773">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-773">string</span></span>|<span data-ttu-id="6ae71-774">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-774">Yes</span></span>|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-775">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-775">uint</span></span>|<span data-ttu-id="6ae71-776">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-776">No</span></span>|<span data-ttu-id="6ae71-777">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-777">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-778">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-778">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-779">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-779">Key</span></span>|<span data-ttu-id="6ae71-780">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-780">Value Type</span></span>|<span data-ttu-id="6ae71-781">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-781">Required</span></span>|<span data-ttu-id="6ae71-782">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-782">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-783">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="6ae71-783">sequence-numbers</span></span>|<span data-ttu-id="6ae71-784">long 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-784">array of long</span></span>|<span data-ttu-id="6ae71-785">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-785">Yes</span></span>|<span data-ttu-id="6ae71-786">시퀀스 번호.</span><span class="sxs-lookup"><span data-stu-id="6ae71-786">Sequence numbers.</span></span>|  
|<span data-ttu-id="6ae71-787">receiver-settle-mode</span><span class="sxs-lookup"><span data-stu-id="6ae71-787">receiver-settle-mode</span></span>|<span data-ttu-id="6ae71-788">ubyte</span><span class="sxs-lookup"><span data-stu-id="6ae71-788">ubyte</span></span>|<span data-ttu-id="6ae71-789">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-789">Yes</span></span>|<span data-ttu-id="6ae71-790">AMQP 코어 v1.0에 지정된 대로 **수신기 장착** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-790">**Receiver settle** mode as specified in AMQP core v1.0.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-791">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-791">Response</span></span>  

<span data-ttu-id="6ae71-792">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-792">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-793">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-793">Key</span></span>|<span data-ttu-id="6ae71-794">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-794">Value Type</span></span>|<span data-ttu-id="6ae71-795">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-795">Required</span></span>|<span data-ttu-id="6ae71-796">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-796">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-797">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-797">statusCode</span></span>|<span data-ttu-id="6ae71-798">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-798">int</span></span>|<span data-ttu-id="6ae71-799">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-799">Yes</span></span>|<span data-ttu-id="6ae71-800">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-800">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-801">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-801">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-802">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-802">statusDescription</span></span>|<span data-ttu-id="6ae71-803">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-803">string</span></span>|<span data-ttu-id="6ae71-804">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-804">No</span></span>|<span data-ttu-id="6ae71-805">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-805">Description of the status.</span></span>|  
  
<span data-ttu-id="6ae71-806">응답 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-806">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-807">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-807">Key</span></span>|<span data-ttu-id="6ae71-808">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-808">Value Type</span></span>|<span data-ttu-id="6ae71-809">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-809">Required</span></span>|<span data-ttu-id="6ae71-810">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-810">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-811">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="6ae71-811">messages</span></span>|<span data-ttu-id="6ae71-812">맵 목록</span><span class="sxs-lookup"><span data-stu-id="6ae71-812">list of maps</span></span>|<span data-ttu-id="6ae71-813">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-813">Yes</span></span>|<span data-ttu-id="6ae71-814">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-814">List of messages where every map represents a message.</span></span>|  
  
<span data-ttu-id="6ae71-815">메시지를 나타내는 맵은 다음 항목을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-815">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-816">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-816">Key</span></span>|<span data-ttu-id="6ae71-817">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-817">Value Type</span></span>|<span data-ttu-id="6ae71-818">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-818">Required</span></span>|<span data-ttu-id="6ae71-819">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-819">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-820">lock-token</span><span class="sxs-lookup"><span data-stu-id="6ae71-820">lock-token</span></span>|<span data-ttu-id="6ae71-821">uuid</span><span class="sxs-lookup"><span data-stu-id="6ae71-821">uuid</span></span>|<span data-ttu-id="6ae71-822">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-822">Yes</span></span>|<span data-ttu-id="6ae71-823">`receiver-settle-mode`가 1인 경우 토큰을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-823">Lock token if `receiver-settle-mode` is 1.</span></span>|  
|<span data-ttu-id="6ae71-824">message</span><span class="sxs-lookup"><span data-stu-id="6ae71-824">message</span></span>|<span data-ttu-id="6ae71-825">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-825">array of byte</span></span>|<span data-ttu-id="6ae71-826">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-826">Yes</span></span>|<span data-ttu-id="6ae71-827">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-827">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="update-disposition-status"></a><span data-ttu-id="6ae71-828">처리 상태 업데이트</span><span class="sxs-lookup"><span data-stu-id="6ae71-828">Update disposition status</span></span>  

<span data-ttu-id="6ae71-829">지연된 메시지의 처리 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-829">Updates the disposition status of deferred messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="6ae71-830">요청</span><span class="sxs-lookup"><span data-stu-id="6ae71-830">Request</span></span>  

<span data-ttu-id="6ae71-831">요청 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-831">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-832">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-832">Key</span></span>|<span data-ttu-id="6ae71-833">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-833">Value Type</span></span>|<span data-ttu-id="6ae71-834">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-834">Required</span></span>|<span data-ttu-id="6ae71-835">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-835">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-836">operation</span><span class="sxs-lookup"><span data-stu-id="6ae71-836">operation</span></span>|<span data-ttu-id="6ae71-837">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-837">string</span></span>|<span data-ttu-id="6ae71-838">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-838">Yes</span></span>|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="6ae71-839">uint</span><span class="sxs-lookup"><span data-stu-id="6ae71-839">uint</span></span>|<span data-ttu-id="6ae71-840">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-840">No</span></span>|<span data-ttu-id="6ae71-841">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-841">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="6ae71-842">요청 메시지 본문은 다음 엔터티와 함께 **맵**을 포함하는 **amqp-value** 섹션으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-842">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="6ae71-843">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-843">Key</span></span>|<span data-ttu-id="6ae71-844">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-844">Value Type</span></span>|<span data-ttu-id="6ae71-845">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-845">Required</span></span>|<span data-ttu-id="6ae71-846">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-846">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-847">disposition-status</span><span class="sxs-lookup"><span data-stu-id="6ae71-847">disposition-status</span></span>|<span data-ttu-id="6ae71-848">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-848">string</span></span>|<span data-ttu-id="6ae71-849">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-849">Yes</span></span>|<span data-ttu-id="6ae71-850">완료됨</span><span class="sxs-lookup"><span data-stu-id="6ae71-850">completed</span></span><br /><br /> <span data-ttu-id="6ae71-851">중단됨</span><span class="sxs-lookup"><span data-stu-id="6ae71-851">abandoned</span></span><br /><br /> <span data-ttu-id="6ae71-852">일시 중단됨</span><span class="sxs-lookup"><span data-stu-id="6ae71-852">suspended</span></span>|  
|<span data-ttu-id="6ae71-853">lock-tokens</span><span class="sxs-lookup"><span data-stu-id="6ae71-853">lock-tokens</span></span>|<span data-ttu-id="6ae71-854">uuid의 배열</span><span class="sxs-lookup"><span data-stu-id="6ae71-854">array of uuid</span></span>|<span data-ttu-id="6ae71-855">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-855">Yes</span></span>|<span data-ttu-id="6ae71-856">처리 상태를 업데이트할 메시지 잠금 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-856">Message lock tokens to update disposition status.</span></span>|  
|<span data-ttu-id="6ae71-857">deadletter-reason</span><span class="sxs-lookup"><span data-stu-id="6ae71-857">deadletter-reason</span></span>|<span data-ttu-id="6ae71-858">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-858">string</span></span>|<span data-ttu-id="6ae71-859">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-859">No</span></span>|<span data-ttu-id="6ae71-860">처리 상태가 **일시 중단됨**으로 설정된 경우 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-860">May be set if disposition status is set to **suspended**.</span></span>|  
|<span data-ttu-id="6ae71-861">deadletter-description</span><span class="sxs-lookup"><span data-stu-id="6ae71-861">deadletter-description</span></span>|<span data-ttu-id="6ae71-862">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-862">string</span></span>|<span data-ttu-id="6ae71-863">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-863">No</span></span>|<span data-ttu-id="6ae71-864">처리 상태가 **일시 중단됨**으로 설정된 경우 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-864">May be set if disposition status is set to **suspended**.</span></span>|  
|<span data-ttu-id="6ae71-865">properties-to-modify</span><span class="sxs-lookup"><span data-stu-id="6ae71-865">properties-to-modify</span></span>|<span data-ttu-id="6ae71-866">map</span><span class="sxs-lookup"><span data-stu-id="6ae71-866">map</span></span>|<span data-ttu-id="6ae71-867">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-867">No</span></span>|<span data-ttu-id="6ae71-868">수정할 Service Bus broker 저장 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-868">List of Service Bus brokered message properties to modify.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="6ae71-869">응답</span><span class="sxs-lookup"><span data-stu-id="6ae71-869">Response</span></span>  

<span data-ttu-id="6ae71-870">응답 메시지에는 다음과 같은 응용 프로그램 속성이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-870">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="6ae71-871">키</span><span class="sxs-lookup"><span data-stu-id="6ae71-871">Key</span></span>|<span data-ttu-id="6ae71-872">값 형식</span><span class="sxs-lookup"><span data-stu-id="6ae71-872">Value Type</span></span>|<span data-ttu-id="6ae71-873">필수</span><span class="sxs-lookup"><span data-stu-id="6ae71-873">Required</span></span>|<span data-ttu-id="6ae71-874">값 내용</span><span class="sxs-lookup"><span data-stu-id="6ae71-874">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="6ae71-875">statusCode</span><span class="sxs-lookup"><span data-stu-id="6ae71-875">statusCode</span></span>|<span data-ttu-id="6ae71-876">int</span><span class="sxs-lookup"><span data-stu-id="6ae71-876">int</span></span>|<span data-ttu-id="6ae71-877">예</span><span class="sxs-lookup"><span data-stu-id="6ae71-877">Yes</span></span>|<span data-ttu-id="6ae71-878">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="6ae71-878">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="6ae71-879">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-879">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="6ae71-880">statusDescription</span><span class="sxs-lookup"><span data-stu-id="6ae71-880">statusDescription</span></span>|<span data-ttu-id="6ae71-881">string</span><span class="sxs-lookup"><span data-stu-id="6ae71-881">string</span></span>|<span data-ttu-id="6ae71-882">아니요</span><span class="sxs-lookup"><span data-stu-id="6ae71-882">No</span></span>|<span data-ttu-id="6ae71-883">상태에 대한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="6ae71-883">Description of the status.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="6ae71-884">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6ae71-884">Next steps</span></span>

<span data-ttu-id="6ae71-885">AMQP 및 Service Bus에 대해 자세히 알아보려면 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="6ae71-885">To learn more about AMQP and Service Bus, visit the following links:</span></span>

* <span data-ttu-id="6ae71-886">[Service Bus AMQP 개요]</span><span class="sxs-lookup"><span data-stu-id="6ae71-886">[Service Bus AMQP overview]</span></span>
* <span data-ttu-id="6ae71-887">[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]</span><span class="sxs-lookup"><span data-stu-id="6ae71-887">[AMQP 1.0 support for Service Bus partitioned queues and topics]</span></span>
* <span data-ttu-id="6ae71-888">[Windows Server용 Service Bus의 AMQP]</span><span class="sxs-lookup"><span data-stu-id="6ae71-888">[AMQP in Service Bus for Windows Server]</span></span>

<span data-ttu-id="6ae71-889">[Service Bus AMQP 개요]: service-bus-amqp-overview.md</span><span class="sxs-lookup"><span data-stu-id="6ae71-889">[Service Bus AMQP overview]: service-bus-amqp-overview.md</span></span>
<span data-ttu-id="6ae71-890">[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md</span><span class="sxs-lookup"><span data-stu-id="6ae71-890">[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md</span></span>
<span data-ttu-id="6ae71-891">[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.asp</span><span class="sxs-lookup"><span data-stu-id="6ae71-891">[AMQP in Service Bus for Windows Server]: https://msdn.microsoft.com/library/dn574799.asp</span></span>