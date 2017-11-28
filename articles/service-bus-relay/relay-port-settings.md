---
title: "aaaAzure 릴레이 포트 설정 | Microsoft Docs"
description: "Azure Relay 포트 값에 대한 세부 정보입니다."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: e66785f786ee241c974d250f9ec29dfcc1fdc3fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="70ffe-103">Azure Relay 포트 설정</span><span class="sxs-lookup"><span data-stu-id="70ffe-103">Azure Relay port settings</span></span>

<span data-ttu-id="70ffe-104">hello 다음 표에 Azure 릴레이 대 한 포트 값에 대 한 hello 필수 구성을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="70ffe-104">hello following table describes hello required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="70ffe-105">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="70ffe-105">Hybrid Connections</span></span>
<span data-ttu-id="70ffe-106">하이브리드 연결 Websocket을 사용 하 여 기본 전송 메커니즘을 사용 하 여 hello로 **HTTPS** 만 합니다.</span><span class="sxs-lookup"><span data-stu-id="70ffe-106">Hybrid Connections uses WebSockets as hello underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="70ffe-107">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="70ffe-107">WCF Relays</span></span>
  
|<span data-ttu-id="70ffe-108">바인딩</span><span class="sxs-lookup"><span data-stu-id="70ffe-108">Binding</span></span>|<span data-ttu-id="70ffe-109">전송 보안</span><span class="sxs-lookup"><span data-stu-id="70ffe-109">Transport Security</span></span>|<span data-ttu-id="70ffe-110">포트</span><span class="sxs-lookup"><span data-stu-id="70ffe-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="70ffe-111">[BasicHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.basichttprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="70ffe-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="70ffe-112">예</span><span class="sxs-lookup"><span data-stu-id="70ffe-112">Yes</span></span>|<span data-ttu-id="70ffe-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70ffe-113">HTTPS</span></span>| 
| |<span data-ttu-id="70ffe-114">"</span><span class="sxs-lookup"><span data-stu-id="70ffe-114">"</span></span> |<span data-ttu-id="70ffe-115">아니요</span><span class="sxs-lookup"><span data-stu-id="70ffe-115">No</span></span>|<span data-ttu-id="70ffe-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-116">HTTP</span></span>|  
|<span data-ttu-id="70ffe-117">[BasicHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.basichttprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="70ffe-118">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-118">Either</span></span>|<span data-ttu-id="70ffe-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-119">9351/HTTP</span></span>|  
|<span data-ttu-id="70ffe-120">[NetEventRelayBinding 클래스](/dotnet/api/microsoft.servicebus.neteventrelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="70ffe-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="70ffe-121">예</span><span class="sxs-lookup"><span data-stu-id="70ffe-121">Yes</span></span>|<span data-ttu-id="70ffe-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="70ffe-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="70ffe-123">"</span><span class="sxs-lookup"><span data-stu-id="70ffe-123">"</span></span> |<span data-ttu-id="70ffe-124">아니요</span><span class="sxs-lookup"><span data-stu-id="70ffe-124">No</span></span>|<span data-ttu-id="70ffe-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-125">9350/HTTP</span></span>|  
|<span data-ttu-id="70ffe-126">[NetEventRelayBinding 클래스](/dotnet/api/microsoft.servicebus.neteventrelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="70ffe-127">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-127">Either</span></span>|<span data-ttu-id="70ffe-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-128">9351/HTTP</span></span>|  
|<span data-ttu-id="70ffe-129">[NetTcpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.nettcprelaybinding)(클라이언트/서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="70ffe-130">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-130">Either</span></span>|<span data-ttu-id="70ffe-131">5671/9352/HTTP(하이브리드를 사용하는 경우 9352/9353)</span><span class="sxs-lookup"><span data-stu-id="70ffe-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="70ffe-132">[NetOnewayRelayBinding 클래스](/dotnet/api/microsoft.servicebus.netonewayrelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="70ffe-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="70ffe-133">예</span><span class="sxs-lookup"><span data-stu-id="70ffe-133">Yes</span></span>|<span data-ttu-id="70ffe-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="70ffe-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="70ffe-135">"</span><span class="sxs-lookup"><span data-stu-id="70ffe-135">"</span></span> |<span data-ttu-id="70ffe-136">아니요</span><span class="sxs-lookup"><span data-stu-id="70ffe-136">No</span></span>|<span data-ttu-id="70ffe-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-137">9350/HTTP</span></span>|  
|<span data-ttu-id="70ffe-138">[NetOnewayRelayBinding 클래스](/dotnet/api/microsoft.servicebus.netonewayrelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="70ffe-139">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-139">Either</span></span>|<span data-ttu-id="70ffe-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-140">9351/HTTP</span></span>|  
|<span data-ttu-id="70ffe-141">[WebHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.webhttprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="70ffe-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="70ffe-142">예</span><span class="sxs-lookup"><span data-stu-id="70ffe-142">Yes</span></span>|<span data-ttu-id="70ffe-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70ffe-143">HTTPS</span></span>|  
||<span data-ttu-id="70ffe-144">"</span><span class="sxs-lookup"><span data-stu-id="70ffe-144">"</span></span> |<span data-ttu-id="70ffe-145">아니요</span><span class="sxs-lookup"><span data-stu-id="70ffe-145">No</span></span>|<span data-ttu-id="70ffe-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-146">HTTP</span></span>|  
|<span data-ttu-id="70ffe-147">[WebHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.webhttprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="70ffe-148">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-148">Either</span></span>|<span data-ttu-id="70ffe-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-149">9351/HTTP</span></span>|  
|<span data-ttu-id="70ffe-150">[WS2007HttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="70ffe-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="70ffe-151">예</span><span class="sxs-lookup"><span data-stu-id="70ffe-151">Yes</span></span>|<span data-ttu-id="70ffe-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70ffe-152">HTTPS</span></span>|  
||<span data-ttu-id="70ffe-153">"</span><span class="sxs-lookup"><span data-stu-id="70ffe-153">"</span></span> |<span data-ttu-id="70ffe-154">아니요</span><span class="sxs-lookup"><span data-stu-id="70ffe-154">No</span></span>|<span data-ttu-id="70ffe-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-155">HTTP</span></span>|  
|<span data-ttu-id="70ffe-156">[WS2007HttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="70ffe-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="70ffe-157">여기서는</span><span class="sxs-lookup"><span data-stu-id="70ffe-157">Either</span></span>|<span data-ttu-id="70ffe-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="70ffe-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="70ffe-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="70ffe-159">Next steps</span></span>
<span data-ttu-id="70ffe-160">다음이 링크를 방문 하는 Azure 릴레이 대 한 자세한 toolearn:</span><span class="sxs-lookup"><span data-stu-id="70ffe-160">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="70ffe-161">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="70ffe-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="70ffe-162">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="70ffe-162">Relay FAQ</span></span>](relay-faq.md)