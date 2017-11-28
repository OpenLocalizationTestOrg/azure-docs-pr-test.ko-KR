---
title: "트래픽 관리자 프로필 aaaNested | Microsoft Docs"
description: "이 문서에서는 Azure 트래픽 관리자의 hello 중첩 프로필 기능 설명"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f1b112c4-a3b1-496e-90eb-41e235a49609
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: e476d58a82ed94d12731156280c9665f980de0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="nested-traffic-manager-profiles"></a><span data-ttu-id="c1f57-103">중첩 트래픽 관리자 프로필</span><span class="sxs-lookup"><span data-stu-id="c1f57-103">Nested Traffic Manager profiles</span></span>

<span data-ttu-id="c1f57-104">트래픽 관리자 끝점 각 최종 사용자 로부터 트래픽을 받아야 트래픽 관리자가 선택 하는 방법 toocontrol 사용할 수 있는 트래픽 라우팅 메서드가의 범위에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-104">Traffic Manager includes a range of traffic-routing methods that allow you toocontrol how Traffic Manager chooses which endpoint should receive traffic from each end user.</span></span> <span data-ttu-id="c1f57-105">자세한 내용은 [트래픽 관리자 트래픽 라우팅 방법](traffic-manager-routing-methods.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1f57-105">For more information, see [Traffic Manager traffic-routing methods](traffic-manager-routing-methods.md).</span></span>

<span data-ttu-id="c1f57-106">각 트래픽 관리자 프로필은 단일 트래픽 라우팅 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-106">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="c1f57-107">그러나 단일 트래픽 관리자 프로필에서 제공 hello 라우팅 보다 더 정교한 트래픽 라우팅이 필요로 하는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-107">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="c1f57-108">둘 이상의 트래픽 라우팅 방법의 트래픽 관리자 프로필 toocombine hello 혜택을 중첩할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-108">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="c1f57-109">중첩 된 프로필을 사용 하면 더 큰 toooverride hello 기본 트래픽 관리자 동작 toosupport 및 더 복잡 한 응용 프로그램 배포.</span><span class="sxs-lookup"><span data-stu-id="c1f57-109">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span>

<span data-ttu-id="c1f57-110">다음 예제는 hello toouse 다양 한 시나리오에서 트래픽 관리자 프로필을 중첩 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-110">hello following examples illustrate how toouse nested Traffic Manager profiles in various scenarios.</span></span>

## <a name="example-1-combining-performance-and-weighted-traffic-routing"></a><span data-ttu-id="c1f57-111">예제 1: '성능' 및 '가중' 트래픽 라우팅 결합</span><span class="sxs-lookup"><span data-stu-id="c1f57-111">Example 1: Combining 'Performance' and 'Weighted' traffic routing</span></span>

<span data-ttu-id="c1f57-112">Azure 지역에 따라 hello에서 응용 프로그램을 배포 하는 가정: 미국 서 부, 서 부 유럽 및 아시아 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-112">Suppose that you deployed an application in hello following Azure regions: West US, West Europe, and East Asia.</span></span> <span data-ttu-id="c1f57-113">트래픽 관리자의 'Performance' 트래픽 라우팅 메서드 toodistribute 트래픽 toohello 지역 가장 가까운 toohello 사용자를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-113">You use Traffic Manager's 'Performance' traffic-routing method toodistribute traffic toohello region closest toohello user.</span></span>

![단일 트래픽 관리자 프로필][4]

<span data-ttu-id="c1f57-115">이제, 원하는 tootest 업데이트 tooyour 서비스 배포 전에 더 광범위 하 게 가정해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-115">Now, suppose you wish tootest an update tooyour service before rolling it out more widely.</span></span> <span data-ttu-id="c1f57-116">Toouse hello 'weighted' 트래픽 라우팅 방법 toodirect 트래픽 tooyour 테스트 배포의 작은 비율을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-116">You want toouse hello 'weighted' traffic-routing method toodirect a small percentage of traffic tooyour test deployment.</span></span> <span data-ttu-id="c1f57-117">서 부 유럽에서 hello 기존 프로덕션 배포와 함께 hello 테스트 배포를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-117">You set up hello test deployment alongside hello existing production deployment in West Europe.</span></span>

<span data-ttu-id="c1f57-118">단일 프로필에서 '가중' 및 '성능' 트래픽 라우팅을 결합할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-118">You cannot combine both 'Weighted' and 'Performance traffic-routing in a single profile.</span></span> <span data-ttu-id="c1f57-119">toosupport hello 두 서 부 유럽 끝점 및 hello '가 중' 트래픽 라우팅 메서드를 사용 하 여 트래픽 관리자 프로필을 만들면이 시나리오에서는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-119">toosupport this scenario, you create a Traffic Manager profile using hello two West Europe endpoints and hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="c1f57-120">다음으로, 끝점 toohello 'parent' 프로필로이 'child' 프로필을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-120">Next, you add this 'child' profile as an endpoint toohello 'parent' profile.</span></span> <span data-ttu-id="c1f57-121">다른 글로벌 배포 끝점으로 hello 하는 hello 부모 프로필 여전히 사용 하 여 성능 트래픽 라우팅 방법 hello 및를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-121">hello parent profile still uses hello Performance traffic-routing method and contains hello other global deployments as endpoints.</span></span>

<span data-ttu-id="c1f57-122">hello 다음 다이어그램에서는이 예제를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-122">hello following diagram illustrates this example:</span></span>

![중첩 트래픽 관리자 프로필][2]

<span data-ttu-id="c1f57-124">이 구성에서는 hello 부모 프로필을 통해 보내지는 트래픽을 트래픽을 분산 영역 정상적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-124">In this configuration, traffic directed via hello parent profile distributes traffic across regions normally.</span></span> <span data-ttu-id="c1f57-125">서 부 유럽 내 hello 중첩된 프로필 배포 트래픽 toohello 프로덕션 환경과 테스트 끝점 toohello 가중치 할당에 따라 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-125">Within West Europe, hello nested profile distributes traffic toohello production and test endpoints according toohello weights assigned.</span></span>

<span data-ttu-id="c1f57-126">Hello 부모 프로필 hello 'Performance' 트래픽 라우팅 메서드를 사용 하는 경우 각 끝점 위치를 할당 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-126">When hello parent profile uses hello 'Performance' traffic-routing method, each endpoint must be assigned a location.</span></span> <span data-ttu-id="c1f57-127">hello 위치는 hello 끝점을 구성할 때 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-127">hello location is assigned when you configure hello endpoint.</span></span> <span data-ttu-id="c1f57-128">Hello Azure 지역 가장 가까운 tooyour 배포를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-128">Choose hello Azure region closest tooyour deployment.</span></span> <span data-ttu-id="c1f57-129">hello Azure 영역은 hello 인터넷 대기 시간 테이블에서 지 원하는 hello 위치 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-129">hello Azure regions are hello location values supported by hello Internet Latency Table.</span></span> <span data-ttu-id="c1f57-130">자세한 내용은 [Traffic Manager '성능' 트래픽 라우팅 메서드](traffic-manager-routing-methods.md#performance)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1f57-130">For more information, see [Traffic Manager 'Performance' traffic-routing method](traffic-manager-routing-methods.md#performance).</span></span>

## <a name="example-2-endpoint-monitoring-in-nested-profiles"></a><span data-ttu-id="c1f57-131">예제 2: 중첩 프로필의 끝점 모니터링</span><span class="sxs-lookup"><span data-stu-id="c1f57-131">Example 2: Endpoint monitoring in Nested Profiles</span></span>

<span data-ttu-id="c1f57-132">트래픽 관리자는 각 서비스 끝점의 hello 상태를 적극적으로 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-132">Traffic Manager actively monitors hello health of each service endpoint.</span></span> <span data-ttu-id="c1f57-133">끝점 상태가 정상이 아닌 경우 서비스의 사용자가 tooalternative 끝점 toopreserve hello 가용성 트래픽 관리자에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-133">If an endpoint is unhealthy, Traffic Manager directs users tooalternative endpoints toopreserve hello availability of your service.</span></span> <span data-ttu-id="c1f57-134">이 끝점 모니터링 및 장애 조치 동작 tooall 트래픽 라우팅 메서드를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-134">This endpoint monitoring and failover behavior applies tooall traffic-routing methods.</span></span> <span data-ttu-id="c1f57-135">자세한 내용은 [트래픽 관리자 끝점 모니터링](traffic-manager-monitoring.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c1f57-135">For more information, see [Traffic Manager Endpoint Monitoring](traffic-manager-monitoring.md).</span></span> <span data-ttu-id="c1f57-136">끝점 모니터링은 중첩 프로필에 대해 다르게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-136">Endpoint monitoring works differently for nested profiles.</span></span> <span data-ttu-id="c1f57-137">중첩 된 프로필을 통해 hello 부모 프로필에서 hello 자식에 대해 상태 검사를 직접 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-137">With nested profiles, hello parent profile doesn't perform health checks on hello child directly.</span></span> <span data-ttu-id="c1f57-138">대신 hello 자식 프로필의 끝점의 hello 상태는 사용 되는 toocalculate hello hello 자식 프로필의 전반적인 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-138">Instead, hello health of hello child profile's endpoints is used toocalculate hello overall health of hello child profile.</span></span> <span data-ttu-id="c1f57-139">이 상태 정보는 중첩 된 hello 프로필 계층 구조를 전파 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-139">This health information is propagated up hello nested profile hierarchy.</span></span> <span data-ttu-id="c1f57-140">hello 부모 프로필이 사용 합니다.이 집계 상태 toodetermine 여부 toodirect 트래픽 toohello 자식 프로필입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-140">hello parent profile uses this aggregated health toodetermine whether toodirect traffic toohello child profile.</span></span> <span data-ttu-id="c1f57-141">Hello 참조 [FAQ](traffic-manager-FAQs.md#traffic-manager-nested-profiles) 대 한 자세한 내용은 중첩 된 프로필의 상태를 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-141">See hello [FAQ](traffic-manager-FAQs.md#traffic-manager-nested-profiles) for full details on health monitoring of nested profiles.</span></span>

<span data-ttu-id="c1f57-142">서 부 유럽에서 hello 프로덕션 배포에 실패 가정 toohello 앞의 예제를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-142">Returning toohello previous example, suppose hello production deployment in West Europe fails.</span></span> <span data-ttu-id="c1f57-143">기본적으로 hello 'child' 프로필에서는 모든 트래픽이 toohello 테스트 배포를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-143">By default, hello 'child' profile directs all traffic toohello test deployment.</span></span> <span data-ttu-id="c1f57-144">Hello 테스트 배포도 실패 하는 경우는 hello 자식 프로필을 받지 않는 트래픽 정상 상태가 아닌 모든 자식 끝점 이후 hello 부모 프로필 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-144">If hello test deployment also fails, hello parent profile determines that hello child profile should not receive traffic since all child endpoints are unhealthy.</span></span> <span data-ttu-id="c1f57-145">그런 다음 부모 프로필 hello 다른 지역의 트래픽 toohello를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-145">Then, hello parent profile distributes traffic toohello other regions.</span></span>

![중첩 프로필 장애 조치(기본 동작)][3]

<span data-ttu-id="c1f57-147">이 정렬에 만족할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-147">You might be happy with this arrangement.</span></span> <span data-ttu-id="c1f57-148">또는 서 부 유럽에 대 한 모든 트래픽이 제한 된 하위 집합 트래픽 대신 toohello 테스트 배포 이제 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-148">Or you might be concerned that all traffic for West Europe is now going toohello test deployment instead of a limited subset traffic.</span></span> <span data-ttu-id="c1f57-149">Hello의 hello 상태에 관계 없이 테스트 배포, toofail 통해 하려는 toohello 다른 지역에 서 부 유럽 hello 프로덕션 배포에 실패 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="c1f57-149">Regardless of hello health of hello test deployment, you want toofail over toohello other regions when hello production deployment in West Europe fails.</span></span> <span data-ttu-id="c1f57-150">tooenable이 장애이 조치 hello 부모 프로필에서 끝점으로 hello 자식 프로필을 구성할 때 hello 'MinChildEndpoints' 매개 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-150">tooenable this failover, you can specify hello 'MinChildEndpoints' parameter when configuring hello child profile as an endpoint in hello parent profile.</span></span> <span data-ttu-id="c1f57-151">hello 매개 변수는 hello hello 자식 프로필에서 사용할 수 있는 끝점의 최소 수를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-151">hello parameter determines hello minimum number of available endpoints in hello child profile.</span></span> <span data-ttu-id="c1f57-152">hello 기본값은 '1'입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-152">hello default value is '1'.</span></span> <span data-ttu-id="c1f57-153">이 시나리오에 대 한 hello MinChildEndpoints 값 too2를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-153">For this scenario, you set hello MinChildEndpoints value too2.</span></span> <span data-ttu-id="c1f57-154">이 임계값 아래로 hello 부모 프로필 hello 전체 자식 프로필 toobe를 사용할 수 없는 것으로 간주 하 고 트래픽을 toohello 다른 끝점을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-154">Below this threshold, hello parent profile considers hello entire child profile toobe unavailable and directs traffic toohello other endpoints.</span></span>

<span data-ttu-id="c1f57-155">hello 다음 그림에서는이 구성을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-155">hello following figure illustrates this configuration:</span></span>

!['MinChildEndpoints' = 2인 중첩 프로필 장애 조치][4]

> [!NOTE]
> <span data-ttu-id="c1f57-157">모든 트래픽 tooa 단일 끝점을 배포 하는 hello 'Priority' 트래픽 라우팅 방법.</span><span class="sxs-lookup"><span data-stu-id="c1f57-157">hello 'Priority' traffic-routing method distributes all traffic tooa single endpoint.</span></span> <span data-ttu-id="c1f57-158">따라서 하위 프로필의 경우 MinChildEndpoints '1'이 아닌 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-158">Thus there is little purpose in a MinChildEndpoints setting other than '1' for a child profile.</span></span>

## <a name="example-3-prioritized-failover-regions-in-performance-traffic-routing"></a><span data-ttu-id="c1f57-159">예제 3: '성능' 트래픽 라우팅에서 우선 순위가 지정된 장애 조치(Failover) 지역</span><span class="sxs-lookup"><span data-stu-id="c1f57-159">Example 3: Prioritized failover regions in 'Performance' traffic routing</span></span>

<span data-ttu-id="c1f57-160">hello 기본 hello 'Performance' 트래픽 라우팅 방법에 대 한 동작은 설계 된 tooavoid 과도 하 게 끝점에 가장 가까운 hello 다음 로드 및 연계 일련의 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-160">hello default behavior for hello 'Performance' traffic-routing method is designed tooavoid over-loading hello next nearest endpoint and causing a cascading series of failures.</span></span> <span data-ttu-id="c1f57-161">끝점에 실패 하면가 지시한 toothat 끝점을 균등 하 게 하는 모든 트래픽을 분산 toohello 다른 끝점 모든 지역.</span><span class="sxs-lookup"><span data-stu-id="c1f57-161">When an endpoint fails, all traffic that would have been directed toothat endpoint is evenly distributed toohello other endpoints across all regions.</span></span>

![기본 장애 조치를 사용하는 '성능' 트래픽 라우팅][5]

<span data-ttu-id="c1f57-163">그러나 두 끝점 모두 사용할 수 없을 때 트래픽을 tooother 영역 직접와 hello 서 부 유럽 트래픽 장애 조치 tooWest US, 원하는 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-163">However, suppose you prefer hello West Europe traffic failover tooWest US, and only direct traffic tooother regions when both endpoints are unavailable.</span></span> <span data-ttu-id="c1f57-164">자식 프로필 hello 'Priority' 트래픽 라우팅 메서드를 사용 하 여이 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-164">You can create this solution using a child profile with hello 'Priority' traffic-routing method.</span></span>

![기본 설정 장애 조치를 사용하는 '성능' 트래픽 라우팅][6]

<span data-ttu-id="c1f57-166">Hello 서 부 유럽 끝점 hello West US 끝점 보다 높은 우선 순위에 있으므로는 모든 트래픽이 양쪽 끝점이 온라인 상태일 때 toohello 서 부 유럽 끝점에 전송 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-166">Since hello West Europe endpoint has higher priority than hello West US endpoint, all traffic is sent toohello West Europe endpoint when both endpoints are online.</span></span> <span data-ttu-id="c1f57-167">서 부 유럽에 실패 하면 해당 트래픽은 directed tooWest 미국입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-167">If West Europe fails, its traffic is directed tooWest US.</span></span> <span data-ttu-id="c1f57-168">중첩 된 hello 프로필을 트래픽은 서 부 유럽 및 West US 모두 실패 하는 경우에 리디렉션된 tooEast 아시아입니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-168">With hello nested profile, traffic is directed tooEast Asia only when both West Europe and West US fail.</span></span>

<span data-ttu-id="c1f57-169">모든 지역에 대해 이 패턴을 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-169">You can repeat this pattern for all regions.</span></span> <span data-ttu-id="c1f57-170">대체 hello 부모 프로필에 세 개 끝점이 모두 세 개의 자식 프로필 각각 우선 순위가 지정 된 장애 조치 순서를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-170">Replace all three endpoints in hello parent profile with three child profiles, each providing a prioritized failover sequence.</span></span>

## <a name="example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-hello-same-region"></a><span data-ttu-id="c1f57-171">예 4: hello에서 여러 끝점 간에 동일한 라우팅 'Performance' 트래픽 제어 영역</span><span class="sxs-lookup"><span data-stu-id="c1f57-171">Example 4: Controlling 'Performance' traffic routing between multiple endpoints in hello same region</span></span>

<span data-ttu-id="c1f57-172">Hello 'Performance' 트래픽 라우팅 방법을 특정 지역에 대 한 둘 이상의 끝점이 있는 프로필 사용을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-172">Suppose hello 'Performance' traffic-routing method is used in a profile that has more than one endpoint in a particular region.</span></span> <span data-ttu-id="c1f57-173">기본적으로 트래픽은 toothat 영역 해당 지역에서 사용할 수 있는 모든 끝점에서 동시에 균등 향합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-173">By default, traffic directed toothat region is distributed evenly across all available endpoints in that region.</span></span>

![지역 내 트래픽 분산의'성능' 트래픽 라우팅(기본 동작)][7]

<span data-ttu-id="c1f57-175">유럽 서부에 있는 여러 끝점을 추가하는 대신 해당 끝점을 별도 하위 프로필에서 묶습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-175">Instead of adding multiple endpoints in West Europe, those endpoints are enclosed in a separate child profile.</span></span> <span data-ttu-id="c1f57-176">hello 자식 프로필 toohello 부모 hello만 끝점 서 부 유럽에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-176">hello child profile is added toohello parent as hello only endpoint in West Europe.</span></span> <span data-ttu-id="c1f57-177">hello 자식 프로필에 hello 설정은 해당 지역 내에서 우선 순위 기반 또는 가중치가 적용 된 트래픽 라우팅을 사용 하 여 서 부 유럽와 hello 트래픽 분배로 인해를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-177">hello settings on hello child profile can control hello traffic distribution with West Europe by enabling priority-based or weighted traffic routing within that region.</span></span>

![사용자 지정 지역 내 트래픽 분산을 사용하는 '성능' 트래픽 라우팅][8]

## <a name="example-5-per-endpoint-monitoring-settings"></a><span data-ttu-id="c1f57-179">예제 5: 끝점 기준 모니터링 설정</span><span class="sxs-lookup"><span data-stu-id="c1f57-179">Example 5: Per-endpoint monitoring settings</span></span>

<span data-ttu-id="c1f57-180">사용 하는 경우를 가정해 볼 트래픽 관리자 toosmoothly 레거시 온-프레미스 웹 사이트 tooa 새로운 클라우드 기반 버전에서 Azure에 호스트 트래픽을 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-180">Suppose you are using Traffic Manager toosmoothly migrate traffic from a legacy on-premises web site tooa new Cloud-based version hosted in Azure.</span></span> <span data-ttu-id="c1f57-181">Hello 레거시 사이트에 대 한 toouse hello 홈 페이지 URI toomonitor 사이트 상태를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-181">For hello legacy site, you want toouse hello home page URI toomonitor site health.</span></span> <span data-ttu-id="c1f57-182">Hello 새 버전을 위한 클라우드 기반을 구현 하는 사용자 지정 모니터링 페이지 하지만 (경로가 ' / monitor.aspx') 추가 검사를 포함 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-182">But for hello new Cloud-based version, you are implementing a custom monitoring page (path '/monitor.aspx') that includes additional checks.</span></span>

![트래픽 관리자 끝점 모니터링(기본 동작)][9]

<span data-ttu-id="c1f57-184">트래픽 관리자 프로필의 모니터링 설정을 hello tooall 끝점 단일 프로필 내에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-184">hello monitoring settings in a Traffic Manager profile apply tooall endpoints within a single profile.</span></span> <span data-ttu-id="c1f57-185">중첩 된 프로필을 통해 모니터링 설정을 다른 사이트 toodefine 당 다른 자식 프로필을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1f57-185">With nested profiles, you use a different child profile per site toodefine different monitoring settings.</span></span>

![끝점 기준 설정을 사용하는 트래픽 관리자 끝점 모니터링][10]

## <a name="next-steps"></a><span data-ttu-id="c1f57-187">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1f57-187">Next steps</span></span>

<span data-ttu-id="c1f57-188">[Traffic Manager 프로필](traffic-manager-overview.md)에 대한 자세한 정보</span><span class="sxs-lookup"><span data-stu-id="c1f57-188">Learn more about [Traffic Manager profiles](traffic-manager-overview.md)</span></span>

<span data-ttu-id="c1f57-189">너무 방법에 대해 알아봅니다[트래픽 관리자 프로필 만들기](traffic-manager-create-profile.md)</span><span class="sxs-lookup"><span data-stu-id="c1f57-189">Learn how too[create a Traffic Manager profile](traffic-manager-create-profile.md)</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-nested-profiles/figure-1.png
[2]: ./media/traffic-manager-nested-profiles/figure-2.png
[3]: ./media/traffic-manager-nested-profiles/figure-3.png
[4]: ./media/traffic-manager-nested-profiles/figure-4.png
[5]: ./media/traffic-manager-nested-profiles/figure-5.png
[6]: ./media/traffic-manager-nested-profiles/figure-6.png
[7]: ./media/traffic-manager-nested-profiles/figure-7.png
[8]: ./media/traffic-manager-nested-profiles/figure-8.png
[9]: ./media/traffic-manager-nested-profiles/figure-9.png
[10]: ./media/traffic-manager-nested-profiles/figure-10.png
