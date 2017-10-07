---
title: "aaaTroubleshoot 경로-포털 | Microsoft Docs"
description: "Hello Azure 리소스 관리자 배포 사용 하 여 모델의 tootroubleshoot 경로 Azure 포털을 hello 하는 방법에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 경로 문제 해결
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

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. 클릭 **더 많은 서비스**, 클릭 **가상 컴퓨터** 표시 되는 hello 목록에서입니다.
3. VM tootroubleshoot 나타나는 hello 목록에서 선택한 옵션과 함께 VM 블레이드를 표시 합니다.
4. **문제 진단 및 해결**을 클릭하고 일반적인 문제를 선택합니다. 예를 들어 **toomy Windows VM을 연결할 수 없습니다.** 을 선택 합니다.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. 단계는 hello 다음 그림에에서 나와 있는 것 처럼 hello 문제를 아래에 나타납니다.

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    클릭 *유효 경로* hello 권장된 단계 목록에 있습니다.
6. hello **유효 경로** hello 다음 그림에에서 나와 있는 것 처럼 블레이드 나타납니다.

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    VM에 하나의 NIC만 있으면 기본적으로 선택됩니다. NIC 1 개 이상 있는 경우 tooview hello 유효 경로 원하는 hello NIC를 선택 합니다.

   > [!NOTE]
   > Hello VM에 연결 된 hello NIC가 실행 중 상태로, 유효 경로 표시 되지 않습니다. 만 hello 처음 200 유효 경로에 표시 됩니다 hello 포털. Hello 전체 목록을 보려면 클릭 **다운로드**합니다. Hello 다운로드 한.csv 파일 로부터 hello 결과에 필터링 할 수 있습니다.
   >
   >

    Hello hello 출력에는 다음 사항을 참고 하십시오.

   * **소스**: 경로의 hello 유형을 나타냅니다. 시스템 경로는 *Default*로, UDR은 *User*로, 게이트웨이 경로(정적 또는 BGP)는 *VPNGateway*로 표시됩니다.
   * **상태**: hello 유효 경로의 상태를 나타냅니다. 가능한 값은 *Active* 또는 *Invalid*입니다.
   * **AddressPrefixes**: CIDR 표기법으로 hello hello 유효한 경로의 주소 접두사를 지정 합니다.
   * **nextHopType**: hello 경로 지정 하는 hello에 대 한 다음 홉을 나타냅니다. 가능한 값은 *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* 또는 *Null*입니다. UDR에서 *nextHopType* 값이 **Null** 이면 잘못된 경로를 나타낼 수 있습니다. 예를 들어 경우 **nextHopType** 은 *virtualappliance 인* 및 hello 네트워크 가상 어플라이언스 VM이 프로 비전/실행 중 상태입니다. 경우 **nextHopType** 은 *VPNGateway* 및 실행 되 고 있는 게이트웨이가 없는 사용자를 프로 비전/hello 지정 된 VNet에에서, hello 경로 잘못 될 수 있습니다.
7. 나열 된 경로 toohello 없습니다는 *WestUS VNET3* hello에서 VNet (접두사 10.10.0.0/16) *WestUS VNet1* (10.9.0.0/16 접두사) hello 이전 단계에서 hello 그림의 합니다. 다음 그림 hello, hello 피어 링 링크가 hello에 *Disconnected* 상태:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    hello 양방향 링크 VM1 tooVM3 hello에 연결 하지 못했습니다 이유를 설명 하 고 중단 되는 hello 피어 링에 대 한 *WestUS VNet3* VNet입니다.
8. hello 다음 다음과 같은 순서로 hello 경로 hello 양방향 피어 링 링크를 설정한 후

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

강제 터널링 및 경로 평가 대 한 더 문제 해결 시나리오에 대 한 읽기 hello [고려 사항](virtual-network-routes-troubleshoot-portal.md#considerations) 이 문서의 섹션.

### <a name="view-effective-routes-for-a-network-interface"></a>네트워크 인터페이스에 대한 유효 경로 보기
특정 네트워크 인터페이스(NIC)에 대해 네트워크 트래픽 흐름이 영향을 받을 경우 NIC에 대한 유효 경로의 전체 목록을 직접 볼 수 있습니다. toosee hello 집계 되 경로 적용 된 tooa NIC를 다음 단계 완료 hello:

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. **더 많은 서비스**를 클릭한 다음 **네트워크 인터페이스**를 클릭합니다.
3. NIC의 hello 이름에 대 한 hello 목록을 검색 하거나 나타나는 hello 목록에서 선택 합니다. 이 예제에서는 **VM1-NIC1** 이 선택됩니다.
4. 선택 **유효 경로** hello에 **네트워크 인터페이스** hello 다음 그림에에서 나와 있는 것 처럼 블레이드에서:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    hello **범위** 기본값 toohello 네트워크 인터페이스를 선택 합니다.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>경로 테이블에 대한 유효 경로 보기
경로 테이블에 사용자 정의 경로 (UDRs)를 수정 하는 경우 특정 VM에 추가 되는 hello 경로의 tooreview hello 영향을 수도 있습니다. 경로 테이블은 제한 없는 수의 서브넷에 연결될 수 있습니다. 지정 된 경로 테이블에 적용 되는 Nic 모든 hello에 대 한 모든 hello 유효 경로 볼 수 경로 테이블 블레이드를 제공 하는 hello tooswitch 컨텍스트가 필요 없이 합니다.

이 예제에서는 UDR(*UDRoute*)이 경로 테이블(*UDRouteTable*)에 지정됩니다. 이 경로에서 모든 인터넷 트래픽에 보냅니다 *Subnet1* hello에 *WestUS VNet1* 네트워크 가상 어플라이언스 (NVA)를 통해 VNet에서 *e t 2* 의 동일한 VNet hello 합니다. hello 경로 hello 다음 그림에에서 표시 됩니다.

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

경로 테이블의 경우 다음 단계 완료 hello toosee hello의 집계 경로:

1. Azure 포털 https://portal.azure.com toohello를 로그인 합니다.
2. **더 많은 서비스**를 클릭한 다음 **경로 테이블**을 클릭합니다.
3. Hello 경로 테이블에 대 한 검색 hello 목록에 대 한 집계 경로 toosee을 선택 합니다. 이 예제에서는 **UDRouteTable** 이 선택됩니다. 선택한 hello 경로 테이블에 대 한 블레이드 hello 다음 그림에에서 나와 있는 것 처럼 표시 됩니다.

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. 선택 **유효 경로** hello에 **경로 테이블** 블레이드입니다. hello **범위** 선택한 toohello 경로 테이블을 설정 합니다.
5. 경로 테이블에 적용 된 toomultiple 서브넷 될 수 있습니다. 선택 hello **서브넷** tooreview hello 목록에서 원하는 합니다. 이 예제에서는 **Subnet1** 이 선택됩니다.
6. **네트워크 인터페이스**를 선택합니다. 모든 Nic 연결 된 toohello 선택한 서브넷이 나열 됩니다. 이 예제에서는 **VM1-NIC1** 이 선택됩니다.

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Hello NIC를 실행 중인 VM과 연결 없으면 효과적인 경로가 표시 됩니다.
   >
   >

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
  * 네트워크 보안 그룹 (NSG) 규칙에 미치는 영향 hello 트래픽 흐름. 자세한 내용은 참조 hello [네트워크 보안 그룹 문제 해결](virtual-network-nsg-troubleshoot-portal.md) 문서.
