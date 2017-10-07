---
title: "온-프레미스 HDFS에서 aaaMove 데이터 | Microsoft Docs"
description: "어떻게 toomove 데이터를 온-프레미스 Azure 데이터 팩터리를 사용 하 여 HDFS에 알아봅니다."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Azure Data Factory를 사용하여 온-프레미스 HDFS에서 데이터 이동
이 문서에서는 toouse 온-프레미스 HDFS에서 Azure Data Factory toomove 데이터에서 복사 작업을 hello 하는 방법을 설명 합니다. Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

HDFS 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. 데이터 팩터리의 현재에서 온-프레미스 HDFS tooother 데이터 저장소만 이동 데이터를 지원 하지만 다른 데이터에서 데이터 이동에 대해 저장소 tooan 온-프레미스 HDFS 합니다.

> [!NOTE]
> 복사 작업으로 복사한 toohello 대상 않아 hello 소스 파일을 삭제 하지 않습니다. 성공적인 복사 후 toodelete hello 소스 파일을 필요한 경우 사용자 지정 활동 toodelete hello 파일 만들고 hello 파이프라인에서 hello 활동을 사용 합니다. 

## <a name="enabling-connectivity"></a>연결 사용
데이터 팩터리 서비스는 hello 데이터 관리 게이트웨이 사용 하 여 연결 tooon 온-프레미스 HDFS 지원 합니다. 참조 [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 데이터 관리 게이트웨이 및 hello 게이트웨이 설정에 대 한 단계별 지침에 대 한 문서 toolearn 합니다. Azure IaaS VM에서 호스팅되는 경우에 게이트웨이 tooconnect tooHDFS hello를 사용 합니다.

> [!NOTE]
> 데이터 관리 게이트웨이에 너무 액세스할 수 있는지 hello를 확인**모든** hello [노드 서버 이름]: [노드 포트 이름을] 및 [데이터 노드 서버]: [데이터 노드 포트] hello Hadoop 클러스터의 합니다. 기본 [이름 노드 포트]는 50070이며 기본 [데이터 노드 포트]는 50075입니다.

Hello에 게이트웨이 설치할 수 있지만 동일한 온-프레미스 컴퓨터 또는 Azure VM hello HDFS hello, 별도 컴퓨터/Azure IaaS VM에 hello 게이트웨이 설치 하는 것이 좋습니다. 별도의 컴퓨터에 게이트웨이가 있으면 리소스 경합이 줄어들고 성능이 향상됩니다. 별도 컴퓨터에 hello 게이트웨이 설치할 때 hello 컴퓨터 HDFS hello 사용 하 여 수 tooaccess hello 컴퓨터 여야 합니다.

## <a name="getting-started"></a>시작
다른 도구/API를 사용하여 HDFS 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 참조 [자습서: 복사 마법사를 사용 하 여 파이프라인을 만들고](data-factory-copy-data-wizard-tutorial.md) 간략 한 설명이 hello 복사 데이터 마법사를 사용 하 여 파이프라인을 만드는 방법에 대 한 합니다.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 참조 [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 단계별 지침 toocreate 복사 작업으로 파이프라인에 대 한 합니다.

Hello 도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구/Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다.  Data Factory 된 엔터티를 HDFS에 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 [JSON의 예: 온-프레미스 HDFS tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) 이 문서의 섹션.

다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooHDFS는 JSON 속성에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다. 형식의 연결 된 서비스를 만들면 **Hdfs** toolink는 온-프레미스 HDFS tooyour 데이터 팩터리입니다. 다음 표에서 hello JSON 요소 특정 tooHDFS 연결 된 서비스에 대 한 설명을 제공 합니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |hello type 속성 설정 해야 합니다: **Hdfs** |예 |
| Url |URL toohello HDFS |예 |
| authenticationType |익명 또는 Windows입니다. <br><br> toouse **Kerberos 인증** HDFS 커넥터에 대 한 참조 너무[이 여기서](#use-kerberos-authentication-for-hdfs-connector) 온-프레미스 환경을 tooset 적절 하 게 합니다. |예 |
| userName |Windows 인증에 대한 사용자 이름. |예(Windows 인증에 대한) |
| password |Windows 인증에 대한 암호. |예(Windows 인증에 대한) |
| gatewayName |데이터 팩터리 서비스 hello hello 게이트웨이의 이름 tooconnect toohello HDFS 사용 해야 합니다. |예 |
| encryptedCredential |[새 AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) hello 액세스 자격 증명의 출력입니다. |아니요 |

### <a name="using-anonymous-authentication"></a>익명 인증 사용

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Windows 인증 사용

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>데이터 집합 속성
섹션 및 데이터 집합 정의에 사용 가능한 속성의 전체 목록을 보려면 hello [데이터 집합을 만드는](data-factory-create-datasets.md) 문서. 구조, 가용성 및 JSON 데이터 집합의 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(Azure SQL, Azure blob, Azure 테이블 등).

hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. 형식의 데이터 집합에 대 한 hello typeProperties 섹션 **FileShare** hello 다음과 같은 속성에 (HDFS 데이터 집합 포함)

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| folderPath |경로 toohello 폴더입니다. 예: `myfolder`<br/><br/>이스케이프 문자를 사용 하 여 ' \ ' hello 문자열의 특수 문자에 대 한 합니다. 예: 폴더\하위 폴더의 경우 폴더\\\\하위 폴더를 지정하고 d:\samplefolder의 경우 d:\\\\samplefolder를 지정합니다.<br/><br/>이 속성을 결합할 수 **partitionBy** toohave 폴더 경로 분할 영역에 따라 시작/종료 날짜와 시간입니다. |예 |
| fileName |Hello에 hello hello 파일 이름을 지정 **folderPath** hello 테이블 toorefer tooa 특정 파일 hello 폴더에 들어 있습니다. 이 속성에 대 한 모든 값을 지정 하지 않는 경우 hello 테이블 hello 폴더의 tooall 파일을 가리킵니다.<br/><br/>출력 데이터 집합에 대 한 파일 이름을 지정 하지 않으면,이 형식에 따라 hello에 hello 생성 된 파일의 hello 이름이 표시 됩니다. <br/><br/>Data<Guid>.txt(예: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |아니요 |
| partitionedBy |partitionedBy 사용된 toospecify 동적 folderPath 시계열 데이터에 대 한 파일 이름이 될 수 있습니다. 예를 들어 folderPath는 매시간 데이터에 대해 매개 변수화됩니다. |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [Json 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format) 및 [Parquet 형식](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션을 참조하세요. <br><br> 너무 하려는 경우**파일을 다음으로 복사-은** 간의 파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의의 hello 형식 섹션을 건너뛰십시오. |아니요 |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원되는 형식은 **GZip**, **Deflate**, **BZip2** 및 **ZipDeflate**입니다. 지원되는 수준은 **최적** 및 **가장 빠름**입니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 |

> [!NOTE]
> filename 및 fileFilter는 동시에 사용할 수 없습니다.

### <a name="using-partionedby-property"></a>partionedBy 속성 사용
동적 folderPath 및 filename 시계열 데이터에 대 한 hello로 지정할 수 hello 이전 섹션에서 설명 했 듯이 **partitionedBy** 속성 [데이터 팩터리 함수 및 시스템 변수 hello](data-factory-functions-variables.md)합니다.

시간 시계열 데이터 집합, 일정 및 분할에 대해 자세히 toolearn 참조 [데이터 집합 만들기](data-factory-create-datasets.md), [일정 예약 및 실행](data-factory-scheduling-and-execution.md), 및 [파이프라인 만들기](data-factory-create-pipelines.md) 문서입니다.

#### <a name="sample-1"></a>샘플 1:

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
이 예제에서 {Slice}는 지정 된 hello (yyyymmddhh)에서 데이터 팩터리 시스템 변수 SliceStart의 hello 값으로 대체 됩니다. hello SliceStart hello 조각의 toostart 시간을 의미합니다. hello folderPath 각 조각에 대 한 차이가 있습니다. 예를 들어 wikidatagateway/wikisampledataout/2014100103 또는 wikidatagateway/wikisampledataout/2014100104입니다.

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
이 예제에서 SliceStart의 연도, 월, 일 및 시간은 folderPath 및 fileName 속성에서 사용하는 별도 변수로 추출됩니다.

## <a name="copy-activity-properties"></a>복사 작업 속성
섹션 및 활동 정의에 사용 가능한 속성의 전체 목록을 참조 hello [파이프라인 만들기](data-factory-create-pipelines.md) 문서. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다.

반면 hello 활동의 hello typeProperties 섹션에서 사용할 수 있는 속성에 각 활동 유형에 따라 다릅니다. 복사 작업은 원본 및 싱크의 hello 형식에 따라 변경합니다.

원본 유형인 경우 복사 작업에 대 한 **FileSystemSource** 다음과 같은 속성 hello는 typeProperties 섹션에 있습니다.

**FileSystemSource** hello 다음과 같은 속성을 지원 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 데이터 읽는지 재귀적으로 hello 하위 폴더 또는 hello 지정한 폴더에서만 나타냅니다. |True, False(기본값) |아니요 |

## <a name="supported-file-and-compression-formats"></a>지원되는 파일 및 압축 형식
자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md) 문서를 참조하세요.

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>JSON의 예: 온-프레미스 HDFS tooAzure Blob에서에서 데이터 복사
이 샘플은 어떻게 온-프레미스 HDFS tooAzure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터를 복사할 수 있습니다 **직접** 명시 된 hello 싱크 tooany [여기](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Azure Data Factory에서 복사 작업 hello를 사용 하 여 합니다.  

hello 예제 Data Factory 엔터티에 따라 hello에 대 한 JSON 정의 제공 합니다. 이러한 정의 toocreate HDFS tooAzure Blob 저장소에서에서 파이프라인 toocopy 데이터를 사용 하 여 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md) 또는 [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) 또는 [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.

1. [OnPremisesHdfs](#linked-service-properties) 형식의 연결된 서비스입니다.
2. [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) 형식의 연결된 서비스
3. [FileShare](#dataset-properties) 형식의 입력 [데이터 집합](data-factory-create-datasets.md)
4. [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
5. [FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 온-프레미스 HDFS tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

첫 번째 단계로 hello 데이터 관리 게이트웨이를 설정 합니다. hello에 대 한 지침을 hello [온-프레미스 위치와 클라우드 간의 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 문서.

**연결 된 서비스 HDFS:** 이 예제를 사용 하 여 hello Windows 인증입니다. 사용할 수 있는 다른 유형의 인증은 [HDFS 연결된 서비스](#linked-service-properties) 섹션을 참조하세요.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Azure 저장소 연결된 서비스:**

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

**HDFS 입력 데이터 집합:** 이 데이터 집합 참조 toohello HDFS 폴더 DataTransfer/UnitTest/합니다. hello 파이프라인이 폴더 toohello 대상의 모든 hello 파일을 복사합니다.

설정 "외부": "true" 알리고 hello 데이터 팩터리 서비스 hello 데이터 집합의 데이터 팩터리 외부 toohello hello data factory에는 활동에 의해 생성 되지 않습니다.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Azure Blob 출력 데이터 집합:**

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 연도, 월, 일 및 시간 부분을 사용 합니다.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**파일 시스템 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업:**

복사 작업을 포함 하는 hello 파이프라인 구성된 toouse 이러한 입력 및 출력 데이터 집합은 하 고 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource** 및 **싱크** 형식이 너무 설정**BlobSink**합니다. hello에 대 한 지정 된 hello SQL 쿼리 **쿼리** 속성 시간 toocopy 지난 hello에 hello 데이터를 선택 합니다.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>HDFS 커넥터에 Kerberos 인증 사용
따라서 HDFS 커넥터에서 Kerberos 인증 toouse로 hello 온-프레미스 환경을 옵션 tooset 두 가지가 있습니다. 하나는 hello 케이스를 더 잘 맞게 선택할 수 있습니다.
* 옵션 1: [게이트웨이 컴퓨터를 Kerberos 영역에 가입](#kerberos-join-realm)
* 옵션 2: [Windows 도메인과 Kerberos 영역 사이에 상호 트러스트를 사용하도록 설정](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>옵션 1: 게이트웨이 컴퓨터를 Kerberos 영역에 가입

#### <a name="requirement"></a>요구 사항:

* hello 게이트웨이 컴퓨터 toojoin hello Kerberos 영역 하며 모든 Windows 도메인에 가입할 수 없습니다.

#### <a name="how-tooconfigure"></a>어떻게 tooconfigure:

**게이트웨이 컴퓨터에서:**

1.  Hello 실행 **Ksetup** 유틸리티 tooconfigure hello Kerberos KDC 서버 및 영역입니다.

    hello 컴퓨터 Kerberos 영역은 Windows 도메인에서 다른 작업 그룹의 구성원으로 구성 되어야 합니다. Hello Kerberos 영역을 설정 하 고 다음과 같이 KDC 서버 추가 하 여이 작업을 수행할 수 있습니다. *REALM.COM*은 고유한 각 영역으로 필요에 맞게 바꿉니다.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **다시 시작** 2 이러한 명령을 실행 한 후 hello 컴퓨터입니다.

2.  사용 하 여 hello 구성을 확인 **Ksetup** 명령입니다. hello 출력은 같은 됩니다.

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**Azure Data Factory에서:**

* 사용 하 여 hello HDFS 커넥터 구성 **Windows 인증** Kerberos 보안 주체 이름 및 암호 tooconnect toohello HDFS 데이터 소스와 함께 합니다. 구성 세부 정보에서 [HDFS 연결된 서비스 속성](#linked-service-properties)을 확인합니다.

### <a name="kerberos-mutual-trust"></a>옵션 2: Windows 도메인과 Kerberos 영역 사이에 상호 트러스트를 사용하도록 설정

#### <a name="requirement"></a>요구 사항:
*   hello 게이트웨이 컴퓨터에 Windows 도메인에 참가 해야 합니다.
*   사용 권한 tooupdate hello 도메인 컨트롤러 설정 해야합니다.

#### <a name="how-tooconfigure"></a>어떻게 tooconfigure:

> [!NOTE]
> 필요에 따라 사용자 고유의 각 영역과 도메인 컨트롤러와 자습서를 따라 hello에과 같습니다 및 AD.COM를 교체 합니다.

**KDC 서버에서:**

1.  hello KDC 구성을 편집 **krb5.conf** 파일 toolet KDC toohello 다음 구성 템플릿을 참조 하는 Windows 도메인을 신뢰 합니다. 기본적으로 hello 구성에 위치한 **/etc/krb5.conf**합니다.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **다시 시작** KDC 서비스 구성 후 hello 합니다.

2.  라는 보안 주체를 준비  **krbtgt/REALM.COM@AD.COM**  다음 명령을 hello로 KDC 서버에서:

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  **hadoop.security.auth_to_local** HDFS 서비스 구성 파일에서 `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`를 추가합니다.

**도메인 컨트롤러에서:**

1.  Hello 다음 실행 **Ksetup** tooadd 영역 항목 명령:

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Windows 도메인 tooKerberos 영역 트러스트를 설정 합니다. [암호]는 hello 주체에 대 한 hello 암호  **krbtgt/REALM.COM@AD.COM** 합니다.

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Kerberos에서 사용되는 암호화 알고리즘을 선택합니다.

    1. 이동 tooServer 관리자 > 그룹 정책 관리 > 도메인 > 그룹 정책 개체 > 기본 또는 활성 도메인 정책 및 편집 합니다.

    2. Hello에 **그룹 정책 관리 편집기** 팝업 창 이동 tooComputer 구성 > 정책 > Windows 설정 > 보안 설정 > 로컬 정책 > 보안 옵션을 구성 하 고 **네트워크 보안: Kerberos에 대해 허용 되는 암호화 유형 구성**합니다.

    3. 선택 hello 암호화 알고리즘을 toouse tooKDC를 연결 하는 경우. 일반적으로 모든 hello 옵션 선택할 수 있습니다.

        ![Kerberos의 암호화 유형 구성](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. 사용 하 여 **Ksetup** 명령 toospecify hello 암호화 알고리즘 toobe hello에 사용 되는 특정 영역입니다.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  순서 toouse Kerberos 주체 Windows 도메인의 보안 주체 hello 도메인 계정 및 Kerberos 간의 hello 매핑을 만듭니다.

    1. Hello 관리 도구를 시작 > **Active Directory 사용자 및 컴퓨터**합니다.

    2. **보기** > **고급 기능**을 클릭하여 고급 기능을 구성합니다.

    3. Hello 계정 toowhich toocreate 매핑의 tooview를 마우스 오른쪽 단추로 클릭 찾을 **이름 매핑** > 클릭 **Kerberos 이름** 탭 합니다.

    4. Hello 영역에서 사용자를 추가 합니다.

        ![보안 ID 매핑](media/data-factory-hdfs-connector/map-security-identity.png)

**게이트웨이 컴퓨터에서:**

* Hello 다음 실행 **Ksetup** tooadd 영역 항목 명령입니다.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**Azure Data Factory에서:**

* 사용 하 여 hello HDFS 커넥터 구성 **Windows 인증** 도메인 계정이 나 Kerberos 주체 tooconnect toohello HDFS 데이터 소스와 함께 합니다. 구성 세부 정보에서 [HDFS 연결된 서비스 속성](#linked-service-properties)을 확인합니다.

> [!NOTE]
> 원본 데이터 집합 toocolumns 싱크 데이터 집합에서의 열을 toomap 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.


## <a name="performance-and-tuning"></a>성능 및 튜닝
참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md) toolearn 키에 대 한 Azure 데이터 팩터리 및 다양 한 방법으로 toooptimize에서 데이터 이동 (복사 작업)의 성능에 영향을 해당 놓은 것입니다.
