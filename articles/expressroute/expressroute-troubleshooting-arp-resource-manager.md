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
# <a name="getting-arp-tables-in-hello-resource-manager-deployment-model"></a>ARP 테이블 hello 리소스 관리자 배포 모델에서 가져오기
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-troubleshooting-arp-resource-manager.md)
> * [PowerShell - 클래식](expressroute-troubleshooting-arp-classic.md)
> 
> 

이 문서는 hello 단계 toolearn hello ARP ExpressRoute 회로 대 한 테이블을 안내 합니다. 

> [!IMPORTANT]
> 이 문서는 의도 한 toohelp 진단 하 고 간단한 문제를 해결 합니다. 의도 한 toobe Microsoft 지원에 대 한 대체 하지 않습니다. 지원 티켓을 열어야 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 아래에 설명 된 hello 지침을 사용 하 여 없습니다 toosolve hello 문제가 있다면 합니다.
> 
> 

## <a name="address-resolution-protocol-arp-and-arp-tables"></a>주소 확인 프로토콜(ARP) 및 ARP 테이블
주소 확인 프로토콜(ARP)은 [RFC 826](https://tools.ietf.org/html/rfc826)에 정의된 계층 2 프로토콜입니다. ARP는 사용 되는 toomap hello ip 주소와 이더넷 주소 (MAC 주소)입니다.

hello ARP 테이블 hello ipv4 주소와 MAC 주소가 특정 피어 링에 대 한 매핑을 제공합니다. 피어 링는 ExpressRoute 회로 대 한 ARP 테이블 hello hello 다음 (기본 및 보조)에 각 인터페이스에 대 한 정보를 제공 합니다.

1. 온-프레미스 라우터 인터페이스 ip 주소 toohello MAC 주소에 매핑
2. ExpressRoute 라우터 인터페이스 ip 주소 toohello MAC 주소에 매핑
3. Hello 매핑의 보존 기간

ARP 테이블은 계층 2 구성의 유효성을 검사하고 기본적인 계층 2 연결 문제를 해결하는 데 도움을 줍니다. 

ARP 테이블의 예: 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


hello 다음 섹션에서는 정보를 보는 방법을 hello ARP 테이블 hello ExpressRoute에 지 라우터에 표시 합니다. 

## <a name="prerequisites-for-learning-arp-tables"></a>ARP 테이블을 학습하기 위한 필수 조건
Hello 더 진행 하기 전에 다음 있는지 확인 하십시오.

* 1개 이상 피어링으로 구성된 유효한 ExpressRoute 회로. hello 회로 hello 연결 공급자가 완벽 하 게 구성 되어야 합니다. 사용자 (또는 연결 공급자)가 구성 합니다 (개인, Azure 공용 Azure 및 Microsoft) hello 피어 링 중 하나 이상을이 회로에.
* IP 주소 범위 (개인, Azure 공용 Azure 및 Microsoft) hello 피어 링을 구성 하는 데 사용 합니다. Hello hello ip 주소 할당 예 검토 [ExpressRoute 라우팅 요구 사항 페이지](expressroute-routing.md) tooget ip 주소 하는 방법에 대 한 이해가 toointerfaces 편이 및 hello ExpressRoute 쪽에 매핑됩니다. Hello를 검토 하 여 hello 피어 링 구성에 대 한 정보를 읽을 수 [express 경로 피어 링 구성 페이지](expressroute-howto-routing-arm.md)합니다.
* 네트워킹 팀에서 정보 / 이러한 IP 주소와 연결 공급자 인터페이스의 MAC 주소 hello 사용 합니다.
* (1.50 또는 최신 버전) Azure 용 hello 최신 PowerShell 모듈을 있어야 합니다.

## <a name="getting-hello-arp-tables-for-your-expressroute-circuit"></a>ExpressRoute 회로 대 한 hello ARP 테이블을 가져오지
이 섹션에서는 볼 수는 방법에 대 한 지침 hello PowerShell을 사용 하 여 피어 링 당 ARP 테이블을 제공 합니다. 또는 연결 공급자 추가 진행 하기 전에 피어 링 hello 구성 있어야 합니다. 각 회로는 두 가지 경로(기본 및 보조)가 있습니다. 확인할 수 있습니다 하지 hello 각 경로 대 한 ARP 테이블 독립적으로.

### <a name="arp-tables-for-azure-private-peering"></a>Azure 개인 피어링용 ARP 테이블
cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Azure 개인 피어 링

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure private peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Primary

        # ARP table for Azure private peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePrivatePeering -DevicePath Secondary 

Hello 경로 중 하나에 대 한 다음은 샘플 출력

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           10.0.0.1   ffff.eeee.dddd
          0 Microsoft         10.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-azure-public-peering"></a>Azure 공용 피어링용 ARP 테이블
cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Azure 공용 피어 링

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Azure public peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Primary

        # ARP table for Azure public peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType AzurePublicPeering -DevicePath Secondary 


Hello 경로 중 하나에 대 한 다음은 샘플 출력

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           64.0.0.1   ffff.eeee.dddd
          0 Microsoft         64.0.0.2   aaaa.bbbb.cccc


### <a name="arp-tables-for-microsoft-peering"></a>Microsoft 피어링용 ARP 테이블
cmdlet을 다음 hello hello ARP 테이블에 대 한 제공 Microsoft 피어 링

        # Required Variables
        $RG = "<Your Resource Group Name Here>"
        $Name = "<Your ExpressRoute Circuit Name Here>"

        # ARP table for Microsoft peering - Primary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Primary

        # ARP table for Microsoft peering - Secodary path
        Get-AzureRmExpressRouteCircuitARPTable -ResourceGroupName $RG -ExpressRouteCircuitName $Name -PeeringType MicrosoftPeering -DevicePath Secondary 


Hello 경로 중 하나에 대 한 다음은 샘플 출력

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


## <a name="how-toouse-this-information"></a>어떻게 toouse이이 정보
hello 피어 링의 ARP 테이블 용도 toodetermine 2 계층 구성 및 연결의 유효성을 검사 합니다. 이 섹션은 다양한 시나리오에서 ARP 테이블이 표시되는 모습의 개요를 보여줍니다.

### <a name="arp-table-when-a-circuit-is-in-operational-state-expected-state"></a>회로가 작동 상태일 때 ARP 테이블(예상 상태)
* 유효한 IP 주소 및 MAC 주소를 사용 하는 hello 온-프레미스 측에 대 한 항목이 Microsoft의 hello에 대 한 유사 항목 hello ARP 테이블 갖게 됩니다. 
* hello 마지막 8 진수 hello 온-프레미스 ip 주소는 항상 홀수 됩니다.
* hello 마지막 8 진수 hello Microsoft ip 주소는 항상 짝수 됩니다.
* hello 같은 MAC 주소 (기본 / 보조) 모든 3 피어 링에 대 한 Microsoft의 hello에 표시 됩니다. 

        Age InterfaceProperty IpAddress  MacAddress    
        --- ----------------- ---------  ----------    
         10 On-Prem           65.0.0.1   ffff.eeee.dddd
          0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

### <a name="arp-table-when-on-premises--connectivity-provider-side-has-problems"></a>온-프레미스/연결 공급자 측에 문제가 있을 때 ARP 테이블
Hello 온-프레미스 문제가 있는 경우 연결 공급자 ARP 테이블 또는 hello 온-프레미스 MAC 주소 중 하나가 하나의 항목만 hello에 표시 됩니다 표시 될 수 있습니다는 불완전 한 표시 됩니다. 이 MAC 주소 hello 및 Microsoft의 hello에 사용 된 IP 주소 간의 hello 매핑을 표시 됩니다. 
  
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------    
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc

또는
       
       Age InterfaceProperty IpAddress  MacAddress    
       --- ----------------- ---------  ----------   
         0 On-Prem           65.0.0.1   Incomplete
         0 Microsoft         65.0.0.2   aaaa.bbbb.cccc


> [!NOTE]
> 이러한 문제 연결 공급자 toodebug으로 지원 요청을 엽니다. Hello ARP 테이블에 없는 경우 다음 정보 검토 hello tooMAC 주소 hello 인터페이스의 IP 주소에 매핑됩니다.
> 
> 1. Hello hello/30 서브넷의 첫 번째 IP 주소 간의 hello 링크에 대 한 할당 된 경우 hello MSEE PR 및 MSEE MSEE 프로의 hello 인터페이스에서 사용 됩니다. Azure는 항상 MSEEs에 대 한 hello 두 번째 IP 주소를 사용합니다.
> 2. Hello 고객 (C 태그)와 서비스 (S 태그) VLAN 태그 일치 모두 MSEE PR 및 MSEE 쌍에서 확인 하십시오.
> 

### <a name="arp-table-when-microsoft-side-has-problems"></a>Microsoft 측에 문제가 있을 때 ARP 테이블
* Microsoft의 hello에 문제가 있을 경우 피어 링에 대해 표시 된 ARP 테이블에는 표시 되지 않습니다. 
* [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)으로 지원 티켓을 엽니다. 계층 2 연결 문제가 있다고 표시합니다. 

## <a name="next-steps"></a>다음 단계
* ExpressRoute 회로를 위한 계층 3 구성의 유효성 검사
  * BGP 세션의 경로 요약 toodetermine hello 상태 가져오기 
  * 경로 테이블 toodetermine는 접두사는 ExpressRoute를 통해 보급 가져오기
* 바이트 입출력으로 데이터 전송의 유효성 검사
* 여전히 문제가 해결되지 않을 경우 [Microsoft 지원](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) 으로 지원 티켓을 엽니다.

