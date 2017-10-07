---
title: "Azure 데이터 팩터리를 사용 하 여 Teradata의 데이터 aaaMove | Microsoft Docs"
description: "Hello Teradata 데이터베이스에서 데이터를 이동할 수 있는 데이터 팩터리 서비스에 대 한 Teradata 커넥터에 대 한 자세한 내용은"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용하여 Teradata에서 데이터 이동
이 문서에서는 toouse 온-프레미스 Teradata 데이터베이스에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

온-프레미스 Teradata 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리는 현재 tooother 데이터 저장소를 저장 하는 Teradata 데이터에서 데이터 이동 뿐만 아니라 다른 데이터 저장소 tooa Teradata 데이터 저장소에서 데이터 이동에 대해 지원 합니다. 

## <a name="prerequisites"></a>필수 조건
데이터 팩터리 hello 데이터 관리 게이트웨이 통해 연결 tooon 온-프레미스 Teradata 원본을 지원합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.

게이트웨이 hello Teradata에서에서 호스팅되는 Azure IaaS VM 하는 경우에 필요 합니다. Hello IaaS VM hello 데이터로 저장 같거나 hello 게이트웨이 다른 VM toohello 데이터베이스 연결 될 수 있습니다에 hello 게이트웨이 설치할 수 있습니다.

> [!NOTE]
> 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.

## <a name="supported-versions-and-installation"></a>지원되는 버전 및 설치
Tooinstall hello 해야 데이터 관리 게이트웨이 tooconnect toohello Teradata 데이터베이스를 [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) 버전 14 또는 위에 환영 동일 데이터 관리 게이트웨이 hello 시스템입니다. Teradata 버전 12 이상이 지원됩니다.

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다. 
- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 온-프레미스 Teradata 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: Teradata tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-teradata-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa Teradata 데이터 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooTeradata 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesTeradata** |예 |
| server |Hello Teradata 서버의 이름입니다. |예 |
| authenticationType |Tooconnect toohello Teradata 데이터베이스를 사용 하는 인증 유형입니다. 가능한 값은 익명, 기본 및 Windows입니다. |예 |
| username |기본 또는 Windows 인증을 사용하는 경우 사용자 이름을 지정합니다. |아니요 |
| 암호 |Hello 사용자 이름에 대해 지정한 사용자 계정에 hello에 대 한 암호를 지정 합니다. |아니요 |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello 온-프레미스 Teradata 데이터베이스를 사용 해야 합니다. |예 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 현재,는 hello Teradata 데이터 집합에 대 한 지원 형식 속성이 없습니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

Hello 원본 유형의 경우 **RelationalSource** (Teradata 포함), hello 다음과 같은 속성에서 사용할 수 있는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL 쿼리 문자열. 예: select * from MyTable. |예 |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a>JSON의 예: Teradata tooAzure Blob에서에서 데이터 복사
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 Teradata tooAzure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.   

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesTeradata](#linked-service-properties)형식의 연결된 서비스
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
3. [RelationalTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. hello [파이프라인](data-factory-create-pipelines.md) 사용 하 여 복사 작업으로 [RelationalSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)합니다.

hello 샘플 데이터 복사 Teradata 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, hello 데이터 관리 게이트웨이 설치 합니다. hello 지침은 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**Teradata 연결된 서비스:**

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Azure Blob 저장소 연결된 서비스:**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Teradata 입력 데이터 집합:**

hello 샘플 테이블 "MyTable" Teradata에서 만들고 시계열 데이터에 대 한 "timestamp" 라는 열이 포함 된 가정 합니다.

"External" 설정: true 알립니다 hello 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
**복사 작업을 포함하는 파이프라인:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업은 예약 된 toorun 매 및 hello 입력 및 출력 데이터 집합. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**RelationalSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
                    }
                ],                    
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a>Teradata에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서 hello 복사 활동 소스 형식 toosink 형식에서 자동 형식 변환 2 단계 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

데이터 tooTeradata를 이동할 때는 hello 다음 매핑은 사용 하는 Teradata 형식 too.NET 형식에서 합니다.

| Teradata 데이터베이스 형식 | .NET Framework 형식 |
| --- | --- |
| Char |문자열 |
| Clob |문자열 |
| Graphic |문자열 |
| VarChar |문자열 |
| VarGraphic |문자열 |
| Blob |Byte[] |
| Byte |Byte[] |
| VarByte |Byte[] |
| BigInt |Int64 |
| ByteInt |Int16 |
| 10진수 |10진수 |
| Double |Double |
| Integer |Int32 |
| Number |Double |
| SmallInt |Int16 |
| Date |DateTime |
| Time |TimeSpan |
| Time With Time Zone |문자열 |
| Timestamp |DateTime |
| Timestamp With Time Zone |DateTimeOffset |
| Interval Day |TimeSpan |
| 간격 날짜 tooHour |TimeSpan |
| 간격 날짜 tooMinute |TimeSpan |
| 간격 날짜 tooSecond |TimeSpan |
| Interval Hour |TimeSpan |
| 간격 시간 tooMinute |TimeSpan |
| 간격 시간 tooSecond |TimeSpan |
| Interval Minute |TimeSpan |
| 간격은 분 tooSecond |TimeSpan |
| Interval Second |TimeSpan |
| Interval Year |문자열 |
| 간격 연도 tooMonth |문자열 |
| Interval Month |문자열 |
| Period(Date) |문자열 |
| Period(Time) |문자열 |
| Period(Time With Time Zone) |문자열 |
| Period(Timestamp) |문자열 |
| Period(Timestamp With Time Zone) |문자열 |
| Xml |문자열 |

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.
