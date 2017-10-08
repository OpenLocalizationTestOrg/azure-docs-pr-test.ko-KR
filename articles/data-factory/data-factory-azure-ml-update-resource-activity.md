---
title: "Azure 데이터 팩터리를 사용 하 여 aaaUpdate 기계 학습 모델 | Microsoft Docs"
description: "Toocreate Azure 데이터 팩터리 및 Azure 기계 학습을 사용 하 여 예측 파이프라인을 생성 하는 방법을 설명 합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>업데이트 리소스 작업을 사용하여 Azure Machine Learning 모델 업데이트

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

이 문서 보완 hello 주요 Azure 데이터 팩터리-Azure 기계 학습 통합 문서: [Azure 기계 학습 및 Azure 데이터 팩터리를 사용 하 여 예측 파이프라인 만들기](data-factory-azure-ml-batch-execution-activity.md)합니다. 그렇게 이미 하지 않은 경우이 문서 전체를 읽기 전에 hello 기본 문서를 검토 합니다. 

## <a name="overview"></a>개요
시간이 지남에 따라 hello hello Azure 기계 학습 점수 매기기 실험에 예측 모델에 새 입력된 데이터 집합을 통해 유지 toobe가 필요 합니다. 재교육를 완료 한 후 웹 서비스 hello와 점수 매기기 tooupdate hello ML 모델을 다시 학습 되도록 할 수 있습니다. hello 일반적인 단계 tooenable 재교육 및 웹 서비스를 통해 Azure ML 모델을 업데이트 됩니다.

1. [Azure 기계 학습 스튜디오](https://studio.azureml.net)에서 실험을 만듭니다.
2. Hello 모델 만족 스 러 우면 두 hello에 대 한 Azure 기계 학습 스튜디오 toopublish 웹 서비스를 사용할 **학습 실험** 및 평가 /**예측 실험**합니다.

hello 다음 표에서 설명 hello 웹 서비스를이 예제에서 사용 합니다.  자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](../machine-learning/machine-learning-retrain-models-programmatically.md) 을 참조하세요.

- **학습 웹 서비스** - 학습 데이터를 수신하고 학습된 모델을 생성합니다. hello 재교육의 hello 출력은 Azure Blob 저장소에.ilearner 파일. hello **끝점 기본** hello 교육을 게시할 때 실험을 웹 서비스에 대해 자동으로 생성 됩니다. 더 많은 끝점을 만들 수 있지만 hello 기본 끝점을 사용 하 여 hello 예제입니다.
- **점수 매기기 웹 서비스** - 레이블이 지정되지 않은 데이터 예제를 수신하고 예측을 합니다. 예측의 hello 출력.csv 파일 또는 hello 실험의 hello 구성에 따라, Azure SQL 데이터베이스의 행 같은 다양 한 형식을 가질 수 있습니다. hello 예측 실험을 웹 서비스로 게시 하는 경우 사용자에 대 한 hello 기본 끝점이 자동으로 만들어집니다. 

hello 다음 그림 보여주고 hello 관계 학습 및 Azure 기계 학습에서 끝점을 평가 합니다.

![웹 서비스](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Hello를 호출할 수 있습니다 **학습 웹 서비스** hello를 사용 하 여 **Azure ML 일괄 처리 실행 작업**합니다. 학습 웹 서비스를 호출하는 것은 점수 매기기 데이터에 대해 Azure ML 웹 서비스(점수 매기기 웹 서비스)를 호출하는 것과 동일합니다. 이전 섹션에서는 커버 tooinvoke Azure ML 웹 서비스를 사용 하 여 Azure Data Factory를 자세히 파이프라인 하는 방법을 hello 합니다. 

Hello를 호출할 수 있습니다 **웹 서비스 점수 매기기** hello를 사용 하 여 **Azure ML 업데이트 리소스 작업** hello 새로 학습 된 모델 tooupdate hello 웹 서비스입니다. 연결 된 서비스 정의 제공 하는 예제 따르는 hello: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>웹 서비스 점수 매기기는 클래식 웹 서비스입니다.
웹 서비스를 평가 하는 hello는 경우는 **클래식 웹 서비스**, hello를 두 번째로 만들 **기본이 아닌 및 업데이트할 수 있는 끝점** hello를 사용 하 여 [Azure 포털](https://manage.windowsazure.com)합니다. 이에 대한 단계는 [끝점 만들기](../machine-learning/machine-learning-create-endpoint.md) 문서를 참조하세요. Hello 기본값이 아닌 업데이트할 수 있는 끝점을 만든 후 다음 단계 hello지 않습니다.

* 클릭 **일괄 처리 실행** tooget hello URI hello에 대 한 값 **인해 mlEndpoint** JSON 속성입니다.
* 클릭 **업데이트 리소스** 링크 hello에 대 한 tooget hello URI 값 **updateResourceEndpoint** JSON 속성입니다. hello API 키가 hello 끝점 페이지 자체에 (hello 오른쪽 아래 모서리)입니다.

![업데이트 가능한 끝점](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

다음 예에서는 hello hello AzureML 연결 서비스에 대 한 샘플 JSON 정의 제공 합니다. hello 연결 된 서비스 hello apiKey 인증에 사용 합니다.  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>웹 서비스 점수 매기기는 Azure Resource Manager 웹 서비스입니다. 
Hello 웹 서비스는 hello 새로운 유형의 Azure 리소스 관리자 끝점을 노출 하는 웹 서비스를 하는 경우 불필요 tooadd hello 둘째 **기본이 아닌** 끝점입니다. hello **updateResourceEndpoint** hello에 연결 된 서비스는 hello 형식: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Hello에 hello 웹 서비스를 쿼리할 때 hello URL에 대 한 자리 표시자에 대 한 값을 가져올 수 [Azure 컴퓨터 학습 웹 서비스 포털](https://services.azureml.net/)합니다. hello 새로운 유형의 업데이트 리소스 끝점에는 AAD (Azure Active Directory) 토큰이 필요 합니다. AzureML 연결된 서비스에서 **servicePrincipalId** 및 **servicePrincipalKey**를 지정합니다. 참조 [toocreate 서비스 보안 주체 하 고 사용 권한을 toomanage Azure 리소스를 할당 하는 방법을](../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다. 샘플 AzureML 연결된 서비스 정의는 다음과 같습니다. 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

hello 다음과 같은 시나리오 자세한 세부 정보를 제공 합니다. Azure Data Factory 파이프라인에서 Azure ML 모델을 재학습 및 업데이트하는 예제가 포함되어 있습니다.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>시나리오: Azure ML 모델 재학습 및 업데이트
이 섹션에서는 hello를 사용 하는 샘플 파이프라인 **Azure ML 일괄 처리 실행 활동** tooretrain 모델입니다. 또한 사용 하 여 hello hello 파이프라인 **Azure ML 업데이트 리소스 작업** 웹 서비스를 평가 하는 hello에서 tooupdate hello 모델입니다. hello 섹션은 또한 모든 JSON 조각을 hello 연결 된 서비스, 데이터 집합 및 hello 예제에서 파이프라인을 제공 합니다.

Hello 샘플 파이프라인의 hello 다이어그램 보기는 다음과 같습니다. 볼 수 있듯이 hello Azure ML 일괄 처리 실행 작업은 hello 학습 입력 하 고 학습 출력 (iLearner 파일)를 생성 합니다. Azure ML 업데이트 리소스 작업 hello이 교육 출력 걸리며 업데이트 hello 웹 서비스 끝점을 점수 매기기 hello에서 모델. hello 업데이트 리소스 작업 출력을 생성 하지 않습니다. hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.

![파이프라인 다이어그램](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Azure Blob 저장소 연결된 서비스:
Azure 저장소 hello 같은 데이터가 hello을 보유 합니다.

* 학습 데이터. hello hello Azure ML 학습 웹 서비스에 대 한 입력된 데이터입니다.  
* iLearner 파일. hello hello Azure ML 학습 웹 서비스에서 출력 합니다. 이 파일 hello 입력된 toohello 업데이트 리소스 작업 이기도합니다.  

Hello 연결 된 서비스의 hello 샘플 JSON 정의 다음과 같습니다.

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a>학습 입력 데이터 집합:
hello 다음 데이터 집합이 나타냅니다 hello Azure ML 학습 웹 서비스에 대 한 hello 입력된 학습 데이터를. Azure ML 일괄 처리 실행 활동 hello이 데이터이 집합을 입력 변수로 사용 합니다.

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a>학습 출력 데이터 집합:
hello 다음 데이터 집합이 나타냅니다 hello 출력 iLearner 파일을 hello Azure ML 학습 웹 서비스에서. Azure ML 일괄 처리 실행 작업 hello이 데이터이 집합을 생성합니다. 이 데이터 집합 hello 입력된 toohello Azure ML 업데이트 리소스 작업 이기도합니다.

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Azure ML 학습 끝점에 대한 연결된 서비스
다음 JSON 코드 조각은 hello hello 학습 웹 서비스의 toohello 기본 끝점을 가리키는 Azure 기계 학습 연결 서비스를 정의 합니다.

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

**Azure 기계 학습 스튜디오**, 다음 tooget 값에 대 한 hello 수행 **인해 mlEndpoint** 및 **apiKey**:

1. 클릭 **웹 서비스** hello 왼쪽된 메뉴에 있습니다.
2. Hello 클릭 **학습 웹 서비스** 의 웹 서비스는 hello 목록에 있습니다.
3. फ 복사 너무**API 키** 입력란. Hello 클립보드의 hello 키를 hello 데이터 팩터리 JSON 편집기에 붙여 넣습니다.
4. Hello에 **Azure 기계 학습 스튜디오**, 클릭 **일괄 처리 실행** 링크 합니다.
5. 복사 hello **요청 URI** hello에서 **요청** 섹션 및 hello 데이터 팩터리 JSON 편집기에 붙여 넣습니다.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Azure ML 업데이트 가능한 점수 매기기 끝점에 대한 연결된 서비스:
다음 JSON 코드 조각은 hello toohello 기본값이 아닌 업데이트할 수 있는 끝점의 웹 서비스를 평가 하는 hello 가리키는 Azure 기계 학습 연결 서비스를 정의 합니다.  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a>자리 표시자 출력 데이터 집합:
hello Azure ML 업데이트 리소스 작업에는 어떠한 출력도 생성 하지 않습니다. 그러나 Azure 데이터 팩터리 파이프라인의 한 출력 데이터 집합 toodrive hello 일정이 필요합니다. 따라서 이 예에서는 더미/자리 표시자 데이터 집합을 사용합니다.  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a>파이프라인
hello 파이프라인에는 두 개의 활동: **AzureMLBatchExecution** 및 **AzureMLUpdateResource**합니다. hello Azure ML 일괄 처리 실행 작업 hello 학습 데이터를 입력으로 사용 하 고 출력으로 iLearner 파일을 생성 합니다. hello 활동 데이터를 학습 하는 hello 입력이 포함 된 hello 학습 웹 서비스 (학습 실험을 웹 서비스로 노출)을 호출 하 고 hello 웹 서비스에서 hello ilearner 파일을 받습니다. hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.

![파이프라인 다이어그램](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
