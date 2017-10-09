---
title: "데이터 연결: 이벤트 스트림의 데이터 스트림 입력 | Microsoft Docs"
description: "데이터 연결 tooStream '입력'를 호출 하는 분석을 설정 하는 방법을 알아봅니다. 입력에는 이벤트의 데이터 스트림과 참조 데이터가 포함되어 있습니다."
keywords: "데이터 스트림, 데이터 연결, 이벤트 스트림"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 8155823c-9dd8-4a6b-8393-34452d299b68
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/05/2017
ms.author: samacha
ms.openlocfilehash: be2008f159061c5c9be9d0314c27fa67193e3269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="data-connection-learn-about-data-stream-inputs-from-events-toostream-analytics"></a>데이터 연결: 이벤트 tooStream 분석의에서 스트림 입력 데이터에 대 한 자세한 내용은
hello 데이터 연결 tooa 스트림 분석 작업은 참조 tooas hello 작업이 있는 데이터 원본의 이벤트 스트림을 *입력*합니다. Stream Analytics는 [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/), [Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) 및 [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)를 비롯한 Azure 데이터 스트림 원본과 높은 수준으로 통합됩니다. Hello에서 소스 수 있도록 이러한 입력 또는 다른 구독에서 분석 작업으로 동일한 Azure 구독.

## <a name="data-input-types-data-stream-and-reference-data"></a>데이터 입력 유형: 데이터 스트림 및 참조 데이터
데이터를 데이터 소스 tooa 밀어넣을, 대로 hello 스트림 분석 작업에서 사용이 있으며 실시간으로 처리 합니다. 입력은 데이터 스트림 입력과 참조 데이터 입력의 두 가지 형식으로 나뉩니다.

### <a name="data-stream-inputs"></a>데이터 스트림 입력
데이터 스트림은 시간이 지남에 따라 생성되는 이벤트의 제한 없는 시퀀스입니다. Stream Analytics 작업은 하나 이상의 데이터 스트림 입력을 포함해야 합니다. Event Hubs, IoT Hub 및 Blob Storage는 데이터 스트림 입력 원본으로 지원됩니다. 이벤트 허브는 여러 장치와 서비스에서 이벤트 스트림을 사용 하는 toocollect 합니다. 이러한 스트림은 소셜 미디어 활동 피드, 주식 거래 정보 또는 센서 데이터를 포함할 수 있습니다. IoT 허브는 사물 인터넷 (IoT) 시나리오에서 연결 된 장치에서 toocollect 최적화 된 데이터입니다.  Blob Storage를 로그 파일과 같은 스트림으로 대량 데이터 수집을 위한 입력 원본으로 사용할 수 있습니다.  

### <a name="reference-data"></a>참조 데이터
Stream Analytics은 *참조 데이터*라는 입력도 지원합니다. 고정적이거나 천천히 변하는 보조 데이터입니다. 일반적으로 상관 관계 및 조회를 수행하는 데 사용됩니다. 예를 들어 정적 값을 SQL 조인 toolook을 수행 하는 것과 마찬가지로 hello 참조 데이터의 hello 데이터 스트림 입력된 toodata에 데이터를 조인할 수 있습니다. Azure Blob 저장소는 현재 참조 데이터에 대 한 입력된 소스 hello만 지원 됩니다. 참조 데이터 원본 blob는 제한 된 too100 제한 합니다.

toocreate 참조 데이터 입력을 확인 하려면 어떻게 해야 toolearn [참조 데이터 사용](stream-analytics-use-reference-data.md)합니다.  

## <a name="create-data-stream-input-from-event-hubs"></a>Event Hubs에서 데이터 스트림 입력 만들기

Azure Event Hubs는 확장성 있는 게시-구독 이벤트 수집기를 제공합니다. 이벤트 허브를 처리 하 고 연결 된 장치 및 응용 프로그램에서 생성 되는 데이터의 양이 hello를 분석할 수 있도록 수백만 개의 초당 이벤트를 수집할 수 있습니다. Event Hubs 및 Stream Analytics를 함께 사용하면 실시간 분석을 위한 종단 간 솔루션이 제공됩니다. Event Hubs를 통해 Azure에 실시간으로 이벤트가 제공되며 Stream Analytics 작업에서 이러한 이벤트를 실시간으로 처리합니다. 예를 들어 웹 클릭, 센서 판독값 또는 온라인 로그 이벤트 tooEvent 허브를 보낼 수 있습니다. hello 입력된 데이터 스트림을 실시간으로 필터링, 집계 및 상관 관계에 대 한 스트림 분석 작업 toouse 이벤트 허브를 만들 수 있습니다.

스트림 분석에서 이벤트 허브에서 오는 이벤트의 hello 기본 타임 스탬프는 hello 이벤트 허브에 도착 한 이벤트 hello hello 타임 스탬프는 `EventEnqueuedUtcTime`합니다. hello를 사용 해야 합니다 tooprocess hello 이벤트 페이로드의 타임 스탬프를 사용 하 여 스트림으로 데이터를 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) 키워드입니다.

### <a name="consumer-groups"></a>소비자 그룹
각 스트림 분석 이벤트 허브 입력된 toohave 자체 소비자 그룹을 구성 해야 합니다. 작업에 셀프 조인이 포함되거나 입력이 여러 개인 경우 둘 이상의 판독기 다운스트림으로 일부 입력을 읽을 수 있습니다. 이 경우 hello 수의 판독기는 하나의 소비자 그룹의 영향을 줍니다. tooavoid 초과 hello 이벤트 허브 소비자 그룹 파티션당 당 5 개 독자, 것 제한은 각 스트림 분석 작업에 대 한 소비자 그룹 모범 사례 toodesignate입니다. 또한 이벤트 허브당 20개의 소비자 그룹으로 제한됩니다. 자세한 내용은 [Event Hubs 프로그래밍 가이드](../event-hubs/event-hubs-programming-guide.md)를 참조하세요.

### <a name="configure-an-event-hub-as-a-data-stream-input"></a>데이터 스트림 입력으로 이벤트 허브 구성
hello 다음 표에서 설명의 각 속성에 hello **새 입력** 블레이드 hello 입력으로 이벤트 허브를 구성할 때 Azure 포털의에서.

| 속성 | 설명 |
| --- | --- |
| **입력 별칭** |이 입력 쿼리 tooreference hello 작업에서에서 사용 하는 이름입니다. |
| **서비스 버스 네임스페이스** |Azure Service Bus 네임스페이스는 메시징 엔터티 집합에 대한 컨테이너입니다. 새 이벤트 허브를 만들 때 서비스 버스 네임스페이스도 만듭니다. |
| **이벤트 허브 이름** |입력으로 hello 이벤트 허브 toouse의 hello 이름입니다. |
| **이벤트 허브 정책 이름** |액세스 toohello 이벤트 허브를 제공 하는 hello 공유 액세스 정책입니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. |
| **이벤트 허브 소비자 그룹**(선택 사항) |hello 소비자 그룹 toouse tooingest 데이터 hello 이벤트 허브에서입니다. 소비자 그룹이 지정 되어 hello 스트림 분석 작업 hello 기본 소비자 그룹이 사용 됩니다. 각 Stream Analytics 작업마다 고유한 소비자 그룹을 사용하는 것이 좋습니다. |
| **이벤트 직렬화 형식** |hello serialization 형식 (JSON, CSV 또는 Avro) hello 들어오는 데이터 스트림을입니다. |
| **Encoding** | U t F-8만 지원 hello 인코딩 형식을 현재입니다. |

데이터 이벤트 허브에 도달할 경우 해야 스트림 분석 쿼리의 메타 데이터 필드를 다음 액세스 toohello:

| 속성 | 설명 |
| --- | --- |
| **EventProcessedUtcTime** |hello 날짜 및 시간에 해당 hello 이벤트 스트림 분석에서 처리 합니다. |
| **EventEnqueuedUtcTime** |hello 날짜 및 시간 해당 hello 이벤트가 이벤트 허브에서 수신 되었습니다. |
| **PartitionId** |hello hello 입력된 어댑터에 대 한 0부터 시작 파티션 ID입니다. |

예를 들어 이러한 필드를 사용 하 여 다음 예제는 hello와 같은 쿼리를 작성할 수 있습니다.

````
SELECT
    EventProcessedUtcTime,
    EventEnqueuedUtcTime,
    PartitionId
FROM Input
````

## <a name="create-data-stream-input-from-iot-hub"></a>IoT Hub에서 데이터 스트림 입력 만들기
Azure Iot 허브는 IoT 시나리오에 최적화된, 확장성이 뛰어난 게시-구독 이벤트 처리기입니다.

스트림 분석에서 IoT hub에서 오는 이벤트의 hello 기본 타임 스탬프는 hello IoT hub에 도착 한 이벤트 hello hello 타임 스탬프는 `EventEnqueuedUtcTime`합니다. hello를 사용 해야 합니다 tooprocess hello 이벤트 페이로드의 타임 스탬프를 사용 하 여 스트림으로 데이터를 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) 키워드입니다.

> [!NOTE]
> `DeviceClient` 속성으로 전송된 메시지만 처리할 수 있습니다.
> 
> 

### <a name="consumer-groups"></a>소비자 그룹
각 스트림 분석 IoT 허브 입력된 toohave 자체 소비자 그룹을 구성 해야 합니다. 작업에 셀프 조인이 포함되거나 입력이 여러 개인 경우 둘 이상의 판독기 다운스트림으로 일부 입력을 읽을 수 있습니다. 이 경우 hello 수의 판독기는 하나의 소비자 그룹의 영향을 줍니다. tooavoid 초과 hello Azure IoT Hub 소비자 그룹 파티션당 당 5 개 독자, 것 제한은 각 스트림 분석 작업에 대 한 소비자 그룹 모범 사례 toodesignate입니다.

### <a name="configure-an-iot-hub-as-a-data-stream-input"></a>데이터 스트림 입력으로 IoT Hub 구성
hello 다음 표에서 설명의 각 속성에 hello **새 입력** 블레이드 hello 입력으로 IoT hub를 구성한 경우 Azure 포털의에서.

| 속성 | 설명 |
| --- | --- |
| **입력 별칭** |이 입력 쿼리 tooreference hello 작업에서에서 사용 하는 이름입니다.|
| **IoT Hub** |입력으로 hello IoT 허브 toouse의 hello 이름입니다. |
| **끝점** |hello IoT 허브에 대 한 hello 끝점입니다.|
| **공유 액세스 정책 이름** |액세스 toohello IoT 허브를 제공 하는 hello 공유 액세스 정책입니다. 각 공유 액세스 정책에는 이름, 사용자가 설정한 사용 권한 및 액세스 키가 있습니다. |
| **공유 액세스 정책 키** |hello 공유 액세스 키 tooauthorize 액세스 toohello IoT 허브를 사용합니다. |
| **소비자 그룹**(선택 사항) |hello 소비자 그룹 toouse tooingest 데이터 hello IoT 허브에서입니다. 소비자 그룹이 지정 되어 스트림 분석 작업 hello 기본 소비자 그룹이 사용 됩니다. 각 Stream Analytics 작업마다 서로 다른 소비자 그룹을 사용하는 것이 좋습니다. |
| **이벤트 직렬화 형식** |hello serialization 형식 (JSON, CSV 또는 Avro) hello 들어오는 데이터 스트림을입니다. |
| **Encoding** |U t F-8만 지원 hello 인코딩 형식을 현재입니다. |

데이터는 IoT 허브에 도달할 경우 해야 스트림 분석 쿼리의 메타 데이터 필드를 다음 액세스 toohello:

| 속성 | 설명 |
| --- | --- |
| **EventProcessedUtcTime** |hello 날짜 및 시간에 해당 hello 이벤트가 처리 되었습니다. |
| **EventEnqueuedUtcTime** |hello 날짜 및 시간 hello IoT 허브에서 해당 hello 이벤트를 수신 했습니다. |
| **PartitionId** |hello hello 입력된 어댑터에 대 한 0부터 시작 파티션 ID입니다. |
| **IoTHub.MessageId** | 가 IoT 허브에서 toocorrelate 양방향 통신을 사용 하는 ID입니다. |
| **IoTHub.CorrelationId** |IoT Hub에서 메시지 응답 및 피드백에 사용되는 ID입니다. |
| **IoTHub.ConnectionDeviceId** |hello 인증 ID toosend이이 메시지를 사용합니다. 이 값은 hello IoT hub에서 servicebound 메시지에 표시 됩니다. |
| **IoTHub.ConnectionDeviceGenerationId** |hello 생성 ID의 hello 장치를 사용 하는 toosend이이 메시지를 인증 합니다. 이 값은 hello IoT hub에서 servicebound 메시지에 표시 됩니다. |
| **IoTHub.EnqueuedTime** |hello IoT hub에서 hello 메시지를 수신한 hello 시간입니다. |
| **IoTHub.StreamId** |Hello 보낸 사람에 게 장치에서 추가 사용자 지정 이벤트 속성입니다. |


## <a name="create-data-stream-input-from-blob-storage"></a>Blob Storage에서 데이터 스트림 입력 만들기
대량의 구조화 되지 않은 데이터 toostore hello 클라우드에서 사용 하는 시나리오에 대 한 Azure Blob 저장소 비용 효율적이 고 확장 가능한 솔루션을 제공합니다. 일반적으로 Blob Storage의 데이터는 미사용 데이터로 간주됩니다. 그러나 Stream Analytics에서 데이터 스트림으로 처리할 수 있습니다. Stream Analytics에서 Blob Storage 입력에 대한 일반적인 시나리오는 로그 처리입니다. 이 시나리오에서는 원격 분석 데이터는 시스템에서 캡처된 및 요구 toobe 구문 분석 하 고 tooextract 의미 있는 데이터를 처리 합니다.

hello 스트림 분석에서 Blob 스토리지 이벤트의 기본 타임 스탬프는 blob hello hello timestamp 마지막으로 수정한 변수인 `BlobLastModifiedUtcTime`합니다. hello를 사용 해야 합니다 tooprocess hello 이벤트 페이로드의 타임 스탬프를 사용 하 여 스트림으로 데이터를 hello [TIMESTAMP BY](https://msdn.microsoft.com/library/azure/dn834998.aspx) 키워드입니다.

CSV 형식의 입력 *필요* 머리글 행 toodefine hello 데이터 집합에 대 한 필드입니다. 또한 모든 헤더 행 필드는 고유해야 합니다.

> [!NOTE]
> 스트림 분석 콘텐츠 tooan 기존 blob을 추가 하는 것을 지원 하지 않습니다. 스트림 분석 한 번만 blob를 볼 및 hello 작업 hello 데이터 읽기 후 hello blob에서 발생 하는 변경 내용을 처리 되지 않습니다. 가장 좋은 방법은 tooupload 모든 hello 데이터를 한 번은 하 고 이벤트 toothat blob 저장소를 추가 하지 합니다.
> 

### <a name="configure-blob-storage-as-a-data-stream-input"></a>데이터 스트림 입력으로 Blob Storage 구성

hello 다음 표에서 설명의 각 속성에 hello **새 입력** 블레이드 hello 입력으로 Blob 저장소를 구성할 때 Azure 포털의에서.

| 속성 | 설명 |
| --- | --- |
| **입력 별칭** | 이 입력 쿼리 tooreference hello 작업에서에서 사용 하는 이름입니다. |
| **저장소 계정** | hello hello 저장소 계정의 이름으로는 hello blob 파일의 위치입니다. |
| **저장소 계정 키** | hello 저장소 계정과 연결 된 hello 비밀 키입니다. |
| **컨테이너** | hello blob 입력에 대 한 hello 컨테이너입니다. 컨테이너는 hello Microsoft Azure Blob 서비스에에서 저장 된 blob에 대 한 논리적 그룹화를 제공 합니다. Blob toohello Azure Blob 저장소 서비스에 업로드할 때 해당 blob에 대 한 컨테이너를 지정 해야 합니다. |
| **경로 패턴**(선택 사항) | hello 파일 경로 hello 지정 된 컨테이너 내에서 toolocate hello blob을 사용 합니다. Hello 경로 내 hello 세 개의 변수를 다음의 하나 이상의 인스턴스를 지정할 수 있습니다: `{date}`, `{time}`, 또는`{partition}`<br/><br/>예 1: `cluster1/logs/{date}/{time}/{partition}`<br/><br/>예 2: `cluster1/logs/{date}`<br/><br/>hello `*` 문자 hello 경로 접두사에 대 한 허용된 된 값이 아닙니다. 유효한 <a HREF="https://msdn.microsoft.com/library/azure/dd135715.aspx">Azure Blob 문자</a>만 허용됩니다. |
| **날짜 형식**(선택 사항) | Hello 경로에 hello 날짜 변수를 사용 하는 경우 hello 날짜 형식을 hello 파일 구성 됩니다. 예: `YYYY/MM/DD` |
| **시간 형식**(선택 사항) |  Hello 경로에 hello 시간 변수를 사용 하는 경우 hello 시간 형식을 hello 파일 구성 됩니다. 현재 hello만 지원 값은 `HH`합니다. |
| **이벤트 직렬화 형식** | hello serialization 형식 (JSON, CSV 또는 Avro) 들어오는 데이터 스트림에입니다. |
| **Encoding** | CSV 및 JSON의 경우 u t F-8만 지원 hello 인코딩 형식을 현재입니다. |

Blob 저장소 원본에서 데이터를 가져온 다음 메타 데이터 스트림 분석 쿼리의 필드 액세스 toohello 있는:

| 속성 | 설명 |
| --- | --- |
| **BlobName** |이벤트 hello hello 입력된 blob의 hello 이름이 제공 되었습니다. |
| **EventProcessedUtcTime** |hello 날짜 및 시간에 해당 hello 이벤트 스트림 분석에서 처리 합니다. |
| **BlobLastModifiedUtcTime** |hello 날짜 및 시간 hello blob은 마지막으로 수정 된 합니다. |
| **PartitionId** |hello hello 입력된 어댑터에 대 한 0부터 시작 파티션 ID입니다. |

예를 들어 이러한 필드를 사용 하 여 다음 예제는 hello와 같은 쿼리를 작성할 수 있습니다.

````
SELECT
    BlobName,
    EventProcessedUtcTime,
    BlobLastModifiedUtcTime
FROM Input
````

## <a name="get-help"></a>도움말 보기
추가 지원이 필요한 경우 [Azure Stream Analytics 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)을 참조하세요.

## <a name="next-steps"></a>다음 단계
Stream Analytics 작업을 위한 Azure의 데이터 연결 옵션에 대해 알아보았습니다. 스트림 분석에 대해 자세히 toolearn 참조:

* [Azure Stream Analytics 사용 시작](stream-analytics-real-time-fraud-detection.md)
* [Azure  Stream Analytics 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure  Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
