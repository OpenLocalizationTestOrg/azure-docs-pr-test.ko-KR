---
title: "데이터 팩터리를 사용 하 여 MongoDB aaaMove 데이터로 | Microsoft Docs"
description: "Toomove 데이터로 MongoDB 데이터베이스 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Azure Data Factory를 사용하여 MongoDB에서 데이터 이동
이 문서에서는 Azure Data Factory toomove 데이터베이스의에서 데이터를 온-프레미스 MongoDB에 toouse 복사 작업 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

온-프레미스 MongoDB 데이터 저장소 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리는 현재 이동 MongoDB 데이터에서 데이터 저장 tooother 데이터 저장소 뿐만 아니라 다른 데이터 저장소 tooan MongoDB 데이터 저장소에서 데이터 이동에 대해 지원 합니다. 

## <a name="prerequisites"></a>필수 조건
Hello Azure Data Factory 서비스 toobe 수 tooconnect tooyour 온-프레미스 MongoDB 데이터베이스에 대 한 다음과 같은 구성 요소가 hello를 설치 해야 합니다.

- 지원되는 MongoDB 버전:  2.4, 2.6, 3.0 및 3.2.
- 데이터 관리 게이트웨이를 동일한 컴퓨터를 hello 데이터베이스를 호스팅 함 hello 또는 경쟁 hello 데이터베이스와 리소스에 대 한 별도 컴퓨터 tooavoid 합니다. 데이터 관리 게이트웨이 온-프레미스 데이터 원본 toocloud 서비스를 안전 하 고 관리 되는 방식으로 연결 하는 소프트웨어입니다. 데이터 관리 게이트웨이에 대한 세부 정보는 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요. 참조 [toocloud 온-프레미스에서에서 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이 데이터 파이프라인 toomove 데이터를 설정 합니다.

    Hello 게이트웨이 설치할 때 자동으로 Microsoft MongoDB ODBC 사용 되는 드라이버 tooconnect tooMongoDB를 설치 합니다.

    > [!NOTE]
    > Azure IaaS Vm에서 호스팅되는 경우에 toouse hello 게이트웨이 tooconnect tooMongoDB 해야 합니다. Tooconnect tooan 인스턴스의 클라우드에서 호스트 되는 MongoDB 시도 하는 경우에 hello IaaS VM에에서 hello 게이트웨이 인스턴스를 설치할 수 있습니다.

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 MongoDB 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다. 

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 온-프레미스 MongoDB 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: MongoDB tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-mongodb-to-azure-blob) 이 문서의 섹션. 

사용 되는 toodefine Data Factory 엔터티에 특정 tooMongoDB 소스는 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:

## <a name="linked-service-properties"></a>연결된 서비스 속성
hello 다음 표에서 설명 특정 JSON 요소에 대 한 너무**OnPremisesMongoDB** 연결 된 서비스입니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **OnPremisesMongoDb** |예 |
| server |Hello MongoDB 서버의 IP 주소 또는 호스트 이름입니다. |예 |
| 포트 |MongoDB 서버 hello TCP 포트는 클라이언트 연결에 대 한 toolisten를 사용 합니다. |선택 사항, 기본값: 27017 |
| authenticationType |Basic 또는 Anonymous입니다. |예 |
| username |사용자 계정 tooaccess MongoDB 합니다. |예(기본 인증을 사용하는 경우) |
| 암호 |Hello 사용자 암호입니다. |예(기본 인증을 사용하는 경우) |
| authSource |원하는 toouse toocheck 자격 증명 인증에 대 한 hello MongoDB 데이터베이스의 이름입니다. |선택 사항(기본 인증을 사용하는 경우). 기본값: hello 관리자 계정 및 databaseName 속성을 사용 하 여 지정 하는 hello 데이터베이스를 사용 합니다. |
| databaseName |원하는 tooaccess hello MongoDB 데이터베이스 이름입니다. |예 |
| gatewayName |Hello 데이터 저장소에 액세스 하는 hello 게이트웨이의 이름입니다. |예 |
| encryptedCredential |게이트웨이에 의해 암호화된 자격 증명입니다. |옵션 |

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **MongoDbCollection** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| collectionName |MongoDB 데이터베이스의 hello 컬렉션의 이름입니다. |예 |

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

Hello 원본 유형의 경우 **MongoDbSource** 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| 쿼리 |사용자 지정 쿼리 tooread 데이터 hello를 사용 합니다. |SQL-92 쿼리 문자열입니다. 예: select * from MyTable. |아니요(**데이터 집합**의 **collectionName**이 지정된 경우) |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>JSON의 예: MongoDB tooAzure Blob에서에서 데이터 복사
이 예제에서는 샘플 JSON 정의 제공 합니다. 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 온-프레미스 MongoDB tooan Azure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터는 복사 tooany 명시 된 hello 싱크 가능 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

1. [OnPremisesMongoDb](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [MongoDbCollection](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [MongoDbSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 MongoDB 데이터베이스 tooa blob에 쿼리 결과에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로, hello의 hello 지침에 따라 hello 데이터 관리 게이트웨이 설치 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서.

**MongoDB 연결된 서비스**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**MongoDB 입력된 데이터 집합:** 설정 "외부": "true" 알립니다 hello 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**MongoDB 소스 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인 입력 및 출력 데이터 집합 위에 구성 된 toouse hello 고 1 시간 마다 예정 된 toorun 길이가 복사 작업을 포함 합니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**MongoDbSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Data Factory에서의 스키마
Azure 데이터 팩터리 서비스는 hello 컬렉션에 있는 최신 100 hello 문서를 사용 하 여 MongoDB 컬렉션에서 스키마를 유추 합니다. 100 이러한 문서를 전체 스키마 포함 되어 있지 않으면 hello 복사 작업 중 일부 열을 무시할 수 있습니다.

## <a name="type-mapping-for-mongodb"></a>MongoDB에 대한 형식 매핑
Hello에 설명 된 대로 [데이터 이동 작업](data-factory-data-movement-activities.md) 문서, 복사 작업 소스 형식 toosink 형식에서 자동 형식 변환 단계 2 방식을 따릅니다 hello로 수행:

1. 네이티브 소스 형식 too.NET 형식에서 변환
2. .NET 형식 toonative 싱크 형식에서 변환

다음 데이터 tooMongoDB hello를 이동할 때 매핑이 MongoDB 형식 too.NET 형식에서 사용 됩니다.

| MongoDB 형식 | .NET Framework 형식 |
| --- | --- |
| 이진 |Byte[] |
| Boolean |Boolean |
| Date |DateTime |
| NumberDouble |Double |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |문자열 |
| 문자열 |문자열 |
| UUID |Guid |
| Object |중첩 구분 기호로 “_”를 사용한 평면화된 열에 다시 정규화 |

> [!NOTE]
> 가상 테이블을 사용 하 여 배열에 대 한 지원에 대 한 toolearn 너무 참조[가상 테이블을 사용 하는 복합 형식에 대 한 지원](#support-for-complex-types-using-virtual-tables) 아래 섹션.

현재 hello MongoDB 데이터 유형만 지원 되지 않습니다: DBPointer, JavaScript, 최대/최소 키, 정규식, 기호, 타임 스탬프, 정의 되지 않음

## <a name="support-for-complex-types-using-virtual-tables"></a>가상 테이블을 사용하는 복합 형식에 대한 지원
Azure 데이터 팩터리는 기본 제공 ODBC 드라이버 tooconnect tooand에서에서 데이터 복사 MongoDB 데이터베이스를 사용합니다. Hello 문서에서 여러 형식으로 배열 또는 개체와 같은 복합 형식에 대 한 hello 드라이버를 다시 데이터를 해당 가상 테이블로 정규화합니다. 특히, 이러한 열을 포함 하는 테이블, hello 드라이버 hello 다음 가상 표를 생성 합니다.

* A **기본 테이블**, 포함 된 hello hello 복합 유형 열을 제외한 실제 테이블 hello와 동일한 데이터입니다. hello 기본 테이블 표시 되는 hello 실제 테이블 hello 이름과 같은 이름을 사용 합니다.
* A **가상 테이블** 각 복합 형식 열에 대 한 hello 중첩 된 데이터 확장입니다. hello hello 실제 테이블 이름, 구분 기호 "_" 및 hello 배열 또는 개체의 hello 이름을 사용 하 여 가상 테이블 hello 라고 합니다.

가상 테이블 참조 toohello hello 실제 테이블에는 데이터, 사용할 수 있도록 hello 드라이버 tooaccess hello 비 정규화 된 데이터입니다. 자세한 내용은 아래의 예제 섹션을 참조하세요. 쿼리 한 hello 가상 테이블을 조인 하 여 MongoDB 배열의 hello 콘텐츠를 액세스할 수 있습니다.

Hello를 사용할 수 있습니다 [복사 마법사](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively hello 가상 테이블을 포함 한 MongoDB 데이터베이스에서 테이블 목록을 hello 뷰와 내부 hello 데이터를 미리 봅니다. Hello 복사 마법사에서에서 쿼리를 작성 하 고 toosee hello 결과 유효성을 검사 수도 있습니다.

### <a name="example"></a>예제
예를 들어, 아래 "ExampleTable"은 MongoDB 테이블로, 각 셀의 개체 배열이 있는 하나의 열(송장)과 스칼라 형식의 배열이 있는 하나의 열(등급)이 있습니다.

| _id | 고객 이름 | 송장 | 서비스 수준 | 등급 |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{송장_id:”123”, 항목:”토스터”, 가격:”456”, 할인:”0.2”}, {송장_id:”124”, 항목:”오븐”, 가격: ”1235”, 할인: ”0.2”}] |Silver |[5,6] |
| 2222 |XYZ |[{송장_id:”135”, 항목:”냉장고”, 가격: ”12543”, 할인: ”0.0”}] |Gold |[1,2] |

hello 드라이버는이 단일 표에 여러 가상 테이블 toorepresent 발생 합니다. hello 첫 번째 가상 테이블은 아래에 표시 된 "ExampleTable" 라는 hello 기본 테이블입니다. hello 원래 테이블의 모든 hello 데이터를 포함 하는 기본 테이블 hello 되지만 hello 데이터 hello 배열에서 누락 되었습니다. hello 가상 테이블에 확장 됩니다.

| _id | 고객 이름 | 서비스 수준 |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

hello 다음 표에서 보여 hello hello 예제에서 hello 원래 배열을 나타내는 가상 테이블입니다. 이러한 테이블 hello 다음을 포함합니다.

* 에 대 한 역참조 (hello _id 열)를 통해 toohello 원래 기본 키 열 toohello의 해당 행 hello 원본 배열
* hello 데이터 hello 원래 배열 내에서 hello 위치 표시
* hello는 hello 배열 내의 각 요소에 대 한 데이터 확장

테이블 "ExampleTable_Invoices":

| _id | ExampleTable_Invoices_dim1_idx | 송장_id | 항목 | 가격 | 할인 |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |토스터 |456 |0.2 |
| 1111 |1 |124 |오븐 |1235 |0.2 |
| 2222 |0 |135 |냉장고 |12543 |0.0 |

테이블 "ExampleTable_Ratings":

| _id | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>원본 toosink 열 매핑
원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 매핑하는 방법에 대 한 toolearn 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="repeatable-read-from-relational-sources"></a>관계형 원본에서 반복 가능한 읽기
관계형 데이터 저장소에서 데이터를 복사할 때 유의 tooavoid에서 반복성을 유지 의도 하지 않은 결과입니다. Azure Data Factory에서는 조각을 수동으로 다시 실행할 수 있습니다. 또한 오류가 발생하면 조각을 다시 실행하도록 데이터 집합에 대한 재시도 정책을 구성할 수 있습니다. Toomake 동일한 데이터를 hello 있는지 어떻게에 관계 없이 읽기 필요한 어느 쪽에 분할 영역을 다시 실행 하는 경우 조각에 여러 번 실행 됩니다. [관계형 원본에서 반복 가능한 읽기](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)를 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

## <a name="next-steps"></a>다음 단계
참조 [온-프레미스와 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) tooan Azure 데이터 저장소를 저장 하는 데이터는 온-프레미스 데이터를 이동 하는 데이터 파이프라인 만들기에 대 한 단계별 지침에 대 한 문서입니다.
