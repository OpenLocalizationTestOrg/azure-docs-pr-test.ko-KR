---
title: "ARP 테이블 가져오기: 클래식: Azure ExpressRoute 문제 해결 | Microsoft Docs"
description: "이 페이지를 ExpressRoute 회로 대 한 ARP 가져오는 hello에 대 한 지침 표를 제공 합니다."
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
ms.openlocfilehash: 2b01304a38fa0e0def27dbd7c391d7ad8bbdabff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-arp-tables-in-hello-classic-deployment-model"></a><span data-ttu-id="dd999-103">ARP 테이블 hello 클래식 배포 모델에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="dd999-103">Getting ARP tables in hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dd999-104">PowerShell - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dd999-104">PowerShell - Resource Manager</span></span>](expressroute-troubleshooting-arp-resource-manager.md)
> * [<span data-ttu-id="dd999-105">PowerShell - 클래식</span><span class="sxs-lookup"><span data-stu-id="dd999-105">PowerShell - Classic</span></span>](expressroute-troubleshooting-arp-classic.md)
> 
> 

<span data-ttu-id="dd999-106">이 문서에서는 Azure express 경로 회로 대 한 hello 프로토콜 ARP (주소 확인) 테이블을 가져오기 위한 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-106">This article walks you through hello steps for getting hello Address Resolution Protocol (ARP) tables for your Azure ExpressRoute circuit.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd999-107">이 문서는 의도 한 toohelp 진단 하 고 간단한 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-107">This document is intended toohelp you diagnose and fix simple issues.</span></span> <span data-ttu-id="dd999-108">의도 한 toobe Microsoft 지원에 대 한 대체 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-108">It is not intended toobe a replacement for Microsoft support.</span></span> <span data-ttu-id="dd999-109">Hello 지침을 사용 하 여 hello 문제를 해결할 수 없는 경우와 지원 요청을 개시 [Microsoft Azure 도움말 + 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-109">If you can't solve hello problem by using hello following guidance, open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a><span data-ttu-id="dd999-110">주소 확인 프로토콜(ARP) 및 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-110">Address Resolution Protocol (ARP) and ARP tables</span></span>
<span data-ttu-id="dd999-111">ARP는 [RFC 826](https://tools.ietf.org/html/rfc826)에 정의된 계층 2 프로토콜입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-111">ARP is a Layer 2 protocol that's defined in [RFC 826](https://tools.ietf.org/html/rfc826).</span></span> <span data-ttu-id="dd999-112">ARP 사용 되는 toomap 이더넷 주소 (MAC 주소) tooan IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-112">ARP is used toomap an Ethernet address (MAC address) tooan IP address.</span></span>

<span data-ttu-id="dd999-113">ARP 테이블 hello IPv4 주소와 MAC 주소가 특정 피어 링에 대 한 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-113">An ARP table provides a mapping of hello IPv4 address and MAC address for a particular peering.</span></span> <span data-ttu-id="dd999-114">피어 링는 ExpressRoute 회로 대 한 ARP 테이블 hello를 hello를 다음 (기본 및 보조)에 각 인터페이스에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-114">hello ARP table for an ExpressRoute circuit peering provides hello following information for each interface (primary and secondary):</span></span>

1. <span data-ttu-id="dd999-115">온-프레미스 라우터 인터페이스 IP 주소 tooa MAC 주소 매핑</span><span class="sxs-lookup"><span data-stu-id="dd999-115">Mapping of an on-premises router interface IP address tooa MAC address</span></span>
2. <span data-ttu-id="dd999-116">ExpressRoute 라우터 인터페이스 IP 주소 tooa MAC 주소 매핑</span><span class="sxs-lookup"><span data-stu-id="dd999-116">Mapping of an ExpressRoute router interface IP address tooa MAC address</span></span>
3. <span data-ttu-id="dd999-117">hello 매핑의 hello 보존 기간</span><span class="sxs-lookup"><span data-stu-id="dd999-117">hello age of hello mapping</span></span>

<span data-ttu-id="dd999-118">ARP 테이블은 계층 2 구성의 유효성을 검사하고 기본적인 계층 2 연결 문제를 해결하는 데 도움을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-118">ARP tables can help with validating Layer 2 configuration and with troubleshooting basic Layer 2 connectivity issues.</span></span>

<span data-ttu-id="dd999-119">다음은 ARP 테이블의 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-119">Following is an example of an ARP table:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="dd999-120">다음 단원을 hello tooview hello ExpressRoute에 지 라우터에 게 표시 되는 ARP 테이블 hello 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-120">hello following section provides information about how tooview hello ARP tables that are seen by hello ExpressRoute edge routers.</span></span>

## <a name="prerequisites-for-using-arp-tables"></a><span data-ttu-id="dd999-121">ARP 테이블을 사용하기 위한 필수 조건</span><span class="sxs-lookup"><span data-stu-id="dd999-121">Prerequisites for using ARP tables</span></span>
<span data-ttu-id="dd999-122">계속 하기 전에 hello 다음 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-122">Ensure that you have hello following before you continue:</span></span>

* <span data-ttu-id="dd999-123">1개 이상 피어링으로 구성된 유효한 Express 경로 회로</span><span class="sxs-lookup"><span data-stu-id="dd999-123">A valid ExpressRoute circuit that's configured with at least one peering.</span></span> <span data-ttu-id="dd999-124">hello 회로 hello 연결 공급자가 완벽 하 게 구성 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-124">hello circuit must be fully configured by hello connectivity provider.</span></span> <span data-ttu-id="dd999-125">사용자 (또는 연결 공급자)이이 회로에 hello 피어 링 (개인, Azure 공용 Azure, 또는 Microsoft) 중 하나 이상으로 구성 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-125">You (or your connectivity provider) must configure at least one of hello peerings (Azure private, Azure public, or Microsoft) on this circuit.</span></span>
* <span data-ttu-id="dd999-126">Hello 피어 링 (개인, Azure 공용 Azure 및 Microsoft)를 구성 하는 데 사용 되는 IP 주소 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-126">IP address ranges that are used for configuring hello peerings (Azure private, Azure public, and Microsoft).</span></span> <span data-ttu-id="dd999-127">Hello hello IP 주소 할당 예 검토 [ExpressRoute 라우팅 요구 사항 페이지](expressroute-routing.md) tooget IP 주소는 방법을 이해 toointerfaces hello ExpressRoute 쪽 및 사용자 aise에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-127">Review hello IP address assignment examples in hello [ExpressRoute routing requirements page](expressroute-routing.md) tooget an understanding of how IP addresses are mapped toointerfaces on your aise and on hello ExpressRoute side.</span></span> <span data-ttu-id="dd999-128">Hello를 검토 하 여 hello 피어 링 구성에 대 한 정보를 읽을 수 [express 경로 피어 링 구성 페이지](expressroute-howto-routing-classic.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-128">You can get information about hello peering configuration by reviewing hello [ExpressRoute peering configuration page](expressroute-howto-routing-classic.md).</span></span>
* <span data-ttu-id="dd999-129">이러한 IP 주소에 사용 되는 hello 인터페이스의 MAC 주소 hello에 대 한 네트워킹 팀 또는 연결 공급자 로부터 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-129">Information from your networking team or connectivity provider about hello MAC addresses of hello interfaces that are used with these IP addresses.</span></span>
* <span data-ttu-id="dd999-130">hello 최신 Windows PowerShell 모듈 (버전 1.50) Azure에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-130">hello latest Windows PowerShell module for Azure (version 1.50 or later).</span></span>

## <a name="arp-tables-for-your-expressroute-circuit"></a><span data-ttu-id="dd999-131">Express 경로 회로에 대한 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-131">ARP tables for your ExpressRoute circuit</span></span>
<span data-ttu-id="dd999-132">이 섹션에서는 각 유형의 PowerShell을 사용 하 여 피어 링에 대해 tooview hello ARP 테이블 하는 방법에 대 한 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-132">This section provides instructions about how tooview hello ARP tables for each type of peering by using PowerShell.</span></span> <span data-ttu-id="dd999-133">계속 하기 전에 사용자 또는 연결 공급자가 tooconfigure hello 피어 링입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-133">Before you continue, either you or your connectivity provider needs tooconfigure hello peering.</span></span> <span data-ttu-id="dd999-134">각 회로는 두 가지 경로(기본 및 보조)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-134">Each circuit has two paths (primary and secondary).</span></span> <span data-ttu-id="dd999-135">확인할 수 있습니다 하지 hello 각 경로 대 한 ARP 테이블 독립적으로.</span><span class="sxs-lookup"><span data-stu-id="dd999-135">You can check hello ARP table for each path independently.</span></span>

### <a name="arp-tables-for-azure-private-peering"></a><span data-ttu-id="dd999-136">Azure 개인 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-136">ARP tables for Azure private peering</span></span>
<span data-ttu-id="dd999-137">cmdlet을 다음 hello Azure 개인 피어 링 용 hello ARP 테이블을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-137">hello following cmdlet provides hello ARP tables for Azure private peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure private peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Primary

        # ARP table for Azure private peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Private -Path Secondary

<span data-ttu-id="dd999-138">다음은 샘플 출력 hello 경로 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-138">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a><span data-ttu-id="dd999-139">Azure 공용 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-139">ARP tables for Azure public peering:</span></span>
<span data-ttu-id="dd999-140">cmdlet을 다음 hello Azure 공용 피어 링에 대 한 hello ARP 테이블을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-140">hello following cmdlet provides hello ARP tables for Azure public peering:</span></span>

        # Required variables
        $ckt = "<your Service Key here>

        # ARP table for Azure public peering--primary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Primary

        # ARP table for Azure public peering--secondary path
        Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Public -Path Secondary

<span data-ttu-id="dd999-141">다음은 샘플 출력 hello 경로 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-141">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1 ffff.eeee.dddd
          0 Microsoft         10.0.0.2 aaaa.bbbb.cccc


<span data-ttu-id="dd999-142">다음은 샘플 출력 hello 경로 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-142">Following is sample output for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1 ffff.eeee.dddd
          0 Microsoft         64.0.0.2 aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a><span data-ttu-id="dd999-143">Microsoft 피어링용 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-143">ARP tables for Microsoft peering</span></span>
<span data-ttu-id="dd999-144">cmdlet을 다음 hello Microsoft 피어 링 용 hello ARP 테이블을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-144">hello following cmdlet provides hello ARP tables for Microsoft peering:</span></span>

    # ARP table for Microsoft peering--primary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Primary

    # ARP table for Microsoft peering--secondary path
    Get-AzureDedicatedCircuitPeeringArpInfo -ServiceKey $ckt -AccessType Microsoft -Path Secondary


<span data-ttu-id="dd999-145">Hello 경로 중 하나에 대 한 샘플 출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-145">Sample output is shown below for one of hello paths:</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a><span data-ttu-id="dd999-146">어떻게 toouse이이 정보</span><span class="sxs-lookup"><span data-stu-id="dd999-146">How toouse this information</span></span>
<span data-ttu-id="dd999-147">hello 피어 링의 ARP 테이블 계층 2 toovalidate 사용 하는 구성 및 연결 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-147">hello ARP table of a peering can be used toovalidate Layer 2 configuration and connectivity.</span></span> <span data-ttu-id="dd999-148">이 섹션은 다양한 시나리오에서 ARP 테이블이 표시되는 방법의 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-148">This section provides an overview of how ARP tables look in different scenarios.</span></span>

### <a name="arp-table-when-a-circuit-is-in-an-operational-expected-state"></a><span data-ttu-id="dd999-149">회로가 작동 (예상) 상태일 때 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-149">ARP table when a circuit is in an operational (expected) state</span></span>
* <span data-ttu-id="dd999-150">Microsoft의 hello에 대 한 유사 항목 hello ARP 테이블에 유효한 IP 및 MAC 주소는 온-프레미스 쪽 hello에 대 한 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-150">hello ARP table has an entry for hello on-premises side with a valid IP and MAC address, and a similar entry for hello Microsoft side.</span></span>
* <span data-ttu-id="dd999-151">hello 마지막 8 진수 단위 값 hello 온-프레미스 IP 주소는 항상 홀수입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-151">hello last octet of hello on-premises IP address is always an odd number.</span></span>
* <span data-ttu-id="dd999-152">hello 마지막 8 진수 단위 값 hello Microsoft IP 주소는 항상 짝수입니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-152">hello last octet of hello Microsoft IP address is always an even number.</span></span>
* <span data-ttu-id="dd999-153">hello hello 모든 세 피어 링 (주/보조)에 대 한 Microsoft의 같은 MAC 주소를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-153">hello same MAC address appears on hello Microsoft side for all three peerings (primary/secondary).</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1 ffff.eeee.dddd
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

### <a name="arp-table-when-its-on-premises-or-when-hello-connectivity-provider-side-has-problems"></a><span data-ttu-id="dd999-154">온-프레미스 또는 때 hello 연결 공급자 측에 문제가 있는 경우 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-154">ARP table when it's on-premises or when hello connectivity-provider side has problems</span></span>
 <span data-ttu-id="dd999-155">Hello ARP 테이블에에서 항목이 하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-155">Only one entry appears in hello ARP table.</span></span> <span data-ttu-id="dd999-156">Hello MAC 주소와 Microsoft의 hello에 사용 되는 hello IP 주소 간의 hello 매핑을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-156">It shows hello mapping between hello MAC address and hello IP address that's used on hello Microsoft side.</span></span>

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
          0 Microsoft         65.0.0.2 aaaa.bbbb.cccc

> [!NOTE]
> <span data-ttu-id="dd999-157">다음과 같은 문제가 발생 하면 기술 지원을 열고 연결 공급자 tooresolve를 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-157">If you experience an issue like this, open a support request with your connectivity provider tooresolve it.</span></span>
> 
> 

### <a name="arp-table-when-hello-microsoft-side-has-problems"></a><span data-ttu-id="dd999-158">Microsoft의 hello에 문제가 있는 경우 ARP 테이블</span><span class="sxs-lookup"><span data-stu-id="dd999-158">ARP table when hello Microsoft side has problems</span></span>
* <span data-ttu-id="dd999-159">Microsoft의 hello에 문제가 있을 경우 피어 링에 대해 표시 된 ARP 테이블에는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-159">You will not see an ARP table shown for a peering if there are issues on hello Microsoft side.</span></span>
* <span data-ttu-id="dd999-160">[Microsoft Azure 도움말+지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)을 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-160">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="dd999-161">계층 2 연결 문제가 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-161">Specify that you have an issue with Layer 2 connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd999-162">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dd999-162">Next steps</span></span>
* <span data-ttu-id="dd999-163">Express 경로 회로에 대한 계층 3 구성의 유효성 검사:</span><span class="sxs-lookup"><span data-stu-id="dd999-163">Validate Layer 3 configurations for your ExpressRoute circuit:</span></span>
  * <span data-ttu-id="dd999-164">BGP 세션의 경로 요약 toodetermine hello 상태를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-164">Get a route summary toodetermine hello state of BGP sessions.</span></span>
  * <span data-ttu-id="dd999-165">ExpressRoute에서 어떤 접두사가 알려 졌는 경로 테이블 toodetermine를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-165">Get a route table toodetermine which prefixes are advertised across ExpressRoute.</span></span>
* <span data-ttu-id="dd999-166">바이트 입출력을 검토하여 데이터 전송의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="dd999-166">Validate data transfer by reviewing bytes in and out.</span></span>
* <span data-ttu-id="dd999-167">여전히 문제가 해결되지 않을 경우 [Microsoft Azure 도움말+지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 을 사용하여 지원 요청을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dd999-167">Open a support request with [Microsoft Azure Help+support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) if you are still experiencing issues.</span></span>

