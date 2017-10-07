---
title: "AWS 및 다른 플랫폼 tooManaged aaaMigrate Azure에서 디스크 | Microsoft Docs"
description: "AWS 또는 기타 가상화 플랫폼과 같은 다른 클라우드에서 업로드한 VHD를 사용하여 Azure에서 VM을 만들고 Azure Managed Disks를 활용합니다."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Azure의 디스크 tooManaged 서비스 AWS (Amazon Web) 및 기타 플랫폼에서 마이그레이션

AWS 또는 온-프레미스 가상화 솔루션 tooAzure toocreate 관리 하는 디스크를 활용 하는 Vm에서에서 VHD 파일을 업로드할 수 있습니다. Azure 관리 되는 디스크 toomanaging 저장소 계정의 Azure IaaS Vm에 대 한 hello 필요성을 제거합니다. 있습니다 (프리미엄 또는 표준) hello 유형 및 필요한 디스크의 크기를 지정 하는 tooonly 있고 Azure 만들어져 hello 디스크를 관리 합니다. 

일반화된 VHD 및 특수한 VHD를 모두 업로드할 수 있습니다. 
- **일반화된 VHD** - Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다. 
- **VHD를 특수화할** -hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 관리 합니다. 

> [!IMPORTANT]
> 모든 VHD tooAzure를 업로드 하기 전에 따라야 [Windows VHD 또는 VHDX tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| 시나리오                                                                                                                         | 설명서                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| 관리 되는 디스크 toomigrate tooAzure 처럼 수 하는 기존 AWS EC2 인스턴스가 있는                                     | [웹 서비스 AWS (Amazon) tooAzure에서 VM 이동](aws-to-azure.md)                           |
| VM 및 싶다는 의사를 이미지 toocreate로 toouse toouse 다른 가상화 플랫폼에서는 여러 Azure Vm입니다. | [일반화 된 VHD를 업로드 하 고 Azure에서 새 Vm toocreate 사용](upload-generalized-managed.md) |
| Azure에서 toorecreate 싶은 고유 하 게 사용자 지정 된 VM이 있는 합니다.                                                      | [특수 한 VHD tooAzure 업로드 하 고 새 VM 만들기](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Managed Disks 개요

Azure 관리 되는 디스크 hello 필요 toomanage 저장소 계정을 제거 하 여 VM 관리를 간소화 합니다. Managed Disks는 가용성 집합에서 VM의 안정성을 향상시킨다는 장점도 있습니다. 가용성 집합에 있는 다른 Vm의 hello 디스크 충분히 각 다른 tooavoid 단일 오류 지점을 으로부터 격리 됩니다 되도록 조정 합니다. 가용성 집합에 다른 저장소 배율 단위 (스탬프) toohardware 및 소프트웨어 오류 때문에 발생 한 단일 저장소 배율 단위 오류의 hello 영향을 제한 하는 자동으로 다른 Vm의 디스크를 배치 합니다. 필요에 따라 두 가지 유형의 저장소 옵션 중에 하나를 선택할 수 있습니다. 
 
- [프리미엄 Managed Disks](../../storage/common/storage-premium-storage.md)는 I/O 집약적인 워크로드를 실행하는 가상 컴퓨터에 대한 고성능의 짧은 대기 시간 디스크 지원을 제공하는 반도체 드라이브(SSD) 기반 저장소 미디어입니다. 마이그레이션 tooPremium 관리 하는 디스크에서 해당이 디스크의 성능 및 hello 속도 활용할 취할 수 있습니다.  

- [표준 관리 디스크](../../storage/common/storage-standard-storage.md) 하드 디스크 드라이브 (HDD) 기반 저장소 미디어를 사용 하며 개발/테스트 및 다른 자주 액세스 작업 비교적 중요 하지 않은 tooperformance 가변성에 가장 적합 합니다.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Hello 마이그레이션 계획 tooManaged 디스크

이 섹션 toomake hello 최선의 결정을 VM 및 디스크 유형에 대 수 있도록 도와줍니다.


### <a name="location"></a>위치

Azure Managed Disks를 사용할 수 있는 위치를 선택합니다. TooPremium 관리 하는 디스크를 마이그레이션하는 경우 또한 toomigrate를 계획 하는 hello 지역에서 프리미엄 저장소를 사용할 수 있는지 확인 합니다. 사용 가능한 위치에 대한 최신 정보는 [지역별 Azure 서비스](https://azure.microsoft.com/regions/#services)를 참조하세요.

### <a name="vm-sizes"></a>VM 크기

TooPremium 관리 하는 디스크를 마이그레이션하는 경우 VM이 있는 hello 영역의 tooupdate hello 크기인 hello VM tooPremium 사용 가능한 저장소 가능 크기를 수 있습니다. 프리미엄 저장소 수 있는 hello VM 크기를 검토 합니다. hello Azure VM 크기 사양에 나열 된 [가상 컴퓨터의 크기](sizes.md)합니다.
프리미엄 저장소를 사용 하 고 작업에 가장 적합 한 hello 가장 적절 한 VM 크기를 선택 하는 가상 컴퓨터의 hello 성능 특성을 검토 합니다. VM toodrive hello 디스크 트래픽에 사용할 수 있는 충분 한 대역폭이 있는지 확인 합니다.

### <a name="disk-sizes"></a>디스크 크기

**프리미엄 Managed Disks**

VM에서 사용할 수 있는 프리미엄 Managed Disks에는 세 종류가 있으며 각 종류에는 특정 IOP 및 처리량 제한이 있습니다. Hello 프리미엄 디스크 유형 VM에 대 한 용량, 성능, 확장성, 관점에서 응용 프로그램의 hello 요구 사항에 따라 적중 영향과 최고 선택할 때 이러한 제한을 고려 합니다.

| 프리미엄 디스크 유형  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| 디스크 크기           | 128GB            | 512GB            | 1024GB(1TB)    |
| 디스크당 IOPS       | 500               | 2,300              | 5000              |
| 디스크당 처리량 | 초당 100MB | 초당 150MB | 초당 200MB |

**표준 Managed Disks**

VM에서 사용할 수 있는 표준 Managed Disks에는 다섯 가지 종류가 있습니다. 각각은 용량이 다르지만 동일한 IOPS 및 처리량이 제한됩니다. Hello 유형의 응용 프로그램의 hello 용량 요구 사항에 따라 관리 되는 표준 디스크를 선택 합니다.

| 표준 디스크 유형  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| 디스크 크기           | 30GB            | 64GB            | 128GB           | 512GB           | 1024GB(1TB)   |
| 디스크당 IOPS       | 500              | 500              | 500              | 500              | 500              |
| 디스크당 처리량 | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second | 60 MB per second |

### <a name="disk-caching-policy"></a>디스크 캐싱 정책 

**프리미엄 Managed Disks**

디스크 캐싱 정책은 기본적으로 *읽기 전용* 모든 hello 프리미엄 데이터 디스크에 대 한 및 *읽기 / 쓰기* hello 프리미엄 운영 체제 디스크에 대 한 toohello VM을 연결 합니다. 이 구성 설정은 응용 프로그램의 IOs 용 tooachieve hello 최적의 성능은 것이 좋습니다. 쓰기가 많거나 쓰기 전용인 디스크의 경우(예: SQL Server 로그 파일) 더 나은 응용 프로그램 성능을 얻기 위해 디스크 캐싱을 사용하지 않도록 설정합니다.

### <a name="pricing"></a>가격

검토 hello [관리 하는 디스크에 대 한 가격 책정](https://azure.microsoft.com/en-us/pricing/details/managed-disks/)합니다. 프리미엄 관리 되는 디스크의 가격 책정은 hello 프리미엄 관리 되지 않는 디스크와 동일 합니다. 하지만 표준 Managed Disks의 가격 책정은 관리되지 않는 표준 디스크와 다릅니다.


## <a name="next-steps"></a>다음 단계

- 모든 VHD tooAzure를 업로드 하기 전에 따라야 [Windows VHD 또는 VHDX tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
