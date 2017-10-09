---
title: "데이터 팩터리-Azure HDInsight를 사용 하는 요청 시 Hadoop 클러스터 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate 주문형 Hadoop 클러스터를 Azure 데이터 팩터리를 사용 하 여 HDInsight에 알아봅니다."
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
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="acd41-103">Azure Data Factory를 사용하여 HDInsight에서 주문형 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="acd41-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) 는 오케스트레이션 하 고 데이터의 hello 이동 및 변환을 자동화 하는 클라우드 기반 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="acd41-105">HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 분할을 만들 수 있으며 hello 처리가 완료 되 면 hello 클러스터를 삭제.</span><span class="sxs-lookup"><span data-stu-id="acd41-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="acd41-106">주문형 HDInsight Hadoop 클러스터를 사용 하 여 hello 혜택은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="acd41-107">사용자만 급여 hello 타이머 작업에 대 한 hello 간략 한 구성 가능한 유휴 시간) (더하기 HDInsight Hadoop 클러스터에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="acd41-108">HDInsight 클러스터에 대 한 hello 청구는 비례 배분 분당 여부 사용 하 든 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="acd41-109">주문형 HDInsight 연결 된 서비스를 사용 하 여 데이터 팩터리에서 hello 클러스터 요청 시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="acd41-110">고 hello 클러스터는 hello 작업이 완료 되 면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="acd41-111">따라서 요금만 지불 하기 hello 작업 시간 및 hello 간략 한 유휴 시간 (활성 시간 설정)를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="acd41-112">Data Factory 파이프라인을 사용하여 워크플로를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="acd41-113">예를 들어 hello 파이프라인 toocopy 데이터는 온-프레미스 SQL Server tooan Azure blob 저장소, 주문형 HDInsight Hadoop 클러스터에서 하이브 스크립트와 Pig 스크립트를 실행 하 여 hello 데이터 처리를에서 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="acd41-114">그런 다음 응용 프로그램 tooconsume BI에 대 한 hello 결과 데이터 tooan Azure SQL 데이터 웨어하우스를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="acd41-115">Hello 워크플로 toorun 주기적으로 (시간별, 일별, 주별, 월별, 등)를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="acd41-116">Azure Data Factory에서 데이터 팩터리에는 하나 이상의 데이터 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="acd41-117">데이터 파이프라인은 하나 이상의 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="acd41-118">두 가지 유형의 활동이 있으며 [데이터 이동 활동](../data-factory/data-factory-data-movement-activities.md) 및 [데이터 변환 활동](../data-factory/data-factory-data-transformation-activities.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="acd41-119">원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터 이동을 활동 (현재만 복사 작업) toomove 데이터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="acd41-120">데이터 변환 활동 tootransform/프로세스 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="acd41-121">HDInsight Hive 활동 데이터 팩터리에서 지원 되는 hello 변환 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="acd41-122">이 자습서에서는 hello Hive 변환 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="acd41-123">사용자 고유의 HDInsight Hadoop 클러스터 또는 주문형 HDInsight Hadoop 클러스터에 hive 활동 toouse를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="acd41-124">이 자습서에서는 hello Hive 작업 hello 데이터 팩터리 파이프라인에서 구성 된 toouse 주문형 HDInsight 클러스터는입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="acd41-125">따라서 tooprocess 데이터 조각을 실행 하는 hello 활동을 여기 일이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="acd41-126">HDInsight Hadoop 클러스터 적시에 tooprocess hello 조각에 대 한 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="acd41-127">hello 입력된 데이터는 hello 클러스터에 HiveQL 스크립트를 실행 하 여 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="acd41-128">hello HDInsight Hadoop 클러스터 hello 처리가 완료 되 고 hello 클러스터는 시간 (timeToLive 설정) 구성 하는 hello 동안만 유휴 상태 후 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="acd41-129">다음 데이터 조각을 hello timeToLive 유휴 시간에 사용 하 여 처리에 사용할 경우 hello 동일한 클러스터 사용 되는 tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="acd41-130">이 자습서에서는 hello HiveQL 스크립트 hello 하이브 활동과 관련 된 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="acd41-131">외부 테이블을 참조 hello Azure Blob 저장소에 저장 된 원시 웹 로그 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="acd41-132">연도 / 월 파티션 hello의 원시 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="acd41-133">저장소 hello hello Azure blob 저장소에서에서 분할 된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="acd41-134">이 자습서에서는 hello HiveQL 스크립트 hello 하이브 활동과 연결 된 외부 테이블을 참조 hello hello Azure Blob 저장소에에서 저장 된 원시 웹 로그 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="acd41-135">Hello 입력된 파일에 다음 각 월에 대 한 hello 샘플 행은</span><span class="sxs-lookup"><span data-stu-id="acd41-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="acd41-136">hello HiveQL 스크립트 파티션을 년 및 월 단위로 원시 데이터를 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="acd41-137">Hello 이전 입력을 기반으로 세 출력 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="acd41-138">각 폴더에는 각 월의 항목과 함께 파일이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="acd41-139">목록이 추가 tooHive 활동에서 데이터 팩터리 데이터 변환 작업에 대 한 참조 [변환 하 고 Azure 데이터 팩터리를 사용 하 여 분석](../data-factory/data-factory-data-transformation-activities.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="acd41-140">현재, Azure Data Factory에서 HDInsight 클러스터 버전 3.2 만들기만 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acd41-141">필수 조건</span><span class="sxs-lookup"><span data-stu-id="acd41-141">Prerequisites</span></span>
<span data-ttu-id="acd41-142">이 문서의 지침 hello를 시작 하기 전에 다음 항목 hello가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="acd41-143">[Azure 구독](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="acd41-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="acd41-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="acd41-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="acd41-145">저장소 계정 준비</span><span class="sxs-lookup"><span data-stu-id="acd41-145">Prepare storage account</span></span>
<span data-ttu-id="acd41-146">이 시나리오에서 toothree 저장소 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="acd41-147">hello HDInsight 클러스터에 대 한 기본 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="acd41-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="acd41-148">hello 입력된 데이터에 대 한 저장소 계정</span><span class="sxs-lookup"><span data-stu-id="acd41-148">storage account for hello input data</span></span>
- <span data-ttu-id="acd41-149">hello에 대 한 저장소 계정 데이터를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-149">storage account for hello output data</span></span>

<span data-ttu-id="acd41-150">toosimplify hello 자습서에서는 하나의 저장소 계정 tooserve hello 세 가지 목적으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="acd41-151">이 섹션에서 제공 하는 hello Azure PowerShell 예제 스크립트는 hello 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="acd41-152">TooAzure에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="acd41-153">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="acd41-154">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="acd41-155">Hello 저장소 계정에서 Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="acd41-156">다음 두 개의 파일 toohello Blob 컨테이너 hello를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="acd41-157">입력 데이터 파일: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="acd41-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="acd41-158">HiveQL 스크립트: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="acd41-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="acd41-159">두 파일은 공용 Blob 컨테이너에 저장되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="acd41-160">**tooprepare hello 저장소 파일을 복사할 hello Azure PowerShell을 사용 하 여:**</span><span class="sxs-lookup"><span data-stu-id="acd41-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="acd41-161">Hello Azure 리소스 그룹 및 hello 스크립트에 의해 생성 되는 hello Azure 저장소 계정 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="acd41-162">적어 **리소스 그룹 이름은**, **저장소 계정 이름**, 및 **저장소 계정 키** hello 스크립트에 의해 출력 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="acd41-163">Hello 다음 섹션에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="acd41-164">Hello PowerShell 스크립트에서 도움이 필요한 경우 참조 [hello를 사용 하 여 Azure 저장소와 Azure PowerShell](../storage/common/storage-powershell-guide-full.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="acd41-165">त ु toouse Azure CLI hello 대신 참조 [부록](#appendix) hello Azure CLI 스크립트에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="acd41-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="acd41-166">**tooexamine hello 저장소 계정 및 hello 내용**</span><span class="sxs-lookup"><span data-stu-id="acd41-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="acd41-167">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="acd41-168">클릭 **리소스 그룹** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="acd41-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="acd41-169">PowerShell 스크립트에서 만든 hello 리소스 그룹 이름이 두 번 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="acd41-170">나열 된 너무 많은 리소스 그룹이 있는 경우 hello 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="acd41-171">Hello에 **리소스** 타일을 다른 프로젝트와 hello 리소스 그룹을 공유 하지 않는 한 나열 된 리소스가 두 개 있어야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="acd41-172">해당 리소스에는 이전에 지정한 hello 이름의 hello 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="acd41-173">Hello 저장소 계정 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="acd41-174">Hello 클릭 **Blob** 타일입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="acd41-175">Hello 클릭 **adfgetstarted** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="acd41-176">**inputdata** 및 **script**라는 두 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="acd41-177">Hello 폴더를 열고 hello 폴더에 hello 파일을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="acd41-178">hello inputdata 입력된 데이터를 포함 하는 hello input.log 파일 있어서 hello HiveQL 스크립트 파일이 hello 스크립트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="acd41-179">Resource Manager 템플릿을 사용하여 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="acd41-180">Hello 저장소 계정, hello 입력된 데이터 및 hello 준비 HiveQL 스크립트를 준비 toocreate Azure 데이터 팩터리에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="acd41-181">데이터 팩터리는 여러 가지 방법으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="acd41-182">이 자습서에서는 Azure 포털 hello를 사용 하는 Azure 리소스 관리자 템플릿을 배포 하 여 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="acd41-183">또한 [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) 및 [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template)을 사용하여 Resource Manager 템플릿을 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="acd41-184">기타 데이터 팩터리 만들기 방법은 [자습서: 첫 번째 데이터 팩터리 빌드](../data-factory/data-factory-build-your-first-pipeline.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd41-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="acd41-185">Hello tooAzure에 이미지 toosign와 hello Azure 포털에서에서 열기 hello 리소스 관리자 템플릿을 다음를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="acd41-186">hello 서식 파일은 https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="acd41-187">Hello 참조 [hello 서식 파일에서 엔터티를 Data Factory](#data-factory-entities-in-the-template) hello 서식 파일에 정의 된 엔터티에 대 한 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="acd41-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="acd41-188">선택 **기존 항목 사용** hello에 대 한 옵션 **리소스 그룹** 설정과 선택 hello 이름 (PowerShell 스크립트를 사용 하 여) hello 이전 단계에서 만든 hello 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="acd41-189">Hello 데이터 팩토리에 대 한 이름을 입력 하십시오 (**데이터 팩토리 이름이**).</span><span class="sxs-lookup"><span data-stu-id="acd41-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="acd41-190">이 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="acd41-191">Hello 입력 **저장소 계정 이름** 및 **저장소 계정 키** hello 이전 단계에서 적어 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="acd41-192">선택 **toohello 약관 동의** 읽은 후 위에 언급 된 **약관**합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="acd41-193">선택 **Pin toodashboard** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="acd41-194">**구매/만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="acd41-195">대시보드를 호출 하는 hello에 타일을 표시 **배포 템플릿 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="acd41-196">Hello 될 때까지 기다렸다가 **리소스 그룹** 리소스 그룹에 대 한 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="acd41-197">이라는 제목으로 사용자 리소스 그룹 이름 tooopen hello 리소스 그룹 블레이드 hello 타일을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="acd41-198">리소스 그룹 블레이드 hello 아직 열려 있지 않으면 hello 타일 tooopen hello 리소스 그룹을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="acd41-199">이제 하나 더 많은 데이터 팩터리 리소스 나열 또한 toohello 저장소 계정 리소스를 표시 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="acd41-200">데이터 팩터리의 hello 이름을 클릭 (hello에 대 한 지정 된 값 **데이터 팩토리 이름이** 매개 변수).</span><span class="sxs-lookup"><span data-stu-id="acd41-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="acd41-201">Hello Data Factory 블레이드에서 hello 클릭 **다이어그램** 바둑판식으로 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="acd41-202">hello 다이어그램 입력된 데이터 집합 및는 출력 데이터 집합을 사용 하 여 하나의 동작을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 다이어그램](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="acd41-204">hello 이름은 hello 리소스 관리자 서식 파일에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="acd41-205">**AzureBlobOutput**을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="acd41-206">Hello에 **최근 업데이트 조각**, 한 조각만 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="acd41-207">Hello 상태가 **진행에서**, 너무 변경 될 때까지 기다렸다가**준비**합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="acd41-208">에 대 한는 대개 **20 분** toocreate HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="acd41-209">Hello 데이터 팩터리 출력 확인</span><span class="sxs-lookup"><span data-stu-id="acd41-209">Check hello data factory output</span></span>

1. <span data-ttu-id="acd41-210">사용 하 여 hello 동일 hello 마지막 세션 toocheck hello 컨테이너에서 hello adfgetstarted 컨테이너의 절차입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="acd41-211">없는 두 개의 새 컨테이너 또한 너무**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="acd41-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="acd41-212">Hello 패턴을 따르는 이름 가진 컨테이너: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="acd41-213">이 컨테이너는 hello HDInsight 클러스터에 대 한 hello 기본 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="acd41-214">adfjobs:이 컨테이너는 hello ADF 작업 로그에 대 한 hello 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="acd41-215">데이터 팩터리 출력이 hello에 저장 됩니다 **afgetstarted** hello 리소스 관리자 서식 파일에서 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="acd41-216">**adfgetstarted**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="acd41-217">**partitioneddata**를 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="acd41-218">표시는 **연도 2014 =** 폴더 2014 년에 모든 hello 웹 로그 일자 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="acd41-220">드릴 다운 하면 hello 목록, 1 월, 2 월 및 월에 대 한 세 폴더는 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="acd41-221">각 월에 대한 로그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight 주문형 hive 작업 파이프라인 출력](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="acd41-223">Hello 서식 파일에서 데이터 팩터리 엔터티</span><span class="sxs-lookup"><span data-stu-id="acd41-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="acd41-224">와 같은 데이터 팩토리에 대 한 최상위 리소스 관리자 템플릿을 hello 표시 되는 모양을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="acd41-225">데이터 팩터리 정의</span><span class="sxs-lookup"><span data-stu-id="acd41-225">Define data factory</span></span>
<span data-ttu-id="acd41-226">Hello 다음 예제와 같이 hello 리소스 관리자 서식 파일에서 데이터 팩터리를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="acd41-227">hello dataFactoryName은 hello 서식 파일을 배포할 때 지정 하는 hello 데이터 팩터리의 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="acd41-228">데이터 팩터리는 현재 hello 미국 동부, 미국 서 부 및 북부 유럽 지역의 에서만 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="acd41-229">Hello 데이터 팩터리 내에서 엔터티를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="acd41-230">hello 다음과 같은 데이터 팩터리 엔터티 템플릿에 정의 된 hello JSON:</span><span class="sxs-lookup"><span data-stu-id="acd41-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="acd41-231">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="acd41-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="acd41-232">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="acd41-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="acd41-233">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="acd41-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="acd41-234">Azure Blob 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="acd41-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="acd41-235">복사 작업을 포함하는 데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="acd41-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="acd41-236">Azure 저장소 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="acd41-236">Azure Storage linked service</span></span>
<span data-ttu-id="acd41-237">hello Azure 저장소는 Azure 저장소 계정 toohello 데이터 팩터리 서비스 링크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="acd41-238">이 자습서에서는 hello 동일한 저장소 계정으로 사용 됩니다 hello 기본 HDInsight 저장소 계정, 입력된 데이터 저장 및 출력 데이터 저장소.</span><span class="sxs-lookup"><span data-stu-id="acd41-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="acd41-239">따라서 Azure Storage 연결된 서비스 하나만 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="acd41-240">연결 된 hello 서비스 정의에 hello 이름 및 사용자의 Azure 저장소 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="acd41-241">참조 [Azure 저장소 연결 된 서비스](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

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
<span data-ttu-id="acd41-242">hello **connectionString** 사용 하 여 hello storageAccountName 및 storageAccountKey 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="acd41-243">Hello 서식 파일을 배포 하는 동안 이러한 매개 변수 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="acd41-244">HDInsight 주문형 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="acd41-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="acd41-245">Hello 주문형 HDInsight 연결 되며 서비스 정의 hello Data Factory 서비스 toocreate 런타임 시 HDInsight Hadoop 클러스터에서 사용 되는 구성 매개 변수 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="acd41-246">참조 [계산 연결 된 서비스](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) HDInsight 주문형 연결 된 서비스 JSON 사용 되는 속성 toodefine 대 한 자세한 내용은 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="acd41-247">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="acd41-247">Note hello following points:</span></span>

* <span data-ttu-id="acd41-248">hello 데이터 팩터리가 **Linux 기반** HDInsight 클러스터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="acd41-249">hello HDInsight Hadoop 클러스터를 만든 hello에 동일한 hello 저장소 계정과 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="acd41-250">공지 hello *timeToLive* 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="acd41-251">hello 데이터 팩터리의 hello 클러스터 되 고 유휴 30 분 후 자동으로 hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="acd41-252">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="acd41-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="acd41-253">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="acd41-254">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-254">This behavior is by design.</span></span> <span data-ttu-id="acd41-255">주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="acd41-256">자세한 내용은 [주문형 HDInsight 연결된 서비스](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd41-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acd41-257">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="acd41-258">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="acd41-259">이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="acd41-260">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="acd41-261">Azure Blob 입력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="acd41-261">Azure blob input dataset</span></span>
<span data-ttu-id="acd41-262">Hello 입력된 데이터 집합 정의 있는 blob 컨테이너, 폴더 및 hello 입력된 데이터가 포함 된 파일의 hello 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="acd41-263">참조 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

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

<span data-ttu-id="acd41-264">Hello hello JSON 정의에서 특정 설정을 다음 사항을 참고 하십시오.</span><span class="sxs-lookup"><span data-stu-id="acd41-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="acd41-265">Azure Blob 출력 데이터 집합</span><span class="sxs-lookup"><span data-stu-id="acd41-265">Azure Blob output dataset</span></span>
<span data-ttu-id="acd41-266">Hello 출력 데이터 집합 정의 blob 컨테이너 및 hello 출력 데이터를 보유 하는 폴더의 hello 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="acd41-267">참조 [Azure Blob 데이터 집합 속성](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) JSON 사용 되는 속성 toodefine 된 Azure Blob 데이터 집합에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="acd41-268">hello folderPath hello 출력 데이터를 보유 하는 hello 경로 toohello 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="acd41-269">hello [dataset 가용성](../data-factory/data-factory-create-datasets.md#dataset-availability) 설정을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="acd41-270">Azure Data Factory에 출력 데이터 집합 가용성 드라이브 hello 파이프라인입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="acd41-271">이 예제에서는 hello 조각이 hello (EndOfInterval) 달의 마지막 날에 월별 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="acd41-272">자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd41-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="acd41-273">데이터 파이프라인</span><span class="sxs-lookup"><span data-stu-id="acd41-273">Data pipeline</span></span>
<span data-ttu-id="acd41-274">주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하여 데이터를 변환하는 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="acd41-275">참조 [파이프라인 JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) JSON 사용 되는 요소 toodefine이이 예제에서 파이프라인에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

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

<span data-ttu-id="acd41-276">hello 파이프라인 한 작업, HDInsightHive 활동을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="acd41-277">시작 및 종료 날짜 모두 2016년 1월에 있으므로 한 달에 대한 데이터(조각)만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="acd41-278">둘 다 *시작* 및 *끝* hello 활동의 없으므로 과거 날짜로 hello Data Factory에서 즉시 hello 월에 대 한 데이터를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="acd41-279">Hello 끝 날짜는 미래의 날짜 이면 hello 데이터 팩터리의 hello 시간이 되 다른 분할 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="acd41-280">자세한 내용은 [데이터 팩터리 예약 및 실행](../data-factory/data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="acd41-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="acd41-281">Hello 자습서 정리</span><span class="sxs-lookup"><span data-stu-id="acd41-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="acd41-282">주문형 HDInsight 클러스터에서 만들어진 hello blob 컨테이너를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="acd41-283">주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 toobe 기존 라이브 클러스터 (timeToLive;)이 없는 경우를 처리 해야 때마다 만드는 및 hello 클러스터 hello 처리가 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="acd41-284">각 클러스터에 대 한 Azure Data Factory hello hello 클러스터에 대 한 hello 기본 저장소 계정으로 사용 되는 Azure blob 저장소에서에서 blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="acd41-285">HDInsight 클러스터를 삭제 하는 경우에 hello 기본 blob 저장소 컨테이너와 연결 된 hello 저장소 계정이 삭제 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="acd41-286">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-286">This behavior is by design.</span></span> <span data-ttu-id="acd41-287">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="acd41-288">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="acd41-289">이러한 컨테이너의 hello 이름 패턴을 따르도록: `adfyourdatafactoryname-linkedservicename-datetimestamp`합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="acd41-290">Hello 삭제 **adfjobs** 및 **adfyourdatafactoryname-linkedservicename-datetimestamp** 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="acd41-291">hello adfjobs 컨테이너 Azure Data Factory에서 작업 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="acd41-292">Hello 리소스 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="acd41-292">Delete hello resource group</span></span>
<span data-ttu-id="acd41-293">[Azure 리소스 관리자](../azure-resource-manager/resource-group-overview.md) 사용된 toodeploy가 관리 하 고 하나의 그룹으로 솔루션을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="acd41-294">리소스 그룹을 삭제 해도 hello 그룹 내의 모든 hello 구성 요소를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="acd41-295">Toohello 로그온 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="acd41-296">클릭 **리소스 그룹** hello 왼쪽된 창에서.</span><span class="sxs-lookup"><span data-stu-id="acd41-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="acd41-297">PowerShell 스크립트에서 만든 hello 리소스 그룹 이름을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="acd41-298">나열 된 너무 많은 리소스 그룹이 있는 경우 hello 필터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="acd41-299">Hello 리소스 그룹에는 새 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="acd41-300">Hello에 **리소스** hello 기본 저장소 계정 및 hello 데이터 팩터리 나열 다른 프로젝트와 hello 리소스 그룹을 공유 하지 않는 한 사용할은 타일을 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="acd41-301">클릭 **삭제** hello hello 블레이드 맨 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="acd41-302">이렇게 hello 저장소 계정 및 hello 저장소 계정에 저장 된 hello 데이터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="acd41-303">Hello 리소스 그룹 이름 tooconfirm 삭제를 입력 한 다음 클릭 **삭제**합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="acd41-304">되지 않도록 toodelete hello 저장소 계정 hello 리소스 그룹을 삭제 하는 경우 hello를 hello 기본 저장소 계정에서 hello 비즈니스 데이터를 분리 하 여 아키텍처를 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="acd41-305">이 경우 hello 비즈니스 데이터로 hello 저장소 계정에 대 한 리소스 그룹에 있고 다른 리소스 그룹 HDInsight 연결 된 서비스 및 hello 데이터 팩토리에 대 한 hello 기본 저장소 계정에 대 한 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="acd41-306">Hello 두 번째 리소스 그룹을 삭제 하면 hello 비즈니스 데이터 저장소 계정 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="acd41-307">toodo 하므로:</span><span class="sxs-lookup"><span data-stu-id="acd41-307">toodo so:</span></span>

* <span data-ttu-id="acd41-308">Hello 다음 hello 리소스 관리자 템플릿에 Microsoft.DataFactory/datafactories 리소스와 함께 toohello 최상위 리소스 그룹을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="acd41-309">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="acd41-310">새 연결 된 서비스 지점 toohello 새 저장소 계정을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-310">Add a new linked service point toohello new storage account:</span></span>

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
* <span data-ttu-id="acd41-311">추가 dependsOn 및는 additionalLinkedServiceNames 사용 하 여 hello HDInsight 주문형 연결 된 서비스를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="acd41-312">다음 단계</span><span class="sxs-lookup"><span data-stu-id="acd41-312">Next steps</span></span>
<span data-ttu-id="acd41-313">이 문서에서는 배웠습니다 어떻게 toouse Azure Data Factory toocreate 주문형 HDInsight 클러스터 tooprocess 하이브 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="acd41-314">더 많은 tooread:</span><span class="sxs-lookup"><span data-stu-id="acd41-314">tooread more:</span></span>

* [<span data-ttu-id="acd41-315">Hadoop 자습서: HDInsight에서 Linux 기반 Hadoop 사용 시작</span><span class="sxs-lookup"><span data-stu-id="acd41-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="acd41-316">HDInsight에서 Linux 기반 Hadoop 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="acd41-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="acd41-317">HDInsight 설명서</span><span class="sxs-lookup"><span data-stu-id="acd41-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="acd41-318">데이터 팩터리 설명서</span><span class="sxs-lookup"><span data-stu-id="acd41-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="acd41-319">부록</span><span class="sxs-lookup"><span data-stu-id="acd41-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="acd41-320">Azure CLI 스크립트</span><span class="sxs-lookup"><span data-stu-id="acd41-320">Azure CLI script</span></span>
<span data-ttu-id="acd41-321">Azure PowerShell toodo hello 자습서를 사용 하는 대신 Azure CLI를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="acd41-322">먼저 Azure CLI toouse hello 다음 지침에 따라 Azure CLI를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="acd41-323">Azure CLI tooprepare hello 저장소를 사용 하 고 hello 파일 복사</span><span class="sxs-lookup"><span data-stu-id="acd41-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

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

<span data-ttu-id="acd41-324">hello 컨테이너 이름이 *adfgetstarted*합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="acd41-325">그대로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-325">Keep it as it is.</span></span> <span data-ttu-id="acd41-326">그렇지 않으면 tooupdate hello 리소스 관리자 템플릿이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="acd41-327">이 CLI 스크립트에서 도움이 필요한 경우 참조 [hello를 사용 하 여 Azure 저장소와 Azure CLI](../storage/common/storage-azure-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="acd41-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
