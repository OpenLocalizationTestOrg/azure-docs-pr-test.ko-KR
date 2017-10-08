---
title: "Azure Data Lake 분석에 대 한 진단 로그 aaaViewing | Microsoft Docs"
description: "Toosetup 및 진단 액세스 기록 하는 방법에 대 한 Azure 데이터 레이크 분석 이해 "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Azure Data Lake Analytics에 대한 진단 로그에 액세스

진단 로깅 toocollect 데이터 액세스 감사 내역은 있습니다. 이러한 로그는 다음과 같은 정보를 제공합니다.

* Hello 데이터에 액세스 하는 사용자의 목록입니다.
* 얼마나 자주 hello 데이터 액세스 합니다.
* 데이터의 양을 hello 계정에 저장 됩니다.

## <a name="enable-logging"></a>로깅 사용

1. Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.

2. Data Lake 분석 계정을 열고 선택 **진단 로그** hello에서 __모니터__ 섹션. 다음으로, __진단 상태 켜기__를 선택합니다.

    ![진단 toocollect 감사를 켜고 요청 로그](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. __진단 설정을__hello 상태 too__On__를 설정 하 고 로깅 옵션을 선택 합니다.

    ![요청 로그 및 진단 toocollect 감사 설정](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "진단 로그를 사용 하도록 설정")

   * 설정 **상태** 너무**에** tooenable 진단 로깅.

   * 세 가지 방법으로 toostore/프로세스 hello 데이터를 선택할 수 있습니다.

     * 선택 __tooa 저장소 계정 보관__ toostore가 Azure 저장소 계정에 로그인 합니다. Tooarchive hello 데이터를 원하는 경우이 옵션을 사용 합니다. 이 옵션을 선택 하는 경우에 Azure 저장소 계정 toosave hello 로그를 제공 해야 합니다.

     * 선택 **tooan 이벤트 허브를 Stream** toostream 로그 데이터 tooan Azure 이벤트 허브입니다. 들어오는 로그를 실시간으로 분석하는 다운스트림 처리 파이프라인을 사용하는 경우 이 옵션을 사용합니다. 이 옵션을 선택 하는 경우에 hello toouse를 원하는 Azure 이벤트 허브에 대 한 hello 세부 정보를 제공 해야 합니다.

     * 선택 __tooLog 분석 보내기__ toosend hello 데이터 toohello 로그 분석 서비스입니다. 로그 분석 toogather toouse 원하는 로그를 분석 하는 경우이 옵션을 사용 합니다.
   * Tooget 감사 로그 나 요청 로그 중 하나 또는 둘 다에 사용할지를 지정 합니다.  요청 로그는 모든 API 요청을 캡처합니다. 감사 로그는 해당 API 요청에 의해 트리거되는 모든 작업을 기록합니다.

   * 에 대 한 __tooa 저장소 계정 보관__, hello tooretain hello 데이터 일 수를 지정 합니다.

   * __저장__을 클릭합니다.

        > [!NOTE]
        > 하나를 선택 해야 __tooa 저장소 계정 보관__, __tooan 이벤트 허브를 Stream__ 또는 __tooLog 분석 보내기__ hello 클릭 하기 전에 __저장__단추입니다.

진단 설정을 사용 하도록 설정한 후 toohello 반환할 수 있습니다 __진단 로그__ 블레이드 tooview hello 로그 합니다.

## <a name="view-logs"></a>로그 보기

### <a name="use-hello-data-lake-analytics-view"></a>Hello Data Lake 분석 보기를 사용 하 여

1. Data Lake 분석에서 블레이드에서 아래에서 계정 **모니터링**선택, **진단 로그** 및 항목 toodisplay 로그를 선택 합니다.

    ![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기")

2. hello 로그는로 분류 되어 **감사 로그** 및 **요청 로그**합니다.

    ![로그 항목](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * 요청 로그 hello Data Lake 분석 계정에 수행 된 모든 API 요청을 캡처합니다.
   * 감사 로그는 유사한 toorequest 로그 되지만 더욱 세부적인된 분석 hello 작업을 제공 합니다. 예를 들어, 요청 로그에서 단일 업로드 API 호출은 감사 로그에서 여러 "추가" 작업을 발생시킬 수 있습니다.

3. Hello 클릭 **다운로드** 로그 하는 로그 항목 toodownload에 대 한 링크입니다.

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a>로그 데이터를 포함 하는 hello Azure 저장소 계정 사용

1. 로깅에 대 한 연결 된 데이터 레이크 분석 hello Azure 저장소 계정 블레이드를 열고 클릭 __Blob__합니다. hello **Blob 서비스** 블레이드에 두 개의 컨테이너를 나열 합니다.

    ![진단 로깅 보기](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")

   * hello 컨테이너 **insights 로그 감사** hello 감사 로그를 포함 합니다.
   * hello 컨테이너 **insights 로그 요청이** hello 요청 로그를 포함 합니다.
2. 이러한 컨테이너 내에서 hello 로그 hello 구조를 다음으로 저장 됩니다.

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > hello `##` hello 경로에 항목이 hello 연도, 월, 일 및 어떤 hello 로그가 만들어진 시간을 포함 합니다. Data Lake Analytics는 1시간마다 하나의 파일을 만들므로 `m=`은(는) 항상 `00`의 값을 포함합니다.

    예를 들어 hello 전체 경로 tooan 감사 로그 될 수 있습니다.

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    마찬가지로, hello 전체 경로 tooa 요청 로그 수 수 있습니다.

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>로그 구조

hello 감사 및 요청 로그는 구조화 된 JSON 형식에서입니다.

### <a name="request-logs"></a>요청 로그

Hello JSON 형식의 요청 로그에서 샘플 항목 다음과 같습니다. 각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>요청 로그 스키마

| Name | 형식 | 설명 |
| --- | --- | --- |
| 실시간 |문자열 |hello 타임 스탬프 (UTC) hello 로그 |
| resourceId |문자열 |작업에서 걸리는 hello 리소스의 hello 식별자에 배치 |
| 카테고리 |문자열 |hello 로그 범주입니다. 예: **Requests** |
| operationName |문자열 |기록 된 hello 작업의 이름입니다. 예를 들어 GetAggregatedJobHistory |
| resultType |문자열 |예를 들어 200 hello 연산의 hello 상태입니다. |
| callerIpAddress |문자열 |hello 요청을 만드는 hello 클라이언트의 hello IP 주소 |
| CorrelationId |문자열 |hello 로그의 hello 식별자입니다. 이 값에 사용 되는 toogroup는 관련된 로그 항목 집합 수 있습니다. |
| ID |Object |hello 로그를 생성 하는 hello id |
| properties |JSON |자세한 내용은 hello 다음 섹션 (요청 로그 속성 스키마)를 참조 하십시오 |

#### <a name="request-log-properties-schema"></a>요청 로그 속성 스키마

| Name | 형식 | 설명 |
| --- | --- | --- |
| HttpMethod |문자열 |hello HTTP 메서드가 사용 hello 작업에 대 한 합니다. 예를 들어 GET |
| Path |문자열 |hello 경로 hello 작업에 수행 했습니다. |
| RequestContentLength |int |hello hello HTTP 요청의 콘텐츠 길이 |
| ClientRequestId |문자열 |이 요청을 고유 하 게 식별 하는 hello 식별자 |
| StartTime |문자열 |hello는 hello 받은 서버 hello 요청 시간 |
| EndTime |문자열 |hello 시간은 hello 서버 응답 전송 |

### <a name="audit-logs"></a>감사 로그

Hello JSON 형식 감사 로그에 샘플 항목 다음과 같습니다. 각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>감사 로그 스키마

| Name | 형식 | 설명 |
| --- | --- | --- |
| 실시간 |문자열 |hello 타임 스탬프 (UTC) hello 로그 |
| resourceId |문자열 |작업에서 걸리는 hello 리소스의 hello 식별자에 배치 |
| 카테고리 |문자열 |hello 로그 범주입니다. 예: **Audit**. |
| operationName |문자열 |기록 된 hello 작업의 이름입니다. 예를 들어 JobSubmitted |
| resultType |문자열 |Hello 작업 상태 (operationName)에 대 한 하위 상태입니다. |
| resultSignature |문자열 |Hello에 대 한 자세한 내용은 작업 상태 (operationName). |
| ID |문자열 |hello 작업을 요청한 hello 사용자입니다. 예: susan@contoso.com. |
| properties |JSON |자세한 내용은 hello 다음 섹션 (감사 로그 속성 스키마)를 참조 하십시오. |

> [!NOTE]
> **resultType** 및 **resultSignature** hello 결과 작업의 정보를 제공 하 고 작업을 완료 하는 경우에 값을 포함 합니다. 예를 들어 **operationName**이 **JobStarted** 또는 **JobEnded**의 값을 포함할 때 값을 포함합니다.
>
>

#### <a name="audit-log-properties-schema"></a>감사 로그 속성 스키마

| Name | 형식 | 설명 |
| --- | --- | --- |
| JobId |문자열 |hello ID 할당된 toohello 작업 |
| JobName |문자열 |hello 작업에 대해 제공 된 hello 이름 |
| JobRunTime |문자열 |hello 런타임 tooprocess hello 작업 사용 |
| SubmitTime |문자열 |hello 시간 (UTC)에 해당 hello 작업이 제출 된 |
| StartTime |문자열 |hello 시간 hello 작업 제출 (UTC)에서 실행이 시작 |
| EndTime |문자열 |hello 시간 hello 작업 종료 |
| 병렬 처리 |문자열 |데이터 레이크 분석 단위 제출 하는 동안이 작업에 대해 요청 된 hello 수 |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** 및 **Parallelism**은 작업에 대한 정보를 제공합니다. 해당 작업이 시작 또는 완료되는 경우 이러한 항목만 값을 포함합니다. 예를 들어 **SubmitTime** 만 후 값이 포함 된 **operationName** hello 값 **JobSubmitted**합니다.

## <a name="process-hello-log-data"></a>프로세스 hello 로그 데이터

Azure Data Lake 분석 방법에 대 한 샘플을 제공 tooprocess hello 로그 데이터를 분석 하 고 있습니다. Hello에 있는 샘플을 찾을 수 있습니다 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)합니다.

## <a name="next-steps"></a>다음 단계
* [Azure Data Lake Analytics 개요](data-lake-analytics-overview.md)
