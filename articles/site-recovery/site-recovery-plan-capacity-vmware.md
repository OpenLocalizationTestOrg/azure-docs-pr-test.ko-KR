---
title: "용량 및 Azure 사이트 복구와 복제 tooAzure VMware에 대 한 확장성 aaaPlan | Microsoft Docs"
description: "Azure Site Recovery와 VMware Vm tooAzure를 복제 하는 경우이 문서 tooplan 용량 및 확장을 사용 하 여"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 0a1cd8eb-a8f7-4228-ab84-9449e0b2887b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: rayne
ms.openlocfilehash: 7ca9147d1b4611f6b4a67c3de3f27fb9878f4c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-capacity-and-scaling-for-vmware-replication-with-azure-site-recovery"></a>Azure Site Recovery를 사용하여 VMware 복제를 위한 용량 및 크기 조정 계획

이 문서 toofigure 용량 계획 및 크기 조정, 온-프레미스 VMware Vm 및 물리적 서버 tooAzure와 복제할 때 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.

## <a name="how-do-i-start-capacity-planning"></a>용량 계획을 시작하려면 어떻게 해야 하나요?

복제 환경에 대 한 정보를 수집 하 여 hello를 실행 하 여 [Azure 사이트 복구 배포 계획](https://aka.ms/asr-deployment-planner-doc) VMware 복제에 대 한 합니다. [자세히 알아보세요](site-recovery-deployment-planner.md) . 호환되거나 호환되지 않는 VM, VM당 디스크 및 디스크당 데이터 변동에 대한 정보를 수집합니다. hello 도구 hello 복제 및 테스트 장애 조치에 필요한 Azure 인프라 및 네트워크 대역폭 요구 사항에 대해서도 설명 합니다.

## <a name="capacity-considerations"></a>용량 고려 사항

**구성 요소** | **세부 정보** |
--- | --- | ---
**복제** | **최대 매일 변경 비율:** 보호 된 컴퓨터에는 하나의 프로세스 서버만 사용할 수 있으며 단일 프로세스 서버 too2 TB 매일 변경 비율을 처리할 수 있습니다. 따라서 2TB hello 최대 일일 데이터 변경 률 보호 된 컴퓨터에 대해 지원 되는입니다.<br/><br/> **최대 처리량:** 복제 된 컴퓨터는 Azure의 저장소 계정 tooone 속할 수 있습니다. 표준 저장소 계정을 최대 20, 000 초 당 요청을 처리할 수 있습니다 및 원본 컴퓨터 too20 000 걸쳐 hello IOPS (초당) 입/출력 작업 수를 유지 하는 것이 좋습니다. 예를 들어 5 개의 디스크를 사용 하는 원본 컴퓨터 있고 hello 원본 컴퓨터 120 IOPS (8k 크기)를 생성 하는 각 디스크 다음 됩니다 당 500 디스크 IOPS 제한 hello Azure 내에서. (필요한 저장소 계정의 hello 수 같은 toohello 총 소스 컴퓨터 IOPS, 20, 000로 나눈 값입니다.)
**구성 서버** | hello 구성 서버에 보호 된 컴퓨터에서 실행 되는 모든 작업에서 수 toohandle hello 매일 변경 비율 용량 있어야 하 고 필요한 충분 한 대역폭 toocontinuously tooAzure 데이터 저장소를 복제 합니다.<br/><br/> 모범 사례로, hello 구성 서버를 찾을 hello에 동일한 네트워크 및와 LAN 세그먼트 hello tooprotect 컴퓨터입니다. 다른 네트워크 하지만 tooprotect 계층 3 네트워크 가시성 tooit 있어야 합니다. 원하는 컴퓨터에 위치할 수 있습니다.<br/><br/> Hello 구성 서버에 대 한 크기 권장 사항 hello 섹션 다음에 hello 표에 요약 되어 있습니다.
**프로세스 서버** | 첫 번째 프로세스 서버 hello hello 구성 서버에 기본적으로 설치 됩니다. 사용자 환경의 추가 프로세스 서버 tooscale를 배포할 수 있습니다. <br/><br/> 보호 된 컴퓨터에서 복제 데이터를 수신 하 고 캐싱, 압축 및 암호화를 최적화 하는 hello 프로세스 서버입니다. 그런 다음 데이터 tooAzure hello를 보냅니다. hello 프로세스 서버 컴퓨터는 이러한 작업 충분 한 리소스 tooperform 있어야 합니다.<br/><br/> hello 프로세스 서버에서 디스크 기반 캐시를 사용 합니다. 600GB 또는 네트워크 병목 현상 또는 중단의 hello 이벤트에 저장 된 자세한 toohandle 데이터 변경의 별도 캐시 디스크를 사용 합니다.

## <a name="size-recommendations-for-hello-configuration-server"></a>Hello 구성 서버에 대 한 크기 권장 사항

**CPU** | **메모리** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터**
--- | --- | --- | --- | ---
8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) | 16GB | 300GB | 500GB 이하 | 100대 미만의 컴퓨터를 복제합니다.
12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) | 18GB | 600GB | 500GB too1 TB | 100-150대 컴퓨터를 복제합니다.
16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz) | 32GB | 1TB | 1TB too2 TB | 150-200대 컴퓨터를 복제합니다.
다른 프로세스 서버 배포 | | | > 2TB | 200 개 이상의 컴퓨터를 복제 하는 또는 속도 hello 일별 데이터 변경 하는 경우 2TB를 초과 하는 경우 추가 프로세스 서버를 배포 합니다.

여기서,

* 각 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.
* 캐시 디스크 측정을 위해 벤치마킹 저장소로 RAID 10을 이용한 10K RPM의 8개 SAS 드라이브를 사용했습니다.

## <a name="size-recommendations-for-hello-process-server"></a>프로세스 서버 hello에 대 한 크기 권장 사항

Tooprotect 200 개 이상의 컴퓨터가 필요 하거나 hello 매일 변경 률 2TB 보다 큰 경우에 프로세스 서버 toohandle hello 복제 부하를 추가할 수 있습니다. out tooscale를 수행할 수 있습니다.

* 구성 서버 hello 수를 늘립니다. 예를 들어 두 명의 구성 서버와 too400 컴퓨터를 보호할 수 있습니다.
* 프로세스 서버를 더 추가 하 고 이러한 toohandle 대신 (또는 외에) 트래픽 hello 구성 서버를 사용 합니다.

다음 표에서 hello는 시나리오를 설명 합니다.

* 프로세스 서버와 toouse hello 구성 서버를 의사가 있습니다.
* 추가 프로세스 서버를 설정했습니다.
* 보호 된 가상 컴퓨터 toouse hello 추가 프로세스 서버를 구성 했습니다.
* 보호된 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.

**구성 서버** | **추가 프로세스 서버** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터**
--- | --- | --- | --- | ---
8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB 메모리 | 4개 vCPU(2개 소켓 * 2코어 @ 2.5GHz), 8GB 메모리 | 300GB | 250GB 이하 | 85개 이하의 컴퓨터를 복제합니다.
8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 16GB 메모리 | 8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz), 12GB 메모리 | 600GB | 250GB too1 TB | 85-150대 컴퓨터를 복제합니다.
12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 18GB 메모리 | 12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz), 24GB 메모리 | 1TB | 1TB too2 TB | 150-225대 컴퓨터를 복제합니다.

서버 크기를 조정 하는 hello 방법은 수직 또는 수평 확장 모델에 대 한 기본 설정에 따라 다릅니다.  몇 가지 고급 구성 및 프로세스 서버를 배포하여 강화하거나 적은 리소스로 더 많은 서버를 배포하여 규모를 확장합니다. 예를 들어 tooprotect 220 컴퓨터 필요한 경우 hello 다음 중 하나 수행할 수 있습니다.

* 12 vCPU, 18 GB의 메모리를 12 vCPU, 24GB의 메모리를 사용 하 여 추가 프로세스 서버와 hello 구성 서버를 설정 합니다. 보호 된 컴퓨터 toouse hello 추가 프로세스 서버를 구성 합니다.
* 두 명의 구성 서버 (2 x 8 vCPU, 16GB RAM) 및 두 명의 추가 프로세스 서버 (1x8 vCPU 및 4 vCPU x 1 toohandle 135 + 85 [220] 컴퓨터)를 설정 합니다. 보호 된 컴퓨터 toouse hello 추가 프로세스 서버에만 구성 합니다.


## <a name="control-network-bandwidth"></a>네트워크 대역폭 제어

Hello를 사용한 후 [hello 배포 계획 도구](site-recovery-deployment-planner.md) (hello 초기 복제 및 다음 델타) 복제에 필요한 toocalculate hello 대역폭, hello 몇을 사용 하 여 복제에 사용 되는 대역폭 양을 제어할 수 있습니다 옵션:

* **대역폭 제한**: VMware 트래픽이 tooAzure를 복제 하는 특정 프로세스 서버를 통과 합니다. 프로세스 서버를 실행 하는 hello 컴퓨터의 대역폭을 제한할 수 있습니다.
* **대역폭에 영향을 줄**: 몇 가지 레지스트리 키를 사용 하 여 복제를 위해 사용 하는 hello 대역폭에 영향을 줄 수 있습니다.
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 레지스트리 값 hello 디스크의 데이터 전송 (초기 또는 델타 복제)에 사용 되는 스레드 수를 지정 합니다. 값을 높게 복제에 사용 되는 hello 네트워크 대역폭을 늘립니다.
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** hello 장애 복구 하는 동안 데이터 전송에 사용 되는 스레드 수를 지정 합니다.

### <a name="throttle-bandwidth"></a>대역폭 제한

1. Hello 프로세스 서버와 hello 컴퓨터 역할에 hello Azure 백업 MMC 스냅인을 엽니다. 기본적으로 백업에 대 한 바로 가기는 다음 폴더 hello 또는 hello 바탕 화면에서 사용할 수 있는: C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 합니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.

    ![Azure 백업 MMC 스크린샷 스냅인 옵션 toochange 속성](./media/site-recovery-vmware-to-azure/throttle1.png)
3. Hello에 **제한** 탭에서 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**합니다. 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다. 유효 범위는 512 Kbps too102 Mbps 초당에서.

    ![Azure Backup 속성 대화 상자의 스크린샷](./media/site-recovery-vmware-to-azure/throttle2.png)

Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다. 다음은 샘플입니다.

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.

### <a name="influence-network-bandwidth-for-a-vm"></a>VM의 네트워크 대역폭에 영향

1. Hello VM의 레지스트리에 이동 너무**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.
   * 복제 디스크에서 tooinfluence hello 대역폭 트래픽을의 hello 값을 수정 **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.
   * hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.
2. hello 기본값은 4입니다. "Overprovisioned" 네트워크에서 이러한 레지스트리 키 hello 기본값에서 변경 되어야 합니다. 최대 hello은 32입니다. 트래픽 toooptimize hello 값을 모니터링 합니다.


## <a name="deploy-additional-process-servers"></a>추가 프로세스 서버 배포

원본 컴퓨터를 200 개 초과 배포 아웃 tooscale 없거나 매일 이상 2TB의 속도 변동 총 경우 추가 프로세스 서버 toohandle hello 트래픽 볼륨을 해야 합니다. 이러한 지침은 tooset을 hello 프로세스 서버를 따릅니다. 마이그레이션한 원본 컴퓨터 toouse hello 서버를 설정한 후 것입니다.

1. **사이트 복구 서버**hello 구성 서버를 클릭 한 다음 클릭, **프로세스 서버**합니다.

    ![사이트 복구 스크린샷 서버 옵션 tooadd 프로세스 서버](./media/site-recovery-vmware-to-azure/migrate-ps1.png)
2. **서버 형식**에서 **프로세스 서버(온-프레미스)**를 클릭합니다.

    ![프로세스 서버 대화 상자의 스크린샷](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
3. Hello Site Recovery 통합 설치 파일을 다운로드 하 고 tooinstall hello 프로세스 서버를 실행 합니다. Hello 자격 증명 모음에이 등록도 됩니다.
4. **시작 하기 전에**선택, **배포 아웃 추가 프로세스 서버 tooscale 추가**합니다.
5. Hello에서 마법사를 완료 하는 hello 때 수행한 동일한 방식으로 있습니다 [설정](#step-2-set-up-the-source-environment) hello 구성 서버입니다.

    ![Azure Site Recovery 통합 설치 마법사의 스크린샷](./media/site-recovery-vmware-to-azure/add-ps1.png)
6. **구성 서버 세부 정보**hello 구성 서버의 hello IP 주소를 지정 하 고 hello 암호입니다. 실행 되는 tooobtain hello 암호 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello 구성 서버에 있습니다.

    ![구성 서버 세부 정보 페이지의 스크린샷](./media/site-recovery-vmware-to-azure/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>컴퓨터 toouse hello 새 프로세스 서버 마이그레이션
1. **설정** > **사이트 복구 서버**hello 구성 서버를 클릭 한 다음 확장, **서버 처리**합니다.

    ![프로세스 서버 대화 상자의 스크린샷](./media/site-recovery-vmware-to-azure/migrate-ps2.png)
2. 현재 사용, hello 프로세스 서버를 마우스 오른쪽 단추로 클릭 하 고 클릭 **스위치**합니다.

    ![구성 서버 대화 상자의 스크린샷](./media/site-recovery-vmware-to-azure/migrate-ps3.png)
3. **선택 대상 프로세스 서버**선택, 해당 hello 서버를 처리할 hello 새 프로세스 서버의 toouse, 한 다음 hello 가상 컴퓨터를 선택 합니다. Hello 정보 아이콘 tooget hello 서버에 대 한 정보를 클릭 합니다. 의사 결정을 로드을 tooreplicate 각 선택한 가상 컴퓨터 toohello 새 프로세스 서버의 표시 되는 데 필요한 평균 공간 hello toohelp 확인 합니다. Hello 확인 표시가 toostart 복제 toohello 새 프로세스 서버를 클릭 합니다.


## <a name="next-steps"></a>다음 단계

다운로드 및 실행 hello [Azure 사이트 복구 배포 계획](https://aka.ms/asr-deployment-planner)
