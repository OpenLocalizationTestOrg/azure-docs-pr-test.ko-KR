---
title: "Azure Data Factory에서 Spark aaaInvoke 프로그램 | Microsoft Docs"
description: "Tooinvoke Spark 프로그램을 사용 하 여 Azure 데이터 팩터리에서 MapReduce Activity hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="31dac-103">Azure Data Factory 파이프라인에서 Spark 프로그램 호출</span><span class="sxs-lookup"><span data-stu-id="31dac-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="31dac-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="31dac-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="31dac-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="31dac-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="31dac-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="31dac-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="31dac-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="31dac-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="31dac-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="31dac-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="31dac-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="31dac-114">소개</span><span class="sxs-lookup"><span data-stu-id="31dac-114">Introduction</span></span>
<span data-ttu-id="31dac-115">Spark 활동을 사용 하면 hello 중 하나인 [데이터 변환 작업](data-factory-data-transformation-activities.md) Azure Data Factory에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="31dac-116">이 작업이 실행 지정 hello Azure HDInsight의 Apache Spark 클러스터에서 Spark 프로그램.</span><span class="sxs-lookup"><span data-stu-id="31dac-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="31dac-117">Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="31dac-118">Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="31dac-119">주문형 HDInsight 연결된 서비스는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="31dac-120">연습: Spark 활동이 포함된 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="31dac-121">Hello 일반적인 단계 toocreate Spark 활동으로 데이터 팩터리 파이프라인은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="31dac-122">데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-122">Create a data factory.</span></span>
2. <span data-ttu-id="31dac-123">Azure 저장소 연결 서비스 toolink HDInsight Spark 클러스터 toohello 데이터 팩터리와 연결 된 Azure 저장소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="31dac-124">Azure HDInsight toohello data factory에는 Azure HDInsight 연결 된 서비스 toolink Apache Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="31dac-125">Toohello Azure 저장소 연결 된 서비스를 참조 하는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="31dac-126">현재 생성 중인 출력이 없더라도 작업의 출력 데이터 집합을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="31dac-127"># 2에서 만든 toohello HDInsight 연결 된 서비스를 참조 하는 스파크 작업으로 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="31dac-128">hello 활동 출력 데이터 집합으로 hello 이전 단계에서 만든 hello 데이터 집합으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="31dac-129">hello 출력 데이터 집합은 어떤 드라이브 hello 일정 (시간별, 일별, 등).</span><span class="sxs-lookup"><span data-stu-id="31dac-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="31dac-130">따라서 실제로 hello 활동 출력을 만들지 않고 하는 경우에 hello 출력 데이터 집합을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="31dac-131">필수 조건</span><span class="sxs-lookup"><span data-stu-id="31dac-131">Prerequisites</span></span>
1. <span data-ttu-id="31dac-132">만들기는 **범용 Azure 저장소 계정** 지침 hello 연습에 따라: [저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="31dac-133">만들기는 **Azure HDInsight의 Apache Spark 클러스터** hello 자습서의 지침에 따라: [Azure HDInsight의 Apache Spark 만드는 클러스터](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="31dac-134">이 클러스터와 1 단계에서 만든 hello Azure 저장소 계정을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="31dac-135">다운로드 하 여 hello python 스크립트 파일을 검토 **test.py** 에 있는: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="31dac-136">업로드 **test.py** toohello **pyFiles** 폴더 hello에 **adfspark** Azure Blob 저장소의 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="31dac-137">존재 하지 않는 경우 hello 컨테이너 및 hello 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="31dac-138">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-138">Create data factory</span></span>
<span data-ttu-id="31dac-139">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="31dac-140">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="31dac-141">클릭 **새로** hello 왼쪽된 메뉴에서 클릭 **데이터 + 분석**, 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="31dac-142">Hello에 **새 데이터 팩터리** 블레이드에서 입력 **SparkDF** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="31dac-143">hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="31dac-144">Hello 오류가 나타나는 경우: **"SparkDF" 데이터 팩터리 이름을 사용할 수 없으면**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="31dac-145">변경 hello hello 데이터 팩터리의 이름입니다 (예: yournameSparkDFdate, 및 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="31dac-146">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dac-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="31dac-147">선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="31dac-148">기존 **리소스 그룹**을 선택하거나 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="31dac-149">선택 **Pin toodashboard** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="31dac-150">클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="31dac-151">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="31dac-152">Hello에 생성 되 고 hello 데이터 팩터리 참조 **대시보드** hello 다음과 같이 Azure 포털의.</span><span class="sxs-lookup"><span data-stu-id="31dac-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="31dac-153">보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="31dac-154">Hello 데이터 팩터리 페이지를 표시 되지 않으면 hello 대시보드에서 데이터 팩터리에 대 한 hello 타일을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![데이터 팩터리 블레이드](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="31dac-156">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-156">Create linked services</span></span>
<span data-ttu-id="31dac-157">이 단계에서는 두 개의 연결 된 서비스를 하나의 toolink Spark 클러스터 tooyour 데이터 팩터리를 만들고 다른 toolink tooyour 데이터 팩터리를 Azure 저장소 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="31dac-158">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="31dac-159">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="31dac-160">이 연습 뒷부분에 나오는 단계에서 만든 데이터 집합 toothis 연결 된 서비스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="31dac-161">hello hello 다음 단계에서 정의 하는 HDInsight 연결 된 서비스는 너무 toothis 연결 된 서비스를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="31dac-162">클릭 **작성자 및 배포** hello에 **Data Factory** 블레이드 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="31dac-163">데이터 팩터리 편집기 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="31dac-164">**새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="31dac-166">Hello 표시 되어야 **JSON 스크립트** Azure 저장소를 만들기 위한 hello 편집기에서 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="31dac-168">대체 **계정 이름** 및 **계정 키** hello 사용자의 Azure 저장소 계정 이름과 액세스 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="31dac-169">toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="31dac-170">toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="31dac-171">Hello 연결 된 서비스를 배포한 후 성공적으로 hello **Draft 1** 창 사라져야 나타나고 **AzureStorageLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="31dac-172">HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-172">Create HDInsight linked service</span></span>
<span data-ttu-id="31dac-173">이 단계에서는 Azure HDInsight 연결 된 서비스 toolink HDInsight Spark 클러스터 toohello 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="31dac-174">hello HDInsight 클러스터는이 샘플의 hello 파이프라인의 hello Spark 활동에 지정 된 사용 되는 toorun hello Spark 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="31dac-175">도구 모음에서 **... 더 많은** hello 도구 모음에서 **새 계산**, 클릭 하 고 **HDInsight 클러스터**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![HDInsight 연결된 서비스 만들기](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="31dac-177">복사 및 붙여넣기 다음 코드 조각 toohello hello **Draft 1** 창.</span><span class="sxs-lookup"><span data-stu-id="31dac-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="31dac-178">Hello JSON 편집기에서 수행 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="31dac-179">Hello 지정 **URI** hello HDInsight Spark 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="31dac-180">예: `https://<sparkclustername>.azurehdinsight.net/`</span><span class="sxs-lookup"><span data-stu-id="31dac-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="31dac-181">Hello의 hello 이름을 지정 **사용자** 액세스 toohello Spark 클러스터를가지고 있는 사람입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="31dac-182">Hello 지정 **암호** 사용자에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="31dac-183">Hello 지정 **Azure 저장소 연결 된 서비스** hello HDInsight Spark 클러스터와 연결 된 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="31dac-184">이 예제에서는 **AzureStorageLinkedService**입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="31dac-185">Spark 활동은 기본 저장소로 Azure Data Lake Store를 사용하는 HDInsight Spark 클러스터를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="31dac-186">Spark 활동은 사용자 고유의 기존 HDInsight Spark 클러스터만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="31dac-187">주문형 HDInsight 연결된 서비스는 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="31dac-188">참조 [HDInsight 연결 된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) hello에 대 한 자세한 내용은 HDInsight 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="31dac-189">toodeploy hello 연결 된 서비스를 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="31dac-190">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-190">Create output dataset</span></span>
<span data-ttu-id="31dac-191">hello 출력 데이터 집합은 어떤 드라이브 hello 일정 (시간별, 일별, 등).</span><span class="sxs-lookup"><span data-stu-id="31dac-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="31dac-192">따라서 hello 활동 실제로 출력을 생성 하지 않는 경우에 hello 파이프라인의 hello spark 활동에 대 한 출력 데이터 집합을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="31dac-193">Hello 활동에 대 한 입력된 데이터 집합을 지정 하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="31dac-194">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="31dac-195">복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="31dac-196">라는 데이터 집합을 정의 하는 hello JSON 코드 조각은 **OutputDataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="31dac-197">Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfspark** 및 라고 하는 hello 폴더 **pyFiles/출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="31dac-198">앞에서 설명한 대로 이 데이터 집합은 더미 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="31dac-199">이 예제의 hello Spark 프로그램 출력을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="31dac-200">hello **가용성** 섹션 해당 hello 출력 데이터 집합을 매일 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="31dac-201">toodeploy hello 데이터 집합, 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="31dac-202">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="31dac-202">Create pipeline</span></span>
<span data-ttu-id="31dac-203">이 단계에서는 **HDInsightSpark** 활동을 포함하는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="31dac-204">현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="31dac-205">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="31dac-206">따라서 이 예제에서는 입력 데이터 집합을 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="31dac-207">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** 명령 모음 hello 되 고 클릭 **새 파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="31dac-208">Hello 스크립트를 hello Draft 1 창에 다음 스크립트는 hello로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

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
    <span data-ttu-id="31dac-209">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="31dac-209">Note hello following points:</span></span>
    - <span data-ttu-id="31dac-210">hello **형식** 너무 속성이**HDInsightSpark**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="31dac-211">hello **rootPath** 너무 설정**adfspark\\pyFiles** adfspark 란 pyFiles 고 hello Azure Blob 컨테이너는 세밀 하 게 폴더 해당 컨테이너에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="31dac-212">이 예제에서는 hello Azure Blob 저장소는 hello 즉 hello Spark 클러스터와 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="31dac-213">Hello 파일 tooa 업로드할 수 있습니다 다른 Azure 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="31dac-214">이렇게 하면 Azure 저장소 연결 서비스 toolink 해당 저장소 계정 toohello 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="31dac-215">그런 다음 hello 연결 된 서비스의 hello 이름을 hello에 대 한 값으로 지정 **sparkJobLinkedService** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="31dac-216">참조 [Spark 활동 속성](#spark-activity-properties) hello Spark 활동에서 지 원하는 다른 속성 및이 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="31dac-217">hello **entryFilePath** toohello 설정 **test.py**, hello python 파일인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="31dac-218">hello **getDebugInfo** 너무 속성이**항상**, (성공 또는 실패) 생성 된 hello 로그 파일은 항상 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="31dac-219">설정 하지 않으면이 속성 너무 권장`Always` 프로덕션 환경에서 문제를 해결 하는 경우가 아니면 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="31dac-220">hello **출력** 섹션에는 하나의 출력 데이터 집합에 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="31dac-221">Hello spark 프로그램 출력을 생성 하지 않는 경우에 출력 데이터 집합을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="31dac-222">hello 출력 데이터 집합 드라이브 hello에 대 한 일정 hello 파이프라인 (시간별, 일별, 등).</span><span class="sxs-lookup"><span data-stu-id="31dac-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="31dac-223">Spark 활동에서 지 원하는 hello 속성에 대 한 세부 정보를 참조 하십시오. [활동 속성 멤버](#spark-activity-properties) 섹션.</span><span class="sxs-lookup"><span data-stu-id="31dac-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="31dac-224">toodeploy hello 파이프라인 클릭 **배포** hello 명령 모음에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="31dac-225">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="31dac-225">Monitor pipeline</span></span>
1. <span data-ttu-id="31dac-226">클릭 **X** tooclose 데이터 팩터리 편집기 블레이드와 toonavigate 다시 toohello Data Factory 홈 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="31dac-227">클릭 **모니터 및 관리** toolaunch hello 다른 탭에서 응용 프로그램을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![모니터링 및 관리 타일](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="31dac-229">변경 hello **시작 시간** hello 위쪽에 너무 필터링**2/1/2017**를 클릭 하 고 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="31dac-230">하루가 hello 사이 (2017-02-01)를 시작 및 종료 시간 (2017-02-02) hello 파이프라인의 그대로 활동 창이 하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="31dac-231">해당 hello 데이터 조각에 속하는지 확인 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![모니터 hello 파이프라인](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="31dac-233">선택 hello **활동 창** hello 활동 실행에 대 한 toosee 세부 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="31dac-234">오류가 발생 하는 hello 오른쪽 창에서 항목에 대 한 세부 정보 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="31dac-235">Hello 결과 확인</span><span class="sxs-lookup"><span data-stu-id="31dac-235">Verify hello results</span></span>

1. <span data-ttu-id="31dac-236">https://CLUSTERNAME.azurehdinsight.net/jupyter로 이동하여 HDInsight Spark 클러스터에 대한 **Jupyter 노트북**을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="31dac-237">또한 HDInsight Spark 클러스터에 대한 클러스터 대시보드를 실행한 다음 **Jupyter 노트북**을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="31dac-238">클릭 **새로** -> **PySpark** toostart 새 노트북 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![새 Jupyter 노트북](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="31dac-240">실행 hello 다음 명령을 복사/붙여넣기 hello 텍스트 고 키를 눌러 **SHIFT + ENTER** hello hello 두 번째 문이 끝날 때.</span><span class="sxs-lookup"><span data-stu-id="31dac-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="31dac-241">Hello 테이블의에서 데이터를 hello hvac 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Jupyter 쿼리 결과](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="31dac-243">자세한 지침은 [Spark SQL 쿼리 실행](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="31dac-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="31dac-244">문제 해결</span><span class="sxs-lookup"><span data-stu-id="31dac-244">Troubleshooting</span></span>
<span data-ttu-id="31dac-245">설정한 이후로 **getDebugInfo** 너무**항상**, 표시는 **로그** hello에 하위 폴더로 **pyFiles** Azure Blob 컨테이너에 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="31dac-246">hello 로그 폴더에 hello 로그 파일 추가 세부 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="31dac-247">이 로그 파일은 오류가 발생할 때 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="31dac-248">프로덕션 환경에서 tooset 경우가 것 너무**오류**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="31dac-249">추가 문제 해결에 대 한 않습니다 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="31dac-250">너무 이동`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN UI 응용 프로그램](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="31dac-252">클릭 **로그** hello 중 하나에 대 한 시도 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-252">Click **Logs** for one of hello run attempts.</span></span>

    ![응용 프로그램 페이지](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="31dac-254">Hello 로그 페이지에 추가 오류 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-254">You should see additional error information in hello log page.</span></span>

    ![로그 오류](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="31dac-256">다음 섹션 hello Data Factory 엔터티에 toouse Apache Spark 클러스터 및 데이터 팩터리에서 Spark 활동에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="31dac-257">Spark 활동 속성</span><span class="sxs-lookup"><span data-stu-id="31dac-257">Spark activity properties</span></span>
<span data-ttu-id="31dac-258">Spark 활동을 포함 하는 파이프라인의 hello 샘플 JSON 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="31dac-259">hello 다음 표에서 설명 hello JSON 정의에서 사용 되는 hello JSON 속성:</span><span class="sxs-lookup"><span data-stu-id="31dac-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="31dac-260">속성</span><span class="sxs-lookup"><span data-stu-id="31dac-260">Property</span></span> | <span data-ttu-id="31dac-261">설명</span><span class="sxs-lookup"><span data-stu-id="31dac-261">Description</span></span> | <span data-ttu-id="31dac-262">필수</span><span class="sxs-lookup"><span data-stu-id="31dac-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="31dac-263">name</span><span class="sxs-lookup"><span data-stu-id="31dac-263">name</span></span> | <span data-ttu-id="31dac-264">Hello 파이프라인의 hello 활동의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="31dac-265">예</span><span class="sxs-lookup"><span data-stu-id="31dac-265">Yes</span></span> |
| <span data-ttu-id="31dac-266">설명</span><span class="sxs-lookup"><span data-stu-id="31dac-266">description</span></span> | <span data-ttu-id="31dac-267">어떤 hello 활동을 설명 하는 텍스트는 다음 작업을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="31dac-268">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-268">No</span></span> |
| <span data-ttu-id="31dac-269">type</span><span class="sxs-lookup"><span data-stu-id="31dac-269">type</span></span> | <span data-ttu-id="31dac-270">이 속성은 tooHDInsightSpark 설정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="31dac-271">예</span><span class="sxs-lookup"><span data-stu-id="31dac-271">Yes</span></span> |
| <span data-ttu-id="31dac-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="31dac-272">linkedServiceName</span></span> | <span data-ttu-id="31dac-273">서비스는 hello Spark에서 프로그램 실행 연결 된 하는 hello HDInsight의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="31dac-274">예</span><span class="sxs-lookup"><span data-stu-id="31dac-274">Yes</span></span> |
| <span data-ttu-id="31dac-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="31dac-275">rootPath</span></span> | <span data-ttu-id="31dac-276">hello Azure Blob 컨테이너 및 hello Spark 파일이 있는 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="31dac-277">hello 파일 이름은 대/소문자 구분입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="31dac-278">예</span><span class="sxs-lookup"><span data-stu-id="31dac-278">Yes</span></span> |
| <span data-ttu-id="31dac-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="31dac-279">entryFilePath</span></span> | <span data-ttu-id="31dac-280">Hello Spark 코드/패키지의 상대 경로 toohello 루트 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="31dac-281">예</span><span class="sxs-lookup"><span data-stu-id="31dac-281">Yes</span></span> |
| <span data-ttu-id="31dac-282">className</span><span class="sxs-lookup"><span data-stu-id="31dac-282">className</span></span> | <span data-ttu-id="31dac-283">응용 프로그램의 Java/Spark main 클래스</span><span class="sxs-lookup"><span data-stu-id="31dac-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="31dac-284">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-284">No</span></span> |
| <span data-ttu-id="31dac-285">arguments</span><span class="sxs-lookup"><span data-stu-id="31dac-285">arguments</span></span> | <span data-ttu-id="31dac-286">명령줄 인수 toohello Spark 프로그램의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="31dac-287">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-287">No</span></span> |
| <span data-ttu-id="31dac-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="31dac-288">proxyUser</span></span> | <span data-ttu-id="31dac-289">hello 사용자 계정 tooimpersonate tooexecute hello Spark 프로그램</span><span class="sxs-lookup"><span data-stu-id="31dac-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="31dac-290">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-290">No</span></span> |
| <span data-ttu-id="31dac-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="31dac-291">sparkConfig</span></span> | <span data-ttu-id="31dac-292">Hello 항목에 나열 된 Spark 구성 속성에 대 한 값을 지정: [Spark 구성-응용 프로그램 속성](https://spark.apache.org/docs/latest/configuration.html#available-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="31dac-293">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-293">No</span></span> |
| <span data-ttu-id="31dac-294">getDebugInfo</span><span class="sxs-lookup"><span data-stu-id="31dac-294">getDebugInfo</span></span> | <span data-ttu-id="31dac-295">Hello Spark 로그 파일에서 복사한 toohello HDInsight 클러스터에서 사용 하는 Azure 저장소를가 하는 경우를 지정 합니다 (또는) sparkJobLinkedService 하 여 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="31dac-296">허용되는 값: None, Always 또는 Failure.</span><span class="sxs-lookup"><span data-stu-id="31dac-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="31dac-297">기본값: None.</span><span class="sxs-lookup"><span data-stu-id="31dac-297">Default value: None.</span></span> | <span data-ttu-id="31dac-298">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-298">No</span></span> |
| <span data-ttu-id="31dac-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="31dac-299">sparkJobLinkedService</span></span> | <span data-ttu-id="31dac-300">hello hello Spark 작업 파일, 종속성 및 로그를 보유 하는 Azure 저장소 연결 된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="31dac-301">이 속성에 대 한 값을 지정 하지 않으면 HDInsight 클러스터와 연결 된 hello 저장소 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="31dac-302">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="31dac-303">폴더 구조</span><span class="sxs-lookup"><span data-stu-id="31dac-303">Folder structure</span></span>
<span data-ttu-id="31dac-304">Spark 활동 hello 인라인 스크립트 된 Pig로 지원 하지 않으며 Hive 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="31dac-305">Spark 작업은 Pig/Hive 작업보다 확장성이 뛰어납니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="31dac-306">Spark 작업에 대 한 제공할 수 있습니다 여러 종속성와 같은 패키지 (hello java CLASSPATH에에서 배치 됨), python 파일 (PYTHONPATH hello에 배치 됨) 및 기타 파일 jar.</span><span class="sxs-lookup"><span data-stu-id="31dac-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="31dac-307">Hello 다음 hello hello HDInsight 연결 된 서비스에서 참조 하는 Azure Blob 저장소의에서 폴더 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="31dac-308">그런 다음 나타내는 hello 루트 폴더에서 종속 파일 toohello 적절 한 하위 폴더를 업로드 **entryFilePath**합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="31dac-309">예를 들어 python 파일 toohello pyFiles 하위 폴더 및 jar 파일 toohello jar의 하위 폴더 hello 루트 폴더를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="31dac-310">런타임 시 데이터 팩터리 서비스는 hello Azure Blob 저장소의에서 폴더 구조를 다음 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="31dac-311">Path</span><span class="sxs-lookup"><span data-stu-id="31dac-311">Path</span></span> | <span data-ttu-id="31dac-312">설명</span><span class="sxs-lookup"><span data-stu-id="31dac-312">Description</span></span> | <span data-ttu-id="31dac-313">필수</span><span class="sxs-lookup"><span data-stu-id="31dac-313">Required</span></span> | <span data-ttu-id="31dac-314">형식</span><span class="sxs-lookup"><span data-stu-id="31dac-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="31dac-315">에서도 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-315">.</span></span> | <span data-ttu-id="31dac-316">hello 저장소 연결 된 서비스에서 hello Spark 작업의 hello 루트 경로</span><span class="sxs-lookup"><span data-stu-id="31dac-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="31dac-317">예</span><span class="sxs-lookup"><span data-stu-id="31dac-317">Yes</span></span> | <span data-ttu-id="31dac-318">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-318">Folder</span></span> |
| <span data-ttu-id="31dac-319">&lt;사용자 정의 &gt;</span><span class="sxs-lookup"><span data-stu-id="31dac-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="31dac-320">hello Spark 작업의 toohello 항목 파일을 가리키는 hello 경로</span><span class="sxs-lookup"><span data-stu-id="31dac-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="31dac-321">예</span><span class="sxs-lookup"><span data-stu-id="31dac-321">Yes</span></span> | <span data-ttu-id="31dac-322">파일</span><span class="sxs-lookup"><span data-stu-id="31dac-322">File</span></span> |
| <span data-ttu-id="31dac-323">./jars</span><span class="sxs-lookup"><span data-stu-id="31dac-323">./jars</span></span> | <span data-ttu-id="31dac-324">이 폴더 아래에 있는 모든 파일 업로드 되어 hello 클러스터의 hello java 클래스 경로에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="31dac-325">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-325">No</span></span> | <span data-ttu-id="31dac-326">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-326">Folder</span></span> |
| <span data-ttu-id="31dac-327">./pyFiles</span><span class="sxs-lookup"><span data-stu-id="31dac-327">./pyFiles</span></span> | <span data-ttu-id="31dac-328">이 폴더 아래에 있는 모든 파일 업로드 되어 hello 클러스터의 PYTHONPATH hello에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="31dac-329">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-329">No</span></span> | <span data-ttu-id="31dac-330">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-330">Folder</span></span> |
| <span data-ttu-id="31dac-331">./files</span><span class="sxs-lookup"><span data-stu-id="31dac-331">./files</span></span> | <span data-ttu-id="31dac-332">이 폴더 아래 모든 파일이 업로드되고 실행기 작업 디렉터리에 배치됨</span><span class="sxs-lookup"><span data-stu-id="31dac-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="31dac-333">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-333">No</span></span> | <span data-ttu-id="31dac-334">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-334">Folder</span></span> |
| <span data-ttu-id="31dac-335">./archives</span><span class="sxs-lookup"><span data-stu-id="31dac-335">./archives</span></span> | <span data-ttu-id="31dac-336">이 폴더 아래 모든 파일이 압축 해제됨</span><span class="sxs-lookup"><span data-stu-id="31dac-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="31dac-337">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-337">No</span></span> | <span data-ttu-id="31dac-338">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-338">Folder</span></span> |
| <span data-ttu-id="31dac-339">./logs</span><span class="sxs-lookup"><span data-stu-id="31dac-339">./logs</span></span> | <span data-ttu-id="31dac-340">hello hello Spark 클러스터에서 로그를 저장 된 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="31dac-341">아니요</span><span class="sxs-lookup"><span data-stu-id="31dac-341">No</span></span> | <span data-ttu-id="31dac-342">폴더</span><span class="sxs-lookup"><span data-stu-id="31dac-342">Folder</span></span> |

<span data-ttu-id="31dac-343">Hello hello HDInsight 연결 된 서비스에서 참조 하는 Azure Blob 저장소에서에서 두 개의 Spark 작업 파일을 포함 하는 저장소에 대 한 예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="31dac-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

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
