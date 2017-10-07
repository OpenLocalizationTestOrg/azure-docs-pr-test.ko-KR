---
title: "자습서: REST API를 사용 toocreate Azure 데이터 팩터리 파이프라인 | Microsoft Docs"
description: "이 자습서에서는 Azure blob 저장소는 Azure SQL 데이터베이스에서 복사 작업 toocopy 데이터와 함께 REST API toocreate Azure 데이터 팩터리 파이프라인을 사용합니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="9cc1f-103">자습서: REST API를 사용 toocreate Azure 데이터 팩터리 파이프라인 toocopy 데이터</span><span class="sxs-lookup"><span data-stu-id="9cc1f-103">Tutorial: Use REST API toocreate an Azure Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cc1f-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="9cc1f-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9cc1f-105">복사 마법사</span><span class="sxs-lookup"><span data-stu-id="9cc1f-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9cc1f-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="9cc1f-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9cc1f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9cc1f-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9cc1f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cc1f-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9cc1f-109">Azure Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="9cc1f-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9cc1f-110">REST API</span><span class="sxs-lookup"><span data-stu-id="9cc1f-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9cc1f-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="9cc1f-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="9cc1f-112">이 문서에서는 어떻게 toouse REST API toocreate Azure blob 저장소 tooan Azure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인으로 데이터 팩터리 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-112">In this article, you learn how toouse REST API toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="9cc1f-113">새 tooAzure 데이터 팩터리 인 경우 hello 읽어 [소개 tooAzure Data Factory](data-factory-introduction.md) 이 자습서를 수행 하기 전에 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="9cc1f-114">이 자습서에는 한 가지 작업 즉, 복사 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="9cc1f-115">hello 복사 작업 지원 되는 데이터 저장소 tooa 싱크를 지원 되는 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="9cc1f-116">원본 및 싱크로 지원되는 데이터 저장소 목록은 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9cc1f-117">hello 활동은 안전 하 고 안정적 이며 확장 가능한 방식으로 다양 한 데이터 저장소 간에 데이터를 복사할 수 있는 전역적으로 사용 가능한 서비스에 의해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="9cc1f-118">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="9cc1f-119">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="9cc1f-120">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="9cc1f-121">자세한 내용은 [파이프라인의 여러 작업](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="9cc1f-122">이 문서에서 모든 hello 데이터 팩터리 REST API를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-122">This article does not cover all hello Data Factory REST API.</span></span> <span data-ttu-id="9cc1f-123">데이터 팩터리 REST API에 대한 포괄적인 설명서는 [데이터 팩터리 Cmdlet 참조](/rest/api/datafactory/) (영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-123">See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.</span></span>
>  
> <span data-ttu-id="9cc1f-124">이 자습서의 데이터 파이프라인 hello 원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="9cc1f-125">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 tootransform 데이터 참조 [자습서: 빌드 Hadoop 클러스터를 사용 하 여 파이프라인 tootransform 데이터](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9cc1f-126">필수 조건</span><span class="sxs-lookup"><span data-stu-id="9cc1f-126">Prerequisites</span></span>
* <span data-ttu-id="9cc1f-127">통해 이동 [자습서 개요](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) 및 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-127">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="9cc1f-128">컴퓨터에 [Curl](https://curl.haxx.se/dlwiz/) 을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-128">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="9cc1f-129">데이터 팩터리 REST 명령 toocreate와 hello Curl 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-129">You use hello Curl tool with REST commands toocreate a data factory.</span></span> 
* <span data-ttu-id="9cc1f-130">[이 문서](../azure-resource-manager/resource-group-create-service-principal-portal.md) 의 지침에 따라 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-130">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="9cc1f-131">Azure Active Directory에서 **ADFCopyTutorialApp** 이라는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-131">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="9cc1f-132">**클라이언트 ID** 및 **암호 키**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-132">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="9cc1f-133">**테넌트 ID**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-133">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="9cc1f-134">Hello 할당 **ADFCopyTutorialApp** 응용 프로그램 toohello **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-134">Assign hello **ADFCopyTutorialApp** application toohello **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="9cc1f-135">[Azure PowerShell](/powershell/azure/overview)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-135">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="9cc1f-136">시작 **PowerShell** 및 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-136">Launch **PowerShell** and do hello following steps.</span></span> <span data-ttu-id="9cc1f-137">이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-137">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="9cc1f-138">닫고 다시 열 경우 toorun hello 명령을 다시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-138">If you close and reopen, you need toorun hello commands again.</span></span>
  
  1. <span data-ttu-id="9cc1f-139">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-139">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="9cc1f-140">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-140">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="9cc1f-141">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-141">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="9cc1f-142">대체  **&lt;NameOfAzureSubscription** &gt; hello 이름의 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-142">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="9cc1f-143">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="9cc1f-143">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="9cc1f-144">Hello 리소스 그룹이 이미 있는 경우, 지정 여부 tooupdate 것 (Y) 하거나 (N)로 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-144">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="9cc1f-145">이 자습서의 hello 단계 중 일부 ADFTutorialResourceGroup 라는 hello 리소스 그룹을 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-145">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="9cc1f-146">다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-146">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="9cc1f-147">JSON 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-147">Create JSON definitions</span></span>
<span data-ttu-id="9cc1f-148">다음 JSON 파일 curl.exe 위치한 hello 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-148">Create following JSON files in hello folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="9cc1f-149">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-149">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cc1f-150">Tooprefix/접미사 ADFCopyTutorialDF toomake 수 있도록 이름은 전역적으로 고유 해야 하기 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-150">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span> 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="9cc1f-151">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-151">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cc1f-152">**accountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-152">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="9cc1f-153">toolearn 어떻게 tooget 저장소 액세스 키가 참조 [보기, 복사 및 다시 생성 저장소 액세스 키](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-153">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

<span data-ttu-id="9cc1f-154">JSON 속성에 대한 자세한 내용은 [Azure Storage 연결된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-154">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="9cc1f-155">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-155">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cc1f-156">대체 **servername**, **databasename**, **username**, 및 **암호** SQL 데이터베이스의 이름, Azure SQL server의 이름으로 사용자 계정 및 hello 계정의 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-156">Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for hello account.</span></span>  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="9cc1f-157">JSON 속성에 대한 자세한 내용은 [Azure SQL 연결된 서비스](data-factory-azure-sql-connector.md#linked-service-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-157">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="9cc1f-158">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-158">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
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
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="9cc1f-159">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-159">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="9cc1f-160">속성</span><span class="sxs-lookup"><span data-stu-id="9cc1f-160">Property</span></span> | <span data-ttu-id="9cc1f-161">설명</span><span class="sxs-lookup"><span data-stu-id="9cc1f-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9cc1f-162">type</span><span class="sxs-lookup"><span data-stu-id="9cc1f-162">type</span></span> | <span data-ttu-id="9cc1f-163">hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-163">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="9cc1f-164">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9cc1f-164">linkedServiceName</span></span> | <span data-ttu-id="9cc1f-165">Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-165">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="9cc1f-166">folderPath</span><span class="sxs-lookup"><span data-stu-id="9cc1f-166">folderPath</span></span> | <span data-ttu-id="9cc1f-167">Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-167">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="9cc1f-168">이 자습서에서는 adftutorial는 hello blob 컨테이너 및 폴더는 hello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-168">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
| <span data-ttu-id="9cc1f-169">fileName</span><span class="sxs-lookup"><span data-stu-id="9cc1f-169">fileName</span></span> | <span data-ttu-id="9cc1f-170">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-170">This property is optional.</span></span> <span data-ttu-id="9cc1f-171">이 속성을 생략 하는 경우 hello folderPath에서 모든 파일을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-171">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="9cc1f-172">이 자습서에서는 **emp.txt** hello 파일 이름, 해당 파일에만 선택 처리를 위해 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-172">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="9cc1f-173">format -> type</span><span class="sxs-lookup"><span data-stu-id="9cc1f-173">format -> type</span></span> |<span data-ttu-id="9cc1f-174">사용 하도록 hello 입력된 파일은 hello 텍스트 형식 **TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-174">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="9cc1f-175">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="9cc1f-175">columnDelimiter</span></span> | <span data-ttu-id="9cc1f-176">hello 입력된 파일에 hello 열으로 구분 됩니다 **쉼표 문자 (`,`)**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-176">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="9cc1f-177">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9cc1f-177">frequency/interval</span></span> | <span data-ttu-id="9cc1f-178">hello 빈도가 너무 설정**시간** 간격이 너무 설정 되 고**1**, 즉, 해당 hello 입력 분할 영역을 사용할 수 있는 **매시간**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-178">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="9cc1f-179">즉, hello 데이터 팩터리 서비스 검색 입력된 데이터에 대 한 1 시간 마다 blob 컨테이너의 hello 루트 폴더 (**adftutorial**) 사용자가 지정한 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-179">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="9cc1f-180">Hello 파이프라인 시작 및 종료 시간, 날짜부터 또는이 시간 이후로 내의 hello 데이터를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-180">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="9cc1f-181">external</span><span class="sxs-lookup"><span data-stu-id="9cc1f-181">external</span></span> | <span data-ttu-id="9cc1f-182">이 속성은 너무**true** 경우 hello 데이터가이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-182">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="9cc1f-183">이 자습서의 hello 입력된 데이터는 hello emp.txt 파일을 설정 하 여이 속성 tootrue 있으므로이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-183">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

<span data-ttu-id="9cc1f-184">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-184">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="9cc1f-185">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-185">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
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
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="9cc1f-186">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-186">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="9cc1f-187">속성</span><span class="sxs-lookup"><span data-stu-id="9cc1f-187">Property</span></span> | <span data-ttu-id="9cc1f-188">설명</span><span class="sxs-lookup"><span data-stu-id="9cc1f-188">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9cc1f-189">type</span><span class="sxs-lookup"><span data-stu-id="9cc1f-189">type</span></span> | <span data-ttu-id="9cc1f-190">hello type 속성이 너무 설정 되어**AzureSqlTable** 데이터가 Azure SQL 데이터베이스에서 복사 된 tooa 테이블 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-190">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
| <span data-ttu-id="9cc1f-191">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="9cc1f-191">linkedServiceName</span></span> | <span data-ttu-id="9cc1f-192">Toohello 참조 **AzureSqlLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-192">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="9cc1f-193">tableName</span><span class="sxs-lookup"><span data-stu-id="9cc1f-193">tableName</span></span> | <span data-ttu-id="9cc1f-194">지정 된 hello **테이블** toowhich hello 데이터가 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-194">Specified hello **table** toowhich hello data is copied.</span></span> | 
| <span data-ttu-id="9cc1f-195">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="9cc1f-195">frequency/interval</span></span> | <span data-ttu-id="9cc1f-196">hello 주기 설정 너무**시간** 간격은 및 **1**, hello 출력 조각만 생성 되는 것이 즉 **매시간** hello 파이프라인 시작 및 종료 시간, 이전은 아님 사이 또는 이 시간 후.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-196">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="9cc1f-197">세 개의 열인 – **ID**, **FirstName**, 및 **LastName** – hello 데이터베이스의 hello emp 테이블에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-197">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="9cc1f-198">Toospecify만 필요 하므로 ID는 id 열 **FirstName** 및 **LastName** 여기 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-198">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="9cc1f-199">이러한 JSON 속성에 대한 자세한 내용은 [Azure SQL 커넥터 문서](data-factory-azure-sql-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-199">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="9cc1f-200">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="9cc1f-200">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="9cc1f-201">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="9cc1f-201">Note hello following points:</span></span>

- <span data-ttu-id="9cc1f-202">Hello 활동 섹션에는 활동이 하나만 인 **형식** 너무 설정**복사**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-202">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="9cc1f-203">Hello 복사 작업에 대 한 자세한 내용은 참조 [데이터 이동 작업](data-factory-data-movement-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-203">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9cc1f-204">Data Factory 솔루션에서 [데이터 변환 활동](data-factory-data-transformation-activities.md)을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-204">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="9cc1f-205">Hello 활동 너무 설정 되어 입력**AzureBlobInput** 및 hello 활동 너무 설정 되어 출력**AzureSqlOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-205">Input for hello activity is set too**AzureBlobInput** and output for hello activity is set too**AzureSqlOutput**.</span></span> 
- <span data-ttu-id="9cc1f-206">Hello에 **typeProperties** 섹션 **BlobSource** hello 원본 유형으로 지정 된 및 **SqlSink** hello 싱크 유형으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-206">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="9cc1f-207">원본 및 싱크도 hello 복사 작업에서 지 원하는 데이터 저장소의 전체 목록은 참조 하십시오. [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-207">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9cc1f-208">소스/싱크도 toouse 지원 되는 특정 데이터를 저장 하는 방법 toolearn hello 표에 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-208">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
 
<span data-ttu-id="9cc1f-209">Hello hello 값 바꾸기 **시작** hello 현재 날짜를 사용 하 여 속성 및 **끝** 다음날 hello 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-209">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="9cc1f-210">Hello 날짜 부분만 지정 하 고 날짜 시간 hello의 hello 시간 부분을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-210">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="9cc1f-211">예를 들어 "2017-02-03", 즉 너무 "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="9cc1f-211">For example, "2017-02-03", which is equivalent too"2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="9cc1f-212">start 및 end 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-212">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="9cc1f-213">예를 들어 2016-10-14T16:32:41Z입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-213">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="9cc1f-214">hello **끝** 시간 선택 사항 이지만이 자습서에서 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-214">hello **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="9cc1f-215">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간**"입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-215">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="9cc1f-216">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-216">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
 
<span data-ttu-id="9cc1f-217">앞 예제는 hello에서 24 데이터 조각이 각 데이터 조각이 시간 단위로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-217">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="9cc1f-218">파이프라인 정의의 JSON 속성에 대한 설명은 [파이프라인 만들기](data-factory-create-pipelines.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-218">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9cc1f-219">복사 활동 정의의 JSON 속성에 대한 설명은 [데이터 이동 활동](data-factory-data-movement-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-219">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="9cc1f-220">BlobSource에서 지원하는 JSON 속성에 대한 설명은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-220">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="9cc1f-221">SqlSink에서 지원하는 JSON 속성에 대한 설명은 [Azure SQL Database 커넥터 문서](data-factory-azure-sql-connector.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-221">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="9cc1f-222">전역 변수 설정</span><span class="sxs-lookup"><span data-stu-id="9cc1f-222">Set global variables</span></span>
<span data-ttu-id="9cc1f-223">Azure PowerShell에서 명령을 직접 hello 값 바꾼 후 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-223">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cc1f-224">클라이언트 ID, 클라이언트 암호, 테넌트 ID 및 구독 ID를 가져오는 지침은 [필수 구성 요소](#prerequisites) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-224">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

<span data-ttu-id="9cc1f-225">Hello를 사용 하는 hello 데이터 팩터리의 hello 이름을 업데이트 한 후 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-225">Run hello following command after updating hello name of hello data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="9cc1f-226">AAD로 인증</span><span class="sxs-lookup"><span data-stu-id="9cc1f-226">Authenticate with AAD</span></span>
<span data-ttu-id="9cc1f-227">Hello 명령 tooauthenticate와 Azure Active Directory (AAD) 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-227">Run hello following command tooauthenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="9cc1f-228">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-228">Create data factory</span></span>
<span data-ttu-id="9cc1f-229">이 단계에서는 **ADFCopyTutorialDF**라는 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-229">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="9cc1f-230">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-230">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="9cc1f-231">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-231">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="9cc1f-232">예를 들어 복사 작업 toocopy 데이터 소스 tooa 대상 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-232">For example, a Copy Activity toocopy data from a source tooa destination data store.</span></span> <span data-ttu-id="9cc1f-233">HDInsight Hive 활동 toorun 하이브 스크립트 tootransform 데이터 tooproduct 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-233">A HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="9cc1f-234">Hello 명령을 toocreate hello 데이터 팩터리를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-234">Run hello following commands toocreate hello data factory:</span></span> 

1. <span data-ttu-id="9cc1f-235">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-235">Assign hello command toovariable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > <span data-ttu-id="9cc1f-236">여기에서 지정한 일치 하는 항목 (ADFCopyTutorialDF) hello hello에 지정 된 이름이 hello 데이터 팩터리의 hello 이름이 하는지 확인 **datafactory.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-236">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-237">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-237">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-238">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-238">View hello results.</span></span> <span data-ttu-id="9cc1f-239">Hello 데이터 팩토리에 hello에 대 한 JSON hello 참조 hello 데이터 팩터리 성공적으로 생성 된 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-239">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="9cc1f-240">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="9cc1f-240">Note hello following points:</span></span>

* <span data-ttu-id="9cc1f-241">Azure Data Factory hello의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-241">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="9cc1f-242">결과에 hello 오류가 나타나는 경우: **"ADFCopyTutorialDF" 데이터 팩터리 이름을 사용할 수 없으면**, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-242">If you see hello error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do hello following steps:</span></span>  
  
  1. <span data-ttu-id="9cc1f-243">Hello에 hello 이름 변경 (예를 들어 yournameADFCopyTutorialDF) **datafactory.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-243">Change hello name (for example, yournameADFCopyTutorialDF) in hello **datafactory.json** file.</span></span>
  2. <span data-ttu-id="9cc1f-244">Hello 첫 번째 명령은에 있는 hello **$cmd** 변수 ְ ÷ ° × ADFCopyTutorialDF hello 새 이름으로 바꾸고 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-244">In hello first command where hello **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with hello new name and run hello command.</span></span> 
  3. <span data-ttu-id="9cc1f-245">Hello 이후의 두 명령은 tooinvoke hello REST API toocreate hello 데이터 팩터리 및 인쇄 hello hello 작업 결과 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-245">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span> 
     
     <span data-ttu-id="9cc1f-246">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-246">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="9cc1f-247">toocreate 데이터 팩터리 인스턴스 해야 toobe hello Azure 구독 참가자/관리자</span><span class="sxs-lookup"><span data-stu-id="9cc1f-247">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="9cc1f-248">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 있으므로 공개 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-248">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="9cc1f-249">Hello 오류가 나타나면: "**이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-249">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="9cc1f-250">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-250">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="9cc1f-251">데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-251">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="9cc1f-252">Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-252">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="9cc1f-253">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-253">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="9cc1f-254">파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-254">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="9cc1f-255">연결 된 서비스 toolink 소스를 먼저 만들어야 하 고 tooyour 데이터를 저장 하는 대상 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-255">You first create linked services toolink source and destination data stores tooyour data store.</span></span> <span data-ttu-id="9cc1f-256">그런 다음 연결 된 데이터 저장소 모두에서 입력 및 출력 데이터 집합 toorepresent 데이터를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-256">Then, define input and output datasets toorepresent data in linked data stores.</span></span> <span data-ttu-id="9cc1f-257">마지막으로 이러한 데이터 집합을 사용 하는 작업이 있는 hello 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-257">Finally, create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="9cc1f-258">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-258">Create linked services</span></span>
<span data-ttu-id="9cc1f-259">데이터 팩터리 toolink 데이터 저장 및 계산 toohello 데이터 팩터리 서비스에에서 연결 된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-259">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="9cc1f-260">이 자습서에서는 Azure HDInsight 또는 Azure Data Lake Analytics와 같은 계산 서비스를 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-260">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="9cc1f-261">Azure Storage(원본) 및 Azure SQL Database(대상) 유형의 두 데이터 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-261">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="9cc1f-262">이에 따라 두 개의 연결된 서비스, 즉 AzureStorage와 AzureSqlDatabase 유형의 AzureStorageLinkedService와 AzureSqlLinkedService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-262">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="9cc1f-263">AzureStorageLinkedService hello Azure 저장소 계정 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-263">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="9cc1f-264">이 저장소 계정은 hello 하나 컨테이너를 생성 하 고 hello 데이터의 일부로 업로드 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-264">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="9cc1f-265">AzureSqlLinkedService는 Azure SQL 데이터베이스 toohello 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-265">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="9cc1f-266">hello blob 저장소에서 복사 된 hello 데이터는이 데이터베이스에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-266">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="9cc1f-267">이 데이터베이스에 hello emp 테이블의 일부분으로 만든 [필수 구성 요소](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-267">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="9cc1f-268">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-268">Create Azure Storage linked service</span></span>
<span data-ttu-id="9cc1f-269">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-269">In this step, you link your Azure storage account tooyour data factory.</span></span> <span data-ttu-id="9cc1f-270">이 섹션의 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-270">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="9cc1f-271">참조 [Azure 저장소 연결 된 서비스](data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-271">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="9cc1f-272">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-272">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-273">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-273">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-274">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-274">View hello results.</span></span> <span data-ttu-id="9cc1f-275">Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-275">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="9cc1f-276">Azure SQL 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-276">Create Azure SQL linked service</span></span>
<span data-ttu-id="9cc1f-277">이 단계에서는 Azure SQL 데이터베이스 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-277">In this step, you link your Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="9cc1f-278">이 섹션의 hello Azure SQL server 이름, 데이터베이스 이름, 사용자 이름 및 사용자 암호를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-278">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="9cc1f-279">참조 [Azure SQL 연결 된 서비스](data-factory-azure-sql-connector.md#linked-service-properties) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure SQL 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-279">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>

1. <span data-ttu-id="9cc1f-280">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-280">Assign hello command toovariable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-281">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-281">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-282">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-282">View hello results.</span></span> <span data-ttu-id="9cc1f-283">Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-283">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="9cc1f-284">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-284">Create datasets</span></span>
<span data-ttu-id="9cc1f-285">Hello 이전 단계에서 Azure 저장소 계정 및 Azure SQL 데이터베이스 tooyour 데이터 팩터리에 연결 된 서비스 toolink을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-285">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="9cc1f-286">이 단계에서는 AzureBlobInput 및 입력을 나타내는 AzureSqlOutput 각각 AzureStorageLinkedService 및 AzureSqlLinkedService에서 참조 하는 hello 데이터 저장소에 저장 되어 있는 출력 데이터 라는 두 개의 데이터 집합을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-286">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="9cc1f-287">hello Azure 저장소 연결 서비스 런타임에 tooconnect tooyour Azure 저장소 계정에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-287">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9cc1f-288">고 hello 입력된 blob 데이터 집합 (AzureBlobInput) hello 컨테이너 및 hello 입력된 데이터를 포함 하는 hello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-288">And, hello input blob dataset (AzureBlobInput) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="9cc1f-289">마찬가지로, hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-289">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9cc1f-290">및 hello 출력 SQL 테이블의 데이터 집합 (OututDataset) hello blob 저장소에서 데이터를 복사 하는 hello 데이터베이스 toowhich hello에 hello 테이블을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-290">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="9cc1f-291">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-291">Create input dataset</span></span>
<span data-ttu-id="9cc1f-292">이 단계에서는 hello hello AzureStorageLinkedService 연결 된 서비스를 나타내는 Azure 저장소에서에서 blob 컨테이너 (adftutorial)의 hello 루트 폴더에 tooa blob 파일 (emp.txt)를 가리키는 AzureBlobInput 라는 데이터 집합이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-292">In this step, you create a dataset named AzureBlobInput that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="9cc1f-293">하지 hello 파일 이름에 대 한 값을 지정 (하거나 건너뛸 수), 데이터 hello 입력된 폴더의 모든 blob에서 됩니다 복사한 toohello 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-293">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="9cc1f-294">이 자습서에서는 hello 파일 이름에 대 한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-294">In this tutorial, you specify a value for hello fileName.</span></span> 

1. <span data-ttu-id="9cc1f-295">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-295">Assign hello command toovariable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-296">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-296">Run hello command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-297">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-297">View hello results.</span></span> <span data-ttu-id="9cc1f-298">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-298">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="9cc1f-299">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-299">Create output dataset</span></span>
<span data-ttu-id="9cc1f-300">hello 연결 된 Azure SQL 데이터베이스 서비스는 런타임에 tooconnect tooyour Azure SQL 데이터베이스에서 사용 하는 데이터 팩터리 서비스는 hello 연결 문자열을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-300">hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="9cc1f-301">hello 출력 SQL 테이블 데이터 집합 (OututDataset)이이 단계에서 만드는 지정 hello 표 hello 데이터베이스 toowhich hello hello blob 저장소에서 데이터에서를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-301">hello output SQL table dataset (OututDataset) you create in this step specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

1. <span data-ttu-id="9cc1f-302">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-302">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-303">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-303">Run hello command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-304">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-304">View hello results.</span></span> <span data-ttu-id="9cc1f-305">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-305">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="9cc1f-306">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="9cc1f-306">Create pipeline</span></span>
<span data-ttu-id="9cc1f-307">이 단계에서는 **AzureBlobInput**을 입력으로 사용하고 **AzureSqlOutput**을 출력으로 사용하는 **복사 작업**을 포함하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-307">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="9cc1f-308">현재 출력 데이터 집합은 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-308">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="9cc1f-309">이 자습서에서는 출력 데이터 집합은 구성 된 tooproduce 조각을 두 번는 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-309">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="9cc1f-310">hello 파이프라인 시작 시간과 종료 시간이 되는 24 시간 이상 떨어져 1 일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-310">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="9cc1f-311">따라서 출력 데이터 집합의 24 조각은 hello 파이프라인에 의해 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-311">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="9cc1f-312">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-312">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="9cc1f-313">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-313">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="9cc1f-314">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-314">View hello results.</span></span> <span data-ttu-id="9cc1f-315">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-315">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="9cc1f-316">**축하합니다.**</span><span class="sxs-lookup"><span data-stu-id="9cc1f-316">**Congratulations!**</span></span> <span data-ttu-id="9cc1f-317">Azure Blob 저장소 tooAzure SQL 데이터베이스에서 데이터를 복사 하는 파이프라인와 Azure 데이터 팩터리를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-317">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage tooAzure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="9cc1f-318">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="9cc1f-318">Monitor pipeline</span></span>
<span data-ttu-id="9cc1f-319">이 단계에서는 hello 파이프라인에 의해 생성 되는 데이터 팩터리 REST API toomonitor 분할 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-319">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> <span data-ttu-id="9cc1f-320">Hello 시작 및 종료 시간 뒤에 지정 된 hello 명령 일치 hello 시작 및 종료 시간 hello 파이프라인의 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-320">Make sure that hello start and end times specified in hello following command match hello start and end times of hello pipeline.</span></span> 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="9cc1f-321">실행 Invoke-command hello 및 hello 다음에 있는 분할 영역에 표시 될 때까지 **준비** 상태 또는 **실패** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-321">Run hello Invoke-Command and hello next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="9cc1f-322">Hello 조각 준비 상태에 있으면 확인 hello **emp** hello 출력 데이터에 대 한 Azure SQL 데이터베이스의 테이블에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-322">When hello slice is in Ready state, check hello **emp** table in your Azure SQL database for hello output data.</span></span> 

<span data-ttu-id="9cc1f-323">각 조각에 대 한 hello 소스 파일에서 데이터의 두 행이 hello Azure SQL 데이터베이스에서 복사 된 toohello emp 테이블 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-323">For each slice, two rows of data from hello source file are copied toohello emp table in hello Azure SQL database.</span></span> <span data-ttu-id="9cc1f-324">따라서 모든 hello 분할 영역 (준비 상태)에 성공적으로 처리 되 면 hello emp 테이블에 새 레코드를 24 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-324">Therefore, you see 24 new records in hello emp table when all hello slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="9cc1f-325">요약</span><span class="sxs-lookup"><span data-stu-id="9cc1f-325">Summary</span></span>
<span data-ttu-id="9cc1f-326">이 자습서에서는 REST API toocreate Azure blob tooan Azure SQL 데이터베이스에서 Azure 데이터 팩터리 toocopy 데이터를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-326">In this tutorial, you used REST API toocreate an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="9cc1f-327">이 자습서에서 수행 하는 hello 상위 수준 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-327">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="9cc1f-328">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-328">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="9cc1f-329">**연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-329">Created **linked services**:</span></span>
   1. <span data-ttu-id="9cc1f-330">Azure 저장소 입력된 데이터를 보유 하는 Azure 저장소 계정의 서비스 toolink에 연결 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-330">An Azure Storage linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="9cc1f-331">Azure SQL 서비스 toolink hello 출력 데이터를 보유 하 여 Azure SQL 데이터베이스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-331">An Azure SQL linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="9cc1f-332">파이프라인의 입력 데이터와 출력 데이터를 설명하는 **데이터 집합**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-332">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="9cc1f-333">원본인 BlobSource와 싱크인 SqlSink를 사용하여 복사 작업으로 **파이프라인** 을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-333">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9cc1f-334">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9cc1f-334">Next steps</span></span>
<span data-ttu-id="9cc1f-335">이 자습서에서는 Azure Blob 저장소를 원본 데이터 저장소로 사용하고 Azure SQL 데이터베이스를 복사 작업의 대상 데이터 저장소로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-335">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9cc1f-336">hello 다음 표에서 hello 복사 작업에서 원본과 대상으로 지 원하는 데이터 저장소는 목록:</span><span class="sxs-lookup"><span data-stu-id="9cc1f-336">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9cc1f-337">toolearn toocopy 데이터는 데이터를 저장 하는 방법에 대 한 hello 테이블에서 데이터 저장소에 hello에 대 한 hello 링크를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9cc1f-337">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
