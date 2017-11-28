---
title: "Azure Data Factory에서 Spark 프로그램 호출 | Microsoft Docs"
description: "MapReduce 작업을 사용하여 Azure Data Factory에서 Spark 프로그램을 호출하는 방법에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="dc044-103">Azure Data Factory 파이프라인에서 Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="dc044-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="dc044-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="dc044-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="dc044-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="dc044-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="dc044-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="dc044-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="dc044-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="dc044-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="dc044-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="dc044-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="dc044-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="dc044-114">소개</span><span class="sxs-lookup"><span data-stu-id="dc044-114">Introduction</span></span>
<span data-ttu-id="dc044-115">Spark 활동은 Azure Data Factory에서 지원하는 [데이터 변환 활동](data-factory-data-transformation-activities.md) 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="dc044-116">이 활동은 Azure HDInsight의 Apache Spark 클러스터에서 지정된 Spark 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="dc044-117">Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="dc044-118">Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="dc044-119">주문형 HDInsight 연결된 서비스는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="dc044-120">연습: Spark 활동이 포함된 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="dc044-121">Spark 활동이 포함된 Data Factory 파이프라인을 만드는 일반적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="dc044-122">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-122">Create a data factory.</span></span>
2. <span data-ttu-id="dc044-123">Azure Storage 연결된 서비스를 만들어 HDInsight Spark 클러스터와 연결된 Azure 저장소를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="dc044-124">Azure HDInsight 연결된 서비스를 만들어 Azure HDInsight의 Apache Spark 클러스터를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="dc044-125">Azure Storage 연결된 서비스를 참조하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="dc044-126">현재 생성 중인 출력이 없더라도 작업의 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="dc044-127">2단계에서 만든 Apache HDInsight 연결된 서비스를 참조하는 Spark 활동을 포함하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="dc044-128">이 작업은 이전 단계에서 출력 데이터 집합으로 만든 데이터 집합을 통해 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="dc044-129">출력 데이터 집합은 일정(매시간, 매일 등)을 구동하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="dc044-130">따라서 작업에서 실제로 출력을 생성하지 않더라도 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dc044-131">필수 조건</span><span class="sxs-lookup"><span data-stu-id="dc044-131">Prerequisites</span></span>
1. <span data-ttu-id="dc044-132">연습의 [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account) 지침에 따라 **범용 Azure Storage 계정**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="dc044-133">자습서의 [Azure HDInsight에서 Apache Spark 클러스터 만들기](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) 지침에 따라 **Azure HDInsight에서 Apache Spark 클러스터**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="dc044-134">1단계에서 만든 Azure 저장소 계정을 이 클러스터와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="dc044-135">[https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)에 있는 **test.py** python 스크립트 파일을 다운로드하여 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="dc044-136">Azure Blob 저장소의 **adfspark** 컨테이너에 있는 **test.py**를 **pyFiles** 폴더로 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="dc044-137">컨테이너와 폴더가 없으면 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="dc044-138">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-138">Create data factory</span></span>
<span data-ttu-id="dc044-139">이 단계에서는 데이터 팩터리 만들기를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="dc044-140">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dc044-141">왼쪽 메뉴에서 **새로 만들기**를 클릭하고 **데이터 + 분석**을 클릭하고 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="dc044-142">**새 데이터 팩터리** 블레이드에서 이름으로 **SparkDF**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dc044-143">Azure Data Factory의 이름은 **전역적으로 고유**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="dc044-144">**"SparkDF" 데이터 팩터리 이름은 사용할 수 없습니다** 오류가 표시되는 경우</span><span class="sxs-lookup"><span data-stu-id="dc044-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="dc044-145">데이터 팩터리(예: yournameSparkDFdate)의 이름을 변경하고 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="dc044-146">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="dc044-147">데이터 팩터리를 만들려는 위치의 **Azure 구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="dc044-148">기존 **리소스 그룹**을 선택하거나 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="dc044-149">**대시보드에 고정** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="dc044-150">**새 Data Factory** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="dc044-151">데이터 팩터리 인스턴스를 만들려면 구독/리소스 그룹 수준에서 [데이터 팩터리 참여자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="dc044-152">다음과 같이 Azure Portal의 **대시보드**에 만들어지는 데이터 팩터리가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="dc044-153">데이터 팩터리 만들기를 완료한 후에는 데이터 팩터리 페이지가 표시되며 여기에 데이터 팩터리의 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="dc044-154">데이터 팩터리 페이지가 표시되지 않으면 대시보드에서 데이터 팩터리의 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![데이터 팩터리 블레이드](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="dc044-156">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-156">Create linked services</span></span>
<span data-ttu-id="dc044-157">이 단계에서는 두 개의 연결된 서비스를 만듭니다. 하나는 Spark 클러스터를 데이터 팩터리에 연결하는 서비스이고, 다른 하나는 Azure 저장소를 데이터 팩터리에 연결하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="dc044-158">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="dc044-159">이 단계에서는 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="dc044-160">이 연습의 뒷부분에서 만드는 데이터 집합은 이 연결된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="dc044-161">다음 단계에서 정의하는 HDInsight 연결된 서비스는 이 연결된 서비스를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="dc044-162">데이터 팩터리의 **데이터 팩터리** 블레이드에서 **작성자 및 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="dc044-163">데이터 팩터리 편집기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="dc044-164">**새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="dc044-166">편집기에 Azure Storage 연결된 서비스를 만들기 위한 **JSON 스크립트**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="dc044-168">**계정 이름** 및 **계정 키**를 Azure 저장소 계정의 이름 및 계정 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="dc044-169">저장소 액세스 키를 가져오는 방법은 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)의 저장소 액세스 키 보기, 복사 및 생성 방법 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="dc044-170">연결된 서비스를 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="dc044-171">연결된 서비스를 성공적으로 배포한 후에 **Draft-1** 창은 사라지고 왼쪽의 트리 보기에 **AzureStorageLinkedService**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="dc044-172">HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-172">Create HDInsight linked service</span></span>
<span data-ttu-id="dc044-173">이 단계에서는 Azure HDInsight 연결된 서비스를 만들어 HDInsight Spark 클러스터를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="dc044-174">HDInsight 클러스터는 이 샘플에서 파이프라인의 Spark 활동에 지정된 Spark 프로그램을 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="dc044-175">도구 모음에서 **... 추가**, **새 계산**, **HDInsight 클러스터**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![HDInsight 연결된 서비스 만들기](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="dc044-177">다음 코드 조각을 복사하여 **Draft-1** 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="dc044-178">JSON 편집기에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="dc044-179">HDInsight Spark 클러스터에 대한 **URI**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="dc044-180">예: `https://<sparkclustername>.azurehdinsight.net/`</span><span class="sxs-lookup"><span data-stu-id="dc044-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="dc044-181">Spark 클러스터에 액세스할 수 있는 **사용자**의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="dc044-182">사용자에 대한 **암호**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="dc044-183">HDInsight Spark 클러스터와 연결되는 **Azure Storage 연결된 서비스**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="dc044-184">이 예제에서는 **AzureStorageLinkedService**입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="dc044-185">Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="dc044-186">Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="dc044-187">주문형 HDInsight 연결된 서비스는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="dc044-188">HDInsight 연결된 서비스에 대한 자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="dc044-189">연결된 서비스를 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="dc044-190">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-190">Create output dataset</span></span>
<span data-ttu-id="dc044-191">출력 데이터 집합은 일정(매시간, 매일 등)을 구동하는 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="dc044-192">따라서 활동이 실제로 출력을 생성하지 않더라도 파이프라인에서 Spark 활동에 대한 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="dc044-193">활동에 대한 입력 데이터 집합을 지정하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="dc044-194">**데이터 팩터리 편집기**의 명령 모음에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 **Azure Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="dc044-195">다음 코드 조각을 복사하여 Draft-1 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="dc044-196">JSON 조각은 **OutputDataset**이라는 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="dc044-197">또한 결과를 **adfspark**라는 Blob 컨테이너와 **pyFiles/output**이라는 폴더에 저장하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="dc044-198">앞에서 설명한 대로 이 데이터 집합은 더미 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="dc044-199">이 예제의 Spark 프로그램은 출력을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="dc044-200">**availability** 섹션에서는 출력 데이터 집합을 매일 생성하도록 지정하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="dc044-201">데이터 집합을 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="dc044-202">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="dc044-202">Create pipeline</span></span>
<span data-ttu-id="dc044-203">이 단계에서는 **HDInsightSpark** 활동을 포함하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="dc044-204">현재 출력 데이터 집합이 일정을 결정하므로 작업이 출력을 생성하지 않는 경우 출력 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="dc044-205">활동이 입력을 가져오지 않으면 입력 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="dc044-206">따라서 이 예제에서는 입력 데이터 집합을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="dc044-207">**데이터 팩터리 편집기**의 명령 모음에서 **… 추가**를 클릭한 다음 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="dc044-208">Draft-1 창의 스크립트를 다음 스크립트로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-208">Replace the script in the Draft-1 window with the following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="dc044-209">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-209">Note the following points:</span></span>
    - <span data-ttu-id="dc044-210">**type** 속성은 **HDInsightSpark**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="dc044-211">**rootPath**는 **adfspark\\pyFiles**로 설정되며, 여기서 adfspark는 Azure Blob 컨테이너이고, pyFiles는 해당 컨테이너의 파일 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="dc044-212">이 예에서 Azure Blob Storage는 Spark 클러스터와 연결되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="dc044-213">파일을 다른 Azure Storage에 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="dc044-214">이렇게 하는 경우 해당 저장소 계정을 데이터 팩터리에 연결하는 Azure Storage 연결된 서비스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="dc044-215">그런 다음 연결된 서비스의 이름을 **sparkJobLinkedService** 속성의 값으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="dc044-216">이 속성과 Spark 작업에서 지원하는 기타 속성에 대한 자세한 내용은 [Spark 작업 속성](#spark-activity-properties)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="dc044-217">**entryFilePath**는 python 파일인 **test.py**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="dc044-218">**getDebugInfo** 속성은 **Always**로 설정되며, 이는 로그 파일이 항상 생성(성공 또는 실패)된다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="dc044-219">문제를 해결하는 경우가 아니라면 프로덕션 환경에서 이 속성을 `Always`로 설정하지 않는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="dc044-220">**outputs** 섹션에는 하나의 출력 데이터 집합만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="dc044-221">Spark 프로그램이 출력을 생성하지 않더라도 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="dc044-222">출력 데이터 집합은 파이프라인의 일정(매시간, 매일 등)을 구동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="dc044-223">Spark 활동에서 지원하는 속성에 대한 자세한 내용은 [Spark 활동 속성](#spark-activity-properties) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="dc044-224">파이프라인을 배포하려면 명령 모음에서 **배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="dc044-225">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="dc044-225">Monitor pipeline</span></span>
1. <span data-ttu-id="dc044-226">**X**를 클릭하여 Data Factory 편집기 블레이드를 닫고 Data Factory 홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="dc044-227">다른 탭에서 모니터링 응용 프로그램을 시작하려면 **모니터링 및 관리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![모니터링 및 관리 타일](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="dc044-229">위쪽의 **시작 시간** 필터를 **2/1/2017**로 변경하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="dc044-230">파이프라인의 시작 시간(2017년 2월 1일)과 종료 시간(2017년 2월 2일) 사이에는 하루가 있기 때문에 하나의 활동 창만 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="dc044-231">데이터 조각이 **ready**(준비) 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-231">Confirm that the data slice is in **ready** state.</span></span>

    ![파이프라인 모니터링](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="dc044-233">**활동 창**을 선택하여 활동 실행에 대한 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="dc044-234">오류가 있으면 오른쪽 창에 오류에 대한 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="dc044-235">결과 확인</span><span class="sxs-lookup"><span data-stu-id="dc044-235">Verify the results</span></span>

1. <span data-ttu-id="dc044-236">https://CLUSTERNAME.azurehdinsight.net/jupyter로 이동하여 HDInsight Spark 클러스터에 대한 **Jupyter 노트북**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="dc044-237">또한 HDInsight Spark 클러스터에 대한 클러스터 대시보드를 실행한 다음 **Jupyter 노트북**을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="dc044-238">**새로 만들기** -> **PySpark**를 클릭하여 새 노트북을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![새 Jupyter 노트북](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="dc044-240">텍스트를 복사하여 붙여넣고 두 번째 문의 끝에서 **Shift+Enter**를 눌러 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="dc044-241">hvac 테이블의 데이터가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Jupyter 쿼리 결과](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="dc044-243">자세한 지침은 [Spark SQL 쿼리 실행](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc044-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="dc044-244">문제 해결</span><span class="sxs-lookup"><span data-stu-id="dc044-244">Troubleshooting</span></span>
<span data-ttu-id="dc044-245">**getDebugInfo**를 **Always**로 설정한 후에는 Azure Blob 컨테이너의 **pyFiles** 폴더에 **log** 하위 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="dc044-246">로그 폴더의 로그 파일에서 추가 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="dc044-247">이 로그 파일은 오류가 발생할 때 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="dc044-248">프로덕션 환경에서는 이 오류를 **실패**로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="dc044-249">추가 문제 해결을 위해 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="dc044-250">`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI 응용 프로그램](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="dc044-252">실행 시도 중 하나에 대해 **로그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-252">Click **Logs** for one of the run attempts.</span></span>

    ![응용 프로그램 페이지](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="dc044-254">로그 페이지에 추가 오류 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-254">You should see additional error information in the log page.</span></span>

    ![로그 오류](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="dc044-256">다음 섹션에서는 데이터 팩터리에 Apache Spark 클러스터 및 Spark 작업을 사용하는 데이터 팩터리 엔터티에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="dc044-257">Spark 활동 속성</span><span class="sxs-lookup"><span data-stu-id="dc044-257">Spark activity properties</span></span>
<span data-ttu-id="dc044-258">다음은 Spark 작업을 사용하는 파이프라인의 샘플 JSON 정의입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="dc044-259">다음 표에서는 JSON 정의에 사용하는 JSON 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="dc044-260">속성</span><span class="sxs-lookup"><span data-stu-id="dc044-260">Property</span></span> | <span data-ttu-id="dc044-261">설명</span><span class="sxs-lookup"><span data-stu-id="dc044-261">Description</span></span> | <span data-ttu-id="dc044-262">필수</span><span class="sxs-lookup"><span data-stu-id="dc044-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="dc044-263">name</span><span class="sxs-lookup"><span data-stu-id="dc044-263">name</span></span> | <span data-ttu-id="dc044-264">파이프라인의 작업 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="dc044-265">예</span><span class="sxs-lookup"><span data-stu-id="dc044-265">Yes</span></span> |
| <span data-ttu-id="dc044-266">설명</span><span class="sxs-lookup"><span data-stu-id="dc044-266">description</span></span> | <span data-ttu-id="dc044-267">작업이 어떤 일을 수행하는지 설명하는 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-267">Text describing what the activity does.</span></span> | <span data-ttu-id="dc044-268">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-268">No</span></span> |
| <span data-ttu-id="dc044-269">type</span><span class="sxs-lookup"><span data-stu-id="dc044-269">type</span></span> | <span data-ttu-id="dc044-270">이 속성은 HDInsightSpark로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="dc044-271">예</span><span class="sxs-lookup"><span data-stu-id="dc044-271">Yes</span></span> |
| <span data-ttu-id="dc044-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="dc044-272">linkedServiceName</span></span> | <span data-ttu-id="dc044-273">Spark 프로그램이 실행되는 HDInsight 연결된 서비스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="dc044-274">예</span><span class="sxs-lookup"><span data-stu-id="dc044-274">Yes</span></span> |
| <span data-ttu-id="dc044-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="dc044-275">rootPath</span></span> | <span data-ttu-id="dc044-276">Spark 파일이 포함된 Azure Blob 컨테이너 및 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="dc044-277">파일 이름은 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="dc044-278">예</span><span class="sxs-lookup"><span data-stu-id="dc044-278">Yes</span></span> |
| <span data-ttu-id="dc044-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="dc044-279">entryFilePath</span></span> | <span data-ttu-id="dc044-280">Spark 코드/패키지의 루트 폴더에 대한 상대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="dc044-281">예</span><span class="sxs-lookup"><span data-stu-id="dc044-281">Yes</span></span> |
| <span data-ttu-id="dc044-282">className</span><span class="sxs-lookup"><span data-stu-id="dc044-282">className</span></span> | <span data-ttu-id="dc044-283">응용 프로그램의 Java/Spark main 클래스</span><span class="sxs-lookup"><span data-stu-id="dc044-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="dc044-284">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-284">No</span></span> |
| <span data-ttu-id="dc044-285">arguments</span><span class="sxs-lookup"><span data-stu-id="dc044-285">arguments</span></span> | <span data-ttu-id="dc044-286">Spark 프로그램에 대한 명령줄 인수 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="dc044-287">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-287">No</span></span> |
| <span data-ttu-id="dc044-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="dc044-288">proxyUser</span></span> | <span data-ttu-id="dc044-289">Spark 프로그램 실행을 가장하는 사용자 계정</span><span class="sxs-lookup"><span data-stu-id="dc044-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="dc044-290">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-290">No</span></span> |
| <span data-ttu-id="dc044-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="dc044-291">sparkConfig</span></span> | <span data-ttu-id="dc044-292">[Spark 구성 - 응용 프로그램 속성](https://spark.apache.org/docs/latest/configuration.html#available-properties) 항목에 나열된 Spark 구성 속성의 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="dc044-293">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-293">No</span></span> |
| <span data-ttu-id="dc044-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="dc044-294">getDebugInfo</span></span> | <span data-ttu-id="dc044-295">sparkJobLinkedService에 지정되었거나 HDInsight 클러스터에 사용된 Azure Storage에 Spark 로그 파일을 언제 복사할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="dc044-296">허용되는 값: None, Always 또는 Failure.</span><span class="sxs-lookup"><span data-stu-id="dc044-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="dc044-297">기본값: None.</span><span class="sxs-lookup"><span data-stu-id="dc044-297">Default value: None.</span></span> | <span data-ttu-id="dc044-298">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-298">No</span></span> |
| <span data-ttu-id="dc044-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="dc044-299">sparkJobLinkedService</span></span> | <span data-ttu-id="dc044-300">Spark 작업 파일, 종속성 및 로그를 보유하는 Azure Storage 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="dc044-301">이 속성에 대한 값을 지정하지 않으면 HDInsight 클러스터와 연결된 저장소가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="dc044-302">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="dc044-303">폴더 구조</span><span class="sxs-lookup"><span data-stu-id="dc044-303">Folder structure</span></span>
<span data-ttu-id="dc044-304">Spark 작업은 Pig 및 Hive 작업에서 수행하는 것처럼 인라인 스크립트를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="dc044-305">Spark 작업은 Pig/Hive 작업보다 확장성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="dc044-306">Spark 작업의 경우 jar 패키지(java CLASSPATH에 배치), python 파일(PYTHONPATH에 배치) 및 기타 파일과 같은 여러 종속성을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="dc044-307">HDInsight 연결된 서비스에서 참조하는 Azure Blob Storage에 다음 폴더 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="dc044-308">그런 다음 종속 파일을 **entryFilePath**로 표시되는 루트 폴더의 해당 하위 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="dc044-309">예를 들어 python 파일을 루트 폴더의 pyFiles 하위 폴더에, jar 파일을 jars 하위 폴더에 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="dc044-310">런타임 시, Data Factory 서비스는 Azure Blob Storage에서 다음 폴더 구조를 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="dc044-311">Path</span><span class="sxs-lookup"><span data-stu-id="dc044-311">Path</span></span> | <span data-ttu-id="dc044-312">설명</span><span class="sxs-lookup"><span data-stu-id="dc044-312">Description</span></span> | <span data-ttu-id="dc044-313">필수</span><span class="sxs-lookup"><span data-stu-id="dc044-313">Required</span></span> | <span data-ttu-id="dc044-314">형식</span><span class="sxs-lookup"><span data-stu-id="dc044-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="dc044-315"> 등 4가지 유형의 클러스터가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-315">.</span></span> | <span data-ttu-id="dc044-316">저장소 연결된 서비스에서 Spark 작업의 루트 경로</span><span class="sxs-lookup"><span data-stu-id="dc044-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="dc044-317">예</span><span class="sxs-lookup"><span data-stu-id="dc044-317">Yes</span></span> | <span data-ttu-id="dc044-318">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-318">Folder</span></span> |
| <span data-ttu-id="dc044-319">&lt;사용자 정의 &gt;</span><span class="sxs-lookup"><span data-stu-id="dc044-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="dc044-320">Spark 작업의 엔트리 파일을 가리키는 경로</span><span class="sxs-lookup"><span data-stu-id="dc044-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="dc044-321">예</span><span class="sxs-lookup"><span data-stu-id="dc044-321">Yes</span></span> | <span data-ttu-id="dc044-322">파일</span><span class="sxs-lookup"><span data-stu-id="dc044-322">File</span></span> |
| <span data-ttu-id="dc044-323">./jars</span><span class="sxs-lookup"><span data-stu-id="dc044-323">./jars</span></span> | <span data-ttu-id="dc044-324">이 폴더 아래 모든 파일이 업로드되고 클러스터의 java classpath에 배치됨</span><span class="sxs-lookup"><span data-stu-id="dc044-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="dc044-325">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-325">No</span></span> | <span data-ttu-id="dc044-326">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-326">Folder</span></span> |
| <span data-ttu-id="dc044-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="dc044-327">./pyFiles</span></span> | <span data-ttu-id="dc044-328">이 폴더 아래 모든 파일이 업로드되고 클러스터의 PYTHONPATH에 배치됨</span><span class="sxs-lookup"><span data-stu-id="dc044-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="dc044-329">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-329">No</span></span> | <span data-ttu-id="dc044-330">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-330">Folder</span></span> |
| <span data-ttu-id="dc044-331">./files</span><span class="sxs-lookup"><span data-stu-id="dc044-331">./files</span></span> | <span data-ttu-id="dc044-332">이 폴더 아래 모든 파일이 업로드되고 실행기 작업 디렉터리에 배치됨</span><span class="sxs-lookup"><span data-stu-id="dc044-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="dc044-333">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-333">No</span></span> | <span data-ttu-id="dc044-334">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-334">Folder</span></span> |
| <span data-ttu-id="dc044-335">./archives</span><span class="sxs-lookup"><span data-stu-id="dc044-335">./archives</span></span> | <span data-ttu-id="dc044-336">이 폴더 아래 모든 파일이 압축 해제됨</span><span class="sxs-lookup"><span data-stu-id="dc044-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="dc044-337">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-337">No</span></span> | <span data-ttu-id="dc044-338">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-338">Folder</span></span> |
| <span data-ttu-id="dc044-339">./logs</span><span class="sxs-lookup"><span data-stu-id="dc044-339">./logs</span></span> | <span data-ttu-id="dc044-340">Spark 클러스터의 로그가 저장되는 폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="dc044-341">아니요</span><span class="sxs-lookup"><span data-stu-id="dc044-341">No</span></span> | <span data-ttu-id="dc044-342">폴더</span><span class="sxs-lookup"><span data-stu-id="dc044-342">Folder</span></span> |

<span data-ttu-id="dc044-343">HDInsight 연결된 서비스에서 참조하는 Azure Blob Storage에 두 개의 Spark 작업 파일이 포함된 저장소에 대한 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc044-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
