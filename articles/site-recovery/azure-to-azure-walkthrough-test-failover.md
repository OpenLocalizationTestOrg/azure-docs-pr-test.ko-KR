---
title: "Azure Site Recovery와 Azure VM 복제에 대 한 테스트 장애 조치 aaaRun | Microsoft Docs"
description: "필요한 Azure Vm 복제 tooanother Azure 지역을 사용 하 여 Azure Site Recovery를 hello에 대 한 테스트 장애 조치를 실행 하기 위한 서비스는 hello 단계를 요약 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>6단계: Azure VM 복제를 위한 테스트 장애 조치 실행

Azure 가상 컴퓨터 (Vm)에 대 한 복제를 사용 하도록 설정한 후이 문서에서는 Azure 지역 tooanother, hello를 사용 하 여에서 toorun 테스트 장애 조치 hello 단계에 따라 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

- Hello 문서를 완료 하면 해야 확인 했습니다 테스트 장애 조치 있는 Azure VM을 하나 이상 tooyour 보조 Azure 지역 조치 실패할 수 있습니다. 
- 이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> Azure VM 복제는 현재 미리 보기로 제공됩니다.


## <a name="before-you-start"></a>시작하기 전에

- 테스트 장애 조치를 실행 하기 전에 hello VM 속성을 확인 해야 할 변경 하는 것이 좋습니다. hello VM 속성에 액세스할 수 있습니다 **복제 항목**합니다. hello **Essentials** 블레이드 컴퓨터 설정 및 상태에 대 한 정보를 표시 합니다.
- Hello 테스트 장애 조치 및 hello 네트워크가 아니라 별도 Azure VM 네트워크를 사용 하는 것이 좋습니다 (기본 또는 사용자 지정) 프로덕션 장애 조치에 대해 설정 되었습니다.
- hello 테스트 장애 조치 Azure Vm (및 해당 저장소)를 통해 실패 toohello 보조 Azure 지역입니다. 종속된 앱이나 리소스는 복제하지 않습니다. 실행 되는 앱 실패 한 Vm을 통해 DNS, Active Directory 등의 다른 리소스에 종속 된 경우 필요한 tooreplicate 이러한도 있지 않는 경우 이미 사용할 수 있는 보조 지역의 합니다. [자세히 알아보기](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- 너무 필요한 tooaccess 온-프레미스 사이트에서 장애 조치 후 Vm을 복제 하려면[tooconnect 준비](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese Vm입니다.

## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행

1. **설정** > **복제 항목**, VM hello 클릭 **+ 테스트 장애 조치** 아이콘입니다. 

2. **테스트 장애 조치**를 hello 장애 조치에 대 한 복구 지점 toouse 선택:

    - **최신 처리**: 실패 hello Site Recovery 서비스에서 처리 된 toohello 최신 복구 지점을 통해 VM hello 합니다. hello 타임 스탬프가 표시 됩니다. 이 옵션을 사용하면 데이터를 처리하는 데 시간을 소비하지 않으므로 낮은 RTO(복구 시간 목표)가 제공됩니다.
    - **최신 응용 프로그램에 일관 된**:이 옵션 모든 Vm toohello 최신 응용 프로그램 일치 복구 지점으로 장애 조치 합니다. hello 타임 스탬프가 표시 됩니다. 
    - **사용자 지정**: 복구 지점을 선택합니다.
 
3. Hello 장애 조치가 발생 한 후 선택 hello 대상 Azure 가상 네트워크 toowhich hello 보조 지역에서 Azure Vm 연결 됩니다.
4. toostart hello 장애 조치를 클릭 **확인**합니다. tootrack 진행 되는 hello VM tooopen 해당 속성을 클릭 합니다. 또는 hello를 클릭할 수 **테스트 장애 조치** hello 자격 증명 모음 이름에는 작업 > **설정** > **작업** > **사이트복구작업**.
5. Hello 후 장애 조치 완료 되 면 hello 복제 Azure VM hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 합니다.
6. toodelete hello hello 테스트 장애 조치 중에 만든 Vm 클릭 **테스트 장애 조치 정리** hello에서 항목 또는 hello 복구 계획을 복제 합니다. **노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 

테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).

## <a name="next-steps"></a>다음 단계

장애 조치를 테스트한 후에 이 연습이 완료되었습니다. 이제 프로덕션에서 장애 조치를 실행하는 방법을 자세히 알아봅니다.

- [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치에 대 한 방법과 toorun 해당 합니다.
- [복구 계획을 사용](site-recovery-create-recovery-plans.md)하여 여러 VM을 장애 조치하는 방법을 자세히 알아봅니다.
- [복구 계획 사용](site-recovery-create-recovery-plans.md)을 자세히 알아봅니다.
- 장애 조치(failover) 후에 [Azure VM을 다시 보호](site-recovery-how-to-reprotect.md)하는 방법에 대해 자세히 알아보세요.

