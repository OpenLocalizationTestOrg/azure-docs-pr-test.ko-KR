---
title: "클래식 tooResource 관리자에서에서 express 경로 연결 된 가상 네트워크 마이그레이션: Azure: PowerShell | Microsoft Docs"
description: "이 페이지에서는 toomigrate 회로 이동한 후 가상 네트워크 tooResource 관리자에 연결 하는 방법을 설명 합니다."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>클래식 tooResource 관리자에서에서 express 경로 연결 된 가상 네트워크 마이그레이션

이 문서에서는 toomigrate Azure ExpressRoute ExpressRoute 회로 이동한 후 hello 클래식 배포 모델 toohello Azure 리소스 관리자 배포 모델에서 가상 네트워크에 연결 하는 방식에 대해 설명 합니다. 


## <a name="before-you-begin"></a>시작하기 전에
* Hello Azure PowerShell 모듈의 최신 버전 hello 있는지 확인 합니다. 자세한 내용은 참조 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.
* Hello 검토 했는지 확인 [필수 구성 요소](expressroute-prerequisites.md), [라우팅 요구 사항](expressroute-routing.md), 및 [워크플로](expressroute-workflows.md) 구성을 시작 하기 전에.
* 제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다. 완전히 이해 하는 hello 제한 및 제한 사항이 있는지 확인 합니다.
* Hello 회로 hello 클래식 배포 모델에서 완전 하 게 작동 하는지 확인 합니다.
* Hello 리소스 관리자 배포 모델에서 만든 리소스 그룹 가졌는지 확인 합니다.
* Hello 리소스 마이그레이션 설명서를 검토 합니다.

    * [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 플랫폼 지원](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션 Faq:](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [가장 일반적인 마이그레이션 오류 및 완화 방법 검토](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>지원되는 및 지원되지 않는 시나리오

* ExpressRoute 회로 중단 시간 없이 hello 클래식 toohello 리소스 관리자 환경에서 이동할 수 있습니다. Hello 클래식 toohello 중단 시간 없이 리소스 관리자 환경에서에서 모든 ExpressRoute 회로 이동할 수 있습니다. Hello 지침에 따라 [PowerShell을 사용 하 여 hello 클래식 toohello 리소스 관리자 배포 모델에서 ExpressRoute 회로 이동](expressroute-howto-move-arm.md)합니다. 이 필수 구성 요소 toomove 리소스 toohello 연결 된 가상 네트워크입니다.
* 가상 네트워크, 게이트웨이 및 연결 된 배포 hello 가상 네트워크 내에서 연결 된 tooan hello 동일한 구독 수의 ExpressRoute 회로 중단 시간 없이 toohello 리소스 관리자 환경이 마이그레이션됩니다. Hello 단계 설명된 이후 toomigrate 주고받는 가상 네트워크, 게이트웨이 및 hello 가상 네트워크 내에서 배포 된 가상 컴퓨터를 따를 수 있습니다. 마이그레이션된 전에 hello 가상 네트워크가 올바르게 구성 되어 있는지 확인 해야 합니다. 
* 가상 네트워크, 게이트웨이 및 hello에 없는 가상 네트워크 내에서 관련된 배포가 hello hello ExpressRoute 회로는 일부 가동 중지 시간 toocomplete hello 마이그레이션 필요에 따라 동일한 구독 합니다. hello 문서의 마지막 섹션 hello hello 단계 뒤에 toobe toomigrate 리소스에 설명 합니다.
* ExpressRoute 게이트웨이와 VPN Gateway가 모두 있는 가상 네트워크는 마이그레이션할 수 없습니다.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동 합니다.
Hello 클래식 toohello toomigrate 리소스를 시도 하기 전에 리소스 관리자 환경에서에서 ExpressRoute 회로 연결 toohello ExpressRoute 회로 이동 해야 합니다. tooaccomplish 작업이 hello 다음 문서를 참조 하세요.

* 제공 하는 hello 정보를 검토 [클래식 tooResource 관리자에서에서 ExpressRoute 회로 이동](expressroute-move.md)합니다.
* [클래식 tooResource Azure PowerShell을 사용 하 여 관리자에서에서 회로 이동](expressroute-howto-move-arm.md)합니다.
* Hello Azure 서비스 관리 포털을 사용 합니다. 너무 hello 워크플로 따를 수[새 ExpressRoute 회로 만들기](expressroute-howto-circuit-portal-resource-manager.md) hello 가져오기 옵션을 선택 합니다. 

이 작업에는 가동 중지 시간이 없습니다. Hello 마이그레이션이 진행 중인 동안 프레미스와 Microsoft 간에 tootransfer 데이터를 계속할 수 있습니다.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>가상 네트워크, 게이트웨이 및 연결된 배포 마이그레이션

hello toomigrate 수행 단계에 종속 hello에 리소스가 있는 여부 동일한 구독, 서로 다른 구독 또는 둘 다 합니다.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>대로 hello ExpressRoute 회로에 연결 된 배포 hello 동일한 구독 및 가상 네트워크 게이트웨이 마이그레이션
이 섹션에서는 hello 단계 뒤에 toobe toomigrate 설명 가상 네트워크, 게이트웨이 및 연결 된 배포에 동일한 구독으로 ExpressRoute 회로 hello hello 합니다. 이 마이그레이션은 가동 중지 시간이 없습니다. Toouse hello 마이그레이션 프로세스를 통해 모든 리소스를 계속할 수 있습니다. hello 관리 평면 hello 마이그레이션이 진행 중인 동안 잠겨 있습니다. 

1. Hello ExpressRoute 회로 hello 클래식 toohello 리소스 관리자 환경에서 옮겨 졌음을 있는지 확인 합니다.
2. Hello 마이그레이션에 대 한 hello 가상 네트워크 적절 하 게 준비 된 것을 확인 합니다.
3. 리소스 마이그레이션을 위해 구독을 등록합니다. tooregister 리소스 마이그레이션-다음 PowerShell 코드 조각을 사용 하 여 hello에 대 한 구독:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. 유효성을 검사하고 준비한 후, 마이그레이션합니다. toomove hello 가상 네트워크, 다음 PowerShell 코드 조각을 사용 하 여 hello:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  또한 hello 다음 PowerShell cmdlet을 실행 하 여 마이그레이션을 중단할 수 있습니다.

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>다음 단계
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 마이그레이션 플랫폼 지원](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [클래식 tooAzure 리소스 관리자에서에서 마이그레이션 플랫폼 지원에 기술 심층 분석](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [클래식 tooAzure 리소스 관리자에서에서 IaaS 리소스의 플랫폼에서 지 원하는 마이그레이션 Faq:](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [가장 일반적인 마이그레이션 오류 및 완화 방법 검토](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
