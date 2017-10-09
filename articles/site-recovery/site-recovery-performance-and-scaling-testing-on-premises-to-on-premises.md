---
title: "Azure Site Recovery와 사이트 간 Hyper-v 복제에 대 한 aaaTest 결과 | Microsoft Docs"
description: "이 문서에서는 Azure Site Recovery를 사용 하 여 성능 Hyper-v Vm의 온-프레미스 tooon 온-프레미스 복제에 대 한 테스트에 대 한 정보를 제공 합니다."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>사이트 복구와 온-프레미스 tooon 온-프레미스 Hyper-v 복제에 대 한 테스트 결과

Tooorchestrate Microsoft Azure Site Recovery를 사용 하 고 가상 컴퓨터 및 물리적 서버 tooAzure 또는 tooa 보조 데이터 센터의 복제를 관리할 수 있습니다. 이 문서에서는 성능 때 두 Hyper-v 가상 컴퓨터를 복제할 온-프레미스 데이터 센터에 수행한 테스트의 hello 결과 제공.

## <a name="test-goals"></a>테스트 목표

테스트의 hello 목표는 안정 상태 복제 중 Azure 사이트 복구가 수행 하는 방법을 tooexamine 이었습니다. 안정적 상태 복제는 가상 컴퓨터가 초기 복제를 완료하고 델타 변경 내용을 동기화하는 경우에 발생합니다. 대부분의 가상 컴퓨터 유지 예기치 않은 중단이 발생 하지 않으면 hello 상태 이기 때문에 일정 한 상태를 사용 하 여 중요 한 toomeasure 성능 것 합니다.

각 사이트에서 VMM 서버와 함께 두 개의 온-프레미스 사이트로 hello 테스트 배포 구성 되었습니다. 이 테스트 배포는 hello 주 사이트 및 hello 보조 또는 복구 사이트로 hello 지점 역할을 하는 본사와 대표적인 본사/지사 office 배포의 합니다.

## <a name="what-we-did"></a>수행한 내용

어떤 않았습니다 hello 테스트에서 전달 다음과 같습니다.

1. VMM 템플릿을 사용하여 가상 컴퓨터 생성.
2. 가상 컴퓨터 시작 및 12시간 동안 기준 성능 메트릭 캡처.
3. 기본 및 복구 VMM 서버에 클라우드 생성.
4. 원본 및 복구 클라우드의 매핑을 비롯하여 Azure Site Recovery에서 클라우드 보호 구성.
5. 가상 컴퓨터에 대 한 보호를 사용 하 고 toocomplete 초기 복제를 허용 합니다.
6. 시스템에 안정화될 때까지 대기.
7. 12시간 동안 예상된 복제 상태로 모든 가상 컴퓨터가 유지되는지 확인하기 위해 12시간 동안 성능 메트릭 캡처.
8. Hello 기본 성능 메트릭과 복제 성능 메트릭을 hello 간의 hello 델타를 측정 합니다.


## <a name="primary-server-performance"></a>기본 서버 성능

* Hyper-v 복제본 hello 주 서버에 변경 내용을 tooa 로그 파일 최소 저장소 오버 헤드를 비동기적으로 추적합니다.
* Hyper-v 복제본에서 자체 관리 되는 메모리 캐시 toominimize IOPS 오버 헤드에 대 한 추적을 사용합니다. 메모리 및 hello 하기 전에 hello 로그 파일에 시간 해당 hello 로그 플러시에서 VHDX toohello 복구 사이트에 전송 되는 쓰기 toohello를 저장 합니다. 디스크 플러시 hello 쓰기가 미리 결정 된 제한에 도달 하는 경우에 발생 합니다.
* hello 그래프 아래에 복제에 대 한 안정적인 상태 IOPS 오버 헤드를 hello 보여 줍니다. IOPS 오버 헤드 due tooreplication 약 상당히 낮 5%는 해당 hello를 볼 수 있습니다.

![기본 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Hyper-v 복제본에서 주 서버 toooptimize 디스크 성능 hello에 메모리를 사용합니다. 다음 그래프는 hello와 같이 메모리 hello 주 클러스터의 모든 서버에 오버 헤드가 한계가 됩니다. 오버 헤드를 표시 하는 hello 메모리는 hello hello Hyper-v 서버에 비해 복제 설치 toohello 총 메모리에 의해 사용 된 메모리 비율입니다.

![기본 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Hyper-V 복제본에는 최소 CPU 오버헤드가 있습니다. Hello 그래프에 표시 된 것과 같이 복제 오버 헤드가 2-3%의 hello 범위에서입니다.

![기본 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>보조(복구) 서버 성능

Hyper-v 복제본 저장소 작업의 hello 복구 서버 toooptimize hello 번호에서 적은 양의 메모리를 사용합니다. hello 그래프 hello 복구 서버의 hello 메모리 사용량을 요약합니다. 오버 헤드를 표시 하는 hello 메모리는 hello hello Hyper-v 서버에 비해 복제 설치 toohello 총 메모리에 의해 사용 된 메모리 비율입니다.

![보조 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

hello 복구 사이트에서 I/O 작업 양은 hello 함수 hello hello 기본 사이트에 쓰기 작업 수입니다. Hello 기본 사이트에 대 한 쓰기 작업와 hello 총 I/O 작업 hello 총 I/O 작업 수와 비교한 hello 복구 사이트에서 보고 해 보겠습니다. hello 그래프에는 hello 복구 사이트에서 IOPS는 해당 hello 합계 표시

* 약 1.5 배 hello 기본 hello를 IOPS를 작성 합니다.
* 약 37 %hello 총 hello 기본 사이트에 대 한 IOPS입니다.

![보조 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![보조 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>네트워크 사용률에 미치는 영향

네트워크 대역폭의 초당 275mb 평균 초당 5gb 인 기존 대역폭에 대 한 hello 주 노드와 복구 노드 사이의 압축과 함께 사용 하도록 설정 사용 되었습니다.

![결과 네트워크 사용률](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>VM 성능에 미치는 영향

중요 한 고려 사항에는의 hello 가상 컴퓨터에서 실행 되는 프로덕션 작업 복제 hello 영향입니다. Hello 주 사이트 복제에 대 한 프로 비전 적절 하 게 되 면 hello 워크 로드에 영향을 받지 되지 않아야 합니다. Hyper-v 복제본의 간단한 추적 메커니즘을 사용 하면 hello 가상 컴퓨터에서 실행 되는 작업 안정 상태 복제 중 영향을 받지 않습니다. 이 hello 다음 그래프에에서 표시 됩니다.

이 Graph는 복제를 사용하기 전과 후에 다른 워크로드를 실행하는 가상 컴퓨터를 통해 수행되는 IOPS를 보여줍니다. Hello 2 사이 차이점이 없고 있다는 것을 확인할 수 있습니다.

![복제본 효과 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

hello 다음 그래프 hello 처리량 복제를 사용 하는 후 및 하기 전에 다양 한 작업을 실행 중인 가상 컴퓨터. 해당 복제에 심각한 영향이 없음을 확인할 수 있습니다.

![복제본 효과에 대한 결과](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>결론

hello 결과 Azure 사이트 복구를 Hyper-v 복제본과 결합 된 대규모 클러스터 오버 헤드를 최소화 하면서 적절히 조정 있는지 명확 하 게 표시 됩니다.  Azure Site Recovery는 간단한 배포, 복제, 관리 및 모니터링을 제공합니다. Hyper-v 복제본은 성공적인 복제 크기 조정에 대 한 hello 필요한 인프라를 제공합니다. 최적의 배포를 계획에 대 한 hello 다운로드 제안 [Hyper-v 복제본 용량 플래너](https://www.microsoft.com/download/details.aspx?id=39057)합니다.

## <a name="test-environment-details"></a>테스트 환경 세부 정보

### <a name="primary-site"></a>기본 사이트

* hello 기본 사이트에는 470 개의 가상 컴퓨터를 실행 하는 5 명의 Hyper-v 서버를 포함 하는 클러스터를 있습니다.
* hello 가상 컴퓨터에 여러 작업을 실행 하 고 모든는 Azure Site Recovery 보호 기능을 사용 합니다.
* Hello 클러스터 노드에 대 한 저장소는 iSCSI SAN 통해 제공 됩니다. 모델 – Hitachi HUS130.
* 각 클러스터는 서버의 각각 1Gbps인 네트워크 카드(NIC)가 4개 있습니다.
* Hello 네트워크 카드의 두 가지는 연결 된 tooan iSCSI 개인 네트워크 및 연결 된 tooan 외부 엔터프라이즈 네트워크 두 개는 합니다. Hello 외부 네트워크 중 하나는 클러스터 통신 전용으로 예약 됩니다.

![기본 하드웨어 요구 사항](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| 서버 | RAM | 모델 | 프로세서 | 프로세서 수 | NIC | 소프트웨어 |
| --- | --- | --- | --- | --- | --- | --- |
| 클러스터의 Hyper-V 서버:  <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128ESTLAB-HOST25는 256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0, 2.20GHz |4 |IGbps 4개 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V role |
| VMM 서버 |2 | | |2 |1Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>보조(복구) 사이트

* hello 보조 사이트에는 6 개 노드 장애 조치 클러스터를 있습니다.
* Hello 클러스터 노드에 대 한 저장소는 iSCSI SAN 통해 제공 됩니다. 모델 – Hitachi HUS130.

![기본 하드웨어 사양](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| 서버 | RAM | 모델 | 프로세서 | 프로세서 수 | NIC | 소프트웨어 |
| --- | --- | --- | --- | --- | --- | --- |
| 클러스터의 Hyper-V 서버:  <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell ™ PowerEdge ™ R720 |Intel(R) Xeon(R) CPU E5-2630 0, 2.30GHz |2 |IGbps 4개 |Windows Server Datacenter 2012 R2 (x64) + Hyper-V role |
| ESTLAB-HOST17 |128 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0, 2.20GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V role |
| ESTLAB-HOST24 |256 |Dell ™ PowerEdge ™ R820 |Intel(R) Xeon(R) CPU E5-4620 0, 2.20GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + Hyper-V role |
| VMM 서버 |2 | | |2 |1Gbps |Windows Server Database 2012 R2 (x64) + VMM 2012 R2 |

### <a name="server-workloads"></a>서버 작업

* 테스트를 위해 엔터프라이즈 고객 시나리오에서 일반적으로 사용되는 작업을 선택했습니다.
* 사용 하 여 [IOMeter](http://www.iometer.org) 시뮬레이션에 대 한 hello 표에 요약 된 hello 작업 특성과 사용 합니다.
* 모든 IOMeter 프로필 toowrite 임의 바이트 toosimulate 최악의 쓰기 작업 패턴을 설정 합니다.

| 워크로드 | I/O 크기(KB) | 액세스 % | 쓰기 % | 미해결 I/O | I/O 패턴 |
| --- | --- | --- | --- | --- | --- |
| 파일 서버 |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |모두 100% 임의 |
| SQL Server(볼륨 1) SQL Server(볼륨 2) |864 |100%100% |70%0% |88 |100% 임의 100% 순차 |
| Exchange |32 |100% |67% |8 |100% 임의 |
| 워크스테이션/VDI |464 |66%34% |70%95% |11 |둘 다 100% 임의 |
| 웹 파일 서버 |4864 |33%34%33% |95%95%95% |888 |모두 75% 임의 |

### <a name="vm-configuration"></a>VM 구성

* hello 주 클러스터의 가상 컴퓨터 470 합니다.
* VHDX 디스크에 있는 모든 가상 컴퓨터입니다.
* Hello 표에 요약 된 작업을 실행 하는 가상 컴퓨터. 모두 VMM 템플릿으로 생성되었습니다.

| 워크로드 | VM 수 | 최소 RAM(GB) | 최대 RAM(GB) | VM당 논리 디스크 크기(GB) | 최대 IOPS |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| 파일 서버 |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| 웹 서버 |149 |.5 |1 |80 |6 |
| 전체 |470 | | |96.83TB |4108 |

### <a name="site-recovery-settings"></a>Site Recovery 설정

* Azure Site Recovery 온-프레미스 tooon 온-프레미스 보호에 대해 구성 된
* hello VMM 서버에 Hyper-v 클러스터 서버 hello 및 해당 가상 컴퓨터를 포함 하는 4 개의 클라우드가 구성 되어 있습니다.

| 기본 VMM 클라우드 | Hello 클라우드의 가상 컴퓨터 보호 | 복제 빈도 | 추가 복구 지점 |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15분 |없음 |
| PrimaryCloudRpo30s |47 |30초 |없음 |
| PrimaryCloudRpo30sArp1 |47 |30초 |1 |
| PrimaryCloudRpo5m |235 |5분 |없음 |

### <a name="performance-metrics"></a>성능 메트릭

hello 성능 메트릭 및 카운터 hello 배포에서 측정 된 hello 테이블에 요약 되어 있습니다.

| 메트릭 | 카운터 |
| --- | --- |
| CPU |\Processor(_Total)\% 프로세서 시간 |
| 사용 가능한 메모리 |\Memory\사용 가능한 MB |
| IOPS |\PhysicalDisk(_Total)\디스크 전송/초 |
| VM 읽기(IOPS) 작업/초 |\Hyper-V 가상 저장소 장치(<VHD>)\읽기 작업/초 |
| VM 쓰기(IOPS) 작업/초 |\Hyper-V 가상 저장소 장치(<VHD>)\쓰기 작업/초 |
| VM 읽기 처리량 |\Hyper-V 가상 저장소 장치(<VHD>)\읽기 바이트/초 |
| VM 쓰기 처리량 |\Hyper-V 가상 저장소 장치(<VHD>)\쓰기 바이트/초 |

## <a name="next-steps"></a>다음 단계

[2개의 온-프레미스 VMM 사이트 간 복제 설정](site-recovery-vmm-to-vmm.md)
