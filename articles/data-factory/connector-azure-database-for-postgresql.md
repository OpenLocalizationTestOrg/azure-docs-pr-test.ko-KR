---
title: "Azure Data Factory를 사용하여 Azure Database for PostgreSQL에서 데이터 복사 | Microsoft Docs"
description: "Azure Data Factory 파이프라인의 복사 작업을 사용하여 Azure Database for PostgreSQL에서 지원되는 싱크 데이터 저장소로 데이터를 복사하는 방법에 대해 알아봅니다."
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
ms.date: 11/30/2017
ms.author: jingwang
ms.openlocfilehash: adc8ebe282fa4e4b242924bf1fea9b62d704835e
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-from-azure-database-for-postgresql-using-azure-data-factory"></a>Azure Data Factory를 사용하여 Azure Database for PostgreSQL에서 데이터 복사 

이 문서에서는 Azure Data Factory의 복사 작업을 사용하여 Azure Database for PostgreSQL에서 데이터를 복사하는 방법에 대해 설명합니다. 이 문서는 복사 작업에 대한 일반적인 개요를 제공하는 [복사 작업 개요](copy-activity-overview.md) 문서를 기반으로 합니다.

> [!NOTE]
> 이 문서는 현재 미리 보기 상태인 Data Factory 버전 2에 적용됩니다. GA(일반 공급) 상태인 Data Factory 버전 1 서비스를 사용 중인 경우 [V1의 복사 작업](v1/data-factory-data-movement-activities.md)을 참조하세요.

## <a name="supported-capabilities"></a>지원되는 기능

Azure Database for PostgreSQL에서 지원되는 모든 싱크 데이터 저장소로 데이터를 복사할 수 있습니다. 복사 작업의 원본/싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats) 표를 참조하세요.

Azure Data Factory는 연결을 사용하는 기본 제공 드라이버를 제공합니다. 따라서 이 커넥터를 사용하여 드라이버를 수동으로 설치하지 않아도 됩니다.

## <a name="getting-started"></a>시작

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

다음 섹션에서는 Azure Database for PostgreSQL 커넥터에 한정된 Data Factory 엔터티를 정의하는 데 사용되는 속성에 대해 자세히 설명합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성

다음은 Azure Database for PostgreSQL 연결된 서비스에 대해 지원되는 속성입니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | type 속성은 **AzurePostgreSql**로 설정해야 합니다. | 적용 |
| connectionString | Azure Database for PostgreSQL에 연결하는 ODBC 연결 문자열입니다. 이 필드를 SecureString으로 표시하여 ADF에 안전하게 저장하도록 선택하거나, Azure Key Vault에 암호를 저장하고 복사 작업이 데이터 복사를 수행할 때 거기에서 끌어오도록 할 수 있습니다. [Key Vault에 자격 증명 저장](store-credentials-in-key-vault.md)에서 자세히 알아보세요. | 적용 |
| connectVia | 데이터 저장소에 연결하는 데 사용할 [Integration Runtime](concepts-integration-runtime.md)입니다. Azure Integration Runtime 또는 자체 호스팅 Integration Runtime을 사용할 수 있습니다(데이터 저장소가 개인 네트워크에 있는 경우). 지정하지 않으면 기본 Azure Integration Runtime을 사용합니다. |아니요 |

**예제:**

```json
{
    "name": "AzurePostgreSqlLinkedService",
    "properties": {
        "type": "AzurePostgreSql",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<server>.postgres.database.azure.com;Database=<database>;Port=<port>;UID=<username>@admstest;Password=<Password>"
            }
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성

데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합](concepts-datasets-linked-services.md) 문서를 참조하세요. 이 섹션에서는 Azure Database for PostgreSQL 데이터 집합에서 지원하는 속성의 목록을 제공합니다.

Azure Database for PostgreSQL에서 데이터를 복사하려면 데이터 집합의 type 속성을 **AzurePostgreSqlTable**로 설정합니다. 이 형식의 데이터 집합에는 추가적인 형식별 속성이 없습니다.

**예제**

```json
{
    "name": "AzurePostgreSqlDataset",
    "properties": {
        "type": "AzurePostgreSqlTable",
        "linkedServiceName": {
            "referenceName": "<AzurePostgreSql linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>복사 작업 속성

작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인](concepts-pipelines-activities.md) 문서를 참조하세요. 이 섹션에서는 Azure Database for PostgreSQL 원본에서 지원하는 속성의 목록을 제공합니다.

### <a name="azurepostgresqlsource-as-source"></a>AzurePostgreSqlSource를 원본으로 설정

Azure Database for PostgreSQL에서 데이터를 복사하려면 복사 작업의 원본 형식을 **AzurePostgreSqlSource**로 설정합니다. 복사 작업 **source** 섹션에서 다음 속성이 지원됩니다.

| 자산 | 설명 | 필수 |
|:--- |:--- |:--- |
| 형식 | 복사 작업 원본의 type 속성은 **AzurePostgreSqlSource**로 설정해야 합니다. | 적용 |
| 쿼리 | 사용자 지정 SQL 쿼리를 사용하여 데이터를 읽습니다. 예: `"SELECT * FROM MyTable"` | 적용 |

**예제:**

```json
"activities":[
    {
        "name": "CopyFromAzurePostgreSql",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<AzurePostgreSql input dataset name>",
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
                "type": "AzurePostgreSqlSource",
                "query": "<custom query e.g. SELECT * FROM MyTable>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>다음 단계
Azure Data Factory에서 복사 작업의 원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](copy-activity-overview.md#supported-data-stores-and-formats)를 참조하세요.
