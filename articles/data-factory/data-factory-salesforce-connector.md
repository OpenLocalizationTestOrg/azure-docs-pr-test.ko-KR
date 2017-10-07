---
title: "데이터 팩터리를 사용 하 여 Salesforce에서 aaaMove 데이터 | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 Salesforce에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Azure Data Factory를 사용하여 Salesforce에서 데이터 이동
이 문서는 Azure 데이터 팩터리 toocopy 데이터 hello 싱크 열의 hello에 나열 된 Salesforce tooany 데이터 저장소에서 복사 작업을 사용 하는 방법을 간략하게 설명 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 복사 작업 및 지원 되는 데이터 저장소 조합이 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

Azure Data Factory에는 현재 너무 Salesforce 로부터 데이터를 이동만 지원[싱크 데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats), 하지만 다른 데이터 저장소 tooSalesforce에서 데이터 이동을 지원 하지 않습니다.

## <a name="supported-versions"></a>지원되는 버전
이 커넥터는 지원의 Salesforce 버전에 따라 hello: Developer Edition, Professional Edition, Enterprise Edition 또는 무제한 버전입니다. 그리고 Salesforce 프로덕션, 샌드박스 및 사용자 지정 도메인에서 복사를 지원합니다.

## <a name="prerequisites"></a>필수 조건
* API 권한을 사용하도록 설정해야 합니다. [권한 집합에 따라 Salesforce에서 API 액세스를 사용하도록 설정하는 방법](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)
* Salesforce tooon 온-프레미스 데이터 저장소에서 데이터 toocopy 있어야 이상 데이터 관리 게이트웨이 2.0 온-프레미스 환경에 설치 합니다.

## <a name="salesforce-request-limits"></a>Salesforce 요청 제한
Salesforce에는 총 API 요청 수와 동시 API 요청 수에 대한 제한이 있습니다. 포인트 다음 참고 hello:

- 동시 요청 수가 hello hello 제한을 초과 하면 조절 작업이 발생 하 고 임의 오류가 표시 됩니다.
- Hello 제한 hello 총 요청 수를 초과 하면 hello Salesforce 계정 24 시간 동안 차단 됩니다.

또한 두 시나리오 모두에서 hello "REQUEST_LIMIT_EXCEEDED" 오류가 발생할 수 있습니다. Hello hello "API 요청 제한" 섹션을 참조 [Salesforce 개발자 제한](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) 을 참조 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 Salesforce의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Salesforce에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 샘플을 보려면 [JSON의 예: Salesforce tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-salesforce-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooSalesforce는 JSON 속성에 대 한 세부 정보를 제공 합니다. 

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소를 특정 toohello Salesforce 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **Salesforce**합니다. |예 |
| environmentUrl | Hello URL의 Salesforce 인스턴스를 지정 합니다. <br><br> -기본값은 " https://login.salesforce.com " 입니다. <br> -toocopy 데이터로 샌드박스 "https://test.salesforce.com"를 지정 합니다. <br> -사용자 지정 도메인에서 toocopy 데이터 지정, 예를 들어 "https://[domain].my.salesforce.com"입니다. |아니요 |
| username |Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다. |예 |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예 |
| securityToken |Hello 사용자 계정에 대 한 보안 토큰을 지정 합니다. 참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 방법에 대 한 보안 토큰 tooreset/get입니다. 보안 토큰에 대 한 toolearn 일반적으로 참조 [보안과 hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)합니다. |예 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. hello typeProperties hello 형식의 데이터 집합에 대 한 섹션 **RelationalTable** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| tableName |Salesforce에 hello 테이블의 이름입니다. |아니요(**RelationalSource**의 **query**가 지정된 경우) |

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용할 수 있는 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력과 출력 테이블 및 다양한 정책과 같은 속성은 모든 유형의 활동에 사용할 수 있습니다.

사용할 수 있는 hello 속성 hello hello에 hello 활동의 typeProperties 섹션 반면, 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

Hello 소스 hello 유형인 경우 복사 활동에서 **RelationalSource** (Salesforce 포함), 다음과 같은 속성 hello typeProperties 섹션에서 사용할 수 있는:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리입니다. 예제: `select * from MyTable__c` |더 (경우 hello **tableName** 의 hello **dataset** 지정) |

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>쿼리 팁
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>DateTime 열에서 where 절을 사용하여 데이터 검색
때 hello SOQL 또는 SQL 쿼리, 사용량 기준 과금 주의 toohello 날짜/시간 형식 차이 지정 합니다. 예:

* **SOQL 샘플**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **SQL 샘플**:
    * **복사 마법사 toospecify hello 쿼리를 사용 하 여:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **Toospecify hello 쿼리를 편집 하는 JSON을 사용 하 여 (이스케이프 문자 제대로):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Salesforce 보고서에서 데이터 검색
`{call "<report name>"}`과 같이 쿼리를 지정하여 Salesforce 보고서에서 데이터를 검색할 수 있으며 그 예는 다음과 같습니다. `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Salesforce 휴지통에서 삭제된 레코드 검색
Salesforce 휴지통에서 tooquery hello 소프트 삭제 된 레코드를 지정할 수 있습니다 **"IsDeleted = 1"** 쿼리에 합니다. 예를 들면 다음과 같습니다.

* 유일한 hello 삭제 레코드 tooquery 지정 "선택 * MyTable__c에서 **여기서 IsDeleted = 1**"
* 모든 기존 hello 및 hello 삭제를 비롯 한 레코드를 hello tooquery 지정 "선택 * MyTable__c에서 **여기서 IsDeleted = 0 또는 IsDeleted = 1**"

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>JSON의 예: Salesforce tooAzure Blob에서에서 데이터 복사
hello 다음 예에서는 샘플 JSON 정의 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 Salesforce tooAzure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.   

다음은 hello 데이터 팩터리 아티팩트의 toocreate tooimplement hello 시나리오 필요가 있다는 것입니다. hello 목록 다음에 나오는 hello 섹션에서는 이러한 단계에 대 한 세부 정보를 제공 합니다.

* Hello 형식의 연결 된 서비스 [Salesforce](#linked-service-properties)
* Hello 형식의 연결 된 서비스 [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* 입력 [dataset](data-factory-create-datasets.md) hello 형식의 [RelationalTable](#dataset-properties)
* 출력 [dataset](data-factory-create-datasets.md) hello 형식의 [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* [RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

**Salesforce 연결된 서비스**

이 예에서는 hello **Salesforce** 연결 된 서비스입니다. Hello 참조 [Salesforce에 연결 된 서비스](#linked-service-properties) 이 연결 된 서비스에서 지원 되는 hello 속성에 대 한 섹션.  참조 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) tooreset/get 보안 토큰을 hello 하는 방법에 대 한 지침은 합니다.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Azure 저장소 연결된 서비스**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```
**Salesforce 입력 데이터 집합**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**복사 작업을 포함하는 파이프라인**

hello 파이프라인에 포함 된 구성 된 복사 작업 toouse hello 입력 및 출력 데이터 집합 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource**, 및 hello **싱크** 형식이 너무 설정**BlobSink**합니다.

참조 [RelationalSource 형식 속성](#copy-activity-properties) hello hello RelationalSource에서 지원 되는 속성 목록에 대 한 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> 모든 사용자 지정 개체에 대 한 hello "__c" hello API 이름 부분이 필요 합니다.

![Data Factory - Salesforce 연결 - API 이름](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Salesforce에 대한 형식 매핑
| Salesforce 형식 | .NET 기반 형식 |
| --- | --- |
| 자동 번호 |문자열 |
| 확인란 |Boolean |
| 통화 |Double |
| Date |DateTime |
| 날짜/시간 |DateTime |
| Email |문자열 |
| Id |문자열 |
| 관계 조회 |문자열 |
| 다중 선택 선택 목록 |문자열 |
| Number |Double |
| 백분율 |Double |
| Phone |문자열 |
| 선택 목록 |문자열 |
| 텍스트 |문자열 |
| 텍스트 영역 |문자열 |
| 텍스트 영역(Long) |문자열 |
| 텍스트 영역(Rich) |문자열 |
| 텍스트(암호화됨) |문자열 |
| URL |문자열 |

> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>성능 및 튜닝
Hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 요소 것입니다.
