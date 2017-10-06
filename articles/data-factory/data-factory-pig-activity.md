---
title: "Azure 데이터 팩터리에서 Pig 작업을 사용 하 여 aaaTransform 데이터 | Microsoft Docs"
description: "에-필요 시/사용자 고유의 HDInsight 클러스터에서 Pig 작업은 Azure 데이터 팩터리 toorun Pig 스크립트에 hello를 사용 하는 방법을 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 5af07a1a-2087-455e-a67b-a79841b4ada5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 3ad096c4a9e8603b09f574f6d129b4339a75d381
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-using-pig-activity-in-azure-data-factory"></a>Azure Data Factory에서 Pig 활동을 사용하여 데이터 변환
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

Data Factory에 HDInsight Pig 작업 hello [파이프라인](data-factory-create-pipelines.md) 에서 Pig 쿼리를 실행 [고유한](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 또는 [주문형](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) Windows/Linux 기반 HDInsight 클러스터 합니다. Hello를 기반으로 한이 문서 [데이터 변환 작업](data-factory-data-transformation-activities.md) 데이터 변환 및 지원 hello 변환 작업에 대 한 일반적인 개요를 제공 하는 문서입니다.

> [!NOTE] 
> 새 tooAzure 데이터 팩터리 인 경우 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 자습서 hello 수행 하 고: [첫 번째 데이터 파이프라인을 빌드](data-factory-build-your-first-pipeline.md) 이 문서를 읽기 전에 합니다. 

## <a name="syntax"></a>구문

```JSON
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```
## <a name="syntax-details"></a>구문 세부 정보
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| name |Hello 활동의 이름 |예 |
| 설명 |어떤 hello 활동을 설명 하는 텍스트에 사용 됩니다. |아니요 |
| type |HDinsightPig |예 |
| inputs |하나 이상의 입력 사용한 hello Pig 작업 |아니요 |
| outputs |Pig 작업 hello에서 하나 이상의 출력 생성 |예 |
| linkedServiceName |Data Factory에 연결 된 서비스로 등록 toohello HDInsight 클러스터를 참조 합니다. |예 |
| script |Hello Pig 스크립트를 인라인으로 지정 |아니요 |
| script path |Azure blob 저장소에 hello Pig 스크립트를 저장 하 고 hello toohello 파일 경로 제공 합니다. 'script' 또는 'scriptPath' 속성을 사용합니다. 둘 모두를 사용할 수는 없습니다. hello 파일 이름은 대/소문자 구분입니다. |아니요 |
| defines |키/값 쌍으로 hello Pig 스크립트 내에서 참조 하는 것에 대 한 매개 변수를 지정 |아니요 |

## <a name="example"></a>예제
살펴보겠습니다 게임의 예가 기록 하려는 회사에서 시작 하는 게임을 즐기고 플레이어에서 사용한 tooidentify hello 시간 분석 합니다.

다음 샘플 게임 로그 hello 쉼표 (,) 구분 된 파일입니다. 다음 필드 – 프로필 Id, SessionStart, 기간, SrcIPAddress, 및 게임 종류 hello를 포함 합니다.

```
1809,2014-05-04 12:04:25.3470000,14,221.117.223.75,CaptureFlag
1703,2014-05-04 06:05:06.0090000,16,12.49.178.247,KingHill
1703,2014-05-04 10:21:57.3290000,10,199.118.18.179,CaptureFlag
1809,2014-05-04 05:24:22.2100000,23,192.84.66.141,KingHill
.....
```

hello **Pig 스크립트** tooprocess이이 데이터:

```
PigSampleIn = LOAD 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/samplein/' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);

GroupProfile = Group PigSampleIn all;

PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);

Store PigSampleOut into 'wasb://adfwalkthrough@anandsub14.blob.core.windows.net/sampleoutpig/' USING PigStorage (',');
```

데이터 팩터리 파이프라인에서이 Pig 스크립트 tooexecute 단계 hello지 않습니다.

1. 연결 된 서비스 tooregister 만들기 [고유한 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 구성 또는 [주문형 HDInsight 계산 클러스터](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)합니다. 이 연결된 서비스를 **HDInsightLinkedService**라고 하겠습니다.
2. 만들기는 [연결 된 서비스](data-factory-azure-blob-connector.md) tooconfigure hello 연결 tooAzure Blob 저장소 hello 데이터를 호스트 합니다. 이 연결된 서비스를 **StorageLinkedService**라고 하겠습니다.
3. 만들 [데이터 집합](data-factory-create-datasets.md) toohello 입력과 hello를 가리키는 데이터를 출력 합니다. 입력된 데이터 집합 hello 부르겠습니다 **PigSampleIn** hello 출력 데이터 집합 및 **PigSampleOut**합니다.
4. Hello Pig 쿼리 파일 hello 2 단계에서 구성 된 Azure Blob 저장소에에서 복사 합니다. Hello hello 데이터를 호스팅하는 Azure 저장소 hello 쿼리 파일을 호스팅하는 하나 hello와에서 다른 경우에 별도 Azure 저장소 연결 서비스를 만듭니다. Hello 작업 구성에서 toohello 연결 된 서비스를 참조 하십시오. 사용 하 여 * * scriptPath * * toospecify hello toopig 스크립트 파일 경로 및 **scriptLinkedService**합니다. 
   
   > [!NOTE]
   > Hello를 사용 하 여 hello Pig 스크립트를 인라인으로 hello 활동 정의에서 제공할 수도 있습니다 **스크립트** 속성입니다. 그러나 권장 하지는 않습니다이 방법으로 hello 스크립트에 모든 특수 문자 이스케이프 toobe 하며 디버깅 문제가 발생할 수 있습니다. hello 최상의 방법 #4 toofollow 단계입니다.
   > 
   > 
5. Hello HDInsightPig 활동으로 hello 파이프라인을 만듭니다. 이 작업은 HDInsight 클러스터에서 Pig 스크립트를 실행 하 여 hello 입력된 데이터를 처리 합니다.

    ```JSON   
    {
      "name": "PigActivitySamplePipeline",
      "properties": {
        "activities": [
          {
            "name": "PigActivitySample",
            "type": "HDInsightPig",
            "inputs": [
              {
                "name": "PigSampleIn"
              }
            ],
            "outputs": [
              {
                "name": "PigSampleOut"
              }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
              "scriptPath": "adfwalkthrough\\scripts\\enrichlogs.pig",
              "scriptLinkedService": "StorageLinkedService"
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
        ]
      }
    } 
    ```
6. Hello 파이프라인을 배포 합니다. 자세한 내용은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요. 
7. Hello 데이터 팩터리 모니터링을 사용 하 여 hello 파이프라인 및 관리 뷰를 모니터링 합니다. 자세한 내용은 [데이터 팩터리 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하세요.

## <a name="specifying-parameters-for-a-pig-script"></a>Pig 스크립트에 대한 매개 변수 지정
다음 예제는 hello 고려: 게임 로그는 Azure Blob 저장소에 매일 수집 된 및 분할된에 따라 날짜 및 시간 폴더에 저장 합니다. Tooparameterize hello Pig 스크립트 및 런타임 시 hello 입력된 폴더 위치를 동적으로 전달할 한도 날짜 및 시간을 사용 하 여 분할 하는 hello 출력을 생성 합니다.

toouse Pig 스크립트를 매개 변수화를 수행 하는 hello를 실행 합니다.

* Hello 매개 변수에서 정의 **정의**합니다.

    ```JSON  
    {
        "name": "PigActivitySamplePipeline",
          "properties": {
        "activities": [
            {
                "name": "PigActivitySample",
                "type": "HDInsightPig",
                "inputs": [
                      {
                        "name": "PigSampleIn"
                      }
                ],
                "outputs": [
                      {
                        "name": "PigSampleOut"
                      }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "typeproperties": {
                      "scriptPath": "adfwalkthrough\\scripts\\samplepig.hql",
                      "scriptLinkedService": "StorageLinkedService",
                      "defines": {
                        "Input": "$$Text.Format('wasb: //adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0: yyyy}/monthno={0:MM}/dayno={0: dd}/',SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                      }
                },
                   "scheduler": {
                      "frequency": "Day",
                      "interval": 1
                }
              }
        ]
      }
    }
    ```  
* Pig 스크립트 hello toohello 매개 변수를 사용 하 여 참조 하는 '**$parameterName**' hello 다음 예제와 같이:

    ```  
    PigSampleIn = LOAD '$Input' USING PigStorage(',') AS (ProfileID:chararray, SessionStart:chararray, Duration:int, SrcIPAddress:chararray, GameType:chararray);    
    GroupProfile = Group PigSampleIn all;        
    PigSampleOut = Foreach GroupProfile Generate PigSampleIn.ProfileID, SUM(PigSampleIn.Duration);        
    Store PigSampleOut into '$Output' USING PigStorage (','); 
    ```
## <a name="see-also"></a>참고 항목
* [Hive 작업](data-factory-hive-activity.md)
* [MapReduce 작업](data-factory-map-reduce.md)
* [Hadoop 스트리밍 작업](data-factory-hadoop-streaming-activity.md)
* [Spark 프로그램 호출](data-factory-spark.md)
* [R 스크립트 호출](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)

