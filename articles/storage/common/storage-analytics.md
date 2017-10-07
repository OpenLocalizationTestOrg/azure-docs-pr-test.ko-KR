---
title: "Azure Storage Analytics toocollect 로그 및 메트릭 데이터 aaaUse | Microsoft Docs"
description: "저장소 분석 모든 저장소 서비스에 대 한 메트릭 데이터 tootrack 있으며 toocollect Blob, 큐 및 테이블 저장소에 대 한 기록 합니다."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>저장소 분석

Azure 저장소 분석은 로깅을 수행하며 저장소 계정에 대한 메트릭 데이터를 제공합니다. 이 데이터 tootrace 요청을 사용 하 고, 사용 추세를 분석 하 고, 저장소 계정 문제를 진단할 수 있습니다.

toouse Storage Analytics를 사용 하도록 설정 해야 개별적으로 각 서비스에 대해 원하는 toomonitor 합니다. Hello에서 사용할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 자세한 내용은 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링](storage-monitor-storage-account.md)합니다. Hello REST API를 통해 프로그래밍 방식으로 Storage Analytics 하거나 hello 클라이언트 라이브러리를 사용할 수도 있습니다. 사용 하 여 hello [Blob 서비스 속성 가져오기](https://msdn.microsoft.com/library/hh452239.aspx), [큐 서비스 속성 가져오기](https://msdn.microsoft.com/library/hh452243.aspx), [테이블 서비스 속성 가져오기](https://msdn.microsoft.com/library/hh452238.aspx), 및 [파일 서비스 속성을가져오기](https://msdn.microsoft.com/library/mt427369.aspx) 각 서비스에 대 한 작업 tooenable 저장소 분석 합니다.

hello 집계 된 데이터 및 저장 된 잘 알려진 blob (로깅용)에 잘 알려진 테이블 (통계용), hello Blob 서비스 및 테이블 서비스 Api 사용 하 여 액세스할 수 있는 합니다.

Storage Analytics에서는 hello 저장소 계정의 총 한도와 hello와 독립적인 저장 된 데이터 양이 20TB로 제한 합니다. 청구 및 데이터 보존 정책에 대한 자세한 내용은 [저장소 분석 및 청구](https://msdn.microsoft.com/library/hh360997.aspx)를 참조하세요. 저장소 계정 제한에 대한 자세한 내용은 [Azure Storage 확장성 및 성능 목표](storage-scalability-targets.md)를 참조하세요.

저장소 분석 및 기타 도구 tooidentify를 사용 하 여 상세 가이드에 대 한 진단, 및 Azure 저장소 관련 문제를 해결 하 고, 참조 [모니터, 진단 및 해결 Microsoft Azure 저장소](storage-monitoring-diagnosing-troubleshooting.md)합니다.

## <a name="about-storage-analytics-logging"></a>저장소 분석 로깅 정보
Storage Analytics는 성공 및 실패 한 요청 tooa 저장소 서비스에 대 한 세부 정보를 기록 합니다. 이 정보는 개별 요청을 사용 하는 toomonitor 및 저장소 서비스와 toodiagnose 문제 수 있습니다. 요청은 최상의 노력을 기준으로 기록됩니다.

저장소 서비스 활동이 있는 경우에만 로그 항목이 작성됩니다. 예를 들어 저장소 계정에 해당 Blob 서비스에 있지만 해당 테이블 또는 큐 서비스에 없는 작업, toohello Blob 서비스와 관련 된 로그만 생성 됩니다.

Azure File Storage에는 저장소 분석 로깅을 사용할 수 없습니다.

### <a name="logging-authenticated-requests"></a>인증된 요청 로깅
hello 다음 유형의 인증 된 요청이 기록 됩니다.

* 성공한 요청
* 실패한 요청(제한 시간, 제한, 네트워크, 권한 부여 및 기타 오류)
* 실패한 요청 및 성공한 요청을 포함하는 SAS(공유 액세스 서명)를 사용하는 요청
* 요청 tooanalytics 데이터입니다.

로그 만들기/삭제 등 저장소 분석 자체에서 수행한 요청은 기록되지 않습니다. Hello 기록 데이터의 전체 목록은 hello에 설명 되어 [저장소 분석에서 기록한 작업 및 상태 메시지](https://msdn.microsoft.com/library/hh343260.aspx) 및 [저장소 분석 로그 형식](https://msdn.microsoft.com/library/hh343259.aspx) 항목입니다.

### <a name="logging-anonymous-requests"></a>익명 요청 로깅
hello 다음 유형의 익명 요청이 기록 됩니다.

* 성공한 요청
* 서버 오류
* 클라이언트와 서버에 대한 시간 초과 오류
* 오류 코드가 304(수정되지 않음)인 실패한 GET 요청

기타 모든 실패한 익명 요청은 기록되지 않습니다. Hello 기록 데이터의 전체 목록은 hello에 설명 되어 [저장소 분석에서 기록한 작업 및 상태 메시지](https://msdn.microsoft.com/library/hh343260.aspx) 및 [저장소 분석 로그 형식](https://msdn.microsoft.com/library/hh343259.aspx) 항목입니다.

### <a name="how-logs-are-stored"></a>로그 저장 방법
모든 로그는 $logs 컨테이너의 블록 Blob에 저장됩니다. 이 컨테이너는 저장소 계정에 대해 저장소 분석을 사용하도록 설정하면 자동으로 작성됩니다. hello $logs 컨테이너 hello 저장소 계정의 blob 네임 스페이스 hello에에서 예를 들어 있는: `http://<accountname>.blob.core.windows.net/$logs`합니다. 저장소 계정을 사용하도록 설정한 후에는 이 컨테이너를 삭제할 수 없지만 해당 콘텐츠는 삭제할 수 있습니다.

> [!NOTE]
> hello $logs 컨테이너에는 hello 같은 컨테이너 나열 작업을 수행 하는 경우 표시 되지 않습니다 [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) 메서드. 직접 액세스해야 합니다. 예를 들어 hello를 사용할 수 있습니다 [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) 메서드 tooaccess hello blob을 hello `$logs` 컨테이너입니다.
> 요청을 기록할 때 저장소 분석은 중간 결과를 블록으로 업로드합니다. 그리고 이러한 블록을 정기적으로 커밋하여 Blob로 제공합니다.
> 
> 

Hello에 생성 된 로그에 대 한 중복 된 레코드가 존재할 수 있습니다 같은 시간입니다. Hello를 확인 하 여 레코드가 중복 되었는지 확인할 수 있습니다 **RequestId** 및 **작업** 번호입니다.

### <a name="log-naming-conventions"></a>로그 명명 규칙
각 로그 형식에 따라 hello에 작성 됩니다.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

hello 다음 설명 hello 로그 이름의 각 특성입니다.

| 특성 | 설명 |
| --- | --- |
| <service-name> |hello 저장소 서비스의 hello 이름입니다. 예: blob, table, queue |
| YYYY |hello hello 로그에 대 한 네 자리 연도입니다. 예: 2011 |
| MM |hello 로그에 대 한 hello 두 자리 월입니다. 예: 07 |
| DD |hello 로그에 대 한 hello 두 자리 월입니다. 예: 07 |
| hh |hello에 대 한 시간부터 hello 나타내는 hello 두 자리 시간 24 시간 UTC 형식으로 기록 합니다. 예: 18 |
| MM |hello 시작 hello 로그에 대 한 분을 나타내는 hello 두 자리 숫자입니다. 이 값은 hello 현재 버전의 Storage Analytics에서 지원 되지 않습니다 및 그 값 00은 항상 합니다. |
| <counter> |0부터 시작 하는 카운터 6 자리 숫자 hello hello 저장소 서비스에 대해 한 시간 기간에에서 생성 된 로그 blob 수를 나타냅니다. 이 카운터는 000000부터 시작됩니다. 예: 000001 |

hello 다음은 hello 이전 예제를 결합 하는 전체 예제 로그 이름입니다.

    blob/2011/07/31/1800/000001.log

hello 다음은 샘플 hello 이전 로그를 사용 하는 tooaccess 일 수 있는 URI입니다.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

저장소 요청이 기록 될 때 hello 결과 로그 이름이 toohello 시간 hello र ् ण를 요청 하는 경우 상관 관계를 지정 합니다. 예를 들어 GetBlob 요청이 2011/7/31 오후 6시 30분에 완료된 경우 7/31/2011에 hello 로그가 접두사 뒤 hello로 기록 됩니다.`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>로그 메타데이터
모든 로그 blob는 어떤 로깅 데이터 hello blob 포함 tooidentify 사용된 될 수 있는 메타 데이터와 함께 저장 됩니다. 다음 표에서 hello 각 메타 데이터 특성을 설명 합니다.

| 특성 | 설명 |
| --- | --- |
| LogType |Hello 로그 tooread, 쓰기 또는 삭제 작업에 대 한 정보가 포함 되는지 여부를 설명 합니다. 이 값에는 한 가지 형식이 포함될 수도 있고 3개 형식이 모두 조합(쉼표로 구분)되어 포함될 수도 있습니다. 예제 1: 쓰기; 예제 2: 읽기,쓰기; 예제 3: 읽기,쓰기,삭제하기. |
| StartTime |YYYY hello 형태로 hello 로그에에서 항목의 가장 빠른 시간 hello-m M-DDThh:mm:ssZ 합니다. 예: 2011-07-31T18:21:46Z |
| EndTime |YYYY hello 형태로 hello 로그에에서 항목의 최신 시간 hello-m M-DDThh:mm:ssZ 합니다. 예: 2011-07-31T18:22:09Z |
| LogVersion |hello 버전 hello 로그 형식입니다. 현재 hello만 지원 값은 1.0입니다. |

hello 다음 목록에 표시 됩니다 hello 이전 예제를 사용 하 여 전체 예제 메타 데이터입니다.

* LogType=write
* StartTime=2011-07-31T18:21:46Z
* EndTime=2011-07-31T18:22:09Z
* LogVersion=1.0

### <a name="accessing-logging-data"></a>로깅 데이터 액세스
Hello에서 모든 데이터 `$logs` hello hello에서 제공 된.NET Api를 포함 하 여 Azure 관리 되는 라이브러리를 hello Blob 서비스 Api를 사용 하 여 컨테이너를 액세스할 수 있습니다. 저장소 계정 관리자에 게 수 읽기 및 로그를 삭제 하지만 만들거나 업데이트할 수 없습니다 하 합니다. 로그를 쿼리할 때 hello 로그의 메타 데이터와 로그 이름을 모두 사용할 수 있습니다. 특정된 시간의 로그가 tooappear 순서 대로 대 한 수도 있지만 항상 hello 메타 데이터는 로그에 로그 항목의 hello timespan을 지정 합니다. 따라서 특정 로그를 검색할 때 로그 이름과 메타데이터 조합을 사용할 수 있습니다.

## <a name="about-storage-analytics-metrics"></a>저장소 분석 메트릭 정보
Storage Analytics는 요청 tooa 저장소 서비스에 대 한 집계 된 트랜잭션 통계 및 용량 데이터가 포함 된 메트릭을 저장할 수 있습니다. Hello 저장소 서비스 수준에서 뿐만 아니라 두 hello API 작업 수준에서 트랜잭션을 보고 하 고 용량은 hello 저장소 서비스 수준에서 보고 됩니다. 메트릭 데이터는 사용 되는 tooanalyze 저장소 서비스 사용 될, hello 저장소 서비스 및 서비스를 사용 하는 응용 프로그램의 tooimprove hello 성능에 대해 수행 된 요청 문제를 진단할 수 있습니다.

toouse Storage Analytics를 사용 하도록 설정 해야 개별적으로 각 서비스에 대해 원하는 toomonitor 합니다. Hello에서 사용할 수 있습니다 [Azure 포털](https://portal.azure.com)합니다. 자세한 내용은 참조 [hello Azure 포털에서에서 저장소 계정을 모니터링](storage-monitor-storage-account.md)합니다. Hello REST API를 통해 프로그래밍 방식으로 Storage Analytics 하거나 hello 클라이언트 라이브러리를 사용할 수도 있습니다. 사용 하 여 hello **서비스 속성 가져오기** 각 서비스에 대 한 작업 tooenable 저장소 분석 합니다.

### <a name="transaction-metrics"></a>트랜잭션 메트릭
각 저장소 서비스 및 요청한 API 작업에 대해 시간 또는 분 간격으로 유용한 데이터 집합이 기록됩니다. 이러한 데이터에는 수신/송신, 가용성, 오류, 분류된 요청 비율 등이 포함됩니다. 전체 목록은 hello에서 hello 트랜잭션 세부 정보를 볼 수 [저장소 분석 통계 테이블 스키마](https://msdn.microsoft.com/library/hh343264.aspx) 항목입니다.

트랜잭션 데이터는 두 수준 hello 서비스 수준 및 hello API 작업 수준에서 기록 됩니다. Hello 서비스 수준에서 통계를 요약 하는 모든 API 작업은 기록 tooa 테이블 엔터티 1 시간 마다 요청이 없는 toohello 서비스에 적용 된 경우에 요청 했습니다. Hello API 작업 수준에서 통계 hello 작업이 해당 시간 내에서 요청 하는 경우 유일한 서 면된 tooan 엔터티는 합니다.

예를 들어, 수행 하는 경우는 **GetBlob** Storage Analytics 메트릭에서 Blob 서비스에 대 한 작업을 hello 요청을 기록 하 고 Blob 서비스 뿐 아니라 hello hello 둘 다에 대 한 집계 hello 데이터에 포함할 **GetBlob** 작업 합니다. 그러나 되지 않은 경우 **GetBlob** hello 시간 동안 작업이 요청 엔터티가 기록 되지 않으며 toohello `$MetricsTransactionsBlob` 해당 작업에 대 한 합니다.

저장소 분석 자체에서 수행한 요청과 사용자 요청 둘 모두에 대해 트랜잭션 메트릭이 기록됩니다. 예를 들어 Storage Analytics toowrite 로그 및 테이블 엔터티 요청 기록 됩니다. 이러한 요청에 대해 요금이 청구되는 방식에 대한 자세한 내용은 [저장소 분석 및 청구](https://msdn.microsoft.com/library/hh360997.aspx)를 참조하세요.

### <a name="capacity-metrics"></a>용량 메트릭
> [!NOTE]
> 현재 용량 메트릭은 hello Blob 서비스에 사용할 수만 있습니다. Hello 테이블 서비스 및 큐 서비스에 대 한 용량 메트릭은 이후 버전의 저장소 분석에 사용할 수 있습니다.
> 
> 

용량 데이터는 저장소 계정의 Blob service에 대해 매일 기록되며 2개의 테이블 엔터티가 작성됩니다. 하나의 엔터티가 사용자 데이터에 대 한 통계를 제공 하 고 hello에 대 한 통계를 제공 하는 다른 hello `$logs` Storage Analytics에서 사용 되는 blob 컨테이너입니다. hello `$MetricsCapacityBlob` 테이블 통계를 다음 hello에 포함 됩니다.

* **용량**: hello 양을 바이트 단위로 hello 저장소 계정의 Blob 서비스에 의해 사용 되는 저장소입니다.
* **ContainerCount**: hello hello 저장소 계정의 Blob 서비스에서 blob 컨테이너 수입니다.
* **ObjectCount**: hello hello 저장소 계정의 Blob 서비스에서 커밋된 블록과 커밋되지 않은 블록 또는 페이지 blob 수입니다.

Hello 용량 메트릭에 대 한 자세한 내용은 참조 하십시오. [저장소 분석 통계 테이블 스키마](https://msdn.microsoft.com/library/hh343264.aspx)합니다.

### <a name="how-metrics-are-stored"></a>메트릭 저장 방법
각 hello 저장소 서비스에 대 한 모든 메트릭 데이터는 해당 서비스에 대해 예약 된 세 개의 테이블에 저장 됩니다: 트랜잭션 정보용 테이블, 세부 트랜잭션 정보용 테이블 및 용량 정보에 대 한 다른 테이블입니다. 트랜잭션 및 세부 트랜잭션 정보는 요청과 응답 데이터로 구성되며 용량 정보는 저장소 사용량 데이터로 구성됩니다. 시간 메트릭, 분 메트릭 및 저장소 계정의 Blob 서비스에 대 한 용량 hello 표 다음에 설명 된 대로 명명 된 테이블에 액세스할 수 있습니다.

| 메트릭 수준 | 테이블 이름 | 지원되는 버전 |
| --- | --- | --- |
| 시간 메트릭, 기본 위치 |$MetricsTransactionsBlob  <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |버전 이전 too2013-08-15만 합니다. 이러한 이름이 계속 지원 하지만 아래 나열 된 toousing hello 테이블을 전환 하는 것이 좋습니다. |
| 시간 메트릭, 기본 위치 |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |2013-08-15를 포함한 모든 버전. |
| 분 메트릭, 기본 위치 |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |2013-08-15를 포함한 모든 버전. |
| 시간 메트릭, 보조 위치 |$MetricsHourSecondaryTransactionsBlob  <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |2013-08-15를 포함한 모든 버전. 읽기 권한의 지역 중복 복제를 사용하도록 설정해야 합니다. |
| 분 메트릭, 보조 위치 |$MetricsMinuteSecondaryTransactionsBlob  <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |2013-08-15를 포함한 모든 버전. 읽기 권한의 지역 중복 복제를 사용하도록 설정해야 합니다. |
| 용량(Blob 서비스만 해당) |$MetricsCapacityBlob |2013-08-15를 포함한 모든 버전. |

이러한 테이블은 저장소 계정에 대해 저장소 분석을 사용하도록 설정하면 자동으로 작성됩니다. 예를 들어 hello 저장소 계정의 hello 네임 스페이스를 통해 액세스 하 있습니다.`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>메트릭 데이터 액세스
Hello hello에서 제공 된.NET Api를 포함 하 여 Azure 관리 되는 라이브러리를 hello 테이블 서비스 Api를 사용 하 여 hello 메트릭 테이블의 모든 데이터를 액세스할 수 있습니다. 저장소 계정 관리자에 게 수 읽기 및 테이블 엔터티를 삭제 하지만 만들거나 업데이트할 수 없습니다 하 합니다.

## <a name="billing-for-storage-analytics"></a>저장소 분석 청구
모든 메트릭 데이터는 저장소 계정의 hello 서비스에 의해 기록 됩니다. 따라서 저장소 분석에서 수행하는 각 쓰기 작업에 대해 요금이 청구됩니다. 또한 hello 양의 메트릭 데이터에서 사용 하는 저장소 용량도 청구 됩니다.

Storage Analytics에서 수행 하는 작업을 수행 하는 hello는 청구 가능 합니다.

* 로깅에 대 한 toocreate blob를 요청합니다. 
* 메트릭에 대 한 요청 toocreate 테이블 엔터티입니다.

데이터 보존 정책을 구성한 경우에는 저장소 분석에서 이전 로깅 및 메트릭 데이터를 삭제할 때 삭제 트랜잭션에 대해 요금이 부과되지 않습니다. 그러나 클라이언트의 삭제 트랜잭션에는 요금이 청구됩니다. 보존 정책에 대한 자세한 내용은 [저장소 분석 데이터 보존 정책 설정](https://msdn.microsoft.com/library/azure/hh343263.aspx)을 참조하세요.

### <a name="understanding-billable-requests"></a>청구 가능한 요청 이해
Tooan 계정의 저장소 서비스에 수행 된 모든 요청에는 청구 가능 또는 불가능입니다. 저장소 분석 방법을 hello 요청이 처리 됨을 나타내는 상태 메시지를 포함 하 여 tooa 서비스를 만든 개별 요청을 기록 합니다. 마찬가지로, Storage Analytics는 특정 상태 메시지의 hello 비율 및 개수를 포함 하 여 해당 서비스의 서비스와 hello API 작업에 대 한 메트릭을 저장 합니다. 함께 이러한 기능은 유용 청구 가능한 요청을 분석, 응용 프로그램 성능을 개선 하 고 요청 tooyour 서비스 문제를 진단 합니다. 청구에 대한 자세한 내용은 [Azure Storage 청구 이해 - 대역폭, 트랜잭션 및 용량](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx)을 참조하세요.

Storage Analytics 데이터를 확인 하면 hello에 hello 테이블을 사용할 수 있습니다 [저장소 분석에서 기록한 작업 및 상태 메시지](https://msdn.microsoft.com/library/azure/hh343260.aspx) 항목 toodetermine는 청구 가능 요청 합니다. 그런 다음 특정 요청에 대 한 요금이 부과 되었는지 경우 로그 및 메트릭 데이터 toohello 상태 메시지 toosee 비교할 수 있습니다. 저장소 서비스 또는 개별 API 작업에 대 한 hello 이전 항목 tooinvestigate 가용성의 hello 테이블을 사용할 수도 있습니다.

## <a name="next-steps"></a>다음 단계
### <a name="setting-up-storage-analytics"></a>저장소 분석 설정
* [Hello Azure 포털에서에서 저장소 계정을 모니터링합니다](storage-monitor-storage-account.md)
* [저장소 분석 설정 및 구성](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>저장소 분석 로깅
* [저장소 분석 로깅 정보](https://msdn.microsoft.com/library/hh343262.aspx)
* [저장소 분석 로그 형식](https://msdn.microsoft.com/library/hh343259.aspx)
* [저장소 분석에서 기록한 작업 및 상태 메시지](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>저장소 분석 메트릭
* [저장소 분석 메트릭 정보](https://msdn.microsoft.com/library/hh343258.aspx)
* [저장소 분석 메트릭 테이블 스키마](https://msdn.microsoft.com/library/hh343264.aspx)
* [저장소 분석에서 기록한 작업 및 상태 메시지](https://msdn.microsoft.com/library/hh343260.aspx)  

