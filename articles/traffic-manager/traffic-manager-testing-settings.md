---
title: "Azure 트래픽 관리자 설정 aaaVerify | Microsoft Docs"
description: "이 문서는 Traffic Manager 설정을 확인하는 데 도움이 됩니다."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="05573-103">Traffic Manager 설정 확인</span><span class="sxs-lookup"><span data-stu-id="05573-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="05573-104">tootest 트래픽 관리자 설정 테스트를 실행할 수 있는 다양 한 위치에서 여러 클라이언트 toohave 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-104">tootest your Traffic Manager settings, you need toohave multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="05573-105">그런 다음 한 번에 하나씩 작동 중지 트래픽 관리자 프로필 끝점 hello 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="05573-105">Then, bring hello endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="05573-106">신속 하 게 (예: 30 초) 한 변경 내용이 전파 되도록 DNS TTL 값 hello 낮게 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-106">Set hello DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="05573-107">Hello Azure 클라우드 서비스 및 테스트 하는 hello 프로필에 대 한 웹 사이트의 IP 주소를 파악 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-107">Know hello IP addresses of your Azure cloud services and websites in hello profile you are testing.</span></span>
* <span data-ttu-id="05573-108">DNS 이름 tooan IP 주소를 확인 하 고 해당 주소를 표시할 수 있는 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-108">Use tools that let you resolve a DNS name tooan IP address and display that address.</span></span>

<span data-ttu-id="05573-109">Hello DNS 이름을 hello 프로필에는 끝점의 tooIP 주소를 확인 하는 toosee 확인.</span><span class="sxs-lookup"><span data-stu-id="05573-109">You are checking toosee that hello DNS names resolve tooIP addresses of hello endpoints in your profile.</span></span> <span data-ttu-id="05573-110">hello 이름은 hello 트래픽 관리자 프로필에에서 정의 된 hello 트래픽 라우팅 방법을와 동일한 방식으로 해결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-110">hello names should resolve in a manner consistent with hello traffic routing method defined in hello Traffic Manager profile.</span></span> <span data-ttu-id="05573-111">와 같은 hello 도구를 사용할 수 있습니다 **nslookup** 또는 **분석** tooresolve DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05573-111">You can use hello tools like **nslookup** or **dig** tooresolve DNS names.</span></span>

<span data-ttu-id="05573-112">hello 다음 예제에서는 테스트할 수 있으려면 트래픽 관리자 프로필.</span><span class="sxs-lookup"><span data-stu-id="05573-112">hello following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="05573-113">Windows에서 nslookup 및 ipconfig를 사용하여 Traffic Manager 프로필을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="05573-114">관리자로 명령 또는 Windows PowerShell 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="05573-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="05573-115">형식 `ipconfig /flushdns` tooflush hello DNS 확인 프로그램 캐시 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-115">Type `ipconfig /flushdns` tooflush hello DNS resolver cache.</span></span>
3. <span data-ttu-id="05573-116">`nslookup <your Traffic Manager domain name>`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="05573-117">예를 들어 다음 명령을 검사 hello hello 접두사가 포함 된 도메인 이름 hello *myapp.contoso*</span><span class="sxs-lookup"><span data-stu-id="05573-117">For example, hello following command checks hello domain name with hello prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="05573-118">일반적인 결과 hello 다음 정보를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="05573-118">A typical result shows hello following information:</span></span>

    + <span data-ttu-id="05573-119">hello DNS 이름 및 IP 주소는 hello DNS 서버 액세스 tooresolve이 트래픽 관리자 도메인 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="05573-119">hello DNS name and IP address of hello DNS server being accessed tooresolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="05573-120">hello 트래픽 관리자 도메인 이름을 입력 한 hello 명령줄에서 "nslookup" 뒤 및 hello IP 주소 toowhich hello 트래픽 관리자 도메인이 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-120">hello Traffic Manager domain name you typed on hello command line after "nslookup" and hello IP address toowhich hello Traffic Manager domain resolves.</span></span> <span data-ttu-id="05573-121">hello 두 번째 IP 주소는 중요 한 toocheck hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-121">hello second IP address is hello important one toocheck.</span></span> <span data-ttu-id="05573-122">Hello 클라우드 서비스나 웹 사이트에 hello는 테스트할 트래픽 관리자 프로필 중 하나에 대 한 공용 가상 IP (VIP) 주소와 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-122">It should match a public virtual IP (VIP) address for one of hello cloud services or websites in hello Traffic Manager profile you are testing.</span></span>

## <a name="how-tootest-hello-failover-traffic-routing-method"></a><span data-ttu-id="05573-123">어떻게 tootest hello 장애 조치 트래픽 라우팅 방법</span><span class="sxs-lookup"><span data-stu-id="05573-123">How tootest hello failover traffic routing method</span></span>

1. <span data-ttu-id="05573-124">모든 끝점을 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05573-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="05573-125">단일 클라이언트를 사용할 경우, Nslookup이나 유사한 유틸리티를 사용하여 회사의 도메인 이름에 대한 DNS 확인을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="05573-126">해당 hello 해결 hello 기본 끝점을 일치 하는 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-126">Ensure that hello resolved IP address matches hello primary endpoint.</span></span>
4. <span data-ttu-id="05573-127">트래픽 관리자 생각 응용 프로그램 hello 하 고 아래로 있도록 파일을 모니터링 하는 hello 제거 또는 기본 끝점이 다운 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="05573-127">Bring down your primary endpoint or remove hello monitoring file so that Traffic Manager thinks that hello application is down.</span></span>
5. <span data-ttu-id="05573-128">Hello 트래픽 관리자 프로필의 DNS-Time-to-live (TTL) hello와는 다시 2 분 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="05573-128">Wait for hello DNS Time-to-Live (TTL) of hello Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="05573-129">예를 들어, DNS TTL이 300초(5분)인 경우 7분을 대기해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="05573-130">Nslookup을 사용하여 DNS 클라이언트 캐시 및 요청 DNS 확인을 플러시하십시오.</span><span class="sxs-lookup"><span data-stu-id="05573-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="05573-131">Windows에서 hello ipconfig /flushdns 명령 사용 하 여 DNS 캐시를 플러시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05573-131">In Windows, you can flush your DNS cache with hello ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="05573-132">해당 hello 해결 경우 보조 끝점을 일치 하는 IP 주소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-132">Ensure that hello resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="05573-133">Hello 프로세스를 각 끝점에를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-133">Repeat hello process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="05573-134">Hello 목록에 hello 다음 끝점의 hello IP 주소를 반환 하는 해당 hello DNS를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-134">Verify that hello DNS returns hello IP address of hello next endpoint in hello list.</span></span> <span data-ttu-id="05573-135">모든 끝점이 다운 되 면 hello 기본 끝점의 hello IP 주소를 다시 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-135">When all endpoints are down, you should obtain hello IP address of hello primary endpoint again.</span></span>

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a><span data-ttu-id="05573-136">Tootest hello 가중치가 트래픽 라우팅 방법을 적용 하는 방법</span><span class="sxs-lookup"><span data-stu-id="05573-136">How tootest hello weighted traffic routing method</span></span>

1. <span data-ttu-id="05573-137">모든 끝점을 실행 상태로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="05573-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="05573-138">단일 클라이언트를 사용할 경우, Nslookup이나 유사한 유틸리티를 사용하여 회사의 도메인 이름에 대한 DNS 확인을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="05573-139">해당 hello 해결 IP 주소는 끝점 중 하 나와 일치를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-139">Ensure that hello resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="05573-140">각 끝점에 대해 DNS 클라이언트 캐시를 플러시하고 2단계와 3단계를 계속 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="05573-141">각 끝점에 대해 서로 다른 IP 주소가 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-tootest-hello-performance-traffic-routing-method"></a><span data-ttu-id="05573-142">어떻게 tootest hello 성능 트래픽 라우팅 방법</span><span class="sxs-lookup"><span data-stu-id="05573-142">How tootest hello performance traffic routing method</span></span>

<span data-ttu-id="05573-143">tooeffectively 성능 트래픽 라우팅 방법, 클라이언트 hello 전 세계 각 지점에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-143">tooeffectively test a performance traffic routing method, you must have clients located in different parts of hello world.</span></span> <span data-ttu-id="05573-144">클라이언트 tootest 사용된 될 수 있는 다른 Azure 지역에 서비스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05573-144">You can create clients in different Azure regions that can be used tootest your services.</span></span> <span data-ttu-id="05573-145">글로벌 네트워크를 사용 하도록 설정한 경우 원격으로 hello world의 다른 부분에서 tooclients 로그인 있고 여기에서 테스트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-145">If you have a global network, you can remotely sign in tooclients in other parts of hello world and run your tests from there.</span></span>

<span data-ttu-id="05573-146">웹 기반 DNS 조회를 해제하고 사용할 수 있는 서비스를 이용합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="05573-147">이 중 일부 도구는 hello 전 세계 여러 위치에서 기능 toocheck DNS 이름 확인을 hello에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-147">Some of these tools give you hello ability toocheck DNS name resolution from various locations around hello world.</span></span> <span data-ttu-id="05573-148">예제를 보려면 "DNS 조회"를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="05573-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="05573-149">Gomez 또는 Keynote와 같은 타사 서비스에 사용 되는 tooconfirm 프로필은 예상 대로 트래픽을 분산 시키고 있는지 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05573-149">Third-party services like Gomez or Keynote can be used tooconfirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05573-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="05573-150">Next steps</span></span>

* [<span data-ttu-id="05573-151">Traffic Manager 트래픽 라우팅 방법 정보</span><span class="sxs-lookup"><span data-stu-id="05573-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="05573-152">Traffic Manager 성능 고려 사항</span><span class="sxs-lookup"><span data-stu-id="05573-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="05573-153">Traffic Manager 성능 저하 상태 문제 해결</span><span class="sxs-lookup"><span data-stu-id="05573-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
