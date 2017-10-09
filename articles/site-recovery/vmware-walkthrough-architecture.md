---
title: "VMware 복제 tooAzure aaaReview hello 아키텍처 | Microsoft Docs"
description: "이 문서에서는 구성 요소와 hello Azure Site Recovery 서비스와 온-프레미스 VMware Vm tooAzure 복제할 때 사용 되는 아키텍처의 개요"
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>1 단계: 복제 tooAzure VMware에 대 한 hello 아키텍처를 검토 합니다.

이 문서에서는 hello 구성 요소 및 복제 온-프레미스 hello를 사용 하 여 VMware 가상 컴퓨터 tooAzure 때 사용 되는 프로세스를 설명 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

이 문서에서는 hello 맨 아래에 대 한 설명을 게시 하거나 hello에서 질문 하기 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="architectural-components"></a>아키텍처 구성 요소

hello 표에서 필요한 hello 구성 요소를 요약 합니다.

**구성 요소** | **요구 사항** | **세부 정보**
--- | --- | ---
**Azure** | Azure 구독, Azure Storage 계정 및 Azure 네트워크가 필요합니다. | 복제 된 데이터는 hello 저장소 계정에 저장 됩니다. Azure Vm은 온-프레미스 사이트에서 장애 조치 발생 시 hello 복제 된 데이터와 함께 생성 됩니다. Azure Vm hello 처음 만들어질 때 toohello Azure 가상 네트워크를 연결 합니다.
**구성 서버** | 단일 온-프레미스 모든 hello 온-프레미스 hello 배포에 대 한 Site Recovery 구성 요소를 실행 하는 관리 서버 (VMware VM). 여기에는 구성 서버, 프로세스 서버, 마스터 대상 서버가 포함됩니다. | 온-프레미스와 Azure 간의 통신을 조정 하 고 데이터 복제를 관리 하는 hello 구성 서버 구성 요소입니다.
 **프로세스 서버**:  | Hello 구성 서버에 기본적으로 설치 합니다. | 복제 게이트웨이의 역할을 합니다. 복제 데이터를 수신 하 고 캐싱, 압축 및 암호화와 최적화 tooAzure 저장소 보냅니다.<br/><br/> 또한 hello 프로세스 서버 hello 이동성 서비스 tooprotected 컴퓨터의 강제 설치를 처리 하 고 VMware Vm의 자동 검색을 수행 합니다.<br/><br/> 배포에까지 확장 되면서 복제 트래픽 볼륨을 늘리면 추가 별도 전용된 프로세스 서버 toohandle를 추가할 수 있습니다.
 **마스터 대상 서버** | Hello 온-프레미스 구성 서버에 기본적으로 설치 합니다. | Azure에서 장애 복구 중에 복제 데이터를 처리합니다.<br/><br/> 장애 복구 트래픽 볼륨이 높은 경우 장애 복구를 위해 별도 마스터 대상 서버를 배포할 수 있습니다.
**VMware 서버** | VMware Vm는 vSphere ESXi 서버에서 호스팅되며 vCenter server toomanage hello 호스트 권장 합니다. | VMware 서버 tooyour 복구 서비스 자격 증명 모음을 추가 합니다.
**복제된 컴퓨터** | 모바일 서비스 hello 복제 하는 각 VMware VM에 설치 됩니다. Hello 프로세스 서버에서 강제 설치 또는 각 컴퓨터에 수동으로 설치할 수 있습니다.

**그림 1: VMware tooAzure 구성 요소**

![구성 요소](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>복제 프로세스

1. 온-프레미스 및 Azure 구성 요소를 포함 하 여 hello 배포를 설정 합니다. Hello 복구 서비스 자격 증명 모음에 hello 복제 원본 및 대상, hello 구성 서버를 설치한 복제 정책을 만들지, hello 모바일 서비스를 배포, 복제를 사용 및 테스트 장애 조치를 실행할 지정 합니다.
2. Hello 복제 정책 및 hello 데이터의 초기 복사본에 따라 컴퓨터 복제는 복제 된 tooAzure 저장소.
3. 초기 복제가 완료 되 면 델타 변경 내용 tooAzure의 복제를 시작 합니다. .hrl 파일에는 컴퓨터에 대한 추적된 변경 내용이 유지됩니다.
    - 복제 컴퓨터 서버와 통신 hello 구성 HTTPS 443 포트에서 인바운드 복제 관리에 대 한 합니다.
    - 복제 컴퓨터 보내고 복제 데이터 toohello 프로세스 서버 HTTPS 9443 포트에서 인바운드 (수정할 수 있음).
    - 구성 서버 hello HTTPS 443 아웃 바운드 포트를 통해 Azure 사용한 복제 관리를 조정합니다.
    - hello 프로세스 서버가 원본 컴퓨터에서 데이터를 수신, 최적화 및, 암호화를 보냅니다 tooAzure 저장소 포트 443 통해 아웃 바운드.
    - 다중 VM 일관성이 사용 하도록 설정 하면 다음 hello 복제 그룹에 컴퓨터 서로 통신할 포트 20004 통해 합니다. 다중 VM은 장애 조치 시(failover) 크래시 일관성 및 앱 일관성 복구 지점을 공유하는 복제 그룹에 여러 컴퓨터를 그룹화하는 경우 사용됩니다. 이 컴퓨터가 실행 중인 경우에 유용 같은 작업을 hello 및 toobe 일치 해야 합니다.
4. 복제 된 tooAzure 저장소 공용 끝점을 넘는 트래픽은 인터넷 hello 합니다. Azure ExpressRoute [공용 피어링](../expressroute/expressroute-circuit-peerings.md#public-peering)을 사용할 수도 있습니다. 온-프레미스 사이트 tooAzure에서 사이트 간 VPN을 통해 복제 하는 트래픽을 지원 되지 않습니다.


**그림 2: VMware tooAzure 복제**

![향상된](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>장애 조치 및 장애 복구 프로세스

1. 테스트 장애 조치가 수행 되는 예상 대로 작동 하는지 확인 한 후 필요에 따라 계획 되지 않은 장애 조치 tooAzure를 실행할 수 있습니다. 계획된 장애 조치는 지원되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md), 여러 Vm에 toofail 합니다.
3. 장애 조치를 실행하면 Azure에 복제본 VM이 만들어집니다. Hello 복제 Azure VM에서에서 장애 조치 toostart 액세스 hello 작업을 커밋합니다.
4. 기본 온-프레미스 사이트를 다시 사용할 수 있는 경우 장애 복구를 수행할 수 있습니다. Hello 컴퓨터 hello 보조 사이트 toohello 기본에서 복제를 시작을 hello 보조 사이트에서 계획 되지 않은 경우 장애 조치를 실행 장애 복구 인프라를 설정 합니다. 이 장애 조치를 커밋하면 데이터가 다시 온-프레미스, 됩니다 하 고 다시 tooenable 복제 tooAzure 사용 해야 합니다. [자세히 알아보기](site-recovery-failback-azure-to-vmware.md)

몇 가지 장애 복구 요구 사항이 있습니다.


- **Azure에서 임시 프로세스 서버**: 장애 조치 후 Azure에서 다시 toofail 하려는 경우 Azure에서 toohandle 복제 프로세스 서버로 구성 된 Azure VM을 tooset 필요 합니다. 장애 복구를 완료한 후 이 VM을 삭제할 수 있습니다.
- **VPN 연결**: 해야 하는 장애 복구에 대 한 VPN 연결 (이나 Azure express 경로)에서 설정 hello Azure 네트워크 toohello 온-프레미스 사이트입니다.
- **별도 온-프레미스 마스터 대상 서버**: hello 온-프레미스 마스터 대상 서버 장애 복구를 처리 합니다. hello 마스터 대상 서버 hello 관리 서버에 기본적으로 설치 됩니다 없으며이 목적을 위해 별도 온-프레미스 마스터 대상 서버를 설정 해야 트래픽의 다시 더 큰 볼륨 실패 하는 경우.
- **장애 복구 정책**: tooreplicate 백 tooyour 온-프레미스 사이트 장애 복구 정책을 사용 해야 합니다. 이 정책은 복제 정책을 만들 때 자동으로 생성됩니다.
- **VMware 인프라**: 다시 장애 복구 해야 tooan 온-프레미스 VMware VM입니다. 즉, 온-프레미스 VMware 인프라를 사용 하는 온-프레미스 물리적 서버 tooAzure를 복제 하는 경우에 합니다.

**그림 3: VMware/물리적 장애 복구**

![장애 복구](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>다음 단계

너무 이동[2 단계: 사전 요구 사항 및 제한 사항 확인](vmware-walkthrough-prerequisites.md)
