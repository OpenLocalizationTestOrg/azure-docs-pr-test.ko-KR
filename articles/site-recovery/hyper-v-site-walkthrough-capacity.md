---
title: "용량 및 Azure 사이트 복구와 Hyper-v VM (VMM 없음) 복제 tooAzure에 대 한 확장성 aaaPlan | Microsoft Docs"
description: "Azure Site Recovery와 tooAzure Hyper-v Vm을 복제 하는 경우이 문서 tooplan 용량 및 확장을 사용 하 여"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8687af60-5b50-481c-98ee-0750cbbc2c57
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: f5b029f273e51c01c7d918d176832f6d1735b5f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-tooazure-replication"></a>3 단계: Hyper-v tooAzure 복제에 대 한 확장성 및 용량 계획

이 문서 toofigure 용량 계획 및 크기 조정와 온-프레미스 Hyper-v Vm (System Center VMM) 없이 tooAzure 복제할 때 사용 하 여 [Azure Site Recovery](site-recovery-overview.md)합니다.

이 문서를 읽은 후 hello 맨 아래에 모든 메모를 게시 하거나 hello에 대 한 기술적 질문 [Azure 복구 서비스 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)합니다.


## <a name="how-do-i-start-capacity-planning"></a>용량 계획을 시작하려면 어떻게 해야 하나요?


복제 환경에 대 한 정보를 수집 하 고 hello 고려 사항은이 문서에서 강조 표시와 함께이 정보를 사용 하 여 용량을 계획 합니다.


## <a name="gather-information"></a>정보 수집

1. VM, VM당 디스크, 디스크당 저장소를 포함하여 복제 환경에 대한 정보를 수집합니다.
2. 복제된 데이터에 대한 일일 변경(이탈)률을 식별합니다. Hello 다운로드 [Hyper-v 용량 계획 도구](https://www.microsoft.com/download/details.aspx?id=39057) tooget hello 변경 비율입니다. 평균 주 toocapture를 통해이 도구를 실행 하는 것이 좋습니다.
 

## <a name="figure-out-capacity"></a>용량 파악

Hello를 실행 했습니다. 수집 hello 정보에 따라 [사이트 복구 용량 계획 도구](http://aka.ms/asr-capacity-planner-excel) tooanalyze 원본 환경 및 작업에서 대역폭 요구 사항과 hello 원본 위치에 대 한 서버 리소스를 예측 하 고 hello 리소스 (가상 컴퓨터 및 저장소 등)는 hello 대상 위치에 필요한입니다. 몇 가지 모드에서에서 hello 도구를 실행할 수 있습니다.

- 계획 빠른: Vm, 디스크, 저장소 및 변경률이 평균 수에 따라 tooget 네트워크 및 서버 프로젝션이이 모드에서는 hello 도구를 실행 합니다.
- 자세한 계획:이 모드에서는 hello 도구를 실행 하 고 VM 수준에서 각 작업의 세부 정보를 제공 합니다. VM 호환성을 분석하고 네트워크 및 서버를 예상합니다.

이제 hello 도구를 실행 합니다.

1. Hello 다운로드 [도구](http://aka.ms/asr-capacity-planner-excel)
2. toorun hello 빠른 계획에 따라 [이러한 지침](site-recovery-capacity-planner.md#run-the-quick-planner), 및 select hello 시나리오 **Hyper-v tooAzure**합니다.
3. toorun 자세한 플래너 hello를 수행 하십시오. [이러한 지침](site-recovery-capacity-planner.md#run-the-detailed-planner), 및 select hello 시나리오 **Hyper-v tooAzure**합니다.

## <a name="control-network-bandwidth"></a>네트워크 대역폭 제어

필요한 계산 된 hello 대역폭 한 후에 몇 가지 복제에 사용 되는 대역폭 제어 hello 크기에 대 한 옵션

* **대역폭 제한**: tooAzure를 복제 하는 Hyper-v 트래픽이 특정 Hyper-v 호스트를 통과 합니다. Hello 호스트 서버에서 대역폭을 제한할 수 있습니다.
* **대역폭에 영향을 줄**: 몇 가지 레지스트리 키를 사용 하 여 복제에 사용 되는 hello 대역폭에 영향을 줄 수 있습니다.

### <a name="throttle-bandwidth"></a>대역폭 제한
1. Hello Microsoft Azure 백업 MMC 스냅인 hello Hyper-v 호스트 서버에서 엽니다. 기본적으로 Microsoft Azure 백업에 대 한 바로 가기는 C:\Program Files\Microsoft Azure 복구 서비스 Agent\bin\wabadmin 또는 hello 바탕 화면에서 사용할 수 있습니다.
2. Hello 스냅인에서 클릭 **속성 변경**합니다.
3. Hello에 **제한** 탭 선택 **백업 작업에 대 한 인터넷 대역폭 제한을 사용 하도록 설정**, 작업에 대 한 hello 제한을 설정 하 고 비 작업 시간입니다. 유효 범위는 512 Kbps too102 Mbps 초당에서.

    ![대역폭 제한](./media/hyper-v-site-walkthrough-capacity/throttle2.png)

Hello를 사용할 수도 있습니다 [Set-obmachinesetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset 제한 합니다. 다음은 샘플입니다.

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** 은 제한이 필요 없다는 뜻입니다.

### <a name="influence-network-bandwidth"></a>네트워크 대역폭에 영향
1. 너무 hello 레지스트리 이동**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**합니다.
   * 복제 디스크에서 tooinfluence hello 대역폭 트래픽을 수정 hello 값 hello **UploadThreadsPerVM**, 하거나 존재 하지 않는 경우 hello 키를 만듭니다.
   * hello 값을 수정 하는 Azure에서 장애 복구 트래픽을 tooinfluence hello 대역폭 **DownloadThreadsPerVM**합니다.
2. hello 기본값은 4입니다. "Overprovisioned" 네트워크에서 이러한 레지스트리 키 hello 기본값에서 변경 되어야 합니다. 최대 hello은 32입니다. 트래픽 toooptimize hello 값을 모니터링 합니다.

## <a name="next-steps"></a>다음 단계

너무 이동[4 단계: 네트워킹 계획](hyper-v-site-walkthrough-network.md)합니다.
