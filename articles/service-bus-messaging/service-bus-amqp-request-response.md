---
title: "Azure 서비스 버스 요청-응답 기반 작업에서 aaaAMQP 1.0 | Microsoft Docs"
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
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a><span data-ttu-id="e15ec-103">Microsoft Azure Service Bus에서 AMQP 1.0: Microsoft Azure Service Bus 요청/응답 기반 작업</span><span class="sxs-lookup"><span data-stu-id="e15ec-103">AMQP 1.0 in Microsoft Azure Service Bus: request-response-based operations</span></span>

<span data-ttu-id="e15ec-104">이 항목에는 Microsoft Azure 서비스 버스 요청/응답 기반 작업의 hello 목록을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-104">This topic defines hello list of Microsoft Azure Service Bus request/response-based operations.</span></span> <span data-ttu-id="e15ec-105">이 정보는 hello AMQP 관리 버전 1.0의 시행 중인 초안을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-105">This information is based on hello AMQP Management Version 1.0 working draft.</span></span>  
  
<span data-ttu-id="e15ec-106">자세한 지침을 보려면 유선 수준 AMQP 1.0 프로토콜, 서비스 버스를 구현 하 고 hello OASIS AMQP 기술 사양에 빌드하 하는 방법을 설명에 참조 hello [Azure 서비스 버스 및 이벤트 허브 프로토콜 가이드에서 AMQP 1.0](service-bus-amqp-protocol-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-106">For a detailed wire-level AMQP 1.0 protocol guide, which explains how Service Bus implements and builds on hello OASIS AMQP technical specification, see hello [AMQP 1.0 in Azure Service Bus and Event Hubs protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="concepts"></a><span data-ttu-id="e15ec-107">개념</span><span class="sxs-lookup"><span data-stu-id="e15ec-107">Concepts</span></span>  
  
### <a name="entity-description"></a><span data-ttu-id="e15ec-108">엔터티 설명</span><span class="sxs-lookup"><span data-stu-id="e15ec-108">Entity description</span></span>  

<span data-ttu-id="e15ec-109">엔터티 설명을 tooeither 서비스 버스 참조 [QueueDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.topicdescription), 또는 [SubscriptionDescription 클래스](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-109">An entity description refers tooeither a Service Bus [QueueDescription Class](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription Class](/dotnet/api/microsoft.servicebus.messaging.topicdescription), or [SubscriptionDescription Class](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) object.</span></span>  
  
### <a name="brokered-message"></a><span data-ttu-id="e15ec-110">broker 저장 메시지</span><span class="sxs-lookup"><span data-stu-id="e15ec-110">Brokered message</span></span>  

<span data-ttu-id="e15ec-111">서비스 버스를 매핑된 tooan AMQP 메시지에서 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-111">Represents a message in Service Bus, which is mapped tooan AMQP message.</span></span> <span data-ttu-id="e15ec-112">hello에 hello 매핑이 정의 되어 [서비스 버스 AMQP 프로토콜 가이드](service-bus-amqp-protocol-guide.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-112">hello mapping is defined in hello [Service Bus AMQP protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="attach-tooentity-management-node"></a><span data-ttu-id="e15ec-113">Tooentity 관리 노드를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-113">Attach tooentity management node</span></span>  

<span data-ttu-id="e15ec-114">이 문서에 설명 된 모든 hello 작업이 요청/응답 패턴을 따르는 범위가 지정 된 tooan 엔터티 되며 tooan 엔터티 관리 노드를 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-114">All hello operations described in this document follow a request/response pattern, are scoped tooan entity, and require attaching tooan entity management node.</span></span>  
  
### <a name="create-link-for-sending-requests"></a><span data-ttu-id="e15ec-115">요청 전송을 위한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="e15ec-115">Create link for sending requests</span></span>  

<span data-ttu-id="e15ec-116">요청을 보내기 위한 링크 toohello 관리 노드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-116">Creates a link toohello management node for sending requests.</span></span>  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a><span data-ttu-id="e15ec-117">응답 수신을 위한 링크 만들기</span><span class="sxs-lookup"><span data-stu-id="e15ec-117">Create link for receiving responses</span></span>  

<span data-ttu-id="e15ec-118">Hello 관리 노드에서 응답을 받기에 대 한 링크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-118">Creates a link for receiving responses from hello management node.</span></span>  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a><span data-ttu-id="e15ec-119">요청 메시지 전송</span><span class="sxs-lookup"><span data-stu-id="e15ec-119">Transfer a request message</span></span>  

<span data-ttu-id="e15ec-120">요청 메시지를 전송합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-120">Transfers a request message.</span></span>  
  
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
  
### <a name="receive-a-response-message"></a><span data-ttu-id="e15ec-121">응답 메시지 수신</span><span class="sxs-lookup"><span data-stu-id="e15ec-121">Receive a response message</span></span>  

<span data-ttu-id="e15ec-122">Hello 응답 링크에서 hello 응답 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-122">Receives hello response message from hello response link.</span></span>  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
<span data-ttu-id="e15ec-123">hello 응답 메시지는 다음 폼 hello에:</span><span class="sxs-lookup"><span data-stu-id="e15ec-123">hello response message is in hello following form:</span></span>
  
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
  
### <a name="service-bus-entity-address"></a><span data-ttu-id="e15ec-124">Service Bus 엔터티 주소</span><span class="sxs-lookup"><span data-stu-id="e15ec-124">Service Bus entity address</span></span>  

<span data-ttu-id="e15ec-125">Service Bus 엔터티 주소는 다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-125">Service Bus entities must be addressed as follows:</span></span>  
  
|<span data-ttu-id="e15ec-126">엔터티 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-126">Entity type</span></span>|<span data-ttu-id="e15ec-127">주소</span><span class="sxs-lookup"><span data-stu-id="e15ec-127">Address</span></span>|<span data-ttu-id="e15ec-128">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-128">Example</span></span>|  
|-----------------|-------------|-------------|  
|<span data-ttu-id="e15ec-129">큐</span><span class="sxs-lookup"><span data-stu-id="e15ec-129">queue</span></span>|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|<span data-ttu-id="e15ec-130">토픽</span><span class="sxs-lookup"><span data-stu-id="e15ec-130">topic</span></span>|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|<span data-ttu-id="e15ec-131">subscription</span><span class="sxs-lookup"><span data-stu-id="e15ec-131">subscription</span></span>|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a><span data-ttu-id="e15ec-132">메시지 작업</span><span class="sxs-lookup"><span data-stu-id="e15ec-132">Message operations</span></span>  
  
### <a name="message-renew-lock"></a><span data-ttu-id="e15ec-133">메시지 갱신 잠금</span><span class="sxs-lookup"><span data-stu-id="e15ec-133">Message Renew Lock</span></span>  

<span data-ttu-id="e15ec-134">Hello 시간별 hello 엔터티 설명에 지정 된 메시지의 잠금 hello를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-134">Extends hello lock of a message by hello time specified in hello entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-135">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-135">Request</span></span>  

<span data-ttu-id="e15ec-136">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-136">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-137">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-137">Key</span></span>|<span data-ttu-id="e15ec-138">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-138">Value Type</span></span>|<span data-ttu-id="e15ec-139">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-139">Required</span></span>|<span data-ttu-id="e15ec-140">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-140">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-141">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-141">operation</span></span>|<span data-ttu-id="e15ec-142">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-142">string</span></span>|<span data-ttu-id="e15ec-143">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-143">Yes</span></span>|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-144">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-144">uint</span></span>|<span data-ttu-id="e15ec-145">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-145">No</span></span>|<span data-ttu-id="e15ec-146">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-146">Operation server timeout in milliseconds.</span></span>|  
  
 <span data-ttu-id="e15ec-147">항목을 다음 hello로 맵을 포함 하는 amqp 값 섹션 hello 요청 메시지 본문 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-147">hello request message body must consist of an amqp-value section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-148">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-148">Key</span></span>|<span data-ttu-id="e15ec-149">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-149">Value Type</span></span>|<span data-ttu-id="e15ec-150">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-150">Required</span></span>|<span data-ttu-id="e15ec-151">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-151">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|<span data-ttu-id="e15ec-152">uuid의 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-152">array of uuid</span></span>|<span data-ttu-id="e15ec-153">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-153">Yes</span></span>|<span data-ttu-id="e15ec-154">메시지 잠금 토큰 toorenew 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-154">Message lock tokens toorenew.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-155">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-155">Response</span></span>  

<span data-ttu-id="e15ec-156">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-156">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-157">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-157">Key</span></span>|<span data-ttu-id="e15ec-158">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-158">Value Type</span></span>|<span data-ttu-id="e15ec-159">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-159">Required</span></span>|<span data-ttu-id="e15ec-160">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-160">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-161">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-161">statusCode</span></span>|<span data-ttu-id="e15ec-162">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-162">int</span></span>|<span data-ttu-id="e15ec-163">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-163">Yes</span></span>|<span data-ttu-id="e15ec-164">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-164">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-165">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-165">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="e15ec-166">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-166">statusDescription</span></span>|<span data-ttu-id="e15ec-167">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-167">string</span></span>|<span data-ttu-id="e15ec-168">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-168">No</span></span>|<span data-ttu-id="e15ec-169">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-169">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-170">항목을 다음 hello로 맵을 포함 하는 amqp 값 섹션 hello 응답 메시지 본문 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-170">hello response message body must consist of an amqp-value section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-171">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-171">Key</span></span>|<span data-ttu-id="e15ec-172">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-172">Value Type</span></span>|<span data-ttu-id="e15ec-173">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-173">Required</span></span>|<span data-ttu-id="e15ec-174">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-174">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-175">만료</span><span class="sxs-lookup"><span data-stu-id="e15ec-175">expirations</span></span>|<span data-ttu-id="e15ec-176">타임 스탬프 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-176">array of timestamp</span></span>|<span data-ttu-id="e15ec-177">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-177">Yes</span></span>|<span data-ttu-id="e15ec-178">메시지 잠금 토큰 새 만료 해당 toohello 요청 잠금 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-178">Message lock token new expiration corresponding toohello request lock tokens.</span></span>|  
  
### <a name="peek-message"></a><span data-ttu-id="e15ec-179">메시지 보기</span><span class="sxs-lookup"><span data-stu-id="e15ec-179">Peek Message</span></span>  

<span data-ttu-id="e15ec-180">잠그지 않고 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-180">Peeks messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-181">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-181">Request</span></span>  

<span data-ttu-id="e15ec-182">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-182">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-183">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-183">Key</span></span>|<span data-ttu-id="e15ec-184">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-184">Value Type</span></span>|<span data-ttu-id="e15ec-185">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-185">Required</span></span>|<span data-ttu-id="e15ec-186">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-186">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-187">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-187">operation</span></span>|<span data-ttu-id="e15ec-188">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-188">string</span></span>|<span data-ttu-id="e15ec-189">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-189">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-190">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-190">uint</span></span>|<span data-ttu-id="e15ec-191">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-191">No</span></span>|<span data-ttu-id="e15ec-192">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-192">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-193">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-193">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-194">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-194">Key</span></span>|<span data-ttu-id="e15ec-195">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-195">Value Type</span></span>|<span data-ttu-id="e15ec-196">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-196">Required</span></span>|<span data-ttu-id="e15ec-197">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-197">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|<span data-ttu-id="e15ec-198">long</span><span class="sxs-lookup"><span data-stu-id="e15ec-198">long</span></span>|<span data-ttu-id="e15ec-199">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-199">Yes</span></span>|<span data-ttu-id="e15ec-200">Toostart 피킹은에서 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-200">Sequence number from which toostart peek.</span></span>|  
|`message-count`|<span data-ttu-id="e15ec-201">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-201">int</span></span>|<span data-ttu-id="e15ec-202">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-202">Yes</span></span>|<span data-ttu-id="e15ec-203">메시지 toopeek의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-203">Maximum number of messages toopeek.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-204">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-204">Response</span></span>  

<span data-ttu-id="e15ec-205">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-205">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-206">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-206">Key</span></span>|<span data-ttu-id="e15ec-207">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-207">Value Type</span></span>|<span data-ttu-id="e15ec-208">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-208">Required</span></span>|<span data-ttu-id="e15ec-209">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-209">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-210">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-210">statusCode</span></span>|<span data-ttu-id="e15ec-211">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-211">int</span></span>|<span data-ttu-id="e15ec-212">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-212">Yes</span></span>|<span data-ttu-id="e15ec-213">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-213">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-214">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="e15ec-214">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="e15ec-215">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="e15ec-215">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="e15ec-216">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-216">statusDescription</span></span>|<span data-ttu-id="e15ec-217">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-217">string</span></span>|<span data-ttu-id="e15ec-218">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-218">No</span></span>|<span data-ttu-id="e15ec-219">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-219">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-220">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-220">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-221">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-221">Key</span></span>|<span data-ttu-id="e15ec-222">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-222">Value Type</span></span>|<span data-ttu-id="e15ec-223">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-223">Required</span></span>|<span data-ttu-id="e15ec-224">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-224">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-225">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="e15ec-225">messages</span></span>|<span data-ttu-id="e15ec-226">맵 목록</span><span class="sxs-lookup"><span data-stu-id="e15ec-226">list of maps</span></span>|<span data-ttu-id="e15ec-227">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-227">Yes</span></span>|<span data-ttu-id="e15ec-228">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-228">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="e15ec-229">메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-229">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-230">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-230">Key</span></span>|<span data-ttu-id="e15ec-231">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-231">Value Type</span></span>|<span data-ttu-id="e15ec-232">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-232">Required</span></span>|<span data-ttu-id="e15ec-233">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-233">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-234">message</span><span class="sxs-lookup"><span data-stu-id="e15ec-234">message</span></span>|<span data-ttu-id="e15ec-235">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-235">array of byte</span></span>|<span data-ttu-id="e15ec-236">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-236">Yes</span></span>|<span data-ttu-id="e15ec-237">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-237">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="schedule-message"></a><span data-ttu-id="e15ec-238">메시지 예약</span><span class="sxs-lookup"><span data-stu-id="e15ec-238">Schedule Message</span></span>  

<span data-ttu-id="e15ec-239">메시지를 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-239">Schedules messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-240">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-240">Request</span></span>  

<span data-ttu-id="e15ec-241">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-241">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-242">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-242">Key</span></span>|<span data-ttu-id="e15ec-243">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-243">Value Type</span></span>|<span data-ttu-id="e15ec-244">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-244">Required</span></span>|<span data-ttu-id="e15ec-245">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-245">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-246">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-246">operation</span></span>|<span data-ttu-id="e15ec-247">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-247">string</span></span>|<span data-ttu-id="e15ec-248">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-248">Yes</span></span>|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-249">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-249">uint</span></span>|<span data-ttu-id="e15ec-250">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-250">No</span></span>|<span data-ttu-id="e15ec-251">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-251">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-252">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-252">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-253">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-253">Key</span></span>|<span data-ttu-id="e15ec-254">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-254">Value Type</span></span>|<span data-ttu-id="e15ec-255">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-255">Required</span></span>|<span data-ttu-id="e15ec-256">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-256">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-257">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="e15ec-257">messages</span></span>|<span data-ttu-id="e15ec-258">맵 목록</span><span class="sxs-lookup"><span data-stu-id="e15ec-258">list of maps</span></span>|<span data-ttu-id="e15ec-259">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-259">Yes</span></span>|<span data-ttu-id="e15ec-260">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-260">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="e15ec-261">메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-261">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-262">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-262">Key</span></span>|<span data-ttu-id="e15ec-263">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-263">Value Type</span></span>|<span data-ttu-id="e15ec-264">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-264">Required</span></span>|<span data-ttu-id="e15ec-265">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-265">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-266">message-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-266">message-id</span></span>|<span data-ttu-id="e15ec-267">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-267">string</span></span>|<span data-ttu-id="e15ec-268">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-268">Yes</span></span>|<span data-ttu-id="e15ec-269">string으로 `amqpMessage.Properties.MessageId`</span><span class="sxs-lookup"><span data-stu-id="e15ec-269">`amqpMessage.Properties.MessageId` as string</span></span>|  
|<span data-ttu-id="e15ec-270">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-270">session-id</span></span>|<span data-ttu-id="e15ec-271">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-271">string</span></span>|<span data-ttu-id="e15ec-272">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-272">Yes</span></span>|`amqpMessage.Properties.GroupId as string`|  
|<span data-ttu-id="e15ec-273">파티션 키</span><span class="sxs-lookup"><span data-stu-id="e15ec-273">partition-key</span></span>|<span data-ttu-id="e15ec-274">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-274">string</span></span>|<span data-ttu-id="e15ec-275">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-275">Yes</span></span>|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|<span data-ttu-id="e15ec-276">message</span><span class="sxs-lookup"><span data-stu-id="e15ec-276">message</span></span>|<span data-ttu-id="e15ec-277">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-277">array of byte</span></span>|<span data-ttu-id="e15ec-278">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-278">Yes</span></span>|<span data-ttu-id="e15ec-279">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-279">AMQP 1.0 wire-encoded message.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-280">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-280">Response</span></span>  

<span data-ttu-id="e15ec-281">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-281">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-282">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-282">Key</span></span>|<span data-ttu-id="e15ec-283">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-283">Value Type</span></span>|<span data-ttu-id="e15ec-284">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-284">Required</span></span>|<span data-ttu-id="e15ec-285">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-285">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-286">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-286">statusCode</span></span>|<span data-ttu-id="e15ec-287">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-287">int</span></span>|<span data-ttu-id="e15ec-288">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-288">Yes</span></span>|<span data-ttu-id="e15ec-289">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-289">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-290">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-290">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="e15ec-291">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-291">statusDescription</span></span>|<span data-ttu-id="e15ec-292">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-292">string</span></span>|<span data-ttu-id="e15ec-293">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-293">No</span></span>|<span data-ttu-id="e15ec-294">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-294">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-295">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:</span><span class="sxs-lookup"><span data-stu-id="e15ec-295">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-296">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-296">Key</span></span>|<span data-ttu-id="e15ec-297">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-297">Value Type</span></span>|<span data-ttu-id="e15ec-298">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-298">Required</span></span>|<span data-ttu-id="e15ec-299">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-299">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-300">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="e15ec-300">sequence-numbers</span></span>|<span data-ttu-id="e15ec-301">long 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-301">array of long</span></span>|<span data-ttu-id="e15ec-302">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-302">Yes</span></span>|<span data-ttu-id="e15ec-303">예약된 메시지의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-303">Sequence number of scheduled messages.</span></span> <span data-ttu-id="e15ec-304">시퀀스 번호가 사용 되는 toocancel입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-304">Sequence number is used toocancel.</span></span>|  
  
### <a name="cancel-scheduled-message"></a><span data-ttu-id="e15ec-305">예약된 메시지 취소</span><span class="sxs-lookup"><span data-stu-id="e15ec-305">Cancel Scheduled Message</span></span>  

<span data-ttu-id="e15ec-306">예약된 메시지를 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-306">Cancels scheduled messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-307">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-307">Request</span></span>  

<span data-ttu-id="e15ec-308">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-308">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-309">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-309">Key</span></span>|<span data-ttu-id="e15ec-310">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-310">Value Type</span></span>|<span data-ttu-id="e15ec-311">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-311">Required</span></span>|<span data-ttu-id="e15ec-312">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-312">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-313">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-313">operation</span></span>|<span data-ttu-id="e15ec-314">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-314">string</span></span>|<span data-ttu-id="e15ec-315">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-315">Yes</span></span>|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-316">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-316">uint</span></span>|<span data-ttu-id="e15ec-317">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-317">No</span></span>|<span data-ttu-id="e15ec-318">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-318">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-319">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-319">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-320">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-320">Key</span></span>|<span data-ttu-id="e15ec-321">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-321">Value Type</span></span>|<span data-ttu-id="e15ec-322">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-322">Required</span></span>|<span data-ttu-id="e15ec-323">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-323">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-324">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="e15ec-324">sequence-numbers</span></span>|<span data-ttu-id="e15ec-325">long 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-325">array of long</span></span>|<span data-ttu-id="e15ec-326">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-326">Yes</span></span>|<span data-ttu-id="e15ec-327">예약 된 메시지 toocancel의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-327">Sequence numbers of scheduled messages toocancel.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-328">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-328">Response</span></span>  

<span data-ttu-id="e15ec-329">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-329">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-330">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-330">Key</span></span>|<span data-ttu-id="e15ec-331">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-331">Value Type</span></span>|<span data-ttu-id="e15ec-332">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-332">Required</span></span>|<span data-ttu-id="e15ec-333">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-333">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-334">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-334">statusCode</span></span>|<span data-ttu-id="e15ec-335">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-335">int</span></span>|<span data-ttu-id="e15ec-336">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-336">Yes</span></span>|<span data-ttu-id="e15ec-337">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-337">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-338">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-338">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="e15ec-339">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-339">statusDescription</span></span>|<span data-ttu-id="e15ec-340">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-340">string</span></span>|<span data-ttu-id="e15ec-341">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-341">No</span></span>|<span data-ttu-id="e15ec-342">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-342">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-343">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:</span><span class="sxs-lookup"><span data-stu-id="e15ec-343">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-344">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-344">Key</span></span>|<span data-ttu-id="e15ec-345">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-345">Value Type</span></span>|<span data-ttu-id="e15ec-346">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-346">Required</span></span>|<span data-ttu-id="e15ec-347">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-347">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-348">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="e15ec-348">sequence-numbers</span></span>|<span data-ttu-id="e15ec-349">long 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-349">array of long</span></span>|<span data-ttu-id="e15ec-350">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-350">Yes</span></span>|<span data-ttu-id="e15ec-351">예약된 메시지의 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-351">Sequence number of scheduled messages.</span></span> <span data-ttu-id="e15ec-352">시퀀스 번호가 사용 되는 toocancel입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-352">Sequence number is used toocancel.</span></span>|  
  
## <a name="session-operations"></a><span data-ttu-id="e15ec-353">세션 작업</span><span class="sxs-lookup"><span data-stu-id="e15ec-353">Session Operations</span></span>  
  
### <a name="session-renew-lock"></a><span data-ttu-id="e15ec-354">세션 갱신 잠금</span><span class="sxs-lookup"><span data-stu-id="e15ec-354">Session Renew Lock</span></span>  

<span data-ttu-id="e15ec-355">Hello 시간별 hello 엔터티 설명에 지정 된 메시지의 잠금 hello를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-355">Extends hello lock of a message by hello time specified in hello entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-356">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-356">Request</span></span>  

<span data-ttu-id="e15ec-357">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-357">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-358">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-358">Key</span></span>|<span data-ttu-id="e15ec-359">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-359">Value Type</span></span>|<span data-ttu-id="e15ec-360">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-360">Required</span></span>|<span data-ttu-id="e15ec-361">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-361">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-362">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-362">operation</span></span>|<span data-ttu-id="e15ec-363">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-363">string</span></span>|<span data-ttu-id="e15ec-364">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-364">Yes</span></span>|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-365">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-365">uint</span></span>|<span data-ttu-id="e15ec-366">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-366">No</span></span>|<span data-ttu-id="e15ec-367">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-367">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-368">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-368">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-369">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-369">Key</span></span>|<span data-ttu-id="e15ec-370">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-370">Value Type</span></span>|<span data-ttu-id="e15ec-371">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-371">Required</span></span>|<span data-ttu-id="e15ec-372">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-372">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-373">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-373">session-id</span></span>|<span data-ttu-id="e15ec-374">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-374">string</span></span>|<span data-ttu-id="e15ec-375">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-375">Yes</span></span>|<span data-ttu-id="e15ec-376">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="e15ec-376">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-377">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-377">Response</span></span>  

<span data-ttu-id="e15ec-378">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-378">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-379">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-379">Key</span></span>|<span data-ttu-id="e15ec-380">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-380">Value Type</span></span>|<span data-ttu-id="e15ec-381">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-381">Required</span></span>|<span data-ttu-id="e15ec-382">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-382">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-383">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-383">statusCode</span></span>|<span data-ttu-id="e15ec-384">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-384">int</span></span>|<span data-ttu-id="e15ec-385">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-385">Yes</span></span>|<span data-ttu-id="e15ec-386">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-386">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-387">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="e15ec-387">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="e15ec-388">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="e15ec-388">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="e15ec-389">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-389">statusDescription</span></span>|<span data-ttu-id="e15ec-390">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-390">string</span></span>|<span data-ttu-id="e15ec-391">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-391">No</span></span>|<span data-ttu-id="e15ec-392">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-392">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-393">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:</span><span class="sxs-lookup"><span data-stu-id="e15ec-393">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-394">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-394">Key</span></span>|<span data-ttu-id="e15ec-395">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-395">Value Type</span></span>|<span data-ttu-id="e15ec-396">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-396">Required</span></span>|<span data-ttu-id="e15ec-397">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-397">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-398">expiration</span><span class="sxs-lookup"><span data-stu-id="e15ec-398">expiration</span></span>|<span data-ttu-id="e15ec-399">timestamp</span><span class="sxs-lookup"><span data-stu-id="e15ec-399">timestamp</span></span>|<span data-ttu-id="e15ec-400">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-400">Yes</span></span>|<span data-ttu-id="e15ec-401">새 만료.</span><span class="sxs-lookup"><span data-stu-id="e15ec-401">New expiration.</span></span>|  
  
### <a name="peek-session-message"></a><span data-ttu-id="e15ec-402">세션 메시지 보기</span><span class="sxs-lookup"><span data-stu-id="e15ec-402">Peek Session Message</span></span>  

<span data-ttu-id="e15ec-403">잠그지 않고 세션 메시지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-403">Peeks session messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-404">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-404">Request</span></span>  

<span data-ttu-id="e15ec-405">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-405">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-406">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-406">Key</span></span>|<span data-ttu-id="e15ec-407">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-407">Value Type</span></span>|<span data-ttu-id="e15ec-408">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-408">Required</span></span>|<span data-ttu-id="e15ec-409">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-409">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-410">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-410">operation</span></span>|<span data-ttu-id="e15ec-411">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-411">string</span></span>|<span data-ttu-id="e15ec-412">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-412">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-413">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-413">uint</span></span>|<span data-ttu-id="e15ec-414">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-414">No</span></span>|<span data-ttu-id="e15ec-415">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-415">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-416">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-416">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-417">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-417">Key</span></span>|<span data-ttu-id="e15ec-418">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-418">Value Type</span></span>|<span data-ttu-id="e15ec-419">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-419">Required</span></span>|<span data-ttu-id="e15ec-420">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-420">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-421">from-sequence-number</span><span class="sxs-lookup"><span data-stu-id="e15ec-421">from-sequence-number</span></span>|<span data-ttu-id="e15ec-422">long</span><span class="sxs-lookup"><span data-stu-id="e15ec-422">long</span></span>|<span data-ttu-id="e15ec-423">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-423">Yes</span></span>|<span data-ttu-id="e15ec-424">Toostart 피킹은에서 시퀀스 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-424">Sequence number from which toostart peek.</span></span>|  
|<span data-ttu-id="e15ec-425">message-count</span><span class="sxs-lookup"><span data-stu-id="e15ec-425">message-count</span></span>|<span data-ttu-id="e15ec-426">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-426">int</span></span>|<span data-ttu-id="e15ec-427">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-427">Yes</span></span>|<span data-ttu-id="e15ec-428">메시지 toopeek의 최대 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-428">Maximum number of messages toopeek.</span></span>|  
|<span data-ttu-id="e15ec-429">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-429">session-id</span></span>|<span data-ttu-id="e15ec-430">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-430">string</span></span>|<span data-ttu-id="e15ec-431">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-431">Yes</span></span>|<span data-ttu-id="e15ec-432">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="e15ec-432">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-433">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-433">Response</span></span>  

<span data-ttu-id="e15ec-434">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-434">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-435">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-435">Key</span></span>|<span data-ttu-id="e15ec-436">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-436">Value Type</span></span>|<span data-ttu-id="e15ec-437">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-437">Required</span></span>|<span data-ttu-id="e15ec-438">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-438">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-439">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-439">statusCode</span></span>|<span data-ttu-id="e15ec-440">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-440">int</span></span>|<span data-ttu-id="e15ec-441">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-441">Yes</span></span>|<span data-ttu-id="e15ec-442">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-442">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-443">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="e15ec-443">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="e15ec-444">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="e15ec-444">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="e15ec-445">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-445">statusDescription</span></span>|<span data-ttu-id="e15ec-446">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-446">string</span></span>|<span data-ttu-id="e15ec-447">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-447">No</span></span>|<span data-ttu-id="e15ec-448">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-448">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-449">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 지도 항목을 다음 hello로 포함 된 섹션:</span><span class="sxs-lookup"><span data-stu-id="e15ec-449">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-450">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-450">Key</span></span>|<span data-ttu-id="e15ec-451">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-451">Value Type</span></span>|<span data-ttu-id="e15ec-452">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-452">Required</span></span>|<span data-ttu-id="e15ec-453">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-453">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-454">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="e15ec-454">messages</span></span>|<span data-ttu-id="e15ec-455">맵 목록</span><span class="sxs-lookup"><span data-stu-id="e15ec-455">list of maps</span></span>|<span data-ttu-id="e15ec-456">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-456">Yes</span></span>|<span data-ttu-id="e15ec-457">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-457">List of messages in which every map represents a message.</span></span>|  
  
 <span data-ttu-id="e15ec-458">메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-458">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-459">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-459">Key</span></span>|<span data-ttu-id="e15ec-460">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-460">Value Type</span></span>|<span data-ttu-id="e15ec-461">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-461">Required</span></span>|<span data-ttu-id="e15ec-462">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-462">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-463">message</span><span class="sxs-lookup"><span data-stu-id="e15ec-463">message</span></span>|<span data-ttu-id="e15ec-464">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-464">array of byte</span></span>|<span data-ttu-id="e15ec-465">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-465">Yes</span></span>|<span data-ttu-id="e15ec-466">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-466">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="set-session-state"></a><span data-ttu-id="e15ec-467">세션 상태 설정</span><span class="sxs-lookup"><span data-stu-id="e15ec-467">Set Session State</span></span>  

<span data-ttu-id="e15ec-468">집합 hello 세션의 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-468">Sets hello state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-469">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-469">Request</span></span>  

<span data-ttu-id="e15ec-470">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-470">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-471">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-471">Key</span></span>|<span data-ttu-id="e15ec-472">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-472">Value Type</span></span>|<span data-ttu-id="e15ec-473">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-473">Required</span></span>|<span data-ttu-id="e15ec-474">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-474">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-475">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-475">operation</span></span>|<span data-ttu-id="e15ec-476">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-476">string</span></span>|<span data-ttu-id="e15ec-477">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-477">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-478">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-478">uint</span></span>|<span data-ttu-id="e15ec-479">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-479">No</span></span>|<span data-ttu-id="e15ec-480">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-480">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-481">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-481">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-482">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-482">Key</span></span>|<span data-ttu-id="e15ec-483">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-483">Value Type</span></span>|<span data-ttu-id="e15ec-484">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-484">Required</span></span>|<span data-ttu-id="e15ec-485">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-485">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-486">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-486">session-id</span></span>|<span data-ttu-id="e15ec-487">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-487">string</span></span>|<span data-ttu-id="e15ec-488">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-488">Yes</span></span>|<span data-ttu-id="e15ec-489">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="e15ec-489">Session ID.</span></span>|  
|<span data-ttu-id="e15ec-490">session-state</span><span class="sxs-lookup"><span data-stu-id="e15ec-490">session-state</span></span>|<span data-ttu-id="e15ec-491">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-491">array of bytes</span></span>|<span data-ttu-id="e15ec-492">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-492">Yes</span></span>|<span data-ttu-id="e15ec-493">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="e15ec-493">Opaque binary data.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-494">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-494">Response</span></span>  

<span data-ttu-id="e15ec-495">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-495">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-496">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-496">Key</span></span>|<span data-ttu-id="e15ec-497">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-497">Value Type</span></span>|<span data-ttu-id="e15ec-498">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-498">Required</span></span>|<span data-ttu-id="e15ec-499">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-499">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-500">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-500">statusCode</span></span>|<span data-ttu-id="e15ec-501">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-501">int</span></span>|<span data-ttu-id="e15ec-502">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-502">Yes</span></span>|<span data-ttu-id="e15ec-503">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-503">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-504">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-504">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-505">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-505">statusDescription</span></span>|<span data-ttu-id="e15ec-506">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-506">string</span></span>|<span data-ttu-id="e15ec-507">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-507">No</span></span>|<span data-ttu-id="e15ec-508">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-508">Description of hello status.</span></span>|  
  
### <a name="get-session-state"></a><span data-ttu-id="e15ec-509">세션 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="e15ec-509">Get Session State</span></span>  

<span data-ttu-id="e15ec-510">세션의 hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-510">Gets hello state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-511">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-511">Request</span></span>  

<span data-ttu-id="e15ec-512">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-512">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-513">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-513">Key</span></span>|<span data-ttu-id="e15ec-514">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-514">Value Type</span></span>|<span data-ttu-id="e15ec-515">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-515">Required</span></span>|<span data-ttu-id="e15ec-516">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-516">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-517">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-517">operation</span></span>|<span data-ttu-id="e15ec-518">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-518">string</span></span>|<span data-ttu-id="e15ec-519">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-519">Yes</span></span>|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-520">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-520">uint</span></span>|<span data-ttu-id="e15ec-521">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-521">No</span></span>|<span data-ttu-id="e15ec-522">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-522">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-523">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-523">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-524">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-524">Key</span></span>|<span data-ttu-id="e15ec-525">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-525">Value Type</span></span>|<span data-ttu-id="e15ec-526">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-526">Required</span></span>|<span data-ttu-id="e15ec-527">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-527">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-528">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-528">session-id</span></span>|<span data-ttu-id="e15ec-529">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-529">string</span></span>|<span data-ttu-id="e15ec-530">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-530">Yes</span></span>|<span data-ttu-id="e15ec-531">세션 ID.</span><span class="sxs-lookup"><span data-stu-id="e15ec-531">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-532">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-532">Response</span></span>  

<span data-ttu-id="e15ec-533">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-533">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-534">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-534">Key</span></span>|<span data-ttu-id="e15ec-535">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-535">Value Type</span></span>|<span data-ttu-id="e15ec-536">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-536">Required</span></span>|<span data-ttu-id="e15ec-537">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-537">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-538">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-538">statusCode</span></span>|<span data-ttu-id="e15ec-539">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-539">int</span></span>|<span data-ttu-id="e15ec-540">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-540">Yes</span></span>|<span data-ttu-id="e15ec-541">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-541">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-542">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-542">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-543">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-543">statusDescription</span></span>|<span data-ttu-id="e15ec-544">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-544">string</span></span>|<span data-ttu-id="e15ec-545">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-545">No</span></span>|<span data-ttu-id="e15ec-546">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-546">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-547">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-547">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-548">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-548">Key</span></span>|<span data-ttu-id="e15ec-549">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-549">Value Type</span></span>|<span data-ttu-id="e15ec-550">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-550">Required</span></span>|<span data-ttu-id="e15ec-551">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-551">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-552">session-state</span><span class="sxs-lookup"><span data-stu-id="e15ec-552">session-state</span></span>|<span data-ttu-id="e15ec-553">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-553">array of bytes</span></span>|<span data-ttu-id="e15ec-554">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-554">Yes</span></span>|<span data-ttu-id="e15ec-555">불투명한 이진 본문.</span><span class="sxs-lookup"><span data-stu-id="e15ec-555">Opaque binary data.</span></span>|  
  
### <a name="enumerate-sessions"></a><span data-ttu-id="e15ec-556">세션 열거</span><span class="sxs-lookup"><span data-stu-id="e15ec-556">Enumerate Sessions</span></span>  

<span data-ttu-id="e15ec-557">메시지 엔터티에서 세션을 열거합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-557">Enumerates sessions on a messaging entity.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-558">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-558">Request</span></span>  

<span data-ttu-id="e15ec-559">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-559">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-560">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-560">Key</span></span>|<span data-ttu-id="e15ec-561">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-561">Value Type</span></span>|<span data-ttu-id="e15ec-562">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-562">Required</span></span>|<span data-ttu-id="e15ec-563">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-563">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-564">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-564">operation</span></span>|<span data-ttu-id="e15ec-565">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-565">string</span></span>|<span data-ttu-id="e15ec-566">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-566">Yes</span></span>|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-567">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-567">uint</span></span>|<span data-ttu-id="e15ec-568">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-568">No</span></span>|<span data-ttu-id="e15ec-569">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-569">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-570">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-570">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-571">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-571">Key</span></span>|<span data-ttu-id="e15ec-572">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-572">Value Type</span></span>|<span data-ttu-id="e15ec-573">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-573">Required</span></span>|<span data-ttu-id="e15ec-574">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-574">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-575">last-updated-time</span><span class="sxs-lookup"><span data-stu-id="e15ec-575">last-updated-time</span></span>|<span data-ttu-id="e15ec-576">timestamp</span><span class="sxs-lookup"><span data-stu-id="e15ec-576">timestamp</span></span>|<span data-ttu-id="e15ec-577">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-577">Yes</span></span>|<span data-ttu-id="e15ec-578">지정된 된 시간 후에 업데이트 tooinclude만 세션을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-578">Filter tooinclude only sessions updated after a given time.</span></span>|  
|<span data-ttu-id="e15ec-579">skip</span><span class="sxs-lookup"><span data-stu-id="e15ec-579">skip</span></span>|<span data-ttu-id="e15ec-580">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-580">int</span></span>|<span data-ttu-id="e15ec-581">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-581">Yes</span></span>|<span data-ttu-id="e15ec-582">세션 수를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-582">Skip a number of sessions.</span></span>|  
|<span data-ttu-id="e15ec-583">top</span><span class="sxs-lookup"><span data-stu-id="e15ec-583">top</span></span>|<span data-ttu-id="e15ec-584">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-584">int</span></span>|<span data-ttu-id="e15ec-585">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-585">Yes</span></span>|<span data-ttu-id="e15ec-586">최대 세션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-586">Maximum number of sessions.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-587">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-587">Response</span></span>  

<span data-ttu-id="e15ec-588">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-588">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-589">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-589">Key</span></span>|<span data-ttu-id="e15ec-590">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-590">Value Type</span></span>|<span data-ttu-id="e15ec-591">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-591">Required</span></span>|<span data-ttu-id="e15ec-592">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-592">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-593">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-593">statusCode</span></span>|<span data-ttu-id="e15ec-594">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-594">int</span></span>|<span data-ttu-id="e15ec-595">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-595">Yes</span></span>|<span data-ttu-id="e15ec-596">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-596">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-597">200: OK – 더 많은 메시지가 있음</span><span class="sxs-lookup"><span data-stu-id="e15ec-597">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="e15ec-598">0xcc: 콘텐츠 없음 – 더 이상 메시지가 없음</span><span class="sxs-lookup"><span data-stu-id="e15ec-598">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="e15ec-599">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-599">statusDescription</span></span>|<span data-ttu-id="e15ec-600">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-600">string</span></span>|<span data-ttu-id="e15ec-601">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-601">No</span></span>|<span data-ttu-id="e15ec-602">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-602">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-603">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-603">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-604">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-604">Key</span></span>|<span data-ttu-id="e15ec-605">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-605">Value Type</span></span>|<span data-ttu-id="e15ec-606">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-606">Required</span></span>|<span data-ttu-id="e15ec-607">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-607">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-608">skip</span><span class="sxs-lookup"><span data-stu-id="e15ec-608">skip</span></span>|<span data-ttu-id="e15ec-609">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-609">int</span></span>|<span data-ttu-id="e15ec-610">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-610">Yes</span></span>|<span data-ttu-id="e15ec-611">상태 코드가 200인 경우 건너뛴 세션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-611">Number of skipped sessions if status code is 200.</span></span>|  
|<span data-ttu-id="e15ec-612">sessions-ids</span><span class="sxs-lookup"><span data-stu-id="e15ec-612">sessions-ids</span></span>|<span data-ttu-id="e15ec-613">문자열 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-613">array of strings</span></span>|<span data-ttu-id="e15ec-614">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-614">Yes</span></span>|<span data-ttu-id="e15ec-615">상태 코드가 200인 경우 세션 ID 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-615">Array of session IDs if status code is 200.</span></span>|  
  
## <a name="rule-operations"></a><span data-ttu-id="e15ec-616">규칙 작업</span><span class="sxs-lookup"><span data-stu-id="e15ec-616">Rule operations</span></span>  
  
### <a name="add-rule"></a><span data-ttu-id="e15ec-617">규칙 추가</span><span class="sxs-lookup"><span data-stu-id="e15ec-617">Add Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-618">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-618">Request</span></span>  

<span data-ttu-id="e15ec-619">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-619">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-620">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-620">Key</span></span>|<span data-ttu-id="e15ec-621">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-621">Value Type</span></span>|<span data-ttu-id="e15ec-622">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-622">Required</span></span>|<span data-ttu-id="e15ec-623">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-623">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-624">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-624">operation</span></span>|<span data-ttu-id="e15ec-625">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-625">string</span></span>|<span data-ttu-id="e15ec-626">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-626">Yes</span></span>|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-627">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-627">uint</span></span>|<span data-ttu-id="e15ec-628">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-628">No</span></span>|<span data-ttu-id="e15ec-629">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-629">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-630">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-630">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-631">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-631">Key</span></span>|<span data-ttu-id="e15ec-632">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-632">Value Type</span></span>|<span data-ttu-id="e15ec-633">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-633">Required</span></span>|<span data-ttu-id="e15ec-634">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-634">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-635">rule-name</span><span class="sxs-lookup"><span data-stu-id="e15ec-635">rule-name</span></span>|<span data-ttu-id="e15ec-636">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-636">string</span></span>|<span data-ttu-id="e15ec-637">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-637">Yes</span></span>|<span data-ttu-id="e15ec-638">구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-638">Rule name, not including subscription and topic names.</span></span>|  
|<span data-ttu-id="e15ec-639">rule-description</span><span class="sxs-lookup"><span data-stu-id="e15ec-639">rule-description</span></span>|<span data-ttu-id="e15ec-640">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-640">map</span></span>|<span data-ttu-id="e15ec-641">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-641">Yes</span></span>|<span data-ttu-id="e15ec-642">다음 섹션에 지정된 대로 규칙 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-642">Rule description as specified in next section.</span></span>|  
  
<span data-ttu-id="e15ec-643">hello **규칙 설명** 맵 항목을 다음 hello 있어야 합니다. 여기서 **sql 필터** 및 **상관 관계 필터** 함께 사용할 수 없습니다:</span><span class="sxs-lookup"><span data-stu-id="e15ec-643">hello **rule-description** map must include hello following entries, where **sql-filter** and **correlation-filter** are mutually exclusive:</span></span>  
  
|<span data-ttu-id="e15ec-644">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-644">Key</span></span>|<span data-ttu-id="e15ec-645">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-645">Value Type</span></span>|<span data-ttu-id="e15ec-646">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-646">Required</span></span>|<span data-ttu-id="e15ec-647">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-647">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-648">sql-filter</span><span class="sxs-lookup"><span data-stu-id="e15ec-648">sql-filter</span></span>|<span data-ttu-id="e15ec-649">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-649">map</span></span>|<span data-ttu-id="e15ec-650">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-650">Yes</span></span>|<span data-ttu-id="e15ec-651">`sql-filter`hello 다음 섹션에 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-651">`sql-filter`, as specified in hello next section.</span></span>|  
|<span data-ttu-id="e15ec-652">correlation-filter</span><span class="sxs-lookup"><span data-stu-id="e15ec-652">correlation-filter</span></span>|<span data-ttu-id="e15ec-653">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-653">map</span></span>|<span data-ttu-id="e15ec-654">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-654">Yes</span></span>|<span data-ttu-id="e15ec-655">`correlation-filter`hello 다음 섹션에 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-655">`correlation-filter`, as specified in hello next section.</span></span>|  
|<span data-ttu-id="e15ec-656">sql-rule-action</span><span class="sxs-lookup"><span data-stu-id="e15ec-656">sql-rule-action</span></span>|<span data-ttu-id="e15ec-657">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-657">map</span></span>|<span data-ttu-id="e15ec-658">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-658">Yes</span></span>|<span data-ttu-id="e15ec-659">`sql-rule-action`hello 다음 섹션에 지정 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-659">`sql-rule-action`, as specified in hello next section.</span></span>|  
  
<span data-ttu-id="e15ec-660">hello sql 필터 맵 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-660">hello sql-filter map must include hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-661">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-661">Key</span></span>|<span data-ttu-id="e15ec-662">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-662">Value Type</span></span>|<span data-ttu-id="e15ec-663">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-663">Required</span></span>|<span data-ttu-id="e15ec-664">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-664">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-665">식</span><span class="sxs-lookup"><span data-stu-id="e15ec-665">expression</span></span>|<span data-ttu-id="e15ec-666">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-666">string</span></span>|<span data-ttu-id="e15ec-667">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-667">Yes</span></span>|<span data-ttu-id="e15ec-668">Sql 필터 식.</span><span class="sxs-lookup"><span data-stu-id="e15ec-668">Sql filter expression.</span></span>|  
  
<span data-ttu-id="e15ec-669">hello **상관 관계 필터** 맵에 hello 다음 항목 중 하나 이상을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-669">hello **correlation-filter** map must include at least one of hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-670">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-670">Key</span></span>|<span data-ttu-id="e15ec-671">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-671">Value Type</span></span>|<span data-ttu-id="e15ec-672">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-672">Required</span></span>|<span data-ttu-id="e15ec-673">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-673">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-674">correlation-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-674">correlation-id</span></span>|<span data-ttu-id="e15ec-675">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-675">string</span></span>|<span data-ttu-id="e15ec-676">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-676">No</span></span>||  
|<span data-ttu-id="e15ec-677">message-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-677">message-id</span></span>|<span data-ttu-id="e15ec-678">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-678">string</span></span>|<span data-ttu-id="e15ec-679">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-679">No</span></span>||  
|<span data-ttu-id="e15ec-680">to</span><span class="sxs-lookup"><span data-stu-id="e15ec-680">to</span></span>|<span data-ttu-id="e15ec-681">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-681">string</span></span>|<span data-ttu-id="e15ec-682">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-682">No</span></span>||  
|<span data-ttu-id="e15ec-683">reply-to</span><span class="sxs-lookup"><span data-stu-id="e15ec-683">reply-to</span></span>|<span data-ttu-id="e15ec-684">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-684">string</span></span>|<span data-ttu-id="e15ec-685">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-685">No</span></span>||  
|<span data-ttu-id="e15ec-686">label</span><span class="sxs-lookup"><span data-stu-id="e15ec-686">label</span></span>|<span data-ttu-id="e15ec-687">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-687">string</span></span>|<span data-ttu-id="e15ec-688">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-688">No</span></span>||  
|<span data-ttu-id="e15ec-689">session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-689">session-id</span></span>|<span data-ttu-id="e15ec-690">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-690">string</span></span>|<span data-ttu-id="e15ec-691">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-691">No</span></span>||  
|<span data-ttu-id="e15ec-692">reply-to-session-id</span><span class="sxs-lookup"><span data-stu-id="e15ec-692">reply-to-session-id</span></span>|<span data-ttu-id="e15ec-693">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-693">string</span></span>|<span data-ttu-id="e15ec-694">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-694">No</span></span>||  
|<span data-ttu-id="e15ec-695">content-type</span><span class="sxs-lookup"><span data-stu-id="e15ec-695">content-type</span></span>|<span data-ttu-id="e15ec-696">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-696">string</span></span>|<span data-ttu-id="e15ec-697">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-697">No</span></span>||  
|<span data-ttu-id="e15ec-698">properties</span><span class="sxs-lookup"><span data-stu-id="e15ec-698">properties</span></span>|<span data-ttu-id="e15ec-699">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-699">map</span></span>|<span data-ttu-id="e15ec-700">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-700">No</span></span>|<span data-ttu-id="e15ec-701">버스 tooService 매핑합니다 [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-701">Maps tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).</span></span>|  
  
<span data-ttu-id="e15ec-702">hello **sql 규칙-작업** 지도 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-702">hello **sql-rule-action** map must include hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-703">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-703">Key</span></span>|<span data-ttu-id="e15ec-704">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-704">Value Type</span></span>|<span data-ttu-id="e15ec-705">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-705">Required</span></span>|<span data-ttu-id="e15ec-706">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-706">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-707">식</span><span class="sxs-lookup"><span data-stu-id="e15ec-707">expression</span></span>|<span data-ttu-id="e15ec-708">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-708">string</span></span>|<span data-ttu-id="e15ec-709">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-709">Yes</span></span>|<span data-ttu-id="e15ec-710">Sql 작업 식.</span><span class="sxs-lookup"><span data-stu-id="e15ec-710">Sql action expression.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-711">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-711">Response</span></span>  

<span data-ttu-id="e15ec-712">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-712">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-713">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-713">Key</span></span>|<span data-ttu-id="e15ec-714">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-714">Value Type</span></span>|<span data-ttu-id="e15ec-715">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-715">Required</span></span>|<span data-ttu-id="e15ec-716">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-716">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-717">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-717">statusCode</span></span>|<span data-ttu-id="e15ec-718">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-718">int</span></span>|<span data-ttu-id="e15ec-719">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-719">Yes</span></span>|<span data-ttu-id="e15ec-720">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-720">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-721">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-721">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-722">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-722">statusDescription</span></span>|<span data-ttu-id="e15ec-723">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-723">string</span></span>|<span data-ttu-id="e15ec-724">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-724">No</span></span>|<span data-ttu-id="e15ec-725">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-725">Description of hello status.</span></span>|  
  
### <a name="remove-rule"></a><span data-ttu-id="e15ec-726">규칙 제거</span><span class="sxs-lookup"><span data-stu-id="e15ec-726">Remove Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-727">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-727">Request</span></span>  

<span data-ttu-id="e15ec-728">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-728">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-729">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-729">Key</span></span>|<span data-ttu-id="e15ec-730">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-730">Value Type</span></span>|<span data-ttu-id="e15ec-731">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-731">Required</span></span>|<span data-ttu-id="e15ec-732">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-732">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-733">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-733">operation</span></span>|<span data-ttu-id="e15ec-734">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-734">string</span></span>|<span data-ttu-id="e15ec-735">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-735">Yes</span></span>|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-736">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-736">uint</span></span>|<span data-ttu-id="e15ec-737">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-737">No</span></span>|<span data-ttu-id="e15ec-738">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-738">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-739">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-739">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-740">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-740">Key</span></span>|<span data-ttu-id="e15ec-741">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-741">Value Type</span></span>|<span data-ttu-id="e15ec-742">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-742">Required</span></span>|<span data-ttu-id="e15ec-743">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-743">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-744">rule-name</span><span class="sxs-lookup"><span data-stu-id="e15ec-744">rule-name</span></span>|<span data-ttu-id="e15ec-745">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-745">string</span></span>|<span data-ttu-id="e15ec-746">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-746">Yes</span></span>|<span data-ttu-id="e15ec-747">구독 및 토픽 이름을 포함하지 않는 규칙 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-747">Rule name, not including subscription and topic names.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-748">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-748">Response</span></span>  

<span data-ttu-id="e15ec-749">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-749">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-750">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-750">Key</span></span>|<span data-ttu-id="e15ec-751">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-751">Value Type</span></span>|<span data-ttu-id="e15ec-752">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-752">Required</span></span>|<span data-ttu-id="e15ec-753">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-753">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-754">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-754">statusCode</span></span>|<span data-ttu-id="e15ec-755">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-755">int</span></span>|<span data-ttu-id="e15ec-756">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-756">Yes</span></span>|<span data-ttu-id="e15ec-757">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-757">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-758">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-758">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-759">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-759">statusDescription</span></span>|<span data-ttu-id="e15ec-760">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-760">string</span></span>|<span data-ttu-id="e15ec-761">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-761">No</span></span>|<span data-ttu-id="e15ec-762">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-762">Description of hello status.</span></span>|  
  
## <a name="deferred-message-operations"></a><span data-ttu-id="e15ec-763">지연된 메시지 작업</span><span class="sxs-lookup"><span data-stu-id="e15ec-763">Deferred message operations</span></span>  
  
### <a name="receive-by-sequence-number"></a><span data-ttu-id="e15ec-764">시퀀스 번호로 받기</span><span class="sxs-lookup"><span data-stu-id="e15ec-764">Receive by sequence number</span></span>  

<span data-ttu-id="e15ec-765">시퀀스 번호로 지연된 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-765">Receives deferred messages by sequence number.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-766">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-766">Request</span></span>  

<span data-ttu-id="e15ec-767">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-767">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-768">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-768">Key</span></span>|<span data-ttu-id="e15ec-769">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-769">Value Type</span></span>|<span data-ttu-id="e15ec-770">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-770">Required</span></span>|<span data-ttu-id="e15ec-771">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-771">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-772">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-772">operation</span></span>|<span data-ttu-id="e15ec-773">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-773">string</span></span>|<span data-ttu-id="e15ec-774">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-774">Yes</span></span>|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-775">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-775">uint</span></span>|<span data-ttu-id="e15ec-776">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-776">No</span></span>|<span data-ttu-id="e15ec-777">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-777">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-778">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-778">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-779">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-779">Key</span></span>|<span data-ttu-id="e15ec-780">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-780">Value Type</span></span>|<span data-ttu-id="e15ec-781">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-781">Required</span></span>|<span data-ttu-id="e15ec-782">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-782">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-783">시퀀스 번호</span><span class="sxs-lookup"><span data-stu-id="e15ec-783">sequence-numbers</span></span>|<span data-ttu-id="e15ec-784">long 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-784">array of long</span></span>|<span data-ttu-id="e15ec-785">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-785">Yes</span></span>|<span data-ttu-id="e15ec-786">시퀀스 번호.</span><span class="sxs-lookup"><span data-stu-id="e15ec-786">Sequence numbers.</span></span>|  
|<span data-ttu-id="e15ec-787">receiver-settle-mode</span><span class="sxs-lookup"><span data-stu-id="e15ec-787">receiver-settle-mode</span></span>|<span data-ttu-id="e15ec-788">ubyte</span><span class="sxs-lookup"><span data-stu-id="e15ec-788">ubyte</span></span>|<span data-ttu-id="e15ec-789">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-789">Yes</span></span>|<span data-ttu-id="e15ec-790">AMQP 코어 v1.0에 지정된 대로 **수신기 장착** 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-790">**Receiver settle** mode as specified in AMQP core v1.0.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-791">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-791">Response</span></span>  

<span data-ttu-id="e15ec-792">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-792">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-793">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-793">Key</span></span>|<span data-ttu-id="e15ec-794">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-794">Value Type</span></span>|<span data-ttu-id="e15ec-795">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-795">Required</span></span>|<span data-ttu-id="e15ec-796">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-796">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-797">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-797">statusCode</span></span>|<span data-ttu-id="e15ec-798">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-798">int</span></span>|<span data-ttu-id="e15ec-799">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-799">Yes</span></span>|<span data-ttu-id="e15ec-800">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-800">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-801">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-801">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-802">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-802">statusDescription</span></span>|<span data-ttu-id="e15ec-803">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-803">string</span></span>|<span data-ttu-id="e15ec-804">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-804">No</span></span>|<span data-ttu-id="e15ec-805">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-805">Description of hello status.</span></span>|  
  
<span data-ttu-id="e15ec-806">hello 응답 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-806">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-807">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-807">Key</span></span>|<span data-ttu-id="e15ec-808">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-808">Value Type</span></span>|<span data-ttu-id="e15ec-809">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-809">Required</span></span>|<span data-ttu-id="e15ec-810">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-810">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-811">메시지의 최대 전달 수</span><span class="sxs-lookup"><span data-stu-id="e15ec-811">messages</span></span>|<span data-ttu-id="e15ec-812">맵 목록</span><span class="sxs-lookup"><span data-stu-id="e15ec-812">list of maps</span></span>|<span data-ttu-id="e15ec-813">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-813">Yes</span></span>|<span data-ttu-id="e15ec-814">모든 맵이 메시지를 나타내는 메시지 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-814">List of messages where every map represents a message.</span></span>|  
  
<span data-ttu-id="e15ec-815">메시지를 나타내는 hello 맵 hello 다음 항목을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-815">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-816">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-816">Key</span></span>|<span data-ttu-id="e15ec-817">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-817">Value Type</span></span>|<span data-ttu-id="e15ec-818">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-818">Required</span></span>|<span data-ttu-id="e15ec-819">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-819">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-820">lock-token</span><span class="sxs-lookup"><span data-stu-id="e15ec-820">lock-token</span></span>|<span data-ttu-id="e15ec-821">uuid</span><span class="sxs-lookup"><span data-stu-id="e15ec-821">uuid</span></span>|<span data-ttu-id="e15ec-822">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-822">Yes</span></span>|<span data-ttu-id="e15ec-823">`receiver-settle-mode`가 1인 경우 토큰을 잠급니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-823">Lock token if `receiver-settle-mode` is 1.</span></span>|  
|<span data-ttu-id="e15ec-824">message</span><span class="sxs-lookup"><span data-stu-id="e15ec-824">message</span></span>|<span data-ttu-id="e15ec-825">바이트 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-825">array of byte</span></span>|<span data-ttu-id="e15ec-826">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-826">Yes</span></span>|<span data-ttu-id="e15ec-827">AMQP 1.0 실시간 인코딩된 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-827">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="update-disposition-status"></a><span data-ttu-id="e15ec-828">처리 상태 업데이트</span><span class="sxs-lookup"><span data-stu-id="e15ec-828">Update disposition status</span></span>  

<span data-ttu-id="e15ec-829">지연 된 메시지의 hello 처리 상태를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-829">Updates hello disposition status of deferred messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="e15ec-830">요청</span><span class="sxs-lookup"><span data-stu-id="e15ec-830">Request</span></span>  

<span data-ttu-id="e15ec-831">hello 요청 메시지에는 다음과 같은 응용 프로그램 속성 hello를 포함 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-831">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-832">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-832">Key</span></span>|<span data-ttu-id="e15ec-833">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-833">Value Type</span></span>|<span data-ttu-id="e15ec-834">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-834">Required</span></span>|<span data-ttu-id="e15ec-835">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-835">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-836">operation</span><span class="sxs-lookup"><span data-stu-id="e15ec-836">operation</span></span>|<span data-ttu-id="e15ec-837">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-837">string</span></span>|<span data-ttu-id="e15ec-838">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-838">Yes</span></span>|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="e15ec-839">uint</span><span class="sxs-lookup"><span data-stu-id="e15ec-839">uint</span></span>|<span data-ttu-id="e15ec-840">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-840">No</span></span>|<span data-ttu-id="e15ec-841">작업 서버 제한 시간(밀리초)입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-841">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="e15ec-842">hello 요청 메시지 본문으로 구성 되어야는 **amqp 값** 섹션을 포함 하는 **지도** 항목 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="e15ec-842">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="e15ec-843">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-843">Key</span></span>|<span data-ttu-id="e15ec-844">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-844">Value Type</span></span>|<span data-ttu-id="e15ec-845">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-845">Required</span></span>|<span data-ttu-id="e15ec-846">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-846">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-847">disposition-status</span><span class="sxs-lookup"><span data-stu-id="e15ec-847">disposition-status</span></span>|<span data-ttu-id="e15ec-848">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-848">string</span></span>|<span data-ttu-id="e15ec-849">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-849">Yes</span></span>|<span data-ttu-id="e15ec-850">완료됨</span><span class="sxs-lookup"><span data-stu-id="e15ec-850">completed</span></span><br /><br /> <span data-ttu-id="e15ec-851">중단됨</span><span class="sxs-lookup"><span data-stu-id="e15ec-851">abandoned</span></span><br /><br /> <span data-ttu-id="e15ec-852">일시 중단됨</span><span class="sxs-lookup"><span data-stu-id="e15ec-852">suspended</span></span>|  
|<span data-ttu-id="e15ec-853">lock-tokens</span><span class="sxs-lookup"><span data-stu-id="e15ec-853">lock-tokens</span></span>|<span data-ttu-id="e15ec-854">uuid의 배열</span><span class="sxs-lookup"><span data-stu-id="e15ec-854">array of uuid</span></span>|<span data-ttu-id="e15ec-855">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-855">Yes</span></span>|<span data-ttu-id="e15ec-856">메시지 잠금 토큰 tooupdate 처리 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-856">Message lock tokens tooupdate disposition status.</span></span>|  
|<span data-ttu-id="e15ec-857">deadletter-reason</span><span class="sxs-lookup"><span data-stu-id="e15ec-857">deadletter-reason</span></span>|<span data-ttu-id="e15ec-858">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-858">string</span></span>|<span data-ttu-id="e15ec-859">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-859">No</span></span>|<span data-ttu-id="e15ec-860">처리 상태 너무 설정 된 경우에 설정할 수 있습니다**일시 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-860">May be set if disposition status is set too**suspended**.</span></span>|  
|<span data-ttu-id="e15ec-861">deadletter-description</span><span class="sxs-lookup"><span data-stu-id="e15ec-861">deadletter-description</span></span>|<span data-ttu-id="e15ec-862">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-862">string</span></span>|<span data-ttu-id="e15ec-863">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-863">No</span></span>|<span data-ttu-id="e15ec-864">처리 상태 너무 설정 된 경우에 설정할 수 있습니다**일시 중단**합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-864">May be set if disposition status is set too**suspended**.</span></span>|  
|<span data-ttu-id="e15ec-865">properties-to-modify</span><span class="sxs-lookup"><span data-stu-id="e15ec-865">properties-to-modify</span></span>|<span data-ttu-id="e15ec-866">map</span><span class="sxs-lookup"><span data-stu-id="e15ec-866">map</span></span>|<span data-ttu-id="e15ec-867">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-867">No</span></span>|<span data-ttu-id="e15ec-868">메시지 속성 toomodify를 중개 하는 서비스 버스의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-868">List of Service Bus brokered message properties toomodify.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="e15ec-869">응답</span><span class="sxs-lookup"><span data-stu-id="e15ec-869">Response</span></span>  

<span data-ttu-id="e15ec-870">hello 응답 메시지는 hello 다음과 같은 응용 프로그램 속성을 포함 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-870">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="e15ec-871">키</span><span class="sxs-lookup"><span data-stu-id="e15ec-871">Key</span></span>|<span data-ttu-id="e15ec-872">값 형식</span><span class="sxs-lookup"><span data-stu-id="e15ec-872">Value Type</span></span>|<span data-ttu-id="e15ec-873">필수</span><span class="sxs-lookup"><span data-stu-id="e15ec-873">Required</span></span>|<span data-ttu-id="e15ec-874">값 내용</span><span class="sxs-lookup"><span data-stu-id="e15ec-874">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="e15ec-875">statusCode</span><span class="sxs-lookup"><span data-stu-id="e15ec-875">statusCode</span></span>|<span data-ttu-id="e15ec-876">int</span><span class="sxs-lookup"><span data-stu-id="e15ec-876">int</span></span>|<span data-ttu-id="e15ec-877">예</span><span class="sxs-lookup"><span data-stu-id="e15ec-877">Yes</span></span>|<span data-ttu-id="e15ec-878">HTTP 응답 코드 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="e15ec-878">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="e15ec-879">200: OK – 성공, 그렇지 않으면 실패입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-879">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="e15ec-880">statusDescription</span><span class="sxs-lookup"><span data-stu-id="e15ec-880">statusDescription</span></span>|<span data-ttu-id="e15ec-881">string</span><span class="sxs-lookup"><span data-stu-id="e15ec-881">string</span></span>|<span data-ttu-id="e15ec-882">아니요</span><span class="sxs-lookup"><span data-stu-id="e15ec-882">No</span></span>|<span data-ttu-id="e15ec-883">Hello 상태에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e15ec-883">Description of hello status.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="e15ec-884">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e15ec-884">Next steps</span></span>

<span data-ttu-id="e15ec-885">AMQP 및 서비스 버스에 대해 자세히 toolearn 방문 링크를 따라 hello:</span><span class="sxs-lookup"><span data-stu-id="e15ec-885">toolearn more about AMQP and Service Bus, visit hello following links:</span></span>

* <span data-ttu-id="e15ec-886">[Service Bus AMQP 개요]</span><span class="sxs-lookup"><span data-stu-id="e15ec-886">[Service Bus AMQP overview]</span></span>
* <span data-ttu-id="e15ec-887">[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]</span><span class="sxs-lookup"><span data-stu-id="e15ec-887">[AMQP 1.0 support for Service Bus partitioned queues and topics]</span></span>
* <span data-ttu-id="e15ec-888">[Windows Server용 Service Bus의 AMQP]</span><span class="sxs-lookup"><span data-stu-id="e15ec-888">[AMQP in Service Bus for Windows Server]</span></span>

[Service Bus AMQP 개요]: service-bus-amqp-overview.md
[Service Bus 분할 큐 및 토픽에 대한 AMQP 1.0 지원]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server용 Service Bus의 AMQP]: https://msdn.microsoft.com/library/dn574799.asp