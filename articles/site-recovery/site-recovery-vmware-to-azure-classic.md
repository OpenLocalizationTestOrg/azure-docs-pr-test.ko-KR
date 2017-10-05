---
title: "클래식 포털에서 Azure에 VMware VM 및 물리적 서버 복제 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 배포하여 온-프레미스 VMware 가상 컴퓨터 및 Windows/Linux 물리적 서버에서 Azure로 복제, 장애 조치 및 복구를 오케스트레이션하는 방법에 대해 설명합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: 73c3fb5cf4056ddb9554f598ec7f173d81802f17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-to-azure-with-azure-site-recovery"></a>Azure Site Recovery를 사용하여 Azure에 VMware 가상 컴퓨터 및 물리적 서버 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmware-to-azure.md)
> * [클래식 포털](site-recovery-vmware-to-azure-classic.md)
> * [클래식 포털(레거시)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Azure Site Recovery 서비스는 가상 컴퓨터와 물리적 서버의 복제, 장애 조치 및 복구를 오케스트레이션하여 BCDR(비즈니스 연속성 및 재해 복구) 전략에 기여합니다. 컴퓨터는 Azure 또는 보조 온-프레미스 데이터 센터로 복제할 수 있습니다. 간략한 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)을 참조하세요.

## <a name="overview"></a>개요
이 문서에서는 다음과 같이 방법을 설명합니다.

* **Azure에 VMware 가상 컴퓨터 복제**: Site Recovery를 배포하여 온-프레미스 VMware 가상 컴퓨터에서 Azure 저장소로의 복제, 장애 조치, 복구를 조정합니다.
* **Azure에 물리적 서버 복제**: Azure Site Recovery를 배포하여 온-프레미스 물리적 Windows 및 Linux 서버에서 Azure로의 복제, 장애 조치, 복구를 조정합니다.

> [!NOTE]
> 이 문서에서는 Azure에 복제하는 방법을 설명합니다. VMware VM 또는 Windows/Linux 물리적 서버를 보조 데이터 센터에 복제하려면 [Site Recovery를 통해 VMware 간 복제](site-recovery-vmware-to-vmware.md)를 참조하세요.
>
>

이 문서의 하단 또는 [Azure Recovery Services 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)에서 의견이나 질문을 게시합니다.

## <a name="enhanced-deployment"></a>향상된 배포
이 문서는 Azure 클래식 포털의 향상된 배포에 대한 지침을 포함하고 있습니다. 새로운 모든 배포에 대해 이 버전을 사용하는 것이 좋습니다. 이전의 레거시 버전을 사용하여 이미 배포한 경우 새 버전으로 마이그레이션하는 것이 좋습니다. 마이그레이션에 대한 자세한 내용은 [Site Recovery를 통해 Azure 클래식 레거시에 VMware 복제](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment)를 참조하세요.

향상된 배포가 주요 업데이트입니다. 개선 사항에 대한 요약은 다음과 같습니다.

* **Azure에서 VM 인프라 없음**: Azure 저장소 계정에 데이터를 직접 복제합니다. 또한 레거시 배포에서 요구한 대로 복제 및 장애 조치를 위해 인프라 VM(예: 구성 서버 또는 마스터 대상 서버)을 설정할 필요가 없습니다.  
* **통합 설치**: 단일 설치는 온-프레미스 구성 요소에 대해 간단한 설정 및 확장성을 제공합니다.
* **안전한 배포**: 모든 트래픽이 암호화되고 복제 관리 통신이 HTTPS 443을 통해 전송됩니다.
* **복구 지점**: Windows 및 Linux 환경에 대한 크래시 일관성 및 응용 프로그램 일치 복구 지점을 지원하며, 단일 VM 및 여러 VM 일치 구성을 지원합니다.
* **테스트 장애 조치**: 프로덕션에 영향을 주거나 복제를 일시 중지하지 않고 Azure로의 무중단 테스트 장애 조치를 지원합니다.
* **계획되지 않은 장애 조치**: 장애 조치 이전에 VM을 자동으로 종료하는 향상된 옵션으로 Azure로의 계획되지 않은 장애 조치를 지원합니다.
* **장애 복구(failback)**: 온-프레미스 사이트에 대해 델타 변경만 복제하는 통합된 장애 복구입니다.
* **vSphere 6.0**: VMware vSphere 6.0 배포를 제한적으로 지원합니다.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>사이트 복구로 가상 컴퓨터 및 물리적 서버를 어떻게 보호할 수 있나요?
* VMware 관리자는 VMware 가상 컴퓨터에서 실행되는 응용 프로그램 및 비즈니스 워크로드에서 Azure를 보호하기 위해 오프사이트 보호를 구성할 수 있습니다. 서버 관리자는 물리적 온-프레미스 Windows 및 Linux 서버를 Azure에 복제할 수 있습니다.
* Azure Site Recovery 콘솔은 복제, 장애 조치(Failover), 복구 프로세스의 간단한 설정 및 관리를 위한 단일 위치를 제공합니다.
* vCenter Server에서 관리하는 VMware 가상 컴퓨터를 복제하는 경우 사이트 복구는 해당 VM을 자동으로 검색할 수 있습니다. 컴퓨터가 ESXi 호스트에 있는 경우 Site Recovery는 호스트에서 VM을 검색합니다.
* 온-프레미스 인프라에서 Azure로 손쉽게 장애 조치를 실행하면 Azure에서 온-프레미스 사이트의 VMware VM 서버로 장애 복구(복원)할 수 있습니다.
* 여러 컴퓨터에 계층화된 응용 프로그램 워크로드를 그룹화하는 복구 계획을 구성할 수 있습니다. 이러한 계획을 장애 조치하면 Site Recovery는 동일한 워크로드를 실행하는 컴퓨터를 일관된 데이터 지점으로 함께 복구할 수 있도록 다중 VM 일관성을 제공합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제
### <a name="windows-64-bit-only"></a>Windows(64비트만 해당)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux(64비트만 해당)
* Red Hat Enterprise Linux 6.7, 7.1 및 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 및 7.2
* Red Hat 호환 커널 또는 UEK3(Unbreakable Enterprise Kernel Release 3)을 실행하는 Oracle Enterprise Linux 6.4 및 6.5
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>시나리오 아키텍처
시나리오 구성 요소:

* **온-프레미스 관리 서버**: 사이트 복구 구성 요소를 실행하는 관리 서버:
  * **구성 서버**: 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.
  * **프로세스 서버**:복제 게이트웨이 역할을 합니다. 보호된 원본 컴퓨터에서 데이터를 받고, 캐싱, 압축 및 암호화를 사용하여 최적화하며, 복제 데이터를 Azure 저장소로 보냅니다. 또한 보호되는 컴퓨터에서 모바일 서비스의 푸시 설치를 처리하며 VMware VM의 자동 복구를 수행합니다.
  * **마스터 대상 서버**: Azure에서 장애 복구(failback) 중에 복제 데이터를 처리합니다.
    또한 프로세스 서버로만 작동하는 관리 서버를 배포하여 배포를 확장할 수도 있습니다.
* **모바일 서비스**: 이 구성 요소는 Azure에 복제하고자 하는 각 컴퓨터(VMware VM 또는 물리적 서버)에 배포됩니다. 컴퓨터에 기록된 데이터를 캡처하고 프로세스 서버에 전달합니다.
* **Azure**: 복제 및 장애 조치(Failover)를 처리하기 위해 어떤 Azure VM도 만들 필요가 없습니다. 사이트 복구 서비스가 데이터 관리를 처리하고 Azure 저장소로 데이터가 직접 복제됩니다. 복제된 Azure VM은 Azure로 장애 조치가 발생한 경우에만 자동으로 작동됩니다. 그러나 Azure에서 온-프레미스 사이트로 장애 복구하려면 Azure VM을 프로세스 서버로 작동하도록 설정해야 합니다.

다음 그래픽(Henry Robalino 작성)은 이러한 구성 요소가 상호 작용하는 방식을 보여 줍니다.

![구성 요소 아키텍처](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>용량 계획
용량을 계획하는 경우 고려해야 할 항목은 다음과 같습니다.

* **원본 환경**: 용량 계획 또는 VMware 인프라, 원본 컴퓨터 요구 사항
* **관리 서버**: Site Recovery 구성 요소를 실행하는 온-프레미스 관리 서버 계획
* **원본과 대상 간 네트워크 대역폭**: 원본과 Azure 간 복제에 필요한 네트워크 대역폭 계획

### <a name="source-environment-considerations"></a>원본 환경 고려 사항
* **일일 최대 변경률**: 보호된 컴퓨터는 하나의 프로세스 서버만 사용할 수 있습니다. 단일 프로세스 서버는 일일 최대 2TB의 데이터 변경을 처리할 수 있습니다. 따라서 2TB는 보호된 컴퓨터에 지원되는 최대 일일 데이터 변경률입니다.
* **최대 처리량**: 복제된 컴퓨터는 Azure에서 하나의 저장소 계정에 속할 수 있습니다. 표준 저장소 계정은 초당 최대 20,000개의 요청을 처리할 수 있으며 원본 컴퓨터 간에 IOPS 수를 20,000으로 유지하는 것이 좋습니다 예를 들어 원본 컴퓨터의 디스크가 5개이고 각 디스크가 원본에서 120IOPS(8KB 크기)를 생성하는 경우 Azure 디스크당 IOPS 제한인 500을 초과하지 않습니다. 필요한 저장소 계정 수 = 총 원본 IOPS/20,000

### <a name="management-server-considerations"></a>관리 서버 고려 사항
관리 서버는 데이터 최적화, 복제 및 관리를 처리하는 Site Recovery 구성 요소를 실행합니다. 보호된 컴퓨터에서 실행되는 모든 워크로드에서 일일 변경률 용량을 처리할 수 있어야 하며, 데이터를 Azure 저장소로 지속적으로 복제할 수 있을 만큼 충분한 대역폭이 있어야 합니다. 구체적으로 살펴보면 다음과 같습니다.

* 프로세스 서버는 보호된 컴퓨터에서 복제 데이터를 받고 캐싱, 압축 및 암호화를 사용하여 최적화한 후 Azure로 보냅니다. 관리 서버에는 이러한 작업을 수행할 충분한 리소스가 있어야 합니다.
* 프로세스 서버는 디스크 기반 캐시를 사용합니다. 네트워크 병목 현상 또는 중단이 발생하는 경우 저장된 데이터 변경을 처리할 수 있도록 600GB 이상의 별도의 캐시 디스크를 사용하는 것이 좋습니다. 배포 중에 5GB 이상의 저장소를 사용할 수 있는 드라이브에서 캐시를 구성할 수 있지만 600GB가 최소 권장 사항입니다.
* 가장 좋은 방법은 보호할 컴퓨터와 동일한 네트워크 및 LAN 세그먼트에 관리 서버를 배치하는 것입니다. 다른 네트워크에 있을 수 있지만 보호할 컴퓨터에서 L3 네트워크를 볼 수 있어야 합니다.

다음 표에는 관리 서버에 권장되는 크기가 요약되어 있습니다.

| **관리 서버 CPU** | **메모리** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- | --- |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) |16GB |300GB |500GB 이하 |이러한 설정으로 관리 서버를 배포하여 100개 미만의 컴퓨터를 복제합니다. |
| 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) |18GB |600GB |500GB ~ 1TB |이러한 설정으로 관리 서버를 배포하여 100-150개의 컴퓨터를 복제합니다. |
| 16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz) |32GB |1TB |1TB ~ 2TB |이러한 설정으로 관리 서버를 배포하여 150-200개의 컴퓨터를 복제합니다. |
| 다른 프로세스 서버 배포 | | |> 2TB |200대 이상의 컴퓨터를 복제하는 경우 또는 일일 데이터 변경률이 2TB를 초과하는 경우 추가 프로세스 서버를 배포합니다. |

여기서,

* 각 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.
* 캐시 디스크 측정을 위해 벤치마킹 저장소로 RAID 10을 이용한 10,000RPM의 8개 SAS 드라이브를 사용했습니다.

### <a name="network-bandwidth-from-source-to-target"></a>원본에서 대상까지 네트워크 대역폭
[Capacity Planner 도구](site-recovery-capacity-planner.md)를 사용하여 초기 복제 및 델타 복제에 필요한 대역폭을 계산해야 합니다.

#### <a name="throttling-bandwidth-used-for-replication"></a>복제에 사용되는 대역폭 제한
Azure에 복제되는 VMware 트래픽은 특정 프로세스 서버를 통해 전송됩니다. 다음과 같이 해당 서버에서 사이트 복구 복제에 사용할 수 있는 대역폭을 제한할 수 있습니다.

1. 주 관리 서버 또는 추가 프로비전된 프로세스 서버가 실행되는 관리 서버에서 Microsoft Azure 백업 MMC 스냅인을 엽니다. 기본적으로 Microsoft Azure Backup에 대한 바로 가기가 바탕 화면에 만들어집니다. 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin에서 찾을 수 있습니다.
2. 스냅인에서 **속성 변경**을 클릭합니다.

    ![대역폭 제한 속성 변경](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. **제한** 탭에서 Site Recovery 복제 및 적용 가능한 일정에 사용할 수 있는 대역폭을 지정합니다.

    ![복제 대역폭 제한](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

PowerShell을 사용하여 제한을 설정할 수도 있습니다. 예를 들면 다음과 같습니다.

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>대역폭 사용량 최대화
Azure Site Recovery에서 복제에 사용하는 대역폭을 늘리려면 레지스트리 키를 변경해야 합니다.

다음 키는 복제할 때 사용되는 복제 디스크당 스레드 수를 제어합니다.

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 과도하게 프로비전된 네트워크에서는 이 레지스트리 키를 기본값에서 변경해야 합니다. 지원되는 최대값은 32입니다.  

자세한 용량 계획에 대한 자세한 내용은 [Site Recovery Capacity Planner](site-recovery-capacity-planner.md)를 참조하세요.

### <a name="additional-process-servers"></a>추가 프로세스 서버
200개 이상의 컴퓨터를 보호해야 하거나 일일 변경률이 2TB를 초과하는 경우 추가 서버를 추가하여 해당 로드를 처리할 수 있습니다. 다음과 같이 규모를 확장할 수 있습니다.

* 관리 서버 수를 늘립니다. 예를 들어 두 관리 서버를 사용할 경우 최대 400개의 컴퓨터를 보호할 수 있습니다.
* 프로세스 서버를 더 추가하고 추가한 프로세스 서버를 사용하여 관리 서버 대신(또는 추가로) 트래픽을 처리할 수 있습니다.

다음 표에서는 이에 대한 시나리오를 설명합니다.

* 원래 관리 서버를 구성 서버로만 사용하도록 설정합니다.
* 추가 프로세스 서버를 설정합니다.
* 추가 프로세스 서버를 사용하도록 보호된 가상 컴퓨터를 구성합니다.
* 보호된 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.

| **원래 관리 서버**<br/><br/>(구성 서버) | **추가 프로세스 서버** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- | --- |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB RAM |4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB RAM |300GB |250GB 이하 |85개 이하의 컴퓨터를 복제할 수 있습니다. |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB RAM |8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB RAM |600GB |250GB ~ 1TB |85-150개의 컴퓨터를 복제할 수 있습니다. |
| 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 18GB RAM |12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB RAM |1TB |1TB ~ 2TB |150-225개의 컴퓨터를 복제할 수 있습니다. |

서버 크기를 조정하는 방법은 강화 모델 또는 규모 확장 모델에 대한 선호도에 따라 달라집니다. 몇 가지 고급 관리 서버 및 프로세스 서버를 배포하여 강화하거나 더 적은 리소스로 더 많은 서버를 배포하여 규모를 확장합니다. 예를 들어 220개 컴퓨터를 보호해야 하는 경우 다음 중 하나를 수행할 수 있습니다.

* 12개 vCPU와 18GB RAM을 갖춘 원래 관리 서버를 구성합니다. 12개 vCPU와 24GB RAM을 갖춘 추가 프로세스 서버를 구성합니다. 보호된 컴퓨터에서 추가 프로세스 서버만 사용하도록 구성합니다.
* 2개 관리 서버(2 x 8 vCPU, 16GB RAM)와 2개 추가 프로세스 서버(1 x 8 vCPU 및 1 x 4 vCPU: 135 + 85(220) 컴퓨터 처리)를 구성합니다. 보호된 컴퓨터에서 추가 프로세스 서버만 사용하도록 구성합니다.

[추가 프로세스 서버 배포](#deploy-additional-process-servers)의 지침에 따라 추가 프로세스 서버를 설정합니다.

## <a name="before-you-start-deployment"></a>배포를 시작하기 전에
다음 표에는 이 시나리오를 배포하기 위한 필수 조건이 요약되어 있습니다.

### <a name="azure-prerequisites"></a>Azure 필수 조건
| **필수 요소** | **세부 정보** |
| --- | --- |
| **Azure 계정** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. Site Recovery 가격 책정에 대한 자세한 내용은 [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)를 참조하세요. |
| **Azure 저장소** |복제된 데이터를 저장하려면 Azure 저장소 계정이 필요합니다. 복제된 데이터는 Azure 저장소에 저장되고, 장애 조치가 발생할 때 Azure VM이 작동합니다. <br/><br/>[표준 지역 중복 저장소 계정](../storage/storage-redundancy.md#geo-redundant-storage)이 필요합니다. 계정은 Site Recovery와 동일한 지역에 있고 동일한 구독과 연결되어 있어야 합니다. 프리미엄 저장소 계정으로의 복제는 현재 지원되지 않으며 사용할 수 없습니다.<br/><br/>[Azure Portal](../storage/storage-create-storage-account.md)을 사용하여 만든 저장소 계정의 리소스 그룹 간 이동은 지원하지 않습니다. 자세한 내용은 [Microsoft Azure Storage 소개](../storage/storage-introduction.md) 를 참조하세요.<br/><br/> |
| **Azure 네트워크** |장애 조치가 발생할 때 Azure VM에서 연결할 Azure 가상 네트워크가 필요합니다. Azure 가상 네트워크는 사이트 복구 자격 증명 모음과 같은 하위 지역에 있어야 합니다.<br/><br/>Azure로 장애 조치한 후에 장애 복구하려면 Azure 네트워크에서 온-프레미스 사이트로의 VPN 연결(또는 Azure ExpressRoute)을 설정해야 합니다. |

### <a name="on-premises-prerequisites"></a>온-프레미스 필수 조건
| **필수 요소** | **세부 정보** |
| --- | --- |
| **관리 서버** |가상 컴퓨터 또는 물리적 서버에서 실행되는 온-프레미스 Windows 2012 R2 서버가 필요합니다. 모든 온-프레미스 Site Recovery 구성 요소가 이 관리 서버에 설치됩니다.<br/><br/> 항상 사용 가능한 VMware VM으로 서버를 배포하는 것이 좋습니다. Azure에서 온-프레미스 사이트로 장애 복구(failback)는 VM 또는 물리적 서버 장애 조치에 관계없이 항상 VMware VM으로 이루어집니다. 관리 서버를 VMware VM으로 구성하지 않으면 장애 복구 트래픽을 받을 수 있도록 별도의 마스터 대상 서버를 VMware VM으로 설정해야 합니다.<br/><br/>서버는 도메인 컨트롤러일 수 없습니다.<br/><br/>서버에는 고정 IP 주소가 있어야 합니다.<br/><br/>서버의 호스트 이름은 15자 이내여야 합니다.<br/><br/>운영 체제 로캘은 영어여야 합니다.<br/><br/>관리 서버에는 인터넷 액세스가 필요합니다.<br/><br/>서버에서 아웃바운드 액세스가 필요합니다. 즉 MySQL을 다운로드하기 위한 Site Recovery 구성 요소 설치 시의 HTTP 80에 대한 임시 액세스, 복제를 관리하기 위한 HTTPS 443에서 진행 중인 아웃바운드 액세스 및 복제 트래픽을 위한 HTTPS 9443(이 포트는 수정할 수 있음)에서 진행 중인 아웃바운드 액세스가 필요합니다.<br/><br/> 관리 서버에서 다음 URL에 액세스할 수 있는지 확인합니다. <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [ https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>서버에 IP 주소 기반 방화벽 규칙이 있는 경우 해당 규칙이 Azure와의 통신을 허용하는지 확인합니다. [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653) 및 HTTPS(443) 포트를 허용해야 합니다. 또한 구독의 Azure 지역 및 미국 서부에 대한 IP 주소 범위를 허용 목록에 지정해야 합니다. URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi](https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")는 MySQL을 다운로드하기 위한 것입니다. |
| **VMware vCenter/ESXi 호스트** |최신 업데이트와 함께 ESX/ESXi 버전 6.0, 5.5 또는 5.1을 실행하고 VMware 가상 컴퓨터를 관리하는 VMware vSphere ESX/ESXi 하이퍼바이저가 하나 이상 필요합니다.<br/><br/> VMware vCenter 서버를 배포하여 ESXi 호스트를 관리하는 것이 좋습니다. 최신 업데이트와 함께 vCenter 버전 6.0 또는 5.5를 실행해야 합니다.<br/><br/>사이트 복구에서는 교차 vCenter vMotion, 가상 볼륨 및 저장소 DRS와 같은 새로운 vCenter 및 vSphere 6.0 기능을 지원하지 않습니다. 사이트 복구 지원은 버전 5.5에서도 사용할 수 있는 기능에 제한됩니다. |
| **보호된 컴퓨터** |**Azure**<br/><br/>보호할 컴퓨터는 Azure VM을 만들기 위한 [Azure 필수 조건](site-recovery-prereq.md)을 충족해야 합니다.<br><br/>장애 조치 후 Azure VM에 연결하려면 로컬 방화벽에서 원격 데스크톱 연결을 사용하도록 설정해야 합니다.<br/><br/>보호되는 컴퓨터의 개별 디스크 용량이 1023GB 이하여야 합니다. VM은 최대 64개의 디스크(따라서 최대 64TB)를 포함할 수 있습니다. 1TB보다 큰 디스크가 있는 경우 SQL Server AlwaysOn 또는 Oracle Data Guard와 같은 데이터베이스 복제를 사용하는 것이 좋습니다.<br/><br/>구성 요소 설치를 위해 설치 드라이브에 최소 2GB의 사용 가능한 공간이 있어야 합니다.<br/><br/>공유 디스크 게스트 클러스터는 지원되지 않습니다. 클러스터형 배포를 사용하는 경우 SQL Server AlwaysOn 또는 Oracle Data Guard와 같은 데이터베이스 복제를 사용하는 것이 좋습니다.<br/><br/>UEFI(Unified Extensible Firmware Interface)/EFI(Extensible Firmware Interface) 부팅은 지원되지 않습니다.<br/><br/>컴퓨터 이름은 1-63자(문자, 숫자 및 하이픈)를 포함해야 합니다. 이름은 문자나 숫자로 시작하고 문자나 숫자로 끝나야 합니다. 컴퓨터가 보호된 후에는 Azure 이름을 수정할 수 있습니다.<br/><br/>**VMware VM**<br/><br>VMware vSphere PowerCLI 6.0을 설치해야 합니다. 관리 서버(구성 서버)에 설치해야 합니다.<br/><br/>보호하려는 VMware VM에는 VMware 도구가 설치되어 있고 실행 중이어야 합니다.<br/><br/>원본 VM에서 NIC 팀을 사용하는 경우 Azure로 장애 조치한 후 단일 NIC로 변환됩니다.<br/><br/>보호된 VM에 iSCSI 디스크가 있는 경우 VM을 Azure로 장애 조치할 때 Site Recovery는 보호된 VM iSCSI 디스크를 VHD 파일로 변환합니다. Azure VM에서 iSCSI 대상에 연결할 수 있는 경우 iSCSI 대상에 연결하며 기본적으로 두 개의 디스크, 즉 Azure VM VHD 디스크 및 원본 iSCSI 디스크가 표시됩니다. 이 경우 장애 조치된 Azure VM에 표시되는 iSCSI 대상의 연결을 끊어야 합니다.<br/><br/>Site Recovery에 필요한 VMware 사용자 권한에 대한 자세한 내용은 [vCenter 액세스를 위한 VMware 권한](#vmware-permissions-for-vcenter-access)을 참조하세요.<br/><br/> **VMware VM 또는 물리적 서버의 Windows Server 컴퓨터**<br/><br/>서버는 지원되는 64비트 운영 체제(Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 R2 SP1 이상)를 실행해야 합니다.<br/><br/>운영 체제는 C 드라이브에 설치해야 하며, OS 디스크는 Windows 기본 디스크여야 합니다. (Windows 동적 디스크에 OS를 설치하면 안됩니다.)<br/><br/>Windows Server 2008 R2 컴퓨터의 경우 .NET Framework 3.5.1이 설치되어 있어야 합니다.<br/><br/>Windows 서버에 모바일 서비스를 강제 설치하려면 관리자 계정(Windows 컴퓨터의 로컬 관리자여야 함)을 제공해야 합니다. 제공된 관리자 계정이 도메인 계정이 아닌 경우 로컬 컴퓨터에서 원격 사용자 액세스 제어를 사용하지 않도록 설정해야 합니다. 자세한 내용은 [강제 설치로 모바일 서비스 설치](#install-the-mobility-service-with-push-installation)를 참조하세요.<br/><br/>Site Recovery에서는 RDM 디스크를 사용한 VM을 지원합니다. 장애 복구 시 원래 원본 VM과 RDM 디스크를 사용할 수 있는 경우 Site Recovery에서 RDM 디스크를 다시 사용합니다. 장애 복구 시 사용할 수 없는 경우 Site Recovery에서 각 디스크에 대한 새 VMDK 파일을 만듭니다.<br/><br/>**Linux 컴퓨터**<br/><br/>Red Hat Enterprise Linux 6.7, Centos 6.5, 6.6 또는 6.7, Red Hat 호환 커널 또는 UEK3(Unbreakable Enterprise Kernel Release 3)을 실행하는 Oracle Enterprise Linux 6.4 또는 6.5, SUSE Linux Enterprise Server 11 SP3 등의 지원되는 64비트 운영 체제가 필요합니다.<br/><br/>다음 저장소의 Linux 컴퓨터에 대해서만 보호를 사용할 수 있습니다. <br/><br/>장애 조치 후에 ssh(보안 셸) 클라이언트를 사용하여 Linux를 실행하는 Azure 가상 컴퓨터에 연결하려면 시스템 부팅 시 보호된 컴퓨터의 보안 셸 서비스를 자동으로 시작하도록 설정되어 있는지 및 방화벽 규칙에서 ssh 연결을 허용하는지 확인합니다.<br/><br/>보호는 파일 시스템(EXT3, ETX4, ReiserFS, XFS), 다중 경로 소프트웨어-장치 매퍼(multipath), 볼륨 관리자(LVM2) 등의 저장소를 포함한 Linux 컴퓨터에만 사용하도록 설정할 수 있습니다. HP CCISS 컨트롤러 저장소가 있는 물리적 서버는 지원되지 않습니다. ReiserFS 파일 시스템은 SUSE Linux Enterprise Server 11 SP3에서만 지원됩니다.<br/><br/>Site Recovery에서는 RDM 디스크를 사용한 VM을 지원합니다. Linux에 대한 장애 복구(failback) 중에는 사이트 복구에서 RDM 디스크를 다시 사용하지 않습니다. 대신 해당 RDM 디스크마다 새 VMDK 파일을 만듭니다. |

Linux VM인 경우에만 VMware의 VM 구성 매개 변수에서 disk.enableUUID=true로 설정합니다. 이 행이 존재하지 않는 경우 추가합니다. 올바르게 탑재할 수 있도록 VMDK에 일관성 있는 UUID를 제공해야 합니다. 이 설정을 사용하지 않으면 VM을 온-프레미스에서 사용할 수 있는 경우에도 장애 복구에서 전체 다운로드가 발생합니다. 이 설정을 추가하면 장애 복구 중에 델타 변경만 다시 보냅니다.

## <a name="step-1-create-a-vault"></a>1단계: 자격 증명 모음 만들기
1. [Azure 포털](https://manage.windowsazure.com/)에 로그인합니다.
2. **Data Services** > **Recovery Services**를 확장하고 **Site Recovery 자격 증명 모음**을 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**에 자격 증명 모음을 식별하기 위한 이름을 입력합니다.
5. **지역**에서 자격 증명 모음에 대한 지리적 지역을 선택합니다. 지원되는 지역을 확인하려면 [Azure Site Recovery 가격 책정 세부 정보](https://azure.microsoft.com/pricing/details/site-recovery/)를 참조하세요.
6. **자격 증명 모음 만들기**를 클릭합니다.
    ![자격 증명 모음 만들기](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

상태 표시줄을 점검하여 자격 증명 모음이 성공적으로 만들어졌는지 확인합니다. 자격 증명 모음은 기본 **Recovery Services** 페이지에서 **활성** 으로 나열됩니다.

## <a name="step-2-set-up-an-azure-network"></a>2단계: Azure 네트워크 설정
장애 조치(Failover) 후 Azure VM이 네트워크에 연결되고 온-프레미스 사이트로 장애 복구(failback)가 예상대로 작동할 수 있도록 Azure 네트워크를 설정합니다.

1. Azure Portal에서 **가상 네트워크 만들기**를 선택하고 네트워크 이름, IP 주소 범위 및 서브넷 이름을 지정합니다.
2. 장애 복구를 수행해야 하는 경우 네트워크에 VPN/ExpressRoute를 추가합니다. 장애 조치(Failover) 후에도 VPN/Express 경로를 네트워크에 추가할 수 있습니다.

Azure 네트워크에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.

> [!NOTE]
> 같은 구독 내에 있거나 여러 구독에 있는 리소스 그룹에 대한 [네트워크의 마이그레이션](../azure-resource-manager/resource-group-move-resources.md)은 Site Recovery를 배포하는 데 사용되는 네트워크에 지원되지 않습니다.
>
>

## <a name="step-3-install-the-vmware-components"></a>3단계: VMware 구성 요소 설치
VMware 가상 컴퓨터를 복제하려면 관리 서버에서 다음 단계를 수행합니다.

1. [다운로드](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) 하여 설치합니다.
2. 서버를 다시 시작합니다.

## <a name="step-4-download-a-vault-registration-key"></a>4단계: 자격 증명 모음 등록 키 다운로드
1. 관리 서버에서 Azure의 Site Recovery 콘솔을 엽니다. **Recovery Services** 페이지에서 자격 증명 모음을 클릭하여 **빠른 시작** 페이지를 엽니다. 또한 해당 아이콘을 클릭하여 언제든지 **빠른 시작** 페이지를 열 수도 있습니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. **빠른 시작** 페이지에서 **대상 리소스 준비** > **등록 키 다운로드**를 차례로 클릭합니다. 등록 파일이 자동으로 생성됩니다. 이 파일은 생성 후 5일 동안 유효합니다.

## <a name="step-5-install-the-management-server"></a>5단계: 관리 서버 설치
> [!TIP]
> 관리 서버에서 다음 URL에 액세스할 수 있는지 확인합니다.
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. **빠른 시작** 페이지에서 통합 설치 파일을 서버로 다운로드합니다.
2. 설치 파일을 실행하여 **Site Recovery 통합 설치** 마법사에서 설치를 시작합니다.
3. **시작하기 전에**에서 **구성 서버 및 프로세스 서버 설치**를 선택합니다.

   ![시작하기 전에](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. **타사 소프트웨어 라이선스**에서 **동의함**을 클릭하고 MySQL을 다운로드 및 설치합니다.

    ![타사 소프트웨어](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. **등록**에서 자격 증명 모음에서 다운로드한 등록 키를 찾아 선택합니다.

    ![등록](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. **인터넷 설정**에서 구성 서버에서 실행 중인 공급자가 인터넷을 통해 Azure Site Recovery에 연결하는 방법을 지정합니다.

   * 현재 컴퓨터에 설정된 프록시를 사용하여 연결하려면 **기존 프록시 설정을 사용하여 연결**을 선택합니다.
   * 공급자를 직접 연결하려면 **프록시 없이 직접 연결**을 선택합니다.
   * 기존 프록시에 인증이 필요하거나 공급자 연결에 대해 사용자 지정 프록시를 사용하려면 **사용자 지정 프록시 설정으로 연결**을 선택합니다.
     * 사용자 지정 프록시를 사용하는 경우 주소, 포트 및 자격 증명을 지정해야 합니다.
     * 프록시를 사용하는 경우 다음 URL을 이미 허용했어야 합니다.
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![방화벽](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. **필수 조건 확인**에서 설치 프로그램에서 설치를 실행할 수 있는지 확인합니다.

    ![필수 조건](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     **글로벌 시간 동기화 확인**에 대한 경고가 표시되면 시스템 시계의 시간(**날짜 및 시간** 설정)이 표준 시간대와 같은지 확인합니다.

     ![시간 동기화 문제](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. **MySQL 구성**에서 설치할 MySQL 서버 인스턴스에 로그인하기 위한 자격 증명을 만듭니다.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. **환경 세부 정보**에서 VMware VM을 복제 여부를 선택합니다. 복제하는 경우 설치 프로그램에서 PowerCLI 6.0이 설치되어 있는지 확인합니다.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. **설치 위치**에서 이진 파일을 설치하고 캐시를 저장할 위치를 선택합니다. 사용 가능한 디스크 공간이 5GB 이상인 드라이브를 선택할 수 있지만, 사용 가능한 디스크 공간이 600GB 이상인 캐시 드라이브를 사용하는 것이 좋습니다.

   ![설치 위치](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. **네트워크 선택**에서 구성 서버가 복제 데이터를 전송 및 수신할 수신기(네트워크 어댑터 및 SSL 포트)를 지정합니다. 기본 포트(9443)를 수정할 수 있습니다. 복제 작업을 오케스트레이션하는 웹 서버에서는 이 포트 외에도 443 포트를 사용합니다. 복제 트래픽을 받는 데 443 포트를 사용하면 안됩니다.

    ![네트워크 선택](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. **요약**에서 정보를 검토하고 **설치**를 클릭합니다. 설치가 완료되면 암호가 생성됩니다. 복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.

   ![요약](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Microsoft Azure Recovery Services 에이전트 프록시를 설정해야 합니다.
> 설치가 완료되면 Windows 시작 메뉴에서 Microsoft Azure Recovery Services 셸을 시작합니다. 열리는 명령 창에서 다음과 같은 명령 집합을 실행하여 프록시 서버 설정을 설정합니다.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-the-command-line"></a>명령줄에서 설치 실행
다음과 같이 명령줄에서 통합 마법사를 실행할 수도 있습니다.

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]

여기서,

* /ServerMode: 필수. 설치 시 구성 서버와 프로세스 서버를 모두 또는 프로세스 서버만(추가 프로세스 서버를 설치하는 데 사용됨) 설치해야 하는지 여부를 지정합니다. 입력 값: CS, PS.
* InstallDrive: 필수. 구성 요소가 설치되는 폴더를 지정합니다.
* /MySQLCredFilePath. 필수. MySQL 서버 자격 증명이 저장되는 파일의 경로를 지정합니다. 템플릿을 가져와 템플릿을 만듭니다.
* /VaultCredFilePath. 필수. 자격 증명 모음 자격 증명 파일의 위치입니다.
* /EnvType. 필수. 설치 유형. 값: VMware, NonVMware
* /PSIP 및 /CSIP. 필수. 프로세스 서버와 구성 서버의 IP 주소.
* /PassphraseFilePath. 필수. 암호 파일의 위치.
* /ByPassProxy. 선택 사항입니다. 프록시 없이 Azure에 연결하는 관리 서버를 지정합니다.
* /ProxySettingsFilePath. 선택 사항입니다. 사용자 지정 프록시(인증이 필요한 서버의 기본 프록시 또는 사용자 지정 프록시)에 대한 설정을 지정합니다.

## <a name="step-6-set-up-credentials-for-the-vcenter-server"></a>6단계: vCenter Server에 대한 자격 증명 설정
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

프로세스 서버는 vCenter Server에서 관리하는 VMware VM을 자동으로 검색할 수 있습니다. 자동 검색의 경우 Site Recovery에는 vCenter 서버에 액세스할 수 있는 계정과 자격 증명이 필요합니다. 물리적 서버만 복제하는 경우에는 관련이 없습니다.

계정 및 자격 증명을 설정하려면 다음을 수행합니다.

1. vCenter 서버에서 [필수 권한](#vmware-permissions-for-vcenter-access)으로 vCenter 수준에서 역할(**Azure_Site_Recovery**)을 만듭니다.
2. **Azure_Site_Recovery** 역할을 vCenter 사용자에게 할당합니다.

   > [!NOTE]
   > 읽기 전용 역할이 있는 vCenter 사용자 계정은 보호된 원본 컴퓨터를 종료하지 않고 장애 조치(Failover)를 실행할 수 있습니다. 이러한 컴퓨터를 종료하려면 Azure_Site_Recovery 역할이 필요합니다. VMware에서 Azure로 VM을 마이그레이션하지만 장애 복구가 필요하지 않으면 읽기 전용 역할만으로 충분합니다.
   >
   >
3. 계정을 추가하려면 **cspsconfigtool**을 엽니다. 바탕 화면에 바로 가기로 사용 가능하며 [설치 위치]\home\svsystems\bin 폴더에 있습니다.
4. **계정 관리** 탭에서 **계정 추가**를 클릭합니다.

    ![계정 추가](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. **계정 세부 정보**에서 vCenter 서버에 액세스하는 데 사용할 수 있는 자격 증명을 추가합니다. 포털에 계정 이름이 표시되는 데 15분 이상 걸릴 수 있습니다. 즉시 업데이트하려면 **구성 서버** 탭에서 **새로 고침**을 클릭합니다.

    ![세부 정보](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>7단계: vCenter Server 또는 ESXi 호스트 추가
VMware VM을 복제하는 경우 vCenter 서버(또는 ESXi 호스트)를 추가해야 합니다.

1. **서버** > **구성 서버** 탭에서 **vCenter 서버 추가**를 선택합니다.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. vCenter 서버 또는 ESXi 호스트 세부 정보, 이전 단계에서 vCenter 서버에 액세스하기 위해 지정한 계정 이름 및 vCenter 서버에서 관리하는 VMware VM을 검색하는 데 사용할 프로세스 서버를 추가합니다. vCenter 서버 또는 ESXi 호스트는 프로세스 서버를 설치한 서버와 동일한 네트워크에 있어야 합니다.

   > [!NOTE]
   > vCenter 서버 또는 호스트 서버에 대한 관리자 권한이 없는 계정으로 vCenter 서버 또는 ESXi 호스트를 추가하는 경우 vCenter 또는 ESXi 계정에서 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터 및 vSphere Distributed Switch에 대한 권한을 사용하도록 설정되어 있는지 확인합니다. vCenter 서버에서 저장소 보기 권한을 사용하도록 설정되어야 합니다.
   >
   >

    ![vCenter 서버 추가](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. 검색이 완료되면 해당 vCenter 서버가 **구성 서버** 탭에 나열됩니다.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>8단계: 보호 그룹 만들기
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

보호 그룹은 동일한 보호 설정을 사용하여 보호하려는 가상 컴퓨터 또는 물리적 서버의 논리적 그룹화입니다. 보호 설정을 보호 그룹에 적용하면 해당 설정이 그룹에 추가한 모든 가상 컴퓨터(가상 또는 물리적)에 적용됩니다.

1. **보호된 항목** > **보호 그룹**으로 차례로 이동하고 아이콘을 클릭하여 보호 그룹을 추가합니다.

    ![보호 그룹 만들기](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. **보호 그룹 설정 지정** 페이지에서 그룹의 이름을 지정합니다. **원본** 드롭다운 목록에서 그룹을 만들려는 구성 서버를 선택합니다. **대상**은 Microsoft Azure입니다.

    ![보호 그룹 설정](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. **복제 설정 지정** 페이지에서 그룹의 모든 컴퓨터에 사용할 복제 설정을 구성합니다.

    ![보호 그룹 복제](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **다중 VM 일관성**: 이 설정을 사용하면 보호 그룹의 컴퓨터 전체에 공유된 응용 프로그램 일치 복구 지점이 만들어집니다. 이 설정은 보호 그룹의 모든 컴퓨터에서 동일한 워크로드를 실행하는 경우에 가장 적합합니다. 모든 컴퓨터가 동일한 데이터 지점으로 복구됩니다. 이는 VMware VM 또는 물리적 서버(Windows 또는 Linux)를 복제하는지 여부에 상관없이 사용할 수 있습니다.
   * **RPO 임계값**: RPO를 설정합니다. 연속 데이터 보호 복제가 구성된 RPO 임계값을 초과하면 경고가 생성됩니다.
   * **복구 지점 보존**: 보존 기간을 지정합니다. 보호된 컴퓨터를 이 기간 내의 모든 지점으로 복구할 수 있습니다.
   * **응용 프로그램 일치 스냅숏 빈도**: 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도를 지정합니다.

확인 표시를 선택하면 지정된 이름으로 보호 그룹이 만들어집니다. 또한 *protection-group-name*-Failback> 이름의 두 번째 보호 그룹이 만들어집니다. 이 보호 그룹은 Azure에 장애 조치 후 온-프레미스 사이트에 장애 복구(failback)하는 경우 사용됩니다. **보호된 항목** 페이지에서 만들 때 보호 그룹을 모니터링할 수 있습니다.

## <a name="step-9-install-the-mobility-service"></a>9단계: 모바일 서비스 설치
가상 컴퓨터 및 물리적 서버에 대해 보안을 설정하는 첫 번째 단계는 모바일 서비스를 설치하는 것입니다. 다음 두 가지 방법으로 수행할 수 있습니다.

* 프로세스 서버에서 각 컴퓨터에 서비스를 자동으로 푸시 및 설치합니다. 보호 그룹에 컴퓨터를 추가하고 이미 적절한 버전의 모바일 서비스를 실행 중인 경우 강제 설치가 발생하지 않습니다. 또한 WSUS 또는 System Center Configuration Manager와 같은 엔터프라이즈 푸시 메서드를 사용하여 서비스를 자동으로 설치할 수도 있습니다. 이렇게 하려면 먼저 관리 서버를 설정해야 합니다.
* 보호하려는 각 컴퓨터에 서비스를 수동으로 설치합니다. 이렇게 하려면 먼저 관리 서버를 설정해야 합니다.

### <a name="install-the-mobility-service-with-push-installation"></a>강제 설치로 모바일 서비스 설치
보호 그룹에 컴퓨터를 추가하면 프로세스 서버에서 모바일 서비스를 각 컴퓨터에 자동으로 푸시하여 설치합니다.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Windows 컴퓨터에서 자동 푸시 준비
프로세스 서버에서 모바일 서비스를 자동으로 설치할 수 있도록 Windows 컴퓨터를 준비하려면 다음을 수행합니다.

1. 프로세스 서버가 컴퓨터에 액세스하는 데 사용할 수 있는 계정을 작성합니다. 계정에는 관리자 권한(로컬 또는 도메인)이 있어야 합니다. 이러한 자격 증명은 모바일 서비스의 강제 설치에서만 사용합니다.

   > [!NOTE]
   > 도메인 계정을 사용하지 않는 경우 로컬 컴퓨터에서 원격 사용자 액세스 제어를 사용하지 않도록 설정해야 합니다. 이렇게 하려면 레지스트리의 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System에서 값이 1인 LocalAccountTokenFilterPolicy DWORD 항목을 추가합니다. CLI에서 레지스트리 항목을 추가하려면 명령을 열거나 PowerShell을 사용하여 **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`**을 입력합니다.
   >
   >
2. 보호할 컴퓨터에 대한 Windows 방화벽의 경우 **방화벽을 통해 앱 또는 기능 허용**을 선택하고, **파일 및 프린터 공유**와 **WMI(Windows Management Instrumentation)**을 사용하도록 설정합니다. 도메인에 속한 컴퓨터의 경우 GPO를 사용하여 방화벽 정책을 구성할 수 있습니다.

   ![방화벽 설정](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. 만든 계정을 다음과 같이 추가합니다.

   * **cspsconfigtool**을 엽니다. 바탕 화면에 바로 가기로 사용 가능하며 [설치 위치]\home\svsystems\bin 폴더에 있습니다.
   * **계정 관리** 탭에서 **계정 추가**를 클릭합니다.
   * 만든 계정을 추가합니다. 계정을 추가한 후 보호 그룹에 컴퓨터를 추가할 때 자격 증명을 제공해야 합니다.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Linux 서버에서 자동 푸시 준비
1. 보호하려는 Linux 컴퓨터가 [온-프레미스 필수 구성 요소](#on-premises-prerequisites)에 설명된 대로 지원되는지 확인합니다. 보호할 컴퓨터와 프로세스 서버를 실행하는 관리 서버 간에 네트워크 연결이 있는지 확인합니다.
2. 프로세스 서버가 컴퓨터에 액세스하는 데 사용할 수 있는 계정을 작성합니다. 계정은 원본 Linux 서버의 루트 사용자여야 합니다. 이러한 자격 증명은 모바일 서비스의 강제 설치에서만 사용합니다.

   * **cspsconfigtool**을 엽니다. 바탕 화면에 바로 가기로 사용 가능하며 [설치 위치]\home\svsystems\bin 폴더에 있습니다.
   * **계정 관리** 탭에서 **계정 추가**를 클릭합니다.
   * 만든 계정을 추가합니다. 계정을 추가한 후 보호 그룹에 컴퓨터를 추가할 때 자격 증명을 제공해야 합니다.
3. 원본 Linux 서버의 /etc/hosts 파일에 로컬 호스트 이름을 모든 네트워크 어댑터와 연결된 IP 주소에 매핑하는 항목이 포함되어 있는지 확인합니다.
4. 보호할 컴퓨터에 최신 openssh, openssh-server 및 openssl 패키지를 설치합니다.
5. SSH가 22 포트에서 사용되고 실행 중인지 확인합니다.
6. 다음과 같이 sshd_config 파일에서 SFTP 하위 시스템 및 암호 인증을 사용하도록 설정합니다.

   * 루트로 로그인합니다.
   * /etc/ssh/sshd_config 파일에서 PasswordAuthentication으로 시작하는 줄을 찾습니다.
   * 줄의 주석 처리를 제거하고 값을 **아니요**에서 **예**로 변경합니다.
   * **Subsystem** 으로 시작하는 줄을 찾아서 주석 처리를 제거합니다.

     ![Linux에서 기본값(하위 시스템 없음) 재정의](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-the-mobility-service-manually"></a>모바일 서비스 수동 설치
설치 관리자는 C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository에서 사용할 수 있습니다.

| 원본 운영 체제 | 모바일 서비스 설치 파일 |
| --- | --- |
| Windows Server(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-the-mobility-service-manually-on-a-windows-server"></a>Windows 서버에 모바일 서비스 수동 설치
1. 관련 설치 관리자를 다운로드 및 실행합니다.
2. **시작하기 전에**에서 **모바일 서비스**를 선택합니다.

    ![모바일 서비스 설치](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. **구성 서버 세부 정보**에서 관리 서버의 IP 주소와 관리 서버 구성 요소를 설치할 때 생성된 암호를 지정합니다. 관리 서버에서 **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe –n**을 실행하여 암호를 검색할 수 있습니다.

    ![모바일 서비스](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. **설치 위치**에서 기본 위치를 유지하고 **다음**을 클릭하여 설치를 시작합니다.
5. **설치 진행률**에서 설치를 확인하고 메시지가 표시되면 컴퓨터를 다시 시작합니다.

또한 명령줄에 다음 텍스트를 입력하여 설치할 수도 있습니다.

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

이전 명령에서:

* /Role: 필수. 모바일 서비스를 설치해야 하는지 여부를 지정합니다.
* /InstallLocation: 필수. 서비스를 설치할 위치를 지정합니다.
* /PassphraseFilePath: 필수. 구성 서버의 암호를 지정합니다.
* /LogFilePath: 필수. 로그 설정 파일의 위치를 지정합니다.

#### <a name="uninstall-the-mobility-service-manually"></a>모바일 서비스 수동 설치 제거
[제어판]에서 **프로그램 제거 또는 변경**을 사용하거나 명령줄을 사용하여 모바일 서비스를 제거할 수 있습니다.

명령줄을 사용하여 모바일 서비스를 제거하는 명령은 다음과 같습니다.

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-the-ip-address-of-the-management-server"></a>관리 서버의 IP 주소 변경
마법사를 실행한 후 다음과 같이 관리 서버의 IP 주소를 변경할 수 있습니다.

1. (바탕 화면에 있는) hostconfig.exe 파일을 엽니다.
2. **전역** 탭에서 관리 서버의 IP 주소를 변경합니다.

   > [!NOTE]
   > 관리 서버의 IP 주소만 변경하세요. 관리 서버 통신을 위한 포트 번호는 443이어야 하며 **HTTPS 사용**은 사용하도록 설정된 상태로 두어야 합니다. 암호를 변경하면 안됩니다.
   >
   >

    ![관리 서버 IP 주소](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-the-mobility-service-manually-on-a-linux-server"></a>Linux 서버에 모바일 서비스 수동 설치
1. 적절한 tar 아카이브를 보호하려는 Linux 컴퓨터에 복사합니다. 사용할 tar 아카이브를 결정하려면 [모바일 서비스 수동 설치](#install-the-mobility-service-manually)에 있는 표를 참조하세요.
2. 셸 프로그램을 열고 다음을 실행하여 압축된 tar 아카이브를 로컬 경로로 추출합니다: `tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. tar 아카이브의 압축을 풀어 내용을 추출한 로컬 디렉터리에 passphrase.txt라는 이름의 파일을 만듭니다. 이렇게 하려면 관리 서버의 C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase에서 암호를 복사하고 셸에서 *`echo <passphrase> >passphrase.txt`*를 실행하여 passphrase.txt에 저장합니다.
4. 다음 명령을 입력하여 모바일 서비스를 설치합니다. *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. 관리 서버의 내부 IP 주소를 지정하고 443 포트가 선택되어 있는지 확인합니다.

#### <a name="install-the-mobility-service-from-the-command-line"></a>명령줄에서 모바일 서비스 설치

관리 서버의 C:\Program Files(x86)\InMage Systems\private\connection에서 암호를 복사하고 관리 서버에 "passphrase.txt"로 저장합니다. 다음 명령을 실행합니다. 이 예제에서 관리 서버 IP 주소는 104.40.75.37이고, HTTPS 포트는 443입니다.

운영 서버에 설치하려면

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

마스터 대상 서버에 설치하려면

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>10단계: 컴퓨터의 보호 활성화
보호를 사용하려면 가상 컴퓨터와 물리적 서버를 보호 그룹에 추가합니다. 시작하기 전에 VMware 가상 컴퓨터를 보호하려면 다음 사항에 유의하세요.

* VMware VM은 15분마다 검색되며, 검색 후 Site Recovery에 표시되는 데 15분 이상 걸릴 수 있습니다.
* 사이트 복구에서 가상 컴퓨터의 환경 변경 사항(예: VMware 도구 설치)이 업데이트되는 데 최대 15분이 소요될 수 있습니다.
* **구성 서버** 탭에서 vCenter Server/ESXi 호스트에 대한 **마지막 연락** 필드에서 VMware VM이 마지막으로 검색된 시간을 확인할 수 있습니다.
* 보호 그룹을 만든 후 vCenter Server 또는 ESXi 호스트를 추가하면 Azure Site Recovery 포털을 새로 고치고, **보호 그룹에 컴퓨터 추가** 대화 상자에 가상 컴퓨터가 나열되는 데 15분 이상 걸릴 수 있습니다.
* 예약된 검색을 기다리지 않고 바로 진행하여 보호 그룹에 컴퓨터를 추가하려면 구성 서버를 강조 표시하고(클릭하지 않음) **새로 고침**을 클릭합니다.

또한,

* 워크로드를 미러링하도록 보호 그룹을 설계하는 것이 좋습니다. 예를 들어 특정 응용 프로그램을 실행하는 컴퓨터를 동일한 그룹에 추가합니다.
* 보호 그룹에 컴퓨터를 추가하면 프로세스 서버가 자동으로 모바일 서비스를 푸시 및 설치합니다(아직 설치되지 않은 경우). 이전 단계에서 설명한 대로 푸시 메커니즘을 준비해야 합니다.

### <a name="add-machines-to-a-protection-group"></a>보호 그룹에 컴퓨터 추가

1. **보호된 항목** > **보호 그룹** > **컴퓨터** > **컴퓨터 추가**로 이동합니다.
2. VMware 가상 컴퓨터를 보호하는 경우 **가상 컴퓨터 선택**에서 가상 컴퓨터(또는 실행 중인 EXSi 호스트)를 관리하는 vCenter 서버를 선택한 다음 컴퓨터를 선택합니다.

    ![가상 컴퓨터의 보호 활성화](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. 물리적 서버를 보호하는 경우 **가상 컴퓨터 선택**에서 **물리적 컴퓨터 추가** 마법사를 열고 IP 주소와 이름을 입력합니다. 그런 다음 운영 체제 제품군을 선택합니다.

   ![물리적 서버 보호를 사용하도록 설정](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. **대상 리소스 지정**에서 복제에 사용하는 저장소 계정을 선택하고, 모든 워크로드에 설정을 사용해야 하는지 여부를 선택합니다. 프리미엄 저장소 계정은 현재 지원되지 않습니다.

   > [!NOTE]
   > [Azure Portal](../storage/storage-create-storage-account.md)을 사용하여 만든 저장소 계정의 리소스 그룹 간 이동은 지원하지 않습니다.                           
   > [저장소 계정 마이그레이션](../azure-resource-manager/resource-group-move-resources.md) 작업은 Site Recovery를 배포하는 데 사용되는 저장소 계정에서 같은 구독 내에 있거나 여러 구독에 있는 리소스 그룹에 대해 수행할 수 없습니다.
   >
   >

    ![대상 설정 구성](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. **계정 지정**에서 모바일 서비스의 자동 설치에 사용하도록 [설정한](#install-the-mobility-service-with-push-installation) 계정을 선택합니다.

    ![계정 지정](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. 확인 표시를 클릭하여 보호 그룹에 컴퓨터 추가를 완료하고 각 컴퓨터에 대해 초기 복제를 시작합니다.

   > [!NOTE]
   > 강제 설치가 준비되면 보호 그룹에 추가될 때 설치되지 않은 컴퓨터에 모바일 서비스가 자동으로 설치됩니다. 서비스가 설치된 후 보호 작업이 시작되고 실패합니다. 실패 후에는 모바일 서비스가 설치된 각 컴퓨터를 수동으로 다시 시작해야 합니다. 다시 시작한 후 보호 작업이 다시 시작되고 초기 복제가 발생합니다.
   >
   >

**작업** 페이지에서 상태를 모니터링할 수 있습니다.

![작업 페이지에서 상태 모니터링](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

보호 상태는 **보호된 항목** > *보호 그룹 이름* > **가상 컴퓨터**에서 모니터링할 수도 있습니다. 초기 복제가 완료되고 데이터가 동기화되면 컴퓨터 상태가 **보호됨**으로 변경됩니다.

![보호된 항목의 상태 모니터링](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>11단계: 보호된 컴퓨터 속성 설정
1. 컴퓨터가 **보호됨** 상태이면 해당 장애 조치(failover) 속성을 구성할 수 있습니다. 보호 그룹 세부 정보에서 컴퓨터를 선택하고 **구성** 탭을 엽니다.
2. 사이트 복구는 자동으로 Azure VM에 대한 속성을 제안하고 온-프레미스 네트워크 설정을 감지합니다.

    ![가상 컴퓨터 등록 설정](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. 다음 설정을 변경할 수 있습니다.

   * **Azure VM 이름**: 장애 조치(failover) 후에 Azure에서 컴퓨터에 지정될 이름입니다. 이름은 Azure 요구 사항을 준수해야 합니다.
   * **Azure VM 크기**: 네트워크 어댑터 수가 대상 가상 컴퓨터에 대해 지정한 크기에 따라 결정됩니다. 크기와 어댑터에 대한 자세한 내용은 [크기 표](../virtual-machines/linux/sizes.md)를 참조하세요. 다음 사항에 유의하세요.

     * 가상 컴퓨터의 크기를 수정하고 설정을 저장하면 다음에 **구성** 탭을 열 때 네트워크 어댑터의 수가 변경됩니다. 대상 가상 컴퓨터의 최소 네트워크 어댑터 수는 원본 가상 컴퓨터의 최소 네트워크 어댑터 수와 같습니다. 최대 네트워크 어댑터 수는 가상 컴퓨터의 크기에 따라 결정됩니다.
       * 원본 컴퓨터의 네트워크 어댑터 수가 대상 컴퓨터 크기에 허용되는 어댑터 수보다 작거나 같은 경우 대상에는 원본과 동일한 수의 어댑터가 있습니다.
       * 원본 가상 컴퓨터의 어댑터의 수가 대상 크기에 허용된 수를 초과하면 대상 크기의 최대값이 사용됩니다.
        예를 들어 원본 컴퓨터에 두 네트워크 어댑터가 있고 대상 컴퓨터 크기가 4를 지원하는 경우, 대상 컴퓨터에는 2개의 어댑터가 있어야 합니다. 원본 컴퓨터에 두 어댑터가 있지만 지원되는 대상 크기에서 하나만 지원하는 경우 대상 컴퓨터에는 하나의 어댑터만 있습니다.
     * 가상 컴퓨터에 여러 네트워크 어댑터가 있는 경우 모든 어댑터가 동일한 Azure 네트워크에 연결되어야 합니다.
   * **Azure 네트워크**: 장애 조치(failover) 후 Azure VM이 연결될 Azure 네트워크를 지정해야 합니다. 지정하지 않으면 Azure VM은 네트워크에 연결되지 않습니다. 또한 Azure에서 온-프레미스 사이트로 장애 복구하려면 Azure 네트워크를 지정해야 합니다. 장애 복구(failback)를 위해서는 Azure 네트워크와 온-프레미스 네트워크 간의 VPN 연결이 필요합니다.
   * **Azure IP 주소/서브넷**: 각 네트워크 어댑터에 대해 Azure VM에서 연결할 서브넷을 선택합니다. 원본 컴퓨터의 네트워크 어댑터에서 고정 IP 주소를 사용하도록 구성된 경우 Azure VM에 고정 IP 주소를 지정할 수 있습니다. 고정 IP 주소를 제공하지 않으면 사용 가능한 IP 주소가 할당됩니다. 대상 IP 주소가 지정되었지만 Azure의 다른 VM에서 해당 주소를 이미 사용 중이면 장애 조치가 실패합니다. 원본 컴퓨터의 네트워크 어댑터가 DHCP를 사용하도록 구성되어 있으면 Azure를 위한 설정으로 DHCP를 사용하게 됩니다.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>12단계: 복구 계획 만들기 및 장애 조치 실행
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

단일 컴퓨터에 대해 장애 조치를 실행할 수 있거나, 동일한 작업을 수행하거나 동일한 워크로드를 실행하는 여러 가상 컴퓨터를 장애 조치할 수 있습니다. 동시에 여러 컴퓨터를 장애 조치하려면 복구 계획에 추가합니다.

복구 계획을 만들려면 다음을 수행합니다.

1. **복구 계획** 페이지에서 **복구 계획 추가**를 클릭하고 복구 계획을 추가합니다. 계획의 세부 정보를 지정하고 대상으로 **Azure** 를 선택합니다.

 ![복구 계획 구성](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. **가상 컴퓨터 선택**에서 보호 그룹을 선택한 다음 그룹의 컴퓨터를 선택하여 복구 계획에 추가합니다.

 ![가상 컴퓨터 추가](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

계획을 사용자 지정하여 그룹을 만들고 복구 계획의 컴퓨터가 장애 조치(Failover)되는 순서를 지정할 수 있습니다. 수동 작업 및 스크립트에 대한 프롬프트를 추가할 수도 있습니다. 스크립트를 수동으로 또는 [Azure Automation Runbook](site-recovery-runbook-automation.md)을 사용하여 만듭니다. 복구 계획 사용자 지정에 대한 자세한 내용은 [복구 계획 만들기](site-recovery-create-recovery-plans.md)를 참조하세요.

## <a name="run-a-failover"></a>장애 조치(Failover) 실행
장애 조치를 실행하기 전에 다음을 수행합니다.

* 관리 서버가 실행 중이고 사용 가능한지 확인합니다. 그렇지 않으면 장애 조치가 실패합니다.
* 계획되지 않은 장애 조치를 실행하는 경우:

  * 가능한 경우 계획되지 않은 장애 조치를 실행하기 전에 주 컴퓨터를 종료해야 합니다. 이렇게 하면 원본 및 복제본 컴퓨터가 동시에 실행되지 않아도 됩니다. 계획되지 않은 장애 조치를 실행할 때 VMware VM을 복제하는 경우 Site Recovery에서 원본 컴퓨터를 종료하도록 지정할 수 있습니다. 이 설정은 기본 사이트의 상태에 따라 작동하거나 작동하지 않을 수 있습니다. 물리적 서버를 복제하는 경우 Site Recovery에서 이 옵션을 제공하지 않습니다.
  * 계획되지 않은 장애 조치는 주 컴퓨터에서 데이터 복제를 중지하므로 계획되지 않은 장애 조치를 시작한 후 모든 데이터 델타가 전송되지 않습니다.
  * 장애 조치 후 Azure에서 복제본 가상 컴퓨터에 연결하려면 먼저 원본 컴퓨터에서 원격 데스크톱 연결을 사용하도록 설정한 후에 장애 조치를 실행합니다. 그런 다음 방화벽을 통해 RDP 연결을 허용합니다. 또한 장애 조치 후 Azure 가상 컴퓨터의 공용 끝점에서 RDP를 허용해야 합니다. [모범 사례](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)에 따라 장애 조치 후 해당 RDP가 작동하는지 확인합니다.

> [!NOTE]
> Azure로 장애 조치를 수행할 때 최상의 성능을 얻으려면 보호된 컴퓨터에 Azure 에이전트를 설치했는지 확인합니다. 이렇게 하면 시스템 부팅이 빨라지고 문제를 진단할 수 있습니다. Azure 에이전트는 [Linux](https://github.com/Azure/WALinuxAgent) 및 [Windows](http://go.microsoft.com/fwlink/?LinkID=394789)에서 사용할 수 있습니다.
>
>

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
테스트 장애 조치를 실행하여 프로덕션 환경에 영향을 미치지 않고 일반 복제를 정상적으로 계속 수행할 수 있는 격리된 네트워크에서 장애 조치 및 복구 프로세스를 시뮬레이션합니다. 테스트 장애 조치는 원본에서 시작되고, 다음 두 가지 방법으로 실행할 수 있습니다.

* **Azure 네트워크 지정 안 함**: 네트워크 없이 테스트 장애 조치를 실행하면 테스트에서 가상 컴퓨터가 시작되고 Azure에 올바르게 나타나는지 확인합니다. 가상 컴퓨터는 장애 조치 후 Azure 네트워크에 연결되지 않습니다.
* **Azure 네트워크 지정**: 이 형식의 장애 조치(failover)는 전체 복제 환경이 예상대로 작동하고 Azure 가상 컴퓨터가 지정한 네트워크에 연결되는지 확인합니다.

테스트 장애 조치(Failover)를 실행하려면

1. **복구 계획** 페이지에서 계획을 선택하고 **테스트 장애 조치**를 클릭합니다.

 ![계획 선택](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. **테스트 장애 조치(Failover) 확인**에서 **없음**을 선택하여 테스트 장애 조치에 Azure 네트워크를 사용하지 않음을 나타내거나 장애 조치 후 테스트 VM을 연결할 네트워크를 선택합니다. 확인 표시를 클릭하여 장애 조치를 시작합니다.

 ![선택](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. **작업** 탭에서 장애 조치(failover) 진행 상황을 모니터링합니다.

 ![진행률 모니터링](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. 장애 조치가 완료되면 Azure Portal의 복제본 **가상 컴퓨터**에서 해당 복제본 Azure 컴퓨터가 표시되는 것을 확인할 수 있습니다. Azure VM에 대한 RDP 연결을 시작하려면 VM 끝점에서 3389 포트를 열어야 합니다.
5. 완료된 후 장애 조치가 **완료** 테스트 단계에 도달하면 **테스트 완료**를 클릭하여 마칩니다. **참고**에서 테스트 장애 조치와 관련된 모든 관측 내용을 기록하고 저장합니다.
6. **테스트 장애 조치가 완료됨** 을 클릭하면 테스트 환경이 자동으로 정리됩니다. 이 작업이 완료되면 테스트 장애 조치에서 **완료** 상태를 표시합니다. 테스트 장애 조치 중에 자동으로 생성된 모든 요소 또는 VM이 삭제됩니다. 테스트 장애 조치가 2주 이상 지속되면 강제로 완료됩니다.

### <a name="run-an-unplanned-failover"></a>계획되지 않은 장애 조치 실행
계획되지 않은 장애 조치가 Azure에서 시작되며 기본 사이트를 사용할 수 없는 경우에도 수행할 수 있습니다.

1. **복구 계획** 페이지에서 계획을 선택하고 **장애 조치(failover)** > **계획되지 않은 장애 조치(failover)**를 차례로 클릭합니다.

 ![계획 선택](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. VMware 가상 컴퓨터를 복제하는 경우 온-프레미스 VM을 종료할 수 있습니다. 이는 최선의 작업이며 작업의 성공 여부에 관계없이 장애 조치가 계속됩니다. 성공하지 않으면 오류 세부 정보가 **작업** 탭의 **계획되지 않은 장애 조치(failover) 작업**에 나타납니다.

 ![온-프레미스 VM 종료 옵션](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > 이 옵션은 물리적 서버를 복제하는 경우에는 사용할 수 없습니다. 가능한 경우 수동으로 종료해야 합니다.
 >
 >

3. **장애 조치(failover) 확인**에서 Azure로의 장애 조치 방향을 확인하고 장애 조치에 사용할 복구 지점을 선택합니다. 복제 속성을 구성할 때 다중 VM을 사용하도록 설정한 경우 최신 응용 프로그램 일치 또는 크래시 일관성 복구 지점으로 복구할 수 있습니다. **사용자 지정 복구 지점** 을 선택하여 이전 시점으로 복구할 수도 있습니다. 확인 표시를 클릭하여 장애 조치를 시작합니다.

 ![장애 조치 방향 확인](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. 계획되지 않은 장애 조치 작업이 완료될 때까지 기다립니다. **작업** 탭에서 장애 조치(failover) 진행 상황을 모니터링할 수 있습니다. 계획되지 않은 장애 조치 중에 오류가 발생하더라도 복구 계획은 완료될 때까지 실행됩니다. 또한 Azure Portal의 **가상 컴퓨터**에서 복제본 Azure 컴퓨터가 표시되는 것을 확인할 수 있습니다.

### <a name="connect-to-replicated-azure-virtual-machines-after-failover"></a>장애 조치 후 복제된 Azure 가상 컴퓨터에 연결
장애 조치 후 Azure에서 복제된 가상 컴퓨터에 연결하려면 다음이 필요합니다.

- 주 컴퓨터에서 원격 데스크톱 연결을 사용할 수 있어야 합니다.
- 주 컴퓨터의 Windows 방화벽에서 RDP를 허용해야 합니다.
- Azure 가상 컴퓨터의 공용 끝점에 RDP를 추가해야 합니다.

이렇게 설정하는 방법에 대한 자세한 내용은 [ASR을 사용하여 장애 조치 후 원격 데스크톱 연결 문제 해결](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)(영문)을 참조하세요.

## <a name="deploy-additional-process-servers"></a>추가 프로세스 서버 배포
200개가 넘는 원본 컴퓨터로 배포 규모를 확장해야 하거나 일일 총 변동률이 2TB를 초과하는 경우 트래픽 볼륨을 처리하기 위해 추가 프로세스가 필요합니다. 추가 프로세스 서버를 설정하려면 [추가 프로세스 서버](#additional-process-servers)의 요구 사항을 확인한 후 다음 지침에 따라 프로세스 서버를 설정합니다. 서버를 설정한 후 원본 컴퓨터에서 이 서버를 사용하도록 구성할 수 있습니다.

### <a name="set-up-an-additional-process-server"></a>추가 프로세스 서버 설정
다음과 같이 추가 프로세스 서버를 설정합니다.

* 통합 마법사를 실행하여 관리 서버를 프로세스 서버로만 구성합니다.
* 새 프로세스 서버만 사용하여 데이터 복제를 관리하려는 경우 보호된 컴퓨터를 마이그레이션해야 합니다.

### <a name="install-the-process-server"></a>프로세스 서버 설치
1. **빠른 시작** 페이지에서 Site Recovery 구성 요소를 설치하기 위한 통합 설치 파일을 다운로드합니다. 설치 프로그램을 실행합니다.
2. **시작하기 전에**에서 **배포 규모 확장을 위해 추가 프로세스 서버 추가**를 선택합니다.

 ![프로세스 서버 추가](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. 첫 번째 관리 서버를 [설정](#step-5-install-the-management-server)할 때 수행한 대로 마법사를 완료합니다.
4. **구성 서버 세부 정보**에서 구성 서버를 설치한 원래 관리 서버의 IP 주소를 입력한 다음 암호를 입력합니다. 암호를 가져오려면 원래 관리 서버에서 **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe –n**을 실행하여 검색합니다.

 ![구성 서버 세부 정보](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-to-use-the-new-process-server"></a>새 프로세스 서버를 사용하도록 컴퓨터 마이그레이션
1. **구성 서버** > **서버** > *원래 관리 서버의 이름* > **서버 세부 정보**를 엽니다.

 ![서버 세부 정보](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. **프로세스 서버** 목록에서 변경할 서버 옆에 있는 **프로세스 서버 변경**을 선택합니다.

 ![프로세스 서버 업데이트](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. **프로세스 서버 변경**을 선택하고 **대상 프로세스 서버**를 선택한 다음 새 관리 서버를 선택합니다. 그런 다음 새 프로세스 서버에서 처리할 가상 컴퓨터를 선택합니다. 서버에 대한 정보를 얻으려면 정보 아이콘을 클릭합니다. 선택된 각 가상 컴퓨터를 새 프로세스 서버로 복제하는 데 필요한 평균 공간이 표시되므로 부하 결정을 할 때 도움이 됩니다. 새 프로세스 서버로 복제를 시작하려면 확인 표시를 클릭합니다.

 ![프로세스 서버 변경](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>vCenter 액세스를 위한 VMware 권한
프로세스 서버는 vCenter Server에서 VM을 자동으로 검색할 수 있습니다. 자동 검색을 수행하려면 Site Recovery에서 vCenter 서버에 액세스할 수 있도록 vCenter 수준에서 역할(Azure_Site_Recovery)을 정의해야 합니다. VMware 컴퓨터를 Azure로 마이그레이션해야 하고 Azure에서 장애 복구할 필요가 없는 경우 읽기 전용 역할만 정의하면 됩니다. [6단계: vCenter 서버에 대한 자격 증명 설정](#step-6-set-up-credentials-for-the-vcenter-server)에서 설명한 대로 권한을 설정합니다. 다음 표에는 역할 권한이 요약되어 있습니다.

| **역할** | **세부 정보** | **권한** |
| --- | --- | --- |
| Azure_Site_Recovery 역할 |VMware VM 검색 |v-Center Server에 대해 이러한 권한 할당:<br/><br/>데이터 저장소: 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트<br/><br/>네트워크: 네트워크 할당<br/><br/>리소스: 리소스 풀에 가상 컴퓨터 할당, 전원이 꺼진 가상 컴퓨터 마이그레이션, 전원이 켜진 가상 컴퓨터 마이그레이션<br/><br/>태스크: 만들기 태스크, 업데이트 태스크<br/><br/>가상 컴퓨터 > 구성<br/><br/>가상 컴퓨터 > 상호 작용 > 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치<br/><br/>가상 컴퓨터 > 인벤토리 > 만들기, 등록, 등록 취소<br/><br/>가상 컴퓨터 > 프로비전 > 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용<br/><br/>가상 컴퓨터 > 스냅숏 > 스냅숏 제거 |
| vCenter 사용자 역할 |VMware VM 검색/원본 VM을 종료하지 않고 장애 조치 |v-Center Server에 대해 이러한 권한 할당:<br/><br/>데이터 센터 개체 > 자식 개체에 전파, role=Read-only <br/><br/>사용자는 데이터 센터 수준에서 할당되므로 데이터 센터의 모든 개체에 대한 액세스 권한이 있습니다. 액세스를 제한하려면 **자식 개체에 전파**를 사용하여 **액세스 권한 없음** 역할을 자식 개체(ESX 호스트, 데이터 저장소, VM 및 네트워크)에 할당합니다. |
| vCenter 사용자 역할 |장애 조치 및 장애 복구 |v-Center Server에 대해 이러한 권한 할당:<br/><br/>데이터 센터 개체 –> 자식 개체에 전파, role=Azure_Site_Recovery<br/><br/>사용자는 데이터 센터 수준에서 할당되므로 데이터 센터의 모든 개체에 대한 액세스 권한이 있습니다.  액세스를 제한하려면 **자식 개체에 전파**를 사용하여 **액세스 권한 없음** 역할을 자식 개체(ESX 호스트, 데이터 저장소, VM 및 네트워크)에 할당합니다. |

## <a name="third-party-software-notices-and-information"></a>타사 소프트웨어 통지 및 정보
<!--Do Not Translate or Localize-->

The software and firmware running in the Microsoft product or service is based on or incorporates material from the projects listed below (collectively, “Third Party Code”).  Microsoft is the not original author of the Third Party Code.  The original copyright notice and license, under which Microsoft received such Third Party Code, are set forth below.

The information in Section A is regarding Third Party Code components from the projects listed below. Such licenses and information are provided for informational purposes only.  This Third Party Code is being relicensed to you by Microsoft under Microsoft's software licensing terms for the Microsoft product or service.  

The information in Section B is regarding Third Party Code components that are being made available to you by Microsoft under the original licensing terms.

The complete file may be found on the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>다음 단계
Azure에서 실행 중인 장애 조치된 컴퓨터를 온-프레미스 환경으로 [장애 복구하는 방법에 대해 자세히 알아봅니다](site-recovery-failback-azure-to-vmware-classic.md).
