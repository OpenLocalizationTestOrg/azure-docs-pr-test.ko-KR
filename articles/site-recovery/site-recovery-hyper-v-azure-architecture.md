---
title: "사이트 복구에서 Hyper-v 복제 tooAzure 작업을 수행 하는 aaaHow? | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery에서 Hyper-V 복제가 어떻게 작동하는지에 대한 개요를 제공합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-architecture-hyper-v-to-azure
ms.openlocfilehash: e982806b4d6cdec2f71f82d8c73c17cc50ad3c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-hyper-v-replication-tooazure-work"></a>Hyper-v 복제 tooAzure 어떻게 작동 합니까?

이 문서 toounderstand hello 아키텍처 및 Hyper-v 복제 tooAzure hello를 사용 하 여에 대 한 워크플로 읽은 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

Hello 또는이 문서의 hello 맨 아래에 모든 메모를 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

Hello tooAzure 다음 복제할 수 있습니다.
- **Hyper-V(VMM 포함)**: System Center VMM(Virtual Machine Manager) 클라우드에서 관리되는 온-프레미스 Hyper-V 호스트에 있는 VM. [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)에서 실행할 수 있는 호스트. [Hyper-V 및 Azure에서 지원하는](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) 게스트 운영 체제를 실행하는 Hyper-V VM을 복제할 수 있습니다.
- **Hyper-V(VMM 없음)**: VMM 클라우드에서 관리되지 않는 Hyper-V 호스트에 있는 온-프레미스 VM. 호스트에 hello를 실행할 수 [지원 되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)합니다. [Hyper-V 및 Azure에서 지원하는](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) 게스트 운영 체제를 실행하는 Hyper-V VM을 복제할 수 있습니다.


## <a name="architectural-components"></a>아키텍처 구성 요소

**영역** | **구성 요소** | **세부 정보**
--- | --- | ---
**Azure** | Azure에서는 Microsoft Azure 계정, Azure Storage 계정 및 Azure 네트워크가 필요합니다. | 저장소 및 네트워크는 Resource Manager 기반 계정 또는 기존 계정일 수 있습니다.<br/><br/> 복제 된 데이터는 hello 저장소 계정에 저장 하 고 Azure Vm이 온-프레미스 사이트에서 장애 조치 발생 시 hello 복제 된 데이터와 함께 만들어집니다.<br/><br/> Azure Vm hello 처음 만들어질 때 toohello Azure 가상 네트워크를 연결 합니다.
**VMM 서버** | VMM 클라우드에 있는 Hyper-V 호스트 | VMM 클라우드에서 Hyper-v 호스트를 관리 하는 경우에 hello 복구 서비스 자격 증명 모음에 hello VMM 서버를 등록 합니다.<br/><br/> Hello VMM 서버의 azure hello Site Recovery Provider tooorchestrate 복제를 설치합니다.<br/><br/> 논리 및 VM 네트워크가 tooconfigure 네트워크 매핑을 설정 합니다. VM 네트워크는 hello 클라우드와 연결 된 논리 네트워크를 연결 된 tooa 이어야 합니다.
**Hyper-V 호스트** | Hyper-V 서버는 VMM 서버를 사용하거나 사용하지 않고 배포할 수 있습니다. | VMM 서버가 없는 경우 사이트 복구 공급자를 통해 Site Recovery와 hello 호스트 tooorchestrate 복제에 설치 되어 hello 인터넷 hello 합니다. VMM 서버인 경우 hello 공급자가 설치 되어 있는지, 및 hello 호스트에 없습니다.<br/><br/> hello 호스트 toohandle 데이터 복제에 hello 복구 서비스 에이전트가 설치 되어 있습니다.<br/><br/> Hello 공급자 및 hello 에이전트 모두의 통신을 안전 하 고 암호화 됩니다. Azure 저장소에 복제된 데이터도 암호화됩니다.
**Hyper-V VM** | Hello Hyper-v 호스트 서버에서 Vm을 하나 이상 필요합니다. | Vm에 설치 된 tooexplicitly 필요 없습니다.

## <a name="deployment-steps"></a>배포 단계

1. **Azure**: Azure 구성 요소 hello를 설정 합니다. Site Recovery 배포를 시작하기 전에 저장소 및 네트워크 계정을 설정하는 것이 좋습니다.
2. **자격 증명 모음**: Site Recovery에 대한 Recovery Services 자격 증명 모음을 만들고 원본 및 대상 설정 구성, 복제 정책 설정 및 복제 활성화를 포함하는 자격 증명 모음 설정을 구성합니다.
3. **원본 및 대상**:
    - **VMM 클라우드에서 Hyper-v 호스트**: 소스 설정 지정의 일부로 다운로드 하 고이 hello VMM 서버와 각 Hyper-v 호스트에서 hello Azure 복구 서비스 에이전트에서 hello Azure Site Recovery Provider를 설치 합니다. hello 원본 VMM 서버 hello 됩니다. hello 대상이 Azure입니다.
    - Hyper-v 호스트가 VMM 없이: 소스 설정을 지정 하면 다운로드 해 서 각 Hyper-v 호스트에 hello 공급자 및 에이전트를 설치 합니다. 배포 하는 동안 hello 호스트 하이퍼-V 사이트에 모으고이 사이트 hello 원본으로 지정 합니다. hello 대상이 Azure입니다.

    ![하이퍼-V/v m M 복제 tooAzure](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png) ![하이퍼-V 사이트 복제 tooAzure](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)


4. **복제 정책**: hello 하이퍼-V 사이트 또는 VMM 클라우드에 대 한 복제 정책을 만듭니다. hello 정책이 적용 된 tooall Vm의 hello 사이트 또는 클라우드 호스트에 있는입니다.
5. **복제 활성화**: Hyper-V VM에 대한 복제를 활성화합니다. 초기 복제 hello 복제 정책 설정에 따라 발생합니다. 데이터 변경 내용을 추적 하 고 hello 초기 복제가 완료 된 후에 델타 변경 내용 tooAzure의 복제 시작 합니다. .hrl 파일에는 항목에 대한 추적된 변경 내용이 유지됩니다.
6. **테스트 장애 조치**: 모든 것이 예상 대로 작동 하는지 테스트 장애 조치 toomake를 실행 합니다.

배포에 대해 자세히 알아보세요.
- [VMM과 Hyper-v VM 복제 tooAzure-시작](site-recovery-vmm-to-azure.md)
- [Hyper-v VM 복제 tooAzure-VMM 하지 않고 시작](site-recovery-hyper-v-site-to-azure.md)

## <a name="hyper-v-replication-workflow"></a>Hyper-V 복제 워크플로

### <a name="enable-protection"></a>보호 사용

1. Hyper-v VM에 대 한 보호를 사용 하도록 설정한 후 hello에 Azure 포털 또는 온-프레미스, hello **보호 사용** 시작 합니다.
2. hello 작업 확인 hello를 호출 하기 전에 해당 hello 컴퓨터 필수 구성 요소를 준수 [CreateReplicationRelationship](https://msdn.microsoft.com/library/hh850036.aspx)를 구성 하는 hello 설정 사용 하 여 복제를 tooset 합니다.
3. hello 작업이 hello를 호출 하 여 초기 복제 시작 [StartReplication](https://msdn.microsoft.com/library/hh850303.aspx) 메서드와 tooinitialize 전체 VM 복제를 송신 hello VM의 가상 디스크 tooAzure 합니다.
4. Hello에 hello 작업을 모니터링할 수 있습니다 **작업** 탭 합니다.      ![작업 목록](media/site-recovery-hyper-v-azure-architecture/image1.png)![보호 드릴 다운 사용](media/site-recovery-hyper-v-azure-architecture/image2.png)

### <a name="initial-replication"></a>초기 복제

1. 초기 복제가 트리거될 때 [Hyper-V VM 스냅숏](https://technet.microsoft.com/library/dd560637.aspx)이 만들어집니다.
2. 가상 하드 디스크 모두 복사한 tooAzure 하기가 하나씩 복제 됩니다. Hello VM 크기에 따라 시간이 오래 걸릴 하 고 네트워크 대역폭을 수 있습니다. toooptimize 네트워크 사용을 참조 [어떻게 toomanage 온-프레미스 tooAzure 보호 네트워크 대역폭 사용량](https://support.microsoft.com/kb/3056159)합니다.
3. 초기 복제가 진행 중인 동안 디스크 변경 내용이 발생 한 경우 Hyper-v 복제본 복제 추적기 hello Hyper-v 복제 로그 (.hrl)으로 변경 된 내용을 추적 합니다. 이러한 파일은 hello hello 디스크와 같은 폴더입니다. 각 디스크 toosecondary 저장소를 전송 하는 관련된.hrl 파일을 있습니다.
4. 초기 복제가 진행 중인 동안 hello 스냅숏 및 로그 파일에서 디스크 리소스를 소비 합니다.
5. Hello 초기 복제가 완료 되 면 hello VM 스냅숏이 삭제 됩니다. 델타 디스크 hello 로그에 변경은 동기화 되거나 병합 된 toohello 부모 디스크입니다.


### <a name="finalize-protection"></a>보호 완료

1. Hello 초기 복제가 완료 되 면 hello **hello 가상 컴퓨터에 대 한 보호 완료** hello 가상 컴퓨터가 보호 되 고 있도록 작업 네트워크 및 기타 복제 후 설정을 구성 합니다.
    ![보호 작업 완료](media/site-recovery-hyper-v-azure-architecture/image3.png)
2. TooAzure를 복제 하는 경우 장애 조치에 대해 준비 되도록 hello 가상 컴퓨터에 대 한 tootweak hello 설정을 할 수 있습니다. 이 시점에서 모든 것이 예상 대로 작동 하는 테스트 장애 조치 toocheck를 실행할 수 있습니다.

### <a name="delta-replication"></a>델타 복제

1. Hello 초기 복제 후 델타 동기화가 시작 되, 복제 설정에 따라 합니다.
2. Hyper-v 복제본 복제 추적기 hello.hrl 파일로 hello 변경 tooa 가상 하드 디스크를 추적합니다. 복제를 위해 구성된 각 디스크에는 연결된 .hrl 파일이 있습니다. 초기 복제가 완료 된 후이 로그 toohello 고객 저장소 계정을 보내집니다. 주 디스크 hello hello 변경 내용을 hello에 다른 로그 파일에서 추적 로그 전송 tooAzure 이면 동일한 디렉터리입니다.
3. 초기 및 델타 복제 하는 동안 VM 보기 hello에 VM hello를 모니터링할 수 있습니다. [자세히 알아봅니다](site-recovery-monitoring-and-troubleshooting.md#monitor-replication-health-for-virtual-machines).  

### <a name="replication-synchronization"></a>복제 동기화

1. 델타 복제에 실패했고 전체 복제에는 대역폭이나 시간이 많이 소모될 경우 VM에서 다시 동기화가 발생합니다. 예를 들어 hello.hrl 파일이 hello 디스크 크기의 50%에 도달 하는 경우 다음 hello VM 표시될지 다시 동기화에 대 한 합니다.
2.  다시 동기화 hello hello 소스 및 대상 가상 컴퓨터의 체크섬을 계산 하 고만 hello 델타 데이터를 보내는 여 보내지는 데이터 양을 최소화 합니다. 다시 동기화는 고정 블록 청크 알고리즘을 사용하며 이 경우 원본 및 대상 파일이 고정 청크로 나누어집니다. 각 청크에 대 한 체크섬 생성 되 고 hello 소스 필요 toobe 적용 된 toohello 대상에서 차단 되 toodetermine와 비교 합니다.
3. 다시 동기화를 마치면 일반 델타 복제가 다시 시작됩니다. 기본적으로 다시 동기화가 자동으로 근무 시간 외부 예약된 toorun 하지만 수동으로 가상 컴퓨터를 동기화 할 수 있습니다. 예를 들어 네트워크 중단 또는 다른 중단이 발생하면 다시 동기화를 다시 시작할 수 있습니다. toodo hello 포털에서이 선택 hello VM > **다시 동기화**합니다.

    ![수동 다시 동기화](media/site-recovery-hyper-v-azure-architecture/image4.png)


### <a name="retries"></a>다시 시도

복제 오류가 발생한 경우 기본 제공 재시도가 있습니다. 이 논리는 두 가지 범주로 분류할 수 있습니다.

**범주** | **세부 정보**
--- | ---
**복구할 수 없는 오류** | 재시도가 수행되지 않습니다. VM 상태가 **위험**으로 표시되고 관리자 개입이 필요합니다. 이러한 오류의 예로: VHD 체인; 분할 Hello 복제본 VM;에 대 한 잘못 된 상태 네트워크 인증 오류: 권한 부여 오류; VM (독립 실행형 Hyper-v 서버)에 대 한 오류를 찾을 수 없습니다
**복구할 수 있는 오류** | 다시 시도 횟수는 지 수 백오프 hello 다시 시도 간격에서 시작 하 여 1, 2, 4, 8, 첫 번째 시도 hello hello 및 10 분 증가 하는 사용 하 여 복제 간격 마다 발생 합니다. 오류가 계속되면 30분마다 다시 시도하십시오. 이러한 예로는 네트워크 오류, 디스크 공간 부족, 메모리 부족 상태가 있습니다. |

## <a name="protection-and-recovery-lifecycle"></a>보호 및 복구 수명 주기

![워크플로](./media/site-recovery-components/arch-hyperv-azure-workflow.png)

## <a name="next-steps"></a>다음 단계

- [배포 필수 조건 확인](site-recovery-prereq.md)
- 문제 해결:
    - [보호 모니터링 및 문제 해결](site-recovery-monitoring-and-troubleshooting.md)
    - [Microsoft 지원의 도움](site-recovery-monitoring-and-troubleshooting.md#reach-out-for-microsoft-support)
    - [일반적인 문제 및 해결 방법](site-recovery-monitoring-and-troubleshooting.md#common-azure-site-recovery-errors-and-their-resolutions)
