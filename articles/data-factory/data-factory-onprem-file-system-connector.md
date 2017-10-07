---
title: "Azure 데이터 팩터리를 사용 하 여 파일 시스템에서 데이터를 aaaCopy | Microsoft Docs"
description: "자세한 내용은 방법 Azure 데이터 팩터리를 사용 하 여 온-프레미스 파일 시스템에서 데이터 tooand toocopy 합니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 온-프레미스 파일 시스템에서 데이터 tooand 복사
이 문서에서는 toouse 온-프레미스 파일 시스템에서 Azure Data Factory toocopy 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **온-프레미스 파일 시스템에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooan 온-프레미스 파일 시스템**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> 복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다. 성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다. 

## <a name="enabling-connectivity"></a>연결 사용
데이터 팩터리를 통해 온-프레미스 파일 시스템에서 연결 tooand 지원 **데이터 관리 게이트웨이**합니다. Hello Data Factory 서비스 tooconnect tooany 지원 되는 온-프레미스 데이터 저장소 용 파일 시스템을 포함 하 여 온-프레미스 환경에서 hello 데이터 관리 게이트웨이 설치 해야 합니다. toolearn hello 게이트웨이 설정에 대 한 단계별 지침은 및 데이터 관리 게이트웨이 대 한 참조 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다. 데이터 관리 게이트웨이 외에도 다른 이진 파일이 설치 toobe toocommunicate tooand 온-프레미스 파일 시스템에서 필요합니다. 설치 하 고 hello 파일 시스템은 Azure IaaS VM의 경우에 hello 데이터 관리 게이트웨이 사용 해야 합니다. Hello 게이트웨이에 대 한 자세한 내용은 참조 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)합니다.

toouse Linux 파일 공유, 설치 [Samba](https://www.samba.org/) Linux 서버 및 Windows 서버에서 데이터 관리 게이트웨이 설치 합니다. Linux 서버에 대한 데이터 관리 게이트웨이 설치는 지원되지 않습니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 파일 시스템 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Azure blob 저장소 tooan 온-프레미스 파일 시스템에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink 온-프레미스 파일 시스템 및 Azure 저장소 계정 tooyour 데이터 팩터리입니다. 연결 된 서비스를 속성에는 특정 tooan 온-프레미스 파일 시스템에 대 한 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션.
3. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다. 고 다른 데이터 집합 toospecify hello 폴더 및 파일 이름 파일 시스템에서 (선택 사항)를 만듭니다. 데이터 집합 속성을 특정 tooon 온-프레미스 파일 시스템에 대 한 참조 [데이터 집합 속성](#dataset-properties) 섹션.
4. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 FileSystemSink 싱크도 hello 복사 작업에 대 한 합니다. 마찬가지로, 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 복사 하는 경우 FileSystemSource 및 사용 BlobSink hello 복사 활동에서. 복사 활동 속성을 특정 tooon 온-프레미스 파일 시스템에 대 한 참조 [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플 은/파일 시스템에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-file-system) 이 문서의 섹션.

사용 되는 toodefine Data Factory 엔터티에 특정 toofile 시스템은 JSON 속성에 대 한 세부 정보를 제공 하는 다음 섹션 hello:

## <a name="linked-service-properties"></a>연결된 서비스 속성
온-프레미스 파일 시스템 tooan Azure 데이터 팩터리에 hello로 연결할 수 있습니다 **온-프레미스 파일 서버** 연결 된 서비스입니다. 다음 표에서 hello JSON 요소를 특정 toohello 온-프레미스 파일 서버를 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |Hello type 속성이 너무 설정 되어 있는지 확인**OnPremisesFileServer**합니다. |예 |
| host |Toocopy hello 폴더의 hello 루트 경로 지정 합니다. Hello 이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요. |예 |
| userid |Hello 있는 사용자에 게 액세스 toohello 서버 hello ID를 지정 합니다. |아니요(encryptedCredential을 선택하는 경우) |
| 암호 |Hello 사용자 (userid)에 대 한 hello 암호를 지정 합니다. |아니요(encryptedcredential을 선택하는 경우) |
| encryptedCredential |새로 만들기-AzureRmDataFactoryEncryptValue hello cmdlet을 실행 하 여 얻을 수 있는 암호화 hello 자격 증명을 지정 합니다. |아니요 (일반 텍스트로 toospecify userid 및 password 선택) 하는 경우 |
| gatewayName |데이터 팩터리 tooconnect toohello 온-프레미스 파일 서버를 사용 해야 하는 hello 게이트웨이의 hello 이름을 지정 합니다. |예 |


### <a name="sample-linked-service-and-dataset-definitions"></a>연결된 서비스 및 데이터 집합 정의 샘플
| 시나리오 | 연결된 서비스 정의의 호스트 | 데이터 집합 정의의 folderPath |
| --- | --- | --- |
| 데이터 관리 게이트웨이 컴퓨터의 로컬 폴더:  <br/><br/>예: D:\\\* 또는 D:\folder\subfolder\\* |D:\\\\(데이터 관리 게이트웨이 버전 2.0 이상) <br/><br/> localhost(데이터 관리 게이트웨이 버전 2.0 미만) |.\\\\ 또는 folder\\\\subfolder(데이터 관리 게이트웨이 버전 2.0 이상) <br/><br/>D:\\\\ 또는 D:\\\\folder\\\\subfolder(게이트웨이 버전 2.0 미만) |
| 원격 공유 폴더:  <br/><br/>예: \\\\myserver\\share\\\* 또는 \\\\myserver\\share\\folder\\subfolder\\* |\\\\\\\\myserver\\\\share |.\\\\ 또는 folder\\\\subfolder |


### <a name="example-using-username-and-password-in-plain-text"></a>예제: 일반 텍스트에 사용자 이름 및 암호 사용

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a>예제: encryptedcredential 사용

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다.

hello typeProperties 섹션은 데이터 집합의 각 유형에 대해 다릅니다. Hello 위치와 hello 데이터 저장소에 hello 데이터 형식과 같은 정보를 제공 합니다. hello typeProperties 형식의 hello 데이터 집합에 대 한 섹션 **FileShare** hello 다음과 같은 속성에:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |Hello 하위 경로 toohello 폴더를 지정합니다. Hello 이스케이프 문자를 사용 하 여 ' \' hello 문자열의 특수 문자에 대 한 합니다. 예제를 살펴보려면 [연결된 서비스 및 데이터 집합 정의 샘플](#sample-linked-service-and-dataset-definitions) 을 참조하세요.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello hello 생성 된 파일의 이름이 형식에 따라 hello에 활동 싱크에 지정 되지 않은: <br/><br/>`Data.<Guid>.txt`(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| fileFilter |필터 toobe tooselect 사용 되는 모든 파일이 아니라 hello folderPath에 있는 파일의 하위 집합을 지정 합니다. <br/><br/>허용 되는 값은 `*`(여러 문자) 및 `?`(하나의 문자)입니다.<br/><br/>예 1: "fileFilter": "*.log"<br/>예 2: "fileFilter": 2014-1-?. txt "<br/><br/>fileFilter는 FileShare 입력 데이터 집합에 적용할 수 있습니다. |아니요 |
| partitionedBy |시계열 데이터에 대 한 partitionedBy toospecify 동적 folderPath/파일 이름을 사용할 수 있습니다. 예를 들어 매시간 데이터에 대한 매개 변수를 포함하는 folderPath가 있습니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

> [!NOTE]
> fileName 및 fileFilter는 동시에 사용할 수 없습니다.

### <a name="using-partitionedby-property"></a>partitionedBy 속성 사용
동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.

toounderstand 시계열 데이터 집합, 일정 및 분할에 대 한 자세한 내용은 참조 [데이터 집합을 만드는](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md)합니다.

#### <a name="sample-1"></a>샘플 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

이 예제에서 {Slice} hello (yyyymmddhh)에서 hello 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다. SliceStart는 hello 조각의 toostart 시간을 의미합니다. hello folderPath 각 조각에 대 한 차이가 있습니다. 예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.

#### <a name="sample-2"></a>샘플 2:

```JSON
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

이 예제에서는 SliceStart의 년, 월, 일, 시간과 hello folderPath 및 fileName 속성에 사용 하는 개별 변수로 추출 됩니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다. 반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다.

복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다. 온-프레미스 파일 시스템에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**FileSystemSource**합니다. 마찬가지로, 데이터 tooan를 이동 하는 경우 온-프레미스 파일 시스템, 너무 hello 복사 작업에서 싱크 유형이 hello을 설정**FileSystemSink**합니다. 이 섹션에서는 FileSystemSource 및 FileSystemSink에서 지원되는 속성의 목록을 제공합니다.

**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 지정 된 폴더 또는 hello 하위 폴더에서 나타냅니다. |True, False(기본값) |아니요 |

**FileSystemSink** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| copyBehavior |파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다. |**PreserveHierarchy:** hello 대상 폴더에서 hello 파일 계층 구조를 유지 합니다. 즉, hello 소스 파일 toohello 원본 폴더의 상대 경로 hello hello hello 대상 파일 toohello 대상 폴더의 상대 경로와 같은 hello 됩니다.<br/><br/>**FlattenHierarchy:** hello 원본 폴더에서 모든 파일은 hello 첫 번째 수준의 대상 폴더에 만들어집니다. hello 대상 파일은 자동으로 생성 된 이름으로 만들어집니다.<br/><br/>**MergeFiles:** hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 파일 이름/blob 이름이 지정 된 경우 hello 병합 된 파일 이름은 hello 지정 된 이름이입니다. 그렇지 않으면 자동 생성되는 파일 이름이 적용됩니다. |아니요 |

### <a name="recursive-and-copybehavior-examples"></a>recursive 및 copyBehavior 예제
이 섹션에서는 hello hello 재귀 및 copyBehavior 속성에 대 한 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.

| recursive 값 | copyBehavior 값 | 결과 동작 |
| --- | --- | --- |
| true |preserveHierarchy |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 소스로 구조체 같은 hello로 Folder1 hello 대상 폴더를 만듭니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 |
| true |flattenHierarchy |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름 |
| true |mergeFiles |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다. |
| false |preserveHierarchy |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다. |
| false |flattenHierarchy |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/><br/>File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다. |
| false |mergeFiles |구조에 따라 hello로 Folder1 소스 폴더에 대 한<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 폴더 Folder1 hello 구조를 다음으로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다.<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동 생성된 이름<br/><br/>File3, File4, File5를 포함한 Subfolder1은 선택되지 않습니다. |

## <a name="supported-file-and-compression-formats"></a>지원되는 파일 및 압축 형식
자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a>파일 시스템에서 데이터 tooand 복사 하기 위한 JSON 예제
hello 다음 예에서는 샘플 JSON 정의 hello를 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 표시 방법을 toocopy 데이터 tooand에서 온-프레미스 파일 시스템 및 Azure Blob 저장소의 합니다. 그러나 데이터를 복사할 수 있습니다 *직접* hello 싱크에 나열 된 hello 소스 tooany 중 어디에서 든 [원본 및 싱크를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업을 사용 하 여 합니다.

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a>예: 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 데이터를 복사 합니다.
이 샘플은 어떻게 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 toocopy 데이터입니다. hello 샘플 Data Factory 엔터티에 따라 hello에 있습니다.

* [OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
* [FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

다음 예제는 hello 시계열 데이터 복사 온-프레미스 파일 시스템 tooAzure Blob 저장소에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 후 hello 섹션에 설명 되어 있습니다.

첫 번째 단계로, 설정 데이터 관리 게이트웨이 hello 지침에 따라 [온-프레미스 원본 및 데이터 관리 게이트웨이 사용 하는 hello 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md)합니다.

**온-프레미스 파일 서버 연결 서비스:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Hello를 사용 하는 것이 좋습니다 **encryptedCredential** 속성 대신 hello **userid** 및 **암호** 속성입니다. 이 연결 서비스에 대한 자세한 내용은 [파일 서버 연결 서비스](#linked-service-properties)를 참조하세요.

**Azure 저장소 연결 서비스:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**온-프레미스 파일 시스템 입력 데이터 집합:**

데이터는 매시간 새 파일에서 선택됩니다. hello folderPath 및 fileName 속성 hello 조각의 hello 시작 시간에 따라 결정 됩니다.  

설정 `"external": "true"` 알리고 Data Factory hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**Azure Blob 저장소 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
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
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a>예: Azure SQL 데이터베이스 tooan 온-프레미스 파일 시스템에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

* [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.
* [OnPremisesFileServer](#linked-service-properties)형식의 연결된 서비스
* [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 데이터 집합입니다.
* [FileShare](#dataset-properties) 형식의 출력 데이터 집합입니다.
* [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) 및 [FileSystemSink](#copy-activity-properties)를 사용하는 복사 작업의 파이프라인입니다.

hello 샘플 시계열 데이터 복사 Azure SQL 테이블 tooan 온-프레미스 파일 시스템에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성은 hello 샘플 이후 섹션에서 설명 합니다.

**Azure SQL Database 연결된 서비스:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

**온-프레미스 파일 서버 연결 서비스:**

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

Hello를 사용 하는 것이 좋습니다 **encryptedCredential** hello를 사용 하는 대신 속성 **userid** 및 **암호** 속성입니다. 이 연결 서비스에 대한 자세한 내용은 [파일 시스템 연결 서비스](#linked-service-properties)를 참조하세요.

**Azure SQL 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 되었다고 가정 합니다.

설정 ``“external”: ”true”`` 알리고 Data Factory hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**온-프레미스 파일 시스템 출력 데이터 집합:**

데이터 복사 tooa 새 파일을 1 시간입니다. hello folderPath 및 fileName hello blob에 대 한 hello 조각의 hello 시작 시간에 따라 결정 됩니다.

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

**SQL 원본 및 파일 시스템 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource**, 및 hello **싱크** 형식이 너무 설정**FileSystemSink**합니다. hello에 대해 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


원본 데이터 집합 toocolumns hello 복사 활동 정의에서 싱크 데이터 집합에서의 열을 매핑할 수도 있습니다. 자세한 내용은 [Azure Data Factory에서 데이터 집합 열 매핑](data-factory-map-columns.md)을 참조하세요.

## <a name="performance-and-tuning"></a>성능 및 튜닝
 toolearn 키에 대 한 해당 hello 성능에 영향을 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.
