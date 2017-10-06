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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="85dec-103">자습서: Azure 리소스 관리자 템플릿을 사용하여 첫 번째 Azure Data Factory 빌드</span><span class="sxs-lookup"><span data-stu-id="85dec-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="85dec-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="85dec-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="85dec-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="85dec-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="85dec-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="85dec-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="85dec-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85dec-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="85dec-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="85dec-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="85dec-109">REST API</span><span class="sxs-lookup"><span data-stu-id="85dec-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="85dec-110">이 문서에서는 Azure 리소스 관리자 템플릿 toocreate 첫 번째 Azure 데이터 팩터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="85dec-111">다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="85dec-112">이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="85dec-113">이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="85dec-114">hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="85dec-115">이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="85dec-116">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="85dec-117">이 자습서에서는 hello 파이프라인에 유형의 하나의 활동: HDInsightHive 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="85dec-118">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="85dec-119">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="85dec-120">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85dec-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="85dec-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="85dec-121">Prerequisites</span></span>
* <span data-ttu-id="85dec-122">자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="85dec-123">지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서 tooinstall에 최신 버전의 Azure PowerShell 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="85dec-124">참조 [Azure 리소스 관리자 템플릿 제작](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager 템플릿에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="85dec-125">자습서 내용</span><span class="sxs-lookup"><span data-stu-id="85dec-125">In this tutorial</span></span>
| <span data-ttu-id="85dec-126">엔터티</span><span class="sxs-lookup"><span data-stu-id="85dec-126">Entity</span></span> | <span data-ttu-id="85dec-127">설명</span><span class="sxs-lookup"><span data-stu-id="85dec-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="85dec-128">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-128">Azure Storage linked service</span></span> |<span data-ttu-id="85dec-129">Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="85dec-130">안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="85dec-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="85dec-131">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="85dec-132">주문형 HDInsight 클러스터 toohello 데이터 팩터리에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="85dec-133">hello 클러스터는 자동으로 생성 tooprocess 데이터 하 고 hello 처리를 완료 한 후 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="85dec-134">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-134">Azure Blob input dataset</span></span> |<span data-ttu-id="85dec-135">Toohello Azure 저장소 연결 된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="85dec-136">hello 연결 된 서비스 tooan Azure 저장소 계정을 나타내며 hello Azure Blob 데이터 집합 hello 입력된 데이터를 보유 하는 hello 저장소에 hello 컨테이너, 폴더 및 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="85dec-137">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-137">Azure Blob output dataset</span></span> |<span data-ttu-id="85dec-138">Toohello Azure 저장소 연결 된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="85dec-139">hello 연결 된 서비스 tooan Azure 저장소 계정을 나타내며 hello Azure Blob 데이터 집합 hello 출력 데이터를 보유 하는 hello 저장소에 hello 컨테이너, 폴더 및 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="85dec-140">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="85dec-140">Data pipeline</span></span> |<span data-ttu-id="85dec-141">hello 파이프라인 HDInsightHive hello 입력된 데이터 집합을 사용 하 고 hello 출력 데이터 집합을 생성 하는 유형의 하나의 활동을 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="85dec-142">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="85dec-143">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="85dec-144">이러한 두 가지 유형의 활동은 [데이터 이동 활동](data-factory-data-movement-activities.md) 및 [데이터 변환 활동](data-factory-data-transformation-activities.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="85dec-145">이 자습서에는 한 가지 활동(Hive 활동)이 있는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="85dec-146">hello 다음 섹션에서는 hello 완전 한 리소스 관리자 템플릿 hello 자습서 및 테스트 hello 서식 파일을 통해 신속 하 게 실행할 수 있도록 데이터 팩터리의 엔터티를 정의 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="85dec-147">toounderstand 각 Data Factory 엔터티에 정의 된 참조 [hello 서식 파일에서 엔터티를 Data Factory](#data-factory-entities-in-the-template) 섹션.</span><span class="sxs-lookup"><span data-stu-id="85dec-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="85dec-148">데이터 팩터리 JSON 템플릿</span><span class="sxs-lookup"><span data-stu-id="85dec-148">Data Factory JSON template</span></span>
<span data-ttu-id="85dec-149">데이터 팩터리를 정의 하기 위한 최상위 리소스 관리자 템플릿을 hello은입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="85dec-150">라는 JSON 파일을 만들어 **ADFTutorialARM.json** 에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="85dec-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

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
> <span data-ttu-id="85dec-151">[자습서: Azure Resource Manager 템플릿을 사용하여 복사 활동이 있는 파이프라인 만들기](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)에서 Azure 데이터 팩터리를 만들기 위한 또 다른 Resource Manager 템플릿 예를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="85dec-152">매개 변수 JSON</span><span class="sxs-lookup"><span data-stu-id="85dec-152">Parameters JSON</span></span>
<span data-ttu-id="85dec-153">라는 JSON 파일을 만들어 **ADFTutorialARM Parameters.json** hello Azure Resource Manager 템플릿에 대 한 매개 변수가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="85dec-154">Hello 이름과 hello에 대 한 사용자의 Azure 저장소 계정 키를 지정 **storageAccountName** 및 **storageAccountKey** 이 매개 변수 파일의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="85dec-155">테스트, 개발의 경우 별도 매개 변수로 JSON 파일이 있을 수 있습니다 및 프로덕션 환경으로 사용할 수 있는 hello 같은 데이터 팩터리 JSON 템플릿.</span><span class="sxs-lookup"><span data-stu-id="85dec-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="85dec-156">Power Shell 스크립트를 사용하여 이러한 환경에서 데이터 팩터리 엔터티 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="85dec-157">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="85dec-157">Create data factory</span></span>
1. <span data-ttu-id="85dec-158">시작 **Azure PowerShell** 다음 명령이 실행된 하는 hello 및:</span><span class="sxs-lookup"><span data-stu-id="85dec-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="85dec-159">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="85dec-160">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="85dec-161">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="85dec-162">이 구독은 hello hello Azure 포털에서에서 사용 된 것 처럼 동일한 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="85dec-163">1 단계에서에서 만든 hello 리소스 관리자 템플릿을 사용 하 여 명령 toodeploy Data Factory 엔터티에 따라 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="85dec-164">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="85dec-164">Monitor pipeline</span></span>
1. <span data-ttu-id="85dec-165">Toohello 로그인 한 후 [Azure 포털](https://portal.azure.com/), 클릭 **찾아보기** 선택 **데이터 팩터리**합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="85dec-166">![찾아보기->데이터 팩터리](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="85dec-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="85dec-167">Hello에 **데이터 팩터리** 블레이드에서 hello 데이터 팩터리의 클릭 (**TutorialFactoryARM**) 사용자가 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="85dec-168">Hello에 **Data Factory** 데이터 팩터리를 블레이드 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="85dec-170">Hello에 **다이어그램 보기**를 hello 파이프라인에 대 한 개요를 확인 하 고 데이터 집합에 사용 되는이 자습서입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="85dec-172">다이어그램 보기 hello에서 hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="85dec-173">현재 처리 중인 해당 hello 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-173">You see that hello slice that is currently being processed.</span></span>
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="85dec-175">Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="85dec-176">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="85dec-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="85dec-177">따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="85dec-179">Hello 조각화 된 경우 **준비** 상태, hello 확인 **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="85dec-180">참조 [모니터링 데이터 집합 및 파이프라인](data-factory-monitor-manage-pipelines.md) 어떻게 toouse hello Azure 포털 블레이드 toomonitor hello 파이프라인 및 데이터 집합에서에서 만든이 자습서에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="85dec-181">데이터 파이프라인 toomonitor 모니터 및 앱 관리를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="85dec-182">참조 [모니터 및 관리 응용 프로그램 모니터링을 사용 하 여 Azure 데이터 팩터리 파이프라인](data-factory-monitor-manage-app.md) hello 응용 프로그램을 사용 하는 방법에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="85dec-183">입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="85dec-184">따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="85dec-185">Hello 서식 파일에서 데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="85dec-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="85dec-186">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="85dec-186">Define data factory</span></span>
<span data-ttu-id="85dec-187">Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="85dec-188">hello dataFactoryName 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="85dec-189">Hello 리소스 그룹 ID를 기반으로 고유 문자열</span><span class="sxs-lookup"><span data-stu-id="85dec-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="85dec-190">데이터 팩터리 엔터티 정의</span><span class="sxs-lookup"><span data-stu-id="85dec-190">Defining Data Factory entities</span></span>
<span data-ttu-id="85dec-191">hello 다음과 같은 데이터 팩터리 엔터티 템플릿에 정의 된 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="85dec-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="85dec-192">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="85dec-193">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="85dec-194">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="85dec-195">Azure Blob 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="85dec-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="85dec-196">복사 작업을 포함하는 데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="85dec-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="85dec-197">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-197">Azure Storage linked service</span></span>
<span data-ttu-id="85dec-198">이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="85dec-199">참조 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="85dec-200">hello **connectionString** 사용 하 여 hello storageAccountName 및 storageAccountKey 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="85dec-201">구성 파일을 사용 하 여 전달 하는 이러한 매개 변수에 대 한 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="85dec-202">또한 사용 하 여 변수 hello 정의: azureStroageLinkedService 및 dataFactoryName hello 서식 파일에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="85dec-203">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="85dec-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="85dec-204">참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight 주문형 연결 된 서비스 JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="85dec-205">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="85dec-205">Note hello following points:</span></span> 

* <span data-ttu-id="85dec-206">hello 데이터 팩터리가 **Linux 기반** hello JSON 위에 있는 사용자에 대 한 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="85dec-207">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85dec-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="85dec-208">주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="85dec-209">자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85dec-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="85dec-210">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="85dec-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="85dec-211">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="85dec-212">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-212">This behavior is by design.</span></span> <span data-ttu-id="85dec-213">주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="85dec-214">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="85dec-215">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="85dec-216">이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="85dec-217">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="85dec-218">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85dec-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="85dec-219">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-219">Azure blob input dataset</span></span>
<span data-ttu-id="85dec-220">Blob 컨테이너, 폴더 및 hello 입력된 데이터가 포함 된 파일의 hello 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="85dec-221">참조 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="85dec-222">Hello 매개 변수 서식 파일에 정의 된 매개 변수를 다음을 사용 하 여이 정의: blobContainer, inputBlobFolder, 및 inputBlobName 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="85dec-223">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-223">Azure Blob output dataset</span></span>
<span data-ttu-id="85dec-224">Blob 컨테이너 및 hello 출력 데이터를 보유 하는 폴더의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="85dec-225">참조 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="85dec-226">이 정의 hello 매개 변수 서식 파일에 정의 된 매개 변수 뒤 hello를 사용 하 여: blobContainer 및 outputBlobFolder 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="85dec-227">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="85dec-227">Data pipeline</span></span>
<span data-ttu-id="85dec-228">주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터를 변환하는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="85dec-229">참조 [파이프라인 JSON](data-factory-create-pipelines.md#pipeline-json) JSON 사용 되는 요소 toodefine이이 예제에서 파이프라인에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="85dec-230">Hello 서식 파일을 다시 사용</span><span class="sxs-lookup"><span data-stu-id="85dec-230">Reuse hello template</span></span>
<span data-ttu-id="85dec-231">Hello 자습서에서는 데이터 팩터리의 엔터티 및 매개 변수 값을 전달 하기 위한 서식 파일을 정의 하기 위한 서식 파일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="85dec-232">toouse hello 동일한 템플릿 toodeploy Data Factory 엔터티에 toodifferent 환경, 각 환경에 대 한 매개 변수 파일을 만들고 toothat 환경을 배포 하는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="85dec-233">예제:</span><span class="sxs-lookup"><span data-stu-id="85dec-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="85dec-234">Hello 첫 번째 명령은 file 매개 변수를 사용 하 여 hello 개발 환경에 대 한, 두 번째 hello에 대 한 환경을 테스트 하 고 hello 프로덕션 환경에 대 한 세 번째 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="85dec-235">Hello 템플릿 tooperform 다시 사용할 수도 있습니다 반복 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="85dec-236">더 많은 파이프라인을 구현 하는 동일한 논리 하지만 각 데이터 팩터리 사용 하 여 다른 Azure 저장소 및 Azure SQL 데이터베이스 계정 hello 또는 toocreate 하나를 사용 하는 많은 데이터 팩터리 필요 예를 들어.</span><span class="sxs-lookup"><span data-stu-id="85dec-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="85dec-237">Hello를 사용 하면이 시나리오에서 같은 템플릿을 hello에 다른 매개 변수와 함께 동일한 환경 (개발, 테스트 또는 프로덕션) 파일 toocreate 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="85dec-238">게이트웨이를 만드는 Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="85dec-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="85dec-239">Hello 다시에서 논리 게이트웨이 만들기 위한 샘플 리소스 관리자 템플릿 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="85dec-240">온-프레미스 컴퓨터 또는 Azure IaaS VM에 게이트웨이 설치 하 고 hello 게이트웨이 키를 사용 하 여 데이터 팩터리 서비스를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="85dec-241">자세한 내용은 [온-프레미스 및 클라우드 간 데이터 이동](data-factory-move-data-between-onprem-and-cloud.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="85dec-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="85dec-242">이 템플릿은 GatewayUsingARM이라는 게이트웨이를 포함한 GatewayUsingArmDF라는 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="85dec-243">참고 항목</span><span class="sxs-lookup"><span data-stu-id="85dec-243">See Also</span></span>
| <span data-ttu-id="85dec-244">항목</span><span class="sxs-lookup"><span data-stu-id="85dec-244">Topic</span></span> | <span data-ttu-id="85dec-245">설명</span><span class="sxs-lookup"><span data-stu-id="85dec-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="85dec-246">파이프라인</span><span class="sxs-lookup"><span data-stu-id="85dec-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="85dec-247">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="85dec-248">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="85dec-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="85dec-249">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="85dec-250">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="85dec-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="85dec-251">이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="85dec-252">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="85dec-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="85dec-253">이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="85dec-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

