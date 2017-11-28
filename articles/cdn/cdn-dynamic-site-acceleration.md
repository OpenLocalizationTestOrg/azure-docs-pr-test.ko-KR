---
title: "Azure CDN을 통해 동적 사이트 가속"
description: "동적 사이트 가속 심층 분석"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: v-semcev
ms.openlocfilehash: be2719e0e02c8bc69800ef4a3e7da3c3164cb9dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a><span data-ttu-id="732f4-103">Azure CDN을 통해 동적 사이트 가속</span><span class="sxs-lookup"><span data-stu-id="732f4-103">Dynamic Site Acceleration via Azure CDN</span></span>

<span data-ttu-id="732f4-104">소셜 미디어소셜 미디어, 전자 상거래 및 하이퍼 개인 설정 웹의 폭발적 증가로 인해 최종 사용자에게 제공되는 콘텐츠의 증가율도 실시간으로 빠르게 성장합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-104">With the explosion of social media, electronic commerce, and the hyper-personalized web, a rapidly increasing percentage of the content served to end users is generated in real time.</span></span> <span data-ttu-id="732f4-105">사용자는 브라우저, 위치, 장치 또는 네트워크와 독립된 빠르고 안정적인 개인 설정 웹 환경을 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-105">Users expect fast, reliable, and personalized web experiences, independent of their browser, location, device, or network.</span></span> <span data-ttu-id="732f4-106">그러나 이러한 환경을 구성하는 매우 혁신적인 기능도 페이지 다운로드 속도를 저하시키고 소비자 환경의 품질을 위험에 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-106">However, the very innovations that make these experiences so engaging also slow page downloads and put the quality of the consumer experience at risk.</span></span> 

<span data-ttu-id="732f4-107">표준 CDN 기능에는 고정 파일의 배달 속도를 향상시키기 위해 파일을 최종 사용자에게 가깝게 캐시하는 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-107">Standard CDN capability includes the ability to cache files closer to end users to speed up delivery of static files.</span></span> <span data-ttu-id="732f4-108">그러나 동적 웹 응용 프로그램에서 서버가 사용자 동작에 대한 응답으로 콘텐츠를 생성하기 때문에 에지 위치에 해당 콘텐츠를 캐싱할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-108">However, with dynamic web applications, caching that content in edge locations isn't possible because the server generates the content in response to user behavior.</span></span> <span data-ttu-id="732f4-109">이러한 콘텐츠의 배달 속도를 향상시키는 작업은 기존의 에지 캐싱보다 더 복잡하고 배달할 전체 데이터 경로에 있는 각 요소를 처음부터 세밀하게 조정하는 종단 간 솔루션이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-109">Speeding up the delivery of such content is more complex than traditional edge caching and requires an end-to-end solution that finely tunes each element along the entire data path from inception to delivery.</span></span> <span data-ttu-id="732f4-110">Azure CDN DSA(동적 사이트 가속)을 사용하여 동적 콘텐츠가 포함된 웹 페이지의 성능이 크게 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-110">With Azure CDN Dynamic Site Acceleration (DSA), the performance of web pages with dynamic content is measurably improved.</span></span>

<span data-ttu-id="732f4-111">Akamai 및 Verizon의 Azure CDN은 끝점을 만드는 동안 **최적화 목표** 메뉴를 통해 DSA 최적화를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-111">Azure CDN from Akamai and Verizon offers DSA optimization through the **Optimized for** menu during endpoint creation.</span></span>

## <a name="configuring-cdn-endpoint-to-accelerate-delivery-of-dynamic-files"></a><span data-ttu-id="732f4-112">동적 파일 배달을 가속화하도록 CDN 끝점 구성</span><span class="sxs-lookup"><span data-stu-id="732f4-112">Configuring CDN endpoint to accelerate delivery of dynamic files</span></span>

<span data-ttu-id="732f4-113">끝점을 만드는 동안 **최적화 목표** 속성 선택 영역에서 **동적 사이트 가속** 옵션을 선택하여 Azure Portal을 통해 동적 파일의 배달을 최적화하도록 CDN 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-113">You can configure your CDN endpoint to optimize delivery of dynamic files via Azure portal by selecting the **Dynamic site acceleration** option under the **Optimized for** property selection during the endpoint creation.</span></span> <span data-ttu-id="732f4-114">REST API나 클라이언트 SDK를 사용하여 프로그래밍 방식으로 같은 작업을 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-114">You can also use our REST APIs or any of the client SDKs to do the same thing programmatically.</span></span> 

### <a name="probe-path"></a><span data-ttu-id="732f4-115">프로브 경로</span><span class="sxs-lookup"><span data-stu-id="732f4-115">Probe path</span></span>
<span data-ttu-id="732f4-116">프로브 경로는 동적 사이트 가속에 지정된 기능이고 생성을 위해 유효한 프로브 경로가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-116">Probe path is a feature specific to Dynamic Site Acceleration, and a valid one is required for creation.</span></span> <span data-ttu-id="732f4-117">DSA는 원본에 위치한 작은 *프로브 경로* 파일을 사용하여 CDN에 대한 네트워크 라우팅 구성을 최적화합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-117">DSA uses a small *probe path* file placed on the origin to optimize network routing configurations for the CDN.</span></span> <span data-ttu-id="732f4-118">사이트에 샘플 파일을 다운로드하고 업로드하거나 약 10KB인 원본의 기존 자산이 있는 경우 프로브 경로에 대신 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-118">You can download and upload our sample file to your site, or use an existing asset on your origin that is roughly 10 KB for the probe path instead if the asset exists.</span></span>

> [!Note]
> <span data-ttu-id="732f4-119">DSA 사용 시 별도 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-119">DSA incurs extra charges.</span></span> <span data-ttu-id="732f4-120">자세한 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cdn/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="732f4-120">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/cdn/) for more information.</span></span>

<span data-ttu-id="732f4-121">다음 스크린샷에서는 Azure Portal을 통한 프로세스를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-121">The following screenshots illustrate the process via Azure portal.</span></span>
 
![새 CDN 끝점 추가](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

<span data-ttu-id="732f4-123">*그림 1: CDN 프로필에서 새 CDN 끝점 추가*</span><span class="sxs-lookup"><span data-stu-id="732f4-123">*Figure 1: Adding a new CDN endpoint from the CDN Profile*</span></span>
 
![DSA를 사용하여 새 CDN 끝점 만들기](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

<span data-ttu-id="732f4-125">*그림 2: 동적 사이트 가속 최적화가 선택된 CDN 끝점 만들기*</span><span class="sxs-lookup"><span data-stu-id="732f4-125">*Figure 2: Creating a CDN Endpoint with Dynamic site acceleration Optimization selected*</span></span>

<span data-ttu-id="732f4-126">CDN 끝점을 만든 다음에는 특정 조건에 맞는 모든 파일에 대해 DSA 최적화를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-126">Once the CDN endpoint is created, it applies the DSA optimizations for all files that match certain criteria.</span></span> <span data-ttu-id="732f4-127">다음 섹션에서는 DSA 최적화에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-127">The following section describes DSA optimization in detail.</span></span>

## <a name="dsa-optimization-using-azure-cdn"></a><span data-ttu-id="732f4-128">Azure CDN을 사용하여 DSA 최적화</span><span class="sxs-lookup"><span data-stu-id="732f4-128">DSA Optimization using Azure CDN</span></span>

<span data-ttu-id="732f4-129">Azure CDN의 동적 사이트 가속을 통해 다음 기술을 사용하는 동적 자산 배달 속도가 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-129">Dynamic Site Acceleration on Azure CDN speeds up delivery of dynamic assets using the following techniques:</span></span>

-   <span data-ttu-id="732f4-130">경로 최적화</span><span class="sxs-lookup"><span data-stu-id="732f4-130">Route Optimization</span></span>
-   <span data-ttu-id="732f4-131">TCP 최적화</span><span class="sxs-lookup"><span data-stu-id="732f4-131">TCP Optimizations</span></span>
-   <span data-ttu-id="732f4-132">개체 사전 인출(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="732f4-132">Object Prefetch (Akamai only)</span></span>
-   <span data-ttu-id="732f4-133">모바일 이미지 압축(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="732f4-133">Mobile Image Compression (Akamai only)</span></span>

### <a name="route-optimization"></a><span data-ttu-id="732f4-134">경로 최적화</span><span class="sxs-lookup"><span data-stu-id="732f4-134">Route Optimization</span></span>

<span data-ttu-id="732f4-135">인터넷이 매우 동적이기 때문에 경로 최적화가 중요합니다. 여기서 트래픽 및 일시적인 중단은 지속적으로 네트워크 토폴로지를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-135">Route optimization is important because the Internet is a dynamic place, where traffic and temporarily outages are constantly changing the network topology.</span></span> <span data-ttu-id="732f4-136">BGP(경계 게이트웨이 프로토콜)는 인터넷의 라우팅 프로토콜이지만 중계 PoP(Point of Presence) 서버를 통한 더 빠른 경로가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-136">The Border Gateway Protocol (BGP) is the routing protocol of the Internet, but there may be faster routes via intermediary Point of Presence (PoP) servers.</span></span> 

<span data-ttu-id="732f4-137">경로 최적화는 사이트에 계속 액세스할 수 있고 동적 콘텐츠를 가능한 가장 빠르고 가장 안정적인 경로를 통해 최종 사용자에게 배달하도록 원본에 최적인 경로를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-137">Route optimization chooses the most optimal path to the origin so that a site is continuously accessible and dynamic content is delivered to end users via the fastest and most reliable route possible.</span></span> 

<span data-ttu-id="732f4-138">Akamai 네트워크는 원본과 CDN 에지 간에 가장 빠른 경로를 결정하기 위해 오픈 인터넷에 기본 BGP 경로를 사용할 뿐만 아니라 실시간 데이터를 수집하고 Akamai 서버에서 다른 노드를 통한 다양한 경로를 비교하는 기술을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-138">The Akamai network uses techniques to collect real-time data and compare various paths through different nodes in the Akamai server, as well as the default BGP route across the open Internet to determine the fastest route between the origin and the CDN edge.</span></span> <span data-ttu-id="732f4-139">이러한 기술은 인터넷 정체 지점과 긴 경로를 회피합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-139">These techniques avoid Internet congestion points and long routes.</span></span> 

<span data-ttu-id="732f4-140">마찬가지로, Verizon 네트워크는 Anycast DNS, 고용량 지원 PoP 및 상태 점검 조합을 사용하여 클라이언트에서 원본까지 최상의 경로 데이터에 대한 최적의 게이트웨이를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-140">Similarly, the Verizon network uses a combination of Anycast DNS, high capacity support PoPs, and health checks, to determine the best gateways to best route data from the client to the origin.</span></span>
 
<span data-ttu-id="732f4-141">결과적으로 완전히 동적인 트랜잭션 콘텐츠를 캐시할 수 없는 경우에도 보다 빠르고 안정적으로 최종 사용자에게 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-141">As a result, fully dynamic and transactional content is delivered more quickly and more reliably to end users, even when it is uncacheable.</span></span> 

### <a name="tcp-optimizations"></a><span data-ttu-id="732f4-142">TCP 최적화</span><span class="sxs-lookup"><span data-stu-id="732f4-142">TCP Optimizations</span></span>

<span data-ttu-id="732f4-143">TCP(Transmission Control Protocol)는 IP 네트워크의 응용 프로그램 간에 정보를 전달하는 데 사용되는 인터넷 프로토콜 모음의 표준입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-143">Transmission Control Protocol (TCP) is the standard of the Internet protocol suite used to deliver information between applications on an IP network.</span></span>  <span data-ttu-id="732f4-144">기본적으로 대규모의 비효율성이 발생하는 네트워크 정체를 방지하는 제한뿐만 아니라 TCP 연결을 설정하는 데 필요한 몇 가지 요청이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-144">By default, there are several back and forth requests required to set up a TCP connection, as well as limits to avoid network congestions, which result in inefficiencies at scale.</span></span> <span data-ttu-id="732f4-145">Akamai의 Azure CDN은 3개의 영역을 최적화하여 이 문제를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-145">Azure CDN from Akamai deals with this problem by optimizing in three areas:</span></span> 

 - <span data-ttu-id="732f4-146">느린 시작 제거</span><span class="sxs-lookup"><span data-stu-id="732f4-146">eliminating slow start</span></span>
 - <span data-ttu-id="732f4-147">영구 연결 활용</span><span class="sxs-lookup"><span data-stu-id="732f4-147">leveraging persistent connections</span></span>
 - <span data-ttu-id="732f4-148">TCP 패킷 매개 변수 조정(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="732f4-148">tuning TCP packet parameters (Akamai only)</span></span>

#### <a name="eliminating-slow-start"></a><span data-ttu-id="732f4-149">느린 시작 제거</span><span class="sxs-lookup"><span data-stu-id="732f4-149">Eliminating slow start</span></span>

<span data-ttu-id="732f4-150">*느린 시작*은 네트워크를 통해 전송되는 데이터 양을 제한하여 네트워크 정체를 방지하는 TCP 프로토콜의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-150">*Slow start* is a part of the TCP protocol that prevents network congestion by limiting the amount of data sent over the network.</span></span> <span data-ttu-id="732f4-151">이 기능은 최대값에 도달하거나 패킷 손실이 감지될 때까지 먼저 발신자와 수신자 사이의 작은 정체 창 크기로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-151">It starts off with small congestion window sizes between sender and receiver until the maximum is reached or packet loss is detected.</span></span>

<span data-ttu-id="732f4-152">Akamai 및 Verizon의 Azure CDN은 세 단계로 느린 시작을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-152">Azure CDN from Akamai and Verizon eliminates slow start in three steps:</span></span>

1.  <span data-ttu-id="732f4-153">Akamai와 Verizon의 네트워크 모두 상태 및 대역폭 모니터링을 사용하여 에지 PoP 서버 간 연결의 대역폭을 측정합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-153">Both Akamai and Verizon's network use health and bandwidth monitoring to measure the bandwidth of connections between edge PoP servers.</span></span>
2. <span data-ttu-id="732f4-154">에지 PoP 서버 간에 메트릭이 공유되므로 서버는 주위의 다른 PoP의 네트워크 조건 및 서버 상태에 대해 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-154">The metrics are shared between edge PoP servers so that each server is aware of the network conditions and server health of the other PoPs around them.</span></span>  
3. <span data-ttu-id="732f4-155">이제 CDN 에지 서버는 근접한 다른 CDN 에지 서버와 통신할 때 최적의 창 크기와 같은 일부 전송 매개 변수에 대해 가정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-155">The CDN edge servers are now able to make assumptions about some transmission parameters, such as what the optimal window size should be when communicating with other CDN edge servers in its proximity.</span></span> <span data-ttu-id="732f4-156">이 단계는 CDN 에지 서버 간의 연결 상태가 더 많은 패킷의 데이터를 전송할 수 있는 경우 초기 정체 창 크기를 늘릴 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-156">This step means that the initial congestion window size can be increased if the health of the connection between the CDN edge servers is capable of higher packet data transfers.</span></span>  

#### <a name="leveraging-persistent-connections"></a><span data-ttu-id="732f4-157">영구 연결 활용</span><span class="sxs-lookup"><span data-stu-id="732f4-157">Leveraging persistent connections</span></span>

<span data-ttu-id="732f4-158">CDN을 사용하면 원본에 직접 연결된 사용자와 비교하여 원본 서버에 연결된 고유한 컴퓨터 수가 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-158">Using a CDN, fewer unique machines connect to your origin server directly compared with users connecting directly to your origin.</span></span> <span data-ttu-id="732f4-159">또한 Akamai 및 Verizon의 Azure CDN은 사용자 요청을 풀링하여 원본과 연결 수를 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-159">Azure CDN from Akamai and Verizon also pools user requests together to establish fewer connections with the origin.</span></span>

<span data-ttu-id="732f4-160">앞서 언급했듯이 TCP 연결에는 새 연결을 설정하는 과정에서 몇 가지 요청을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-160">As mentioned earlier, TCP connections take several requests back and forth in a handshake to establish a new connection.</span></span> <span data-ttu-id="732f4-161">"HTTP 연결 유지"라고도 하는 영구 연결은 여러 HTTP 요청에 기존 TCP 연결을 다시 사용하여 왕복 시간을 저장하고 배달 속도를 향상시킵니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-161">Persistent connections, also known as "HTTP Keep-Alive," reuse existing TCP connections for multiple HTTP requests to save round-trip times and speed up delivery.</span></span> 

<span data-ttu-id="732f4-162">또한 Verizon 네트워크는 TCP 연결을 통해 정기적인 연결 유지 패킷을 보내 열린 연결이 닫히지 않게 해줍니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-162">The Verizon network also sends periodic keep-alive packets over the TCP connection to prevent an open connection from being closed.</span></span>

#### <a name="tuning-tcp-packet-parameters"></a><span data-ttu-id="732f4-163">TCP 패킷 매개 변수 조정</span><span class="sxs-lookup"><span data-stu-id="732f4-163">Tuning TCP packet parameters</span></span>

<span data-ttu-id="732f4-164">또한 Akamai에서 Azure CDN은 서버 간 연결을 제어하는 매개 변수를 조정하고 다음 기법을 수행하여 사이트에서 포함된 콘텐츠를 검색하는 데 필요한 긴 장거리 왕복 시간을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-164">Azure CDN from Akamai also tunes the parameters that govern server-to-server connections, and reduces the amount of long haul round trips required to retrieve content embedded in the site by using the following techniques:</span></span>

1.  <span data-ttu-id="732f4-165">초기 정체 창을 증가시키면 승인을 기다리지 않고 더 패킷을 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-165">Increasing the initial congestion window so that more packets can be sent without waiting for an acknowledgement.</span></span>
2.  <span data-ttu-id="732f4-166">초기 재전송 시간 제한을 감소시키면 손실을 감지하고 재전송을 더 빠르게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-166">Decreasing the initial retransmit timeout so that a loss is detected, and retransmission occurs more quickly.</span></span>
3.  <span data-ttu-id="732f4-167">전송 중에 손실된 패킷을 가정하기 전에 대기 시간을 줄이기 위해 최소 및 최대 재전송 시간 제한을 감소시킵니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-167">Decreasing the minimum and maximum retransmit timeout to reduce the wait time before assuming packets were lost in transmission.</span></span>

### <a name="object-prefetch-akamai-only"></a><span data-ttu-id="732f4-168">개체 사전 인출(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="732f4-168">Object Prefetch (Akamai only)</span></span>

<span data-ttu-id="732f4-169">대부분의 웹 사이트는 이미지 및 스크립트와 같은 다양한 리소스를 참조하는 HTML 페이지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-169">Most websites consist of an HTML page, which references various other resources such as images and scripts.</span></span> <span data-ttu-id="732f4-170">일반적으로 클라이언트가 웹 페이지를 요청하면 브라우저는 먼저 HTML 개체를 다운로드하고 구문을 분석한 다음 전체 페이지를 로드하는 데 필요한 연결된 자산을 추가로 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-170">Typically, when a client requests a webpage, the browser first downloads and parses the HTML object, and then makes additional requests to linked assets that are required to fully load the page.</span></span> 

<span data-ttu-id="732f4-171">*사전 인출*은 HTML이 브라우저에 제공되는 반면 브라우저에서 이러한 개체를 요청하기 전에 HTML 페이지에 포함된 이미지 및 스크립트를 검색하는 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-171">*Prefetch* is a technique to retrieve images and scripts embedded in the HTML page while the HTML is served to the browser, and before the browser even makes these object requests.</span></span> 

<span data-ttu-id="732f4-172">사전 인출에서 **사전 인출** 옵션은 CDN이 HTML 기반 페이지를 클라이언트의 브라우저에 제공하는 시점에 켜집니다. CDN은 HTML 파일의 구문을 분석하고, 연결된 리소스를 추가로 요청하고, 해당 캐시에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-172">With the **prefetch** option turned on at the time when the CDN serves the HTML base page to the client’s browser, the CDN parses the HTML file and make additional requests for any linked resources and store it in its cache.</span></span> <span data-ttu-id="732f4-173">클라이언트에서 연결된 자산을 요청하는 경우 CDN 에지 서버에는 이미 요청된 개체가 있으므로 원본에 왕복하지 않고 즉시 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-173">When the client makes the requests for the linked assets, the CDN edge server already has the requested objects and can serve them immediately without a round trip to the origin.</span></span> <span data-ttu-id="732f4-174">이 최적화는 캐시할 수 있는 콘텐츠 및 캐시할 수 없는 콘텐츠에 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-174">This optimization benefits both cacheable and non-cacheable content.</span></span>

### <a name="adaptive-image-compression-akamai-only"></a><span data-ttu-id="732f4-175">적응 이미지 압축(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="732f4-175">Adaptive Image Compression (Akamai only)</span></span>

<span data-ttu-id="732f4-176">특히 모바일과 같은 일부 장치는 때때로 네트워크 속도가 저하되는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-176">Some devices, especially mobile ones, experience slower network speeds from time to time.</span></span> <span data-ttu-id="732f4-177">이러한 시나리오에서는 사용자가 고해상도 이미지를 오래 기다리지 않고 해당 웹 페이지에서 작은 이미지를 신속하게 수신할 수 있다는 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-177">In these scenarios, it is more beneficial for the user to receive smaller images in their webpage more quickly rather than waiting a long time for full resolution images.</span></span>

<span data-ttu-id="732f4-178">이 기능은 자동으로 네트워크 품질을 모니터링하여 네트워크가 느려지는 경우 배달 속도를 개선하기 위해 표준 JPEG 압축 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-178">This feature automatically monitors network quality, and employs standard JPEG compression methods when network speeds are slower to improve delivery time.</span></span>

<span data-ttu-id="732f4-179">적응 이미지 압축</span><span class="sxs-lookup"><span data-stu-id="732f4-179">Adaptive Image Compression</span></span> | <span data-ttu-id="732f4-180">파일 확장명</span><span class="sxs-lookup"><span data-stu-id="732f4-180">File Extensions</span></span>  
--- | ---  
<span data-ttu-id="732f4-181">JPEG 압축</span><span class="sxs-lookup"><span data-stu-id="732f4-181">JPEG compression</span></span> | <span data-ttu-id="732f4-182">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span><span class="sxs-lookup"><span data-stu-id="732f4-182">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span></span>

## <a name="caching"></a><span data-ttu-id="732f4-183">구성</span><span class="sxs-lookup"><span data-stu-id="732f4-183">Caching</span></span>

<span data-ttu-id="732f4-184">원본에 캐시 컨트롤을 포함하고 응답에서 헤더가 만료된 경우에도 DSA를 통해 캐싱이 CDN에서 기본적으로 해제되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-184">With DSA, caching is turned off by default on the CDN, even when the origin includes cache-control/expires headers in the response.</span></span> <span data-ttu-id="732f4-185">DSA는 각 클라이언트에 고유하므로 캐싱되어서는 안 되는 일반적으로 동적 자산에 사용되기 때문에 이 기본값은 해제되어 있으며, 기본값으로 캐싱을 설정하면 이 기능이 중단될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-185">This default is turned off because DSA is typically used for dynamic assets that should not be cached since they are unique to each client, and turning on caching by default can break this behavior.</span></span>

<span data-ttu-id="732f4-186">고정 자산과 동적 자산이 혼합된 웹 사이트가 있는 경우 최상의 성능을 얻기 위해서는 하이브리드 접근 방식을 취하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-186">If you have a website with a mix of static and dynamic assets, it is best to take a hybrid approach to get the best performance.</span></span> 

<span data-ttu-id="732f4-187">Verizon Premium에 ADN을 사용하고 있는 경우 규칙 엔진을 사용하여 특정 사례에 캐싱을 다시 사용 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-187">If you are using ADN with Verizon Premium, you can turn caching back on for specific cases using the Rules Engine.</span></span>  

<span data-ttu-id="732f4-188">대안은 2개의 CDN 끝점을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-188">An alternative is to use two CDN endpoints.</span></span> <span data-ttu-id="732f4-189">DSA 지원 끝점은 동적 자산을 제공하고, 일반 웹 제공 등의 고정 최적화 유형의 다른 끝점은 캐싱 가능한 자산을 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-189">One with DSA to deliver dynamic assets, and another endpoint with a static optimization type, such as general web delivery, to delivery cacheable assets.</span></span> <span data-ttu-id="732f4-190">이 대안을 달성하려면 웹 페이지 URL을 수정하여 사용하려는 CDN 끝점의 자산에 직접 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-190">In order to accomplish this alternative, you will modify your webpage URLs to link directly to the asset on the CDN endpoint you plan to use.</span></span> 

<span data-ttu-id="732f4-191">예: `mydynamic.azureedge.net/index.html`은 동적 페이지이고 DSA 끝점에서 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-191">For example: `mydynamic.azureedge.net/index.html` is a dynamic page and is loaded from the DSA endpoint.</span></span>  <span data-ttu-id="732f4-192">html 페이지는 `mystatic.azureedge.net/banner.jpg` 및 `mystatic.azureedge.net/scripts.js` 등의 정적 CDN 끝점에서 로드한 JavaScript 라이브러리 또는 이미지와 같은 여러 정적 자산을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-192">The html page references multiple static assets such as JavaScript libraries or images that are loaded from the static CDN endpoint, such as `mystatic.azureedge.net/banner.jpg` and `mystatic.azureedge.net/scripts.js`.</span></span> 

<span data-ttu-id="732f4-193">ASP.NET 웹 응용 프로그램의 컨트롤러를 사용하여 특정 CDN URL을 통해 콘텐츠를 제공하는 방법은 [여기](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller)에서 예를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="732f4-193">You can find an example [here](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) on how to use controllers in an ASP.NET web application to serve content through a specific CDN URL.</span></span>




