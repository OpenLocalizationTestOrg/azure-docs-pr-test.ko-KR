---
title: "aaaBuild 첫 번째 데이터 팩터리 (리소스 관리자 템플릿) | Microsoft Docs"
description: "이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>자습서: Azure 리소스 관리자 템플릿을 사용하여 첫 번째 Azure Data Factory 빌드
> [!div class="op_single_selector"]
> * [개요 및 필수 구성 요소](data-factory-build-your-first-pipeline.md)
> * [Azure 포털](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager 템플릿](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

이 문서에서는 Azure 리소스 관리자 템플릿 toocreate 첫 번째 Azure 데이터 팩터리를 사용합니다. 다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.

이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다. 이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다. hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다. 

> [!NOTE]
> 이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다. 방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.
> 
> 이 자습서에서는 hello 파이프라인에 유형의 하나의 활동: HDInsightHive 합니다. 파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다. 및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다. 자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요. 

## <a name="prerequisites"></a>필수 조건
* 자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.
* 지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서 tooinstall에 최신 버전의 Azure PowerShell 컴퓨터입니다.
* 참조 [Azure 리소스 관리자 템플릿 제작](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager 템플릿에 대 한 합니다. 

## <a name="in-this-tutorial"></a>자습서 내용
| 엔터티 | 설명 |
| --- | --- |
| Azure 저장소 연결된 서비스 |Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다. 안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정. |
| HDInsight 주문형 연결된 서비스 |주문형 HDInsight 클러스터 toohello 데이터 팩터리에 연결 되어 있습니다. hello 클러스터는 자동으로 생성 tooprocess 데이터 하 고 hello 처리를 완료 한 후 삭제 됩니다. |
| Azure Blob 입력 데이터 집합 |Toohello Azure 저장소 연결 된 서비스를 참조합니다. hello 연결 된 서비스 tooan Azure 저장소 계정을 나타내며 hello Azure Blob 데이터 집합 hello 입력된 데이터를 보유 하는 hello 저장소에 hello 컨테이너, 폴더 및 파일 이름을 지정 합니다. |
| Azure Blob 출력 데이터 집합 |Toohello Azure 저장소 연결 된 서비스를 참조합니다. hello 연결 된 서비스 tooan Azure 저장소 계정을 나타내며 hello Azure Blob 데이터 집합 hello 출력 데이터를 보유 하는 hello 저장소에 hello 컨테이너, 폴더 및 파일 이름을 지정 합니다. |
| 데이터 파이프라인 |hello 파이프라인 HDInsightHive hello 입력된 데이터 집합을 사용 하 고 hello 출력 데이터 집합을 생성 하는 유형의 하나의 활동을 있습니다. |

데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다. 파이프라인에는 하나 이상의 작업이 있을 수 있습니다. 이러한 두 가지 유형의 활동은 [데이터 이동 활동](data-factory-data-movement-activities.md) 및 [데이터 변환 활동](data-factory-data-transformation-activities.md)입니다. 이 자습서에는 한 가지 활동(Hive 활동)이 있는 파이프라인을 만듭니다.

hello 다음 섹션에서는 hello 완전 한 리소스 관리자 템플릿 hello 자습서 및 테스트 hello 서식 파일을 통해 신속 하 게 실행할 수 있도록 데이터 팩터리의 엔터티를 정의 하기 위한 합니다. toounderstand 각 Data Factory 엔터티에 정의 된 참조 [hello 서식 파일에서 엔터티를 Data Factory](#data-factory-entities-in-the-template) 섹션.

## <a name="data-factory-json-template"></a>데이터 팩터리 JSON 템플릿
데이터 팩터리를 정의 하기 위한 최상위 리소스 관리자 템플릿을 hello은입니다. 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```
라는 JSON 파일을 만들어 **ADFTutorialARM.json** 에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureStorage",
                  "description": "Azure Storage linked service",
                  "typeProperties": {
                    "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
                  }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
                  }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]",
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> [자습서: Azure Resource Manager 템플릿을 사용하여 복사 활동이 있는 파이프라인 만들기](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)에서 Azure 데이터 팩터리를 만들기 위한 또 다른 Resource Manager 템플릿 예를 찾을 수 있습니다.  
> 
> 

## <a name="parameters-json"></a>매개 변수 JSON
라는 JSON 파일을 만들어 **ADFTutorialARM Parameters.json** hello Azure Resource Manager 템플릿에 대 한 매개 변수가 포함 된 합니다.  

> [!IMPORTANT]
> Hello 이름과 hello에 대 한 사용자의 Azure 저장소 계정 키를 지정 **storageAccountName** 및 **storageAccountKey** 이 매개 변수 파일의 매개 변수입니다. 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> 테스트, 개발의 경우 별도 매개 변수로 JSON 파일이 있을 수 있습니다 및 프로덕션 환경으로 사용할 수 있는 hello 같은 데이터 팩터리 JSON 템플릿. Power Shell 스크립트를 사용하여 이러한 환경에서 데이터 팩터리 엔터티 배포를 자동화할 수 있습니다. 
> 
> 

## <a name="create-data-factory"></a>데이터 팩터리 만들기
1. 시작 **Azure PowerShell** 다음 명령이 실행된 하는 hello 및: 
   * Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * 이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * 다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다. 이 구독은 hello hello Azure 포털에서에서 사용 된 것 처럼 동일한 hello 해야 합니다.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. 1 단계에서에서 만든 hello 리소스 관리자 템플릿을 사용 하 여 명령 toodeploy Data Factory 엔터티에 따라 hello를 실행 합니다. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>파이프라인 모니터링
1. Toohello 로그인 한 후 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기** 선택 **데이터 팩터리**합니다.
     ![찾아보기->데이터 팩터리](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Hello에 **데이터 팩터리** 블레이드에서 hello 데이터 팩터리의 클릭 (**TutorialFactoryARM**) 사용자가 만든 합니다.    
3. Hello에 **Data Factory** 데이터 팩터리를 블레이드 클릭 **다이어그램**합니다.

     ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Hello에 **다이어그램 보기**를 hello 파이프라인에 대 한 개요를 확인 하 고 데이터 집합에 사용 되는이 자습서입니다.
   
   ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. 다이어그램 보기 hello에서 hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다. 현재 처리 중인 해당 hello 조각이 표시 됩니다.
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다. 주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분) 따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Hello 조각화 된 경우 **준비** 상태, hello 확인 **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.  

참조 [모니터링 데이터 집합 및 파이프라인](data-factory-monitor-manage-pipelines.md) 어떻게 toouse hello Azure 포털 블레이드 toomonitor hello 파이프라인 및 데이터 집합에서에서 만든이 자습서에 대 한 지침은 합니다.

데이터 파이프라인 toomonitor 모니터 및 앱 관리를 사용할 수도 있습니다. 참조 [모니터 및 관리 응용 프로그램 모니터링을 사용 하 여 Azure 데이터 팩터리 파이프라인](data-factory-monitor-manage-app.md) hello 응용 프로그램을 사용 하는 방법에 대 한 합니다. 

> [!IMPORTANT]
> 입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다. 따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Hello 서식 파일에서 데이터 팩터리 엔터티
### <a name="define-data-factory"></a>데이터 팩터리 정의
Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
hello dataFactoryName 다음과 같이 정의 됩니다. 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
Hello 리소스 그룹 ID를 기반으로 고유 문자열  

### <a name="defining-data-factory-entities"></a>데이터 팩터리 엔터티 정의
hello 다음과 같은 데이터 팩터리 엔터티 템플릿에 정의 된 hello JSON: 

* [Azure 저장소 연결된 서비스](#azure-storage-linked-service)
* [HDInsight 주문형 연결된 서비스](#hdinsight-on-demand-linked-service)
* [Azure Blob 입력 데이터 집합](#azure-blob-input-dataset)
* [Azure Blob 출력 데이터 집합:](#azure-blob-output-dataset)
* [복사 작업을 포함하는 데이터 파이프라인](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Azure 저장소 연결된 서비스
이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다. 참조 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다. 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
hello **connectionString** 사용 하 여 hello storageAccountName 및 storageAccountKey 매개 변수입니다. 구성 파일을 사용 하 여 전달 하는 이러한 매개 변수에 대 한 hello 값입니다. 또한 사용 하 여 변수 hello 정의: azureStroageLinkedService 및 dataFactoryName hello 서식 파일에 정의 합니다. 

#### <a name="hdinsight-on-demand-linked-service"></a>HDInsight 주문형 연결된 서비스
참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight 주문형 연결 된 서비스 JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 문서입니다.  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
포인트 다음 참고 hello: 

* hello 데이터 팩터리가 **Linux 기반** hello JSON 위에 있는 사용자에 대 한 HDInsight 클러스터입니다. 자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요. 
* 주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다. 자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.
* hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**). HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.
  
    많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.

자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.

#### <a name="azure-blob-input-dataset"></a>Azure Blob 입력 데이터 집합
Blob 컨테이너, 폴더 및 hello 입력된 데이터가 포함 된 파일의 hello 이름을 지정할 수 있습니다. 참조 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다. 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
Hello 매개 변수 서식 파일에 정의 된 매개 변수를 다음을 사용 하 여이 정의: blobContainer, inputBlobFolder, 및 inputBlobName 합니다. 

#### <a name="azure-blob-output-dataset"></a>Azure Blob 출력 데이터 집합
Blob 컨테이너 및 hello 출력 데이터를 보유 하는 폴더의 hello 이름을 지정 합니다. 참조 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

이 정의 hello 매개 변수 서식 파일에 정의 된 매개 변수 뒤 hello를 사용 하 여: blobContainer 및 outputBlobFolder 합니다. 

#### <a name="data-pipeline"></a>데이터 파이프라인
주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터를 변환하는 파이프라인을 정의합니다. 참조 [파이프라인 JSON](data-factory-create-pipelines.md#pipeline-json) JSON 사용 되는 요소 toodefine이이 예제에서 파이프라인에 대 한 설명입니다. 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-hello-template"></a>Hello 서식 파일을 다시 사용
Hello 자습서에서는 데이터 팩터리의 엔터티 및 매개 변수 값을 전달 하기 위한 서식 파일을 정의 하기 위한 서식 파일을 만들었습니다. toouse hello 동일한 템플릿 toodeploy Data Factory 엔터티에 toodifferent 환경, 각 환경에 대 한 매개 변수 파일을 만들고 toothat 환경을 배포 하는 경우 사용 합니다.     

예제:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Hello 첫 번째 명령은 file 매개 변수를 사용 하 여 hello 개발 환경에 대 한, 두 번째 hello에 대 한 환경을 테스트 하 고 hello 프로덕션 환경에 대 한 세 번째 hello를 확인 합니다.  

Hello 템플릿 tooperform 다시 사용할 수도 있습니다 반복 되는 작업입니다. 더 많은 파이프라인을 구현 하는 동일한 논리 하지만 각 데이터 팩터리 사용 하 여 다른 Azure 저장소 및 Azure SQL 데이터베이스 계정 hello 또는 toocreate 하나를 사용 하는 많은 데이터 팩터리 필요 예를 들어. Hello를 사용 하면이 시나리오에서 같은 템플릿을 hello에 다른 매개 변수와 함께 동일한 환경 (개발, 테스트 또는 프로덕션) 파일 toocreate 데이터 팩터리입니다. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>게이트웨이를 만드는 Resource Manager 템플릿
Hello 다시에서 논리 게이트웨이 만들기 위한 샘플 리소스 관리자 템플릿 다음과 같습니다. 온-프레미스 컴퓨터 또는 Azure IaaS VM에 게이트웨이 설치 하 고 hello 게이트웨이 키를 사용 하 여 데이터 팩터리 서비스를 등록 합니다. 자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
이 템플릿은 GatewayUsingARM이라는 게이트웨이를 포함한 GatewayUsingArmDF라는 데이터 팩터리를 만듭니다. 

## <a name="see-also"></a>참고 항목
| 항목 | 설명 |
|:--- |:--- |
| [파이프라인](data-factory-create-pipelines.md) |이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다. |
| [데이터 집합](data-factory-create-datasets.md) |이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다. |
| [예약 및 실행](data-factory-scheduling-and-execution.md) |이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다. |
| [모니터링 앱을 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md) |이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다. |

