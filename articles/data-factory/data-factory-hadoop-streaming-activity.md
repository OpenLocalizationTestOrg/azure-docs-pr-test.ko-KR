---
title: "Hadoop 스트리밍 작업-Azure를 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "에-필요 시/사용자 고유의 HDInsight 클러스터에서 Hadoop 스트리밍 프로그램을 실행 하 여 Azure 데이터 팩터리 tootransform 데이터에서 Hadoop 스트리밍 작업 hello를 사용 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4c3ff8f2-2c00-434e-a416-06dfca2c41ec
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: a7ddb7268f47162709a9c8136ccd69e0b7d4ad7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-hadoop-streaming-activity-in-azure-data-factory"></a>Azure Data Factory에서 Hadoop 스트리밍 작업을 사용하여 데이터 변환
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive 작업](data-factory-hive-activity.md) 
> * [Pig 작업](data-factory-pig-activity.md)
> * [MapReduce 작업](data-factory-map-reduce.md)
> * [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
> * [Spark 작업](data-factory-spark.md)
> * [Machine Learning Batch 실행 작업](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning 업데이트 리소스 작업](data-factory-azure-ml-update-resource-activity.md)
> * [저장 프로시저 작업](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL 작업](data-factory-usql-activity.md)
> * [.NET 사용자 지정 작업](data-factory-use-custom-activities.md)

사용할 수 있습니다 HDInsightStreamingActivity 활동 hello Azure 데이터 팩터리 파이프라인에서 Hadoop 스트리밍 작업을 호출 합니다. hello 다음 JSON 코드 조각은 구문을 보여 줍니다 hello HDInsightStreamingActivity hello를 사용 하 여 파이프라인 JSON 파일. 

Data Factory에 HDInsight 스트리밍 활동 hello [파이프라인](data-factory-create-pipelines.md) 에서 Hadoop 스트리밍 프로그램을 실행 합니다. [고유한](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터입니다. Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.

> [!NOTE] 
> 새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다. 

## <a name="json-sample"></a>JSON 샘플
hello HDInsight 클러스터 (wc.exe 및 cat.exe) 예제 프로그램 및 데이터 (davinci.txt)으로 자동으로 채워집니다. 기본적으로 hello HDInsight 클러스터에서 사용 되는 hello 컨테이너의 이름에는 hello 클러스터 자체의 hello 이름이입니다. 예를 들어 클러스터 이름이 myhdicluster 이면 연결 된 hello blob 컨테이너의 이름을 myhdicluster 것입니다. 

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<nameofthecluster>/example/apps/wc.exe",
                        "<nameofthecluster>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "AzureStorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00Z",
        "end": "2014-01-05T00:00:00Z"
    }
}
```

포인트 다음 참고 hello:

1. 집합 hello **linkedServiceName** 연결 된 서비스는 hello 스트리밍 mapreduce 작업 실행 tooyour HDInsight 클러스터를 가리키는의 hello toohello 이름입니다.
2. 너무 hello 유형의 hello 활동 설정**HDInsightStreaming**합니다.
3. Hello에 대 한 **매퍼** 속성을 hello 매퍼 실행 파일 이름을 지정 합니다. Hello 예제 cat.exe는 hello 매퍼 실행 파일입니다.
4. Hello에 대 한 **리 듀 서** 속성 리 듀 서 실행 파일의 hello 이름을 지정 합니다. Hello 예제 wc.exe는 hello 리 듀 서 실행 합니다.
5. Hello에 대 한 **입력** type 속성을 hello 맵 편집기에 대 한 hello 입력된 파일 (hello 위치)를 지정 합니다. Hello 예에서: "wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt": adfsample이 blob 컨테이너 hello, 예제/data/Gutenberg hello 폴더 이며 davinci.txt가 blob hello 합니다.
6. Hello에 대 한 **출력** type 속성을 hello 리 듀 서에 대 한 hello 출력 파일 (hello 위치 포함)를 지정 합니다. hello Hadoop 스트리밍 작업의 hello 출력은이 속성에 지정 된 toohello 위치를 기록 합니다.
7. Hello에 **filePaths** 섹션에서 hello 매퍼 및 리 듀 서 실행 파일에 대 한 hello 경로 지정 합니다. Hello 예에서: "adfsample/example/apps/wc.exe" adfsample이 blob 컨테이너 hello, example/apps가 hello 폴더 및 wc.exe는 hello를 실행 합니다.
8. Hello에 대 한 **fileLinkedService** 속성을 hello Azure 저장소 연결 된 서비스를 나타내는 hello hello filePaths 섹션에 지정 된 hello 파일이 포함 된 Azure 저장소를 지정 합니다.
9. Hello에 대 한 **인수** 속성을 hello 스트리밍 작업에 대 한 hello 인수를 지정 합니다.
10. hello **getDebugInfo** 속성은 선택적 요소입니다. TooFailure, 설정 되 면 hello 로그 오류에 대해서만 다운로드 됩니다. TooAlways, 설정 되어 있는 경우 로그 hello 실행 상태에 관계 없이 항상 다운로드 됩니다.

> [!NOTE]
> Hello에 대 한 hello Hadoop 스트리밍 작업에 대 한 출력 데이터 집합 지정 hello 예제 에서처럼 **출력** 속성입니다. 이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다. 않아도 toospecify 모든 입력된 데이터 집합 hello에 대 한 hello 활동에 대 한 **입력** 속성입니다.  
> 
> 

## <a name="example"></a>예제
Azure HDInsight 클러스터에서 hello 단어 개수 스트리밍 Map/Reduce 프로그램을 실행 하는이 연습에서 hello 파이프라인. 

### <a name="linked-services"></a>연결된 서비스
#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
먼저, 연결 된 서비스 toolink hello hello Azure HDInsight 클러스터 toohello Azure 데이터 팩터리에서 사용 되는 Azure 저장소를 만듭니다. 경우 하면 복사/붙여넣기 코드 다음 hello 잊지 마십시오 hello 이름의 tooreplace 계정 이름 및 계정 키 및 Azure 저장소의 키입니다. 

```JSON
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>"
        }
    }
}
```

#### <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스
다음으로 연결 된 서비스 toolink Azure HDInsight 클러스터 toohello Azure 데이터 팩터리를 만듭니다. 경우 하면 복사/붙여넣기 코드 다음 hello HDInsight 클러스터의 hello 이름의 HDInsight 클러스터 이름을 바꾼 사용자 이름 및 암호 값을 변경 합니다. 

```JSON
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": "https://<HDInsight cluster name>.azurehdinsight.net",
            "userName": "admin",
            "password": "**********",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

### <a name="datasets"></a>데이터 집합
#### <a name="output-dataset"></a>출력 데이터 집합
이 예제에서 hello 파이프라인 어떤 입력도 수행 하지 않습니다. Hello HDInsight 스트리밍 활동에 대 한 출력 데이터 집합을 지정합니다. 이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다. 

```JSON
{
    "name": "StreamingOutputDataset",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "adftutorial/streamingdata/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>파이프라인
이 예에서 hello 파이프라인에 유형의 활동이 하나만: **HDInsightStreaming**합니다. 

hello HDInsight 클러스터 (wc.exe 및 cat.exe) 예제 프로그램 및 데이터 (davinci.txt)으로 자동으로 채워집니다. 기본적으로 hello HDInsight 클러스터에서 사용 되는 hello 컨테이너의 이름에는 hello 클러스터 자체의 hello 이름이입니다. 예를 들어 클러스터 이름이 myhdicluster 이면 연결 된 hello blob 컨테이너의 이름을 myhdicluster 것입니다.  

```JSON
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<blobcontainer>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": [
                        "<blobcontainer>/example/apps/wc.exe",
                        "<blobcontainer>/example/apps/cat.exe"
                    ],
                    "fileLinkedService": "StorageLinkedService"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00Z",
        "end": "2017-01-04T00:00:00Z"
    }
}
```
## <a name="see-also"></a>참고 항목
* [Hive 작업](data-factory-hive-activity.md)
* [Pig 작업](data-factory-pig-activity.md)
* [MapReduce 작업](data-factory-map-reduce.md)
* [Spark 프로그램 호출](data-factory-spark.md)
* [R 스크립트 호출](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

