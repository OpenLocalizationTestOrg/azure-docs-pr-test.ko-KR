---
title: "Azure tooAzure에서 복제에 대 한 사이트 복구 지원 매트릭스 aaaAzure | Microsoft Docs"
description: "재해 복구 (DR) 요구 사항에 대 한 한 지역 tooanother에서 hello 지원 운영 체제 및 Azure 가상 컴퓨터 (Vm)의 복제를 Azure Site Recovery에 대 한 구성 요약 되어 있습니다."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Azure tooAzure에서 복제에 대 한 azure 사이트 복구 지원 매트릭스


>[!NOTE]
>
> Azure Virtual Machines에 대한 Site Recovery 복제는 현재 미리 보기로 제공됩니다.

이 문서를 복제 하 고 하나의 영역 tooanother 지역에서 Azure 가상 컴퓨터를 복구 하는 경우 Azure Site Recovery에 대 한 지원 되는 구성 및 구성 요소를 요약 합니다.

## <a name="user-interface-options"></a>사용자 인터페이스 옵션

**사용자 인터페이스** |  **지원됨/지원되지 않음**
--- | ---
**Azure 포털** | 지원됨
**클래식 포털** | 지원되지 않음
**PowerShell** | 현재 지원되지 않음
**REST API** | 현재 지원되지 않음
**CLI** | 현재 지원되지 않음


## <a name="resource-move-support"></a>리소스 이동 지원

**리소스 이동 유형** | **지원됨/지원되지 않음** | **설명**  
--- | --- | ---
**리소스 그룹 간 자격 증명 모음 이동** | 지원되지 않음 |리소스 그룹에 걸쳐 hello 복구 서비스 자격 증명 모음을 이동할 수 없습니다.
**리소스 그룹 간에 계산, 저장소 및 네트워크 이동** | 지원되지 않음 |복제를 사용 하도록 설정한 후 가상 컴퓨터 (또는 예: 저장소 및 네트워크 관련된 구성 요소)를 이동 하는 경우 toodisable 복제 필요 하 고 hello 가상 컴퓨터에 대 한 복제를 다시 사용 하도록 설정 합니다.


## <a name="support-for-deployment-models"></a>배포 모델 지원

**배포 모델** | **지원됨/지원되지 않음** | **설명**  
--- | --- | ---
**클래식** | 지원됨 | 클래식 가상 컴퓨터는 복제한 후 클래식 가상 컴퓨터로 복구할 수만 있습니다. Resource Manager 가상 컴퓨터로는 복구할 수 없습니다. 클래식 가상 네트워크와 직접 Azure 지역 tooan 없이 VM을 배포 하는 경우 지원 되지 않습니다.
**리소스 관리자** | 지원됨 |

## <a name="support-for-replicated-machine-os-versions"></a>복제된 컴퓨터 운영 체제 버전에 대한 지원

운영 체제를 언급 hello에서 실행 중인 모든 작업에 대 한 지원 아래 hello 적용 됩니다.

#### <a name="windows"></a>Windows

- Windows Server 2016(Server Core 및 데스크톱 경험이 포함된 Server)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 SP1 이상

>[!NOTE]
>
> \* Windows Server 2016 Nano Server는 지원되지 않습니다.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Ubuntu 14.04 LTS 서버[(지원되는 커널 버전)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS 서버[(지원되는 커널 버전)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4 6.5 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3) 중 하나를 실행 합니다.
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> 인증 및 로그인을 기반으로 하는 암호를 사용 하 여 Ubuntu 서버 및 hello 클라우드 init 패키지 tooconfigure 클라우드 가상 컴퓨터를 사용 하는 암호 기반을 수도 있습니다 (hello cloudinit 구성 합니다.)에 따라 장애 조치 시 사용 하지 않도록 설정 하는 로그인 장애 조치 hello Azure 포털에서 가상 컴퓨터는 hello hello 지원 + 문제 해결 섹션) (아래 hello 설정 메뉴에서 hello 암호 다시 설정 하 여 암호 기반 로그인 hello 가상 컴퓨터에서 다시 설정할 수 있습니다.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Azure virtual Machines에 대해 지원되는 Ubuntu 커널 버전

**릴리스** | **모바일 서비스 버전** | **커널 버전** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-generic too3.13.0-117-일반,<br/>3.16.0-25-generic too3.16.0-77-일반,<br/>3.19.0-18-generic too3.19.0-80-일반,<br/>4.2.0-18-generic too4.2.0-42-일반,<br/>4.4.0-21-generic too4.4.0 75 제네릭이 |
14.04 LTS | 9.10 | 3.13.0-24-generic too3.13.0-121-일반,<br/>3.16.0-25-generic too3.16.0-77-일반,<br/>3.19.0-18-generic too3.19.0-80-일반,<br/>4.2.0-18-generic too4.2.0-42-일반,<br/>4.4.0-21-generic too4.4.0 81 제네릭이 |
16.04 LTS | 9.10 | 4.4.0-21-generic too4.4.0-81-일반,<br/>4.8.0-34-generic too4.8.0-56-일반,<br/>4.10.0-14-generic too4.10.0-24-일반 |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Linux OS를 실행하는 Azure Virtual Machines에서 지원되는 파일 시스템 및 게스트 저장소 구성

* 파일 시스템: ext3, ext4, ReiserFS(Suse Linux Enterprise Server만), XFS
* 볼륨 관리자: LVM2
* 다중 경로 소프트웨어: 장치 매퍼

## <a name="region-support"></a>지역 지원

복제 하 고 hello 내에서 모든 두 지역 간에 Vm을 복구할 수 같은 지리적 클러스터입니다.

**지리적 클러스터** | **Azure 지역**
-- | --
아메리카 | 캐나다 동부, 캐나다 중부, 미국 중남부, 미국 중서부, 미국 동부, 미국 동부 2, 미국 서부, 미국 서부 2, 미국 중부, 미국 중북부
유럽 | 영국 서부, 영국 남부, 북유럽, 유럽 서부
아시아 | 인도 남부, 인도 중부, 동남 아시아, 동아시아, 일본 동부, 일본 서부, 한국 중부, 한국 남부
오스트레일리아   | 오스트레일리아 동부, 오스트레일리아 남동부

>[!NOTE]
>
> 브라질 남쪽 영역에 대 한 복제만 수행 하 고 미국 중남부, 미국 서 부, 미국 동부, 미국 동부 2, 미국 서 부, 미국 서 부 2 North Central US 영역 및 실패의 장애 조치 tooone 백업.


## <a name="support-for-compute-configuration"></a>계산 구성 지원

**구성** | **지원됨/지원되지 않음** | **설명**
--- | --- | ---
크기 | CPU 코어가 2개 이상이고 1GB 이상의 RAM이 탑재된 모든 Azure VM | 너무 참조[Azure 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md)
가용성 집합 | 지원됨 | 포털에서 '사용 복제 단계 hello 기본 옵션을 사용 하는 경우 hello 가용성 집합은 자동 소스 영역 구성에 따라 만들어집니다. Hello 대상 가용성 집합을 변경할 수 있습니다 ' 복제 된 항목 > 설정 > 계산 및 네트워크 > 가용성 집합 ' 언제 든 지 합니다.
HUB(하이브리드 사용 혜택) VM | 지원됨 | Hello 원본 VM 사용 하도록 설정 하는 허브 라이선스가 있으면 hello 테스트 장애 조치 또는 VM 장애 조치는 또한 hello 허브 라이선스를 사용 합니다.
가상 컴퓨터 확장 집합 | 지원되지 않음 |
Azure 갤러리 이미지 - Microsoft 게시 | 지원됨 | Site Recovery에 의해 지원 되는 운영 체제에서 실행 되는 hello VM으로 지원 합니다.
Azure 갤러리 이미지 - 타사 게시 | 지원됨 | Site Recovery에 의해 지원 되는 운영 체제에서 실행 되는 hello VM으로 지원 합니다.
사용자 지정 이미지 - 타사 게시 | 지원됨 | Site Recovery에 의해 지원 되는 운영 체제에서 실행 되는 hello VM으로 지원 합니다.
Site Recovery를 사용하여 마이그레이션된 VM | 지원됨 | 경우 이므로/물리적 컴퓨터를 마이그레이션할 tooAzure Site Recovery를 사용 하 여, toouninstall hello 이전 버전의 모바일 서비스를 필요 하 고 tooanother Azure 지역 복제 하기 전에 hello 컴퓨터를 다시 시작 합니다.

## <a name="support-for-storage-configuration"></a>저장소 구성 지원

**구성** | **지원됨/지원되지 않음** | **설명**
--- | --- | ---
최대 OS 디스크 크기 | 1023GB | 너무 참조[Vm에서 사용 되는 디스크.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
최대 데이터 디스크 크기 | 1023GB | 너무 참조[Vm에서 사용 되는 디스크.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
데이터 디스크 수 | Azure VM 크기에 따라 최대 64개 지원 | 너무 참조[Azure 가상 컴퓨터 크기](../virtual-machines/windows/sizes.md)
임시 디스크 | 항상 복제에서 제외됨 | 임시 디스크는 항상 복제에서 제외됩니다. Azure 지침에 따라 임시 디스크에 영구 데이터를 저장해서는 안 됩니다. 너무 참조[Azure Vm에서 임시 디스크](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) 내용을 확인 합니다.
데이터 변경 률 hello 디스크에 | 디스크당 최대 6MBps | Hello 평균 데이터 변경 률에 6 MBps hello 디스크 지속적으로 벗어납니다, 그리고 복제 처리 하지 않습니다. 그러나 필요에 따른 데이터 버스트 이며 hello 데이터 변경 률 일정 시간 동안 6 MBps 보다 크면 및 관건은, 복제 catch 합니다. 이 경우 복구 지점이 약간 지연될 수 있습니다.
표준 저장소 계정의 디스크 | 지원됨 |
Premium Storage 계정의 디스크 | 지원됨 | 다른 대상 저장소 계정에 대 한 각 디스크 tooensure 있는 VM에 디스크를 프리미엄, 표준 저장소 계정의 경우 선택할 수 있습니다 hello 대상 영역에 동일한 저장소 구성
표준 Managed Disks | 지원되지 않음 |  
프리미엄 Managed Disks | 지원되지 않음 |
저장소 공간 | 지원됨 |         
미사용 암호화(SSE) | 지원됨 | 캐시 및 대상 저장소 계정에 대해 SSE 사용 저장소 계정을 선택할 수 있습니다.     
ADE(Azure Disk Encryption) | 지원되지 않음 |
디스크 핫 추가/제거 | 지원되지 않음 | 를 추가 하거나 hello VM에 데이터 디스크를 제거 하는 경우 toodisable 복제 필요 하 고 다시 hello VM에 대 한 복제를 사용 하도록 설정 합니다.
디스크 제외 | 지원되지 않음|   임시 디스크는 기본적으로 제외됩니다.
LRS | 지원됨 |
GRS | 지원됨 |
RA-GRS | 지원됨 |
ZRS | 지원되지 않음 |  
콜드 및 핫 저장소 | 지원되지 않음 | 가상 컴퓨터 디스크는 콜드 및 핫 저장소에서 지원되지 않습니다.

>[!IMPORTANT]
> Hello를 따라야 [는 저장소 지침도](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 소스 Azure 가상 컴퓨터가 tooavoid 모든 성능 문제에 대해 합니다. Hello 기본 설정을 수행 하는 경우 사이트 복구에 필요한 hello 저장소 계정은 hello 소스 구성에 따라 만들어집니다. 사용자 지정 설정을 직접을 선택 하는 경우 따라야 hello (... / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 원본 Vm으로 합니다.

## <a name="support-for-network-configuration"></a>네트워크 구성 지원
**구성** | **지원됨/지원되지 않음** | **설명**
--- | --- | ---
NIC(네트워크 인터페이스) | 특정 Azure VM 크기에서 지원되는 최대 NIC 수 | Nic는 hello VM 장애 조치 또는 테스트 장애 조치의 일부로 만들어질 때 생성 됩니다. hello Nic 개수 hello 장애 조치의 VM Nic hello 소스 VM 복제 활성화 hello 시에 hello 수에 따라 달라 집니다. 경우 하면 추가/제거 NIC 복제를 사용 하도록 설정한 후, hello 장애 조치 VM에서 NIC 개수 영향을 주지 않습니다.
인터넷 부하 분산 장치 | 지원됨 | Tooassociate 필요한 hello azure 자동화 스크립트를 사용 하 여 복구 계획에는 부하 분산 장치를 미리 구성 합니다.
내부 부하 분산 장치 | 지원됨 | Tooassociate 필요한 hello azure 자동화 스크립트를 사용 하 여 복구 계획에는 부하 분산 장치를 미리 구성 합니다.
공용 IP| 지원됨 | 기존 공용 IP toohello NIC tooassociate 필요 또는 하나 만들고 toohello NIC는 azure 자동화 스크립트를 사용 하 여 복구 계획에 연결 합니다.
NIC의 NSG(Resource Manager)| 지원됨 | Tooassociate hello NSG toohello NIC는 azure 자동화 스크립트를 사용 하 여 복구 계획에 필요 합니다.  
서브넷의 NSG(Resource Manager 및 클래식)| 지원됨 | Tooassociate hello NSG toohello NIC는 azure 자동화 스크립트를 사용 하 여 복구 계획에 필요 합니다.
VM의 NSG(클래식)| 지원됨 | Tooassociate hello NSG toohello NIC는 azure 자동화 스크립트를 사용 하 여 복구 계획에 필요 합니다.
예약된 IP(고정 IP)/원본 IP 유지 | 지원됨 | Hello hello 원본 VM에서 NIC에 고정 IP 구성 및 hello 대상 서브넷 장애 조치 toohello VM 할당 되어 사용할 수 있는 동일한 IP hello 했습니다. Hello 대상 서브넷 중 하나를 사용할 수 있는 동일한 IP의 사용 가능한 Ip hello hello 없으면 hello 서브넷이이 VM에 대 한 예약 되어 있습니다. '복제된 항목 > 설정 > 계산 및 네트워크 > 네트워크 인터페이스'에서 원하는 고정 IP를 지정할 수 있습니다. Hello NIC 선택한 hello 서브넷 및 IP를 지정 합니다.
동적 IP| 지원됨 | Hello hello 원본 VM에서 NIC에 동적 IP 구성이 있는 경우 hello hello 장애 조치에서 NIC VM은 또한 기본적으로 동적. '복제된 항목 > 설정 > 계산 및 네트워크 > 네트워크 인터페이스'에서 원하는 고정 IP를 지정할 수 있습니다. Hello NIC 선택한 hello 서브넷 및 IP를 지정 합니다.
Traffic Manager 통합 | 지원됨 | 미리 hello 트래픽이 라우트된 toohello 끝점 장애 조치 시 대상 지역에 정기적으로 및 toohello 끝점에서 소스 영역에 되는 방식으로 트래픽 관리자를 구성할 수 있습니다.
Azure 관리 DNS | 지원됨 |
사용자 지정 DNS  | 지원됨 |    
인증되지 않은 프록시 | 지원됨 | 너무 참조[네트워킹 지침 문서입니다.](site-recovery-azure-to-azure-networking-guidance.md)    
인증된 프록시 | 지원되지 않음 | VM hello를 사용 중인 경우 인증 된 프록시 아웃 바운드 연결에 대 한 Azure Site Recovery를 사용 하 여 복제할 수 없습니다.  
온-프레미스 (ExpressRoute 사용 또는) 사이트 tooSite VPN| 지원됨 | Hello UDRs 및 Nsg hello 사이트 복구 트래픽이 라우팅된 tooon 온-프레미스 아닌지 하는 방식으로 구성 되어 있는지 확인 합니다. 너무 참조[네트워킹 지침 문서입니다.](site-recovery-azure-to-azure-networking-guidance.md)  
VNET tooVNET 연결 | 지원됨 | 너무 참조[네트워킹 지침 문서입니다.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>다음 단계
- [Azure VM 복제를 위한 네트워킹 지침](site-recovery-azure-to-azure-networking-guidance.md)에 대해 자세히 알아보기
- [Azure VM을 복제](site-recovery-azure-to-azure.md)하여 워크로드 보호 시작
