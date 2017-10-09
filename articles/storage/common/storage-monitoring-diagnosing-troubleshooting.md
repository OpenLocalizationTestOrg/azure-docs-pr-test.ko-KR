---
title: "aaaMonitor, 진단 및 해결 Azure 저장소 | Microsoft Docs"
description: "과 같은 클라이언트 쪽 로깅, storage analytics를 사용 하 여 기능 및 기타 타사 도구 tooidentify 진단 및 Azure 저장소 관련 문제를 해결 합니다."
services: storage
documentationcenter: 
author: fhryo-msft
manager: jahogg
editor: tysonn
ms.assetid: d1e87d98-c763-4caa-ba20-2cf85f853303
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: fhryo-msft
ms.openlocfilehash: 43f34a4ccbc3071cdb489958252498a1f88e1a34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-diagnose-and-troubleshoot-microsoft-azure-storage"></a>Microsoft Azure 저장소 모니터링, 진단 및 문제 해결
[!INCLUDE [storage-selector-portal-monitoring-diagnosing-troubleshooting](../../../includes/storage-selector-portal-monitoring-diagnosing-troubleshooting.md)]

## <a name="overview"></a>개요
클라우드 환경에서 호스트된 분산 응용 프로그램의 문제를 진단하고 해결하는 과정이 기존 환경보다 복잡할 수 있습니다. 응용 프로그램은 PaaS/IaaS 인프라, 온-프레미스, 모바일 장치에 배포될 수도 있고 이러한 항목이 조합되어 있는 환경에 배포될 수도 있습니다. 일반적으로 응용 프로그램의 네트워크 트래픽을 공용 및 개인 네트워크를 이동할 수 있습니다 및 응용 프로그램에 Microsoft Azure 저장소 테이블, Blob, 큐와 같은 여러 저장소 기술을 사용할 수 있습니다 또는 더하기 tooother 데이터의 파일 저장 등으로 관계형 및 문서 데이터베이스입니다.

toomanage 이러한 응용 프로그램 성공적으로 적극적으로 모니터링 하 고 이해 해야 방법을 toodiagnose 고 및 해당 종속 기술의 모든 측면의 문제를 해결 합니다. Azure 저장소 서비스의 사용자로 지속적으로 응용 프로그램 (예: 보다 느린 일반적인 응답 시간), 동작에 예기치 않은 변경 내용을 사용 하는 hello 저장소 서비스를 모니터링 하 고 사용 해야 로깅 toocollect 자세한 tooanalyze과 데이터는 깊이에 문제가 있습니다. hello 진단 정보를 모니터링 및 로깅을 모두에서 가져와야 있습니다 toodetermine hello의 근본 원인을 hello 발생 하는 응용 프로그램을 실행할 할 수 있습니다. Hello 문제를 해결 하 고 tooremediate를 수행할 수 있는 hello 적절 한 단계를 확인할 것입니다. Azure 저장소는 핵심 Azure 서비스 하 고 hello 대부분의 고객 toohello Azure 인프라를 배포 하는 솔루션의 중요 한 부분을 형성 합니다. Azure 저장소 기능 toosimplify 모니터링, 진단 및 클라우드 기반 응용 프로그램의 저장소 문제 해결을 포함 합니다.

> [!NOTE]
> Azure 파일 저장소 hello이 이번에는 로깅을 지원 하지 않습니다.
> 

실무 가이드 tooend 간 Azure 저장소는 응용 프로그램에서 문제 해결을 참조 하십시오. [에 종단 간 Azure 저장소 메트릭 및 로깅, AzCopy 및 메시지 분석기를 사용 하 여 문제 해결](../storage-e2e-troubleshooting.md)합니다.

* [소개]
  * [이 가이드의 구성 방식]
* [저장소 서비스를 모니터링]
  * [서비스 상태 모니터링]
  * [용량 모니터링]
  * [가용성 모니터링]
  * [성능 모니터링]
* [저장소 문제를 진단]
  * [서비스 상태 문제]
  * [성능 문제]
  * [오류 진단]
  * [저장소 에뮬레이터 문제]
  * [저장소 로깅 도구]
  * [네트워크 로깅 도구 사용]
* [종단 간 추적]
  * [로그 데이터 상관 관계 설정]
  * [클라이언트 요청 ID]
  * [서버 요청 ID]
  * [타임스탬프]
* [문제 해결 지침]
  * [메트릭에서 높은 AverageE2ELatency 및 낮은 AverageServerLatency]
  * [낮은 AverageE2ELatency 및 낮은 AverageServerLatency 메트릭을 표시 하지만 hello 클라이언트에서 높은 대기 시간이 발생 합니다.]
  * [메트릭에서 AverageServerLatency가 높게 표시됨]
  * [큐에서 메시지 배달 중에 예기치 않은 대기 시간이 발생함]
  * [메트릭에서 PercentThrottlingError의 증가]
  * [메트릭에서 PercentTimeoutError의 증가]
  * [메트릭에서 PercentNetworkError가 증가하는 것으로 표시됨]
  * [HTTP 403 (금지 됨) 메시지를 받고 hello 클라이언트]
  * [hello 클라이언트에서 HTTP 404 (찾을 수 없음) 메시지를 받는]
  * [hello 클라이언트 HTTP 409 (충돌) 메시지 수신]
  * [메트릭에서 낮은 PercentSuccess 또는 분석 로그 항목 된 작업이 있을 ClientOtherErrors의 트랜잭션 상태]
  * [용량 메트릭에 예기치 않은 저장소 용량 사용 증가가 표시됨]
  * [많은 수의 VHD가 연결된 가상 컴퓨터가 예기치 않게 다시 부팅됨]
  * [개발 또는 테스트에 대 한 hello 저장소 에뮬레이터를 사용 하 여 문제 발생]
  * [Hello Azure SDK for.NET 설치에 문제가 발생 하는]
  * [저장소 서비스에서 다른 문제가 발생함]
  * [Windows에서 Azure File Storage 문제 해결](../files/storage-troubleshoot-windows-file-connection-problems.md)   
  * [Linux에서 Azure File Storage 문제 해결](../files/storage-troubleshoot-linux-file-connection-problems.md)
* [부록]
  * [부록 1: toocapture HTTP 및 HTTPS 트래픽을 Fiddler를 사용 하 여]
  * [부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여]
  * [부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여]
  * [부록 4: Excel tooview 메트릭 및 로그 데이터를 사용 하 여]
  * [부록5: Visual Studio Team Services용 Application Insights를 사용한 모니터링]

## <a name="introduction"></a>소개
관련 문제를이 가이드를 표시 하면 toouse Azure 저장소 분석, hello Azure 저장소 클라이언트 라이브러리에서에서 클라이언트 쪽 로깅 및 기타 타사 도구 tooidentify 같은 기능을 진단 하는 방법과 Azure 저장소 문제를 해결 합니다.

![][1]

이 가이드는 Azure 저장소 서비스와 같은 온라인 서비스 관리를 담당 하는 IT 전문가 사용 하는 온라인 서비스의 개발자가 주로 읽기 의도 한 toobe 있습니다. 이 가이드의 hello 목표 같습니다.

* toohelp Azure 저장소 계정의 hello 상태 및 성능을 유지 합니다.
* tooprovide hello 필요한 프로세스 및 응용 프로그램에서 문제점을 tooAzure 저장소 관련 경우 결정 도구 toohelp 있습니다.
* tooprovide tooAzure 저장소와 관련 된 문제 해결에 대 한 실행 가능한 설명서와 함께 있습니다.

### <a name="how-this-guide-is-organized"></a>이 가이드의 구성 방식
hello 섹션 "[저장소 서비스를 모니터링]" Azure 저장소 분석 통계 (저장소 메트릭)를 사용 하 여 Azure 저장소 서비스의 상태와 성능을 toomonitor hello 하는 방법에 대해 설명 합니다.

hello 섹션 "[저장소 문제를 진단]" toodiagnose 발급 하는 방법을 설명 합니다. Azure 저장소 분석 로깅 (저장소 로깅)을 사용 하 여 합니다. 또한 tooenable 클라이언트 쪽 로깅을 사용 하 여.NET 용 저장소 클라이언트 라이브러리 hello 같은 hello 클라이언트 라이브러리 중 하나에서 기능 hello 또는 Azure SDK for Java 환영 방법을 설명 합니다.

hello 섹션 "[종단 간 추적]" 다양 한 로그 파일 및 메트릭 데이터에 포함 된 hello 정보 상호 연결 수에 대해 설명 합니다.

hello 섹션 "[문제 해결 지침]" hello 일반적인 저장소 관련 문제가 발생할 수 있는 일부에 대 한 해결 지침을 제공 합니다.

hello "[부록]" 패킷 데이터, Fiddler HTTP/HTTPS 메시지를 분석 하기 위한 네트워크 분석 및 Microsoft 메시지 분석기를 연결 하기 위한 로그 데이터에 대 한 Wireshark 및 Netmon와 같은 다른 도구를 사용 하는 방법에 대 한 정보를 포함 합니다.

## <a name="monitoring-your-storage-service"></a>저장소 서비스 모니터링
Windows 성능 모니터링에 대해 잘 알고 있는 경우 저장소 메트릭은 Windows 성능 모니터 카운터의 Azure 저장소 버전이라고 생각하면 됩니다. 저장소 메트릭에서, 서비스 가용성 성공한 요청 tooservice의 요청 tooservice의 총 개수 또는 비율 메트릭 (용어로 Windows 성능 모니터 카운터) 포괄적인 집합이 있습니다. Hello 사용할 수 있는 메트릭 전체 목록은 참조 하십시오. [저장소 분석 통계 테이블 스키마](http://msdn.microsoft.com/library/azure/hh343264.aspx)합니다. 저장소 서비스 toocollect hello 및 집계 메트릭을 매 시간 또는 1 분 마다 사용할지를 지정할 수 있습니다. Tooenable 메트릭 및 모니터 저장소 계정을 참조 하는 방법에 대 한 자세한 내용은 [저장소 메트릭 사용 및 메트릭 데이터 보기](http://go.microsoft.com/fwlink/?LinkId=510865)합니다.

시간별 메트릭을 선택할 수 있습니다 toodisplay hello에 원하는 [Azure 포털](https://portal.azure.com) 및 관리자 전자 메일을 통해 알림을 생성 한 시간별 메트릭이 특정 임계값을 초과할 때마다 규칙을 구성 합니다. 자세한 내용은 [경고 알림 받기](/azure/monitoring-and-diagnostics/monitoring-overview-alerts.md)를 참조하세요. 

hello 저장소 서비스는 최상의 노력을 사용 하 여 메트릭을 수집 되지만 모든 저장소 작업을 기록 하지 않을 수 있습니다.

Hello Azure 포털에서에서 가용성, 총 요청 및 저장소 계정에 대 한 평균 대기 시간 번호와 같은 메트릭을 볼 수 있습니다. 알림 규칙도 설정한 tooalert 관리자 가용성 특정 수준 이하로 떨어지면 합니다. 이 데이터를 볼 수 없도록 조사를 위해 가능한 한 영역은 hello 테이블 서비스 성공률이 100% 미만이 되 고 (자세한 내용은 hello 섹션을 참조 하십시오. "[메트릭에서 낮은 PercentSuccess 또는 분석 로그 항목 된 작업이 있을 ClientOtherErrors의 트랜잭션 상태]").

정상 상태이 고 예상 대로 수행 하 여 Azure 응용 프로그램 tooensure를 지속적으로 모니터링 해야 합니다.

* Toocompare 현재 데이터를 설정 하 고 hello 동작 Azure 저장소와 응용 프로그램의 중요 한 변경 내용을 식별 하는 응용 프로그램에 대 한 몇 가지 초기 메트릭을 설정 합니다. 초기 메트릭을 hello 값을, 대부분의 경우에서 특정 응용 프로그램 되며 성능 응용 프로그램을 테스트 했으면 설정 해야 합니다.
* 분 메트릭을 기록 하 고 사용 하 여 해당 toomonitor 적극적으로 예기치 않은 오류 및 오류 개수 또는 요청 속도에 스파이크가 있으면 같은 잘못 된 부분에 대 한 합니다.
* 시간 메트릭 기록 하 고 사용 하 여 해당 toomonitor 평균 값와 같은 오류 수를 평균 하 고 급여를 요청 합니다.
* Hello 섹션의 뒷부분에서 설명 하는 대로 진단 도구를 사용 하 여 잠재적인 문제를 조사 하 고 "[저장소 문제를 진단]."

다음 이미지는 hello의 hello 차트 방법을 hello 시간 메트릭의 경우 발생 하는 평균에 숨길 수 스파이크 활동 하는 방법을 보여 줍니다. 시간 메트릭 hello hello 분 메트릭을 실제로 수행 중인 hello 변동 표시 하는 동안 요청을 일정 한 속도로 tooshow 나타납니다.

![][3]

hello이 섹션의 나머지 부분에 설명 어떤 메트릭을 모니터링 하 고 이유입니다.

### <a name="monitoring-service-health"></a>서비스 상태 모니터링
Hello를 사용할 수 있습니다 [Azure 포털](https://portal.azure.com) 모든 hello 저장소 서비스 (및 다른 Azure 서비스)의 tooview hello 상태 hello hello 전 세계 Azure 지역입니다. 이렇게 하면 toosee 즉시 제어할 문제 hello 응용 프로그램에 사용 하는 hello 지역에서 저장소 서비스에 영향을 주는 경우.

hello [Azure 포털](https://portal.azure.com) hello에 영향을 주는 인시던트 알림을 다양 한 Azure 서비스를 제공할 수도 있습니다.
참고:이 정보를 hello에서 기록 데이터와 함께 이전에 사용할 수 [Azure 서비스 대시보드](http://status.azure.com)합니다.

Hello 동안 [Azure 포털](https://portal.azure.com) 내에서 상태 정보를 수집 합니다. Azure 데이터 센터 (바깥 모니터링) hello, 간접적인 방법은 toogenerate 가상 트랜잭션을 주기적으로 채택 수도 여러 위치에서 Azure를 호스팅하는 웹 응용 프로그램에 액세스 합니다. 제공 하는 서비스 hello [Dynatrace](http://www.dynatrace.com/en/synthetic-monitoring) 및 Visual Studio Team Services에 대 한 Application Insights는이 간접적인 방법의 예입니다. Visual Studio Team Services에 대 한 Application Insights에 대 한 자세한 내용은 hello 부록을 참조 하십시오. "[부록 5: Visual Studio Team Services에 대 한 Application Insights를 사용 하 여 모니터링](#appendix-5)."

### <a name="monitoring-capacity"></a>용량 모니터링
저장소 메트릭을 저장 hello blob 서비스에 대 한 용량 메트릭 blob는 일반적으로 저장 된 데이터의 가장 큰 비율 hello에 대 한 계정 때문에 (작성 hello 시이 테이블 및 큐의 가능한 toouse 저장소 메트릭을 toomonitor hello 용량) . Hello에서이 데이터를 찾을 수 있습니다 **$MetricsCapacityBlob** hello Blob 서비스에 대 한 모니터링을 설정한 경우 테이블입니다. 하루에 한 번이 데이터를 기록 하는 저장소 메트릭 및 hello hello 값을 사용 하 여 **RowKey** toodetermine hello 행 toouser 데이터와 관련 된 엔터티를 포함 하는 여부 (값 **데이터**) 또는 분석 데이터 ( 값 **분석**). 사용 된 저장소 용량 hello에 대 한 정보를 포함 하는 저장 된 각 엔터티 (**용량** 바이트 단위로 지정) 및 컨테이너의 현재 개수 hello (**ContainerCount**) 및 blob ( **ObjectCount**) hello 저장소 계정에 사용에서 합니다. Hello에 저장 된 hello 용량 메트릭에 대 한 자세한 내용은 **$MetricsCapacityBlob** 테이블에서 참조 [저장소 분석 통계 테이블 스키마](http://msdn.microsoft.com/library/azure/hh343264.aspx)합니다.

> [!NOTE]
> 저장소 계정의 hello 용량 제한에 도달 하는 조기 경고에 대 한 이러한 값을 모니터링 해야 합니다. Azure 포털 hello 집계 저장소 사용량을 초과 하거나 임계값 미만으로 떨어질 했는지 여부를 지정 하는 경고 규칙 toonotify를 추가할 수 있습니다.
> 
> 

Blob와 같은 다양 한 저장소 개체의 hello 크기를 계산 하는 데 도움이 필요한 경우 hello 블로그 게시물을 참조 [Azure 저장소 청구 이해-대역폭, 트랜잭션 및 용량](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx)합니다.

### <a name="monitoring-availability"></a>가용성 모니터링
Hello에 hello 값을 모니터링 하 여 저장소 계정의 hello 저장소 서비스의 hello 가용성을 모니터링 해야 **가용성** 열에 시간 또는 분 메트릭 테이블 hello- **$ MetricsHourPrimaryTransactionsBlob**, **$MetricsHourPrimaryTransactionsTable**, **$MetricsHourPrimaryTransactionsQueue**, **$ MetricsMinutePrimaryTransactionsBlob**, **$MetricsMinutePrimaryTransactionsTable**, **$MetricsMinutePrimaryTransactionsQueue**, **$ MetricsCapacityBlob**합니다. hello **가용성** hello 서비스나 hello 행으로 표시 되는 hello API 작업의 hello 사용 가능성을 나타내는 백분율 값을 포함 하는 열 (hello **RowKey** hello 행이 포함 된 경우 표시 메트릭 hello 서비스 전체에 대해 또는 특정 API 작업에 대 한).

값이 100%보다 작으면 일부 저장소 요청이 실패함을 나타냅니다. 검사 하 여 실패 하는 이유를 확인할 수와 같은 여러 오류 유형 사용 하 여 요청 수가 hello를 표시 하는 hello 메트릭 데이터의 다른 열을 hello **ServerTimeoutError**합니다. Toosee 하시면 **가용성** hello 서비스 파티션 toobetter 부하를 분산 요청이 이동 하는 동안 임시 서버 제한 시간 등의 이유로 100% 보다 일시적으로 해당; hello 재시도 논리를 클라이언트 응용 프로그램에서 같은 일시적인 조건을 처리 해야 합니다. hello 문서 [저장소 분석에서 기록한 작업 및 상태 메시지](http://msdn.microsoft.com/library/azure/hh343260.aspx) 목록에 저장소 메트릭을 포함 하는 트랜잭션 유형 hello 해당 **가용성** 계산 합니다.

Hello에 [Azure 포털](https://portal.azure.com), toonotify 경고 규칙을 추가할 수 있습니다 하는 경우 **가용성** 서비스가 지정한 임계값에 미달할에 대 한 합니다.

hello "[문제 해결 지침]"이이 가이드의 섹션에서는 몇 가지 일반적인 저장소 서비스 문제 관련된 tooavailability를 설명 합니다.

### <a name="monitoring-performance"></a>성능 모니터링
hello 저장소 서비스의 toomonitor hello 성능을 hello를 사용할 수 있습니다 메트릭을 hello에서 1 시간 마다 하 고 분 메트릭 테이블입니다.

* hello 값 hello **AverageE2ELatency** 및 **AverageServerLatency** 열 hello 평균 시간 hello 저장소 서비스를 표시 하거나 API 작업 유형이 시간이 tooprocess 요청 합니다. **AverageE2ELatency** 는 tooread hello 요청을 수행 하는 hello 시간을 포함 하는 종단 간 대기 시간 측정 및 추가 toohello tooprocess hello 요청에 걸린 시간에 hello 응답을 보냅니다 (따라서 포함 네트워크 대기 시간 hello 요청 되 면 hello 저장소 서비스에 도달); **AverageServerLatency** 따라서 관련 네트워크 대기 시간을 제외 하는 방금 hello 처리 시간 측정 toocommunicating hello 클라이언트와 함께 합니다. Hello 섹션을 참조 "[메트릭에서 높은 AverageE2ELatency 및 낮은 AverageServerLatency]" 이유에 대 한 내용은이 가이드의 뒷부분에 나오는 있을 수 있습니다이 두 값 간에 큰 차이 합니다.
* hello에 대 한 값을 hello **TotalIngress** 및 **TotalEgress** 저장소 서비스에서 또는 특정 API 작업 유형을 통해 이동 tooand에 방문 하 고 열을 바이트 단위로 hello 총 양의 데이터를 표시 합니다.
* hello에 대 한 값을 hello **TotalRequests** 열 표시 hello의 총 저장소 서비스 API 작업의 hello 하는 요청을 수신 합니다. **TotalRequests** hello hello 저장소 서비스에서 수신한 요청의 총 수입니다.

일반적으로는 이러한 값이 예기치 않게 변경되는지 여부를 모니터링하여 조사가 필요한 문제가 있는지 파악합니다.

Hello에 [Azure 포털](https://portal.azure.com), toonotify 여부이 서비스에 대 한 성능 메트릭을 hello 미만으로 떨어질 또는 지정 된 임계값을 초과 경고 규칙을 추가할 수 있습니다.

hello "[문제 해결 지침]"이이 가이드의 섹션에서는 몇 가지 일반적인 저장소 서비스 문제 관련된 tooperformance를 설명 합니다.

## <a name="diagnosing-storage-issues"></a>저장소 문제 진단
여러 가지 방법으로 다음과 같은 응용 프로그램의 문제를 파악할 수 있습니다.

* Hello 응용 프로그램 toocrash 또는 toostop 작업을 발생 시키는 오류가 발생 합니다.
* Hello 메트릭 hello 이전 섹션에 설명 된 대로 모니터링 하는 초기 계획 값에서 크게 변화 "[저장소 서비스를 모니터링]."
* 일부 특정 작업이 정상적으로 완료되지 않거나 일부 기능이 작동하지 않는다는 응용 프로그램 사용자의 보고
* 응용 프로그램 내에서 생성되어 로그 파일이나 일부 기타 알림 방법을 통해 표시되는 오류

일반적으로 문제 관련된 tooAzure 저장소 서비스는 네 가지 광범위 한 범주 중 하나에 속합니다.

* 응용 프로그램에서 사용자에 게 보고 또는 hello 성능 메트릭의 변경 내용에 의해 표시 된 성능 문제를 있습니다.
* 하나 이상의 영역에 hello Azure 저장소 인프라에 문제가 있습니다.
* 응용 프로그램에서 사용자에 게 보고 또는 증가 모니터링 hello 오류 개수 메트릭 중 하나에 의해 표시 된 오류가 발생 합니다.
* 개발 및 테스트 하는 동안 사용할 수 있습니다 hello 로컬 저장소 에뮬레이터; hello 저장소 에뮬레이터의 toousage 특별히 관련 된 몇 가지 문제가 발생할 수 있습니다.

hello 다음 섹션에서는 단계에 설명 hello toodiagnose를 수행 하 고 이러한 네 가지 범주의 각각의 문제를 해결 해야 합니다. hello 섹션 "[문제 해결 지침]"이이 가이드의 뒷부분에 나오는 발생할 수 있는 몇 가지 일반적인 문제에 대 한 자세한 정보를 제공 합니다.

### <a name="service-health-issues"></a>서비스 상태 문제
서비스 상태 문제는 대개 직접 해결할 수가 없습니다. hello [Azure 포털](https://portal.azure.com) 저장소 서비스를 포함 하 여 Azure 서비스와 모든 진행 중인 문제에 대 한 정보를 제공 합니다. 를 선택한 경우 읽기 액세스 지역 중복 저장소에 대 한 저장소 계정을 만들 때 다음 hello 기본 위치에서 사용할 수 없게 하 여 데이터의 hello 이벤트에서 응용 프로그램 전환 일시적으로 toohello 읽기 전용 hello 보조 위치에 복사 합니다. toodo이 응용 프로그램 수 tooswitch hello 기본 및 보조 저장소 위치를 사용 하 고 읽기 전용 데이터로 기능 제한 모드로 수 toowork 설정 해야 합니다. hello Azure 저장소 클라이언트 라이브러리를 사용 하면 주 저장소에서 읽기 실패 하는 경우 보조 저장소에서 읽을 수 있는 다시 시도 정책은 toodefine 합니다. 응용 프로그램에 또한 toobe hello 보조 위치에 있는 hello 데이터는 결국 일관성이 필요 합니다. 자세한 내용은 hello 블로그 게시물을 참조 하십시오. [Azure 저장소 중복 옵션 및 읽기 액세스 지역 중복 저장소](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/)합니다.

### <a name="performance-issues"></a>성능 문제
응용 프로그램의 성능을 hello 사용자 관점에서 특히 주관적인 될 수 있습니다. 따라서 중요 한 toohave 기준 메트릭을 사용할 수 있는 toohelp 식별 하는 경우 성능 문제가 있을 수 있습니다. 다양 한 요인 hello 클라이언트 응용 프로그램 관점에서 Azure 저장소 서비스의 hello 성능에 영향을 줄 수 있습니다. 이러한 요소는 hello 네트워크 인프라; hello 클라이언트 또는 hello 저장소 서비스 작동 될 수 있습니다. 따라서 중요 한 toohave hello 원점 hello 성능 문제를 식별 하기 위한 전략 합니다.

Hello hello 메트릭에서 hello 성능 문제의 가능한 원인 hello 가능성이 위치를 식별 한 후 사용 하 여 hello 로그 파일 toofind 세부 정보 toodiagnose 고 hello 문제를 세부적 문제를 해결 한 다음 수 있습니다.

hello 섹션 "[문제 해결 지침]" 문제와 관련 된 몇 가지 일반적인 성능에 대 한 자세한 내용은이 가이드의 뒷부분에 나오는 제공 발생할 수 있습니다.

### <a name="diagnosing-errors"></a>오류 진단
사용자가 응용 프로그램의 hello 클라이언트 응용 프로그램에서 보고 된 오류 알려 수 있습니다. 저장소 메트릭은 **NetworkError**, **ClientTimeoutError**, **AuthorizationError** 등의 저장소 서비스에서 발생하는 여러 오류 유형의 수도 기록합니다. 저장소 메트릭은 서로 다른 오류 유형의 수만 기록하지만 서버 쪽, 클라이언트 쪽 및 네트워크 로그를 검사하여 개별 요청에 대한 추가 정보를 얻을 수도 있습니다. 일반적으로 hello hello 저장소 서비스에서 반환 되는 HTTP 상태 코드는 hello 요청이 실패 한 이유를 나타내는 값을 제공 합니다.

> [!NOTE]
> 예상 하는 해야 toosee 일부 일시적인 오류 기억: 예를 들어: tootransient 네트워크 상태로 인해 오류 또는 응용 프로그램 오류입니다.
> 
> 

hello 다음 리소스는 저장소 관련 상태 및 오류 코드를 이해 하는 데 유용 합니다.

* [공통 REST API 오류 코드](http://msdn.microsoft.com/library/azure/dd179357.aspx)
* [Blob 서비스 오류 코드](http://msdn.microsoft.com/library/azure/dd179439.aspx)
* [큐 서비스 오류 코드](http://msdn.microsoft.com/library/azure/dd179446.aspx)
* [테이블 서비스 오류 코드](http://msdn.microsoft.com/library/azure/dd179438.aspx)
* [파일 서비스 오류 코드](https://msdn.microsoft.com/library/azure/dn690119.aspx)

### <a name="storage-emulator-issues"></a>저장소 에뮬레이터 문제
hello Azure SDK 개발 워크스테이션에서 실행할 수는 저장소 에뮬레이터를 포함 합니다. 이 에뮬레이터는 대부분의 hello Azure 저장소 서비스의 hello 동작을 시뮬레이션 하 고 개발 및 테스트 중에 유용, toorun 있도록 hello 없이 Azure 저장소 서비스를 사용 하는 응용 프로그램에 Azure 구독 및 Azure 저장소 계정에 대 한 필요 합니다.

hello "[문제 해결 지침]"이이 가이드의 섹션에서는 hello 저장소 에뮬레이터를 사용 하 여 발생 하는 몇 가지 일반적인 문제를 설명 합니다.

### <a name="storage-logging-tools"></a>저장소 로깅 도구
저장소 로깅은 Azure 저장소 계정의 저장소 요청에 대한 서버 쪽 로깅 기능을 제공합니다. 어떻게 tooenable 서버 쪽 로깅을 액세스 hello 로그 및 데이터에 대 한 자세한 내용은 참조 [저장소 로깅을 사용 하도록 설정 및 로그 데이터에 액세스](http://go.microsoft.com/fwlink/?LinkId=510867)합니다.

.NET 용 저장소 클라이언트 라이브러리 hello toocollect 클라이언트 쪽 로그 데이터를 응용 프로그램에서 수행 되는 toostorage 작업와 관련 된 수 있도록 합니다. 자세한 내용은 참조 [클라이언트 hello.NET 저장소 클라이언트 라이브러리를 사용 하 여 로깅](http://go.microsoft.com/fwlink/?LinkId=510868)합니다.

> [!NOTE]
> 일부 경우 (예: SAS 권한 부여 오류)에 사용자를 찾을 수 있습니다 요청 데이터가 없습니다 hello 서버 쪽 저장소 로그 오류를 보고할 수 있습니다. Hello hello 문제는 발생 hello 클라이언트의 경우 저장소 클라이언트 라이브러리 tooinvestigate hello hello 로깅 기능을 사용 하거나 네트워크 모니터링 도구 tooinvestigate hello 네트워크를 사용할 수 있습니다.
> 
> 

### <a name="using-network-logging-tools"></a>네트워크 로깅 도구 사용
자세한 hello 클라이언트와 서버 tooprovide 간의 hello 트래픽을 캡처할 수 있습니다 hello 데이터 hello 클라이언트와 서버에 대 한 정보를 교환 하 고 hello 네트워크 상태를 기본 됩니다. 다음과 같은 유용한 네트워크 로깅 도구를 사용할 수 있습니다.

* [Fiddler](http://www.telerik.com/fiddler) 무료 웹 디버깅 tooexamine hello 헤더 및 HTTP 및 HTTPS 요청 및 응답 메시지의 페이로드 데이터를 사용 하면 프록시입니다. 자세한 내용은 참조 [부록 1:를 사용 하 여 Fiddler toocapture HTTP 및 HTTPS 트래픽을](#appendix-1)합니다.
* [Microsoft 네트워크 모니터 (Netmon)](http://www.microsoft.com/download/details.aspx?id=4865) 및 [Wireshark](http://www.wireshark.org/) 은 사용 가능한 네트워크 프로토콜 분석기 tooview 수 있도록 하는 다양 한 네트워크 프로토콜에 대 한 패킷 정보를 자세히 설명 합니다. Wireshark에 대 한 자세한 내용은 참조 하십시오. "[부록 2:를 사용 하 여 Wireshark toocapture 네트워크 트래픽을](#appendix-2)"입니다.
* Microsoft 메시지 분석기 이며 Netmon과 toocapturing 패킷 데이터 네트워크 또한 대체 하는 microsoft 도구 tooview를 사용 하면 다른 도구에서 캡처한 hello 로그 데이터를 분석 합니다. 자세한 내용은 참조 하십시오. "[부록 3: Microsoft 메시지 분석기를 사용 하 여 toocapture 네트워크 트래픽을](#appendix-3)"입니다.
* 클라이언트 컴퓨터 hello 네트워크를 통해 toohello Azure 저장소 서비스를 연결할 수 있는지는 기본 연결 테스트 toocheck tooperform 하려는 경우 그럴 수 없으면 hello 표준을 사용 하 여 **ping** hello 클라이언트에는 도구입니다. 그러나 hello를 사용할 수 있습니다 [ **tcping** 도구](http://www.elifulkerson.com/projects/tcping.php) toocheck 연결 합니다.

대부분의 경우에서 저장소 로깅 및 hello 저장소 클라이언트 라이브러리에서 로그 데이터를 hello 충분 한 toodiagnose 문제가 있지만 일부 시나리오에서 보다 자세한 정보 이러한 네트워크 로깅 도구를 제공 하는 hello를 할 수 있습니다. 예를 들어 tooview Fiddler를 사용 하 여 HTTP 및 HTTPS 메시지 수 있도록 tooview 헤더 및 페이로드 분석 데이터 tooand에서에서 보낸 hello를 사용 하면 tooexamine 방법을 클라이언트 응용 프로그램 저장소 서비스에 다시 시도 저장소 작업 합니다. Wireshark 같은 프로토콜 분석기를 사용 하면 tootroubleshoot 모드 해제 패킷 및 연결 문제를 손실 tooview TCP 데이터를 사용 하면 hello 패킷 수준에서 작동 합니다. 메시지 분석기는 HTTP 및 TCP 계층에서 모두 작동할 수 있습니다.

## <a name="end-to-end-tracing"></a>종단 간 추적
다양한 로그 파일을 사용하는 종단 간 추적은 잠재적 문제를 조사하는 데 유용한 기술입니다. 메트릭 데이터에서 위치 toostart hello에 대 한 hello 로그 파일에서 자세한 hello 문제를 해결 하는 데 도움이 되는 정보를 확인 hello 날짜/시간 정보를 사용할 수 있습니다.

### <a name="correlating-log-data"></a>로그 데이터 상관 관계 지정
클라이언트 응용 프로그램에서 로그를 볼 때 네트워크 추적, 및 기록 하는 서버 쪽 저장소는 hello 다른 로그 파일에서 중요 한 toobe 수 toocorrelate 요청 합니다. hello 로그 파일에는 여러 상관 관계 식별자로 사용 되는 다른 필드가 포함 됩니다. hello 클라이언트 요청 id는 hello 가장 유용한 필드 toouse toocorrelate 항목 hello 다른 로그의입니다. 그러나 경우에 따라 유용 toouse 수 hello 서버 요청 id 또는 타임 스탬프입니다. hello 다음 섹션에서는 이러한 옵션에 대 한 자세한 정보.

### <a name="client-request-id"></a>클라이언트 요청 ID
hello 저장소 클라이언트 라이브러리는 자동으로 모든 요청에 대 한 고유한 클라이언트 요청 id를 생성합니다.

* Hello에서 저장소 클라이언트 라이브러리를 hello 클라이언트 쪽 로그를 만드는 hello에 hello 클라이언트 요청 id가 표시 **클라이언트 요청 ID** toohello 요청와 관련 된 모든 로그 항목의 필드입니다.
* Fiddler에서 캡처한 하나 같은 네트워크 추적에 hello 클라이언트 요청 id는 요청 메시지에 표시 hello로 **x ms-클라이언트-요청 id** HTTP 헤더 값입니다.
* Hello 서버 쪽 저장소 로깅 로그 hello 클라이언트 요청 id hello 클라이언트 요청 ID 열에 나타납니다.

> [!NOTE]
> 클라이언트 hello (하지만 hello 저장소 클라이언트 라이브러리에 새 값을 자동으로 할당)이이 값을 할당할 수 있으므로 여러 요청 tooshare hello 동일한 클라이언트 요청 id에 대 한 것 가능 합니다. Hello hello 클라이언트에서 다시 시도의 경우에서 모든 시도 hello 공유 동일한 클라이언트 요청 id입니다. Hello 클라이언트에서 전송 된 일괄 처리의 경우 hello hello 일괄 처리는 단일 클라이언트 요청 id에 있습니다.
> 
> 

### <a name="server-request-id"></a>서버 요청 ID
hello 저장소 서비스 서버 요청 id를 자동으로 생성합니다.

* Hello 서버 쪽 저장소 로깅 로그 hello 서버 요청 id 표시 hello **요청 ID 헤더가** 열입니다.
* Fiddler에서 캡처한 하나 같은 네트워크 추적에 hello 서버 요청 id로 표시 됩니다 응답 메시지 hello **ms 요청 id x** HTTP 헤더 값입니다.
* Hello에서 저장소 클라이언트 라이브러리를 hello 클라이언트 쪽 로그를 만드는 hello에 hello 서버 요청 id가 표시 **작업 텍스트** hello 서버 응답의 세부 정보를 보여 주는 hello 로그 항목에 대 한 열입니다.

> [!NOTE]
> hello 저장소 서비스 항상 고유한 서버 요청 id tooevery 요청이 할당, 수신 하므로 hello 클라이언트에서 모든 다시 시도 및 일괄 처리에 포함 된 모든 작업은 고유한 서버 요청 id입니다.
> 
> 

저장소 클라이언트 라이브러리를 throw 하는 경우 hello는 **StorageException** hello 클라이언트에서 hello **RequestInformation** 속성을 포함 한 **RequestResult** 포함 된 개체는 **ServiceRequestID** 속성입니다. **OperationContext** 인스턴스에서 **RequestResult** 개체에 액세스할 수도 있습니다.

hello 다음 코드 예제에서는 어떻게 tooset 사용자 지정 **ClientRequestId** 연결 하 여 값은 **OperationContext** hello 요청 toohello 저장소 서비스 개체입니다. 또한 표시 방법을 tooretrieve hello **ServerRequestId** hello 응답 메시지의 값입니다.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Create an Operation Context that includes custom ClientRequestId string based on constants defined within hello application along with a Guid.
OperationContext oc = new OperationContext();
oc.ClientRequestID = String.Format("{0} {1} {2} {3}", HOSTNAME, APPNAME, USERID, Guid.NewGuid().ToString());

try
{
    CloudBlobContainer container = blobClient.GetContainerReference("democontainer");
    ICloudBlob blob = container.GetBlobReferenceFromServer("testImage.jpg", null, null, oc);  
    var downloadToPath = string.Format("./{0}", blob.Name);
    using (var fs = File.OpenWrite(downloadToPath))
    {
        blob.DownloadToStream(fs, null, null, oc);
        Console.WriteLine("\t Blob downloaded toofile: {0}", downloadToPath);
    }
}
catch (StorageException storageException)
{
    Console.WriteLine("Storage exception {0} occurred", storageException.Message);
    // Multiple results may exist due tooclient side retry logic - each retried operation will have a unique ServiceRequestId
    foreach (var result in oc.RequestResults)
    {
            Console.WriteLine("HttpStatus: {0}, ServiceRequestId {1}", result.HttpStatusCode, result.ServiceRequestID);
    }
}
```

### <a name="timestamps"></a>타임스탬프
타임 스탬프를 사용할 수도 있습니다 toolocate 로그 항목을 관련 되지만 모든 클럭 hello 클라이언트와 서버에 있을 수 있는 오차의 주의 해야 합니다. 더하기 또는 빼기 일치 하는 클라이언트 hello에 hello 타임 스탬프에 따라 서버 쪽 항목에 대 일 분을 검색 해야 합니다. 포함 된 메트릭을; hello blob에 저장 된 hello 메트릭에 대 한 hello 시간 범위를 나타냅니다. hello blob에 대 한 hello blob 메타 데이터를 기억 합니다. 이 hello 동일한 분 또는 1 시간에 대 한 많은 메트릭 blob을 사용 하는 경우에 유용 합니다.

## <a name="troubleshooting-guidance"></a>문제 해결 지침
이 섹션 hello 진단에 도움이 됩니다 및 hello Azure 저장소 서비스를 사용할 때 발생할 hello 일반적인 문제 중 일부의 응용 프로그램으로 해결 합니다. Toolocate hello 정보 관련 tooyour 특정 문제 아래 hello 목록을 사용 합니다.

**문제 해결 결정 트리**

---
문제는 hello 저장소 서비스 중 하나의 성능 toohello 어떤 관계가 있습니까?

* [메트릭에서 높은 AverageE2ELatency 및 낮은 AverageServerLatency]
* [낮은 AverageE2ELatency 및 낮은 AverageServerLatency 메트릭을 표시 하지만 hello 클라이언트에서 높은 대기 시간이 발생 합니다.]
* [메트릭에서 AverageServerLatency가 높게 표시됨]
* [큐에서 메시지 배달 중에 예기치 않은 대기 시간이 발생함]

---
문제는 hello 저장소 서비스 중 하나의 가용성 toohello 어떤 관계가 있습니까?

* [메트릭에서 PercentThrottlingError의 증가]
* [메트릭에서 PercentTimeoutError의 증가]
* [메트릭에서 PercentNetworkError가 증가하는 것으로 표시됨]

---
 클라이언트 응용 프로그램이 저장소 서비스에서 HTTP 4XX(예: 404) 응답을 받는 경우

* [HTTP 403 (금지 됨) 메시지를 받고 hello 클라이언트]
* [hello 클라이언트에서 HTTP 404 (찾을 수 없음) 메시지를 받는]
* [hello 클라이언트 HTTP 409 (충돌) 메시지 수신]

---
[메트릭에서 낮은 PercentSuccess 또는 분석 로그 항목 된 작업이 있을 ClientOtherErrors의 트랜잭션 상태]

---
[용량 메트릭에 예기치 않은 저장소 용량 사용 증가가 표시됨]

---
[많은 수의 VHD가 연결된 가상 컴퓨터가 예기치 않게 다시 부팅됨]

---
[개발 또는 테스트에 대 한 hello 저장소 에뮬레이터를 사용 하 여 문제 발생]

---
[Hello Azure SDK for.NET 설치에 문제가 발생 하는]

---
[저장소 서비스에서 다른 문제가 발생함]

---
### <a name="metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency"></a>메트릭에서 AverageE2ELatency는 높게 표시되고 AverageServerLatency는 낮게 표시됨
hello에서 아래 그림 hello [Azure 포털](https://portal.azure.com) 여기서 hello 예가 나와 모니터링 도구 **AverageE2ELatency** hello 보다 훨씬 높은 **AverageServerLatency**.

![][4]

Hello 저장소 서비스에만 hello 메트릭을 계산 하는 참고 **AverageE2ELatency** 성공한 요청 수 및 달리 **AverageServerLatency**, hello 클라이언트에서는 toosend hello hello 시간을 포함 데이터 및 승인을 hello 저장소 서비스에서 수신 합니다. 따라서 간에 차이가 **AverageE2ELatency** 및 **AverageServerLatency** 수 toorespond, 또는 due tooconditions hello 네트워크에 대 한 느린 인해 toohello 클라이언트 응용 프로그램 중 하나입니다.

> [!NOTE]
> 볼 수 있습니다 **E2ELatency** 및 **ServerLatency** hello 저장소 로깅에서는 개별 저장소 작업에 대 한 데이터를 기록 합니다.
> 
> 

#### <a name="investigating-client-performance-issues"></a>클라이언트 성능 문제 조사
느리게 응답 하는 hello 클라이언트에 대 한 가능한 이유는 제한 된 수의 사용 가능한 연결 또는 스레드, CPU, 메모리 또는 네트워크 대역폭 등의 리소스 부족 또는 포함 됩니다. Hello 클라이언트 코드 toobe 보다 효율적인 (예를 사용 하 여 비동기 호출 toohello 저장소 서비스)를 수정 하 여 또는 더 큰 가상 컴퓨터 (더 많은 코어와 더 많은 메모리) 사용 하 여 수 tooresolve hello 문제를 수 있습니다.

Hello Nagle 알고리즘 hello 테이블 및 큐 서비스에 대 한 높은 일으킬 수도 있습니다 **AverageE2ELatency** 너무 비교할 때**AverageServerLatency**: 자세한 내용은 참조를 게시 하는 hello [Nagle 알고리즘은 작은 요청으로 친숙 하지](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/06/25/nagle-s-algorithm-is-not-friendly-towards-small-requests.aspx)합니다. Hello를 사용 하 여 코드에서 hello Nagle 알고리즘을 해제할 수 있습니다 **ServicePointManager** hello 클래스 **System.Net** 네임 스페이스입니다. 호출 toohello 테이블 또는 열이 이미 있는 연결에는 영향을 주지 않는 이후 응용 프로그램에서 큐 서비스 전에이 작업을 수행 해야 합니다. hello 다음 예제에서에서 가져온 hello **Application_Start** 작업자 역할에서 메서드.

```csharp
var storageAccount = CloudStorageAccount.Parse(connStr);
ServicePoint tableServicePoint = ServicePointManager.FindServicePoint(storageAccount.TableEndpoint);
tableServicePoint.UseNagleAlgorithm = false;
ServicePoint queueServicePoint = ServicePointManager.FindServicePoint(storageAccount.QueueEndpoint);
queueServicePoint.UseNagleAlgorithm = false;
```

Hello 클라이언트 쪽 로그 toosee 클라이언트 응용 프로그램을 제출 하는 요청 및 일반적인.NET에 대 한 확인 수와 관련 된 CPU,.NET 가비지 수집, 네트워크 사용률 또는 메모리 등의 클라이언트에 성능 병목 상태를 확인 해야 합니다. .NET 클라이언트 응용 프로그램 문제 해결을 시작하려면 [디버깅, 추적 및 프로파일링](http://msdn.microsoft.com/library/7fe0dd2y)을 참조하세요.

#### <a name="investigating-network-latency-issues"></a>네트워크 대기 시간 문제 조사
일반적으로, 종단 간 대기 시간이 긴 hello 네트워크로 인해 tootransient 조건 때문입니다. Wireshark 또는 Microsoft Message Analyzer와 같은 도구를 사용하여 일시적인 네트워크 문제와 영구적인 네트워크 문제(예: 패킷 삭제)를 모두 조사해야 합니다.

Wireshark tootroubleshoot 네트워크 문제를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여]."

Microsoft 메시지 분석기 tootroubleshoot 네트워크 문제를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여]."

### <a name="metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency"></a>낮은 AverageE2ELatency 및 낮은 AverageServerLatency 메트릭을 표시 하지만 hello 클라이언트에서 높은 대기 시간이 발생 합니다.
이 시나리오에서는 가장 가능성이 높은 원인 hello hello 저장소 서비스에 도달 하는 hello 저장소 요청에 지연이 하기 쉽습니다. 이유 hello 클라이언트의에서 요청을 하지 게 toohello blob 서비스를 통해 확인 해야 합니다.

요청을 보낼 지연 hello 클라이언트에 대 한 한 가지 가능한 이유는 제한 된 수의 사용 가능한 연결 또는 스레드 않는다는 것입니다.

Hello 클라이언트는 여러 번의 재시도 수행 되며 hello 좋다고 hello 이유를 조사 있는지 여부를 확인 해야 합니다. toodetermine hello 클라이언트에서 여러 번의 재시도 수행 하는지 여부를 다음을 할 수 있습니다.

* Hello 저장소 분석 로그를 검사 합니다. 여러 번의 재시도 발생 하 고 여러 작업과 나타납니다 동일한 클라이언트 요청 ID hello 하지만 다른 서버 요청 Id입니다.
* Hello 클라이언트 로그를 검사 합니다. 자세한 정보 로깅은 다시 시도가 발생된 것을 표시됩니다.
* 코드를 디버깅 하 고 hello의 hello 속성 확인 **OperationContext** hello 요청과 관련 된 개체입니다. Hello 작업을 다시 시도 하는 경우 hello **RequestResults** 속성이 여러 개의 고유 서버 요청 Id를 포함 합니다. Hello 시작을 확인 하 고 종료 각 요청에 대 한 시간 수도 있습니다. 자세한 내용은 참조 hello 부분의 코드 샘플에서는 hello [서버 요청 ID]합니다.

클라이언트 hello에에서 문제가 없는지, 패킷 손실 등 잠재적인 네트워크 문제를 조사 해야 합니다. Wireshark 또는 Microsoft 메시지 분석기 tooinvestigate 네트워크 문제 등의 도구를 사용할 수 있습니다.

Wireshark tootroubleshoot 네트워크 문제를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여]."

Microsoft 메시지 분석기 tootroubleshoot 네트워크 문제를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여]."

### <a name="metrics-show-high-AverageServerLatency"></a>메트릭에서 AverageServerLatency가 높게 표시됨
높음 hello 경우에서 **AverageServerLatency** blob 다운로드 요청에 대 한 저장소 로깅을 기록 toosee hello 같은 blob (또는 blob의 설정)에 대 한 반복 된 요청이 없는 경우 hello를 사용 해야 합니다. Blob에 대 한 요청을 업로드, 어떤 블록 크기 hello 클라이언트가 사용 하는 기능을 검토해 (예를 들어 블록에는 크기의 64k hello 읽고 하지 않는 한 오버 헤드가 발생할 수 있습니다 미만을 64k 보다 작은 청크로), 여러 클라이언트 업로드 하는 경우 및 블록 toohello 동일한 동시에 blob 수입니다. 급격히 증가 하는 두 번째 확장성 목표 당 hello 초과 될 요청 수가 hello에 대 일 분 메트릭을 확인 해야: 참조 "[메트릭에서 PercentTimeoutError의 증가]."

상위 표시 되는 경우 **AverageServerLatency** blob 다운로드 요청에 대 한 blob 또는 blob 집합이 동일한 요청 hello 반복 되는 경우 다음 Azure 캐시를 사용 하 여 이러한 blob를 캐싱 하거나 hello Azure 콘텐츠 배달 CDN (네트워크)입니다. 업로드 요청에 대 한 큰 블록 크기를 사용 하 여 hello 처리량을 향상 시킬 수 있습니다. 쿼리 tootables에 대 한 클라이언트 쪽에 캐싱 가능한 tooimplement는 hello 동일 쿼리 작업 하 고 여기서 hello를 수행 하는 클라이언트에서 데이터는 자주 변경 되지 합니다.

높은 **AverageServerLatency** 값 잘못 디자인 된 테이블의 징후가 될 수도 있습니다 또는 검사 작업의 결과 나 hello를 수행 하는 쿼리를 추가/앞에 추가 안티패턴 합니다. 자세한 내용은 "[메트릭에서 PercentThrottlingError의 증가]"을 참조하세요.

> [!NOTE]
> [Microsoft Azure 저장소 성능 및 확장성 검사 목록](storage-performance-checklist.md)에서 포괄적 성능 및 확장성 검사 목록을 확인할 수 있습니다.
> 
> 

### <a name="you-are-experiencing-unexpected-delays-in-message-delivery"></a>큐에서 메시지 배달 중에 예기치 않은 대기 시간이 발생함
Hello 시간 사이는 지연이 발생 하는 경우에 메시지 tooa 큐와 hello 시간 hello 큐에서 사용할 수 있는 tooread 막대로 추가 하는 응용 프로그램 후 hello 단계 toodiagnose hello 문제 다음을 수행 해야 합니다.

* Hello 응용 프로그램 hello 메시지 toohello 큐 추가 성공적으로 하는 것을 확인 합니다. Hello 응용 프로그램 hello 다시 시도 하지 않습니다는 확인 **AddMessage** 메서드를 여러 번 성공 하기 전에. hello 저장소 클라이언트 라이브러리 로그 저장소 작업의 모든 반복된 재시도 표시 됩니다.
* hello 메시지 toohello 큐와 hello 메시지를 사용 하면 hello 큐에서 읽는 hello 작업자 역할은 처리에서 지연을 처럼 표시를 추가 하는 hello 작업자 역할 간에 일정 없음 시계를 확인 합니다.
* Hello 메시지 hello 큐에서 읽는 hello 작업자 역할이 실패 하는지 확인 합니다. 큐 클라이언트 hello를 호출 하는 경우 **GetMessage** 승인을 toorespond 하지만 실패 하는 메서드, hello 메시지 hello까지 hello 큐에 유지 됩니다 **invisibilityTimeout** 기간이 만료 됩니다. 이 시점에서 hello 메시지를 다시 처리 하기 위해 사용할 수 있습니다.
* 시간이 지남에 따라 hello 큐 길이 증가 하 고 확인 합니다. 이 작업 자가 사용 가능한 tooprocess 충분 한 다른 작업 자가 hello 큐에 배치 되는 모든 hello 메시지 하지 않은 경우 발생할 수 있습니다. 또한 hello 메트릭 toosee 삭제 요청이 실패 하 고 hello 큐에서 제거한 횟수를 나타내는 메시지에 반복 실패 한 시도 toodelete hello 메시지를 확인 해야 합니다.
* 큐 작업에 예상 보다 높은 hello 저장소 로깅 로그를 검사 **E2ELatency** 및 **ServerLatency** 평소 보다 긴 시간 동안에 따른 값입니다.

### <a name="metrics-show-an-increase-in-PercentThrottlingError"></a>메트릭에서 PercentThrottlingError가 증가하는 것으로 표시됨
저장소 서비스의 hello 확장성 대상을 초과 하면 제한 오류가 발생 합니다. hello 저장소 서비스는이 tooensure 하는 단일 클라이언트나 테 넌 트의 hello 부담 hello 서비스를 사용할 수 있습니다. 저장소 계정의 확장성 목표와 저장소 계정 내 파티션의 성능 목표에 대한 자세한 내용은 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.

경우 hello **PercentThrottlingError** 메트릭에 제한 오류로 실패 하는 요청의 hello 백분율에 증가 하는 표시 tooinvestigate 두 상황 중 하나 사용 해야 합니다.

* [일시적인 PercentThrottlingError 증가]
* [영구적인 PercentThrottlingError 증가]

증가 **PercentThrottlingError** hello hello 저장소 요청 수가 증가 같거나 때 처음에 부하 테스트 응용 프로그램에서 자주 발생 합니다. 이 또한에서 명확 하 게 "503 서버 사용 중" 또는 "500 작업 Timeout" HTTP 상태 메시지에서 저장소 작업으로 hello 클라이언트입니다.

#### <a name="transient-increase-in-PercentThrottlingError"></a>일시적인 PercentThrottlingError 증가
하는 경우의 hello 값에 스파이크가 있으면 **PercentThrottlingError** hello 응용 프로그램에 대 한 작업량이 많은 기간과 함께 일치 하는, (하지 선형)는 지 수 백오프 전략 재시도 대 한 클라이언트를 구현 해야 합니다:이 hello 파티션에 hello 즉시 부하 줄어들고 프로그램 응용 프로그램 toosmooth 트래픽 급증 아웃는 데 도움이 될 합니다. Tooimplement 다시 시도 정책을 사용 하 여 저장소 클라이언트 라이브러리를 hello 하는 방법에 대 한 자세한 내용은 참조 [Microsoft.WindowsAzure.Storage.RetryPolicies Namespace](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.retrypolicies.aspx)합니다.

> [!NOTE]
> Hello 값에 스파이크가 있으면 나타날 **PercentThrottlingError** hello 응용 프로그램에 대 한 작업량이 많은 기간과 일치 하지 않는: hello 가장 가능성이 높은 원인 여기는 파티션을 tooimprove 부하를 이동 하는 hello 저장소 서비스 균형 조정 합니다.
> 
> 

#### <a name="permanent-increase-in-PercentThrottlingError"></a>영구적인 PercentThrottlingError 증가
값이 높은 일관 되 게 표시 되는 경우 **PercentThrottlingError** 응용 프로그램에서 테스트 한 영구 증가 하므로 트랜잭션 볼륨 또는 초기 부하를 수행 하는 경우 다음 tooevaluate를 해야 합니다 응용 프로그램 저장소 파티션을 사용 하는 방법 및 저장소 계정에 대 한 hello 확장성 목표에 도달 하는지 여부입니다. 예를 들어 제한 (계산 하는 하나의 파티션으로) 큐에는 오류가 나타나면 다음 사용을 고려해 야 추가 큐 toospread hello 트랜잭션을 여러 파티션에서 합니다. 제한 오류 테이블에는 표시 하는 경우 필요한 tooconsider 다른 파티션 구성표 toospread를 사용 하 여 트랜잭션을 여러 파티션에서 보다 넓은 범위의 파티션 키 값을 사용 하 여 합니다. 한 가지 일반적인 원인은이 문제는 hello 앞에 추가 하 고 추가 안티패턴 hello 파티션 키로 hello 날짜를 선택 하 고 다음 특정 날짜의 모든 데이터가 tooone 파티션 쓰여집니다 있는: 로드가이 될 수 있습니다 쓰기 병목 현상이 발생 합니다. 따라서 다른 파티션 디자인을 사용하거나 Blob 저장소를 사용하는 것이 더 효율적인 해결 방법인지 평가해야 합니다. 트래픽이 급증 결과로 발생 하 고 요청 패턴을 다듬기 방법을 조사 hello 제한을 확인 해야 합니다.

여러 파티션에서 거래를 배포 하는 경우 hello 저장소 계정에 대해 설정 된 hello 확장성 제한을 알아야 계속 합니다. 예를 들어 초당 2, 000 1KB 메시지 각 처리 hello 최대 10 개 큐를 사용한 경우 됩니다 hello에 hello 저장소 계정에 대 한 초당 20, 000 메시지의 전체 제한 합니다. 초당 20, 000 개 이상의 엔터티 tooprocess 해야 할 경우 여러 저장소 계정을 사용 하는 것이 좋습니다. 하면도 명심 해야 hello 크기에 대 한 요청 중 한 엔터티 hello 저장소 서비스 클라이언트를 제한 하는 경우에 영향이: 큰 요청 및 엔터티를 설정한 경우 있습니다 수 스로틀할 수 더 빨리 합니다.

비효율적인 쿼리 디자인 테이블 파티션에 대 한 toohit hello 확장성 제한도 발생할 수 있습니다. 예를 들어 파티션의 hello 엔터티 1 %만 선택 하는 하지만 파티션의 모든 hello 엔터티를 검색 하는 필터를 사용 하 여 쿼리 tooaccess 각 엔터티에 필요 합니다. 해당 파티션의; 트랜잭션의 총 수 hello 진행할 읽는 모든 엔터티 수 있습니다. 따라서 hello 확장성 목표를 쉽게 도달할 수 있습니다.

> [!NOTE]
> 성능 테스트를 통해 응용 프로그램의 비효율적인 쿼리 디자인을 확인해야 합니다.
> 
> 

### <a name="metrics-show-an-increase-in-PercentTimeoutError"></a>메트릭에서 PercentTimeoutError가 증가하는 것으로 표시됨
메트릭에서 저장소 서비스 중 하나의 **PercentTimeoutError**가 증가하는 것으로 표시됨과 동시에, Hello에 이와 hello 클라이언트 저장소 작업에서 많은 양의 "500 작업 Timeout" HTTP 상태 메시지를 받습니다.

> [!NOTE]
> 파티션 tooa 새 서버를 이동 하 여 잔액 요청의 부하를 hello 저장소 서비스를 일시적으로 시간 초과 오류가 표시 될 수 있습니다.
> 
> 

hello **PercentTimeoutError** 메트릭을 메트릭에 따라 hello 집계 한 값: **ClientTimeoutError**, **AnonymousClientTimeoutError**,  **SASClientTimeoutError**, **ServerTimeoutError**, **AnonymousServerTimeoutError**, 및 **SASServerTimeoutError**합니다.

hello 서버 시간 초과 되어 hello 서버에 오류가 발생 합니다. hello 클라이언트 시간 초과가 발생 hello 서버에서 작업이 hello 클라이언트;에서 지정 된 hello 제한 시간을 초과 했기 때문에 로 인해 hello 저장소 클라이언트 라이브러리를 사용 하는 클라이언트 hello를 사용 하 여 작업에 대 한 시간 초과 설정할 수는 예를 들어 **ServerTimeout** hello 속성 **QueueRequestOptions** 클래스입니다.

서버 제한 시간을 계속 조사 해야 하는 hello 저장소 서비스의 문제를 나타냅니다. Hello 확장성 제한 tooidentify hello 서비스에 대 한이 문제를 일으킬 수 있는 트래픽이 스파이크가 적중할 경우 메트릭 toosee를 사용할 수 있습니다. Due 수도 hello 문제가 중단 되 면 hello 서비스의 활동 tooload 분산 합니다. Hello 문제가 지속적이 고 hello 서비스의 hello 확장성 제한에 도달 하는 응용 프로그램에서 발생 시 키 지는 경우 지원 문제를 발생 시켜야 합니다. 클라이언트 시간 제한에 대 한 hello timeout hello 클라이언트에서 tooan 적절 한 값 설정 되 고 변경 hello 제한 시간 값 중 하나가 hello 클라이언트에서 설정 하거나에 대 한 hello 저장소 서비스에 대 한 hello 작업의 hello 성능을 개선 하는 방법을 조사를 결정 해야 테이블 쿼리를 최적화 하거나 메시지의 hello 크기를 줄여 예입니다.

### <a name="metrics-show-an-increase-in-PercentNetworkError"></a>메트릭에서 PercentNetworkError가 증가하는 것으로 표시됨
메트릭에서 저장소 서비스 중 하나의 **PercentNetworkError** 가 증가하는 것으로 표시됩니다. hello **PercentNetworkError** 메트릭을 메트릭에 따라 hello 집계 한 값: **NetworkError**, **AnonymousNetworkError**, 및  **SASNetworkError**합니다. 이 hello 저장소 서비스는 hello 클라이언트에서 저장소를 요청 하는 경우 네트워크 오류를 감지할 때 발생 합니다.

hello이 오류의 가장 일반적인 이유는 클라이언트 hello 저장소 서비스에 시간 제한이 만료 되기 전에 연결을 끊는 중입니다. 프로그램 클라이언트 toounderstand hello 저장소 서비스에서 hello 클라이언트 연결이 끊어지면 이유 및 시기에 hello 코드를 조사 해야 합니다. Wireshark, Microsoft 메시지 분석기 또는 Tcping tooinvestigate 네트워크 연결 문제 hello 클라이언트에서 사용할 수 있습니다. 이러한 도구는 hello에 설명 된 [부록]합니다.

### <a name="the-client-is-receiving-403-messages"></a>HTTP 403 (금지 됨) 메시지를 받고 hello 클라이언트
한 가지 가능한 원인은 (다른 원인이 클록 스큐, 잘못 된 키를 포함 하 고 비어 있지만 저장소 요청을 보낼 때 해당 hello 클라이언트는 만료 된 SAS 공유 액세스 서명 ()을 사용 하는 클라이언트 응용 프로그램이 HTTP 403 (사용할 수 없음) 오류를 throw 하는 경우 헤더)입니다. 만료 된 SAS 키 hello 원인인 경우 hello 서버 쪽 저장소 로깅 로그 데이터의 모든 항목 표시 되지 않습니다. hello 아래 표에 나와 hello 이러한 문제가 발생할 보여 주는 저장소 클라이언트 라이브러리에서 생성 하는 hello 클라이언트 쪽 로그에서 샘플.

| 원본 | 자세한 정도 | 자세한 정도 | 클라이언트 요청 ID | 작업 텍스트 |
| --- | --- | --- | --- | --- |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab-… |위치 모드 PrimaryOnly에 대해 위치 Primary로 작업을 시작하는 중입니다. |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab -… |Toohttps://domemaildist.blob.core.windows.netazureimblobcontainer/blobCreatedViaSAS.txt?sv=2014-02-14 요청 시작 동기&amp;sr = c&amp;si mypolicy =&amp;sig OFnd4Rd7z01fIvh %2BmcR6zbudIH2F5Ikm % = 2FyhNYZEmJNQ %3D&amp;api-version = 2014-02-14입니다. |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab -… |응답을 기다리는 중입니다. |
| Microsoft.WindowsAzure.Storage |Warning |2 |85d077ab -… |응답을 기다리는 동안 예외가 발생 했습니다: 오류를 반환 하는 원격 서버 hello: (403) 사용할 수 없음... |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab -… |응답을 받았습니다. 상태 코드 = 403, 요청 ID = 9d67c64a-64ed-4b0d-9515-3b14bbcdc63d, Content-MD5 = , ETag = . |
| Microsoft.WindowsAzure.Storage |Warning |2 |85d077ab -… |Hello 작업 중에 throw 된 예외: 원격 서버 hello 오류가 반환 되었습니다: (403) 사용할 수 없음... |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab -… |Hello 작업을 다시 시도해 야 하는 경우 확인 중입니다. 다시 시도 횟수 = 0, HTTP 상태 코드 403, 예외 = = hello 원격 서버에서 오류를 반환 합니다. (403) 사용할 수 없음... |
| Microsoft.WindowsAzure.Storage |정보 |3 |85d077ab -… |다음 위치 hello hello 위치 모드에 따라 tooPrimary 설정 되었습니다. |
| Microsoft.WindowsAzure.Storage |오류 |1 |85d077ab -… |다시 시도 정책에서 다시 시도를 허용하지 않았습니다. Hello 원격 서버와 함께 실패 오류를 반환 했습니다: (403) 사용할 수 없음. |

이 시나리오에서는 hello 클라이언트 hello 토큰 toohello 서버에서 전송 하기 전에 hello SAS 토큰이 곧 만료 됩니다. 이유를 조사 해야 합니다.

* 일반적으로 클라이언트 toouse에 대 한 SAS를 즉시 만들 때 시작 시간을 설정 하지 않아야 합니다. Hello 저장소 서비스 tooreceive 아직 유효 하지 않은 SAS에 대 한 것일 수 있는 작은 hello SAS를 사용 하 여 생성 하는 hello 호스트 간의 시계 차이점 현재 시간과 hello 저장소 서비스를 hello 합니다.
* SAS에 대해 매우 짧은 만료 시간을 설정해서는 안 됩니다. 다시 생성 하는 hello 호스트 작은 시계가 차이점 hello SAS 및 저장소 서비스 hello tooa SAS 발생할 수 있습니다 분명히 예상 보다 일찍 만료 합니다.
* Hello SAS 키의 버전 매개 변수를 hello지 않습니다 (예를 들어 **sv = 2015-04-05**) 일치 hello 버전의 저장소 클라이언트 라이브러리를 사용 하는 hello? 항상 최신 버전의 hello hello를 사용 하는 것이 좋습니다 [저장소 클라이언트 라이브러리](https://www.nuget.org/packages/WindowsAzure.Storage/)합니다.
* 저장소 액세스 키를 다시 생성하면 기존 SAS 토큰이 무효화될 수 있습니다. SAS 토큰에 대 한 클라이언트 응용 프로그램 toocache 긴 만료 시간을 사용 하 여 생성 하는 경우 문제가 수 있습니다.

Hello 저장소 클라이언트 라이브러리 toogenerate SAS 토큰을 사용 하는 다음 경우 쉽게 toobuild 유효한 토큰입니다. 그러나 hello 저장소 REST API를 사용 하 고 hello SAS 토큰을 직접 생성 하는 경우 주의 깊게 읽어야 hello 항목 [공유 액세스 서명으로 액세스 위임](http://msdn.microsoft.com/library/azure/ee395415.aspx)합니다.

### <a name="the-client-is-receiving-404-messages"></a>hello 클라이언트에서 HTTP 404 (찾을 수 없음) 메시지를 받는
Hello 서버에서 HTTP 404 (찾을 수 없음) 메시지를 수신 하는 hello 클라이언트 응용 프로그램, 즉, 해당 hello 개체 hello 클라이언트 시도 했습니다 (예: 엔터티, 테이블, blob, 컨테이너 또는 큐) toouse hello 저장소 서비스에 존재 하지 않습니다. 이러한 현상은 다음과 같은 여러 가지 이유로 인해 발생합니다.

* [클라이언트 hello 또는 다른 프로세스를 이전에 삭제 hello 개체]
* [SAS(공유 액세스 서명) 권한 부여 문제]
* [클라이언트 쪽 JavaScript 코드가 권한 tooaccess hello 개체를 가질 수 없습니다.]
* [네트워크 오류]

#### <a name="client-previously-deleted-the-object"></a>클라이언트 hello 또는 다른 프로세스를 이전에 삭제 hello 개체
Tooread, 업데이트 또는 삭제 데이터는 일반적으로 저장소 서비스에서 클라이언트 hello 시도 시나리오 hello 서버 쪽에서 쉽게 tooidentify hello 개체에 hello 저장소 서비스에서 삭제 하는 이전 작업을 기록 합니다. 대개 hello 로그 데이터를 다른 사용자나 프로세스 삭제 된 hello 개체를 보여 줍니다. Hello 서버 쪽 저장소 로깅 로그에 hello 작업 유형 및 요청-개체-키 열 표시 클라이언트 개체를 삭제 하는 경우.

클라이언트가 tooinsert 개체 시도 하는 hello 시나리오에서는 것 어려울 수 있습니다 즉시 hello 클라이언트는 새 개체를 만드는 것이 인해 HTTP 404 (찾을 수 없음) 응답에서 하는 이유입니다. 그러나 hello 클라이언트는 클라이언트 hello가 수 toofind 큐 있어야 하는 메시지를 만드는 경우 수 toofind hello blob 컨테이너 수 및 hello 클라이언트는 행을 추가 하는 경우 다음 조건을 충족 해야 하는 blob를 만드는 경우 수 toofind hello 테이블 이어야 합니다.

세분화 된 이해 hello 클라이언트가 보내면 특정 요청 toohello 저장소 서비스는 hello 저장소 클라이언트 라이브러리 toogain hello 클라이언트 쪽 로그를 사용할 수 있습니다.

hello hello 저장소 클라이언트 라이브러리에서 생성 하는 클라이언트 쪽 로그는 다음 문제를 보여 줍니다 hello hello 클라이언트 hello blob를 만드는 것에 대 한 hello 컨테이너를 찾을 수 없는 경우. 이 로그 저장소 작업을 수행 하는 hello에 대 한 세부 정보에 포함 됩니다.

| 요청 ID | 작업 |
| --- | --- |
| 07b26a5d-... |**DeleteIfExists** 메서드 toodelete hello blob 컨테이너입니다. 이 작업에 포함 된 메모는 **H e a d** toocheck hello 컨테이너의 존재 여부 hello에 대 한 요청입니다. |
| e2d06d78… |**경고는 CreateIfNotExists** 메서드 toocreate hello blob 컨테이너입니다. 이 작업에 포함 된 메모는 **H e a d** hello 컨테이너의 hello 있는지 여부를 확인 하는 요청입니다. hello **H e a d** 404 메시지를 반환 하지만 계속 합니다. |
| de8b1c3c-... |**UploadFromStream** 메서드 toocreate hello blob입니다. hello **배치** 404 메시지와 함께 요청이 실패 |

로그 항목:

| 요청 ID | 작업 텍스트 |
| --- | --- |
| 07b26a5d-... |동기 요청 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer를 시작합니다. |
| 07b26a5d-... |StringToSign = HEAD............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:11 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |응답을 기다리는 중입니다. |
| 07b26a5d-... |응답을 받았습니다. 상태 코드 = 200, 요청 ID = eeead849-...Content-MD5 = , ETag = &quot;0x8D14D2DC63D059B&quot; |
| 07b26a5d-... |응답 헤더는 hello 나머지 hello 작업으로 계속 성공적으로 처리 되었습니다. |
| 07b26a5d-... |응답 본문을 다운로드하는 중입니다. |
| 07b26a5d-... |작업이 완료되었습니다. |
| 07b26a5d-... |동기 요청 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer를 시작합니다. |
| 07b26a5d-... |StringToSign = DELETE............x-ms-client-request-id:07b26a5d-....x-ms-date:Tue, 03 Jun 2014 10:33:12    GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| 07b26a5d-... |응답을 기다리는 중입니다. |
| 07b26a5d-... |응답을 받았습니다. 상태 코드 = 202, 요청 ID = 6ab2a4cf-..., Content-MD5 = , ETag = . |
| 07b26a5d-... |응답 헤더는 hello 나머지 hello 작업으로 계속 성공적으로 처리 되었습니다. |
| 07b26a5d-... |응답 본문을 다운로드하는 중입니다. |
| 07b26a5d-... |작업이 완료되었습니다. |
| e2d06d78-... |비동기 요청 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer를 시작합니다.</td> |
| e2d06d78-... |StringToSign = HEAD............x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |응답을 기다리는 중입니다. |
| de8b1c3c-... |동기 요청 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer/blobCreated.txt를 시작합니다. |
| de8b1c3c-... |StringToSign = PUT...64.qCmF+TQLPhq/YYK50mP9ZQ==........x-ms-blob-type:BlockBlob.x-ms-client-request-id:de8b1c3c-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer/blobCreated.txt. |
| de8b1c3c-... |Toowrite 요청 데이터를 준비 합니다. |
| e2d06d78-... |응답을 기다리는 동안 예외가 발생 했습니다: 오류를 반환 하는 원격 서버 hello: (404) 찾을 수 없습니다. |
| e2d06d78-... |응답을 받았습니다. 상태 코드 = 404, 요청 ID = 353ae3bc-..., Content-MD5 = , ETag = . |
| e2d06d78-... |응답 헤더는 hello 나머지 hello 작업으로 계속 성공적으로 처리 되었습니다. |
| e2d06d78-... |응답 본문을 다운로드하는 중입니다. |
| e2d06d78-... |작업이 완료되었습니다. |
| e2d06d78-... |비동기 요청 toohttps://domemaildist.blob.core.windows.net/azuremmblobcontainer를 시작합니다. |
| e2d06d78-... |StringToSign = PUT...0.........x-ms-client-request-id:e2d06d78-....x-ms-date:Tue, 03 Jun 2014 10:33:12 GMT.x-ms-version:2014-02-14./domemaildist/azuremmblobcontainer.restype:container. |
| e2d06d78-... |응답을 기다리는 중입니다. |
| de8b1c3c-... |요청 데이터를 쓰는 중입니다. |
| de8b1c3c-... |응답을 기다리는 중입니다. |
| e2d06d78-... |응답을 기다리는 동안 예외가 발생 했습니다: hello 원격 서버에 오류가 반환 되었습니다. (409) 충돌... |
| e2d06d78-... |응답을 받았습니다. 상태 코드 = 409, 요청 ID = c27da20e-..., Content-MD5 = , ETag = . |
| e2d06d78-... |오류 응답 본문을 다운로드하는 중입니다. |
| de8b1c3c-... |응답을 기다리는 동안 예외가 발생 했습니다: 오류를 반환 하는 원격 서버 hello: (404) 찾을 수 없습니다. |
| de8b1c3c-... |응답을 받았습니다. 상태 코드 = 404, 요청 ID = 0eaeab3e-..., Content-MD5 = , ETag = . |
| de8b1c3c-... |Hello 작업 중에 throw 된 예외: 원격 서버 hello 오류가 반환 되었습니다: (404) 찾을 수 없습니다. |
| de8b1c3c-... |다시 시도 정책에서 다시 시도를 허용하지 않았습니다. Hello 원격 서버와 함께 실패 오류를 반환 했습니다: (404) 찾을 수 없습니다. |
| e2d06d78-... |다시 시도 정책에서 다시 시도를 허용하지 않았습니다. Hello 원격 서버와 함께 실패 오류가 반환 되었습니다. (409) 충돌... |

이 예제에서는 hello 로그 표시는 hello 클라이언트 hello의 요청을 인터리빙은 **경고는 CreateIfNotExists** hello의 hello 요청을 사용 하 여 메서드 (요청 id e2d06d78...) **UploadFromStream** 메서드 ( de8b1c3c-...); 이 hello 클라이언트 응용 프로그램은 이러한 메서드를 비동기적으로 호출 하기 때문에 발생 합니다. 만들 수 있다는 hello 컨테이너 tooupload 시도 하기 전에 모든 데이터 tooa blob 해당 컨테이너에서 hello 클라이언트 tooensure hello 비동기 코드를 수정 해야 합니다. 모든 컨테이너를 미리 만드는 것이 가장 좋습니다.

#### <a name="SAS-authorization-issue"></a>SAS(공유 액세스 서명) 권한 부여 문제
Hello 클라이언트 응용 프로그램 시도 toouse hello hello 작업에 대 한 필요한 사용 권한을 포함 하지 않는 SAS 키를 hello 저장소 서비스에서 HTTP 404 (찾을 수 없음) 메시지 toohello 클라이언트를 반환 합니다. Hello에서 동일한 시간, 표시 됩니다는 0이 아닌 값에 대 한 **SASAuthorizationError** hello 메트릭에서.

다음 표에서 hello hello 저장소 로깅 로그 파일에서 예제 서버 쪽 로그 메시지를 보여 줍니다.

| 이름 | 값 |
| --- | --- |
| 요청 시작 시간 | 2014-05-30T06:17:48.4473697Z |
| 작업 유형     | GetBlobProperties            |
| 요청 상태     | SASAuthorizationError        |
| HTTP 상태 코드   | 404                          |
| 인증 유형| Sas                          |
| 서비스 유형       | Blob                         |
| 요청 URL        | https://domemaildist.blob.core.windows.net/azureimblobcontainer/blobCreatedViaSAS.txt |
| nbsp;              |   ?sv=2014-02-14&sr=c&si=mypolicy&sig=XXXXX&;api-version=2014-02-14 |
| 요청 ID 헤더  | a1f348d5-8032-4912-93ef-b393e5252a3b |
| 클라이언트 요청 ID  | 2d064953-8436-4ee0-aa0c-65cb874f7929 |


클라이언트 응용 프로그램에 대 한 권한을 부여 되지 않은 작업 tooperform가 시도 하는 이유를 조사 해야 합니다.

#### <a name="JavaScript-code-does-not-have-permission"></a>클라이언트 쪽 JavaScript 코드가 권한 tooaccess hello 개체를 가질 수 없습니다.
JavaScript 클라이언트를 사용 하는 hello 저장소 서비스에서 HTTP 404 메시지를 반환 하는 경우 다음 hello 브라우저에서 JavaScript 오류 hello에 대 한 확인 합니다.

```
SEC7120: Origin http://localhost:56309 not found in Access-Control-Allow-Origin header.
SCRIPT7002: XMLHttpRequest: Network Error 0x80070005, Access is denied.
```

> [!NOTE]
> 클라이언트 쪽 JavaScript 문제를 해결할 때 hello 브라우저와 hello 저장소 서비스 간에 교환 되는 Internet Explorer tootrace hello 메시지에 hello F12 개발자 도구를 사용할 수 있습니다.
> 
> 

Hello 웹 브라우저 hello를 구현 하기 때문에 이러한 오류가 발생 [동일 원본 정책](http://www.w3.org/Security/wiki/Same_Origin_Policy) 에서 웹 페이지 hello 도메인 hello 페이지에서 다른 도메인에는 API를 호출 하지 않도록 설정 하는 보안 제한을 제공 합니다.

JavaScript 문제 hello 주위 toowork, hello 저장소 서비스 hello 클라이언트가 액세스에 대 한 교차 원본 리소스 공유 (CORS)을 구성할 수 있습니다. 자세한 내용은 [Azure 저장소 서비스에 대한 CORS(크로스-원본 자원 공유) 지원](http://msdn.microsoft.com/library/azure/dn535601.aspx)을 참조하세요.

아래의 코드 예제는 hello 방법을 tooconfigure blob 서비스 tooallow blob 저장소 서비스에 blob hello Contoso 도메인 tooaccess에서에서 실행 되는 JavaScript를 보여 줍니다.

```csharp
CloudBlobClient client = new CloudBlobClient(blobEndpoint, new StorageCredentials(accountName, accountKey));
// Set hello service properties.
ServiceProperties sp = client.GetServiceProperties();
sp.DefaultServiceVersion = "2013-08-15";
CorsRule cr = new CorsRule();
cr.AllowedHeaders.Add("*");
cr.AllowedMethods = CorsHttpMethods.Get | CorsHttpMethods.Put;
cr.AllowedOrigins.Add("http://www.contoso.com");
cr.ExposedHeaders.Add("x-ms-*");
cr.MaxAgeInSeconds = 5;
sp.Cors.CorsRules.Clear();
sp.Cors.CorsRules.Add(cr);
client.SetServiceProperties(sp);
```

#### <a name="network-failure"></a>네트워크 오류
일부 경우에 손실 된 네트워크 패킷이 toohello 저장소 서비스 HTTP 404 메시지 toohello 클라이언트에 반환 될 수 있습니다. 예를 들어 클라이언트 응용 프로그램은 hello 테이블 서비스에서 엔터티를 삭제 하는 경우 표시 보고 저장소 예외를 throw 하는 hello 클라이언트는 "HTTP 404 (찾을 수 없음)" hello 테이블 서비스에서 상태 메시지입니다. Hello hello 테이블 저장소 서비스에는 테이블을 조사 하는 경우에 hello 서비스가 요청한 대로 hello 엔터티를 삭제 하는 것이 표시 됩니다.

클라이언트 hello에에서 hello 예외 정보 포함 hello 요청에 대 한 hello 테이블 서비스에서 할당 된 hello 요청 id (7e84f12d...): hello를 검색 하 여 hello 서버 쪽 저장소 로그에서이 정보 toolocate hello 요청 세부 정보를 사용할 수 있습니다  **요청 id 헤더** hello 로그 파일의 열입니다. Hello 메트릭 tooidentify 발생이 적은 다음 hello 시간 hello 메트릭을 기반으로 하는 hello 로그 파일을 검색 하는 같은 오류가 발생 했습니다.이 오류를 기록 하는 경우에 사용할 수 있습니다. 이 로그 항목은 삭제 hello을 "HTTP (404) 클라이언트 기타 오류" 상태 메시지와 함께 실패 했습니다. hello 동일한 로그 항목도 포함 hello 클라이언트 hello에 의해 생성 된 hello 요청 id **클라이언트 요청 id** 열 (813ea74f...).

hello 서버 쪽 로그에 hello로 또 다른 행도 포함 되어 동일한 **클라이언트 요청 id** 값 (813ea74f...)를 성공적으로 대 한 삭제 작업에 대 한 동일한 엔터티를 hello와에서 동일 hello 클라이언트입니다. 이 성공적으로 삭제 작업이 hello 실패 한 삭제 요청 되기 매우 바로 전에 발생을 했습니다.

이 시나리오의 hello 가능성이 가장 높은 원인은 성공 했지만 (아마도 인해 tooa 일시적인 네트워크 문제) hello 서버에서 승인을 받지 못했습니다는 hello 엔터티 toohello 테이블 서비스에 대 한 삭제 요청을 전송 하는 hello 클라이언트를입니다. 클라이언트 hello 다음 자동으로 다시 시도 hello 작업 (동일 hello를 사용 하 여 **클라이언트 요청 id**), 및 hello 엔터티가 이미 삭제 되었으므로이 다시 시도 실패 했습니다.

이 문제가 자주 발생 하는 경우 hello 클라이언트 hello 테이블 서비스의 tooreceive 승인을 실패 한 이유를 조사 해야 합니다. Hello 문제가 중단 되 면 hello "HTTP (404)를 찾을 수 없음" 오류 트래핑 되어야 하 고 hello 클라이언트 로그인 하지만 hello 클라이언트 toocontinue 허용 합니다.

### <a name="the-client-is-receiving-409-messages"></a>hello 클라이언트 HTTP 409 (충돌) 메시지 수신
hello 다음 표에 두 클라이언트 작업에 대 한 hello 서버 쪽 로그에서 추출: **DeleteIfExists** 즉시 올 **경고는 CreateIfNotExists** 동일한 blob 컨테이너 이름 hello를 사용 하 여 합니다. 각 클라이언트 작업으로 인해 전송 된 두 개의 요청 toohello 서버 먼저 참고는 **GetContainerProperties** 요청 toocheck hello 컨테이너가 있는지 뒤에는 hello **DeleteContainer** 또는  **CreateContainer** 요청 합니다.

| Timestamp | 작업 | 결과 | 컨테이너 이름 | 클라이언트 요청 ID |
| --- | --- | --- | --- | --- |
| 05:10:13.7167225 |GetContainerProperties |200 |mmcont |c9f52c89-… |
| 05:10:13.8167325 |DeleteContainer |202 |mmcont |c9f52c89-… |
| 05:10:13.8987407 |GetContainerProperties |404 |mmcont |bc881924-… |
| 05:10:14.2147723 |CreateContainer |409 |mmcont |bc881924-… |

hello hello 클라이언트 응용 프로그램의 코드를 삭제 하 고 hello를 사용 하 여 blob 컨테이너를 즉시 다시 이름이 같은: hello **경고는 CreateIfNotExists** 메서드 (클라이언트 요청 ID bc881924-...) hello HTTP 409 (충돌)와 함께 실패 결국 오류가 발생 했습니다. Blob 컨테이너, 테이블 또는 큐에 대 한 간단한 마침표 하기 전에 클라이언트를 삭제 하는 경우 hello 이름을 다시 사용할 수 있습니다.

hello 클라이언트 응용 프로그램 hello 삭제/다시 만들기 패턴은 일반적인 경우에 새 컨테이너를 만들 때마다 고유한 컨테이너 이름을 사용 해야 합니다.

### <a name="metrics-show-low-percent-success"></a>메트릭에 PercentSuccess가 낮게 표시되거나 분석 로그 항목에 트랜잭션 상태가 ClientOtherErrors 상태인 작업이 있음
hello **PercentSuccess** 메트릭을 hello % 성공 했습니다. HTTP 상태 코드에 따라 작업을 캡처합니다. 2XX의 상태 코드 작업과 계산 3XX, 4XX 및 5XX 범위에서 상태 코드를 사용 하 여 작업 실패 하 여 낮은 hello로 계산 되는 반면 성공으로 **PercentSucess** 메트릭 값입니다. Hello 서버 쪽 저장소 로그 파일의 이러한 작업의 트랜잭션 상태와 함께 기록 됩니다 **ClientOtherErrors**합니다.

것이 중요 한 toonote 이러한 작업이 성공적으로 완료 하 고 따라서 가용성 같은 다른 메트릭을 영향을 주지 않습니다. 정상적으로 실행되지만 작업 실패에 해당하는 HTTP 상태 코드를 표시하는 작업의 몇 가지 예는 다음과 같습니다.

* **ResourceNotFound** (없습니다 찾을 404), 예를 들어 GET에서 요청이 tooa blob는 없습니다.
* **ResouceAlreadyExists** (409 충돌)에서 예를 들어 한 **CreateIfNotExist** hello 리소스가 이미 존재 하는 작업입니다.
* **ConditionNotMet** (되지 수정 304), 예를 들어 클라이언트를 보낼 때와 같은 조건부 연산에서에서 한 **ETag** 값과 HTTP **없음-If-match** 헤더 toorequest 경우에만 이미지 hello 마지막 작업 이후에 업데이트 되었습니다.

Hello 저장소 서비스는 hello 페이지에서 반환 하는 일반적인 REST API 오류 코드 목록을 찾을 수 있습니다 [일반적인 REST API 오류 코드](http://msdn.microsoft.com/library/azure/dd179357.aspx)합니다.

### <a name="capacity-metrics-show-an-unexpected-increase"></a>용량 메트릭에 예기치 않은 저장소 용량 사용 증가가 표시됨
갑자기 표시 되는 경우 저장소 계정의 용량 사용량에 예기치 않은 변경 내용의 원인을 조사할 수 있습니다 hello 이유를 보면 첫 번째 가용성 메트릭을; hello 실패 한 삭제 요청 수가 증가 하는 hello 양의 있습니다 예상 된 toobe 공간 확보를 사용할 수 없습니다 (예상 대로 응용 프로그램 특정 정리 작업으로는 사용 하는 blob 저장소는 tooan 증가 이어질 수 예를 들어 예제에서는 공간을 확보 하기 위한 사용 되는 hello SAS 토큰 만료 때문에).

### <a name="you-are-experiencing-unexpected-reboots"></a>많은 수의 VHD가 연결된 가상 컴퓨터가 예기치 않게 다시 부팅됨
Azure 가상 컴퓨터 (VM)에 많은 hello에 있는 연결 된 Vhd의 경우 동일한 저장소 계정을 hello VM toofail 일으키는 개별 저장소 계정에 대 한 hello 확장성 목표를 초과할 수 있습니다. Hello 저장소 계정에 대 한 분 메트릭 hello를 확인 해야 (**TotalRequests**/**TotalIngress**/**TotalEgress**) 급격히 증가 하는 저장소 계정에 대 한 hello 확장성 목표를 초과합니다. Hello 섹션을 참조 "[메트릭에서 PercentThrottlingError의 증가]" 조정 여부를 결정 하기를 지 원하는 저장소 계정에서 발생에 대 한 합니다.

일반적으로 각 개별 입력 또는 출력 작업에서 가상 컴퓨터에서 VHD로 변환 너무**받기 페이지** 또는 **Put Page** hello 기본 페이지 blob에 대 한 작업입니다. 따라서 사용할 수 hello 예상 IOPS에 대 한 환경 tootune 있습니다 기준 사용할 수 있는 단일 저장소 계정에 응용 프로그램의 특정 동작 hello 개수 Vhd입니다. 단일 저장소 계정에 디스크를 40개 이하로 유지하는 것이 좋습니다. 참조 [Azure 저장소 확장성 및 성능 목표](storage-scalability-targets.md) hello 저장소 계정에 대 한 현재 확장성 목표의 자세한 특히 hello 유형의 저장소 계정에 대 한 hello 총 요청 속도 총 대역폭 사용 하는 .
저장소 계정에 대 한 hello 확장성 목표를 초과 하는 경우에 각 개별 계정에 여러 개의 다른 저장소 계정 tooreduce hello 활동에서 Vhd를 배치 해야 합니다.

### <a name="your-issue-arises-from-using-the-storage-emulator"></a>개발 또는 테스트에 대 한 hello 저장소 에뮬레이터를 사용 하 여 문제 발생
일반적으로 개발 하는 동안 hello 저장소 에뮬레이터를 사용 하 고 Azure 저장소 계정에 대 한 tooavoid hello 요구 사항 테스트 합니다. hello 일반적인 hello 저장소 에뮬레이터를 사용 하는 경우 발생할 수 있는 사항은 다음과 같습니다.

* [기능 "X" hello 저장소 에뮬레이터에서 작동 하지 않습니다.]
* [오류 "hello 값 hello HTTP 헤더 중 하나에 대 한이 형식이 잘못 된 hello" 때 저장소 에뮬레이터를 사용 하 여 hello]
* [Hello 저장소 에뮬레이터를 실행 하려면 관리자 권한이 필요]

#### <a name="feature-X-is-not-working"></a>기능 "X" hello 저장소 에뮬레이터에서 작동 하지 않습니다.
hello 저장소 에뮬레이터의 모든 hello hello 파일 서비스와 같은 hello Azure 저장소 서비스 기능을 지원 하지 않습니다. 자세한 내용은 참조 [개발 및 테스트에 Azure 저장소 에뮬레이터 사용 하 여 hello](storage-use-emulator.md)합니다.

저장소 hello 하는 기능에 대 한 에뮬레이터 지원, hello Azure 저장소 서비스를 사용 하 여 hello 클라우드에서 않습니다.

#### <a name="error-HTTP-header-not-correct-format"></a>오류 "hello 값 hello HTTP 헤더 중 하나에 대 한이 형식이 잘못 된 hello" 때 저장소 에뮬레이터를 사용 하 여 hello
와 같은 hello 로컬 저장소 에뮬레이터 및 메서드 호출에 대 한 hello 저장소 클라이언트 라이브러리를 사용 하는 응용 프로그램을 테스트할 **경고는 CreateIfNotExists** hello 오류와 함께 실패 "hello HTTP 헤더 중 하나에 대 한 hello 값에 없는 메시지 hello 올바른 형식입니다. " 해당 hello 나타냅니다 hello 저장소 에뮬레이터를 사용 하는 버전을 사용 하는 hello 저장소 클라이언트 라이브러리의 hello 버전을 지원 하지 않습니다. hello 헤더를 추가 하는 저장소 클라이언트 라이브러리 hello **x ms 버전** tooall hello 들어간다는 것을 요청 합니다. Hello 저장소 에뮬레이터의 hello hello 값을 인식 하지 않으므로 **x ms 버전** 헤더로, hello 요청을 거부 합니다.

Hello의 hello 저장소 라이브러리 클라이언트 로그 toosee hello 값을 사용할 수 **x-ms-버전 헤더** 는 전송 합니다. Hello hello 값을 볼 수 있습니다 **x-ms-버전 헤더** 클라이언트 응용 프로그램에서 Fiddler tootrace hello 요청을 사용 하는 경우.

이 시나리오는 일반적으로 설치 하 고 hello 저장소 에뮬레이터를 업데이트 하지 않고 hello 최신 버전의 hello 저장소 클라이언트 라이브러리를 사용 하는 경우에 발생 합니다. Hello 저장소 에뮬레이터의 hello 최신 버전을 설치 하거나 hello 에뮬레이터 대신 개발 및 테스트에 대 한 클라우드 저장소를 사용 해야 합니다.

#### <a name="storage-emulator-requires-administrative-privileges"></a>Hello 저장소 에뮬레이터를 실행 하려면 관리자 권한이 필요
Hello 저장소 에뮬레이터를 실행 하는 경우 관리자 자격 증명을 묻는 합니다. 처음으로 hello에 대 한 hello 저장소 에뮬레이터 초기화 하려는 경우에 발생 합니다. 관리자 권한 toorun 불필요 hello 저장소 에뮬레이터를 초기화 한 후 다시 합니다.

자세한 내용은 참조 [개발 및 테스트에 Azure 저장소 에뮬레이터 사용 하 여 hello](storage-use-emulator.md)합니다. 참고도 관리자 권한이 필요 하는 Visual Studio에서 저장소 에뮬레이터 hello 초기화할 수도 있습니다.

### <a name="you-are-encountering-problems-installing-the-Windows-Azure-SDK"></a>Hello Azure SDK for.NET 설치에 문제가 발생 하는
Tooinstall hello SDK을 시도할 때 로컬 컴퓨터에 있는 동안 tooinstall hello 저장소 에뮬레이터를 실패 합니다. hello 설치 로그 hello 메시지를 다음 중 하나를 포함 합니다.

* CAQuietExec: 오류: tooaccess 수 없습니다 SQL 인스턴스
* CAQuietExec: 오류: 수 없습니다 toocreate 데이터베이스

hello 원인에는 기존 LocalDB 설치는 문제입니다. 기본적으로 hello 저장소 에뮬레이터 hello Azure 저장소 서비스를 시뮬레이션 하는 경우 LocalDB toopersist 데이터를 사용 합니다. Hello tooinstall hello SDK를 시도 하기 전에 명령을 명령 프롬프트 창에서 다음을 실행 하 여 LocalDB 인스턴스를 다시 설정할 수 있습니다.

```
sqllocaldb stop v11.0
sqllocaldb delete v11.0
delete %USERPROFILE%\WAStorageEmulatorDb3*.*
sqllocaldb create v11.0
```

hello **삭제** 명령은 hello 저장소 에뮬레이터의 이전 설치에서 이전 데이터베이스 파일을 모두 제거 합니다.

### <a name="you-have-a-different-issue-with-a-storage-service"></a>저장소 서비스에서 다른 문제가 발생함
Hello 이전 문제 해결 섹션에서는 저장소 서비스는 hello 문제를 포함 하지 않은 경우 hello 접근 방식을 toodiagnosing 하 고 문제 해결을 채택 해야 합니다.

* 기준선에 예상된 된 동작에서 변경 된 경우 메트릭 toosee를 확인 합니다. Hello 메트릭에서 hello 문제는 일시적 이거나 영구적으로 적용 하 고 있는 저장소 작업 hello 문제에 영향을 주는 여부 수 toodetermine 될 수 있습니다.
* 발생 하는 모든 오류에 대 한 자세한 내용을 보려면 서버 쪽 로그 데이터를 검색할 toohelp hello 메트릭 정보를 사용할 수 있습니다. 이 정보는 hello 문제를 해결 하는 데 도움이 될 수 있습니다.
* Wireshark, Fiddler 등의 도구 및 클라이언트 응용 프로그램의 hello 저장소 클라이언트 라이브러리 클라이언트 쪽 로그 tooinvestigate hello 동작을 사용 하 여 hello 정보가 없으면 hello 서버 쪽 로그에 충분 한 tootroubleshoot hello 문제 성공적으로, 및 Microsoft 메시지 분석기 tooinvestigate 네트워크입니다.

Fiddler를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 1: toocapture HTTP 및 HTTPS 트래픽을 Fiddler를 사용 하 여]."

Wireshark 사용에 대 한 자세한 내용은 참조 하십시오. "[부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여]."

Microsoft 메시지 분석기를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. "[부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여]."

## <a name="appendices"></a>부록
hello 부록 유용할 수 있습니다를 진단 하 고 Azure 저장소 (및 기타 서비스) 문제를 해결 하는 경우 여러 가지 도구에 설명 합니다. 이러한 도구는 Azure 저장소에 포함되지는 않으며, 타사 제품도 있습니다. 따라서,이 부록에 설명 된 hello 도구는 Microsoft Azure 또는 Azure 저장소와 모든 지원 계약에서 다루지 않는 한 hello 지원 및 라이선스 옵션에서 사용할 수 있는 검사 해야 하므로 평가 프로세스의 일부로 이러한 도구의 hello 공급자입니다.

### <a name="appendix-1"></a>부록 1: Fiddler toocapture HTTP 및 HTTPS 트래픽에 사용 하 여
[Fiddler](http://www.telerik.com/fiddler) hello 사용 중인 Azure 저장소 서비스 및 클라이언트 응용 프로그램 간의 hello HTTP 및 HTTPS 트래픽을 분석 하는 데 유용한 도구입니다.

> [!NOTE]
> Fiddler;의 HTTPS 트래픽을 디코딩할 수 있습니다. 자세히 읽어보아야 hello Fiddler 설명서 toounderstand이를 수행 하는 방법 및 toounderstand hello 보안 의미 합니다.
> 
> 

이 부록 tooconfigure Fiddler toocapture hello 로컬 컴퓨터 Fiddler를 설치 하 고 hello Azure 저장소 서비스 간의 트래픽이 하는 방법의 간단한 연습을 제공 합니다.

Fiddler를 시작하면 로컬 컴퓨터에서 HTTP 및 HTTPS 트래픽 캡처가 시작됩니다. hello 다음은 Fiddler를 제어 하기 위한 몇 가지 유용한 명령입니다.

* 트래픽 캡처를 중지 및 시작하려면 Hello 주 메뉴에서 이동 너무**파일** 클릭 하 고 **트래픽 캡처** tootoggle 캡처 켜고 끕니다.
* 캡처된 트래픽 데이터를 저장하려면 Hello 주 메뉴에서 이동 너무**파일**, 클릭 **저장**, 클릭 하 고 **모든 세션**:이 설정을 통해 있습니다 toosave hello 트래픽을 세션 보관 파일에 있습니다. 분석을 위해 나중에 세션 아카이브를 다시 로드 하거나 tooMicrosoft 지원을 요청 하는 경우이 보낼 수 있습니다.

Fiddler를 캡처하는 트래픽의 toolimit hello 양 hello에 구성 하는 필터를 사용할 수 있습니다 **필터** 스크린 샷 다음 탭 hello만 보낸 트래픽은 toohello 캡처하는 필터를 보여 줍니다.  **contosoemaildist.table.core.windows.net** 저장소 끝점:

![][5]

### <a name="appendix-2"></a>부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여
[Wireshark](http://www.wireshark.org/) tooview 수 있도록 하는 네트워크 프로토콜 분석기는 다양 한 네트워크 프로토콜에 대 한 패킷 정보를 자세히 설명 합니다.

hello 다음 절차에서는 있습니다 toocapture hello 로컬 컴퓨터에서 트래픽에 대 한 패킷 정보를 설명 하는 방법을 Azure 저장소 계정에 Wireshark toohello 테이블 서비스를 설치한

1. 로컬 컴퓨터에서 Wireshark를 시작합니다.
2. Hello에 **시작** 섹션, 선택 hello 로컬 네트워크 인터페이스 또는 인터페이스를 연결 된 toohello 인터넷 합니다.
3. **캡처 옵션**을 클릭합니다.
4. 추가 필터 toohello **캡처 필터** 텍스트 상자에 붙여넣습니다. 예를 들어 **contosoemaildist.table.core.windows.net 호스트** 패킷을 hello에 hello 테이블 서비스 끝점에서 tooor 전송만 Wireshark toocapture 구성 **contosoemaildist** 저장소 계정입니다. 체크 아웃 hello [캡처 필터의 전체 목록은](http://wiki.wireshark.org/CaptureFilters)합니다.
   
   ![][6]
5. **시작**을 클릭합니다. 이제 Wireshark는 클라이언트 응용 프로그램을 사용 하 여 로컬 컴퓨터의 hello 테이블 서비스 끝점에서 모든 패킷을 보내기 tooor를 hello을 캡처합니다.
6. 완료 했을 때, hello 주 메뉴 클릭 **캡처** 차례로 **중지**합니다.
7. toosave hello Wireshark 캡처 파일에서 hello 주 메뉴에서 데이터를 캡처한 **파일** 차례로 **저장**합니다.

WireShark hello에 존재 하는 모든 오류는 강조 표시 **packetlist** 창. Hello를 사용할 수도 있습니다 **전문가 정보** 창 (클릭 **분석**, 다음 **전문가 정보**) tooview의 오류 및 경고 요약 합니다.

![][7]

Hello 응용 프로그램 계층 hello TCP 데이터를 마우스 오른쪽 단추로 클릭 하 고 선택 하 여 표시 하는 대로 tooview hello TCP 데이터를 선택할 수도 **TCP 스트림을 따라**합니다. 캡처 필터를 사용하지 않고 덤프를 캡처한 경우 이와 같이 확인하면 특히 유용합니다. 자세한 내용은 [Following TCP Streams](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvFollowTCPSection.html)(TCP 스트림 따라 이동)를 참조하세요.

![][8]

> [!NOTE]
> Wireshark 사용에 대 한 자세한 내용은 참조 hello [Wireshark 사용자 가이드](http://www.wireshark.org/docs/wsug_html_chunked)합니다.
> 
> 

### <a name="appendix-3"></a>부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여
유사한 방식으로 tooFiddler에서 Microsoft 메시지 분석기 toocapture HTTP 및 HTTPS 트래픽을 사용할 수 있으며 유사한 방식으로 tooWireshark에서 네트워크 트래픽을 캡처할 수 있습니다.

#### <a name="configure-a-web-tracing-session-using-microsoft-message-analyzer"></a>Microsoft Message Analyzer를 사용하여 웹 추적 세션 구성
웹 추적 세션 hello Microsoft 메시지 분석기 응용 프로그램을 실행 되는 Microsoft 메시지 분석기를 사용 하 여 HTTP 및 HTTPS 트래픽에 대 한 고 hello tooconfigure **파일** 메뉴를 클릭 하 여 **캡처/추적**합니다. 사용 가능한 추적 시나리오의 hello 목록에서 선택 **웹 프록시**합니다. Hello 그런 다음 **추적 시나리오 구성** 패널 hello에 **HostnameFilter** textbox 저장소 끝점의 hello 이름을 추가 (hello 이러한 이름을 조회할 수 [Azure포털](https://portal.azure.com)). 예를 들어 경우 hello Azure 저장소 계정 이름은 **contosodata**, hello toohello 뒤에 추가 해야 **HostnameFilter** 텍스트 상자에 붙여넣습니다.

```
contosodata.blob.core.windows.net contosodata.table.core.windows.net contosodata.queue.core.windows.net
```

> [!NOTE]
> 공백 문자는 hello 호스트 이름을 구분합니다.
> 
> 

추적 데이터를 수집 하는 준비 toostart 인 경우 hello 클릭 **Start With** 단추입니다.

Microsoft 메시지 분석기 hello에 대 한 자세한 내용은 **웹 프록시** 추적, 참조 [WebProxy PEF-Microsoft-공급자](http://technet.microsoft.com/library/jj674814.aspx)합니다.

기본 제공 hello **웹 프록시** Fiddler를 기반으로 하는 Microsoft 메시지 분석기에서 추적 않으면 클라이언트의 HTTPS 트래픽을 캡처할 수 있고 암호화 되지 않은 HTTPS 메시지를 표시 합니다. hello **웹 프록시** 액세스 toounencrypted 메시지를 제공 하는 모든 HTTP 및 HTTPS 트래픽에 대 한 로컬 프록시를 구성 하 여 작업을 추적 합니다.

#### <a name="diagnosing-network-issues-using-microsoft-message-analyzer"></a>Microsoft Message Analyzer를 사용하여 네트워크 문제 진단
또한 toousing hello Microsoft 메시지 분석기 **웹 프록시** hello 기본 제공을 사용할 수 있습니다, toocapture 세부 정보를 추적 hello hello 클라이언트 응용 프로그램과 hello 저장소 서비스 간의 HTTP/HTTPs 트래픽을  **로컬 링크 계층** toocapture 네트워크 패킷 정보를 추적 합니다. 와 같은 네트워크에 문제가 발생 하면 toocapture 데이터 비슷한 toothat wireshark를 캡처 및 진단할 수 있는이 사용 하도록이 설정 하는 패킷이 삭제 합니다.

hello 다음 스크린 샷에서 예가 나와 **로컬 링크 계층** 일부를 사용 하 여 추적 **정보** hello 메시지 **DiagnosisTypes** 열입니다. Hello에 아이콘을 클릭 하면 **DiagnosisTypes** 열 hello 메시지의 hello 세부 정보를 표시 합니다. 이 예제에서는 hello 서버 hello 클라이언트에서 승인을 받지 못했기 때문에 #305 메시지를 전송할 때:

![][9]

Microsoft 메시지 분석기에서 hello 추적 세션을 만들 때 hello 추적에서 의미 없는 양을 tooreduce hello 필터를 지정할 수 있습니다. Hello에 **캡처 / 추적** hello 추적을 정의할 수 있는 페이지 클릭 hello **구성** 너무 다음 연결**Microsoft Windows-NDIS PacketCapture**합니다. hello 스크린 샷 다음 세 가지 저장소 서비스의 IP 주소 hello에 대 한 TCP 트래픽을 필터링 하는 구성을 보여 줍니다.

![][10]

Microsoft 메시지 분석기 로컬 링크 계층 추적 hello에 대 한 자세한 내용은 참조 [PEF NDIS PacketCapture Microsoft 공급자](http://technet.microsoft.com/library/jj659264.aspx)합니다.

### <a name="appendix-4"></a>부록 4: Excel tooview 메트릭 및 로그 데이터를 사용 하 여
대부분의 도구를 사용 하면 Azure 테이블 저장소 분석 및 사용 하면 쉽게 tooload hello 데이터에 대 한 Excel로 보고 하는 구분 기호로 분리 된 형식에서에서 toodownload hello 저장소 메트릭 데이터 있습니다. Azure Blob 저장소의 저장소 로깅 데이터는 이미 Excel에 로드할 수 있는 구분된 형식으로 되어 있습니다. 그러나 tooadd 해당 열 머리글에 hello 정보에 기반 할 [저장소 분석 로그 형식](http://msdn.microsoft.com/library/azure/hh343259.aspx) 및 [저장소 분석 통계 테이블 스키마](http://msdn.microsoft.com/library/azure/hh343264.aspx)합니다.

tooimport 후 저장소 로깅 데이터를 Excel로 다운로드 blob 저장소에서:

* Hello에 **데이터** 메뉴를 클릭 하 여 **에서 텍스트**합니다.
* 찾아보기 toohello 로그 파일 누르고 tooview 원하는 **가져오기**합니다.
* hello의 1 단계 **텍스트 가져오기 마법사**선택, **구분 기호로 분리 됨**합니다.

hello의 1 단계 **텍스트 가져오기 마법사**선택, **세미콜론** 으로 hello 유일한 구분 기호 및 \ hello로 선택 **텍스트 한정자**합니다. 클릭 **마침** 여기서 tooplace hello 통합 문서의 데이터를 선택 합니다.

### <a name="appendix-5"></a>부록5: Visual Studio Team Services용 Application Insights를 사용한 모니터링
또한 Visual Studio Team Services에 대 한 성능 및 가용성 모니터링의 일환으로 hello Application Insights 기능을 사용할 수 있습니다. 이 도구는 다음과 같은 작업을 수행할 수 있습니다.

* 웹 서비스가 사용 가능하며 응답할 수 있는 상태인지 확인합니다. 에 관계 없이 응용 프로그램 웹 사이트 또는 웹 서비스를 사용 하는 장치 앱 수 hello world 여러 위치에서 몇 분 마다으로 URL을 테스트 하 고 문제가 있는지 여부를 알려 줍니다.
* 웹 서비스의 성능 문제나 예외를 빠르게 진단합니다. CPU 또는 기타 리소스가 확대되는지 확인하고 예외에서 스택 추적을 가져오며 로그 추적을 쉽게 검색할 수 있습니다. 경우 hello 성능 작은지에 응용 프로그램의 허용 한도 받을 수는 전자 메일입니다. .NET 및 Java 웹 서비스를 모두 모니터링할 수 있습니다.

[Application Insights란?](../../application-insights/app-insights-overview.md)에서 추가 정보를 찾을 수 있습니다.

<!--Anchors-->
[소개]: #introduction
[이 가이드의 구성 방식]: #how-this-guide-is-organized

[저장소 서비스를 모니터링]: #monitoring-your-storage-service
[서비스 상태 모니터링]: #monitoring-service-health
[용량 모니터링]: #monitoring-capacity
[가용성 모니터링]: #monitoring-availability
[성능 모니터링]: #monitoring-performance

[저장소 문제를 진단]: #diagnosing-storage-issues
[서비스 상태 문제]: #service-health-issues
[성능 문제]: #performance-issues
[오류 진단]: #diagnosing-errors
[저장소 에뮬레이터 문제]: #storage-emulator-issues
[저장소 로깅 도구]: #storage-logging-tools
[네트워크 로깅 도구 사용]: #using-network-logging-tools

[종단 간 추적]: #end-to-end-tracing
[로그 데이터 상관 관계 설정]: #correlating-log-data
[클라이언트 요청 ID]: #client-request-id
[서버 요청 ID]: #server-request-id
[타임스탬프]: #timestamps

[문제 해결 지침]: #troubleshooting-guidance
[메트릭에서 높은 AverageE2ELatency 및 낮은 AverageServerLatency]: #metrics-show-high-AverageE2ELatency-and-low-AverageServerLatency
[낮은 AverageE2ELatency 및 낮은 AverageServerLatency 메트릭을 표시 하지만 hello 클라이언트에서 높은 대기 시간이 발생 합니다.]: #metrics-show-low-AverageE2ELatency-and-low-AverageServerLatency
[메트릭에서 AverageServerLatency가 높게 표시됨]: #metrics-show-high-AverageServerLatency
[큐에서 메시지 배달 중에 예기치 않은 대기 시간이 발생함]: #you-are-experiencing-unexpected-delays-in-message-delivery

[메트릭에서 PercentThrottlingError의 증가]: #metrics-show-an-increase-in-PercentThrottlingError
[일시적인 PercentThrottlingError 증가]: #transient-increase-in-PercentThrottlingError
[영구적인 PercentThrottlingError 증가]: #permanent-increase-in-PercentThrottlingError
[메트릭에서 PercentTimeoutError의 증가]: #metrics-show-an-increase-in-PercentTimeoutError
[메트릭에서 PercentNetworkError가 증가하는 것으로 표시됨]: #metrics-show-an-increase-in-PercentNetworkError

[HTTP 403 (금지 됨) 메시지를 받고 hello 클라이언트]: #the-client-is-receiving-403-messages
[hello 클라이언트에서 HTTP 404 (찾을 수 없음) 메시지를 받는]: #the-client-is-receiving-404-messages
[클라이언트 hello 또는 다른 프로세스를 이전에 삭제 hello 개체]: #client-previously-deleted-the-object
[SAS(공유 액세스 서명) 권한 부여 문제]: #SAS-authorization-issue
[클라이언트 쪽 JavaScript 코드가 권한 tooaccess hello 개체를 가질 수 없습니다.]: #JavaScript-code-does-not-have-permission
[네트워크 오류]: #network-failure
[hello 클라이언트 HTTP 409 (충돌) 메시지 수신]: #the-client-is-receiving-409-messages

[메트릭에서 낮은 PercentSuccess 또는 분석 로그 항목 된 작업이 있을 ClientOtherErrors의 트랜잭션 상태]: #metrics-show-low-percent-success
[용량 메트릭에 예기치 않은 저장소 용량 사용 증가가 표시됨]: #capacity-metrics-show-an-unexpected-increase
[많은 수의 VHD가 연결된 가상 컴퓨터가 예기치 않게 다시 부팅됨]: #you-are-experiencing-unexpected-reboots
[개발 또는 테스트에 대 한 hello 저장소 에뮬레이터를 사용 하 여 문제 발생]: #your-issue-arises-from-using-the-storage-emulator
[기능 "X" hello 저장소 에뮬레이터에서 작동 하지 않습니다.]: #feature-X-is-not-working
[오류 "hello 값 hello HTTP 헤더 중 하나에 대 한이 형식이 잘못 된 hello" 때 저장소 에뮬레이터를 사용 하 여 hello]: #error-HTTP-header-not-correct-format
[Hello 저장소 에뮬레이터를 실행 하려면 관리자 권한이 필요]: #storage-emulator-requires-administrative-privileges
[Hello Azure SDK for.NET 설치에 문제가 발생 하는]: #you-are-encountering-problems-installing-the-Windows-Azure-SDK
[저장소 서비스에서 다른 문제가 발생함]: #you-have-a-different-issue-with-a-storage-service

[부록]: #appendices
[부록 1: toocapture HTTP 및 HTTPS 트래픽을 Fiddler를 사용 하 여]: #appendix-1
[부록 2: Wireshark toocapture 네트워크 트래픽을 사용 하 여]: #appendix-2
[부록 3: Microsoft 메시지 분석기 toocapture 네트워크 트래픽을 사용 하 여]: #appendix-3
[부록 4: Excel tooview 메트릭 및 로그 데이터를 사용 하 여]: #appendix-4
[부록5: Visual Studio Team Services용 Application Insights를 사용한 모니터링]: #appendix-5

<!--Image references-->
[1]: ./media/storage-monitoring-diagnosing-troubleshooting/overview.png
[3]: ./media/storage-monitoring-diagnosing-troubleshooting/hour-minute-metrics.png
[4]: ./media/storage-monitoring-diagnosing-troubleshooting/high-e2e-latency.png
[5]: ./media/storage-monitoring-diagnosing-troubleshooting/fiddler-screenshot.png
[6]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-1.png
[7]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-2.png
[8]: ./media/storage-monitoring-diagnosing-troubleshooting/wireshark-screenshot-3.png
[9]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-1.png
[10]: ./media/storage-monitoring-diagnosing-troubleshooting/mma-screenshot-2.png
