---
title: "Azure Relay 포트 설정 | Microsoft Docs"
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
ms.openlocfilehash: 5906495c565dad583e74a43b2e5eed57e0c68df1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-port-settings"></a><span data-ttu-id="2c15d-103">Azure Relay 포트 설정</span><span class="sxs-lookup"><span data-stu-id="2c15d-103">Azure Relay port settings</span></span>

<span data-ttu-id="2c15d-104">다음 표에서는 Azure Relay의 포트 값에 필요한 구성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15d-104">The following table describes the required configuration for port values for Azure Relay.</span></span>

## <a name="hybrid-connections"></a><span data-ttu-id="2c15d-105">하이브리드 연결</span><span class="sxs-lookup"><span data-stu-id="2c15d-105">Hybrid Connections</span></span>
<span data-ttu-id="2c15d-106">하이브리드 연결은 기본 전송 메커니즘으로 **HTTPS**만 사용하는 WebSockets을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15d-106">Hybrid Connections uses WebSockets as the underlying transport mechanism, which uses **HTTPS** only.</span></span> 

## <a name="wcf-relays"></a><span data-ttu-id="2c15d-107">WCF 릴레이</span><span class="sxs-lookup"><span data-stu-id="2c15d-107">WCF Relays</span></span>
  
|<span data-ttu-id="2c15d-108">바인딩</span><span class="sxs-lookup"><span data-stu-id="2c15d-108">Binding</span></span>|<span data-ttu-id="2c15d-109">전송 보안</span><span class="sxs-lookup"><span data-stu-id="2c15d-109">Transport Security</span></span>|<span data-ttu-id="2c15d-110">포트</span><span class="sxs-lookup"><span data-stu-id="2c15d-110">Port</span></span>|  
|-------------|------------------------|----------|  
|<span data-ttu-id="2c15d-111">[BasicHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.basichttprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="2c15d-111">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (client)</span></span>|<span data-ttu-id="2c15d-112">예</span><span class="sxs-lookup"><span data-stu-id="2c15d-112">Yes</span></span>|<span data-ttu-id="2c15d-113">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2c15d-113">HTTPS</span></span>| 
| |<span data-ttu-id="2c15d-114">"</span><span class="sxs-lookup"><span data-stu-id="2c15d-114">"</span></span> |<span data-ttu-id="2c15d-115">아니요</span><span class="sxs-lookup"><span data-stu-id="2c15d-115">No</span></span>|<span data-ttu-id="2c15d-116">HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-116">HTTP</span></span>|  
|<span data-ttu-id="2c15d-117">[BasicHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.basichttprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-117">[BasicHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.basichttprelaybinding) (service)</span></span>|<span data-ttu-id="2c15d-118">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-118">Either</span></span>|<span data-ttu-id="2c15d-119">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-119">9351/HTTP</span></span>|  
|<span data-ttu-id="2c15d-120">[NetEventRelayBinding 클래스](/dotnet/api/microsoft.servicebus.neteventrelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="2c15d-120">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (client)</span></span>|<span data-ttu-id="2c15d-121">예</span><span class="sxs-lookup"><span data-stu-id="2c15d-121">Yes</span></span>|<span data-ttu-id="2c15d-122">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="2c15d-122">9351/HTTPS</span></span>|  
||<span data-ttu-id="2c15d-123">"</span><span class="sxs-lookup"><span data-stu-id="2c15d-123">"</span></span> |<span data-ttu-id="2c15d-124">아니요</span><span class="sxs-lookup"><span data-stu-id="2c15d-124">No</span></span>|<span data-ttu-id="2c15d-125">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-125">9350/HTTP</span></span>|  
|<span data-ttu-id="2c15d-126">[NetEventRelayBinding 클래스](/dotnet/api/microsoft.servicebus.neteventrelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-126">[NetEventRelayBinding Class](/dotnet/api/microsoft.servicebus.neteventrelaybinding) (service)</span></span>|<span data-ttu-id="2c15d-127">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-127">Either</span></span>|<span data-ttu-id="2c15d-128">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-128">9351/HTTP</span></span>|  
|<span data-ttu-id="2c15d-129">[NetTcpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.nettcprelaybinding)(클라이언트/서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-129">[NetTcpRelayBinding Class](/dotnet/api/microsoft.servicebus.nettcprelaybinding) (client/service)</span></span>|<span data-ttu-id="2c15d-130">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-130">Either</span></span>|<span data-ttu-id="2c15d-131">5671/9352/HTTP(하이브리드를 사용하는 경우 9352/9353)</span><span class="sxs-lookup"><span data-stu-id="2c15d-131">5671/9352/HTTP (9352/9353 if using hybrid)</span></span>|  
|<span data-ttu-id="2c15d-132">[NetOnewayRelayBinding 클래스](/dotnet/api/microsoft.servicebus.netonewayrelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="2c15d-132">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (client)</span></span>|<span data-ttu-id="2c15d-133">예</span><span class="sxs-lookup"><span data-stu-id="2c15d-133">Yes</span></span>|<span data-ttu-id="2c15d-134">9351/HTTPS</span><span class="sxs-lookup"><span data-stu-id="2c15d-134">9351/HTTPS</span></span>|  
||<span data-ttu-id="2c15d-135">"</span><span class="sxs-lookup"><span data-stu-id="2c15d-135">"</span></span> |<span data-ttu-id="2c15d-136">아니요</span><span class="sxs-lookup"><span data-stu-id="2c15d-136">No</span></span>|<span data-ttu-id="2c15d-137">9350/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-137">9350/HTTP</span></span>|  
|<span data-ttu-id="2c15d-138">[NetOnewayRelayBinding 클래스](/dotnet/api/microsoft.servicebus.netonewayrelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-138">[NetOnewayRelayBinding Class](/dotnet/api/microsoft.servicebus.netonewayrelaybinding) (service)</span></span>|<span data-ttu-id="2c15d-139">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-139">Either</span></span>|<span data-ttu-id="2c15d-140">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-140">9351/HTTP</span></span>|  
|<span data-ttu-id="2c15d-141">[WebHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.webhttprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="2c15d-141">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (client)</span></span>|<span data-ttu-id="2c15d-142">예</span><span class="sxs-lookup"><span data-stu-id="2c15d-142">Yes</span></span>|<span data-ttu-id="2c15d-143">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2c15d-143">HTTPS</span></span>|  
||<span data-ttu-id="2c15d-144">"</span><span class="sxs-lookup"><span data-stu-id="2c15d-144">"</span></span> |<span data-ttu-id="2c15d-145">아니요</span><span class="sxs-lookup"><span data-stu-id="2c15d-145">No</span></span>|<span data-ttu-id="2c15d-146">HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-146">HTTP</span></span>|  
|<span data-ttu-id="2c15d-147">[WebHttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.webhttprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-147">[WebHttpRelayBinding Class](/dotnet/api/microsoft.servicebus.webhttprelaybinding) (service)</span></span>|<span data-ttu-id="2c15d-148">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-148">Either</span></span>|<span data-ttu-id="2c15d-149">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-149">9351/HTTP</span></span>|  
|<span data-ttu-id="2c15d-150">[WS2007HttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)(클라이언트)</span><span class="sxs-lookup"><span data-stu-id="2c15d-150">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (client)</span></span>|<span data-ttu-id="2c15d-151">예</span><span class="sxs-lookup"><span data-stu-id="2c15d-151">Yes</span></span>|<span data-ttu-id="2c15d-152">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2c15d-152">HTTPS</span></span>|  
||<span data-ttu-id="2c15d-153">"</span><span class="sxs-lookup"><span data-stu-id="2c15d-153">"</span></span> |<span data-ttu-id="2c15d-154">아니요</span><span class="sxs-lookup"><span data-stu-id="2c15d-154">No</span></span>|<span data-ttu-id="2c15d-155">HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-155">HTTP</span></span>|  
|<span data-ttu-id="2c15d-156">[WS2007HttpRelayBinding 클래스](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)(서비스)</span><span class="sxs-lookup"><span data-stu-id="2c15d-156">[WS2007HttpRelayBinding Class](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding) (service)</span></span>|<span data-ttu-id="2c15d-157">여기서는</span><span class="sxs-lookup"><span data-stu-id="2c15d-157">Either</span></span>|<span data-ttu-id="2c15d-158">9351/HTTP</span><span class="sxs-lookup"><span data-stu-id="2c15d-158">9351/HTTP</span></span>|

## <a name="next-steps"></a><span data-ttu-id="2c15d-159">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c15d-159">Next steps</span></span>
<span data-ttu-id="2c15d-160">Azure Relay에 대한 자세한 내용은 다음 링크를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="2c15d-160">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="2c15d-161">Azure 릴레이란?</span><span class="sxs-lookup"><span data-stu-id="2c15d-161">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="2c15d-162">릴레이 FAQ</span><span class="sxs-lookup"><span data-stu-id="2c15d-162">Relay FAQ</span></span>](relay-faq.md)