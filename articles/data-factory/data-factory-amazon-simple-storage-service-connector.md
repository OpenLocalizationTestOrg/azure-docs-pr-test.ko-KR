---
title: "데이터 팩터리를 사용 하 여 Amazon 간단한 저장소 서비스에서 데이터를 aaaMove | Microsoft Docs"
description: "방법에 대 한 자세한 내용은 Azure 데이터 팩터리를 사용 하 여 toomove 데이터로 Amazon 간단한 저장소 서비스 (S3)."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Azure Data Factory를 사용하여 Amazon 단순 저장소 서비스에서 데이터 이동
이 문서에서는 어떻게 toouse hello 활동의 Azure Data Factory toomove 데이터에서에서 복사 Amazon 간단한 저장소 서비스 (S3). Hello에 기반 [데이터 이동 작업](data-factory-data-movement-activities.md) hello 복사 작업으로 데이터 이동에 대 한 일반적인 개요를 제공 하는 문서입니다.

Amazon S3 지원 tooany 싱크 데이터 저장소에서 데이터를 복사할 수 있습니다. 데이터 목록에 대 한 지원 저장소 hello 복사 작업에서 싱크 참조 hello [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 테이블입니다. data Factory에는 현재만 Amazon S3 tooother 데이터 저장소에서 데이터를 이동 지원 하지만 tooAmazon S3 저장 다른 데이터에서 데이터를 이동 하지 않습니다.

## <a name="required-permissions"></a>필요한 사용 권한
Amazon s 3에서 toocopy 데이터 hello 다음 권한을 부여 받은 있는지 확인 합니다.

* Amazon S3 개체 작업에 대한 `s3:GetObject` 및 `s3:GetObjectVersion`.
* Amazon S3 버킷 작업에 대한 `s3:ListBucket`. Hello 데이터 팩터리 복사 마법사를 사용 하는 경우 `s3:ListAllMyBuckets` 은 필요 합니다.

Amazon S3 사용 권한의 전체 목록 hello에 대 한 세부 정보를 참조 하십시오. [정책에서 사용 권한 지정](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html)합니다.

## <a name="getting-started"></a>시작
다른 도구 또는 API를 사용하여 Amazon S3 원본의 데이터를 이동하는 복사 작업으로 파이프라인을 만들 수 있습니다.

hello 가장 쉬운 방법은 toocreate 파이프라인은 toouse hello **복사 마법사**합니다. 빠른 연습을 위해서는 [자습서: 복사 마법사를 사용하여 파이프라인 만들기](data-factory-copy-data-wizard-tutorial.md)를 참조하세요.

다음 도구 toocreate 파이프라인 hello을 사용할 수 있습니다: **Azure 포털**, **Visual Studio**, **Azure PowerShell**, **Azure 리소스 관리자 템플릿** , **.NET API**, 및 **REST API**합니다. 단계별 지침은 toocreate 복사 작업으로 파이프라인에 대 한 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.

도구 또는 Api를 사용 하는지 여부를 hello tooa 싱크 데이터 저장소를 저장 하는 원본 데이터에서 데이터를 이동 하는 파이프라인 단계 toocreate 다음을 수행 합니다.

1. 만들 **연결 된 서비스** toolink 입력 및 출력 데이터 저장소 tooyour 데이터 팩터리입니다.
2. 만들 **데이터 집합** 입력 및 출력 toorepresent hello에 대 한 데이터 복사 작업을 합니다.
3. 입력으로 데이터 집합을, 출력으로 데이터 집합을 사용하는 복사 작업을 통해 **파이프라인**을 만듭니다.

Hello 마법사를 사용 하 여 이러한 데이터 팩터리 엔터티 (연결 된 서비스, 데이터 집합 및 hello 파이프라인)에 대 한 JSON 정의를 자동으로 만들어집니다. 도구 또는 Api (제외.NET API)를 사용 하면 hello JSON 형식을 사용 하 여이 Data Factory 엔터티를 정의 합니다. Data Factory 된 엔터티를 Amazon S3 데이터 저장소에서 사용 되는 toocopy 데이터에 대 한 JSON 정의 된 샘플을 보려면 hello [JSON의 예: Amazon S3 tooAzure Blob에서에서 데이터를 복사](#json-example-copy-data-from-amazon-s3-to-azure-blob) 이 문서의 섹션.

> [!NOTE]
> 복사 작업에 대해 지원되는 파일 및 압축 형식에 대한 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md)을 참조하세요.

다음 섹션 hello 사용 되는 toodefine Data Factory 엔터티에 특정 tooAmazon S3는 JSON 속성에 대 한 세부 정보를 제공 합니다.

## <a name="linked-service-properties"></a>연결된 서비스 속성
연결 된 서비스는 데이터 저장소 tooa 데이터 팩터리를 연결합니다. 형식의 연결 된 서비스를 만들면 **AwsAccessKey** toolink Amazon S3 데이터 tooyour 데이터 팩터리를 저장 합니다. 다음 표에서 hello에 대 한 설명 JSON 요소 특정 tooAmazon S3 (AwsAccessKey) 연결 된 서비스를 제공 합니다.

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| accessKeyID |Hello 비밀 선택 키의 ID입니다. |string |예 |
| secretAccessKey |자체 hello 비밀 선택 키입니다. |암호화된 비밀 문자열 |예 |

다음은 예제입니다.

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>데이터 집합 속성
데이터 집합 toorepresent toospecify 입력 데이터 집합 hello type 속성 hello 데이터 집합의 Azure Blob 저장소에 너무**AmazonS3**합니다. 집합 hello **linkedServiceName** hello Amazon S3의 hello dataset toohello 이름의 속성이 연결 된 서비스입니다. 데이터 집합 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [데이터 집합 만들기](data-factory-create-datasets.md)를 참조하세요. 

구조, 가용성 및 정책과 같은 섹션이 모든 데이터 집합 형식에 대해 유사합니다(예: SQL Database, Azure Blob, Azure 테이블). hello **typeProperties** 데이터 집합의 각 형식에 대 한 다른 섹션과 hello 데이터 저장소에 hello 데이터의 hello 위치에 대 한 정보를 제공 합니다. hello **typeProperties** 형식의 데이터 집합에 대 한 섹션 **AmazonS3** hello 다음과 같은 속성에 (Amazon S3 hello 데이터 집합 포함):

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| bucketName |hello S3 버킷 이름입니다. |문자열 |예 |
| key |S3 hello 개체 키입니다. |문자열 |아니요 |
| 접두사 |Hello S3 개체 키에 대 한 접두사입니다. 이 접두사로 시작하는 키를 가진 개체가 선택됩니다. 키가 비어 있을 때에만 적용됩니다. |string |아니요 |
| 버전 |S3 버전 관리를 사용 하는 경우 hello S3 개체의 hello 버전입니다. |문자열 |아니요 |
| format | hello 형식 유형만 지원 됩니다: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**합니다. 집합 hello **형식** 이러한 값의 형식 tooone 아래의 속성입니다. 자세한 내용은 참조 hello [텍스트 형식](data-factory-supported-file-and-compression-formats.md#text-format), [JSON 형식](data-factory-supported-file-and-compression-formats.md#json-format), [Avro 형식](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc 형식](data-factory-supported-file-and-compression-formats.md#orc-format), 및 [Parquet 형식 ](data-factory-supported-file-and-compression-formats.md#parquet-format) 섹션. <br><br> 으로 toocopy 파일-파일 기반 저장소 (이진 복사), 두 입력 및 출력 데이터 집합 정의에서 skip hello 형식 섹션 사이입니다. |아니요 | |
| 압축 | Hello 유형 및 hello 데이터에 대 한 압축 수준을 지정 합니다. 지원 되는 hello 유형은: **GZip**, **Deflate**, **BZip2**, 및 **ZipDeflate**합니다. 지원 되는 hello 수준은: **최적** 및 **fastest 이면**합니다. 자세한 내용은 [Azure Data Factory의 파일 및 압축 형식](data-factory-supported-file-and-compression-formats.md#compression-support)을 참조하세요. |아니요 | |


> [!NOTE]
> **bucketName + 키** hello S3 개체, 여기서 버킷에 S3 개체에 대 한 hello 루트 컨테이너 하 고 키가 hello 전체 경로 toohello S3 개체의 hello 위치를 지정 합니다.

### <a name="sample-dataset-with-prefix"></a>접두사를 사용한 샘플 데이터 집합

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>샘플 데이터 집합(버전 포함)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>S3에 대한 동적 경로
hello 위의 샘플에서는 고정된 값 hello에 대 한 **키** 및 **bucketName** hello Amazon S3 데이터 집합의 속성입니다.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

SliceStart와 같은 시스템 변수를 사용하여 Data Factory가 런타임에 동적으로 이러한 속성을 계산하게 할 수 있습니다.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

작업을 수행할 수 동일 hello에 대 한 hello **접두사** Amazon S3 데이터 집합의 속성입니다. 지원되는 함수 및 변수 목록은 [Data Factory 함수 및 시스템 변수](data-factory-functions-variables.md)를 참조하세요.

## <a name="copy-activity-properties"></a>복사 작업 속성
작업 정의에 사용할 수 있는 섹션 및 속성의 전체 목록은 [파이프라인 만들기](data-factory-create-pipelines.md)를 참조하세요. 이름, 설명, 입력/출력 테이블, 정책 등의 속성은 모든 형식의 활동에 사용할 수 있습니다. Hello에 사용할 수 있는 속성 **typeProperties** hello 활동의 섹션에 각 활동 유형에 따라 다릅니다. Hello 복사 작업에 대 한 속성의 원본 및 싱크 hello 유형에 따라 달라 집니다. Hello 복사 작업의 원본 유형의 경우 **FileSystemSource** (Amazon S3 포함), hello 다음 속성은 영어로 **typeProperties** 섹션:

| 속성 | 설명 | 허용되는 값 | 필수 |
| --- | --- | --- | --- |
| recursive |Hello 디렉터리 개체 toorecursively 목록 S3 여부를 지정 합니다. |True/False |아니요 |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>JSON의 예: Amazon S3 tooAzure Blob 저장소에서에서 데이터 복사
이 샘플은 어떻게 Amazon S3 tooan Azure Blob 저장소에서에서 toocopy 데이터입니다. 그러나 데이터 복사할 수 직접 너무[지원 되는 hello 싱크 중](data-factory-data-movement-activities.md#supported-data-stores-and-formats) Data Factory에 hello 복사 작업을 사용 하 여 합니다.

hello 예제 Data Factory 엔터티에 따라 hello에 대 한 JSON 정의 제공 합니다. 이러한 정의 toocreate Amazon S3 tooBlob 저장소에서 파이프라인 toocopy 데이터를 사용 하 여 hello를 사용 하 여 [Azure 포털](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), 또는 [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)합니다.   

* [AwsAccessKey](#linked-service-properties)형식의 연결된 서비스.
* [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)형식의 연결된 서비스
* [AmazonS3](#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties) 형식의 출력 [데이터 집합](data-factory-create-datasets.md)
* [FileSystemSource](#copy-activity-properties) 및 [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)를 사용하는 복사 작업의 [파이프라인](data-factory-create-pipelines.md)입니다.

hello 샘플 데이터 복사 Amazon S3 tooan Azure blob에서에서 1 시간 마다 합니다. 이 예제에 사용 되는 hello JSON 속성 hello 샘플 다음 섹션에 설명 되어 있습니다.

### <a name="amazon-s3-linked-service"></a>Amazon S3 연결된 서비스

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스

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

### <a name="amazon-s3-input-dataset"></a>Amazon S3 입력 데이터 집합

설정 **"외부": true** 해당 hello 데이터 집합은 외부 toohello 데이터 팩터리 hello 데이터 팩터리 서비스에 알립니다. 이 속성 tootrue 하지 hello 파이프라인의 활동에 의해 생성 되는 입력된 데이터 집합에 설정 합니다.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합

데이터가 새 blob tooa 1 시간 마다 기록 됩니다 (빈도: 시, 간격: 1). hello blob에 대 한 hello 폴더 경로 처리 중인 hello 조각의 hello 시작 시간에 따라 동적으로 평가 됩니다. hello 폴더 경로 hello 시작 시간의 hello 연도, 월, 일 및 시간 부분을 사용 합니다.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Amazon S3 원본 및 Blob 싱크를 사용하는 파이프라인의 복사 작업

hello 파이프라인에 포함 된 구성된 toouse 않은 복사 작업 입력 및 출력 데이터 집합을 hello 및 예약 된 toorun 1 시간입니다. Hello 파이프라인 JSON 정의에서 hello **소스** 형식이 너무 설정**FileSystemSource**, 및 **싱크** 형식이 너무 설정**BlobSink**합니다.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> 싱크 데이터 집합에서 원본 데이터 집합 toocolumns toomap 열 참조 [Azure Data Factory에서 데이터 집합 열에 매핑](data-factory-map-columns.md)합니다.


## <a name="next-steps"></a>다음 단계
Hello 다음 문서를 참조 하십시오.

* 키에 대 한 toolearn Data Factory에서 데이터 이동을 (복사 작업) 및 다양 한 방법으로 toooptimize의 성능에 영향을 해당 요소를 hello 참조 [복사 활동 성능 및 조정 가이드](data-factory-copy-activity-performance.md)합니다.

* 복사 작업을 사용 하 여 파이프라인 만들기에 대 한 단계별 지침은 참조 hello [복사 활동 자습서](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
