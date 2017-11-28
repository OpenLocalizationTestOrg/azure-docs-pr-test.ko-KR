---
title: "aaaPerformance 고려 사항에 대 한 Azure 트래픽 관리자 | Microsoft Docs"
description: "트래픽 관리자 성능 이해 및 방법을 트래픽 관리자를 사용 하는 경우 웹 사이트의 tootest 성능"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="760b2-103">Traffic Manager 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="760b2-103">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="760b2-104">이 페이지에서는 Traffic Manager를 사용할 때의 성능 고려 사항에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-104">This page explains performance considerations using Traffic Manager.</span></span> <span data-ttu-id="760b2-105">Hello를 시나리오를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-105">Consider hello following scenario:</span></span>

<span data-ttu-id="760b2-106">Hello WestUS에서에서 웹 사이트의 인스턴스 및 한국 우편 영역 있는데</span><span class="sxs-lookup"><span data-stu-id="760b2-106">You have instances of your website in hello WestUS and EastAsia regions.</span></span> <span data-ttu-id="760b2-107">트래픽 관리자 프로브 hello에 대 한 hello 상태 검사를 실패 hello 인스턴스 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-107">One of hello instances is failing hello health check for hello traffic manager probe.</span></span> <span data-ttu-id="760b2-108">응용 프로그램 트래픽은 directed toohello 정상 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-108">Application traffic is directed toohello healthy region.</span></span> <span data-ttu-id="760b2-109">이 장애 조치가 발생할 수 있지만 성능이 이제 tooa 떨어져 있는 영역을 이동 하는 hello 트래픽의 hello 대기 시간에 따라 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-109">This failover is expected but performance can be a problem based on hello latency of hello traffic now traveling tooa distant region.</span></span>

## <a name="performance-considerations-for-traffic-manager"></a><span data-ttu-id="760b2-110">Traffic Manager 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="760b2-110">Performance considerations for Traffic Manager</span></span>

<span data-ttu-id="760b2-111">hello만 성능에 미치는 영향 트래픽 관리자 수 웹 사이트는 hello 초기 DNS 조회입니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-111">hello only performance impact that Traffic Manager can have on your website is hello initial DNS lookup.</span></span> <span data-ttu-id="760b2-112">트래픽 관리자 프로필의 hello 이름에 대 한 DNS 요청은 해당 호스트 hello trafficmanager.net 영역 hello Microsoft DNS 루트 서버에서 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-112">A DNS request for hello name of your Traffic Manager profile is handled by hello Microsoft DNS root server that hosts hello trafficmanager.net zone.</span></span> <span data-ttu-id="760b2-113">트래픽 관리자 채우고 hello Microsoft DNS 루트 서버 hello 트래픽 관리자 정책 및 hello 검색 결과에 따라, 정기적으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-113">Traffic Manager populates, and regularly updates, hello Microsoft's DNS root servers based on hello Traffic Manager policy and hello probe results.</span></span> <span data-ttu-id="760b2-114">Hello 초기 DNS 조회 하는 동안에 DNS 쿼리가 더 이상 관리자 tooTraffic 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-114">So even during hello initial DNS lookup, no DNS queries are sent tooTraffic Manager.</span></span>

<span data-ttu-id="760b2-115">트래픽 관리자는 여러 가지 구성 요소로 이루어진: DNS 서버, API 서비스, hello 저장소 계층 및 모니터링 서비스 끝점 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-115">Traffic Manager is made up of several components: DNS name servers, an API service, hello storage layer, and an endpoint monitoring service.</span></span> <span data-ttu-id="760b2-116">트래픽 관리자 서비스 구성 요소에 실패 하면 트래픽 관리자 프로필에 연결 된 hello DNS 이름에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-116">If a Traffic Manager service component fails, there is no effect on hello DNS name associated with your Traffic Manager profile.</span></span> <span data-ttu-id="760b2-117">hello 레코드 hello Microsoft DNS 서버에서 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-117">hello records in hello Microsoft DNS servers remain unchanged.</span></span> <span data-ttu-id="760b2-118">그러나 끝점 모니터링 및 DNS 업데이트는 일어나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-118">However, endpoint monitoring and DNS updating do not happen.</span></span> <span data-ttu-id="760b2-119">따라서 트래픽 관리자는 하지 수 tooupdate DNS toopoint tooyour 장애 조치 사이트 기본 사이트가 중단 되 면 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-119">Therefore, Traffic Manager is not able tooupdate DNS toopoint tooyour failover site when your primary site goes down.</span></span>

<span data-ttu-id="760b2-120">DNS 이름 확인은 신속하고 결과는 캐시됩니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-120">DNS name resolution is fast and results are cached.</span></span> <span data-ttu-id="760b2-121">hello 초기 DNS 조회의 hello 속도 이름 확인을 위해 사용 하 여 DNS 서버 hello 클라이언트 hello에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-121">hello speed of hello initial DNS lookup depends on hello DNS servers hello client uses for name resolution.</span></span> <span data-ttu-id="760b2-122">일반적으로 클라이언트는 50ms 이내에 DNS 조회를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-122">Typically, a client can complete a DNS lookup within ~50 ms.</span></span> <span data-ttu-id="760b2-123">hello 조회의 hello 결과의 DNS-time-to-live (TTL) hello hello 기간에 대 한 캐시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-123">hello results of hello lookup are cached for hello duration of hello DNS Time-to-live (TTL).</span></span> <span data-ttu-id="760b2-124">hello 기본 트래픽 관리자에 대 한 TTL은 300 초입니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-124">hello default TTL for Traffic Manager is 300 seconds.</span></span>

<span data-ttu-id="760b2-125">트래픽은 Traffic Manager를 통해 전달되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-125">Traffic does NOT flow through Traffic Manager.</span></span> <span data-ttu-id="760b2-126">Hello DNS 조회 완료 되 면 hello 클라이언트 웹 사이트의 인스턴스에 대 한 IP 주소를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-126">Once hello DNS lookup completes, hello client has an IP address for an instance of your web site.</span></span> <span data-ttu-id="760b2-127">hello 클라이언트 toothat 주소에 직접 연결 하 고 트래픽 관리자를 통해 전달 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-127">hello client connects directly toothat address and does not pass through Traffic Manager.</span></span> <span data-ttu-id="760b2-128">트래픽 관리자 정책을 선택 하면 hello에 hello DNS 성능에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-128">hello Traffic Manager policy you choose has no influence on hello DNS performance.</span></span> <span data-ttu-id="760b2-129">그러나 성능 라우팅 방법 hello 응용 프로그램 환경이 저하 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-129">However, a Performance routing-method can negatively impact hello application experience.</span></span> <span data-ttu-id="760b2-130">예를 들어 정책에 아시아에서 호스팅되는 북미 지역 tooan 인스턴스에서 트래픽을 리디렉션합니다, 하는 경우 해당 세션에 대 한 hello 네트워크 대기 시간 성능 문제를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-130">For example, if your policy redirects traffic from North America tooan instance hosted in Asia, hello network latency for those sessions may be a performance issue.</span></span>

## <a name="measuring-traffic-manager-performance"></a><span data-ttu-id="760b2-131">Traffic Manager 성능 측정</span><span class="sxs-lookup"><span data-stu-id="760b2-131">Measuring Traffic Manager Performance</span></span>

<span data-ttu-id="760b2-132">여러 웹 사이트 toounderstand hello 성능 및 트래픽 관리자 프로필의 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-132">There are several websites you can use toounderstand hello performance and behavior of a Traffic Manager profile.</span></span> <span data-ttu-id="760b2-133">이러한 대다수의 사이트는 무료이지만 제한이 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-133">Many of these sites are free but may have limitations.</span></span> <span data-ttu-id="760b2-134">일부 사이트는 유료로 향상된 모니터링 및 보고를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-134">Some sites offer enhanced monitoring and reporting for a fee.</span></span>

<span data-ttu-id="760b2-135">이러한 사이트에 hello 도구 DNS 대기 시간을 측정 하 고 디스플레이 hello hello 전 세계 클라이언트 위치에 대 한 IP 주소를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-135">hello tools on these sites measure DNS latencies and display hello resolved IP addresses for client locations around hello world.</span></span> <span data-ttu-id="760b2-136">대부분의이 도구는 hello DNS 결과 캐시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-136">Most of these tools do not cache hello DNS results.</span></span> <span data-ttu-id="760b2-137">따라서 hello 도구는 테스트를 실행할 때마다 hello 전체 DNS 조회를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-137">Therefore, hello tools show hello full DNS lookup each time a test is run.</span></span> <span data-ttu-id="760b2-138">사용자 고유의 클라이언트에서 테스트 하는 경우 hello 전체 DNS 조회 성능을 hello TTL 기간 동안 한 번만 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-138">When you test from your own client, you only experience hello full DNS lookup performance once during hello TTL duration.</span></span>

## <a name="sample-tools-toomeasure-dns-performance"></a><span data-ttu-id="760b2-139">샘플 도구 toomeasure DNS 성능</span><span class="sxs-lookup"><span data-stu-id="760b2-139">Sample tools toomeasure DNS performance</span></span>

* [<span data-ttu-id="760b2-140">SolveDNS</span><span class="sxs-lookup"><span data-stu-id="760b2-140">SolveDNS</span></span>](http://www.solvedns.com/dns-comparison/)

    <span data-ttu-id="760b2-141">SolveDNS는 많은 성능 도구를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-141">SolveDNS offers many performance tools.</span></span> <span data-ttu-id="760b2-142">hello DNS 비교 도구 시간 tooresolve DNS 이름 및 tooother DNS 서비스 공급자를 비교 하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-142">hello DNS Comparison tool can show you how long it takes tooresolve your DNS name and how that compares tooother DNS service providers.</span></span>

* [<span data-ttu-id="760b2-143">WebSitePulse</span><span class="sxs-lookup"><span data-stu-id="760b2-143">WebSitePulse</span></span>](http://www.websitepulse.com/help/tools.php)

    <span data-ttu-id="760b2-144">Hello 가장 간단한 도구 중 하나는 WebSitePulse 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-144">One of hello simplest tools is WebSitePulse.</span></span> <span data-ttu-id="760b2-145">Hello URL toosee DNS 확인 시간, 첫 번째 바이트, 마지막 바이트 및 기타 성능 통계를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-145">Enter hello URL toosee DNS resolution time, First Byte, Last Byte, and other performance statistics.</span></span> <span data-ttu-id="760b2-146">3개의 서로 다른 테스트 위치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-146">You can choose from three different test locations.</span></span> <span data-ttu-id="760b2-147">이 예제에서는 첫 번째 실행 hello 0.204 sec DNS 조회를 사용 한다고 표시 되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-147">In this example, you see that hello first execution shows that DNS lookup takes 0.204 sec.</span></span>

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    <span data-ttu-id="760b2-149">Hello 결과가 캐시 되므로 hello에 대 한 두 번째 테스트 hello 같은 트래픽 관리자 끝점 hello DNS 조회 때문에 0.002 초를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-149">Because hello results are cached, hello second test for hello same Traffic Manager endpoint hello DNS lookup takes 0.002 sec.</span></span>

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [<span data-ttu-id="760b2-151">CA 앱 가상 모니터</span><span class="sxs-lookup"><span data-stu-id="760b2-151">CA App Synthetic Monitor</span></span>](https://asm.ca.com/en/checkit.php)

    <span data-ttu-id="760b2-152">이전 hello Watchmouse 검사 웹 사이트 도구에는,이 사이트 알려주는 동시에 여러 지리적 지역에서 시간 hello DNS 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-152">Formerly known as hello Watchmouse Check Website tool, this site show you hello DNS resolution time from multiple geographic regions simultaneously.</span></span> <span data-ttu-id="760b2-153">여러 지리적 위치에서 hello URL toosee DNS 확인 시간, 연결 시간 및 속도 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-153">Enter hello URL toosee DNS resolution time, connection time, and speed from several geographic locations.</span></span> <span data-ttu-id="760b2-154">이 테스트 toosee 반환 되는 호스팅된 서비스를 사용 하 여 hello 전 세계 여러 위치에 대 한.</span><span class="sxs-lookup"><span data-stu-id="760b2-154">Use this test toosee which hosted service is returned for different locations around hello world.</span></span>

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [<span data-ttu-id="760b2-156">Pingdom</span><span class="sxs-lookup"><span data-stu-id="760b2-156">Pingdom</span></span>](http://tools.pingdom.com/)

    <span data-ttu-id="760b2-157">이 도구는 웹 페이지의 각 요소에 대한 성능 통계를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-157">This tool provides performance statistics for each element of a web page.</span></span> <span data-ttu-id="760b2-158">hello 페이지 분석 탭 DNS 조회에 소요 된 시간의 hello 백분율을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-158">hello Page Analysis tab shows hello percentage of time spent on DNS lookup.</span></span>

* [<span data-ttu-id="760b2-159">Azure DNS란?</span><span class="sxs-lookup"><span data-stu-id="760b2-159">What's My DNS?</span></span>](http://www.whatsmydns.net/)

    <span data-ttu-id="760b2-160">이 사이트에서 DNS 조회 20 개의 다른 위치에서 상속 되지 않습니다 하 고 지도에 hello 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-160">This site does a DNS lookup from 20 different locations and displays hello results on a map.</span></span>

* [<span data-ttu-id="760b2-161">Dig 웹 인터페이스</span><span class="sxs-lookup"><span data-stu-id="760b2-161">Dig Web Interface</span></span>](http://www.digwebinterface.com)

    <span data-ttu-id="760b2-162">이 사이트에서는 CNAME 및 A 기록을 포함한 보다 자세한 DNS 정보를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-162">This site shows more detailed DNS information including CNAMEs and A records.</span></span> <span data-ttu-id="760b2-163">옵션에서 '색상화 출력' hello 및 '통계'를 확인 하 고 이름 서버에서 '모두'를 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="760b2-163">Make sure you check hello 'Colorize output' and 'Stats' under options, and select 'All' under Nameservers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="760b2-164">다음 단계</span><span class="sxs-lookup"><span data-stu-id="760b2-164">Next Steps</span></span>

[<span data-ttu-id="760b2-165">Traffic Manager 트래픽 라우팅 방법 정보</span><span class="sxs-lookup"><span data-stu-id="760b2-165">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)

[<span data-ttu-id="760b2-166">Traffic Manager 설정 테스트</span><span class="sxs-lookup"><span data-stu-id="760b2-166">Test your Traffic Manager settings</span></span>](traffic-manager-testing-settings.md)

[<span data-ttu-id="760b2-167">Traffic Manager 작업(REST API 참조)</span><span class="sxs-lookup"><span data-stu-id="760b2-167">Operations on Traffic Manager (REST API Reference)</span></span>](http://go.microsoft.com/fwlink/?LinkId=313584)

[<span data-ttu-id="760b2-168">Azure Traffic Manager cmdlet</span><span class="sxs-lookup"><span data-stu-id="760b2-168">Azure Traffic Manager Cmdlets</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=400769)

