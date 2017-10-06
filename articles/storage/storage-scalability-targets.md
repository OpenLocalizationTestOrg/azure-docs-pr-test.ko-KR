---
title: "aaaAzure 저장소 확장성 및 성능 목표 | Microsoft Docs"
description: "Azure 저장소의 경우 용량, 요청 속도 및 두 표준 및 프리미엄 저장소 계정에 대 한 인바운드 및 아웃 바운드 대역폭을 포함 하 여 hello 확장성 및 성능 목표에 알아봅니다. Hello Azure 저장소 서비스의 각 파티션에 대 한 성능 목표를 이해 합니다."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 98de116a01b64f3418808a5f626b6c70d8d432e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Azure 저장소 확장성 및 성능 목표
## <a name="overview"></a>개요
이 항목에서는 Microsoft Azure 저장소에 대 한 hello 확장성 및 성능 항목을 설명 합니다. 기타 Azure 제한 사항에 대한 요약은 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)을 참조하세요.

> [!NOTE]
> 모든 저장소 계정은 새로운 플랫 네트워크 토폴로지에서 hello에서 실행 되며 작성 된 시간에 관계 없이 아래에 설명 된 hello 확장성 및 성능 목표가 지원. 자세한 내용은 hello Azure 저장소 플랫 네트워크 아키텍처 및 확장성 참조 [Microsoft Azure 저장소: A 항상 사용 가능한 클라우드 저장소 서비스 강력한 일관성](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)합니다.
> 
> [!IMPORTANT]
> 여기에 나열 된 hello 확장성 및 성능 목표는 고성능 저장소의 목표 이지만 충분히 충족 가능 합니다. 어떤 경우 든, 저장 된 개체의 hello 크기에 따라 달라 집니다 속도 대역폭을 저장소 계정으로 이용할 hello 요청 hello 액세스 패턴 사용량에 및 유형의 응용 프로그램에서 수행 하는 작업 부하를 hello 합니다. 성능 요구 사항을 충족 하는지 여부를 있는지 tootest 서비스 toodetermine를 수 있습니다. 가능 하면 트래픽의 hello 속도가 갑자기 증가 하지 않도록 하 고 파티션 간에 트래픽을 적절 하 게 분산 인지 확인 합니다.
> 
> 응용 프로그램 워크 로드에 대 한 파티션을 처리할 수 있는 것 hello 제한에 도달 하면 Azure 저장소는 tooreturn 오류 코드 503 (서버 작업 중)를 시작 하거나 오류 코드: 500 (작업 시간 초과) 응답 합니다. 이 경우 hello 응용 프로그램 재시도 대 한 지 수 백오프 정책을 사용 해야 합니다. hello 지 수 백오프 hello 부하를 hello 파티션 toodecrease 및 스파이크 아웃 tooease 트래픽 toothat 파티션을 사용할 수 있습니다.
> 
> 

Hello 필요한 응용 프로그램의 단일 저장소 계정의 확장성 목표 hello를 초과 하는 경우 응용 프로그램 toouse 여러 저장소 계정 구축 수 있으며 해당 저장소 계정에 데이터 개체를 분할할 수 있습니다. 볼륨 가격에 대한 자세한 내용은 [Azure 저장소 가격 책정](https://azure.microsoft.com/pricing/details/storage/) 을 참조하세요.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>Blob, 큐, 테이블 및 파일에 대한 확장성 목표
[!INCLUDE [azure-storage-limits](../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>가상 컴퓨터 디스크에 대한 확장성 목표
[!INCLUDE [azure-storage-limits-vm-disks](../../includes/azure-storage-limits-vm-disks.md)]

자세한 내용은 [Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux VM 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.

## <a name="managed-virtual-machine-disks"></a>관리되는 가상 컴퓨터 디스크

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>관리되지 않는 가상 컴퓨터 디스크
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Azure 리소스 관리자에 대한 확장성 목표
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Azure 저장소의 파티션
Azure 저장소 (blob, 메시지, 엔터티 및 파일)에 저장 된 데이터를 보유 하는 모든 개체 tooa 파티션에 속하며 파티션 키로 식별 됩니다. hello 파티션 방법을 Azure 저장소 부하를 분산 blob, 메시지, 엔터티 및 파일 서버 toomeet hello 트래픽 요구 사항을 이러한 개체의 결정 합니다. hello 파티션 키는 고유 하며 blob, 메시지 또는 엔터티 toolocate 사용된 됩니다.

hello 테이블에서 위의 [표준 저장소 계정의 확장성 목표](#standard-storage-accounts) 목록 hello 각 서비스용 단일 파티션의 성능 목표입니다.

파티션 부하 분산 및 확장성에 영향을 각 방법으로 다음 hello에 hello 저장소 서비스에 대해:

* **Blob**: blob에 대 한 hello 파티션 키는 계정 이름 + 컨테이너 이름 + blob 이름입니다. 이 요구 하는 hello blob에 로드 하는 경우 각 blob 자체 분할에 있을 수 있음을 의미 합니다. Blob 액세스 toothem 아웃 순서 tooscale의 여러 서버에서 배포할 수 있습니다 하지만 단일 blob 단일 서버에 의해 제공 될 수 있습니다. Blob 컨테이너에서 blob를 논리적으로 그룹화하는 반면 해당 그룹화에는 파티션이 적용되지 않습니다.
* **파일**: hello 파티션 키 파일 이름 + 파일 이름을 공유 하는 계정입니다. 즉, 파일 공유의 모든 파일도 단일 파티션에 포함됩니다.
* **메시지**: 메시지에 대 한 hello 파티션 키 이므로 hello 계정 이름 + 큐 이름, 큐에 있는 모든 메시지를 단일 파티션으로 그룹화 되 고 단일 서버에 의해 제공 됩니다. 많은 큐 저장소 계정이 있을 수 있지만 toobalance hello에 대 한 로드 하는 다른 서버에서 다른 큐를 처리할 수 있습니다.
* **엔터티**: hello 파티션 키는 엔터티에 대 한 계정 이름 + 테이블 이름 + 파티션 키를 hello 파티션 키의 필요한 hello hello 값이 사용자 정의 **PartitionKey** hello 엔터티에 대 한 속성. 서버를 분할 하는 동일한 분할 및에서 제공 hello 동일 hello로 그룹화 되 고 동일한 파티션 키 값 hello로 모든 엔터티. 응용 프로그램을 디자인 하는 중요 한 지점 toounderstand입니다. 응용 프로그램 엔터티를 엔터티를 단일 파티션으로 그룹화의 hello 데이터 액세스 기능을 사용 하 여 여러 파티션을 분산의 hello 확장성 이점을 균형을 조정 해야 합니다.  

주요 이점은 toogrouping 단일 파티션으로 테이블의에서 엔터티 집합이 hello 동일 분할 단일 서버에는 파티션이 있기 때문에 엔터티 간에 가능한 tooperform 원자성 일괄 처리 작업이 된다는 점입니다. 엔터티 그룹에 일괄 처리 작업 tooperform을 원할 경우 것이 좋습니다 hello로 그룹화 동일한 파티션 키입니다. 

다른 손 hello, hello 테이블 동일 하지만 서로 다른 파티션 키에에서 있는 엔터티는 확장성이 뛰어난 가능한 toohave 있어서 서로 다른 서버에서 부하 분산 될 수 있습니다.

테이블 분할 전략 디자인에 대한 자세한 권장 사항은 [여기](https://msdn.microsoft.com/library/azure/hh508997.aspx)에서 확인할 수 있습니다.

## <a name="see-also"></a>참고 항목
* [저장소 가격 정보](https://azure.microsoft.com/pricing/details/storage/)
* [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../azure-subscription-service-limits.md)
* [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](storage-premium-storage.md)
* [Azure 저장소에서 복제](storage-redundancy.md)
* [Microsoft Azure 저장소 성능 및 확장성 검사 목록](storage-performance-checklist.md)
* [Microsoft Azure 저장소: 일관성과 가용성이 뛰어난 클라우드 저장소 서비스](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

