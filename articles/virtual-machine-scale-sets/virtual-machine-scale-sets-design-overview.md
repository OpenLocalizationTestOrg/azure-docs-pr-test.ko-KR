---
title: "Azure 가상 컴퓨터 크기 집합에 대 한 고려 사항 aaaDesign | Microsoft Docs"
description: "Azure 가상 컴퓨터 확장 집합에 대한 디자인 고려 사항에 대해 알아보기"
keywords: "linux 가상 컴퓨터, 가상 컴퓨터 확장 집합"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>확장 집합 디자인 고려 사항
이 항목은 Virtual Machine 확장 집합을 설계할 때 고려할 사항에 대해 논의합니다. 가상 컴퓨터 크기 집합 이란 하는 방법에 대 한 정보에 대 한 참조 너무[가상 컴퓨터 크기 조정 설정 개요](virtual-machine-scale-sets-overview.md)합니다.

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>때 가상 컴퓨터 대신 toouse 배율 설정 합니다.
일반적으로 확장 집합은 유사한 구성을 가진 일련의 컴퓨터로 구성된 고가용성 인프라를 배포하는 데 유용합니다. 그러나 일부 기능은 확장 집합에서만 사용할 수 있고, 다른 일부 기능은 VM에서만 사용할 수 있습니다. 순서로 toomake 시기에 대 한 결정을 내릴된 toouse 각 기술 해야 먼저 살펴보면는 몇 가지 하지 Vm 크기 집합에 사용할 수 있는 일반적으로 사용 하는 hello 기능:

### <a name="scale-set-specific-features"></a>확장 집합 특정 기능

- Hello 크기 조정 설정 구성을 지정 하면 "용량" 속성 toodeploy hello를 동시에 더 많은 Vm 단순히 업데이트할 수 있습니다. 이 동시에 많은 개별 Vm을 배포 하는 스크립트 tooorchestrate 쓰는 것 보다 훨씬 더 간단 합니다.
- 있습니다 수 [사용 하 여 Azure 자동 크기 조정 tooautomatically 크기 집합의 크기를 조정](./virtual-machine-scale-sets-autoscale-overview.md) 하지만 개별이 아닌 Vm입니다.
- [확장 집합 VM을 이미지로 다시 설치](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm)할 수 있지만 [개별 VM의 경우는 불가능합니다](https://docs.microsoft.com/rest/api/compute/virtualmachines).
- 안정성 향상과 배포 시간 단축을 위해 확장 집합 VM을 [오버프로비전](./virtual-machine-scale-sets-design-overview.md)할 수 있습니다. 그럴 수 없으면 개별 vm이 사용자 지정 코드 toodo 작성 하지 않는 경우.
- 지정할 수는 [업그레이드 정책의](./virtual-machine-scale-sets-upgrade-scale-set.md) toomake 것 쉽게 tooroll 크기 집합의 Vm에서 업그레이드 합니다. 개별 VM의 경우 업데이트를 직접 오케스트레이션해야 합니다.

### <a name="vm-specific-features"></a>VM 특정 기능

Hello 반면에, 일부 기능은 Vm에서 사용할 수만 (적어도 hello 당분간에 대 한):

- 데이터 디스크 toospecific 첨부할 수 개별 Vm 되지만 연결 된 데이터 디스크 크기 집합의 모든 Vm에 대해 구성 됩니다.
- 비어 있지 않은 데이터 디스크 tooindividual Vm 하지만 하지 Vm 크기 집합에 연결할 수 있습니다.
- 개별 VM의 스냅숏을 만들 수 있지만 확장 집합의 VM의 스냅숏은 만들 수 없습니다.
- 개별 VM에서 이미지를 캡처할 수 있지만 확장 집합의 VM에서는 캡처할 수 없습니다.
- 기본 디스크 toomanaged 디스크에서 개별 VM을 마이그레이션할 수 있지만 크기 집합의 Vm에 대 한 이렇게 수 없습니다.
- 수행할 수 없습니다 vm 크기 집합의 하지만 tooindividual VM nic IPv6 공용 IP 주소를 할당할 수 있습니다. IPv6 공용 IP를 할당할 수 있는 주소 tooload 분산 개별 Vm 중 하나 앞에 크기 집합 Vm 또는 합니다.

## <a name="storage"></a>저장소

### <a name="scale-sets-with-azure-managed-disks"></a>Azure Managed Disks를 사용하는 확장 집합
확장 집합은 기존의 Azure Storage 계정 대신 [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md)를 사용하여 만들 수 있습니다. 관리 되는 디스크 hello 이점은 다음을 제공 합니다.
- Toopre 없는-hello 크기 집합 Vm에 대 한 Azure 저장소 계정 집합을 만듭니다.
- 정의한 [연결 된 데이터 디스크](virtual-machine-scale-sets-attached-disks.md) 눈금에 Vm hello에 대 한 설정입니다.
- 크기 집합을 너무 구성할 수 있습니다.[too1, 000 Vm 집합에 최대](virtual-machine-scale-sets-placement-groups.md)합니다. 

기존 템플릿을 설정한 경우 수도 있습니다 [hello 템플릿 toouse 관리 되는 디스크 업데이트](virtual-machine-scale-sets-convert-template-to-md.md)합니다.

### <a name="user-managed-storage"></a>사용자 관리 저장소
Azure 관리 되는 디스크와 정의 되지 않은 크기 집합 hello 집합에 있는 hello Vm의 사용자가 만든 저장소 계정 toostore hello OS 디스크에 의존 합니다. 저장소 계정당 이하의 20 대의 Vm의 비율 tooachieve 최대 IO 및 활용 좋습니다 _과도 프로 비전_ (아래 참조). 또한 hello 시작 자의 hello 저장소 계정 이름은 hello 알파벳에 분산 하는 것이 좋습니다. 그러면 여러 내부 시스템에서 부하를 분산할 수 있습니다. 


## <a name="overprovisioning"></a>오버프로비전
배율 현재 기본 설정 Vm 너무 "이라는"입니다. 켜져 과도 프로 비전와 hello 눈금 설정에 대 한 요청 보다 더 많은 Vm 실제로 작동 하 다음 hello hello Vm 수를 요청한 후 추가 Vm이 프로 비전 성공적으로 삭제 합니다. 오버프로비전은 프로비전 성공률을 높이고 배포 시간을 절약합니다. Hello 추가 Vm 및은 포함 되지 않는 할당량 제한에 대 한 청구 되지 됩니다.

과도 프로 비전가 프로 비전 된 성공률을 향상 시킬, 동작이 발생할 수 있기 혼동 응용 프로그램에 대 한 디자인된 하지 toohandle 나타나고 사라지면 다음 추가 Vm은 합니다. off, tooturn 과도 프로 비전을 확보 문자열 서식 파일에 다음 hello: `"overprovision": "false"`합니다. 자세한 내용은 hello에서 확인할 수 있습니다 [배율 설정 REST API 문서](/rest/api/virtualmachinescalesets/create-or-update-a-set)합니다.

사용자 관리 저장소를 사용 하는 크기 집합 과도 프로 비전 해제 하는 경우 저장소 계정당 20 개 이상의 Vm 수 있지만 toogo 위에 40 IO 성능상의 이유로 권장 되지 않습니다. 

## <a name="limits"></a>제한
크기 집합 (플랫폼 이미지) 마켓플레이스 이미지를 기반으로 하며 구성 toouse Azure 관리 되는 디스크의 용량이 too1, 000 Vm 지원 합니다. 눈금 집합 toosupport 100 개 이상의 Vm을 구성 하면 일부 시나리오 작업 (예에서는 부하 분산) 용 동일 hello 합니다. 자세한 내용은 [대규모 가상 컴퓨터 확장 집합과 작동](virtual-machine-scale-sets-placement-groups.md)을 참조하세요. 

크기 집합 사용자 관리 저장소 계정으로 구성 된 현재 제한 too100 Vm (이며 5 저장소 계정은이 눈금에 대 한 권장 됩니다).

(하나는 사용자에 의해 작성) 사용자 지정 이미지를 기반으로 크기 집합의 Azure 관리 하는 디스크를 사용 하 여 구성 하는 경우 too100 vm 용량이 있을 수 있습니다. Hello 크기 집합을 사용자가 관리 하는 저장소 계정으로 구성 된 경우 하나의 저장소 계정 내에서 모든 운영 체제 디스크 Vhd를 만들어야 합니다. 결과적으로, hello 최대 권장 Vm 크기 집합 기반으로 사용자 지정 이미지의에서 수 및 사용자 관리 저장소는 20 개입니다. 과도 프로 비전 해제 하면 too40 위로 이동할 수 있습니다.

많은 수의 Vm에 대 한 여러 크기 조정 설정에 표시 된 대로 toodeploy 해야 이러한 제한을 허용 보다 [이 서식 파일](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale)합니다.

