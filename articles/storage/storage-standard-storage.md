---
title: "aaaHD 기반 비용 효율적인 표준 저장소 및 Azure VM 디스크 | Microsoft Docs"
description: "비용 효율적인 표준 저장소와 관리되지 않는 VM 디스크 및 관리 VM 디스크를 설명합니다."
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c454c61254c6b160bdf2cd39ea3319452e3e4898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>비용 효율적인 표준 저장소와 관리되지 않는 Azure VM 디스크 및 관리 Azure VM 디스크

Azure 표준 저장소는 대기 시간에 영향을 받지 않는 워크로드를 실행하는 VM에 대해 안정적인 저비용 디스크 지원을 제공합니다. 또한 Blob, 테이블, 큐 및 파일을 지원합니다. 표준 저장소로 hello 데이터는 하드 디스크 드라이브 (Hdd)에 저장 됩니다. VM 작업 시 개발/테스트 시나리오 및 덜 중요한 워크로드에는 표준 저장소 디스크를 사용하고 중요 업무용 프로덕션 응용 프로그램에는 프리미엄 저장소 디스크를 사용할 수 있습니다. 표준 저장소는 모든 Azure 지역에서 사용할 수 있습니다. 

이 문서 중점적으로 VM 디스크에 대 한 표준 저장소의 hello 사용 합니다. Blob, 테이블, 큐 및 파일을 사용 하 여 저장소의 hello 사용에 대 한 자세한 내용은 toohello를 참조 하십시오 [소개 tooStorage](storage-introduction.md)합니다.

## <a name="disk-types"></a>디스크 유형

Azure Vm에 대 한 toocreate 표준 디스크는 두 가지가.

**디스크 관리 되지 않는**:이 방법은 hello 원래 hello 저장소 사용 되는 계정 toostore hello VHD 해당 하는 파일 toohello VM 디스크를 관리할 수 있습니다. VHD 파일은 저장소 계정에 페이지 Blob으로 저장됩니다. 관리 되지 않는 디스크 주로 DSv2 hello 및 GS 시리즈 처럼 프리미엄 저장소를 사용 하는 hello Vm을 포함 하는 Azure VM 크기, 연결 된 tooany 될 수 있습니다. Azure Vm 지원 VM 당 저장소 too256 TB를 허용 하는 여러 가지 표준 디스크를 연결 합니다.

[**Azure 관리 되는 디스크**](storage-managed-disks-overview.md):이 기능은 귀하에 대해 hello VM 디스크에 대 한 사용 하는 hello 저장소 계정을 관리 합니다. Hello 유형 (프리미엄 또는 표준) 및 크기를 지정 하면 필요한 디스크의을 Azure 만들고에서 hello 디스크를 관리 합니다. 여러 저장소 계정에서 순서 tooensure에 hello 저장소 계정에 대 한 hello 확장성 제한 내에 유지 hello 디스크를 배치 하는 방법에 대 한 tooworry 없는-Azure를 처리 하는 사용자에 대 한 합니다.

두 가지 유형의 디스크를 사용할 수 있는 경우에 관리 하는 디스크 tootake 혜택 많은 기능을 사용 하는 것이 좋습니다.

Azure 표준 저장소 시작 tooget 방문 [무료로 시작](https://azure.microsoft.com/pricing/free-trial/)합니다. 

어떻게 toocreate 관리 하는 디스크를 사용 하 여 VM을 참조 하십시오 hello 다음 중 하나에 대 한 내용은 문서입니다.

* [Resource Manager 및 PowerShell을 사용하여 VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md)
* [Hello Azure CLI 2.0을 사용 하 여 Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md)

## <a name="standard-storage-features"></a>표준 저장소 기능 

표준 저장소의 hello 기능 중 일부에 대해 살펴보겠습니다. 자세한 내용은 참조 하십시오 [소개 tooAzure 저장소](storage-introduction.md)합니다.

**표준 저장소**: Azure 표준 저장소는 Azure Disks, Azure Blobs, Azure File Storage, Azure Tables 및 Azure Queues를 지원합니다. toouse 표준 저장소 서비스와 함께 시작 [Azure 저장소 계정 만들기](storage-create-storage-account.md#create-a-storage-account)합니다.

**표준 저장소 디스크:** tooall Azure Vm 크기 시리즈 Vm hello DSv2 및 GS 시리즈와 같이 프리미엄 저장소로 사용을 포함 하 여 직접 연결 된 표준 저장소 디스크 될 수 있습니다. 표준 저장소 디스크에 연결 된 tooone VM 수만 있습니다. 그러나 하나 이상의 toohello 최대 디스크 개수 해당 VM 크기에 대해 정의 된 이러한 디스크 tooa VM에 연결할 수 있습니다. 섹션에 나오는 표준 저장소 확장성 및 성능 목표에 hello, hello 사양 보다 자세히 설명 합니다. 

**표준 페이지 blob**: 표준 페이지 blob는 사용 되는 toohold Vm에 대 한 영구 디스크 및 Azure Blob의 다른 형식 처럼 REST를 통해 직접 액세스할 수도 있습니다. [페이지 Blob](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs)은 임의 읽기 및 쓰기 작업용으로 최적화된 512바이트 페이지 컬렉션입니다. 

**저장소 복제:** 대부분의 지역에서 표준 저장소 계정의 데이터는 로컬에 복제되거나 여러 데이터 센터에 지리적으로 복제될 수 있습니다. hello 4 유형의 복제에 사용할 수 있는 로컬 중복 저장소 (LRS), 영역 중복 저장소 (ZRS), 지역 중복 저장소 (GRS) 및 읽기 액세스 지역 중복 저장소 (RA-GRS) 됩니다. 표준 저장소의 Managed Disks는 현재 LRS(로컬 중복 저장소)만 지원합니다. 자세한 내용은 [저장소 복제](storage-redundancy.md)를 참조하세요.

## <a name="scalability-and-performance-targets"></a>확장성 및 성능 대상

이 섹션에서는 표준 저장소를 사용 하는 경우 필요한 tooconsider hello 확장성 및 성능 목표를 설명 합니다.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>계정 제한 – toomanaged 디스크는 적용 되지 마십시오

| **리소스** | **기본 제한** |
|--------------|-------------------|
| 저장소 계정당 TB  | 500TB |
| 저장소 계정당<sup>1</sup> 최대 수신(미국 지역) | GRS/ZRS를 사용하는 경우 10Gbps, LRS의 경우 20Gbps |
| 저장소 계정당<sup>1</sup> 최대 송신(미국 지역) | RA-GRS/GRS/ZRS를 사용하는 경우 20Gbps, LRS의 경우 30Gbps |
| 저장소 계정당<sup>1</sup> 최대 수신(유럽 및 아시아 지역) | GRS/ZRS를 사용하는 경우 5Gbps, LRS의 경우 10Gbps |
| 저장소 계정당<sup>1</sup> 최대 송신(유럽 및 아시아 지역) | RA-GRS/GRS/ZRS를 사용하는 경우 10Gbps, LRS의 경우 15Gbps |
| 저장소 계정당 총 요청 빈도(개체 크기는 1KB로 가정함) | Too20, 000 IOPS, 초당, 엔터티 또는 메시지 / 초 |

<sup>1</sup> 유입은 저장소 계정 tooa 송신할 tooall 데이터 (요청)입니다. 유출은 저장소 계정에서 수신 되 고 tooall 데이터 (요청)입니다.

자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.

Hello 필요한 응용 프로그램의 단일 저장소 계정의 확장성 목표 hello를 초과 하는 경우 응용 프로그램 toouse 여러 저장소 계정을 빌드하고 해당 저장소 계정에서 데이터를 분할 합니다. 또는 Azure 관리 되는 디스크 수 및 Azure는 hello 분할 및 데이터의 배치를 관리 합니다.

### <a name="standard-disks-limits"></a>표준 디스크 한도

프리미엄 디스크와는 달리 당 IOPS (초당) 및 처리량 (대역폭)의 표준 디스크 입/출력 작업 hello 프로 비전 되지 않습니다. hello 표준 디스크의 성능에 따라 달라 집니다 hello VM 크기 toowhich hello 디스크를 연결 하면 뷰어에서 hello 디스크의 크기가 아니라 toohello 합니다. Tooachieve hello 테이블 아래에 나열 된 toohello 성능 제한을 예상할 수 있습니다.

**표준 디스크 한도(관리 및 관리되지 않는)**

| **VM 계층**            | **기본 계층 VM** | **표준 계층 VM** |
|------------------------|-------------------|----------------------|
| 최대 디스크 크기          | 4,095GB           | 4,095GB              |
| 디스크당 최대 8KB IOPS | Too300를         | Too500를            |
| 디스크당 최대 대역폭 | too60 m B/초     | too60 m B/초        |

워크로드에 대기 시간이 짧은 고성능 디스크 지원이 필요한 경우 Premium Storage를 사용하는 것이 좋습니다. 프리미엄 저장소의 많은 혜택 방문 tooknow [고성능 프리미엄 저장소 및 Azure VM 디스크](storage-premium-storage.md)합니다. 

## <a name="snapshots-and-copy-blob"></a>스냅숏 및 Blob 복사

toohello 저장소 서비스를 hello VHD 파일은 페이지 blob입니다. 페이지 blob의 스냅숏을 만들 수 있으며 다른 저장소 계정 등의 tooanother 위치를 복사할 수 있습니다.

### <a name="unmanaged-disks"></a>관리되지 않는 디스크

만들 수 있습니다 [증분 스냅숏](storage-incremental-snapshots.md) 동일 hello에 관리 되지 않는 표준 디스크에 대 한 스냅숏 저장소를 사용 하면 표준 방법입니다. 스냅숏을 만들 원본 디스크가 로컬 중복 저장소 계정에 해당 스냅숏을 tooa 표준 지역 중복 저장소 계정 다음 복사 하는 것이 좋습니다. 자세한 내용은 [Azure 저장소 중복 옵션](storage-redundancy.md)을 참조하세요.

연결 된 tooa VM 디스크가 있는 경우 특정 API 작업 hello 디스크에 허용 되지 않습니다. 예를 들어 수행할 수 없습니다는 [Blob 복사](/rest/api/storageservices/Copy-Blob) hello 디스크가 있다면 해당 blob에 대 한 작업이 tooa VM을 연결 합니다. 대신, hello를 사용 하 여 해당 blob의 스냅숏을 먼저 만들 [스냅숏 Blob](/rest/api/storageservices/Snapshot-Blob) REST API 메서드, 한 다음 hello [Blob 복사](/rest/api/storageservices/Copy-Blob) hello 스냅숏 toocopy hello의 디스크를 연결 합니다. 또는 hello 디스크를 분리 하 고 필요한 모든 작업을 수행할 수 있습니다.

전자 메일로 toomaintain 지리적 중복 복사본을 스냅숏 Blob 복사 또는 AzCopy를 사용 하 여 로컬 중복 저장소 계정 tooa 표준 지역 중복 저장소 계정에서 복사할 수 있습니다. 자세한 내용은 참조 [hello AzCopy 명령줄 유틸리티를 사용 하 여 데이터를 전송](storage-use-azcopy.md) 및 [Blob 복사](/rest/api/storageservices/Copy-Blob)합니다.

표준 저장소 계정에서 페이지 Blob에 대한 REST 작업을 수행하는 방법에 대한 자세한 내용은 [Azure Storage 서비스 REST API](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference)를 참조하세요.

### <a name="managed-disks"></a>관리 디스크

관리 되는 디스크에 대 한 스냅숏은 hello 표준 관리 디스크도 저장 되는 관리 되는 디스크의 읽기 전용 복사본입니다. 증분 스냅숏 관리 하는 디스크에 대 한 현재 지원 되지 않지만 hello 나중에 지원 됩니다.

관리 되는 디스크가 있는 VM 연결된 tooa, 특정 API 작업 hello 디스크에 허용 되지 않습니다. 예를 들어 hello 디스크가 연결 된 tooa VM 되는 동안 공유 액세스 서명 (SAS) tooperform 복사 작업을 생성할 수 없습니다. 대신 먼저 hello 디스크의 스냅숏을 만들고 hello 스냅숏의 hello 복사를 수행 합니다. 또는 hello 디스크를 분리 하 고 공유 액세스 서명 (SAS) tooperform hello 복사 작업을 생성 합니다.

## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구

표준 저장소를 사용할 때는 hello 다음 청구 고려 사항이 적용 됩니다.

* 표준 저장소 관리되지 않는 디스크/데이터 크기 
* 표준 관리 디스크
* 표준 저장소 스냅숏
* 아웃바운드 데이터 전송
* 트랜잭션

**저장소 디스크 및 데이터 크기를 관리 되지 않는:** 관리 되지 않는 디스크 및 기타 데이터 (blob, 테이블, 큐 및 파일)에 대해 사용 중인 공간의 hello 크기에 대해서만 청구 됩니다. 예를 들어, 페이지 blob 인 127 GB으로 프로 비전 된 VM이 있는 경우 hello VM은 실제로 10GB의 공간을 사용 하 여 결제일 10GB의 공간에 대 한 합니다. Too8191 GB 표준 저장소 및 표준 관리 되지 않는 디스크 too4095 GB 지원합니다. 

**관리 디스크:** 관리 되는 디스크를 프로 비전 하는 hello 크기에 청구 됩니다. 10GB 디스크로 프로 비전 된 디스크에만 5GB를 사용 하는 경우 여전히 10gb hello 프로 비전 크기에 대 한 청구 됩니다.

**스냅숏을**: 표준 디스크의 스냅숏은 hello 스냅숏에 사용 되는 hello 추가 용량에 대 한 요금이 청구 됩니다. 스냅숏에 대한 자세한 내용은 [Blob의 스냅숏 만들기](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob)를 참조하세요.

**아웃바운드 데이터 전송**: [아웃바운드 데이터 전송](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 데이터 센터에서 데이터 전송) 시 대역폭 사용에 대해 청구가 발생합니다.

**트랜잭션**: Azure에서는 표준 저장소의 트랜잭션 100,000개당 0.0036달러의 요금이 청구됩니다. 트랜잭션 모두 읽기 및 쓰기 작업 toostorage 있습니다.

표준 저장소, Virtual Machines 및 Managed Disks 가격 책정에 대한 자세한 내용은 다음을 참조하세요.

* [Azure 저장소 가격](https://azure.microsoft.com/pricing/details/storage/)
* [가상 컴퓨터 가격](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Managed Disks 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Azure Backup 서비스 지원 

관리되지 않는 디스크가 포함된 가상 컴퓨터는 Azure Backup을 사용하여 백업할 수 있습니다. [자세한 내용](../backup/backup-azure-vms-first-look-arm.md).

시간 기반 백업, 쉽게 복원할 수 VM 및 백업 보존 정책을 관리 하는 디스크 toocreate 백업 작업으로 hello Azure 백업 서비스를 사용할 수 있습니다. 자세한 내용은 [Managed Disks로 VM에 Azure Backup 서비스 사용](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)을 참조하세요.

## <a name="next-steps"></a>다음 단계

* [소개 tooAzure 저장소](storage-introduction.md)

* [저장소 계정을 만드는](storage-create-storage-account.md)

* [Managed Disks 개요](storage-managed-disks-overview.md)

* [Resource Manager 및 PowerShell을 사용하여 VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Hello Azure CLI 2.0을 사용 하 여 Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md)
