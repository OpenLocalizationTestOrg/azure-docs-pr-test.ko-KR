---
title: "진단 로그로 Azure 스트림 분석 aaaTroubleshoot | Microsoft Docs"
description: "어떻게 tooanalyze 진단에서에서 로그 스트림 분석 작업에서 Microsoft Azure에 알아봅니다."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>진단 로그를 사용하여 Azure Stream Analytics 문제 해결

경우에 따라 Azure Stream Analytics 작업이 예기치 않게 처리를 중지합니다. 중요 한 toobe 수 tootroubleshoot이 이벤트의 종류는 hello 이벤트는 예기치 않은 쿼리 결과, 연결 toodevices 또는 예기치 않은 서비스 중단으로 발생할 수 있습니다. hello 스트림 분석에서 진단 로그의 활용 발생 하 고 복구 시간을 줄일 때 문제의 원인을 hello를 식별 합니다.

## <a name="log-types"></a>로그 형식

Stream Analytics에서는 다음과 같은 두 가지 형식의 로그를 제공합니다. 
* [활동 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)(항상 켜짐). 활동 로그는 작업을 수행하는 작업에 대한 통찰력을 제공합니다.
* [진단 로그](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)(구성 가능). 진단 로그는 작업과 관련하여 발생하는 모든 항목에 대해 더 다양한 통찰력을 제공합니다. 진단 로그에 hello 작업이 만들어질 때 시작 및 종료 시간도 hello 작업이 삭제 됩니다. Hello 작업이 업데이트 되 고 실행 하는 동안 이벤트를 처리 합니다.

> [!NOTE]
> Azure 저장소, Azure 이벤트 허브 및 Azure 로그 분석 tooanalyze 일치 하지 않는 데이터와 같은 서비스를 사용할 수 있습니다. 가격 책정 모델 해당 서비스에 대 한 hello에 따라 요금이 청구 됩니다.
>

## <a name="turn-on-diagnostics-logs"></a>진단 로그 켜기

진단 로그는 기본적으로 **해제**되어 있습니다. tooturn 진단 로그에 다음이 단계를 완료 합니다.

1.  Toohello Azure 포털에에서 로그인 하 고 toohello 스트리밍 작업 블레이드로 이동 합니다. **모니터링** 아래에서 **진단 로그**를 선택합니다.

    ![블레이드 탐색 toodiagnostics 로그](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  **진단 켜기**를 선택합니다.

    ![진단 로그 켜기](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Hello에 **진단 설정을** 페이지에 대 한 **상태**선택, **에**합니다.

    ![진단 로그에 대한 상태 변경](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  원하는 hello 보관 대상 (저장소 계정, 이벤트 허브, 로그 분석)를 설정 합니다. 그런 다음 (실행, 작성) toocollect 로그의 hello 범주를 선택 합니다. 

5.  Hello 새 진단 구성을 저장 합니다.

hello 진단 구성에는 약 10 분 tootake 적용이 됩니다. 그 후 hello 로그 보관 hello 구성 대상에 나타나는 시작 (hello에서이 확인할 수 있습니다 **진단 로그** 페이지):

![블레이드 탐색 toodiagnostics 로그-보관 대상](./media/stream-analytics-job-diagnostic-logs/image4.png)

진단을 구성하는 방법에 대한 자세한 내용은 [Azure 리소스의 진단 데이터 수집 및 사용](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)을 참조하세요.

## <a name="diagnostics-log-categories"></a>진단 로그 범주

현재 두 가지 진단 로그 범주를 캡처합니다.

* **작성**. 캡처 작업을 제작 하는 관련된 toojob 된 이벤트 로그: 작업 만들기를 추가 하 고 입력 및 출력을 추가 하 고 hello 쿼리, 시작 및 중지 hello 작업 업데이트를 삭제 합니다.
* **실행**. 작업 실행 중 발생하는 이벤트를 캡처합니다.
    * 연결 오류
    * 다음을 포함하는 데이터 처리 오류
        * Toohello 따르지 않는 이벤트 쿼리 정의 (일치 하지 않는 필드 형식, 누락 된 필드 및 값 등)
        * 식 평가 오류
    * 다른 이벤트 및 오류

## <a name="diagnostics-logs-schema"></a>진단 로그 스키마

모든 로그는 JSON 형식으로 저장됩니다. 각 항목에 공통 문자열 필드에 따라 hello:

이름 | 설명
------- | -------
실시간 | 타임 스탬프 (UTC) hello 로그의 합니다.
resourceId | 작업 hello hello 리소스의 ID에 발생, 대문자로 합니다. Hello 구독 ID, hello 리소스 그룹 및 hello 작업 이름이 포함 됩니다. 예: **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT.STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
카테고리 | 로그 범주로, **실행** 또는 **작성** 중 하나입니다.
operationName | 기록 된 hello 작업의 이름입니다. 예를 들어 **이벤트 보내기: SQL 출력 쓰기 실패 toomysqloutput**합니다.
status | Hello 작업의 상태입니다. 예: **실패** 또는 **성공**.
최소 수준 | 로그 수준. 예: **오류**, **경고** 또는 **정보**.
properties | 로그 항목별 세부 정보로, JSON 문자열로 직렬화됩니다. 자세한 내용은 hello 다음 섹션을 참조 하세요.

### <a name="execution-log-properties-schema"></a>실행 로그 속성 스키마

실행 로그에는 Stream Analytics 작업 실행 중에 발생한 이벤트에 대한 정보가 포함됩니다. 속성의 hello 스키마 이벤트의 hello 유형에 따라 달라 집니다. 현재 실행 로그의 유형만 hello를 해야 합니다.

### <a name="data-errors"></a>데이터 오류

이 범주의 로그 hello 작업은 데이터를 처리 하는 동안 발생 하는 모든 오류가입니다. 이러한 로그는 데이터 읽기, serialization 및 쓰기 작업 도중에 가장 자주 생성됩니다. 이러한 로그는 연결 오류를 포함하지 않습니다. 연결 오류는 일반 이벤트로 처리됩니다.

이름 | 설명
------- | -------
원본 | Hello 작업의 이름 입력 또는 출력 hello 오류가 발생 했습니다.
Message | Hello 오류와 관련 된 메시지입니다.
형식 | 오류의 형식입니다. 예: **DataConversionError**, **CsvParserError** 또는 **ServiceBusPropertyColumnMissingError**.
Data | 유용한 데이터를 포함 tooaccurately hello hello 오류 소스를 찾습니다. 크기에 따라 제목 tootruncation 합니다.

Hello에 따라 **operationName** 값, 데이터 오류의 경우 스키마를 따르는 hello:
* **직렬화 이벤트**입니다. 직렬화 이벤트는 이벤트 읽기 작업 중에 발생합니다. Hello hello 입력 데이터에 맞지 않는 hello 쿼리 스키마 다음이 이유 중 하나에 대 한 경우 발생 합니다.
    * *이벤트 (de) 하는 동안 형식 불일치 serialize*: hello 오류가 발생 하는 hello 필드를 식별 합니다.
    * *이벤트, 잘못 된 직렬화를 읽을 수 없습니다*: hello 오류가 발생 hello 입력된 데이터에 hello 위치에 대 한 정보를 나열 합니다. Blob 이름이 blob 입력, 오프셋 및 hello 데이터의 샘플에 포함 됩니다.
* **전송 이벤트**. 전송 이벤트는 쓰기 작업 중에 발생합니다. Hello 스트리밍 hello 오류를 발생 시킨 이벤트를 식별 합니다.

### <a name="generic-events"></a>일반 이벤트

일반 이벤트는 다른 모든 항목을 처리합니다.

이름 | 설명
-------- | --------
오류 | (선택 사항) 오류 정보입니다. 일반적으로 사용 가능한 경우 예외 정보입니다.
Message| 로그 메시지
형식 | 메시지 형식입니다. 오류의 toointernal 분류를 매핑합니다. 예: **JobValidationError** 또는 **BlobOutputAdapterInitializationFailure**.
상관관계 ID | [GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) hello 작업이 실행을 고유 하 게 식별 합니다. 동일한 hello 작업 중지 hello 있을 때까지 hello 시간 hello에서 모든 실행 로그 항목에 시작 작업 **상관 관계 ID** 값입니다.

## <a name="next-steps"></a>다음 단계

* [소개 tooStream 분석](stream-analytics-introduction.md)
* [Stream Analytics 시작](stream-analytics-real-time-fraud-detection.md)
* [Stream Analytics 작업 크기 조정](stream-analytics-scale-jobs.md)
* [Stream Analytics 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Stream Analytics 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)
