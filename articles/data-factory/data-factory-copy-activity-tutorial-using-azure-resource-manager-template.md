---
title: "자습서: Resource Manager 템플릿을 사용하여 파이프라인 생성 | Microsoft Docs"
description: "이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 Azure Data Factory 파이프라인을 만듭니다. 이 파이프라인은 Azure Blob Storage에서 Azure SQL Database로 데이터를 복사합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="21597-104">자습서: Azure Resource Manager 템플릿을 사용하여 데이터를 복사하는 Data Factory 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="21597-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21597-105">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="21597-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="21597-106">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="21597-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="21597-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="21597-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="21597-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21597-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="21597-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21597-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="21597-110">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="21597-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="21597-111">REST API</span><span class="sxs-lookup"><span data-stu-id="21597-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="21597-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="21597-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="21597-113">이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 Azure Data Factory를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="21597-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="21597-114">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="21597-115">출력 데이터를 생성하기 위해 입력 데이터를 변환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="21597-116">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="21597-117">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21597-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="21597-118">복사 작업은 지원되는 데이터 저장소에서 지원되는 싱크 데이터 저장소로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="21597-119">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="21597-120">이 작업은 다양한 데이터 저장소 간에 데이터를 안전하고 안정적이며 확장성 있는 방법으로 복사할 수 있는 전역적으로 사용 가능한 서비스를 통해 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="21597-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="21597-121">복사 작업에 대한 자세한 내용은 [데이터 이동 작업](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="21597-122">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="21597-123">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="21597-124">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="21597-125">이 자습서에서 데이터 파이프라인은 원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="21597-126">Azure Data Factory를 사용하여 데이터를 변환하는 방법에 대한 자습서는 [자습서: Hadoop 클러스터를 사용하여 데이터를 변환하도록 파이프라인 빌드](data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="21597-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="21597-127">Prerequisites</span></span>
* <span data-ttu-id="21597-128">[자습서 개요 및 필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 살펴보고 **필수 구성 요소** 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="21597-129">[Azure PowerShell을 설치 및 구성하는 방법](/powershell/azure/overview) 문서의 지침을 수행하여 컴퓨터에 Azure PowerShell의 최신 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="21597-130">이 자습서에서는 PowerShell을 사용하여 데이터 팩터리 엔터티를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="21597-131">(선택 사항) Azure Resource Manager 템플릿에 대한 자세한 내용은 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="21597-132">자습서 내용</span><span class="sxs-lookup"><span data-stu-id="21597-132">In this tutorial</span></span>
<span data-ttu-id="21597-133">이 자습서에서는 다음 데이터 팩터리 엔터티로 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21597-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="21597-134">엔터티</span><span class="sxs-lookup"><span data-stu-id="21597-134">Entity</span></span> | <span data-ttu-id="21597-135">설명</span><span class="sxs-lookup"><span data-stu-id="21597-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21597-136">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-136">Azure Storage linked service</span></span> |<span data-ttu-id="21597-137">Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="21597-138">Azure Storage는 원본 데이터 저장소이고 Azure SQL Database는 자습서의 복사 작업에 대한 싱크 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="21597-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="21597-139">복사 작업을 위한 입력 데이터가 포함된 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="21597-140">Azure SQL Database 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="21597-141">Azure SQL Database를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="21597-142">복사 작업에 대한 출력 데이터를 보유하는 Azure SQL Database를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="21597-143">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-143">Azure Blob input dataset</span></span> |<span data-ttu-id="21597-144">Azure Storage 연결된 서비스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="21597-145">연결된 서비스는 Azure Storage 계정을 말하며 Azure Blob 데이터 집합은 입력 데이터를 가진 저장소의 컨테이너, 폴더, 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="21597-146">Azure SQL 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-146">Azure SQL output dataset</span></span> |<span data-ttu-id="21597-147">Azure SQL 연결된 서비스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="21597-148">Azure SQL 연결된 서비스는 Azure SQL Server를 말하며 Azure SQL 데이터 집합은 출력 데이터를 가진 테이블의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="21597-149">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="21597-149">Data pipeline</span></span> |<span data-ttu-id="21597-150">파이프라인에는 입력으로 Azure Blob 데이터 집합을 사용하고 출력으로 Azure SQL 데이터 집합을 사용하는 복사 유형의 작업이 하나 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="21597-151">복사 작업은 Azure Blob의 데이터를 Azure SQL Database의 테이블에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="21597-152">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="21597-153">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="21597-154">이러한 두 가지 유형의 활동은 [데이터 이동 활동](data-factory-data-movement-activities.md) 및 [데이터 변환 활동](data-factory-data-transformation-activities.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="21597-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="21597-155">이 자습서에는 한 가지 활동(복사 활동)이 있는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21597-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Azure Blob을 Azure SQL Database로 복사](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="21597-157">다음 섹션에서는 신속하게 자습서를 살펴보고 템플릿을 테스트할 수 있도록 데이터 팩터리 엔터티를 정의하기 위한 완전한 Resource Manager 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="21597-158">각 데이터 팩터리 엔터티를 정의하는 방법을 알아보려면 [템플릿의 데이터 팩터리 엔터티](#data-factory-entities-in-the-template) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="21597-159">데이터 팩터리 JSON 템플릿</span><span class="sxs-lookup"><span data-stu-id="21597-159">Data Factory JSON template</span></span>
<span data-ttu-id="21597-160">데이터 팩터리 정의를 위한 최상위 Resource Manager 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="21597-161">**C:\ADFGetStarted** 폴더에 다음과 같은 내용으로 **ADFCopyTutorialARM.json**이라는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21597-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
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
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
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
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
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
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="21597-162">매개 변수 JSON</span><span class="sxs-lookup"><span data-stu-id="21597-162">Parameters JSON</span></span>
<span data-ttu-id="21597-163">Azure Resource Manager 템플릿에 대한 매개 변수를 포함하는 **ADFCopyTutorialARM-Parameters.json**이라는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21597-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="21597-164">storageAccountName 및 storageAccountKey 매개 변수에 대한 Azure Storage 계정의 이름과 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="21597-165">sqlServerName, databaseName, sqlServerUserName 및 sqlServerPassword 매개 변수에 대한 Azure SQL 서버, 데이터베이스, 사용자 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="21597-166">개발, 테스트 및 프로덕션 환경에 별도의 매개 변수 JSON 파일을 두고 동일한 데이터 팩터리 JSON 템플릿을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="21597-167">Power Shell 스크립트를 사용하여 이러한 환경에서 데이터 팩터리 엔터티 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="21597-168">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="21597-168">Create data factory</span></span>
1. <span data-ttu-id="21597-169">**Azure PowerShell** 을 시작하고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="21597-170">다음 명령을 실행하고 Azure 포털에 로그인하는 데 사용할 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="21597-171">다음 명령을 실행하여 이 계정의 모든 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="21597-172">다음 명령을 실행하여 사용하려는 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="21597-173">1단계에서 만든 Resource Manager 템플릿을 사용하여 데이터 팩터리 엔터티를 배포하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="21597-174">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="21597-174">Monitor pipeline</span></span>

1. <span data-ttu-id="21597-175">Azure 계정을 사용하여 [Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="21597-176">왼쪽 메뉴에서 **데이터 팩터리**를 클릭하거나 **더 많은 서비스**를 클릭하고 **INTELLIGENCE + ANALYTICS** 범주 아래에서 **데이터 팩터리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![데이터 팩터리 메뉴](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="21597-178">**데이터 팩터리** 페이지에서 데이터 팩터리(AzureBlobToAzureSQLDatabaseDF)를 검색하고 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![데이터 팩터리 검색](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="21597-180">Azure Data Factory를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-180">Click your Azure data factory.</span></span> <span data-ttu-id="21597-181">데이터 팩터리의 홈 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-181">You see the home page for the data factory.</span></span>
   
    ![데이터 팩터리의 홈 페이지](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="21597-183">이 자습서에서 만든 파이프라인과 데이터 집합을 모니터링하려면 [데이터 집합 및 파이프라인 모니터링](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline)의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="21597-184">Visual Studio는 현재 Data Factory 파이프라인 모니터링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="21597-185">조각이 **준비** 상태일 때 데이터가 Azure SQL Database의 **emp** 테이블에 복사되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="21597-186">이 자습서에서 만든 파이프라인과 데이터집합을 Azure Portal 블레이드를 사용하여 모니터링하는 방법은 [데이터 집합 및 파이프라인 모니터링](data-factory-monitor-manage-pipelines.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="21597-187">모니터링 및 관리 응용 프로그램을 사용하여 데이터 파이프라인을 모니터링하는 방법에 대한 자세한 내용은 [모니터링 앱을 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="21597-188">템플릿의 데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="21597-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="21597-189">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="21597-189">Define data factory</span></span>
<span data-ttu-id="21597-190">다음 예제에서처럼 Resource Manager 템플릿에서 데이터 팩터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="21597-191">dataFactoryName은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="21597-192">리소스 그룹 ID를 기반으로 하는 고유 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="21597-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="21597-193">데이터 팩터리 엔터티 정의</span><span class="sxs-lookup"><span data-stu-id="21597-193">Defining Data Factory entities</span></span>
<span data-ttu-id="21597-194">다음 데이터 팩터리 엔터티는 JSON 템플릿에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="21597-195">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="21597-196">Azure SQL 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="21597-197">Azure Blob 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="21597-198">Azure SQL 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="21597-199">복사 작업을 포함하는 데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="21597-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="21597-200">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-200">Azure Storage linked service</span></span>
<span data-ttu-id="21597-201">AzureStorageLinkedService는 Azure 저장소 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="21597-202">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 컨테이너를 만들고 이 저장소 계정에 데이터를 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="21597-203">이 섹션의 Azure 저장소 계정 이름 및 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="21597-204">Azure Storage 연결된 서비스를 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Storage 연결된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="21597-205">connectionString은 storageAccountName 및 storageAccountKey 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="21597-206">이러한 매개 변수의 값은 구성 파일을 사용하여 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="21597-207">정의 또한 템플릿에 정의된 azureStroageLinkedService 및 dataFactoryName 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="21597-208">Azure SQL Database 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="21597-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="21597-209">AzureSqlLinkedService는 Azure SQL 데이터베이스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="21597-210">Blob 저장소에서 복사된 데이터는 이 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="21597-211">[필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)의 일부로 이 데이터베이스에서 emp 테이블을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="21597-212">이 섹션에서 Azure SQL 서버 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="21597-213">Azure SQL 연결된 서비스를 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure SQL 연결된 서비스](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="21597-214">connectionString은 sqlServerName, databaseName, sqlServerUserName, sqlServerPassword 매개 변수를 사용하며 해당 값은 구성 파일을 사용하여 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="21597-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="21597-215">정의 또한 템플릿에서 azureSqlLinkedServiceName, dataFactoryName 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="21597-216">Azure Blob 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-216">Azure blob dataset</span></span>
<span data-ttu-id="21597-217">Azure 저장소 연결된 서비스는 런타임에 Data Factory 서비스에서 Azure 저장소 계정에 연결하는 데 사용하는 연결 문자열을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="21597-218">Azure Blob 데이터 집합 정의에서 입력 데이터를 포함하는 Blob 컨테이너, 폴더 및 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="21597-219">Azure Blob 데이터 집합을 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="21597-220">Azure SQL 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="21597-220">Azure SQL dataset</span></span>
<span data-ttu-id="21597-221">Azure Blob 저장소에서 복사된 데이터를 보유하는 Azure SQL Database의 테이블 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="21597-222">Azure SQL 데이터 집합을 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Blob 데이터 집합 속성](data-factory-azure-sql-connector.md#dataset-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="21597-223">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="21597-223">Data pipeline</span></span>
<span data-ttu-id="21597-224">Azure Blob 데이터 집합에서Azure SQL 데이터 집합으로 데이터를 복사하는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="21597-225">이 예에서 파이프라인을 정의하는 데 사용된 JSON 요소에 대한 자세한 설명은 [파이프라인 JSON](data-factory-create-pipelines.md#pipeline-json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="21597-226">템플릿 재사용</span><span class="sxs-lookup"><span data-stu-id="21597-226">Reuse the template</span></span>
<span data-ttu-id="21597-227">이 자습서에서는 데이터 팩터리 엔터티를 정의하는 템플릿과 매개 변수 값을 전달하는 템플릿을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="21597-228">이 파이프라인은 Azure Storage 계정에서 매개 변수를 통해 지정된 Azure SQL Database로 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="21597-229">같은 템플릿을 사용하여 데이터 팩터리 엔터티를 다른 환경에 배포하는 데 사용하려면 각 환경에 대한 매개 변수 파일을 만들고 해당 환경에 배포할 때 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="21597-230">예제:</span><span class="sxs-lookup"><span data-stu-id="21597-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="21597-231">첫 번째 명령은 개발 환경에 대한 매개 변수 파일, 두 번째 명령은 테스트 환경에 대한 매개 변수 파일, 세 번째 명령은 프로덕션 환경에 대한 매개 변수 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="21597-232">또한 이 템플릿을 재사용하여 반복 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="21597-233">예를 들어 동일한 논리를 구현하는 하나 이상의 파이프라인으로 여러 데이터 팩터리를 만들어야 하는데 각 데이터 팩터리가 서로 다른 Storage 및 SQL Database 계정을 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="21597-234">이 경우 매개 변수가 서로 다른 동일한 환경(개발, 테스트 또는 프로덕션)에서 동일한 템플릿을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="21597-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="21597-235">Next steps</span></span>
<span data-ttu-id="21597-236">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="21597-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="21597-237">다음 표에서는 복사 활동에서 원본 및 싱크로 지원되는 데이터 저장소의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="21597-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="21597-238">데이터 저장소간에 데이터를 복사하는 방법에 대해 알아보려면 테이블에서 데이터 저장소에 대한 링크를 클릭하세요.</span><span class="sxs-lookup"><span data-stu-id="21597-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
