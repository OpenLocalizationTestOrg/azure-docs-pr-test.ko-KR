---
title: "Azure 데이터 레이크 저장소에 대 한 진단 로그 aaaViewing | Microsoft Docs"
description: "이해 어떻게 Azure 데이터 레이크 저장소에 대 한 진단 로그 toosetup 및 액세스 "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Azure Data Lake Store에 대한 진단 로그에 액세스
데이터 레이크 저장소 계정과 tooview hello 기록 하는 방법에 대 한 진단 로깅 tooenable 계정에 대해 수집 하는 방법에 대해 알아봅니다.

조직 계정 toocollect 데이터 액세스 감사 내역은 hello 데이터, hello 데이터를 액세스 하는 빈도, 데이터의 크기를 액세스 하는 사용자의 목록과 같은 정보를 제공 하는 hello에 저장 되는 Azure 데이터 레이크 저장소에 대 한 진단 로깅을 사용 하도록 설정할 수 있습니다. 계정, 등입니다.

## <a name="prerequisites"></a>필수 조건
* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure Data Lake Store 계정**. Hello 지침에 따라 [hello Azure 포털을 사용 하 여 Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)합니다.

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Data Lake Store 계정에 대한 진단 로깅 사용
1. 새 toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.
2. Data Lake Store 계정을 열고 Data Lake Store 계정 블레이드에서 **설정**, **진단 로그**를 차례로 클릭합니다.
3. Hello에 **진단 로그** 블레이드에서 클릭 **진단을 설정**합니다.

    ![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "진단 로그 사용")

3. Hello에 **진단** 블레이드에서 다음 변경 내용을 tooconfigure 진단 로깅 hello를 확인 합니다.
   
    ![진단 로깅 사용](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "진단 로그 사용")
   
   * 설정 **상태** 너무**에** tooenable 진단 로깅.
   * 다양 한 방식에서 toostore/프로세스 hello 데이터를 선택할 수 있습니다.
     
        * 너무 hello 옵션을 선택**tooa 저장소 계정 보관** toostore tooan Azure 저장소 계정을 기록 합니다. Tooarchive hello 데이터 될 일괄 처리는 나중에이 옵션을 사용 합니다. 이 옵션을 선택 하는 경우 toosave hello 로그를 Azure 저장소 계정을 제공 해야 합니다.
        
        * Hello 옵션을 너무 선택**스트림 tooan 이벤트 허브** toostream 로그 데이터 tooan Azure 이벤트 허브입니다. 다운스트림 처리 하는 경우이 옵션을 사용 합니다 대개 tooanalyze 들어오는 실시간으로 로그, 파이프라인. 이 옵션을 선택 하는 경우에 hello toouse를 원하는 Azure 이벤트 허브에 대 한 hello 세부 정보를 제공 해야 합니다.

        * Hello 옵션을 너무 선택**tooLog 분석 보내기** toouse hello Azure 로그 분석 서비스 tooanalyze hello 생성 된 로그 데이터입니다. 이 옵션을 선택 하는 경우 hello에 대 한 정보 hello Operations Management Suite 작업 영역을 사용 하 여 hello 로그 분석을 수행 합니다 제공 해야 합니다.
     
   * Tooget 감사 로그 나 요청 로그 중 하나 또는 둘 다에 사용할지를 지정 합니다.
   * Hello hello 데이터를 유지 해야 하는 일 수를 지정 합니다. 보존은 Azure 저장소 계정 tooarchive 로그 데이터를 사용 하는 경우에 적용할 수만 있습니다.
   * **Save**를 클릭합니다.

진단 설정을 사용 하도록 설정한 후 hello hello에 로그를 볼 수 있습니다 **진단 로그** 탭 합니다.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>Data Lake Store 계정에 대한 진단 로그 보기
데이터 레이크 저장소 계정에 대 한 tooview hello 로그 데이터는 두 가지가.

* Hello Data Lake 저장소 계정에서 설정을 확인합니다
* Hello 데이터가 저장 되는 hello Azure 저장소 계정에서

### <a name="using-hello-data-lake-store-settings-view"></a>Hello를 사용 하 여 데이터 레이크 저장소 설정 보기
1. Data Lake Store 계정 **설정** 블레이드에서 **진단 로그**를 클릭합니다.
   
    ![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "진단 로그 보기") 
2. Hello에 **진단 로그** 블레이드를 표시 되어야 hello 로그에 의해 분류 **감사 로그** 및 **요청 로그**합니다.
   
   * 요청 로그 hello Data Lake 저장소 계정에서 수행 된 모든 API 요청을 캡처합니다.
   * 감사 로그는 유사한 toorequest 로그 되지만 더욱 세부적인된 분석 hello Data Lake 저장소 계정에서 수행 되는 hello 작업을 제공 합니다. 예를 들어 hello 감사 로그에서 "추가" 작업을 여러 개 요청 로그에서 단일 업로드 API 호출이 발생할 수 있습니다.
3. Hello 클릭 **다운로드** 링크 각각에 대해 항목 toodownload hello 로그를 로그 합니다.

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a>로그 데이터를 포함 하는 hello Azure 저장소 계정에서
1. 로깅에 대 한 데이터 레이크 저장소와 관련 된 hello Azure 저장소 계정 블레이드 열고 Blob을 클릭 합니다. hello **Blob 서비스** 블레이드에 두 개의 컨테이너를 나열 합니다.
   
    ![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "진단 로그 보기")
   
   * hello 컨테이너 **insights 로그 감사** hello 감사 로그를 포함 합니다.
   * hello 컨테이너 **insights 로그 요청이** hello 요청 로그를 포함 합니다.
2. 이러한 컨테이너 내에서 hello 로그 hello 구조를 다음으로 저장 됩니다.
   
    ![진단 로깅 보기](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "진단 로그 보기")
   
    예를 들어 hello 전체 경로 tooan 감사 로그 수 있습니다.`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    마찬가지로, hello 전체 경로 tooa 요청 로그 수 있습니다.`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-hello-structure-of-hello-log-data"></a>Hello 로그 데이터의 hello 구조 이해
hello 감사 및 요청 로그는 JSON 형식에서입니다. 이 섹션에서는 요청에 대 한 JSON의 hello 구조를 확인 하 고 감사 로그 합니다.

### <a name="request-logs"></a>요청 로그
Hello JSON 형식의 요청 로그에서 샘플 항목 다음과 같습니다. 각 Blob는 **레코드** 라는 하나의 루트 개체를 포함하며 여기에는 로그 개체의 배열이 포함됩니다.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>요청 로그 스키마
| Name | 형식 | 설명 |
| --- | --- | --- |
| 실시간 |문자열 |hello 타임 스탬프 (UTC) hello 로그 |
| resourceId |문자열 |에 배치 되는 작업에 걸린 hello 리소스의 hello ID |
| 카테고리 |문자열 |hello 로그 범주입니다. 예: **Requests** |
| operationName |문자열 |기록 된 hello 작업의 이름입니다. 예를 들어 getfilestatus |
| resultType |문자열 |예를 들어 200 hello 연산의 hello 상태입니다. |
| callerIpAddress |문자열 |hello 요청을 만드는 hello 클라이언트의 hello IP 주소 |
| CorrelationId |문자열 |hello 로그 수 함께 사용 되는 toogroup는 관련된 로그 항목 집합의 hello id |
| ID |Object |hello 로그를 생성 하는 hello id |
| properties |JSON |자세한 내용은 다음을 참조하세요. |

#### <a name="request-log-properties-schema"></a>요청 로그 속성 스키마
| Name | 형식 | 설명 |
| --- | --- | --- |
| HttpMethod |문자열 |hello HTTP 메서드가 사용 hello 작업에 대 한 합니다. 예를 들어 GET |
| Path |문자열 |hello 경로 hello 작업에 수행 했습니다. |
| RequestContentLength |int |hello hello HTTP 요청의 콘텐츠 길이 |
| ClientRequestId |문자열 |이 요청을 고유 하 게 식별 하는 Id hello |
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
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>감사 로그 스키마
| Name | 형식 | 설명 |
| --- | --- | --- |
| 실시간 |문자열 |hello 타임 스탬프 (UTC) hello 로그 |
| resourceId |문자열 |에 배치 되는 작업에 걸린 hello 리소스의 hello ID |
| 카테고리 |문자열 |hello 로그 범주입니다. 예: **Audit**. |
| operationName |문자열 |기록 된 hello 작업의 이름입니다. 예를 들어 getfilestatus |
| resultType |문자열 |예를 들어 200 hello 연산의 hello 상태입니다. |
| CorrelationId |문자열 |hello 로그 수 함께 사용 되는 toogroup는 관련된 로그 항목 집합의 hello id |
| ID |Object |hello 로그를 생성 하는 hello id |
| properties |JSON |자세한 내용은 다음을 참조하세요. |

#### <a name="audit-log-properties-schema"></a>감사 로그 속성 스키마
| Name | 형식 | 설명 |
| --- | --- | --- |
| StreamName |문자열 |hello 경로 hello 작업에 수행 했습니다. |

## <a name="samples-tooprocess-hello-log-data"></a>샘플 tooprocess hello 로그 데이터
Azure 데이터 레이크 저장소 방법에 대 한 샘플을 제공 tooprocess hello 로그 데이터를 분석 하 고 있습니다. Hello에 있는 샘플을 찾을 수 있습니다 [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample)합니다. 

## <a name="see-also"></a>참고 항목
* [Azure 데이터 레이크 저장소 개요](data-lake-store-overview.md)
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)

