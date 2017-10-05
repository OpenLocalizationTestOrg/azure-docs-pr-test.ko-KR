---
title: "Azure Data Factory 파이프라인에서 사용자 지정 작업 사용"
description: "사용자 지정 작업을 만들고 Azure Data Factory 파이프라인에서 사용하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="ffddf-103">Azure Data Factory 파이프라인에서 사용자 지정 작업 사용</span><span class="sxs-lookup"><span data-stu-id="ffddf-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ffddf-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ffddf-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ffddf-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ffddf-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ffddf-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ffddf-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ffddf-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ffddf-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ffddf-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ffddf-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="ffddf-114">Azure Data Factory 파이프라인에서 사용할 수 있는 두 가지 작업 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="ffddf-115">[데이터 이동 작업](data-factory-data-movement-activities.md)은 [지원되는 원본 및 싱크 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 간에 데이터를 이동하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="ffddf-116">[데이터 변환 작업](data-factory-data-transformation-activities.md)은 Azure HDInsight, Azure Batch, Azure Machine Learning과 같은 계산 서비스를 사용하여 데이터를 변환하는 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="ffddf-117">Data Factory에서 지원되지 않는 데이터 저장소에서 다른 위치로 또는 그 반대로 데이터를 이동하려면 고유의 데이터 이동 논리가 포함된 **사용자 지정 작업**을 만들어서 파이프라인에 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="ffddf-118">마찬가지로, Data Factory에서 지원되지 않는 방식으로 데이터를 변환/처리하려면 고유의 데이터 변환 논리가 포함된 사용자 지정 작업을 만들어서 파이프라인에 해당 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="ffddf-119">Virtual Machines의 **Azure Batch** 풀 또는 Windows 기반 **Azure HDInsight** 클러스터에서 실행할 사용자 지정 작업을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="ffddf-120">Azure Batch를 사용할 때는 기존 Azure Batch 풀만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="ffddf-121">반면, HDInsight를 사용할 때는 기존 HDInsight 클러스터 또는 필요 시 런타임에 자동으로 생성된 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="ffddf-122">다음 연습에서는 사용자 지정 .NET 작업을 만들어서 해당 사용자 작업을 파이프라인에 사용하는 단계별 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="ffddf-123">이 연습에서는 **Azure Batch** 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="ffddf-124">Azure HDInsight 연결된 서비스를 대신 사용하려면 **HDInsight**(사용자 고유의 HDInsight 클러스터) 또는 **HDInsightOnDemand**(Data Factory에서 필요 시 HDInsight 클러스터 생성) 형식의 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="ffddf-125">그런 다음 HDInsight 연결된 서비스를 사용하도록 사용자 지정 작업을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="ffddf-126">Azure HDInsight를 사용하여 사용자 지정 작업을 실행하는 방법에 대한 자세한 내용은 [Azure HDInsight 연결된 서비스 사용](#use-hdinsight-compute-service) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="ffddf-127">사용자 지정 .NET 작업은 Windows 기반 HDInsight 클러스터에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ffddf-128">이 제한 사항에 대한 해결 방법은 MapReduce 작업을 사용하여 Linux 기반 HDInsight 클러스터에서 사용자 지정 Java 코드를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ffddf-129">또 다른 옵션은 VM의 Azure Batch 풀을 사용하여 HDInsight 클러스터를 사용하는 대신 사용자 지정 작업을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="ffddf-130">사용자 지정 작업에서 데이터 관리 게이트웨이를 사용하여 온-프레미스 데이터 원본에 액세스할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="ffddf-131">현재 [데이터 관리 게이트웨이](data-factory-data-management-gateway.md)에서는 Data Factory의 복사 작업 및 저장 프로시저 작업만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="ffddf-132">연습: 사용자 지정 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ffddf-133">필수 조건</span><span class="sxs-lookup"><span data-stu-id="ffddf-133">Prerequisites</span></span>
* <span data-ttu-id="ffddf-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="ffddf-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="ffddf-135">[Azure .NET SDK](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ffddf-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="ffddf-136">Azure 배치 필수 조건</span><span class="sxs-lookup"><span data-stu-id="ffddf-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="ffddf-137">이 연습에서는 Azure 배치를 계산 리소스로 사용하여 사용자 지정 .NET 작업을 실행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="ffddf-138">**Azure Batch**는 클라우드에서 대규모 병렬 및 HPC(고성능 컴퓨팅) 응용 프로그램을 효율적으로 실행하기 위한 플랫폼 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="ffddf-139">Azure Batch는 **가상 컴퓨터의 관리되는 컬렉션**에서 실행되는 계산 집약적 작업을 예약하고, 작업 요구에 맞게 계산 리소스의 규모를 자동으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="ffddf-140">Azure Batch 서비스의 개요에 대한 자세한 내용은 [Azure Batch 기본 사항][batch-technical-overview] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="ffddf-141">자습서를 위해 VM 풀과 함께 Azure Batch 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="ffddf-142">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-142">Here are the steps:</span></span>

1. <span data-ttu-id="ffddf-143">**Azure 포털** 을 사용하여 [Azure 배치 계정](http://portal.azure.com)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="ffddf-144">지침은 [Azure Batch 계정 만들기 및 관리][batch-create-account] 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="ffddf-145">Azure Batch 계정 이름, 계정 키, URI 및 풀 이름을 적어둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="ffddf-146">Azure Batch 연결된 서비스를 만드는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="ffddf-147">Azure Batch 계정의 홈 페이지에서 `https://myaccount.westus.batch.azure.com` 형식의 **URL**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="ffddf-148">이 예제에서 **myaccount**는 Azure Batch 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="ffddf-149">연결된 서비스 정의에서 사용하는 URI는 계정 이름이 없는 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="ffddf-150">예: `https://<region>.batch.azure.com`</span><span class="sxs-lookup"><span data-stu-id="ffddf-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="ffddf-151">왼쪽 메뉴에서 **키**를 클릭하고 **기본 액세스 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="ffddf-152">기존 풀을 사용하려면 메뉴에서 **풀**을 클릭하고 풀의 **ID**를 메모해둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="ffddf-153">기존 풀이 없는 경우 다음 단계로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="ffddf-154">**Azure 배치 풀**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="ffddf-155">[Azure 포털](https://portal.azure.com)에서 왼쪽 메뉴의 **찾아보기**, **배치 계정**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="ffddf-156">Azure 배치 계정을 선택하여 **배치 계정** 블레이드를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="ffddf-157">**풀** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="ffddf-158">**풀** 블레이드에서 도구 모음의 추가 단추를 클릭하여 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="ffddf-159">풀에 대한 ID(풀 ID)를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="ffddf-160">Data Factory 솔루션을 만들 때 필요하므로 **풀의 ID**를 메모해둡니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="ffddf-161">운영 체제 제품군 설정에 **Windows Server 2012 R2** 를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="ffddf-162">**노드 가격 책정 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="ffddf-163">**대상 전용** 설정 값으로 **2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="ffddf-164">**노드당 최대 작업** 설정 값으로 **2**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="ffddf-165">**확인** 을 클릭하여 풀을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="ffddf-166">풀의 **ID**를 메모해둡니다</span><span class="sxs-lookup"><span data-stu-id="ffddf-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="ffddf-167">대략적인 단계</span><span class="sxs-lookup"><span data-stu-id="ffddf-167">High-level steps</span></span>
<span data-ttu-id="ffddf-168">이 연습의 일환으로 수행하는 두 가지 대략적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="ffddf-169">간단한 데이터 변환/처리 논리가 포함된 사용자 지정 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="ffddf-170">사용자 지정 작업을 사용하는 파이프라인으로 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="ffddf-171">사용자 지정 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-171">Create a custom activity</span></span>
<span data-ttu-id="ffddf-172">.NET 사용자 지정 작업을 만들려면 **IDotNetActivity** 인터페이스를 구현하는 클래스를 사용하는 **.NET 클래스 라이브러리** 프로젝트를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="ffddf-173">이 인터페이스는 [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) 라는 메서드 하나만 포함하며 서명은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="ffddf-174">이 메서드는 다음과 같은 네 개의 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-174">The method takes four parameters:</span></span>

- <span data-ttu-id="ffddf-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="ffddf-175">**linkedServices**.</span></span> <span data-ttu-id="ffddf-176">이 속성은 작업에 대한 입력/출력으로 참조되는 데이터 저장소 연결된 서비스의 열거형 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="ffddf-177">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="ffddf-177">**datasets**.</span></span> <span data-ttu-id="ffddf-178">이 속성은 작업에 대한 입력/출력 데이터 집합의 열거형 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="ffddf-179">이 매개 변수를 사용하여 입력 및 출력 데이터 집합에 정의된 위치 및 스키마를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="ffddf-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="ffddf-180">**activity**.</span></span> <span data-ttu-id="ffddf-181">이 속성은 현재 작업을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-181">This property represents the current activity.</span></span> <span data-ttu-id="ffddf-182">사용자 지정 작업과 연결된 확장된 속성에 액세스하려면 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="ffddf-183">자세한 내용은 [확장 속성 액세스](#access-extended-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="ffddf-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="ffddf-184">**logger**.</span></span> <span data-ttu-id="ffddf-185">이 개체를 사용하면 파이프라인에 대한 사용자 로그로 노출할 디버그 주석을 기록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="ffddf-186">이 메서드는 나중에 사용자 지정 작업을 함께 연결하는 데 사용할 수 있는 사전을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="ffddf-187">이 기능은 아직 구현되지 않았기 때문에, 메서드로부터 빈 사전이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="ffddf-188">절차</span><span class="sxs-lookup"><span data-stu-id="ffddf-188">Procedure</span></span>
1. <span data-ttu-id="ffddf-189">**.NET 클래스 라이브러리** 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="ffddf-190"><b>Visual Studio 2017</b> 또는 <b>Visual Studio 2015</b> 또는 <b>Visual Studio 2013</b> 또는 <b>Visual Studio 2012</b>를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="ffddf-191"><b>파일</b>을 클릭하고 <b>새로 만들기</b>를 가리킨 다음 <b>프로젝트</b>를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="ffddf-192"><b>템플릿</b>을 확장하고 <b>Visual C#</b>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="ffddf-193">이 연습에서는 C#을 사용하지만 다른 .NET 언어를 사용하여 사용자 지정 작업을 개발할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="ffddf-194">오른쪽의 프로젝트 형식 목록에서 <b>클래스 라이브러리</b>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="ffddf-195">VS 2017에서 <b>클래스 라이브러리(.NET Framework)</b> 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="ffddf-196"><b>이름</b>에 <b>MyDotNetActivity</b>를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="ffddf-197"><b>위치</b>에 <b>C:\ADFGetStarted</b>를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="ffddf-198"><b>확인</b> 을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="ffddf-199">
2. **도구**를 클릭하고 **NuGet 패키지 관리자**를 가리킨 다음 **패키지 관리자 콘솔**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="ffddf-200">3.</span><span class="sxs-lookup"><span data-stu-id="ffddf-200">3.</span></span> <span data-ttu-id="ffddf-201">패키지 관리자 콘솔에서 다음 명령을 실행하여 **Microsoft.Azure.Management.DataFactories**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="ffddf-202">**Azure 저장소** NuGet 패키지를 프로젝트로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ffddf-203">Data Factory 서비스 시작 관리자에는 4.3 버전의 WindowsAzure.Storage가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="ffddf-204">사용자 지정 작업 프로젝트에서 이후 버전의 Azure Storage 어셈블리에 대한 참조를 추가한 경우 작업을 실행할 때 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="ffddf-205">이 오류를 해결하려면 [Appdomain 격리](#appdomain-isolation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="ffddf-206">다음 **using** 문을 프로젝트의 원본 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-206">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="ffddf-207">**namespace**의 이름을 **MyDotNetActivityNS**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="ffddf-208">클래스 이름을 **MyDotNetActivity**로 변경하고 다음 코드 조각에서 보여 주듯이 **IDotNetActivity** 인터페이스에서 해당 클래스를 파생합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="ffddf-209">**IDotNetActivity** 인터페이스의 **Execute** 메서드를 **MyDotNetActivity** 클래스에 구현(추가)하고 다음 샘플 코드를 메서드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="ffddf-210">다음 샘플은 데이터 조각과 연결된 각 Blob의 검색 단어("Microsoft") 발생 횟수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="ffddf-211">다음과 같은 도우미 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-211">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="ffddf-212">GetFolderPath 메서드는 데이터 집합이 가리키는 폴더로 경로를 반환하고 GetFileName 메서드는 데이터 집합이 가리키는 BLOB/파일의 이름을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="ffddf-213">{Year}, {Month}, {Day} 등의 변수를 사용하여 폴더 경로를 정의하면 이 메서드는 변수를 런타임 값으로 바꾸지 않고 문자열을 있는 그대로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="ffddf-214">SliceStart, SliceEnd 등에 대한 액세스에 대해 자세히 알아보려면 [확장 속성 액세스](#access-extended-properties) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="ffddf-215">Calculate 메서드는 입력 파일(폴더에서 BLOB)에서 Microsoft 키워드의 인스턴스 수를 계산합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="ffddf-216">검색 용어("Microsoft")는 코드에 하드 코딩됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="ffddf-217">프로젝트를 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-217">Compile the project.</span></span> <span data-ttu-id="ffddf-218">메뉴에서 **빌드**, **솔루션 빌드**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ffddf-219">4.5.2 버전의 .NET Framework를 프로젝트의 대상 프레임워크로 설정합니다. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭하여 대상 프레임워크를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="ffddf-220">데이터 팩터리는 .NET Framework 4.5.2 이후 버전에 대해 컴파일된 사용자 지정 작업을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="ffddf-221">**Windows 탐색기**를 시작하고 빌드 유형에 따라 **bin\debug** 또는 **bin\release** 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="ffddf-222"><project folder>\bin\Debug 폴더의 이진을 모두 포함하는 **MyDotNetActivity.zip** Zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="ffddf-223">오류가 있는 경우 문제를 발생시킨 소스 코드의 줄 번호 같은 추가 정보를 받을 수 있도록 **MyDotNetActivity.pdb** 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="ffddf-224">사용자 지정 작업에 대한 zip 파일의 모든 파일은 하위 폴더가 없는 **최상위** 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![이진 출력 파일](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="ffddf-226">명명된 Blob 컨테이너 **customactivitycontainer**가 아직 없는 경우 새로 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="ffddf-227">MyDotNetActivity.zip을 AzureStorageLinkedService에서 참조되는 **범용** Azure Blob Storage(핫/쿨 Blob Storage 아님)의 customactivitycontainer에 Blob으로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ffddf-228">Data Factory 프로젝트를 포함하는 Visual Studio의 솔루션에 이 .NET 작업 프로젝트를 추가하고 Data Factory 응용 프로그램 프로젝트의 .NET 작업 프로젝트에 참조를 추가하는 경우에는 zip 파일을 만들고 범용 Azure Blob Storage에 업로드하는 마지막 두 단계를 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="ffddf-229">Visual Studio를 사용하여 데이터 팩터리 엔터티를 게시하면 이러한 단계가 게시 프로세스에서 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="ffddf-230">자세한 내용은 [Visual Studio의 데이터 팩터리 프로젝트](#data-factory-project-in-visual-studio) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="ffddf-231">사용자 지정 작업을 포함하는 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="ffddf-232">사용자 지정 작업을 만들어 이진 파일이 있는 zip 파일을 **범용** Azure Storage 계정의 Blob 컨테이너에 업로드했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="ffddf-233">이 섹션에서는 사용자 지정 작업을 사용하는 파이프라인으로 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="ffddf-234">사용자 지정 작업에 대한 입력 데이터 집합은 Blob Storage에서 adftutorial 컨테이너의 customactivityinput 폴더에 있는 Blob(파일)을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="ffddf-235">작업에 대한 출력 데이터 집합은 Blob Storage에서 adftutorial 컨테이너의 customactivityoutput 폴더에 있는 출력 Blob을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="ffddf-236">다음 내용이 포함된 **file.txt** 파일을 만들고 **adftutorial** 컨테이너의 **customactivityinput** 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="ffddf-237">아직 없는 경우 adftutorial 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="ffddf-238">입력 폴더는 폴더에 2개 이상의 파일이 포함된 경우에도 Azure Data Factory의 조각에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="ffddf-239">각 조각이 파이프라인으로 처리될 때 사용자 지정 작업은 해당 조각에 대한 입력 폴더에서 모든 BLOB를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="ffddf-240">adftutorial\customactivityoutput 폴더에 1개 이상의 줄(입력 폴더에서 Blob 수와 동일)이 포함된 하나의 출력 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="ffddf-241">이 섹션에서 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="ffddf-242">**데이터 팩터리**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="ffddf-243">사용자 지정 작업이 실행되는 VM의 Azure Batch 풀과 입/출력 Blob을 보유하는 Azure Storage에 대한 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="ffddf-244">사용자 지정 작업의 입력 및 출력을 나타내는 입력 및 출력 **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="ffddf-245">사용자 지정 작업을 사용하는 **파이프라인**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="ffddf-246">아직 **file.txt** 을 만들어서 Blob 컨테이너에 업로드하지 않았으면 지금 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="ffddf-247">이전 섹션의 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="ffddf-248">1단계: 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="ffddf-249">Azure Portal에 로그인한 후에 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="ffddf-250">왼쪽 메뉴에서 **새로 만들기** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="ffddf-251">**새** 블레이드에서 **데이터 + 분석**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="ffddf-252">**데이터 분석** 블레이드에서 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![새 Azure Data Factory 메뉴](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="ffddf-254">**새 Data Factory** 블레이드에서 이름으로 **CustomActivityFactory**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="ffddf-255">Azure Data Factory 이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="ffddf-256">**"CustomActivityFactory" Data Factory 이름은 사용할 수 없습니다.**라는 오류 메시지가 표시되는 경우 Data Factory 이름을 변경하고(예: **yournameCustomActivityFactory**) 해당 Data Factory를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![새 Azure Data Factory 블레이드](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="ffddf-258">**리소스 그룹 이름**을 클릭하여 기존 리소스 그룹을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="ffddf-259">**subscription** 및 Data Factory를 만들려는 **region**을 제대로 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="ffddf-260">**새 Data Factory** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="ffddf-261">Azure 포털의 **대시보드** 에 생성된 데이터 팩터리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="ffddf-262">데이터 팩터리 만들기를 완료한 후에는 Data Factory 블레이드가 표시되며 여기에 데이터 팩터리의 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![데이터 팩터리 블레이드](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="ffddf-264">2단계: 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-264">Step 2: Create linked services</span></span>
<span data-ttu-id="ffddf-265">연결된 서비스는 데이터 저장소 또는 계산 서비스를 Azure Data Factory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="ffddf-266">이 단계에서는 Azure Storage 계정 및 Azure 배치 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ffddf-267">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="ffddf-268">**CustomActivityFactory**에 대한 **Data Factory** 블레이드에서 **작성 및 배포 타일**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="ffddf-269">데이터 팩터리 편집기가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="ffddf-270">명령 모음에서 **새 데이터 저장소**를 클릭하고 **Azure 저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="ffddf-271">편집기에 Azure 저장소 연결된 서비스를 만들기 위한 JSON 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![새 데이터 저장소 - Azure Storage](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="ffddf-273">`<accountname>`을 Azure Storage 계정 이름으로 바꾸고 `<accountkey>`를 Azure Storage 계정의 액세스 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="ffddf-274">저장소 액세스 키를 확보하는 방법을 알아보려면 [저장소 액세스 키 보기, 복사 및 다시 생성](../storage/common/storage-create-storage-account.md#manage-your-storage-account)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure Storage 연결 서비스](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="ffddf-276">명령 모음에서 **배포**를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="ffddf-277">Azure 배치 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="ffddf-278">Data Factory Editor의 도구 모음에서 **... 추가**를 클릭하고 **새 계산**을 클릭한 다음 메뉴에서 **Azure 배치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![새 계산 - Azure 배치](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="ffddf-280">JSON 스크립트를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ffddf-281">**accountName** 속성의 Azure 배치 계정 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="ffddf-282">**Azure 배치 계정 블레이드**의 **URL**은 `http://accountname.region.batch.azure.com` 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="ffddf-283">JSON의 **batchUri** 속성에 대해 URL에서 `accountname.`을 제거하고 `accountName` JSON 속성에 대해 `accountname`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="ffddf-284">**accessKey** 속성에 대한 Azure 배치 계정 키를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="ffddf-285">**poolName** 속성에 대한 필수 조건의 일부로 만든 풀의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="ffddf-286">풀 이름 대신 풀 ID를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="ffddf-287">**batchUri** 속성에 대한 Azure 배치 URI를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="ffddf-288">예: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ffddf-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="ffddf-289">**AzureStorageLinkedService** for the **linkedServiceName** 속성의 Azure 배치 계정 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="ffddf-290">**poolName** 속성의 경우 풀 이름 대신 풀 ID를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="ffddf-291">데이터 팩터리 서비스는 HDInsight에 대해서와 마찬가지로 Azure Batch에 대한 주문형 옵션을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="ffddf-292">Azure Data Factory에서는 사용자 고유의 Azure Batch 풀만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="ffddf-293">3단계: 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-293">Step 3: Create datasets</span></span>
<span data-ttu-id="ffddf-294">이 단계에서는 입력 및 출력 데이터를 나타낼 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="ffddf-295">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-295">Create input dataset</span></span>
1. <span data-ttu-id="ffddf-296">Data Factor의 **편집기**에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 **Azure Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="ffddf-297">오른쪽 창의 JSON을 다음 JSON 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="ffddf-298">이 연습에서는 시작 시간: 2016-11-16T00:00:00Z 및 종료 시간: 2016-11-16T05:00:00Z로 나중에 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="ffddf-299">매시간 데이터를 생성하도록 예약되어 있어 5개의 입/출력 조각이 있습니다(**00**:00:00 -> **05**:00:00 범위).</span><span class="sxs-lookup"><span data-stu-id="ffddf-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="ffddf-300">입력 데이터 집합의 **빈도** 및 **간격**은 **Hour** 및 **1**로 설정되며 이는 입력 조각이 매시간 제공됨을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="ffddf-301">이 샘플에서는 intputfolder에서와 동일한 파일(file.txt)입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="ffddf-302">다음은 각 조각에 대한 시작 시간이며 위의 JSON 코드 조각에서 SliceStart 시스템 변수로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="ffddf-303">도구 모음에서 **배포**를 클릭하여 **InputDataset**을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="ffddf-304">편집기의 제목 표시줄에 **테이블이 성공적으로 생성됨** 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="ffddf-305">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-305">Create an output dataset</span></span>
1. <span data-ttu-id="ffddf-306">**데이터 팩터리 편집기**의 명령 모음에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭한 다음 **Azure Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="ffddf-307">오른쪽 창의 JSON 스크립트를 다음 JSON 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="ffddf-308">출력 위치는 **adftutorial/customactivityoutput/**이고 출력 파일 이름은 yyyy-MM-dd-HH.txt입니다. 여기서 yyyy-MM-dd-HH는 조각이 생성되는 년, 월, 일 및 시입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="ffddf-309">자세한 내용은 [개발자 참조][adf-developer-reference](영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="ffddf-310">각 입력 조각에 대해 출력 BLOB/파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="ffddf-311">각 조각에 대해 출력 파일의 이름을 지정하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="ffddf-312">출력 파일은 모두 **adftutorial\customactivityoutput**이라는 하나의 출력 폴더에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="ffddf-313">조각</span><span class="sxs-lookup"><span data-stu-id="ffddf-313">Slice</span></span> | <span data-ttu-id="ffddf-314">시작 시간</span><span class="sxs-lookup"><span data-stu-id="ffddf-314">Start time</span></span> | <span data-ttu-id="ffddf-315">출력 파일</span><span class="sxs-lookup"><span data-stu-id="ffddf-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="ffddf-316">1</span><span class="sxs-lookup"><span data-stu-id="ffddf-316">1</span></span> |<span data-ttu-id="ffddf-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="ffddf-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="ffddf-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="ffddf-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="ffddf-319">2</span><span class="sxs-lookup"><span data-stu-id="ffddf-319">2</span></span> |<span data-ttu-id="ffddf-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="ffddf-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="ffddf-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="ffddf-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="ffddf-322">3</span><span class="sxs-lookup"><span data-stu-id="ffddf-322">3</span></span> |<span data-ttu-id="ffddf-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="ffddf-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="ffddf-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="ffddf-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="ffddf-325">4</span><span class="sxs-lookup"><span data-stu-id="ffddf-325">4</span></span> |<span data-ttu-id="ffddf-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="ffddf-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="ffddf-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="ffddf-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="ffddf-328">5</span><span class="sxs-lookup"><span data-stu-id="ffddf-328">5</span></span> |<span data-ttu-id="ffddf-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="ffddf-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="ffddf-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="ffddf-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="ffddf-331">입력 폴더에 있는 모든 파일은 위에 언급된 시작 시간의 조각 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="ffddf-332">이 조각을 처리할 때 사용자 지정 작업은 각 파일을 검색하고 검색 용어("Microsoft") 항목 수와 함께 출력 파일에 줄을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="ffddf-333">inputfolder에 세 개의 파일이 있는 경우 출력 파일에 각 시간별 조각에 해당하는 세 개의 줄이 생깁니다(예: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt 등).</span><span class="sxs-lookup"><span data-stu-id="ffddf-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="ffddf-334">**OutputDataset**을 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="ffddf-335">사용자 지정 작업을 사용하는 파이프라인 만들기 및 실행</span><span class="sxs-lookup"><span data-stu-id="ffddf-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="ffddf-336">Data Factory Editor의 도구 모음에서 **... 추가**를 클릭한 다음 명령 모음에서 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="ffddf-337">오른쪽 창의 JSON을 다음 JSON 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-337">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="ffddf-338">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-338">Note the following points:</span></span>

   * <span data-ttu-id="ffddf-339">Azure 배치 풀의 VM 2대에서 2개 조각을 동시에 처리하도록 **동시성**이 **2**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="ffddf-340">activities 섹션에는 **DotNetActivity**유형의 작업 하나밖에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="ffddf-341">**AssemblyName**은 **MyDotnetActivity.dll** DLL 이름으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="ffddf-342">**EntryPoint**는 **MyDotNetActivityNS.MyDotNetActivity**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="ffddf-343">**PackageLinkedService**는 사용자 지정 작업 Zip 파일을 포함하는 Blob 저장소를 가리키는 **AzureStorageLinkedService**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="ffddf-344">입/출력 파일 및 사용자 지정 작업 zip 파일에 대해 서로 다른 Azure Storage 계정을 사용하는 경우 다른 Azure Storage 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="ffddf-345">이 문서에서는 동일한 Azure 저장소 계정을 사용 중이라고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="ffddf-346">**PackageFile**은 **customactivitycontainer/MyDotNetActivity.zip**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="ffddf-347">containerforthezip/nameofthezip.zip 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="ffddf-348">사용자 지정 작업은 입력으로 **InputDataset**, 출력으로 **OutputDataset**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="ffddf-349">사용자 지정 활동의 linkedServiceName 속성은 **AzureBatchLinkedService**를 가리키며 Azure Data Factory에 사용자 지정 작업을 Azure 배치 VM에서 실행해야 함을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="ffddf-350">**isPaused** 속성은 기본적으로 **false**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="ffddf-351">이 예제에서는 조각이 이전에 시작되므로 파이프라인이 즉시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="ffddf-352">파이프라인을 일시 중지하려면 이 속성을 true로 설정하고 다시 시작하려면 false로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="ffddf-353">**start** 시간과 **end** 시간은 **5**시간 차이이며 파이프라인이 작동하면서 매시간 5개 조각이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="ffddf-354">파이프라인을 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="ffddf-355">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="ffddf-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="ffddf-356">Azure 포털의 Data Factory 블레이드에서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![다이어그램 타일](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="ffddf-358">다이어그램 뷰에서 OutputDataset을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![다이어그램 뷰](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="ffddf-360">5개의 출력 조각이 준비 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="ffddf-361">준비 상태가 아닌 경우 아직 생성되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![출력 분할](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="ffddf-363">출력 파일이 **adftutorial** 컨테이너의 Blob 저장소에 생성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![사용자 지정 작업의 출력][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="ffddf-365">출력 파일을 열면 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="ffddf-366">[Azure 포털][azure-preview-portal] 또는 Azure PowerShell cmdlet을 사용하여 데이터 팩터리, 파이프라인 및 데이터 집합을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="ffddf-367">포털을 통해서나 cmdlet을 사용하여 다운로드할 수 있는 로그(특히 user-0.log)에 있는 사용자 지정 활동의 코드에서 **ActivityLogger** 의 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![사용자 지정 작업의 로그 다운로드][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="ffddf-369">데이터 집합 및 파이프라인 모니터링에 대한 자세한 단계는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="ffddf-370">Visual Studio의 데이터 팩터리 프로젝트</span><span class="sxs-lookup"><span data-stu-id="ffddf-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="ffddf-371">Azure Portal 대신 Visual Studio를 사용하여 데이터 팩터리 엔터티를 만들고 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="ffddf-372">Visual Studio를 사용하여 데이터 팩터리 엔터티를 만들고 게시하는 방법에 대한 자세한 내용은 [Visual Studio를 사용하여 첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline-using-vs.md) 및 [Azure Blob에서 Azure SQL로 데이터 복사](data-factory-copy-activity-tutorial-using-visual-studio.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="ffddf-373">Visual Studio에서 데이터 팩터리 프로젝트를 만드는 경우 다음과 같은 추가 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="ffddf-374">사용자 지정 작업 프로젝트가 포함된 Visual Studio 솔루션에 데이터 팩터리 프로젝트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="ffddf-375">데이터 팩터리 프로젝트에서 .NET 작업 프로젝트에 대한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="ffddf-376">데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가**를 가리킨 다음 **참조**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="ffddf-377">**참조 추가** 대화 상자에서 **MyDotNetActivity** 프로젝트를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="ffddf-378">솔루션을 빌드하여 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ffddf-379">데이터 팩터리 엔터티를 게시하면 zip 파일이 자동으로 생성되어 Blob 컨테이너 customactivitycontainer에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="ffddf-380">Blob 컨테이너가 없으면 자동으로 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="ffddf-381">Data Factory 및 배치 통합</span><span class="sxs-lookup"><span data-stu-id="ffddf-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="ffddf-382">Data Factory 서비스가 Azure Batch에 **adf-poolname:job-xxx**라는 이름으로 작업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="ffddf-383">왼쪽 메뉴에서 **작업**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-383">Click **Jobs** from the left menu.</span></span> 

![Azure Data Factory - 배치 작업](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="ffddf-385">조각의 각 작업 실행에 대한 작업(task)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="ffddf-386">처리를 위해 준비된 5개 조각이 있는 경우 이 작업(job)에 5개 작업(task)이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="ffddf-387">Batch 풀에 여러 계산 노드가 있는 경우 두 개 이상의 조각을 병렬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="ffddf-388">계산 노드당 최대 작업이 1보다 크게 설정된 경우에도 동일한 계산에 실행 중인 두 개 이상의 조각을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Azure Data Factory - 배치 작업 태스크](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="ffddf-390">다음 다이어그램에서는 Azure Data Factory 및 배치 작업 간의 관계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![데이터 팩터리 및 배치](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="ffddf-392">오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="ffddf-392">Troubleshoot failures</span></span>
<span data-ttu-id="ffddf-393">문제 해결은 몇 가지 기본적인 방법으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="ffddf-394">다음과 같은 오류가 표시되면 범용 Azure Blob Storage를 사용하는 대신 핫/쿨 Blob Storage를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="ffddf-395">zip 파일을 **범용 Azure Storage 계정**에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="ffddf-396">다음과 같은 오류가 나타나면 CS 파일에서 클래스 이름이 파이프라인 JSON에서 **EntryPoint** 속성에 대해 지정한 이름과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="ffddf-397">이 연습에서 클래스의 이름은 MyDotNetActivity이고 JSON의 진입점은 MyDotNetActivityNS.**MyDotNetActivity**입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="ffddf-398">이름이 일치하는 경우 zip 파일의 **루트 폴더** 에 모든 이진 파일이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="ffddf-399">즉, zip 파일을 열 때 하위 폴더가 아닌 루트 폴더에 모든 파일이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="ffddf-400">입력 조각이 **Ready**로 설정되지 않은 경우 입력 폴더 구조가 올바르고 **file.txt**가 입력 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="ffddf-401">사용자 지정 작업의 **Execute** 메서드에서 **IActivityLogger** 개체를 사용하여 문제 해결에 도움이 되는 정보를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="ffddf-402">기록된 메시지는 사용자 로그 파일(다음과 같은 이름의 파일 하나 또는 여러 개: user-0.log, user-1.log, user-2.log 등)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="ffddf-403">**OutputDataset** 블레이드에서 조각에 대한 **데이터 조각** 블레이드를 보려면 해당 조각을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="ffddf-404">해당 조각에 대한 **작업 실행** 이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="ffddf-405">해당 조각에 대한 하나의 작업 실행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="ffddf-406">명령 모음에서 실행을 클릭하면 동일한 조각에 대해 다른 작업 실행을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="ffddf-407">작업 실행을 클릭하면 로그 파일 목록과 함께 **작업 실행 세부 정보** 블레이드가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="ffddf-408">기록된 메시지는 user_0.log 파일에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="ffddf-409">오류가 발생하면 파이프라인/작업 JSON에서 재시도 횟수가 3으로 설정되므로 세 개의 작업 실행이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="ffddf-410">작업 실행을 클릭하면 문제 해결을 위해 검토할 수 있는 로그 파일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="ffddf-411">로그 파일 목록에서 **user-0.log**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="ffddf-412">오른쪽 패널은 **IActivityLogger.Write** 메서드를 사용한 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="ffddf-413">일부 메시지가 보이지 않으면 user_1.log, user_2.log 등 비슷한 이름의 로그 파일이 더 있는지 확인합니다. 로그 파일이 더 없으면 마지막 메시지가 기록된 후에 코드가 실패한 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="ffddf-414">또한 **system-0.log**에서 시스템 오류 메시지 및 예외를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="ffddf-415">Zip 파일에 **PDB** 파일을 포함하여 오류 발생 시 오류 세부 정보에 **호출 스택**과 같은 정보가 포함되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="ffddf-416">사용자 지정 작업에 대한 zip 파일의 모든 파일은 하위 폴더가 없는 **최상위** 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="ffddf-417">**assemblyName**(MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile**(customactivitycontainer/MyDotNetActivity.zip) 및 **packageLinkedService**(zip 파일을 포함하는 **범용** Azure Blob Storage를 가리켜야 함)가 올바른 값으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="ffddf-418">오류를 해결했고 조각을 다시 처리하려면 **OutputDataset** 블레이드에서 조각을 마우스 오른쪽 단추로 클릭하고 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="ffddf-419">다음 오류가 표시되면 4.3.0 이후 버전의 Azure Storage 패키지를 사용하고 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="ffddf-420">Data Factory 서비스 시작 관리자에는 4.3 버전의 WindowsAzure.Storage가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="ffddf-421">이후 버전의 Azure Storage 어셈블리를 사용해야 하는 경우 해결 방법은 [Appdomain 격리](#appdomain-isolation) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="ffddf-422">4.3.0 버전의 Azure Storage 패키지를 사용할 수 있는 경우 4.3.0 이후 버전의 Azure Storage 패키지에 대한 기존 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="ffddf-423">그런 다음 NuGet 패키지 관리자 콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="ffddf-424">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-424">Build the project.</span></span> <span data-ttu-id="ffddf-425">bin\Debug 폴더에서 4.3.0 이후 버전의 Azure.Storage 어셈블리를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="ffddf-426">이진 파일 및 PDB 파일이 포함된 zip 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="ffddf-427">Blob 컨테이너(customactivitycontainer)에서 이전 zip 파일을 새 zip 파일로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="ffddf-428">실패한 조각을 다시 실행합니다(조각을 마우스 오른쪽 단추로 클릭하고 실행을 클릭).</span><span class="sxs-lookup"><span data-stu-id="ffddf-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="ffddf-429">사용자 지정 작업은 패키지에서 **app.config** 파일을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="ffddf-430">따라서 코드가 구성 파일에서 연결 문자열을 읽는 경우 런타임 시 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="ffddf-431">Azure 배치를 사용할 경우 **Azure KeyVault**에 모든 암호를 저장하고, 인증서 기반 서비스 주체를 사용하여 **KeyVault**을 보호하고, 인증서를 Azure 배치 풀에 배포하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="ffddf-432">그러면 .NET 사용자 지정 활동은 런타임에 주요 자격 증명 모음의 암호에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="ffddf-433">이 솔루션은 일반 솔루션이며 연결 문자열뿐 아니라 모든 유형의 암호로 확장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="ffddf-434">최상은 아니지만 좀 더 쉬운 해결 방법이 있습니다. 즉 연결 문자열 설정을 사용하여 **Azure SQL 연결 서비스**를 만들고, 이 서비스를 사용하는 데이터 집합을 만든 다음 사용자 지정 .NET 작업에 이 데이터 집합을 더미 입력 데이터 집합으로 연결하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="ffddf-435">그런 다음 사용자 지정 활동 코드에서 연결된 서비스의 연결 문자열에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="ffddf-436">사용자 지정 작업 업데이트</span><span class="sxs-lookup"><span data-stu-id="ffddf-436">Update custom activity</span></span>
<span data-ttu-id="ffddf-437">사용자 지정 작업의 코드를 업데이트하는 경우 코드를 작성하고 새 이진이 포함된 zip 파일을 Blob 저장소로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="ffddf-438">Appdomain 격리</span><span class="sxs-lookup"><span data-stu-id="ffddf-438">Appdomain isolation</span></span>
<span data-ttu-id="ffddf-439">Data Factory 시작 관리자에서 사용하는 어셈블리 버전(예: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x 등)의 제약을 받지 않는 사용자 지정 작업을 만드는 방법을 보여 주는 [크로스 AppDomain 샘플](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="ffddf-440">확장 속성 액세스</span><span class="sxs-lookup"><span data-stu-id="ffddf-440">Access extended properties</span></span>
<span data-ttu-id="ffddf-441">다음 샘플과 같이 작업 JSON에서 확장 속성을 선언할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="ffddf-442">이 예제에는 두 가지 확장 속성, **SliceStart** 및 **DataFactoryName**이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="ffddf-443">SliceStart의 값은 SliceStart 시스템 변수를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="ffddf-444">지원되는 시스템 변수 목록은 [시스템 변수](data-factory-functions-variables.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="ffddf-445">DataFactoryName의 값은 CustomActivityFactory로 하드 코드됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="ffddf-446">**Execute** 메서드에서 이러한 확장 속성에 액세스하려면 다음 코드와 유사한 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="ffddf-447">Azure Batch의 자동 확장</span><span class="sxs-lookup"><span data-stu-id="ffddf-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="ffddf-448">**자동 크기 조정** 기능으로 Azure 배치 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="ffddf-449">예를 들어 보류 중인 작업의 수에 따라 전용 VM 0개 및 자동 크기 조정 수식을 사용하여 Azure 배치 풀을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="ffddf-450">여기에 나오는 샘플 수식은 다음과 같은 동작을 구현합니다. 풀이 처음 만들어질 때는 VM 1개로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="ffddf-451">$PendingTasks 메트릭은 실행되거나 큐에 대기 중인 활성 상태의 작업 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="ffddf-452">이 수식은 지난 180초 동안에서 보류 중인 작업의 평균 수를 찾은 후 그에 따라 TargetDedicated를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="ffddf-453">또한 TargetDedicated가 25개의 VM을 초과하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="ffddf-454">따라서 새 작업이 제출되면 풀이 자동으로 커지고, 작업이 완료되면 VM은 하나씩 사용 가능한 상태로 해제된 후 자동 크기 조정에 따라 해당 VM이 축소됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="ffddf-455">startingNumberOfVMs 및 maxNumberofVMs은 요구에 맞게 조정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="ffddf-456">자동 크기 조정 수식:</span><span class="sxs-lookup"><span data-stu-id="ffddf-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="ffddf-457">자세한 내용은 [Azure 배치 풀에서 자동으로 계산 노드 크기 조정](../batch/batch-automatic-scaling.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="ffddf-458">풀에 기본 [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx)이 사용되는 경우, 배치 서비스가 사용자 지정 작업을 실행하기 전에 VM을 준비하는 데 15~30분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="ffddf-459">풀에 다른 autoScaleEvaluationInterval이 사용되는 경우, 배치 서비스는 autoScaleEvaluationInterval +10분이 소요될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="ffddf-460">HDInsight 계산 서비스 사용</span><span class="sxs-lookup"><span data-stu-id="ffddf-460">Use HDInsight compute service</span></span>
<span data-ttu-id="ffddf-461">이 연습에서는 Azure 배치 계산을 사용하여 사용자 지정 작업을 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="ffddf-462">또한 사용자 고유의 Windows 기반 HDInsight 클러스터를 사용할 수도 있고, 데이터 팩터리가 주문형 Windows 기반 HDInsight 클러스터를 만들고 그 HDInsight 클러스터에서 사용자 지정 작업을 실행하게 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="ffddf-463">다음은 HDInsight 클러스터를 사용하는 고급 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffddf-464">사용자 지정 .NET 작업은 Windows 기반 HDInsight 클러스터에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ffddf-465">이 제한 사항에 대한 해결 방법은 MapReduce 작업을 사용하여 Linux 기반 HDInsight 클러스터에서 사용자 지정 Java 코드를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ffddf-466">또 다른 옵션은 VM의 Azure Batch 풀을 사용하여 HDInsight 클러스터를 사용하는 대신 사용자 지정 작업을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="ffddf-467">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="ffddf-468">파이프라인 JSON에 **AzureBatchLinkedService** 대신 HDInsight 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="ffddf-469">연습을 테스트해 보려면 Azure HDInsight 서비스를 사용하는 시나리오를 테스트할 수 있도록 파이프라인의 **start** 및 **end** 시간을 변경하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="ffddf-470">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="ffddf-471">Azure Data Factory 서비스는 주문형 클러스터 만들기를 지원하며 이 클러스터를 사용하여 입력을 처리하고 출력 데이터를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="ffddf-472">또한 고유한 클러스터를 사용하여 같은 작업을 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="ffddf-473">주문형 HDInsight 클러스터를 사용하면 각 조각에 대해 클러스터가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="ffddf-474">반면 고유한 HDInsight 클러스터를 사용하는 경우에는 클러스터에서 조각을 즉시 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="ffddf-475">따라서 주문형 클러스터를 사용하는 경우 출력 데이터가 고유한 클러스터를 사용할 때처럼 빠르게 표시되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ffddf-476">런타임에 .NET 작업의 한 인스턴스는 HDInsight 클러스터의 작업자 노드 하나에서만 실행됩니다. 여러 노드에서 실행되도록 확장할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="ffddf-477">.NET 작업의 여러 인스턴스는 HDInsight 클러스터의 서로 다른 노드에서 병렬로 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="ffddf-478">주문형 HDInsight 클러스터를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="ffddf-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="ffddf-479">**Azure 배치 계정**에서 왼쪽의 **작성자 및 배포** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="ffddf-480">Data Factory 편집기의 명령 모음에서 **새 계산**을 클릭하고 메뉴에서 **주문형 HDInsight 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="ffddf-481">JSON 스크립트를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ffddf-482">**clusterSize** 속성에 대해 HDInsight 클러스터의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="ffddf-483">**timeToLive** 속성에 대해 고객이 삭제되기 전에 유휴 상태로 유지될 수 있는 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="ffddf-484">**version** 속성에 대해 사용할 HDInsight 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="ffddf-485">이 속성을 제외하면 최신 버전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="ffddf-486">**linkedServiceName**에 대해 **AzureStorageLinkedService**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="ffddf-487">사용자 지정 .NET 작업은 Windows 기반 HDInsight 클러스터에서만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ffddf-488">이 제한 사항에 대한 해결 방법은 MapReduce 작업을 사용하여 Linux 기반 HDInsight 클러스터에서 사용자 지정 Java 코드를 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="ffddf-489">또 다른 옵션은 VM의 Azure Batch 풀을 사용하여 HDInsight 클러스터를 사용하는 대신 사용자 지정 작업을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="ffddf-490">명령 모음에서 **배포**를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="ffddf-491">고유한 HDInsight 클러스터를 사용하려면</span><span class="sxs-lookup"><span data-stu-id="ffddf-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="ffddf-492">**Azure 배치 계정**에서 왼쪽의 **작성자 및 배포** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="ffddf-493">**Data Factory 편집기**의 명령 모음에서 **새 계산**을 클릭하고 메뉴에서 **HDInsight 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="ffddf-494">JSON 스크립트를 다음과 같이 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="ffddf-495">**clusterUri** 속성에 대해 HDInsight의 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="ffddf-496">예를 들어 https://<clustername>.azurehdinsight.net/을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="ffddf-497">**UserName** 속성에 대해 HDInsight 클러스터에 액세스할 수 있는 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="ffddf-498">**password** 속성에 대해 사용자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="ffddf-499">**LinkedServiceName** 속성에 대해 **AzureStorageLinkedService**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="ffddf-500">명령 모음에서 **배포**를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="ffddf-501">자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="ffddf-502">**파이프라인 JSON**에서 HDInsight(주문형 또는 사용자 고유의) 연결된 서비스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="ffddf-503">.NET SDK를 사용하여 사용자 지정 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="ffddf-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="ffddf-504">이 문서의 연습에서는 Azure Portal을 사용하여 사용자 지정 작업을 사용하는 파이프라인이 포함된 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="ffddf-505">다음 코드는 .NET SDK를 대신 사용하여 데이터 팩터리를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="ffddf-506">SDK를 사용하여 프로그래밍 방식으로 파이프라인을 만드는 방법에 대한 자세한 내용은 [.NET API를 사용하여 복사 작업이 포함된 파이프라인 만들기](data-factory-copy-activity-tutorial-using-dotnet-api.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffddf-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="ffddf-507">Visual Studio에서 사용자 지정 작업 디버깅</span><span class="sxs-lookup"><span data-stu-id="ffddf-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="ffddf-508">GitHub의 [Azure Data Factory - 로컬 환경](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) 샘플은 Visual Studio 내에서 사용자 지정 .NET 작업을 디버깅할 수 있는 도구를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="ffddf-509">GitHub의 샘플 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="ffddf-510">샘플</span><span class="sxs-lookup"><span data-stu-id="ffddf-510">Sample</span></span> | <span data-ttu-id="ffddf-511">사용자 지정 작업의 기능</span><span class="sxs-lookup"><span data-stu-id="ffddf-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="ffddf-512">[HTTP 데이터 다운로더](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)</span><span class="sxs-lookup"><span data-stu-id="ffddf-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="ffddf-513">Data Factory의 사용자 지정 C# 작업을 사용하여 HTTP 끝점에서 Azure Blob 저장소로 데이터를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="ffddf-514">Twitter 감성 분석 샘플</span><span class="sxs-lookup"><span data-stu-id="ffddf-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="ffddf-515">Azure ML 모델을 호출하고 감성 분석, 점수 매기기, 예측 등을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="ffddf-516">[R 스크립트 실행](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)</span><span class="sxs-lookup"><span data-stu-id="ffddf-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="ffddf-517">R이 이미 설치된 HDInsight 클러스터에서 RScript.exe를 실행하여 R 스크립트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="ffddf-518">크로스 AppDomain .NET 작업</span><span class="sxs-lookup"><span data-stu-id="ffddf-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="ffddf-519">Data Factory 시작 관리자가 사용한 것과 다른 버전의 어셈블리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="ffddf-520">Azure Analysis Services에서 모델 다시 처리</span><span class="sxs-lookup"><span data-stu-id="ffddf-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="ffddf-521">Azure Analysis Services에서 모델을 다시 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="ffddf-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
