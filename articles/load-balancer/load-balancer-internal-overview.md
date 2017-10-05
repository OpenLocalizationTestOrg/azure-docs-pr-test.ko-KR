---
title: "내부 부하 분산 장치 개요 | Microsoft Docs"
description: "내부 부하 분산 장치 및 해당 기능에 대한 개요입니다. Azure에 대한 부하 분산 장치의 작동 방식 및 내부 끝점을 구성하는 가능한 시나리오입니다."
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
ms.openlocfilehash: d324aaf8ec2c8766d5cf11452158d14c19cba4d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="8b993-103">내부 부하 분산 장치 개요</span><span class="sxs-lookup"><span data-stu-id="8b993-103">Internal load balancer overview</span></span>

<span data-ttu-id="8b993-104">인터넷 연결 부하 분산 장치와는 달리, ILB(내부 부하 분산 장치)는 클라우드 서비스 내의 리소스에만 트래픽을 전달하거나 VPN을 사용하여 Azure 인프라에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="8b993-105">이러한 인프라에서는 가상 네트워크 또는 클라우드 서비스의 부하 분산된 VIP(가상 IP) 주소가 인터넷 끝점에 직접 표시되지 않도록 이러한 주소에 대한 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="8b993-106">이렇게 하면 내부 기간 업무(LOB) 응용 프로그램을 Azure에서 실행하고 온-프레미스의 리소스나 클라우드 내에서 해당 응용 프로그램에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="8b993-107">내부 부하 분산 장치가 필요한 이유</span><span class="sxs-lookup"><span data-stu-id="8b993-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="8b993-108">Azure ILB(내부 부하 분산)는 클라우드 서비스 또는 지역 범위의 가상 네트워크 내부에 있는 가상 컴퓨터 간의 부하 분산을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="8b993-109">지역 범위의 가상 네트워크 사용 및 구성에 대한 자세한 내용은 Azure 블로그의 [지역 가상 네트워크](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8b993-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="8b993-110">선호도 그룹에 대해 구성된 기존 가상 네트워크는 ILB를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="8b993-111">ILB를 통해 다음과 같은 유형의 부하 분산을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="8b993-112">클라우드 서비스 내의 가상 컴퓨터에서 동일한 클라우드 서비스 내에 있는 가상 컴퓨터 집합으로(그림 1 참조)</span><span class="sxs-lookup"><span data-stu-id="8b993-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="8b993-113">가상 네트워크 내의 가상 컴퓨터에서 가상 네트워크의 동일한 클라우드 서비스 내에 있는 가상 컴퓨터 집합으로(그림 2 참조)</span><span class="sxs-lookup"><span data-stu-id="8b993-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="8b993-114">크로스-프레미스 가상 네트워크의 경우 온-프레미스 컴퓨터에서 가상 네트워크의 동일한 클라우드 서비스 내에 있는 가상 컴퓨터 집합으로(그림 3 참조)</span><span class="sxs-lookup"><span data-stu-id="8b993-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="8b993-115">백 엔드 계층이 인터넷에 연결되어 있지 않지만 인터넷 연결 계층에서 전송된 트래픽에 대한 부하 분산을 요구하는 인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b993-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="8b993-116">추가적인 부하 분산 장치 하드웨어 또는 소프트웨어 없이도 Azure에서 호스트되는 LOB 응용 프로그램의 부하를 분산합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="8b993-117">트래픽 부하가 분산되는 컴퓨터 집합에 온-프레미스 서버 포함</span><span class="sxs-lookup"><span data-stu-id="8b993-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="8b993-118">인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b993-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="8b993-119">웹 계층은 인터넷 클라이언트에 대한 인터넷 연결 끝점을 포함하며 부하 분산 집합의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="8b993-120">부하 분산 장치는 TCP 포트 443(HTTPS)에 대해 웹 클라이언트에서 들어오는 트래픽을 웹 서버로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="8b993-121">데이터베이스 서버는 웹 서버가 저장소에 사용하는 ILB 끝점 뒤에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="8b993-122">이 데이터베이스 서비스 부하 분산 끝점의 트래픽은 ILB 집합의 데이터베이스 서버 간에 부하 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="8b993-123">다음 이미지는 동일한 클라우드 서비스 내의 인터넷 연결 다중 계층 응용 프로그램을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![내부 부하 분산 단일 클라우드 서비스](./media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="8b993-125">그림 1 - 인터넷 연결 다중 계층 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b993-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="8b993-126">다중 계층 응용 프로그램에 대한 다른 가능한 사용은 ILB에 대한 서비스를 사용하는 클라우드 서비스가 아닌 다른 클라우드 서비스에 ILB가 배포된 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="8b993-127">동일한 가상 네트워크를 사용하는 클라우드 서비스는 ILB 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="8b993-128">다음 이미지에서는 프런트 엔드 웹 서버가 데이터베이스 백 엔드와 다른 클라우드 서비스에 있고 동일한 가상 네트워크 내의 ILB 끝점을 사용하는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![클라우드 서비스 간의 내부 부하 분산](./media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="8b993-130">그림 2 - 다른 클라우드 서비스의 프런트 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="8b993-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="8b993-131">인트라넷 기간 업무 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b993-131">Intranet line of business applications</span></span>

<span data-ttu-id="8b993-132">온-프레미스 네트워크의 클라이언트에서 전송된 트래픽은 Azure 네트워크에 대한 VPN 연결을 통해 LOB 서버 집합에 부하 분산됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="8b993-133">클라이언트 컴퓨터는 지점과 사이트 간 VPN을 사용하여 Azure VPN 서비스의 IP 주소에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="8b993-134">이 경우 ILB 끝점 뒤에 호스트된 LOB 응용 프로그램을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![지점과 사이트 간 VPN을 사용한 내부 부하 분산](./media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="8b993-136">그림 3 - LB 끝점 뒤에 호스트된 LOB 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="8b993-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="8b993-137">LOB에 대한 다른 시나리오는 ILB 끝점이 구성된 가상 네트워크에 대해 사이트 간 VPN을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="8b993-138">이 경우 온-프레미스 네트워크 트래픽을 ILB 끝점으로 라우팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![사이트 간 VPN을 사용한 내부 부하 분산](./media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="8b993-140">그림 4 - 온-프레미스 네트워크 트래픽을 ILB 끝점으로 라우팅</span><span class="sxs-lookup"><span data-stu-id="8b993-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="8b993-141">제한 사항</span><span class="sxs-lookup"><span data-stu-id="8b993-141">Limitations</span></span>

<span data-ttu-id="8b993-142">내부 부하 분산 장치 구성에서 SNAT가 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="8b993-143">이 문서에 나오는 SNAT는 원본 네트워크 주소 변환을 가장하는 포트를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="8b993-144">이는 부하 분산 장치 풀의 VM이 각 내부 부하 분산 장치의 프런트 엔드 IP 주소에 도달해야 하는 시나리오에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="8b993-145">이 시나리오는 내부 부하 분산 장치에는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="8b993-146">흐름이 처음 시작된 VM으로 부하 분산되면 연결 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="8b993-147">이러한 시나리오에는 프록시 스타일의 부하 분산 장치를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b993-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b993-148">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8b993-148">Next Steps</span></span>

[<span data-ttu-id="8b993-149">Azure Load Balancer에 대한 Azure Resource Manager 지원</span><span class="sxs-lookup"><span data-stu-id="8b993-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="8b993-150">인터넷 연결 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="8b993-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="8b993-151">내부 부하 분산 장치 구성 시작</span><span class="sxs-lookup"><span data-stu-id="8b993-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="8b993-152">부하 분산 장치 배포 모드 구성</span><span class="sxs-lookup"><span data-stu-id="8b993-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8b993-153">부하 분산 장치에 대한 유휴 TCP 시간 제한 설정 구성</span><span class="sxs-lookup"><span data-stu-id="8b993-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
