---
title: "Data Factory를 사용하여 주문형 Hadoop 클러스터 만들기 - Azure HDInsight | Microsoft Docs"
description: "Azure Data Factory를 사용하여 HDInsight에서 주문형 Hadoop 클러스터를 만드는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="51d44-103">Azure Data Factory를 사용하여 HDInsight에서 주문형 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="51d44-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) 는 데이터의 이동과 변환을 조율하고 자동화하는 클라우드 기반의 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="51d44-105">입력 데이터 조각을 처리하고 처리가 완료되면 클러스터를 삭제하기 위해 HDInsight Hadoop 클러스터를 적시에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="51d44-106">주문형 HDInsight Hadoop 클러스터를 사용할 때의 이점은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="51d44-107">HDInsight Hadoop 클러스터에서 실행 중인 작업(및 간략히 구성 가능한 유휴 시간)에만 시간을 할애합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="51d44-108">HDInsight 클러스터에 대한 결제는 사용 여부에 관계없이 분당으로 비례 배분됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="51d44-109">Data Factory에서 주문형 HDInsight 연결된 서비스를 사용할 때 클러스터는 주문 시 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="51d44-110">그리고 작업이 완료되면 클러스터가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="51d44-111">따라서 작업 실행 시간 및 잠깐의 유휴 시간(TTL 설정)에 대해서만 지불합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="51d44-112">Data Factory 파이프라인을 사용하여 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="51d44-113">예를 들어 온-프레미스 SQL Server에서 Azure Blob Storage로 데이터를 복사하는 파이프라인을 포함하고 주문형 HDInsight Hadoop 클러스터에서 Hive 스크립트 및 Pig 스크립트를 실행하여 데이터를 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="51d44-114">그런 다음 결과 데이터를 사용할 BI 응용 프로그램에 대한 Azure SQL Data Warehouse에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="51d44-115">주기적(매시간, 매일, 매주, 매월 등)으로 워크플로 실행을 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="51d44-116">Azure Data Factory에서 데이터 팩터리에는 하나 이상의 데이터 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="51d44-117">데이터 파이프라인은 하나 이상의 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="51d44-118">두 가지 유형의 활동이 있으며 [데이터 이동 활동](../data-factory/data-factory-data-movement-activities.md) 및 [데이터 변환 활동](../data-factory/data-factory-data-transformation-activities.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="51d44-119">데이터 이동 활동(현재는, 복사 작업만)을 사용하여 원본 데이터 저장소에서 대상 데이터 저장소로 데이터를 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="51d44-120">데이터 변환 활동을 사용하여 데이터를 변환/처리합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="51d44-121">HDInsight Hive 작업은 Data Factory에서 지원하는 데이터 변환 활동 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="51d44-122">이 자습서에서는 Hive 변환 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="51d44-123">고유한 HDInsight Hadoop 클러스터 또는 주문형 HDInsight Hadoop 클러스터를 사용하도록 hive 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="51d44-124">이 자습서에서 데이터 팩터리 파이프라인의 Hive 작업은 주문형 HDInsight 클러스터를 사용하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="51d44-125">따라서 데이터 조각을 처리하기 위해 작업을 실행하면 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="51d44-126">조각을 처리하기 위해 HDInsight Hadoop 클러스터가 자동으로 적시에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="51d44-127">입력 데이터는 클러스터에서 HiveQL 스크립트를 실행하여 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="51d44-128">처리가 완료된 후 HDInsight Hadoop 클러스터가 삭제되고 클러스터는 구성된 시간(timeToLive 설정) 동안 유휴 상태입니다</span><span class="sxs-lookup"><span data-stu-id="51d44-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="51d44-129">이 timeToLive 유휴 시간에 처리를 위해 다음 데이터 조각이 제공되면 조각을 처리하는 데 동일한 클러스터가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="51d44-130">이 자습서에서 hive 작업과 관련된 HiveQL 스크립트는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="51d44-131">Azure Blob Storage에 저장된 원시 웹 로그 데이터를 참조하는 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="51d44-132">원시 데이터를 연도별, 월별로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="51d44-133">분할된 데이터를 Azure Blob Storage에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="51d44-134">이 자습서에서 hive 작업과 관련된 HiveQL 스크립트는 Azure Blob Storage에 저장된 원시 웹 로그 데이터를 참조하는 외부 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="51d44-135">다음은 입력 파일의 각 월에 대한 샘플 행입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="51d44-136">HiveQL 스크립트는 원시 데이터를 연도별, 월별로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="51d44-137">이전 입력을 기반으로 세 개의 출력 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="51d44-138">각 폴더에는 각 월의 항목과 함께 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="51d44-139">Hive 작업 외에도 데이터 팩터리의 데이터 변환 활동 목록은 [Azure Data Factory를 사용한 분석 및 변환](../data-factory/data-factory-data-transformation-activities.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="51d44-140">현재, Azure Data Factory에서 HDInsight 클러스터 버전 3.2 만들기만 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51d44-141">필수 조건</span><span class="sxs-lookup"><span data-stu-id="51d44-141">Prerequisites</span></span>
<span data-ttu-id="51d44-142">이 문서의 지침을 시작하기 전에 다음 항목이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="51d44-143">[Azure 구독](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="51d44-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="51d44-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51d44-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="51d44-145">저장소 계정 준비</span><span class="sxs-lookup"><span data-stu-id="51d44-145">Prepare storage account</span></span>
<span data-ttu-id="51d44-146">이 시나리오에서는 최대 3개의 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="51d44-147">HDInsight 클러스터에 대한 기본 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="51d44-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="51d44-148">입력 데이터에 대한 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="51d44-148">storage account for the input data</span></span>
- <span data-ttu-id="51d44-149">출력 데이터에 대한 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="51d44-149">storage account for the output data</span></span>

<span data-ttu-id="51d44-150">자습서를 간단하게 만들기 위해 1개의 저장소 계정을 3가지 용도로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="51d44-151">이 섹션에 있는 Azure PowerShell 샘플 스크립트는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="51d44-152">Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-152">Log in to Azure.</span></span>
2. <span data-ttu-id="51d44-153">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="51d44-154">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="51d44-155">저장소 계정에 Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="51d44-156">Blob 컨테이너에 다음 두 파일 복사</span><span class="sxs-lookup"><span data-stu-id="51d44-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="51d44-157">입력 데이터 파일: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="51d44-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="51d44-158">HiveQL 스크립트: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="51d44-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="51d44-159">두 파일은 공용 Blob 컨테이너에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="51d44-160">**저장소를 준비하고 Azure PowerShell을 사용하여 파일을 복사하려면**</span><span class="sxs-lookup"><span data-stu-id="51d44-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="51d44-161">스크립트로 생성될 Azure 리소스 그룹 및 Azure Storage 계정 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="51d44-162">스크립트에 출력된 **리소스 그룹 이름**, **저장소 계정 이름** 및 **저장소 계정 키**를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="51d44-163">다음 섹션에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="51d44-164">PowerShell 스크립트에 대해 도움이 필요한 경우 [Azure Storage에서 Azure PowerShell 사용](../storage/common/storage-powershell-guide-full.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="51d44-165">대신 Azure CLI를 사용하려는 경우 Azure CLI 스크립트에 대한 [부록](#appendix) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="51d44-166">**저장소 계정 및 그 내용을 검사하려면**</span><span class="sxs-lookup"><span data-stu-id="51d44-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="51d44-167">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="51d44-168">왼쪽 창에서 **리소스 그룹** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="51d44-169">PowerShell 스크립트에서 만든 리소스 그룹 이름을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="51d44-170">나열된 리소스 그룹이 너무 많은 경우 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="51d44-171">**리소스** 타일에서 리소스 그룹을 다른 프로젝트와 공유하지 않는 한 하나의 리소스가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="51d44-172">그 리소스는 이전에 지정한 이름의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="51d44-173">저장소 계정 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-173">Click the storage account name.</span></span>
5. <span data-ttu-id="51d44-174">**Blob** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="51d44-175">**adfgetstarted** 컨테이너를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="51d44-176">**inputdata** 및 **script**라는 두 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="51d44-177">폴더를 열고 폴더에서 파일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="51d44-178">inputdata에는 입력 데이터가 있는 input.log 파일이 포함되며 스크립트 폴더에는 HiveQL 스크립트 파일이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="51d44-179">Resource Manager 템플릿을 사용하여 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="51d44-180">저장소 계정, 입력 데이터 및 HiveQL 스크립트가 준비되었으면 Azure Data Factory를 만들 준비가 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="51d44-181">데이터 팩터리는 여러 가지 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="51d44-182">이 자습서에서는 Azure Portal을 사용하여 Azure Resource Manager 템플릿을 배포하여 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="51d44-183">또한 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 및 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)을 사용하여 Resource Manager 템플릿을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="51d44-184">기타 데이터 팩터리 만들기 방법은 [자습서: 첫 번째 데이터 팩터리 빌드](../data-factory/data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="51d44-185">Azure에 로그인하여 Azure Portal에서 Azure Resource Manager 템플릿을 열려면 다음 이미지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="51d44-186">템플릿은 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="51d44-187">템플릿에 정의된 엔터티에 대한 자세한 내용은 [템플릿의 Data Factory 엔터티](#data-factory-entities-in-the-template) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="51d44-188">**리소스 그룹** 설정에 대해 **Use existing**(기존 항목 사용) 옵션을 선택하고 이전 단계에서 만든 리소스 그룹의 이름을 선택합니다(PowerShell 스크립트 사용).</span><span class="sxs-lookup"><span data-stu-id="51d44-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="51d44-189">데이터 팩터리의 이름(**Data Factory Name**)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="51d44-190">이 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="51d44-191">이전 단계에서 기록해 둔 **저장소 계정 이름** 및 **저장소 계정 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="51d44-192">**사용 약관**을 읽은 다음 위에 명시된 **사용 약관에 동의함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="51d44-193">**대시보드에 고정** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="51d44-194">**구매/만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="51d44-195">대시보드에 **템플릿 배포 중**이라는 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="51d44-196">리소스 그룹에 대한 **리소스 그룹** 블레이드가 열릴 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="51d44-197">리소스 그룹 이름이 제목으로 표시된 타일을 클릭하여 리소스 그룹 블레이드를 열 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="51d44-198">리소스 그룹 블레이드가 아직 열리지 않은 경우 타일을 클릭하여 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="51d44-199">이제 저장소 계정 리소스 외에 하나 이상의 데이터 팩터리 리소스가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="51d44-200">데이터 팩터리의 이름을 클릭합니다(**Data Factory Name** 매개 변수에 대해 지정한 값).</span><span class="sxs-lookup"><span data-stu-id="51d44-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="51d44-201">Data Factory 블레이드에서 **다이어그램** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="51d44-202">다이어그램은 입력 데이터 집합 및 출력 데이터 집합이 있는 하나의 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 다이어그램](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="51d44-204">이름은 Resource Manager 템플릿에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="51d44-205">**AzureBlobOutput**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="51d44-206">**최근 업데이트된 조각**에 하나의 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="51d44-207">상태가 **진행 중**이면 **준비**로 변경될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="51d44-208">HDInsight 클러스터를 만들려면 보통 약 **20분** 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="51d44-209">데이터 팩터리 출력 확인</span><span class="sxs-lookup"><span data-stu-id="51d44-209">Check the data factory output</span></span>

1. <span data-ttu-id="51d44-210">마지막 세션에서와 동일한 절차를 사용하여 Adfgetstarted 컨테이너의 컨테이너들을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="51d44-211">**adfgetsarted**외에도 두 개의 새 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="51d44-212">`adf<yourdatafactoryname>-linkedservicename-datetimestamp` 패턴을 따르는 이름을 가진 컨테이너.</span><span class="sxs-lookup"><span data-stu-id="51d44-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="51d44-213">이 컨테이너는 HDInsight 클러스터의 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="51d44-214">adfjobs: 이 컨테이너는 ADF 작업 로그에 대한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="51d44-215">데이터 팩터리 출력은 Resource Manager 템플릿에 구성된 대로 **afgetstarted**에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="51d44-216">**adfgetstarted**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="51d44-217">**partitioneddata**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="51d44-218">모든 웹 로그가 2014년에 지정되었으므로 **year=2014** 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="51d44-220">목록을 드릴다운하면 1월, 2월 및 3월에 대한 3개 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="51d44-221">각 월에 대한 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="51d44-223">템플릿의 데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="51d44-223">Data Factory entities in the template</span></span>
<span data-ttu-id="51d44-224">데이터 팩터리를 위한 최상위 Resource Manager 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
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

### <a name="define-data-factory"></a><span data-ttu-id="51d44-225">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="51d44-225">Define data factory</span></span>
<span data-ttu-id="51d44-226">다음 예제에서처럼 Resource Manager 템플릿에서 데이터 팩터리를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="51d44-227">dataFactoryName은 템플릿을 배포할 때 지정하는 데이터 팩터리의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="51d44-228">데이터 팩터리는 현재 미국 동부, 미국 서부 및 북유럽 하위 지역에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="51d44-229">데이터 팩터리 내에서 엔터티 정의</span><span class="sxs-lookup"><span data-stu-id="51d44-229">Defining entities within the data factory</span></span>
<span data-ttu-id="51d44-230">다음 데이터 팩터리 엔터티는 JSON 템플릿에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="51d44-231">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="51d44-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="51d44-232">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="51d44-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="51d44-233">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="51d44-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="51d44-234">Azure Blob 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="51d44-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="51d44-235">복사 작업을 포함하는 데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="51d44-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="51d44-236">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="51d44-236">Azure Storage linked service</span></span>
<span data-ttu-id="51d44-237">Azure Storage 연결된 서비스는 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="51d44-238">이 자습서에서는 기본 HDInsight 저장소 계정, 입력 데이터 저장소 및 출력 데이터 저장소로 동일한 저장소 계정이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="51d44-239">따라서 Azure Storage 연결된 서비스 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="51d44-240">연결된 서비스 정의에서 Azure Storage 계정의 이름 및 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="51d44-241">Azure Storage 연결된 서비스를 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Storage 연결된 서비스](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="51d44-242">**connectionString**은 storageAccountName 및 storageAccountKey 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="51d44-243">템플릿을 배포하는 동안 다음 매개 변수 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="51d44-244">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="51d44-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="51d44-245">주문형 HDInsight 연결된 서비스 정의에서 Data Factory 서비스에 사용된 구성 매개 변수에 대한 값을 지정하여 런타임에 HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="51d44-246">HDInsight 주문형 연결된 서비스를 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [연결된 서비스 계산](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="51d44-247">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-247">Note the following points:</span></span>

* <span data-ttu-id="51d44-248">Data Factory는 사용자 대신 **Linux 기반** HDInsight 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="51d44-249">HDInsight Hadoop 클러스터는 저장소 계정과 동일한 지역에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="51d44-250">*timeToLive* 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="51d44-251">데이터 팩터리는 클러스터가 30분 동안 유휴 상태가 지속되면 클러스터를 자동으로 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="51d44-252">HDInsight 클러스터는 JSON(**linkedServiceName**)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="51d44-253">HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="51d44-254">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-254">This behavior is by design.</span></span> <span data-ttu-id="51d44-255">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리해야 할 때마다 HDInsight 클러스터가 만들어지며 처리가 완료되면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="51d44-256">자세한 내용은 [주문형 HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51d44-257">많은 조각이 처리될수록 Azure Blob 저장소에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="51d44-258">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="51d44-259">이 컨테이너의 이름은 "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp" 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="51d44-260">[Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob 저장소에서 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="51d44-261">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="51d44-261">Azure blob input dataset</span></span>
<span data-ttu-id="51d44-262">입력 데이터 집합 정의에서 입력 데이터를 포함하는 Blob 컨테이너, 폴더 및 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="51d44-263">Azure Blob 데이터 집합을 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="51d44-264">JSON 정의에서 다음과 같은 특정 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="51d44-265">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="51d44-265">Azure Blob output dataset</span></span>
<span data-ttu-id="51d44-266">출력 데이터 집합 정의에서 출력 데이터를 포함하는 Blob 컨테이너 및 폴더의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="51d44-267">Azure Blob 데이터 집합을 정의하는 데 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="51d44-268">folderPath는 출력 데이터를 포함하는 폴더에 대한 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="51d44-269">[데이터 집합 가용성](../data-factory/data-factory-create-datasets.md#dataset-availability) 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="51d44-270">Azure Data Factory에서 출력 데이터 집합 가용성이 파이프라인을 유도합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="51d44-271">이 예에서, 월의 마지막 날(EndOfInterval)에 조각이 매달 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="51d44-272">자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="51d44-273">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="51d44-273">Data pipeline</span></span>
<span data-ttu-id="51d44-274">주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터를 변환하는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="51d44-275">이 예에서 파이프라인을 정의하는 데 사용된 JSON 요소에 대한 자세한 설명은 [파이프라인 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="51d44-276">파이프라인에는 HDInsightHive 작업 한 가지가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="51d44-277">시작 및 종료 날짜 모두 2016년 1월에 있으므로 한 달에 대한 데이터(조각)만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="51d44-278">작업에 대한 *start* 및 *end*가 모두 과거 날짜이므로 Data Factory는 해당 월에 대한 데이터를 즉시 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="51d44-279">end가 미래 날짜이면 데이터 팩터리는 시간이 되면 다른 조각을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="51d44-280">자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="51d44-281">자습서 정리</span><span class="sxs-lookup"><span data-stu-id="51d44-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="51d44-282">주문형 HDInsight 클러스터에 생성된 Blob 컨테이너 삭제</span><span class="sxs-lookup"><span data-stu-id="51d44-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="51d44-283">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 한 조각을 처리해야 할 때마다 HDInsight 클러스터가 만들어지며 처리가 완료되면 클러스터가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="51d44-284">각 클러스터에 대해 Azure Data Factory는 클러스터에 대한 기본 저장소 계정으로 사용되는 Azure Blob Storage에 Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="51d44-285">HDInsight 클러스터가 삭제되어도 기본 Blob 저장소 컨테이너와 연결된 저장소 계정은 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="51d44-286">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-286">This behavior is by design.</span></span> <span data-ttu-id="51d44-287">많은 조각이 처리될수록 Azure Blob 저장소에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="51d44-288">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="51d44-289">이러한 컨테이너의 이름은 `adfyourdatafactoryname-linkedservicename-datetimestamp` 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="51d44-290">**adfjobs** 및 **adfyourdatafactoryname-linkedservicename-datetimestamp** 폴더를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="51d44-291">adfjobs 컨테이너는 Azure Data Factory의 작업 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="51d44-292">리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="51d44-292">Delete the resource group</span></span>
<span data-ttu-id="51d44-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)는 솔루션을 그룹으로 배포, 관리 및 모니터링하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="51d44-294">리소스 그룹을 삭제하면 그룹 내의 모든 구성 요소가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="51d44-295">[Azure 포털](https://portal.azure.com)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="51d44-296">왼쪽 창에서 **리소스 그룹** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="51d44-297">PowerShell 스크립트에서 만든 리소스 그룹 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="51d44-298">나열된 리소스 그룹이 너무 많은 경우 필터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="51d44-299">새 블레이드에서 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="51d44-300">**리소스** 타일에서 리소스 그룹을 다른 프로젝트와 공유하지 않는 한 기본 저장소 계정과 데이터 팩터리가 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="51d44-301">블레이드 맨 위의 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="51d44-302">이렇게 하면 저장소 계정 및 저장소 계정에 저장된 데이터도 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="51d44-303">삭제를 확인하려면 리소스 그룹 이름을 입력하고 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="51d44-304">리소스 그룹을 삭제할 때 저장소 계정을 삭제하지 않으려는 경우 기본 저장소 계정에서 비즈니스 데이터를 구분하여 다음 아키텍처를 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="51d44-305">이 경우 비즈니스 데이터가 있는 저장소 계정에 대해 하나의 리소스 그룹을 포함하고 HDInsight 연결된 서비스용 기본 저장소 계정 및 데이터 팩터리에 대해 다른 리소스 그룹을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="51d44-306">두 번째 리소스 그룹을 삭제할 경우 비즈니스 데이터 저장소 계정에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="51d44-307">이렇게 하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-307">To do so:</span></span>

* <span data-ttu-id="51d44-308">다음을 Resource Manager 템플릿에서 Microsoft.DataFactory/datafactories 리소스와 함께 최상위 수준 리소스 그룹에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="51d44-309">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="51d44-310">새 저장소 계정에 새 연결된 서비스 지점을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="51d44-311">추가 dependsOn 및 additionalLinkedServiceNames로 HDInsight 주문형 연결된 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="51d44-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="51d44-312">Next steps</span></span>
<span data-ttu-id="51d44-313">이 문서에서는 Azure Data Factory를 사용하여 주문형 HDInsight 클러스터를 만들고 Hive 작업을 처리하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="51d44-314">자세히 알아보려면 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-314">To read more:</span></span>

* [<span data-ttu-id="51d44-315">Hadoop 자습서: HDInsight에서 Linux 기반 Hadoop 사용 시작</span><span class="sxs-lookup"><span data-stu-id="51d44-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="51d44-316">HDInsight에서 Linux 기반 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="51d44-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="51d44-317">HDInsight 설명서</span><span class="sxs-lookup"><span data-stu-id="51d44-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="51d44-318">데이터 팩터리 설명서</span><span class="sxs-lookup"><span data-stu-id="51d44-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="51d44-319">부록</span><span class="sxs-lookup"><span data-stu-id="51d44-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="51d44-320">Azure CLI 스크립트</span><span class="sxs-lookup"><span data-stu-id="51d44-320">Azure CLI script</span></span>
<span data-ttu-id="51d44-321">Azure PowerShell을 사용하는 대신 Azure CLI를 사용하여 자습서를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="51d44-322">Azure CLI를 사용하려면 다음 지침에 따라 먼저 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="51d44-323">Azure CLI를 사용하여 저장소 준비 및 파일 복사</span><span class="sxs-lookup"><span data-stu-id="51d44-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="51d44-324">컨테이너 이름은 *adfgetstarted*입니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="51d44-325">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-325">Keep it as it is.</span></span> <span data-ttu-id="51d44-326">그렇지 않으면 Resource Manager 템플릿을 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="51d44-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="51d44-327">이 CLI 스크립트에 대해 도움이 필요한 경우 [Azure 저장소에서 Azure CLI 사용](../storage/common/storage-azure-cli.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51d44-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
