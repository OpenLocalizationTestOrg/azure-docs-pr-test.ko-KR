---
title: "Hyper-v (System Center VMM) 없이 복제 tooAzure에 대 한 테스트 장애 조치 aaaRun | Microsoft Docs"
description: "Hyper-v Vm tooAzure hello Azure Site Recovery 서비스를 사용 하 여 복제에 대 한 테스트 장애 조치를 실행 하는 데 필요한 hello 단계를 요약 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c9a4c3ca-84a0-4668-b700-9b0046202299
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: dbcca080a8fa139e2ea0d132323101dd0f7cd265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-run-a-test-failover-for-hyper-v-replication-tooazure"></a>11 단계: Hyper-v 복제 tooAzure에 대 한 테스트 장애 조치 실행

이 문서에서는 어떻게 toorun 테스트 장애 조치에서 온-프레미스 Hyper-v 가상 컴퓨터 (System Center VMM에서 관리 하지) 설명 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 서비스.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="before-you-start"></a>시작하기 전에

Hello VM 속성을 확인 하 고 변경 하는 것을 권장 하는 테스트 장애 조치를 실행 하기 전에 해야 합니다. hello VM 속성에 액세스할 수 있습니다 **복제 항목**합니다. hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.

## <a name="managed-disk-considerations"></a>Managed Disk 고려 사항

[관리 디스크](../virtual-machines/windows/managed-disks-overview.md) hello VM 디스크와 연결 된 hello 저장소 계정을 관리 하 여 Azure Vm에 대 한 디스크 관리를 단순화 합니다. 

- 관리 되는 디스크에 생성 되 고 장애 조치 tooAzure 발생 toohello VM 연결. 보호를 사용 하면 온-프레미스 Vm에서 데이터 toostorage 계정을 복제 됩니다.
- Hello 리소스 관리자 배포 모델을 사용 하 여 배포 된 Vm에 대해서만 관리 하는 디스크를 만들 수 있습니다.
- 장애 복구 tooan Azure에서 온-프레미스 Hyper-v 환경을 관리 하는 디스크를 사용 하 여 컴퓨터에 대 한 현재 지원 되지 않습니다. 설정 해야 **관리 되는 디스크 사용** 너무**예** 는 마이그레이션만 (장애 조치 tooAzure 장애 복구 하지 않고)을 수행 하는 경우
- 이 설정을 사용하면, **관리 디스크 사용**을 활성화한 리소스 그룹의 가용성 집합만 선택할 수 있습니다. 가용성 집합에 관리 되는 디스크와 Vm 있어야 **관리 되는 디스크 사용** 도**예**합니다. Vm에 대 한 hello 설정을 활성화 하지 않으면 가용성 집합에만 리소스 그룹에 사용 하도록 설정 하는 관리 되는 디스크 없이 선택할 수 있습니다. [자세히 알아봅니다](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).
- - 복제를 위해 사용할 hello 저장소 계정의 저장소 서비스 암호화로 암호화 된, 하는 경우 장애 조치 중 관리 되는 디스크를 만들 수 없습니다. 이 경우 관리 되는 디스크의 사용을 활성화 하 고 또는 VM hello에 대 한 보호를 사용 하지 않도록 설정 하 고, toouse 없는 경우 암호화를 사용 하는 저장소 계정을 다시 설정 하지 않는 하나. [자세히 알아봅니다](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).

 
## <a name="network-considerations"></a>네트워크 고려 사항
    
- 장애 조치 후 hello Azure VM에도 사용 하는 hello 대상 IP 주소 toobe를 설정할 수 있습니다. 주소를 제공 하지 않으면 장애 조치 컴퓨터 hello DHCP를 사용 합니다. 장애 조치에 사용할 수 없는 주소를 설정 하는 경우 hello 장애 조치가 실패 합니다. hello hello 주소는 hello 테스트 장애 조치 네트워크에서 사용할 수 있는 하는 경우 테스트 장애 조치에 대해 동일한 대상 IP 주소를 사용할 수 있습니다.
- 네트워크 어댑터의 hello 수는 다음과 같이 hello 대상 가상 컴퓨터에 대해 지정 하는 hello 크기에 따라 결정 됩니다.
    - Hello hello 원본 컴퓨터의 네트워크 어댑터 수가 보다 작거나 같은 경우 hello 대상 컴퓨터 크기에 허용 되는 어댑터 수가 toohello 다음 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
    - Hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수를 초과 하면 hello 수 수 hello 대상 크기 다음 hello 대상 크기는 최대 사용 됩니다.
    - 예를 들어 원본 컴퓨터에 네트워크 어댑터가 두 개 및 4 hello 대상 컴퓨터 크기 지원로 hello 대상 컴퓨터는 두 개의 어댑터를 포함 합니다. Hello 원본 컴퓨터에 두 개의 어댑터가 있지만 hello 지원 되는 대상 크기 하나만 지원 하는 경우 hello 대상 컴퓨터에서 하나의 어댑터를 해야 합니다.     
- Hello VM에 여러 네트워크 어댑터는 모든 연결 toohello 동일한 네트워크입니다.
- Hello 가상 컴퓨터에 여러 네트워크 어댑터가 다음 hello 경우 먼저 하나 hello 목록에 표시 될 hello *기본* hello Azure 가상 컴퓨터의에서 네트워크 어댑터입니다.


## <a name="view-and-manage-vm-settings"></a>VM 설정 보기 및 관리

장애 조치를 실행 하기 전에 hello 원본 컴퓨터의 hello 속성을 확인 하는 것이 좋습니다.

1. **보호 된 항목**, 클릭 **복제 항목**, hello VM을 클릭 합니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-test-failover/test-failover1.png)
2. Hello에 **복제 된 항목** 창 VM 정보, 상태 상태 및 hello 최신 사용 가능한 복구 지점은 요약을 볼 수 있습니다. 클릭 **속성** tooview 더 자세히 설명 합니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-test-failover/test-failover2.png)
3. **계산 및 네트워크**에서 다음을 수행할 수 있습니다.
    - Hello Azure VM 이름을 수정 합니다. hello 이름은 만족 해야 합니다 [Azure 요구 사항](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
    - 장애 조치(failover) 후 [리소스 그룹]을 지정합니다.
    - Hello Azure VM에 대 한 대상 크기를 지정 합니다.
    - [가용성 집합](../virtual-machines/windows/tutorial-availability-sets.md)을 선택합니다.
    - 지정 여부 toouse [관리 디스크](#managed-disk-considerations)합니다. 선택 **예**tooattach 마이그레이션 tooAzure에 tooyour 컴퓨터를 관리 하는 디스크를 하려는 경우.
    - 보거나 hello 네트워크/서브넷이 있는 hello에 Azure VM 배치 될 장애 조치 후 및 할당할 tooit hello IP 주소 등의 네트워크 설정을 수정 합니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-test-failover/test-failover4.png)
4. **디스크**및 hello 운영 체제에 대 한 정보를 확인할 수 있습니다에 데이터 디스크 VM hello 합니다.


## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행

이제 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

- Tooconnect tooAzure Vm을 원하는 경우 RDP를 사용 하 여 장애 조치 후 [tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)합니다.
 - 테스트 환경에서 Active Directory 및 DNS toocopy 필요한 toofully 테스트 합니다. [자세히 알아봅니다](site-recovery-active-directory.md#test-failover-considerations).
 - 테스트 장애 조치(failover)에 대한 전체 정보는 [이 문서](site-recovery-test-failover-to-azure.md)를 읽어보세요.
 
 이제 장애 조치(failover)를 실행합니다.

1. 단일 컴퓨터를 통해 toofail에서 **복제 항목**, hello VM을 클릭 > **+ 테스트 장애 조치** 아이콘입니다.
2. 복구를 통해 toofail 계획 **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 > **테스트 장애 조치**합니다. 복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다.
3. **테스트 장애 조치**선택, 장애 조치 발생 후 hello Azure 네트워크 toowhich Azure Vm 연결 됩니다.
4. 클릭 **확인** toobegin hello 장애 조치 합니다. Hello 또는 hello VM tooopen에 해당 속성을 클릭 하 여 진행률을 추적할 수 **테스트 장애 조치** 자격 증명 모음 이름에는 작업 > **작업** > **사이트 복구 작업이**합니다.
5. Hello 장애 조치가 끝나면도 있어야 toosee hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 해야 합니다.
6. 연결에 대 한 장애 조치 후 준비 수 tooconnect toohello Azure VM이 있어야 합니다.
7. 를 완료 한 후 클릭 **테스트 장애 조치 정리** hello 복구 계획에 있습니다. **노트** 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 테스트 장애 조치 중에 생성 된 hello 가상 컴퓨터를 삭제 합니다.



## <a name="next-steps"></a>다음 단계

- [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.
- [장애 복구에 대해 알아보세요](site-recovery-failback-from-azure-to-hyper-v.md), 복제 Azure Vm 및 toofail 다시 toohello 기본 온-프레미스 Hyper-v 사이트를 백업 합니다.

