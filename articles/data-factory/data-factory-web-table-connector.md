---
title: "Azure 데이터 팩터리를 사용 하 여 웹 테이블에서 데이터 aaaMove | Microsoft Docs"
description: "Toomove 테이블의에서 데이터를 웹에서 페이지 Azure 데이터 팩터리를 사용 하 여 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a>Azure Data Factory를 사용하여 웹 테이블 원본에서 데이터 이동
이 문서에서는 웹 페이지 tooa의 테이블에서 Azure Data Factory toomove 데이터에 대 한 복사 작업 toouse hello 싱크 데이터 저장소를 지원 되는 방식에 대해 설명 합니다. Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 원본/싱크의로 지원 되는 데이터 저장소의 복사 작업 및 hello 목록 사용 하 여 데이터 이동의 일반적인 개요를 제공 하는 문서입니다.

데이터 팩터리는 현재 웹 테이블 tooother 데이터의 이동 데이터를 저장 하지만 tooa 웹 테이블 대상 저장 다른 데이터에서 데이터를 이동 하지만 지원 합니다.

> [!IMPORTANT]
> 이 웹 커넥터는 현재 HTML 페이지에서 테이블 콘텐츠를 추출하도록 지원합니다. tooretrieve 데이터 HTTP/s 끝점에서 사용 하 여 [HTTP 커넥터](data-factory-http-connector.md) 대신 합니다.

## <a name="getting-started"></a>시작
여러 도구/API를 사용하여 온-프레미스 Cassandra 데이터 저장소의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다. 

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다. 
- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. 

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. 
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 사용 하는 toocopy 테이블의에서 데이터를 웹에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: 웹 테이블 tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-web-table-to-azure-blob) 이 문서의 섹션. 

다음 섹션 hello JSON 속성을 사용 하는 toodefine 데이터 팩터리 엔터티 특정 tooa 웹 테이블에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooWeb 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **웹** |예 |
| Url |URL toohello 웹 소스 |예 |
| authenticationType |익명 |예 |

### <a name="using-anonymous-authentication"></a>익명 인증 사용

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **WebTable** hello 다음과 같은 속성에

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type |hello 데이터 집합의 형식입니다. 너무 설정 되어 있어야**WebTable** |예 |
| path |상대 URL toohello 리소스 hello 테이블을 포함 합니다. |아니요. 경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다. |
| index |hello 리소스에 대 한 hello 테이블의 hello 인덱스입니다. 참조 [HTML 페이지에 테이블의 Get 인덱스](#get-index-of-a-table-in-an-html-page) 단계 toogetting 인덱스에 대 한 HTML 페이지에 테이블의 섹션입니다. |예 |

**예제:**

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

현재 복사 작업에서 hello 소스 경우 형식의 **WebSource**, 추가 속성이 지원 됩니다.


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a>JSON의 예: 웹 테이블 tooAzure Blob에서에서 데이터 복사
다음 샘플에서는 hello:

1. [웹](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [WebTable](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [WebSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 웹 테이블 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

다음 예제는 hello toocopy 데이터 웹 테이블 tooan Azure에서에서 blob 하는 방법을 보여 줍니다. 하지만 hello tooany 싱크에 언급 된 hello 직접 데이터 복사할 수 있습니다 [데이터 이동 작업](data-factory-data-movement-activities.md) Azure Data Factory에서 hello 복사 작업을 사용 하 여 문서.

**연결 된 서비스 웹** 사용 하 여 hello 웹이이 예제는 연결 된 서비스 익명 인증을 사용 합니다. 사용할 수 있는 다른 유형의 인증은 [웹 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
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

**WebTable 입력된 데이터 집합** 설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello에 활동에 의해 생성 되지 않습니다 데이터 팩터리입니다.

> [!NOTE]
> 참조 [HTML 페이지에 테이블의 Get 인덱스](#get-index-of-a-table-in-an-html-page) 단계 toogetting 인덱스에 대 한 HTML 페이지에 테이블의 섹션입니다.  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


**Azure Blob 출력 데이터 집합**

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
            "folderPath": "adfgetstarted/Movies"
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

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**WebSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

참조 [WebSource 형식 속성](#copy-activity-type-properties) hello 목록이 hello WebSource에서 지 원하는 속성에 대 한 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a>HTML 페이지에서 테이블의 인덱스 가져오기
1. 시작 **Excel 2016** toohello 전환 **데이터** 탭 합니다.  
2. 클릭 **새 쿼리** hello 도구 모음의 가리킨 너무**기타 원본** 클릭 **웹**합니다.

    ![파워 쿼리 메뉴](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. Hello에 **웹에서** 대화 상자에 입력 **URL** 연결 된 서비스 JSON에 사용할 때 (예: https://en.wikipedia.org/wiki/) hello 데이터 집합에 대해 지정 된 경로 함께 (예: AFI % 27s_100_Years 중... 100_Movies)를 클릭 하 고 **확인**합니다.

    ![웹 대화 상자](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    이 예제에 사용된 URL: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies
4. 표시 되 면 **액세스 웹 콘텐츠** 대화 상자, 선택 hello right **URL**, **인증**를 클릭 하 고 **연결**합니다.

   ![웹 콘텐츠 액세스 대화 상자](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. 클릭는 **테이블** hello 트리 toosee 콘텐츠 보기 hello 테이블에서 항목을 클릭 한 다음 **편집** hello 아래쪽 단추입니다.  

   ![탐색기 대화 상자](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. Hello에 **쿼리 편집기** 창 클릭 **고급 편집기** hello 도구 모음에서 단추입니다.

    ![고급 편집기 단추](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. Hello 번호 hello 고급 편집기 대화 상자에서 다음 너무 "Source"에 hello 인덱스입니다.

    ![고급 편집기 - 인덱스](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

Excel 2013을 사용 하는 경우 사용 하 여 [Microsoft Excel 용 파워 쿼리](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello 인덱스입니다. 참조 [연결 tooa 웹 페이지](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) 을 참조 합니다. hello 단계는 사용 중인 경우 유사 [Microsoft Power BI Desktop에 대 한](https://powerbi.microsoft.com/desktop/)합니다.

> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.
