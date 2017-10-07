---
title: "가상 네트워크 피어 링 aaaAzure | Microsoft Docs"
description: "Azure의 가상 네트워크 피어링에 대해 알아봅니다."
services: virtual-network
documentationcenter: na
author: NarayanAnnamalai
manager: jefco
editor: tysonn
ms.assetid: eb0ba07d-5fee-4db0-b1cb-a569b7060d2a
ms.service: virtual-network
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: narayan
ms.openlocfilehash: 46a14b416a7d4389f79a3cd7c55e388b5d312577
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-network-peering"></a>가상 네트워크 피어링
가상 네트워크 피어 링 수 있도록 하면 tooconnect 2에서 가상 네트워크를 통해 동일한 지역 hello hello Azure 백본 네트워크입니다. 겹치기, hello 두 가상 네트워크 연결을 위해 하나의 단위로 표시 됩니다. hello 두 가상 네트워크는 여전히 별도 리소스 그룹으로 관리 하지만 hello 가상 네트워크 겹치기 수의 가상 컴퓨터와 서로 직접 통신할 개인 IP 주소를 사용 하 여 합니다.

hello의 가상 컴퓨터 간에 hello 트래픽 가상 네트워크를 겹치기 hello hello의 가상 컴퓨터 간에 트래픽 라우팅됩니다 처럼 Azure 인프라를 통해 라우팅되어 동일한 가상 네트워크입니다. 가상 네트워크 피어 링을 사용 하 여 hello 이점 중 일부는 다음과 같습니다.

* 다른 가상 네트워크에 있는 리소스 간에 짧은 대기 시간, 높은 대역폭 연결
* 네트워크 장치 및 peered 가상 네트워크의 지점에 전송으로 VPN 게이트웨이와 같은 hello 기능 toouse 리소스입니다.
* hello 기능 toopeer 두 가상 네트워크 hello Azure 리소스 관리자 배포 모델을 통해 만든 또는 hello 클래식 배포 모델을 통해 만든 리소스 관리자 tooa 가상 네트워크를 통해 만들어진 toopeer 하나의 가상 네트워크입니다. 읽기 hello [이해 Azure 배포 모델](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 두 Azure 배포 모델 간의 차이 hello에 대 한 자세한 문서 toolearn 합니다.

## <a name="requirements-constraints"></a>요구 사항 및 제약 조건

* hello 겹치기 가상 네트워크에에서 존재 해야 hello 동일한 Azure 지역입니다. [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V)를 사용하여 다른 Azure 지역에서 가상 네트워크를 연결할 수 있습니다.
* hello 가상 네트워크 겹치기 있어야 겹치지 않는 IP 주소 공간입니다.
* 가상 네트워크가 다른 가상 네트워크와 피어링되면 주소 공간을 추가하거나 가상 네트워크에서 삭제할 수 없습니다.
* 가상 네트워크 피어링은 두 개의 가상 네트워크 간에 가능합니다. 피어링을 통해 파생된 전이적 관계가 없습니다. 예를 들어 virtualNetworkA virtualNetworkB와 겹치기는 경우 virtualNetworkB virtualNetworkC와 겹치기는 virtualNetworkA은 *하지* 겹치기 toovirtualNetworkC 합니다.
* 권한 있는 사용자 긴로 서로 다른 두 구독에 있는 가상 네트워크 피어 링 할 수 있습니다 (참조 [특정 사용 권한이](create-peering-different-deployment-models-subscriptions.md#permissions)) 둘 다의 구독 hello 피어 링 권한을 부여 하 고 hello 구독은 연결된 toohello 동일한 Azure Active Directory 테 넌 트입니다. 사용할 수는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) 구독에서 가상 네트워크 tooconnect toodifferent Active Directory 테 넌 트에 연결 합니다.
* 가상 네트워크 둘 다 hello 리소스 관리자 배포 모델을 통해 생성 되는 경우 또는 hello 리소스 관리자 배포 모델을 통해 하나의 가상 네트워크를 만든 하 고 다른 hello hello 클래식 배포 모델을 통해 만들어지는 경우 겹치기 될 수 있습니다. 그러나 Hello 클래식 배포 모델을 통해 생성 된 두 개의 가상 네트워크는 겹치기 tooeach 기타, 수 없습니다. 사용할 수는 [VPN 게이트웨이](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) hello 클래식 배포 모델을 통해 만든 tooconnect 두 가상 네트워크입니다.
* Hello 통신 겹치기 가상 네트워크의 가상 컴퓨터 간에 대역폭도 추가로 제한이 있지만 여전히 적용 되지만 hello 가상 컴퓨터 크기에 따라 최대 네트워크 대역폭이 있습니다. hello를 읽고, 다른 가상 컴퓨터 크기에 대 한 최대 네트워크 대역폭에 대 한 자세한 toolearn [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 또는 [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) 가상 컴퓨터의 문서 크기를 조정 합니다.
* Azure에서 제공한 가상 컴퓨터에 대한 내부 DNS 이름 확인은 피어링된 가상 네트워크에 작동하지 않습니다. 가상 컴퓨터에는 hello 로컬 가상 네트워크 내 에서만 확인할 수 있으면 내부 DNS 이름을 갖습니다. 그러나 수 가상 네트워크에 대 한 DNS 서버와 연결 된 가상 컴퓨터 toopeered 가상 네트워크를 구성 합니다. 자세한 내용은 hello 읽을 [자체 DNS 서버를 사용 하 여 이름 확인](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) 문서.

![기본 가상 네트워크 피어링](./media/virtual-networks-peering-overview/figure01.png)

## <a name="connectivity"></a>연결
두 가상 네트워크 피어로 설정 되어, 후 hello 겹치기 가상 네트워크에 있는 리소스와 각 가상 네트워크의 리소스 직접 연결할 수 있습니다. hello 두 가상 네트워크에는 전체 IP 수준 연결 합니다.

hello 네트워크 대기 시간 겹치기 가상 네트워크에 두 개의 가상 컴퓨터 간 왕복에 대 한 hello 동일와 단일 가상 네트워크 내에서 라운드트립 합니다. hello 네트워크 처리량은 비례 tooits 크기 hello 가상 컴퓨터에 대해 허용 되는 대역폭을 hello 기반으로 합니다. 대역폭 hello 피어 링 내에 추가 제한 하지 않습니다.

가상 네트워크 겹치기의 가상 컴퓨터 간에 트래픽 hello hello 하지 게이트웨이 통해 Azure의 백 엔드 인프라를 통해 직접 라우팅됩니다.

가상 컴퓨터 연결 된 tooa 가상 네트워크는 hello 겹치기 가상 네트워크의 내부 부하 분산 된 끝점 hello 액세스할 수 있습니다. 원하는 경우 가상 네트워크 tooblock 액세스 tooother 가상 네트워크 또는 서브넷에서 네트워크 보안 그룹을 적용할 수 있습니다.

가상 네트워크 피어 링을 구성할 때 열 하거나 hello hello 가상 네트워크 간의 네트워크 보안 그룹 규칙을 닫습니다. (즉, hello 기본 옵션) 겹치기 가상 네트워크 간의 전체 연결을 열면 네트워크는 보안 그룹 toospecific 서브넷 또는 가상 컴퓨터 tooblock 적용 하거나 특정 액세스를 거부할 수 있습니다. hello 읽기에 대해 더 알아봅니다 toolearn 네트워크 보안 그룹 [네트워크 보안 그룹을 개요](virtual-networks-nsg.md) 문서.

## <a name="service-chaining"></a>서비스 체이닝
대로 구성할 수 있습니다 사용자 정의 경로 지점 toovirtual 컴퓨터를 사용 하는 가상 네트워크 겹치기에 "다음 홉" IP 주소 tooenable 서비스 체인 hello 합니다. 서비스 연결을 설정을 통해 사용자 정의 경로 통해 peered 가상 네트워크에 하나의 가상 네트워크 tooa 가상 기기에서 있습니다 toodirect 트래픽을.

Hello 허브 네트워크 가상 어플라이언스와 같은 인프라 구성 요소를 호스트할 수 있는, 허브 및 스포크 유형의 환경을 효과적으로 작성할 수 있습니다. Hello 허브 가상 네트워크와 모든 hello 스포크 가상 네트워크 피어 링 다음 할 수 있습니다. 트래픽은 hello 허브 가상 네트워크에서 실행 되는 네트워크 가상 어플라이언스를 통해 전달 될 수 있습니다. 즉, 가상 네트워크 피어 링 hello 겹치기 가상 네트워크에 가상 컴퓨터의 사용자 정의 hello 경로 toobe hello IP 주소에 hello 다음 홉 IP 주소를 수 있습니다. hello 읽기 사용자 정의 경로 대 한 자세한 toolearn [사용자 정의 경로 개요](virtual-networks-udr-overview.md) 문서.

## <a name="gateways-and-on-premises-connectivity"></a>게이트웨이 및 온-프레미스 연결
다른 가상 네트워크와 겹치기는 여부에 관계 없이 각 가상 네트워크 게이트웨이 자체는 여전히 수 tooconnect tooan 온-프레미스 네트워크를 사용 합니다. 구성할 수 있습니다 [가상 네트워크를 가상 네트워크 연결](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello 가상 네트워크 피어로 설정 되어 있어도 게이트웨이 사용 하 여 합니다.

Hello 가상 네트워크 간의 트래픽 hello hello 피어 링 구성을 통해 흐름을 상호 연결 가상 네트워크에 대 한 옵션을 모두 구성 된 경우 (즉,: 통해 hello Azure backbone).

가상 네트워크 피어로 설정 되어 때 전송 지점 tooan 온-프레미스 네트워크로 hello 겹치기 가상 네트워크의 hello 게이트웨이 구성할 수도 있습니다. 이 경우 원격 게이트웨이 사용 하는 hello 가상 네트워크는 자체 게이트웨이 사용할 수 없습니다. 가상 네트워크는 하나의 게이트웨이만을 가질 수 있습니다. hello 게이트웨이 hello 다음 그림에에서 표시 된 대로 로컬 또는 원격 게이트웨이 (hello 겹치기 가상 네트워크에서) 될 수 있습니다.

![VNet 피어링 전송](./media/virtual-networks-peering-overview/figure02.png)

다양 한 배포 모델을 통해 만든 가상 네트워크 간의 hello 피어 링 관계에서 게이트웨이 전송 중 지원 되지 않습니다. Hello 피어 링 관계에서 두 가상 네트워크가 만들어야 리소스 관리자를 통해 게이트웨이 전송 toowork에 대 한 합니다.

가상 네트워크는 단일 Azure express 경로 연결을 공유 하는 hello 피어로 설정 되어, 둘 사이의 hello 트래픽 hello 피어 링 관계를 통해 이동 (즉,: 통해 hello Azure 백본 네트워크). 각 가상 네트워크 tooconnect toohello 온-프레미스 회로에 로컬 게이트웨이 계속 사용할 수 있습니다. 또는 공유 게이트웨이를 사용하고 온-프레미스 연결에 대한 전송을 구성할 수 있습니다.

## <a name="provisioning"></a>프로비전
가상 네트워크 피어링은 권한 있는 작업입니다. 그는 hello VirtualNetworks 네임 스페이스에서 별도 함수입니다. 사용자는 특정 권한이 tooauthorize 피어 링 부여할 수 있습니다. 읽기 / 쓰기 액세스 toohello 가상 네트워크를 가진 사용자는 이러한 권한을 자동으로 상속 합니다.

Hello 피어 링 기능 권한이 있는 사용자 또는 사용자가 관리자 중 하나는 다른 가상 네트워크에 피어 링 작업을 시작할 수 있습니다. 에 피어 링에 대 한 일치 하는 요청 하는 경우 다른 쪽 hello 고 hello 피어 링 설정 하 고 다른 요구 사항이 충족 됩니다.

## <a name="limits"></a>제한
단일 가상 네트워크에 허용 되는 피어 링 hello 수에 제한이 있습니다. 자세한 내용을 보려면 검토 hello [Azure 네트워킹 제한을](../azure-subscription-service-limits.md#networking-limits)합니다.

## <a name="pricing"></a>가격
가상 네트워크 피어링을 활용하는 수신 및 송신 트래픽에 대한 명목 요금이 부과됩니다. 자세한 내용은 참조 hello [가격 책정 페이지](https://azure.microsoft.com/pricing/details/virtual-network)합니다.

## <a name="next-steps"></a>다음 단계

* 가상 네트워크 피어링 자습서를 완료합니다. 동일 hello를 통해 만든 가상 네트워크 간에 만들어진 가상 네트워크 피어 링 하거나 다양 한 배포 모델에 존재 하는 hello 같거나 다른 데이터 집합 구독 합니다. Hello 다음 시나리오 중 하나에 대 한 자습서를 완료 합니다.
 
    |Azure 배포 모델  | 구독  |
    |---------|---------|
    |둘 다 Resource Manager |[동일](virtual-network-create-peering.md)|
    | |[다름](create-peering-different-subscriptions.md)|
    |하나는 Resource Manager, 다른 하나는 클래식     |[동일](create-peering-different-deployment-models.md)|
    | |[다름](create-peering-different-deployment-models-subscriptions.md)|

* 자세한 내용은 방법 toocreate는 [허브 및 스포크 네트워크 토폴로지](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
* 모든에 대 한 자세한 내용은 [가상 네트워크 피어 링 설정 방법과 toochange에](virtual-network-manage-peering.md)
