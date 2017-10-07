---
title: "Azure Site Recovery와 복제 tooa 보조 사이트에 대 한 VMM 및 Hyper-v를 aaaSet | Microsoft Docs"
description: "설명 방법을 tooset System Center VMM 서버와 복제 tooa 보조 VMM 사이트에 대 한 Hyper-v 호스트를 구성 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>4 단계: Hyper-v VM 복제 tooa 보조 사이트에 대 한 VMM 및 Hyper-v를 설정 합니다. 

System Center Virtual Machine Manager (VMM) 서버 및 Hyper-v 가상 컴퓨터 (VM) 복제 tooa 보조 사이트에 대 한 Hyper-v 호스트를 설정 하는 네트워킹에 대 한 준비 된 후 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) hello Azure 포털에서에서 합니다. 

이 문서를 읽은 후 게시 설명을 hello 맨 아래에 하거나 hello에 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.



## <a name="prepare-vmm-servers"></a>VMM 서버 준비 

배포에 대 한 tooprepare:


1. VMM 서버 hello를 준수 하는지 확인 [요구 사항을 지원](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), 및 [배포 필수 구성 요소](vmm-to-vmm-walkthrough-prerequisites.md)합니다.
2. VMM 서버가 연결 된 toohello 하는지 확인 하기 인터넷 toothese url이 액세스 하 고 있습니다.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.
    - Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.
    - West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.
3. Hello VMM 서버 인지 확인 [네트워크 매핑 준비](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Hyper-V 호스트/클러스터 준비

1. Hyper-v 호스트/클러스터 hello를 준수 하는지 확인 [요구 사항을 지원](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), 및 [배포 필수 구성 요소](vmm-to-vmm-walkthrough-prerequisites.md)합니다.
2. 에 대 한 hello 요구 사항을 확인 [Hyper-v Vm](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. [네트워크](site-recovery-support-matrix-to-sec-site.md#network-configuration) 및 [저장소](site-recovery-support-matrix-to-sec-site.md#storage) 요구 사항을 확인합니다.
4. Hyper-v 호스트에 연결 된 toohello 되는지 확인 인터넷 toothese url이 액세스 하 고 있습니다.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - IP 주소를 기준으로 방화벽 규칙을 사용 하는 경우 통신 tooAzure를 허용 하는지 확인 합니다.
    - Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 hello HTTPS (443) 포트입니다.
    - West US (액세스 제어 및 Id 관리에 사용) 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.

## <a name="prepare-for-single-server-deployment"></a>단일 서버 배포 준비


단일 VMM 서버를만 있는 경우 복제 하는 Vm hello VMM 클라우드에 있는 Hyper-v 호스트에서 너무[Azure](hyper-v-site-walkthrough-overview.md) 또는 tooa 보조 VMM 클라우드에이 문서에 설명 된 대로 합니다. 클라우드 간의 복제 원활 하 게 아니어서 hello 첫 번째 옵션을 좋습니다.

스트레치 된 Windows 클러스터에 배포 된 단일 VMM 서버 또는 단일 독립 실행형 VMM 서버와 클라우드 간의 tooreplicate 않도록 하려는 경우 복제할 수 있습니다.

### <a name="replicate-with-a-standalone-vmm-server"></a>독립 실행형 VMM 서버로 복제

이 시나리오에서는 hello 기본 사이트에서 가상 컴퓨터로 hello 단일 VMM 서버를 배포 하 고 Site Recovery 및 Hyper-v 복제본을 사용 하 여이 VM tooa 보조 사이트를 복제 합니다.

1. **Hyper-V VM에 VMM을 설정합니다**. Hello에 VMM에서 사용 하는 hello SQL Server 인스턴스를 배치 하는 것이 동일한 VM입니다. 하나의 VM에 만든 toobe 시간이 절약 됩니다. SQL Server의 원격 인스턴스 toouse 원하고 중단이 발생 한 경우 있어야만 toorecover 해당 인스턴스에 VMM을 복구할 수 있습니다.
2. **Hello VMM 서버에 둘 이상의 클라우드가 구성 되어 있는지 확인**합니다. 한 클라우드 hello hello 보조 위치로 사용할 tooreplicate을 다른 클라우드 hello Vm이 포함 됩니다. tooprotect 준수 해야 하는 것이 원하는 hello Vm이 포함 된 클라우드 hello [필수 구성 요소](#prerequisites)합니다.
3. 이 문서에 설명된 대로 Site Recovery를 설정합니다. 만들기 및 자격 증명 모음에 hello VMM 서버를 등록, 복제 정책을 설정 및 복제를 사용 하도록 설정 합니다. hello 원본 및 대상 VMM 이름은 같은 hello 됩니다. Hello 네트워크를 통해 초기 복제 발생을 지정 합니다.
4. 네트워크 매핑을 설정할 때 hello VM 네트워크를 보조 클라우드 hello에 대 한 hello 기본 클라우드 toohello VM 네트워크를 매핑합니다.
5. Hello Hyper-v Manager 콘솔에서 VMM VM hello를 포함 하는 hello Hyper-v 호스트에서 Hyper-v 복제본을 사용 하도록 설정 하 고 hello VM에 복제를 사용 합니다. Hyper-v 복제본 설정을 Site Recovery에 의해 재정의 되지 tooensure Site Recovery로 보호 되는 hello VMM 가상 컴퓨터 tooclouds 추가 하지 않으면 있는지 확인 합니다.
6. 사용 하는 장애 조치에 대 한 복구 계획을 만드는 경우 원본에 대 한 동일한 VMM 서버 hello 및 대상 합니다.
7. 전체 가동 중단 시 다음과 같이 장애 조치를 수행하고 복구합니다.

   1. Hello Hyper-v 관리자 콘솔의 hello 기본 VMM VM toohello 보조 사이트를 통해 toofail hello 보조 사이트에서 계획 되지 않은 장애 조치를 실행 합니다.
   2. VMM VM이 위쪽 해당 hello를 확인 하 고 실행 되 고 hello 자격 증명 모음에서 실행 계획 되지 않은 장애 조치 toofail hello Vm을 통해 기본 toosecondary 클라우드에서 키를 누릅니다. Hello 장애 조치 커밋 및 필요한 경우 대체 복구 지점을 선택 합니다.
   3. Hello 계획 되지 않은 장애 조치가 완료 되 면 리소스를 모두 액세스할 수 있습니다 hello 기본 사이트에서 다시.
   4. Hello 기본 사이트를 hello Hyper-v 관리자 콘솔의 hello 보조 사이트에서 다시 사용할 수 있는 VMM VM hello에 대 한 역방향 복제를 사용 하도록 설정 합니다. 이 보조 tooprimary에서 VM hello에 대 한 복제를 시작합니다.
   5. Hello Hyper-v 관리자 콘솔의 hello VMM VM toohello 기본 사이트를 통해 toofail hello 보조 사이트에서 계획된 된 장애 조치를 실행 합니다. Hello 장애 조치를 커밋하십시오. Hello VMM VM은 다시에서 복제할 primary toosecondary 있도록 역방향 복제를 사용 합니다.
   6. Hello 복구 서비스 자격 증명 모음에 hello 작업 부하 Vm의 경우 보조 tooprimary에서 복제 하지 toostart 역방향 복제를 설정 합니다.
   7. Hello 복구 서비스 자격 증명 모음에, 계획 된 장애 조치 toofail 백 hello 작업 부하 Vm toohello 기본 사이트를 실행 합니다. 커밋 장애 조치 toocomplete hello 것입니다. 역방향 복제 toostart 복제 hello 작업 부하 Vm 기본 toosecondary에서 사용 하도록 설정 합니다.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>확대 VMM 클러스터로 복제

배포 tooa 보조 사이트를 복제 하는 VM으로 독립 실행형 VMM 서버를 배포 하는 대신 VMM 항상 사용 가능 하 게 만들 하는 Windows 장애 조치 클러스터에서 VM으로 배포 하 여 수 있습니다. 그러면 워크로드 복원력이 제공되고 하드웨어 장애로부터 보호됩니다. 사이트 복구 hello VMM VM로 toodeploy 지리적으로 분산 된 사이트에 걸쳐 늘이기 클러스터에 배포 되어야 합니다. toodo이:

1. Windows 장애 조치 클러스터에서 가상 컴퓨터에 VMM을 설치 하 고 설치 하는 동안 항상 사용 가능 hello 옵션 toorun hello 서버를 선택 합니다.
2. VMM에서 사용 되는 hello SQL Server 인스턴스에 hello hello 보조 사이트에는 데이터베이스의 복제본이 되도록 SQL Server AlwaysOn 가용성 그룹이 포함 된 복제 되어야 합니다.
3. 이 문서 toocreate 자격 증명 모음에에서 hello 지침, hello 서버를 등록 하 고 보호를 설정 합니다. 각 VMM 서버 hello에 hello 복구 서비스 자격 증명 모음에 있는 클러스터 tooregister가 필요 합니다. toodo이를 액티브 노드에서 hello 공급자를 설치 하 고 hello VMM 서버를 등록 합니다. 그런 다음 다른 노드에서 hello 공급자를 설치합니다.
4. 중단이 발생할 때 hello VMM 서버와 해당 SQL Server 데이터베이스, 장애 조치 되며 hello 보조 사이트에서 액세스 합니다.



## <a name="next-steps"></a>다음 단계

너무 이동[5 단계: 자격 증명 모음 설정](vmm-to-vmm-walkthrough-create-vault.md)합니다.
