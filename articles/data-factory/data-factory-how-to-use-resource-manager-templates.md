---
title: "Data Factory에서 Resource Manager 템플릿 사용 | Microsoft 문서"
description: "Azure Resource Manager 템플릿을 만들고 사용하여 데이터 팩터리 엔터티를 만드는 방법을 알아봅니다."
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
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="cf76c-103">템플릿을 사용하여 Azure Data Factory 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="cf76c-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="cf76c-104">개요</span><span class="sxs-lookup"><span data-stu-id="cf76c-104">Overview</span></span>
<span data-ttu-id="cf76c-105">데이터 통합 요구에 Azure Data Factory를 사용하면서 다양한 환경에서 동일한 패턴을 재사용하거나 동일한 작업을 동일한 솔루션에서 반복적으로 구현하는 상황이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="cf76c-106">템플릿을 사용하면 이러한 시나리오에서 간편하게 구현 및 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="cf76c-107">Azure Data Factory의 템플릿은 재사용 및 반복이 관계된 시나리오에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="cf76c-108">전 세계에 10개 제조 공장이 있는 조직의 상황을 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="cf76c-109">각 공장의 로그는 개별 온-프레미스 SQL Server 데이터베이스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="cf76c-110">회사에서는 임시 분석을 위해 클라우드에서 단일 데이터 웨어하우스를 구축하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="cf76c-111">또한 논리는 동일하면서 구성은 다른 개발, 테스트 및 프러덕션 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="cf76c-112">이 경우 동일한 환경에서 작업을 반복하지만 각 제조 공장에 대해 서로 다른 값을 갖는 10개 데이터 팩터리가 생깁니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="cf76c-113">실제로 **반복**되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="cf76c-114">템플릿에서는 이 고유 흐름(즉 각 데이터 팩터리에서 동일한 활동의 파이프라인)의 추상이 가능하지만 각 제조 공장마다 별도의 매개 변수 파일을 사용합니다. </span><span class="sxs-lookup"><span data-stu-id="cf76c-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="cf76c-115">나아가 조직이 서로 다른 환경에서 수차례 이 10개 데이터 팩터리를 배포하려 하므로 템플릿은 개발, 테스트 및 프러덕션 환경에 별도의 매개 변수 파일을 적용함으로써 이러한 **재사용성**을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="cf76c-116">Azure Resource Manager의 템플릿</span><span class="sxs-lookup"><span data-stu-id="cf76c-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="cf76c-117">[Azure Resource Manager 템플릿](../azure-resource-manager/resource-group-overview.md#template-deployment)은 Azure Data Factory에서 템플릿을 만드는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="cf76c-118">Resource Manager 템플릿은 JSON 파일을 통해 Azure 솔루션의 인프라와 구성을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="cf76c-119">Azure Resource Manager 템플릿이 모든/대부분의 Azure 서비스에서 작동하므로 광범위한 사용을 통해 Azure 자산의 모든 리소스를 간편하게 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="cf76c-120">Azure Resource Manager 템플릿에 대한 일반적인 내용은 [Azure Resource Manager 템플릿 작성](../azure-resource-manager/resource-group-authoring-templates.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="cf76c-121">자습서</span><span class="sxs-lookup"><span data-stu-id="cf76c-121">Tutorials</span></span>
<span data-ttu-id="cf76c-122">Resource Manager 템플릿을 사용하여 데이터 팩터리 엔터티를 만들기 위한 단계별 지침은 다음 자습서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="cf76c-123">자습서: Azure Resource Manager 템플릿을 사용하여 데이터를 복사하기 위해 파이프라인 생성</span><span class="sxs-lookup"><span data-stu-id="cf76c-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="cf76c-124">자습서: Azure Resource Manager 템플릿을 사용하여 데이터를 처리하기 위해 파이프라인 생성</span><span class="sxs-lookup"><span data-stu-id="cf76c-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="cf76c-125">GitHub의 Data Factory 템플릿</span><span class="sxs-lookup"><span data-stu-id="cf76c-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="cf76c-126">GitHub에서 다음 Azure 빠른 시작 템플릿을 확인해 보세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="cf76c-127">Azure Blob Storage에서 Azure SQL Database로 데이터를 복사하는 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="cf76c-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="cf76c-128">Azure HDInsight 클러스터에서 Hive 활동으로 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="cf76c-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="cf76c-129">Salesforce에서 Azure Blob으로 데이터를 복사하는 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="cf76c-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* <span data-ttu-id="cf76c-130">[작업을 연결하는 Data Factory 만들기](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob): 데이터를 FTP 서버에서 Azure Blob으로 복사하고, 주문형 HDInsight 클러스터의 하이브 스크립트를 호출하여 데이터를 변환하며, Azure SQL Database에 결과를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-130">[Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)</span></span>

<span data-ttu-id="cf76c-131">[Azure 빠른 시작](https://azure.microsoft.com/documentation/templates/)에서 Azure Data Factory를 자유롭게 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="cf76c-132">이 리포지토리를 통해 공유할 수 있는 템플릿을 개발할 때는 [기여 가이드](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="cf76c-133">다음 섹션에서는 Resource Manager 템플릿에서 데이터 팩터리 리소스를 정의하는 것과 관련한 세부 정보를 제공합니다. </span><span class="sxs-lookup"><span data-stu-id="cf76c-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="cf76c-134">템플릿의 데이터 팩터리 리소스 정의</span><span class="sxs-lookup"><span data-stu-id="cf76c-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="cf76c-135">데이터 팩터리 정의를 위한 최상위 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-135">The top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="cf76c-136">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="cf76c-136">Define data factory</span></span>
<span data-ttu-id="cf76c-137">다음 예제에서처럼 Resource Manager 템플릿에서 데이터 팩터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="cf76c-138">dataFactoryName은 “variables”에 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="cf76c-139">연결된 서비스 정의</span><span class="sxs-lookup"><span data-stu-id="cf76c-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="cf76c-140">배포하려는 특정 연결 서비스의 JSON 속성과 관련한 자세한 내용은 [저장소 연결 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) 또는 [연결된 서비스 계산](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="cf76c-141">"DependsOn" 매개 변수는 해당 데이터 팩터리의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="cf76c-142">Azure Storage의 연결 서비스 정의 예제는 다음 JSON 정의에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="cf76c-143">데이터 집합 정의</span><span class="sxs-lookup"><span data-stu-id="cf76c-143">Define datasets</span></span>

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
<span data-ttu-id="cf76c-144">배포할 특정 데이터 집합 형식의 JSON 속성에 관한 자세한 내용은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="cf76c-145">"DependsOn" 매개 변수는 해당 데이터 팩터리와 저장소 연결 서비스의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="cf76c-146">Azure Blob 저장소의 데이터 집합 정의 예제는 다음 JSON 정의에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="cf76c-147">파이프라인 정의</span><span class="sxs-lookup"><span data-stu-id="cf76c-147">Define pipelines</span></span>

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

<span data-ttu-id="cf76c-148">배포할 특정 파이프라인과 활동의 JSON 속성에 대한 자세한 내용은 [파이프라인 정의](data-factory-create-pipelines.md#pipeline-json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="cf76c-149">"dependsOn" 매개 변수는 데이터 팩터리와 해당 연결 서비스 또는 저장소 집합의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="cf76c-150">Azure Blob Storage의 데이터를 Azure SQL Database에 복사하는 파이프라인 예제는 다음 JSON 코드 조각에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="cf76c-151">데이터 팩터리 템플릿 매개 변수화</span><span class="sxs-lookup"><span data-stu-id="cf76c-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="cf76c-152">매개 변수화의 모범 사례는 [Azure Resource Manager 템플릿 만들기 모범 사례](../azure-resource-manager/resource-manager-template-best-practices.md#parameters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cf76c-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="cf76c-153">일반적으로 매개 변수는 최소로 사용해야 합니다. 특히 그 대신 변수를 사용할 수 있는 경우가 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="cf76c-154">다음 시나리오에서는 매개 변수만 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="cf76c-155">설정은 환경에 따라 달라집니다(예: 개발, 테스트, 프러덕션 환경).</span><span class="sxs-lookup"><span data-stu-id="cf76c-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="cf76c-156">암호(Secret)(예: 암호(password))</span><span class="sxs-lookup"><span data-stu-id="cf76c-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="cf76c-157">템플릿을 사용하여 Azure Data Factory 엔터티를 배포할 때 [Azure Key Vault](../key-vault/key-vault-get-started.md)에서 암호를 가져와야 할 경우 다음 예제처럼 **키 자격 증명 모음**과 **암호 이름**을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

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
> <span data-ttu-id="cf76c-158">기존 데이터 팩터리에 대한 템플릿 내보내기는 아직 지원되지 않지만 작업 중에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cf76c-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
