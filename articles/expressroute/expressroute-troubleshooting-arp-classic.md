---
title: "ARP 테이블 가져오기: 클래식: Azure ExpressRoute 문제 해결 | Microsoft Docs"
description: "이 페이지에서는 Express 경로 회로의 ARP 테이블을 가져오는 방법을 제공합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: carolz
editor: tysonn
ms.assetid: b5856acf-03c2-4933-8111-6ce12998d92a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/30/2017
ms.author: ganesr
ms.openlocfilehash: fcc847b7e30fd55ca759830e0254ab7542e7663e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-arp-tables-in-the-classic-deployment-model"></a><span data-ttu-id="a1ee0-103">클래식 배포 모델에서 ARP 테이블 가져오기</span><span class="sxs-lookup"><span data-stu-id="a1ee0-103">Getting ARP tables in the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1ee0-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a1ee0-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="a1ee0-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="a1ee0-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="a1ee0-106">이 문서에서는 Azure Express 경로 회로에 대한 ARP(주소 확인 프로토콜) 테이블을 가져오는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-106">This article walks you through the steps for getting the Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1ee0-107">이 문서는 간단한 문제를 진단하고 수정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-107">This document is intended to help you diagnose and fix simple issues.</span></span> <span data-ttu-id="a1ee0-108">이 문서는 Microsoft 기술 지원 서비스를 대체하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-108">It is not intended to be a replacement for Microsoft support.</span></span> <span data-ttu-id="a1ee0-109">다음 지침을 사용하여 문제를 해결할 수 없는 경우 [Microsoft Azure 도움말+지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)을 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-109">If you can't solve the problem by using the following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="a1ee0-110">주소 확인 프로토콜(ARP) 및 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="a1ee0-111">ARP는 [RFC 826](https://tools.ietf.org/html/rfc826)에 정의된 계층 2 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="a1ee0-112">ARP는 IP 주소로 이더넷 주소(MAC 주소)를 매핑하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-112">ARP is used to map an Ethernet address (MAC address) to an IP address.</span></span>

<span data-ttu-id="a1ee0-113">ARP 테이블은 특정 피어링에 대한 IPv4 주소와 MAC 주소 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-113">An ARP table provides a mapping of the IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="a1ee0-114">Express 경로 회로 피어링의 ARP 테이블은 각 인터페이스(기본 및 보조)에 대한 다음 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-114">The ARP table for an ExpressRoute circuit peering provides the following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="a1ee0-115">온-프레미스 라우터 인터페이스 IP 주소를 MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="a1ee0-115">Mapping of an on-premises router interface IP address to a MAC address</span></span>
2. <span data-ttu-id="a1ee0-116">Express 경로 라우터 인터페이스 IP 주소를 MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="a1ee0-116">Mapping of an ExpressRoute router interface IP address to a MAC address</span></span>
3. <span data-ttu-id="a1ee0-117">매핑 사용 기간</span><span class="sxs-lookup"><span data-stu-id="a1ee0-117">The age of the mapping</span></span>

<span data-ttu-id="a1ee0-118">ARP 테이블은 계층 2 구성의 유효성을 검사하고 기본적인 계층 2 연결 문제를 해결하는 데 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="a1ee0-119">다음은 ARP 테이블의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="a1ee0-120">다음 섹션에서는 Express 경로 에지 라우터에서 표시한 ARP 테이블을 보는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-120">The following section provides information about how to view the ARP tables that are seen by the ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="a1ee0-121">ARP 테이블을 사용하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="a1ee0-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="a1ee0-122">계속하기 전에 다음이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-122">Ensure that you have the following before you continue:</span></span>

* <span data-ttu-id="a1ee0-123">1개 이상 피어링으로 구성된 유효한 Express 경로 회로</span><span class="sxs-lookup"><span data-stu-id="a1ee0-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="a1ee0-124">연결 공급자가 완벽히 구성한 회로여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-124">The circuit must be fully configured by the connectivity provider.</span></span> <span data-ttu-id="a1ee0-125">사용자(또는 연결 공급자)는 이 회로에서 하나 이상의 피어링을 구성했어야 합니다(Azure 개인, Azure 공용 또는 Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a1ee0-125">You (or your connectivity provider) must configure at least one of the peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="a1ee0-126">피어링(Azure 개인, Azure 공용 및 Microsoft) 구성에 사용한 IP 주소 범위</span><span class="sxs-lookup"><span data-stu-id="a1ee0-126">IP address ranges that are used for configuring the peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="a1ee0-127">[ExpressRoute 라우팅 요구 사항 페이지](expressroute-routing.md)에서 IP 주소 할당 예시를 검토하고 사용자와 ExpressRoute 측의 인터페이스에 IP 주소를 매핑하는 방법을 이해합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-127">Review the IP address assignment examples in the [ExpressRoute routing requirements page](expressroute-routing.md) to get an understanding of how IP addresses are mapped to interfaces on your aise and on the ExpressRoute side.</span></span> <span data-ttu-id="a1ee0-128">[ExpressRoute 피어링 구성 페이지](expressroute-howto-routing-classic.md)를 검토하면 피어링 구성에 관한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-128">You can get information about the peering configuration by reviewing the [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="a1ee0-129">해당 IP 주소와 함께 사용되는 인터페이스의 MAC 주소에 대한 네트워킹 팀 또는 연결 공급자가 제공한 정보</span><span class="sxs-lookup"><span data-stu-id="a1ee0-129">Information from your networking team or connectivity provider about the MAC addresses of the interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="a1ee0-130">Azure용 최신 Windows PowerShell 모듈(1.50 이상)</span><span class="sxs-lookup"><span data-stu-id="a1ee0-130">The latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="a1ee0-131">Express 경로 회로에 대한 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="a1ee0-132">이 섹션에서는 PowerShell을 사용하여 피어링의 각 형식에 대한 ARP 테이블을 표시하는 방법에 대한 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-132">This section provides instructions about how to view the ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="a1ee0-133">계속하기 전에 연결 공급자가 또는 피어링을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-133">Before you continue, either you or your connectivity provider needs to configure the peering.</span></span> <span data-ttu-id="a1ee0-134">각 회로는 두 가지 경로(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="a1ee0-135">각 경로의 ARP 테이블을 독립적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-135">You can check the ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="a1ee0-136">Azure 개인 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="a1ee0-137">다음 cmdlet은 Azure 개인 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-137">The following cmdlet provides the ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="a1ee0-138">경로 중 하나에 대한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-138">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="a1ee0-139">Azure 공용 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="a1ee0-140">다음 cmdlet은 Azure 공용 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-140">The following cmdlet provides the ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="a1ee0-141">경로 중 하나에 대한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-141">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="a1ee0-142">경로 중 하나에 대한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-142">Following is sample output for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="a1ee0-143">Microsoft 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="a1ee0-144">다음 cmdlet은 Microsoft 피어링용 ARP 테이블을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-144">The following cmdlet provides the ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="a1ee0-145">아래의 샘플 출력은 그 경로 중 하나를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-145">Sample output is shown below for one of the paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-to-use-this-information"></a><span data-ttu-id="a1ee0-146">이 정보를 사용하는 방법</span><span class="sxs-lookup"><span data-stu-id="a1ee0-146">How to use this information</span></span>
<span data-ttu-id="a1ee0-147">피어링의 ARP 테이블을 사용하여 계층 2 구성과 연결의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-147">The ARP table of a peering can be used to validate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="a1ee0-148">이 섹션은 다양한 시나리오에서 ARP 테이블이 표시되는 방법의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="a1ee0-149">회로가 작동 (예상) 상태일 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="a1ee0-150">ARP 테이블은 유효한 IP 주소 및 MAC 주소가 포함된 온-프레미스 측의 항목과 Microsoft 측의 유사한 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-150">The ARP table has an entry for the on-premises side with a valid IP and MAC address, and a similar entry for the Microsoft side.</span></span>
* <span data-ttu-id="a1ee0-151">온-프레미스 IP 주소의 마지막 옥텟은 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-151">The last octet of the on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="a1ee0-152">Microsoft IP 주소의 마지막 옥텟은 항상 짝수입니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-152">The last octet of the Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="a1ee0-153">세 개 피어링(기본/보조) 모두에 대해 Microsoft 쪽에 같은 MAC 주소가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-153">The same MAC address appears on the Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-the-connectivity-provider-side-has-problems"></a><span data-ttu-id="a1ee0-154">온-프레미스 또는 연결 공급자 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-154">ARP table when it's on-premises or when the connectivity-provider side has problems</span></span>
 <span data-ttu-id="a1ee0-155">ARP 테이블에 하나의 항목만이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-155">Only one entry appears in the ARP table.</span></span> <span data-ttu-id="a1ee0-156">Microsoft 측에서 사용된 MAC 주소와 IP 주소 사이의 매핑을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-156">It shows the mapping between the MAC address and the IP address that's used on the Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="a1ee0-157">다음과 같은 문제가 발생하면 문제를 해결하는 연결 공급자를 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-157">If you experience an issue like this, open a support request with your connectivity provider to resolve it.</span></span>
> 
> 

### <a name="arp-table-when-the-microsoft-side-has-problems"></a><span data-ttu-id="a1ee0-158">Microsoft 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="a1ee0-158">ARP table when the Microsoft side has problems</span></span>
* <span data-ttu-id="a1ee0-159">Microsoft 측에 문제가 있으면 피어링에 대한 ARP 테이블이 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-159">You will not see an ARP table shown for a peering if there are issues on the Microsoft side.</span></span>
* <span data-ttu-id="a1ee0-160">[Microsoft Azure 도움말+지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)을 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="a1ee0-161">계층 2 연결 문제가 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1ee0-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a1ee0-162">Next steps</span></span>
* <span data-ttu-id="a1ee0-163">Express 경로 회로에 대한 계층 3 구성의 유효성 검사:</span><span class="sxs-lookup"><span data-stu-id="a1ee0-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="a1ee0-164">라우트 요약을 가져와서 BGP 세션의 상태 확인</span><span class="sxs-lookup"><span data-stu-id="a1ee0-164">Get a route summary to determine the state of BGP sessions.</span></span>
  * <span data-ttu-id="a1ee0-165">라우트 테이블에서 Express 경로에 접두사가 보급되었는지 확인</span><span class="sxs-lookup"><span data-stu-id="a1ee0-165">Get a route table to determine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="a1ee0-166">바이트 입출력을 검토하여 데이터 전송의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="a1ee0-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="a1ee0-167">여전히 문제가 해결되지 않을 경우 [Microsoft Azure 도움말+지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 을 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a1ee0-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

