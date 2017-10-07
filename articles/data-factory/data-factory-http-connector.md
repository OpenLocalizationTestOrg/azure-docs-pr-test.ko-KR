---
title: "HTTP 소스-Azure에서에서 aaaMove 데이터 | Microsoft Docs"
description: "온-프레미스 또는 클라우드에서 HTTP toomove 데이터 원본 Azure 데이터 팩터리를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a>Azure Data Factory를 사용하여 HTTP 소스에서 데이터 이동
이 문서에서는 toouse hello 복사 작업에서-프레미스/클라우드 HTTP 끝점 tooa에서 Azure Data Factory toomove 데이터에서 싱크 데이터 저장소를 지원 되는 방식에 대해 설명 합니다. Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 원본/싱크의로 지원 되는 데이터 저장소의 복사 작업 및 hello 목록 사용 하 여 데이터 이동의 일반적인 개요를 제공 하는 문서입니다.

데이터 팩터리의 현재만 HTTP에서 데이터를 이동할 원본 tooother 데이터 저장소, 하지만 HTTP tooan 대상 저장 다른 데이터에서 데이터를 이동 하지 않습니다.

## <a name="supported-scenarios-and-authentication-types"></a>지원되는 시나리오 및 인증 형식
이 HTTP 커넥터 tooretrieve 데이터를 사용할 수 **클라우드와 온-프레미스 둘 다 HTTP/s 끝점** HTTP를 사용 하 여 **가져오기** 또는 **POST** 메서드. hello 인증 유형만 지원 됩니다: **익명**, **기본**, **다이제스트**, **Windows**, 및  **ClientCertificate**합니다. 이 커넥터 및 hello hello 차이점에 주의 해야 [웹 테이블 커넥터](data-factory-web-table-connector.md) 은: hello 후자는 HTML 웹 페이지에서 콘텐츠 tooextract 사용 되는 테이블입니다.

온-프레미스 HTTP 끝점에서 데이터를 복사할 때 hello 온-프레미스 환경/Azure VM에서에서 데이터 관리 게이트웨이 설치 해야 합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 HTTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. HTTP 소스 tooAzure Blob 저장소에서에서 toocopy 데이터를 샘플링 하는 JSON, 참조 [JSON 예제](#json-examples) 이 문서의 섹션.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooHTTP 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type | hello type 속성 설정 해야 합니다: `Http`합니다. | 예 |
| url | 기본 URL toohello 웹 서버 | 예 |
| authenticationType | Hello 인증 유형을 지정합니다. 허용되는 값: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**. <br><br> 이 표 아래에 더 많은 속성 및 JSON 샘플 toosections 해당 인증 형식에 각각 참조 합니다. | 예 |
| enableServerCertificateValidation | 소스 HTTPS 웹 서버인 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다. | 아니요. 기본값은 True입니다. |
| gatewayName | 데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 HTTP 소스입니다. | 온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에는 필수입니다. |
| encryptedCredential | 암호화 된 자격 증명 tooaccess hello HTTP 끝점입니다. 자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에 hello 인증 정보를 구성 합니다. | 아니요. 온-프레미스 HTTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |

참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 온-프레미스 HTTP 커넥터 데이터 원본에 대 한 자격 증명을 설정 하는 방법에 대 한 세부 정보에 대 한 합니다.

### <a name="using-basic-digest-or-windows-authentication"></a>Basic, Digest 또는 Windows 인증 사용

설정 `authenticationType` 으로 `Basic`, `Digest`, 또는 `Windows`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| username | 사용자 이름 tooaccess hello HTTP 끝점입니다. | 예 |
| 암호 | Hello 사용자 (사용자 이름)에 대 한 암호입니다. | 예 |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>예: Basic, Digest 또는 Windows 인증

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a>ClientCertificate 인증 사용

toouse 기본 인증 설정 `authenticationType` 으로 `ClientCertificate`, hello hello HTTP 커넥터 제네릭 위에서 소개 하는 것 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| embeddedCertData | hello 개인 정보 교환 (PFX) 파일의 이진 데이터의 Base64 인코딩 내용 hello입니다. | 어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다. |
| certThumbprint | 게이트웨이 컴퓨터의 인증서 저장소에 설치 된 hello 인증서의 지문을 hello 합니다. 온-프레미스 HTTP 소스에서 데이터를 복사하는 경우에만 적용됩니다. | 어느 hello 지정 `embeddedCertData` 또는 `certThumbprint`합니다. |
| 암호 | Hello 인증서와 연결 된 암호입니다. | 아니요 |

사용 하는 경우 `certThumbprint` toogrant hello 읽기 권한은 toohello 게이트웨이 서비스가 필요한 경우 인증 및 hello 인증서 hello hello 로컬 컴퓨터의 개인 저장소에 설치 하면:

1. MMC(Microsoft Management Console)를 시작합니다. Hello 추가 **인증서** 스냅인 해당 대상 hello **로컬 컴퓨터**합니다.
2. **인증서**, **개인**을 확장하고 **인증서**를 클릭합니다.
3. Hello 개인 저장소에서 hello 인증서를 마우스 오른쪽 단추로 클릭 하 고 선택 **모든 작업**->**개인 키 관리...**
3. Hello에 **보안** 탭에서 데이터 관리 게이트웨이 호스트 서비스가 실행 되 고 있는 hello 읽기 액세스 toohello 인증서로 hello 사용자 계정을 추가 합니다.  

#### <a name="example-using-client-certificate"></a>예제: 클라이언트 인증서 사용
서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다. 데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 설치 된 클라이언트 인증서를 사용 합니다.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>예제: 파일로 클라이언트 인증서 사용
서비스 링크 데이터 팩터리 tooan 온-프레미스 HTTP 웹 서버를 연결 설정 합니다. 데이터 관리 게이트웨이가 설치 된 hello 컴퓨터에 클라이언트 인증서 파일을 사용 합니다.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **Http** hello 다음과 같은 속성에

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| type | Hello 유형의 hello 데이터 집합을 지정 합니다. 너무 설정 되어 있어야`Http`합니다. | 예 |
| relativeUrl | 상대 URL toohello 리소스 hello 데이터가 들어 있는입니다. 경로 지정 하지 않으면 hello 연결 된 서비스 정의에 지정 된 유일한 hello URL 사용 됩니다. <br><br> 사용할 수 있습니다 tooconstruct 동적 URL [데이터 팩터리 함수 및 시스템 변수](data-factory-functions-variables.md), 예: "relativeUrl": "$$Text.Format ('/ my/보고서? 월 = {0:yyyy}-{0:MM} & fmt csv =', SliceStart)"입니다. | 아니요 |
| requestMethod | HTTP 메서드입니다. 허용되는 값은 **GET** 또는 **POST**입니다. | 아니요. 기본값은 `GET`입니다. |
| additionalHeaders | 추가 HTTP 요청 헤더입니다. | 아니요 |
| requestBody | HTTP 요청의 본문입니다. | 아니요 |
| format | Toosimply 하려는 경우 **으로 HTTP 끝점에서 hello 데이터를 검색-은** 것, 구문 분석 하지 않고 형식 설정에이 건너뜁니다. <br><br> 복사 중 tooparse hello HTTP 응답을 콘텐츠에 삭제 하는 경우에 hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**합니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

### <a name="example-using-hello-get-default-method"></a>예: hello GET (기본값) 메서드 사용

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a>예: hello POST 메서드를 사용 하 여

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
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

Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello에 hello 활동의 다른 손 활동 형식에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

현재 복사 작업에서 hello 소스 경우 형식의 **HttpSource**, 다음과 같은 속성 hello 지원 됩니다.

| 속성 | 설명 | 필수 |
| -------- | ----------- | -------- |
| httpRequestTimeout | 안녕 hello HTTP 요청 tooget 응답 하기 위한 시간 제한 (TimeSpan). Hello timeout tooget 응답으로 hello timeout tooread 응답 데이터가 아닌 경우 | 아니요. 기본값: 00:01:40 |

## <a name="supported-file-and-compression-formats"></a>지원되는 파일 및 압축 형식
자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.

## <a name="json-examples"></a>JSON 예
샘플 JSON 정의 제공 하는 다음 예제는 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. HTTP에서 toocopy 데이터 tooAzure Blob 저장소를 원본 하는 방법을 보여 줍니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a>예: HTTP 소스 tooAzure Blob 저장소에서에서 데이터를 복사 합니다.
이 샘플에 대 한 데이터 팩터리의 솔루션 hello를 Data Factory 엔터티에 따라 hello를 포함 되어 있습니다.

1. [HTTP](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [Http](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [HttpSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 HTTP 소스 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

### <a name="http-linked-service"></a>HTTP 연결된 서비스
이 예제를 사용 하 여 hello HTTP 익명 인증을 사용 하는 서비스를 연결 합니다. 사용할 수 있는 다른 유형의 인증은 [HTTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스

```JSON
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

### <a name="http-input-dataset"></a>HTTP 데이터 집합
설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1).

```JSON
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

### <a name="pipeline-with-copy-activity"></a>복사 작업을 포함하는 파이프라인

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**HttpSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

참조 [HttpSource](#copy-activity-properties) hello 목록이 hello HttpSource에서 지 원하는 속성에 대 한 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.
