---
title: "aaaReplicate VMware Vm 및 물리적 서버 tooAzure (클래식 레거시) | Microsoft Docs"
description: "어떻게 tooreplicate 온-프레미스 Vm에 설명 하 고 hello 클래식 포털에서 기존 배포에서 Azure Site Recovery를 사용 하 여 Windows/Linux 물리적 서버의 tooAzure 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>VMware 가상 컴퓨터와 물리적 서버 tooAzure hello 클래식 포털 (레거시)를 사용 하 여 Azure Site Recovery와 복제
> [!div class="op_single_selector"]
> * [Azure 포털](site-recovery-vmware-to-azure.md)
> * [클래식 포털](site-recovery-vmware-to-azure-classic.md)
> * [클래식 포털(레거시)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

TooAzure 사이트 복구를 시작! 이 문서에서는 온-프레미스 VMware 가상 컴퓨터 또는 Windows/Linux 물리적 서버의 tooAzure hello 클래식 포털에서 Azure Site Recovery를 사용 하 여 복제에 대 한 레거시 배포를 설명 합니다.

## <a name="overview"></a>개요
조직은 어떻게 응용 프로그램, 작업, 및 데이터 얻을 실행 되 고 사용할 수 있는 동안 계획 되거나 계획 되지 않은 가동 중지 시간을 결정 하는 BCDR 전략이 필요 하 고 가능한 한 빨리 toonormal 작업 조건 복구. BCDR 전략은 재해가 발생했을 때 비즈니스 데이터를 안전하고 복구 가능하게 유지하고 워크로드를 지속적으로 가용 상태로 유지해야 합니다.

사이트 복구는 온-프레미스 물리적 서버와 가상 컴퓨터 toohello 클라우드 (Azure) 또는 tooa 보조 데이터 센터의 복제를 조정 함으로써 tooyour BCDR 전략을 강화 하는 Azure 서비스입니다. 기본 위치에서 중단이 발생할 때 장애 조치 toohello 보조 위치 tookeep 앱 및 워크 로드에 사용할 수 있습니다. Toonormal 작업을 반환 하는 경우 백 tooyour 기본 위치를 실패 합니다. [Azure Site Recovery란?](site-recovery-overview.md)

> [!WARNING]
> 이 문서에는 **레거시 지침**이 포함되어 있습니다. 새 배포에는 사용하지 마십시오. 대신, [다음이 지침에 따라](site-recovery-vmware-to-azure.md) hello Azure 포털에서에서 사이트 복구 toodeploy 또는 [다음이 지침을 따르세요](site-recovery-vmware-to-azure-classic.md) tooconfigure hello hello 클래식 포털에서 배포를 강화 합니다. 이 문서에서 설명 하는 hello 메서드를 사용 하 여 이미 배포 되었으며, hello 클래식 포털에서 향상 된 toohello 배포를 마이그레이션하는 것이 좋습니다.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>향상 된 toohello 배포 마이그레이션
이 섹션은이 문서의 hello 지침을 사용 하 여 사이트 복구를 이미 배포한 경우 해당 수만 있습니다.

toomigrate 기존 배포 해야 합니다.

1. 온-프레미스 사이트에서 새 사이트 복구 구성 요소를 배포합니다.
2. Hello 새 구성 서버에서 VMware Vm의 자동 검색에 대 한 자격 증명을 구성 합니다.
3. 새 구성 서버 hello와 hello VMware 서버를 검색 합니다.
4. Hello 새 구성 서버와 새 보호 그룹을 만듭니다.

시작하기 전에 다음을 수행합니다.

* 마이그레이션을 위해 유지 관리 기간을 계획하는 것이 좋습니다.
* hello **마이그레이션할 컴퓨터** 옵션은 레거시 배포 중에 만든 기존 보호 그룹이 있는 경우에 사용할 수 있습니다.
* Hello 마이그레이션 단계를 완료 한 후 보호 그룹 tooa 추가할 수 있도록 15 분 또는 긴 toorefresh hello 자격 증명 및 가상 컴퓨터 새로 고침 및 toodiscover 걸릴 수 있습니다. 기다리지 않고 직접 새로 고침할 수도 있습니다.

마이그레이션 과정은 다음과 같습니다.

1. 에 대 한 읽기 [hello 클래식 포털에서 배포를 강화](site-recovery-vmware-to-azure-classic.md)합니다. 향상 된 검토 hello [아키텍처](site-recovery-vmware-to-azure-classic.md), 및 [필수 구성 요소](site-recovery-vmware-to-azure-classic.md)합니다.
2. 현재 복제 하는 컴퓨터에서 hello 모바일 서비스를 제거 합니다. 새 버전의 hello 서비스 toohello 새 보호 그룹을 추가할 때 hello 컴퓨터에 설치 됩니다.
3. 다운로드 한 [자격 증명 모음 등록 키](site-recovery-vmware-to-azure-classic.md) 및 [hello 통합된 설치 마법사를 실행](site-recovery-vmware-to-azure-classic.md) tooinstall hello 구성 서버, 프로세스 서버 및 마스터 대상 서버 구성 요소입니다. [용량 계획](site-recovery-vmware-to-azure-classic.md)에 대해 자세히 알아보세요.
4. [자격 증명 설정](site-recovery-vmware-to-azure-classic.md) 해당 사이트 복구 tooaccess VMware צ ְ ײ 서버 tooautomatically VMware Vm을 검색 합니다. [필요한 권한](site-recovery-vmware-to-azure-classic.md)에 대해 알아보세요.
5. [vCenter 서버 또는 vSphere 호스트](site-recovery-vmware-to-azure-classic.md)를 추가합니다. Hello Site Recovery 포털의 서버 tooappear에 대 한 추가 대 일 분 걸릴 수 있습니다.
6. [새 보호 그룹](site-recovery-vmware-to-azure-classic.md)을 만듭니다. Hello 가상 컴퓨터는 검색 및 표시 되도록 hello 포털 toorefresh too15 분까지 걸릴 수 있으므로 합니다. Toowait 않으려면 hello 관리 서버 이름을 강조할 수 있습니다 (클릭 하지 말고) > **새로 고침**합니다.
7. Hello 새 보호 그룹에서 클릭 **마이그레이션할 컴퓨터**합니다.

    ![계정 추가](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. **컴퓨터 선택** 선택 hello 보호 그룹에서 toomigrate을 hello toomigrate 컴퓨터입니다.

    ![계정 추가](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. **대상 설정 구성** toouse 것인지 지정 모든 컴퓨터 및 선택 hello 프로세스 서버와 Azure 저장소 계정에 대 한 동일한 설정을 hello 합니다. 별도 프로세스 서버에 없는 경우이 hello 구성 서버 서버의 hello hello IP 주소가 됩니다.

    ![계정 추가](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [저장소 계정 마이그레이션](../resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 저장소 계정에 대 한 합니다.

1. **계정 지정**, hello 프로세스 서버 tooaccess hello 컴퓨터 toopush hello hello 모바일 서비스의 새 버전으로 만든 hello 계정을 선택 합니다.

   ![계정 추가](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. 사이트 복구에서 복제 된 데이터 toohello Azure 저장소 계정 사용자가 제공한 마이그레이션합니다. 필요에 따라 hello 레거시 배포에 사용 되는 hello 저장소 계정을 다시 사용할 수 있습니다.
3. Hello 작업 이후 완료 된 가상 컴퓨터는 자동으로 동기화 합니다. 동기화가 완료 된 후에 hello 기존 보호 그룹에서 hello 가상 컴퓨터를 삭제할 수 있습니다.
4. 모든 컴퓨터를 마이그레이션한 후에 hello 기존 보호 그룹을 삭제할 수 있습니다.
5. 컴퓨터에 대 한 toospecify hello 장애 조치 속성을 기억 하 고 동기화가 완료 된 후 Azure 네트워크 설정을 hello 합니다.
6. 기존 복구 계획이 있는 경우 마이그레이션할 수 있습니다 이러한 hello로 향상 toohello 배포 **복구 계획 마이그레이션** 옵션입니다. 모든 보호된 컴퓨터를 마이그레이션한 후에 이 작업을 수행해야 합니다.

   ![계정 추가](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> 마이그레이션 후 hello로 계속 [향상 된 문서](site-recovery-vmware-to-azure-classic.md)합니다. hello이 문서의 나머지 부분 레거시을 더 이상 관련 되며 모든 toofollow 필요 하지 않습니다 it * *에 설명 된 hello 단계 중입니다.
>
>

## <a name="what-do-i-need"></a>무엇이 필요하나요?
이 다이어그램에서는 hello 배포 구성 요소를 보여 줍니다.

![새 자격 증명 모음](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

다음 항목이 필요합니다.

| **구성 요소** | **배포웹사이트를** | **세부 정보** |
| --- | --- | --- |
| **구성 서버** |표준 A3는 Azure 가상 컴퓨터 hello에 사이트 복구와 같은 구독 합니다. |hello 구성 서버는 보호 된 컴퓨터, hello 프로세스 서버 및 Azure의 마스터 대상 서버 간의 통신을 조정 합니다. 복제를 설정하고 장애 조치(Failover) 발생 시 Azure에서 복구를 조정합니다. |
| **마스터 대상 서버** |Azure 가상 컴퓨터-OpenLogic CentOS 6.6 갤러리 이미지 (tooprotect Linux 컴퓨터)에 따라을 Windows 서버 기반 또는 Linux 서버 (tooprotect Windows 컴퓨터)는 Windows Server 2012 R2 갤러리 이미지에 있습니다.<br/><br/> 세 가지 크기 옵션(표준 A4, 표준 D14 및 표준 DS4)을 사용할 수 있습니다.<br/><br/> hello 서버는 연결 된 toohello hello 구성 서버와 같은 Azure 네트워크입니다.<br/><br/> Hello Site Recovery 포털에서 설정 |Azure 저장소 계정으로 Blob 저장소에 만든 연결된 VHD를 사용하여 보호된 컴퓨터의 복제된 데이터를 수신 및 유지합니다.<br/><br/> 특히, 프리미엄 저장소 계정을 사용하여 일관된 고성능과 짧은 대기 시간이 요구되는 워크로드에 대한 보호를 구성하는 경우 표준 DS4를 선택합니다. |
| **프로세스 서버** |Windows Server 2012 R2를 실행하는 온-프레미스 가상 또는 물리적 서버<br/><br/> 이 항목에 배치 hello 동일한 것이 좋습니다 네트워크 가시성 tooit 네트워크 및 LAN 세그먼트 hello 컴퓨터로 tooprotect, 하지만 L3를 보유 하는 보호 된 컴퓨터를 다른 네트워크에서 실행할 수 있습니다.<br/><br/> 설정 하 고 toohello 구성 서버 hello Site Recovery 포털에서 등록 합니다. |보호 된 컴퓨터는 복제 데이터 toohello 온-프레미스 프로세스 서버를 보냅니다. 수신 하는 디스크 기반 캐시 toocache 복제 데이터 있음 해당 데이터에 대해 다양한 작업을 수행합니다.<br/><br/> Toohello 마스터 대상 서버에 보내기 전에 암호화 하 고 캐싱를 압축 하 여 데이터를 최적화 합니다.<br/><br/> Hello 모바일 서비스의 강제 설치를 처리합니다.<br/><br/> VMware 가상 컴퓨터의 자동 검색을 수행합니다. |
| **온-프레미스 컴퓨터** |Windows 또는 Linux를 실행하는 온-프레미스 VMware 가상 컴퓨터 또는 물리적 서버. |하나 이상의 컴퓨터에 적용되는 복제 설정을 구성합니다. 개별 컴퓨터 또는 보다 일반적으로 복구 계획에 한데 모아놓은 여러 대의 컴퓨터를 장애 조치(Failover)할 수 있습니다. |
| **모바일 서비스** |각 가상 컴퓨터 또는 실제 서버에 설치 하려는 tooprotect<br/><br/> 수동으로 설치 또는 푸시 및 컴퓨터에서 복제를 사용 하도록 설정 하면 hello 프로세스 서버에서 자동으로 설치 수입니다. |hello 모바일 서비스 (resync) 초기 복제 하는 동안 데이터 toohello 프로세스 서버를 보냅니다. Hello 컴퓨터는 보호 된 상태 (끝나면 resync) 후 hello 모바일 서비스 쓰기 toodisk 메모리 캡처하고 toohello 프로세스 서버에 전송 합니다. Windows 서버에 대한 응용 프로그램 일관성은 VSS를 사용하여 구현됩니다. |
| **Azure Site Recovery 자격 증명 모음** |Azure 구독 사용 하 여 사이트 복구 자격 증명 모음을 만들고 hello 자격 증명 모음에 서버를 등록 합니다. |자격 증명 모음 좌표 hello 및 데이터 복제, 장애 조치 및 온-프레미스 사이트와 Azure 간의 복구를 오케스트레이션 합니다. |
| **복제 메커니즘** |**Hello 인터넷을 통해**-통신 및 복제 데이터를 통해 보안 SSL/TLS 채널을 사용 하 여 보호 된 온-프레미스 서버 tooAzure hello 인터넷 합니다. Hello 기본 옵션입니다.<br/><br/> **VPN/Express 경로**- VPN 연결을 통해 온-프레미스 서버와 Azure 간에 데이터를 전달 및 복제합니다. 사이트 간 VPN 또는 express 경로 연결 온-프레미스 사이트와 Azure 네트워크 간에 tooset이 필요 합니다.<br/><br/> 사이트 복구 배포 하는 동안 원하는 tooreplicate를 선택 합니다. 기존 컴퓨터의 복제가 영향을 주지 않고 구성 된 후에 hello 메커니즘을 변경할 수 없습니다. |두 옵션 모두 보호 된 컴퓨터에서 모든 인바운드 네트워크 포트 tooopen 있습니다 필요합니다. 모든 네트워크 통신 hello 온-프레미스 사이트에서 시작 됩니다. |

## <a name="capacity-planning"></a>용량 계획
hello 주요 영역 tooconsider 필요 합니다.

* **원본 환경**-hello VMware 인프라, 원본 컴퓨터 설정 및 요구 사항입니다.
* **구성 요소 서버**-프로세스 서버, 구성 서버 및 마스터 대상 서버 hello

### <a name="considerations-for-hello-source-environment"></a>Hello 소스 환경에 대 한 고려 사항
* **최대 디스크 크기**— hello tooa 연결 된 가상 컴퓨터 일 수 있는 hello 디스크의 현재 최대 크기는 1TB입니다. 따라서 hello 복제할 수 있는 원본 디스크의 최대 크기 제한 too1 TB 이기도 합니다.
* **소스 마다 최대 크기**— 단일 원본 컴퓨터의 최대 크기 hello (31 디스크)와 31 TB를는 hello 마스터 대상 서버에 대 한 사용자를 프로 비전 D14 인스턴스.
* **마스터 대상 서버당 원본 수**- 단일 마스터 대상 서버로 여러 원본 컴퓨터를 보호할 수 있습니다. 그러나 단일 원본 컴퓨터는 hello hello 디스크 크기를 반영 하는 VHD를 Azure blob 저장소에 생성 되어 데이터 디스크 toohello 마스터 대상 서버에 연결 된 디스크 복제 하기 때문에 여러 마스터 대상 서버에 보호할 수 없습니다.  
* **소스 마다 최대 매일 변경 비율**-toobe 때 권장 hello를 고려 하는 것으로 간주 해야 하는 세 가지 요소 소스당 비율을 변경할 수 있습니다. Hello 기준으로 대상 고려 사항에 대 한 두 개의 IOPS hello 소스에서 각 작업에 대 한 hello 대상 디스크에 필요 합니다. 즉, 오래 된 데이터의 읽기 및 쓰기 hello 새 데이터를 hello 대상 디스크에 실행 됩니다.
  * **매일 hello 프로세스 서버에서 지원 되는 빈도 변경할**-원본 컴퓨터는 여러 프로세스 서버에 걸쳐 있을 수 있습니다. 단일 프로세스 서버 매일 변경률을 too1 TB를 지원할 수 있습니다. 따라서 1TB hello 최대 일별 데이터 변경 원본 컴퓨터에 대해 지원 되는 속도입니다.
  * **Hello 대상 디스크에서 지 원하는 최대 처리량**-소스 디스크당 최대 변동을 (8k 쓰기 크기)와 이상 144 g B/일 수 없습니다. Hello 처리량 및 IOPs의 다양 한 쓰기 크기에 대 한 hello 대상에 대 한 hello 마스터 대상 섹션의 hello 표를 참조 하십시오. 이 번호는 각 원본 IOP 2 hello 대상 디스크 IOPS를 생성 하기 때문에 2로 나누었을 해야 합니다. 에 대 한 읽기 [Azure 확장성 및 성능 목표가](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 프리미엄 저장소 계정에 대 한 hello 대상을 구성 하는 경우.
  * **Hello 저장소 계정에서 지 원하는 최대 처리량**-소스 여러 저장소 계정에 걸쳐 있을 수 있습니다. 제공 하는 저장소 계정 최대 20, 000 초 당 요청 수를 사용 하 고 각 원본 IOP hello 마스터 대상 서버에서 2 IOPS가 생성 하 좋습니다 hello hello 소스 too10 000 간에 IOPS 수를 유지 합니다. 에 대 한 읽기 [Azure 확장성 및 성능 목표가](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 프리미엄 저장소 계정에 대 한 hello 소스를 구성 하는 경우.

### <a name="considerations-for-component-servers"></a>구성 요소 서버 고려 사항
표 1 hello 구성 및 마스터 대상 서버에 대 한 가상 컴퓨터 크기 hello 요약 되어 있습니다.

| **구성 요소** | **Azure 인스턴스 배포** | **코어 수** | **메모리** | **최대 디스크 수** | **디스크 크기** |
| --- | --- | --- | --- | --- | --- |
| 구성 서버 |표준 A3 |4 |7 GB |8 |1023GB |
| 마스터 대상 서버 |표준 A4 |8 |14 GB |16 |1023GB |
| 표준 D14 |16 |112GB |32 |1023GB | |
| 표준 DS4 |8 |28GB |16 |1023GB | |

**표 1**

#### <a name="process-server-considerations"></a>프로세스 서버 고려 사항
일반적으로 프로세스 서버 크기에서 보호 되는 모든 작업 hello 매일 변경 비율에 따라 다릅니다.

* 인라인 압축 및 암호화와 같은 계산 tooperform 작업 충분 해야합니다.
* 프로세스 서버 hello 디스크 기반 캐시를 사용합니다. 캐시 공간을 권장 있는지 hello 확인 및 디스크 처리량은 중단 또는 네트워크 병목 현상의 hello 이벤트에 저장 된 사용 가능한 toofacilitate hello 데이터 변경 합니다.
* Hello 프로세스 서버를 업로드할 수 hello 데이터 toohello 마스터 대상 서버 tooprovide 지속적인 데이터 보호 되도록 충분 한 대역폭을 확인 합니다.

표 2 hello 프로세스 서버 지침의 요약을 제공 합니다.

| **데이터 변경률** | **CPU** | **메모리** | **캐시 디스크 크기** | **캐시 디스크 처리량** | **대역폭 수신/송신** |
| --- | --- | --- | --- | --- | --- |
| < 300GB |4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz) |4GB |600GB |7 too10 m B / 초 |30Mbps/21Mbps |
| 300 too600 GB |8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) |6GB |600GB |11 too15 m B / 초 |60Mbps/42Mbps |
| 600GB too1 TB |12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) |8GB |600GB |16 too20 m B / 초 |100Mbps/70Mbps |
| > 1TB |다른 프로세스 서버 배포 | | | | |

**표 2**

여기서,

* 수신은 다운로드 대역폭 (hello 원본 서버와 프로세스 서버 간에 인트라넷)입니다.
* 송신은 업로드 대역폭 (hello 프로세스 서버와 마스터 대상 서버 간의 인터넷)입니다. 송신 수치는 평균 30%의 프로세스 서버 압축을 가정합니다.
* 캐시 디스크인 경우 모든 프로세스 서버에 대해 128GB 이상의 개별 OS 디스크를 사용하는 것이 좋습니다.
* 캐시 디스크 처리량 hello에 대 한 저장소를 다음에 사용한 벤치마킹: RAID 10 구성 사용 하 여 10 K RPM의 SAS 드라이브를 8입니다.

#### <a name="configuration-server-considerations"></a>구성 서버 고려 사항
각 구성 서버 3-4 볼륨 too100 소스 컴퓨터를 지원할 수 있습니다. 배포의 규모가 더 큰 경우에는 또 다른 구성 서버를 배포하는 것이 좋습니다. Hello 구성 서버 hello 기본 가상 컴퓨터 속성 표 1을 참조 하십시오.

#### <a name="master-target-server-and-storage-account-considerations"></a>마스터 대상 서버 및 저장소 계정 고려 사항
각 마스터 대상 서버에 대 한 hello 저장소는 OS 디스크, 보존 볼륨 및 데이터 디스크를 포함합니다. hello Site Recovery 포털에 정의 된 hello 보존 창의 hello 기간에 대 한 hello 보존 드라이브에 디스크 변경 내용이의 hello 저널 유지 관리 합니다.  Hello 마스터 대상 서버의 가상 컴퓨터 속성 hello tooTable 1을 참조 하십시오. 표 3의 A4 hello 디스크를 사용 하는 방법을 보여 줍니다.

| **인스턴스** | **OS 디스크** | **보존** | **데이터 디스크** |
| --- | --- | --- | --- |
| **보존** |**데이터 디스크** | | |
| 표준 A4 |1개 디스크(1 * 1023GB) |1개 디스크(1 * 1023GB) |15개 디스크(15 * 1023GB) |
| 표준 D14 |1개 디스크(1 * 1023GB) |1개 디스크(1 * 1023GB) |31개 디스크(15 * 1023GB) |
| 표준 DS4 |1개 디스크(1 * 1023GB) |1개 디스크(1 * 1023GB) |15개 디스크(15 * 1023GB) |

**표 3**

Hello 마스터 대상 서버를 위한 용량 계획에 따라 달라 집니다.

* Azure 저장소의 성능 및 제한 사항
  * hello 최대 수는 항상 표준 계층 VM에 대 한 디스크 사용, 단일 저장소 계정에 (디스크 당 IOPS 20000/500)을 40 약 합니다. [표준 저장소 계정의 확장성 목표](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) 및 [프리미엄 저장소 계정](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)을 참조하세요.
* 일일 데이터 변경률
* 보존 볼륨 저장소.

다음 사항에 유의하세요.

* 하나의 원본을 여러 저장소 계정에 사용할 수 없습니다. 이 toohello 데이터 디스크를 보호를 구성할 때 선택한 toohello 저장소 계정에 적용 됩니다. hello OS 및 hello 보존 디스크는 일반적으로 저장소 계정을 자동으로 배포 됩니다 toohello 이동 합니다.
* hello에 필요한 저장소 볼륨 보존 hello 매일 변경 률 및 hello 보존 일 수에 따라 달라 집니다. 마스터 대상 서버 당 보존 저장소 hello = 하루 원본의 총 변동 수 * 보존 일 수 있습니다.
* 각각의 마스터 대상 서버에는 하나의 보존 볼륨만 있습니다. hello 디스크 toohello 연결 된 마스터 대상 서버 보존 볼륨 hello 공유 됩니다. 예:
  * 원본 컴퓨터는 5 개의 디스크와이 각 디스크 hello 소스 120 IOPS (8k 크기)를 생성 하는 경우 (두 가지 작업, IO 소스당 hello 대상 디스크에) 디스크당 too240 IOPS로 변환 합니다. 240 IOPS는 Azure hello 당 500 디스크 IOPS 제한 이내입니다.
  * 이 120 * 5 = 600 hello 보존 볼륨에 IOPS 및이 bottle 목 될 수 있습니다. 이 시나리오에서는 좋은 전략 tooadd 더 많은 디스크 toohello 보존 볼륨이 고, 샤 RAID stripe 구성으로 확장 됩니다. 이렇게 하면 hello IOPS 여러 드라이브에 분산 되어 때문에 성능이 향상 됩니다. 드라이브 toobe hello 수가 추가 toohello 보존 볼륨이 다음과 같이 됩니다.
    * 원본 환경의 총 IOPS / 500
    * 원본 환경에서 일일 총 변동 수(비압축)/287GB 287 GB hello 하루 대상 디스크에서 지원 되는 최대 처리량입니다. 이 경우 8k는 보내 쓰기 크기를 가정 하기 때문에이 메트릭은 hello 쓰기 크기는 8k이 비율로 따라 달라 집니다. 예를 들어 경우 hello 쓰기 크기는 4k 처리량이 287/2 됩니다. 및 hello 쓰기 크기는 16k 같으면 처리량 됩니다 287 * 2.
* 필요한 저장소 계정 수 hello = 총 IOPs/10000 원본입니다.

## <a name="before-you-start"></a>시작하기 전에
| **구성 요소** | **요구 사항** | **세부 정보** |
| --- | --- | --- |
| **Azure 계정** |[Microsoft Azure](https://azure.microsoft.com/) 계정이 있어야 합니다. [무료 평가판](https://azure.microsoft.com/pricing/free-trial/)으로 시작할 수 있습니다. | |
| **Azure 저장소** |Azure 저장소 계정 복제 toostore 데이터 필요 합니다.<br/><br/> 각 hello 계정 이어야 합니다는 [표준 지역 중복 저장소 계정](../storage/common/storage-redundancy.md#geo-redundant-storage) 또는 [프리미엄 저장소 계정](../storage/common/storage-premium-storage.md)합니다.<br/><br/> Hello hello Azure Site Recovery 서비스와 동일한 지역 또는 hello와 연결할에 해야 동일한 구독 합니다. Hello를 사용 하 여 만든 저장소 계정의 hello 이동을 지원 하지 않습니다 [새 Azure 포털](../storage/common/storage-create-storage-account.md) 리소스 그룹에 걸쳐 있습니다.<br/><br/> 읽기 더 toolearn [소개 tooMicrosoft Azure 저장소](../storage/common/storage-introduction.md) | |
| **Azure 가상 네트워크** |어떤 hello에 구성 서버 및 마스터 대상 서버 배포 될 Azure 가상 네트워크가 필요 합니다. Hello에 것 같은 구독과 지역 hello Azure Site Recovery 자격 증명 모음으로 합니다. 원할 경우 tooreplicate 데이터 VPN 또는 express 경로 연결 hello Azure 통해 가상 네트워크는 ExpressRoute 연결 또는 사이트 간 VPN 연결된 tooyour 온-프레미스 네트워크 이어야 합니다. | |
| **Azure 리소스** |Azure 리소스 toodeploy 충분 한 모든 구성 요소가 있는 있는지 확인 합니다. [Azure 구독 제한](../azure-subscription-service-limits.md)을 참조하세요. | |
| **Azure 가상 컴퓨터** |Tooprotect 원하는 가상 컴퓨터를 준수 해야 [Azure 필수 구성 요소](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements)합니다.<br/><br/> **디스크 수**—하나의 보호된 서버에서 최대 31개의 디스크를 지원할 수 있습니다.<br/><br/> **디스크 크기**—개별 디스크 용량은 1023GB 이하여야 합니다.<br/><br/> **클러스터링**—클러스터형 서버는 지원되지 않습니다.<br/><br/> **부팅**—UEFI(Unified Extensible Firmware Interface)/EFI(Extensible Firmware Interface) 부팅은 지원되지 않습니다.<br/><br/> **볼륨**—Bitlocker 암호화된 볼륨은 지원되지 않습니다.<br/><br/> **서버 이름**- 이름은 1~63자 사이여야 하며 문자, 숫자, 하이픈을 사용할 수 있습니다. hello 이름은 문자 또는 숫자로 시작 하 고 문자 또는 숫자로 끝나야 합니다. 컴퓨터를 보호 한 후 Azure 이름 hello를 수정할 수 있습니다. | |
| **구성 서버** |Azure 사이트 복구 Windows Server 2012 R2 갤러리 이미지에 따라 표준 A3 가상 컴퓨터는 hello 구성 서버에 대 한 구독에서 생성 됩니다. 새 클라우드 서비스에 첫 번째 인스턴스가 hello로 생성 됩니다. 예약 된 공용 IP 주소와 hello 구성 서버 hello 클라우드 서비스에 대 한 연결 형식 hello를 만들 수는 공용 인터넷을 선택 합니다.<br/><br/> 영어 문자만 hello 설치 경로 여야 합니다. | |
| **마스터 대상 서버** |Azure 가상 컴퓨터, 표준 A4, D14 또는 DS4.<br/><br/> 영어 문자만 hello 설치 경로 여야 합니다. 예를 들어 hello 경로 여야 합니다 **/usr/local/ASR** Linux를 실행 하는 마스터 대상 서버에 대 한 합니다. | |
| **프로세스 서버** |물리적 컴퓨터 또는 hello 최신 업데이트와 함께 Windows Server 2012 r 2를 실행 하는 가상 컴퓨터에 hello 프로세스 서버를 배포할 수 있습니다. C:/에 설치합니다.<br/><br/> Hello에 hello 서버를 배치 하는 것이 좋습니다 동일한 네트워크 및 서브넷으로 hello tooprotect 컴퓨터입니다.<br/><br/> Hello 프로세스 서버에서 VMware vSphere CLI 5.5.0 설치 합니다. vCenter 서버 또는 ESXi 호스트에서 실행 중인 가상 컴퓨터에 의해 관리 되는 순서 toodiscover 가상 컴퓨터의 프로세스 서버 hello에 hello VMware vSphere CLI 구성 요소가 필요 합니다.<br/><br/> 영어 문자만 hello 설치 경로 여야 합니다.<br/><br/> ReFS 파일 시스템은 지원되지 않습니다. | |
| **VMware** |VMware vSphere 하이퍼바이저를 관리하는 VMWare vCenter 서버. Hello 최신 업데이트로 vCenter 버전 5.1 또는 5.5를 실행 해야 합니다.<br/><br/> VMware 가상 컴퓨터를 포함 하는 하나 이상의 vSphere 하이퍼바이저 tooprotect을 원하는 합니다. hello 하이퍼바이저 hello 최신 업데이트로 ESX/ESXi 버전 5.1 또는 5.5 실행 되어야 합니다.<br/><br/> VMware 가상 컴퓨터에 VMware 도구가 설치되어 있고 실행 중이어야 합니다. | |
| **Windows 컴퓨터** |Windows를 실행하는 보호된 실제 서버 또는 VMware 가상 컴퓨터에는 몇 가지 요구 사항이 있습니다.<br/><br/> 지원되는 64비트 운영 체제: **Windows Server 2012 R2**, **Windows Server 2012** 또는 **Windows Server 2008 R2 SP1 이상**.<br/><br/> 호스트 이름, 탑재 지점, 장치 이름, Windows 시스템 경로 hello (예: C:\Windows)만 영어에 있어야 합니다.<br/><br/> hello 운영 체제는 C:\ 드라이브에 설치 되어야 합니다.<br/><br/> 기본 디스크만 지원됩니다. 동적 디스크는 지원되지 않습니다.<br/><br/> 보호 된 컴퓨터에서 방화벽 규칙 해야 해당 tooreach hello 구성 및 마스터 대상 서버에서에서 허용 Azure.p ><p>Tooprovide 관리자 계정이 필요 합니다 (hello Windows 컴퓨터에서 로컬 관리자 여야 함) toopush Windows 서버에 hello 모바일 서비스를 설치 합니다. 제공 된 hello 계정이 아닌 도메인 계정인 경우 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 해야 합니다. toodo이 추가 hello LocalAccountTokenFilterPolicy DWORD 레지스트리 항목을 찾아에서 1의 값을 사용 합니다. CLI에서 tooadd hello 레지스트리 항목 cmd 또는 powershell을 열고 다음을 입력  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 합니다. 액세스 제어에 대해 [자세히 알아보세요](https://msdn.microsoft.com/library/aa826699.aspx).<br/><br/> 장애 조치 후 원격 데스크톱 tooWindows Azure 가상 컴퓨터에 연결 하려면 원격 데스크톱 hello 온-프레미스 컴퓨터에 대 한 활성화 되어 있는지 확인 합니다. 방화벽 규칙 hello를 통해 원격 데스크톱 연결을 허용 해야 하지 연결한 경우 VPN을 통해, 인터넷 합니다. | |
| **Linux 컴퓨터** |지원 되는 64 비트 운영 체제: **6.5, 6.6 Centos 6.4**; **Oracle Enterprise Linux 6.4 hello Red Hat 호환 커널 또는 바꿀 엔터프라이즈 커널 Release 3 (UEK3)을 실행 하는 6.5**, **SUSE Linux Enterprise Server 11 s p 3**합니다.<br/><br/> 보호 된 컴퓨터에서 방화벽 규칙 해야 있도록 tooreach hello 구성 및 마스터 대상 서버가 Azure에서.<br/><br/> 보호 된 컴퓨터의 /etc/hosts 파일에 모든 Nic와 관련 된 hello 로컬 호스트 이름 tooIP 주소에 매핑하는 항목이 없어야 합니다. <br/><br/> Azure 가상 tooconnect tooan 하려는 경우 실행 중인 Linux 컴퓨터 클라이언트를 사용 하는 보안 셸 (ssh), 장애 조치 해당 hello hello 보호에서 보안 셸 서비스를 확인 한 후 컴퓨터 toostart 시스템 부팅 시 자동으로 설정 하 고 방화벽 규칙을 사용 하는 ssh 연결 tooit 합니다.<br/><br/> hello 호스트 이름, 탑재 지점, 장치 이름 및 Linux 시스템 경로 및 파일 이름 (예: / 등 /; /usr) 영어로 이어야 합니다.<br/><br/> 다음 저장소 hello로 온-프레미스 컴퓨터에 대 한 보호를 사용할 수 있습니다.-<br>파일 시스템: EXT3, ETX4, ReiserFS, XFS<br>다중 경로 소프트웨어 장치 매퍼(다중 경로)<br>볼륨 관리자: LVM2<br>HP CCISS 컨트롤러 저장소가 있는 물리적 서버는 지원되지 않습니다. | |
| **타사** |이 시나리오에서 일부 배포 구성 요소는 제 3 자 소프트웨어 toofunction에 제대로 따라 다릅니다. 전체 목록은 [타사 소프트웨어 통지 및 정보](#third-party) | |

### <a name="network-connectivity"></a>네트워크 연결
온-프레미스 사이트 간의 네트워크 연결을 구성할 때 두 가지 옵션이 및 Azure 가상 네트워크 인프라 구성 요소 (구성 서버, 마스터 대상 서버)는 hello에 배포 된 hello 합니다. 구성 서버를 배포할 수 있는 네트워크 연결 옵션 toouse 하기 전에 toodecide가 필요 합니다. 이 설정은 배포 시 hello toochoose 필요 합니다. 나중에 변경할 수 없습니다.

**인터넷:** 보안 SSL을 통해 발생 하는 통신 및 hello 온-프레미스 서버 (프로세스 서버, 보호 된 컴퓨터) 및 (구성 서버, 마스터 대상 서버) hello Azure 인프라 구성 요소 서버 간 데이터 복제 / 온-프레미스 toohello hello 구성 및 마스터 대상 서버에서 공용 끝점에서 TLS 연결 합니다. (hello 유일한 예외 사이 연결이 hello hello 프로세스 서버와 마스터 대상 서버는 암호화 되지 않습니다는 TCP 포트 9080에 hello 합니다. 만 제어 정보 관련 toohello 복제 프로토콜 복제 설정에 대 한이 연결에서 교환 됩니다.)

![배포 다이어그램 인터넷](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: VPN 연결을 통해 발생 하는 통신 및 hello 온-프레미스 서버 (프로세스 서버, 보호 된 컴퓨터) 및 (구성 서버, 마스터 대상 서버) hello Azure 인프라 구성 요소 서버 간 데이터 복제 온-프레미스 네트워크와 Azure hello는 hello 구성 서버 및 마스터 대상 서버가 배포 된 가상 네트워크입니다. 온-프레미스 네트워크에 연결 된 toohello ExpressRoute 연결 또는 사이트 간 VPN 연결에 의해 Azure 가상 네트워크 인지 확인 합니다.

![배포 다이어그램 VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>1단계: 자격 증명 모음 만들기
1. Toohello 로그인 [관리 포털](https://portal.azure.com)합니다.
2. **Data Services** > **Recovery Services**를 확장하고 **Site Recovery 자격 증명 모음**을 클릭합니다.
3. **새로 만들기** > **빠른 생성**을 클릭합니다.
4. **이름**, 이름 tooidentify hello 자격 증명 모음을 입력 합니다.
5. **지역**, 선택 hello hello 자격 증명 모음에 대 한 지리적 영역입니다. 지원 toocheck 지역에서 지역 가용성 참조 [Azure 사이트 복구 가격 정보](https://azure.microsoft.com/pricing/details/site-recovery/)
6. **자격 증명 모음 만들기**를 클릭합니다.

    ![새 자격 증명 모음](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

자격 증명 모음 hello hello 상태 표시줄 tooconfirm 올바르게 만들어졌는지 확인 합니다. hello 자격 증명 모음으로 나열 됩니다 **활성** 주 hello에 **복구 서비스** 페이지.

## <a name="step-2-deploy-a-configuration-server"></a>2단계: 구성 서버 배포
### <a name="configure-server-settings"></a>서버 설정 구성
1. Hello에 **복구 서비스** 페이지 hello 자격 증명 모음 tooopen hello 빠른 시작 페이지를 클릭 합니다. 빠른 시작 언제 든 지 hello 아이콘을 사용 하 여 열 수도 있습니다.

    ![빠른 시작 아이콘](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Hello 드롭다운 목록에서 선택 **/물리적 서버 및 Azure와 온-프레미스 사이트 간**합니다.
3. **대상(Azure) 리소스 준비**에서 **구성 서버 배포**를 클릭합니다.

    ![구성 서버 배포](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. **새 구성 서버 세부 정보** 에 다음을 지정합니다.

   * Hello 구성 서버 및 자격 증명 tooconnect tooit에 대 한 이름입니다.
   * Hello 네트워크 연결 유형에서 드롭다운 선택 목록 **공용 인터넷** 또는 **VPN**합니다. 이 설정이 적용된 후에는 수정할 수 없습니다.
   * 선택 hello Azure 네트워크는 hello에 서버를 배치 해야 합니다. VPN 확인을 사용 하 여 있는지 hello Azure 네트워크는 연결 된 tooyour 온-프레미스 네트워크 예상 대로입니다.
   * Hello 내부 IP 주소 및 서브넷을 할당할 toohello 서버를 지정 합니다. Azure 내부 사용에 대 한 hello 모든 서브넷에 있는 처음 네 개의 IP 주소는 예약 되어 있습니다. 다른 IP 주소를 사용하세요.

     ![구성 서버 배포](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. 클릭할 때 **확인** hello 구성 서버에 대 한 구독에 Azure 사이트 복구 Windows Server 2012 R2 갤러리 이미지에 따라 표준 A3 가상 컴퓨터 생성 됩니다. 새 클라우드 서비스에 첫 번째 인스턴스가 hello로 생성 됩니다. Hello 인터넷 hello 클라우드 서비스를 통해 tooconnect를 선택한 경우 예약 된 공용 IP 주소로 만들어집니다. Hello에서 진행률을 모니터링할 수 **작업** 탭 합니다.

    ![진행률 모니터링](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. 통해 연결 하는 경우 인터넷 hello 구성 서버 배포 참고 hello 공용 IP 주소 할당 tooit hello에 되 면 hello **가상 컴퓨터** hello Azure 포털에서에서 페이지입니다. 그 다음에 hello **끝점** 탭 참고 hello 공용 HTTPS 포트 매핑된 tooprivate 포트 443입니다. Hello 구성 서버와 마스터 대상 hello 및 프로세스 서버를 등록 하면 나중에이 정보를 해야 합니다. 이러한 끝점과 hello 구성 서버를 배포 합니다.

   * HTTPS: 공용 포트는 구성 요소 서버 간 통신 사용 되는 toocoordinate 및 Azure를 통해 인터넷 hello 합니다. 개인 포트 443는 VPN을 통해 구성 요소 서버와 Azure 간에 사용 되는 toocoordinate 통신입니다.
   * Custom: 공용 포트가 사용 되는 장애 복구 도구 통신에 대 한 hello를 통해 인터넷 합니다. 개인 포트 9443은 VPN에서 장애 복구 도구 통신에 사용됩니다.
   * PowerShell: 개인 포트 5986
   * 원격 데스크톱: 개인 포트 3389

   ![VM 끝점](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > 구성 서버 배포 중에 만들어진 모든 끝점의 hello 공개 또는 개인 포트 번호를 변경 하거나 삭제 하지 마십시오.
   >
   >

hello 구성 서버는 예약 된 IP 주소로 자동으로 만들어진된 Azure 클라우드 서비스에 배포 됩니다. hello 예약 된 주소는 구성 서버 클라우드 서비스 IP 주소를 hello 필요한 tooensure 남아 hello에 가상 컴퓨터 (hello 구성 서버 포함) hello 클라우드 서비스의 다시 부팅 해도 hello 동일 합니다. hello 예약 된 공용 IP 주소가 필요 합니다 toobe 수동으로 예약 되지 않은 경우 hello 구성 서버를 서비스 해제 하거나 예약 된 상태로 유지 합니다. 기본적으로 구독당 예약된 공용 IP 주소 수는 20개로 제한됩니다. 예약된 IP 주소에 대해 [자세히 알아보세요](../virtual-network/virtual-networks-reserved-private-ip.md).

### <a name="register-hello-configuration-server-in-hello-vault"></a>Hello 구성 서버 hello 자격 증명 모음 등록
1. Hello에 **빠른 시작** 페이지 **대상 리소스 준비** > **등록 키 다운로드**합니다. hello 키 파일이 자동으로 생성 됩니다. 이 파일은 생성된 날로부터 5일간 유효합니다. 구성 서버 toohello 복사 합니다.
2. **가상 컴퓨터** hello 가상 컴퓨터 목록에서 구성 서버 hello 선택 합니다. 열기 hello **대시보드** 탭을 클릭 **연결**합니다. **열기** hello 원격 데스크톱을 사용 하 여 hello 구성 서버에 RDP 파일 toolog 다운로드 합니다. VPN을 사용 하는 경우 hello 온-프레미스 사이트에서 원격 데스크톱 연결에 대 한 hello 내부 IP 주소 (hello 구성 서버를 배포할 때 지정한 hello 주소)를 사용 합니다. hello Azure 사이트 복구 구성 서버 설치 마법사가 자동으로 로그온 할 때 hello에 대 한 처음으로 실행 합니다.

    ![등록](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. **제 3 자 소프트웨어 설치** 클릭 **동의** toodownload 및 MySQL 설치 합니다.

    ![MySQL 설치](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. **MySQL 서버 세부 정보** hello MySQL 서버 인스턴스로 toolog 자격 증명을 만듭니다.

    ![MySQL 자격 증명](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. **인터넷 설정을** hello 구성 서버에서 toohello를 연결 하는 방법을 지정 합니다. 인터넷 합니다. 다음 사항에 유의하세요.

   * Toouse 하려는 경우 사용자 지정 프록시 설정 해야이 hello 공급자를 설치 하기 전에.
   * 클릭할 때 **다음** 테스트 toocheck hello 프록시 연결을 실행 합니다.
   * 사용자 지정 프록시를 사용 하 여 수행 하거나 기본 프록시에 인증이 필요한 경우 hello 주소, 포트 및 자격 증명을 포함 한 tooenter hello 프록시 정보를 해야 합니다.
   * 다음 Url hello hello 프록시를 통해 액세스할 수 있어야 합니다.
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * IP 주소 기반 있는 경우 방화벽 규칙 hello 규칙에 설명 된 hello 구성 서버 toohello IP 주소에서 tooallow 통신이 설정 되어 있는지 확인 [Azure 데이터 센터 IP 범위](https://msdn.microsoft.com/library/azure/dn175718.aspx) 및 HTTPS (443) 프로토콜입니다. Hello 계획 toouse, 및 미국 서 부의 Azure 지역의 IP 범위 toowhite 나열 해야 합니다.

     ![프록시 등록](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. **공급자 오류 메시지 지역화 설정** 오류 메시지 tooappear 하려는 언어를 지정 합니다.

    ![오류 메시지 등록](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. **Azure 사이트 복구 등록** 찾아보기 및 선택 hello 키 파일 toohello 서버를 복사 합니다.

    ![키 파일 등록](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Hello hello 마법사 완료 페이지에서 이러한 옵션을 선택 합니다.

   * 선택 **계정 관리 대화 상자 시작** hello 마법사를 완료 한 후 관리 계정 대화 상자를 hello toospecify 열려야 합니다.
   * 선택 **Cspsconfigtool에 대 한 바탕 화면 아이콘을 만드는** tooadd hello 구성 서버에서 바탕 화면 바로 가기 hello를 열 수 있도록 **계정 관리** 언제 든 지 toorerun hello 필요 없이 대화 상자 마법사입니다.

     ![등록 완료](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. 클릭 **마침** toocomplete hello 마법사. 암호가 생성됩니다. Tooa 안전한 위치로 복사 합니다. Tooauthenticate 필요 하 고 구성 서버 hello에 hello 프로세스 및 마스터 대상 서버를 등록 합니다. 구성 서버 통신에서 tooensure 채널 무결성을 데도 했습니다. Hello 암호를 다시 생성할 수 있지만 toore 레지스터 hello 마스터 대상 및 프로세스 서버 hello 새 암호를 사용 하 여이 필요 합니다.

    ![암호](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

등록 후 hello 구성 서버 hello에 나열 됩니다 **구성 서버** hello 자격 증명 모음에 페이지입니다.

### <a name="set-up-and-manage-accounts"></a>계정 설정 및 관리
배포 하는 동안 사이트 복구 작업을 수행 하는 hello에 대 한 자격 증명을 요청 합니다.

* 사이트 복구가 vCenter 서버나 vSphere 호스트에서 VM을 자동으로 검색할 수 있도록 하는 VMware 계정.
* 추가 하면 컴퓨터를 보호 하기 위해 사이트 복구에 hello 모바일 서비스를 설치할 수 있도록 합니다.

Hello 구성 서버에 등록 한 후에 hello을 열 수 있습니다 **계정 관리** 대화 tooadd 계정을 이러한 작업에 사용 해야 하 고 관리 합니다. 두 가지 방법으로 toodo이

* Hello 바로 가기 toocreated hello hello hello 구성 서버 (cspsconfigtool)에 대 한 설치 프로그램의 마지막 페이지에는 대화에 대 한 제외를 엽니다.
* 구성 서버 설치 프로그램의 대화 상자가 열려 hello 완료 합니다.

1. **계정 관리** click **계정 추가**이 포함되어 있습니다. 기존 계정을 수정 및 삭제할 수도 있습니다.

    ![계정 관리](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. **계정 세부 정보** Azure 및 자격 증명 (도메인/사용자 이름)에서 계정 이름을 toouse를 지정 합니다.

    ![계정 관리](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Toohello 구성 서버에 연결
두 가지 방법으로 tooconnect toohello 구성 서버 가지가 있습니다.

* VPN 사이트 간 연결 또는 Express 경로를 통해
* 통해 인터넷 hello

다음 사항에 유의하세요.

* Hello 가상 컴퓨터의 hello 끝점 hello 공용 가상 IP 주소 hello 서버와 함께에서 사용 하는 인터넷에 연결 합니다.
* VPN 연결 hello 끝점 개인 포트와 함께 hello hello 서버의 내부 IP 주소를 사용합니다.
* 일회성 의사 결정 toodecide 여부는 온-프레미스 서버 toohello에서 tooconnect (제어 및 복제 데이터) (구성 서버, 마스터 대상 서버)의 다양 한 구성 요소 서버 VPN 연결을 통해 Azure에서 실행 중인 또는 인터넷을 환영 합니다. 나중에 이 설정을 변경할 수 없습니다. 이렇게 하면 필요 tooredeploy 시나리오 hello 하 여 컴퓨터를 다시 보호 하십시오.  

## <a name="step-3-deploy-hello-master-target-server"></a>3 단계: hello 마스터 대상 서버를 배포 합니다.
1. **대상(Azure) 리소스 준비** > **마스터 대상 서버 배포**를 클릭합니다.
2. Hello 마스터 대상 서버 세부 정보 및 자격 증명을 지정 합니다. hello 서버 hello에 배포 될 hello 구성 서버와 같은 Azure 네트워크입니다. Toocomplete를 클릭할 때 Windows 또는 Linux 갤러리 이미지를 사용 하는 Azure 가상 컴퓨터 생성 됩니다.

    ![대상 서버 설정](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Azure 내부 사용에 대 한 hello 모든 서브넷에 있는 처음 네 개의 IP 주소는 예약 되어 있습니다. 사용 가능한 다른 IP 주소를 사용하세요.

> [!NOTE]
> 일관 된 높은 I/O 성능 및 낮은 대기 시간 사용 하 여 순서 toohost I/O 집약적인 작업에 필요한 작업에 대 한 보호를 구성할 때 표준 DS4 선택 [프리미엄 저장소 계정](../storage/common/storage-premium-storage.md)합니다.
>
>

1. 이러한 끝점을 사용하여 Windows 마스터 대상 서버 VM이 만들어집니다. Note는 공용 끝점 인터넷 hello를 통해 연결 하는 경우에 생성 됩니다.

   * Custom: hello를 통한 hello 프로세스 서버 toosend 복제 데이터에서 사용 되는 공용 포트 인터넷 합니다. 개인 포트 9443 VPN을 통해 hello 프로세스 서버 toosend 복제 데이터 toohello 마스터 대상 서버에서 사용 됩니다.
   * 사용자 지정 1: hello를 통한 hello 프로세스 서버 toosend 메타 데이터에 의해 사용 되는 공용 포트 인터넷 합니다. 개인 포트 9080 VPN을 통해 hello 프로세스 서버 toosend 메타 데이터 toohello 마스터 대상 서버에서 사용 됩니다.
   * PowerShell: 개인 포트 5986
   * 원격 데스크톱: 개인 포트 3389
2. 이러한 끝점을 사용하여 Linux 마스터 대상 서버 VM이 만들어집니다. 공용 끝점 hello를 통해 연결 하는 경우에 생성 됩니다 인터넷 합니다.

   * Custom: hello를 통한 서버 toosend 복제 데이터를 처리 하 여 사용 되는 공용 포트 인터넷 합니다. 개인 포트 9443 VPN을 통해 hello 프로세스 서버 toosend 복제 데이터 toohello 마스터 대상 서버에서 사용 됩니다.
   * 사용자 지정 1: 공용 포트는 hello 프로세스 서버 toosend 메타 데이터를 통해 의해 사용 hello 인터넷 합니다. 개인 포트 9080 VPN을 통해 hello 프로세스 서버 toosend 메타 데이터 toohello 마스터 대상 서버에서 사용 됩니다.
   * SSH: 개인 포트 22

     > [!WARNING]
     > Hello 마스터 대상 서버를 배포 하는 동안 만든 hello 끝점의 모든 hello 공개 또는 개인 포트 번호를 변경 하거나 삭제 하지 마십시오.
     >
     >
3. **가상 컴퓨터** hello 가상 컴퓨터 toostart 때까지 대기 합니다.

   * Hello 원격 데스크톱 세부 정보는 Windows server 기록해 경우.
   * Linux 서버와 hello 가상 컴퓨터의 VPN 참고 hello 내부 IP 주소를 통해 연결 하는 합니다. Hello 인터넷 참고 hello 공용 IP 주소를 통해 연결 합니다.
4. Hello 서버 toocomplete 설치에 로깅과 hello 구성 서버를 등록 합니다.
5. Windows를 실행하는 경우 다음을 수행합니다.

   1. 원격 데스크톱 연결 toohello 가상 컴퓨터를 시작 합니다. hello 스크립트에 로그온 하는 처음으로 실행 됩니다 PowerShell 창에서. 창을 닫지 마세요. 완료 되 면 자동으로 tooregister hello 서버를 hello 호스트 에이전트 구성 도구가 열립니다.
   2. **호스트 에이전트 구성** hello hello 구성 서버 및 포트 443의 내부 IP 주소를 지정 합니다. Hello 가상 컴퓨터가 연결 된 toohello 않아 하지 VPN을 통해 연결 하는 경우에 hello 내부 주소 및 개인 포트가 443 사용할 수 있습니다 hello 구성 서버와 같은 Azure 네트워크입니다. **HTTPS 사용** 을 설정된 상태로 둡니다. 앞에서 기록해 둔 hello 구성 서버에 대 한 hello 암호를 입력 합니다. 클릭 **확인** tooregister hello 서버입니다. Hello NAT 옵션을 무시할 수 있습니다. 해당 옵션은 사용되지 않습니다.
   3. 가상 디스크를 사용 하 여 hello 보존 볼륨 (r:) 해야 할 경우 예상된 보존 드라이브 1TB 이상 구성할 수 있습니다 및 [저장소 공간](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Windows 마스터 대상 서버](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Linux를 실행하는 경우 다음을 수행합니다.

   1. 있는지 확인 이전에 설치한 hello hello 마스터 대상 서버를 설치 하기 전에 최신 Linux Integration Services (LIS) 설치 합니다. 방법에 지침과 함께 LIS의 hello 최신 버전을 찾을 수 있습니다 tooinstall [여기](https://www.microsoft.com/download/details.aspx?id=46842)합니다. Hello LIS를 설치 hello 컴퓨터를 다시 시작 합니다.
   2. **대상(Azure) 리소스 준비**에서 **추가 소프트웨어 다운로드 및 설치(Linux 마스터 대상 서버 전용)**를 클릭합니다. 복사 hello sftp 클라이언트를 사용 하 여 tar 파일 toohello 가상 컴퓨터를 다운로드 합니다. Toohello 배포 된 linux 마스터 대상 서버에 로그온 하 고 사용할 수 또는 *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* toodownload hello hello 파일입니다.
   3. 보안 셸 클라이언트를 사용 하 여 toohello 서버에 로그온 합니다. 연결 된 경우 VPN 통해 Azure 네트워크 toohello hello 내부 IP 주소를 사용 합니다. 그렇지 않으면 hello 외부 IP 주소와 hello SSH 공용 끝점을 사용 합니다.
   4. Hello 파일을 실행 하 여 hello gzipped 설치 관리자에서 추출: **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![Linux 마스터 대상 서버](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Hello 디렉터리 toowhich에 맞는지 확인 hello tar 파일의 hello 내용을 추출 합니다.
   6. Hello 구성 서버 암호가 tooa 로컬 파일을 복사 hello 명령을 사용 하 여 **에코  *`<passphrase>`*  > passphrase.txt**
   7. Hello 명령을 실행 "**sudo. /-t 설치 두-a 호스트-R-d /usr/local/ASR MasterTarget-i  *`<Configuration server internal IP address>`*  -p 443-s y-c https-P passphrase.txt**" 합니다.

      ![대상 서버 등록](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. (10-15) 몇 분 동안 기다렸다가 hello 페이지 검사에 해당 hello 마스터 대상 서버에 등록 된 것으로 표시 된 **서버** > **구성 서버** **서버세부정보** 탭 합니다. Linux를 실행 하는 경우 등록 하지 않았습니다. hello 호스트 구성 도구를 다시 실행 /usr/local/ASR/Vx/bin/hostconfigcli에서. Chmod 루트로 실행 하 여 tooset 액세스 권한이 필요 합니다.

    ![대상 서버 확인](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> 등록 hello 마스터 대상 서버 toobe hello 포털에 나열 된에 대 한 완료 된 후 분 too15를 걸릴 수 있습니다. tooupdate 즉시 클릭 **새로 고침** hello에 **구성 서버** 페이지.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>4 단계: hello 온-프레미스 프로세스 서버 배포
시작 하기 전에 영구 toobe across 재부팅 보장할 수는 있도록 hello 프로세스 서버에서 고정 IP 주소를 구성 하는 것이 좋습니다.

1. 빠른 시작 > **프로세스 서버 설치 온-프레미스** > **hello 프로세스 서버 다운로드 및 설치**합니다.

    ![프로세스 서버 설치](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. 복사 hello tooinstall hello 프로세스 서버 들어가려는 거 zip 파일 toohello 서버를 다운로드 합니다. hello zip 파일을는 두 개의 설치 파일이 들어 있습니다.

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Hello 보관 및 복사 hello 파일 tooa 서버의 설치 위치를 hello 압축을 풉니다.
4. Hello 실행 **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** 설치 파일과 따라 hello 지시 합니다. Hello 배포에 필요한 타사 구성 요소를 설치 합니다.
5. 그런 다음 **Microsoft-ASR_CX_8.4.0.0_Windows***를 실행합니다.
6. Hello에 **서버 모드** 페이지 선택 **프로세스 서버**합니다.
7. Hello에 **환경 정보** 페이지 뒤 hello지 않습니다.

    - Tooprotect VMware 가상 컴퓨터 클릭 하려는 경우 **예**
    - 물리적 서버 tooprotect 높은 사람만 ् च VMware vCLI hello 프로세스 서버에 설치 되므로 필요 하지 않습니다. **아니요** 를 클릭하고 계속합니다.

1. VMware vCLI를 설치할 때 hello 다음 note:

   * **VMware vSphere CLI 5.5.0만 지원됩니다**. 다른 버전 또는 업데이트 vSphere CLI의 hello 프로세스 서버를 작동 하지 않습니다.
   * [여기](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * 바로 전에 hello 프로세스 서버 설치를 시작 하 고 설치 프로그램에서 검색 되지 않을 vSphere CLI를 설치한 경우까지 대기한 다음 toofive 설치 프로그램을 다시 시도 하기 전에 시간 (분)입니다. 이렇게 하면 있는지 모든 hello 환경 변수 필요한 vSphere CLI 검색에 대 한 초기화 된 올바르게 합니다.
2. **프로세스 서버에 대 한 NIC 선택을** 선택 hello 네트워크 어댑터가 해당 hello 프로세스 서버를 사용 해야 합니다.

   ![어댑터 선택](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. **구성 서버 세부 정보**에서:

   * Hello IP 주소 및 포트를 VPN을 통해 연결 하는 경우 hello hello 구성 서버의 내부 IP 주소 및 지정 hello 포트는 443입니다. 그렇지 않은 경우 hello 공용 가상 IP 주소와 공용 매핑된 HTTP 끝점을 지정 합니다.
   * Hello 구성 서버 hello 암호를 입력 합니다.
   * 지우기 **확인 이동성 서비스 소프트웨어 서명을** 자동 푸시 tooinstall hello 서비스를 사용 하는 경우 toodisable 확인 하려는 경우. 서명 확인 hello 프로세스 서버에서 인터넷 연결이 필요합니다.
   * **다음**을 누릅니다.

   ![구성 서버 등록](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. **설치 드라이브 선택** 에서 캐시 드라이브를 선택합니다. hello 프로세스 서버 캐시 드라이브와 600 g B 이상의 여유 공간이 있어야합니다. **설치**를 클릭합니다.

   ![구성 서버 등록](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. 참고 toorestart hello 서버 toocomplete hello 설치를 할 수 있습니다. **구성 서버** > **서버 세부 정보** 나타나고 hello 자격 증명 모음에 성공적으로 등록 되어 해당 hello 프로세스 서버를 확인 합니다.

> [!NOTE]
> 등록 hello 구성 서버에서 나열 된 프로세스 서버 tooappear hello에 대 한 완료 된 후 too15 분까지 걸릴 수 있으므로 합니다. tooupdate는 hello hello 구성 서버 페이지 맨 아래에 hello 새로 고침 단추를 클릭 하 여 hello 구성 서버를 즉시 새로
>
>

![프로세스 서버 유효성 검사](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Hello 프로세스 서버를 등록할 때 hello 모바일 서비스에 대 한 서명 확인 사용 하지 않도록 설정 하지 않은 경우 나중에 다음과 같이 수행할 수 있습니다.

1. 관리자 권한으로 프로세스 서버 hello에 오류를 로깅하고 hello C:\pushinstallsvc\pushinstaller.conf 편집할 파일을 엽니다. Hello 섹션 아래의 **[PushInstaller.transport]** 이 줄 추가: **SignatureVerificationChecks = "0"**합니다. 저장 하 고 hello 파일을 닫습니다.
2. Hello InMage PushInstall 서비스를 다시 시작 합니다.

## <a name="step-5-update-site-recovery-components"></a>5단계: 사이트 복구 구성 요소 업데이트
사이트 복구 구성 요소는 시간 tootime에서 업데이트 됩니다. 새 업데이트가 있는 경우 순서에 따라 hello에 설치 해야 합니다.

1. 구성 서버
2. 프로세스 서버
3. 마스터 대상 서버
4. 장애 복구(failback) 도구(vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Hello 업데이트 설치
1. Hello 사이트 복구에서에서 hello 구성, 프로세스 및 마스터 대상 서버에 대 한 업데이트를 가져올 수 **대시보드**합니다. Linux 설치에 대 한 hello gzipped 설치 관리자에서 hello 파일을 추출 하 고 hello 명령을 실행 "sudo. / 설치" tooinstall hello 업데이트 합니다.
2. [다운로드](http://go.microsoft.com/fwlink/?LinkID=533813) hello 장애 복구 tool(vContinuum) hello에 대 한 최신 업데이트.
3. 가상 컴퓨터 또는 설치 하는 hello 모바일 서비스가 이미 있는 물리적 서버를 실행 하는 경우 다음과 같이 업데이트 hello 서비스에 대 한 가져올 수 있습니다.

   * **옵션 1**: 업데이트를 다운로드합니다.
     * [Windows Server(64비트만 해당)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6(64비트만 해당)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5(64비트만 해당)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3(64비트만 해당)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Hello 프로세스 서버 hello를 업데이트 한 후 업데이트 된 버전의 모바일 서비스 hello 사용할 수 있는 폴더에 있을 hello C:\pushinstallsvc\repository hello 프로세스 서버입니다.
   * **옵션 2**: hello 컴퓨터에서 모바일 서비스 hello hello 관리 포털에서 자동으로 업그레이드할 수는 컴퓨터는 이전 버전의 hello 이동성 서비스가 설치 되어 있는 경우.

     1. Hello 프로세스 서버가 해당 업데이트 되었는지 확인 합니다.
     2. 해당 hello 보호 된 컴퓨터 hello 준수 확인 [필수 구성 요소](#install-the-mobility-service-automatically) hello 업데이트가 예상 대로 작동 되도록 hello 모바일 서비스를 자동으로 밀어 넣는 합니다.
     3. 선택 hello 보호 그룹을 강조 표시 hello 보호 된 컴퓨터 및 클릭 **업데이트 모바일 서비스**합니다. 이 단추는 hello 모바일 서비스의 최신 버전이 있는 경우에 사용할 수만 있습니다.

         ![vCenter 서버 선택](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Select 계정에서 보호 하는 hello 서버의 hello 관리자 계정 사용 toobe tooupdate hello 모바일 서비스를 지정 합니다. 확인을 클릭 하 고 hello 트리거된 작업 toocomplete 될 때까지 기다립니다.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>6단계: vCenter 서버 또는 vSphere 호스트 추가
1. 클릭 **서버** > **구성 서버** > 구성 서버 >**vCenter Server 추가** tooadd vCenter 서버나 vSphere 호스트 합니다.

    ![vCenter 서버 선택](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Hello 서버 또는 호스트와 사용 되는 toodiscover 될 선택 hello 프로세스 서버에 대 한 세부 정보를 지정 것입니다.

   * Hello vCenter 서버 hello 기본 443 포트에서 실행 되 고 있지는 hello vCenter 서버가 실행 중인 hello 포트 번호를 지정 합니다.
   * 프로세스 서버 hello 동일 네트워크에 hello vCenter 서버/vSphere 호스트 하 고 VMware vSphere CLI 5.5.0 설치 되어 있어야 하는 hello에 있어야 합니다.

     ![vCenter 서버 설정](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. 검색을 완료 한 후 hello vCenter 서버 hello 구성 서버 세부 정보 아래에 나열 됩니다.

    ![vCenter 서버 설정](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. 관리자가 아닌 계정 tooadd hello 서버 또는 호스트를 사용 하는 경우 hello 계정 권한을 다음 hello에 있는지 확인:

   * vCenter 계정은 데이터 센터, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 저장소 보기, 가상 컴퓨터가 있고 vSphere Distributed Switch 권한을 사용하도록 설정해야 합니다.
   * vSphere 계정을 호스트 hello Datacenter, 데이터 저장소, 폴더, 호스트, 네트워크, 리소스, 가상 컴퓨터 및 vSphere Distributed 스위치 권한을 사용할 수 있어야 합니다.

## <a name="step-7-create-a-protection-group"></a>7단계: 보호 그룹 만들기
1. **보호된 항목** > **보호 그룹** > **보호 그룹 만들기**를 엽니다.

    ![보호 그룹 만들기](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Hello에 **보호 그룹 설정 지정** 페이지 hello 그룹과 toocreate hello 그룹 원하는 선택 hello 구성 서버에 대 한 이름을 지정 합니다.

    ![보호 그룹 설정](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Hello에 **복제 설정 지정** 페이지 hello 그룹의 모든 hello 컴퓨터에 사용할 hello 복제 설정을 구성 합니다.

    ![보호 그룹 복제](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. 설정:

   * **다중 VM 일관성**: hello 시스템 hello 보호 그룹에 대해 공유 응용 프로그램 일치 복구 지점에서이 설정한 경우 만듭니다. 이 설정은 hello 보호 그룹에 있는 hello 컴퓨터의 모든 실행 하 고 경우에 가장 관련성이 높은 hello 같은 작업입니다. 모든 컴퓨터는 복구 된 toohello 됩니다 동일한 데이터 요소입니다. Windows 서버에만 사용할 수 있습니다.
   * **RPO 임계값**: hello 지속적인 데이터 보호 복제 RPO hello 구성 RPO 임계값을 초과할 때 경고가 생성 됩니다.
   * **복구 지점 보존**: hello 보존 기간을 지정 합니다. 보호 된 컴퓨터 수 있는이 창에서 tooany 포인트를 복구 합니다.
   * **응용 프로그램 일치 스냅숏 빈도**: 응용 프로그램 일치 스냅숏이 포함된 복구 지점을 만드는 방법을 지정합니다.

Hello에 만들어질 때 hello 보호 그룹을 모니터링할 수 있습니다 **보호 된 항목** 페이지.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>8 단계: 컴퓨터를 설정 하려는 tooprotect
Tooinstall hello tooprotect 원하는 물리적 서버와 가상 컴퓨터에서 모바일 서비스가 필요 합니다. 다음 두 가지 방법으로 수행할 수 있습니다.

* 자동으로 강제 하 고 hello 프로세스 서버에서 각 컴퓨터에 hello 서비스를 설치 합니다.
* Hello 서비스를 수동으로 설치 합니다.

### <a name="install-hello-mobility-service-automatically"></a>Hello 모바일 서비스를 자동으로 설치
추가할 컴퓨터 tooa 보호 그룹 hello 모바일 서비스가 자동으로 푸시 및 hello 프로세스 서버에서 각 컴퓨터에 설치 합니다.

**자동으로 푸시 Windows 서버에서 hello 모바일 서비스를 설치 합니다.**

1. 에 설명 된 대로 hello hello 프로세스 서버에 대 한 최신 업데이트를 설치 [5 단계: 최신 업데이트를 설치](#step-5-install-latest-updates), 해당 hello 프로세스 서버를 사용할 수 있는지 확인 합니다.
2. Hello 원본 컴퓨터 간에 네트워크로 연결 되어를 지정 했는지 확인 hello 프로세스 서버와 해당 hello 소스 컴퓨터 hello 프로세스 서버에서 액세스할 수 있습니다.  
3. Windows 방화벽 tooallow hello 구성 **파일 및 프린터 공유** 및 **Windows Management Instrumentation**합니다. Windows 방화벽 설정을 "응용 프로그램 또는 기능 허용 방화벽을 통해" hello 옵션을 선택 하 고 아래 hello 그림에 표시 된 대로 hello 응용 프로그램을 선택 합니다. 컴퓨터는 속해 tooa 도메인 GPO와 hello 방화벽 정책을 구성할 수 있습니다.

    ![방화벽 설정](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. hello 사용 되는 계정 tooperform hello 강제 설치 tooprotect 원하는 hello 컴퓨터에서 Administrators 그룹 hello 이어야 합니다. 이러한 자격 증명은 hello 모바일 서비스의 강제 설치에만 사용 하 고 컴퓨터 tooa 보호 그룹을 추가할 때 제공 합니다.
5. Hello 제공 계정을 도메인 계정이 없는 경우 toodisable hello 로컬 컴퓨터에 원격 사용자 액세스 제어 해야 합니다. toodo이 추가 hello LocalAccountTokenFilterPolicy DWORD 레지스트리 항목을 찾아에서 1의 값을 사용 합니다. CLI에서 tooadd hello 레지스트리 항목 cmd 또는 powershell을 열고 다음을 입력  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** 합니다.

**자동으로 푸시 hello 모바일 서비스를 Linux 서버에 설치 합니다.**

1. 에 설명 된 대로 hello hello 프로세스 서버에 대 한 최신 업데이트를 설치 [5 단계: 최신 업데이트를 설치](#step-5-install-latest-updates), 해당 hello 프로세스 서버를 사용할 수 있는지 확인 합니다.
2. Hello 원본 컴퓨터 간에 네트워크로 연결 되어를 지정 했는지 확인 hello 프로세스 서버와 해당 hello 소스 컴퓨터 hello 프로세스 서버에서 액세스할 수 있습니다.  
3. Hello 계정이 hello 원본 Linux 서버에 루트 사용자 인지 확인 합니다.
4. Hello 소스 서버 hello 로컬 호스트 이름 tooIP 주소 모든 Nic와 관련 된 매핑하는 항목을 포함 하는 Linux hello /etc/hosts 파일을 확인 합니다.
5. Hello 최신 openssh, openssh 서버, openssl 패키지 설치 tooprotect hello 컴퓨터에 원하는 합니다.
6. 포트 22에 SSH를 사용하고 실행 중인지 확인합니다.
7. 다음과 같이 hello sshd_config 파일에서 SFTP 하위 시스템 및 암호 인증을 사용 합니다.

   * a) 루트로 로그인합니다.
   * b)에서 hello 파일/등/ssh/sshd_config 파일으로 시작 하는 hello 줄 찾기 **PasswordAuthentication**합니다.
   * c) hello 줄의 주석 처리 제거 하 고 hello "no" 값을 너무 "yes" 변경 합니다.

       ![Linux 이동성](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * 하위 시스템으로 시작 하 고 hello 줄 주석 처리를 제거 하는 d) 찾기 hello 선입니다.

       ![Linux 푸시 이동성](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Hello 원본 컴퓨터 Linux 변형이 지원 되는지 확인 합니다.

### <a name="install-hello-mobility-service-manually"></a>Hello 모바일 서비스를 수동으로 설치
hello 소프트웨어 패키지 tooinstall hello Mobility C:\pushinstallsvc\repository hello 프로세스 서버에서이 서비스를 사용 합니다. Hello 프로세스 서버와 아래 hello 테이블을 기반으로 복사 hello 적절 한 설치 패키지 toohello 원본 컴퓨터에 로그온:-

| 원본 운영 체제 | 프로세스 서버의 모바일 서비스 패키지 |
| --- | --- |
| Windows Server(64비트만 해당) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6(64비트만 해당) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3(64비트만 해당) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5(64비트만 해당) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**Windows server에서 수동으로 모바일 서비스 tooinstall hello**, 다음 hello지 않습니다:

1. 복사 hello **Microsoft ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe** toohello 원본 컴퓨터 위에 hello 테이블에 hello 프로세스 서버 디렉터리 경로에서 패키지를 나열 합니다.
2. Hello 원본 컴퓨터에서 실행 하는 hello를 실행 하 여 hello 모바일 서비스를 설치 합니다.
3. Hello 설치 지침을 따릅니다.
4. 선택 **모바일 서비스** hello 역할과 클릭으로 **다음**합니다.

    ![모바일 서비스 설치](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. 기본 설치 경로 hello와 hello 설치 디렉터리를 두고 클릭 **설치**합니다.
6. **호스트 에이전트 구성** hello IP 주소 및 HTTPS 포트 hello 구성 서버를 지정 합니다.

   * 인터넷을 지정 하는 hello를 통해 연결 하는 경우 공용 가상 IP 주소와 공용 HTTPS 끝점 hello 포트로 hello 합니다.
   * VPN을 통해 연결 하는 경우에 hello 내부 IP 주소 및 hello 포트 443을 지정 합니다. **HTTPS 사용** 을 선택된 상태로 둡니다.

     ![모바일 서비스 설치](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Hello 구성 서버 암호가 지정 하 고 클릭 **확인** tooregister hello hello 구성 서버와 모바일 서비스입니다.

**hello 명령줄에서 toorun:**

1. Hello 암호 hello CX toohello 파일 "C:\connection.passphrase" hello 서버에서 복사한이 명령을 실행 합니다. 예에서 CX i 104.40.75.37 및 hello HTTPS 포트는 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Linux 서버에 hello 모바일 서비스를 수동으로 설치**:

1. Hello 프로세스 서버 toohello 원본 컴퓨터에서 위의 hello 테이블을 기반으로 하는 hello 적절 한 tar 보관 파일을 복사 합니다.
2. 셸 프로그램 연 hello 압축 된 tar 보관 tooa 로컬 경로 실행 하 여 추출`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Passphrase.txt 파일 만들기 hello 로컬 디렉터리 toowhich 입력 하 여 hello tar 보관의 hello 내용을 추출한  *`echo <passphrase> >passphrase.txt`*  셸에서 합니다.
4. 입력 하 여 hello 모바일 서비스를 설치  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* 합니다.
5. Hello IP 주소와 포트를 지정 합니다.

   * 인터넷 hello 구성 서버 가상 공용 IP 주소와 공용 HTTPS 끝점에 지정 하는 hello 통해 toohello 구성 서버를 연결 하는 경우 `<IP address>` 및 `<port>`합니다.
   * VPN 연결을 통해 연결 하는 경우에 hello 내부 IP 주소 및 443을 지정 합니다.

**hello 명령줄에서 toorun**:

1. Hello 암호 hello CX toohello 파일 "passphrase.txt" hello 서버에서 복사한이 명령을 실행 합니다. 예에서 CX i 104.40.75.37 및 hello HTTPS 포트는 62519:

프로덕션 서버의 tooinstall:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall hello 대상 서버에서:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Hello 강제 설치를 건너뜁니다 다음 hello 모바일 서비스의 적절 한 버전을 이미 실행 중인 컴퓨터 tooa 보호 그룹을 추가 하면 됩니다.
>
>

## <a name="step-9-enable-protection"></a>단계 9: 보호 사용
tooenable 보호 가상 컴퓨터와 물리적 서버 tooa 보호 그룹을 추가 합니다. 시작하기 전에 다음 사항에 주의하세요.

* 가상 컴퓨터는 15 분 마다 검색 하 고 해당 too15 분까지 걸릴 수 있으므로 Azure Site Recovery에서 검색 한 후 tooappear 합니다.
* 환경 변화 (예: VMware 도구 설치) hello 가상 컴퓨터도 too15 분 toobe 사이트 복구에서 업데이트를 차지할 수 있습니다.
* 마지막으로 검색 한 hello에 시간 hello를 확인할 수 있습니다 **마지막 연락처에** hello vCenter 서버/ESXi 호스트 hello에 대 한 필드 **구성 서버** 페이지.
* 가상 컴퓨터 toobe hello에 나열 된 및 Azure 사이트 복구 포털 toorefresh hello에 대 일 분이 걸리는 이미 만들어진 보호 그룹이 생성 하 고 그 후 vCenter 서버나 ESXi 호스트를 추가 하는 경우 **컴퓨터 tooa 보호 그룹 추가**  대화 상자.
* Hello에 예약 된 검색까지 기다리지 않고 컴퓨터 tooprotection 그룹을 추가 하 여 즉시 tooproceed, 원하는 경우 hello 구성 서버를 강조 표시 (클릭 하지 말고) hello 클릭 **새로 고침** 단추입니다.
* 가상 컴퓨터 또는 물리적 컴퓨터 tooa 보호 그룹을 추가 프로세스 서버 hello 자동으로 푸시 하 고 hello 이미 설치 되어 있지 hello 원본 서버에서 hello 모바일 서비스를 설치 합니다.
* Hello 자동 푸시 메커니즘에 대 한 toowork hello 이전 단계에 설명 된 대로 보호 된 컴퓨터를 설정한 있는지 확인 합니다.

다음 단계에 따라 컴퓨터를 추가합니다.

1. **보호된 항목** > **보호 그룹** > **컴퓨터** > **컴퓨터 추가**를 클릭합니다. 가장 좋은 방법은 특정 응용 프로그램 toohello 실행 되는 컴퓨터를 추가할 보호 그룹 작업 그대로 반영 해야 권장 같은 그룹입니다.
2. **가상 컴퓨터 선택** hello의 물리적 서버를 보호 하는 경우 **물리적 컴퓨터 추가** 마법사 hello IP 주소 및 이름을 제공 합니다. Hello 운영 체제 제품군을 선택 합니다.

    ![V-Center Server 추가](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. **가상 컴퓨터 선택** VMware 가상 컴퓨터를 보호 하는 경우 가상 컴퓨터 (또는 실행 하는 hello EXSi 호스트)를 관리 하 고 있는 vCenter 서버를 선택 하 고 hello 컴퓨터를 선택 합니다.

    ![V-Center Server 추가](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. **대상 리소스 지정** hello 마스터 대상 서버와 복제에 대 한 저장소 toouse를 선택 하 고 모든 작업에 대해 hello 설정을 사용할지 여부를 선택 합니다. 선택 [프리미엄 저장소 계정](../storage/common/storage-premium-storage.md) IO 일관 된 고성능 및 낮은 대기 시간 순서 toohost IO가 많은 작업에 필요한 작업에 대 한 보호를 구성 하는 중입니다. 프리미엄 저장소 계정의 toouse 작업 디스크에 대 한 원하는 경우 toouse hello DS 시리즈의 마스터 대상 해야 합니다. DS 시리즈가 아닌 마스터 대상의 경우 프리미엄 저장소 디스크를 사용할 수 없습니다.

   > [!NOTE]
   > Hello를 사용 하 여 만든 저장소 계정의 hello 이동을 지원 하지 않습니다 [새 Azure 포털](../storage/common/storage-create-storage-account.md) 리소스 그룹에 걸쳐 있습니다.
   >
   >

    ![vCenter Server](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. **계정 지정** toouse 보호 된 컴퓨터에 hello 모바일 서비스를 설치 하기 위한 원하는 hello 계정을 선택 합니다. hello 모바일 서비스의 자동 설치에 대 한 hello 계정 자격 증명이 필요 합니다. 계정을 선택할 수 없을 경우 2단계의 설명에 따라 설정합니다. 이 계정은 Azure로 액세스할 수 없습니다. Windows에 대 한 서버 hello 계정은 hello 원본 서버에서 관리자 권한이 있어야 합니다. Linux 용 hello 계정은 루트 이어야 합니다.

    ![Linux 자격 증명](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Hello 확인 표시가 toofinish 컴퓨터 toohello 보호 그룹과 toostart 초기 복제 각 컴퓨터에 대 한 추가 클릭 합니다. Hello에 상태를 모니터링할 수 **작업** 페이지.

    ![V-Center Server 추가](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. 또한 **보호된 항목** > 보호 그룹 이름 > **가상 컴퓨터**를 클릭하여 보호 상태를 모니터링할 수 있습니다. 표시는 초기 복제를 완료 하 고 데이터를 동기화 하는 hello 컴퓨터 **Protected** 상태입니다.

    ![가상 컴퓨터 작업](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>보호된 컴퓨터 속성 설정
1. 컴퓨터가 **보호됨** 상태이면 해당 장애 조치(failover) 속성을 구성할 수 있습니다. Hello 보호 그룹 세부 정보에서 선택 hello 시스템 및 열기 hello **구성** 탭 합니다.
2. 제공 될 toohello 컴퓨터 Azure에서 장애 조치 및 hello Azure 가상 컴퓨터 크기 후 hello 이름을 수정할 수 있습니다. 선택할 수도 있습니다 hello Azure 네트워크 toowhich hello 컴퓨터는 장애 조치 후 연결 됩니다.

   > [!NOTE]
   > [마이그레이션 네트워크의](../resource-group-move-resources.md) 전체 리소스 그룹 내 hello 동일한 구독 또는 구독에서 지원 되지 않습니다 Site Recovery를 배포 하는 데 사용 되는 네트워크에 대 한 합니다.
   >
   >

    ![가상 컴퓨터 등록 설정](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

다음 사항에 유의하세요.

* hello Azure 컴퓨터의 hello 이름 Azure 요구 사항을 준수 해야 합니다.
* 기본적으로 Azure에 복제 된 가상 컴퓨터에 연결 된 Azure 네트워크 tooan 되지 않습니다. Toocommunicate 있는지 확인 하는 복제 된 가상 컴퓨터를 원하는 tooset을 동일한 Azure 네트워크를 hello 합니다.
* VMware 가상 컴퓨터 또는 물리적 서버에서 볼륨 크기를 조정할 경우 심각한 상태가 됩니다. Toomodify hello 크기를 해야 하는 경우 다음 hello지 않습니다.

  * a) hello 크기 설정을 변경 합니다.
  * b)에서 hello **가상 컴퓨터** 탭 hello 가상 컴퓨터를 선택 하 고 클릭 **제거**합니다.
  * c)에서 **가상 컴퓨터 제거** hello 옵션을 선택 **(복구 드릴 및 볼륨 크기 조정) 보호 사용 안 함**합니다. 이 옵션은 보호를 사용 하지 않도록 설정 하지만 Azure의 hello 복구 지점 유지 합니다.

      ![가상 컴퓨터 등록 설정](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d) hello 가상 컴퓨터에 대 한 보호를 다시 설정 합니다. 볼륨 크기를 조정 하는 hello에 대 한 hello 데이터 보호를 다시 전송된 tooAzure 됩니다.

## <a name="step-10-run-a-failover"></a>10단계: 장애 조치(Failover) 실행
현재는 보호된 VMware 가상 컴퓨터 및 물리적 서버에 대해 계획되지 않은 장애 조치(Failover)만 실행할 수 있습니다. 참고 hello 다음.

* 장애 조치를 시작 하기 전에 hello 구성 및 마스터 대상 서버가 실행 되 고 정상 있는지 확인 합니다. 그렇지 않으면 장애 조치(Failover)가 실패합니다.
* 계획되지 않은 장애 조치(Failover) 시 원본 컴퓨터는 종료되지 않습니다. 예기치 않은 장애 조치가 수행 hello 보호 된 서버에 대 한 데이터 복제를 중지 합니다. Hello 보호 그룹에서 toodelete hello 컴퓨터가 필요 하 고 순서 toostart hello 계획 되지 않은 장애 조치가 완료 된 후 컴퓨터를 다시 보호에 다시 추가 합니다.
* 데이터 손실 없이 toofail 통해 하려는 경우 hello 장애 조치를 시작 하기 전에 hello 기본 사이트 가상 컴퓨터는 꺼져 있는지 확인 합니다.

1. Hello에 **복구 계획** 페이지 및 복구 계획을 추가 합니다. Hello 계획에 대 한 세부 정보를 지정 하 고 선택 **Azure** hello 대상으로 합니다.

    ![복구 계획 구성](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. **가상 컴퓨터 선택** 보호 그룹을 선택 하 고 hello 그룹 tooadd toohello 복구 계획에 컴퓨터를 선택 합니다. [자세한](site-recovery-create-recovery-plans.md) 복구 계획을 알아봅니다.

    ![가상 컴퓨터 추가](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. 필요한 사용자 지정할 수 있습니다 hello 계획 toocreate 그룹과 시퀀스 hello 순서 hello 복구의 어떤 컴퓨터에서 계획 된 장애 조치 합니다. 수동 작업 및 스크립트에 대한 프롬프트를 추가할 수도 있습니다. 스크립트를 사용 하 여 tooAzure 복구를 추가할 수 있습니다 때 hello [Azure 자동화 Runbook](site-recovery-runbook-automation.md)합니다.
4. Hello에 **복구 계획** 선택 hello 계획과 클릭 페이지 **계획 되지 않은 장애 조치**합니다.
5. **확인 장애 조치** hello 장애 조치 방향 (tooAzure)를 확인 하 고를 통해 복구 지점 toofail hello를 선택 합니다.
6. Hello 장애 조치 작업 toocomplete 표시 될 때까지 기다린 다음 hello 장애 조치가 예상 대로 작동 하 고 해당 hello 복제 가상 컴퓨터 시작 Azure에서 성공적으로 확인 합니다.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>11단계: Azure에서 장애 조치(Failover)된 컴퓨터 장애 복구
[자세한 내용은](site-recovery-failback-azure-to-vmware-classic-legacy.md) 방법에 대 한 toobring 프로그램 실패 한 컴퓨터에서 실행 중인 Azure 다시 tooyour 온-프레미스 환경입니다.

## <a name="manage-your-process-servers"></a>프로세스 서버 관리
프로세스 서버 hello Azure에서 복제 데이터 toohello 마스터 대상 서버를 보냅니다 및 새 VMware 가상 컴퓨터 추가 tooa vCenter 서버를 검색 합니다. 상황에 따라 hello 배포에 toochange hello 프로세스 서버를 설정할 수 있습니다.

* 현재 프로세스 서버 hello 작동이 중지 된 경우
* 경우 복구 지점 목표 (RPO) 조직에 대 한 허용 되지 않는 수준 tooan 상승 합니다.

온-프레미스 VMware 가상의 일부 또는 전부의 hello 복제를 이동할 수 필요한 경우 컴퓨터 및 물리적 서버 tooa 다른 서버를 처리 합니다. 예:

* **오류**-프로세스 서버가 실패 하거나 사용할 수 없는 복제 tooanother 프로세스 서버를 보호 된 컴퓨터를 이동할 수 있습니다. Hello 원본 컴퓨터와 복제 컴퓨터의 메타 데이터 이동된 toohello 새 프로세스 서버의 그리고 데이터 다시 동기화 됩니다. 새 프로세스 서버 hello toohello vCenter 서버 tooperform 자동 검색을 자동으로 연결 됩니다. 사이트 복구 대시보드 hello에 프로세스 서버 hello 상태를 모니터링할 수 있습니다.
* **부하 분산 RPO tooadjust**-향상 된 로드 균형 조정을 hello Site Recovery 포털에서 다른 프로세스 서버를 선택 하 고 수동 부하 분산에 대 한 하나 이상의 컴퓨터 tooit의 복제를 이동할 수 있습니다. 이 경우 hello 선택한 소스와 복제 컴퓨터의 메타 데이터는 새 프로세스 서버로 이동된 toohello 합니다. 원본 프로세스 서버 hello에 vCenter 서버를 연결 된 toohello 유지 됩니다.

### <a name="monitor-hello-process-server"></a>Hello 프로세스 서버 모니터
프로세스 서버가 위험 상태에 있으면 사이트 복구 대시보드 hello에 상태 경고가 표시 됩니다. Hello 상태 tooopen hello 이벤트 탭 클릭 하 고 드릴 다운 hello [작업] 탭에서 toospecific 작업 수 있습니다.

### <a name="modify-hello-process-server-used-for-replication"></a>복제에 사용 되는 hello 프로세스 서버를 수정 합니다.
1. **서버** > **구성 서버** > 구성 서버 > **서버 세부 정보**를 엽니다.
2. 클릭 **프로세스 서버** > **프로세스 서버 변경** toomodify 원하는 다음 toohello 서버입니다.

    ![프로세스 서버 1 변경](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. **프로세스 서버 변경** > **대상 프로세스 서버** 선택 hello 새 서버 toouse 한 다음 원하는 tooreplicate toohello 새 서버 hello 가상 컴퓨터를 선택 합니다. Hello 정보 아이콘 다음 toohello 서버 이름을 클릭 가능한 공간 및 사용 된 메모리의 세부 정보에 대 한 합니다. 각 가상 컴퓨터를 선택한 toohello 새 프로세스 서버를 결정 로드를 확인 하는 표시 된 toohelp 필요한 tooreplicate 될 평균 공간 hello입니다.

    ![프로세스 서버 2 변경](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Hello 확인 표시가 toobegin 복제 toohello 새 프로세스 서버를 클릭 합니다. 중요 하는 프로세스 서버에서 모든 가상 컴퓨터를 제거 하면 더 이상 표시할지 중요 한 경고 hello 대시보드에 참고 합니다.

## <a name="third-party-software-notices-and-information"></a>타사 소프트웨어 통지 및 정보
Do Not Translate or Localize

hello 소프트웨어 및 펌웨어에서 실행 중인 hello Microsoft 제품 또는 서비스 기반으로 하거나 통합 hello의 자료 (통칭 "제 3 자 코드") 아래에 나열 된 프로젝트입니다.  Microsoft는 hello hello 제 3 자 코드의 하지 원 작 자가 있습니다.  hello 원본 저작권 표시 및 라이선스, Microsoft는 이러한 제 3 자 코드를 받은 아래 명시 설정 됩니다.

A 섹션의 hello 정보에는 제 3 자 코드 아래에 나열 된 hello 프로젝트에서 구성 요소 관련입니다. Such licenses and information are provided for informational purposes only.  이 제 3 자 코드에서 Microsoft의 소프트웨어 사용 약관 hello Microsoft 제품 또는 서비스에 대 한 Microsoft에서 relicensed tooyou 되 고 있습니다.  

hello 정보 섹션 B에 대해 시도 하는 사용 가능한 tooyou microsoft hello 원래 라이선스 조건에 따라 제 3 자 코드 구성 요소 관련입니다.

hello 전체 파일 hello에서 발견 [Microsoft 다운로드 센터](http://go.microsoft.com/fwlink/?LinkId=529428)합니다. Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
