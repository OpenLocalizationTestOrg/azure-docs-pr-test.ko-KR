---
title: "Azure 데이터 팩터리를 사용 하 여 FTP 서버에서 데이터 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 FTP 서버에서 toomove 데이터입니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a>Azure Data Factory를 사용하여 FTP 서버에서 데이터 이동
이 문서에서는 어떻게 toouse hello 복사 작업이 Azure Data Factory toomove 데이터에는 FTP 서버에서 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

FTP 서버 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. Data Factory에는 현재 FTP 서버 tooother 데이터에서 데이터 이동을 저장 하지만 tooan FTP 서버를 다른 데이터에서 데이터를 이동 하지 저장만 지원 됩니다. 온-프레미스 및 클라우드 FTP 서버를 지원합니다.

> [!NOTE]
> hello 복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다. 성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일을 만들고 hello 파이프라인에서 hello 활동을 사용 합니다. 

## <a name="enable-connectivity"></a>연결 설정
데이터를 이동 하는 경우는 **온-프레미스** FTP 서버 tooa 클라우드 데이터 저장소 (예를 들어 tooAzure Blob 저장소)를 설치 하 고 데이터 관리 게이트웨이 사용 합니다. hello 데이터 관리 게이트웨이 온-프레미스 컴퓨터에 설치 된 클라이언트 에이전트로, 및 클라우드 서비스 tooconnect tooan 온-프레미스 리소스를 허용 합니다. 자세한 내용은 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) 문서를 참조하세요. Hello 게이트웨이를 설정 하 고 사용에 대 한 단계별 지침에 대 한 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다. 경우에 hello 서버는 Azure 인프라 서비스 (IaaS) 가상 컴퓨터 (VM)으로 hello 게이트웨이 tooconnect tooan FTP 서버를 사용 합니다.

가능한 tooinstall hello 수단 hello에 동일한 온-프레미스 컴퓨터 또는 IaaS VM FTP 서버 hello 합니다. 그러나 별도 컴퓨터 또는 IaaS VM tooavoid 리소스 경합 및 성능 향상을 위해 hello 게이트웨이 설치 하는 것이 좋습니다. 별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 수 tooaccess hello FTP 서버가 있어야 합니다.

## <a name="get-started"></a>시작
다른 도구 또는 API를 사용하여 FTP 원본의 데이터를 이동하는 복사 작업이 포함된 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **데이터 팩터리 복사 마법사**합니다. 빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **PowerShell**, **Azure리소스관리자템플릿**, **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구 또는 Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다. Data Factory 된 엔터티를 FTP 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 hello [JSON의 예: FTP 서버 tooAzure blob에서 데이터를 복사](#json-example-copy-data-from-ftp-server-to-azure-blob) 이 문서의 섹션.

> [!NOTE]
> 지원 되는 파일 및 압축 형식 toouse에 대 한 세부 정보를 참조 하십시오. [Azure Data Factory에서 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)합니다.

다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooFTP는 JSON 속성에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooan 연결 하는 FTP 서비스를 설명 합니다.

| 속성 | 설명 | 필수 | 기본값 |
| --- | --- | --- | --- |
| type |이 tooFtpServer를 설정 합니다. |예 |&nbsp; |
| host |Hello 이름 또는 hello FTP 서버의 IP 주소를 지정 합니다. |예 |&nbsp; |
| authenticationType |Hello 인증 유형을 지정 합니다. |예 |기본, 익명 |
| username |Hello 있는 사용자에 게 액세스 toohello FTP 서버를 지정 합니다. |아니요 |&nbsp; |
| 암호 |Hello 사용자 (사용자 이름)에 대 한 hello 암호를 지정 합니다. |아니요 |&nbsp; |
| encryptedCredential |Hello 암호화 된 자격 증명 tooaccess hello FTP 서버를 지정 합니다. |아니요 |&nbsp; |
| gatewayName |데이터 관리 게이트웨이 tooconnect tooan 온-프레미스 FTP 서버에 hello 게이트웨이의 hello 이름을 지정 합니다. |아니요 |&nbsp; |
| 포트 |Hello 수신 포트를 어떤 hello FTP 서버를 지정 합니다. |아니요 |21 |
| enableSsl |Toouse SSL/TLS 채널을 통해 FTP 여부를 지정 합니다. |아니요 |true |
| enableServerCertificateValidation |SSL/TLS 채널을 통해 FTP를 사용 하는 경우 tooenable 서버 SSL 인증서 유효성 검사 여부를 지정 합니다. |아니요 |true |

### <a name="use-anonymous-authentication"></a>익명 인증 사용

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a>일반 텍스트에 사용자 이름 및 암호를 기본 인증에 사용

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a>포트, enableSsl, enableServerCertificateValidation 사용

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a>인증 및 게이트웨이에 encryptedCredential 사용

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.

hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다. 가 특정 toohello 데이터 집합 형식 정보를 제공 합니다. hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **FileShare** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |하위 경로 toohello 폴더입니다. 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작 및 종료 날짜 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>때 **fileName** hello hello 생성 된 파일의 이름이 형식에 따라 hello에 출력 데이터 집합의 경우 지정 하지 않으면: <br/><br/>Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |Hello에 필터 사용 toobe tooselect 파일의 하위 집합을 지정 **folderPath**, 모든 파일이 아닌 합니다.<br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: `"fileFilter": "*.log"`<br/>예 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> **fileFilter**는 FileShare 입력 데이터 집합에 적용할 수 있습니다. 이 속성은 HDFS(Hadoop Distributed File System)에서 지원되지 않습니다. |아니요 |
| partitionedBy |사용 하는 동적 toospecify **folderPath** 및 **fileName** 시계열 데이터에 대 한 합니다. 예를 들어 매 시간 데이터에 대해 매개 변수가 있는 **folderPath**를 지정할 수 있습니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션. <br><br> 파일 기반 저장소 (이진 복사) 사이 있는 대로 toocopy 파일을 만들려는 경우 두 입력 및 출력 데이터 집합 정의에 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2**, **ZipDeflate**이고 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |
| useBinaryTransfer |전송 모드를 toouse hello 이진 여부를 지정 합니다. hello 값은 이진 모드 (이것이 hello 기본값)에 대 한 true이 고 ASCII false입니다. 이 속성 hello 관련된 연결 된 서비스 유형의 유형인 경우에 사용할 수 있습니다: ftp 서버입니다. |아니요 |

> [!NOTE]
> **filename** 및 **fileFilter**는 동시에 사용할 수 없습니다.

### <a name="use-hello-partionedby-property"></a>Hello partionedBy 속성 사용
Hello 이전 섹션에서 설명 했 듯이 동적을 지정할 수 있습니다 **folderPath** 및 **fileName** hello로 시계열 데이터에 대 한 **partitionedBy** 속성입니다.

toolearn 시간 시계열 데이터 집합, 일정 및 분할 하는 방법에 대 한 참조 [데이터 집합을 만드는](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md)합니다.

#### <a name="sample-1"></a>샘플 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
이 예제에서 {Slice}는 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다, 그리고 hello에 지정 된 (yyyymmddhh). hello SliceStart hello 조각의 toostart 시간을 의미합니다. hello 폴더 경로 각 조각에 대 한 차이가 있습니다. (예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.)

#### <a name="sample-2"></a>샘플 2

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Hello에서 사용 되는 개별 변수로 hello 연도, 월, 일 및 시간 SliceStart의이 예제에서는 추출 **folderPath** 및 **fileName** 속성입니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

Hello에 사용할 수 있는 속성 **typeProperties** 섹션 hello hello에 활동 반면, 각 활동 유형에 따라 다릅니다. Hello 복사 작업에 대 한 hello 형식 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다.

Hello 원본 유형인 경우 복사 활동에서 **FileSystemSource**, hello 다음 속성은 영어로 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다. |True, False(기본값) |아니요 |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a>JSON의 예: FTP 서버 tooAzure Blob에서에서 데이터 복사
이 샘플은 어떻게 FTP 서버 tooAzure Blob 저장소에서에서 toocopy 데이터입니다. 하지만 hello tooany 싱크에 언급 된 hello 직접 데이터 복사할 수 있습니다 [지원 되는 데이터 저장소 및 형식](data-factory-data-movement-activities.md#supported-data-stores-and-formats), Data Factory에 hello 복사 작업을 사용 하 여 합니다.  

hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):

* [FtpServer](#linked-service-properties) 형식의 연결된 서비스
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
* [FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)

hello 샘플 데이터 복사 FTP 서버 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

### <a name="ftp-linked-service"></a>FTP 연결 서비스

이 예제에서는 hello 사용자 이름과 암호가 일반 텍스트로 기본 인증을 사용 합니다. 또한 hello 같은 방법으로 다음 중 하나를 사용할 수 있습니다.

* 익명 인증 
* 암호화된 자격 증명으로 기본 인증 
* SSL/TLS 경우 FTP(FTPS)

Hello 참조 [FTP 연결 된 서비스](#linked-service-properties) 섹션에 대 한 다양 한 유형의 인증을 사용할 수 있습니다.

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
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
### <a name="ftp-input-dataset"></a>FTP 입력 데이터 집합

이 데이터 집합 참조 toohello FTP 폴더 `mysharedfolder` 파일과 `test.csv`합니다. hello 파이프라인 hello 파일 toohello 대상에 복사합니다.

설정 **외부** 너무**true** 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello 폴더 경로 hello blob에 대 한 동적으로 평가 처리 중인 hello 조각의 hello 시작 시간에 기반 합니다. hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a>파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 hello **싱크** 형식이 너무 설정**BlobSink**합니다.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 참조 하십시오.

* 키에 대 한 toolearn Data Factory에서 데이터 이동을 (복사 작업) 및 다양 한 방법으로 toooptimize의 성능에 영향을 해당 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.

* 복사 작업을 사용 하 여 파이프라인 만들기에 대 한 단계별 지침은 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
