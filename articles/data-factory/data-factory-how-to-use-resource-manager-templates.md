---
title: "Data Factory에 aaaUse 리소스 관리자 템플릿을 | Microsoft Docs"
description: "자세한 내용은 방법 toocreate 및 사용 하 여 Azure 리소스 관리자 템플릿 toocreate Data Factory 엔터티에 합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="35502-103">템플릿 toocreate Azure Data Factory 엔터티를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="35502-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="35502-104">개요</span><span class="sxs-lookup"><span data-stu-id="35502-104">Overview</span></span>
<span data-ttu-id="35502-105">서로 다른 환경에서 동일한 패턴을 hello 재사용을 직접 데이터 통합 요구 사항에 대 한 Azure 데이터 팩터리를 사용 하는 동안 하거나 hello 구현 동일한 태스크를 반복 해 서 hello 내에서 동일한 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="35502-106">템플릿을 사용하면 이러한 시나리오에서 간편하게 구현 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35502-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="35502-107">Azure Data Factory의 템플릿은 재사용 및 반복이 관계된 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="35502-108">Hello 상황을 hello 전 세계 조직 10 제조 공장에 있는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="35502-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="35502-109">각 식물에서 hello 로그는 별도 온-프레미스 SQL Server 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="35502-110">hello 회사 toobuild hello 클라우드에서는 단일 데이터 웨어하우스에 대 한 임시 분석 하려고합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="35502-111">Toohave 있었으면 hello 동일한 논리 하지만 개발, 테스트 및 프로덕션 환경에 대 한 다양 한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="35502-112">반복 toobe는 작업을 수행 하는 경우에 내 동일한 환경 hello 하지만 간에 서로 다른 값으로 hello 각 제조 공장에 대 한 10 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="35502-113">실제로 **반복**되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="35502-114">템플릿 허용 hello 추상화 하 여이 일반 흐름 (즉, 파이프라인 hello 있는 각 데이터 팩터리에서 동일한 활동), 하지만 각 제조 공장에 대 한 별도 매개 변수 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="35502-115">또한 hello 조직이 toodeploy 이러한 10 개의 데이터 팩터리 여러 번 서로 다른 환경에서 템플릿을 사용할 수이 **재사용성** 개발을 위한 별도 매개 변수 파일을 사용 하 여 테스트 하 고 프로덕션 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="35502-116">Azure Resource Manager의 템플릿</span><span class="sxs-lookup"><span data-stu-id="35502-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="35502-117">[Azure 리소스 관리자 템플릿](../azure-resource-manager/resource-group-overview.md#template-deployment) Azure Data Factory에는 훌륭한 방법 tooachieve 템플릿 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="35502-118">리소스 관리자 템플릿 JSON 파일을 통해 hello 인프라 및 Azure 솔루션의 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="35502-119">Azure 리소스 관리자 템플릿을 모든/대부분 Azure 서비스를 사용 하기 때문에 광범위 하 게 사용할 수 tooeasily Azure 자산의 모든 리소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="35502-120">참조 [제작 Azure 리소스 관리자 템플릿을](../azure-resource-manager/resource-group-authoring-templates.md) toolearn에 더 알아봅니다 hello 리소스 관리자 템플릿을 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="35502-121">자습서</span><span class="sxs-lookup"><span data-stu-id="35502-121">Tutorials</span></span>
<span data-ttu-id="35502-122">리소스 관리자 템플릿을 사용 하 여 toocreate Data Factory 엔터티에 대 한 단계별 지침에 대 한 자습서를 따라 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="35502-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="35502-123">자습서: Azure 리소스 관리자 템플릿을 사용 하 여 파이프라인 toocopy 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="35502-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="35502-124">자습서: Azure 리소스 관리자 템플릿을 사용 하 여 파이프라인 tooprocess 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="35502-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="35502-125">GitHub의 Data Factory 템플릿</span><span class="sxs-lookup"><span data-stu-id="35502-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="35502-126">Azure 빠른 시작 서식 파일에 나오는 GitHub에 hello 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="35502-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="35502-127">Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 데이터 팩터리 toocopy 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="35502-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="35502-128">Azure HDInsight 클러스터에서 Hive 활동으로 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="35502-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="35502-129">Salesforce tooAzure Blob에서 데이터 팩터리 toocopy 데이터 만들기</span><span class="sxs-lookup"><span data-stu-id="35502-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="35502-130">활동을 연결 하는 데이터 팩터리 만들기: FTP 서버에서 데이터를 복사 tooAzure Blob는 주문형 HDInsight 클러스터 tootransform hello 데이터에서 하이브 스크립트를 호출 하 고 Azure SQL 데이터베이스에 결과 복사</span><span class="sxs-lookup"><span data-stu-id="35502-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="35502-131">무료 tooshare에서 Azure Data Factory 템플릿을 느껴집니다 [Azure 빠른 시작](https://azure.microsoft.com/documentation/templates/)합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="35502-132">Toohello 참조 [기여 가이드](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) 서식 파일에서이 리포지토리를 통해 공유할 수 있는 개발 하는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="35502-133">hello 다음 섹션에는 리소스 관리자 템플릿을 Data Factory 리소스를 정의 하는 방법에 대 한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="35502-134">템플릿의 데이터 팩터리 리소스 정의</span><span class="sxs-lookup"><span data-stu-id="35502-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="35502-135">데이터 팩터리를 정의 하기 위한 hello 최상위 서식 파일은입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-135">hello top-level template for defining a data factory is:</span></span>

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a><span data-ttu-id="35502-136">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="35502-136">Define data factory</span></span>
<span data-ttu-id="35502-137">Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="35502-138">hello dataFactoryName로 "변수"에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="35502-139">연결된 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="35502-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="35502-140">참조 [저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [계산 연결 된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 원하는 toodeploy hello 특정 연결 된 서비스에 대 한 hello JSON 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="35502-141">hello "dependsOn" 매개 변수는 hello 해당 데이터 팩터리의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="35502-142">Azure 저장소에 대 한 연결 된 서비스 정의의 예로 hello JSON 정의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="35502-143">데이터 집합 정의</span><span class="sxs-lookup"><span data-stu-id="35502-143">Define datasets</span></span>

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
<span data-ttu-id="35502-144">너무 참조[데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원하는 toodeploy hello 특정 데이터 집합 형식에 대 한 hello JSON 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="35502-145">참고 hello "dependsOn" 매개 변수는 hello 해당 데이터의 이름을 지정 합니다. 팩터리 및 저장소 서비스에 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="35502-146">Azure blob 저장소의 데이터 집합 형식 정의의 예로 hello JSON 정의 뒤에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a><span data-ttu-id="35502-147">파이프라인 정의</span><span class="sxs-lookup"><span data-stu-id="35502-147">Define pipelines</span></span>

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

<span data-ttu-id="35502-148">너무 참조[파이프라인 정의](data-factory-create-pipelines.md#pipeline-json) toodeploy 원하는 특정 파이프라인 및 활동을 정의 하기 위한 hello JSON 속성에 대 한 세부 정보 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="35502-149">참고 hello "dependsOn" 매개 변수는 hello 데이터 팩터리의 이름 및 해당 연결 된 서비스 또는 데이터 집합을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="35502-150">Azure Blob 저장소 tooAzure SQL 데이터베이스에서에서 데이터를 복사 하는 파이프라인의 예는 다음 JSON 코드 조각은 hello에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35502-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="35502-151">데이터 팩터리 템플릿 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="35502-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="35502-152">매개 변수화의 모범 사례는 [Azure Resource Manager 템플릿 만들기 모범 사례](../azure-resource-manager/resource-manager-template-best-practices.md#parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="35502-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="35502-153">일반적으로 매개 변수는 최소로 사용해야 합니다. 특히 그 대신 변수를 사용할 수 있는 경우가 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="35502-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="35502-154">만 hello 다음 시나리오에서에서 매개 변수를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="35502-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="35502-155">설정은 환경에 따라 달라집니다(예: 개발, 테스트, 프러덕션 환경).</span><span class="sxs-lookup"><span data-stu-id="35502-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="35502-156">암호(Secret)(예: 암호(password))</span><span class="sxs-lookup"><span data-stu-id="35502-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="35502-157">toopull 비밀 해야 할 경우 [Azure 키 자격 증명 모음](../key-vault/key-vault-get-started.md) 템플릿을 사용 하 여 Azure Data Factory 엔터티를 배포할 때 지정 hello **주요 자격 증명 모음** 및 **암호 이름이** 에 표시 된 대로 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="35502-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> <span data-ttu-id="35502-158">기존 데이터 팩터리에 대 한 템플릿 내보내기는 현재 지원 되지 않고 아직, hello works입니다.</span><span class="sxs-lookup"><span data-stu-id="35502-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
