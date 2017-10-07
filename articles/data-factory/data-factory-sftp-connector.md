---
title: "Azure 데이터 팩터리를 사용 하 여 SFTP 서버에서 데이터 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 온-프레미스 또는 Azure 데이터 팩터리를 사용 하 여 클라우드 SFTP 서버에서 toomove 데이터입니다."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a>Azure Data Factory를 사용하여 SFTP 서버에서 데이터 이동
이 문서에서는 toouse hello 복사 작업에서-프레미스/클라우드 SFTP 서버 tooa에서 Azure Data Factory toomove 데이터에서 싱크 데이터 저장소를 지원 되는 방식에 대해 설명 합니다. Hello를 기반으로 한이 문서 [데이터 이동 작업](data-factory-data-movement-activities.md) 원본/싱크의로 지원 되는 데이터 저장소의 복사 작업 및 hello 목록 사용 하 여 데이터 이동의 일반적인 개요를 제공 하는 문서입니다.

데이터 팩터리의 현재만 지 원하는 SFTP 서버 tooother 데이터에서 데이터 저장소, 아니면 이동 tooan SFTP 서버 저장소를 다른 데이터와 데이터를 이동 합니다. 온-프레미스 및 클라우드 SFTP 서버를 지원합니다.

> [!NOTE]
> 복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다. 성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다. 

## <a name="supported-scenarios-and-authentication-types"></a>지원되는 시나리오 및 인증 형식
이 SFTP 커넥터 toocopy 데이터를 사용할 수 **SFTP 서버와 온-프레미스 SFTP 서버 클라우드 둘 다**합니다. **기본** 및 **SshPublicKey** toohello SFTP 서버에 연결 하는 경우에 인증 형식이 지원 됩니다.

온-프레미스 SFTP 서버에서 데이터를 복사할 때 hello 온-프레미스 환경/Azure VM에서에서 데이터 관리 게이트웨이 설치 해야 합니다. 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md) hello 게이트웨이에 대 한 자세한 내용은 합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서에 대 한 단계별 지침은 hello 게이트웨이를 설정 하 고 사용 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 SFTP 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

- hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

- 다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다. SFTP 서버 tooAzure Blob 저장소에서에서 toocopy 데이터를 샘플링 하는 JSON, 참조 [JSON의 예: SFTP 서버 tooAzure blob에서 데이터를 복사](#json-example-copy-data-from-sftp-server-to-azure-blob) 이 문서의 섹션.

## <a name="linked-service-properties"></a>연결된 서비스 속성
다음 표에서 hello JSON 요소 특정 tooFTP 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| type | 너무 hello 유형 속성을 설정 해야`Sftp`합니다. |예 |
| host | Hello SFTP 서버의 이름 또는 IP 주소입니다. |예 |
| 포트 |어떤 hello SFTP 서버 수신 대기 중인 포트입니다. hello 기본값은: 21 |아니요 |
| authenticationType |인증 유형을 지정합니다. 허용되는 값은 **기본** 및 **SshPublicKey**입니다. <br><br> 너무 참조[기본 인증을 사용 하 여](#using-basic-authentication) 및 [를 사용 하 여 SSH 공개 키 인증](#using-ssh-public-key-authentication) 더 많은 속성 및 JSON 샘플에서 각각 섹션. |예 |
| skipHostKeyValidation | Tooskip 호스트 키 유효성 검사 여부를 지정 합니다. | 아니요. hello 기본값: false |
| hostKeyFingerprint | Hello 호스트 키의 지문 안녕하세요를 지정 합니다. | 예 경우 hello `skipHostKeyValidation` toofalse 설정 됩니다.  |
| gatewayName |데이터 관리 게이트웨이 tooconnect tooan hello의 이름 온-프레미스 SFTP 서버. | 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에는 필수입니다. |
| encryptedCredential | 암호화 된 자격 증명 tooaccess hello SFTP 서버입니다. 자동 생성 된 복사 마법사 또는 hello ClickOnce 팝업 대화 상자에서 기본 인증 (사용자 이름 + 암호) 또는 SshPublicKey 인증 (사용자 이름 + 개인 키의 경로 또는 콘텐츠)를 지정 합니다. | 아니요. 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |

### <a name="using-basic-authentication"></a>기본 인증 사용

toouse 기본 인증 설정 `authenticationType` 으로 `Basic`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| username | 사용자가 액세스 toohello SFTP 서버입니다. |예 |
| 암호 | Hello 사용자 (사용자 이름)에 대 한 암호입니다. | 예 |

#### <a name="example-basic-authentication"></a>예: 기본 인증 사용
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>예: 암호화된 자격 증명으로 기본 인증 사용

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a>SSH 공개 키 인증 사용

toouse SSH 공용 키 인증, 설정 `authenticationType` 으로 `SshPublicKey`, hello SFTP 커넥터 hello 마지막 섹션에 도입 된 일반 자원을 hello 외에 다음과 같은 속성을 지정 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- | --- |
| username |액세스 toohello SFTP 서버에 있는 사용자 |예 |
| privateKeyPath | 절대 경로 toohello 지정 개인 키 파일 해당 게이트웨이에 액세스할 수 있습니다. | 어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다. <br><br> 온-프레미스 SFTP 서버에서 데이터를 복사하는 경우에만 적용됩니다. |
| privateKeyContent | Hello 개인 키 콘텐츠는 serialize 된 문자열입니다. hello 복사 마법사 hello 개인 키 파일 읽고 hello 개인 키 콘텐츠를 자동으로 추출할 수 있습니다. 모든 다른 도구/SDK를 사용 하는 경우 hello privateKeyPath 속성을 대신 사용 합니다. | 어느 hello 지정 `privateKeyPath` 또는 `privateKeyContent`합니다. |
| passPhrase | 암호 구문을 통해 hello 키 파일을 보호 하는 경우에 hello 전달 구를/암호 toodecrypt hello 개인 키를 지정 합니다. | Yes 전달 구에 의해 hello 개인 키 파일 보호를 사용 합니다. |

> [!NOTE]
> SFTP 커넥터는 OpenSSH 키만 지원합니다. 키 파일 hello 적절 한 형식에서 인지 확인 합니다. Putty 도구 tooconvert tooOpenSSH 형식.ppk에서에서 사용할 수 있습니다.

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a>예: 개인 키 파일 경로를 사용하여 SshPublicKey 인증

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>예: 개인 키 콘텐츠를 사용하여 SshPublicKey 인증

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.

hello **typeProperties** 섹션은 데이터 집합의 각 형식 마다 다릅니다. 가 특정 toohello 데이터 집합 형식 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **FileShare** 데이터 집합에 다음과 같은 속성 hello:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |하위 경로 toohello 폴더입니다. 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다. <br/><br/>Data.<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다.<br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: `"fileFilter": "*.log"`<br/>예 2: `"fileFilter": 2014-1-?.txt"`<br/><br/> fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다. 이 속성은 HDFS에는 지원되지 않습니다. |아니요 |
| partitionedBy |partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다. 예를 들어 매시간 데이터에 대한 매개 변수가 있는 folderPath입니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |
| useBinaryTransfer |이전 전송 모드를 사용할지 여부를 지정합니다. 이진 모드인 경우 true이고 ASCII인 경우 false입니다. 기본값은 True입니다. 이 속성은 연결된 서비스 유형이 FtpServer인 경우에만 사용할 수 있습니다. |아니요 |

> [!NOTE]
> filename 및 fileFilter는 동시에 사용할 수 없습니다.

### <a name="using-partionedby-property"></a>partionedBy 속성 사용
Hello 이전 섹션에서 설명 했 듯이 동적 folderPath에 partitionedBy 된 시계열 데이터에 대 한 파일 이름을 지정할 수 있습니다. Hello Data Factory 매크로와 SliceEnd hello 지정 된 데이터 조각에 대 한 논리적 기간을 나타내는 hello 시스템 변수 SliceStart, 그렇게 할 수 있습니다.

toolearn 시간 시계열 데이터 집합, 일정 및 분할 하는 방법에 대 한 참조 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md) 문서입니다.

#### <a name="sample-1"></a>샘플 1:

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다. hello SliceStart hello 조각의 toostart 시간을 의미합니다. hello folderPath 각 조각에 대 한 차이가 있습니다. 예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.

#### <a name="sample-2"></a>샘플 2:

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
이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업에 대 한 hello 형식 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다.

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a>지원되는 파일 및 압축 형식
자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a>SFTP 서버 tooAzure blob에서 데이터를 복사 하는 JSON의 예:
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. SFTP에서 toocopy 데이터 tooAzure Blob 저장소를 원본 하는 방법을 보여 줍니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

> [!IMPORTANT]
> 이 샘플은 JSON 코드 조각을 제공합니다. Hello 데이터 팩터리를 만들기 위한 단계별 지침을 다루지 않습니다. 단계별 지침은 [온-프레미스 위치와 클라우드 간에 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서를 참조하세요.

hello 샘플 hello 데이터 팩터리 엔터티 뒤에 있습니다.

* [sftp](#linked-service-properties) 형식의 연결된 서비스
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
* [FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 SFTP 서버 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**SFTP 연결된 서비스**

이 예제에서는 사용자 이름과 암호가 일반 텍스트로 hello 기본 인증을 사용 합니다. 또한 hello 같은 방법으로 다음 중 하나를 사용할 수 있습니다.

* 암호화된 자격 증명으로 기본 인증 
* SSH 공개 키 인증

사용할 수 있는 다른 유형의 인증은 [FTP 연결 서비스](#linked-service-properties) 섹션을 참조하세요.

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
**Azure 저장소 연결된 서비스**

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
**SFTP 입력 데이터 집합**

이 데이터 집합 참조 toohello SFTP 폴더 `mysharedfolder` 파일과 `test.csv`합니다. hello 파이프라인 hello 파일 toohello 대상에 복사합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Azure Blob 출력 데이터 집합**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**복사 작업을 포함하는 파이프라인**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.

## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 참조 하십시오.

* [복사 작업 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) .
