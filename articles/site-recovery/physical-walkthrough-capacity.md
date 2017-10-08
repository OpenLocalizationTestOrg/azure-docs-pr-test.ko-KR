---
title: "용량 및 Azure 사이트 복구와 복제 tooAzure 물리적 서버에 대 한 확장성 aaaPlan | Microsoft Docs"
description: "Azure Site Recovery와 Windows/Linux 물리적 서버의 tooAzure를 복제 하는 경우이 문서 tooplan 용량 및 확장을 사용 하 여"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>3 단계: 물리적 서버 tooAzure 복제에 대 한 확장성 및 용량 계획

이 문서 toofigure 용량 out을 사용 하 여 및 크기 조정이 복제 하는 온-프레미스와 Windows/Linux 물리적 서버의 tooAzure [Azure Site Recovery](site-recovery-overview.md)합니다.

Hello 아래쪽 hello 또는이 문서에 의견과 질문을 게시 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="plan-deployment-capacity"></a>배포 용량 계획

1. 이 내용을 읽고 [문서](site-recovery-plan-capacity-vmware.md) toolearn 복제 요구 사항 및 사이트 복구 구성 요소 크기 조정에 대 한 지침을 예측 하는 방법에 대 한 합니다.
2. 구성 요소 서버를 확장 하 고 복제 된 컴퓨터 대역폭을 제어 하는 방법에 대 한 toolearn 아래 hello 고려 사항 읽기입니다.

## <a name="replication-considerations"></a>복제 시 고려 사항

이러한 고려 사항 toofigure 요구 사항을 확인 된 복제 서버를 사용 합니다.

**구성 요소** | **세부 정보** 
--- | --- 
**복제** | **최대 매일 변경 비율:** 보호 된 컴퓨터에는 하나의 프로세스 서버만 사용할 수 있으며 단일 프로세스 서버 too2 TB 매일 변경 비율을 처리할 수 있습니다. 따라서 2TB hello 최대 일일 데이터 변경 률 보호 된 컴퓨터에 대해 지원 되는입니다.<br/><br/> **최대 처리량:** 복제 된 컴퓨터는 Azure의 저장소 계정 tooone 속할 수 있습니다. 표준 저장소 계정을 최대 20, 000 초 당 요청을 처리할 수 있습니다 및 원본 컴퓨터 too20 000 걸쳐 hello IOPS (초당) 입/출력 작업 수를 유지 하는 것이 좋습니다. 예를 들어 5 개의 디스크를 사용 하는 원본 컴퓨터 있고 hello 원본 컴퓨터 120 IOPS (8k 크기)를 생성 하는 각 디스크 다음 됩니다 당 500 디스크 IOPS 제한 hello Azure 내에서. (필요한 저장소 계정의 hello 수 같은 toohello 총 소스 컴퓨터 IOPS, 20, 000로 나눈 값입니다.)

## <a name="configuration-server-capacity"></a>구성 서버 용량

hello 구성 서버에 보호 된 컴퓨터에서 실행 되는 모든 작업에서 수 toohandle hello 매일 변경 비율 용량 있어야 하 고 필요한 충분 한 대역폭 toocontinuously tooAzure 데이터 저장소를 복제 합니다.

모범 사례로, hello 구성 서버를 찾을 hello에 동일한 네트워크 및와 LAN 세그먼트 hello tooprotect 컴퓨터입니다. 다른 네트워크 하지만 tooprotect 계층 3 네트워크 가시성 tooit 있어야 합니다. 원하는 컴퓨터에 위치할 수 있습니다.

## <a name="sizing-recommendations"></a>크기 조정 권장 사항

hello 테이블에는 CPU를 기반으로 크기 조정 권장 사항을 요약 합니다.

**CPU** | **메모리** | **캐시 디스크 크기** | **데이터 변경률** | **보호된 컴퓨터**
--- | --- | --- | --- | ---
8개 vCPU(2개 소켓 * 4코어 @ 2.5GHz) | 16GB | 300GB | 500GB 이하 | 100대 미만의 컴퓨터를 복제합니다.
12개 vCPU(2개 소켓 * 6코어 @ 2.5GHz) | 18GB | 600GB | 500GB too1 TB | 100-150대 컴퓨터를 복제합니다.
16개 vCPU(2개 소켓 * 8코어 @ 2.5GHz) | 32GB | 1TB | 1TB too2 TB | 150-200대 컴퓨터를 복제합니다.
다른 프로세스 서버 배포 | | | > 2TB | 200 개 이상의 컴퓨터를 복제 하는 또는 속도 hello 일별 데이터 변경 하는 경우 2TB를 초과 하는 경우 추가 프로세스 서버를 배포 합니다.

여기서,

* 각 원본 컴퓨터는 각각 100GB의 디스크 3개로 구성됩니다.
* 캐시 디스크 측정을 위해 벤치마킹 저장소로 RAID 10을 이용한 10K RPM의 8개 SAS 드라이브를 사용했습니다.

## <a name="process-server-capacity"></a>프로세스 서버 용량


보호 된 컴퓨터에서 복제 데이터를 수신 하 고 캐싱, 압축 및 암호화를 최적화 하는 hello 프로세스 서버입니다. 그런 다음 데이터 tooAzure hello를 보냅니다.

- hello 프로세스 서버 컴퓨터는 이러한 작업 충분 한 리소스 tooperform 있어야 합니다.
- 첫 번째 프로세스 서버 hello hello 구성 서버에 기본적으로 설치 됩니다. 사용자 환경의 추가 프로세스 서버 tooscale를 배포할 수 있습니다.
- hello 프로세스 서버에서 디스크 기반 캐시를 사용 합니다. 600GB 또는 네트워크 병목 현상 또는 중단의 hello 이벤트에 저장 된 자세한 toohandle 데이터 변경의 별도 캐시 디스크를 사용 합니다.
- Tooprotect 200 개 이상의 컴퓨터가 필요 하거나 hello 매일 변경 률 2TB 보다 큰 경우에 프로세스 서버 toohandle hello 복제 부하를 추가할 수 있습니다. out tooscale를 수행할 수 있습니다.
    - 구성 서버 hello 수를 늘립니다. 예를 들어 두 명의 구성 서버와 too400 컴퓨터를 보호할 수 있습니다.
    - 프로세스 서버를 더 추가 하 고 이러한 toohandle 대신 (또는 외에) 트래픽 hello 구성 서버를 사용 합니다.


### <a name="example-process-server-scaling"></a>예제 프로세스 서버 크기 조정

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

## <a name="deploy-additional-process-servers"></a>추가 프로세스 서버 배포

1. 에 따라 [이러한 지침](site-recovery-vmware-setup-azure-ps-resource-manager.md) tooset 추가 프로세스 서버를 구성 합니다.
2. Hello 암호를 설정 하지 않은 경우 실행 **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** hello 구성 서버 tooget에 해당 합니다.
3. 마이그레이션한 원본 컴퓨터 toouse hello 프로세스 서버를 설정한 후 것입니다.

    1. **설정** > **사이트 복구 서버**, hello 구성 서버를 클릭 > **서버 처리**합니다.
    2. 현재 사용 중인 hello 프로세스 서버를 마우스 오른쪽 단추로 클릭 > **스위치**합니다.
    3. **선택 대상 프로세스 서버**선택, 해당 hello 서버를 처리할 hello 프로세스 서버 toouse, 한 hello Vm을 선택 합니다.
    4. Hello 정보 아이콘을 클릭 합니다. 의사 결정을 로드을 tooreplicate 각 선택한 VM toohello 새 프로세스 서버에서 표시 되는 데 필요한 평균 공간 hello toohelp 확인 합니다.
    5. Hello 확인 표시가 toostart 복제 toohello 새 프로세스 서버를 클릭 합니다.

## <a name="control-network-bandwidth"></a>네트워크 대역폭 제어

실행 한 후 [hello 배포 계획 도구](site-recovery-deployment-planner.md) (hello 초기 복제 및 다음 델타) 복제에 필요한 toocalculate hello 대역폭, hello는 두 가지 옵션을 사용 하 여 복제에 사용 되는 대역폭 양을 제어할 수 있습니다.

* **대역폭 제한**: VMware 트래픽이 tooAzure를 복제 하는 특정 프로세스 서버를 통과 합니다. 프로세스 서버를 실행 하는 hello 컴퓨터의 대역폭을 제한할 수 있습니다.
* **대역폭에 영향을 줄**: 몇 가지 레지스트리 키를 사용 하 여 복제를 위해 사용 하는 hello 대역폭에 영향을 줄 수 있습니다.
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** 레지스트리 값 hello 디스크의 데이터 전송 (초기 또는 델타 복제)에 사용 되는 스레드 수를 지정 합니다. 값을 높게 복제에 사용 되는 hello 네트워크 대역폭을 늘립니다.
  * hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** hello 장애 복구 하는 동안 데이터 전송에 사용 되는 스레드 수를 지정 합니다.

### <a name="throttle-bandwidth"></a>대역폭 제한

1. Hello 프로세스 서버와 hello 컴퓨터 역할에 hello Azure 백업 MMC 스냅인을 엽니다. 기본적으로 백업에 대 한 바로 가기는 다음 폴더 hello 또는 hello 바탕 화면에서 사용할 수 있는: C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 합니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.
3. Hello에 **제한** 탭에서 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**합니다.
4. 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다. 유효 범위는 512 Kbps too102 Mbps 초당에서.

    ![제한](./media/physical-walkthrough-capacity/throttle2.png)

Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다. 다음은 샘플입니다.

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.

### <a name="influence-network-bandwidth-for-a-vm"></a>VM의 네트워크 대역폭에 영향

1. Hello VM의 레지스트리에서 이동 너무**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.
   * 복제 디스크에서 tooinfluence hello 대역폭 트래픽을의 hello 값을 수정 **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.
   * hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.
2. hello 기본값은 4입니다. 과도하게 프로비전된 네트워크에서는 이러한 레지스트리 키를 수정해야 합니다. 최대 hello은 32입니다. 트래픽 toooptimize hello 값을 모니터링 합니다.




## <a name="next-steps"></a>다음 단계

너무 이동[4 단계: 네트워킹 계획](physical-walkthrough-network.md)합니다.
