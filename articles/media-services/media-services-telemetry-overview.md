---
title: "미디어 서비스 원격 분석 aaaAzure | Microsoft Docs"
description: "이 문서에서는 Azure 미디어 서비스 원격 분석에 대한 개요를 제공합니다."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 95c20ec4-c782-4063-8042-b79f95741d28
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 659e1c947a77aad0e4acacb541d95714da4775ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-telemetry"></a>Azure Media Services 원격 분석

Azure 미디어 서비스 AMS () 사용 하면 해당 서비스에 대 한 원격 분석/메트릭 데이터 tooaccess 있습니다. AMS의 현재 버전 hello를 사용 하면 실시간에 대 한 원격 분석 데이터를 수집 **채널**, **StreamingEndpoint**, 라이브 **보관** 엔터티. 

원격 분석 tooa 저장소 테이블을 지정 하는 Azure 저장소 계정에 기록 됩니다 (일반적으로 있습니다 사용 AMS 계정과 연결 된 hello 저장소 계정). 

hello 원격 분석 시스템 데이터 보존을 관리 하지 않습니다. Hello 저장소 테이블을 삭제 하 여 hello 오래 된 원격 분석 데이터를 제거할 수 있습니다.

이 항목에서는 방법을 tooconfigure 및 hello AMS 원격 분석을 사용 합니다.

## <a name="configuring-telemetry"></a>원격 분석 구성

구성 요소 세분성 수준에서 원격 분석을 구성할 수 있습니다. "Normal" 및 "Verbose"라는 두 가지 세부 수준이 있습니다. 두 수준 hello를 반환 하는 현재 동일한 정보입니다. Toouse "Normal 것이 좋습니다. 

항목 표시 방법을 다음 hello tooenable 원격 분석:

[.NET에서 원격 분석 사용](media-services-dotnet-telemetry.md) 

[REST에서 원격 분석 사용](media-services-rest-telemetry.md)

## <a name="consuming-telemetry-information"></a>이

원격 분석 hello 미디어 서비스 계정에 대 한 원격 분석을 구성할 때 지정한 hello 저장소 계정에서 Azure 저장소 테이블 tooan을 쓰여집니다. 이 섹션에서는 hello 메트릭에 대 한 hello 저장소 테이블을 설명 합니다.

Hello 같은 방법으로 다음 중 하나에 대 한 원격 분석 데이터를 사용할 수 있습니다.

- Azure 테이블 저장소 (예: hello 저장소 SDK 사용)에서 직접 데이터를 읽습니다. 원격 분석 저장소 테이블의 hello 설명 hello 참조 **원격 분석 정보를 사용해** 에 [이](https://msdn.microsoft.com/library/mt742089.aspx) 항목입니다.

또는

- 에 설명 된 대로 저장소 데이터를 읽기 위한 hello 지원을 hello 미디어 서비스.NET SDK에서에서 사용할 [이](media-services-dotnet-telemetry.md) 항목입니다. 


아래에서 설명 하는 hello 원격 분석 스키마가 디자인 된 toogive 좋은 성능을 hello Azure 테이블 저장소에 대 한 제한 내에서:

- 데이터는 계정 ID 및 서비스 ID로 분할에서 독립적으로 쿼리할 각 서비스 toobe tooallow 원격 분석 합니다.
- 파티션에는 hello 날짜 toogive hello 파티션 크기에 적절 한 상한 값을 포함 합니다.
- 역방향 시간 순서 tooallow hello 가장 최근의 원격 분석 항목 toobe에 행 키를 지정된 된 서비스에 대 한 쿼리 합니다.

그러면 수 대부분의 일반적인 쿼리 toobe hello 효율적인:

- 별도 서비스에 대한 데이터를 병렬로, 독립적으로 다운로드
- 날짜 범위 내에서 지정된 서비스에 대한 모든 데이터 검색
- 서비스에 대 한 hello 가장 최근 데이터를 검색 합니다.

### <a name="telemetry-table-storage-output-schema"></a>원격 분석 Table Storage 출력 스키마

원격 분석 데이터 집계 한 테이블에서 "TelemetryMetrics20160321" 여기서 "20160321"는 hello 만든 테이블의 날짜에에서 저장 됩니다. 원격 분석 시스템은 00:00 UTC 기반으로 각 날마다 별도의 테이블을 만듭니다. hello 테이블 사용 toostore 되풀이 값와 같은 시간, 보낸 바이트 수 등의 지정된 된 창 내에서 비트 전송률을 수집 합니다. 

속성|값|예제/참고 사항
---|---|---
PartitionKey|{account ID}_{entity ID}|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66<br/<br/>계정에 여러 미디어 서비스 계정을 toohello를 작성 하는 hello 파티션 키 toosimplify 워크플로 ID가 포함 hello 동일한 저장소 계정입니다.
RowKey|{초 toomidnight} _ {임의의 값을 (를)|01688_00199<br/><br/>hello 행 키는 파티션 내의 초 toomidnight tooallow 상위 n 스타일 쿼리 hello 수로 시작합니다. 자세한 내용은 [이](../cosmos-db/table-storage-design-guide.md#log-tail-pattern) 문서를 참조하세요. 
Timestamp|날짜/시간|Hello 2016 Azure 테이블의에서 타임 스탬프를 자동으로-09-09T22:43:42.241Z
형식|hello 유형의 원격 분석 데이터를 제공 하는 hello 엔터티|Channel/StreamingEndpoint/Archive<br/><br/>이벤트 형식은 문자열 값입니다.
이름|hello 원격 분석 이벤트의 hello 이름|ChannelHeartbeat/StreamingEndpointRequestLog
ObservedTime|hello 시간 hello 원격 분석 이벤트가 발생 (UTC)|2016-09-09T22:42:36.924Z<br/><br/>hello 관찰 시간은 hello 엔터티 보내는 hello 원격 분석 (예: 채널)에서 제공 됩니다. 구성 요소 간에 시간 동기화 문제가 있을 수 있으므로 이 값은 근사치입니다.
ServiceID|{service ID}|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
엔터티별 속성|Hello 이벤트에 의해 정의 된 대로|StreamName: stream1, Bitrate 10123, …<br/><br/>hello 나머지 속성은 지정 된 이벤트 유형의으로 hello에 대 한 정의 됩니다. Azure 테이블 콘텐츠는 키/값 쌍입니다.  (즉, 다른 행에 hello 테이블이 다른 속성 집합이).

### <a name="entity-specific-schema"></a>엔터티별 스키마

세 가지 방법으로 다음 주파수 hello로 푸시 각 엔터티 관련 가져오고 데이터 항목의 수 있습니다:

- 스트리밍 끝점: 30초 간격
- 라이브 채널: 1분 간격
- 라이브 보관: 1분 간격

**스트리밍 끝점**

자산|값|예
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Azure 테이블에서의 자동 타임스탬프 2016-09-09T22:43:42.241Z
형식|형식|StreamingEndpoint
이름|이름|StreamingEndpointRequestLog
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|서비스 ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
HostName|Hello 끝점의 호스트 이름|builddemoserver.origin.mediaservices.windows.net
StatusCode|레코드 HTTP 상태|200
ResultCode|결과 코드 세부 정보|S_OK
RequestCount|Hello 집계의 총 요청|3
BytesSent|집계된 보낸 바이트 수|2987358
ServerLatency|평균 서버 대기 시간(저장소 포함)|129
E2ELatency|평균 종단 간 대기 시간|250

**라이브 채널**

자산|값|예제/참고 사항
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Hello 2016 Azure 테이블의에서 타임 스탬프를 자동으로-09-09T22:43:42.241Z
형식|형식|채널
이름|이름|ChannelHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|서비스 ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
TrackType|비디오/오디오/텍스트 트랙 유형|비디오/오디오
TrackName|Hello 트랙의 이름이|video/audio_1
Bitrate|트랙 비트 전송률|785000
CustomAttributes||   
IncomingBitrate|실제 들어오는 비트 전송률|784548
OverlapCount|Hello에 중복 수집|0
DiscontinuityCount|트랙 불연속성|0
LastTimestamp|마지막으로 수집된 데이터 타임스탬프|1800488800
NonincreasingCount|조각 타임 스탬프 toonon 증가 인해 삭제 수|2
UnalignedKeyFrames|키 프레임이 정렬되지 않은 조각을 수신했는지 여부(전체 품질 수준) |True
UnalignedPresentationTime|프레젠테이션 시간이 정렬되지 않은 조각을 수신했는지 여부(전체 품질 수준/트랙)|True
UnexpectedBitrate|오디오/비디오 트랙의 계산된/실제 비트 전송률이 40,000bps보다 크고 IncomingBitrate == 0, 또는 IncomingBitrate 및 actualBitrate이 50% 다른 경우 True |True
Healthy|다음과 같은 경우 True <br/>overlapCount, <br/>DiscontinuityCount, <br/>NonIncreasingCount, <br/>UnalignedKeyFrames, <br/>UnalignedPresentationTime, <br/>UnexpectedBitrate<br/> 위 항목이 모두 0|True<br/><br/>정상은 때 다음 조건 보류 hello false를 반환 하는 복합 함수가입니다.<br/><br/>- OverlapCount > 0<br/>- DiscontinuityCount > 0<br/>- NonincreasingCount > 0<br/>- UnalignedKeyFrames == True<br/>- UnalignedPresentationTime == True<br/>- UnexpectedBitrate == True

**라이브 보관**

자산|값|예제/참고 사항
---|---|---
PartitionKey|PartitionKey|e49bef329c29495f9b9570989682069d_64435281c50a4dd8ab7011cb0f4cdf66
RowKey|RowKey|01688_00199
Timestamp|Timestamp|Hello 2016 Azure 테이블의에서 타임 스탬프를 자동으로-09-09T22:43:42.241Z
형식|형식|보관
이름|이름|ArchiveHeartbeat
ObservedTime|ObservedTime|2016-09-09T22:42:36.924Z
ServiceID|서비스 ID|f70bd731-691d-41c6-8f2d-671d0bdc9c7e
ManifestName|프로그램 URL|asset-eb149703-ed0a-483c-91c4-e4066e72cce3/a0a5cfbf-71ec-4bd2-8c01-a92a2b38c9ba.ism
TrackName|Hello 트랙의 이름이|audio_1
TrackType|Hello 트랙의 유형|오디오/비디오
CustomAttribute|동일한 이름 및 비트 전송률을 갖는 다른 트랙 간을 구분하는 16진수 문자열(다중 카메라 각도)|
Bitrate|트랙 비트 전송률|785000
Healthy|FragmentDiscardedCount == 0 && ArchiveAcquisitionError == False인 경우 True|True (이 두 값은 hello 메트릭에 존재 하지 않는 hello 원본 이벤트에)<br/><br/>정상은 때 다음 조건 보류 hello false를 반환 하는 복합 함수가입니다.<br/><br/>- FragmentDiscardedCount > 0<br/>- ArchiveAcquisitionError == True

## <a name="general-qa"></a>일반 질문과 답변

### <a name="how-tooconsume-metrics-data"></a>어떻게 tooconsume 메트릭 데이터?

메트릭 데이터는 hello 고객 저장소 계정에 일련의 Azure 테이블으로 저장 됩니다. Hello 다음 도구를 사용 하 여이 데이터를 사용할 수 있습니다.

- AMS SDK
- Microsoft Azure 저장소 탐색기 (내보내기 toocomma 구분 된 값 형식 및 처리에서 Excel 지원)
- REST API

### <a name="how-toofind-average-bandwidth-consumption"></a>어떻게 toofind 평균 대역폭 사용량을?

hello 평균 대역폭 사용량은 시간 기간 동안 BytesSent의 hello 평균입니다.

### <a name="how-toodefine-streaming-unit-count"></a>어떻게 toodefine 스트리밍 단위 수 있습니까?

스트리밍 단위 수가 hello 하나의 스트리밍 끝점의 최대 처리량 hello로 나눈 hello 서비스 스트리밍 끝점에서 hello 최대 처리량으로 정의할 수 있습니다. 하나의 스트리밍 끝점의 hello 사용량이 가장 많을 때 사용할 수 있는 처리량은 160 Mbps입니다.
예를 들어, 고객의 서비스에서 hello 최대 처리량이 40mbps (hello 최대값인 BytesSent 시간 기간 동안). 그런 다음, 스트리밍 단위 수가 hello이 같으면 too(40 MBps) * (8 비트/바이트) /(160 Mbps) = 2 스트리밍 단위입니다.

### <a name="how-toofind-average-requestssecond"></a>어떻게 toofind 평균 요청 수/초?

toofind hello 평균 수의 요청 수/초, 시간 기간 동안 hello (RequestCount) 요청의 평균 수를 계산합니다.

### <a name="how-toodefine-channel-health"></a>어떻게 toodefine 채널 상태?

채널 상태 hello 다음 조건 중 하나를 저장할 때 false 되도록 복합 부울 함수도 정의할 수 있습니다.

- OverlapCount > 0
- DiscontinuityCount > 0
- NonincreasingCount > 0
- UnalignedKeyFrames == True 
- UnalignedPresentationTime == True 
- UnexpectedBitrate == True


### <a name="how-toodetect-discontinuities"></a>어떻게 toodetect 불연속?

모든 채널 데이터 항목을 검색 하는 toodetect 불연속 여기서 DiscontinuityCount > 0입니다. hello 해당 ObservedTime 타임 스탬프 hello 번 hello 불연속 발생 한 시간을 나타냅니다.

### <a name="how-toodetect-timestamp-overlaps"></a>어떻게 toodetect 타임 스탬프 겹치는?

모든 채널 데이터 항목을 검색 하는 toodetect 타임 스탬프 overlaps 여기서 OverlapCount > 0입니다. hello 해당 ObservedTime 타임 스탬프는 hello에 타임 스탬프 겹치는 번 발생 하는 hello를 나타냅니다.

### <a name="how-toofind-streaming-request-failures-and-reasons"></a>Toofind 스트리밍 요청 하려면 어떻게 실패 한 이유?

toofind 스트리밍 요청 실패 및 이유로 모든 스트리밍 끝점 데이터 항목을 찾을 ResultCode 하지 않은 경우에 같은 tooS_OK 합니다. hello 해당 StatusCode 필드 hello 요청 실패에 대 한 hello 이유를 나타냅니다.

### <a name="how-tooconsume-data-with-external-tools"></a>어떻게 외부 도구를 사용 하 여 tooconsume 데이터?

가져오고 데이터를 처리 하 고 시각화 도구를 수행 하는 hello 수 있습니다.

- PowerBI
- Application Insights
- Azure Monitor(이전의 Shoebox)
- AMS 라이브 대시보드
- Azure Portal(릴리스 보류 중)

### <a name="how-toomanage-data-retention"></a>어떻게 toomanage 데이터 보존?

hello 원격 분석 시스템 제공 하지 않습니다 데이터 보존 관리 또는 자동 삭제 이전 레코드. 따라서 toomanage 필요 하 고 hello 저장소 테이블에서 오래 된 레코드를 수동으로 삭제 합니다. 방법에 대 한 toostorage SDK를 참조할 수 있습니다 toodo 것입니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>피드백 제공

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
