---
title: "Azure Vm tooManaged 디스크 aaaMigrate | Microsoft Docs"
description: "저장소 계정 toouse 관리 되는 디스크에에서 관리 되지 않는 디스크를 사용 하 여 만든 Azure 가상 컴퓨터를 마이그레이션하십시오."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Azure에서 Azure Vm tooManaged 디스크 마이그레이션

Azure 관리 되는 디스크 hello 필요성을 제거 하 여 저장소 관리를 간소화 tooseparately 저장소 계정을 관리 합니다.  가용성 집합에 있는 Vm의 안정성을 향상에서 프로그램 기존 Azure Vm tooManaged 디스크 toobenefit를 마이그레이션할 수도 있습니다. 가용성 집합에 있는 다른 Vm의 hello 디스크 충분히 각 다른 tooavoid 단일 오류 지점을 으로부터 격리 됩니다 되도록 조정 합니다. 가용성 집합에 다른 저장소 배율 단위 (스탬프) toohardware 및 소프트웨어 오류 때문에 발생 한 단일 저장소 배율 단위 오류의 hello 영향을 제한 하는 자동으로 다른 Vm의 디스크를 배치 합니다.
필요에 따라 두 가지 유형의 저장소 옵션 중에 하나를 선택할 수 있습니다.

- [프리미엄 Managed Disks](../../storage/common/storage-premium-storage.md)는 I/O 집약적인 워크로드를 실행하는 가상 컴퓨터에 대한 고성능의 짧은 대기 시간 디스크 지원을 제공하는 반도체 드라이브(SSD) 기반 저장소 미디어입니다. 마이그레이션 tooPremium 관리 하는 디스크에서 해당이 디스크의 성능 및 hello 속도 활용할 취할 수 있습니다.

- [표준 관리 디스크](../../storage/common/storage-standard-storage.md) 하드 디스크 드라이브 (HDD) 기반 저장소 미디어를 사용 하며 개발/테스트 및 다른 자주 액세스 작업 비교적 중요 하지 않은 tooperformance 가변성에 가장 적합 합니다.

다음과 같은 시나리오에서 tooManaged 디스크를 마이그레이션할 수 있습니다.

| 마이그레이션...                                            | 문서 링크                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 독립 실행형 Vm 및 Vm을 가용성 집합 toomanaged 디스크의 변환   | [Toouse 관리 디스크 Vm으로 변환](convert-unmanaged-to-managed-disks.md) |
| 관리 되는 디스크에 클래식 tooResource 관리자에서에서 단일 VM     | [단일 VM 마이그레이션](migrate-single-classic-to-resource-manager.md)  | 
| 관리 되는 디스크에 클래식 tooResource 관리자에서에서 vNet에 있는 모든 hello Vm     | [IaaS 리소스 클래식 tooResource 관리자에서에서 마이그레이션](migration-classic-resource-manager-ps.md) 차례로 [관리 되지 않는 디스크 toomanaged 디스크에서 VM으로 변환](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Hello 변환에 대 한 계획 tooManaged 디스크

이 섹션 toomake hello 최선의 결정을 VM 및 디스크 유형에 대 수 있도록 도와줍니다.


## <a name="location"></a>위치

Azure Managed Disks를 사용할 수 있는 위치를 선택합니다. TooPremium 관리 하는 디스크를 이동 하는 경우 또한 toomove를 계획 하는 hello 지역에서 프리미엄 저장소를 사용할 수 있는지 확인 합니다. 사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.

## <a name="vm-sizes"></a>VM 크기

TooPremium 관리 하는 디스크를 마이그레이션하는 경우 VM이 있는 hello 영역의 tooupdate hello 크기인 hello VM tooPremium 사용 가능한 저장소 가능 크기를 수 있습니다. 프리미엄 저장소 수 있는 hello VM 크기를 검토 합니다. hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](sizes.md)합니다.
프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다. VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.

## <a name="disk-sizes"></a>디스크 크기

**프리미엄 Managed Disks**

VM에서 사용할 수 있는 프리미엄 관리 디스크에는 7가지 형식이 있으며 각 형식에는 특정 IOP 및 처리량 한도가 있습니다. 이러한 제한은 때 고려해 hello 프리미엄 디스크 유형 VM에 대 한 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 적중 영향과 최고를 선택 합니다.

| 프리미엄 디스크 유형  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 디스크 크기           | 128GB| 512GB| 128GB| 512GB            | 1,024GB(1TB)    | 2,048GB(2TB)    | 4,095GB(4TB)    | 
| 디스크당 IOPS       | 120   | 240   | 500   | 2,300              | 5,000              | 7,500              | 7,500              | 
| 디스크당 처리량 | 초당 25MB  | 초당 50MB  | 초당 100MB | 초당 150MB | 초당 200MB | 초당 250MB | 초당 250MB |

**표준 Managed Disks**

VM에서 사용할 수 있는 표준 관리 디스크에는 7가지 형식이 있습니다. 각각은 용량이 다르지만 동일한 IOPS 및 처리량이 제한됩니다. Hello 유형의 응용 프로그램의 hello 용량 요구 사항에 따라 관리 되는 표준 디스크를 선택 합니다.

| 표준 디스크 유형  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| 디스크 크기           | 30GB            | 64GB            | 128GB           | 512GB           | 1,024GB(1TB)   | 2,048GB(2TB)    | 4,095GB(4TB)   | 
| 디스크당 IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| 디스크당 처리량 | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 

## <a name="disk-caching-policy"></a>디스크 캐싱 정책

**프리미엄 Managed Disks**

디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다. 이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다. 쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.

## <a name="pricing"></a>가격

검토 hello [관리 하는 디스크에 대 한 가격 책정](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)합니다. 프리미엄 관리 되는 디스크의 가격 책정은 hello 프리미엄 관리 되지 않는 디스크와 동일 합니다. 하지만 표준 Managed Disks의 가격 책정은 관리되지 않는 표준 디스크와 다릅니다.



## <a name="next-steps"></a>다음 단계

- [Managed Disks](managed-disks-overview.md)에 대한 자세한 정보
