---
title: "데이터 팩터리를 사용 하 여 Cassandra aaaMove 데이터로 | Microsoft Docs"
description: "온-프레미스 Cassandra toomove 데이터로 데이터베이스 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Azure Data Factory를 사용하여 온-프레미스 Cassandra 데이터베이스에서 데이터 이동
이 문서에서는 Azure Data Factory toomove 데이터베이스의에서 데이터를 온-프레미스 Cassandra에서 toouse 복사 작업 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

온-프레미스 Cassandra 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리는 현재 이동 Cassandra 데이터에서 데이터 저장 tooother 데이터 저장소 뿐만 아니라 다른 데이터 저장소 tooa Cassandra 데이터 저장소에서 데이터 이동에 대해 지원 합니다. 

## <a name="supported-versions"></a>지원되는 버전
hello Cassandra 커넥터 버전 Cassandra의 다음 hello는 지원: 2.X 합니다.

## <a name="prerequisites"></a>필수 조건
Hello Azure Data Factory 서비스 toobe 수 tooconnect tooyour 온-프레미스 Cassandra 데이터베이스에서 데이터 관리 게이트웨이 설치 해야 동일한 컴퓨터 hello 데이터베이스를 호스팅 함 hello에 컴퓨터나 경쟁 hello 사용 하 여 리소스에 대 한 별도 컴퓨터 tooavoid 데이터베이스입니다. 데이터 관리 게이트웨이 안전 하 고 관리 되는 방식으로 온-프레미스 데이터 원본 toocloud 서비스를 연결 하는 구성 요소입니다. 데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요. 참조 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 toomove 데이터를 설정 합니다.

Hello 데이터베이스가 호스팅되면 hello 클라우드의 예를 들어 Azure IaaS VM의 경우에 hello 게이트웨이 tooconnect tooa Cassandra 데이터베이스를 사용 해야 합니다. Y hello 게이트웨이에 있을 수 있습니다 동일한 VM hello 데이터베이스를 호스팅 함 hello 또는 hello 게이트웨이 별도 VM toohello 데이터베이스 연결 될 수 있습니다.  

Hello 게이트웨이 설치할 때 자동으로 Microsoft Cassandra ODBC 사용 되는 드라이버 tooconnect tooCassandra 데이터베이스를 설치 합니다. 따라서 필요 하지 않습니다 toomanually hello Cassandra 데이터베이스에서 데이터를 복사할 때 hello 게이트웨이 컴퓨터에 모든 드라이버를 설치 합니다. 

> [!NOTE]
> 연결/게이트웨이 관련 문제 해결에 대한 팁은 [게이트웨이 문제 해결](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) 을 참조하세요.

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다. 
- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 온-프레미스 Cassandra 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: Cassandra tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-cassandra-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooa Cassandra 데이터 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooCassandra 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesCassandra** |예 |
| host |Cassandra 서버에 대한 하나 이상의 IP 주소 또는 호스트 이름.<br/><br/>동시에 IP 주소 또는 호스트 이름 tooconnect tooall 서버의 쉼표로 구분 된 목록을 지정 합니다. |예 |
| 포트 |hello Cassandra 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다. |아니요. 기본값: 9042 |
| authenticationType |Basic 또는 Anonymous |예 |
| username |Hello 사용자 계정에 대 한 사용자 이름을 지정 합니다. |예, authenticationType tooBasic 설정 된 경우. |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예, authenticationType tooBasic 설정 된 경우. |
| gatewayName |데이터베이스가 사용 되는 tooconnect toohello 온-프레미스 Cassandra hello 게이트웨이의 hello 이름입니다. |예 |
| encryptedCredential |Hello 게이트웨이로 암호화 된 자격 증명입니다. |아니요 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **CassandraTable** hello 다음과 같은 속성에

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| keyspace |키 스페이스 hello 또는 Cassandra 데이터베이스에서 스키마의 이름입니다. |예(**CassandraSource**의 **query**가 정의되지 않은 경우) |
| tableName |Hello Cassandra 데이터베이스 테이블의 이름입니다. |예(**CassandraSource**의 **query**가 정의되지 않은 경우) |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

원본 유형의 경우 **CassandraSource**, 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 또는 CQL 쿼리입니다. [CQL 참조](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html)를 참조하세요. <br/><br/>SQL 쿼리를 사용할 때 지정 **키 스페이스 name.table 이름** tooquery 원하는 toorepresent hello 테이블입니다. |아니요(데이터 집합의 tableName 및 keyspace가 정의된 경우) |
| consistencyLevel |hello 일관성 수준이 지정 복제 개수 데이터 toohello 클라이언트 응용 프로그램을 반환 하기 전에 tooa 읽기 요청 응답 해야 합니다. Cassandra 검사 읽기 요청을 데이터 toosatisfy hello에 대 한 복제본의 지정 된 수를 hello 합니다. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. 자세한 내용은 [데이터 일관성 구성](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) 을 참조하세요. |아니요. 기본값은 ONE입니다. |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>JSON의 예: Cassandra tooAzure Blob에서에서 데이터 복사
이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 온-프레미스 Cassandra toocopy 데이터로 데이터베이스 tooan Azure Blob 저장소를 표시 합니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

> [!IMPORTANT]
> 이 샘플은 JSON 코드 조각을 제공합니다. Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다. 단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

* [OnPremisesCassandra](#linked-service-properties)형식의 연결된 서비스입니다.
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
* [CassandraTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [CassandraSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

**Cassandra 연결된 서비스:**

이 예에서는 hello **Cassandra** 연결 된 서비스입니다. 참조 [Cassandra 연결 된 서비스](#linked-service-properties) 이 연결 된 서비스에서 지 원하는 hello 속성에 대 한 섹션.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure 저장소 연결된 서비스:**

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

**Cassandra 입력 데이터 집합:**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Cassandra 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**CassandraSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

참조 [RelationalSource 형식 속성](#copy-activity-properties) hello 목록이 hello RelationalSource에서 지 원하는 속성에 대 한 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Cassandra에 대한 형식 매핑
| Cassandra 형식 | .NET 기반 형식 |
| --- | --- |
| ASCII |문자열 |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |단일 |
| INET |문자열 |
| INT |Int32 |
| TEXT |문자열 |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |문자열 |
| VARINT |10진수 |

> [!NOTE]
> 컬렉션에 대 한 형식은 (지도, 집합, 목록, 등)를 참조 너무[가상 테이블을 사용 하 여 Cassandra 컬렉션 형식을 사용할](#work-with-collections-using-virtual-table) 섹션.
>
> 사용자 정의 형식은 지원되지 않습니다.
>
> hello 길이의 이진 열과 문자열 열 길이가 4000 보다 클 수 없습니다.
>
>

## <a name="work-with-collections-using-virtual-table"></a>가상 테이블을 사용하여 컬렉션으로 작업
Azure 데이터 팩터리는 기본 제공 ODBC 드라이버 tooconnect tooand에서에서 데이터 복사 Cassandra 데이터베이스를 사용합니다. 목록, 집합 및 맵을 포함 하는 컬렉션 형식에 대해 hello 드라이버를 해당 가상 테이블로 구하고 hello 데이터 다시 정규화 합니다. 특히, 컬렉션 열이 포함 된 테이블, hello 드라이버 hello 다음 가상 표를 생성 합니다.

* A **기본 테이블**, 포함 된 hello hello 컬렉션 열 제외 하 고 실제 테이블 hello와 동일한 데이터입니다. hello 기본 테이블 표시 되는 hello 실제 테이블 hello 이름과 같은 이름을 사용 합니다.
* A **가상 테이블** hello 중첩 된 데이터 확장 되는 각 컬렉션 열에 대 한 합니다. 구분 기호, hello 실제 테이블의 hello 이름을 사용 하 여 컬렉션을 나타내는 hello 가상 테이블 이름의 "*vt*" 및 hello hello 열의 이름입니다.

가상 테이블 참조 toohello hello 실제 테이블에는 데이터, 사용할 수 있도록 hello 드라이버 tooaccess hello 비 정규화 된 데이터입니다. 자세한 내용은 예제 섹션을 참조하세요. Cassandra 컬렉션의 내용을 hello 쿼리 한 hello 가상 테이블을 조인 하 여 액세스할 수 있습니다.

Hello를 사용할 수 있습니다 [복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively hello 가상 테이블을 포함 한 Cassandra 데이터베이스에서 테이블 목록을 hello 뷰와 내부 hello 데이터를 미리 봅니다. Hello 복사 마법사에서에서 쿼리를 작성 하 고 toosee hello 결과 유효성을 검사 수도 있습니다.

### <a name="example"></a>예제
예를 들어 hello ExampleTable"다음"은 정수 기본 키 열 이름은 "pk_int", value 라는 텍스트 열, 목록의 열, 열 매핑 ("StringSet" 라고 함) 집합 열이 포함 된 Cassandra 데이터베이스 테이블입니다.

| pk_int | 값 | 나열 | Map | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"sample value 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"sample value 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

hello 드라이버는이 단일 표에 여러 가상 테이블 toorepresent 발생 합니다. hello hello 가상 테이블의 외래 키 열 hello hello real 테이블의 기본 키 열을 참조 하 고는 실시간 표시 테이블 행 hello 가상 테이블 행에 해당 합니다.

hello 첫 번째 가상 테이블은 hello 라는 "ExampleTable"는 기본 테이블은 다음 표에 hello에 표시 됩니다. hello hello 기본 테이블에 포함 되어이 테이블에서 생략 하 고 다른 가상 테이블에서 확장 되는 hello 컬렉션을 제외 하 고 원본 데이터베이스 테이블 hello와 동일한 데이터입니다.

| pk_int | 값 |
| --- | --- |
| 1 |"sample value 1" |
| 3 |"sample value 3" |

hello 다음 표에서 보여 hello 열의 데이터를 hello 목록, 지도 및 StringSet renormalize hello 가상 테이블입니다. "_index" 또는 "(_k)"로 끝나는 이름의 hello 열 hello 원래 목록 또는 맵 내 hello 데이터 hello 위치를 나타냅니다. "_value"로 끝나는 이름의 hello 열 hello 컬렉션에서 hello 확장 데이터를 포함 합니다.

#### <a name="table-exampletablevtlist"></a>테이블 "ExampleTable_vt_List":
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>테이블 “ExampleTable_vt_Map”:
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |A |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>테이블 “ExampleTable_vt_StringSet”:
| pk_int | StringSet_value |
| --- | --- |
| 1 |A |
| 1 |b |
| 1 |C |
| 3 |A |
| 3 |E |

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.
