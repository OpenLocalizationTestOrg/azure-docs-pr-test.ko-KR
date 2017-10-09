---
title: "Azure Site Recovery 온-프레미스 컴퓨터 복제 tooa 보조 온-프레미스 사이트 작업을 수행 하는 aaaHow? | Microsoft Docs"
description: "이 문서에서는 구성 요소 및 복제 온-프레미스 Vm 및 물리적 서버 hello Azure Site Recovery 서비스와 보조 사이트 tooa 때 사용 되는 아키텍처의 개요를 제공 합니다."
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
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>온-프레미스 사이트 복구에서 복제 tooa 보조 사이트 작업을 컴퓨터 하는 방법

이 문서에서는 hello 구성 요소를 설명 및 복제 하는 경우 관련 된 프로세스 온-프레미스 가상 컴퓨터 및 물리적 서버 tooAzure, hello를 사용 하 여 [Azure Site Recovery](site-recovery-overview.md) 서비스입니다.

Hello 다음 tooa 보조 온-프레미스 사이트를 복제할 수 있습니다.
- Site Recovery는 System Center VMM(Virtual Machine Manager)의 사용과 상관없이 관리되는 Hyper-V 클러스터 및 독립 실행형 호스트의 온-프레미스 Hyper-V VM
- 온-프레미스 VMware VM 및 Windows/Linux 물리적 서버 이 시나리오에서 복제는 Scout에 의해 관리됩니다.

Hello 또는이 문서의 hello 맨 아래에 모든 메모를 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Hyper-v Vm tooa 보조 온-프레미스 사이트를 복제 합니다.


### <a name="architectural-components"></a>아키텍처 구성 요소

Hyper-v Vm tooa 보조 사이트를 복제에 필요한 것 같습니다.

**구성 요소** | **위치** | **세부 정보**
--- | --- | ---
**Azure** | Microsoft에서는 계정이 필요합니다. |
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

**그림 1: VMM tooVMM 복제**

![온-프레미스 tooon 온-프레미스](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>장애 조치 및 장애 복구 프로세스

1. 온-프레미스 사이트 간에 계획된 또는 계획되지 않은 [장애 조치](site-recovery-failover.md)를 실행할 수 있습니다. 경우 계획된 된 장애 조치를 실행 한 후 원본 Vm이 tooensure 종료 데이터가 손실 되지 않습니다.
2. 단일 컴퓨터를 장애 조치할 하거나 만들 수 있습니다 [복구 계획](site-recovery-create-recovery-plans.md) tooorchestrate 여러 컴퓨터를 장애 조치 합니다.
4. Hello 보조 위치에서 장애 조치 컴퓨터 hello 후 계획 되지 않은 장애 조치 tooa 보조 사이트를 수행 하는 경우에 사용 되지 않도록 보호 또는 복제용으로 설정 합니다. Hello 장애 조치 후 계획된 된 장애 조치를 실행 한 경우 hello 보조 위치에서 컴퓨터 보호 됩니다.
5. 그런 다음 hello 장애 조치 toostart 액세스 hello 작업을 hello 복제본 VM에서에서 커밋합니다.
6. 기본 사이트를 사용할 수 있는 다시 역방향 복제 tooreplicate hello 보조 사이트 toohello 기본에서 시작 합니다. 역방향 복제 보호 된 상태로 가상 컴퓨터 hello 가져오지만 hello 보조 데이터 센터는 여전히 hello 활성 위치 합니다.
7. hello toomake hello 활성 위치에 기본 사이트를 다시 시작할 있습니다 보조 tooprimary, 다른 역방향 복제 뒤에서 계획된 된 장애 조치 합니다.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Vm/물리적 서버 tooa 보조 사이트를 복제 합니다.

VMware Vm 또는 이러한 아키텍처 구성 요소를 사용 하 여, InMage Scout를 사용 하 여 실제 서버 tooa 보조 사이트를 복제 합니다.


### <a name="architectural-components"></a>아키텍처 구성 요소

**구성 요소** | **위치** | **세부 정보**
--- | --- | ---
**Azure** | InMage Scout. | tooobtain InMage Scout를 Azure 구독이 필요 합니다.<br/><br/> 복구 서비스 자격 증명 모음을 만든 후 InMage Scout를 다운로드 하 고 hello 최신 업데이트 tooset hello 배포를 설치 합니다.
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

**그림 2: VMware tooVMware 복제**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>다음 단계

검토 hello [지원 매트릭스](site-recovery-support-matrix-to-sec-site.md)
