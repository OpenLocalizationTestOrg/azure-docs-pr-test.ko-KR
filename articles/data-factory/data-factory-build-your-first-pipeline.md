---
title: "데이터 팩터리 자습서: 첫 번째 데이터 파이프라인 | Microsoft Docs"
description: "이 Azure 데이터 팩터리 자습서에서는 Hadoop 클러스터에서 Hive 스크립트를 사용하여 데이터를 처리하는 데이터 팩터리를 만들고 예약하는 방법을 보여 줍니다."
services: data-factory
keywords: "Azure 데이터 팩터리 자습서, Hadoop 클러스터, Hadoop Hive"
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.assetid: 81f36c76-6e78-4d93-a3f2-0317b413f1d0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 08e2988d455cca21726162d9fb128e91fd51f463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-pipeline-to-transform-data-using-hadoop-cluster"></a><span data-ttu-id="1ef4c-104">자습서: Hadoop 클러스터를 사용하여 데이터를 변환하는 첫 번째 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="1ef4c-104">Tutorial: Build your first pipeline to transform data using Hadoop cluster</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ef4c-105">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="1ef4c-105">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="1ef4c-106">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="1ef4c-106">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="1ef4c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ef4c-107">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="1ef4c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ef4c-108">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="1ef4c-109">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="1ef4c-109">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="1ef4c-110">REST API</span><span class="sxs-lookup"><span data-stu-id="1ef4c-110">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="1ef4c-111">이 자습서에서는 데이터 파이프라인을 사용하여 첫 번째 Azure Data Factory를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-111">In this tutorial, you build your first Azure data factory with a data pipeline.</span></span> <span data-ttu-id="1ef4c-112">이 파이프라인은 Azure HDInsight(Hadoop) 클러스터에서 Hive 스크립트를 실행하여 입력 데이터를 변환하고 출력 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-112">The pipeline transforms input data by running Hive script on an Azure HDInsight (Hadoop) cluster to produce output data.</span></span>  

<span data-ttu-id="1ef4c-113">이 문서에서는 자습서에 대한 개요와 필수 구성 요소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-113">This article provides overview and prerequisites for the tutorial.</span></span> <span data-ttu-id="1ef4c-114">필수 구성 요소를 완료한 후에는 다음 도구/SDK: Azure Portal, Visual Studio, PowerShell, Resource Manager 템플릿, REST API 중 하나를 사용하여 자습서를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-114">After you complete the prerequisites, you can do the tutorial using one of the following tools/SDKs: Azure portal, Visual Studio, PowerShell, Resource Manager template, REST API.</span></span> <span data-ttu-id="1ef4c-115">이러한 옵션 중 하나를 사용하여 자습서를 수행하려면 이 문서의 시작에 있는 드롭다운 목록이나 끝에 있는 링크에서 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-115">Select one of the options in the drop-down list at the beginning (or) links at the end of this article to do the tutorial using one of these options.</span></span>    

## <a name="tutorial-overview"></a><span data-ttu-id="1ef4c-116">자습서 개요</span><span class="sxs-lookup"><span data-stu-id="1ef4c-116">Tutorial overview</span></span>
<span data-ttu-id="1ef4c-117">이 자습서에서는 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-117">In this tutorial, you perform the following steps:</span></span>

1. <span data-ttu-id="1ef4c-118">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-118">Create a **data factory**.</span></span> <span data-ttu-id="1ef4c-119">데이터 팩터리는 데이터를 이동 및 변환하는 하나 이상의 데이터 파이프라인을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-119">A data factory can contain one or more data pipelines that move and transform data.</span></span> 

    <span data-ttu-id="1ef4c-120">이 자습서에서는 데이터 팩터리에 하나의 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-120">In this tutorial, you create one pipeline in the data factory.</span></span> 
2. <span data-ttu-id="1ef4c-121">**파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-121">Create a **pipeline**.</span></span> <span data-ttu-id="1ef4c-122">파이프라인에는 하나 이상의 활동(예: 복사 활동, HDInsight Hive 활동)이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-122">A pipeline can have one or more activities (Examples: Copy Activity, HDInsight Hive Activity).</span></span> <span data-ttu-id="1ef4c-123">이 샘플에서는 HDInsight Hadoop 클러스터에서 Hive 스크립트를 실행하는 HDInsight Hive 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-123">This sample uses the HDInsight Hive activity that runs a Hive script on a HDInsight Hadoop cluster.</span></span> <span data-ttu-id="1ef4c-124">스크립트는 먼저 Azure Blob Storage에 저장된 원시 웹 로그 데이터를 참조하는 테이블을 만든 다음 원시 데이터를 연도별 및 월별로 분할합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-124">The script first creates a table that references the raw web log data stored in Azure blob storage and then partitions the raw data by year and month.</span></span>

    <span data-ttu-id="1ef4c-125">이 자습서에서 파이프라인은 Azure HDInsight Hadoop 클러스터에서 Hive 쿼리를 실행하여 데이터를 변환하기 위해 Hive 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-125">In this tutorial, the pipeline uses the Hive Activity to transform data by running a Hive query on an Azure HDInsight Hadoop cluster.</span></span> 
3. <span data-ttu-id="1ef4c-126">**연결된 서비스**만들기.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-126">Create **linked services**.</span></span> <span data-ttu-id="1ef4c-127">연결된 서비스를 만들어서 데이터 저장소 또는 계산 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-127">You create a linked service to link a data store or a compute service to the data factory.</span></span> <span data-ttu-id="1ef4c-128">Azure 저장소와 같은 데이터 저장소는 파이프라인에서 활동의 입/출력 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-128">A data store such as Azure Storage holds input/output data of activities in the pipeline.</span></span> <span data-ttu-id="1ef4c-129">HDInsight Hadoop cluster 클러스터와 같은 계산 서비스는 데이터를 처리/변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-129">A compute service such as HDInsight Hadoop cluster processes/transforms data.</span></span>

    <span data-ttu-id="1ef4c-130">이 자습서에는 두 가지 연결된 서비스 **Azure Storage** 및 **Azure HDInsight**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-130">In this tutorial, you create two linked services: **Azure Storage** and **Azure HDInsight**.</span></span> <span data-ttu-id="1ef4c-131">Azure Storage 연결된 서비스는 데이터 팩터리에 대한 입력/출력 데이터를 보유하는 Azure Storage 계정을 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-131">The Azure Storage linked service links an Azure Storage Account that holds the input/output data to the data factory.</span></span> <span data-ttu-id="1ef4c-132">Azure HDInsight 연결된 서비스는 데이터 팩터리에 대한 데이터를 변환하는 데 사용된 Azure HDInsight 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-132">Azure HDInsight linked service links an Azure HDInsight cluster that is used to transform data to the data factory.</span></span> 
3. <span data-ttu-id="1ef4c-133">입력 및 출력 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-133">Create input and output **datasets**.</span></span> <span data-ttu-id="1ef4c-134">입력 데이터 집합은 파이프라인의 작업에 대한 입력을 나타내고 출력 데이터 집합은 작업에 대한 출력을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-134">An input dataset represents the input for an activity in the pipeline and an output dataset represents the output for the activity.</span></span>

    <span data-ttu-id="1ef4c-135">이 자습서에서 입력 및 출력 데이터 집합은 Azure Blob Storage에서 입력 및 출력 데이터의 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-135">In this tutorial, the input and output datasets specify locations of input and output data in the Azure Blob Storage.</span></span> <span data-ttu-id="1ef4c-136">Azure Storage 연결된 서비스는 어떤 Azure Storage 계정이 사용되는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-136">The Azure Storage linked service specifies what Azure Storage Account is used.</span></span> <span data-ttu-id="1ef4c-137">입력 데이터 집합은 입력 파일의 위치를 지정하고 출력 데이터 집합은 출력 파일이 있는 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-137">An input dataset specifies where the input files are located and an output dataset specifies where the output files are placed.</span></span> 


<span data-ttu-id="1ef4c-138">Azure Data Factory에 대한 자세한 개요는 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-138">See [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of Azure Data Factory.</span></span>
  
<span data-ttu-id="1ef4c-139">다음은 이 자습서에서 빌드한 샘플 데이터 팩터리의 **다이어그램 뷰** 입니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-139">Here is the **diagram view** of the sample data factory you build in this tutorial.</span></span> <span data-ttu-id="1ef4c-140">**MyFirstPipeline**에는 입력으로 **AzureBlobInput** 데이터 집합을 사용하고 **AzureBlobOutput** 데이터 집합을 출력으로 생성하는 Hive 형식의 한 가지 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-140">**MyFirstPipeline** has one activity of type Hive that consumes **AzureBlobInput** dataset as an input and produces **AzureBlobOutput** dataset as an output.</span></span> 

![데이터 팩터리 자습서에서 다이어그램 보기](media/data-factory-build-your-first-pipeline/data-factory-tutorial-diagram-view.png)


<span data-ttu-id="1ef4c-142">이 자습서에서 **adfgetstarted** Azure blob 컨테이너의 **inputdata** 폴더에는 input.log라는 하나의 파일이 들어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-142">In this tutorial, **inputdata** folder of the **adfgetstarted** Azure blob container contains one file named input.log.</span></span> <span data-ttu-id="1ef4c-143">이 로그 파일은 2016년 1월, 2월 및 3월 등 세 달에 항목이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-143">This log file has entries from three months: January, February, and March of 2016.</span></span> <span data-ttu-id="1ef4c-144">다음은 입력 파일의 각 월에 대한 샘플 행입니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-144">Here are the sample rows for each month in the input file.</span></span> 

```
2016-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871 
2016-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2016-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="1ef4c-145">HDInsight Hive 작업을 사용하여 파이프라인에서 파일이 처리될 때 작업은 입력 데이터를 연도별 및 월별로 분할하는 HDInsight 클러스터에서 Hive 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-145">When the file is processed by the pipeline with HDInsight Hive Activity, the activity runs a Hive script on the HDInsight cluster that partitions input data by year and month.</span></span> <span data-ttu-id="1ef4c-146">스크립트는 각 월의 항목을 가진 파일을 포함하는 세 개의 출력 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-146">The script creates three output folders that contain a file with entries from each month.</span></span>  

```
adfgetstarted/partitioneddata/year=2016/month=1/000000_0
adfgetstarted/partitioneddata/year=2016/month=2/000000_0
adfgetstarted/partitioneddata/year=2016/month=3/000000_0
```

<span data-ttu-id="1ef4c-147">위에 표시된 샘플 줄에서 첫 번째 줄(2016-01-01)은 월=1 폴더의 000000_0 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-147">From the sample lines shown above, the first one (with 2016-01-01) is written to the 000000_0 file in the month=1 folder.</span></span> <span data-ttu-id="1ef4c-148">마찬가지로 두 번째 줄은 월=2 폴더의 파일에 기록되고 세 번째 줄은 월=3 폴더의 파일에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-148">Similarly, the second one is written to the file in the month=2 folder and the third one is written to the file in the month=3 folder.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="1ef4c-149">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1ef4c-149">Prerequisites</span></span>
<span data-ttu-id="1ef4c-150">이 자습서를 시작하기 전에 다음 필수 조건이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-150">Before you begin this tutorial, you must have the following prerequisites:</span></span>

1. <span data-ttu-id="1ef4c-151">**Azure 구독** - Azure 구독이 없는 경우 몇 분 만에 무료 평가판 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-151">**Azure subscription** - If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="1ef4c-152">무료 평가판 계정을 확보하는 방법은 [무료 평가판](https://azure.microsoft.com/pricing/free-trial/) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-152">See the [Free Trial](https://azure.microsoft.com/pricing/free-trial/) article on how you can obtain a free trial account.</span></span>
2. <span data-ttu-id="1ef4c-153">**Azure Storage** – 이 자습서에서는 데이터 저장을 위해 범용 표준 Azure Storage 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-153">**Azure Storage** – You use a general-purpose standard Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="1ef4c-154">범용 표준 Azure Storage 계정이 없는 경우 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-154">If you don't have a general-purpose standard Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="1ef4c-155">저장소 계정을 만든 후 **계정 이름**과 **액세스 키**를 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-155">After you have created the storage account, note down the **account name** and **access key**.</span></span> <span data-ttu-id="1ef4c-156">[저장소 액세스 키 보기, 복사 및 다시 생성](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-156">See [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>
3. <span data-ttu-id="1ef4c-157">다음 위치에서 Hive 쿼리 파일(**HQL**)을 다운로드하여 검토합니다. [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span><span class="sxs-lookup"><span data-stu-id="1ef4c-157">Download and review the Hive query file (**HQL**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql](https://adftutorialfiles.blob.core.windows.net/hivetutorial/partitionweblogs.hql).</span></span> <span data-ttu-id="1ef4c-158">이 쿼리는 출력 데이터를 생성하기 위해 입력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-158">This query transforms input data to produce output data.</span></span> 
4. <span data-ttu-id="1ef4c-159">다음 위치에서 샘플 입력 파일(**input.log**)을 다운로드하여 검토합니다. [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span><span class="sxs-lookup"><span data-stu-id="1ef4c-159">Download and review the sample input file (**input.log**) located at: [https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log](https://adftutorialfiles.blob.core.windows.net/hivetutorial/input.log)</span></span>
5. <span data-ttu-id="1ef4c-160">Azure Blob Storage에 **adfgetstarted**라는 Blob 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-160">Create a blob container named **adfgetstarted** in your Azure Blob Storage.</span></span> 
6. <span data-ttu-id="1ef4c-161">**adfgetstarted** 컨테이너의 **script** 폴더에 **partitionweblogs.hql** 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-161">Upload **partitionweblogs.hql** file to the **script** folder in the **adfgetstarted** container.</span></span> <span data-ttu-id="1ef4c-162">[Microsoft Azure 저장소 탐색기](http://storageexplorer.com/)와 같은 도구를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-162">Use tools such as [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span> 
7. <span data-ttu-id="1ef4c-163">**adfgetstarted** 컨테이너의 **inputdata** 폴더에 **input.log** 파일을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-163">Upload **input.log** file to the **inputdata** folder in the **adfgetstarted** container.</span></span> 

<span data-ttu-id="1ef4c-164">필수 조건을 완료했으면 다음 도구/SDK 중 하나를 선택하여 자습서를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-164">After you complete the prerequisites, select one of the following tools/SDKs to do the tutorial:</span></span> 

- [<span data-ttu-id="1ef4c-165">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1ef4c-165">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
- [<span data-ttu-id="1ef4c-166">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ef4c-166">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
- [<span data-ttu-id="1ef4c-167">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ef4c-167">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
- [<span data-ttu-id="1ef4c-168">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="1ef4c-168">Resource Manager template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
- [<span data-ttu-id="1ef4c-169">REST API</span><span class="sxs-lookup"><span data-stu-id="1ef4c-169">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="1ef4c-170">Azure Portal 및 Visual Studio는 데이터 팩터리를 빌드하는 GUI 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-170">Azure portal and Visual Studio provide GUI way of building your data factories.</span></span> <span data-ttu-id="1ef4c-171">반면, PowerShell, Resource Manager 템플릿 및 REST API 옵션은 데이터 팩터리를 빌드하는 스크립팅/프로그래밍 방식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-171">Whereas, PowerShell, Resource Manager Template, and REST API options provides scripting/programming way of building your data factories.</span></span>

> [!NOTE]
> <span data-ttu-id="1ef4c-172">이 자습서의 데이터 파이프라인은 출력 데이터를 생성하는 입력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-172">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="1ef4c-173">원본 데이터 저장소의 데이터를 대상 데이터 저장소로 복사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-173">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="1ef4c-174">Azure Data Factory를 사용하여 데이터를 복사하는 방법에 대한 자습서는 [자습서: Blob Storage에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-174">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="1ef4c-175">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정하여 두 활동을 연결하면 해당 활동을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-175">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1ef4c-176">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ef4c-176">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 





  
