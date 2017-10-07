---
title: "aaaAzure 고급 도메인 및 표준 관리 디스크 개요 | Microsoft Docs"
description: "Azure 관리 되는 디스크를 Azure Vm을 사용 하는 경우 hello 저장소 계정 수에 대 한 처리 개요"
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 70d45226e531b43f2142f2798bdaf40f77f057f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-disks-overview"></a>Azure Managed Disks 개요

Azure 관리 되는 디스크 hello를 관리 하 여 Azure IaaS Vm에 대 한 디스크 관리를 간소화 [저장소 계정은](storage-introduction.md) hello VM 디스크와 연결 된입니다. Toospecify hello 유형 하나만 있습니다 ([프리미엄](storage-premium-storage.md) 또는 [표준](storage-standard-storage.md)) 및 hello 크기와 디스크의 필요, Azure 만들고에서 hello 디스크를 관리 합니다.

## <a name="benefits-of-managed-disks"></a>관리 디스크의 이점

이 채널 9 비디오 부터는 관리 되는 디스크를 사용 하 여 얻을 hello 이점 중 일부에 대해 살펴보겠습니다 [관리 되는 디스크와 Azure VM 복원 력 더 나은](https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency)합니다.
<br/>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Managed-Disks-for-Azure-Resiliency/player]

### <a name="simple-and-scalable-vm-deployment"></a>간단하고 확장성 있는 VM 배포

Hello 백그라운드 있습니다에 대 한 핸들 저장소 디스크를 관리합니다. 이전에 Azure Vm에 대 한 toocreate 저장소 계정 toohold hello 디스크 (VHD 파일)을 했습니다. 확장 하는 경우 디스크를 사용 하 여 저장소에 대 한 IOPS 제한은 hello를 초과 하지 않도록 추가 저장소 계정을 만든 있는지 toomake 해야 했습니다. 관리 되는 디스크 저장소를 처리를 사용 하면 더 이상 영향을 받습니다 hello 저장소 계정 제한 하 여 (20, 000 IOPS 등 / 계정). 또한 없을 toocopy 사용자 지정 이미지 (VHD 파일) toomultiple 저장소 계정입니다. – Azure 지역 마다 하나의 저장소 계정-중앙 위치에서 관리할 수 있으며 구독에 있는 Vm의 toocreate 수백 사용.

관리 되는 디스크 사용 하면 too10, 000 VM toocreate **디스크** 는 구독에 있는 하면 toocreate 수천 대의 **Vm** 단일 구독에 있습니다. 또한이 기능은 hello 확장성의 증가 [가상 컴퓨터 크기 조정 설정 (VMSS)](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) 마켓플레이스 이미지를 사용 하 여 VMSS에 천 tooa vm toocreate를 허용 하 여 합니다.

### <a name="better-reliability-for-availability-sets"></a>가용성 집합에 대한 안정성 향상

관리 되는 디스크 가용성 집합에 대 한 해당 hello 되도록 하 여 안정성을 향상을 제공의 디스크 [가용성 집합에 Vm](../virtual-machines/windows/manage-availability.md#use-managed-disks-for-vms-in-an-availability-set) 충분히 격리 서로 tooavoid 단일 실패 지점이 됩니다. 다른 저장소 배율 단위 (스탬프)에 hello 디스크를 자동으로 배치 하 여 수행 합니다. 스탬프 toohardware 또는 소프트웨어 오류로 인해 실패 하면 해당 스탬프에 디스크를 사용 하 여 VM 인스턴스만 hello 실패 합니다. 예를 들어 5 개의 Vm에서 실행 되는 응용 프로그램 및 hello Vm은 가용성 집합에 가정해 봅니다. hello 해당 Vm에 대 한 디스크 않습니다에 저장 되어 스탬프 동일 hello 한 스템 프가 다운 되 면 hello hello 응용 프로그램의 다른 인스턴스 계속 해 서 toorun 합니다.

### <a name="highly-durable-and-available"></a>뛰어난 내구성 및 가용성

Azure 디스크는 99.999% 가용성을 위해 설계되었습니다. 데이터 복제본을 3개 만들어 내구성이 뛰어나므로 데이터에 대해 안심하셔도 됩니다. 하나 또는 두 개의 복제 관련 문제가 발생 한 데이터와 오류에 대 한 높은 허용 오차를 보장할 hello 남은 복제본 수 있습니다. 이러한 아키텍처를 통해 Azure는 IaaS 디스크에 엔터프라이즈급 내구성을 지속적으로 제공할 뿐만 아니라 연간 실패율 0%로 업계 최고를 자랑합니다. 

### <a name="granular-access-control"></a>세부적인 액세스 제어

사용할 수 있습니다 [신속히 알아봅니다 액세스 제어 (RBAC)](../active-directory/role-based-access-control-what-is.md) tooassign 관리 되는 디스크 tooone 또는 더 많은 사용자에 대 한 특정 사용 권한이 있습니다. 관리 되는 디스크 읽기는 다양 한 작업을 포함 하 여 노출, 쓰기 (만들기/업데이트), delete 및 검색 하는 [공유 액세스 서명 (SAS) URI](storage-dotnet-shared-access-signature-part-1.md) hello 디스크에 대 한 합니다. 필요 tooperform 될까요 액세스 tooonly hello 작업에 권한을 부여할 수 있습니다. 예를 들어 person toocopy 관리 되는 디스크 tooa 저장소 계정을 사용 하지 않으려는 경우 하지 toogrant 액세스 toohello export 작업 해당 관리 되는 디스크에 대해 선택할 수 있습니다. 마찬가지로, person toouse SAS URI toocopy 관리 되는 디스크를 사용 하지 않으려는 경우 선택할 수 있습니다 toogrant 하지 해당 권한을 toohello 관리 되는 디스크.

### <a name="azure-backup-service-support"></a>Azure Backup 서비스 지원
Azure 백업 서비스를 관리 하는 디스크 toocreate 시간 기반 백업을, 쉽게 복원할 수 VM 및 백업 보존 정책을 사용 하 여 백업 작업을 사용 합니다. 관리 되는 디스크는만 로컬 중복 저장소 (LRS) hello 복제 옵션으로 지원 즉, 단일 지역 내 hello 데이터 복사본이 3 개 유지 합니다. 지역적 재해 복구를 위해 [Azure Backup 서비스](../backup/backup-introduction-to-azure-backup.md) 및 GRS 저장소 계정을 백업 자격 증명 모음으로 사용하여 VM 디스크를 다른 지역에 백업해야 합니다. 현재 Azure 백업 지원 데이터 디스크 크기 too1TB 백업 합니다. 자세한 내용은 [Managed Disks로 VM에 Azure Backup 서비스 사용](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup)을 참조하세요.

## <a name="pricing-and-billing"></a>가격 책정 및 대금 청구

관리 하는 디스크를 사용 하 여 hello 청구 고려 사항에 따라 적용 됩니다.
* 저장소 유형

* 디스크 크기

* 트랜잭션 수

* 아웃바운드 데이터 전송

* 관리 디스크 스냅숏(전체 디스크 복사)

좀 더 자세히 살펴보겠습니다.

**저장소 유형:** Managed Disks에는 [프리미엄](storage-premium-storage.md)(SSD 기반) 및 [표준](storage-standard-storage.md)(HDD 기반)이라는 2개의 성능 계층이 제공됩니다. 관리 되는 디스크의 hello 청구 hello 디스크에 대해 선택한 어떤 유형의 저장소에 따라 달라 집니다.


**디스크 크기**: 관리 되는 디스크에 대 한 청구 hello 디스크의 사용자를 프로 비전 하는 hello 크기에 따라 달라 집니다. Azure 지도 hello hello 테이블 아래에 지정 된 대로 디스크 관리 옵션에 가장 가까운 toohello 프로 비전 된 크기 (반올림). 각 관리 되는 디스크 지도 tooone hello의 프로 비전 된 크기를 지원 하 고 그에 따라 요금이 청구 됩니다. 예를 들어 표준 관리 디스크를 만들고 프로 비전 된 크기는 200GB를 지정 하는 경우 hello hello S20 디스크 종류의 가격 책정에 따라 청구 됩니다.

다음은 premium 관리 되는 디스크에 사용할 수 있는 hello 디스크 크기:

| **프리미엄 관리 <br>디스크 유형** | **P4** | **P6** |**P10** | **P20** | **P30** | **P40** | **P50** | 
|------------------|---------|---------|---------|---------|----------------|----------------|----------------|  
| 디스크 크기        | 32GB   | 64GB   | 128GB  | 512GB  | 1,024GB(1TB) | 2,048GB(2TB) | 4,095GB(4TB) | 


다음은 표준 관리 디스크에 사용할 수 있는 hello 디스크 크기:

| **표준 관리 <br>디스크 유형** | **S4** | **S6** | **S10** | **S20** | **S30** | **S40** | **S50** |
|------------------|---------|---------|--------|--------|----------------|----------------|----------------| 
| 디스크 크기        | 32GB   | 64GB   | 128GB | 512GB | 1,024GB(1TB) | 2,048GB(2TB) | 4,095GB(4TB) | 


**트랜잭션 수가**: hello 표준 관리 디스크에서 수행 하는 트랜잭션 수에 대 한 요금이 청구 됩니다. 프리미엄 관리 디스크에 대한 트랜잭션 비용은 없습니다.

**아웃바운드 데이터 전송**: [아웃바운드 데이터 전송](https://azure.microsoft.com/pricing/details/data-transfers/) (Azure 데이터 센터에서 데이터 전송) 시 대역폭 사용에 대해 청구가 발생합니다.

Managed Disks 가격 책정에 대한 자세한 내용은 [Managed Disks 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks)을 참조하세요.


## <a name="managed-disk-snapshots"></a>관리 디스크 스냅숏

관리 스냅숏은 기본적으로 표준 관리 디스크로 저장되는 관리 디스크의 완전한 읽기 전용 복사본입니다. 스냅숏을 사용하면 관리 디스크를 언제든지 백업할 수 있습니다. 이러한 스냅숏은 hello 원본 디스크는 별도로 존재 하 고 새 관리 되는 디스크 사용된 toocreate를 수 있습니다. 이러한 hello 사용 되는 크기에 따라 요금이 청구 됩니다. 예를 들어 64GB의 프로 비전 된 용량 및 10GB의 실제 사용 되는 데이터 크기와 관리 되는 디스크의 스냅숏을 만들면 스냅숏 10GB의 hello 사용 되는 데이터 크기에 대해서만 요금이 청구 됩니다.  

[증분 스냅숏](storage-incremental-snapshots.md) 관리 하는 디스크에 대 한 현재 지원 되지 않지만 향후 hello에 지원 됩니다.

toolearn에 더 알아봅니다 이러한 리소스를 관리 하는 디스크를 사용 하 여 toocreate 스냅숏의 하십시오 확인 방법:

* [Windows에서 스냅숏을 사용하여 관리 디스크로 저장된 VHD 복사본 만들기](../virtual-machines/windows/snapshot-copy-managed-disk.md)
* [Linux에서 스냅숏을 사용하여 관리 디스크로 저장된 VHD 복사본 만들기](../virtual-machines/linux/snapshot-copy-managed-disk.md)


## <a name="images"></a>이미지

Managed Disks는 관리되는 사용자 지정 이미지 만들기도 지원합니다. 저장소 계정의 사용자 지정 VHD에서 이미지를 만들거나 일반화된(시스템에서 준비된) VM에서 직접 만들 수 있습니다. Hello 운영 체제와 데이터 디스크를 모두 포함 하는 VM과 연결 된 디스크를 관리 되는 모든 단일 이미지를 캡처합니다. 수백 개의 hello 하지 않고 사용자 지정 이미지를 사용 하 여 Vm 만들 수이 있도록이 toocopy 또는 모든 저장소 계정을 관리 합니다.

이미지를 만드는 방법에 대 한 정보를 hello 다음 문서를 확인 하십시오.
* [어떻게 toocapture Azure에서 일반화 된 VM의 관리 되는 이미지](../virtual-machines/windows/capture-image-resource.md)
* [어떻게 toogeneralize 및 사용 하 여 Linux 가상 컴퓨터 캡처 hello Azure CLI 2.0](../virtual-machines/linux/capture-image.md)

## <a name="images-versus-snapshots"></a>이미지 및 스냅숏

종종 hello 단어 vm에서 사용 되는 "이미지"를 참조 하 고 "스냅숏"도 참조 이제 합니다. 중요 한 toounderstand hello 다음 차이 Managed Disks를 사용하면 할당이 취소되어 일반화된 VM의 이미지를 만들 수 있습니다. 이 이미지는 hello 연결 된 디스크 toohello VM의 모든 포함 됩니다. 이 이미지 toocreate 새 VM을 사용할 수 있습니다 하 고 hello 디스크를 모두 포함 됩니다.

스냅숏은은 hello 지점에서 디스크의 사본을 나올 때 시간입니다. 또한 tooone 디스크만을 적용 됩니다. (Hello OS) 디스크를 하나에 있는 VM이 있는 경우 스냅숏 또는 이미지를 사용 하 고 hello 스냅숏 또는 hello 이미지에서 VM을 만들 수 있습니다.

VM의 디스크가 5개이고 스트라이프된 경우는 어떨까요? 각 hello 디스크의 스냅숏으로 걸릴 수 있지만 VM hello 디스크 – hello 스냅숏 상태의 hello에 대 한 디스크에 대해 알고 hello 내에서 인식 하지 않습니다. 이 경우 hello 스냅숏을 toobe 서로 조정 해야 하 고는 현재 지원 되지 않습니다.

## <a name="managed-disks-and-encryption"></a>Managed Disks 및 암호화

두 가지 암호화 toodiscuss 참조 toomanaged 디스크에 있습니다. hello 먼저 하나는 저장소 서비스 암호화 SSE (), hello 저장소 서비스에서 수행 하는 합니다. hello 두 번째 메서드는 Vm에 대 한 hello OS 및 데이터 디스크에서 사용할 수 있는 Azure 디스크 암호화 합니다.

### <a name="storage-service-encryption-sse"></a>SSE(저장소 서비스 암호화)

[Azure 저장소 서비스 암호화](storage-service-encryption.md) 휴지 암호화를 제공 하 고 데이터 toomeet 조직 보안 및 규정 준수 행 결과 보호 합니다. SSE 모든 관리 하는 디스크, 스냅숏 및 관리 하는 디스크를 사용할 수 있는 모든 hello 지역에서 이미지에 대해 기본적으로 사용 됩니다. 2017 년 6 월 10 일, 년부터 모든 새 관리 되는 디스크/스냅숏/이미지 되며 tooexisting 관리 되는 디스크에 기록 하는 새 데이터 자동으로 암호화-에-rest Microsoft에서 관리 하는 키를 사용 합니다.  Hello 방문 [관리 되는 디스크 FAQ 페이지](storage-faq-for-disks.md#managed-disks-and-storage-service-encryption) 자세한 세부 정보에 대 한 합니다.


### <a name="azure-disk-encryption-ade"></a>ADE(Azure Disk Encryption)

Azure 디스크 암호화 tooencrypt hello OS 및 IaaS 가상 컴퓨터에서 사용 되는 데이터 디스크를 있습니다. 여기에 Managed Disks가 포함됩니다. Windows hello 드라이브는 업계 표준 BitLocker 암호화 기술을 사용 하 여 암호화 됩니다. Linux 용 hello 디스크 hello DM 암호화 기술을 사용 하 여 암호화 됩니다. 이 Azure 키 자격 증명 모음 tooallow 있습니다 toocontrol와 통합 hello 디스크 암호화 키를 관리 합니다. 자세한 내용은 [Windows 및 Linux IaaS VM용 Azure Disk Encryption](../security/azure-security-disk-encryption.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

관리 되는 디스크에 대 한 자세한 내용은 다음 문서 toohello를 참조 하십시오.

### <a name="get-started-with-managed-disks"></a>Managed Disks 시작

* [Resource Manager 및 PowerShell을 사용하여 VM 만들기](../virtual-machines/virtual-machines-windows-ps-create.md)

* [Hello Azure CLI 2.0을 사용 하 여 Linux VM 만들기](../virtual-machines/linux/quick-create-cli.md)

* [관리 되는 데이터 디스크 tooa Windows VM 연결 PowerShell을 사용 하 여](../virtual-machines/windows/attach-disk-ps.md)

* [관리 되는 디스크 tooa Linux VM 추가](../virtual-machines/linux/add-disk.md)

* [Managed Disks PowerShell 샘플 스크립트](https://github.com/Azure-Samples/managed-disks-powershell-getting-started)

* [Azure Resource Manager 템플릿에서 Managed Disks 사용](storage-using-managed-disks-template-deployments.md)

### <a name="compare-managed-disks-storage-options"></a>Managed Disks 저장소 옵션 비교

* [프리미엄 저장소 및 디스크](storage-premium-storage.md)

* [표준 저장소 및 디스크](storage-standard-storage.md)

### <a name="operational-guidance"></a>운영 가이드

* [Azure의 tooManaged 디스크 AWS 및 기타 플랫폼에서 마이그레이션](../virtual-machines/windows/on-prem-to-azure.md)

* [Azure에서 Azure Vm toomanaged 디스크 변환](../virtual-machines/windows/migrate-to-managed-disks.md)
