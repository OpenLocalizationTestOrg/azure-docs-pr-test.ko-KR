---
title: "aaaInternal 부하 분산 장치 개요 | Microsoft Docs"
description: "내부 부하 분산 장치 및 해당 기능에 대 한 개요를 제공 합니다. Azure와 가능한 시나리오 tooconfigure 내부 끝점에 대 한 부하 분산 장치 작동 방식"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9a901aad224d8821c154e130e142699d57282b25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="d9bd3-103">내부 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="d9bd3-103">Internal load balancer overview</span></span>

<span data-ttu-id="d9bd3-104">Hello 인터넷 연결 부하 분산 장치를 달리 hello 내부 부하 분산 장치 (ILB) hello 클라우드 서비스 또는 VPN tooaccess hello Azure 인프라를 사용 하 여 내 유일한 tooresources를 트래픽을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-104">Unlike hello Internet facing load balancer, hello internal load balancer (ILB) directs traffic only tooresources inside hello cloud service or using VPN tooaccess hello Azure infrastructure.</span></span> <span data-ttu-id="d9bd3-105">hello 인프라 직접 노출 된 tooan 인터넷 끝점 안 됩니다 되도록 액세스 toohello 부하 분산 된 가상 IP 주소 (Vip)의 클라우드 서비스 또는 가상 네트워크를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-105">hello infrastructure restricts access toohello load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed tooan Internet endpoint.</span></span> <span data-ttu-id="d9bd3-106">기간 업무 (LOB) 응용 프로그램 toorun Azure에서 내부 줄 있으며 리소스 온-프레미스 또는 hello 클라우드 내에서 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-106">This enables internal line of business (LOB) applications toorun in Azure and be accessed from within hello cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="d9bd3-107">내부 부하 분산 장치가 필요한 이유</span><span class="sxs-lookup"><span data-stu-id="d9bd3-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="d9bd3-108">Azure ILB(내부 부하 분산)는 클라우드 서비스 또는 지역 범위의 가상 네트워크 내부에 있는 가상 컴퓨터 간의 부하 분산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="d9bd3-109">Hello 사용 하 고 지역 범위가 있는 가상 네트워크 구성에 대 한 정보를 참조 하십시오. [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) hello Azure 블로그에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-109">For information about hello use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in hello Azure blog.</span></span> <span data-ttu-id="d9bd3-110">선호도 그룹에 대해 구성된 기존 가상 네트워크는 ILB를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="d9bd3-111">ILB를 사용 하면 부하 분산의 유형만 hello:</span><span class="sxs-lookup"><span data-stu-id="d9bd3-111">ILB enables hello following types of load balancing:</span></span>

* <span data-ttu-id="d9bd3-112">클라우드 서비스 내에서 가상 컴퓨터 tooa 집합이 hello 내에 있는 가상 컴퓨터에서 동일한 클라우드 서비스 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="d9bd3-112">Within a cloud service, from virtual machines tooa set of virtual machines that reside within hello same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="d9bd3-113">가상 네트워크 내에서 hello 내에 있는 가상 컴퓨터의 hello 가상 네트워크 tooa 집합에서 가상 컴퓨터에서 동일한 클라우드 서비스의 hello 가상 네트워크 (그림 2 참조).</span><span class="sxs-lookup"><span data-stu-id="d9bd3-113">Within a virtual network, from virtual machines in hello virtual network tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 2).</span></span>
* <span data-ttu-id="d9bd3-114">크로스-프레미스 가상 네트워크에 대 한 hello 내에 있는 가상 컴퓨터의 온-프레미스 컴퓨터 tooa 집합에서 동일한 클라우드 서비스의 hello 가상 네트워크 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="d9bd3-114">For a cross-premises virtual network, from on-premises computers tooa set of virtual machines that reside within hello same cloud service of hello virtual network (see Figure 3).</span></span>
* <span data-ttu-id="d9bd3-115">인터넷 연결 다중 계층 응용 프로그램 백 엔드 계층 hello 인터넷에 연결 되지 않습니다 되지만 필요 부하 hello 인터넷 연결 계층에서 트래픽을 분산 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-115">Internet-facing, multi-tier applications in which hello back-end tiers are not Internet-facing but require load balancing for traffic from hello Internet-facing tier.</span></span>
* <span data-ttu-id="d9bd3-116">추가적인 부하 분산 장치 하드웨어 또는 소프트웨어 없이도 Azure에서 호스트되는 LOB 응용 프로그램의 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="d9bd3-117">분산 된 트래픽의 부하를가 하는 컴퓨터의 hello 집합에 온-프레미스 서버를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-117">Including on-premises servers in hello set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="d9bd3-118">인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d9bd3-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="d9bd3-119">hello 웹 계층 인터넷 클라이언트에 대 한 인터넷 연결 끝점 고 부하 분산 된 집합의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-119">hello web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="d9bd3-120">hello 부하 분산 장치에는 TCP 포트 443 (HTTPS) toohello 웹 서버에 대 한 웹 클라이언트에서 들어오는 트래픽을 분산 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-120">hello load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) toohello web servers.</span></span>

<span data-ttu-id="d9bd3-121">저장소에 사용 하는 hello 웹 서버는 ILB 끝점 뒤 hello 데이터베이스 서버는입니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-121">hello database servers are behind an ILB endpoint which hello web servers use for storage.</span></span> <span data-ttu-id="d9bd3-122">이 데이터베이스 서비스 부하 분산 끝점에 트래픽을 hello 데이터베이스 서버 hello ILB 집합에 적절히 분산 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-122">This database service load balanced endpoint, which traffic is load balanced across hello database servers in hello ILB set.</span></span>

<span data-ttu-id="d9bd3-123">다음 그림과 hello hello 인터넷 연결 다중 계층 응용 프로그램 hello 내에서 동일한 클라우드 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-123">hello following image shows hello Internet facing multi-tier application within hello same cloud service.</span></span>

![내부 부하 분산 단일 클라우드 서비스](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="d9bd3-125">그림 1 - 인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d9bd3-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="d9bd3-126">다중 계층 응용 프로그램에 대해 사용할 수 있는 다른 때 사용 하는 하나의 hello 서비스가 ILB hello에 대 한 hello 보다 hello ILB tooa 다른 클라우드 서비스를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-126">Another possible use for a multi-tier application is when hello ILB deployed tooa different cloud service than hello one consuming hello service for hello ILB.</span></span>

<span data-ttu-id="d9bd3-127">클라우드 서비스는 hello 동일한 가상 네트워크를 사용 하 여 toohello ILB 끝점에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-127">Cloud services using hello same virtual network will have access toohello ILB endpoint.</span></span> <span data-ttu-id="d9bd3-128">프런트 엔드 웹 서버 hello 데이터베이스 백 엔드에서 다른 클라우드 서비스에는 이미지 표시 하 고 사용 하 여 hello hello ILB 끝점이 hello 내에서 동일한 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-128">hello following image shows front-end web servers are in a different cloud service from hello database back-end and using hello ILB endpoint within hello same virtual network.</span></span>

![클라우드 서비스 간의 내부 부하 분산](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="d9bd3-130">그림 2 - 다른 클라우드 서비스의 프런트 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="d9bd3-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="d9bd3-131">인트라넷 기간 업무 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d9bd3-131">Intranet line of business applications</span></span>

<span data-ttu-id="d9bd3-132">Hello 온-프레미스 네트워크에서 클라이언트의 트래픽이 VPN 연결 tooAzure 네트워크를 사용 하 여 LOB 서버 hello 집합에서 부하 분산을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-132">Traffic from clients on hello on-premises network get load-balanced across hello set of LOB servers using VPN connection tooAzure network.</span></span>

<span data-ttu-id="d9bd3-133">hello 클라이언트 컴퓨터는 지점 toosite VPN을 사용 하 여 Azure VPN 서비스에서 액세스 tooan IP 주소를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-133">hello client machine will have access tooan IP address from Azure VPN service using point toosite VPN.</span></span> <span data-ttu-id="d9bd3-134">Hello 사용 하 여 hello를 hello ILB 끝점 뒤 호스팅되는 LOB 응용 프로그램 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-134">It allows hello use hello LOB application hosted behind hello ILB endpoint.</span></span>

![내부 부하 분산 지점 toosite VPN을 사용 하 여](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="d9bd3-136">그림 3-hello LB 끝점 뒤에 호스팅되는 LOB 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="d9bd3-136">Figure 3 - LOB applications hosted behind hello LB endpoint</span></span>

<span data-ttu-id="d9bd3-137">LOB hello에 대 한 또 다른 시나리오 toohave hello ILB 끝점이 구성 되어 있는 사이트 toosite VPN toohello 가상 네트워크입니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-137">Another scenario for hello LOB is toohave a site toosite VPN toohello virtual network where hello ILB endpoint is configured.</span></span> <span data-ttu-id="d9bd3-138">이렇게 하면 온-프레미스 네트워크 트래픽을 라우팅할 toobe toohello ILB 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-138">This allows on-premises network traffic toobe routed toohello ILB endpoint.</span></span>

![내부 부하 분산 사이트 toosite VPN을 사용 하 여](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="d9bd3-140">그림 4-온-프레미스 네트워크 트래픽 라우팅할 toohello ILB 끝점</span><span class="sxs-lookup"><span data-stu-id="d9bd3-140">Figure 4 - On-premises network traffic routed toohello ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="d9bd3-141">제한 사항</span><span class="sxs-lookup"><span data-stu-id="d9bd3-141">Limitations</span></span>

<span data-ttu-id="d9bd3-142">내부 부하 분산 장치 구성에서 SNAT가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="d9bd3-143">이 문서의 hello 컨텍스트에서 SNAT tooport 가상 원본 네트워크 주소 변환을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-143">In hello context of this document, SNAT refers tooport masquerading source  network address translation.</span></span>  <span data-ttu-id="d9bd3-144">이 VM에 부하 분산 장치 풀 해야 tooreach hello 해당 내부 부하 분산 장치의 프런트 엔드 IP 주소 tooscenarios 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-144">This applies tooscenarios where a VM in a load balancer pool needs tooreach hello respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="d9bd3-145">이 시나리오는 내부 부하 분산 장치에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="d9bd3-146">연결 실패는 hello 흐름은 부하 분산 된 toohello VM hello 흐름 시작 된 때 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-146">Connection failures will occur when hello flow is load balanced toohello VM which originated hello flow.</span></span> <span data-ttu-id="d9bd3-147">이러한 시나리오에는 프록시 스타일의 부하 분산 장치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d9bd3-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9bd3-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9bd3-148">Next Steps</span></span>

[<span data-ttu-id="d9bd3-149">Azure Load Balancer에 대한 Azure Resource Manager 지원</span><span class="sxs-lookup"><span data-stu-id="d9bd3-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="d9bd3-150">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="d9bd3-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d9bd3-151">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="d9bd3-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="d9bd3-152">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="d9bd3-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d9bd3-153">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="d9bd3-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
