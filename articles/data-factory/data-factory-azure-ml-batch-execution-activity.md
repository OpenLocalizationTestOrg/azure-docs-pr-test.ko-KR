---
title: "Azure 데이터 팩터리를 사용 하 여 aaaCreate 예측 데이터 파이프라인 | Microsoft Docs"
description: "Toocreate Azure 데이터 팩터리 및 Azure 기계 학습을 사용 하 여 예측 파이프라인을 생성 하는 방법을 설명 합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Azure Machine Learning 및 Azure Data Factory를 사용하여 예측 파이프라인 만들기

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

## <a name="introduction"></a>소개

### <a name="azure-machine-learning"></a>Azure 기계 학습
[Azure 기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/) toobuild, 테스트 및 예측 분석 솔루션을 배포할 수 있습니다. 대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.

1. **학습 실험 만들기**. Hello Azure 기계 학습 스튜디오를 사용 하 여이 단계를 수행 합니다. hello 기계 학습 스튜디오는 tootrain를 사용 하 여 학습 데이터를 사용 하 여 예측 분석 모델을 테스트 하는 시각적 공동 개발 환경입니다.
2. **Tooa 예측 실험으로 변환**합니다. 기존 데이터와 모델의 학습 및 준비 toouse 되 면 그 tooscore 새 데이터를 준비 하 고 점수 매기기 실험을 간소화 합니다.
3. **웹 서비스로 배포**. 점수 매기기 실험을 Azure 웹 서비스로 게시할 수 있습니다. 이 웹 서비스 끝점을 통해 데이터 tooyour 모델을 보내고 결과 예측을 hello 모델에서 받을 수 있습니다.  

### <a name="azure-data-factory"></a>Azure 데이터 팩터리
데이터 팩터리는 오케스트레이션 하 고 hello를 자동화 하는 클라우드 기반 데이터 통합 서비스 **이동** 및 **변환** 데이터입니다. 데이터 통합 솔루션 Azure 데이터 팩터리를 사용 하 고 수 있는 다양 한 데이터 저장소에서 데이터를 수집, hello 데이터 변환/프로세스가 hello 결과 데이터 toohello 데이터 저장소에 게시를 만들 수 있습니다.

데이터 팩터리 서비스 이동 하 고 데이터를 변환 하는 toocreate 데이터 파이프라인을 허용 하 고 (시간별, 일별, 주별 등). 지정된 된 일정에 hello 파이프라인을 실행 하십시오. 또한 다양 한 시각화 기능 toodisplay hello 계보 및 데이터 파이프라인, 간의 종속성을 제공 하 고 모든 데이터 파이프라인에서 단일 통합된 뷰 tooeasily 정확 하 게 문제를 모니터링 하 고 모니터링 경고 설정.

참조 [소개 tooAzure Data Factory](data-factory-introduction.md) 및 [첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 문서 tooquickly hello Azure 데이터 팩터리 서비스를 시작 합니다.

### <a name="data-factory-and-machine-learning-together"></a>Data Factory 및 Machine Learning
Azure Data Factory 수 있도록 tooeasily 하면 게시 된 보고서를 사용 하는 파이프라인을 만들 [Azure 기계 학습] [ azure-machine-learning] 웹 서비스에 대 한 예측 분석 합니다. Hello를 사용 하 여 **일괄 처리 실행 작업** 는 Azure 데이터 팩터리 파이프라인에서 일괄 처리의 hello 데이터에는 Azure ML 웹 서비스 toomake 예측을 호출할 수 있습니다. 참조 [일괄 처리 실행 작업 hello 웹 서비스를 사용 하 여 Azure 기계 학습 호출](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) 자세한 내용은 섹션.

시간이 지남에 따라 hello hello Azure 기계 학습 점수 매기기 실험에 예측 모델에 새 입력된 데이터 집합을 통해 유지 toobe가 필요 합니다. 데이터 팩토리 파이프라인에서는 Azure ML 모델을 보존 하기 위해 hello 다음 단계를 수행 하 여 수 있습니다.

1. Hello 학습 실험 (예측 하지 실험) 웹 서비스로 게시 합니다. Hello 이전 시나리오에서 웹 서비스로 tooexpose 예측 실험을 수행한 것 처럼 hello Azure 기계 학습 스튜디오에서에서이 단계를 수행 합니다.
2. Hello 학습 실험에 대 한 hello Azure ML 일괄 처리 실행 작업 tooinvoke hello 웹 서비스를 사용 합니다. 기본적으로, hello Azure ML 일괄 처리 실행 활동 tooinvoke 학습 웹 서비스 및 웹 서비스 점수 매기기를 사용할 수 있습니다.

재교육를 완료 한 후 업데이트 hello를 사용 하 여 웹 서비스 (웹 서비스로 노출 된 예측 실험) hello 새로 학습 된 모델 점수 매기기 hello **Azure ML 업데이트 리소스 작업**합니다. 자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>배치 실행 작업을 사용하여 웹 서비스 호출
Azure Data Factory tooorchestrate 데이터 이동 및 처리를 사용 하 고이 정보를 Azure 기계 학습을 사용 하 여 일괄 처리 실행을 수행 합니다. Hello 최상위 단계는 다음과 같습니다.

1. Azure 기계 학습 연결된 서비스를 만듭니다. 다음 값에는 hello가 필요 합니다.

   1. **요청 URI** hello 일괄 처리 실행 API에 대 한 합니다. Hello를 클릭 하 여 hello 요청 URI를 찾을 수 있습니다 **일괄 처리 실행** hello 웹 서비스 페이지에 링크 합니다.
   2. **API 키** hello Azure 기계 학습 웹 서비스를 게시 합니다. Hello 웹 서비스 게시를 클릭 하 여 hello API 키를 찾을 수 있습니다.
   3. 사용 하 여 hello **AzureMLBatchExecution** 활동입니다.

      ![기계 학습 대시보드](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![배치 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>시나리오: 웹 서비스 입력/출력 toodata Azure Blob 저장소에 참조를 사용 하 여 실험
이 시나리오에서는 hello Azure 컴퓨터 학습 웹 서비스에서 Azure blob 저장소의 파일에서 데이터를 사용 하 여 예측을 수행 하 고 hello blob 저장소에 hello 예측 결과 저장 합니다. hello 다음 JSON 정의 AzureMLBatchExecution 작업과 함께 데이터 팩터리 파이프라인 합니다. hello 활동에 데이터 집합이 두 hello **DecisionTreeInputBlob** 입력으로 및 **DecisionTreeResultBlob** hello 출력으로 합니다. hello **DecisionTreeInputBlob** hello를 사용 하 여 입력된 toohello 웹 서비스로 전달 되 **webServiceInput** JSON 속성입니다. hello **DecisionTreeResultBlob** hello를 사용 하 여 출력 toohello 웹 서비스로 전달 되 **webServiceOutputs** JSON 속성입니다.  

> [!IMPORTANT]
> Hello를 사용 하 여 hello 웹 서비스 변수를 사용할 경우 여러 개의 입력 **webServiceInputs** 사용 하는 대신 속성 **webServiceInput**합니다. Hello 참조 [웹 서비스 작업에 여러 개의 입력](#web-service-requires-multiple-inputs) hello webServiceInputs 속성을 사용 하는 예제에 대 한 섹션.
>
> Hello에서 참조 되는 데이터 집합 **webServiceInput**/**webServiceInputs** 및 **webServiceOutputs** 속성 (에서  **typeProperties**) hello 활동에에서도 포함 해야 **입력** 및 **출력**합니다.
>
> Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다. webServiceInputs, webServiceOutputs, 및 globalParameters 설정에 사용할 수는 hello 이름에는 hello 실험에서 hello 이름과 정확히 일치 해야 합니다. Azure 기계 학습 끝점 tooverify 예상 hello 매핑을 대 한 hello 일괄 처리 실행 도움말 페이지에 hello 샘플 요청 페이로드를 볼 수 있습니다.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> 유일한 입 / 출력 hello AzureMLBatchExecution 활동의 매개 변수 toohello 웹 서비스 변수로 전달할 수 있습니다. 예를 들어 JSON 코드 조각은 위에 hello, DecisionTreeInputBlob은 입력된 toohello webServiceInput 매개 변수를 통해 웹 서비스는 입력된 toohello 변수로 전달 되는 AzureMLBatchExecution 활동에는 사용 합니다.   
>
>

### <a name="example"></a>예제
이 예에서는 사용 하 여 Azure 저장소 toohold 입력 및 출력 데이터 hello 둘 다 있습니다.

Hello를 통과 하는 것이 좋습니다 [데이터 팩터리와 첫 번째 파이프라인 빌드] [ adf-build-1st-pipeline] 자습서이 예제를 진행 하십시오. 이 예에서 hello 데이터 팩터리 편집기 toocreate 데이터 팩터리 아티팩트의 (연결 된 서비스, 데이터 집합, 파이프라인)를 사용 합니다.   

1. **Azure Storage**에 대한 **연결된 서비스**를 만듭니다. Hello 입력 및 출력 파일에 있는 경우 다른 저장소 계정에는 두 개의 연결 된 서비스가 필요 합니다. 다음은 JSON 예제입니다.

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Hello 만들기 **입력** Azure Data Factory **dataset**합니다. 다른 Data Factory 데이터 집합과 달리 이러한 데이터 집합은 **folderPath** 및 **fileName** 값을 둘 다 포함해야 합니다. 각 일괄 처리 실행 (각 데이터 조각) tooprocess toocause 분할을 사용 하 여 또는 고유한 입력을 생성 한 출력 파일 수 있습니다. Tooinclude 일부 업스트림 작업 tootransform hello hello CSV 파일 형식으로 입력 하 고 각 조각에 대 한 hello 저장소 계정에 배치 해야 합니다. Hello 하지 포함 경우 **외부** 및 **externalData** hello 뒤에 표시 된 예제에서는 하 여 DecisionTreeInputBlob 것은 다른 활동의 hello 출력 데이터 집합 설정 합니다.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    입력된 csv 파일 hello 열 머리글 행에 있어야 합니다. Hello를 사용 하는 경우 **복사 작업** hello blob 저장소로 toocreate/이동 hello csv hello 싱크 속성을 설정 해야 **blobWriterAddHeader** 너무**true**합니다. 예:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Hello csv 파일 hello 머리글 행이 없는 경우 hello 다음 오류가 표시 될 수 있습니다: **활동에서 오류가: 문자열을 읽는 동안 오류가 발생 합니다. Unexpected token: StartObject. Path '', line 1, position 1**.
3. Hello 만들기 **출력** Azure Data Factory **dataset**합니다. 이 예제에서는 각 조각 실행에 대 한 분할 toocreate 고유한 출력 경로 사용 합니다. Hello 활동 hello 분할 수 없이 hello 파일을 덮어씁니다.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. 만들기는 **연결 된 서비스** 형식의: **AzureMLLinkedService**, hello API 키를 제공 하 및 일괄 처리 실행 URL을 모델링 합니다.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. 끝으로, **AzureMLBatchExecution** 작업이 포함된 파이프라인을 작성합니다. 런타임 시, 파이프라인 단계를 수행 하는 hello를 수행 합니다.

   1. 입력된 데이터 집합에서 hello 입력된 파일의 hello 위치를 가져옵니다.
   2. Hello Azure 기계 학습 일괄 처리 실행 API를 호출합니다.
   3. 복사는 출력 데이터 집합에 지정 된 일괄 처리 실행 출력 toohello blob을 hello 합니다.

      > [!NOTE]
      > AzureMLBatchExecution 작업에는 0개 이상의 입력 및 1개 이상의 출력이 있을 수 있습니다.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      **start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예: 2014-10-14T16:32:41Z. hello **끝** 으로 선택 사항입니다. Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간입니다.**" toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다. JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.

      > [!NOTE]
      > Hello AzureMLBatchExecution 활동에 대 한 입력을 지정 하는 것은 선택 사항입니다.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>시나리오: toorefer toodata 판독기/작성기 모듈을 사용 하 여 다양 한 저장소에서 실험
Azure 기계 학습 실험을 만들 때 또 다른 일반적인 시나리오는 toouse 판독기 및 작성기 모듈입니다. hello 판독기는 실험에 사용 되는 tooload 데이터 고 hello 기록기 모듈은 실험에서 toosave 데이터입니다. 판독기 및 기록기 모듈에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요.     

Hello 판독기 및 작성기 모듈을 사용할 경우 좋습니다 toouse 이러한 판독기/작성기 모듈의 각 속성에 대 한 웹 서비스 매개 변수는 합니다. 이러한 웹 매개 변수 런타임 동안 tooconfigure hello 값을 사용 합니다. 예를 들어 Azure SQL 데이터베이스: XXX.database.windows.net을 사용하는 판독기 모듈을 사용하여 실험을 만들 수 있습니다. Hello 웹 서비스가 배포 된 후 원하는 hello 웹 서비스 toospecify의 tooenable hello 소비자 YYY.database.windows.net 라는 다른 Azure SQL Server. 이 값 toobe 구성 된 웹 서비스 매개 변수 tooallow를 사용할 수 있습니다.

> [!NOTE]
> 웹 서비스 입력 및 출력은 웹 서비스 매개 변수와 다릅니다. Hello 첫 번째 시나리오에서는 Azure 기계 학습 웹 서비스에 대 한 입력 및 출력 수 지정 하는 방법을 설명 했습니다. 이 시나리오에서는 tooproperties 판독기/작성기 모듈의 해당 하는 웹 서비스에 대 한 매개 변수를 전달 합니다.
>
>

웹 서비스 매개 변수를 사용하는 시나리오를 살펴보겠습니다. 판독기 모듈 tooread 데이터를 Azure 기계 학습에서 지 원하는 hello 데이터 원본 중 하나를 사용 하는 배포 된 Azure 기계 학습 웹 서비스 (예: Azure SQL 데이터베이스). Hello 일괄 처리 실행이 수행 된 후 기록기 모듈 (Azure SQL 데이터베이스)를 사용 하 여 hello 결과가 기록 됩니다.  웹 서비스 입력 및 출력 없음 hello 실험에서 정의 됩니다. 이 경우 hello 판독기 및 작성기 모듈에 대 한 관련 웹 서비스 매개 변수를 구성 하는 것이 좋습니다. 이 구성은 hello AzureMLBatchExecution 활동을 사용 하는 경우 구성 모듈 toobe hello 읽기/쓰기를 허용 합니다. Hello에 웹 서비스 매개 변수를 지정 하면 **globalParameters** 다음과 같이 hello 활동 JSON 섹션.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

사용할 수도 있습니다 [데이터 팩터리 함수](data-factory-functions-variables.md) hello에 대 한 값 hello 다음 예제와 같이 웹 서비스 매개 변수를 전달 합니다.

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> hello 웹 서비스 매개 변수가 대/소문자를 구분 하므로 hello 활동에서 지정 하는 hello 이름을 JSON과 일치 하는지 hello hello 웹 서비스에서 노출 하는 것입니다.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>판독기 모듈 tooread 데이터를 사용 하 여 Azure Blob에 여러 파일에서
Pig, Hive와 같은 작업이 있는 빅 데이터 파이프라인은 확장명 없이 하나 이상의 출력 파일을 만들 수 있습니다. 예를 들어 외부 하이브 테이블을 지정 하면 hello 외부 Hive 테이블에 대 한 hello 데이터 저장할 수 있습니다 Azure blob 저장소에 이름 000000_0 다음 hello로. 여러 개의 파일을 실험 tooread에 hello 판독기 모듈을 사용할 수 있으며 예측에 대 한 사용.

Azure 기계 학습 실험에서 hello 판독기 모듈을 사용할 때 Azure Blob을 입력으로 지정할 수 있습니다. hello Azure blob 저장소의에서 hello 파일 hello 출력 파일 일 수 있습니다 (예: 000000_0) HDInsight에서 실행 되는 Pig 및 Hive 스크립트에 의해 생성 된입니다. hello 판독기 모듈 있습니다 tooread 파일 (확장명이 없는) hello를 구성 하 여 **경로 toocontainer, 디렉터리/blob**합니다. hello **경로 toocontainer** 포인트 toohello 컨테이너 및 **디렉터리/blob** hello 다음 이미지와 같이 hello 파일이 포함 된 toofolder를 가리킵니다. hello, 즉 별표 \*) **hello 컨테이너/폴더에 파일을 hello 모두 지정 (즉, 데이터/aggregateddata/년 = 2014/월-6 /\*)** hello 실험의 일환으로 읽혀집니다.

![Azure Blob 속성](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>예
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>AzureMLBatchExecution 작업 및 웹 서비스 매개 변수가 포함된 파이프라인

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

위 예제 JSON hello에서:

* hello Azure 컴퓨터 학습 웹 서비스에는 판독기와 기록기 모듈 tooread/쓰기 데이터를 사용 하 여 배포 / tooan Azure SQL 데이터베이스입니다. 이 웹 서비스는 hello 다음 4 개의 매개 변수가 노출: 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호입니다.  
* **start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다. 예: 2014-10-14T16:32:41Z. hello **끝** 으로 선택 사항입니다. Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간입니다.**" toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다. JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.

### <a name="other-scenarios"></a>기타 시나리오
#### <a name="web-service-requires-multiple-inputs"></a>웹 서비스에는 다중 입력이 필요합니다
Hello를 사용 하 여 hello 웹 서비스 변수를 사용할 경우 여러 개의 입력 **webServiceInputs** 사용 하는 대신 속성 **webServiceInput**합니다. Hello에서 참조 되는 데이터 집합 **webServiceInputs** hello 활동에에서도 포함 해야 **입력**합니다.

Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다. webServiceInputs, webServiceOutputs, 및 globalParameters 설정에 사용할 수는 hello 이름에는 hello 실험에서 hello 이름과 정확히 일치 해야 합니다. Azure 기계 학습 끝점 tooverify 예상 hello 매핑을 대 한 hello 일괄 처리 실행 도움말 페이지에 hello 샘플 요청 페이로드를 볼 수 있습니다.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>웹 서비스에는 입력이 필요하지 않습니다.
Azure ML 일괄 처리 실행 웹 서비스 사용된 toorun 모든 워크플로 수 있으며, 예: R 또는 Python 스크립트에는 필요 하지 않을 수 어떤 입력도 합니다. 또는 모든 GlobalParameters를 노출 하지 않는 판독기 모듈 hello 실험 구성할 수 있습니다. 이 경우 hello AzureMLBatchExecution 활동 다음과 같이 구성 합니다.

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>웹 서비스에는 입력/출력이 필요하지 않습니다.
hello Azure ML 일괄 처리 실행 웹 서비스에 구성 된 웹 서비스 출력이 없을 수 있습니다. 이 예제에서는 웹 서비스 입력 또는 출력이 없으며 GlobalParameters도 구성되어 있지 않습니다. Hello 활동 자체에 구성 된 출력 하지만 webServiceOutput으로 제공 되지 않습니다.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>웹 서비스 사용 하 여 판독기 및 기록기 및 다른 작업이 성공한 경우에 hello 활동을 실행
hello는 Azure ML 웹 서비스 판독기 및 작성기 모듈 구성된 toorun 상관 없이 모든 GlobalParameters 수도 있습니다. 그러나 일부 업스트림 처리가 완료 된 경우에 데이터 집합 종속성 tooinvoke hello 서비스를 사용 하는 파이프라인에서 tooembed 서비스를 호출 하는 것이 좋습니다. 이 방식을 사용 하 여 hello 일괄 처리 실행이 완료 한 후에 다른 작업을 트리거할 수 있습니다. 이 경우 그 중 하나를 웹 서비스 입력 또는 출력으로 이름을 지정 하지 않고 작업 입력 및 출력을 사용 하 여 hello 종속성을 표현할 수 있습니다.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

hello **자** 됩니다.

* 실험 끝점은 webServiceInput를 사용 하는 경우: 그 blob 데이터 집합 표시 되 고 hello 작업의 입력 및 hello webServiceInput 속성에 포함 되어 있습니다. 그렇지 않으면 hello webServiceInput 속성을 생략 합니다.
* 실험 끝점 webServiceOutput(s)를 사용 하는 경우: blob 데이터 집합으로 표시 되 고 hello webServiceOutputs 속성 및 hello 활동 출력에 포함 되어 있습니다. hello 활동 출력 하 고 webServiceOutputs hello 실험에서 각 출력의 hello 이름별으로 매핑됩니다. 그렇지 않으면 hello webServiceOutputs 속성을 생략 합니다.
* 실험 끝점 globalParameter(s)을 노출할 경우 hello 활동 globalParameters 속성의 키 값 쌍으로 제공 됩니다. 그렇지 않으면 hello globalParameters 속성을 생략 합니다. hello 키 대/소문자를 구분 하지 않습니다. [Azure 데이터 팩터리 함수](data-factory-functions-variables.md) hello 값에 사용할 수 있습니다.
* 추가 데이터 집합 hello 활동 typeproperties에서 참조 하지 않고 hello 활동 입 / 출력 속성에 포함 될 수 있습니다. 이러한 데이터 집합 조각 종속성을 사용 하 여 실행을 제어 합니다. 하지만 hello AzureMLBatchExecution 활동에서 무시 됩니다.


## <a name="updating-models-using-update-resource-activity"></a>업데이트 리소스 작업을 사용하여 모델 업데이트
재교육를 완료 한 후 업데이트 hello를 사용 하 여 웹 서비스 (웹 서비스로 노출 된 예측 실험) hello 새로 학습 된 모델 점수 매기기 hello **Azure ML 업데이트 리소스 작업**합니다. 자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.

### <a name="reader-and-writer-modules"></a>판독기 및 작성기 모듈
웹 서비스 매개 변수를 사용 하기 위한 일반적인 시나리오에는 hello를 사용 하 여 Azure SQL 판독기 및 작성기입니다. hello 판독기 모듈은 Azure 기계 학습 스튜디오 외부의 데이터 관리 서비스에서 실험에 사용 되는 tooload 데이터입니다. hello 기록기 모듈은 Azure 기계 학습 스튜디오 외부의 데이터 관리 서비스에 실험에서 toosave 데이터입니다.  

Azure Blob/Azure SQL 판독기/기록기에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요. hello 이전 단원의 hello 예제 hello Azure Blob 판독기 및 작성기 Azure Blob을 사용 합니다. 이 섹션에서는 Azure SQL 판독기 및 Azure SQL 기록기를 사용하는 방법을 설명합니다.

## <a name="frequently-asked-questions"></a>질문과 대답
**Q:** 빅 데이터 파이프라인에서 생성된 여러 파일이 있습니다. Hello AzureMLBatchExecution 활동 toowork 모든 hello 파일에 사용할 수 있습니까?

**A:** 예. Hello 참조 **판독기 모듈 tooread 데이터를 사용 하 여 Azure Blob에 여러 파일의** 자세한 내용은 섹션.

## <a name="azure-ml-batch-scoring-activity"></a>Azure ML 일괄 처리 점수 매기기 작업
Hello를 사용 하는 경우 **AzureMLBatchScoring** 와 Azure 기계 학습 작업 toointegrate, 권장 메서드 최신 hello를 사용 하는 **AzureMLBatchExecution** 활동입니다.

hello AzureMLBatchExecution 활동은 2015 년 8 월 릴리스의 Azure SDK 및 Azure PowerShell hello에 도입 되었습니다.

Toocontinue hello AzureMLBatchScoring 활동을 사용 하 여 원하는 경우이 섹션 전체를 읽고 계속 합니다.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>입/출력에 대해 Azure 저장소를 사용하는 Azure ML 일괄 처리 점수 매기기 작업

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>웹 서비스 매개 변수
웹 서비스 매개 변수에 대 한 toospecify 값 추가 **typeProperties** 섹션 toohello **AzureMLBatchScoringActivty** hello 파이프라인 hello 다음 예제와 같이 JSON의 섹션:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
사용할 수도 있습니다 [데이터 팩터리 함수](data-factory-functions-variables.md) hello에 대 한 값 hello 다음 예제와 같이 웹 서비스 매개 변수를 전달 합니다.

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> hello 웹 서비스 매개 변수가 대/소문자를 구분 하므로 hello 활동에서 지정 하는 hello 이름을 JSON과 일치 하는지 hello hello 웹 서비스에서 노출 하는 것입니다.
>
>

## <a name="see-also"></a>참고 항목
* [Azure 블로그 게시물: Azure 데이터 팩터리 및 Azure 기계 학습 시작하기](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
