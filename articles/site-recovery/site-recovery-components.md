---
title: "사이트 복구 작업을 수행 하는 aaaHow? | Microsoft Docs"
description: "이 문서는 사이트 복구 아키텍처의 개요를 제공합니다."
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
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>온-프레미스 인프라에 Azure Site Recovery가 작동하나요?

> [!div class="op_single_selector"]
> * [Azure 가상 컴퓨터 복제](site-recovery-azure-to-azure-architecture.md)
> * [온-프레미스 컴퓨터 복제](site-recovery-components.md)

이 문서에서는 hello의 기본 아키텍처를 설명 [Azure Site Recovery](site-recovery-overview.md) tooAzure 온-프레미스에서에서 작업을 복제 하기 위한 작동 하는 서비스 및 해당 하는 hello 구성 합니다.

Hello 또는이 문서의 hello 맨 아래에 모든 메모를 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="replicate-tooazure"></a>TooAzure 복제

복제 및 프레미스 인프라 tooAzure에서 hello 다음 보호할 수 있습니다.

- **VMware**: [지원되는 호스트](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)에서 실행되는 온-프레미스 VMware VM. [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)에서 실행되는 VMware VM을 복제할 수 있습니다.
- **Hyper-V**: [지원되는 호스트](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)에서 실행되는 온-프레미스 Hyper-V VM.
- **물리적 컴퓨터**: [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)에서 Windows 또는 Linux를 실행하는 온-프레미스 물리적 서버. [Hyper-V 및 Azure에서 지원하는](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) 게스트 운영 체제를 실행하는 Hyper-V VM을 복제할 수 있습니다.

## <a name="vmware-tooazure"></a>VMware tooAzure

VMware Vm tooAzure 복제에 필요한 것 같습니다.

영역 | 구성 요소 | 세부 정보
--- | --- | ---
**구성 서버** | 모든 온-프레미스 구성 요소(단일 관리 서버구성 서버, 프로세스 서버, 마스터 대상 서버)를 실행하는 단일 관리 서버(VMWare VM) | 온-프레미스와 Azure 간의 통신을 조정 하 고 데이터 복제를 관리 하는 hello 구성 서버입니다.
 **프로세스 서버**:  | Hello 구성 서버에 기본적으로 설치 합니다. | 복제 게이트웨이의 역할을 합니다. 복제 데이터를 수신 하 고 캐싱, 압축 및 암호화와 최적화 tooAzure 저장소 보냅니다.<br/><br/> 또한 hello 프로세스 서버 hello 이동성 서비스 tooprotected 컴퓨터의 강제 설치를 처리 하 고 VMware Vm의 자동 검색을 수행 합니다.<br/><br/> 배포에까지 확장 되면서 복제 트래픽 볼륨을 늘리면 추가 별도 전용된 프로세스 서버 toohandle를 추가할 수 있습니다.
 **마스터 대상 서버** | Hello 온-프레미스 구성 서버에 기본적으로 설치 합니다. | Azure에서 장애 복구 중에 복제 데이터를 처리합니다.<br/><br/> 장애 복구 트래픽 볼륨이 높은 경우 장애 복구를 위해 별도 마스터 대상 서버를 배포할 수 있습니다.
**VMware 서버** | VMware Vm는 vSphere ESXi 서버에서 호스팅되며 vCenter server toomanage hello 호스트 권장 합니다. | VMware 서버 tooyour 복구 서비스 자격 증명 모음을 추가 합니다.<br/><br/>
**복제된 컴퓨터** | 모바일 서비스 hello 각 VMware tooreplicate 원하는 VM에 설치 됩니다. Hello 프로세스 서버에서 강제 설치 또는 각 컴퓨터에 수동으로 설치할 수 있습니다.| -

**그림 1: VMware tooAzure 구성 요소**

![구성 요소](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>복제 프로세스

1. 복구 서비스 자격 증명 모음 및 Azure 구성 요소를 포함 하 여 hello 배포를 설정 합니다. Hello 자격 증명 모음에 hello 복제 원본 및 대상, hello 구성 서버를 설치한 VMware 서버를 추가, 복제 정책을 만들지, hello 모바일 서비스를 배포, 복제를 사용 하도록 설정 및 지정 테스트 장애 조치를 실행 합니다.
2.  컴퓨터 hello 복제 정책에 따라 복제를 시작 하 고 hello 데이터의 초기 복사본에 복제 된 tooAzure 저장소가 합니다.
4. 델타 변경 내용 tooAzure의 복제 hello 초기 복제가 완료 된 후 시작 합니다. .hrl 파일에는 컴퓨터에 대한 추적된 변경 내용이 유지됩니다.
    - 복제 컴퓨터 서버와 통신 hello 구성 HTTPS 443 포트에서 인바운드 복제 관리에 대 한 합니다.
    - 복제 컴퓨터 보내고 복제 데이터 toohello 프로세스 서버 HTTPS 9443 포트에서 인바운드 (구성할 수 있습니다).
    - 구성 서버 hello HTTPS 443 아웃 바운드 포트를 통해 Azure 사용한 복제 관리를 조정합니다.
    - hello 프로세스 서버가 원본 컴퓨터에서 데이터를 수신, 최적화 및, 암호화를 보냅니다 tooAzure 저장소 포트 443 통해 아웃 바운드.
    - 다중 VM 일관성이 사용 하도록 설정 하면 다음 hello 복제 그룹에 컴퓨터 서로 통신할 포트 20004 통해 합니다. 다중 VM은 장애 조치 시(failover) 크래시 일관성 및 앱 일관성 복구 지점을 공유하는 복제 그룹에 여러 컴퓨터를 그룹화하는 경우 사용됩니다. 이 컴퓨터가 실행 중인 경우에 유용 같은 작업을 hello 및 toobe 일치 해야 합니다.
5. 복제 된 tooAzure 저장소 공용 끝점을 넘는 트래픽은 인터넷 hello 합니다. Azure ExpressRoute [공용 피어링](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering)을 사용할 수도 있습니다. 온-프레미스 사이트 tooAzure에서 사이트 간 VPN을 통해 복제 하는 트래픽을 지원 되지 않습니다.

**그림 2: VMware tooAzure 복제**

![향상된](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>장애 조치 및 장애 복구

1. 테스트 장애 조치가 수행 되는 예상 대로 작동 하는지 확인 한 후 필요에 따라 계획 되지 않은 장애 조치 tooAzure를 실행할 수 있습니다. 계획된 장애 조치는 지원되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md), 여러 Vm에 toofail 합니다.
3. 장애 조치를 실행하면 Azure에 복제본 VM이 만들어집니다. Hello 복제 Azure VM에서에서 장애 조치 toostart 액세스 hello 작업을 커밋합니다.
4. 기본 온-프레미스 사이트를 다시 사용할 수 있는 경우 장애 복구를 수행할 수 있습니다. Hello 컴퓨터 hello 보조 사이트 toohello 기본에서 복제를 시작을 hello 보조 사이트에서 계획 되지 않은 경우 장애 조치를 실행 장애 복구 인프라를 설정 합니다. 이 장애 조치를 커밋하면 데이터가 다시 온-프레미스, 됩니다 하 고 다시 tooenable 복제 tooAzure 사용 해야 합니다. [자세히 알아보기](site-recovery-failback-azure-to-vmware.md)

**그림 3: VMware/물리적 장애 복구**

![장애 복구](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>물리적 tooAzure

동일한 구성 요소 및 프로세스를 사용 하 여 복제도 hello 실제 온-프레미스 서버 tooAzure을 복제 하면 [VMware tooAzure](#vmware-replication-to-azure), 이러한 차이점이 있지만:

- VMware VM 대신 hello 구성 서버에 대 한 물리적 서버를 사용할 수 있습니다.
- 장애 복구를 위해 온-프레미스 VMware 인프라가 필요합니다. 물리적 컴퓨터 백 tooa 실패로 지정할 수 없습니다.

## <a name="hyper-v-tooazure"></a>Hyper-v tooAzure

### <a name="replication-process"></a>복제 프로세스

1. Azure 구성 요소 hello를 설정 합니다. Site Recovery 배포를 시작하기 전에 저장소 및 네트워크 계정을 설정하는 것이 좋습니다.
2. Site Recovery에 대한 복제 서비스 자격 증명 모음을 만들고 다음을 포함한 자격 증명 모음 설정을 구성합니다.
    - 원본 및 대상 설정. VMM 클라우드에서 Hyper-v 호스트를 관리 하지 하는 경우 hello 대상에 대 한 Hyper-v 사이트 컨테이너를 만들고 Hyper-v 호스트 tooit를 추가 합니다. Hyper-v 호스트를 VMM에서 관리 하는 경우 hello 원본은 hello v m M 클라우드입니다. hello 대상이 Azure입니다.
    - Azure Site Recovery Provider hello 및 hello Microsoft Azure 복구 서비스 에이전트 설치입니다. 공급자를에 설치 됩니다. 및 각 Hyper-v 호스트의 에이전트 hello VMM hello 경우 클릭 합니다. VMM에 없으면 hello 공급자 및 에이전트 모두 각 호스트에 설치 됩니다.
    - Hyper-v 사이트 hello 또는 VMM 클라우드에 대 한 복제 정책을 만듭니다. hello 정책이 적용 된 tooall Vm의 hello 사이트 또는 클라우드 호스트에 있는입니다.
    - Hyper-V VM에 복제를 사용하도록 설정합니다. 초기 복제 hello 복제 정책 설정에 따라 발생합니다.
4. 데이터 변경 내용을 추적 하 고 hello 초기 복제가 완료 된 후에 델타 변경 내용 tooAzure의 복제 시작 합니다. .hrl 파일에는 항목에 대한 추적된 변경 내용이 유지됩니다.
5. 테스트 장애 조치 toomake 있는지를 실행 하면 모든 기능이 작동 합니다.

### <a name="failover-and-failback-process"></a>장애 조치 및 장애 복구 프로세스

1. 계획을 실행할 수 있습니다 또는 계획 되지 않은 [장애 조치](site-recovery-failover.md) 온-프레미스 Hyper-v Vm tooAzure에서 합니다. 경우 계획된 된 장애 조치를 실행 한 후 원본 Vm이 tooensure 종료 데이터가 손실 되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md) tooorchestrate 여러 컴퓨터를 장애 조치 합니다.
4. Hello 장애 조치를 실행 한 후에 Azure에서 복제본 Vm을 만든 수 toosee hello 있어야 합니다. 필요한 경우 공용 IP 주소 toohello VM을 할당할 수 있습니다.
5. 그런 다음 hello 복제 Azure VM에서에서 hello 작업에 액세스 하는 hello 장애 조치 toostart를 커밋합니다.
6. 기본 온-프레미스 사이트를 다시 사용할 수 있는 경우 [장애 복구](site-recovery-failback-from-azure-to-hyper-v.md)를 수행할 수 있습니다. 하면 Azure toohello 기본 사이트에서 계획된 된 장애 조치를 시작 합니다. 계획 된 장애 조치를 수행할 수 있습니다 선택 toofailback toohello 동일한 VM 또는 tooan 대체 위치를 하 고 동기화 사이 변경 Azure 및 온-프레미스, tooensure 데이터가 손실 되지 않습니다. Vm에서 온-프레미스를 만든 경우 hello 장애 조치를 커밋합니다.

**그림 4: 하이퍼-V 사이트 tooAzure 복제**

![구성 요소](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**그림 5: VMM에서 Hyper-v 클라우드 tooAzure 복제**

![구성 요소](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>Tooa 보조 사이트를 복제 합니다.

Hello 다음 tooyour 보조 사이트를 복제할 수 있습니다.

- **VMware**: [지원되는 호스트](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)에서 실행되는 온-프레미스 VMware VM. [지원되는 운영 체제](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)에서 실행되는 VMware VM을 복제할 수 있습니다.
- **물리적 컴퓨터**: [지원되는 운영 체제](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)에서 Windows 또는 Linux를 실행하는 온-프레미스 물리적 서버.
- **Hyper-V**: VMM 클라우드에서 관리되는 [지원되는 Hyper-V 호스트](site-recovery-support-matrix-to-sec-site.md#on-premises-servers)에서 실행되는 온-프레미스 Hyper-V VM. [지원되는 호스트](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). [Hyper-V 및 Azure에서 지원하는](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) 게스트 운영 체제를 실행하는 Hyper-V VM을 복제할 수 있습니다.


## <a name="vmwarephysical-tooa-secondary-site"></a>보조 사이트/물리적 tooa

VMware Vm 또는 실제 서버 tooa 보조 사이트 InMage Scout를 사용 하 여 복제할 수 있습니다.

### <a name="components"></a>구성 요소

**영역** | **구성 요소** | **세부 정보**
--- | --- | ---
**프로세스 서버** | 기본 사이트에 있음 | Hello 프로세스 서버 toohandle 캐싱, 압축 및 데이터 최적화를 배포 합니다.<br/><br/> 또한 에이전트 통합 toomachines tooprotect 원하는 hello의 강제 설치를 처리 합니다.
**구성 서버** | 보조 사이트에 있음 | hello 구성 서버를 관리, 구성 및 배포, 하거나 모니터링 hello 관리 웹 사이트 또는 hello vContinuum 콘솔을 사용 하 여 합니다.
**vContinuum 서버** | 선택 사항입니다. Hello에 동일한 설치 hello 구성 서버와 위치 합니다. | 보호되는 환경을 관리 및 모니터링하기 위한 콘솔을 제공합니다.
**마스터 대상 서버** | Hello 보조 사이트에 있는 | hello 마스터 대상 서버는 복제 된 데이터를 저장합니다. Hello 프로세스 서버에서 데이터를 수신, 복제 컴퓨터 hello 보조 사이트에 만들고 hello 데이터 보존 지점을 보유 합니다.<br/><br/> hello 수가 필요한 마스터 대상 서버를 보호 하는 컴퓨터의 hello 수에 따라 다릅니다.<br/><br/> 원하는 toofail 백 toohello 기본 사이트는 마스터 대상 서버 너무 필요 합니다. hello 통합 에이전트는이 서버에 설치 합니다.
**VMware ESX/ESXi 및 vCenter 서버** |  ESX/ESXi 호스트에서 호스트되는 VM. vCenter 서버로 관리되는 호스트. | VMware 인프라 tooreplicate VMware Vm 필요합니다.
**VM/물리적 서버** |  Tooreplicate 원하는 물리적 서버와 VMware Vm에 설치 된 에이전트를 통합 합니다. | hello 에이전트의 모든 hello 구성 요소 간의 통신 공급자 역할을 합니다.


### <a name="replication-process"></a>복제 프로세스

1. (구성, 프로세스, 마스터 대상)에 각 사이트에 구성 요소 서버 hello 설정 하 고 hello 통합 에이전트 tooreplicate 컴퓨터에 설치 합니다.
2. 초기 복제 후 각 컴퓨터에 hello 에이전트 델타 복제 변경 내용 toohello 프로세스 서버를 보냅니다.
3. hello 프로세스 서버 hello 데이터를 최적화 하 고 toohello 마스터 대상 서버 hello 보조 사이트에 전송 합니다. hello 구성 서버 hello 복제 프로세스를 관리합니다.

**그림 6: VMware tooVMware 복제**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Hyper-v tooa 보조 사이트

Hyper-v Vm tooa 보조 사이트를 복제에 필요한 것 같습니다.


**영역** | **구성 요소** | **세부 정보**
--- | --- | ---
**VMM 서버** | Hello 기본 사이트에서 VMM 서버에 한 hello 보조 사이트는 것이 좋습니다. | 각 VMM 서버에 연결 된 toohello 해야 인터넷 합니다.<br/><br/> 각 서버 hello Hyper-v 기능 프로필 설정 된 하나 이상의 VMM 사설 클라우드, 있어야 합니다.<br/><br/> VMM 서버 hello에 hello Azure Site Recovery Provider를 설치합니다. hello 공급자를 조정 하 고 hello를 통해 hello Site Recovery 서비스와의 복제를 조정 인터넷 합니다. Hello 공급자와 Azure 간의 통신에 안전 하 고 암호화 됩니다.
**Hyper-V 서버** |  하나 이상의 Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 있습니다.<br/><br/> 서버에 연결 된 toohello 되어야 합니다 인터넷 합니다.<br/><br/> Hello LAN 또는 VPN, Kerberos 또는 인증서 인증을 사용 하 여 hello 기본 및 보조 Hyper-v 호스트 서버 간에 데이터가 복제 됩니다.  
**Hyper-V VM** | Hello 원본 Hyper-v 호스트 서버에 위치합니다. | 원본 호스트 서버 hello tooreplicate 원하는 VM을 하나 이상 있어야 합니다.

### <a name="replication-process"></a>복제 프로세스

1. Hello Azure 계정 설정합니다.
2. Site Recovery에 대한 복제 서비스 자격 증명 모음을 만들고 다음을 포함한 자격 증명 모음 설정을 구성합니다.

    - hello 복제 원본 및 대상 (기본 및 보조 사이트).
    - Azure Site Recovery Provider hello 및 hello Microsoft Azure 복구 서비스 에이전트 설치입니다. hello 공급자는 VMM 서버 및 각 Hyper-v 호스트에서 hello 에이전트에 설치 됩니다.
    - 원본 VMM 클라우드에 대한 복제 정책을 만듭니다. hello 정책이 적용 된 tooall hello 클라우드의 호스트에 있는 Vm입니다.
    - Hyper-V VM에 복제를 사용하도록 설정합니다. 초기 복제 hello 복제 정책 설정에 따라 발생합니다.
4. 데이터 변경 내용이 추적 됩니다 및 hello 초기 복제가 완료 된 후의 델타 복제 toobegins를 변경 합니다. .hrl 파일에는 항목에 대한 추적된 변경 내용이 유지됩니다.
5. 테스트 장애 조치 toomake 있는지를 실행 하면 모든 기능이 작동 합니다.

**그림 7: VMM tooVMM 복제**

![온-프레미스 tooon 온-프레미스](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>장애 조치 및 장애 복구

1. 온-프레미스 사이트 간에 계획된 또는 계획되지 않은 [장애 조치](site-recovery-failover.md)를 실행할 수 있습니다. 경우 계획된 된 장애 조치를 실행 한 후 원본 Vm이 tooensure 종료 데이터가 손실 되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md) tooorchestrate 여러 컴퓨터를 장애 조치 합니다.
4. Hello 보조 위치에서 장애 조치 컴퓨터 hello 후 계획 되지 않은 장애 조치 tooa 보조 사이트를 수행 하는 경우에 사용 되지 않도록 보호 또는 복제용으로 설정 합니다. Hello 장애 조치 후 계획된 된 장애 조치를 실행 한 경우 hello 보조 위치에서 컴퓨터 보호 됩니다.
5. 그런 다음 hello 장애 조치 toostart 액세스 hello 작업을 hello 복제본 VM에서에서 커밋합니다.
6. 기본 사이트를 사용할 수 있는 다시 역방향 복제 tooreplicate hello 보조 사이트 toohello 기본에서 시작 합니다. 역방향 복제 보호 된 상태로 가상 컴퓨터 hello 가져오지만 hello 보조 데이터 센터는 여전히 hello 활성 위치 합니다.
7. hello toomake hello 활성 위치에 기본 사이트를 다시 시작할 있습니다 보조 tooprimary, 다른 역방향 복제 뒤에서 계획된 된 장애 조치 합니다.


## <a name="next-steps"></a>다음 단계

- [자세한 내용은](site-recovery-hyper-v-azure-architecture.md) hello Hyper-v 복제 워크플로에 대 한 합니다.
- [필수 구성 요소 확인](site-recovery-prereq.md)
