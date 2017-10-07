---
title: "tooAzure 복제 하기 위한 aaaAzure 사이트 복구 지원 매트릭스 | Microsoft Docs"
description: "Azure Site Recovery에 대 한 hello 지원 운영 체제 및 구성 요소를 요약"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>온-프레미스 tooAzure에서 복제에 대 한 azure 사이트 복구 지원 매트릭스


이 문서를 복제 하 고 tooAzure를 복구 하는 경우 Azure Site Recovery에 대 한 지원 되는 구성 및 구성 요소를 요약 합니다. Azure 사이트 복구 요구 사항에 대 한 자세한 참조 hello [필수 구성 요소](site-recovery-prereq.md)합니다.


## <a name="support-for-deployment-options"></a>배포 옵션에 대한 지원

**배포웹사이트를** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)** |
--- | --- | ---
**Azure 포털** | 온-프레미스 네트워크와 Azure 리소스 관리자 또는 클래식 저장소와 VMware Vm tooAzure 저장소.<br/><br/> 장애 조치 tooResource 관리자 기반 또는 클래식 Vm입니다. | 온-프레미스 리소스 관리자 또는 클래식 저장소 및 네트워크와 Hyper-v Vm tooAzure 저장소.<br/><br/> 장애 조치 tooResource 관리자 기반 또는 클래식 Vm입니다.
**클래식 포털** | 유지 관리 모드에만 해당됩니다. 새 자격 증명 모음은 만들 수 없습니다. | 유지 관리 모드에만 해당됩니다.
**PowerShell** | 현재 지원되지 않습니다. | 지원됨


## <a name="support-for-datacenter-management-servers"></a>데이터 센터 관리 서버에 대한 지원

### <a name="virtualization-management-entities"></a>가상화 관리 엔터티

**배포웹사이트를** | **지원**
--- | ---
**VMware VM/물리적 서버** | vCenter 6.5, 6.0 또는 5.5
**Hyper-V(Virtual Machine Manager 있음)** | System Center Virtual Machine Manager 2016 및 System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Windows Server 2016 및 2012 R2 호스트가 혼합된 System Center Virtual Machine Manager 2016 클라우드는 현재 지원되지 않습니다.

### <a name="host-servers"></a>호스트 서버

**배포웹사이트를** | **지원**
--- | ---
**VMware VM/물리적 서버** | vSphere 6.5, 6.0, 5.5
**Hyper-V(Virtual Machine Manager 있음/없음)** | Windows Server 2016, 최신 업데이트가 포함된 Windows Server 2012 R2<br></br>SCVMM을 사용하는 경우 Windows Server 2016 호스트는 SCVMM 2016을 통해 관리되어야 합니다.


  >[!Note]
  >Windows Server 2016 및 2012 R2를 실행하는 호스트가 혼합된 Hyper-V 사이트는 현재 지원되지 않습니다. 복구 tooan 대체 위치 Vm에 대 한 Windows Server 2016 호스트에 현재 지원 되지 않습니다.

## <a name="support-for-replicated-machine-os-versions"></a>복제된 컴퓨터 운영 체제 버전에 대한 지원

보호 되는 가상 컴퓨터에서 충족 해야 [Azure 요구 사항](#failed-over-azure-vm-requirements) tooAzure를 복제 하는 경우.
다음 표에 hello Azure Site Recovery를 사용 하는 동안 다양 한 배포 시나리오에서 복제 된 운영 체제 지원을 요약 되어 있습니다. 이 지원은 운영 체제를 언급 hello에서 실행 중인 모든 작업에 대 한에 해당 합니다.

 **VMware/물리적 서버** | **Hyper-V(VMM 포함/제외)** |
--- | --- |
64비트 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1 이상<br/>*Windows Server 2016* - VMware 가상 컴퓨터 및 물리적 서버에서 현재 지원되지 않습니다. <br/><br/> Red Hat Enterprise Linux: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Cent OS: 5.2 too5.11, 6.1 too6.8, 7.0 too7.3 <br/><br/>Ubuntu 14.04 LTS 서버[(지원되는 커널 버전)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Ubuntu 16.04 LTS 서버[(지원되는 커널 버전)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4 6.5 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3) 중 하나를 실행 합니다. <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(SLES 11 SP3 tooSLES 11 s p 4에서에서 컴퓨터를 복제의 업그레이드가 지원 되지 않습니다. SLES 11SP3 tooSLES 11 s p 4에서에서 복제 된 컴퓨터를 업그레이드 한 경우 toodisable 복제 필요 하 고 합니다 hello 업그레이드 hello 컴퓨터를 다시 게시 보호.) | [Azure에서 지원하는](https://technet.microsoft.com/library/cc794868.aspx) 모든 게스트 OS


>[!IMPORTANT]
>(적용 가능한 tooVMware e/물리적 서버가 tooAzure 복제)
>
> Red Hat Enterprise Linux Server 7 이상 및 CentOS 7 이상 서버에서 커널 버전 3.10.0-514 9.8 hello Azure 사이트 복구 모바일 서비스의 버전에서부터 지원 됩니다.<br/><br/>
> 고객 hello 9.8 버전 보다 낮은 모바일 서비스의 버전과 hello 3.10.0-514 커널에 필요한 toodisable 복제, hello 이동성 서비스 tooversion 9.8의 업데이트 hello 버전 및 복제를 다시 사용 됩니다.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>VMware/물리적 서버에 대해 지원되는 Ubuntu 커널 버전

**릴리스** | **모바일 서비스 버전** | **커널 버전** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-generic too3.13.0-117-일반,<br/>3.16.0-25-generic too3.16.0-77-일반,<br/>3.19.0-18-generic too3.19.0-80-일반,<br/>4.2.0-18-generic too4.2.0-42-일반,<br/>4.4.0-21-generic too4.4.0 75 제네릭이 |
14.04 LTS | 9.10 | 3.13.0-24-generic too3.13.0-121-일반,<br/>3.16.0-25-generic too3.16.0-77-일반,<br/>3.19.0-18-generic too3.19.0-80-일반,<br/>4.2.0-18-generic too4.2.0-42-일반,<br/>4.4.0-21-generic too4.4.0 81 제네릭이 |
16.04 LTS | 9.10 | 4.4.0-21-generic too4.4.0-81-일반,<br/>4.8.0-34-generic too4.8.0-56-일반,<br/>4.10.0-14-generic too4.10.0-24-일반 |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>Linux(VMware/물리적 서버)에서 지원되는 파일 시스템 및 게스트 저장소 구성

hello 다음 파일 시스템 및 저장소 구성 소프트웨어는 VMware 또는 실제 서버에서 실행 중인 Linux 서버에서 지원 됩니다.
* 파일 시스템: ext3, ext4, ReiserFS(Suse Linux Enterprise Server만), XFS
* 볼륨 관리자: LVM2
* 다중 경로 소프트웨어: 장치 매퍼

반가상화된 저장 장치(반가상화된 드라이버에서 내보낸 장치)는 지원되지 않습니다.<br/>
다중 큐 블록 IO 장치는 지원되지 않습니다.<br/>
물리적 서버 hello HP CCISS 저장소 컨트롤러와 지원 되지 않습니다.<br/>

>[!Note]
> 디렉터리를 다음 Linux 서버 hello에 (경우 별도 파티션을/파일 시스템으로 설정) 모두 hello에 있어야 hello 원본 서버에서 동일한 디스크 (hello OS 디스크): / (응용 프로그램 루트), /boot, /usr, /usr/local, /var, /etc<br/><br/>
> 버전 9.10 hello 모바일 서비스의 시작 XFSv5 기능 메타 데이터 체크섬 등 XFS 파일 시스템에서 지원 됩니다. XFSv5 기능을 사용하는 경우 9.10 이상 버전의 모바일 서비스를 실행하고 있어야 합니다. Hello 파티션에 대 한 hello xfs_info 유틸리티 toocheck hello XFS 슈퍼 블록을 사용할 수 있습니다. Ftype too1 설정 되 면 XFSv5 기능이 사용 되 고 됩니다.
>


## <a name="support-for-network-configuration"></a>네트워크 구성 지원
다음 표에서 hello tooreplicate tooAzure Azure Site Recovery를 사용 하는 다양 한 배포 시나리오에서 네트워크 구성 지원을 요약 되어 있습니다.

### <a name="host-network-configuration"></a>호스트 네트워크 구성

**구성** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | ---
NIC 팀 | 예<br/><br/>물리적 컴퓨터가 복제되는 경우 지원되지 않음| 예
VLAN | 예 | 예
IPv4 | 예 | 예
IPv6 | 아니요 | 아니요

### <a name="guest-vm-network-configuration"></a>게스트 VM 네트워크 구성

**구성** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | ---
NIC 팀 | 아니요 | 아니요
IPv4 | 예 | 예
IPv6 | 아니요 | 아니요
고정 IP(Windows) | 예 | 예
고정 IP(Linux) | 예 <br/><br/>가상 컴퓨터 장애 복구에 구성 된 toouse DHCP입니다.  | 아니요
다중 NIC | 예 | 예

### <a name="failed-over-azure-vm-network-configuration"></a>장애 조치(Failover)된 Azure VM 네트워크 구성

**Azure 네트워킹** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | ---
Express 경로 | 예 | 예
ILB | 예 | 예
ELB | 예 | 예
트래픽 관리자 | 예 | 예
다중 NIC | 예 | 예
예약된 IP | 예 | 예
IPv4 | 예 | 예
원본 IP 유지 | 예 | 예


## <a name="support-for-storage"></a>저장소에 대한 지원
다음 표에서 hello tooreplicate tooAzure Azure Site Recovery를 사용 하는 다양 한 배포 시나리오에서 저장소 구성 지원을 요약 되어 있습니다.

### <a name="host-storage-configuration"></a>호스트 저장소 구성

**구성** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | --- | ---
NFS | VMware의 경우 예<br/><br/> 물리적 서버의 경우 아니요 | 해당 없음
SMB 3.0 | 해당 없음 | 예
SAN(ISCSI) | 예 | 예
다중 경로(MPIO)<br></br>테스트 제품: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM for CLARiiON | 예 | 예

### <a name="guest-or-physical-server-storage-configuration"></a>게스트 또는 물리적 서버 저장소 구성

**구성** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | ---
VMDK | 예 | 해당 없음
VHD/VHDX | 해당 없음 | 예
2세대 VM | 해당 없음 | 예
EFI/UEFI| 아니요 | 예
공유 클러스터 디스크 | 아니요 | 아니요
암호화된 디스크 | 아니요 | 아니요
NFS | 아니요 | 해당 없음
SMB 3.0 | 아니요 | 아니요
RDM | 예<br/><br/> 물리적 서버의 경우 해당 없음 | 해당 없음
디스크 > 1TB | 예<br/><br/>최대 4095GB | 예<br/><br/>최대 4095GB
4K 섹터 크기 디스크 | 예 | 예, 1세대 VM에 지원됨<br/><br/>2세대 VM에 지원되지 않음
스트라이프 디스크 포함 볼륨 > 1TB<br/><br/> LVM 논리 볼륨 관리 | 예 | 예
저장소 공간 | 아니요 | 예
디스크 핫 추가/제거 | 아니요 | 아니요
디스크 제외 | 예 | 예
다중 경로(MPIO) | 해당 없음 | 예

**Azure 저장소** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | ---
LRS | 예 | 예
GRS | 예 | 예
RA-GRS | 예 | 예
쿨 저장소 | 아니요 | 아니요
핫 저장소| 아니요 | 아니요
휴지 상태의 암호화(SSE)| 예 | 예
Premium Storage | 예 | 예
Import/Export 서비스 | 아니요 | 아니요


## <a name="support-for-azure-compute-configuration"></a>Azure 계산 구성에 대한 지원

**Compute 기능** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 있음/없음)**
--- | --- | --- 
가용성 집합 | 예 | 예
HUB | 예 | 예  
관리 디스크 | 예 | 예<br/><br/>장애 복구 tooon 온-프레미스에서 Azure VM 관리 되는 디스크와 현재 지원 되지 않습니다.

## <a name="failed-over-azure-vm-requirements"></a>장애 조치(Failover)된 Azure VM 요구 사항

사이트 복구 tooreplicate 가상 컴퓨터와 Azure에서 지원 되는 운영 체제를 실행 하는 물리적 서버를 배포할 수 있습니다. 여기에는 대부분 버전의 Windows 및 Linux가 포함됩니다. 온-프레미스의 Vm tooreplicate hello tooAzure를 복제 하는 동안 Azure 요구 사항 준수 해야 합니다.

**엔터티** | **요구 사항** | **세부 정보**
--- | --- | ---
**게스트 운영 체제** | Hyper-v tooAzure 복제: 사이트 복구 지원 되는 모든 운영 체제 [Azure에서 지 원하는](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx)합니다. <br/><br/> VMware와 실제 서버 복제: hello Windows 및 Linux 확인 [필수 구성 요소](site-recovery-vmware-to-azure-classic.md) | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**게스트 운영 체제 아키텍처** | 64비트 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**운영 체제 디스크 크기** | 복제 하는 경우 too2048 GB를 **VMware Vm 또는 실제 서버 tooAzure**합니다.<br/><br/>**Hyper-V 1세대** VM에 대해 최대 2048GB<br/><br/>**Hyper-V 2세대** VM에 대해 최대 300GB  | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**운영 체제 디스크 수** | 1 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**데이터 디스크 수** | 복제 하는 경우에 64 또는 **VMware Vm tooAzure**; 16 개이 복제 하는 경우 **tooAzure Hyper-v Vm** | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**데이터 디스크 VHD 크기** | Too4095 GB를 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**네트워크 어댑터** | 여러 어댑터가 지원됩니다. |
**공유 VHD** | 지원되지 않음 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**FC 디스크** | 지원되지 않음 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**하드 디스크 형식** | VHD  <br/><br/> VHDX | VHDX 현재 Azure에서 지원 되지 않음, 있지만 tooAzure 장애 조치할 때 Site Recovery가 자동으로 VHDX tooVHD 변환 합니다. 장애 복구 하는 경우 tooon 온-프레미스 hello 가상 컴퓨터가 계속 toouse hello VHDX 형식입니다.
**Bitlocker** | 지원되지 않음 | 가상 컴퓨터를 보호하기 전에 Bitlocker를 사용하지 않도록 설정해야 합니다.
**VM 이름** | 1 자에서 63자 사이입니다. 제한 된 tooletters, 숫자 및 하이픈입니다. hello VM 이름은 시작 하 고 문자 또는 숫자로 끝나야 합니다. | 사이트 복구에서 가상 컴퓨터 속성 hello hello 값을 업데이트 합니다.
**VM 유형** | 1세대<br/><br/> 2세대 -- Windows | 기본 OS 디스크 형식이 있는 2세대 VM(VHDX로 포맷된 한 개 또는 두 개의 데이터 볼륨을 포함) 및 300GB 미만의 디스크 공간이 지원됩니다.<br></br>Linux 2세대 VM은 지원되지 않습니다. [자세히 알아보기](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Recovery Services 자격 증명 모음 작업 지원

**작업** | **VMware/물리적 서버** | **Hyper-V(Virtual Machine Manager 없음)** | **Hyper-V(Virtual Machine Manager 있음)**
--- | --- | --- | ---
리소스 그룹 간 자격 증명 모음 이동<br/><br/> 구독 내 및 구독 간 | 아니요 | 아니요 | 아니요
저장소 그룹 간 저장소, 네트워크, Azure VM 이동<br/><br/> 구독 내 및 구독 간 | 아니요 | 아니요 | 아니요


## <a name="support-for-provider-and-agent"></a>공급자 및 에이전트에 대한 지원

**Name** | **설명** | **최신 버전** | **세부 정보**
--- | --- | --- | --- | ---
**Azure Site Recovery 공급자** | 온-프레미스 서버와 Azure 간 통신 조정 <br/><br/> Virtual Machine Manager 서버가 없는 경우 온-프레미스 Virtual Machine Manager 서버 또는 Hyper-V 서버에 설치 | 5.1.19([포털에서 사용 가능](http://aka.ms/downloaddra)) | [최신 기능 및 수정](https://support.microsoft.com/kb/3155002)
**Azure Site Recovery 통합 설치 (VMware tooAzure)** | 온-프레미스 VMware 서버와 Azure 간 통신 조정  <br/><br/> 온-프레미스 VMware 서버에 설치 | 9.3.4246.1(포털에서 사용 가능) | [최신 기능 및 수정](https://support.microsoft.com/kb/3155002)
**모바일 서비스** | 온-프레미스 VMware 서버/물리적 서버 및 Azure/보조 사이트 간 복제 조정<br/><br/> VMware VM 또는 실제 서버에 설치 된 원하는 tooreplicate  | 해당 없음(포털에서 사용 가능) | 해당 없음
**MARS(Microsoft Azure Recovery Services) 에이전트** | Hyper-V VM과 Azure 간 복제 조정<br/><br/> 온-프레미스 Hyper-V 서버에 설치(Virtual Machine Manager 서버 존재 여부는 관계 없음) | 최신 에이전트([포털에서 제공](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>다음 단계
[필수 구성 요소 확인](site-recovery-prereq.md)
