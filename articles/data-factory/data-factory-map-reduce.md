---
title: "Azure 데이터 팩터리에서 MapReduce 프로그램 aaaInvoke"
description: "Azure data factory에서 Azure HDInsight에서 MapReduce 프로그램을 실행 하 여 tooprocess 데이터 클러스터링 하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c34db93f-570a-44f1-a7d6-00390f4dc0fa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 448ef93a10bd97e7ecd4be4f04f88f8a05decc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-mapreduce-programs-from-data-factory"></a>데이터 팩터리에서 MapReduce 프로그램 호출
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

Data Factory에 HDInsight MapReduce 작업 hello [파이프라인](data-factory-create-pipelines.md) 에서 MapReduce 프로그램을 실행 합니다. [직접](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형으로](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터 합니다. Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.

> [!NOTE] 
> 새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다.  

## <a name="introduction"></a>소개
Azure 데이터 팩터리의 파이프라인은 연결된 저장소 서비스의 데이터를 연결된 계산 서비스를 사용하여 처리합니다. 파이프라인에는 일련의 작업이 포함되며 각 작업에서는 특정 처리 작업을 수행합니다. 이 문서에서는 hello HDInsight MapReduce 작업을 사용 하 여 설명 합니다.

HDInsight Pig 및 Hive를 사용하여 파이프라인에서 Windows/Linux 기반 HDInsight 클러스터에 대해 Pig/Hive 스크립트를 실행하는 방법에 대한 자세한 내용은 [Pig](data-factory-pig-activity.md) 및 [Hive](data-factory-hive-activity.md) 문서를 참조하세요. 

## <a name="json-for-hdinsight-mapreduce-activity"></a>HDInsight MapReduce 작업에 대한 JSON
지 원하는 HDInsight 활동 hello에 대 한 JSON 정의 hello: 

1. 집합 hello **형식** 의 hello **활동** 너무**HDInsight**합니다.
2. Hello에 대 한 hello 클래스 이름을 지정 **className** 속성입니다.
3. 에 대 한 hello 파일 이름을 포함 하는 hello 경로 toohello JAR 파일을 지정 **jarfilepath가** 속성입니다.
4. Toohello에 대 한 hello JAR 파일이 포함 된 Azure Blob 저장소를 참조 하는 연결 된 hello 서비스 지정 **jarLinkedService** 속성입니다.   
5. Hello에 hello MapReduce 프로그램에 대 한 인수를 지정한 **인수** 섹션. 런타임 시 몇 가지 추가 인수 표시 (예: mapreduce.job.tags) hello MapReduce 프레임 워크에서. toodifferentiate hello MapReduce 인수, 인수 hello 다음 예제와 같이 인수로 옵션과 값을 사용 하십시오 (-s-입력,-등에서 출력은 바로 뒤에 해당 값으로 옵션).

    ```JSON   
    {
        "name": "MahoutMapReduceSamplePipeline",
        "properties": {
            "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calcuates an Item Similarity Matrix toodetermine hello similarity between 2 items",
            "activities": [
                {
                    "type": "HDInsightMapReduce",
                    "typeProperties": {
                        "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                        "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                        "jarLinkedService": "StorageLinkedService",
                        "arguments": [
                            "-s",
                            "SIMILARITY_LOGLIKELIHOOD",
                            "--input",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input",
                            "--output",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/",
                            "--maxSimilaritiesPerItem",
                            "500",
                            "--tempDir",
                            "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"
                        ]
                    },
                    "inputs": [
                        {
                            "name": "MahoutInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "MahoutOutput"
                        }
                    ],
                    "policy": {
                        "timeout": "01:00:00",
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "MahoutActivity",
                    "description": "Custom Map Reduce toogenerate Mahout result",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-01-03T00:00:00Z",
            "end": "2017-01-04T00:00:00Z"
        }
    }
    ```
HDInsight 클러스터에 있는 모든 MapReduce jar 파일 hello HDInsight MapReduce 작업 toorun를 사용할 수 있습니다. Hello hello HDInsight 활동은 파이프라인의 다음 샘플 JSON 정의 toorun Mahout JAR 파일을 구성 합니다.

## <a name="sample-on-github"></a>GitHub의 샘플
Hello HDInsight MapReduce 작업을 사용 하기 위한 샘플을 다운로드할 수에서: [GitHub에서 데이터 팩터리 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON/MapReduce_Activity_Sample)합니다.  

## <a name="running-hello-word-count-program"></a>Hello 단어 개수 프로그램 실행
이 예제에서 파이프라인 hello Azure HDInsight 클러스터에서 hello 단어 개수 Map/Reduce 프로그램을 실행합니다.   

### <a name="linked-services"></a>연결된 서비스
먼저, 연결 된 서비스 toolink hello hello Azure HDInsight 클러스터 toohello Azure 데이터 팩터리에서 사용 되는 Azure 저장소를 만듭니다. 경우 하면 복사/붙여넣기 코드 다음 hello tooreplace 잊지 마십시오 **계정 이름** 및 **계정 키** hello 이름 및 Azure 저장소의 키입니다. 

#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스

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
다음으로 연결 된 서비스 toolink Azure HDInsight 클러스터 toohello Azure 데이터 팩터리를 만듭니다. 하면 복사/붙여넣기 코드 다음 hello 하는 경우 대체 **HDInsight 클러스터 이름을** HDInsight 클러스터와 사용자 이름 및 암호 값 변경의 hello 이름으로 합니다.   

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
이 예제에서 hello 파이프라인 어떤 입력도 수행 하지 않습니다. HDInsight MapReduce 작업 hello에 대 한 출력 데이터 집합을 지정합니다. 이 데이터 집합은 방금 더미 필요한 toodrive hello 파이프라인 일정입니다.  

```JSON
{
    "name": "MROutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "WordCountOutput1.txt",
            "folderPath": "example/data/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="pipeline"></a>파이프라인
이 예에서 hello 파이프라인에 유형의 활동이 하나만: HDInsightMapReduce 합니다. Hello hello JSON에서에서 중요 한 속성은 다음과 같습니다. 

| 속성 | 참고 사항 |
|:--- |:--- |
| type |hello 형식이 너무 설정 되어 있어야**HDInsightMapReduce**합니다. |
| className |Hello 클래스의 이름은: **단어 수** |
| jarFilePath  |Hello 클래스를 포함 경로 toohello jar 파일입니다. 경우 하면 복사/붙여넣기 코드 다음 hello hello 클러스터의 toochange hello 이름을 잊지 마십시오. |
| jarLinkedService |Hello jar 파일이 포함 된 azure 저장소 연결 된 서비스입니다. 이 연결 된 서비스는 hello HDInsight 클러스터와 연결 된 toohello 저장소를 참조 합니다. |
| arguments |hello wordcount 프로그램에는 두 개의 인수, 입력 및 출력 확보합니다. hello 입력된 파일은 hello davinci.txt 파일입니다. |
| frequency/interval |이러한 속성에 대 한 hello 값 hello 출력 데이터 집합을 일치합니다. |
| linkedServiceName |이전에 만든 했습니다 toohello HDInsight 연결 된 서비스를 참조 합니다. |

```JSON
{
    "name": "MRSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun hello Word Count Program",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "wordcount",
                    "jarFilePath": "<HDInsight cluster name>/example/jars/hadoop-examples.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": [
                        "/example/data/gutenberg/davinci.txt",
                        "/example/data/WordCountOutput1"
                    ]
                },
                "outputs": [
                    {
                        "name": "MROutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "MRActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-03T00:00:00Z",
        "end": "2014-01-04T00:00:00Z"
    }
}
```

## <a name="run-spark-programs"></a>Spark 프로그램 실행
MapReduce 작업 toorun Spark 프로그램 HDInsight Spark 클러스터에서 사용할 수 있습니다. 자세한 내용은 [Azure Data Factory에서 Spark 프로그램 호출](data-factory-spark.md) 을 참조하세요.  

[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456


[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[adfgetstartedmonitoring]:data-factory-copy-data-from-azure-blob-storage-to-sql-database.md#monitor-pipelines 

[Developer Reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[Azure Portal]: http://portal.azure.com

## <a name="see-also"></a>참고 항목
* [Hive 작업](data-factory-hive-activity.md)
* [Pig 작업](data-factory-pig-activity.md)
* [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
* [Spark 프로그램 호출](data-factory-spark.md)
* [R 스크립트 호출](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

