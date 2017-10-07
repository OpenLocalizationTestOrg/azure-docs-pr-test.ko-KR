---
title: "Azure에서 Linux Vm에 대해 aaaAvailability 설정 | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스의 가용성 집합을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 24f1d91c-8cc0-4251-bb67-ac4c4c37e8cd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78e4da5c8fd9eb186cafacb46454444b73a9439c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-linux-vms"></a>Linux VM에 대한 Azure 가용성 집합 지침

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

이 문서에서는 필요한 이해 hello 가용성 집합 tooensure 응용 프로그램에 대 한 계획 단계에 계속 액세스할 수 계획 되거나 계획 되지 않은 이벤트 동안 합니다.

## <a name="implementation-guidelines-for-availability-sets"></a>가용성 집합에 대한 구현 지침
의사 결정:

* 가용성 집합을 얼마나 필요 한가요 hello에 대 한 다양 한 역할 및 계층 응용 프로그램 인프라에서?

작업:

* 필요한 각 응용 프로그램 계층에서 hello Vm 수를 정의 합니다.
* 응용 프로그램에 사용 되는 오류 또는 업데이트 도메인 toobe tooadjust hello 수 해야 하는지 확인 합니다.
* 명명 규칙 및 작업를 사용 하는 데 필요한 hello 가용성 집합을 정의 합니다. Vm에 상주 합니다. VM은 하나의 가용성 집합에만 포함될 수 있습니다. 

## <a name="availability-sets"></a>가용성 집합
Azure에서 가상 컴퓨터 (Vm)는 가용성 집합 이라는 tooa 논리적 그룹화에 배치할 수 있습니다. 가용성 집합 내에서 Vm을 만들 때 Azure 플랫폼 hello 인프라 내부 hello 해당 Vm의 hello 배치를 분산 합니다. 계획 된 유지 관리 이벤트 toohello Azure 플랫폼 또는 기본 하드웨어 있을 해야/인프라 오류, hello 가용성 집합을 사용 하면 하나 이상의 VM 실행 상태로 유지 됩니다.

모범 사례로 응용 프로그램은 단일 VM에만 상주하지 않는 것이 좋습니다. 단일 VM이 포함 된 가용성 집합에는 계획 되거나 계획 되지 않은 이벤트 hello Azure 플랫폼 내에서 모든 보호를 좁아집니다. hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) 는 가용성 집합 tooallow hello 분배 Vm의 hello 기본 인프라 내에서 둘 이상의 Vm 필요 합니다. 사용 중인 경우 [Azure 프리미엄 저장소](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello Azure SLA 적용 tooa 단일 VM입니다.

Azure의 hello 기본 인프라 toomultiple 하드웨어 클러스터에 분할 됩니다. 각 하드웨어 클러스터는 다양한 VM 크기를 지원할 수 있습니다. 가용성 집합은 언제든지 특정 시점에 단일 하드웨어 클러스터에만 호스트될 수 있습니다. 따라서 단일 가용성 집합에 있을 수 있는 hello 범위의 VM 크기는 hello 하드웨어 클러스터에서 지 원하는 제한 toohello VM의 범위 크기입니다. hello hello 가용성 집합의 첫 번째 VM을 배포할 때 또는 hello 중지-할당 취소 된 상태에서 모든 Vm을 현재 되 가용성 집합에 첫 번째 VM hello 시작할 때 hello 가용성 집합에 대 한 hello 하드웨어 클러스터 선택 되어 있습니다. hello 다음 CLI 명령을 사용 하는 toodetermine hello 범위의 VM 크기 가용성 집합에 사용할 수 있는 일 수 있습니다: "az vm 목록-크기-위치 \<문자열\>"

각 하드웨어 클러스터 toomultiple 업데이트 도메인과 오류 도메인에 분할 됩니다. 이러한 도메인은 공통 업데이트 주기를 공유하거나 전력 및 네트워킹과 같은 비슷한 실제 인프라를 공유하는 호스트에 의해 정의됩니다. Azure는 가용성 집합 도메인 toomaintain 가용성 및 내결함성 내에서 Vm을 자동으로 배포 합니다. 가용성 집합 내에서 Vm 수 hello 및 응용 프로그램의 hello 크기에 따라 hello 수를 조정할 수 있습니다 toouse 원하는 도메인입니다. [업데이트 및 장애 도메인의 가용성 및 사용 관리](manage-availability.md)에 대해 자세히 읽어보세요.

응용 프로그램 인프라를 디자인할 때는 hello 응용 프로그램 계층 toouse을 계획 합니다. Hello를 사용 하는 그룹 Vm의 가용성 집합 nginx 또는 Apache를 실행 하 여 프런트 엔드 Vm을 같은 tooavailability 집합에서 용도로 동일 합니다. MongoDB 또는 MySQL을 실행하는 백 엔드 VM에 대한 별도의 가용성 집합을 만듭니다. hello ´ ֲ tooensure 응용 프로그램의 각 구성 요소 가용성 집합에 의해 보호 되 고 한 번 이상 인스턴스 항상은 계속 실행 됩니다.

부하 분산 장치 가용성 집합과 함께 각 응용 프로그램 계층 toowork 앞에 사용 될 수 있습니다 및 트래픽 인스턴스를 실행 하는 라우트된 tooa 수 있는지 확인 합니다. 부하 분산 장치 없이 Vm에 전체 계획 되거나 계획 되지 않은 유지 관리 이벤트에서 실행을 계속 수는 있지만 최종 사용자의 경우 hello 주 VM 사용할 수 없으면 수 tooresolve 수 없습니다.

저장소 계층에서 고가용성을 위해 응용 프로그램을 디자인합니다. hello 가장 좋은 방법은 너무[가용성 집합에 Vm에 대 한 관리 되는 디스크를 사용 하 여](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set)합니다. 현재 관리 되지 않는 디스크를 사용 하는 경우 항상 좋습니다 너무[toouse 관리 하는 디스크 가용성 집합의 Vm으로 변환](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set)합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

