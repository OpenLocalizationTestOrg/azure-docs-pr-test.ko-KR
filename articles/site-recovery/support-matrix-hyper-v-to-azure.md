---
title: "Azure의 Hyper-V 복제용 지원 행렬 | Microsoft Docs"
description: "Azure Site Recovery를 통한 Azure로의 Hyper-V 복제에 지원되는 구성 요소 및 요구 사항의 요약 정보를 제공합니다."
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: article
ms.date: 12/31/2017
ms.author: raynew
ms.openlocfilehash: 5918c56c2b7d01c884bf846e3a7d621b3393bb96
ms.sourcegitcommit: 9ea2edae5dbb4a104322135bef957ba6e9aeecde
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2018
---
# <a name="support-matrix-for-hyper-v-replication-to-azure"></a>Azure로의 Hyper-V 복제용 지원 행렬


이 문서에서는 [Azure Site Recovery](site-recovery-overview.md) 서비스를 사용하여 온-프레미스 Hyper-V VM을 Azure로 재해 복구하는 데 지원되는 구성 요소와 설정의 요약 정보를 제공합니다.


## <a name="supported-scenarios"></a>지원되는 시나리오

**시나리오** | **세부 정보**
--- | --- 
**Hyper-V(VMM 포함)** | System Center VMM(Virtual Machine Manager) 패브릭에서 관리되는 Hyper-V 호스트에서 실행 중인 VM에 대해 Azure로의 재해 복구를 수행할 수 있습니다.<br/><br/> Azure Portal에서 또는 PowerShell을 사용하여 이 시나리오를 배포할 수 있습니다.<br/><br/> VMM에서 Hyper-V 호스트를 관리하는 경우에는 보조 온-프레미스 사이트로의 재해 복구도 수행할 수 있습니다. 이 시나리오에 대해 자세히 알아보려면 [이 문서](tutorial-vmm-to-vmm.md)의 내용을 확인하세요.
**VMM을 사용하지 않는 Hyper-V** | VMM에서 관리하지 않는 Hyper-V 호스트에서 실행 중인 VM에 대해 Azure로의 재해 복구를 수행할 수 있습니다.<br/><br/> Azure Portal에서 또는 PowerShell을 사용하여 이 시나리오를 배포할 수 있습니다. 


## <a name="on-premises-servers"></a>온-프레미스 서버

**서버** | **요구 사항** | **세부 정보**
--- | --- | ---
**VMM 없이 실행 중인 Hyper-V** | Windows Server 2016, 최신 업데이트가 포함된 Windows Server 2012 R2 | Site Recovery에서 Hyper-V 사이트를 구성하는 경우 Windows Server 2016과 2012 R2를 실행하는 호스트를 함께 포함할 수는 없습니다.<br/><br/> Windows Server 2016을 실행 중인 호스트에 있는 VM의 경우에는 대체 위치로의 복구가 지원되지 않습니다.
**VMM과 함께 실행 중인 Hyper-V** | VMM 2016, VMM 2012 R2 | VMM을 사용하는 경우 VMM 2016에서 Windows Server 2016 호스트를 관리해야 합니다.<br/><br/> Windows Server 2016 및 2012 R2를 실행하는 Hyper-V 호스트가 모두 포함된 VMM 클라우드는 현재 지원되지 않습니다.<br/><br/> 기존 VMM 2012 R2 서버에서 2016으로의 업그레이드를 포함하는 환경은 지원되지 않습니다.


## <a name="replicated-vms"></a>복제된 VM


다음 표에는 VM 지원 정보가 요약되어 있습니다. Site Recovery는 지원되는 운영 체제에서 실행되는 모든 워크로드를 지원합니다. 

 **구성 요소** | **세부 정보**
--- | ---
VM 구성 | Azure로 복제하는 VM은 [Azure 요구 사항](#failed-over-azure-vm-requirements)을 충족해야 합니다.
게스트 운영 체제 | [Azure에서 지원하는](https://technet.microsoft.com/library/cc794868.aspx) 모든 게스트 OS<br/><br/> Windows Server 2016 Nano Server는 지원되지 않습니다.




## <a name="hyper-v-network-configuration"></a>Hyper-V 네트워크 구성

**구성 요소** | **Hyper-V(VMM 포함)** | **VMM을 사용하지 않는 Hyper-V**
--- | --- | ---
호스트 네트워크:NIC 팀 | 예
호스트 네트워크:VLAN | 예
호스트 네트워크:IPv4 | 예
호스트 네트워크:IPv6 | 아니요
게스트 VM 네트워크:NIC 팀 | 아니요
게스트 VM 네트워크:IPv4 | 예
게스트 VM 네트워크:IPv6 | 아니요
게스트 VM 네트워크:고정 IP(Windows) | 예
게스트 VM 네트워크:고정 IP(Linux) | 아니오
게스트 VM 네트워크:다중 NIC | 예



## <a name="azure-vm-network-configuration-after-failover"></a>장애 조치(failover) 이후의 Azure VM 네트워크 구성

**구성 요소** | **Hyper-V(VMM 포함)** | **VMM을 사용하지 않는 Hyper-V**
--- | --- | ---
ExpressRoute | 예 | 예
ILB | 예 | 예
ELB | 예 | 예
Traffic Manager | 예 | 예
다중 NIC | 예 | 예
예약된 IP | 예 | 예
IPv4 | 예 | 예
원본 IP 주소 유지 | 예 | 예
VNET 서비스 끝점<br/><br/> (Azure Storage 방화벽 및 가상 네트워크) | 아니요 | 아니요


## <a name="hyper-v-host-storage"></a>Hyper-V 호스트 저장소

**Storage** | **Hyper-V(VMM 포함)** | VMM을 사용하지 않는 Hyper-V
--- | --- | --- | ---
NFS | 해당 없음 | 해당 없음
SMB 3.0 | 예 | 예
SAN(ISCSI) | 예 | 예
다중 경로(MPIO). 테스트에 사용된 소프트웨어:<br></br> Microsoft DSM, EMC PowerPath 5.7 SP4<br/><br/> EMC PowerPath DSM for CLARiiON | 예 | 예

## <a name="hyper-v-vm-guest-storage"></a>Hyper-V VM 게스트 저장소

**Storage** | **Hyper-V(VMM 포함)** | VMM을 사용하지 않는 Hyper-V
--- | --- | ---
VMDK | 해당 없음 | 해당 없음
VHD/VHDX | 예 | 예
2세대 VM | 예 | 예
EFI/UEFI| 예 | 예
공유 클러스터 디스크 | 아니요 | 아니요
암호화된 디스크 | 아니요 | 아니요
NFS | 해당 없음 | 해당 없음
SMB 3.0 | 아니오 | 아니요
RDM | 해당 없음 | 해당 없음
디스크 > 1TB | 예(최대 4095GB) | 예(최대 4095GB)
디스크: 4K 논리/실제 섹터 | 미지원: 1세대/2세대 | 미지원: 1세대/2세대
디스크: 4K 논리/512바이트 물리 섹터 | 예 |  예
스트라이프 디스크 포함 볼륨 > 1TB<br/><br/> LVM 논리 볼륨 관리 | 예 | 예
저장소 공간 | 예 | 예
디스크 핫 추가/제거 | 아니오 | 아니요
디스크 제외 | 예 | 예
다중 경로(MPIO) | 예 | 예

## <a name="azure-storage"></a>Azure 저장소

**구성 요소** | **Hyper-V(VMM 포함)** | **VMM을 사용하지 않는 Hyper-V**
--- | --- | ---
LRS | 예 | 예
GRS | 예 | 예
RA-GRS | 예 | 예
쿨 저장소 | 아니요 | 아니요
핫 저장소| 아니요 | 아니오
블록 Blob | 아니오 | 아니오
휴지 상태의 암호화(SSE)| 예 | 예
Premium Storage | 예 | 예
Import/Export 서비스 | 아니요 | 아니요
대상에서 복제 데이터에 사용되는 저장소 계정을 캐시하기 위한 VNET 서비스 끝점(Azure Storage 방화벽 및 VNET) | 아니요 | 아니오


## <a name="azure-compute-features"></a>Azure 계산 기능

**기능** | **Hyper-V(VMM 포함)** | **VMM을 사용하지 않는 Hyper-V**
--- | --- | ---
가용성 집합 | 예 | 예
HUB | 예 | 예  
관리 디스크 | 예 - 장애 조치(failover)용<br/><br/> 관리 디스크 장애 복구(failback)는 지원되지 않음 | 예 - 장애 조치(failover)용<br/><br/> 관리 디스크 장애 복구(failback)는 지원되지 않음

## <a name="azure-vm-requirements"></a>Azure VM 요구 사항

Azure로 복제하는 온-프레미스 VM은 이 표에 요약되어 있는 Azure VM 요구 사항을 충족해야 합니다.

**구성 요소** | **요구 사항** | **세부 정보**
--- | --- | ---
**게스트 운영 체제** | Site Recovery에서는 [Azure에서 지원](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx)하는 모든 운영 체제를 지원합니다.  | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**게스트 운영 체제 아키텍처** | 64비트 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**운영 체제 디스크 크기** | 1세대 VM의 경우 최대 2048GB<br/><br/> 2세대 VM의 경우 최대 300GB  | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**운영 체제 디스크 수** | 1 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**데이터 디스크 수** | 16개 이하  | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**데이터 디스크 VHD 크기** | 최대 4095GB | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**네트워크 어댑터** | 여러 어댑터가 지원됩니다. |
**공유 VHD** | 지원되지 않음 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**FC 디스크** | 지원되지 않음 | 지원되지 않는 경우 필수 구성 요소 확인이 실패합니다.
**하드 디스크 형식** | VHD  <br/><br/> VHDX | Azure로의 장애 조치(failover)를 수행하면 Site Recovery는 VHDX를 VHD로 자동 변환합니다. 온-프레미스에 장애 복구 시 가상 머신에서 계속해서 VHDX 형식을 사용합니다.
**Bitlocker** | 지원되지 않음 | VM의 복제를 사용하도록 설정하기 전에 Bitlocker를 사용하지 않도록 설정해야 합니다.
**VM 이름** | 1 자에서 63자 사이입니다. 문자, 숫자 및 하이픈으로 제한됩니다. VM 이름은 문자 또는 숫자로 시작하고 끝나야 합니다. | Site Recovery에서 VM 속성의 값을 업데이트합니다.
**VM 유형** | 1세대<br/><br/> 2세대 -- Windows | 기본 OS 디스크 형식이 있는 2세대 VM(VHDX로 포맷된 한 개 또는 두 개의 데이터 볼륨을 포함) 및 300GB 미만의 디스크 공간이 지원됩니다.<br></br>Linux 2세대 VM은 지원되지 않습니다. [자세히 알아보기](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="recovery-services-vault-actions"></a>Recovery Services 자격 증명 모음 작업

**작업** |  **Hyper-V(VMM 포함)** | **VMM을 사용하지 않는 Hyper-V**
--- | --- | --- 
리소스 그룹 간 자격 증명 모음 이동<br/><br/> 구독 내 및 구독 간 | 아니오 | 아니요 
저장소 그룹 간 저장소, 네트워크, Azure VM 이동<br/><br/> 구독 내 및 구독 간 | 아니요 | 아니요 


## <a name="provider-and-agent"></a>공급자 및 에이전트

배포가 이 문서에 나와 있는 설정과 호환되도록 하려면 최신 공급자 및 에이전트 버전을 실행 중인지 확인합니다.

**Name** | **설명** | **세부 정보**
--- | --- | --- | --- | ---
**Azure Site Recovery 공급자** | 온-프레미스 서버와 Azure 간 통신 조정 <br/><br/> VMM이 있는 Hyper-V: VMM 서버에 설치됨<br/><br/> VMM이 없는 Hyper-V: Hyper-V 호스트에 설치됨| 최신 버전: 5.1.2700.1(Portal에서 제공됨)<br/><br/> [최신 기능 및 수정](https://aka.ms/latest_asr_updates)
**MARS(Microsoft Azure Recovery Services) 에이전트** | Hyper-V VM과 Azure 간 복제 조정<br/><br/> 온-프레미스 Hyper-V 서버에 설치됨(VMM 서버 유무는 관계없음) | Portal에서 제공되는 최신 에이전트






## <a name="next-steps"></a>다음 단계
온-프레미스 Hyper-V VM 재해 복구용으로 [Azure를 준비](tutorial-prepare-azure.md)하는 방법을 알아봅니다. 
