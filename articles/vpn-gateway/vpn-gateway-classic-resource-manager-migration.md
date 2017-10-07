---
title: "aaaVPN 게이트웨이 클래식 tooResource Manager 마이그레이션 | Microsoft Docs"
description: "이 페이지는 hello VPN 게이트웨이 클래식 tooResource Manager 마이그레이션에 대 한 개요를 제공합니다."
documentationcenter: na
services: vpn-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: caa8eb19-825a-4031-8b49-18fbf3ebc04e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: amsriva
ms.openlocfilehash: c1d84bf5315224c5c8faac53d7957b496ed205ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="vpn-gateway-classic-tooresource-manager-migration"></a>VPN 게이트웨이 클래식 tooResource Manager 마이그레이션
VPN 게이트웨이 클래식 tooResource 관리자 배포 모델에서 이제 마이그레이션할 수 있습니다. [Azure Resource Manager 기능 및 이점](../azure-resource-manager/resource-group-overview.md)에 대해 자세히 알아볼 수 있습니다. 이 문서에서는 toomigrate 클래식 배포 toonewer 리소스 관리자에서에서 모델을 기반 하는 방법을 설명 합니다. 

VPN 게이트웨이 클래식 tooResource 관리자에서에서 VNet 마이그레이션의 일부로 마이그레이션됩니다. 이 마이그레이션은 한 번에 하나의 VNet 꼴로 이뤄집니다. 필수 구성 요소 또는 도구 toomigration 측면에서 추가 사항은 없습니다. 마이그레이션 단계는 동일 tooexisting VNet 마이그레이션 및에 정리 되어 [IaaS 리소스 마이그레이션 페이지](../virtual-machines/windows/migration-classic-resource-manager-ps.md)합니다. 마이그레이션 중 데이터 경로 가동 중지 시간 없이 하며 따라서 기존 작업을 계속할 온-프레미스 연결의 손실 없이 toofunction 마이그레이션 중입니다. hello 마이그레이션 프로세스 중 hello VPN 게이트웨이에 연결 된 hello 공용 IP 주소를 변경 하지 않습니다. 이 필요는 없지만 tooreconfigure 온-프레미스 라우터 hello 마이그레이션이 완료 된 후 것을 의미 합니다.  

hello 모델 리소스 관리자의 일반 모델 간에 차이가 있는 되며 가상 네트워크 게이트웨이와 로컬 네트워크 게이트웨이 연결 리소스 구성 됩니다. Hello VPN 게이트웨이 자체를 나타내는, 로컬 사이트 간 프레미스 주소 공간 및 두 개의 hello 간의 연결에 각각 hello이 됩니다. 마이그레이션이 완료되면 게이트웨이는 클래식 모델에서 사용할 수 없게 될 것이며 가상 네트워크 게이트웨이, 로컬 네트워크 게이트웨이 및 연결 개체에서의 모든 관리 작업은 Resource Manager 모델을 사용하여 수행되어야 합니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
가장 일반적인 VPN 연결 시나리오 클래식 tooResource Manager 마이그레이션 지원을 받습니다. hello 지원 시나리오에는 포함-

* 지점 toosite 연결
* VPN 게이트웨이와 함께 사이트 toosite 연결 연결 tooon 프레미스 위치
* VPN 게이트웨이 사용 하 여 두 개의 Vnet 간의 VNet tooVNet 연결
* 여러 Vnet toosame 프레미스 위치에 연결
* 다중 사이트 연결
* 강제 터널링 사용 설정된 VNet

지원되지 않는 시나리오 -  

* ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 VNet은 현재 지원되지 않습니다.
* VM 확장은 연결 된 tooon 온-프레미스 서버 시나리오를 전송 합니다. 전송 시 VPN 연결 제한은 아래에 자세히 설명됩니다.

> [!NOTE]
> 리소스 관리자 모델에서 CIDR 유효성 검사는 기존 모델에 hello 하나 보다 엄격 합니다. 마이그레이션하기 전에 제공 된 기본 주소 범위 hello 마이그레이션을 시작 하기 전에 toovalid CIDR 형식을 준수를 확인 합니다. CIDR는 일반적인 CIDR 유효성 검사기를 사용하여 유효성을 검사할 수 있습니다. 마이그레이션할 때 유효하지 않은 CIDR 범위를 사용한 VNet 또는 로컬 사이트는 실패 상태가 됩니다.
> 
> 

## <a name="vnet-toovnet-connectivity-migration"></a>VNet tooVNet 연결 마이그레이션
클래식에서 VNet tooVNet 연결 이루어졌습니다 hello의 표현을 로컬 사이트를 만들어 VNet을 연결 합니다. 고객은 필요한 toocreate 두 개의 로컬 사이트가 hello toobe 필요한 두 개의 Vnet 연결을 표시 합니다. 이들 다음 두 개의 Vnet hello 연결 된 toohello 간의 IPsec 터널 tooestablish 연결을 사용 하 여 Vnet에 해당 합니다. 이 모델에는 하나의 VNet의 주소 범위 변경 내용을 hello 해당 로컬 사이트 표현에도 유지 해야 하므로 관리 효율성 과제입니다. Resource Manager 모델에서 이 해결 방법은 더 이상 필요하지 않습니다. 두 개의 Vnet 직접 액세스가 가능 연결 리소스에서 'Vnet2Vnet' 연결 유형을 사용 하 여 hello 간의 hello 연결입니다. 

![VNet 스크린샷 tooVNet 마이그레이션입니다.](./media/vpn-gateway-migration/migration1.png)

연결 된 엔터티 hello 검색 VNet 마이그레이션하는 동안 toocurrent VNet VPN 게이트웨이 다른 VNet이 하 두 Vnet의 마이그레이션이 완료 되 면 더 이상 표시 hello를 나타내는 두 개의 로컬 사이트가 다른 VNet 확인 하십시오. VPN 게이트웨이 2 개, 두 개의 로컬 사이트가 및 두 개의 연결이 서로 hello 클래식 모델은 변형 된 tooResource 두 VPN 게이트웨이 및 Vnet2Vnet 형식의 두 개의 연결 관리자 모델입니다.

## <a name="transit-vpn-connectivity"></a>전송 시 VPN 연결
VNet에 대 한 온-프레미스 연결 tooanother는 직접 연결 된 tooon 온-프레미스 VNet를 연결 하 여 수행 됩니다 되도록 토폴로지에서 VPN 게이트웨이 구성할 수 있습니다. 첫 번째 VNet의 인스턴스는 직접 연결 된 tooon 온-프레미스 연결 된 VNet에서 전송 toohello VPN 게이트웨이 통해 연결 된 tooon 온-프레미스 리소스에 있는 VPN 연결 전송 중입니다. tooachieve 클래식 배포 모델에서이 구성에서는 toocreate 접두사 hello 연결 된 VNet 및 온-프레미스 주소 공간을 나타내는 집계에 로컬 사이트 할 수 있습니다. 이 representational 로컬 사이트에 있으면 연결 된 VNet tooachieve toohello 전송 연결. 이 클래식 모델 온-프레미스 주소 범위에 변경 내용을 나타내는 VNet 및 온-프레미스의 hello 집계 hello 로컬 사이트에도 유지 해야 하므로 관리 효율성 해당 하는 문제를 있습니다. 지원 되는 리소스 관리자 게이트웨이 BGP 지원 서비스가 도입 hello 연결 된 게이트웨이 수 경로 알아냅니다에서 수동으로 수정 tooprefixes 없이 온-프레미스에 있으므로 관리 효율성을 간소화 합니다.

![전송 라우팅 시나리오의 스크린샷.](./media/vpn-gateway-migration/migration2.png)

로컬 사이트를 요구 하지 않고 VNet tooVNet 연결, 변환 이후 hello 통과 시나리오는 간접적으로 연결 된 tooon 온-프레미스 VNet에 대 한 온-프레미스 연결을 잃습니다. hello 연결이 손실 완화 될 수 hello 다음 두 가지 방법에서에서 마이그레이션-완료 

* 함께 연결 되어 있는 VPN 게이트웨이 및 tooon 온-프레미스에서 BGP를 사용 하도록 설정 합니다. BGP를 사용하도록 설정하면 경로가 VNet 게이트웨이 간에 학습되고 광고되기 때문에 다른 구성 변경 없이 연결을 복원합니다. BGP 옵션은 표준 및 상위 SKU에서만 사용할 수 있습니다.
* 온-프레미스 위치를 나타내는 영향을 받는 VNet toohello 로컬 네트워크 게이트웨이에서 명시적 연결을 설정 합니다. 이 방법은 hello 온-프레미스 라우터 toocreate에서 구성을 변경 해야 하며 hello IPsec 터널을 구성할 수도 있습니다.

## <a name="next-steps"></a>다음 단계
VPN 게이트웨이 마이그레이션 지원에 대 한 학습 한 후 전환 너무[클래식 tooResource 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션](../virtual-machines/windows/migration-classic-resource-manager-ps.md) tooget 시작 합니다.

