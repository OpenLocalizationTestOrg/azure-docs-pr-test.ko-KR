---
title: "aaaAzure 사이트 복구에 대 한 유용한 정보 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery 배포의 모범 사례를 설명합니다."
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Azure 사이트 복구 준비 toodeploy 가져오기

이 문서에서는 설명 어떻게 tooprepare Azure 사이트 복구 배포에 대 한 합니다.

## <a name="protecting-hyper-v-virtual-machines"></a>Hyper-V 가상 컴퓨터 보호  

몇 가지 배포 방법으로 Hyper-v 가상 컴퓨터를 보호할 수 있습니다. 온-프레미스 Vm 하이퍼 tooAzure 또는 tooa 보조 데이터 센터를 복제할 수 있습니다. 배포마다 요구 사항이 다릅니다.

**요구 사항** | **(VMM)과 tooAzure 복제** | **Hyper-v Vm tooAzure (VMM 없음)를 복제 합니다.** | **Hyper-v Vm toosecondary 사이트 (VMM)를 복제 합니다.** | **세부 정보**
---|---|---|---|---
**VMM** | System Center 2012 R2에서 실행되는 VMM <br/><br/>하나 이상의 VMM 호스트 그룹을 포함하는 하나 이상의 VMM 클라우드 | 해당 없음 | 이상에서 실행 중인 hello 기본 및 보조 사이트의 VMM 서버 최신 업데이트로 System Center 2012 SP1. <br/><br/> 각 VMM 서버에 클라우드가 하나 이상 있습니다. 클라우드 설정 hello Hyper-v 용량 프로필이 있어야 합니다.<br/><br/> hello 원본 클라우드의 VMM 호스트 그룹을 하나 이상 있어야 합니다. | 선택 사항입니다. 순서 tooreplicate Hyper-v 가상 컴퓨터 tooAzure에 배포 된 System Center VMM toohave 필요는 없지만 이렇게 하면 toomake hello VMM 서버 제대로 설정 되어 있는지 필요 합니다. 올바른 VMM 버전 hello 및 클라우드가 설정 되어 실행 하는 확인 포함 됩니다.
**Hyper-V** | Windows Server 2012 r 2를 실행 하는 hello 온-프레미스 사이트에서 하나 이상의 Hyper-v 호스트 서버 또는 이후 | Hyper-v 서버를 하나 이상 이상을 실행 하 고 hello 소스 및 대상 사이트에서 hello 최신 업데이트와 함께 Windows Server 2012를 설치 하 고 toohello를 연결 인터넷 합니다.<br/><br/> Hyper-v 서버 hello VMM 클라우드에 호스트 그룹에 있어야 합니다. | Hyper-v 서버를 하나 이상 이상을 실행 하 고 hello 소스 및 대상 사이트에서 hello 최신 업데이트와 함께 Windows Server 2012를 설치 하 고 toohello를 연결 인터넷 합니다.<br/><br/> hello Hyper-v 서버를 VMM 클라우드에 호스트 그룹에 있어야 합니다. |
**가상 컴퓨터** | Hello 원본 Hyper-v 호스트 서버에서 VM을 하나 이상 | Hello 원본의 v m M 클라우드 hello Hyper-v 호스트 서버에서 VM을 하나 이상 | Hello 원본의 v m M 클라우드 hello Hyper-v 호스트 서버에서 VM을 하나 이상 있습니다. |  Vm 복제 tooAzure Azure 가상 컴퓨터 필수 구성 요소를 준수 해야 합니다
**Azure 계정** | Azure 계정 및 구독 toohello Site Recovery 서비스를 필요 합니다. | Azure 계정 및 구독 toohello Site Recovery 서비스를 필요 합니다. | 해당 없음 | 계정이 없는 경우 무료 평가판으로 시작하세요.
**Azure 저장소** | 지역에서 복제가 활성화된 Azure 저장소 계정에 대한 구독이 필요합니다. | 지역에서 복제가 활성화된 Azure 저장소 계정에 대한 구독이 필요합니다. | 해당 없음 | hello hello Azure Site Recovery 자격 증명 모음과 동일한 지역 및 hello와 연결할 hello 계정에 있어야 동일한 구독 합니다.
**네트워킹** | 모든 컴퓨터에 장애 조치를 hello 동일한 Azure 네트워크는 네트워크 매핑 tooensure 설정 tooeach 기타에 복구 계획과 관계 없이 연결할 수 있습니다. 또한 네트워크 게이트웨이가 hello 대상 Azure 네트워크를 구성 하는 경우 가상 컴퓨터 tooother 온-프레미스 가상 컴퓨터를 연결할 수 있습니다. 설정 하지 않으면 같은 복구 계획에 연결할 수 있는 hello에 장애 조치 하는 컴퓨터만 매핑 네트워크입니다. | 해당 없음 |  <br/><br/>네트워크 매핑 tooensure 장애 조치 후 가상 컴퓨터는 연결 된 tooappropriate 네트워크 하 고 복제본 가상 컴퓨터가 Hyper-v 호스트 서버에 최적으로 배치 된를 설정 합니다. 네트워크를 구성 하지 않으면 복제 된 컴퓨터 매핑 장애 조치 후 연결 된 tooany VM 네트워크 수 없습니다. |  vmm이 네트워크 매핑을 tooset toomake VMM 논리 및 VM 네트워크 올바르게 구성 되어 있는지 필요 합니다.
**공급자 및 에이전트** | 배포 하는 동안 VMM 서버에 hello Azure Site Recovery Provider를 설치 합니다. VMM 클라우드의 Hyper-v 서버에 hello Azure 복구 서비스 에이전트를 설치 합니다. | 배포 중에 설치 hello Azure Site Recovery Provider 및 Azure 복구 서비스 에이전트 hello 모두 hello Hyper-v 호스트 서버 또는 클러스터| 배포 하는 동안 VMM 서버에 hello Azure Site Recovery Provider를 설치 합니다. VMM 클라우드의 Hyper-v 서버에 hello Azure 복구 서비스 에이전트를 설치 합니다. | 공급자 및 에이전트 연결 tooSite 복구 hello 통해 암호화 된 HTTPS 연결을 사용 하 여 인터넷 합니다. Tooadd 방화벽 예외를 필요 하지 않거나 hello 공급자 연결에 대 한 특정 프록시를 만듭니다.
**인터넷 연결** | Hello VMM 서버만 인터넷 연결이 필요 | Hello Hyper-v 호스트 서버에만 인터넷 연결이 필요 | VMM 서버만 인터넷 연결이 필요합니다. | 가상 컴퓨터에 설치 되어 항목이 필요 없습니다와 직접 연결 하지 않음 toohello 인터넷 합니다.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>VMware 가상 컴퓨터 또는 물리적 서버 보호

몇 가지 배포 방법으로 VMware 가상 컴퓨터 또는 Windows/Linux 물리적 서버를 보호할 수 있습니다. TooAzure, 또는 tooa 보조 데이터 센터에 복제할 수 있습니다. 배포마다 요구 사항이 다릅니다.

**요구 사항** | **복제 Vm/물리적 서버 tooAzure)** | * **Vm/물리적 서버 toosecondary 사이트 복제**  
---|---|---
**기본 사이트** | **프로세스 서버**: 전용 Windows 서버(실제 또는 가상) | **프로세스 서버**: 전용 Windows 서버(실제 또는 VMware 가상 컴퓨터)<br/><br/>  
**보조 온-프레미스 사이트** | 해당 없음 | **구성 서버**: 전용 Windows 서버(실제 또는 가상) <br/><br/> **마스터 대상 서버**: 전용 서버(실제 또는 가상) Windows tooprotect Windows 컴퓨터 또는 Linux tooprotect Linux로 구성 합니다.
**Azure** | **구독**: hello Site Recovery 서비스에 대 한 구독을 해야 합니다. <br/><br/> **저장소 계정**: 지역에서 복제를 사용하는 저장소 계정이 필요합니다. hello hello 사이트 복구 자격 증명 모음과 동일한 지역 및 hello와 연결할 hello 계정에 있어야 동일한 구독 합니다. <br/><br/> **구성 서버**: tooset Azure VM으로 hello 구성 서버를 구성 해야 합니다 <br/><br/> **마스터 대상 서버**: tooset hello 마스터 대상 서버는 Azure VM으로 구성 해야 합니다 <br/><br/> Windows tooprotect Windows 컴퓨터 또는 Linux tooprotect Linux로 구성 합니다.<br/><br/> **Azure 가상 네트워크**: 어떤 hello에 구성 서버 및 마스터 대상 서버 배포 될 Azure 가상 네트워크 필요 합니다. Hello에 것 같은 구독과 지역 hello Azure Site Recovery 자격 증명 모음 | 해당 없음  
**가상 컴퓨터/물리적 서버** | VMware 가상 컴퓨터 또는 물리적 Windows/Linux 서버가 하나 이상 필요합니다.<br/><br/>각 컴퓨터에 설치 됩니다 hello 모바일 서비스 배포 중| 하나 이상의 VMware VM 또는 물리적 Windows/Linux 서버.<br/><br/> 배포 하는 동안 hello 통합 에이전트가 각 컴퓨터에 설치 됩니다.




## <a name="azure-virtual-machine-requirements"></a>Azure 가상 컴퓨터 요구 사항

사이트 복구 tooreplicate 가상 컴퓨터와 Azure에서 지원 되는 운영 체제를 실행 하는 물리적 서버를 배포할 수 있습니다. 여기에는 대부분 버전의 Windows 및 Linux가 포함됩니다. 가 필요 합니다 toomake를 있는지 온-프레미스 tooprotect 가상 컴퓨터가 Azure 요구 사항을 준수 합니다.


## <a name="optimizing-your-deployment"></a>배포 최적화

다음 팁 toohelp 최적화 하 고 배포의 크기를 조정 하는 hello를 사용 합니다.

- **운영 체제 볼륨 크기**: 운영 체제 볼륨 가상 컴퓨터 tooAzure hello를 복제 하는 경우 1TB 미만 이어야 합니다. 수동으로 실행할 수 있습니다이 보다 더 많은 볼륨에 있는 경우 이동 tooa 다른 디스크 배포를 시작 하기 전에.
- **데이터 디스크 크기**: tooAzure too32 데이터 디스크를 최대 1TB의 각 가상 컴퓨터를 만들 수 있습니다를 복제 하는 경우. ~32 TB 가상 컴퓨터를 효과적으로 복제 및 장애 조치할 수 있습니다.
- **복구 계획 제한**: 사이트 복구에서 가상 컴퓨터의 toothousands를 확장할 수 있습니다. 복구 계획은 장애 조치 함께 hello 복구 계획 too50 컴퓨터 수가 제한 되어 있으므로 응용 프로그램에 대 한 모델으로 설계 되었습니다.
- **Azure 서비스 제한**: 모든 Azure 구독은 코어, 클라우드 서비스 등에 대한 일련의 기본 제한값이 제공됩니다. 구독에서 리소스의 테스트 장애 조치 toovalidate hello 가용성을 실행 하는 것이 좋습니다. Azure 지원을 통해 이러한 제한을 수정할 수 있습니다.
- **용량 계획**: 크기 조정 및 성능을 위한 계획입니다.
- **복제 대역폭**: 복제 대역폭이 부족한 경우 다음에 유의하십시오.
    - **Express 경로**: 사이트 복구는 Riverbed와 같은 Azure Express 경로 및 WAN 최적화 프로그램과 함께 작동합니다.
    - **복제 트래픽을**: 사용 하 여 사이트 복구만 데이터 블록을 사용 하 여 스마트 초기 복제를 수행 하 고 전체 VHD 하지 hello 합니다. 복제가 진행 중일 때는 변경 내용만 복제됩니다.
    - **네트워크 트래픽**: hello 대상 IP 주소 및 포트에 따라 정책을 사용 하 여 Windows QoS를 설정 하 여 복제에 사용 되는 네트워크 트래픽을 제어할 수 있습니다.  또한 tooAzure 사이트 복구를 복제 하는 경우 hello Azure 백업 에이전트를 사용 하 여 합니다. 해당 에이전트에 대한 제한을 구성할 수 있습니다.
- **RTO**: 테스트 장애 조치를 실행 하며 보기 hello 사이트 복구 작업 tooanalyze 시간 toocomplete hello 작업 제안 하려면 toomeasure hello 복구 시간 목표 (RTO)이 사이트 복구 될 수 있습니다. TooAzure를 통해 실패 한 경우 hello에 대 한 Azure 자동화 및 복구와 통합 하 여 모든 수동 작업을 자동화 하는 것이 좋습니다 최상의 RTO 계획입니다.
- **RPO**: tooAzure를 복제 하는 경우 사이트 복구 근처 동기 복구 지점 목표 (RPO)를 지원 합니다. 이때 데이터 센터와 Azure 사이에서 충분한 대역폭을 가정합니다.
