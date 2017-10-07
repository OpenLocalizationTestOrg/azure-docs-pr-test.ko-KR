---
title: "Azure Premium Storage: 성능을 위한 설계 | Microsoft Docs"
description: "Azure 프리미엄 저장소를 사용하여 고성능 응용 프로그램을 설계합니다. 프리미엄 저장소는 Azure 가상 컴퓨터에서 실행되는 I/O 사용량이 많은 작업에 대해 대기 시간이 짧은 고성능 디스크 지원을 제공합니다."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Azure 프리미엄 저장소: 고성능을 위한 설계
## <a name="overview"></a>개요
이 문서는 Azure 프리미엄 저장소를 사용하여 고성능 응용 프로그램을 구축하기 위한 지침을 제공합니다. 성능 모범 사례 적용 가능한 tootechnologies 응용 프로그램에서 사용 하는와 함께이 문서에 제공 된 hello 지침을 사용할 수 있습니다. tooillustrate hello 지침 예를 들어이 문서를 통해 프리미엄 저장소에서 실행 중인 SQL Server 사용 했습니다.

이 문서의 hello 저장소 계층에 대 한 성능 시나리오를 다루고 있습니다 toooptimize hello 응용 프로그램 계층이 필요 합니다. 예를 들어 Azure 프리미엄 저장소에 SharePoint 팜을 호스팅하는 경우에이 문서 toooptimize hello 데이터베이스 서버에서 SQL Server 예제 hello를 사용할 수 있습니다. 또한 hello SharePoint 팜의 웹 서버 및 응용 프로그램 서버 tooget hello 대부분 성능을 최적화 합니다.

이 문서에서는 Azure 프리미엄 저장소에서 응용 프로그램 성능을 최적화하는 방법에 대한 다음과 같은 일반적인 질문에 대답합니다.

* 어떻게 toomeasure 응용 프로그램 성능을?  
* 예상되는 고성능이 표시되지 않는 이유는 무엇입니까?  
* 프리미엄 저장소에서 응용 프로그램 성능에 영향을 주는 요인은 무엇입니까?  
* 이러한 요소가 프리미엄 저장소의 응용 프로그램 성능에 주는 영향은 무엇입니까?  
* IOPS, 대역폭 및 대기 시간을 최적화하는 방법은 무엇입니까?  

프리미엄 저장소에서 실행되는 작업은 성능이 매우 중요하므로 특별히 프리미엄 저장소에 대한 지침을 제공합니다. 적절한 예제를 제공합니다. 또한 표준 저장소 디스크와 IaaS Vm에서 실행 되는 이러한 지침 tooapplications 중 일부를 적용할 수 있습니다.

를 시작 하기 전에 새 tooPremium 저장 하려는 경우, 먼저 hello 읽어 [프리미엄 저장소: Azure 가상 컴퓨터 워크 로드 용 고성능 저장소](storage-premium-storage.md) 및 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)문서입니다.

## <a name="application-performance-indicators"></a>응용 프로그램 성과 지표
응용 프로그램 성능 지표와 같은 사용 하 여 여부 잘 수행 하는지 여부를 평가, 속도 응용 프로그램이 사용자 요청, 요청에 따라 응용 프로그램에서 처리 하는 데이터의 양을 처리, 특정에서 처리 하는 응용 프로그램 요청 수가 시간, 사용자에 게 toowait tooget 응답의 요청을 제출한 후의 기간입니다. 이러한 성능 지표에 대 한 hello 기술 용어는, IOPS, 처리량 또는 대역폭 및 대기 시간입니다.

이 섹션에서는 프리미엄 저장소의 hello 컨텍스트에서 hello 일반적인 성능 표시기를 설명 합니다. Hello 섹션 뒤, 응용 프로그램 요구 사항 수집, 배웁니다 어떻게 toomeasure 응용 프로그램에 대 한 이러한 성능 표시기입니다. 이러한 성능 지표 및 권장 사항 toooptimize를 영향을 주는 hello 요소에 대해 배웁니다 응용 프로그램 성능 최적화의 뒷부분에 해당 합니다.

## <a name="iops"></a>IOPS
IOPS 수는 응용 프로그램을 보내는 지 toohello 저장소 디스크 1 초에 요청 합니다. 입력/출력 작업은 읽기나 쓰기, 순차 또는 임의가 될 수 있습니다. OLTP 응용 프로그램을 온라인 소매상 웹 사이트와 같은 필요한 tooprocess 많은 동시 사용자가 즉시 요청 합니다. hello 사용자 요청은 insert 및 hello 응용 프로그램을 신속 하 게 처리 해야 하는 데이터베이스 사용량이 많은 트랜잭션을 업데이트 합니다. 따라서 OLTP 응용 프로그램에는 매우 높은 IOPS가 필요합니다. 이러한 응용 프로그램에서는 수백만 개의 작고 임의의 IO 요청을 처리합니다. 이러한 응용 프로그램의 경우 IOPS에 대 한 hello 응용 프로그램 인프라 toooptimize를 디자인 해야 합니다. Hello에 나중에 섹션 *응용 프로그램 성능 최적화*, tooget 고려해 야 할 모든 hello 요인을 자세하게에서 논의 높은 IOPS입니다.

연결할 때는 프리미엄 저장소 디스크 tooyour 대규모 VM을 하면 hello 디스크 사양에 따라 보장된 IOPS 수에 대 한 Azure 프로 비전 합니다. 예를 들어 P50 디스크는 7500IOPS를 프로비전합니다. 각 높은 확장성의 VM 크기에는 유지할 수 있는 특정 IOPS 제한이 있습니다. 예를 들어 표준 GS5 VM에는 80,000 IOPS 제한이 있습니다.

## <a name="throughput"></a>처리량
처리량 또는 대역폭 hello 양의 데이터를 응용 프로그램을 보내는 지 toohello 저장소 디스크에 지정된 된 간격입니다. 응용 프로그램이 대량 IO 단위 크기를 사용하여 입력/출력 작업을 수행하는 경우 높은 처리량이 필요합니다. 데이터 웨어하우스 응용 프로그램에는 한 번에 많은 양의 데이터를 액세스 하 고 일반적으로 대량 작업을 수행할 tooissue 검사 집약적인 작업은 경향이 있습니다. 즉, 이러한 응용 프로그램에는 더 높은 처리량이 필요합니다. 이러한 응용 프로그램을 사용 하는 경우 처리량에 대 한 해당 인프라 toooptimize를 디자인 해야 합니다. Hello 다음 섹션에서 자세히 hello 팩터로 논의 tooachieve이 조정 해야 합니다.

연결할 때는 프리미엄 저장소 디스크 tooa 대규모 VM을 해당 디스크 사양에 따라 Azure 프로 비전 처리량입니다. 예를 들어 P50 디스크는 초당 250MB 디스크 처리량을 프로비전합니다. 높은 확장성의 VM 크기마다 유지할 수 있는 특정 처리량 제한이 있습니다. 예를 들어 표준 GS5 VM에는 초당 2,000MB의 최대 처리량이 있습니다. 

처리량 및 IOPS hello 수식 아래에 나와 있는 것 처럼 사이의 관계가 있습니다.

![](media/storage-premium-storage-performance/image1.png)

따라서 것이 중요 한 toodetermine hello 최적의 처리량 및 IOPS 응용 프로그램에 필요한 값입니다. Toooptimize 하나를 시도할 때 다른 hello 가져옵니다 영향을 받습니다. 이후 섹션 *응용 프로그램 성능 최적화*에서 IOPS 및 처리량 최적화에 대한 자세한 정보에 대해 설명합니다.

## <a name="latency"></a>대기 시간
대기 시간은 hello 시간이 응용 프로그램 tooreceive 단일 요청 하 고 toohello 저장소 디스크를 보낼 hello 응답 toohello 클라이언트 전송 합니다. 이 중요 한 추가 tooIOPS 및 처리량에 응용 프로그램의 성능 측정 합니다. 프리미엄 저장소 디스크의 대기 시간 hello는 hello 시간 요청에 대 한 tooretrieve hello 정보를 사용 하 고 통신 tooyour 응용 프로그램을 백업 합니다. 프리미엄 저장소는 일관된 낮은 대기 시간을 제공합니다. 프리미엄 저장소 디스크에 읽기 전용 호스트 캐싱을 사용하는 경우 훨씬 더 낮은 읽기 대기 시간을 얻을 수 있습니다. *응용 프로그램 성능 최적화*의 이후 섹션에서 디스크 캐싱에 대해 자세히 설명합니다.

응용 프로그램 tooget 최적화할 때 높은 IOPS 및 처리량을 hello 응용 프로그램의 대기 시간에 영향을 줍니다. Hello 응용 프로그램 성능 튜닝 작업 후 항상 hello hello 응용 프로그램 tooavoid의 대기 시간 평가 대기 시간이 긴 예기치 않은 동작입니다.

## <a name="gather-application-performance-requirements"></a>응용 프로그램 성능 요구 사항 수집
Azure 프리미엄 저장소에서 실행 되는 고성능 응용 프로그램 디자인 hello 첫 번째 단계는 응용 프로그램의 toounderstand hello 성능 요구 사항입니다. 성능 요구 사항을 수집 하 여 응용 프로그램 tooachieve hello 최적의 성능을 최적화할 수 있습니다.

Hello 이전 섹션에서는 hello 일반적인 성과 지표, IOPS, 처리량 및 대기 시간에 설명합니다. 이러한 성능 표시기는 중요 한 tooyour 응용 프로그램 toodeliver 원하는 hello 사용자 경험을 식별 해야 합니다. 예를 들어, 높은 IOPS 초당에서 수백만 개의 트랜잭션 처리 하는 대부분 tooOLTP 응용 프로그램을 중요 합니다. 반면 초당 많은 양의 데이터를 처리하는 데이터 웨어하우스 응용 프로그램에는 높은 처리량이 중요합니다. 라이브 비디오 스트리밍 웹 사이트와 같은 실시간 응용 프로그램에는 매우 짧은 대기 시간이 중요합니다.

다음으로 측정 수명 기간 동안 응용 프로그램의 hello 최대 성능을 요구 합니다. 아래 샘플 checklist hello 시작 정보를 사용 합니다. 보통 동안 레코드 hello 최대 성능 요구 사항, 최고 및 업무 시간 이후 작업 기간입니다. 모든 작업 수준에 대 한 요구 사항을 식별 하면 수 toodetermine 됩니다 hello 응용 프로그램의 전체 성능 요구 사항입니다. 예를 들어 전자 상거래 웹 사이트의 정상 작업 hello hello 트랜잭션을 대부분 일 년에서 동안 사용 됩니다. hello 웹 사이트의 최대 작업 hello hello 트랜잭션을 휴일 기간 또는 이벤트 특별 한 판매 하는 동안 사용 됩니다. hello 최대 작업은 일반적으로 숙련 된 제한 된 기간에 대 한 되지만 사용자 응용 프로그램 tooscale 두 필요할 수 있습니다 또는 일반적인 작업 제한 시간이 더 합니다. Hello 50 백분위 수, 90 백분위 수 99 백분위 수 요구 사항에 대해 알아봅니다. 이렇게 하면 hello 성능 요구 사항에서 이상 값을 필터링 하 고 hello 오른쪽 값에 대 한 최적화에 여 노력을 집중할 수 있습니다.

**응용 프로그램 성능 요구 사항 검사 목록**

| **성능 요구 사항** | **50 백분위수** | **90 백분위수** | **99 백분위수** |
| --- | --- | --- | --- |
| 최대 초당 트랜잭션 수 | | | |
| % 읽기 작업 | | | |
| % 쓰기 작업 | | | |
| % 임의 작업 | | | |
| % 순차적 작업 | | | |
| IO 요청 크기 | | | |
| 평균 처리량 | | | |
| 최대 처리량 | | | |
| 최소 대기 시간 | | | |
| 평균 대기 시간 | | | |
| 최대 CPU | | | |
| 평균 CPU | | | |
| 최대 메모리 | | | |
| 평균 메모리 | | | |
| 큐 크기 | | | |

> [!NOTE]
> 응용 프로그램의 예상된 향후 성장에 따라 이러한 숫자를 확장하는 것이 좋습니다. 나중에 성능 향상을 위한 toochange hello 인프라 쉽다는 점 수도 있으므로 미리 증가 위한 것이 좋습니다 tooplan입니다.
>
>

기존 응용 프로그램을 한 toomove tooPremium 저장소를 원하는 경우 먼저 구축 hello 기존 응용 프로그램에 대 한 위의 hello 검사 목록입니다. 그런 다음에 설명 된 지침에 따라 프리미엄 저장소 및 디자인 hello 응용 프로그램에서 응용 프로그램의 프로토타입을 빌드 *응용 프로그램 성능 최적화* 이 문서의 뒷부분에 나오는 섹션에 있습니다. 다음 섹션 hello toogather hello 성능 측정값을 사용할 수 있습니다 하는 hello 도구를 설명 합니다.

검사 목록 유사한 tooyour 기존 응용 프로그램 hello 프로토타입에 대 한를 만듭니다. Benchmarking 도구를 사용 하 여 hello 작업 부하를 시뮬레이트할 수 있으며 hello 프로토타입 응용 프로그램의 성능을 측정할 수도 있습니다. Hello 섹션을 참조 하십시오 [Benchmarking](#benchmarking) toolearn 더 합니다. 이렇게 하여 프리미엄 저장소가 응용 프로그램 성능 요구 사항에 일치하거나 능가할 수 있는지 여부를 결정할 수 있습니다. 구현할 수 있습니다 다음 프로덕션 응용 프로그램에 대 한 동일한 지침 hello 합니다.

### <a name="counters-toomeasure-application-performance-requirements"></a>카운터 toomeasure 응용 프로그램에 대 한 성능 요구 사항
응용 프로그램의 가장 좋은 방법은 toomeasure 성능 요구 hello, toouse 성능 모니터링 도구 hello 서버 hello 운영 체제에서 제공 됩니다. Windows용 PerfMon 및 Linux용 iostat를 사용할 수 있습니다. 이러한 도구는 해당 tooeach 측정값 hello 위의 섹션에서에서 설명 하는 카운터를 캡처합니다. 보통, 최고 및 업무 시간 이후 작업 부하의 응용 프로그램을 실행 하는 경우 이러한 카운터의 값 hello를 캡처해야 합니다.

hello PerfMon 카운터는 프로세서, 메모리, 각 논리 디스크 및 서버의 실제 디스크에 사용할 수 있습니다. 프리미엄 저장소 디스크는 VM으로 사용 하 여 각 프리미엄 저장소 디스크에 대 한 hello 물리적 디스크 카운터 되며 hello 프리미엄 저장소 디스크에 만들어진 각 볼륨에 대 한 논리 디스크 카운터는. 응용 프로그램 워크 로드를 호스트 하는 hello 디스크에 대 한 hello 값을 캡처해야 합니다. 논리적 및 물리적 디스크 간에 하나의 tooone 매핑을 이면 toophysical 디스크 카운터; 참조할 수 있습니다. 그렇지 않으면 toohello logical disk 카운터를 참조 하십시오. Linux에서 hello iostat 명령은 CPU 및 디스크 사용률 보고서를 생성합니다. hello 디스크 사용률 보고서는 물리적 장치 또는 파티션 통계를 제공합니다. 별도 디스크에 해당 데이터와 로그가 있는 데이터베이스 서버가 있는 경우 두 디스크에 대한 이 데이터를 수집합니다. 아래 표에서 디스크, 프로세서 및 메모리에 대한 카운터를 설명합니다.

| 카운터 | 설명 | PerfMon | Iostat |
| --- | --- | --- | --- |
| **초당 IOPS 또는 트랜잭션** |I/O 요청의 수 초당 toohello 저장소 디스크를 발급합니다. |디스크 읽기/초  <br> 디스크 쓰기/초 |tps  <br> r/s  <br> w/s |
| **디스크 읽기 및 쓰기** |% 읽기 및 쓰기 작업 hello 디스크에 수행 합니다. |% 디스크 읽기 시간  <br> % 디스크 쓰기 시간 |r/s  <br> w/s |
| **처리량** |읽거나 toohello 최대 초당 디스크에 쓴 데이터 양입니다. |디스크 읽기 바이트/초  <br> 디스크 쓰기 바이트/초 |kB_read/s <br> kB_wrtn/s |
| **대기 시간** |총 시간 toocomplete 디스크 IO 요청 수입니다. |평균 디스크 초/읽기  <br> 평균 디스크 초/쓰기 |await  <br> svctm |
| **IO 크기** |입/출력 요청 hello 크기 toohello 저장소 디스크를 발급합니다. |평균 디스크 바이트/읽기  <br> 평균 디스크 바이트/쓰기 |avgrq-sz |
| **큐 크기** |대기 중인 toobe 폼에 읽거나 쓸 toohello 저장소 디스크를 요청 하는 미해결 I/O 수입니다. |현재 디스크 큐 길이 |avgqu-sz |
| **최대 메모리** |원활 하 게 필요한 toorun 응용 프로그램 메모리의 양 |% 사용 중인 커밋된 바이트 |vmstat 사용 |
| **최대 CPU** |필요한 toorun 응용 프로그램이 원활 하 게 CPU 양 |% 프로세서 시간 |%util |

[iostat](http://linuxcommand.org/man_pages/iostat1.html) 및 [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx)에 대해 자세히 알아봅니다.

## <a name="optimizing-application-performance"></a>응용 프로그램 성능 최적화
프리미엄 저장소에서 실행 중인 응용 프로그램의 성능에 영향을 주는 hello 주요 요소는 특성의 IO 요청이, VM 크기, 디스크 크기, 디스크, 디스크 캐싱, 다중 스레딩 및 큐 깊이 수 있습니다. 노브 hello 시스템에서 제공 된 일부의이 요소를 제어할 수 있습니다. 대부분의 응용 프로그램 올바르게 있습니다 옵션 tooalter hello IO 크기와 큐 깊이 직접 합니다. 예를 들어 SQL Server를 사용 하는 경우 hello IO 크기와 큐 깊이 선택할 수 없습니다. SQL Server는 대부분의 성능 hello 최적의 IO 크기와 큐 깊이 값 tooget hello를 선택합니다. 적절 한 리소스가 toomeet 성능 요구를 프로 비전 할 수 있도록 것이 중요 한 toounderstand hello에 미치는 영향 요인 두 가지 유형의 응용 프로그램 성능 합니다.

이 단원 전반의 toohello 응용 프로그램 요구 사항 검사 목록 만든 tooidentify 참조 toooptimize를 필요한 얼마나 응용 프로그램 성능을 합니다. 에 따라 수 toodetermine 됩니다, tootune가 필요 합니다를 놓은이 섹션에서 있습니다. toowitness hello 각 요인의 성능에 미치는 영향 프로그램 응용 프로그램을 실행 응용 프로그램 설치에 대 한 도구, 즉 벤치마킹 합니다. Toohello 참조 [Benchmarking](#Benchmarking) hello Windows 및 Linux Vm에 도구, 즉 벤치마킹 일반적인 단계 toorun에 대 한이 문서의 뒷부분에 나오는 섹션.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>한 눈에 IOPS, 처리량 및 대기 시간 최적화
모든 성능 요소 hello 및 hello 단계 toooptimize IOPS, 처리량 및 대기 시간 hello 테이블 아래에 요약 되어 있습니다. hello이 요약 다음 섹션에서는 설명 각 요소에는 훨씬 더 깊이입니다.

| &nbsp; | **IOPS** | **처리량** | **대기 시간** |
| --- | --- | --- | --- |
| **예제 시나리오** |초당 비율로 매우 높은 트랜잭션이 필요한 엔터프라이즈 OLTP 응용 프로그램입니다. |다량의 데이터를 처리하는 엔터프라이즈 데이터 웨어하우징 응용 프로그램입니다. |거의 실시간 응용 프로그램을 온라인 게임 등 인스턴트 응답 toouser 요청을 요구 합니다. |
| 성능 요인 | &nbsp; | &nbsp; | &nbsp; |
| **IO 크기** |작은 크기의 IO는 더 높은 IOPS를 생성합니다. |더 큰 IO 크기 tooyields 처리량을 더 합니다. | &nbsp;|
| **VM 크기** |응용 프로그램 요구 사항보다 큰 IOPS를 제공하는 VM 크기를 사용합니다. VM 크기 및 IOPS 한계는 여기를 참조하세요. |응용 프로그램 요구 사항보다 큰 처리량 한계가 있는 VM 크기를 사용합니다. VM 크기 및 처리량 한계는 여기를 참조하세요. |응용 프로그램 요구 사항보다 큰 규모 제한을 제공하는 VM 크기를 사용합니다. VM 크기 및 한계는 여기를 참조하세요. |
| **디스크 크기** |응용 프로그램 요구 사항보다 큰 IOPS를 제공하는 디스크 크기를 사용합니다. 디스크 크기 및 IOPS 한계는 여기를 참조하세요. |응용 프로그램 요구 사항보다 큰 처리량 한계가 있는 디스크 크기를 사용합니다. 디스크 크기 및 처리량 한계는 여기를 참조하세요. |응용 프로그램 요구 사항보다 큰 규모 제한을 제공하는 디스크 크기를 사용합니다. 디스크 크기 및 한계는 여기를 참조하세요. |
| **VM 및 디스크 규모 제한** |IOPS 제한은 hello VM 크기 선택의 프리미엄 저장소 디스크에 의해 발생 하는 총 IOPS tooit 연결 보다 커야 합니다. |hello VM 크기가 선택한 처리량 한도 프리미엄 저장소 디스크에 의해 발생 하는 총 처리량 tooit 연결 된 이후 여야 합니다. |Hello VM 크기 선택의 규모 제한을 연결 된 프리미엄 저장소 디스크의 총 배율 제한 값 보다 커야 합니다. |
| **디스크 캐싱** |읽기 리소스 사용량이 많은 작업 tooget 있는 프리미엄 저장소 디스크에서 읽기 전용 캐시를 사용 합니다. 더 높은 읽기 IOPS입니다. | &nbsp; |준비 리소스 사용량이 많은 작업 tooget 매우 낮은 읽기 대기 시간이 프리미엄 저장소 디스크에서 읽기 전용 캐시를 사용 하도록 설정 합니다. |
| **디스크 스트라이프** |여러 디스크를 사용 하 고 함께 tooget 결합 된 더 높은 IOPS 및 처리량 한도 스트라이프 합니다. VM 당 결합 된 제한 hello는 hello 연결 된 프리미엄 디스크의 결합 된 한계 보다 높아야 합니다. | &nbsp; | &nbsp; |
| **스트라이프 크기** |OLTP 응용 프로그램에 표시된 작은 임의 IO 패턴에 대한 더 작은 스트라이프 크기입니다. 예: SQL Server OLTP 응용 프로그램에 대해 64KB의 스트라이프 크기를 사용합니다. |데이터 웨어하우스에 응용 프로그램에 표시된 대형 순차 IO 패턴에 대한 더 큰 스트라이프 크기입니다. 예: SQL Server 데이터 웨어하우스 응용 프로그램에 대해 256KB의 스트라이프 크기를 사용합니다. | &nbsp; |
| **멀티 스레드** |다중 스레딩 toopush 수가 높을수록 요청 tooPremium toohigher IOPS 밝혀 저장소 및 처리량을 사용 합니다. 예를 들어 SQL Server에 설정 높은 MAXDOP 값 tooallocate 더 많은 Cpu tooSQL 서버. | &nbsp; | &nbsp; |
| **큐 크기** |더 큰 큐 크기는 더 높은 IOPS를 생성합니다. |더 큰 큐 크기는 더 높은 처리량을 생성합니다. |더 작은 큐 크기는 더 짧은 대기 시간을 생성합니다. |

## <a name="nature-of-io-requests"></a>IO 요청의 특성
IO 요청은 응용 프로그램에서 수행하는 입력/출력 작업의 단위입니다. 난수 또는 순차적, I/O 요청이의 hello 특성을 식별을 읽거나 쓰기 파일 그룹, 소형 또는 대형, 응용 프로그램의 hello 성능 요구 사항을 결정 하는 데 도움이 됩니다. 것은 매우 중요 한 toounderstand hello 특성 toomake hello 올바른 결정 응용 프로그램 인프라를 디자인할 때 IO 요청의 합니다.

IO 크기가 더 중요 한 요인 hello 중 하나입니다. hello IO 크기는 응용 프로그램에 의해 생성 된 hello 입/출력 작업 요청의 hello 크기입니다. hello IO 크기 hello IOPS에 특히는 성능에 상당한 영향 되며 응용 프로그램 hello 대역폭 tooachieve 수 있습니다. hello 수식인 관계를 보여 줍니다 hello IOPS, IO 크기와 대역폭/처리량입니다.  
    ![](media/storage-premium-storage-performance/image1.png)

일부 응용 프로그램을 사용 하면 일부 응용 프로그램 하지 않는 동안 자신의 IO 크기 tooalter 있습니다. SQL Server 자체 hello 최적의 IO 크기를 결정 하 고 모든 노브 toochange와 사용자가 제공 하지 않습니다 예를 들어 것입니다. 다른 손 hello, 호출 매개 변수를 제공 하는 Oracle [DB\_차단\_크기](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) hello 데이터베이스의 I/O 요청 크기 hello 구성할 수 있는 사용 합니다.

응용 프로그램 있습니다 toochange hello IO 크기를 허용 하지 않는 사용 하는 경우이 문서 toooptimize hello 성능이 가장 관련성이 높은 tooyour 응용 프로그램이 KPI hello 지침을 따르세요. 예를 들면 다음과 같습니다.

* OLTP 응용 프로그램에서는 수백만 개의 작고 임의적인 IO 요청을 생성합니다. 응용 프로그램 인프라 tooget 디자인 해야 이러한 IO 유형의 toohandle 요청, 높은 IOPS입니다.  
* 데이터 웨어하우징 응용 프로그램은 크고 순차적인 IO 요청을 생성합니다. IO 요청의 입력 이러한 toohandle, 응용 프로그램 인프라 tooget 더 높은 대역폭이 또는 처리량을 디자인 해야 합니다.

Toochange hello IO 크기를 허용 하는 응용 프로그램을 사용 하는 경우 hello IO 크기 또한 tooother 성능 지침에 대 한 가장이 사용

* 작은 IO 크기 tooget 더 높은 IOPS입니다. 예를 들어 OLTP 응용 프로그램의 경우 8KB입니다.  
* 더 큰 IO 크기 tooget 대역폭/처리량을 더 합니다. 예를 들어 데이터 웨어하우스 응용 프로그램의 경우 1024KB입니다.

응용 프로그램에 대 한 hello IOPS 및 처리량/대역폭을 계산 하는 방법은에 예가입니다. P30 디스크를 사용하여 응용 프로그램을 고려합니다. hello 최대 IOPS 및 처리량/대역폭 P30 디스크 ä à ï 5,000 IOPS 및 200MB 초당 각각입니다. 이제 응용 프로그램에 필요한 hello P30 디스크에서 최대 IOPS 사용 하 여 더 작은 IO 크기 8KB를 같은 hello 됩니다 대역폭으로 인해 발생 하는 hello 수 tooget 40MB / 초입니다. 그러나 응용 프로그램 P30 디스크에서 최대 처리량/대역폭 hello 및 1024KB와 같은 더 큰 IO 크기를 사용 하면 필요한 경우 hello 결과 IOPS 됩니다, 200 IOPS입니다. 따라서 두 응용 프로그램의 IOPS 및 처리량/대역폭 요구 사항이 충족 되도록 hello IO 크기를 조정 합니다. 다음 표에서 P30 디스크에 대 한 hello 다른 IO 크기 및 해당 IOPS 및 처리량을 요약합니다.

| 응용 프로그램 요구 사항 | I/O 크기 | IOPS | 처리량/대역폭 |
| --- | --- | --- | --- |
| 최대 IOPS |8KB |5, 000 |초당 40MB |
| 최대 처리량 |1024KB |200 |초당 200MB |
| 최대 처리량 + 높은 IOPS |64KB |3,200 |초당 200MB |
| 최대 IOPS + 높은 처리량 |32KB |5, 000 |초당 160MB |

tooget IOPS 및 대역폭 hello 단일 프리미엄 저장소 디스크의 최 댓 값 보다 더 높은 함께 스트라이프된 여러 프리미엄 디스크를 사용 합니다. 예를 들어 스트라이프 두 P30 디스크 tooget는 결합 된 IOPS의 10000 IOPS 또는 400MB의 결합 된 처리량 초당 합니다. Hello 다음 섹션에서 설명 했 듯이 결합 hello 디스크 IOPS 및 처리량 지 원하는 VM 크기를 사용 해야 합니다.

> [!NOTE]
> 어느 IOPS 늘리거나 다른 처리량 hello 또한 증가 하는 대로 클릭 하지 않으면 처리량 또는 hello 디스크나 VM의 IOPS 제한 중 하나를 늘릴 때 있는지 확인 합니다.
>
>

toowitness hello IO 크기 응용 프로그램 성능에 미치는 영향, VM 및 디스크에서 벤치마킹 도구를 실행할 수 있습니다. 여러 개의 테스트 실행을 만들고 각 실행된 toosee hello 영향에 대 한 다른 IO 크기를 사용 합니다. Toohello 참조 [Benchmarking](#Benchmarking) hello에 대 한 자세한 내용은이 문서의 뒷부분에 나오는 섹션.

## <a name="high-scale-vm-sizes"></a>높은 확장성의 VM 크기
응용 프로그램 디자인을 시작할 때 hello 첫 번째 작업 toodo 중 하나 이면 VM toohost 응용 프로그램을 선택 합니다. 프리미엄 저장소는 높은 계산 능력 및 높은 로컬 디스크 I/O 성능이 필요한 응용 프로그램을 실행할 수 있는 높은 확장성의 VM 크기와 함께 제공됩니다. 이러한 Vm hello 로컬 디스크에 대 한 빠른 프로세서, 더 높은 메모리 대 코어 비율, 및는 Solid-State 드라이브 (SSD)를 제공합니다. 프리미엄 저장소를 지 원하는 높은 눈금 Vm의 예로 hello DS, DSv2 및 GS 시리즈 Vm입니다.

높은 확장성의 VM은 다양한 수의 CPU 코어, 메모리, OS 및 임시 디스크 크기와 함께 다양한 크기에서 사용할 수 있습니다. 각 VM 크기 또한 개수가 최대 데이터 디스크를 VM toohello를 연결할 수 있습니다. 따라서 hello 선택한 VM 크기는 처리, 메모리 및 저장소 용량의 양과 응용 프로그램에 사용할 수 있는 적용 됩니다. 또한 hello 계산 및 저장소 비용 영향을 줍니다. 예를 들어 다음은 가장 큰 VM 크기 DS 시리즈, DSv2 시리즈 및 GS 시리즈의 hello hello 사양:

| VM 크기 | CPU 코어 | 메모리 | VM 디스크 크기 | 최대 데이터 디스크 | 캐시 크기 | IOPS | 대역폭 캐시 IO 제한 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112GB |OS = 1023GB  <br> 로컬 SSD = 224GB |32 |576GB |50,000 IOPS  <br> 초당 512MB |4,000 IOPS 및 초당 33MB |
| Standard_GS5 |32 |448GB |OS = 1023GB  <br> 로컬 SSD = 896GB |64 |4224GB |80,000 IOPS  <br> 초당 2,000MB |5,000 IOPS 및 초당 50MB |

사용 가능한 모든 Azure VM 크기의 전체 목록은 tooview 너무 참조[Windows VM 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 또는 [Linux VM 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 충족 하 고 원하는 tooyour 응용 프로그램에 대 한 성능 요구 사항을 확장할 수 있는 VM 크기를 선택 합니다. 또한 toothis, VM 크기를 선택할 때 고려해 야 할 다음을 고려해.

*규모 제한*  
hello 최대 IOPS 제한 및 디스크 VM 당이 다르고 서로 독립적입니다. hello 응용 프로그램 제어 IOPS로 hello VM hello 프리미엄 디스크에 대 한 연결 된 tooit hello 제한 내에 있는지 확인 합니다. 그렇지 않은 경우 응용 프로그램 성능에 제한이 발생합니다.

한 예로 응용 프로그램 요구 사항이 최대 4,000 IOPS라 가정합니다. tooachieve P30 디스크 DS1 VM에 구축 하이 합니다. hello P30 디스크 too5, 000 IOPS 제공할 수 있습니다. 그러나 hello DS1 VM 제한 too3, 200 IOPS입니다. 따라서 3,200 iops hello VM 제한 hello 응용 프로그램의 성능을 제한지 것입니다 하 고 성능이 저하 됩니다. tooprevent이이 경우 VM을 선택 하 고 디스크 요구 사항을 모두 충족 응용 프로그램은 크기.

*작업 비용*  
대부분의 경우에서 프리미엄 저장소를 사용하는 작업의 전체 비용은 표준 저장소를 사용하는 비용보다 낮을 수 있습니다.

예를 들어 16,000 IOPS를 필요로 하는 응용 프로그램을 가정합니다. tooachieve이이 성능 표준 해야\_D14 Azure IaaS VM의 16,000 32 개의 표준 저장소 1TB 디스크를 사용 하 여 최대 IOPS 수 있는 합니다. 각 1TB 표준 저장소 디스크는 최대 500 IOPS를 달성할 수 있습니다. hello 예상 비용 한 달이이 VM의 $1,570 됩니다. 32 개의 표준 저장소 디스크 월별 비용이 hello $1,638 됩니다. hello 예상 월간 총 비용 $3,208 됩니다.

그러나 호스트 된 경우 hello 동일 프리미엄 저장소에 응용 프로그램을 및 필요 합니다. 더 작은 VM 크기를 더 적은 프리미엄 저장소 디스크 hello 전반적인 비용을 줄입니다. 표준\_DS13 VM 4 개 P30 디스크를 사용 하 여 hello 16,000 IOPS 요구를 충족할 수 있습니다. hello DS13 VM 25,600의 최대 IOPS 많고 P30 디스크당 5000 최대 IOPS입니다. 전체적으로 이 구성은 5,000 x 4 = 20,000 IOPS를 달성할 수 있습니다. hello 예상 비용 한 달이이 VM의 $1,003 됩니다. 4 개의 P30 프리미엄 저장소 디스크의 월별 비용이 hello $544.34 됩니다. hello 예상 월간 총 비용 $1,544 됩니다.

다음 표에서 표준 및 프리미엄 저장소에 대 한이 시나리오의 hello 비용 분석 결과 요약합니다.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **월별 VM 비용** |$1,570.58(Standard\_D14) |$1,003.66(Standard\_DS13) |
| **월별 디스크 비용** |$1,638.40(32 x 1 TB 디스크) |$544.34(4 x P30 디스크) |
| **월별 전체 비용** |$3,208.98 |$1,544.34 |

*Linux 배포판*  

얻게 hello Azure 프리미엄 저장소와 동일한 수준의 성능 Windows 및 Linux를 실행 하는 Vm에 대 한 합니다. 여러 버전의 Linux 배포판을 지원 하 고 hello 전체 목록을 볼 수 있습니다 [여기](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 다른 유형의 작업에 대해 적합 한 다른 배포판은 더 나은 toonote 유용 합니다. 서로 다른 수준의 hello distro에서 실행 중인 작업에 따라 성능이 표시 됩니다. 응용 프로그램과 함께 hello Linux 배포판을 테스트 하 고 hello 가장 잘 작동 하는 하나를 선택 합니다.

프리미엄 저장소로 Linux를 실행 하는 경우 hello tooensure 높은 성능이 필요한 드라이버에 대 한 최신 업데이트를 확인 합니다.

## <a name="premium-storage-disk-sizes"></a>프리미엄 저장소 디스크 크기
Azure Premium Storage는 현재 일곱 가지 디스크 크기를 제공합니다. 각 디스크 크기는 IOPS, 대역폭 및 저장소에 대한 다른 규모 한도를 가집니다. Hello hello 응용 프로그램 요구 사항 및 hello 대규모 VM 크기에 따라 올바른 프리미엄 저장소 디스크 크기를 선택 합니다. hello 표에서 hello 7 개 디스크 크기와 기능을 보여 줍니다. P4 및 P6 크기는 현재 Managed Disks에 대해서만 지원됩니다.

| 프리미엄 디스크 유형  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| 디스크 크기           | 32GB | 64GB | 128GB| 512GB            | 1,024GB(1TB)    | 2,048GB(2TB)    | 4,095GB(4TB)    | 
| 디스크당 IOPS       | 120   | 240   | 500   | 2,300              | 5,000              | 7,500              | 7,500              | 
| 디스크당 처리량 | 초당 25MB  | 초당 50MB  | 초당 100MB | 초당 150MB | 초당 200MB | 초당 250MB | 초당 250MB | 


Hello 디스크에 따라 선택 하는 디스크 수에 선택한 크기입니다. 사용자 응용 프로그램 요구 사항이 단일 P50 디스크 또는 여러 P10 디스크 toomeet 사용할 수 있습니다. 계정 고려 사항 hello 선택 하는 경우 아래에 나열 된 고려 합니다.

*규모 제한(IOPS 및 처리량)*  
각 프리미엄 디스크 크기의 hello IOPS 및 처리량 제한은 서로 다른 독립적 hello VM 규모 조정 한도에서입니다. Hello 디스크에서 처리량의 hello 확장 제한 내에서 선택 된 VM 크기 및 총 IOPS hello를 확인 합니다.

예를 들어 응용 프로그램 요구 사항이 최대 250MB/초의 처리량이고 단일 P30 디스크와 함께 DS4 VM을 사용하는 경우를 가정합니다. hello DS4 VM too256 m B/초의 처리량을 제공할 수 있습니다. 그러나 단일 P30 디스크의 처리량 제한은 200 m B/초입니다. 따라서 200MB/sec toohello 디스크 제한 때문에 hello 응용 프로그램에 제한이 적용 됩니다. tooovercome이 한이도 둘 이상의 데이터 디스크 toohello VM을 프로 비전 하거나 디스크 tooP40 또는 P50 크기를 조정 합니다.

> [!NOTE]
> Hello 캐시에서 제공 하는 읽기 hello 디스크 IOPS 및 처리량에 포함 되지 않은, 따라서 toodisk 제한 대상이 아닙니다. 캐시에는 VM당 별도 IOPS 및 처리량 제한이 있습니다.
>
> 예를 들어 처음에 읽기 및 쓰기는 각각 60MB/초 및 40MB/초입니다. 시간이 지남에 따라 hello 캐시 warms 하 고 hello 캐시에서 점점 더 많은 hello 읽기를 서비스 합니다. 그런 다음 hello 디스크에서 높은 쓰기 처리량을 얻을 수 있습니다.
>
>

*디스크 수*  
응용 프로그램 요구 사항을 평가 하 여 해야 하는 디스크 hello 수를 결정 합니다. 각 VM 크기에 hello toohello VM를 연결할 수 있는 디스크 수에는 제한이 있습니다. 일반적으로 코어 수를 두 번 hello입니다. 해당 hello hello 필요한 디스크 수를 지원할 수를 선택 하는 VM 크기를 확인 합니다.

Hello 프리미엄 저장소 디스크는 더 높은 성능 비교 기능 tooStandard 저장소 디스크를 기억 합니다. 따라서 표준 저장소 tooPremium 저장소를 사용 하 여 Azure IaaS VM에서 응용 프로그램을 마이그레이션하려는 경우 하면 더 적은 프리미엄 디스크 tooachieve hello 응용 프로그램에 대해 동일 하거나 더 높은 성능입니다.

## <a name="disk-caching"></a>디스크 캐싱
Azure 프리미엄 저장소를 활용하는 높은 확장성의 VM에는 BlobCache 라는 다중 계층 캐싱 기술이 있습니다. BlobCache 캐싱에 대 한 가상 컴퓨터 RAM hello 및 로컬 SSD의 조합을 사용합니다. 이 캐시는 hello 프리미엄 저장소 영구 디스크 및 hello VM 로컬 디스크에 사용할 수 있습니다. 기본적으로이 캐시 설정은 tooRead/운영 체제 디스크에 대 한 쓰기 및 읽기 전용 데이터 디스크를 프리미엄 저장소에서 호스트에 대 한 설정 됩니다. 디스크 캐싱을 hello 프리미엄 저장소 디스크에 사용 hello 대규모 Vm hello 기본 디스크 성능을 초과 하는 매우 높은 수준의 성능 달성할 수 있습니다.

> [!WARNING]
> Azure 디스크의 hello 캐시 설정을 변경를 분리 한 다시 hello 대상 디스크를 연결 합니다. Hello 운영 체제 디스크 이면 hello VM 다시 시작 됩니다. Hello 디스크 캐시 설정을 변경 하기 전에이 중단의 영향을 받을 수 있는 모든 응용 프로그램/서비스를 중지 합니다.
>
>

BlobCache 작동 방식에 대해 자세히 toolearn 참조 내 toohello [Azure 프리미엄 저장소](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) 블로그 게시물입니다.

이 hello 오른쪽 디스크 세트에 중요 한 tooenable 캐시입니다. 프리미엄 디스크에 디스크 캐시를 사용 해야 하거나 하지에 따라 달라 집니다 hello 작업 패턴 해당 디스크를 처리 합니다. 다음 표에서 hello 기본 OS 및 데이터 디스크에 대 한 캐시 설정을 보여줍니다.

| **디스크 유형** | **기본 캐시 설정** |
| --- | --- |
| OS 디스크 |ReadWrite |
| 데이터 디스크  |없음 |

다음에 데이터 디스크에 대 한 권장 되는 디스크 캐시 설정을 hello 됩니다.

| **디스크 캐싱 설정** | **경우에 권장 구성을 toouse이이 설정은** |
| --- | --- |
| 없음 |쓰기 전용 및 쓰기가 많은 디스크에 대해 None으로 호스트-캐시를 구성합니다. |
| ReadOnly |읽기 전용 및 읽기-쓰기 디스크에 대해 ReadOnly로 호스트-캐시를 구성합니다. |
| ReadWrite |응용 프로그램 작성 적절히 처리 하는 경우에 / 쓰기 데이터 toopersistent 디스크 필요할 때 캐시 된 대로 호스트 캐시를 구성 합니다. |

*ReadOnly*  
프리미엄 저장소 데이터 디스크에 ReadOnly 캐싱을 구성하여 짧은 읽기 대기 시간을 달성하고 응용 프로그램에 대한 매우 높은 읽기 IOPS 및 처리량을 얻을 수 있습니다. 다음 두 가지 이유로 인한 것입니다.

1. 읽기는 hello VM 메모리 및 로컬 SSD에 있는 캐시에서 수행, hello Azure blob 저장소에 있는 hello 데이터 디스크에서 읽기 보다 훨씬 빠릅니다.  
2. 프리미엄 저장소에서 읽기 쪽 hello 디스크 IOPS 및 처리량으로 캐시에서 제공 하는 hello를 계산 하지 않습니다. 따라서 응용 프로그램은 더 높은 수 tooachieve 전체 IOPS 및 처리량입니다.

*ReadWrite*  
기본적으로 hello OS 디스크/쓰기 캐싱이 설정 되어 있습니다. 최근에 데이터 디스크에 ReadWrite 캐싱에 대한 지원을 추가했습니다. ReadWrite caching을 사용 하는 경우에 적절 한 방법은 toowrite hello 디스크 데이터를 캐시 toopersistent 있어야 합니다. 예를 들어 SQL Server 핸들 작성 자체적으로 데이터 toohello 영구 저장소 디스크 캐시. 지속 hello를 처리 하지 않는 응용 프로그램 으로/쓰기 캐시를 사용 하 여 필요한 데이터 toodata 손실 될 수 있습니다 hello VM가 충돌 하는 경우.

예를 들어, 이러한 지침 tooSQL 서버를 적용할 수 있습니다 hello 다음을 수행 하 여 프리미엄 저장소에서 실행 중인

1. 데이터 파일을 호스트하는 Premium Storage 디스크에 “ReadOnly” 캐시를 구성합니다.  
   a.  데이터 페이지는 hello 데이터 디스크에서 캐시 비교 toodirectly hello에서에서 훨씬 빠르게 검색 한 이후 hello 빠른 캐시 낮은 hello SQL Server 쿼리 시간에서 읽습니다.  
   b.  캐시에서 읽기 제공은 프리미엄 데이터 디스크에서 사용할 수 있는 추가 처리량이 있음을 의미합니다. SQL Server는 이 추가 처리량을 사용하여 더 많은 데이터 페이지와 백업/복원, 배치 처리 및 인덱스 다시 빌드와 같은 다른 작업을 검색할 수 있습니다.  
2. "None" 구성 호스팅 hello 로그 파일 디스크를 프리미엄 저장소에 캐시 합니다.  
   a.  로그 파일은 주로 많은 쓰기 작업을 가집니다. 따라서은 유용 하지 않습니다 hello 읽기 전용 캐시에서.

## <a name="disk-striping"></a>디스크 스트라이프
대규모 VM 여러 프리미엄 저장소 영구 디스크, hello 디스크와 연결 된 작업을 수 함께 스트라이프된 tooaggregate 자신의 IOPs, 대역폭 및 저장소 용량입니다.

Windows에서는 저장소 공간 toostripe 디스크를 함께 사용할 수 있습니다. 풀에서 각 디스크마다 하나의 열을 구성해야 합니다. 그렇지 않으면 hello 스트라이프 볼륨의 전반적인 성능 수 hello 디스크에 걸쳐 트래픽의 toouneven 배포 인해 예상 보다 더 낮은 합니다.

중요: 서버 관리자 UI를 사용 하 hello 스트라이프 볼륨에 대 한 too8 열의 총 수를 설정할 수 있습니다. 8 개 이상의 디스크를 연결 하는 경우 PowerShell toocreate hello 볼륨을 사용 합니다. PowerShell을 사용 하 설정할 수 있습니다. 있습니다 hello 열 수가 동일 toohello 디스크 수 있습니다. 예를 들어, 16 개의 디스크 단일 스트라이프 세트;에 있는 경우 hello에 16 개의 열을 지정 *NumberOfColumns* hello의 매개 변수 *New-virtualdisk* PowerShell cmdlet.

Linux에서 hello MDADM 유틸리티 toostripe 디스크를 함께 사용 합니다. 에 대 한 스트라이프 디스크 Linux에 관련 된 자세한 단계는 너무 참조[Linux에서 소프트웨어 RAID 구성](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.

*스트라이프 크기*  
중요 한 구성에서 디스크 스트라이프는 hello 스트라이프 크기입니다. hello 스트라이프 크기 또는 블록 크기는 응용 프로그램 스트라이프 볼륨에 해결할 수 있는 데이터의 가장 작은 청크 hello 합니다. 구성한 hello 스트라이프 크기의 응용 프로그램 및 해당 요청 패턴 hello 유형에 따라 다릅니다. Hello 잘못 스트라이프 크기를 선택 하면 응용 프로그램의 성능을 toodegraded 본질적 tooIO 잘못 맞춤을 발생할 수 있습니다.

예를 들어 응용 프로그램에서 생성 하는 IO 요청 hello 디스크 스트라이프 크기 보다 큰 경우 hello 저장소 시스템이 씁니다 stripe 간에 단위 경계 둘 이상의 디스크에 있습니다. 해당 데이터 tooaccess 시간는 것을 하는 경우 둘 이상의 stripe 단위 toocomplete hello 요청 간에 tooseek은입니다. 이러한 동작의 hello 누적 된 효과가 toosubstantial 성능 저하를 발생할 수 있습니다. Hello에 hello IO 요청 크기 스트라이프 크기 보다 작으면 고 본질적으로 무작위 경우 hello I/O 요청이 추가할 수 있습니다 hello에 동일한 경우 디스크 병목 현상이 발생 하 고 궁극적으로 hello IO 성능을 저하 시키는 합니다.

응용 프로그램을 실행 하는 워크 로드의 hello 형식에 따라 적절 한 스트라이프 크기를 선택 합니다. 작은 임의 IO 요청의 경우 더 작은 스트라이프 크기를 사용합니다. 반면 큰 순차 IO 요청의 경우 더 큰 스트라이프 크기를 사용합니다. 프리미엄 저장소에 실행 하려는 hello 응용 프로그램에 대 한 hello 스트라이프 크기 권장을 확인 합니다. SQL Server의 경우 OLTP 작업에 대해 64KB의 스트라이프 크기, 데이터 웨어하우징 작업에 대해 256KB의 스트라이프 크기를 구성합니다. 참조 [Azure Vm에서 SQL Server에 대 한 성능 모범 사례](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn 더 합니다.

> [!NOTE]
> DS 시리즈 VM에 최대 32개의 프리미엄 저장소 디스크를 GS 시리즈 VM에 64개의 프리미엄 저장소 디스크를 함께 스트라이프할 수 있습니다.
>
>

## <a name="multi-threading"></a>다중 스레드
Azure는 프리미엄 저장소 플랫폼 toobe 대규모 병렬 위해 디자인 되었습니다. 따라서 다중 스레드 응용 프로그램은 단일 스레드 응용 프로그램에 비해 훨씬 더 높은 성능을 얻을 수 있습니다. 여러 스레드에서 작업을 분할 하 고 VM hello 사용 하 여 해당 실행의 효율성 및 디스크 리소스 toohello 최대 증가 하는 다중 스레드 응용 프로그램.

예를 들어 응용 프로그램이 단일 코어 두 개의 스레드를 사용 하 여 VM에서 실행 되는 경우 hello CPU hello 스레드가 각각 두 tooachieve 효율성 간에 전환할 수 있습니다. 한 스레드가 디스크 IO toocomplete에서 대기 하는 동안 CPU hello 전환할 수 toohello 다른 스레드가 있습니다. 이러한 방식으로 두 스레드는 단일 스레드보다 더 많은 작업을 수행할 수 있습니다. Hello VM 한 개 이상의 코어에 있는 경우 문제가 각 코어에서 병렬 작업을 실행할 수는 실행 시간이 더 약화 됩니다.

단일 기본 제공 응용 프로그램을 구현 하는 수 toochange hello 방법은 필요가 없는 스레딩 또는 다중 스레딩을 사용 합니다. 예를 들어 SQL Server는 다중 CPU 및 다중 코어를 처리할 수 있습니다. 그러나 SQL Server 어떤 조건에서 하나 이상의 스레드 tooprocess 쿼리를 활용 것을 결정 합니다. 다중 스레드를 사용하여 쿼리를 실행하고 인덱스를 작성할 수 있습니다. 큰 테이블을 조인 하 고 toohello 사용자를 반환 하기 전에 데이터를 정렬 하는 쿼리에 대 한 SQL Server는 여러 스레드를 사용할 가능성이 많습니다. 그러나 사용자는 SQL Server에서 단일 스레드 또는 다중 스레드를 사용하여 쿼리를 실행할지 여부를 제어할 수 없습니다.

이 다중 스레딩을 사용 또는 병렬 tooinfluence를 변경할 수 구성 설정은 응용 프로그램의 처리 합니다. 예를 들어, SQL server hello 최대 Degree of Parallelism 구성입니다. MAXDOP를 호출 합니다.이 설정을 통해 tooconfigure hello 최대 프로세서 수가 병렬 처리 하는 경우 SQL Server를 사용할 수 있습니다. 개별 쿼리 또는 인덱스 작업에 대한 MAXDOP를 구성할 수 있습니다. 이 성능이 중요 한 응용 프로그램에 대 한 시스템의 toobalance 리소스를 원하는 유용 합니다.

예를 들어, SQL Server를 사용 하 여 응용 프로그램 큰 쿼리와 hello에서 인덱스 작업을 실행 중인 동시 합니다. 원하는 hello 인덱스 작업 toobe 자세한 비교는 고성능 toohello 큰 쿼리에서 가정해 보십시오. 이러한 경우 hello 인덱스 작업 toobe hello hello 쿼리에 대 한 MAXDOP 값 보다 높은의 MAXDOP 값을 설정할 수 있습니다. 이러한 방식으로 SQL Server에 더 많은 수의 hello 인덱스 비교 작업 toohello 프로세서 수가 전념할 수에 대 한 활용할 수 있는 프로세서 toohello 큰 쿼리 합니다. 기억 hello 각 작업에 대해 SQL Server에서 사용 하는 스레드 수를 제어 하지 않습니다. Hello에 대 한 전용 되는 프로세서의 최대 수를 제어할 수 있습니다 다중 스레딩을 사용 합니다.

SQL Server에 [병렬 처리의 정도](https://technet.microsoft.com/library/ms188611.aspx) 에 대한 자세한 정보가 있습니다. 확인 이러한 설정에 영향을 주는 응용 프로그램 및 구성 toooptimize 성능에 다중 스레딩을 사용 합니다.

## <a name="queue-depth"></a>큐 크기
큐 깊이 또는 큐 길이 hello 또는 큐 크기는 hello 시스템에서 보류 중인 IO 요청 수가 hello 합니다. 큐 깊이 hello 값 IO 작업의 수 응용 프로그램 정렬할 수 있는 hello 저장소 디스크 처리할를 결정 합니다. 모든 hello 세 개의 응용 프로그램 성능 지표를이 문서 viz. IOPS, 처리량 및 대기 시간에서에서 설명한 영향을 줍니다.

큐 크기 및 다중 스레딩은 밀접한 관련이 있습니다. 큐 깊이 값 hello 나타냅니다 다중 스레드는 hello 응용 프로그램에서 수행할 수 있습니다. Hello 큐 크기가 클 경우 응용 프로그램 더 많은 작업이 동시에 실행할 수, 즉, 더 다중 스레딩을 사용 합니다. 큐 깊이 hello 작으면 다중 스레드 응용 프로그램은 경우에, 동시 실행에 대 한 정렬 되도록 충분 한 요청 않아도 됩니다.

일반적으로 hello 오프 선반 응용 프로그램 수 없습니다. toochange hello 큐 깊이 때문에 경우 올바르게 않습니다 하지 유익한 것 설정 합니다. 응용 프로그램의 큐 깊이 tooget hello 최적의 성능 hello 오른쪽 값을 설정 합니다. 그러나 것은 중요 한 toounderstand이이 개념 응용 프로그램과 함께 성능 문제를 해결할 수 있도록 합니다. 또한 시스템에서 벤치마킹 도구를 실행 하 여 큐 깊이의 hello 효과 확인할 수 있습니다.

일부 응용 프로그램 설정을 tooinfluence hello 큐 깊이 제공합니다. 예를 들어 hello MAXDOP (최대 병렬 처리 수준) 설정을 SQL Server의 이전 섹션에서 설명합니다. MAXDOP 방법을 tooinfluence 큐 깊이 다중 스레드 및 SQL Server의 hello 큐 깊이 값을 직접 변경 하지 않지만 합니다.

*높은 큐 크기*  
높은 큐 깊이 hello 디스크에는 다양 한 작업 정렬 됩니다. hello 디스크 hello 미리 큐에 다음 요청을 알고 있습니다. 따라서 hello 디스크 미리 작업을 예약 하 고 최적의 순서에서 처리할 수 있습니다. Hello 응용 프로그램에서 더 많은 요청 toohello 디스크를 보내고, 이후 hello 디스크에 더 많은 병렬 IOs 처리할 수 있습니다. Hello 응용 프로그램 수 tooachieve 됩니다 궁극적으로, 높은 IOPS입니다. 응용 프로그램이 더 많은 요청을 처리 하 고, 이후 hello hello 응용 프로그램의 총 처리량도 증가 합니다.

일반적으로 응용 프로그램에서 연결된 디스크당 8-16+ 미해결 IO로 최대 처리량을 달성할 수 있습니다. 큐 깊이 하나 경우 응용 프로그램은 충분 한 IOs toohello 시스템 푸시 하지 못하는 하 고 지정 된 기간 동안에서 적은 양의 처리 합니다. 즉, 적은 처리량입니다.

예를 들어 SQL Server의 설정을 hello MAXDOP 값 쿼리에 대 한 너무 "4" toofour 코어 tooexecute hello 쿼리를 사용할 수 있는 SQL Server에 알립니다. SQL Server 수는 얼마 입니까 최적의 큐 깊이 값과 hello hello 쿼리 실행에 대 한 코어를 결정 합니다.

*최적의 큐 크기*  
매우 높은 큐 크기 값 또한 단점이 있습니다. Hello 응용 프로그램에서 toodrive 시도 큐 깊이 값이 너무 높으면 매우 높은 IOPS입니다. 응용 프로그램에 프로비전된 충분한 IOPS의 영구 디스크가 있지 않는 한 응용 프로그램 대기 시간이 늘어날 수 있습니다. 다음 수식을 IOPS, 대기 시간 및 큐 깊이 hello 관계를 보여 줍니다.  
    ![](media/storage-premium-storage-performance/image6.png)

큐 깊이 tooany 높은 값과 동일 하지만 대기 시간이 영향을 주지 않고 hello 응용 프로그램에 대 한 충분 한 IOPS를 배달할 수는 tooan 최적 값으로 구성 해야 합니다. 예를 들어 hello 응용 프로그램 대기 시간 요구 toobe 1 밀리초, hello 큐 깊이 tooachieve 5,000 IOPS는 QD 필요한 = 5000 x 0.001 = 5.

*스트라이프 볼륨에 대한 큐 크기*  
그러한 충분한 큐 크기를 유지하는 스트라이프 볼륨의 경우 모든 디스크는 개별적으로 최대 큐 크기를 가집니다. 예를 들어 2 개 큐 깊이 푸시하는 응용 프로그램 및 hello stripe 된 4 개의 디스크가 있습니다. hello 두 I/O 요청이 tootwo 디스크 되 고 나머지 두 개 이상의 디스크 유휴 상태가 됩니다. 따라서 구성할 hello 큐 깊이 hello 디스크를 모두 사용 될 수 있습니다. 아래 수식을 toodetermine 스트라이프 볼륨 큐 깊이 hello 하는 방법을 보여 줍니다.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>제한
Azure 프리미엄 저장소 프로 비전 hello VM 크기와 선택한 디스크 크기에 따라 처리량 및 IOPS 수를 지정 합니다. 응용 프로그램이 어떤 hello VM 또는 디스크를 처리할 수의이 제한 보다 높게 toodrive IOPS 또는 처리량을 시도 하면, 언제 든 지 것 프리미엄 저장소 조절 됩니다. 이 응용 프로그램에서 성능 저하의 hello 형태로 나타납니다. 이는 더 높은 대기 시간, 더 낮은 처리량 또는 더 낮은 IOPS를 의미할 수 있습니다. 프리미엄 저장소가 제한하지 않는 경우 응용 프로그램은 리소스가 달성할 수 있는 한도를 초과하여 완전히 실패할 수 있습니다. 따라서 tooavoid 성능 문제 due toothrottling, 응용 프로그램에 대 한 충분 한 리소스가 프로 비전 항상 합니다. Hello VM 크기 및 디스크 크기 위의 섹션에서 설명한 고려 고려 합니다. 가장 좋은 방법은 toofigure hello은 벤치마킹 어떤 리소스를 해야 toohost 응용 프로그램입니다.

## <a name="benchmarking"></a>벤치마킹
벤치 마크는 응용 프로그램에 다양 한 작업 부하를 시뮬레이션 하 고 각 작업에 대 한 hello 응용 프로그램 성능을 측정의 hello 프로세스입니다. 이전 섹션에서 설명 하는 hello 단계를 사용 하 여 수집한 hello 응용 프로그램에 대 한 성능 요구 사항입니다. Hello 응용 프로그램을 호스트 하는 hello Vm에 도구, 즉 벤치마킹를 실행 하 여 응용 프로그램 프리미엄 저장소를 얻을 수 있는 hello 성능 수준을 결정할 수 있습니다. 이 섹션에서는 Azure 프리미엄 저장소 디스크로 프로비전된 Standard DS14 VM 벤치마킹의 예를 제공합니다.

Windows 및 Linux용으로 각각 일반 벤치마킹 도구 Iometer 및 FIO를 사용했습니다. 이러한 도구는 여러 스레드를 프로덕션과 유사한 작업 및 hello 시스템 성능을 측정 시뮬레이션을 만듭니다. Hello 도구를 사용 하 여 일반적으로 응용 프로그램에 대 한 변경할 수 없습니다 블록 크기 및 큐 깊이 같은 매개 변수를 구성할 수도 있습니다. 이렇게 하면 더 많은 유연성 toodrive hello 최대 성능을 대규모 VM 프로 비전 되어 다양 한 유형의 응용 프로그램 작업에 대 한 프리미엄 디스크에 있습니다. 방문 벤치마킹 각 도구에 대 한 자세한 toolearn [Iometer](http://www.iometer.org/) 및 [FIO](http://freecode.com/projects/fio)합니다.

toofollow hello 아래의 예제에서 표준 DS14 VM을 만들고 11 프리미엄 저장소 디스크 toohello VM을 연결 합니다. Hello 11 디스크의 캐싱 "None"으로 호스트와 10 디스크를 구성 하 고 NoCacheWrites를 호출 하는 볼륨으로이 스트라이프 합니다. Hello 남아 있는 디스크에 "ReadOnly"로 캐시 호스트를 구성 하 고이 디스크를 사용 하 여 CacheReads를 호출 하는 볼륨을 만듭니다. 이 설치 프로그램을 사용 하 여 수 toosee hello 최대 읽기 및 쓰기 성능을 표준 DS14 VM에서 수 있습니다. 프리미엄 디스크를 사용 하 여 DS14 VM 만들기에 대 한 자세한 단계에 대 한 이동 너무[만들기 및 사용 하 여 데이터 디스크를 가상 컴퓨터에 대 한 프리미엄 저장소 계정](storage-premium-storage.md)합니다.

*Hello 캐시를 준비 중*  
읽기 전용 호스트 캐싱 hello 디스크 수 toogive 됩니다 hello 디스크 제한 보다 더 높은 IOPS입니다. tooget이이 최대 성능 hello 호스트 캐시에서 읽어, 먼저이 디스크의 hello 캐시를 준비 해야 합니다. 이렇게 하면 해당 hello 읽기 IOs 벤치마킹 도구 CacheReads 볼륨에 드라이브는 실제로 도달 hello 캐시와 hello 디스크가 아닌 직접 합니다. hello 캐시 적중 결과 hello 단일 캐시에서 추가 IOPS에 디스크를 사용할 수 있습니다.

> **중요:**  
> VM 다시 부팅 될 때마다 벤치마킹를 실행 하기 전에 hello 캐시를 준비 해야 합니다.
>
>

#### <a name="iometer"></a>Iometer
[Hello Iometer 도구를 다운로드](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) hello VM에 있습니다.

*테스트 파일*  
Iometer는 테스트, 즉 벤치마킹 hello 실행 될 hello 볼륨에 저장 된 테스트 파일을 사용 합니다. 계획과 읽기 및 쓰기에이 파일 toomeasure hello 디스크 IOPS 및 처리량 테스트 합니다. Iometer는 이 테스트 파일을 제공받지 않은 경우 만듭니다. Hello CacheReads 및 NoCacheWrites 볼륨에 iobw.tst 라는 200GB 테스트 파일을 만듭니다.

*액세스 사양*  
hello 사양, 요청 크기 IO % 읽기/쓰기, % 임의/순차적 구성 해 보고 Iometer hello "Access 사양" 탭을 사용 하 합니다. 각 아래에 설명 된 hello 시나리오에 대 한 액세스 사양을 만듭니다. Hello 액세스 사양이 만들고 "저장" 가능한 적절 한 이름을 같은 – RandomWrites\_8k RandomReads\_8k 합니다. Hello 테스트 시나리오를 실행 하는 경우 해당 하는 hello 설정을 선택 합니다.

최대 쓰기 IOPS 시나리오에 대한 액세스 사양의 예는 아래와 같습니다.  
    ![](media/storage-premium-storage-performance/image8.png)

*최대 IOPS 테스트 사양*  
toodemonstrate 최대 IOPs 보다 작은 요청 크기를 사용 합니다. 8K 요청 크기를 사용하고 임의 쓰기 및 읽기에 대한 사양을 만듭니다.

| 액세스 사양 | 요청 크기 | 임의 % | 읽기 % |
| --- | --- | --- | --- |
| RandomWrites\_8K |8K |100 |0 |
| RandomReads\_8K |8K |100 |100 |

*최대 처리량 테스트 사양*  
toodemonstrate 최대 처리량을 더 큰 요청 크기를 사용 합니다. 64K 요청 크기를 사용하여 임의 쓰기 및 읽기에 대한 사양을 만듭니다.

| 액세스 사양 | 요청 크기 | 임의 % | 읽기 % |
| --- | --- | --- | --- |
| RandomWrites\_64K |64K |100 |0 |
| RandomReads\_64K |64K |100 |100 |

*Hello Iometer 테스트 실행*  
캐시를 toowarm 아래 hello 단계를 수행 합니다.

1. 아래에 표시된 값으로 두 액세스 사양을 만듭니다.

   | 이름 | 요청 크기 | 임의 % | 읽기 % |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1MB |100 |0 |
   | RandomReads\_1MB |1MB |100 |100 |
2. 다음 매개 변수가 있는 캐시 디스크를 초기화 하기 위한 hello Iometer 테스트를 실행 합니다. Hello 대상 볼륨 및 128 개 큐 깊이 대 한 세 개의 작업자 스레드를 사용 합니다. 설정 "실행 시간" hello "테스트 설정" 탭에서 테스트 too2hrs hello 기간 hello 합니다.

   | 시나리오 | 대상 볼륨 | 이름 | 기간 |
   | --- | --- | --- | --- |
   | 디스크 캐시 초기화 |CacheReads |RandomWrites\_1MB |2hrs |
3. 다음 매개 변수가 있는 디스크 캐시를 준비 하는 중에 대 한 hello Iometer 테스트를 실행 합니다. Hello 대상 볼륨 및 128 개 큐 깊이 대 한 세 개의 작업자 스레드를 사용 합니다. 설정 "실행 시간" hello "테스트 설정" 탭에서 테스트 too2hrs hello 기간 hello 합니다.

   | 시나리오 | 대상 볼륨 | 이름 | 기간 |
   | --- | --- | --- | --- |
   | 캐시 디스크 준비 |CacheReads |RandomReads\_1MB |2hrs |

캐시 디스크 준비는 후에 아래에 나열 된 hello 테스트 시나리오를 진행 합니다. toorun hello Iometer 테스트에 대 한 세 개 이상의 작업자 스레드를 사용 하 여 **각** 볼륨 대상으로 합니다. 각 작업자 스레드에 대해 hello 대상 볼륨을 선택 하 고 큐 깊이 설정 toorun hello 해당 테스트 시나리오 아래 hello 표에 표시 된 대로 저장 하는 hello 테스트 사양 중 하나를 선택 합니다. hello 테이블도 예상된 결과가 나와 IOPS 및 처리량에 대 한 이러한 테스트를 실행 하는 경우. 모든 시나리오의 경우 8KB의 작은 IO 크기 및 128의 높은 큐 크기가 사용됩니다.

| 테스트 시나리오 | 대상 볼륨 | 이름 | 결과 |
| --- | --- | --- | --- |
| 최대 읽기 IOPS |CacheReads |RandomWrites\_8K |50,000 IOPS  |
| 최대 쓰기 IOPS |NoCacheWrites |RandomReads\_8K |64,000 IOPS |
| 최대 결합된 IOPS |CacheReads |RandomWrites\_8K |100,000 IOPS |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| 최대 읽기 MB/초 |CacheReads |RandomWrites\_64K |524MB/초 |
| 최대 쓰기 MB/초 |NoCacheWrites |RandomReads\_64K |524MB/초 |
| 결합된 MB/초 |CacheReads |RandomWrites\_64K |1000MB/초 |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

Hello의 스크린 샷을 결합 된 IOPS 및 처리량 시나리오에 대 한 해 보고 Iometer 테스트 결과 다음과 같습니다.

*읽기 및 쓰기 최대 IOPS를 결합*  
![](media/storage-premium-storage-performance/image9.png)

*읽기 및 쓰기 최대 처리량을 결합*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO는 hello Linux Vm의 경우에 인기 있는 도구 toobenchmark 저장소입니다. Hello 유연성 tooselect 다른 IO 크기, 순차 또는 임의 읽기 및 쓰기를에 있습니다. 작업자 스레드를 생성 또는 프로세스 tooperform hello I/O 작업을 지정 하십시오. 각 작업자 스레드가 작업 파일을 사용 하 여 수행 해야 하는 I/O 작업의 hello 유형을 지정할 수 있습니다. 아래의 hello 예제에 나와 있는 시나리오로 당 하나의 작업 파일을 만들었습니다. 이러한 작업 파일 toobenchmark 다른 작업에서 프리미엄 저장소에서 실행 중인 hello 사양을 변경할 수 있습니다. Hello 예제에서 사용 하 여 표준 DS 14 VM 실행 **Ubuntu**합니다. 사용 하 여 hello hello의 hello 시작 부분에 설명 된 동일한 설치 [섹션, 즉 벤치마킹](#Benchmarking) 및 테스트, 즉 벤치마킹 hello를 실행 하기 전에 hello 캐시를 준비 합니다.

시작하기 전에 [FIO를 다운로드](https://github.com/axboe/fio) 하고 가상 컴퓨터에 설치합니다.

Hello, Ubuntu 용 다음 명령을 실행 합니다.

```
apt-get install fio
```

Hello 디스크에서 구동 읽기 작업에 대 한 쓰기 작업을 이끌어내기 위한 4 개의 작업자 스레드 및 4 개의 작업자 스레드가 사용 합니다. hello 쓰기 작업 자가 됩니다 수 운전 트래픽을 캐시와 10 디스크가 nocache"hello" 볼륨에 "None"입니다. hello 읽기 작업 자가 됩니다 수 운전 트래픽을 캐시 집합 1 디스크가 너무 readcache"hello" 볼륨에 "ReadOnly"입니다.

*최대 쓰기 IOPS*  
다음 사양 tooget으로 hello 작업 파일을 만들어 최대 쓰기 IOPS입니다. “fiowrite.ini”로 이름을 지정합니다.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

참고 hello 이전 섹션에서 설명 하는 hello 디자인 지침에 일치 하는 주요 작업을 수행 합니다. 이러한 사양은 필수 toodrive 최대 IOPS  

* 256의 높은 큐 크기.  
* 8KB의 작은 블록 크기.  
* 임의 쓰기를 수행하는 다중 스레드.

Hello FIO 30 초 동안 테스트 hello 해제 명령을 tookick 다음 실행  

```
sudo fio --runtime 30 fiowrite.ini
```

Hello 테스트를 실행할 수 toosee hello 수가 쓰기 IOPS hello VM 및 프리미엄 디스크를 배달 하는 수 있습니다. Hello 샘플 아래에 나와 있는 것 처럼 해당 최대 쓰기 IOPS 제한은 50, 000 IOPS의 hello DS14 VM에 제공 하는 합니다.  
    ![](media/storage-premium-storage-performance/image11.png)

*최대 읽기 IOPS*  
다음 사양 tooget으로 hello 작업 파일을 만들어 최대 읽기 IOPS입니다. "fioread.ini"로 이름을 지정합니다.

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

참고 hello 이전 섹션에서 설명 하는 hello 디자인 지침에 일치 하는 주요 작업을 수행 합니다. 이러한 사양은 필수 toodrive 최대 IOPS

* 256의 높은 큐 크기.  
* 8KB의 작은 블록 크기.  
* 임의 쓰기를 수행하는 다중 스레드.

Hello FIO 30 초 동안 테스트 hello 해제 명령을 tookick 다음 실행

```
sudo fio --runtime 30 fioread.ini
```

Hello 테스트 실행 되는 동안 읽기 IOPS hello VM 수 toosee hello 수 있습니다 및 프리미엄 디스크를 배달 하는 합니다. 아래 hello 예제와 같이 hello DS14 VM 64, 000 개 이상의 읽기 IOPS 전달 합니다. 이 hello 디스크와 hello 캐시 성능의 조합입니다.  
    ![](media/storage-premium-storage-performance/image12.png)

*최대 읽기 및 쓰기 IOPS*  
만들 최대 다음 사양 tooget hello 작업 파일 읽기 및 쓰기 IOPS를 결합 합니다. "fioreadwrite.ini"로 이름을 지정합니다.

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

참고 hello 이전 섹션에서 설명 하는 hello 디자인 지침에 일치 하는 주요 작업을 수행 합니다. 이러한 사양은 필수 toodrive 최대 IOPS

* 128의 높은 큐 크기  
* 4KB의 작은 블록 크기  
* 임의 읽기 및 쓰기를 수행하는 다중 스레드

Hello FIO 30 초 동안 테스트 hello 해제 명령을 tookick 다음 실행

```
sudo fio --runtime 30 fioreadwrite.ini
```

Hello 테스트를 실행할 수 없게 toosee hello 결합 된 읽기 및 쓰기 IOPS VM hello 및 프리미엄 디스크를 배달 하는 합니다. Hello 샘플 아래에 나와 있는 것 처럼 100, 000 개 이상의 결합 된 읽기 및 쓰기 IOPS hello DS14 VM 전달 합니다. 이 hello 디스크와 hello 캐시 성능의 조합입니다.  
    ![](media/storage-premium-storage-performance/image13.png)

*결합된 최대 처리량*  
최대 tooget hello 결합 된 읽기 및 쓰기 처리량, 읽기 및 쓰기를 수행 하는 여러 스레드가 더 큰 블록 크기 및 큰 큐 깊이 사용 합니다. 64KB의 블록 크기와 128의 큐 크기를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계
Azure 프리미엄 저장소에 대한 자세한 정보

* [프리미엄 저장소: Azure 가상 컴퓨터 워크로드를 위한 고성능 저장소](storage-premium-storage.md)  

SQL Server 사용자의 경우 SQL Server에 대한 성능 모범 사례의 문서를 읽으세요.

* [Azure 가상 컴퓨터의 SQL Server에 대한 성능 모범 사례](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Azure 프리미엄 저장소는 Azure VM의 SQL Server에 대해 가장 높은 성능을 제공합니다](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
