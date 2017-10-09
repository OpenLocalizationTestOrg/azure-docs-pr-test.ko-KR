---
title: "Azure CDN을 통해 사이트 가속 aaaDynamic"
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
ms.openlocfilehash: 37e6312ae5e83448f2d87c95ef48c387355748bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-site-acceleration-via-azure-cdn"></a><span data-ttu-id="bbde2-103">Azure CDN을 통해 동적 사이트 가속</span><span class="sxs-lookup"><span data-stu-id="bbde2-103">Dynamic Site Acceleration via Azure CDN</span></span>

<span data-ttu-id="bbde2-104">소셜 미디어, 전자 상거래 및 hello 하이퍼 개인 설정 웹 hello 폭발, 빠르게 증가 백분율로 hello 콘텐츠 tooend 사용자 제공은 실시간으로 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-104">With hello explosion of social media, electronic commerce, and hello hyper-personalized web, a rapidly increasing percentage of hello content served tooend users is generated in real time.</span></span> <span data-ttu-id="bbde2-105">사용자는 브라우저, 위치, 장치 또는 네트워크와 독립된 빠르고 안정적인 개인 설정 웹 환경을 기대합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-105">Users expect fast, reliable, and personalized web experiences, independent of their browser, location, device, or network.</span></span> <span data-ttu-id="bbde2-106">그러나 또한 참여 하므로 이러한 환경을 구성 하는 hello 매우 혁신적이 대 한 느린 페이지 다운로드 하 고 hello 소비자 환경의 hello 품질 위험에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-106">However, hello very innovations that make these experiences so engaging also slow page downloads and put hello quality of hello consumer experience at risk.</span></span> 

<span data-ttu-id="bbde2-107">표준 CDN 기능 hello 기능 toocache 파일 자세히 tooend 사용자 toospeed 정적 파일 배달을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-107">Standard CDN capability includes hello ability toocache files closer tooend users toospeed up delivery of static files.</span></span> <span data-ttu-id="bbde2-108">그러나 동적 웹 응용 프로그램과 함께 가장자리 위치에서 해당 콘텐츠를 캐싱하 수는 없습니다 hello 서버 응답 toouser 동작이 hello 콘텐츠를 생성 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-108">However, with dynamic web applications, caching that content in edge locations isn't possible because hello server generates hello content in response toouser behavior.</span></span> <span data-ttu-id="bbde2-109">이러한 콘텐츠의 hello 배달 속도 기존의 지 캐싱 보다 더 복잡 한 고 각 요소에서 초기 toodelivery hello 전체 데이터 경로 따라 정밀 하 게 조정 하는 종단 간 솔루션 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-109">Speeding up hello delivery of such content is more complex than traditional edge caching and requires an end-to-end solution that finely tunes each element along hello entire data path from inception toodelivery.</span></span> <span data-ttu-id="bbde2-110">Azure CDN 동적 사이트 Acceleration (DSA)와 함께, 동적 콘텐츠가 포함 된 웹 페이지의 hello 성능은 눈에 띄게 향상 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-110">With Azure CDN Dynamic Site Acceleration (DSA), hello performance of web pages with dynamic content is measurably improved.</span></span>

<span data-ttu-id="bbde2-111">Akamai 및 Verizon에서 azure CDN은 hello 통해 DSA 최적화를 제공 **에 대 한 액세스에 최적화 된** 메뉴 끝점을 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-111">Azure CDN from Akamai and Verizon offers DSA optimization through hello **Optimized for** menu during endpoint creation.</span></span>

## <a name="configuring-cdn-endpoint-tooaccelerate-delivery-of-dynamic-files"></a><span data-ttu-id="bbde2-112">CDN 끝점 tooaccelerate 배달을 동적 파일의 구성</span><span class="sxs-lookup"><span data-stu-id="bbde2-112">Configuring CDN endpoint tooaccelerate delivery of dynamic files</span></span>

<span data-ttu-id="bbde2-113">Azure 포털을 통해 동적 파일의 CDN 끝점 toooptimize 배송 hello를 선택 하 여 구성할 수 있습니다 **동적 사이트 가속** hello 옵션 **에 대 한 액세스에 최적화 된** 하는 동안 속성 선택 hello 끝점을 만드는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-113">You can configure your CDN endpoint toooptimize delivery of dynamic files via Azure portal by selecting hello **Dynamic site acceleration** option under hello **Optimized for** property selection during hello endpoint creation.</span></span> <span data-ttu-id="bbde2-114">또한 REST Api를 사용할 수 있습니다 또는 동일한 작업을 프로그래밍 방식으로 hello hello 클라이언트 Sdk toodo 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-114">You can also use our REST APIs or any of hello client SDKs toodo hello same thing programmatically.</span></span> 

### <a name="probe-path"></a><span data-ttu-id="bbde2-115">프로브 경로</span><span class="sxs-lookup"><span data-stu-id="bbde2-115">Probe path</span></span>
<span data-ttu-id="bbde2-116">프로브 경로 사이트 가속 기능 특정 tooDynamic 되며 올바른 만들기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-116">Probe path is a feature specific tooDynamic Site Acceleration, and a valid one is required for creation.</span></span> <span data-ttu-id="bbde2-117">DSA 작은 사용 하 여 *프로브 경로* hello 원점 toooptimize 네트워크 라우팅 구성에 대해 CDN hello 파일 배치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-117">DSA uses a small *probe path* file placed on hello origin toooptimize network routing configurations for hello CDN.</span></span> <span data-ttu-id="bbde2-118">다운로드 하 고 우리의 샘플 파일 tooyour 사이트를 업로드 하거나 약 10KB hello 프로브 경로 대 한 대신가 있는 경우 hello 자산 원본에서 기존 자산을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-118">You can download and upload our sample file tooyour site, or use an existing asset on your origin that is roughly 10 KB for hello probe path instead if hello asset exists.</span></span>

> [!Note]
> <span data-ttu-id="bbde2-119">DSA 사용 시 별도 요금이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-119">DSA incurs extra charges.</span></span> <span data-ttu-id="bbde2-120">자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cdn/) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-120">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/cdn/) for more information.</span></span>

<span data-ttu-id="bbde2-121">다음 스크린 샷을 hello Azure 포털을 통해 hello 과정을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-121">hello following screenshots illustrate hello process via Azure portal.</span></span>
 
![새 CDN 끝점 추가](./media/cdn-dynamic-site-acceleration/01_Endpoint_Profile.png) 

<span data-ttu-id="bbde2-123">*그림 1: hello CDN 프로필에서에서 새 CDN 끝점 추가*</span><span class="sxs-lookup"><span data-stu-id="bbde2-123">*Figure 1: Adding a new CDN endpoint from hello CDN Profile*</span></span>
 
![DSA를 사용하여 새 CDN 끝점 만들기](./media/cdn-dynamic-site-acceleration/02_Optimized_DSA.png)  

<span data-ttu-id="bbde2-125">*그림 2: 동적 사이트 가속 최적화가 선택된 CDN 끝점 만들기*</span><span class="sxs-lookup"><span data-stu-id="bbde2-125">*Figure 2: Creating a CDN Endpoint with Dynamic site acceleration Optimization selected*</span></span>

<span data-ttu-id="bbde2-126">Hello CDN 끝점을 만든 후에 특정 기준에 일치 하는 모든 파일에 대 한 hello DSA 최적화 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-126">Once hello CDN endpoint is created, it applies hello DSA optimizations for all files that match certain criteria.</span></span> <span data-ttu-id="bbde2-127">다음 단원을 hello DSA 최적화 자세히 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-127">hello following section describes DSA optimization in detail.</span></span>

## <a name="dsa-optimization-using-azure-cdn"></a><span data-ttu-id="bbde2-128">Azure CDN을 사용하여 DSA 최적화</span><span class="sxs-lookup"><span data-stu-id="bbde2-128">DSA Optimization using Azure CDN</span></span>

<span data-ttu-id="bbde2-129">Azure CDN에서 동적 사이트 가속 기술을 다음 hello를 사용 하 여 동적 자산의 배달 속도가 향상:</span><span class="sxs-lookup"><span data-stu-id="bbde2-129">Dynamic Site Acceleration on Azure CDN speeds up delivery of dynamic assets using hello following techniques:</span></span>

-   <span data-ttu-id="bbde2-130">경로 최적화</span><span class="sxs-lookup"><span data-stu-id="bbde2-130">Route Optimization</span></span>
-   <span data-ttu-id="bbde2-131">TCP 최적화</span><span class="sxs-lookup"><span data-stu-id="bbde2-131">TCP Optimizations</span></span>
-   <span data-ttu-id="bbde2-132">개체 사전 인출(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="bbde2-132">Object Prefetch (Akamai only)</span></span>
-   <span data-ttu-id="bbde2-133">모바일 이미지 압축(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="bbde2-133">Mobile Image Compression (Akamai only)</span></span>

### <a name="route-optimization"></a><span data-ttu-id="bbde2-134">경로 최적화</span><span class="sxs-lookup"><span data-stu-id="bbde2-134">Route Optimization</span></span>

<span data-ttu-id="bbde2-135">경로 최적화는 hello 인터넷 동적 출발점이, 여기서 트래픽 및 일시적으로 중단 지속적으로 변경 하는 hello 네트워크 토폴로지는 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-135">Route optimization is important because hello Internet is a dynamic place, where traffic and temporarily outages are constantly changing hello network topology.</span></span> <span data-ttu-id="bbde2-136">hello 프로토콜 BGP (경계 게이트웨이)는 hello 인터넷의 hello 라우팅 프로토콜 있지만 중간 지점의 현재 상태 (PoP) 서버를 통해 더 빠른 경로 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-136">hello Border Gateway Protocol (BGP) is hello routing protocol of hello Internet, but there may be faster routes via intermediary Point of Presence (PoP) servers.</span></span> 

<span data-ttu-id="bbde2-137">경로 최적화를 hello 최적의 경로 toohello 원본 사이트에서 계속 액세스할 수 있고 동적 콘텐츠를 배달 tooend가 가장 빠른 hello 및 가장 신뢰할 수 있는 경로 통해 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-137">Route optimization chooses hello most optimal path toohello origin so that a site is continuously accessible and dynamic content is delivered tooend users via hello fastest and most reliable route possible.</span></span> 

<span data-ttu-id="bbde2-138">hello Akamai 네트워크 기술을 toocollect 실시간 데이터 사용 하 고 hello open 인터넷 toodetermine hello 빠른 라우팅을 hello 원점과 hello 간의 전체 hello 기본 BGP 경로 비롯 하 여 hello Akamai 서버에 다른 노드를 통해 다양 한 경로 비교 합니다. CDN 가장자리입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-138">hello Akamai network uses techniques toocollect real-time data and compare various paths through different nodes in hello Akamai server, as well as hello default BGP route across hello open Internet toodetermine hello fastest route between hello origin and hello CDN edge.</span></span> <span data-ttu-id="bbde2-139">이러한 기술은 인터넷 정체 지점과 긴 경로를 회피합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-139">These techniques avoid Internet congestion points and long routes.</span></span> 

<span data-ttu-id="bbde2-140">마찬가지로, 애니캐스트 DNS, 대용량의 조합을 지원, Pop 및 상태 검사 toodetermine hello 최상의 게이트웨이 toobest에서 경로 데이터 hello Verizon 네트워크에서 클라이언트 toohello 원점을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-140">Similarly, hello Verizon network uses a combination of Anycast DNS, high capacity support PoPs, and health checks, toodetermine hello best gateways toobest route data from hello client toohello origin.</span></span>
 
<span data-ttu-id="bbde2-141">보다 빠르고 보다 안정적으로 완전히 동적이 고 트랜잭션 콘텐츠 전달 결과적으로, tooend 사용자가 캐시할 수 없는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-141">As a result, fully dynamic and transactional content is delivered more quickly and more reliably tooend users, even when it is uncacheable.</span></span> 

### <a name="tcp-optimizations"></a><span data-ttu-id="bbde2-142">TCP 최적화</span><span class="sxs-lookup"><span data-stu-id="bbde2-142">TCP Optimizations</span></span>

<span data-ttu-id="bbde2-143">전송이 TCP (Control Protocol)의 hello 인터넷 프로토콜 모음 hello 표준을 사용 하는 IP 네트워크에서 응용 프로그램 간 toodeliver 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-143">Transmission Control Protocol (TCP) is hello standard of hello Internet protocol suite used toodeliver information between applications on an IP network.</span></span>  <span data-ttu-id="bbde2-144">기본적으로 몇 백 하며 요청으로 TCP 연결의 경우이 인해 배율로 비효율성 제한 tooavoid 네트워크 congestions를 tooset를 필요한 하는 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-144">By default, there are several back and forth requests required tooset up a TCP connection, as well as limits tooavoid network congestions, which result in inefficiencies at scale.</span></span> <span data-ttu-id="bbde2-145">Akamai의 Azure CDN은 3개의 영역을 최적화하여 이 문제를 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-145">Azure CDN from Akamai deals with this problem by optimizing in three areas:</span></span> 

 - <span data-ttu-id="bbde2-146">느린 시작 제거</span><span class="sxs-lookup"><span data-stu-id="bbde2-146">eliminating slow start</span></span>
 - <span data-ttu-id="bbde2-147">영구 연결 활용</span><span class="sxs-lookup"><span data-stu-id="bbde2-147">leveraging persistent connections</span></span>
 - <span data-ttu-id="bbde2-148">TCP 패킷 매개 변수 조정(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="bbde2-148">tuning TCP packet parameters (Akamai only)</span></span>

#### <a name="eliminating-slow-start"></a><span data-ttu-id="bbde2-149">느린 시작 제거</span><span class="sxs-lookup"><span data-stu-id="bbde2-149">Eliminating slow start</span></span>

<span data-ttu-id="bbde2-150">*시작 속도가 느린* hello hello 네트워크를 통해 전송 되는 데이터 양을 제한 하 여 네트워크 혼잡을 방지 하는 hello TCP 프로토콜의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-150">*Slow start* is a part of hello TCP protocol that prevents network congestion by limiting hello amount of data sent over hello network.</span></span> <span data-ttu-id="bbde2-151">시작 발신자와 수신자 사이의 작은 혼잡 한 창 크기와 최대 hello에 도달 하거나 패킷 손실이 검색 될 때까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-151">It starts off with small congestion window sizes between sender and receiver until hello maximum is reached or packet loss is detected.</span></span>

<span data-ttu-id="bbde2-152">Akamai 및 Verizon의 Azure CDN은 세 단계로 느린 시작을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-152">Azure CDN from Akamai and Verizon eliminates slow start in three steps:</span></span>

1.  <span data-ttu-id="bbde2-153">Akamai와 Verizon의 네트워크 상태 및 toomeasure hello 대역폭 지 PoP 서버 간 연결을 모니터링 하는 대역폭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-153">Both Akamai and Verizon's network use health and bandwidth monitoring toomeasure hello bandwidth of connections between edge PoP servers.</span></span>
2. <span data-ttu-id="bbde2-154">각 서버 hello 네트워크 상태를 인식 하며 서버 상태를 다른 Pop 주위의 hello 있도록 hello 메트릭 지 PoP 서버 간에 공유 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-154">hello metrics are shared between edge PoP servers so that each server is aware of hello network conditions and server health of hello other PoPs around them.</span></span>  
3. <span data-ttu-id="bbde2-155">hello CDN에 지 서버 hello 최적의 창 크기의 근접에서 다른 CDN에 지 서버와 통신할 때 사용 해야 하는 등의 몇 가지 전송 매개 변수 수 toomake 가정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-155">hello CDN edge servers are now able toomake assumptions about some transmission parameters, such as what hello optimal window size should be when communicating with other CDN edge servers in its proximity.</span></span> <span data-ttu-id="bbde2-156">이 단계는 hello 상태 hello CDN에 지 서버 간의 hello 연결의 패킷 데이터 전송을 더 높은 수 있는 경우 hello 초기 혼잡 창 크기를 늘릴 수 있는지를 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-156">This step means that hello initial congestion window size can be increased if hello health of hello connection between hello CDN edge servers is capable of higher packet data transfers.</span></span>  

#### <a name="leveraging-persistent-connections"></a><span data-ttu-id="bbde2-157">영구 연결 활용</span><span class="sxs-lookup"><span data-stu-id="bbde2-157">Leveraging persistent connections</span></span>

<span data-ttu-id="bbde2-158">CDN을 사용 하는 고유 컴퓨터 수가 적어집니다 tooyour 원점 직접 연결 하는 사용자와 직접 비교 tooyour 원본 서버를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-158">Using a CDN, fewer unique machines connect tooyour origin server directly compared with users connecting directly tooyour origin.</span></span> <span data-ttu-id="bbde2-159">Akamai 및 Verizon에서 azure CDN 풀 사용자 요청 함께 tooestablish hello 원점와 더 적은 수의 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-159">Azure CDN from Akamai and Verizon also pools user requests together tooestablish fewer connections with hello origin.</span></span>

<span data-ttu-id="bbde2-160">앞서 언급 했 듯이 TCP 연결 몇 개의 요청 간에에 걸릴 핸드셰이크 tooestablish 새 연결.</span><span class="sxs-lookup"><span data-stu-id="bbde2-160">As mentioned earlier, TCP connections take several requests back and forth in a handshake tooestablish a new connection.</span></span> <span data-ttu-id="bbde2-161">영구 연결 라고도 "HTTP 연결 유지," 여러 HTTP 요청 toosave 라운드트립 시간에 대 한 기존 TCP 연결을 다시 사용 및 배달 속도입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-161">Persistent connections, also known as "HTTP Keep-Alive," reuse existing TCP connections for multiple HTTP requests toosave round-trip times and speed up delivery.</span></span> 

<span data-ttu-id="bbde2-162">또한 hello Verizon 네트워크 hello TCP 연결 tooprevent 닫히는에서 열려 있는 연결을 통해 정기적으로 연결 유지 패킷이 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-162">hello Verizon network also sends periodic keep-alive packets over hello TCP connection tooprevent an open connection from being closed.</span></span>

#### <a name="tuning-tcp-packet-parameters"></a><span data-ttu-id="bbde2-163">TCP 패킷 매개 변수 조정</span><span class="sxs-lookup"><span data-stu-id="bbde2-163">Tuning TCP packet parameters</span></span>

<span data-ttu-id="bbde2-164">Akamai에서 azure CDN도 서버 간 연결을 제어 하는 hello 매개 변수를 튜닝 한 후 다음 기술을 hello를 사용 하 여 hello 사이트에 포함 된 round trips 필요한 tooretrieve 콘텐츠 장거리의 hello 양이 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-164">Azure CDN from Akamai also tunes hello parameters that govern server-to-server connections, and reduces hello amount of long haul round trips required tooretrieve content embedded in hello site by using hello following techniques:</span></span>

1.  <span data-ttu-id="bbde2-165">승인을 기다리지 않고 더 많은 패킷을 보내고 받을 수 있도록 hello 초기 정체 창을 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-165">Increasing hello initial congestion window so that more packets can be sent without waiting for an acknowledgement.</span></span>
2.  <span data-ttu-id="bbde2-166">손실을 검색 하 고 재전송 더 빠르게 수행 되도록 hello 초기 재전송 시간 제한을 감소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-166">Decreasing hello initial retransmit timeout so that a loss is detected, and retransmission occurs more quickly.</span></span>
3.  <span data-ttu-id="bbde2-167">감소 hello 최소 및 최대 재전송 시간 제한 tooreduce hello 대기 시간 패킷 전송 중에 손실 된 가정 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="bbde2-167">Decreasing hello minimum and maximum retransmit timeout tooreduce hello wait time before assuming packets were lost in transmission.</span></span>

### <a name="object-prefetch-akamai-only"></a><span data-ttu-id="bbde2-168">개체 사전 인출(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="bbde2-168">Object Prefetch (Akamai only)</span></span>

<span data-ttu-id="bbde2-169">대부분의 웹 사이트는 이미지 및 스크립트와 같은 다양한 리소스를 참조하는 HTML 페이지로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-169">Most websites consist of an HTML page, which references various other resources such as images and scripts.</span></span> <span data-ttu-id="bbde2-170">일반적으로 웹 페이지를 요청 하는 클라이언트 hello 브라우저를 먼저 다운로드 및 hello HTML 개체를 구문 분석 하 고 있도록 toolinked 자산을 필요한 toofully hello 페이지를 로드 하는 추가 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-170">Typically, when a client requests a webpage, hello browser first downloads and parses hello HTML object, and then makes additional requests toolinked assets that are required toofully load hello page.</span></span> 

<span data-ttu-id="bbde2-171">*프리페치* 은 기술 tooretrieve 이미지 및 스크립트에에서 포함 된 hello HTML 페이지 hello HTML 광고가 toohello 브라우저 및 hello 하기 전에 브라우저도에서는 이러한 개체 요청 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-171">*Prefetch* is a technique tooretrieve images and scripts embedded in hello HTML page while hello HTML is served toohello browser, and before hello browser even makes these object requests.</span></span> 

<span data-ttu-id="bbde2-172">Hello로 **프리페치** 옵션이 경우 CDN hello HTML 기본 페이지 toohello 클라이언트의 브라우저를 사용 하는 hello hello CDN hello 시 설정 되어 있으면 hello HTML 파일의 구문 분석 수행 연결된 된 리소스에 대 한 추가 요청 하 고 캐시에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-172">With hello **prefetch** option turned on at hello time when hello CDN serves hello HTML base page toohello client’s browser, hello CDN parses hello HTML file and make additional requests for any linked resources and store it in its cache.</span></span> <span data-ttu-id="bbde2-173">Hello 클라이언트에서는 hello 요청 hello 연결 된 자산에 대 한, hello CDN에 지 서버가 이미 요청 된 개체에 hello에 및 사용 될 수 있습니다 이러한 즉시 왕복 toohello 원점 하지 않고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-173">When hello client makes hello requests for hello linked assets, hello CDN edge server already has hello requested objects and can serve them immediately without a round trip toohello origin.</span></span> <span data-ttu-id="bbde2-174">이 최적화는 캐시할 수 있는 콘텐츠 및 캐시할 수 없는 콘텐츠에 모두 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-174">This optimization benefits both cacheable and non-cacheable content.</span></span>

### <a name="adaptive-image-compression-akamai-only"></a><span data-ttu-id="bbde2-175">적응 이미지 압축(Akamai에만 해당)</span><span class="sxs-lookup"><span data-stu-id="bbde2-175">Adaptive Image Compression (Akamai only)</span></span>

<span data-ttu-id="bbde2-176">일부 장치, 모바일 세션 특히 느린 네트워크 속도 시간 tootime에서 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-176">Some devices, especially mobile ones, experience slower network speeds from time tootime.</span></span> <span data-ttu-id="bbde2-177">이러한 시나리오에서 더는 것이 hello 사용자 tooreceive 해당 웹 페이지에 더 작은 이미지에 대 한 전체 고해상도 이미지에 대 한 오래 대기 하는 대신에 보다 신속 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-177">In these scenarios, it is more beneficial for hello user tooreceive smaller images in their webpage more quickly rather than waiting a long time for full resolution images.</span></span>

<span data-ttu-id="bbde2-178">이 기능은 자동으로 네트워크 품질을 모니터링 하 고 네트워크 속도가 느린 tooimprove 배달 시간 때 표준 JPEG 압축 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-178">This feature automatically monitors network quality, and employs standard JPEG compression methods when network speeds are slower tooimprove delivery time.</span></span>

<span data-ttu-id="bbde2-179">적응 이미지 압축</span><span class="sxs-lookup"><span data-stu-id="bbde2-179">Adaptive Image Compression</span></span> | <span data-ttu-id="bbde2-180">파일 확장명</span><span class="sxs-lookup"><span data-stu-id="bbde2-180">File Extensions</span></span>  
--- | ---  
<span data-ttu-id="bbde2-181">JPEG 압축</span><span class="sxs-lookup"><span data-stu-id="bbde2-181">JPEG compression</span></span> | <span data-ttu-id="bbde2-182">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span><span class="sxs-lookup"><span data-stu-id="bbde2-182">.jpg, .jpeg, .jpe, .jig, .jgig, .jgi</span></span>

## <a name="caching"></a><span data-ttu-id="bbde2-183">구성</span><span class="sxs-lookup"><span data-stu-id="bbde2-183">Caching</span></span>

<span data-ttu-id="bbde2-184">DSA와 캐싱 꺼져 hello CDN에서에 기본적으로 hello 원점 hello에 대 한 응답 제어/만료 캐시 머리글을 포함 하는 경우에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-184">With DSA, caching is turned off by default on hello CDN, even when hello origin includes cache-control/expires headers in hello response.</span></span> <span data-ttu-id="bbde2-185">DSA 고유 tooeach 클라이언트는 있으므로 캐시 하지 않아야 하는 동적 자산에 대 한 일반적으로 사용 되기 때문에이 기본값은 해제 하 고 기본적으로 캐시를 설정 하면이 동작 손상 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-185">This default is turned off because DSA is typically used for dynamic assets that should not be cached since they are unique tooeach client, and turning on caching by default can break this behavior.</span></span>

<span data-ttu-id="bbde2-186">정적 및 동적 자산을 조합 하 여 웹 사이트를 설정한 경우 최상의 tootake 하이브리드 방식 tooget hello 최상의 성능입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-186">If you have a website with a mix of static and dynamic assets, it is best tootake a hybrid approach tooget hello best performance.</span></span> 

<span data-ttu-id="bbde2-187">ADN Verizon premium을 사용 하는 경우 규칙 엔진 hello를 사용 하 여 특정 사례에 대 한 캐싱 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-187">If you are using ADN with Verizon Premium, you can turn caching back on for specific cases using hello Rules Engine.</span></span>  

<span data-ttu-id="bbde2-188">CDN 끝점을 두 개의 toouse 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-188">An alternative is toouse two CDN endpoints.</span></span> <span data-ttu-id="bbde2-189">DSA toodeliver 동적 자산을 사용 하 여 및 정적 최적화와 함께 다른 끝점 형식, 예: 일반 웹 배달 toodelivery 캐시할 자산입니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-189">One with DSA toodeliver dynamic assets, and another endpoint with a static optimization type, such as general web delivery, toodelivery cacheable assets.</span></span> <span data-ttu-id="bbde2-190">이 대체 순서 tooaccomplish, toohello 자산에 hello toouse CDN 끝점을 직접 웹 페이지 Url toolink를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-190">In order tooaccomplish this alternative, you will modify your webpage URLs toolink directly toohello asset on hello CDN endpoint you plan toouse.</span></span> 

<span data-ttu-id="bbde2-191">예를 들어: `mydynamic.azureedge.net/index.html` 동적 페이지가 고 hello DSA 끝점에서 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-191">For example: `mydynamic.azureedge.net/index.html` is a dynamic page and is loaded from hello DSA endpoint.</span></span>  <span data-ttu-id="bbde2-192">hello html 페이지를 참조 JavaScript 라이브러리와 같은 여러 정적 자산 또는에서 로드 되는 이미지와 같은 정적 CDN 끝점을 hello `mystatic.azureedge.net/banner.jpg` 및 `mystatic.azureedge.net/scripts.js`합니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-192">hello html page references multiple static assets such as JavaScript libraries or images that are loaded from hello static CDN endpoint, such as `mystatic.azureedge.net/banner.jpg` and `mystatic.azureedge.net/scripts.js`.</span></span> 

<span data-ttu-id="bbde2-193">예를 찾을 수 있습니다 [여기](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) 어떻게 toouse 컨트롤러에는 ASP.NET 웹 응용 프로그램 tooserve 콘텐츠 특정 CDN URL을 통해에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbde2-193">You can find an example [here](https://docs.microsoft.com/azure/cdn/cdn-cloud-service-with-cdn#controller) on how toouse controllers in an ASP.NET web application tooserve content through a specific CDN URL.</span></span>




