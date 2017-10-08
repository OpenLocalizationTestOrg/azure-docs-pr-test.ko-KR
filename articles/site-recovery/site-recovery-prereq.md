---
title: "Azure Site Recovery를 사용 하 여 복제 tooAzure에 대 한 aaaPrerequisites | Microsoft Docs"
description: "Vm 및 물리적 컴퓨터 tooAzure hello Azure Site Recovery 서비스를 사용 하 여 복제를 위한 hello 필수 구성 요소에 알아봅니다."
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>사이트 복구를 사용 하 여 온-프레미스 tooAzure에서 복제를 위한 필수 구성 요소

> [!div class="op_single_selector"]
> * [Azure tooAzure에서 복제](site-recovery-azure-to-azure-prereq.md)
> * [온-프레미스 tooAzure에서 복제](site-recovery-prereq.md)

Azure 사이트 복구의 Azure 가상 컴퓨터 (VM) tooanother Azure 지역 복제를 오케스트레이션 하 여 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 지원할 수 있습니다. 사이트 복구는 또한 온-프레미스 물리적 서버 및 Vm toohello 클라우드 (Azure) 또는 tooa 보조 데이터 센터에 복제합니다. 사용자는 기본 위치에서 시스템이 중단 된 경우 tooa 보조 위치 tookeep 앱 및 워크 로드에 사용할 수 있는 조치할 수 있습니다. 기본 위치 hello toonormal 작업 반환 될 때 뒤로 tooyour 기본 위치를 실패할 수 있습니다. Site Recovery에 대한 자세한 내용은 [Site Recovery란?](site-recovery-overview.md)을 참조하세요.

이 문서에서는 hello 온-프레미스 컴퓨터 tooAzure에서 사이트 복구 복제를 시작 하 고 필수 구성 요소에 요약 되어 있습니다.

Hello hello 문서 맨 아래에 모든 메모를 게시할 수 있습니다. 기술 관련 질문 hello에 요청할 수 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="azure-requirements"></a>Azure 요구 사항

**요구 사항** | **세부 정보**
--- | ---
**Azure 계정** | [Microsoft Azure 계정](http://azure.microsoft.com/). [평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다.
**Site Recovery 서비스** | Hello Azure Site Recovery 서비스에 대 한 가격에 대 한 자세한 내용은 참조 [사이트 복구 가격](https://azure.microsoft.com/pricing/details/site-recovery/)합니다. |
**Azure 저장소** | Azure 저장소 계정 복제 toostore 데이터가 있어야합니다. hello 저장소 계정은 hello에 있어야 hello와 같은 지역의 Azure 복구 서비스 자격 증명 모음입니다. 장애 조치(failover) 발생 시 Azure VM이 생성됩니다.<br/><br/> Hello 리소스 모델에 따라 원하는 toouse Azure VM 장애 조치에 대 한 hello를 사용 하 여 계정을 설정할 수 있습니다, [Azure 리소스 관리자 배포 모델](../storage/common/storage-create-storage-account.md) 또는 hello [클래식 배포 모델](../storage/common/storage-create-storage-account.md)합니다.<br/><br/>[지역 중복 저장소](../storage/common/storage-redundancy.md#geo-redundant-storage) 또는 로컬 중복 저장소를 사용할 수 있습니다. 지역 중복 저장소를 사용하는 것이 좋습니다. 지리적 중복 저장소와 데이터는 복원 력 있는 지역 가동 중단 발생 하는 경우 또는 기본 지역의 hello를 복구할 수 없는 경우입니다.<br/><br/> 표준 Azure Storage 계정을 사용하거나 Azure Premium Storage를 사용할 수 있습니다. [프리미엄 저장소](https://docs.microsoft.com/azure/storage/storage-premium-storage)는 일관된 I/O 고성능과 짧은 대기 시간이 요구되는 VM에 일반적으로 사용됩니다. 프리미엄 저장소를 사용하여 VM은 I/O 사용량이 많은 워크로드를 호스트할 수 있습니다. 복제된 데이터에 대해 프리미엄 저장소를 사용하는 경우 표준 저장소 계정도 필요합니다. 표준 저장소 계정이 가져갈 변화 들이 tooon 온-프레미스 데이터를 캡처하는 복제 로그를 저장 합니다.<br/><br/>
**저장소 제한** | 사이트 복구 tooa 다른 리소스 그룹에서 사용 하는 저장소 계정을 이동 하거나 tooor를 사용 하 여 다른 구독으로 이동할 수 없습니다.<br/><br/> 현재, 중앙 인도 및 남 인도 toopremium 저장소 계정 복제 사용할 수 없습니다.
**Azure 네트워크** | Azure 네트워크를 필요한 toowhich Azure Vm 장애 조치 후 연결 합니다. hello Azure 네트워크에에서 있어야 hello hello와 동일한 지역 복구 서비스 자격 증명 모음입니다.<br/><br/> Hello Azure 포털에서에서 Azure 네트워크 hello를 사용 하 여 만들 수 있습니다 [리소스 관리자 배포 모델](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) 또는 hello [클래식 배포 모델](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)합니다.<br/><br/> System Center Virtual Machine Manager (VMM) tooAzure에서 복제 하는 경우 VMM VM 네트워크와 Azure 네트워크 간에 네트워크 매핑을 설정 해야 합니다. 이렇게 하면 Azure Vm 장애 조치 후 tooappropriate 네트워크를 연결 합니다.
**네트워크 제한 사항** | 사이트 복구 tooa 다른 리소스 그룹에서 사용 하는 네트워크 계정을 이동 하거나 tooor를 사용 하 여 다른 구독으로 이동할 수 없습니다.
**네트워크 매핑** | VMM 클라우드에서 Microsoft Hyper-V VM을 복제하는 경우 네트워크 매핑을 설정해야 합니다. 이렇게 하면 장애 조치 후 처음 만들어질 때 Azure Vm tooappropriate 네트워크에 연결 하 합니다.

> [!NOTE]
> hello 다음 단원에서는 hello 고객 환경의 여러 구성 요소에 대 한 hello 필수 구성 요소. 특정 구성에 대 한 지원에 대 한 자세한 내용은 참조 hello [지원 매트릭스](site-recovery-support-matrix.md)합니다.
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>VMware Vm 또는 실제 Windows 또는 Linux 서버 tooAzure의 재해 복구
다음과 같은 구성 요소가 hello는 VMware Vm 또는 실제 Windows 또는 Linux 서버 재해 복구를 위해 필요 합니다. 이들은 toohello에 설명 된 것 뿐만 아니라 [Azure 요구 사항](#azure-requirements)합니다.


### <a name="configuration-server-or-additional-process-server"></a>구성 서버 또는 추가 프로세스 서버

온-프레미스 컴퓨터 hello 온-프레미스 사이트와 Azure 간 hello 구성 서버 tooorchestrate 통신으로 설정 합니다. 또한 온-프레미스 컴퓨터 hello 데이터 복제를 관리합니다. <br/></br>

*   **VMware vCenter 또는 vSphere 호스트 필수 조건**

    | **구성 요소** | **요구 사항** |
    | --- | --- |
    | **vSphere** | 하나 이상의 VMware vSphere 하이퍼바이저가 있어야 합니다.<br/><br/>하이퍼바이저 버전을 실행 해야 vSphere 6.0, 5.5, 또는 5.1 hello로 최신 업데이트.<br/><br/>VSphere 호스트 및 vCenter 서버 모두에서 hello 일 동일 네트워크 하 hello 프로세스 서버와는 것이 좋습니다. 전용된 프로세스 서버를 설정한 경우가 아니면 hello 구성 서버가 위치한 hello 네트워크입니다. |
    | **vCenter** | 배포 하는 VMware vCenter server toomanage vSphere 호스트 하는 것이 좋습니다. Hello 최신 업데이트로 vCenter 버전 6.0 또는 5.5를 실행 해야 합니다.<br/><br/>**제한**: Site Recovery는 vCenter vMotion 인스턴스 간의 복제를 지원하지 않습니다. 저장소 DRS 및 저장소 vMotion 역시 재보호 작업 후 마스터 대상 VM에서 지원되지 않습니다.||

* **복제된 컴퓨터 필수 조건**

    | **구성 요소** | **요구 사항** |
    | --- | --- |
    | **온-프레미스 컴퓨터(VMware VM)** | 복제된 VM에 VMware 도구가 설치되어 있고 실행 중이어야 합니다.<br/><br/> VM은 Azure VM을 만들기 위한 [Azure 필수 조건](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)을 충족해야 합니다.<br/><br/>각 보호된 컴퓨터에 디스크 용량이 1,023GB를 초과할 수 없습니다. <br/><br/>Hello 설치 드라이브에 사용 가능한 공간을 최소 2GB는 구성 요소 설치에 필요 합니다.<br/><br/>Tooenable 다중 VM 일관성을 원하는 경우 포트 20004 hello VM 로컬 방화벽에서 열어야 합니다.<br/><br/>컴퓨터 이름은 1-63자 길이(문자, 숫자 및 하이픈 사용 가능)여야 합니다. hello 이름은 문자 또는 숫자로 시작 하 고 문자 또는 숫자로 끝나야 합니다. <br/><br/>컴퓨터에서 복제를 사용 하도록 설정한 후 hello Azure 이름을 수정할 수 있습니다.<br/><br/> |
    | **Windows 컴퓨터**(물리적 또는 VMware) | hello 컴퓨터 하나를 실행 해야 지원 되는 hello 다음의 64 비트 운영 체제: <br/>- Windows Server 2012 R2<br/>- Windows Server 2012<br/>- Windows Server 2008 R2 SP1 이상 버전<br/><br/> hello 운영 체제 드라이브 C. hello OS 디스크에 설치 이어야 합니다 Windows 기본 디스크 및 동적 하지 않습니다. 데이터 디스크 hello 동적일 수 있습니다.<br/><br/>|
    | **Linux 컴퓨터**(물리적 또는 VMware) | hello 컴퓨터 하나를 실행 해야 지원 되는 hello 다음의 64 비트 운영 체제: <br/>- Red Hat Enterprise Linux 7.2, 7.1, 6.8 또는 6.7<br/>- Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 또는 6.5<br/>- Ubuntu 14.04 LTS 서버(Ubuntu용으로 지원되는 커널 버전 목록은 [지원되는 운영 체제](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) 참조)<br/>-Oracle Enterprise 6.5 또는 6.4 실행 되는 Linux 어느 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3)<br/>- SUSE Linux Enterprise Server 11 SP4 또는 SUSE Linux Enterprise Server 11 SP3<br/><br/>보호 된 컴퓨터의 /etc/hosts 파일에 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목이 있어야 합니다.<br/><br/>장애 조치 후 tooconnect tooan SSH (보안 셸) 클라이언트를 사용 하 여 Linux를 실행 중인 Azure VM을 하려는 경우 hello 보호 된 컴퓨터에서 SSH 서비스를 hello 설정 되어 있는지 확인 toostart 자동으로 시작 시 시스템에 있습니다. 또한, 방화벽 규칙 SSH 연결 toohello 보호 된 컴퓨터를 허용 하는지 확인 하십시오.<br/><br/>hello 호스트 이름, 탑재 지점, 장치 이름 및 Linux 시스템 경로 및 파일 이름 (예: /etc/ 및 /usr) 영어로 이어야 합니다.<br/><br/>다음 디렉터리 hello (경우 별도 파티션으로 설정 하거나 파일 시스템) 모두 hello에 있어야 hello 원본 서버에서 동일한 디스크 (hello OS 디스크):<br/>- / (root)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>현재, 메타데이터 체크섬과 같은 XFS v5 기능은 XFS 파일 시스템의 Site Recovery에 의해 지원되지 않습니다. XFS 파일 시스템이 v5 기능을 사용하고 있지 않은지 확인합니다. Hello 파티션에 대 한 hello xfs_info 유틸리티 toocheck hello XFS 슈퍼 블록을 사용할 수 있습니다. 경우 **ftype** 너무 설정**1**, XFS v5 기능이 사용 되는 합니다.<br/><br/>Red Hat Enterprise Linux 7 및 CentOS 7 서버의 hello lsof 유틸리티 설치 되었으며 사용 가능 이어야 합니다.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Hyper-v Vm tooAzure (VMM 없음)의 재해 복구

다음과 같은 구성 요소가 hello는 VMM 클라우드에서 Hyper-v Vm의 재해 복구를 위해 필요 합니다. 이들은 toohello에 설명 된 것 뿐만 아니라 [Azure 요구 사항](#azure-requirements)합니다.

| **필수 요소** | **세부 정보** |
| --- | --- |
| **Hyper-V 호스트** |하나 이상의 온-프레미스 서버 hello 최신 업데이트 및 사용 하도록 설정 하는 hello Hyper-v 역할 또는 Microsoft Hyper-v Server 2012 r 2와 Windows Server 2012 R2 실행 되어야 합니다.<br/><br/>Hyper-V 서버에 하나 이상의 VM이 있어야 합니다.<br/><br/>직접 또는 프록시를 통해 Hyper-v 서버에서 인터넷에 연결 된 toohello 이어야 합니다.<br/><br/>Hyper-v 서버 hello 기술 자료 문서에 설명 된 hello 수정 있어야 [2961977](https://support.microsoft.com/kb/2961977) 설치 합니다.
|**공급자 및 에이전트**| 사이트 복구를 배포 하는 동안 hello Azure Site Recovery provider를 설치합니다. hello 공급자 설치도 hello Azure 복구 서비스 에이전트를 설치 하려는 tooprotect Vm를 실행 하는 각 Hyper-v 서버에 있습니다. <br/><br/>자격 증명 모음에 있어야 하는 사이트 복구에서 모든 Hyper-v 서버 hello hello 공급자와 hello 에이전트의 버전과 동일 합니다.<br/><br/>hello 공급자가 hello 인터넷을 통해 tooconnect tooSite 복구 합니다. 트래픽은 직접 또는 프록시를 통해 보낼 수 있습니다. HTTPS 기반 프록시는 지원되지 않습니다. hello 프록시 서버에는 다음 Url 액세스 toohello를 허용 해야 합니다.<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Hello 서버에서 IP 주소를 기준으로 방화벽 규칙을 설정한 경우 hello 규칙 tooAzure 통신을 허용 하는지 확인 합니다.<br/><br/> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 및 HTTPS (포트 443).<br/><br/> Hello (액세스 제어 및 id 관리에 사용) 하는 미국 서 부 및 hello 구독의 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>VMM 클라우드 tooAzure의 Hyper-v Vm의 재해 복구

다음과 같은 구성 요소가 hello는 VMM 클라우드에서 Hyper-v Vm의 재해 복구를 위해 필요 합니다. 이들은 toohello에 설명 된 것 뿐만 아니라 [Azure 요구 사항](#azure-requirements)합니다.

| **필수 요소** | **세부 정보** |
| --- | --- |
| **Virtual Machine Manager** |System Center 2012 R2 이상 버전에서 실행되는 하나 이상의 VMM 서버가 있어야 합니다. 각 VMM 서버에 하나 이상의 클라우드가 구성되어 있어야 합니다. <br/><br/>클라우드에 다음 사항이 있어야 합니다.<br/>- 하나 이상의 VMM 호스트 그룹<br/>- 각 호스트 그룹에 있는 하나 이상의 Hyper-V 호스트 서버 또는 클러스터<br/><br/>VMM 클라우드 설정에 대 한 자세한 내용은 참조 [어떻게 toocreate Virtual Machine Manager 2012에서 클라우드](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx)합니다. |
| **Hyper-V** |Hyper-v 호스트 서버가 이상 실행 해야 hello Hyper-v 역할이 활성화 되어, 또는 Microsoft Hyper-v Server 2012 r 2와 Windows Server 2012 r 2입니다. hello 최신 업데이트를 설치 해야 합니다.<br/><br/> Hyper-V 서버에 하나 이상의 VM이 있어야 합니다.<br/><br/> VMM 클라우드에서 Hyper-v 호스트 서버 또는 Vm tooreplicate 원하는 포함 된 클러스터를 관리 되어야 합니다.<br/><br/>직접 또는 프록시를 통해 Hyper-v 서버에서 인터넷에 연결 된 toohello 이어야 합니다.<br/><br/>Hyper-v 서버 hello 기술 자료 문서에 설명 된 hello 수정 있어야 [2961977](https://support.microsoft.com/kb/2961977) 설치 합니다.<br/><br/>Hyper-v 호스트 서버에 데이터 복제 tooAzure에 대 한 인터넷 액세스가 필요 합니다. |
| **공급자 및 에이전트** |Azure 사이트 복구를 배포 하는 동안 hello VMM 서버에 Azure Site Recovery Provider를 설치 합니다. Hyper-V 호스트에 Recovery Services Agent를 설치합니다. hello 공급자 및 에이전트 hello 인터넷을 통해 직접 또는 프록시를 통해 tooconnect tooAzure 필요 합니다. HTTPS 기반 프록시는 지원되지 않습니다. hello VMM 서버와 Hyper-v 호스트에서 프록시 서버 hello에 대 한 액세스를 허용 해야 합니다. <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Hello VMM 서버에서 IP 주소를 기준으로 방화벽 규칙을 설정한 경우 hello 규칙 tooAzure 통신을 허용 하는지 확인 합니다.<br/><br/> Hello 허용 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653) 및 HTTPS (포트 443).<br/><br/>Hello hello 미국 서 부 (액세스 제어 및 id 관리에 사용) 및 구독에 대 한 Azure 지역에 대 한 IP 주소 범위를 허용 합니다.<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>복제된 컴퓨터 필수 조건

| **구성 요소** | **세부 정보** |
| --- | --- |
| **보호되는 VM** | Site Recovery에서는 [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx)에서 지원하는 모든 운영 체제를 지원합니다.<br/><br/>Vm hello를 충족 해야 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) Azure VM을 만들기 위한 합니다. 컴퓨터 이름은 1-63자 길이(문자, 숫자 및 하이픈 사용 가능)여야 합니다. hello 이름은 문자 또는 숫자로 시작 하 고 문자 또는 숫자로 끝나야 합니다. <br/><br/>Hello VM에 대 한 복제를 활성화 한 후 hello VM 이름을 수정할 수 있습니다. <br/><br/> 각 보호된 컴퓨터에 디스크 용량이 1,023GB를 초과할 수 없습니다. Too16 테라바이트) (위쪽 too16 디스크를 VM 있을 수 있습니다.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>VMM 클라우드 tooa 고객 소유의 사이트에 있는 Hyper-v Vm의 재해 복구

다음과 같은 구성 요소가 hello는 VMM 클라우드 tooa 고객 소유의 사이트에 있는 Hyper-v Vm의 재해 복구를 위해 필요 합니다. 이들은 toohello에 설명 된 것 뿐만 아니라 [Azure 요구 사항](#azure-requirements)합니다.

| **구성 요소** | **세부 정보** |
| --- | --- |
| **Virtual Machine Manager** |  Hello 기본 사이트와 hello 보조 사이트 모두에서 VMM 서버를 배포 하는 것이 좋습니다.<br/><br/> [단일 VMM 서버의 클라우드 간에 복제](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment)할 수 있습니다. 단일 VMM 서버에 클라우드 간의 tooreplicate, hello VMM 서버에 구성 하는 두 개 이상의 클라우드가 있어야 합니다.<br/><br/> VMM 서버를 하나 이상 실행 해야 hello 최신 업데이트로 System Center 2012 SP1.<br/><br/> 각 VMM 서버에 하나 이상의 클라우드가 포함되어 있어야 합니다. 모든 클라우드 hello Hyper-v 용량 프로필이 설정 해야 합니다. <br/><br/>클라우드에 하나 이상의 VMM 호스트 그룹이 있어야 합니다. VMM 클라우드 설정에 대한 자세한 내용은 [Azure Site Recovery 배포 준비](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)를 참조하세요. |
| **Hyper-V** | Hyper-v 서버 해야 이상을 실행 하 고 hello Hyper-v 역할과 Windows Server 2012 사용 하도록 설정 하 고 최신 업데이트가 설치 되어 hello 있어야 합니다.<br/><br/> Hyper-V 서버에 하나 이상의 VM이 있어야 합니다.<br/><br/>  Hyper-v 호스트 서버 hello 기본 및 보조 VMM 클라우드에 호스트 그룹에 있어야 합니다.<br/><br/> Windows Server 2012 r 2에서 클러스터에 Hyper-v를 실행 하는 경우 기술 자료 문서에 설명 된 hello 업데이트를 설치 하는 것이 좋습니다 [2961977](https://support.microsoft.com/kb/2961977)합니다.<br/><br/> Windows Server 2012의 클러스터에서 Hyper-V를 실행하는 경우 고정 IP 주소 기반 클러스터가 있으면 클러스터 브로커가 자동으로 만들어지지 않습니다. Hello 클러스터 브로커를 수동으로 구성 해야 합니다. Hello 클러스터 브로커에 대 한 자세한 내용은 참조 [클러스터 간 복제에 대 한 구성 hello 복제 브로커 역할](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx)합니다. |
| **공급자** | 사이트 복구를 배포 하는 동안 VMM 서버에 hello Azure Site Recovery provider를 설치 합니다. hello 공급자는 HTTPS (포트 443) tooorchestrate 복제 통해 Site Recovery와 통신합니다. 데이터 복제 hello 기본 및 보조 Hyper-v 서버 hello LAN 통해 또는 VPN 연결을 통해 간에 발생합니다.<br/><br/> hello VMM 서버에서 실행 되는 hello 공급자 toohello 다음 Url에 액세스할 필요:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>hello Site Recovery provider에서 VMM 서버 toohello hello 방화벽 통신을 허용 해야 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/confirmation.aspx?id=41653), 고 hello HTTPS (포트 443) 프로토콜을 허용 합니다. |


## <a name="url-access"></a>URL 액세스
VMware, VMM, Hyper-V 호스트 서버에서 이러한 URL을 사용할 수 있어야 합니다.

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **Hyper-v tooAzure** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | 허용 | 허용 | 허용 | 허용 |
|``*.backup.windowsazure.com`` | 필요하지 않음 | 허용 | 허용 | 허용 |
|``*.hypervrecoverymanager.windowsazure.com`` | 허용 | 허용 | 허용 | 허용 |
|``*.store.core.windows.net`` | 허용 | 허용 | 허용 | 허용 |
|``*.blob.core.windows.net`` | 필요하지 않음 | 허용 | 허용 | 허용 |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | 필요하지 않음 | 필요하지 않음 | 필요하지 않음 | SQL 다운로드 허용 |
|``time.windows.com`` | 허용 | 허용 | 허용 | 허용|
|``time.nist.gov`` | 허용 | 허용 | 허용 | 허용 |
