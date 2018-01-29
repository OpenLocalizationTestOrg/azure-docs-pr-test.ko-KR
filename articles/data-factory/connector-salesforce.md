---
title: "Azure Data Factory를 사용하여 Salesforce 간에 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory 파이프라인의 복사 작업을 사용하여 Salesforce에서 지원되는 싱크 데이터 저장소로, 또는 지원되는 원본 데이터 저장소에서 Salesforce로 데이터를 복사하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
ms.openlocfilehash: 7cd86922b0445fc81766ca54080e2fd3e64a6c61
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-fromto-salesforce-using-azure-data-factory"></a>Azure Data Factory를 사용하여 Salesforce 간에 데이터 복사
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [버전 1 - GA](v1/data-factory-salesforce-connector.md)
> * [버전 2 - 미리 보기](connector-salesforce.md)

이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Salesforce 간에 데이터를 복사하는 방법을 설명합니다. 이 문서는 복사 작업에 대한 일반적인 개요를 제공하는 [복사 작업 개요](copy-activity-overview.md) 문서를 기반으로 합니다.

> [!NOTE]
> 이 문서는 현재 미리 보기 상태인 Data Factory 버전 2에 적용됩니다. GA(일반 공급) 상태인 Data Factory 버전 1 서비스를 사용 중인 경우 [V1의 Salesforce 커넥터](v1/data-factory-salesforce-connector.md)를 참조하세요.

## <a name="supported-capabilities"></a>지원되는 기능

Salesforce에서 지원되는 싱크 데이터 저장소로 또는 지원되는 원본 데이터 저장소에서 Salesforce로 데이터를 복사할 수 있습니다. 복사 작업의 원본/싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats) 표를 참조하세요.

특히 이 Salesforce 커넥터는 다음을 지원합니다.

- **Developer Edition, Professional Edition, Enterprise Edition 또는 Unlimited Edition**과 같은 Salesforce 버전
- Salesforce **프로덕션, 샌드박스 및 사용자 지정 도메인** 간에 데이터 복사

## <a name="prerequisites"></a>필수 구성 요소

* Salesforce에서 API 권한을 사용하도록 설정해야 합니다. [권한 집합에 따라 Salesforce에서 API 액세스를 사용하도록 설정하는 방법](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)

## <a name="salesforce-request-limits"></a>Salesforce 요청 제한

Salesforce에는 총 API 요청 수와 동시 API 요청 수에 대한 제한이 있습니다. 다음 사항에 유의하세요.

- 동시 요청 수가 이 제한을 초과하면 제한이 발생하며 임의 오류가 표시됩니다.
- 총 요청 수가 이 제한을 초과하면 Salesforce 계정은 24시간 동안 차단됩니다.

두 시나리오 모두에서 "REQUEST_LIMIT_EXCEEDED" 오류가 나타날 수도 있습니다. 자세한 내용은 [Salesforce 개발자 제한](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) 문서의 “API 요청 제한” 섹션을 참조하세요.

## <a name="getting-started"></a>시작

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

다음 섹션에서는 Salesforce 커넥터에 한정된 데이터 팩터리 엔터티를 정의하는 데 사용되는 속성에 대해 자세히 설명합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성

Salesforce 연결된 서비스에 다음 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 |형식 속성은 **Salesforce**로 설정되어야 합니다. |적용 |
| environmentUrl | Salesforce 인스턴스의 URL을 지정합니다. <br> - 기본값은 `"https://login.salesforce.com"`입니다. <br> - 샌드박스에서 데이터를 복사하려면 `"https://test.salesforce.com"`을 지정합니다. <br> - 사용자 지정 도메인에서 데이터를 복사하려면 예를 들어 `"https://[domain].my.salesforce.com"`을 지정합니다. |아니요 |
| 사용자 이름 |사용자 계정의 사용자 이름을 지정합니다. |적용 |
| 암호 |사용자 계정으로 password를 지정합니다.<br/><br/>이 필드를 SecureString으로 표시하거나, ADF에 안전하게 저장하거나, Azure Key Vault에 암호를 저장하도록 선택하고 데이터 복사를 수행하는 경우 여기에서 복사 작업을 끌어올 수 있습니다. [Key Vault에서 자격 증명 저장](store-credentials-in-key-vault.md)에서 자세히 알아봅니다. |적용 |
| securityToken |사용자 계정에 대한 보안 토큰을 지정합니다. 보안 토큰을 재설정하거나 가져오는 방법에 대한 자세한 내용은 [보안 토큰 가져오기](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) 를 참조하세요. 일반적인 보안 토큰에 대해 자세히 알아보려면 [보안 및 API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm)를 참조하세요.<br/><br/>이 필드를 SecureString으로 표시하거나, ADF에 안전하게 저장하거나, Azure Key Vault에 보안 토큰을 저장하도록 선택하고 데이터 복사를 수행하는 경우 여기에서 복사 작업을 끌어올 수 있습니다. [Key Vault에서 자격 증명 저장](store-credentials-in-key-vault.md)에서 자세히 알아봅니다. |적용 |
| connectVia | 데이터 저장소에 연결하는 데 사용할 [Integration Runtime](concepts-integration-runtime.md)입니다. 지정하지 않으면 기본 Azure Integration Runtime을 사용합니다. | 원본에 연결된 서비스에 IR이 없는 경우 원본에는 아니요이고 싱크에는 예입니다. |

>[!IMPORTANT]
>데이터를 Salesforce**에** 복사할 때 기본 Azure Integration Runtime을 복사를 실행하는 데 사용할 수 없습니다. 즉, 원본에 연결된 서비스에 지정된 IR이 없는 경우 다음 예제와 같이 Salesforce 근처 위치를 사용하여 명시적으로 [Azure IR을 만들고](create-azure-integration-runtime.md#create-azure-ir) Salesforce 연결된 서비스에서 연결합니다.

**예: ADF에 자격 증명 저장**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
            },
            "securityToken": {
                "type": "SecureString",
                "value": "<security token>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

**예: Azure Key Vault에 자격 증명 저장**

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<username>",
            "password": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of password in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            },
            "securityToken": {
                "type": "AzureKeyVaultSecret",
                "secretName": "<secret name of security token in AKV>",
                "store":{
                    "referenceName": "<Azure Key Vault linked service>",
                    "type": "LinkedServiceReference"
                }
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성

데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합](concepts-datasets-linked-services.md) 문서를 참조하세요. 이 섹션에서는 Salesforce 데이터 집합에서 지원하는 속성의 목록을 제공합니다.

Salesforce 간에 데이터를 복사하려면 데이터 집합의 형식 속성을 **SalesforceObject**로 설정합니다. 다음과 같은 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | 형식 속성은 **SalesforceObject**로 설정되어야 합니다.  | 적용 |
| objectApiName | 데이터를 검색할 Salesforce 개체 이름입니다. | 원본에는 아니요이고 싱크에는 예입니다 |

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.

![Data Factory - Salesforce 연결 - API 이름](media/copy-data-from-salesforce/data-factory-salesforce-api-name.png)

**예제:**

```json
{
    "name": "SalesforceDataset",
    "properties": {
        "type": "SalesforceObject",
        "linkedServiceName": {
            "referenceName": "<Salesforce linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "objectApiName": "MyTable__c"
        }
    }
}
```

>[!NOTE]
>이전 버전과의 호환성을 위해 Salesforce에서 데이터를 복사하는 경우 이전 "RelationalTable" 형식 데이터 집합이 계속 작동하지만 새 "SalesforceObject" 형식으로 전환하는 것이 좋습니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | 데이터 집합의 type 속성을 **RelationalTable**로 설정해야 합니다. | 적용 |
| tableName | Salesforce에 있는 테이블의 이름입니다. | 아니요(작업 원본에서 "query"가 지정된 경우) |

## <a name="copy-activity-properties"></a>복사 작업 속성

작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인](concepts-pipelines-activities.md) 문서를 참조하세요. 이 섹션에서는 Salesforce 원본 및 싱크에서 지원하는 속성의 목록을 제공합니다.

### <a name="salesforce-as-source"></a>Salesforce를 원본으로

Salesforce에서 데이터를 복사하려면 복사 작업의 원본 형식을 **SalesforceSource**로 설정합니다. 복사 작업 **source** 섹션에서 다음 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | 복사 작업 원본의 형식 속성을 **SalesforceSource**로 설정해야 합니다. | 적용 |
| 쿼리 |사용자 지정 쿼리를 사용하여 데이터를 읽습니다. SQL-92 쿼리 또는 [SOQL(Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) 쿼리를 사용할 수 있습니다. 예: `select * from MyTable__c` | 아니요(데이터 집합의 "tableName"이 지정된 경우) |

> [!IMPORTANT]
> 모든 사용자 지정 개체에 대해 API 이름에 "__c" 부분이 필요합니다.

![Data Factory - Salesforce 연결 - API 이름](media/copy-data-from-salesforce/data-factory-salesforce-api-name-2.png)

**예제:**

```json
"activities":[
    {
        "name": "CopyFromSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Salesforce input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "SalesforceSource",
                "query": "SELECT Col_Currency__c, Col_Date__c, Col_Email__c FROM AllDataType__c"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

>[!NOTE]
>이전 버전과의 호환성을 위해 Salesforce에서 데이터를 복사하는 경우 이전 "RelationalSource" 형식 복사 원본이 계속 작동하지만 새 "SalesforceSource" 형식으로 전환하는 것이 좋습니다.

### <a name="salesforce-as-sink"></a>Salesforce를 싱크로

Salesforce에 데이터를 복사하려면 복사 작업의 싱크 형식을 **SalesforceSink**로 설정합니다. 복사 작업 **sink** 섹션에서 다음 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | 복사 작업 싱크의 형식 속성은 **SalesforceSink**로 설정해야 합니다. | 적용 |
| writeBehavior | 작업의 쓰기 동작입니다.<br/>허용되는 값은 **삽입** 및 **Upsert**입니다. | 아니요(기본값: 삽입) |
| externalIdFieldName | upsert 작업의 외부 ID 필드 이름입니다. 지정된 필드는 Salesforce 개체에서 "외부 ID 필드"로 정의되어야 하고 해당 입력 데이터에 NULL 값을 사용할 수 없습니다. | "Upsert"에서 예 |
| writeBatchSize | 각 일괄 처리에서 Salesforce에 작성된 데이터의 행 수입니다. | 아니요(기본값: 5000) |
| ignoreNullValues | 쓰기 작업 중에 입력 데이터에서 null 값을 무시할지를 나타냅니다.<br/>허용되는 값은 **true** 및 **false**입니다.<br>- **true**: upsert/업데이트 작업을 수행하는 경우 대상 개체의 데이터를 변경하지 않고, 삽입 작업을 수행하는 경우 정의된 기본값을 삽입합니다.<br/>- **false**: upsert/업데이트 작업을 수행하는 경우 대상 개체의 데이터를 NULL로 업데이트하고, 삽입 작업을 수행하는 경우 NULL 값을 삽입합니다. | 아니요(기본값: false) |

### <a name="example-salesforce-sink-in-copy-activity"></a>예: 복사 작업의 Salesforce 싱크

```json
"activities":[
    {
        "name": "CopyToSalesforce",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Salesforce output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "SalesforceSink",
                "writeBehavior": "Upsert",
                "externalIdFieldName": "CustomerId__c",
                "writeBatchSize": 10000,
                "ignoreNullValues": true
            }
        }
    }
]
```

## <a name="query-tips"></a>쿼리 팁

### <a name="retrieving-data-from-salesforce-report"></a>Salesforce 보고서에서 데이터 검색

쿼리를 `{call "<report name>"}`으로 지정하여 Salesforce 보고서에서 데이터를 검색할 수 있습니다. 예: `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Salesforce 휴지통에서 삭제된 레코드 검색

임시 삭제된 쿼리를 Salesforce 휴지통에서 쿼리하려면 쿼리에 **"IsDeleted = 1"**을 지정하면 됩니다. 예를 들면 다음과 같습니다.

* 삭제된 레코드만 쿼리하려면 "select * from MyTable__c **where IsDeleted= 1**"을 지정합니다.
* 기존 레코드와 삭제된 레코드를 포함하여 모든 레코드를 쿼리하려면 "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"을 지정합니다.

### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>DateTime 열에서 where 절을 사용하여 데이터 검색

SOQL 또는 SQL 쿼리를 지정할 때 DateTime 형식 차이에 주의해야 합니다. 예: 

* **SOQL 샘플**: `SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= @{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-ddTHH:mm:ssZ')} AND LastModifiedDate < @{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-ddTHH:mm:ssZ')}`
* **SQL 샘플**: `SELECT * FROM Account WHERE LastModifiedDate >= {ts'@{formatDateTime(pipeline().parameters.StartTime,'yyyy-MM-dd HH:mm:ss')}'} AND LastModifiedDate < {ts'@{formatDateTime(pipeline().parameters.EndTime,'yyyy-MM-dd HH:mm:ss')}'}"`

## <a name="data-type-mapping-for-salesforce"></a>Salesforce에 대한 데이터 형식 매핑

Salesforce에서 데이터를 복사할 경우 Salesforce 데이터 형식에서 Azure Data Factory 중간 데이터 형식으로 다음 매핑이 사용됩니다. 복사 작업에서 원본 스키마 및 데이터 형식을 싱크에 매핑하는 방법에 대한 자세한 내용은 [스키마 및 데이터 형식 매핑](copy-activity-schema-and-type-mapping.md)을 참조하세요.

| Salesforce 데이터 형식 | Data Factory 중간 데이터 형식 |
|:--- |:--- |
| 자동 번호 |문자열 |
| 확인란 |BOOLEAN |
| 통화 |Double |
| Date |Datetime |
| 날짜/시간 |Datetime |
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

## <a name="next-steps"></a>다음 단계
Azure Data Factory에서 복사 작업의 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats)를 참조하세요.