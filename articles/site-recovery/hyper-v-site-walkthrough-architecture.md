---
title: "Azure 사이트 복구와 Hyper-v 복제 (System Center VMM) 없이 tooAzure aaaReview hello 아키텍처 | Microsoft Docs"
description: "이 문서에서는 구성 요소와 hello Azure Site Recovery 서비스와 온-프레미스 Hyper-v Vm (VMM 없음) tooAzure 복제할 때 사용 되는 아키텍처의 개요를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: ec148e87ab2fa17485001ee447ad9f9bf795840e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-hyper-v-replication-tooazure"></a>1 단계: Hyper-v 복제 tooAzure에 대 한 hello 아키텍처를 검토 합니다.


이 문서에서는 hello 구성 요소를 설명 및 복제 하는 경우 관련 된 프로세스 온-프레미스 Hyper-v 가상 컴퓨터 (System Center VMM에서 관리 되지 않는), tooAzure hello를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

Hello 또는이 문서의 hello 맨 아래에 모든 메모를 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



## <a name="architectural-components"></a>아키텍처 구성 요소

여러 가지가 구성 요소와 관련 된 VMM 없이 tooAzure Hyper-v Vm을 복제 하는 경우입니다.

**구성 요소** | **위치** | **세부 정보**
--- | --- | ---
**Azure** | Azure에서는 Microsoft Azure 계정, Azure Storage 계정 및 Azure 네트워크가 필요합니다. | 복제 된 데이터는 hello 저장소 계정에 저장 하 고 Azure Vm이 온-프레미스 사이트에서 장애 조치 발생 시 hello 복제 된 데이터와 함께 만들어집니다.<br/><br/> Azure Vm hello 처음 만들어질 때 toohello Azure 가상 네트워크를 연결 합니다.
**Hyper-V** | Hyper-V 호스트 및 클러스터는 Hyper-V 사이트에 수집됩니다. hello Azure Site Recovery Provider 및 복구 서비스 에이전트는 각 Hyper-v 호스트에 설치 됩니다. | hello 통해 Site Recovery와 복제를 조정 하는 hello 공급자 인터넷 합니다. hello 복구 서비스 에이전트는 복제 데이터를 처리합니다.<br/><br/> Hello 공급자 및 hello 에이전트 모두의 통신을 안전 하 고 암호화 됩니다. Azure 저장소에 복제된 데이터도 암호화됩니다.
**Hyper-V VM** | Hyper-V 호스트 서버에서 실행되는 하나 이상의 VM이 필요합니다. | Vm에 설치 된 tooexplicitly가 필요 없습니다.

Hello 배포 필수 구성 요소 및 각 hello에서 이러한 구성 요소에 대 한 요구 사항을 알아봅니다 [지원 매트릭스](site-recovery-support-matrix-to-azure.md)합니다.

**그림 1: 하이퍼-V 사이트 tooAzure 복제**

![구성 요소](./media/hyper-v-site-walkthrough-architecture/arch-onprem-azure-hypervsite.png)


## <a name="replication-process"></a>복제 프로세스

**Hyper-v 복제 tooAzure에 대 한 그림 2: 복제 및 복구 프로세스**

![워크플로](./media/hyper-v-site-walkthrough-architecture/arch-hyperv-azure-workflow.png)

### <a name="enable-protection"></a>보호 사용

1. Hyper-v VM에 대 한 보호를 사용 하도록 설정한 후 hello에 Azure 포털 또는 온-프레미스, hello **보호 사용** 시작 합니다.
2. hello 작업 확인 hello를 호출 하기 전에 해당 hello 컴퓨터 필수 구성 요소를 준수 [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)를 구성 하는 hello 설정 사용 하 여 복제를 tooset 합니다.
3. hello 작업이 hello를 호출 하 여 초기 복제 시작 [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) 메서드와 tooinitialize 전체 VM 복제를 송신 hello VM의 가상 디스크 tooAzure 합니다.
4. Hello에 hello 작업을 모니터링할 수 있습니다 **작업** 탭 합니다.
 
### <a name="replicate-hello-initial-data"></a>Hello 초기 데이터 복제

1. 초기 복제가 트리거될 때 [Hyper-V VM 스냅숏](https://technet.microsoft.com/library/dd560637.aspx)이 만들어집니다.
2. 가상 하드 디스크 모두 복사한 tooAzure 하기가 하나씩 복제 됩니다. Hello VM 크기에 따라 시간이 오래 걸릴 하 고 네트워크 대역폭을 수 있습니다. toooptimize 네트워크 사용을 참조 [어떻게 toomanage 온-프레미스 tooAzure 보호 네트워크 대역폭 사용량](https://support.microsoft.com/kb/3056159)합니다.
3. 초기 복제가 진행 중인 동안 디스크 변경 내용이 발생 한 경우 Hyper-v 복제본 복제 추적기 hello Hyper-v 복제 로그 (.hrl)으로 변경 된 내용을 추적 합니다. 이러한 파일은 hello hello 디스크와 같은 폴더입니다. 각 디스크 toosecondary 저장소를 전송 하는 관련된.hrl 파일을 있습니다.
4. 초기 복제가 진행 중인 동안 hello 스냅숏 및 로그 파일에서 디스크 리소스를 소비 합니다.
5. Hello 초기 복제가 완료 되 면 hello VM 스냅숏이 삭제 됩니다. 델타 디스크 hello 로그에 변경은 동기화 되거나 병합 된 toohello 부모 디스크입니다.


### <a name="finalize-protection"></a>보호 완료

1. Hello 초기 복제가 완료 되 면 hello **hello 가상 컴퓨터에 대 한 보호 완료** hello 가상 컴퓨터가 보호 되 고 있도록 작업 네트워크 및 기타 복제 후 설정을 구성 합니다.
2. TooAzure를 복제 하는 경우 장애 조치에 대해 준비 되도록 hello 가상 컴퓨터에 대 한 tootweak hello 설정을 할 수 있습니다. 이 시점에서 모든 것이 예상 대로 작동 하는 테스트 장애 조치 toocheck를 실행할 수 있습니다.

### <a name="replicate-hello-delta"></a>Hello 델타 복제

1. Hello 초기 복제 후 델타 동기화가 시작 되, 복제 설정에 따라 합니다.
2. Hyper-v 복제본 복제 추적기 hello.hrl 파일로 hello 변경 tooa 가상 하드 디스크를 추적합니다. 복제를 위해 구성된 각 디스크에는 연결된 .hrl 파일이 있습니다. 초기 복제가 완료 된 후이 로그 toohello 고객 저장소 계정을 보내집니다. 주 디스크 hello hello 변경 내용을 hello에 다른 로그 파일에서 추적 로그 전송 tooAzure 이면 동일한 디렉터리입니다.
3. 초기 및 델타 복제 하는 동안 VM 보기 hello에 VM hello를 모니터링할 수 있습니다. [자세히 알아봅니다](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="synchronize-replication"></a>복제 동기화

1. 델타 복제에 실패했고 전체 복제에는 대역폭이나 시간이 많이 소모될 경우 VM에서 다시 동기화가 발생합니다. 예를 들어 hello.hrl 파일이 hello 디스크 크기의 50%에 도달 하는 경우 다음 hello VM 표시될지 다시 동기화에 대 한 합니다.
2.  다시 동기화 hello hello 소스 및 대상 가상 컴퓨터의 체크섬을 계산 하 고만 hello 델타 데이터를 보내는 여 보내지는 데이터 양을 최소화 합니다. 다시 동기화는 고정 블록 청크 알고리즘을 사용하며 이 경우 원본 및 대상 파일이 고정 청크로 나누어집니다. 각 청크에 대 한 체크섬 생성 되 고 hello 소스 필요 toobe 적용 된 toohello 대상에서 차단 되 toodetermine와 비교 합니다.
3. 다시 동기화를 마치면 일반 델타 복제가 다시 시작됩니다. 기본적으로 다시 동기화가 자동으로 근무 시간 외부 예약된 toorun 하지만 수동으로 가상 컴퓨터를 동기화 할 수 있습니다. 예를 들어 네트워크 중단 또는 다른 중단이 발생하면 다시 동기화를 다시 시작할 수 있습니다. toodo hello 포털에서이 선택 hello VM > **다시 동기화**합니다.

    ![수동 다시 동기화](./media/hyper-v-site-walkthrough-architecture/image4.png)


### <a name="retry-logic"></a>재시도 논리

복제 오류가 발생한 경우 기본 제공 재시도가 있습니다. 이 논리는 두 가지 범주로 분류할 수 있습니다.

**범주** | **세부 정보**
--- | ---
**복구할 수 없는 오류** | 재시도가 수행되지 않습니다. VM 상태가 **위험**으로 표시되고 관리자 개입이 필요합니다. 이러한 오류의 예로: VHD 체인; 분할 Hello 복제본 VM;에 대 한 잘못 된 상태 네트워크 인증 오류: 권한 부여 오류; VM (독립 실행형 Hyper-v 서버)에 대 한 오류를 찾을 수 없습니다
**복구할 수 있는 오류** | 다시 시도 횟수는 지 수 백오프 hello 다시 시도 간격에서 시작 하 여 1, 2, 4, 8, 첫 번째 시도 hello hello 및 10 분 증가 하는 사용 하 여 복제 간격 마다 발생 합니다. 오류가 계속되면 30분마다 다시 시도하십시오. 이러한 예로는 네트워크 오류, 디스크 공간 부족, 메모리 부족 상태가 있습니다. |



## <a name="failover-and-failback-process"></a>장애 조치 및 장애 복구 프로세스

1. 계획을 실행할 수 있습니다 또는 계획 되지 않은 [장애 조치](site-recovery-failover.md) 온-프레미스 Hyper-v Vm tooAzure에서 합니다. 경우 계획된 된 장애 조치를 실행 한 후 원본 Vm이 tooensure 종료 데이터가 손실 되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md) tooorchestrate 여러 컴퓨터를 장애 조치 합니다.
4. Hello 장애 조치를 실행 한 후에 Azure에서 복제본 Vm을 만든 수 toosee hello 있어야 합니다. 필요한 경우 공용 IP 주소 toohello VM을 할당할 수 있습니다.
5. 그런 다음 hello 복제 Azure VM에서에서 hello 작업에 액세스 하는 hello 장애 조치 toostart를 커밋합니다.
6. 기본 온-프레미스 사이트를 다시 사용할 수 있는 경우 [장애 복구](site-recovery-failback-from-azure-to-hyper-v.md)를 수행할 수 있습니다. 하면 Azure toohello 기본 사이트에서 계획된 된 장애 조치를 시작 합니다. 계획 된 장애 조치를 수행할 수 있습니다 선택 toofailback toohello 동일한 VM 또는 tooan 대체 위치를 하 고 동기화 사이 변경 Azure 및 온-프레미스, tooensure 데이터가 손실 되지 않습니다. Vm에서 온-프레미스를 만든 경우 hello 장애 조치를 커밋합니다.




## <a name="next-steps"></a>다음 단계

너무 이동[2 단계: hello 배포 필수 구성 요소를 검토 합니다.](hyper-v-site-walkthrough-prerequisites.md)
