---
title: "aaaReplicate VMware Vm과의 실제 서버 tooAzure hello 클래식 포털 | Microsoft Docs"
description: "이 문서에서는 어떻게 toodeploy Azure Site Recovery tooorchestrate 복제, 장애 조치 및 복구를 온-프레미스 VMware 가상 컴퓨터 및 Windows/Linux 물리적 서버의 tooAzure를 설명 합니다."
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
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>VMware 가상 컴퓨터와 Azure Site Recovery와 실제 서버 tooAzure 복제
> [!div class="op_single_selector"]
> * [hello Azure 포털](site-recovery-vmware-to-azure.md)
> * [hello 클래식 포털](site-recovery-vmware-to-azure-classic.md)
> * [hello 클래식 포털 (레거시)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Azure Site Recovery 서비스 hello 복제, 장애 조치 및 가상 컴퓨터와 물리적 서버와 복구를 오케스트레이션 하 여 tooyour 비즈니스 연속성 및 재해 복구 (BCDR) 전략을 적용 합니다. 복제 된 tooAzure 또는 tooa 보조 온-프레미스 데이터 센터 컴퓨터 수 있습니다. 간략한 개요를 알아보려면 [Azure Site Recovery란?](site-recovery-overview.md)을 참조하세요.

## <a name="overview"></a>개요
이 문서에서는 다음과 같이 방법을 설명합니다.

* **VMware 가상 컴퓨터 tooAzure 복제**: 사이트 복구 배포 toocoordinate 복제, 장애 조치 및 온-프레미스 VMware 가상 컴퓨터 tooAzure 저장소를 복구 합니다.
* **물리적 서버 tooAzure 복제**: Azure 사이트 복구 배포 toocoordinate 복제, 장애 조치 및 온-프레미스 물리적 Windows 및 Linux 서버 tooAzure 복구 합니다.

> [!NOTE]
> 이 문서에서는 설명 방법을 tooreplicate tooAzure 합니다. Tooreplicate VMware Vm 이나 Windows/Linux 물리적 서버의 tooa 보조 데이터 센터 참조 [사이트 복구 VMware tooVMware](site-recovery-vmware-to-vmware.md)합니다.
>
>

Hello 또는이 문서의 hello 맨 아래에 설명 이나 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.

## <a name="enhanced-deployment"></a>향상된 배포
이 문서는 hello Azure 클래식 포털에서에서 향상 된 배포에 대 한 지침을 제공 합니다. 새로운 모든 배포에 대해 이 버전을 사용하는 것이 좋습니다. 가 이미 배포한 경우 이전 레거시 버전 hello를 사용 하 여, toohello 새 버전으로 마이그레이션하는 것이 좋습니다. 마이그레이션에 대 한 자세한 내용은 [사이트 복구 VMware tooAzure 클래식 레거시](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment)합니다.

향상 된 hello 배포가 한 주요 업데이트 이며입니다. 다음은 만들었고 hello 향상 된 기능에 대 한 요약이입니다.

* **Azure의 Vm 인프라가 없는**: 데이터는 직접 tooan Azure 저장소 계정 복제 합니다. 또한 있습니다 없습니다 필요 tooset 모든 인프라 Vm (예: 구성 서버 또는 마스터 대상 서버)를 복제 및 장애 조치에 대 한 hello 레거시 배포에서 필요한 경우 되었습니다.  
* **통합 설치**: 단일 설치는 온-프레미스 구성 요소에 대해 간단한 설정 및 확장성을 제공합니다.
* **안전한 배포**: 모든 트래픽이 암호화되고 복제 관리 통신이 HTTPS 443을 통해 전송됩니다.
* **복구 지점**: Windows 및 Linux 환경에 대한 크래시 일관성 및 응용 프로그램 일치 복구 지점을 지원하며, 단일 VM 및 여러 VM 일치 구성을 지원합니다.
* **테스트 장애 조치**: 프로덕션에 영향을 주지 또는 복제를 일시 중지 없이 장애 조치 tooAzure 정기적인 테스트에 대 한 지원 합니다.
* **계획 되지 않은 장애 조치**: 장애 조치 하기 전에 종료 된 Vm으로 고급 옵션 tooautomatically tooAzure 계획 되지 않은 장애 조치에 대 한 지원.
* **장애 복구**: 델타 변경 내용을 다시 toohello만 복제 하는 통합된 장애 복구 온-프레미스 사이트입니다.
* **vSphere 6.0**: VMware vSphere 6.0 배포를 제한적으로 지원합니다.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>사이트 복구로 가상 컴퓨터 및 물리적 서버를 어떻게 보호할 수 있나요?
* VMware 관리자 비즈니스 작업 및 VMware 가상 컴퓨터에서 실행 되는 응용 프로그램에서 오프 사이트 보호 기능이 tooprotect Azure를 구성할 수 있습니다. 서버 관리자는 실제 온-프레미스 Windows 및 Linux 서버 tooAzure 복제할 수 있습니다.
* hello Azure 사이트 복구 콘솔 간단한 설정 및 복제, 장애 조치 및 복구 프로세스의 관리를 위한 단일 위치를 제공합니다.
* vCenter Server에서 관리하는 VMware 가상 컴퓨터를 복제하는 경우 사이트 복구는 해당 VM을 자동으로 검색할 수 있습니다. 컴퓨터 ESXi 호스트에 있는 경우 사이트 복구는 hello 호스트에 Vm을 검색 합니다.
* 실패 수를 온-프레미스 인프라 tooAzure에서 쉬운 장애 조치를 실행 하는 경우 Azure tooVMware VM 서버 hello 온-프레미스 사이트에서에서 (복원)를 백업 합니다.
* 여러 컴퓨터에 계층화된 응용 프로그램 워크로드를 그룹화하는 복구 계획을 구성할 수 있습니다. 를 장애 조치 이러한 계획 하는 경우 사이트 복구 hello 동일한 작업 수를 실행 하는 컴퓨터를 함께 복구할 tooa 일관 된 데이터 요소가 있도록 다중 VM 일관성을 제공 합니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제
### <a name="windows-64-bit-only"></a>Windows(64비트만 해당)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux(64비트만 해당)
* Red Hat Enterprise Linux 6.7, 7.1 및 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 및 7.2
* Oracle 6.4 및 6.5 실행 하거나 hello Red Hat Enterprise Linux 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>시나리오 아키텍처
시나리오 구성 요소:

* **온-프레미스 관리 서버**: hello 관리 서버는 사이트 복구 구성 요소를 실행 합니다.
  * **구성 서버**: 통신을 조정하고 데이터 복제 및 복구 프로세스를 관리합니다.
  * **프로세스 서버**:복제 게이트웨이 역할을 합니다. 보호 된 컴퓨터에서 데이터를 받을 캐싱, 압축 및 암호화; 최적화 및 보냅니다 복제 데이터 tooAzure 저장 합니다. 또한 모바일 서비스 tooprotected 컴퓨터의 강제 설치를 처리 하 고 VMware Vm의 자동 검색을 수행 합니다.
  * **마스터 대상 서버**: Azure에서 장애 복구(failback) 중에 복제 데이터를 처리합니다.
    배포 프로세스 서버 tooscale로만 사용 되는 관리 서버를 배포할 수 있습니다.
* **모바일 서비스 hello**:이 구성 요소 tooreplicate tooAzure 하려는 각 컴퓨터 (VMware VM 또는 실제 서버)에 배포 됩니다. Hello 컴퓨터에 데이터 쓰기 캡처하고 toohello 프로세스 서버에 전달 합니다.
* **Azure**: 모든 Azure Vm toohandle 복제 및 장애 조치 toocreate 필요 하지 않습니다. 데이터는 직접 tooAzure 저장소 복제 및 사이트 복구 서비스 hello 데이터 관리를 처리 합니다. 복제 된 Azure Vm 장애 조치 tooAzure 발생 하는 경우에으로 작동 됩니다. 그러나 Azure toohello 온-프레미스 사이트에서 다시 toofail 원하는 프로세스 서버와 Azure VM tooact tooset을 해야 합니다.

다음 그래픽 (헨리 Robalino에서 만든) hello 이러한 구성 요소 상호 작용 하는 방법을 보여 줍니다.

![구성 요소 아키텍처](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>용량 계획
용량을 계획할 때 필요한 toothink에 대 한 다음과 같습니다.

* **hello 소스 환경**: 용량 계획 또는 hello VMware 인프라 및 원본 컴퓨터 요구 사항입니다.
* **관리 서버 hello**: hello 온-프레미스 복구 사이트 구성 요소를 실행 하는 관리 서버를 계획 합니다.
* **소스 tootarget에서 네트워크 대역폭이**: hello 원본 서버와 Azure 간의 복제에 필요한 네트워크 대역폭에 대 한 계획입니다.

### <a name="source-environment-considerations"></a>원본 환경 고려 사항
* **일일 최대 변경률**: 보호된 컴퓨터는 하나의 프로세스 서버만 사용할 수 있습니다. 단일 프로세스 서버 too2 하루 변경 t B의 데이터를 처리할 수 있습니다. 따라서 2TB hello 최대 일별 데이터 변경 보호 된 컴퓨터에 지원 되는 속도입니다.
* **최대 처리량**: 복제 된 컴퓨터는 Azure의 저장소 계정 tooone 속할 수 있습니다. 표준 저장소 계정을 최대 20, 000 초 당 요청을 처리할 수 있습니다 및 원본 컴퓨터 too20 000 가로 IOPS의 hello 개수를 유지 하는 것이 좋습니다. 예를 들어 디스크 5 인 원본 컴퓨터가 있고 hello 소스 120 IOPS (8KB 크기)를 생성 하는 각 디스크 당 500 디스크 IOPS 제한 hello Azure 내에서 됩니다. 필요한 저장소 계정 수 hello = 총 원본 IOPs/20, 000입니다.

### <a name="management-server-considerations"></a>관리 서버 고려 사항
관리 서버 hello 데이터 최적화, 복제 및 관리를 처리 하는 사이트 복구 구성 요소를 실행 합니다. 보호 된 컴퓨터에서 실행 되는 모든 작업에서 수 toohandle hello 매일 변경 비율 용량 이어야 합니다 있으며 tooAzure 저장소 데이터를 복제 하는 충분 한 대역폭 toocontinuously입니다. 구체적으로 살펴보면 다음과 같습니다.

* 보호 된 컴퓨터에서 복제 데이터를 수신 하 고 캐싱, 압축 및 tooAzure 보내기 전에 암호화를 최적화 하는 hello 프로세스 서버입니다. hello 관리 서버는 이러한 작업 충분 한 리소스 tooperform 있어야 합니다.
* 프로세스 서버 hello 디스크 기반 캐시를 사용합니다. 600GB 또는 네트워크 병목 현상 또는 중단의 hello 이벤트에 저장 된 자세한 toohandle 데이터 변경의 별도 캐시 디스크를 사용 하는 것이 좋습니다. 배포 하는 동안 5GB 이상의 사용 가능한 저장소에 있는 모든 드라이브에서 hello 캐시를 구성할 수 있지만 600GB이 hello 최소 좋습니다.
* 모범 사례로, 해당 hello 관리 서버 hello에 있는 권장 동일한 네트워크 및와 LAN 세그먼트 hello tooprotect 컴퓨터입니다. 다른 네트워크 하지만 tooprotect L3 네트워크 가시성 tooit 있어야 합니다. 원하는 컴퓨터에 위치할 수 있습니다.

다음 표에 hello에 관리 서버 hello에 대 한 크기 권장 사항 요약 되어 있습니다.

| **관리 서버 CPU** | **메모리** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- | --- |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) |16GB |300GB |500GB 이하 |100 개 미만의 컴퓨터 이러한 설정 tooreplicate로 관리 서버를 배포 합니다. |
| 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) |18GB |600GB |500GB too1 TB |이러한 설정 tooreplicate 100 ~ 150 컴퓨터와 관리 서버를 배포 합니다. |
| 16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz) |32GB |1TB |1TB too2 TB |이러한 설정 tooreplicate 150-200 컴퓨터와 관리 서버를 배포 합니다. |
| 다른 프로세스 서버 배포 | | |> 2TB |200 개 이상의 컴퓨터를 복제 하는 또는 속도 hello 일별 데이터 변경 하는 경우 2TB를 초과 하는 경우 추가 프로세스 서버를 배포 합니다. |

여기서,

* 각 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.
* 캐시 디스크 측정을 위해 벤치마킹 저장소로 RAID 10을 이용한 10,000RPM의 8개 SAS 드라이브를 사용했습니다.

### <a name="network-bandwidth-from-source-tootarget"></a>원본 tootarget에서 네트워크 대역폭
Hello 대역폭 hello를 사용 하 여 초기 복제 및 델타 복제에 필요한 것을 계산 해야 [용량 계획 도구](site-recovery-capacity-planner.md)합니다.

#### <a name="throttling-bandwidth-used-for-replication"></a>복제에 사용되는 대역폭 제한
VMware 복제 트래픽을 tooAzure 특정 프로세스 서버를 통해 이동합니다. 다음과 같이 해당 서버에서 사이트 복구 복제에 사용할 수 있는 hello 대역폭을 제한할 수 있습니다.

1. Hello 주 관리 서버에 Microsoft Azure 백업 MMC 스냅인 hello 열거나 관리 서버에는 프로세스 서버를 프로 비전 추가 실행 합니다. 기본적으로 Microsoft Azure 백업에 대 한 바로 가기 hello 바탕 화면에서 만들어집니다. 또는 C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin에서 찾을 수 있습니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.

    ![대역폭 제한 속성 변경](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. Hello에 **제한** 탭을 Site Recovery 복제에 사용할 수 있습니다 하 고 해당 예약 hello 있는 hello 대역폭을 지정 합니다.

    ![복제 대역폭 제한](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

PowerShell을 사용하여 제한을 설정할 수도 있습니다. 예를 들면 다음과 같습니다.

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>대역폭 사용량 최대화
Azure Site Recovery에서 복제에 대 한 사용 tooincrease hello 대역폭 toochange 레지스트리 키 필요 합니다.

hello 다음과 같은 주요 컨트롤 hello를 복제할 때 사용 되는 디스크 복제 당 스레드 수 있습니다:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 Overprovisioned 네트워크에서이 레지스트리 키 toobe 해당 기본값에서 변경 해야 합니다. 지원되는 최대값은 32입니다.  

자세한 용량 계획에 대한 자세한 내용은 [Site Recovery Capacity Planner](site-recovery-capacity-planner.md)를 참조하세요.

### <a name="additional-process-servers"></a>추가 프로세스 서버
Tooprotect 해야 할 경우 200 개 이상의 컴퓨터 또는 프로그램 매일 변경 률이 2TB를 추가할 수 있는 서버를 추가로 toohandle hello 부하 큽니다. out tooscale를 수행할 수 있습니다.

* 관리 서버 hello 수를 늘립니다. 예를 들어 두 명의 관리 서버와 too400 컴퓨터를 보호할 수 있습니다.
* 추가 프로세스 서버를 추가 하 고 이러한 toohandle 대신 (또는 외에) 트래픽 hello 관리 서버를 사용 합니다.

다음 표에서는 이에 대한 시나리오를 설명합니다.

* 구성 서버를 전용으로 hello 원래 관리 서버 toouse를 설정 합니다.
* 추가 프로세스 서버를 설정합니다.
* 보호 된 가상 컴퓨터 toouse hello 추가 프로세스 서버를 구성 합니다.
* 보호된 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.

| **원래 관리 서버**<br/><br/>(구성 서버) | **추가 프로세스 서버** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터** |
| --- | --- | --- | --- | --- |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB RAM |4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB RAM |300GB |250GB 이하 |85개 이하의 컴퓨터를 복제할 수 있습니다. |
| 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB RAM |8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB RAM |600GB |250GB too1 TB |85-150개의 컴퓨터를 복제할 수 있습니다. |
| 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 18GB RAM |12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB RAM |1TB |1TB too2 TB |150-225개의 컴퓨터를 복제할 수 있습니다. |

서버 크기를 조정하는 방법은 강화 모델 또는 규모 확장 모델에 대한 선호도에 따라 달라집니다. 몇 가지 고급 관리 서버 및 프로세스 서버를 배포하여 강화하거나 더 적은 리소스로 더 많은 서버를 배포하여 규모를 확장합니다. 예를 들어: tooprotect 220 컴퓨터 필요한 hello 다음 중 하나를 수행할 수 있습니다.

* 12 개의 Vcpu와 18 GB의 RAM hello 원래 관리 서버를 구성 합니다. 12개 vCPU와 24GB RAM을 갖춘 추가 프로세스 서버를 구성합니다. 보호 된 컴퓨터 toouse 유일한 hello 추가 프로세스 서버를 구성 합니다.
* 두 명의 관리 서버 (2 x 8 개의 Vcpu, 16GB RAM)와 두 명의 추가 프로세스 서버 (1 x 8 개의 Vcpu 및 4vCPUs toohandle 135 + 85 (220) 컴퓨터를 1 x)를 구성 합니다. 보호 된 컴퓨터 toouse 유일한 hello 추가 프로세스 서버를 구성 합니다.

Hello 지침에 따라 [추가 프로세스 서버 배포](#deploy-additional-process-servers) tooset 추가 프로세스 서버를 구성 합니다.

## <a name="before-you-start-deployment"></a>배포를 시작하기 전에
hello 다음 표에 요약 되어 hello이이 시나리오의 배포 필수 구성 요소입니다.

### <a name="azure-prerequisites"></a>Azure 필수 조건
| **필수 요소** | **세부 정보** |
| --- | --- |
| **Azure 계정** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. Site Recovery 가격 책정에 대한 자세한 내용은 [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)를 참조하세요. |
| **Azure 저장소** |Azure 저장소 계정 복제 toostore 데이터가 있어야합니다. 복제된 데이터는 Azure 저장소에 저장되고, 장애 조치가 발생할 때 Azure VM이 작동합니다. <br/><br/>[표준 지역 중복 저장소 계정](../storage/storage-redundancy.md#geo-redundant-storage)이 필요합니다. hello hello Site Recovery 서비스와 동일한 지역 및 hello와 연결할 hello 계정에 있어야 동일한 구독 합니다. 복제 toopremium 저장소 계정에는 현재 지원 되지 않음 및 사용할 수 있습니다.<br/><br/>Hello를 사용 하 여 만든 이동 저장소 계정을 지원 하지 않습니다 [Azure 포털](../storage/storage-create-storage-account.md) 리소스 그룹에 걸쳐 있습니다. 자세한 내용은 참조 [Azure 저장소 소개 tooMicrosoft](../storage/storage-introduction.md)합니다.<br/><br/> |
| **Azure 네트워크** |Azure Vm 연결 하는 Azure 가상 네트워크 필요 toowhen 장애 조치가 발생 합니다. hello Azure 가상 네트워크에에서 있어야 hello hello 사이트 복구 자격 증명 모음과 동일한 지역입니다.<br/><br/>장애 조치 tooAzure 후 다시 toofail, 해야 VPN 연결 (이나 Azure express 경로) hello Azure 네트워크 toohello 온-프레미스 사이트에서 설정 합니다. |

### <a name="on-premises-prerequisites"></a>온-프레미스 필수 조건
| **필수 요소** | **세부 정보** |
| --- | --- |
| **관리 서버** |가상 컴퓨터 또는 물리적 서버에서 실행되는 온-프레미스 Windows 2012 R2 서버가 필요합니다. 모든 hello 온-프레미스 복구 사이트 구성 요소는이 관리 서버에 설치 됩니다.<br/><br/> 항상 사용 가능한 VMware VM으로 hello 서버를 배포 하는 것이 좋습니다. 장애 복구 toohello 온-프레미스 사이트에서 Azure Vm 또는 실제 서버를 통해 실패 여부에 관계 없이 tooVMware Vm은 항상입니다. VMware VM으로 hello 관리 서버를 구성 하지 않으면, VMware VM tooreceive 장애 복구 트래픽으로 tooset 별도 마스터 대상 서버를 필요 합니다.<br/><br/>hello 서버는 도메인 컨트롤러 수 없습니다.<br/><br/>hello 서버에 고정 IP 주소가 있어야 합니다.<br/><br/>hello 서버 hello 호스트 이름을 15 자 여야 합니다.이 있습니다.<br/><br/>만 hello 운영 체제 로캘은 영어 이어야 합니다.<br/><br/>hello 관리 서버는 인터넷 액세스가 필요 합니다.<br/><br/>Hello 서버에서 아웃 바운드 액세스를 다음과 같이 해야: hello Site Recovery 구성 요소 (toodownload MySQL;) 설치 하는 동안 HTTP 80에 대 한 임시 액세스 복제 관리;에 대 한 HTTPS 443 아웃 바운드 지속적인 액세스 진행 중인 아웃 바운드 HTTPS 9443에에 대 한 액세스 복제 트래픽 (이 포트를 수정할 수 있음).<br/><br/> 이러한 Url hello 관리 서버에서 액세스할 수 있는지 확인 합니다. <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Hello 서버에서 IP 주소를 기준으로 방화벽 규칙을 설정한 경우 hello 규칙 tooAzure 통신을 허용 하는지 확인 합니다. Tooallow hello 필요한 [Azure 데이터 센터 IP 범위](https://www.microsoft.com/download/details.aspx?id=41653) 및 hello HTTPS (443) 포트입니다. Hello 구독의 Azure 지역에 대 한와 West US에 대 한 toowhitelist IP 주소 범위를 필요 합니다. hello URL [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") MySQL 다운로드 하도록 합니다. |
| **VMware vCenter/ESXi 호스트** |Hello 최신 업데이트로 ESX/ESXi 버전 6.0, 5.5, 또는 5.1을 실행 중인 하나 이상의 VMware vSphere ESX/ESXi 하이퍼바이저 VMware 가상 컴퓨터를 관리 해야 합니다.<br/><br/> 배포 하는 VMware vCenter server toomanage ESXi 호스트 하는 것이 좋습니다. Hello 최신 업데이트로 vCenter 버전 6.0 또는 5.5를 실행 해야 합니다.<br/><br/>사이트 복구에서는 교차 vCenter vMotion, 가상 볼륨 및 저장소 DRS와 같은 새로운 vCenter 및 vSphere 6.0 기능을 지원하지 않습니다. 사이트 복구 지원은 버전 5.5에서에서 사용할 수 있는 제한 toofeatures 합니다. |
| **보호된 컴퓨터** |**Azure**<br/><br/>Tooprotect 준수 해야 하는 것이 원하는 컴퓨터 [Azure 필수 구성 요소](site-recovery-prereq.md) Azure Vm을 만들기 위한 합니다.<br><br/>장애 조치 후 tooconnect toohello Azure Vm을 원하는 경우 hello 로컬 방화벽 tooenable 원격 데스크톱 연결 해야 합니다.<br/><br/>보호되는 컴퓨터의 개별 디스크 용량이 1023GB 이하여야 합니다. (따라서 위쪽 too64 테라바이트) too64 디스크를 VM 있을 수 있습니다. 1TB보다 큰 디스크가 있는 경우 SQL Server AlwaysOn 또는 Oracle Data Guard와 같은 데이터베이스 복제를 사용하는 것이 좋습니다.<br/><br/>최소 2GB의 구성 요소 설치에 대 한 hello 설치 드라이브에 사용 가능한 공간입니다.<br/><br/>공유 디스크 게스트 클러스터는 지원되지 않습니다. 클러스터형 배포를 사용하는 경우 SQL Server AlwaysOn 또는 Oracle Data Guard와 같은 데이터베이스 복제를 사용하는 것이 좋습니다.<br/><br/>UEFI(Unified Extensible Firmware Interface)/EFI(Extensible Firmware Interface) 부팅은 지원되지 않습니다.<br/><br/>컴퓨터 이름은 1-63자(문자, 숫자 및 하이픈)를 포함해야 합니다. hello 이름은 문자 또는 숫자로 시작 하 고 문자 또는 숫자로 끝나야 합니다. 컴퓨터를 보호 한 후 Azure 이름 hello를 수정할 수 있습니다.<br/><br/>**VMware VM**<br/><br>Tooinstall VMware vSphere PowerCLI 6.0이 필요합니다. hello 관리 서버 (구성 서버).<br/><br/>VMware Vm을 tooprotect VMware 도구가 설치 되어 있고 실행 해야 합니다.<br/><br/>Hello 소스가 VM에서 NIC 팀을 가진 경우 변환 tooa tooAzure 장애 조치 후 NIC를 단일 합니다.<br/><br/>보호 되는 Vm에 iSCSI 디스크 있으면 사이트 복구 변환 hello hello VM 장애 tooAzure 조치 될 때 VHD 파일에 VM iSCSI 디스크를 보호 합니다. Hello Azure VM에서 iSCSI 대상에 연결할 수 경우 tooiSCSI 대상에 연결 하 고 기본적으로 두 개의 디스크를 볼: hello Azure VM 및 hello 소스 iSCSI 디스크에 VHD 디스크 hello 합니다. Toodisconnect이 경우 해야 hello에 표시 되는 hello iSCSI 대상 장애 조치 된 Azure VM입니다.<br/><br/>Hello VMware 사용자 권한에 대 한 자세한 내용은 해당 사이트 복구 요구 사항, 참조 [VMware vCenter 액세스 권한을](#vmware-permissions-for-vcenter-access)합니다.<br/><br/> **VMware VM 또는 물리적 서버의 Windows Server 컴퓨터**<br/><br/>hello 서버 지원 되는 64 비트 운영 체제를 실행 합니다: Windows Server 2012 R2, Windows Server 2012 또는 Windows Server 2008 r 2와에 최소 s p 1입니다.<br/><br/>C 드라이브에 hello 운영 체제를 설치 해야 하 고 hello OS 디스크는 Windows 기본 디스크 여야 합니다. (hello OS Windows 동적 디스크에 설치할 수 없습니다.)<br/><br/>Windows Server 2008 R2 컴퓨터에 대 한 toohave.NET Framework 3.5.1 설치 해야 합니다.<br/><br/>관리자 계정 tooprovide 필요 (hello Windows 컴퓨터에서 로컬 관리자 여야 함) Windows 서버에서 hello 밀어넣기 설치 hello 모바일 서비스에 대 한 합니다. Hello 제공 계정이 아닌 도메인 계정인 경우 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 해야 합니다. 자세한 내용은 참조 [hello 모바일 서비스를 강제 설치로 설치](#install-the-mobility-service-with-push-installation)합니다.<br/><br/>Site Recovery에서는 RDM 디스크를 사용한 VM을 지원합니다. 장애 복구 하는 동안 사이트 복구는 다시 사용 hello RDM 디스크 hello 원래 원본 VM 및 RDM 디스크를 사용할 수 있는 경우. 장애 복구 시 사용할 수 없는 경우 Site Recovery에서 각 디스크에 대한 새 VMDK 파일을 만듭니다.<br/><br/>**Linux 컴퓨터**<br/><br/>지원 되는 64 비트 운영 체제 필요: Red Hat Enterprise Linux 6.7; Centos 6.5, 6.6, 또는 6.7; 6.4 또는 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3;)을 실행 하는 6.5 oracle Enterprise Linux SUSE Linux Enterprise Server 11 s p 3입니다.<br/><br/>보호 된 컴퓨터의 /etc/hosts 파일에는 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목이 없어야 합니다. <br/><br/>Tooconnect tooan Azure 가상 컴퓨터를 원하는 경우 방화벽 규칙을 사용 하 고 hello 보호 된 컴퓨터에서 보안 셸 서비스 hello toostart 시스템 부팅 시 자동으로 설정 되어 있는지 확인 보안 셸 클라이언트 (ssh)를 사용 하 여 장애 조치 후 Linux를 실행 한 ssh 연결 tooit 합니다.<br/><br/>보호만 사용할 수 있으며 Linux 컴퓨터에 대 한 저장소를 다음 hello로: 파일 시스템 (EXT3, ETX4, ReiserFS, XFS); 다중 경로 소프트웨어 장치 매퍼 (다중 경로); 볼륨 관리자 (l v m 2)입니다. HP CCISS 컨트롤러 저장소가 있는 물리적 서버는 지원되지 않습니다. hello ReiserFS 파일 시스템은 SUSE Linux Enterprise Server 11 s p 3에 대해서만 지원 됩니다.<br/><br/>Site Recovery에서는 RDM 디스크를 사용한 VM을 지원합니다. Linux에 대 한 장애 복구 하는 동안 사이트 복구 hello RDM 디스크를 다시 사용 하지 않습니다. 대신 해당 RDM 디스크마다 새 VMDK 파일을 만듭니다. |

Linux VM에 대해서만:에서 설정 하는 hello disk.enableUUID=true 설정을 hello hello VMware에서 VM의 구성 매개 변수를 확인 합니다. 이 행이 존재하지 않는 경우 추가합니다. 이 소프트웨어는 필요한 tooprovide 일관 된 UUID toohello VMDK 올바르게를 탑재 하는 것입니다. 이 설정이 없으면 장애 복구 hello VM 내부에서 경우에 전체 다운로드가 발생 합니다. 이 설정을 추가하면 장애 복구 중에 델타 변경만 다시 보냅니다.

## <a name="step-1-create-a-vault"></a>1단계: 자격 증명 모음 만들기
1. Toohello 로그인 [Azure 포털](https://manage.windowsazure.com/)합니다.
2. **Data Services** > **Recovery Services**를 확장하고 **Site Recovery 자격 증명 모음**을 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.
5. **지역**, 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 되는 toocheck 지역 참조 [Azure Site Recovery 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)합니다.
6. **자격 증명 모음 만들기**를 클릭합니다.
    ![자격 증명 모음 만들기](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

자격 증명 모음 hello hello 상태 표시줄 tooconfirm 올바르게 만들어졌는지 확인 합니다. hello 자격 증명 모음으로 나열 됩니다 **활성** 주 hello에 **복구 서비스** 페이지.

## <a name="step-2-set-up-an-azure-network"></a>2단계: Azure 네트워크 설정
Azure Vm을 연결 된 tooa 네트워크 장애 조치 후 되며 사이트를 예상 대로 작동 수 장애 복구 toohello 온-프레미스 있도록 있도록 Azure 네트워크를 설정 합니다.

1. Hello Azure 포털에서에서 선택 **가상 네트워크 만들기** hello 네트워크 이름, IP 주소 범위 및 서브넷 이름을 지정 합니다.
2. Toodo 장애 복구 해야 할 경우 VPN/ExpressRoute toohello 네트워크를 추가 합니다. VPN/ExpressRoute 장애 조치 후에 toohello 네트워크를 추가할 수 있습니다.

Azure 네트워크에 대한 자세한 내용은 [가상 네트워크 개요](../virtual-network/virtual-networks-overview.md)를 참조하세요.

> [!NOTE]
> [마이그레이션 네트워크의](../azure-resource-manager/resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 네트워크에 대 한 합니다.
>
>

## <a name="step-3-install-hello-vmware-components"></a>3 단계: hello VMware 구성 요소를 설치 합니다.
Tooreplicate VMware 가상 컴퓨터를 원하는 경우 hello 관리 서버에서 다음이 단계를 따르십시오.

1. [다운로드](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) 하여 설치합니다.
2. Hello 서버를 다시 시작 합니다.

## <a name="step-4-download-a-vault-registration-key"></a>4단계: 자격 증명 모음 등록 키 다운로드
1. Hello 관리 서버에서 Azure의 hello 사이트 복구 콘솔을 엽니다. Hello에 **복구 서비스** 페이지에서 자격 증명 모음 tooopen hello hello **빠른 시작** 페이지. Hello를 열 수도 있습니다 **빠른 시작** hello 아이콘을 클릭 하 여 언제 든 지 페이지입니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. Hello에 **빠른 시작** 페이지 **대상 리소스 준비** > **등록 키 다운로드**합니다. hello 등록 파일은 자동으로 생성 됩니다. 이 파일은 생성 후 5일 동안 유효합니다.

## <a name="step-5-install-hello-management-server"></a>5 단계: hello 관리 서버를 설치 합니다.
> [!TIP]
> 이러한 Url hello 관리 서버에서 액세스할 수 있는지 확인 합니다.
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



1. Hello에 **빠른 시작** 페이지, 통합 된 설치 파일 toohello 서버 hello를 다운로드 합니다.
2. Hello hello 설치 파일 toostart 설치를 실행할 **Site Recovery 통합 설치** 마법사.
3. **시작 하기 전에**선택, **hello 구성 서버와 프로세스 서버 설치**합니다.

   ![시작하기 전에](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. **제 3 자 소프트웨어 라이선스**, 클릭 **동의** toodownload 및 MySQL 설치 합니다.

    ![타사 소프트웨어](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. **등록**찾아 hello 자격 증명 모음에서 다운로드 한 hello 등록 키를 선택 합니다.

    ![등록](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. **인터넷 설정을**, hello 구성 서버에서 실행 되는 hello 공급자 hello 인터넷을 통해 tooAzure Site Recovery에 연결 하는 방법을 지정 합니다.

   * Tooconnect hello 컴퓨터에서 현재 설정 hello 프록시를 사용 하려는 경우 선택 **기존 프록시 설정 사용 하 여 연결**합니다.
   * Hello 공급자 tooconnect을 직접 하려는 경우 선택 **프록시 없이 직접 연결**합니다.
   * Hello 기존 프록시 인증이 필요 하거나 hello 공급자 연결에 대 한 사용자 지정 프록시 toouse을 하려는 경우 선택 **사용자 지정 프록시 설정 사용 하 여 연결**합니다.
     * 사용자 지정 프록시를 사용 하는 경우에 toospecify hello 주소, 포트 및 자격 증명 해야 합니다.
     * 프록시를 사용 하는 경우 해야 이미 허용한 다음 Url hello:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *.store.core.windows.net

    ![방화벽](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. **필수 구성 요소 확인**, hello 설치 실행할 수 있는지는 확인 toomake 실행 됩니다.

    ![필수 조건](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Hello에 대 한 경고가 나타나면 **동기화 확인이 글로벌 시간과**, hello 시스템 시계에 hello 시간을 확인 (**날짜 및 시간** 설정) hello 표준 시간대로 동일 hello 됩니다.

     ![시간 동기화 문제](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. **MySQL 구성**, toohello MySQL 서버 인스턴스에 설치 될 때까지 로그인에 대 한 자격 증명을 만듭니다.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. **환경 정보**tooreplicate VMware Vm 거 여부를 선택 합니다. 복제하는 경우 설치 프로그램에서 PowerCLI 6.0이 설치되어 있는지 확인합니다.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. **설치 위치**tooinstall hello 이진 파일을 hello 캐시를 저장 하는 경우 선택 합니다. 사용 가능한 디스크 공간이 5GB 이상인 드라이브를 선택할 수 있지만, 사용 가능한 디스크 공간이 600GB 이상인 캐시 드라이브를 사용하는 것이 좋습니다.

   ![설치 위치](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. **네트워크 선택**, hello 수신기 (네트워크 어댑터 및 SSL 포트)는 hello에 구성 서버 보내고 받도록 복제 데이터를 지정 합니다. Hello 기본값을 수정할 수 있습니다 (9443) 포트입니다. 또한 toothis 포트에서 복제 작업을 오케스트레이션 하는 웹 서버에서 포트 443 사용 됩니다. 복제 트래픽을 받는 데 443 포트를 사용하면 안됩니다.

    ![네트워크 선택](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. **요약**hello 정보 검토 하 고 클릭 **설치**합니다. 설치가 완료되면 암호가 생성됩니다. 복제를 사용하도록 설정할 때 필요하므로 암호를 복사하고 안전한 위치에 보관합니다.

   ![요약](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> hello Microsoft Azure 복구 서비스 에이전트 프록시를 설정 해야 합니다.
> Hello 설치가 완료 된 후 Microsoft Azure 복구 서비스 셸 hello hello Windows 시작 메뉴에서 시작 합니다. Hello 명령 창이 열리면 hello 프록시 서버 설정을 명령 tooset의 집합을 추적 하는 hello를 실행 합니다.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Hello 명령줄에서 설치 프로그램을 실행 합니다.
다음과 같이 hello 명령줄에서 hello 통합된 마법사를 실행할 수도 있습니다.

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

여기서,

* /ServerMode: 필수. Hello 설치 hello 구성 및 프로세스 서버 또는 hello 프로세스 서버 (사용 되는 tooinstall 추가 프로세스 서버) 설치 해야 하는지 여부를 지정 합니다. 입력 값: CS, PS.
* InstallDrive: 필수. Hello 구성 요소가 설치 되어 hello 폴더를 지정 합니다.
* /MySQLCredFilePath. 필수. Hello tooa 파일 경로 hello MySQL 서버 자격 증명 저장 되는 위치를 지정 합니다. Hello 템플릿 toocreate hello 파일을 가져옵니다.
* /VaultCredFilePath. 필수. Hello 자격 증명 모음 자격 증명 파일의 위치입니다.
* /EnvType. 필수. 설치 유형. 값: VMware, NonVMware
* /PSIP 및 /CSIP. 필수. Hello 프로세스 서버와 구성 서버 IP 주소입니다.
* /PassphraseFilePath. 필수. Hello 암호 파일의 위치입니다.
* /ByPassProxy. 선택 사항입니다. 프록시 없이 tooAzure 연결 하는 hello 관리 서버를 지정 합니다.
* /ProxySettingsFilePath. 선택 사항입니다. 작업에 대 한 사용자 지정 (기본 인증을 필요로 하는 hello 서버 프록시) 또는 사용자 지정 프록시 설정을 지정 합니다.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>6 단계: hello vCenter 서버에 대 한 자격 증명 설정
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

프로세스 서버 hello vCenter 서버에 의해 관리 되는 VMware Vm을 자동으로 검색할 수 있습니다. 사이트 복구에는 자동 검색에 대 한 계정 및 hello vCenter 서버에 액세스할 수 있는 자격 증명 필요 합니다. 물리적 서버만 복제하는 경우에는 관련이 없습니다.

tooset hello 계정 및 자격 증명:

1. Hello vCenter server에서 역할을 만듭니다 (**Azure_Site_Recovery**) hello로 hello vCenter 수준에서 [필요한 권한](#vmware-permissions-for-vcenter-access)합니다.
2. Hello 할당 **Azure_Site_Recovery** 역할 tooa vCenter 사용자입니다.

   > [!NOTE]
   > Hello 읽기 전용 역할을 보유 하는 vCenter 사용자 계정을 보호 된 컴퓨터를 종료 하지 않고 장애 조치를 실행할 수 있습니다. 해당 컴퓨터 다운 tooshut 원하는 Azure_Site_Recovery 역할 hello 해야 합니다. VMware tooAzure에서 Vm을 마이그레이션하만 toofail 다시 필요 하지 않은 경우 hello 읽기 전용 역할은 충분 합니다.
   >
   >
3. 열기 tooadd hello 계정 **cspsconfigtool**합니다. Hello 바탕 화면에서 바로 가기로 사용 가능 하 고 있는 폴더에 배치 됩니다 [설치 위치] hello \home\svsystems\bin 합니다.
4. Hello에 **계정 관리** 탭을 클릭 **계정 추가**합니다.

    ![계정 추가](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. **계정 세부 정보**를 사용 하는 tooaccess 일 수 있는 자격 증명 hello vCenter 서버를 추가 합니다. Hello 포털에서 계정 이름 tooappear hello에 대 일 분 이상 걸릴 수 있습니다. tooupdate 즉시 클릭 **새로 고침** hello에 **구성 서버** 탭 합니다.

    ![세부 정보](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>7단계: vCenter Server 또는 ESXi 호스트 추가
VMware Vm을 복제 하는 경우 tooadd vCenter 서버 (또는 ESXi 호스트) 필요.

1. Hello에 **서버** > **구성 서버** 탭에서 **vCenter 서버 추가**합니다.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. VCenter 서버 hello 또는 ESXi 호스트 세부 정보, tooaccess hello hello 이전 단계에서 vCenter 서버와 hello 프로세스 서버 hello vCenter 서버에서 관리 되는 사용 되는 toodiscover VMware Vm 수를 지정 된 hello 계정의 hello 이름을 추가 합니다. vCenter 서버 hello 또는 ESXi 호스트 hello는 hello 프로세스 서버 설치 된 hello 서버와 동일한 네트워크에 있어야 합니다.

   > [!NOTE]
   > VCenter 서버 hello 또는 hello vCenter 또는 호스트 서버에 대 한 관리자 권한이 없는 계정으로 ESXi 호스트를 추가 하는 경우 hello vCenter 또는 ESXi 계정이 이러한 권한을 사용할 수 있어야 하 고 있는지 확인: 데이터 센터, 데이터 저장소, 폴더, Jost, 네트워크, 리소스, 가상 컴퓨터 및 vSphere 분산 스위치입니다. hello vCenter 서버에는 권한 사용 하도록 설정 하는 hello 저장소 뷰가 필요 합니다.
   >
   >

    ![vCenter 서버 추가](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Hello vCenter 서버 hello에 나열 됩니다 검색을 완료 한 다음 **구성 서버** 탭 합니다.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>8단계: 보호 그룹 만들기
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

보호 그룹에 가상 컴퓨터의 논리적 그룹인 또는 실제 서버를 사용 하 여 tooprotect 되도록 hello 동일한 보호 설정을 하십시오. 보호 설정 tooa 보호 그룹에서 적용 되며 이러한 설정이 적용 된 tooall 컴퓨터 (가상 또는 물리적) toohello 그룹을 추가 합니다.

1. 너무 이동**보호 된 항목** > **보호 그룹** hello 아이콘 tooadd 보호 그룹을 클릭 합니다.

    ![보호 그룹 만들기](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. Hello에 **보호 그룹 설정 지정** 페이지 hello 그룹의 이름을 지정 합니다. Hello에 **에서** 드롭 다운 목록, 선택 hello 구성 서버 toocreate hello 그룹 원하는 합니다. **대상**은 Microsoft Azure입니다.

    ![보호 그룹 설정](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. Hello에 **복제 설정 지정** 페이지 hello 그룹의 모든 hello 컴퓨터에 사용할 hello 복제 설정을 구성 합니다.

    ![보호 그룹 복제](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **다중 VM 일관성**:를 설정 하면이 hello 시스템 hello 보호 그룹에 대해 공유 응용 프로그램 일치 복구 지점을 만듭니다. 이 설정은 hello 보호 그룹의 모든 컴퓨터에서 실행 중인 경우에 가장 관련성이 높은 hello 같은 작업입니다. 모든 컴퓨터는 복구 된 toohello 됩니다 동일한 데이터 요소입니다. 이는 VMware VM 또는 물리적 서버(Windows 또는 Linux)를 복제하는지 여부에 상관없이 사용할 수 있습니다.
   * **RPO 임계값**: 집합 hello RPO 합니다. Hello 지속적인 데이터 보호 복제 구성 hello RPO 임계값을 초과할 때 경고가 생성 됩니다.
   * **복구 지점 보존**: hello 보존 기간을 지정 합니다. 보호 된 컴퓨터 수 있는이 창에서 tooany 포인트를 복구 합니다.
   * **응용 프로그램 일치 스냅숏 빈도**: 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 빈도를 지정합니다.

Hello 확인 표시를 선택 하면 보호 그룹 지정한 hello 이름으로 만들어집니다. 또한, 두 번째 보호 그룹을 만듭니다 hello 이름의 *보호 그룹 이름*-장애 복구 합니다. 이 보호 그룹에 장애 조치 tooAzure 후 뒤로 toohello 온-프레미스 사이트를 실패 한 경우 사용 됩니다. Hello에 만들어질 때 hello 보호 그룹을 모니터링할 수 있습니다 **보호 된 항목** 페이지.

## <a name="step-9-install-hello-mobility-service"></a>9 단계: hello 모바일 서비스를 설치 합니다.
가상 컴퓨터 및 물리적 서버에 대 한 보호를 사용 하기 위한 hello 첫 번째 단계는 tooinstall hello 이동성 서비스입니다. 다음 두 가지 방법으로 수행할 수 있습니다.

* 자동으로 강제 하 고 hello 프로세스 서버에서 각 컴퓨터에 hello 서비스를 설치 합니다. 컴퓨터 tooa 보호 그룹을 추가 하 고 적절 한 버전의 hello 모바일 서비스가 이미 실행 중인 경우 강제 설치도 발생 하지 않습니다. WSUS 또는 System Center Configuration Manager와 같은 엔터프라이즈 밀어넣기 메서드를 사용 하 여 hello 서비스를 자동으로 설치할 수 있습니다. 이렇게 하기 전에 hello 관리 서버를 설정한 있는지 확인 합니다.
* Tooprotect 하려는 각 컴퓨터에 수동으로 hello 서비스를 설치 합니다. 이렇게 하기 전에 hello 관리 서버를 설정한 있는지 확인 합니다.

### <a name="install-hello-mobility-service-with-push-installation"></a>Hello 모바일 서비스를 강제 설치로 설치
컴퓨터 tooa 보호 그룹을 추가 하면 hello 모바일 서비스가 자동으로 푸시 및 hello 프로세스 서버에서 각 컴퓨터에 설치 합니다.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Windows 컴퓨터에서 자동 푸시 준비
tooprepare hello 프로세스 서버에서 해당 hello 모바일 서비스를 자동으로 설치할 수 있도록 Windows 컴퓨터:

1. 해당 hello 프로세스 서버 tooaccess hello 컴퓨터를 사용할 수 있는 계정을 만듭니다. hello 계정 (로컬 또는 도메인) 관리자 권한이 있어야 합니다. 이러한 자격 증명 hello 모바일 서비스의 강제 설치에 대해서만 사용 됩니다.

   > [!NOTE]
   > 도메인 계정을 사용 하지 않는 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 해야 합니다. toodo이를 찾아, 아래 hello 레지스트리에서 hello DWORD로 항목을 추가 LocalAccountTokenFilterPolicy 값이 1에서 합니다. CLI에서 tooadd hello 레지스트리 항목 열기 명령 또는 PowerShell을 사용 하 여 입력  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 합니다.
   >
   >
2. Tooprotect hello 컴퓨터에서 Windows 방화벽에 대 한 선택 **앱 또는 기능 방화벽을 통해 허용**, 사용 하도록 설정 하 고 **파일 및 프린터 공유** 및 **Windows 관리 계측**합니다. 에 tooa 도메인에 속하는 컴퓨터에 대 한 GPO와 hello 방화벽 정책을 구성할 수 있습니다.

   ![방화벽 설정](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. 사용자가 만든 hello 계정을 추가 합니다.

   * **cspsconfigtool**을 엽니다. Hello 바탕 화면에서 바로 가기로 사용 가능 하 고 있는 폴더에 배치 됩니다 [설치 위치] hello \home\svsystems\bin 합니다.
   * Hello에 **계정 관리** 탭을 클릭 **계정 추가**합니다.
   * 사용자가 만든 hello 계정을 추가 합니다. Hello 계정을 추가한 후 컴퓨터 tooa 보호 그룹을 추가할 때 tooprovide hello 자격 증명을 해야 합니다.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Linux 서버에서 자동 푸시 준비
1. 해당 hello Linux 컴퓨터에 설명 된 대로 tooprotect 사용할 수 있는지 확인 [온-프레미스 필수 구성 요소](#on-premises-prerequisites)합니다. 네트워크로 연결 되어 있는지 확인 하려는 hello 프로세스 서버를 실행 하는 hello 및 tooprotect 관리 서버 hello 컴퓨터 간에 합니다.
2. 해당 hello 프로세스 서버 tooaccess hello 컴퓨터를 사용할 수 있는 계정을 만듭니다. hello 계정 hello 원본 Linux 서버에 루트 사용자 여야 합니다. 이러한 자격 증명 hello 모바일 서비스의 강제 설치에 대해서만 사용 됩니다.

   * **cspsconfigtool**을 엽니다. Hello 바탕 화면에서 바로 가기로 사용 가능 하 고 있는 폴더에 배치 됩니다 [설치 위치] hello \home\svsystems\bin 합니다.
   * Hello에 **계정 관리** 탭을 클릭 **계정 추가**합니다.
   * 사용자가 만든 hello 계정을 추가 합니다. Hello 계정을 추가한 후 컴퓨터 tooa 보호 그룹을 추가할 때 tooprovide hello 자격 증명을 해야 합니다.
3. Hello 소스 Linux 모든 네트워크 어댑터와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목을 포함 하는 서버에서 해당 hello /etc/hosts 파일을 확인 합니다.
4. Tooprotect hello 컴퓨터에 hello 최신 openssh, openssh-서버 및 openssl 패키지를 설치 합니다.
5. SSH가 22 포트에서 사용되고 실행 중인지 확인합니다.
6. 다음과 같이 hello sshd_config 파일에서 SFTP 하위 시스템 및 암호 인증을 사용 합니다.

   * 루트로 로그인합니다.
   * Hello /etc/ssh/sshd_config 파일에서 PasswordAuthentication로 시작 하는 hello 줄을 찾습니다.
   * Hello 줄 주석을 제거 하 고 hello 값에서 변경 **없습니다** 너무**예**합니다.
   * 로 시작 하는 찾기 hello 줄 **하위 시스템** hello 줄에서 주석 처리 제거 합니다.

     ![Linux에서 기본값(하위 시스템 없음) 재정의](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Hello 모바일 서비스를 수동으로 설치
hello 설치 관리자는 C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository에서 사용할 수 있습니다.

| 원본 운영 체제 | 모바일 서비스 설치 파일 |
| --- | --- |
| Windows Server(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5(64비트만 해당) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Windows server에서 hello 모바일 서비스를 수동으로 설치
1. 다운로드 하 고 hello 관련 설치 관리자를 실행 합니다.
2. **시작하기 전에**에서 **모바일 서비스**를 선택합니다.

    ![모바일 서비스 설치](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. **구성 서버 세부 정보**hello hello 관리 서버의 IP 주소를 지정 하 고 hello 관리 서버 구성 요소를 설치할 때 생성 된 암호를 hello 합니다. 실행 하 여 hello 암호를 검색할 수 있습니다  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello 관리 서버에 있습니다.

    ![모바일 서비스](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. **설치 위치**hello 기본 위치를 유지 하 고 클릭 **다음** toobegin 설치 합니다.
5. **설치 진행률**, 설치를 확인 하 고 메시지가 표시 되 면 hello 컴퓨터를 다시 시작 합니다.

Hello 텍스트 hello 명령줄에 다음을 입력 하 여 설치할 수 있습니다.

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

명령 앞 hello:

* /Role: 필수. Hello 모바일 서비스를 설치 해야 하는지 여부를 지정 합니다.
* /InstallLocation: 필수. 여기서 tooinstall hello 서비스를 지정 합니다.
* /PassphraseFilePath: 필수. Hello 구성 서버 암호가 지정합니다.
* /LogFilePath: 필수. Hello 로그 설치 파일 위치를 지정합니다.

#### <a name="uninstall-hello-mobility-service-manually"></a>Hello 모바일 서비스를 수동으로 제거
사용 하 여 hello 모바일 서비스를 제거할 수 있습니다 **제거 또는 변경 프로그램** 제어판 또는 명령줄 hello를 사용 하 여 합니다.

다음은 hello 명령 toouninstall hello 명령줄을 사용 하 여 모바일 서비스입니다.

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>관리 서버 hello hello IP 주소 변경
Hello 마법사를 실행 한 후 다음과 같이 hello hello 관리 서버의 IP 주소를 변경할 수 있습니다.

1. Hello 파일 hostconfig.exe를 (hello 바탕 화면에 있음)를 엽니다.
2. Hello에 **Global** 탭 hello hello 관리 서버의 IP 주소를 변경 합니다.

   > [!NOTE]
   > Hello 관리 서버의 IP 주소는 hello만 변경 합니다. 관리 서버 간 통신에 대 한 hello 포트 번호 443을 해야 합니다. 및 **사용 하 여 HTTPS** 왼쪽 활성화 해야 합니다. Hello 암호를 변경 하지 마십시오.
   >
   >

    ![관리 서버 IP 주소](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Linux 서버에 hello 모바일 서비스를 수동으로 설치
1. 원하는 tooprotect hello 적절 한 tar 보관 toohello Linux 컴퓨터를 복사 합니다. Hello 표를 참고 [hello 모바일 서비스를 수동으로 설치](#install-the-mobility-service-manually) 어떤 tar 보관 toodetermine 사용 해야 합니다.
2. 셸 프로그램을 열고 실행 하 여 hello 압축 된 tar 보관 tooa 로컬 경로 추출 합니다.`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Passphrase.txt 라는 파일을 만들어 hello 로컬 디렉터리 toowhich hello tar 보관의 hello 내용을 추출한 합니다. toodo이, 복사 hello C:\ProgramData\Microsoft Azure 사이트 Recovery\private\connection.passphrase에서 hello 관리 서버에 대 한 저장에 암호를 실행 하 여 passphrase.txt  *`echo <passphrase> >passphrase.txt`*  hello 셸에서 합니다.
4. Hello 다음 명령을 입력 하 여 hello 모바일 서비스를 설치 합니다.*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Hello hello 관리 서버의 내부 IP 주소를 지정 하 고 포트 443이 선택 되어 있는지 확인 합니다.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Hello 명령줄에서 hello 모바일 서비스를 설치 합니다.

Hello 암호 hello 관리 서버에서 C:\Program Files (x86) \InMage Systems\private\connection에서 복사한 hello 관리 서버의 "passphrase.txt"로 저장 합니다. Hello 다음 명령을 실행 합니다. 예에서 hello 관리 서버 IP 주소는 104.40.75.37 및 hello HTTPS 포트는 443:

프로덕션 서버의 tooinstall:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

마스터 대상 서버 hello에 tooinstall:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>10단계: 컴퓨터의 보호 활성화
tooenable 보호 가상 컴퓨터 및 물리적 서버 tooa 보호 그룹을 추가 합니다. 시작 하기 전에 hello 다음 note VMware 가상 컴퓨터를 보호 하는 경우:

* VMware Vm에는 15 분 마다 검색 하 고 걸릴 수 있습니다에 대 일 분 넘게 tooappear hello Site Recovery 포털에서 검색 한 후 합니다.
* 환경 변화 hello 가상 컴퓨터 (예: VMware 도구 설치)에서 사이트 복구에서 업데이트 하는 15 분 toobe 보다도 걸릴 수 있습니다.
* Hello 마지막으로 검색 한 시간 VMware Vm에 대 한 hello에서 확인할 수 있습니다 **마지막 연락처에** hello vCenter 서버/ESXi 호스트 hello에 대 한 필드 **구성 서버** 탭 합니다.
* 보호 그룹을 만든 후 vCenter Server 또는 ESXi 호스트를 추가 하는 경우 가상 컴퓨터 toobe hello에 나열 된 및 Azure 사이트 복구 포털 toorefresh hello에 대 일 분 이상 걸릴 수 있습니다 **컴퓨터 tooa 보호 그룹 추가**대화 상자.
* 즉시 tooproceed 원하는 hello에 예약 된 검색까지 기다리지 않고 컴퓨터 tooa 보호 그룹을 추가 하는 경우 hello 구성 서버를 강조 표시 (클릭 하지 말고)를 클릭 하 고 **새로 고침**합니다.

또한,

* 워크로드를 미러링하도록 보호 그룹을 설계하는 것이 좋습니다. 예를 들어 특정 응용 프로그램 toohello를 실행 하는 컴퓨터를 추가 같은 그룹입니다.
* 컴퓨터 tooa 보호 그룹을 추가할 때 hello 프로세스 서버가 자동으로 푸시하고 이미 설치 되어 있지 않으면 hello 모바일 서비스를 설치 합니다. Hello 이전 단계에 설명 된 대로 준비한 toohave hello 푸시 메커니즘이 필요 합니다.

### <a name="add-machines-tooa-protection-group"></a>컴퓨터 tooa 보호 그룹 추가

1. 너무 이동**보호 된 항목** > **보호 그룹** > **컴퓨터** > **추가 컴퓨터** .
2. VMware 가상 컴퓨터에서 보호 하려는 경우 **가상 컴퓨터 선택**, 가상 컴퓨터 (또는 실행 하는 hello EXSi 호스트)를 관리 하 고 있는 vCenter 서버를 선택 하 고 hello 컴퓨터를 선택 합니다.

    ![가상 컴퓨터의 보호 활성화](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. 물리적 서버에서 보호 하려는 경우 **가상 컴퓨터 선택**개방형 hello **물리적 컴퓨터 추가** 마법사 hello IP 주소 및 친숙 한 이름을 입력 하십시오. Hello 운영 체제 제품군을 선택 합니다.

   ![물리적 서버 보호를 사용하도록 설정](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. **대상 리소스 지정**, 복제에 사용 하는 hello 저장소 계정을 선택 하 고 모든 작업에 대해 hello 설정을 사용할지 여부를 선택 합니다. 프리미엄 저장소 계정은 현재 지원되지 않습니다.

   > [!NOTE]
   > Hello를 사용 하 여 만든 이동 저장소 계정을 지원 하지 않습니다 [Azure 포털](../storage/storage-create-storage-account.md) 리소스 그룹에 걸쳐 있습니다.                           
   > [저장소 계정 마이그레이션](../azure-resource-manager/resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 저장소 계정에 대 한 합니다.
   >
   >

    ![대상 설정 구성](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. **계정 지정**선택, hello 계정이 [설정](#install-the-mobility-service-with-push-installation) toouse hello 모바일 서비스의 자동 설치에 대 한 합니다.

    ![계정 지정](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Hello 확인 표시가 toofinish 컴퓨터 toohello 보호 그룹과 toostart 초기 복제 각 컴퓨터에 대 한 추가 클릭 합니다.

   > [!NOTE]
   > 강제 설치를 준비 하는 경우 hello 모바일 서비스는 자동으로 toohello 보호 그룹을 추가 하는 설치 하지 않는 컴퓨터에 설치 됩니다. Hello 서비스를 설치한 후 보호 작업을 시작 하 고 실패 합니다. Hello 실패 후에 있던 각 컴퓨터에 설치 하는 모바일 서비스 hello toomanually 다시 시작을 해야 합니다. Hello 다시 시작한 후 hello 보호 작업 다시 시작 하 고 초기 복제가 발생 합니다.
   >
   >

Hello에 상태를 모니터링할 수 **작업** 페이지.

![Hello 작업 페이지에서 상태 모니터링](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

보호 상태는 **보호된 항목** > *보호 그룹 이름* > **가상 컴퓨터**에서 모니터링할 수도 있습니다. 초기 복제가 완료 된 후 데이터 동기화가 컴퓨터 상태를 변경할 수 너무**Protected**합니다.

![보호된 항목의 상태 모니터링](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>11단계: 보호된 컴퓨터 속성 설정
1. 컴퓨터가 **보호됨** 상태이면 해당 장애 조치(failover) 속성을 구성할 수 있습니다. Hello 보호 그룹 세부 정보에서 선택 hello 시스템 및 열기 hello **구성** 탭 합니다.
2. 사이트 복구를 자동으로 hello Azure VM에 대 한 속성을 소개 하 고 hello 온-프레미스 네트워크 설정을 검색 합니다.

    ![가상 컴퓨터 등록 설정](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. 다음 설정을 변경할 수 있습니다.

   * **Azure VM 이름**: 제공 될 toohello 컴퓨터 Azure에서 장애 조치 후 hello 이름입니다. hello 이름은 Azure 요구 사항을 준수 해야 합니다.
   * **Azure VM 크기**: hello 대상 가상 컴퓨터에 대해 지정 하는 네트워크 어댑터의 hello 수 hello 크기에 따라 결정 됩니다. 크기 및 어댑터에 대 한 자세한 내용은 참조 hello [테이블 크기](../virtual-machines/linux/sizes.md)합니다. 다음 사항에 유의하세요.

     * 네트워크 어댑터 수가 hello hello를 열 때 변경 됩니다 가상 컴퓨터의 hello 크기를 수정 하 고 hello 설정을 저장할 때 **구성** 탭 hello 다음 번입니다. hello 최소 대상 가상 컴퓨터에서 네트워크 어댑터의 번호가 같으면 toohello 원본 가상 컴퓨터에서 네트워크 어댑터의 최소 수입니다. 네트워크 어댑터의 최대 개수 hello hello 가상 컴퓨터의 hello 크기에 따라 결정 됩니다.
       * 작은 hello hello 원본 컴퓨터의 네트워크 어댑터 수가 경우 보다 짧거나 toohello 어댑터 허용 된 수의 hello 대상 컴퓨터 크기에 대 한 hello 대상 갖습니다 hello hello 소스와 같은 수의 어댑터.
       * Hello 대상 크기에 허용 된 hello 수를 초과 하는 hello 원본 가상 컴퓨터에 대 한 어댑터의 hello 수, hello 대상 크기는 최대 사용 됩니다.
        예를 들어, 원본 컴퓨터에 네트워크 어댑터가 두 개 있고을 hello 대상 컴퓨터 크기를 지 원하는 4 개 경우 hello 대상 컴퓨터에 두 개의 어댑터 갖습니다. Hello 원본 컴퓨터에 두 개의 어댑터가 지원 hello 대상 크기를 지 원하는 하나만 표시 되지만 hello 대상 컴퓨터에 어댑터를 하나만 갖습니다.
     * 모든 어댑터가 연결 된 toohello 해야 hello 가상 컴퓨터 네트워크 어댑터가 여러 개 있는 경우 동일한 Azure 네트워크입니다.
   * **Azure 네트워크**: Azure Vm 연결된 tooafter 장애 조치 되도록 Azure 네트워크를 지정 해야 합니다. 하나를 지정 하지 않으면, hello Azure Vm에 연결 된 tooany 네트워크 수 없습니다. 또한 Azure toohello 온-프레미스 사이트에서 toofailback 하려는 경우 Azure 네트워크 toospecify가 필요 합니다. 장애 복구(failback)를 위해서는 Azure 네트워크와 온-프레미스 네트워크 간의 VPN 연결이 필요합니다.
   * **Azure IP 주소/서브넷**: 각 네트워크 어댑터에 대 한 Azure VM에 연결 해야 하는 hello 서브넷 toowhich hello를 선택 합니다. 참고 hello 원본 컴퓨터의 hello 네트워크 어댑터 구성된 toouse 고정 IP 주소를 hello Azure VM에 대 한 고정 IP 주소를 지정할 수 있습니다. 고정 IP 주소를 제공하지 않으면 사용 가능한 IP 주소가 할당됩니다. Hello 대상 IP 주소를 지정 하는 경우 이미 사용 중인 Azure의 다른 VM에서 장애 조치가 실패 합니다. Hello 원본 컴퓨터의 hello 네트워크 어댑터 구성된 toouse DHCP를 DHCP Azure 용 hello 설정으로 해야 합니다.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>12단계: 복구 계획 만들기 및 장애 조치 실행
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

단일 컴퓨터에 대 한 장애 조치를 실행 하거나 hello 작업 같거나 hello 실행을 수행 하는 여러 가상 컴퓨터가 장애 조치할 수 있습니다 같은 작업입니다. 동일한 hello에 여러 통해 toofail 컴퓨터 시간이 tooa 복구 계획에 추가 합니다.

복구 계획 toocreate:

1. Hello에 **복구 계획** 페이지 **복구 계획 추가** 복구 계획을 추가 합니다. Hello 계획에 대 한 세부 정보를 지정 하 고 선택 **Azure** hello 대상으로 합니다.

 ![복구 계획 구성](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. **가상 컴퓨터 선택**보호 그룹을 선택한 다음 hello 그룹 tooadd toohello 복구 계획에 컴퓨터를 선택 합니다.

 ![가상 컴퓨터 추가](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

Hello 계획 toocreate 그룹과 시퀀스 hello 순서는 컴퓨터 hello 복구 계획에는 장애 조치를 사용자 지정할 수 있습니다. 수동 작업 및 스크립트에 대한 프롬프트를 추가할 수도 있습니다. 스크립트를 수동으로 또는 [Azure Automation Runbook](site-recovery-runbook-automation.md)을 사용하여 만듭니다. 복구 계획 사용자 지정에 대한 자세한 내용은 [복구 계획 만들기](site-recovery-create-recovery-plans.md)를 참조하세요.

## <a name="run-a-failover"></a>장애 조치(Failover) 실행
장애 조치를 실행하기 전에 다음을 수행합니다.

* 해당 hello 관리 서버에서 실행 중 이며 사용할 수 있는지 확인 합니다. 그렇지 않으면 장애 조치가 실패합니다.
* 계획되지 않은 장애 조치를 실행하는 경우:

  * 가능한 경우 계획되지 않은 장애 조치를 실행하기 전에 주 컴퓨터를 종료해야 합니다. 이렇게 하면 hello에서 실행 되는 두 hello 원본 및 복제본 컴퓨터 없는지 동시 합니다. 예기치 않은 장애 조치가 실행 하는 경우 VMware Vm을 복제 하는, 사이트 복구 hello 소스 컴퓨터 다운 tooshut을 시도해 야을 지정할 수 있습니다. Hello hello 기본 사이트의 상태에 따라이 하거나 작동 하지 않을 수 있습니다. 물리적 서버를 복제하는 경우 Site Recovery에서 이 옵션을 제공하지 않습니다.
  * 계획되지 않은 장애 조치는 주 컴퓨터에서 데이터 복제를 중지하므로 계획되지 않은 장애 조치를 시작한 후 모든 데이터 델타가 전송되지 않습니다.
  * 장애 조치 후 Azure에서 tooconnect toohello 복제 가상 컴퓨터를 원하는 경우는 hello 장애 조치를 실행 하기 전에 hello 원본 컴퓨터에서 원격 데스크톱 연결을 사용 합니다. Hello 방화벽을 통한 RDP 연결을 허용 합니다. 또한 장애 조치 후 hello hello Azure 가상 컴퓨터의 공용 끝점에 RDP tooallow를 해야 합니다. 에 따라 [모범 사례](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure RDP 장애 조치 후 사용할 수 있는 합니다.

> [!NOTE]
> 장애 조치 tooAzure 작업을 수행할 때 hello에 tooget 최상의 성능을 제공 hello 보호 된 컴퓨터에서 hello Azure 에이전트를 설치 했는지 확인 합니다. Hello 컴퓨터 부팅 더 빠르게 고 문제를 진단 하는 데 도움이 됩니다. hello Azure 에이전트를 사용할 수에 대 한 [Linux](https://github.com/Azure/WALinuxAgent) 및 [Windows](http://go.microsoft.com/fwlink/?LinkID=394789)합니다.
>
>

### <a name="run-a-test-failover"></a>테스트 장애 조치(Failover) 실행
테스트 장애 조치 toosimulate 프로그램 장애 조치를 실행 하 고 프로덕션 환경에 영향을 주지 정기 복제 하는 격리 된 네트워크에서 복구 프로세스를 정상적으로 계속 합니다. 테스트 장애 조치 hello 원본의 initiatd 이며 여러 가지 방법으로 실행할 수 있습니다.

* **Azure 네트워크를 지정 하지 않으면**: 네트워크 없이 테스트 장애 조치를 실행 하면 가상 컴퓨터를 시작 하 고 Azure에 올바르게 표시 hello 테스트 확인 됩니다. 가상 컴퓨터 장애 조치 후 연결 된 Azure 네트워크 tooan 수 없습니다.
* **Azure 네트워크를 지정**:이 유형의 장애 조치는 hello 전체 복제 환경이 예상 대로 표시 되며 지정 된 네트워크를 Azure 가상 컴퓨터가 연결 된 toohello 있는지 확인 합니다.

테스트 장애 조치 toorun:

1. Hello에 **복구 계획** 페이지에서 클릭 하 고 hello 계획 선택 **테스트 장애 조치**합니다.

 ![Hello 계획 선택](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. **확인 테스트 장애 조치**선택, **None** tooindicate hello 테스트 장애 조치에 대해 toouse Azure 네트워크를 원하지 또는 select hello 네트워크 toowhich hello 테스트 Vm 장애 조치 후 연결 됩니다. Hello 확인 표시가 toostart hello 장애 조치를 클릭 합니다.

 ![선택](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Hello에 대 한 장애 조치 진행률 모니터링 **작업** 탭 합니다.

 ![진행률 모니터링](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Hello 장애 조치 완료 되 면도 있어야 toosee hello 복제본 Azure 컴퓨터에 표시 **가상 컴퓨터** hello Azure 포털의에서. Azure VM의 RDP 연결 toohello tooinitiate 원하는 hello VM 끝점에 tooopen 포트 3389 해야 합니다.
5. 한 후 작업이 끝난 후에 장애 조치에 도달 하면 hello **완료** 테스트 단계를 클릭 하 여 **전체 테스트** toofinish 합니다. **노트**을 기록 하 고 테스트 장애 조치 hello와 관련 된 모든 관찰을 저장 합니다.
6. 클릭 **hello 테스트 장애 조치가 완료** tooautomatically hello 테스트 환경을 정리 합니다. 이 작업을 테스트 장애 조치 hello 표시 됩니다는 **완료** 상태입니다. 모든 요소 또는 hello 테스트 장애 조치 시 자동으로 만들어진 Vm 삭제 됩니다. 2 주 넘게 테스트 장애 조치를 계속 하는 경우 강제로 toofinish 합니다.

### <a name="run-an-unplanned-failover"></a>계획되지 않은 장애 조치 실행
계획 되지 않은 장애 조치는 Azure에서 시작 되며 hello 기본 사이트를 사용할 수 없는 경우에 수행할 수 있습니다.

1. Hello에 **복구 계획** 페이지에서 클릭 하 고 hello 계획 선택 **장애 조치** > **계획 되지 않은 장애 조치**합니다.

 ![Hello 계획 선택](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. VMware 가상 컴퓨터를 복제 하는 경우 온-프레미스 Vm 아래로 tooshut을 시도할 수 있습니다. 이 최상의 노력 작업 및 장애 조치 hello 노력 여부 성공 여부를 계속 합니다. Hello에 오류 정보가 표시 되며 성공 하지 못한 경우 **작업** 탭의 **계획 되지 않은 장애 조치 작업**합니다.

 ![온-프레미스 VM 종료 옵션](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > 이 옵션은 물리적 서버를 복제하는 경우에는 사용할 수 없습니다. 해야 tootry tooshut 것 아래로 수동으로 가능 하면 합니다.
 >
 >

3. **확인 장애 조치**hello 장애 조치 방향 (tooAzure)를 확인 하 고 toouse hello 장애 조치에 사용할 hello 복구 지점을 선택 합니다. 복제 속성을 구성할 때 여러 VM을 설정한 경우 toohello 최신 응용 프로그램이 나 크래시 일관성이 있는 복구 지점을 복구할 수 있습니다. 선택할 수도 있습니다 **사용자 지정 복구 지점** toorecover tooan 이전 지정 시간입니다. Hello 확인 표시가 toostart hello 장애 조치를 클릭 합니다.

 ![장애 조치 방향 확인](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Hello에 대 한 대기 작업 toofinish 계획 되지 않은 장애 조치 합니다. Hello에 장애 조치 진행률을 모니터링할 수 **작업** 탭 합니다. 계획 되지 않은 장애 조치 중에 오류가 발생 하는 경우에 hello 복구 계획에는 완료 될 때까지 실행 합니다. 또한 있어야 toosee hello 복제본 Azure 컴퓨터에 표시 **가상 컴퓨터** hello Azure 포털의에서.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>연결 tooreplicated Azure 장애 조치 후 가상 컴퓨터
tooconnect tooreplicated Azure의 가상 컴퓨터 장애 조치 후, 해야합니다.

- 원격 데스크톱 연결을 hello 주 컴퓨터에서 사용 하도록 설정 합니다.
- Hello 주 컴퓨터에서 Windows 방화벽 tooallow RDP를 설정합니다.
- RDP은 toohello hello Azure 가상 컴퓨터에 대 한 공용 끝점을 추가 합니다.

이렇게 설정하는 방법에 대한 자세한 내용은 [ASR을 사용하여 장애 조치 후 원격 데스크톱 연결 문제 해결](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx)(영문)을 참조하세요.

## <a name="deploy-additional-process-servers"></a>추가 프로세스 서버 배포
원본 컴퓨터를 200 개 초과 배포 수평 확장 해야 합니다 또는 프로그램 총 일별 변동률 2TB를 초과 하는 경우에 추가 프로세스 서버 toohandle hello 트래픽 볼륨이 필요 합니다. tooset 검사 hello 요구 사항에는 추가 프로세스 서버를 설치한 [추가 프로세스 서버](#additional-process-servers), 및 지침을 따라 toohello hello 프로세스 서버를 설정 합니다. Hello 서버를 설정한 후에 원본 컴퓨터 toouse을 구성할 수 있습니다 것입니다.

### <a name="set-up-an-additional-process-server"></a>추가 프로세스 서버 설정
다음과 같이 추가 프로세스 서버를 설정합니다.

* 프로세스 서버를 전용으로 통합 하는 hello 마법사 tooconfigure 관리 서버를 실행 합니다.
* 만 hello 새 프로세스 서버를 사용 하 여 toomanage 데이터 복제를 원하는 경우 toomigrate 보호 된 컴퓨터가 필요.

### <a name="install-hello-process-server"></a>Hello 프로세스 서버 설치
1. Hello에 **빠른 시작** 페이지, hello Site Recovery 구성 요소 설치에 대 한 hello 통합 된 설치 파일을 다운로드 합니다. 설치 프로그램을 실행합니다.
2. **시작 하기 전에**선택, **배포 아웃 추가 프로세스 서버 tooscale 추가**합니다.

 ![프로세스 서버 추가](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. 때 수행한 대로 hello 마법사를 완료 하면 [설정](#step-5-install-the-management-server) hello 첫 번째 관리 서버입니다.
4. **구성 서버 세부 정보**를 hello 원래 관리 서버 hello 구성 서버를 설치한 hello IP 주소를 입력 한 다음 hello 암호를 입력 합니다. Hello 암호가 없는 경우 실행  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** hello 원래 관리 서버 tooretrieve에 해당 합니다.

 ![구성 서버 세부 정보](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>컴퓨터 toouse hello 새 프로세스 서버 마이그레이션
1. 열기 **구성 서버** > **서버** > *hello 원래 관리 서버 이름*  >   **서버 세부 정보**합니다.

 ![서버 세부 정보](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. Hello에 **프로세스 서버** 목록에서 **프로세스 서버 변경** toochange 되도록 다음 toohello 서버입니다.

 ![Hello 프로세스 서버를 업데이트 합니다.](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. 선택 **프로세스 서버 변경**선택, **대상 프로세스 서버**을 다음 선택 hello 새 관리 서버 및 합니다. 그런 다음 새 프로세스 서버 hello 선택 hello 가상 컴퓨터를 처리 합니다. Hello 정보 아이콘 tooget hello 서버에 대 한 정보를 클릭 합니다. 필요한 각 선택한 가상 컴퓨터 toohello 새 프로세스 서버를 결정 로드를 확인 하는 표시 된 toohelp tooreplicate 평균 공간 hello입니다. Hello 확인 표시가 toostart 복제 toohello 새 프로세스 서버를 클릭 합니다.

 ![Hello 프로세스 서버 변경](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>vCenter 액세스를 위한 VMware 권한
hello 프로세스 서버 vCenter 서버에 Vm을 자동으로 검색할 수 있습니다. tooperform 자동 검색을 hello vCenter 수준 tooallow 사이트 복구 tooaccess hello vCenter 서버에서 역할 (Azure_Site_Recovery) toodefine가 필요한 합니다. 만 toomigrate VMware 컴퓨터 tooAzure 하 고 Azure에서 toofailback 필요 하지 않습니다, 충분 하는 읽기 전용 역할을 정의할 수 있습니다. 에 설명 된 대로 hello 사용 권한을 설정 [6 단계: hello vCenter 서버에 대 한 자격 증명 설정](#step-6-set-up-credentials-for-the-vcenter-server)합니다. hello 역할 사용 권한은 다음 표에 hello에 요약 되어 있습니다.

| **역할** | **세부 정보** | **권한** |
| --- | --- | --- |
| Azure_Site_Recovery 역할 |VMware VM 검색 |Hello v Center 서버에 대 한 이러한 권한을 할당 합니다.<br/><br/>데이터 저장소: 공간 할당, 데이터 저장소 찾아보기, 낮은 수준 파일 작업, 파일 제거, 가상 컴퓨터 파일 업데이트<br/><br/>네트워크: 네트워크 할당<br/><br/>리소스: 가상 컴퓨터 tooresource 풀, 가상 컴퓨터가 전원 꺼짐 마이그레이션, 마이그레이션 전원이 켜진 가상 컴퓨터 할당<br/><br/>태스크: 만들기 태스크, 업데이트 태스크<br/><br/>가상 컴퓨터 > 구성<br/><br/>가상 컴퓨터 > 상호 작용 > 질문 응답, 장치 연결, CD 미디어 구성, 플로피 미디어 구성, 전원 끄기, 전원 켜기, VMware 도구 설치<br/><br/>가상 컴퓨터 > 인벤토리 > 만들기, 등록, 등록 취소<br/><br/>가상 컴퓨터 > 프로비전 > 가상 컴퓨터 다운로드 허용, 가상 컴퓨터 파일 업로드 허용<br/><br/>가상 컴퓨터 > 스냅숏 > 스냅숏 제거 |
| vCenter 사용자 역할 |VMware VM 검색/원본 VM을 종료하지 않고 장애 조치 |Hello v Center 서버에 대 한 이러한 권한을 할당 합니다.<br/><br/>데이터 센터 개체 > 전파 tooChild 개체, 역할 = 읽기 전용 <br/><br/>hello 사용자 hello 데이터 센터 수준에서 할당 되 고 따라서는 hello 데이터 센터에서 액세스 tooall hello 개체. Toorestrict hello 액세스 하려는 경우 할당 hello **에 액세스할 수 없는** hello로 역할 **toochild 전파** 개체 toohello 자식 개체 (ESX 호스트, 데이터 저장소, Vm 및 네트워크). |
| vCenter 사용자 역할 |장애 조치 및 장애 복구 |Hello v Center 서버에 대 한 이러한 권한을 할당 합니다.<br/><br/>데이터 센터 개체-전파 toochild 개체, 역할 Azure_Site_Recovery =<br/><br/>hello 사용자 데이터 센터 수준에서 할당 되 고 따라서는 hello 데이터 센터에서 액세스 tooall hello 개체.  Toorestrict hello 액세스 하려는 경우 할당 hello * * 권한 없음 * * hello로 역할 **전파 toochild 개체** toohello 자식 개체 (ESX 호스트, 데이터 저장소, Vm 및 네트워크). |

## <a name="third-party-software-notices-and-information"></a>타사 소프트웨어 통지 및 정보
<!--Do Not Translate or Localize-->

hello 소프트웨어 및 펌웨어에서 실행 중인 hello Microsoft 제품 또는 서비스 기반으로 하거나 통합 hello의 자료 (통칭 "제 3 자 코드") 아래에 나열 된 프로젝트입니다.  Microsoft는 hello hello 제 3 자 코드의 하지 원 작 자가 있습니다.  hello 원본 저작권 표시 및 라이선스, Microsoft는 이러한 제 3 자 코드를 받은 아래 명시 설정 됩니다.

A 섹션의 hello 정보에는 제 3 자 코드 아래에 나열 된 hello 프로젝트에서 구성 요소 관련입니다. Such licenses and information are provided for informational purposes only.  이 제 3 자 코드에서 Microsoft의 소프트웨어 사용 약관 hello Microsoft 제품 또는 서비스에 대 한 Microsoft에서 relicensed tooyou 되 고 있습니다.  

hello 정보 섹션 B에 대해 시도 하는 사용 가능한 tooyou microsoft hello 원래 라이선스 조건에 따라 제 3 자 코드 구성 요소 관련입니다.

hello 전체 파일 hello에서 발견 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=529428)합니다. Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>다음 단계
[장애 복구에 대 한 자세한](site-recovery-failback-azure-to-vmware-classic.md) toobring Azure에서 실행 하 여 실패 한 컴퓨터 다시 tooyour 온-프레미스 환경입니다.
