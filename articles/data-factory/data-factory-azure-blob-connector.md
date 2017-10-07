---
title: "Azure Blob 저장소에서 데이터를 aaaCopy | Microsoft Docs"
description: "어떻게 toocopy blob Azure Data Factory에는 데이터에 알아봅니다. 이 샘플을 사용 하 여: 어떻게 Azure Blob 저장소 및 Azure SQL 데이터베이스에서 데이터 tooand toocopy 합니다."
keywords: "Blob 데이터, Azure Blob 복사"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a>Azure 데이터 팩터리를 사용 하 여 Azure Blob 저장소에서 데이터 tooor 복사
이 문서에서는 toouse 복사 작업에서 Azure Blob 저장소에서 Azure Data Factory toocopy 데이터 tooand hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

## <a name="overview"></a>개요
데이터 저장 tooAzure Blob 저장소 또는 저장소 지원 tooany 싱크 데이터를 Azure Blob 저장소에서 모든 지원 되는 원본에서 데이터를 복사할 수 있습니다. hello 다음 테이블 원본으로 지 원하는 데이터 저장소의 목록을 제공 하거나 hello 복사 작업에서 싱크 합니다. 예를 들어 데이터를 SQL Server 데이터베이스 또는 Azure SQL 데이터베이스**에서** Azure Blob 저장소**로**로 이동할 수 있습니다. 그리고 데이터를 Azure Blob Storage 저장소**에서** Azure SQL Data Warehouse 또는 Azure Cosmos DB 컬렉션**으로** 복사할 수 있습니다. 

## <a name="supported-scenarios"></a>지원되는 시나리오
데이터를 복사할 수 **Azure Blob 저장소에서** toohello 데이터 저장소를 다음:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Hello 다음 데이터 저장소에서에서 데이터를 복사할 수 **tooAzure Blob 저장소**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> 복사 작업의 데이터 복사를 지원 합니다. / tooboth 범용 Azure 저장소 계정 및 핫 냉각용/Blob 저장소입니다. hello 활동 지원 **블록에서 읽기, 추가 또는 페이지 blob**를 지원 하지만 **tooonly 블록 blob 쓰기**합니다. Azure Premium Storage는 페이지 Blob으로 지원되므로 싱크로 지원하지 않습니다.
> 
> 복사 활동 데이터를 성공적으로 hello toohello 대상 복사 후 hello 소스에서 데이터 삭제 되지 않습니다. 성공적인 복사 후 toodelete 원본 데이터를 필요한 경우 만들는 [사용자 지정 활동](data-factory-use-custom-activities.md) toodelete 데이터 hello 및 hello 파이프라인에서 hello 활동을 사용 합니다. 예를 들어 참조 hello [GitHub에 Delete blob 또는 폴더 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity)합니다. 

## <a name="get-started"></a>시작
다른 도구/API를 사용하여 Azure Blob Storage 간에 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 이 기술 자료이 문서에는 [연습](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) 파이프라인 toocopy 데이터를 Azure Blob 저장소 위치 tooanother Azure Blob 저장소 위치에서에서 합니다. Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 파이프라인 toocopy 데이터를 만드는 방법에 대 한 자습서를 참조 하십시오. [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md)합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. **데이터 팩터리**를 만듭니다. 데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 
2. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다. 예를 들어 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 경우 만들면 두 개의 연결 된 서비스 toolink Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리입니다. 연결 된 서비스를 속성에는 특정 tooAzure Blob 저장소에 대 한 참조 [연결 된 서비스 속성](#linked-service-properties) 섹션. 
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다. Hello 마지막 단계에서 언급 한 hello 예제에서는 데이터 집합 toospecify hello blob 컨테이너 및 hello 입력된 데이터를 포함 된 폴더를 만듭니다. 고 hello blob 저장소에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터베이스에서 다른 데이터 집합 toospecify hello SQL 테이블을 만듭니다. 특정 tooAzure Blob 저장소는 데이터 집합 속성을 참조 하십시오. [데이터 집합 속성](#dataset-properties) 섹션.
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다. 앞에서 언급 한 hello 예제에서는 사용 BlobSource 원본과 SqlSink 싱크도 hello 복사 작업에 대 한 합니다. 마찬가지로, Azure SQL 데이터베이스 tooAzure Blob 저장소에서에서 복사 하는 경우 SqlSource 및 사용 BlobSink hello 복사 활동에서. 복사 활동 속성을 특정 tooAzure Blob 저장소를 참조 하십시오. [활동 속성을 복사](#copy-activity-properties) 섹션. 에 대 한 내용은 toouse 데이터 저장 되는 방식과 원본 또는 싱크도, 데이터 저장소에 대 한 hello 이전 단원의 hello 링크를 클릭 합니다.  

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  샘플은 Azure Blob 저장소에서 사용 되는 toocopy 데이터를 Data Factory 엔터티에 대 한 JSON 정의 가진 [JSON 예제](#json-examples-for-copying-data-to-and-from-blob-storage  ) 이 문서의 섹션.

다음 섹션 hello JSON 속성을 사용 하는 toodefine Data Factory 엔터티에 특정 tooAzure Blob 저장소에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
두 가지가 연결 된 서비스의 toolink tooan Azure 데이터 팩터리에 Azure 저장소를 사용할 수 있습니다. **AzureStorage** 연결된 서비스 및 **AzureStorageSas** 연결된 서비스입니다. Azure 저장소 연결 서비스 hello 전역 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다. 반면 hello Azure 저장소 SAS (공유 액세스 서명) 연결 된 서비스 시간 제한/범위 액세스 toohello Azure 저장소와 hello data factory에 제공 합니다. 이 두 연결된 서비스에는 다른 차이가 없습니다. 필요에 맞는 hello 연결 된 서비스를 선택 합니다. hello 다음 섹션에서는 더욱 자세히 설명에 두 개의 연결 된 서비스입니다.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 집합 toorepresent toospecify hello 데이터 집합의 hello 형식 속성을 설정 Azure Blob 저장소의 데이터 입력 또는 출력: **AzureBlob**합니다. 집합 hello **linkedServiceName** hello Azure 저장소 서비스 또는 Azure 저장소 SAS의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다.  hello 데이터 집합의 hello 유형 속성 지정 hello **blob 컨테이너** 및 hello **폴더** hello blob 저장소에 있습니다.

JSON 섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 참조 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

데이터 팩터리의 지원 "구조" 읽기 스키마에 데이터 원본에 대 한 Azure blob 등의 형식 정보를 제공 하는 데 CLS 규격.NET 기반 유형 값을 다음 hello: Int16, Int32, Int64, Single, Double, Decimal, Byte, Bool, String, Guid, Datetime, Datetimeoffset, Timespan입니다. 데이터 팩터리 tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동할 때 자동으로 형식 변환을 수행 합니다.

hello **typeProperties** 섹션 데이터 집합의 각 유형에 대해 서로 다른 이며 정보 제공 hello 위치에 대 한 서식을 지정 등을 hello 데이터 저장소에서 hello 데이터입니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **AzureBlob** 데이터 집합에 다음과 같은 속성 hello:

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |경로 toohello 컨테이너 및 blob 저장소 hello에에서 폴더입니다. 예제: myblobcontainer\myblobfolder\ |예 |
| fileName |Hello blob 이름입니다. fileName은 선택 사항이며 대/소문자를 구분합니다.<br/><br/>에 파일 이름, hello 작업 (복사본 포함) 작동을 지정한 경우에 특정 Blob을 hello 합니다.<br/><br/>파일 이름을 지정 하지 않으면 복사 입력된 데이터 집합에 대 한 hello folderPath에 모든 Blob을 포함 합니다.<br/><br/>때 **fileName** 출력 데이터 집합에 지정 되지 않은 및 **preserveHierarchy** hello 생성 된 파일의 이름을 hello 것이 형식에 따라 hello에 활동 싱크에 지정 되지 않은: 데이터.<Guid>합니다. txt (예:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |아니요 |
| partitionedBy |partitionedBy는 선택적 속성입니다. 사용할 수 있습니다 toospecify 동적 folderPath 및 filename 시계열 데이터에 대 한 합니다. 예를 들어 folderPath는 매시간 데이터에 대한 매개 변수화됩니다. Hello 참조 [partitionedBy 속성 섹션을 사용 하 여](#using-partitionedBy-property) 자세한 내용 및 예제입니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

### <a name="using-partitionedby-property"></a>partitionedBy 속성 사용
동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.

시간 시계열 데이터 집합, 예약 및 조각에 대한 자세한 내용은 [데이터 집합 만들기](data-factory-create-datasets.md) 및 [일정 예약 및 실행](data-factory-scheduling-and-execution.md) 문서를 참조하세요.

#### <a name="sample-1"></a>샘플 1

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다. hello SliceStart hello 조각의 toostart 시간을 의미합니다. hello folderPath 각 조각에 대 한 차이가 있습니다. 예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다

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

이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 데이터 집합, 정책 등의 속성은 모든 유형의 활동에 사용할 수 있습니다. 반면 hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다. Azure Blob 저장소에서 데이터를 이동 하는 경우 hello 소스 형식에서에서 설정한 hello 복사 활동 너무**BlobSource**합니다. 마찬가지로, 데이터 tooan Azure Blob 저장소를 이동 하는 경우 설정한 hello 싱크 유형이 hello 복사 활동에서 너무**BlobSink**합니다. 이 섹션에서는 BlobSource 및 BlobSink에서 지원되는 속성의 목록을 제공합니다.

**BlobSource** hello 다음과 같은 hello에 대 한 속성을 지 원하는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True(기본값), False |아니요 |

**BlobSink** hello 다음과 같은 속성을 지 원하는 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| copyBehavior |파일 시스템이 나 BlobSource hello 원본이 상태인 hello 복사 동작을 정의 합니다. |<b>PreserveHierarchy</b>: 전처리 hello hello 대상 폴더에서 파일 계층 구조입니다. hello 소스 파일 toosource 폴더의 상대 경로 동일한 toohello 대상 파일 tootarget 폴더의 상대 경로입니다.<br/><br/><b>FlattenHierarchy</b>: hello 원본 폴더에서 모든 파일에에서 있는 hello 먼저 대상 폴더의 수준입니다. hello 대상 파일에는 자동 생성 된 이름이 있습니다. <br/><br/><b>MergeFiles</b>: hello 소스 폴더 tooone 파일에서 모든 파일을 병합 합니다. Hello 병합 된 파일 이름이 name을 지정된 하는 hello; 됩니다 hello 파일/Blob 이름이 지정 된 경우 그렇지 않은 경우 자동으로 생성 된 파일 이름 것입니다. |아니요 |

**BlobSource**에서도 이전 버전과의 호환성을 위해 이러한 두 속성을 지원합니다.

* **treatEmptyAsNull**:를 지정 하는지 여부를 null 값으로 tootreat null 또는 빈 문자열입니다.
* **skipHeaderLineCount** - 건너뛰어야 하는 줄 수를 지정합니다. 입력 데이터 집합이 TextFormat을 사용하는 경우에만 해당합니다.

마찬가지로, **BlobSink** hello 다음 이전 버전과 호환성에 대 한 속성을 지원 합니다.

* **blobWriterAddHeader**: tooadd tooan에 쓰는 동안 열 정의의 헤더 출력 데이터 집합 여부를 지정 합니다.

다음과 같은 속성을 구현 하는 데이터 집합 지금은 지원 hello hello 동일한 기능: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**합니다.

hello 다음 표에서 지침에 대해 이러한 blob 원본/싱크 속성 대신 hello 새 데이터 집합 속성을 사용 하 여 합니다.

| 복사 작업 속성 | 데이터 집합 속성 |
|:--- |:--- |
| BlobSource에서 skipHeaderLineCount |skipLineCount 및 firstRowAsHeader. 줄은 먼저 건너뜁니다 고 hello 첫 번째 행을 머리글로 다음 읽혀집니다. |
| BlobSource에서 treatEmptyAsNull |입력 데이터 집합에서 treatEmptyAsNull |
| BlobSink에서 blobWriterAddHeader |출력 데이터 집합에서 firstRowAsHeader |

이러한 속성에 대한 자세한 내용은 [TextFormat 지정](data-factory-supported-file-and-compression-formats.md#text-format) 섹션을 참조하세요.    

### <a name="recursive-and-copybehavior-examples"></a>recursive 및 copyBehavior 예제
이 섹션에서는 hello 재귀 및 copyBehavior 값의 다른 조합에 대 한 hello 복사 작업의 결과 동작을 설명 합니다.

| recursive | copyBehavior | 결과 동작 |
| --- | --- | --- |
| true |preserveHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 폴더가 Folder1 hello 소스로 구조체 같은 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| true |flattenHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File3에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4에 대해 자동 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5에 대해 자동 생성된 이름 |
| true |mergeFiles |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>hello 대상 Folder1 hello 구조를 다음으로 만들어집니다. <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1, File2, File3, File4 및 File5의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다. |
| false |preserveHierarchy |원본 폴더의 Folder1 구조를 다음 hello로: <br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |
| false |flattenHierarchy |원본 폴더의 Folder1 구조를 다음 hello로:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1에 대해 자동으로 생성된 이름<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2에 대해 자동 생성된 이름<br/><br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |
| false |mergeFiles |원본 폴더의 Folder1 구조를 다음 hello로:<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5<br/><br/>Folder1 hello 대상 폴더 구조를 다음 hello로 만들어집니다.<br/><br/>Folder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1과 File2의 파일 내용이 자동 생성된 파일 이름을 사용하는 파일 하나로 병합됩니다. File1에 대해 자동으로 생성된 이름<br/><br/>File3, File4, File5를 가진 Subfolder1은 선택되지 않습니다. |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a>연습: 복사 마법사를 사용 하 여 toocopy 한 데이터를 Blob 저장소에서
어떻게 tooquickly 복사 데이터는 Azure에서 blob 저장소에서 살펴보겠습니다. 이 연습에 나오는 원본 및 대상 데이터 저장소의 유형은 모두 Azure Blob Storage입니다. hello이 연습에는 파이프라인에서에서 데이터를 복사 hello에서 폴더 tooanother 동일한 blob 컨테이너입니다. 이 연습에서는 의도적으로 간단한 tooshow 설정이 나 원본 또는 싱크도 Blob 저장소를 사용 하는 경우 속성이 있습니다. 

### <a name="prerequisites"></a>필수 조건
1. 아직 만들지 않은 경우 범용 **Azure Storage 계정**을 만듭니다. Hello blob 저장소를 사용 하 여 두 가지 모두 **소스** 및 **대상** 이 연습에 데이터를 저장 합니다. Azure 저장소 계정이 없으면 참조 hello [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 단계 toocreate 하나에 대 한 문서입니다.
2. 라는 blob 컨테이너 만들기 **adfblobconnector** hello 저장소 계정에 있습니다. 
4. 라는 폴더를 만듭니다 **입력** hello에 **adfblobconnector** 컨테이너입니다.
5. 라는 파일을 만들어 **emp.txt** 다음 hello로 콘텐츠 및 toohello 업로드 **입력** 폴더와 같은 도구를 사용 하 여 [Azure 저장소 탐색기](https://azurestorageexplorer.codeplex.com/)
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a>Hello 데이터 팩터리 만들기
1. Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.
2. 클릭 **+ 새로 만들기** hello 왼쪽 위 모퉁이에서 클릭 **인텔리전스 + 분석**를 클릭 하 고 **Data Factory**합니다.
3. Hello에 **새 데이터 팩터리** 블레이드:   
    1. 입력 **ADFBlobConnectorDF** hello에 대 한 **이름**합니다. hello Azure 데이터 팩터리의 hello 이름을 전역적으로 고유 해야 합니다. Hello 오류가 나타나면: `*Data factory name “ADFBlobConnectorDF” is not available`을 hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameADFBlobConnectorDF)을 변경 하 고 다시 만들어 보십시오. 데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.
    2. Azure **구독**을 선택합니다.
    3. 리소스 그룹에 대 한 선택 **기존 항목 사용** tooselect 기존 리소스 그룹 (또는) 선택 **새로 만들기** tooenter 리소스 그룹에 대 한 이름입니다.
    4. 선택 된 **위치** hello 데이터 팩토리에 대 한 합니다.
    5. 선택 **Pin toodashboard** hello hello 블레이드 맨 아래에 있는 확인란 합니다.
    6. **만들기**를 클릭합니다.
3. Hello 참조 hello 만들기가 완료 되 면 **Data Factory** hello 다음 이미지와 같이 블레이드: ![데이터 팩터리 홈 페이지](./media/data-factory-azure-blob-connector/data-factory-home-page.png)

### <a name="copy-wizard"></a>복사 마법사
1. Hello Data Factory 홈 페이지에서 클릭 hello **[미리 보기] 데이터를 복사** toolaunch 타일 **복사 데이터 마법사** 별도 탭에 있습니다.    
    
    > [!NOTE]
    >    해당 hello 웹 브라우저에서 "권한 부여..." 걸려 표시 되 면 사용 안 함/취소 **타사 쿠키를 차단 하 고 사이트 데이터** 설정 (또는)에 사용 가능한 상태로 유지 하 고 예외를 만들 **login.microsoftonline.com**및 hello 마법사를 다시 시작 해 보십시오.
2. Hello에 **속성** 페이지:
    1. **작업 이름**에 대해 **CopyPipeline**을 입력합니다. hello 작업 이름은 hello 데이터 팩터리에 파이프라인의 hello 이름이입니다.
    2. 입력 한 **설명** hello 작업 (옵션)에 대 한 합니다.
    3. 에 대 한 **작업 흐름 또는 작업 일정**, hello 유지 **일정에 따라 정기적으로 실행** 옵션입니다. Toorun 대신 한 번만이 작업 일정에 따라 반복적으로 실행 선택 **이제 한 번 실행**합니다. **지금 한 번 실행** 옵션을 선택하면 [일회성 파이프라인](data-factory-create-pipelines.md#onetime-pipeline)이 만들어집니다. 
    4. 에 대 한 hello 설정을 유지 **되풀이 패턴**합니다. Hello 다음 단계에서이 작업을 매일 실행 hello 사이의 시작 및 종료 시간을 지정 합니다.
    5. 변경 hello **시작 날짜 시간이** 너무**04/21/2017**합니다. 
    6. 변경 hello **종료 날짜 시간** 너무**04/25/2017**합니다. Hello 달력을 찾아보는 대신 tootype hello 날짜를 할 수 있습니다.     
    8. **다음**을 누릅니다.
      ![복사 도구 - 속성 페이지](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png) 
3. Hello에 **소스 데이터 저장소** 페이지 **Azure Blob 저장소** 바둑판식으로 배열입니다. 이 페이지 toospecify hello 원본 데이터 저장소를 사용 하 여 hello 복사 작업에 대 한 합니다. 기존 데이터 저장소 연결된 서비스를 사용하거나 새 데이터 저장소를 지정할 수 있습니다. 연결 된 서비스는 기존 toouse, 선택 **에서 기존 연결 된 서비스** 선택 hello 오른쪽 연결 된 서비스 및 합니다. 
    ![복사 도구 - 원본 데이터 저장소 페이지](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)
4. Hello에 **hello Azure Blob 저장소 계정을 지정** 페이지:
   1. Hello에 대 한 자동 생성 된 이름을 유지 **연결 이름**합니다. hello 연결 이름은 hello 유형의 hello 연결 된 서비스 이름입니다: Azure 저장소입니다. 
   2. **계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.
   3. Azure 구독을 선택하거나 **Azure 구독**에 대해 **모두 선택**을 유지합니다.   
   4. 선택 된 **Azure 저장소 계정** hello에서 목록은 Azure 저장소 계정 선택 hello 구독에서 사용할 수 있습니다. 선택할 수도 있습니다 tooenter 저장소 계정 설정을 수동으로 선택 하 여 **수동으로 입력** hello에 대 한 옵션 **계정 선택 방법을**합니다.
   5. **다음**을 누릅니다. 
      ![도구에 복사-hello Azure Blob 저장소 계정을 지정 합니다.](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)
5. **선택 hello 입력된 파일이 나 폴더** 페이지:
   1. **adfblobcontainer**를 두 번 클릭합니다.
   2. **input**을 선택하고 **선택**을 클릭합니다. 이 연습에서는 hello 입력된 폴더를 선택합니다. 선택할 수 있습니다 hello emp.txt 파일 hello 폴더에 대신 합니다. 
      ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)
6. Hello에 **선택 hello 입력된 파일이 나 폴더** 페이지:
    1. 해당 hello 확인 **파일 또는 폴더** 너무 설정**adfblobconnector/입력**합니다. Hello 파일이 하위 폴더에 있는 경우 예를 들어 2017/04/01, 02, 2017/04/및, 값을 입력 adfblobconnector / / {year} / {month} / {day} 파일 또는 폴더에 대 한 합니다. Hello 텍스트 상자에서 TAB 키를 누르는 경우 연도 (yyyy), (MM), 월 및 일 (dd)에 대 한 세 가지 드롭 다운 목록을 tooselect 형식 표시 됩니다. 
    2. **파일을 재귀적으로 복사**는 설정하지 마십시오. 이 옵션 toorecursively 트래버스 파일 toobe 복사한 toohello 대상 폴더를 선택 합니다. 
    3. Hello 하지 않는 **이진 복사** 옵션입니다. 이 옵션 tooperform 소스 파일 toohello 대상 이진 복사를 선택 합니다. Hello 다음 페이지에 더 많은 옵션을 볼 수 있도록이 연습에 대 한 선택 하지 마십시오. 
    4. 해당 hello 확인 **압축 유형** 너무 설정**None**합니다. 소스 파일 지원 hello 형식 중 하나에서 압축 된 경우이 옵션에 대 한 값을 선택 합니다. 
    5. **다음**을 누릅니다.
    ![도구에 복사-hello 입력된 파일이 나 폴더를 선택 합니다.](./media/data-factory-azure-blob-connector/chose-input-file-folder.png) 
7. Hello에 **파일 형식 설정** hello 구분 기호 및 hello 파일을 구문 분석 하 여 hello 마법사에 의해 자동으로 감지 있는 hello 스키마 참조 페이지입니다. 
    1. 다음 옵션 hello 확인:는 합니다. hello **파일 형식** 너무 설정**텍스트 형식**합니다. Hello 드롭 다운 목록에서 모든 hello 지원 형식을 확인할 수 있습니다. 예: JSON, Avro, ORC, Parquet.
        b. hello **열 구분 기호** 너무 설정`Comma (,)`합니다. 나타나면 hello hello 드롭 다운 목록에서 데이터 팩터리에서 지 원하는 다른 열 구분 기호입니다. 사용자 지정 구분 기호를 지정할 수도 있습니다.
        c. hello **행 구분 기호** 너무 설정`Carriage Return + Line feed (\r\n)`합니다. 나타나면 hello hello 드롭 다운 목록에서 데이터 팩터리에서 지 원하는 다른 행 구분 기호입니다. 사용자 지정 구분 기호를 지정할 수도 있습니다.
        d. hello **줄 수를 건너뛰고** 너무 설정**0**합니다. Hello 파일의 맨 위에 hello에서 건너뛰는 몇 줄 toobe 여기 hello 번호를 입력 합니다.
        e.  hello **첫 번째 데이터 행에 열 이름이 포함** 설정 되지 않았습니다. Hello 소스 파일 hello 첫 번째 행에 열 이름이 없으면이 옵션을 선택 합니다.
        f. hello **빈 열 값을 null로 취급** 옵션을 설정 합니다.
    2. 확장 **고급 설정** toosee 고급 옵션을 사용할 수 있습니다.
    3. Hello 페이지의 hello 맨 아래에 참조 hello **미리 보기** hello emp.txt 파일의 데이터입니다.
    4. 클릭 **스키마** hello 아래쪽 toosee hello 스키마에서 유추 hello 원본 파일의 hello 데이터 확인 하 여 해당 hello 복사 마법사를 탭 합니다.
    5. 클릭 **다음** hello 구분 기호를 검토 하 고 데이터를 미리 봅니다.
    ![복사 도구 - 파일 형식 설정](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)  
8. Hello에 **대상 데이터 저장소 페이지**선택, **Azure Blob 저장소**를 클릭 하 고 **다음**합니다. 이 연습에서는 두 hello 소스 및 대상 데이터 저장소로 hello Azure Blob 저장소를 사용 하는 합니다.    
    ![복사 도구 - 대상 데이터 저장소 선택](media/data-factory-azure-blob-connector/select-destination-data-store.png)
9. **hello Azure Blob 저장소 계정을 지정** 페이지:
   1. 입력 **AzureStorageLinkedService** hello에 대 한 **연결 이름** 필드입니다.
   2. **계정 선택 방법**에 **Azure 구독에서** 옵션이 선택되었는지 확인합니다.
   3. Azure **구독**을 선택합니다.  
   4. Azure 저장소 계정을 선택합니다. 
   5. **다음**을 누릅니다.     
10. Hello에 **선택 hello 출력 파일 또는 폴더** 페이지: 
    6. **폴더 경로**를 **adfblobconnector/output/{year}/{month}/{day}**로 지정합니다. **탭**을 입력합니다.
    7. Hello에 대 한 **연도**선택, **yyyy**합니다.
    8. Hello에 대 한 **월**, 너무 설정 되어 있는지 확인**MM**합니다.
    9. Hello에 대 한 **일**, 너무 설정 되어 있는지 확인**dd**합니다.
    10. 해당 hello 확인 **압축 유형** 너무 설정**None**합니다.
    11. 해당 hello 확인 **복사 동작** 너무 설정**파일을 병합**합니다. Hello 동일한 이름이 이미 존재 하는 hello로 파일을 출력으로 hello 새 콘텐츠 경우 동일한 파일 hello 끝에 추가 된 toohello입니다.
    12. **다음**을 누릅니다.
    ![복사 도구 - 출력 파일 또는 폴더 선택](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)
11. Hello에 **파일 형식 설정** 페이지 hello 설정을 검토 하 고 클릭 **다음**합니다. Hello 추가 옵션 중 하나 tooadd 헤더 toohello 출력 파일입니다. 해당 옵션을 선택 하면 hello 열 이름을 사용 하 여 hello hello 소스 스키마에서 머리글 행이 추가 됩니다. Hello 소스에 대 한 hello 스키마를 볼 때 hello 기본 열 이름을 바꿀 수 있습니다. 예를 들어 hello 첫 번째 열 tooFirst 이름 및 두 번째 열 tooLast 이름 변경할 수 있습니다. 그런 다음 열 이름으로 이러한 이름 가진 헤더로 hello 출력 파일이 생성 됩니다. 
    ![복사 도구 - 대상의 파일 형식 설정](media/data-factory-azure-blob-connector/file-format-destination.png)
12. Hello에 **성능 설정** 페이지를 확인 하는 **단위 클라우드** 및 **복사본 병렬** 너무 설정**자동**, 고 다음을 클릭 합니다. 이러한 설정에 대한 자세한 내용은 [복사 활동 성능 및 튜닝 가이드](data-factory-copy-activity-performance.md#parallel-copy)를 참조하세요.
    ![복사 도구 - 성능 설정](media/data-factory-azure-blob-connector/copy-performance-settings.png) 
14. Hello에 **요약** 페이지 (작업 속성, 소스 및 대상에 대 한 설정 및 설정 복사) 하는 모든 설정을 검토 하 고 클릭 **다음**합니다.
    ![복사 도구 - 요약 페이지](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)
15. Hello에 대 한 정보를 검토 **요약** 페이지를 클릭 하 여 **마침**합니다. hello 마법사 (여기서 hello 복사 마법사를 실행)에서 hello data factory에 두 개의 연결 된 서비스, 두 개의 데이터 집합 (입력 및 출력) 및 하나의 파이프라인을 만듭니다.
    ![복사 도구 - 배포 페이지](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)

### <a name="monitor-hello-pipeline-copy-task"></a>모니터 hello 파이프라인 (복사 작업)

1. Hello 링크를 클릭 `Click here toomonitor copy pipeline` hello에 **배포** 페이지. 
2. Hello 표시 되어야 **모니터링 하 고 응용 프로그램 관리** 별도 탭에 있습니다.  ![앱 모니터링 및 관리](media/data-factory-azure-blob-connector/monitor-manage-app.png)
3. 변경 hello **시작** hello 위쪽에서 시간을 너무`04/19/2017` 및 **끝** 너무 시간`04/27/2017`, 클릭 하 고 **적용**합니다. 
4. Hello에 5 개 활동 창 표시 되어야 **활동 창** 목록입니다. hello **WindowStart** 번 파이프라인 시작 toopipeline 종료 시간에서 모든 날짜를 포함 해야 합니다. 
5. 클릭 **새로 고침** hello에 대 한 단추 **활동 창** 를 여러 번 표시 될 때까지 모든 hello 활동 창의 hello 상태 목록 tooReady 설정 됩니다. 
6. 이제, hello 출력 파일이 adfblobconnector 컨테이너의 hello 출력 폴더에 생성 되는 것으로 확인 합니다. Hello 출력 폴더의 폴더 구조를 다음 hello를 표시 되어야 합니다. 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
데이터 팩터리 모니터링 및 관리에 대한 자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) 문서를 참조하세요. 
 
### <a name="data-factory-entities"></a>데이터 팩터리 엔터티
이제 hello Data Factory 홈 페이지를 뒤로 toohello 탭을 전환 합니다. 현재 데이터 팩터리에는 두 개의 연결된 서비스, 두 개의 데이터 집합 및 한 개의 파이프라인이 있습니다. 

![엔터티가 있는 데이터 팩터리 홈 페이지](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

클릭 **작성자 및 배포** toolaunch 데이터 팩터리 편집기입니다. 

![데이터 팩터리 편집기](media/data-factory-azure-blob-connector/data-factory-editor.png)

Data factory에 Data Factory 엔터티에 따라 hello를 표시 되어야 합니다. 

 - 두 개의 연결된 서비스. Hello 원본과 hello 대상에 대해 다른 노드로 hello에 대 한 하나입니다. 두 연결 hello 서비스 참조 toohello이이 연습에서 동일한 Azure 저장소 계정입니다. 
 - 두 개의 데이터 집합입니다. 입력 데이터 집합 및 출력 데이터 집합. 이 연습에서는 둘 다 사용 하 여 hello 컨테이너 blob 동일 하지만 toodifferent 폴더 (입력 및 출력)를 참조 하십시오.
 - 파이프라인입니다. hello 파이프라인 blob 원본 및 Azure blob 위치 tooanother Azure blob 위치에서에서 blob 싱크 toocopy 데이터를 사용 하는 복사 작업을 포함 합니다. 

hello 다음 섹션에서는 이러한 엔터티에 대 한 자세한 정보. 

#### <a name="linked-services"></a>연결된 서비스
두 개의 연결된 서비스가 표시되어야 합니다. Hello 원본과 hello 대상에 대해 다른 노드로 hello에 대 한 하나입니다. 이 연습에서는 둘 다 정의 모양을 hello 동일 hello 이름을 제외 하 고 있습니다. hello **형식** hello 연결 된 서비스 설정 너무**AzureStorage**합니다. 연결 된 hello 서비스 정의의 가장 중요 한 속성은 hello **connectionString**, Data Factory tooconnect tooyour 런타임 시 Azure 저장소 계정에서 사용 되는 합니다. Hello 정의 hello hubName 속성을 무시 합니다. 

##### <a name="source-blob-storage-linked-service"></a>원본 Blob 저장소 연결된 서비스
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a>대상 Blob 저장소 연결된 서비스

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

Azure Storage 링크된 서비스에 대한 자세한 내용은 [연결된 서비스 속성](#linked-service-properties) 섹션을 참조하세요. 

#### <a name="datasets"></a>데이터 집합
입력 데이터 집합과 출력 데이터 집합의 두 가지 데이터 집합이 있습니다. hello 데이터 집합의 hello 형식이 너무 설정**AzureBlob** 모두에 대 한 합니다. 

입력된 데이터 집합 hello 가리키는 toohello **입력** hello의 폴더 **adfblobconnector** blob 컨테이너입니다. hello **외부** 너무 속성이**true** hello로이 데이터 집합에 대 한 데이터 생성 되지 않을 hello 파이프라인에서이 데이터 집합을 입력으로 사용 하는 hello 복사 활동을 포함 합니다. 

출력 데이터 집합 포인트 toohello hello **출력** hello의 폴더 같은 blob 컨테이너입니다. hello 출력 데이터 집합 또한 사용 하 여 hello 연도, 월 및 일의 hello **SliceStart** 시스템 변수 toodynamically hello 출력 파일에 대 한 hello 경로 평가 합니다. Data Factory에서 지원하는 함수 및 시스템 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요. hello **외부** 너무 속성이**false** (기본값)이 데이터이 집합은 hello 파이프라인에서 생성 된 때문에 있습니다. 

Azure Blob 데이터 집합이 지원하는 속성에 대한 자세한 내용은 [데이터 집합 속성](#dataset-properties) 섹션을 참조하세요.

##### <a name="input-dataset"></a>입력 데이터 집합

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a>출력 데이터 집합

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a>파이프라인
hello 파이프라인에는 하나의 활동을 있습니다. hello **형식** 활동 너무 설정의 hello**복사**합니다.  Hello 활동에 대 한 hello 형식 속성에 두 개의 섹션, 원본과 싱크에 대 한 다른 하나는 hello에 대 한 하나 있습니다. hello 원본 유형이 너무 설정 되어**BlobSource** 대로 hello 활동은 blob 저장소에서 데이터를 복사 합니다. hello 싱크 유형이 설정 되어 너무**BlobSink** hello 활동 데이터 tooa blob 저장소에 복사 합니다. hello 복사 활동 변수로 InputDataset z4y hello 입력과 OutputDataset z4y hello 출력으로 합니다. 

BlobSource 및 BlobSink에서 지원하는 속성에 대한 자세한 내용은 [복사 활동 속성](#copy-activity-properties) 섹션을 참조하세요. 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a>Blob 저장소에서 데이터 tooand 복사 하기 위한 JSON 예제  
hello 다음 예에서는 샘플 JSON 정의 사용 하 여 toocreate 파이프라인을 사용할 수 있는 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다. 보여 줍니다 어떻게 Azure Blob 저장소 및 Azure SQL 데이터베이스에서 데이터 tooand toocopy 합니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 소스 tooany 중 어디에서 든 [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a>JSON의 예: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](#linked-service-properties) 형식의 연결된 서비스
3. [AzureBlob](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)입니다.
5. [BlobSource](#copy-activity-properties) 및 [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 시계열 데이터 복사, Azure blob tooan Azure SQL 테이블에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure SQL 연결된 서비스:**

```json
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
**Azure 저장소 연결된 서비스:**

```json
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
Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다. 에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다. 자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.  

**Azure Blob 입력 데이터 집합:**

데이터는 매시간 새 blob에 선택됩니다(frequency: hour, interval: 1). hello 폴더 경로 파일 이름은 hello blob에 대 한 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. 연도, 월 및 일 부분은 hello 시작 시간의 hello 폴더 경로 사용 하 고 파일 이름을 hello 시작 시간의 시간 부분을 hello를 사용 합니다. "external": "true" 설정을 알리고 Data Factory hello 테이블 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
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
**Azure SQL 출력 데이터 집합:**

hello 예제는 Azure SQL 데이터베이스에 "MyTable" 라는 이름의 데이터 tooa 테이블에 복사 합니다. Azure SQL 데이터베이스를와 hello 테이블 만들기 hello Blob CSV 파일 toocontain 예상 대로 동일한 수의 열을 hello 합니다. 새 행 1 시간 마다 toohello 테이블을 추가 됩니다.

```json
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Blob 원본 및 SQL 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**BlobSource** 및 **싱크** 형식이 너무 설정**SqlSink**합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a>JSON의 예: Azure SQL tooAzure Blob에서에서 데이터를 복사 합니다.
다음 샘플에서는 hello:

1. [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](#linked-service-properties) 형식의 연결된 서비스
3. [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)입니다.
4. [AzureBlob](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) 및 [BlobSink](#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플에 1 시간 마다 Azure SQL 테이블 tooan Azure blob에서에서 시계열 데이터 복사합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

**Azure SQL 연결된 서비스:**

```json
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
**Azure 저장소 연결된 서비스:**

```json
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
Azure Data Factory는 두 가지 유형의 Azure Storage 연결된 서비스: **AzureStorage** 및 **AzureStorageSas**를 제공합니다. 에 대 한 hello 첫 번째 사용, hello 계정 키를 포함 하는 hello 연결 문자열을 지정 하 고 hello 공유 액세스 서명 (SAS) Uri를 지정 하면 이후 hello에 대 한 키를 누릅니다. 자세한 내용은 [연결된 서비스](#linked-service-properties) 섹션을 참조하세요.  

**Azure SQL 입력 데이터 집합:**

hello 샘플 테이블 "MyTable"에서 만든 Azure SQL 가정 시계열 데이터에 대 한 "timestampcolumn" 라는 열을 포함 합니다.

설정 "외부": "true" 알립니다 데이터 팩터리 서비스는 hello 테이블 데이터 팩터리 외부 toohello 및 hello data factory에는 활동에 의해 생성 되지 않습니다.

```json
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

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

**SQL 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**SqlSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **SqlReaderQuery** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureSQLInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
