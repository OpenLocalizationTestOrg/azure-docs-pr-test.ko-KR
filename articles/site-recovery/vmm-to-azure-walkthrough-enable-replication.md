---
title: "Azure Site Recovery와 VMM의 Hyper-v Vm에 대 한 복제 tooAzure aaaEnable 클라우드 | Microsoft Docs"
description: "Hello Azure Site Recovery 서비스와 VMM의 Hyper-v Vm에 대 한 복제 tooAzure tooenable 클라우드 방법을 설명 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 89a2c4fc-7e03-4a86-a2c0-52831ccebc1a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 1a39bf65490c59a89a5e891184cadfacc2adee6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-11-enable-replication-tooazure-for-hyper-v-vms-in-vmm-clouds"></a>11 단계: 복제 tooAzure VMM 클라우드에서 Hyper-v Vm에 대 한 사용 하도록 설정

복제 정책을 설정한 후 복제를 사용이 문서 tooenable 온-프레미스 Hyper-v 가상 컴퓨터 (Vm)에 대 한 System Center Virtual Machine Manager (VMM) 클라우드에서 관리), hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md)hello Azure 포털의에서 서비스입니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="before-you-start"></a>시작하기 전에

Azure 계정에 올바른 hello 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines)toocreate Azure Vm입니다. Azure 역할 기반 액세스 제어에 대해 자세히 알아보려면 [여기](../active-directory/role-based-access-built-in-roles.md)를 참조하세요.

## <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. 디스크를 복제에서 제외할 수 있습니다. 예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다. [자세히 알아보기](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a>VM 복제

다음과 같이 VM에 대해 복제를 활성화합니다.  

1. **2단계: 응용 프로그램 복제** > **원본**을 클릭합니다. 처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 자격 증명 모음 tooenable 복제 hello에에서 있습니다.

    ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication1.png)
2. Hello에 **소스** 블레이드, 선택 hello VMM 서버 및 hello 클라우드는 hello Hyper-v 호스트는 배치 합니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-source.png)
3. **대상**hello 구독, 장애 조치 후 배포 모델을 선택 하 고 hello 저장소 계정에 복제 된 데이터를 사용 합니다.

    ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication-target.png)
4. 원하는 toouse hello 저장소 계정을 선택 합니다. Toouse 해야 하는 것 보다 다른 저장소 계정 키를 원하는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-storage-account)합니다. 프리미엄 저장소 계정 복제 된 데이터를 사용 하는 경우 필요한 tooselect를 가져갈 변화 들이 tooon 온-프레미스 data.toocreate hello 리소스 관리자 모델을 사용 하 여 저장소 계정을 캡처하는 추가 표준 저장소 계정을 toostore 복제 로그 클릭 **새로 만들기**합니다. Hello 일반 모델을 사용 하 여 저장소 계정을 toocreate을 원하는 경우 [hello Azure 포털에서에서](../storage/common/storage-create-storage-account.md)합니다. 그런 후 **OK**를 클릭합니다.
5. 장애 조치 후 처음 만들어질 때 선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm이 연결 됩니다. 선택 **선택한 컴퓨터에 지금 구성**, tooapply hello 네트워크 설정 tooall 선택한 컴퓨터에 대 한 보호 합니다. 선택 **나중에 구성**, tooselect hello 컴퓨터당 Azure 네트워크입니다. 다른 네트워크 toouse 하려는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-network)합니다. 사용 하 여 네트워크 toocreate hello 리소스 관리자 모델 클릭 **새로 만들기**합니다. Hello 일반 모델을 사용 하는 네트워크 toocreate을 원하는 경우 [hello Azure 포털에서에서](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다. 해당하는 경우 서브넷을 선택합니다. 그런 후 **OK**를 클릭합니다.
6. **가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다. 복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication5.png)

7. **속성** > **속성 구성**OS 디스크 hello을 hello 선택한 Vm에 대 한 hello 운영 체제를 선택 합니다.

    - 해당 hello Azure VM 이름 (대상 이름)을 준수 확인 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.   
    - 기본적으로 모든 hello 디스크 hello VM의 복제를 위해 선택 하지만 디스크 tooexclude 지울 수 있습니다 이러한.

        - Tooexclude 디스크 tooreduce 복제 대역폭을 할 수 있습니다. 예를 들어 임시 데이터로 tooreplicate 디스크 원하지 않을 수 있습니다 또는 (예: pagefile.sys 또는 Microsoft SQL Server tempdb)가 새로 고쳐질 때마다 컴퓨터나 응용 프로그램 데이터를 다시 시작 합니다. Hello 디스크 선택을 취소 하 여 hello 디스크 복제에서 제외할 수 있습니다.
        - 기본 디스크만 제외할 수 있습니다. OS 디스크는 제외할 수 없습니다.
        - 동적 디스크는 제외하지 않는 것이 좋습니다. Site Recovery는 게스트 VM 내의 가상 하드 디스크가 기본 디스크인지 아니면 동적 디스크인지 식별할 수 없습니다. 모든 종속 동적 볼륨 디스크 제외 되지 않으면 hello VM 장애 조치, 되 고 hello 해당 디스크에 액세스할 수 없게 하는 경우 실패 한 디스크 hello 보호 된 동적 디스크가 표시 됩니다.
        - 복제를 사용하도록 설정한 후 복제에 대해 디스크를 추가 또는 제거할 수 없습니다. Tooadd 원하는 디스크를 제외 하거나, hello VM toodisable 보호 해야 하 고 다시 설정 합니다.
        - Azure에서 수동으로 만드는 디스크는 장애 복구되지 않습니다. 예를 들어 세 디스크 실패 하 고 Azure VM에 직접 두 개 만든 경우 Azure tooHyper-V에서 다시 hello 세 디스크만 장애 조치 된 장애 됩니다. 장애 복구 또는 Hyper-v tooAzure에서 역방향 복제를 수동으로 만든 디스크를 포함할 수 없습니다.
        - 응용 프로그램 toooperate에 필요한 디스크를 제외 하면 후 장애 조치 tooAzure 해야 toocreate Azure 때문에 해당 hello 복제 응용 프로그램에서 수동으로 실행할 수 있습니다. 또는 Azure 자동화 hello 컴퓨터의 장애 조치 중 toocreate hello 디스크 복구 계획을 통합할 수 있습니다.

    클릭 **확인** toosave 변경 합니다. 나중에 추가 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

8. **복제 설정을** > **복제 설정을 구성**, hello Vm 보호 된 원하는 tooapply hello 복제 정책을 선택 합니다. 그런 후 **OK**를 클릭합니다. hello 복제 정책을 수정할 수 있습니다 **복제 정책** > 정책 이름 > **설정 편집**합니다. 적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.

   ![복제 활성화](./media/vmm-to-azure-walkthrough-enable-replication/enable-replication7.png)

Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **작업** > **사이트 복구 작업이**합니다. Hello 후 **보호 완료** hello 컴퓨터가 장애 조치에 대해 준비 되었는지, 작업을 실행 합니다.



## <a name="next-steps"></a>다음 단계

너무 이동[12 단계: 테스트 장애 조치 실행](vmm-to-azure-walkthrough-test-failover.md)
