---
title: "Azure Site Recovery와 복제 tooa 보조 사이트에 대 한 aaaSupport 매트릭스 | Microsoft Docs"
description: "Azure Site Recovery에 대 한 hello 지원 운영 체제 및 구성 요소를 요약"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 0b2bbc86aff52308d5a90a56d7a3ff4286877740
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="support-matrix-for-replication-tooa-secondary-site-with-azure-site-recovery"></a>Azure Site Recovery와 복제 tooa 보조 사이트에 대 한 지원 매트릭스

이 문서는 Azure Site Recovery tooreplicate tooa 보조 온-프레미스 사이트를 사용할 때 지원 되는 옵션 요약 되어 있습니다.

## <a name="deployment-options"></a>배포 옵션

**배포웹사이트를** | **VMware/물리적 서버** | **Hyper-V(SCVMM 포함/제외)**
--- | --- | --- | ---
**Azure 포털** | 온-프레미스 VMware Vm toosecondary VMware 사이트입니다.<br/><br/> Hello 다운로드 [InMage Scout 사용자 가이드](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (hello Azure 포털에서에서 사용할 수 없음). | 온-프레미스 VMM 클라우드에 tooa 보조 VMM 클라우드의 Hyper-v Vm입니다.<br></br> VMM이 없으면 지원되지 않음  <br/><br/> 표준 Hyper-V 복제만 해당 SAN은 지원되지 않음
**클래식 포털** | 유지 관리 모드에만 해당됩니다. 새 자격 증명 모음은 만들 수 없습니다. | 유지 관리 모드에만 해당됩니다.<br></br> SCVMM이 없으면 지원되지 않음
**PowerShell** | 지원되지 않음 | 지원됨<br></br> SCVMM이 없으면 지원되지 않음

## <a name="on-premises-servers"></a>온-프레미스 서버

### <a name="virtualization-servers"></a>가상화 서버

**배포웹사이트를** | **지원**
--- | ---
**VMware VM/물리적 서버** | 최신 업데이트가 설치된 vSphere 6.0, 5.5 또는 5.1
**Hyper-V(VMM 포함)** | VMM 2016 및 VMM 2012 R2

  >[!Note]
  > Windows Server 2016 및 2012 R2 호스트가 혼합된 VMM 2016 클라우드는 현재 지원되지 않습니다.

### <a name="host-servers"></a>호스트 서버

**배포웹사이트를** | **지원**
--- | ---
**VMware VM/물리적 서버** | vCenter 5.5 또는 6.0(5.5 기능만 지원) 
**Hyper-V(VMM 없음)** | 지원 되는 구성 하지 tooa 보조 사이트를 복제 하기 위한
**Hyper-V(VMM 포함)** | Windows Server 2016 및 Windows Server 2012 r 2 hello 최신 업데이트.<br/><br/> Windows Server 2016 호스트는 VMM 2016에서 관리되어야 합니다.

## <a name="support-for-replicated-machine-os-versions"></a>복제된 컴퓨터 운영 체제 버전에 대한 지원
다음 표에 hello Azure Site Recovery를 사용 하는 동안 발생 하는 다양 한 배포 시나리오에서 운영 체제 지원이 요약 되어 있습니다. 이 지원은 운영 체제를 언급 hello에서 실행 중인 모든 작업에 대 한에 해당 합니다.

**VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
64비트 Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1 이상<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux 6.4 또는 6.5 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3)를 실행 합니다. <br/><br/> SUSE Linux Enterprise Server 11 SP3 | [Hyper-V에서 지원](https://technet.microsoft.com/library/mt126277.aspx)하는 모든 게스트 운영 체제

>[!Note]
>Linux 컴퓨터 저장소를 다음 hello로만 복제할 수 있습니다.: 파일 시스템 (EXT3, ETX4, ReiserFS, XFS); 다중 경로 소프트웨어 장치 매퍼; 볼륨 관리자 (l v m 2)입니다.
>HP CCISS 컨트롤러 저장소가 있는 물리적 서버는 지원되지 않습니다.
>hello ReiserFS 파일 시스템은 SUSE Linux Enterprise Server 11 s p 3에 대해서만 지원 됩니다.

## <a name="network-configuration"></a>네트워크 구성

### <a name="hosts"></a>호스트

**구성** | **VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
NIC 팀 | 예 | 예
VLAN | 예 | 예
IPv4 | 예 | 예
IPv6 | 아니요 | 아니요

### <a name="guest-vms"></a>게스트 VM

**구성** | **VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
NIC 팀 | 아니요 | 아니요
IPv4 | 예 | 예
IPv6 | 아니요 | 아니요
고정 IP(Windows) | 예 | 예
고정 IP(Linux) | 예 | 예
다중 NIC | 예 | 예


## <a name="storage"></a>저장소

### <a name="host-storage"></a>호스트 저장소

**저장소(호스트)** | **VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
NFS | 예 | 해당 없음
SMB 3.0 | 해당 없음 | 예
SAN(ISCSI) | 예 | 예
다중 경로(MPIO) | 예 | 예

### <a name="guest-or-physical-server-storage"></a>게스트 또는 물리적 서버 저장소

**구성** | **VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
VMDK | 예 | 해당 없음
VHD/VHDX | 해당 없음 | 예 (위쪽 too16 디스크)
2세대 VM | 해당 없음 | 예
공유 클러스터 디스크 | 예  | 아니요
암호화된 디스크 | 아니요 | 아니요
UEFI| 아니요 | 해당 없음
NFS | 아니요 | 아니요
SMB 3.0 | 아니요 | 아니요
RDM | 예 | 해당 없음
디스크 > 1TB | 아니요 | 예
스트라이프 디스크 포함 볼륨 > 1TB<br/><br/> LVM | 예 | 예
저장소 공간 | 아니요 | 예
디스크 핫 추가/제거 | 아니요 | 아니요
디스크 제외 | 아니요 | 예
다중 경로(MPIO) | 해당 없음 | 예

## <a name="vaults"></a>자격 증명 모음

**작업** | **VMware/물리적 서버** | **Hyper-V(VMM 포함)**
--- | --- | ---
리소스 그룹 간에 자격 증명 모음 이동(동일 구독 내 또는 구독 간에) | 아니요 | 아니요
리소스 그룹 간에 저장소, 네트워크, Azure VM 이동(동일 구독 내 또는 구독 간에) | 아니요 | 아니요

## <a name="provider-and-agent"></a>공급자 및 에이전트

**Name** | **설명** | **최신 버전** | **세부 정보**
--- | --- | --- | --- | ---
**Azure Site Recovery 공급자** | 온-프레미스 서버와 Azure 간 통신 조정 <br/><br/> 온-프레미스 VMM 서버에 설치, VMM 서버가 없는 경우 Hyper-V 서버에 설치 | 5.1.19([포털에서 사용 가능](http://aka.ms/downloaddra)) | [최신 기능 및 수정](https://support.microsoft.com/kb/3155002)
**모바일 서비스** | 온-프레미스 VMware 서버 또는 실제 서버와 hello 보조 사이트 간 복제를 조정<br/><br/> VMware VM 또는 tooreplicate 원하는 물리적 서버에 설치 된  | 해당 없음(포털에서 사용 가능) | 해당 없음


## <a name="next-steps"></a>다음 단계

- [VMM 클라우드 tooa 보조 사이트의 Hyper-v Vm 복제](site-recovery-vmm-to-vmm.md)
- [VMware Vm 및 물리적 서버 tooa 보조 사이트를 복제 합니다.](site-recovery-vmware-to-vmware.md)
