---
title: "Hyper-v Vm (System Center VMM) 없이 Azure Site Recovery와 tooAzure 복제에 대 한 복제 aaaEnable | Microsoft Docs"
description: "Tooenable 복제 tooAzure hello Azure Site Recovery 서비스를 사용 하 여 Hyper-v Vm에 필요한 hello 단계가 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a>10 단계: Hyper-v Vm tooAzure 복제에 대 한 복제를 사용 하도록 설정


이 문서에서는 방법에 대 한 복제 tooenable 온-프레미스 Hyper-v 가상 컴퓨터 (System Center VMM에서 관리 하지)를 설명 hello를 사용 하 여 tooAzure [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 서비스.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.




## <a name="before-you-start"></a>시작하기 전에

시작 하기 전에 Azure 사용자 계정에 필요한 hello에 있는지 확인 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) 새 가상 컴퓨터 tooAzure의 tooenable 복제 합니다.

## <a name="exclude-disks-from-replication"></a>복제에서 디스크 제외

기본적으로 컴퓨터의 모든 디스크가 복제됩니다. 디스크를 복제에서 제외할 수 있습니다. 예를 들어 임시 데이터, 또는 새로 고쳐지는 데이터 때마다 컴퓨터 tooreplicate 디스크 원하지 않을 수 있습니다 또는 응용 프로그램 (예: pagefile.sys 또는 SQL Server tempdb)를 다시 시작 합니다. [자세히 알아보기](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a>VM 복제

다음과 같이 VM에 대해 복제를 활성화합니다.          

1. **응용 프로그램 복제** > **원본**을 클릭합니다. 처음으로 hello에 대 한 복제를 설정한 후 클릭 **복제 +** 추가 컴퓨터에 대 한 tooenable 복제 합니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. **소스**선택, hello 하이퍼-V 사이트입니다. 그런 후 **OK**를 클릭합니다.
3. **대상**hello toouse Azure (기본 또는 리소스 관리)에서 장애 조치 후 원하는 장애 조치 모델을 hello 자격 증명 모음 구독을 선택 합니다.
4. 원하는 toouse hello 저장소 계정을 선택 합니다. Toouse 원하는 계정을 없는 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-storage-account)합니다. 그런 후 **OK**를 클릭합니다.
5. 선택 hello Azure 네트워크와 서브넷 toowhich Azure Vm 장애 조치 만들 때 연결 됩니다.

    - tooapply hello 네트워크 설정을 tooall 컴퓨터 사용 하도록 설정 하면 복제를 위해 선택 **선택한 컴퓨터에 지금 구성**합니다.
    - 선택 **나중에 구성** tooselect hello 컴퓨터당 Azure 네트워크입니다.
    - Toouse 원하는 네트워크를 설정 하지 않은 경우 다음을 할 수 있습니다 [만드세요](#set-up-an-azure-network)합니다. 해당하는 경우 서브넷을 선택합니다. 그런 후 **OK**를 클릭합니다.

   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. **가상 컴퓨터** > **가상 컴퓨터 선택**, 클릭 하 고 tooreplicate 사용할 각 컴퓨터를 선택 합니다. 복제를 활성화할 수 있는 컴퓨터만 선택할 수 있습니다. 그런 후 **OK**를 클릭합니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. **속성** > **속성 구성**OS 디스크 hello을 hello 선택한 Vm에 대 한 hello 운영 체제를 선택 합니다.
8. 해당 hello Azure VM 이름 (대상 이름)을 준수 확인 [Azure 가상 컴퓨터 요구 사항을](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.
9. 기본적으로 모든 hello 디스크 hello VM의 복제를 위해 선택 됩니다. 일반 디스크 tooexclude 해당 합니다.
10. 클릭 **확인** toosave 변경 합니다. 나중에 추가 속성을 설정할 수 있습니다.

    ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. **복제 설정을** > **복제 설정을 구성**, hello Vm 보호 된 원하는 tooapply hello 복제 정책을 선택 합니다. 그런 후 **OK**를 클릭합니다. hello 복제 정책을 수정할 수 있습니다 **복제 정책** > 정책 이름 > **설정 편집**합니다. 적용하는 변경 사항은 이미 복제 중인 컴퓨터와 새 컴퓨터에 사용됩니다.


   ![복제 활성화](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

Hello의 진행률을 추적할 수 있습니다 **보호 사용** 작업 **작업** > **사이트 복구 작업이**합니다. Hello 후 **보호 완료** 실행 작업 hello 컴퓨터는 장애 조치에 대해 준비 합니다.


## <a name="next-steps"></a>다음 단계


너무 이동[11 단계: 테스트 장애 조치 실행](hyper-v-site-walkthrough-test-failover.md)
