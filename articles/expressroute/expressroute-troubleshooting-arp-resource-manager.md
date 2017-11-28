---
title: "ARP 테이블 가져오기: Resource Manager: Azure ExpressRoute 문제 해결 | Microsoft Docs"
description: "이 페이지에 지침을 제공 가져오는 hello ARP 테이블 ExpressRoute 회로 대 한"
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
ms.openlocfilehash: c386b031814d40ef6ea3ce5e0eaaab9634470e8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a><span data-ttu-id="da6d4-103">ARP 테이블 hello 리소스 관리자 배포 모델에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="da6d4-103">Getting ARP tables in hello Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="da6d4-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="da6d4-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="da6d4-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="da6d4-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="da6d4-106">이 문서는 hello 단계 toolearn hello ARP ExpressRoute 회로 대 한 테이블을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-106">This article walks you through hello steps toolearn hello ARP tables for your ExpressRoute circuit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="da6d4-107">이 문서는 의도 한 toohelp 진단 하 고 간단한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="da6d4-108">의도 한 toobe Microsoft 지원에 대 한 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="da6d4-109">지원 티켓을 열어야 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 아래에 설명 된 hello 지침을 사용 하 여 없습니다 toosolve hello 문제가 있다면 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-109">You must open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are unable toosolve hello problem using hello guidance described below.</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="da6d4-110">주소 확인 프로토콜(ARP) 및 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="da6d4-111">주소 확인 프로토콜(ARP)은 [RFC 826](https://tools.ietf.org/html/rfc826)에 정의된 계층 2 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-111">Address Resolution Protocol (ARP) is a layer 2 protocol defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="da6d4-112">ARP는 사용 되는 toomap hello ip 주소와 이더넷 주소 (MAC 주소)입니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-112">ARP is used toomap hello Ethernet address (MAC address) with an ip address.</span></span>

<span data-ttu-id="da6d4-113">hello ARP 테이블 hello ipv4 주소와 MAC 주소가 특정 피어 링에 대 한 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-113">hello ARP table provides a mapping of hello ipv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="da6d4-114">피어 링는 ExpressRoute 회로 대 한 ARP 테이블 hello hello 다음 (기본 및 보조)에 각 인터페이스에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary)</span></span>

1. <span data-ttu-id="da6d4-115">온-프레미스 라우터 인터페이스 ip 주소 toohello MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="da6d4-115">Mapping of on-premises router interface ip address toohello MAC address</span></span>
2. <span data-ttu-id="da6d4-116">ExpressRoute 라우터 인터페이스 ip 주소 toohello MAC 주소에 매핑</span><span class="sxs-lookup"><span data-stu-id="da6d4-116">Mapping of ExpressRoute router interface ip address toohello MAC address</span></span>
3. <span data-ttu-id="da6d4-117">Hello 매핑의 보존 기간</span><span class="sxs-lookup"><span data-stu-id="da6d4-117">Age of hello mapping</span></span>

<span data-ttu-id="da6d4-118">ARP 테이블은 계층 2 구성의 유효성을 검사하고 기본적인 계층 2 연결 문제를 해결하는 데 도움을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-118">ARP tables can help validate layer 2 configuration and troubleshooting basic layer 2 connectivity issues.</span></span> 

<span data-ttu-id="da6d4-119">ARP 테이블의 예:</span><span class="sxs-lookup"><span data-stu-id="da6d4-119">Example ARP table:</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


<span data-ttu-id="da6d4-120">hello 다음 섹션에서는 정보를 보는 방법을 hello ARP 테이블 hello ExpressRoute에 지 라우터에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-120">hello following section provides information on how you can view hello ARP tables seen by hello ExpressRoute edge routers.</span></span> 

## <a name="prerequisites-for-learning-arp-tables"></a><span data-ttu-id="da6d4-121">ARP 테이블을 학습하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="da6d4-121">Prerequisites for learning ARP tables</span></span>
<span data-ttu-id="da6d4-122">Hello 더 진행 하기 전에 다음 있는지 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="da6d4-122">Ensure that you have hello following before you progress further</span></span>

* <span data-ttu-id="da6d4-123">1개 이상 피어링으로 구성된 유효한 ExpressRoute 회로.</span><span class="sxs-lookup"><span data-stu-id="da6d4-123">A Valid ExpressRoute circuit configured with at least one peering.</span></span> <span data-ttu-id="da6d4-124">hello 회로 hello 연결 공급자가 완벽 하 게 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="da6d4-125">사용자 (또는 연결 공급자)가 구성 합니다 (개인, Azure 공용 Azure 및 Microsoft) hello 피어 링 중 하나 이상을이 회로에.</span><span class="sxs-lookup"><span data-stu-id="da6d4-125">You (or your connectivity provider) must have configured at least one of hello peerings (Azure private, Azure public and Microsoft) on this circuit.</span></span>
* <span data-ttu-id="da6d4-126">IP 주소 범위 (개인, Azure 공용 Azure 및 Microsoft) hello 피어 링을 구성 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-126">IP address ranges used for configuring hello peerings (Azure private, Azure public and Microsoft).</span></span> <span data-ttu-id="da6d4-127">Hello hello ip 주소 할당 예 검토 [ExpressRoute 라우팅 요구 사항 페이지](expressroute-routing.md) tooget ip 주소 하는 방법에 대 한 이해가 toointerfaces 편이 및 hello ExpressRoute 쪽에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-127">Review hello ip address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how ip addresses are mapped toointerfaces on your side and on hello ExpressRoute side.</span></span> <span data-ttu-id="da6d4-128">Hello를 검토 하 여 hello 피어 링 구성에 대 한 정보를 읽을 수 [express 경로 피어 링 구성 페이지](expressroute-howto-routing-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-128">You can get information on hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-arm.md).</span></span>
* <span data-ttu-id="da6d4-129">네트워킹 팀에서 정보 / 이러한 IP 주소와 연결 공급자 인터페이스의 MAC 주소 hello 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-129">Information from your networking team / connectivity provider on hello MAC addresses of interfaces used with these IP addresses.</span></span>
* <span data-ttu-id="da6d4-130">(1.50 또는 최신 버전) Azure 용 hello 최신 PowerShell 모듈을 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-130">You must have hello latest PowerShell module for Azure (version 1.50 or newer).</span></span>

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="da6d4-131">ExpressRoute 회로 대 한 hello ARP 테이블을 가져오지</span><span class="sxs-lookup"><span data-stu-id="da6d4-131">Getting hello ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="da6d4-132">이 섹션에서는 볼 수는 방법에 대 한 지침 hello PowerShell을 사용 하 여 피어 링 당 ARP 테이블을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-132">This section provides instructions on how you can view hello ARP tables per peering using PowerShell.</span></span> <span data-ttu-id="da6d4-133">또는 연결 공급자 추가 진행 하기 전에 피어 링 hello 구성 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-133">You or your connectivity provider must have configured hello peering before progressing further.</span></span> <span data-ttu-id="da6d4-134">각 회로는 두 가지 경로(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="da6d4-135">확인할 수 있습니다 하지 hello 각 경로 대 한 ARP 테이블 독립적으로.</span><span class="sxs-lookup"><span data-stu-id="da6d4-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="da6d4-136">Azure 개인 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="da6d4-137">cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Azure 개인 피어 링</span><span class="sxs-lookup"><span data-stu-id="da6d4-137">hello following cmdlet provides hello ARP tables for Azure private peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

<span data-ttu-id="da6d4-138">Hello 경로 중 하나에 대 한 다음은 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="da6d4-138">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="da6d4-139">Azure 공용 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-139">ARP tables for Azure public peering</span></span>
<span data-ttu-id="da6d4-140">cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Azure 공용 피어 링</span><span class="sxs-lookup"><span data-stu-id="da6d4-140">hello following cmdlet provides hello ARP tables for Azure public peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


<span data-ttu-id="da6d4-141">Hello 경로 중 하나에 대 한 다음은 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="da6d4-141">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="da6d4-142">Microsoft 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-142">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="da6d4-143">cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Microsoft 피어 링</span><span class="sxs-lookup"><span data-stu-id="da6d4-143">hello following cmdlet provides hello ARP tables for Microsoft peering</span></span>

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


<span data-ttu-id="da6d4-144">Hello 경로 중 하나에 대 한 다음은 샘플 출력</span><span class="sxs-lookup"><span data-stu-id="da6d4-144">Sample output is shown below for one of hello paths</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="da6d4-145">어떻게 toouse이이 정보</span><span class="sxs-lookup"><span data-stu-id="da6d4-145">How toouse this information</span></span>
<span data-ttu-id="da6d4-146">hello 피어 링의 ARP 테이블 용도 toodetermine 2 계층 구성 및 연결의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-146">hello ARP table of a peering can be used toodetermine validate layer 2 configuration and connectivity.</span></span> <span data-ttu-id="da6d4-147">이 섹션은 다양한 시나리오에서 ARP 테이블이 표시되는 모습의 개요를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-147">This section provides an overview of how ARP tables will look under different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a><span data-ttu-id="da6d4-148">회로가 작동 상태일 때 ARP 테이블(예상 상태)</span><span class="sxs-lookup"><span data-stu-id="da6d4-148">ARP table when a circuit is in operational state (expected state)</span></span>
* <span data-ttu-id="da6d4-149">유효한 IP 주소 및 MAC 주소를 사용 하는 hello 온-프레미스 측에 대 한 항목이 Microsoft의 hello에 대 한 유사 항목 hello ARP 테이블 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-149">hello ARP table will have an entry for hello on-premises side with a valid IP address and MAC address and a similar entry for hello Microsoft side.</span></span> 
* <span data-ttu-id="da6d4-150">hello 마지막 8 진수 hello 온-프레미스 ip 주소는 항상 홀수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-150">hello last octet of hello on-premises ip address will always be an odd number.</span></span>
* <span data-ttu-id="da6d4-151">hello 마지막 8 진수 hello Microsoft ip 주소는 항상 짝수 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-151">hello last octet of hello Microsoft ip address will always be an even number.</span></span>
* <span data-ttu-id="da6d4-152">hello 같은 MAC 주소 (기본 / 보조) 모든 3 피어 링에 대 한 Microsoft의 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-152">hello same MAC address will appear on hello Microsoft side for all 3 peerings (primary / secondary).</span></span> 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a><span data-ttu-id="da6d4-153">온-프레미스/연결 공급자 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-153">ARP table when on-premises / connectivity provider side has problems</span></span>
<span data-ttu-id="da6d4-154">Hello 온-프레미스 문제가 있는 경우 연결 공급자 ARP 테이블 또는 hello 온-프레미스 MAC 주소 중 하나가 하나의 항목만 hello에 표시 됩니다 표시 될 수 있습니다는 불완전 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-154">If there are issues with hello on-premises or connectivity provider you may see that either only one entry will appear in hello ARP table or hello on-prem MAC address will show incomplete.</span></span> <span data-ttu-id="da6d4-155">이 MAC 주소 hello 및 Microsoft의 hello에 사용 된 IP 주소 간의 hello 매핑을 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-155">This will show hello mapping between hello MAC address and IP address used in hello Microsoft side.</span></span> 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

<span data-ttu-id="da6d4-156">또는</span><span class="sxs-lookup"><span data-stu-id="da6d4-156">or</span></span>
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> <span data-ttu-id="da6d4-157">이러한 문제 연결 공급자 toodebug으로 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-157">Open a support request with your connectivity provider toodebug such issues.</span></span> <span data-ttu-id="da6d4-158">Hello ARP 테이블에 없는 경우 다음 정보 검토 hello tooMAC 주소 hello 인터페이스의 IP 주소에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-158">If hello ARP table does not have IP addresses of hello interfaces mapped tooMAC addresses, review hello following information:</span></span>
> 
> 1. <span data-ttu-id="da6d4-159">Hello hello/30 서브넷의 첫 번째 IP 주소 간의 hello 링크에 대 한 할당 된 경우 hello MSEE PR 및 MSEE MSEE 프로의 hello 인터페이스에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-159">If hello first IP address of hello /30 subnet assigned for hello link between hello MSEE-PR and MSEE is used on hello interface of MSEE-PR.</span></span> <span data-ttu-id="da6d4-160">Azure는 항상 MSEEs에 대 한 hello 두 번째 IP 주소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-160">Azure always uses hello second IP address for MSEEs.</span></span>
> 2. <span data-ttu-id="da6d4-161">Hello 고객 (C 태그)와 서비스 (S 태그) VLAN 태그 일치 모두 MSEE PR 및 MSEE 쌍에서 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="da6d4-161">Verify if hello customer (C-Tag) and service (S-Tag) VLAN tags match both on MSEE-PR and MSEE pair.</span></span>
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a><span data-ttu-id="da6d4-162">Microsoft 측에 문제가 있을 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="da6d4-162">ARP table when Microsoft side has problems</span></span>
* <span data-ttu-id="da6d4-163">Microsoft의 hello에 문제가 있을 경우 피어 링에 대해 표시 된 ARP 테이블에는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-163">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span> 
* <span data-ttu-id="da6d4-164">[Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)으로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-164">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="da6d4-165">계층 2 연결 문제가 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-165">Specify that you have an issue with layer 2 connectivity.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="da6d4-166">다음 단계</span><span class="sxs-lookup"><span data-stu-id="da6d4-166">Next Steps</span></span>
* <span data-ttu-id="da6d4-167">ExpressRoute 회로를 위한 계층 3 구성의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="da6d4-167">Validate Layer 3 configurations for your ExpressRoute circuit</span></span>
  * <span data-ttu-id="da6d4-168">BGP 세션의 경로 요약 toodetermine hello 상태 가져오기</span><span class="sxs-lookup"><span data-stu-id="da6d4-168">Get route summary toodetermine hello state of BGP sessions</span></span> 
  * <span data-ttu-id="da6d4-169">경로 테이블 toodetermine는 접두사는 ExpressRoute를 통해 보급 가져오기</span><span class="sxs-lookup"><span data-stu-id="da6d4-169">Get route table toodetermine which prefixes are advertised across ExpressRoute</span></span>
* <span data-ttu-id="da6d4-170">바이트 입출력으로 데이터 전송의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="da6d4-170">Validate data transfer by reviewing bytes in / out</span></span>
* <span data-ttu-id="da6d4-171">여전히 문제가 해결되지 않을 경우 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 으로 지원 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="da6d4-171">Open a support ticket with [Microsoft support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

