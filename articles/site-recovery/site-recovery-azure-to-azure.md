---
title: "재해 복구 요구 사항에 대 한 Azure 지역 간에 Azure Vm을 복제: Azure tooAzure | Microsoft Docs"
description: "재해 복구 요구에 대 한 hello Azure Site Recovery 서비스와 Azure 지역 (Azure Azure) 간 tooreplicate Azure Vm을 해야 하는 hello 단계를 요약 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Azure Site Recovery를 사용하여 지역 간 Azure VM 복제

>[!NOTE]
>
> Azure VM(가상 컴퓨터)에 대한 Azure Site Recovery 복제는 현재 미리 보기로 제공됩니다.

이 문서에서 설명 하는 방법을 사용 하 여 Azure 지역 간에 Azure Vm tooreplicate hello [사이트 복구](site-recovery-overview.md) hello Azure 포털의에서 서비스입니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="disaster-recovery-in-azure"></a>Azure에서 재해 복구

기본 제공 Azure 인프라의 기능 및 특징 tooa 강력 하 고 복원 가용성 전략 Azure Vm에서 실행 되는 작업에 대 한 영향을 줍니다. 그러나이 필요한 이유 tooplan Azure 지역 간 재해 복구를 위해 사용자가 직접 여러 가지 이유가 있습니다.

- 특정 앱 및 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 필요로 하는 워크 로드에 대 한 규정 준수 지침 toomeet 해야 합니다.
- Hello 기능 tooprotect 한 기본 제공 된 Azure 기능에 따라 Azure Vm 및 뿐 아니라 비즈니스 결정 사항에 따라 복구 합니다.
- 비즈니스 및 규정 준수 요구 사항, 프로덕션에 영향에 따라 tootest 장애 조치 및 복구 해야 합니다.
- 뒤로 toohello 원래 소스 영역을 원활 하 게 실패 및 재해의 hello 이벤트에서 toohello 복구 지역의 toofail 해야 합니다.

사이트 복구를 사용 하 여 Azure에 Azure VM 복제 toohelp 이러한 작업을 모두 수행 합니다.


## <a name="why-use-site-recovery"></a>사이트 복구를 사용하는 이유는?      

사이트 복구 지역 간의 간단한 방법 tooreplicate Azure Vm 제공합니다.

- **자동 배포**. 액티브-액티브 복제 모델과 달리 hello 보조 지역에서 비용이 많이 들고 복잡 한 인프라에 대 한 않아도가 됩니다. 복제를 사용 하는 경우 사이트 복구 자동으로 만듭니다 hello 필요한 리소스 hello 대상 지역에 소스 지역 설정에 따라.
- **지역 제어**. 사이트 복구와 대륙 내에서 영역 tooany 영역에서 복제할 수 있습니다. 반면, 읽기 액세스 지역 중복 저장소는 표준 [쌍을 이루는 지역](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) 간에만 비동기식으로 복제합니다. 읽기 액세스 지역 중복 저장소는 hello 대상 지역에 읽기 전용 액세스 toohello 데이터를 제공합니다.
- **복제 자동화**. Site Recovery는 자동화된 연속 복제를 제공합니다. 한 번의 클릭으로 장애 조치 및 장애 복구를 트리거할 수 있습니다.
- **RTO 및 RPO**. 사이트 복구는 영역 tookeep를 연결 하는 hello Azure 네트워크 인프라를 활용 RTO 및 RPO 매우 부족 합니다.
- **테스트**. 프로덕션 워크로드 또는 진행 중인 복제에 영향을 주지 않고 필요할 때 주문형 테스트 장애 조치를 사용하여 재해 복구 드릴을 실행할 수 있습니다.
- **복구 계획**. 복구 계획 tooorchestrate 장애 조치 및 여러 Vm에서 실행 중인 hello 전체 응용 프로그램의 장애 복구를 사용할 수 있습니다. hello 복구 계획 기능에 Azure 자동화 runbook과 첫 번째 클래스 풍부한 통합 되었습니다.


## <a name="deployment-summary"></a>배포 요약

여기에 필요한 간략하게 Vm의 Azure 지역 간 복제를 toodo tooset:

1. Recovery Services 자격 증명 모음을 만듭니다. hello 자격 증명 모음 구성 설정을 포함 하 고 복제를 조정 합니다.
2. Hello Azure Vm에 대 한 복제를 사용 하도록 설정 합니다.
3. 테스트 장애 조치 toomake 모든 항목이 예상 대로 작동 하 고 있는지를 실행 합니다.

>[!IMPORTANT]
>
> Hello를 확인할 수 있습니다 [Azure VM 복제에 대 한 지원 매트릭스](./site-recovery-support-matrix-azure-to-azure.md)합니다.

>[!IMPORTANT]
>
> 어떻게 tooconfigure hello 네트워크 아웃 바운드 연결 Azure Vm에 대 한 복제에 필요한 사이트 복구에 대 한 내용은 hello 참조 [네트워킹 지침 문서](./site-recovery-azure-to-azure-networking-guidance.md)합니다.

### <a name="before-you-start"></a>시작하기 전에

* Azure 사용자 계정에 필요한 toohave 특정 [권한을](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable Azure 가상 컴퓨터를 복제 합니다.
* Azure 구독 사용된 toocreate Vm toouse hello 재해 복구 영역으로 원하는 hello 대상 위치에 있어야 합니다. 고객 지원으로 문의 tooenable hello 필요한 할당량입니다.

## <a name="create-a-recovery-services-vault"></a>복구 서비스 자격 증명 모음 만들기

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Vm tooreplicate 저장할 hello 위치에서 hello 복구 서비스 자격 증명 모음을 만드는 것이 좋습니다. 예를 들어 대상 위치는 hello 중앙 미국, 만들에서 자격 증명 모음의 hello **중미**합니다.

## <a name="enable-replication"></a>복제 활성화

**복구 서비스 자격 증명 모음**, hello 자격 증명 모음 이름을 클릭 합니다. Hello 자격 증명 모음에서 클릭 hello **복제 +** 단추입니다.

### <a name="step-1-configure-hello-source"></a>1단계. Hello 소스 구성
1. **원본**에서 **Azure - 미리 보기**를 선택합니다.
2. **소스 위치**선택, hello 소스 Vm에 현재 실행 중인 Azure 지역입니다.
3. Vm의 배포 모델 선택 hello: **리소스 관리자** 또는 **클래식**합니다.
4. 선택 hello **원본 리소스 그룹** 리소스 관리자 Vm에 대 한 또는 **클라우드 서비스** 클래식 Vm에 대 한 합니다.

    ![Hello 소스 구성](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>2단계. 가상 컴퓨터 선택

* 선택한 hello Vm tooreplicate을 차례로 클릭 **확인**합니다.

    ![VM 선택](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>3단계. 설정 구성

1. toooverride hello 기본 설정 대상으로 하 고 hello 설정을 지정의 선택한 클릭 **사용자 지정**합니다. 자세한 내용은 [대상 리소스 사용자 지정](site-recovery-replicate-azure-to-azure.md##customize-target-resources)을 참조하세요.

    ![설정 구성](./media/site-recovery-azure-to-azure/settings.png)


2. 기본적으로 Site Recovery는 4시간마다 앱 일치 스냅숏을 만들고 24시간 동안 복구 지점을 유지하는 복제 정책을 만듭니다. 다른 설정으로 정책 toocreate 클릭 **사용자 지정** 다음 너무**복제 정책**합니다.

    ![정책 사용자 지정](./media/site-recovery-azure-to-azure/customize-policy.png)

3. hello target 리소스를 프로 비전 toostart 클릭 **대상 리소스 만들기**합니다. 프로비전에 1분 정도 걸립니다. 프로 비전 하는 동안 hello 블레이드를 닫지 마십시오 또는 통한 toostart 필요 합니다.

4. hello tootrigger 복제 VM을 선택, 클릭 **복제 사용**합니다.

5. Hello의 진행률을 추적할 수 있습니다 **보호 기능을 활성화** 작업 **설정** > **작업** > **사이트 복구 작업이**.

6. **설정** > **복제 항목**, Vm의 hello 상태를 볼 수 있으며 hello 초기 복제 진행 중입니다. Hello VM toodrill 해당 설정을 클릭 합니다.

## <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행

모든 항목을 설정한 후에 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

1. 단일 컴퓨터를 통해 toofail에서 **설정** > **복제 항목**, hello VM을 클릭 **+ 테스트 장애 조치** 아이콘.

2. 복구를 통해 toofail 계획 **설정** > **복구 계획**를 마우스 오른쪽 단추로 클릭 hello 계획 **테스트 장애 조치**합니다. 복구 계획 toocreate [다음이 지침에 따라](site-recovery-create-recovery-plans.md)합니다. 

3. **테스트 장애 조치**선택, hello 대상 Azure 가상 네트워크 toowhich Azure Vm hello 장애 조치가 발생 한 후에 연결 되어 있습니다.

4. toostart hello 장애 조치를 클릭 **확인**합니다. tootrack 진행 되는 hello VM tooopen 해당 속성을 클릭 합니다. Hello 클릭할 **테스트 장애 조치** hello 자격 증명 모음 이름에는 작업 > **설정** > **작업** > **사이트복구작업**.

5. Hello 후 장애 조치 완료 되 면 hello 복제본 Azure 컴퓨터 hello Azure 포털에에서 표시 > **가상 컴퓨터**합니다. 해당 hello VM 실행 되 고 toohello 적절 한 네트워크 연결 된 hello 적절 한 크기 인지 확인 합니다.

6. toodelete hello hello 테스트 장애 조치 중에 만든 Vm 클릭 **테스트 장애 조치 정리** hello에서 항목 또는 hello 복구 계획을 복제 합니다. **노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다. 

테스트 장애 조치(failover)에 대해 [자세히 알아보세요](site-recovery-test-failover-to-azure.md).


## <a name="next-steps"></a>다음 단계

한 후 hello 배포를 테스트 합니다.

- [자세한 내용은](site-recovery-failover.md) 다양 한 유형의 장애 조치를 수행 하는 방법에 대 한 방법과 toorun 해당 합니다.
- 에 대 한 자세한 내용은 [복구 계획을 사용 하 여](site-recovery-create-recovery-plans.md) tooreduce RTO 합니다.
