---
title: "aaaTroubleshoot 경로-PowerShell | Microsoft Docs"
description: "Tootroubleshoot Azure PowerShell을 사용 하 여 hello Azure 리소스 관리자를 배포 하는 모델에 라우팅하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Azure PowerShell을 사용하여 경로 문제 해결
> [!div class="op_single_selector"]
> * [Azure 포털](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
> 
> 

발생 하는 경우 네트워크 연결 문제 tooor Azure 가상 컴퓨터 (VM)에서 경로 미치는 영향 VM 트래픽 흐름. 이 문서에서는 toohelp 추가로 문제를 해결 하는 경로 대 한 진단 기능에 대 한 개요를 제공 합니다.

경로 테이블은 서브넷과 연결되며 해당 서브넷의 모든 NIC(네트워크 인터페이스)에서 유효합니다. 유형의 경로 따라 hello 적용된 tooeach 네트워크 인터페이스를 사용할 수 있습니다.

* **시스템 경로:** 기본적으로 Azure VNet(가상 네트워크)에서 생성된 모든 서브넷에는 로컬 VNet 트래픽, VPN Gateway를 통한 온-프레미스 트래픽 및 인터넷 트래픽을 허용하는 시스템 경로 테이블이 있습니다. 또한 피어링된 VNet에 대한 시스템 경로도 있습니다.
* **BGP 경로:** toonetwork 인터페이스 ExpressRoute 또는 사이트 간 VPN 연결을 통해 전파 합니다. Hello를 참조 하 여 BGP 라우팅에 대 한 자세한 [VPN 게이트웨이 사용한 BGP](../vpn-gateway/vpn-gateway-bgp-overview.md) 및 [ExpressRoute 개요](../expressroute/expressroute-introduction.md) 문서입니다.
* **사용자 정의 경로 (UDR):** 은 강제 터널링 또는 네트워크 가상 어플라이언스를 사용 하는 경우 사이트 간 VPN 통해 트래픽 tooan 온-프레미스 네트워크를 사용자 정의 된 경로 (UDRs) 연결 된 서브넷 경로 테이블을 할 수 있습니다. UDRs 모르는 경우 읽기 hello [사용자 정의 경로](virtual-networks-udr-overview.md#user-defined-routes) 문서.

Hello로 적용된 tooa 네트워크 인터페이스 일 수 있는 다양 한 경로 가능 어려운 toodetermine 집계는 경로 유효 합니다. toohelp VM 네트워크 연결 문제 해결, 네트워크 인터페이스에 대 한 모든 hello 유효 경로 hello Azure 리소스 관리자 배포 모델에서 볼 수 있습니다.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>유효 경로 tootroubleshoot VM 트래픽 흐름을 사용 하 여
이 문서는 예제 tooillustrate tootroubleshoot hello 유효 네트워크 인터페이스에 대 한 라우팅하는 방법으로 시나리오를 따르는 hello를 사용 합니다.

VM (*VM1*) toohello VNet 연결 (*VNet1*, 접두사: 10.9.0.0/16) tooconnect tooa 새로 peered VNet에서 VM(VM3) 실패 (*VNet3*, 10.10.0.0/16 접두사). 있으며 범위 BGP 없음이나 UDRs 라우팅합니다 tooVM1-c 1의 적용 된 네트워크 인터페이스 연결 toohello VM만 시스템 경로 적용 됩니다.

이 문서에서는 toodetermine hello hello 연결 오류, 유효 경로 기능을 사용 하 여 Azure 리소스 관리 배포 모델에서 발생 하는 방법을 설명 합니다.
동일한 단계를 hello hello 예제에서는 시스템 경로만 사용 하는 동안 모든 경로 형식에 대해 사용 되는 toodetermine 인바운드 및 아웃 바운드 연결 오류가 발생할 수 있습니다.

> [!NOTE]
> VM에 연결 된 NIC를 여러 개 있는 경우 각 VM에서 Nic toodiagnose 네트워크 연결 문제 tooand hello에 대 한 유효한 경로 확인 합니다.
> 
> 

### <a name="view-effective-routes-for-a-virtual-machine"></a>가상 컴퓨터에 대한 유효 경로 보기
toosee hello 집계 되 경로 적용 된 tooa VM을 단계를 수행 하는 전체 hello:

### <a name="view-effective-routes-for-a-network-interface"></a>네트워크 인터페이스에 대한 유효 경로 보기
toosee hello 집계 되 경로 적용 된 tooa 네트워크 인터페이스, 단계를 수행 하는 전체 hello:

1. Azure PowerShell 세션 및 로그인 tooAzure를 시작 합니다. Azure PowerShell 모르는 경우 읽기 hello [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서.
2. hello 다음 명령은 반환 이라는 모든 적용 경로 tooa 네트워크 인터페이스 *VM1 NIC1* hello 리소스 그룹에 *g 1*합니다.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > 네트워크 인터페이스의 hello 이름을 모르면 hello 리소스 group.*에서 모든 네트워크 인터페이스의 명령 tooretrieve hello 이름 다음을 입력 합니다.
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   hello 다음 출력은 유사한 toohello 출력이 NIC에 연결 된 각 경로 적용 toohello 서브넷 hello에 대 한 합니다.
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Hello hello 출력에는 다음 사항을 참고 하십시오.
   
   * **이름**: hello 유효 경로 이름을 사용자 지정 경로 대 한 명시적으로 지정 되지 않은 경우 비어 있을 수 있습니다. 
   * **상태**: hello 유효 경로의 상태를 나타냅니다. 가능한 값은 “Active” 또는 “Invalid”입니다.
   * **AddressPrefixes**: CIDR 표기법으로 hello hello 유효한 경로의 주소 접두사를 지정 합니다. 
   * **nextHopType**: hello 경로 지정 하는 hello에 대 한 다음 홉을 나타냅니다. 가능한 값은 *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* 또는 *Null*입니다. UDR에서 *nextHopType* 값이 **Null** 이면 잘못된 경로를 나타낼 수 있습니다. 예를 들어 경우 **nextHopType** 은 *virtualappliance 인* 및 hello 네트워크 가상 어플라이언스 VM이 프로 비전/실행 중 상태입니다. 경우 **nextHopType** 은 *VPNGateway* 및 실행 되 고 있는 게이트웨이가 없는 사용자를 프로 비전/hello 지정 된 VNet에에서, hello 경로 잘못 될 수 있습니다.
   * **NextHopIpAddress**: hello hello 유효한 경로의 다음 홉의 hello IP 주소를 지정 합니다.
   
   hello 다음 명령은 반환 hello 경로 보다 쉽게 tooview 테이블에:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   hello 다음 출력은 앞에서 설명한 hello 시나리오에 대 한 수신 hello 출력의 일부:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. 나열 된 경로 toohello 없습니다는 *WestUS VNet3* VNet (에서 10.10.0.0/16)** 접두사 *WestUS VNet1* (10.9.0.0/16 접두사) hello 이전 단계에서 hello 출력에 있습니다. Hello 다음 그림에에서 나와 있는 것 처럼 VNet 피어 링 링크 hello로 hello *WestUS VNet3* hello에 VNet이 *Disconnected* 상태입니다.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    hello 양방향 링크 VM1 tooVM3 hello에 연결 하지 못했습니다 이유를 설명 하 고 중단 되는 hello 피어 링에 대 한 *WestUS VNet3* VNet입니다. *WestUS-VNet1* 및 *WestUS-VNet3* VNet에 대해 양방향 VNet 피어링 링크를 다시 설정합니다. VNet 피어 링 링크 hello 올바르게 설정 된 후 반환 된 hello 출력 다음과 같습니다.
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Hello 문제를 결정 했으면 추가, 제거 또는 경로 경로 테이블입니다. Hello 되므로 명령 toosee hello 사용 되는 명령 toodo 목록은 다음을 입력 합니다.
   
        Get-Help *-AzureRmRouteConfig

## <a name="considerations"></a>고려 사항
반환 되는 몇 가지 tookeep hello 경로 목록을 검토할 때 염두에서입니다.

* 라우팅은 UDR, BGP 및 시스템 경로 중에서 LPM(가장 긴 접두사 일치)을 기준으로 합니다. Hello로 둘 이상의 경로가 있는 경우 동일 LPM 일치 한 경로 순서에 따라 hello에서 원본에 따라 선택 됩니다.
  
  * 사용자 정의 경로
  * BGP 경로
  * 시스템(기본) 경로
    
    유효한 경로와 모든 hello 사용할 수 경로에 따라 LPM과 일치 하는 유효 경로 볼 수 있습니다. Hello 경로 실제로 평가 되는 방식을 지정 nic를 표시 하 여이 통해 VM에서 연결에 미치는 영향는 훨씬 더 쉽게 tootroubleshoot 특정 경로.
* UDRs 있고 트래픽을 tooa 네트워크 가상 어플라이언스 (NVA)으로 보내는 경우 *virtualappliance 인* 으로 **nextHopType**, hello NVA 수신 hello 트래픽을 IP 전달 설정 되어 있는지 확인 하거나 패킷이 삭제 됩니다. 
* 강제 터널링을 사용 하는 경우 모든 아웃 바운드 인터넷 트래픽이 라우트된 tooon 온-프레미스 됩니다. 인터넷 tooyour 어떻게 hello 온-프레미스에 따라이 설정을 사용 하 여 VM이 작동 하지 않을 수에서 RDP/SSH이이 트래픽을 처리 합니다. 
  다음과 같이 강제 터널링을 사용하도록 설정할 수 있습니다.
  * nextHopType을 VPN Gateway로 지정하고 UDR(사용자 정의 경로) 설정하여 사이트 간 VPN을 사용하는 경우
  * 기본 경로가 BGP를 통해 보급되는 경우
* VNet 트래픽이 toowork를 올바르게 피어 링 인 시스템 경로 대 한 **nextHopType** *VNetPeering* hello 겹치기 VNet의 접두사 범위에 존재 해야 합니다. 이러한 경로 VNet 피어 링 hello에 존재 하지 않는 경우 링크 된 항목이 있습니다.
  * 몇 초 동안 기다린 후 새로 설정된 피어링 링크가 있으면 다시 시도합니다. 긴 toopropagate 경로 tooall hello 네트워크 인터페이스 서브넷에 있는 경우에 따라 걸립니다.
  * 네트워크 보안 그룹 (NSG) 규칙에 미치는 영향 hello 트래픽 흐름. 자세한 내용은 참조 hello [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-powershell.md) 문서.

