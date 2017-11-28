---
title: "자습서: Resource Manager 템플릿을 사용하여 파이프라인 생성 | Microsoft Docs"
description: "이 자습서에서는 Azure Resource Manager 템플릿을 사용하여 Azure Data Factory 파이프라인을 만듭니다. 이 파이프라인 Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사합니다."
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="4fe1f-104">자습서: Azure 리소스 관리자를 사용 하 여 템플릿 toocreate 데이터 팩터리 파이프라인 toocopy 데이터</span><span class="sxs-lookup"><span data-stu-id="4fe1f-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fe1f-105">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="4fe1f-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="4fe1f-106">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="4fe1f-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="4fe1f-107">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="4fe1f-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="4fe1f-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4fe1f-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="4fe1f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fe1f-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="4fe1f-110">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="4fe1f-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="4fe1f-111">REST API</span><span class="sxs-lookup"><span data-stu-id="4fe1f-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="4fe1f-112">.NET API</span><span class="sxs-lookup"><span data-stu-id="4fe1f-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="4fe1f-113">이 자습서에서는 Azure 리소스 관리자 템플릿 toocreate Azure 데이터 팩터리에 toouse 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="4fe1f-114">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="4fe1f-115">입력된 데이터 tooproduce 출력 데이터를 변환 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="4fe1f-116">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="4fe1f-117">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="4fe1f-118">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="4fe1f-119">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4fe1f-120">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4fe1f-121">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="4fe1f-122">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4fe1f-123">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="4fe1f-124">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="4fe1f-125">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="4fe1f-126">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4fe1f-127">필수 조건</span><span class="sxs-lookup"><span data-stu-id="4fe1f-127">Prerequisites</span></span>
* <span data-ttu-id="4fe1f-128">통해 이동 [자습서 개요 및 필수 조건](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 및 전체 hello **필수 구성 요소** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="4fe1f-129">지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서 tooinstall에 최신 버전의 Azure PowerShell 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="4fe1f-130">이 자습서에서는 PowerShell toodeploy Data Factory 엔터티에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="4fe1f-131">(선택 사항) 참조 [Azure 리소스 관리자 템플릿 제작](../azure-resource-manager/resource-group-authoring-templates.md) toolearn Azure Resource Manager 템플릿에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="4fe1f-132">자습서 내용</span><span class="sxs-lookup"><span data-stu-id="4fe1f-132">In this tutorial</span></span>
<span data-ttu-id="4fe1f-133">이 자습서에서는 Data Factory 엔터티에 따라 hello로 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="4fe1f-134">엔터티</span><span class="sxs-lookup"><span data-stu-id="4fe1f-134">Entity</span></span> | <span data-ttu-id="4fe1f-135">설명</span><span class="sxs-lookup"><span data-stu-id="4fe1f-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4fe1f-136">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-136">Azure Storage linked service</span></span> |<span data-ttu-id="4fe1f-137">Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="4fe1f-138">Azure 저장소는 hello 원본 데이터 저장소 및 Azure SQL 데이터베이스는 hello 자습서에서 hello 복사 작업에 대 한 hello 싱크 데이터 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="4fe1f-139">Hello hello 복사 작업에 대 한 입력된 데이터를 포함 하는 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="4fe1f-140">Azure SQL Database 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="4fe1f-141">Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="4fe1f-142">Hello 복사 작업에 대 한 hello 출력 데이터를 보유 하는 hello Azure SQL 데이터베이스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="4fe1f-143">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-143">Azure Blob input dataset</span></span> |<span data-ttu-id="4fe1f-144">Toohello Azure 저장소 연결 된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="4fe1f-145">hello 연결 된 서비스 tooan Azure 저장소 계정을 나타내며 hello Azure Blob 데이터 집합 hello 입력된 데이터를 보유 하는 hello 저장소에 hello 컨테이너, 폴더 및 파일 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="4fe1f-146">Azure SQL 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-146">Azure SQL output dataset</span></span> |<span data-ttu-id="4fe1f-147">Toohello Azure SQL 연결 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="4fe1f-148">hello Azure SQL 연결 서비스 tooan Azure SQL server를 참조 하 고 hello Azure SQL 데이터 집합 hello hello 출력 데이터를 보유 하는 hello 테이블 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="4fe1f-149">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="4fe1f-149">Data pipeline</span></span> |<span data-ttu-id="4fe1f-150">hello 파이프라인에 대 한 입력으로 hello Azure blob 데이터 집합을 사용 하는 복사본을 입력 하 고 hello를 출력으로 Azure SQL 데이터 집합의 한 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="4fe1f-151">hello 복사 활동 hello Azure SQL 데이터베이스에 있는 Azure blob tooa 테이블에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="4fe1f-152">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4fe1f-153">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4fe1f-154">이러한 두 가지 유형의 활동은 [데이터 이동 활동](data-factory-data-movement-activities.md) 및 [데이터 변환 활동](data-factory-data-transformation-activities.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="4fe1f-155">이 자습서에는 한 가지 활동(복사 활동)이 있는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Azure Blob tooAzure SQL 데이터베이스 복사](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="4fe1f-157">hello 다음 섹션에서는 hello 완전 한 리소스 관리자 템플릿 hello 자습서 및 테스트 hello 서식 파일을 통해 신속 하 게 실행할 수 있도록 데이터 팩터리의 엔터티를 정의 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="4fe1f-158">toounderstand 각 Data Factory 엔터티에 정의 된 참조 [hello 서식 파일에서 엔터티를 Data Factory](#data-factory-entities-in-the-template) 섹션.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="4fe1f-159">데이터 팩터리 JSON 템플릿</span><span class="sxs-lookup"><span data-stu-id="4fe1f-159">Data Factory JSON template</span></span>
<span data-ttu-id="4fe1f-160">데이터 팩터리를 정의 하기 위한 최상위 리소스 관리자 템플릿을 hello은입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="4fe1f-161">라는 JSON 파일을 만들어 **ADFCopyTutorialARM.json** 에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="4fe1f-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="4fe1f-162">매개 변수 JSON</span><span class="sxs-lookup"><span data-stu-id="4fe1f-162">Parameters JSON</span></span>
<span data-ttu-id="4fe1f-163">라는 JSON 파일을 만들어 **ADFCopyTutorialARM Parameters.json** hello Azure Resource Manager 템플릿에 대 한 매개 변수가 포함 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4fe1f-164">storageAccountName 및 storageAccountKey 매개 변수에 대한 Azure Storage 계정의 이름과 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="4fe1f-165">sqlServerName, databaseName, sqlServerUserName 및 sqlServerPassword 매개 변수에 대한 Azure SQL 서버, 데이터베이스, 사용자 및 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="4fe1f-166">테스트, 개발의 경우 별도 매개 변수로 JSON 파일이 있을 수 있습니다 및 프로덕션 환경으로 사용할 수 있는 hello 같은 데이터 팩터리 JSON 템플릿.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="4fe1f-167">Power Shell 스크립트를 사용하여 이러한 환경에서 데이터 팩터리 엔터티 배포를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="4fe1f-168">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="4fe1f-168">Create data factory</span></span>
1. <span data-ttu-id="4fe1f-169">시작 **Azure PowerShell** 다음 명령이 실행된 하는 hello 및:</span><span class="sxs-lookup"><span data-stu-id="4fe1f-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="4fe1f-170">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="4fe1f-171">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="4fe1f-172">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="4fe1f-173">1 단계에서에서 만든 hello 리소스 관리자 템플릿을 사용 하 여 명령 toodeploy Data Factory 엔터티에 따라 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="4fe1f-174">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="4fe1f-174">Monitor pipeline</span></span>

1. <span data-ttu-id="4fe1f-175">Toohello 로그인 [Azure 포털](https://portal.azure.com) Azure 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="4fe1f-176">클릭 **데이터 팩터리** hello 왼쪽 메뉴 (또는)에서 클릭 **더 많은 서비스** 클릭 **데이터 팩터리** 아래 **인텔리전스 + 분석** 범주입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![데이터 팩터리 메뉴](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="4fe1f-178">Hello에 **데이터 팩터리** 페이지 검색 하 고 데이터 팩터리 (AzureBlobToAzureSQLDatabaseDF)를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![데이터 팩터리 검색](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="4fe1f-180">Azure Data Factory를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-180">Click your Azure data factory.</span></span> <span data-ttu-id="4fe1f-181">데이터 팩터리 hello hello 홈 페이지를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-181">You see hello home page for hello data factory.</span></span>
   
    ![데이터 팩터리의 홈 페이지](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="4fe1f-183">지침에 따라 [모니터링 데이터 집합 및 파이프라인](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) 이 자습서에서 만든 toomonitor hello 파이프라인 및 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="4fe1f-184">Visual Studio는 현재 Data Factory 파이프라인 모니터링을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="4fe1f-185">조각을 hello에 있을 때 **준비** 상태, 복사한 toohello hello 데이터 인지 확인 **emp** hello Azure SQL 데이터베이스의 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="4fe1f-186">어떻게 toouse Azure 포털 블레이드 toomonitor 파이프라인 및 데이터 집합에서에서 만든이 자습서에 대 한 자세한 내용은 참조 하십시오. [모니터링 데이터 집합 및 파이프라인](data-factory-monitor-manage-pipelines.md) 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="4fe1f-187">어떻게 toouse hello 모니터링 및 관리 응용 프로그램 toomonitor 데이터 파이프라인에 대 한 자세한 내용은 참조 하십시오. [모니터 및 관리 응용 프로그램 모니터링을 사용 하 여 Azure 데이터 팩터리 파이프라인](data-factory-monitor-manage-app.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="4fe1f-188">Hello 서식 파일에서 데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="4fe1f-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="4fe1f-189">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="4fe1f-189">Define data factory</span></span>
<span data-ttu-id="4fe1f-190">Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="4fe1f-191">hello dataFactoryName 다음과 같이 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="4fe1f-192">Hello 리소스 그룹 ID를 기반으로 고유 문자열</span><span class="sxs-lookup"><span data-stu-id="4fe1f-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="4fe1f-193">데이터 팩터리 엔터티 정의</span><span class="sxs-lookup"><span data-stu-id="4fe1f-193">Defining Data Factory entities</span></span>
<span data-ttu-id="4fe1f-194">hello 다음과 같은 데이터 팩터리 엔터티 템플릿에 정의 된 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="4fe1f-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="4fe1f-195">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="4fe1f-196">Azure SQL 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="4fe1f-197">Azure Blob 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="4fe1f-198">Azure SQL 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="4fe1f-199">복사 작업을 포함하는 데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="4fe1f-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="4fe1f-200">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-200">Azure Storage linked service</span></span>
<span data-ttu-id="4fe1f-201">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="4fe1f-202">컨테이너를 만들고 데이터 toothis 저장소 계정을의 일환으로 업로드할 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="4fe1f-203">이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="4fe1f-204">참조 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="4fe1f-205">hello connectionString hello storageAccountName 및 storageAccountKey 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="4fe1f-206">구성 파일을 사용 하 여 전달 하는 이러한 매개 변수에 대 한 hello 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="4fe1f-207">또한 사용 하 여 변수 hello 정의: azureStroageLinkedService 및 dataFactoryName hello 서식 파일에 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="4fe1f-208">Azure SQL Database 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="4fe1f-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="4fe1f-209">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="4fe1f-210">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="4fe1f-211">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="4fe1f-212">이 섹션의 hello Azure SQL server 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="4fe1f-213">참조 [Azure SQL 연결 된 서비스](data-factory-azure-sql-connector.md#linked-service-properties) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure SQL 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="4fe1f-214">hello connectionString sqlServerName, 데이터베이스 이름, sqlServerUserName, 및 구성 파일을 사용 하 여 해당 값이 전달 되는 sqlServerPassword 매개 변수를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="4fe1f-215">hello 정의 사용 하 여 hello 서식 파일에서 변수를 다음 hello: azureSqlLinkedServiceName, dataFactoryName 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="4fe1f-216">Azure Blob 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-216">Azure blob dataset</span></span>
<span data-ttu-id="4fe1f-217">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="4fe1f-218">Azure blob 데이터 집합 정의에서는 blob 컨테이너, 폴더 및 hello 입력된 데이터가 포함 된 파일의 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="4fe1f-219">참조 [Azure Blob 데이터 집합 속성](data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="4fe1f-220">Azure SQL 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="4fe1f-220">Azure SQL dataset</span></span>
<span data-ttu-id="4fe1f-221">Hello Azure Blob 저장소에서에서 복사 하는 hello 데이터를 보유 하는 hello Azure SQL 데이터베이스의 hello 테이블의 이름을 hello를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="4fe1f-222">참조 [Azure SQL 데이터 집합 속성](data-factory-azure-sql-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure SQL 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="4fe1f-223">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="4fe1f-223">Data pipeline</span></span>
<span data-ttu-id="4fe1f-224">Hello Azure blob 데이터 집합 toohello Azure SQL 데이터 집합에서 데이터를 복사 하는 파이프라인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="4fe1f-225">참조 [파이프라인 JSON](data-factory-create-pipelines.md#pipeline-json) JSON 사용 되는 요소 toodefine이이 예제에서 파이프라인에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="4fe1f-226">Hello 서식 파일을 다시 사용</span><span class="sxs-lookup"><span data-stu-id="4fe1f-226">Reuse hello template</span></span>
<span data-ttu-id="4fe1f-227">Hello 자습서에서는 데이터 팩터리의 엔터티 및 매개 변수 값을 전달 하기 위한 서식 파일을 정의 하기 위한 서식 파일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="4fe1f-228">hello 파이프라인 매개 변수를 통해 지정 된 Azure 저장소 계정 tooan Azure SQL 데이터베이스에서 데이터를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="4fe1f-229">toouse hello 동일한 템플릿 toodeploy Data Factory 엔터티에 toodifferent 환경, 각 환경에 대 한 매개 변수 파일을 만들고 toothat 환경을 배포 하는 경우 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="4fe1f-230">예제:</span><span class="sxs-lookup"><span data-stu-id="4fe1f-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="4fe1f-231">Hello 첫 번째 명령은 file 매개 변수를 사용 하 여 hello 개발 환경에 대 한, 두 번째 hello에 대 한 환경을 테스트 하 고 hello 프로덕션 환경에 대 한 세 번째 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="4fe1f-232">Hello 템플릿 tooperform 다시 사용할 수도 있습니다 반복 되는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="4fe1f-233">구현 하는 자세한 파이프라인 hello 동일 또는 예를 들어 toocreate 하나를 사용 하는 많은 데이터 팩토리를 필요 논리 하지만 각 데이터 팩터리 다른 SQL 데이터베이스 및 저장소 계정을 사용 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="4fe1f-234">Hello를 사용 하면이 시나리오에서 같은 템플릿을 hello에 다른 매개 변수와 함께 동일한 환경 (개발, 테스트 또는 프로덕션) 파일 toocreate 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="4fe1f-235">다음 단계</span><span class="sxs-lookup"><span data-stu-id="4fe1f-235">Next steps</span></span>
<span data-ttu-id="4fe1f-236">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="4fe1f-237">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="4fe1f-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="4fe1f-238">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="4fe1f-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
