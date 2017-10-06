---
title: "Azure의 Windows Vm에 대 한 aaaStorage 솔루션 | Microsoft Docs"
description: "Hello 핵심 디자인 및 구현 지침 Azure 인프라 서비스에서 저장소 솔루션을 배포 하기 위한 방법을 알아봅니다."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Windows VM에 대한 Azure Storage 인프라 지침

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

이 문서에서는 최적의 VM(가상 컴퓨터) 성능을 위한 저장소 요구 사항 및 디자인 고려 사항을 이해하는 데 주안점을 둡니다.

## <a name="implementation-guidelines-for-storage"></a>저장소에 대한 구현 지침
의사 결정:

* 관리 되지 않는 디스크 또는 Azure 관리 되는 디스크 toouse 예정 입니까?
* Toouse 표준 또는 프리미엄 저장소 작업에 필요 합니까?
* 필요 디스크 스트라이프 toocreate 디스크 4TB 보다 큰?
* 디스크 스트라이프 tooachieve 최적의 I/O 성능 작업에 필요 합니까?
* 집합의 저장소 계정이 필요 한가요 toohost IT 작업 또는 인프라?

작업:

* 배포 하 고 적절 한 수 hello 및 저장소 계정의 유형을 계획 hello 응용 프로그램의 I/O 요구 사항을 검토 합니다.
* 명명 규칙을 사용 하 여 저장소 계정의 hello 집합을 만듭니다. Azure PowerShell 또는 hello 포털을 사용할 수 있습니다.

## <a name="storage"></a>저장소
Azure 저장소는 VM(가상 컴퓨터) 및 응용 프로그램의 배포 및 관리 작업의 핵심 부분입니다. Azure 저장소 파일 데이터, 구조화 되지 않은 데이터 및 메시지를 저장 하기 위한 서비스를 제공 하 고 Vm을 지 원하는 hello 인프라의 일부 이기도 합니다.

[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md) hello 백그라운드 있습니다에 대 한 저장소를 처리 합니다. 관리 되지 않는 디스크와 저장소 계정을 만듭니다 toohold hello 디스크 (VHD 파일) Azure Vm에 대 한. 확장 하는 경우 디스크를 사용 하 여 저장소에 대 한 hello IOPS 제한을 초과 하지 않도록 추가 저장소 계정을 만들어지므로 있는지 확인 해야 합니다. 관리 되는 디스크 저장소를 처리를 사용 하면 더 이상 영향을 받습니다 hello 저장소 계정 제한 하 여 (20, 000 IOPS 등 / 계정). 또한 없을 toocopy 사용자 지정 이미지 (VHD 파일) toomultiple 저장소 계정입니다. – Azure 지역 마다 하나의 저장소 계정-중앙 위치에서 관리할 수 있으며 구독에 있는 Vm의 toocreate 수백 사용. 새 배포에 Managed Disks를 사용하는 것이 좋습니다.

VM 지원을 위해 다음 두 가지 저장소 계정 유형을 사용할 수 있습니다.

* 표준 저장소 계정 제공 되는 tooblob 저장소 (Azure VM 디스크를 저장 하는 데 사용), 테이블 저장소, 큐 저장소 및 파일 저장소.
* [Premium 저장소](../../storage/storage-premium-storage.md) 계정은 AlwaysOn 클러스터의 SQL Server와 같이 I/O 집약적 워크로드에 대해 대기 시간이 낮은 고성능 디스크 지원을 제공합니다. Premium 저장소는 현재 Azure VM 디스크만 지원합니다.

Azure는 운영 체제 디스크, 임시 디스크를 및 0개 이상의 선택적 데이터 디스크로 VM을 만듭니다. hello 운영 체제 디스크 및 데이터 디스크는 hello 컴퓨터 거주 hello 노드에서 hello 임시 디스크를 로컬로 저장 하는 반면 Azure 페이지 blob입니다. Tooonly 비 영구적인 데이터에 대 한 VM을 유지 관리 이벤트 중 호스트 간에 마이그레이션할 수 있습니다 hello로이 임시 디스크를 사용 하는 응용 프로그램을 디자인할 때 주의 해야 합니다. Hello 임시 디스크에 저장 된 모든 데이터가 손실 될 수 있습니다.

내 구성과 고가용성 제공한 hello 기본 Azure 저장소 환경 tooensure 데이터가 유지 계획 되지 않은 유지 관리 또는 하드웨어 오류 로부터 보호 됩니다. Azure 저장소 환경을 디자인할 때 tooreplicate VM 저장소를 선택할 수 있습니다.

* 지정된 Azure 데이터 센터 내에서 로컬로
* 지정된 지역 내에서 Azure 데이터 센터에서
* 서로 다른 지역의 Azure 데이터 센터에서

읽을 수 [고가용성에 대 한 hello 복제 옵션에 대 한 자세한](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)합니다.

운영 체제 디스크 및 데이터 디스크의 최대 크기는 4TB입니다. 데이터 디스크 toopresent 논리가 넘는 볼륨 4TB tooyour VM 풀링에 함께 Windows Server 2012 또는 이후 toosurpass의 저장소 공간이 한이도 사용할 수 있습니다.

Azure Storage 배포를 디자인할 때는 확장성이 어느 정도 제한될 수 있습니다. 자세한 내용은 [Microsoft Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../../azure-subscription-service-limits.md#storage-limits)을 참조하세요. [Azure Storage 확장성 및 성능 목표](../../storage/storage-scalability-targets.md)도 참조하세요.

응용 프로그램 저장소의 경우 문서, 이미지, 백업, 구성 데이터, 로그 등의 구조화되지 않은 개체 데이터를 저장할 수 있습니다. Blob Storage를 사용합니다. 응용 프로그램 tooa 연결 된 가상 디스크 toohello VM을 작성 하는 대신 hello 응용 프로그램을 작성할 수 직접 tooAzure blob 저장소. Blob 저장소의 hello 옵션도 제공 [핫 및 저장소 계층 냉각용](../../storage/storage-blob-storage-tiers.md) 가용성 요구와 비용 제약 조건에 따라 합니다.

## <a name="striped-disks"></a>스트라이프 디스크
을 사용 있으므로 toocreate 디스크, 4TB 보다 큰 대부분의 경우에서 외에도 데이터 디스크에 대 한 스트라이프를 사용 하 여 단일 볼륨에 대 한 tooback hello 저장소 여러 blob를 허용 하 여 성능이 향상 됩니다. 스트라이핑 기능을 hello I/O 필요한 toowrite 및 단일 논리적 디스크에서 읽은 데이터 동시에 진행 됩니다.

Azure는 데이터 디스크 개수 hello 및 hello VM 크기에 따라 사용할 수 있는 대역폭에 대 한 제한을 적용 됩니다. 자세한 내용은 [가상 컴퓨터의 크기](sizes.md)를 참조하세요.

Azure 데이터 디스크에 대 한 디스크 스트라이프를 사용 하는 경우 hello 지침을 고려 합니다.

* Hello VM 크기에 허용 되는 hello 최대 데이터 디스크를 연결 합니다.
* 저장소 공간을 사용합니다.
* Azure 데이터 디스크 캐싱 옵션을 사용하지 않습니다(캐싱 정책 = 없음).

자세한 내용은 [저장소 공간 - 성능을 높이기 위한 설계](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx)를 참조하세요.

## <a name="multiple-storage-accounts"></a>여러 저장소 계정
이 섹션이 너무 적용 되지 않습니다[Azure 관리 되는 디스크](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)와 별도 저장소 계정을 만들지 않습니다. 

관리 되지 않는 디스크에 대 한 Azure 저장소 환경을 디자인할 때 여러 저장소 계정을 사용할 수 있습니다 증가 hello 수가 Vm으로 배포 합니다. 이 방법은 hello 기본 Azure 저장소 인프라 toomaintain 최적의 성능 Vm 및 응용 프로그램에서 I/O hello 아웃 배포할 수 있습니다. 배포 하는 hello 응용 프로그램을 디자인할 때 Azure 저장소 계정에서 각 VM에 hello I/O 요구 사항 및 해당 Vm으로 균형을 고려 합니다. Tooavoid Vm 하나 또는 두 개의 toojust 저장소 계정에 요구 되는 모든 hello 높은 I/O를 그룹화 해 보십시오.

Hello 다양 한 Azure 저장소 옵션의 hello I/O 기능에 대 한 자세한 내용은 및 일부 권장 최대값에 대 한 참조 [Azure 저장소 확장성 및 성능 목표가](../../storage/storage-scalability-targets.md)합니다.

## <a name="next-steps"></a>다음 단계
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

