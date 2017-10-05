---
title: "ARP 테이블 가져오기: Resource Manager: Azure ExpressRoute 문제 해결 | Microsoft Docs"
description: "이 페이지는 ExpressRoute 회로의 ARP 테이블을 가져오는 방법을 안내합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: 0a6bf1d5-6baf-44dd-87d3-1ebd2fd08bdc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: a65b1ba2998eae33b3e73bd2492fbbf025eb5946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-resource-manager-deployment-model"></a><span data-ttu-id="141ad-103">Resource Manager 배포 모델에서 ARP 테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="141ad-103">Getting ARP tables in the Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="141ad-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="141ad-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="141ad-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="141ad-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="141ad-106">이 문서는 ExpressRoute 회로의 ARP 테이블을 배우는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-106">This article walks you through the steps to learn the ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="141ad-107">이 문서는 간단한 문제를 진단하고 수정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="141ad-108">이 문서는 Microsoft 기술 지원 서비스를 대체하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="141ad-109">아래 설명한 지침으로 문제를 해결할 수 없다면 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 으로 지원 티켓을 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable to solve the problem using the guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="141ad-110">주소 확인 프로토콜(ARP) 및 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="141ad-111">주소 확인 프로토콜(ARP)은 [RFC 826](https://tools.ietf.org/html/rfc826)에 정의된 계층 2 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="141ad-112">ARP는 IP 주소로 이더넷 주소(MAC 주소)를 매핑하는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-112">ARP is used to map the Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="141ad-113">ARP 테이블은 특정 피어링에 대한 ipv4 주소와 MAC 주소 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-113">The ARP table provides a mapping of the ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="141ad-114">ExpressRoute 회로 피어링의 ARP 테이블은 각 인터페이스(기본 및 보조)에 대한 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="141ad-115">온-프레미스 라우터 인터페이스 IP 주소를 MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="141ad-115">Mapping of on-premises router interface ip address to the MAC address</span></span>
2. <span data-ttu-id="141ad-116">ExpressRoute 라우터 인터페이스 IP 주소를 MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="141ad-116">Mapping of ExpressRoute router interface ip address to the MAC address</span></span>
3. <span data-ttu-id="141ad-117">매핑 사용 기간</span><span class="sxs-lookup"><span data-stu-id="141ad-117">Age of the mapping</span></span>

<span data-ttu-id="141ad-118">ARP 테이블은 계층 2 구성의 유효성을 검사하고 기본적인 계층 2 연결 문제를 해결하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="141ad-119">ARP 테이블의 예:</span><span class="sxs-lookup"><span data-stu-id="141ad-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="141ad-120">다음 섹션은 ExpressRoute 에지 라우터가 나타내는 ARP 테이블을 보는 방법을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-120">The following section provides information on how you can view the ARP tables seen by the ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="141ad-121">ARP 테이블을 학습하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="141ad-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="141ad-122">더 진행하기 전에 다음이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-122">Ensure that you have the following before you progress further</span></span>

* <span data-ttu-id="141ad-123">1개 이상 피어링으로 구성된 유효한 ExpressRoute 회로.</span><span class="sxs-lookup"><span data-stu-id="141ad-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="141ad-124">연결 공급자가 완벽히 구성한 회로여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="141ad-125">사용자(또는 연결 공급자)는 이 회로에서 하나 이상의 피어링을 구성했어야 합니다(Azure 개인, Azure 공용 및 Microsoft).</span><span class="sxs-lookup"><span data-stu-id="141ad-125">You (or your connectivity provider) must have configured at least one of the peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="141ad-126">피어링(Azure 개인, Azure 공용 및 Microsoft) 구성에 사용한 IP 주소 범위.</span><span class="sxs-lookup"><span data-stu-id="141ad-126">IP address ranges used for configuring the peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="141ad-127">[Express 경로 라우팅 요구 사항 페이지](expressroute-routing.md) 에서 IP 주소 할당 예제를 검토하여 사용자 측과 Express 경로 측에서 인터페이스에 IP 주소를 매핑하는 방법을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-127">Review the ip address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how ip addresses are mapped to interfaces on your side and on the ExpressRoute side.</span></span> <span data-ttu-id="141ad-128">[ExpressRoute 피어링 구성 페이지](expressroute-howto-routing-arm.md)를 검토하면 피어링 구성에 관한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-128">You can get information on the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="141ad-129">네트워킹 팀/연결 공급자가 제공한 해당 IP 주소에서 사용하는 인터페이스 MAC 주소 정보.</span><span class="sxs-lookup"><span data-stu-id="141ad-129">Information from your networking team / connectivity provider on the MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="141ad-130">최신 Azure용 PowerShell 모듈(1.50 버전 이상)이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-130">You must have the latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-the-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="141ad-131">ExpressRoute 회로의 ARP 테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="141ad-131">Getting the ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="141ad-132">이 섹션은 PowerShell을 사용하여 피어링당 ARP 테이블을 보는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-132">This section provides instructions on how you can view the ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="141ad-133">사용자 또는 연결 공급자는 더 진행하기 전에 피어링을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-133">You or your connectivity provider must have configured the peering before progressing further.</span></span> <span data-ttu-id="141ad-134">각 회로는 두 가지 경로(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="141ad-135">각 경로의 ARP 테이블을 독립적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="141ad-136">Azure 개인 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="141ad-137">다음 cmdlet은 Azure 개인 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-137">The following cmdlet provides the ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="141ad-138">아래의 샘플 출력은 그 경로 중 하나를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-138">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="141ad-139">Azure 공용 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="141ad-140">다음 cmdlet은 Azure 공용 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-140">The following cmdlet provides the ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="141ad-141">아래의 샘플 출력은 그 경로 중 하나를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-141">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="141ad-142">Microsoft 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="141ad-143">다음 cmdlet은 Microsoft 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-143">The following cmdlet provides the ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="141ad-144">아래의 샘플 출력은 그 경로 중 하나를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-144">Sample output is shown below for one of the paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="141ad-145">이 정보를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="141ad-145">How to use this information</span></span>
<span data-ttu-id="141ad-146">피어링의 ARP 테이블을 사용하여 계층 2 구성과 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-146">The ARP table of a peering can be used to determine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="141ad-147">이 섹션은 다양한 시나리오에서 ARP 테이블이 표시되는 모습의 개요를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="141ad-148">회로가 작동 상태일 때 ARP 테이블(예상 상태)</span><span class="sxs-lookup"><span data-stu-id="141ad-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="141ad-149">ARP 테이블은 유효한 IP 주소 및 MAC 주소가 포함된 온-프레미스 측의 항목과 Microsoft 측의 유사한 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-149">The ARP table will have an entry for the on-premises side with a valid IP address and MAC address and a similar entry for the Microsoft side.</span></span> 
* <span data-ttu-id="141ad-150">온-프레미스 IP 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-150">The last octet of the on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="141ad-151">Microsoft IP 주소의 마지막 옥텟은 항상 짝수입니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-151">The last octet of the Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="141ad-152">모든 3개 피어링(기본/보조)에 대해 Microsoft 측에 같은 MAC 주소가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-152">The same MAC address will appear on the Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="141ad-153">온-프레미스/연결 공급자 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="141ad-154">온-프레미스 또는 연결 공급자에 문제가 있는 경우 ARP 테이블에 한 개의 항목만 나타나거나 온-프레미스 MAC 주소가 불완전하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-154">If there are issues with the on-premises or connectivity provider you may see that either only one entry will appear in the ARP table or the on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="141ad-155">Microsoft 측에서 사용된 MAC 주소와 IP 주소 사이의 매핑을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-155">This will show the mapping between the MAC address and IP address used in the Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="141ad-156">또는</span><span class="sxs-lookup"><span data-stu-id="141ad-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="141ad-157">이 문제를 디버그하려면 연결 공급자로 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-157">Open a support request with your connectivity provider to debug such issues.</span></span> <span data-ttu-id="141ad-158">ARP 테이블에 MAC 주소에 매핑된 인터페이스의 IP 주소가 없으면 다음 정보를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-158">If the ARP table does not have IP addresses of the interfaces mapped to MAC addresses, review the following information:</span></span>
> 
> 1. <span data-ttu-id="141ad-159">MSEE-PR과 MSEE 사이의 링크에 할당된 /30 서브넷의 첫 번째 IP 주소가 MSEE-PR의 인터페이스에서 사용되는 경우</span><span class="sxs-lookup"><span data-stu-id="141ad-159">If the first IP address of the /30 subnet assigned for the link between the MSEE-PR and MSEE is used on the interface of MSEE-PR.</span></span> <span data-ttu-id="141ad-160">Azure에서 항상 두 번째 IP 주소를 MSEE에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-160">Azure always uses the second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="141ad-161">고객(C-Tag) 및 서비스(S-Tag) VLAN 태그가 MSEE-PR 및 MSEE 쌍 모두와 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-161">Verify if the customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="141ad-162">Microsoft 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="141ad-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="141ad-163">Microsoft 측에 문제가 있으면 피어링에 대한 ARP 테이블이 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-163">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span> 
* <span data-ttu-id="141ad-164">[Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)으로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="141ad-165">계층 2 연결 문제가 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="141ad-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="141ad-166">Next Steps</span></span>
* <span data-ttu-id="141ad-167">ExpressRoute 회로를 위한 계층 3 구성의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="141ad-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="141ad-168">라우트 요약에서 BGP 세션 상태 확인</span><span class="sxs-lookup"><span data-stu-id="141ad-168">Get route summary to determine the state of BGP sessions</span></span> 
  * <span data-ttu-id="141ad-169">라우트 테이블에서 ExpressRoute에 어떤 접두사가 보급되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="141ad-169">Get route table to determine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="141ad-170">바이트 입출력으로 데이터 전송의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="141ad-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="141ad-171">여전히 문제가 해결되지 않을 경우 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 으로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="141ad-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

