---
title: "첫 번째 데이터 팩터리(Visual Studio) 빌드 | Microsoft Docs"
description: "이 자습서에서는 Visual Studio를 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 77042219cbe698a33ab9447aa952586772897241
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="0e0bb-103">자습서: Visual Studio를 사용하여 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="0e0bb-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="0e0bb-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="0e0bb-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="0e0bb-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="0e0bb-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e0bb-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="0e0bb-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e0bb-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="0e0bb-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="0e0bb-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="0e0bb-109">REST API</span><span class="sxs-lookup"><span data-stu-id="0e0bb-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="0e0bb-110">이 자습서에서는 Visual Studio를 사용하여 Azure Data Factory를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="0e0bb-111">데이터 팩터리 프로젝트 템플릿을 사용하여 Visual Studio 프로젝트를 만들고 JSON 형식으로 데이터 팩터리 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)를 정의한 다음 이 엔터티를 이러한 클라우드에 게시하고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="0e0bb-112">이 자습서의 파이프라인에는 **HDInsight Hive 작업**이라는 하나의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="0e0bb-113">이 작업은 Azure HDInsight 클러스터에서 입력 데이터를 변환하여 출력 데이터를 생성하는 Hive 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="0e0bb-114">파이프라인은 지정된 시작 및 종료 시간 사이, 한 달에 한 번 실행되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e0bb-115">이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="0e0bb-116">Azure Data Factory를 사용하여 데이터를 복사하는 방법에 대한 자습서는 [자습서: Blob Storage에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="0e0bb-117">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0e0bb-118">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0e0bb-119">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="0e0bb-120">연습: 데이터 팩터리 엔터티 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="0e0bb-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="0e0bb-121">이 연습 일부로 수행하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-121">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="0e0bb-122">2개의 연결된 서비스인 **AzureStorageLinkedService1** 및 **HDInsightOnDemandLinkedService1**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="0e0bb-123">이 자습서에서는 Hive 작업의 입력 및 출력 데이터가 모두 동일한 Azure Blob Storage에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-123">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="0e0bb-124">주문형 HDInsight 클러스터를 사용하여 출력 데이터를 생성하는 기존 입력 데이터를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-124">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="0e0bb-125">입력 데이터를 처리할 준비가 된 경우 런타임 시 주문형 HDInsight 클러스터가 Azure Data Factory에 의해 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-125">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="0e0bb-126">런타임 시 데이터 팩터리 서비스가 연결할 수 있도록 데이터 저장소 또는 계산을 데이터 팩터리에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-126">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="0e0bb-127">따라서 AzureStorageLinkedService1을 사용하여 Azure Storage 계정을 데이터 팩터리에 연결하고 HDInsightOnDemandLinkedService1을 사용하여 주문형 HDInsight 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-127">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="0e0bb-128">만들려는 데이터 팩터리 또는 기존 데이터 팩터리를 게시할 때 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-128">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="0e0bb-129">Azure Blob Storage에 저장된 입출력 데이터를 나타내는 2개의 데이터 집합인 **InputDataset** 및 **OutputDataset**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="0e0bb-130">이러한 데이터 집합 정의는 이전 단계에서 만든 Azure Storage 연결된 서비스를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-130">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="0e0bb-131">InputDataset의 경우 Blob 컨테이너(adfgetstarted)와 입력 데이터와 함께 Blob을 포함하는 폴더(inptutdata)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-131">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="0e0bb-132">OutputDataset의 경우 Blob 컨테이너(adfgetstarted)와 출력 데이터를 포함하는 폴더(partitioneddata)를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-132">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="0e0bb-133">구조, 가용성 및 정책과 같은 기타 속성도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="0e0bb-134">**MyFirstPipeline**이라는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="0e0bb-135">이 자습서에서 파이프라인에는 **HDInsight Hive 작업**이라는 하나의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-135">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="0e0bb-136">이 작업은 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하여 출력 데이터를 생성하는 입력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-136">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0e0bb-137">Hive 작업에 대한 자세한 내용은 [Hive 작업](data-factory-hive-activity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-137">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="0e0bb-138">**DataFactoryUsingVS**라는 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="0e0bb-139">데이터 팩터리 및 모든 Data Factory 엔터티(연결된 서비스, 테이블 및 파이프라인)를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-139">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="0e0bb-140">파이프라인을 게시한 후에 모니터링하려면 Azure Portal 블레이드 및 모니터링 및 관리 앱을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-140">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="0e0bb-141">필수 조건</span><span class="sxs-lookup"><span data-stu-id="0e0bb-141">Prerequisites</span></span>
1. <span data-ttu-id="0e0bb-142">[자습서 개요](data-factory-build-your-first-pipeline.md) 문서를 살펴보고 **필수 구성 요소** 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="0e0bb-143">문서를 전환하려면 맨 위에 있는 드롭다운 목록에서 **개요 및 필수 구성 요소** 옵션을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-143">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="0e0bb-144">필수 구성 요소를 완료한 후에 드롭 다운 목록에서 **Visual Studio** 옵션을 선택하여 이 문서로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-144">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>
2. <span data-ttu-id="0e0bb-145">데이터 팩터리 인스턴스를 만들려면 구독/리소스 그룹 수준에서 [데이터 팩터리 참여자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-145">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>  
3. <span data-ttu-id="0e0bb-146">다음 항목이 컴퓨터에 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-146">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="0e0bb-147">Visual Studio 2013 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="0e0bb-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="0e0bb-148">Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="0e0bb-149">[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/)로 이동하고 **.NET** 섹션에서 **VS 2013** 또는 **VS 2015**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-149">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="0e0bb-150">Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)용 최신 Azure Data Factory 플러그 인을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-150">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="0e0bb-151">메뉴에서 **도구** -> **확장 및 업데이트** -> **온라인** -> **Visual Studio 갤러리** -> **Visual Studio용 Microsoft Azure Data Factory 도구** -> **업데이트**를 클릭하여 플러그 인을 업데이트할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-151">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="0e0bb-152">이제 Visual Studio를 사용하여 Azure Data Factory를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-152">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="0e0bb-153">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="0e0bb-154">**Visual Studio 2013** 또는 **Visual Studio 2015**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="0e0bb-155">**파일**을 클릭하고 **새로 만들기**를 가리킨 다음 **프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="0e0bb-156">**새 프로젝트** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="0e0bb-157">**새 프로젝트** 대화 상자에서 **DataFactory** 템플릿을 선택하고 **빈 데이터 팩터리 프로젝트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![새 프로젝트 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="0e0bb-159">프로젝트의 **이름**, **위치**, **솔루션**의 이름을 입력한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-159">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![솔루션 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="0e0bb-161">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-161">Create linked services</span></span>
<span data-ttu-id="0e0bb-162">이 단계에서는 두 가지 연결된 서비스 **Azure Storage** 및 **주문형 HDInsight**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="0e0bb-163">Azure Storage 연결된 서비스는 연결 정보를 제공하여 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-163">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="0e0bb-164">데이터 팩터리 서비스는 런타임 시 Azure storage에 연결하기 위해 연결된 서비스 설정에서 연결 문자열을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-164">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="0e0bb-165">이 저장소는 파이프라인의 입력 및 출력 데이터와 Hive 작업에서 사용한 Hive 스크립트 파일을 보유합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-165">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="0e0bb-166">입력 데이터를 처리할 준비가 된 경우 런타임 시 HDInsight 클러스터가 주문형 HDInsight 연결된 서비스를 사용하여 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-166">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="0e0bb-167">클러스터의 처리가 완료되고 지정된 시간 동안 유휴 상태를 유지한 후에 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-167">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e0bb-168">데이터 팩터리 솔루션을 게시할 때에 해당 이름 및 설정을 지정하여 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-168">You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="0e0bb-169">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="0e0bb-170">솔루션 탐색기에서 **연결된 서비스**를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-170">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="0e0bb-171">**새 항목 추가** 대화 상자의 목록에서 **Azure Storage 연결된 서비스**를 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-171">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="0e0bb-172">![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="0e0bb-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="0e0bb-173">`<accountname>` 및 `<accountkey>`를 Azure Storage 계정 이름 및 해당 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-173">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="0e0bb-174">저장소 액세스 키를 가져오는 방법은 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)의 저장소 액세스 키 보기, 복사 및 생성 방법 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-174">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="0e0bb-175">![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="0e0bb-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="0e0bb-176">**AzureStorageLinkedService1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-176">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="0e0bb-177">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="0e0bb-178">**솔루션 탐색기**에서 **연결된 서비스**를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-178">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0e0bb-179">**주문형 HDInsight 연결된 서비스**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="0e0bb-180">**JSON**을 다음 JSON으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-180">Replace the **JSON** with the following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="0e0bb-181">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-181">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="0e0bb-182">속성</span><span class="sxs-lookup"><span data-stu-id="0e0bb-182">Property</span></span> | <span data-ttu-id="0e0bb-183">설명</span><span class="sxs-lookup"><span data-stu-id="0e0bb-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="0e0bb-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="0e0bb-184">ClusterSize</span></span> | <span data-ttu-id="0e0bb-185">HDInsight Hadoop 클러스터의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-185">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="0e0bb-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="0e0bb-186">TimeToLive</span></span> | <span data-ttu-id="0e0bb-187">HDInsight 클러스터가 삭제되기 전 유휴 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="0e0bb-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0e0bb-188">linkedServiceName</span></span> | <span data-ttu-id="0e0bb-189">HDInsight Hadoop 클러스터에 의해 생성되는 로그를 저장하는데 사용될 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-189">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="0e0bb-190">HDInsight 클러스터는 JSON(linkedServiceName)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-190">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="0e0bb-191">HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-191">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="0e0bb-192">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-192">This behavior is by design.</span></span> <span data-ttu-id="0e0bb-193">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="0e0bb-194">클러스터는 처리가 완료되면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-194">The cluster is automatically deleted when the processing is done.</span></span>
    > 
    > <span data-ttu-id="0e0bb-195">많은 조각이 처리될수록 Azure Blob 저장소에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0e0bb-196">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-196">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="0e0bb-197">이러한 컨테이너의 이름은 `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp` 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-197">The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="0e0bb-198">[Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob 저장소에서 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="0e0bb-199">JSON 속성에 대한 자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="0e0bb-200">**HDInsightOnDemandLinkedService1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-200">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="0e0bb-201">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-201">Create datasets</span></span>
<span data-ttu-id="0e0bb-202">이 단계에서는 Hive 처리에 대한 입력 및 출력 데이터를 나타내는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-202">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="0e0bb-203">이러한 데이터 집합은 이 자습서의 앞부분에서 만든 **AzureStorageLinkedService1** 를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-203">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="0e0bb-204">연결된 서비스는 Azure 저장소 계정을 가리키고 데이터 집합은 입력 및 출력 데이터를 가진 저장소의 컨테이너, 폴더, 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-204">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="0e0bb-205">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-205">Create input dataset</span></span>
1. <span data-ttu-id="0e0bb-206">**솔루션 탐색기**에서 **테이블**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-206">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0e0bb-207">목록에서 **Azure Blob**을 선택하고 파일의 이름을 **InputDataSet.json**로 변경한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-207">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="0e0bb-208">편집기에서 **JSON**을 다음 JSON 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-208">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="0e0bb-209">이 JSON 코드 조각에서는 파이프라인의 Hive 작업에 대한 입력 데이터를 나타내는 **AzureBlobInput**라는 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="0e0bb-210">입력 데이터가 `adfgetstarted`라는 Blob 컨테이너 및 `inputdata` 폴더에 저장되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-210">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="0e0bb-211">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-211">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="0e0bb-212">속성</span><span class="sxs-lookup"><span data-stu-id="0e0bb-212">Property</span></span> | <span data-ttu-id="0e0bb-213">설명</span><span class="sxs-lookup"><span data-stu-id="0e0bb-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="0e0bb-214">type</span><span class="sxs-lookup"><span data-stu-id="0e0bb-214">type</span></span> |<span data-ttu-id="0e0bb-215">Azure Blob Storage에 데이터가 있기 때문에 형식 속성은 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-215">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="0e0bb-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0e0bb-216">linkedServiceName</span></span> | <span data-ttu-id="0e0bb-217">이전에 만든 AzureStorageLinkedService1을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-217">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="0e0bb-218">fileName</span><span class="sxs-lookup"><span data-stu-id="0e0bb-218">fileName</span></span> |<span data-ttu-id="0e0bb-219">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-219">This property is optional.</span></span> <span data-ttu-id="0e0bb-220">이 속성을 생략하면 folderPath의 모든 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-220">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="0e0bb-221">이 경우에 input.log만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-221">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="0e0bb-222">type</span><span class="sxs-lookup"><span data-stu-id="0e0bb-222">type</span></span> | <span data-ttu-id="0e0bb-223">로그 파일이 텍스트 형식이므로 TextFormat을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-223">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="0e0bb-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="0e0bb-224">columnDelimiter</span></span> | <span data-ttu-id="0e0bb-225">로그 파일의 열은 쉼표(`,`)로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-225">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="0e0bb-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="0e0bb-226">frequency/interval</span></span> | <span data-ttu-id="0e0bb-227">월 및 간격을 설정한 빈도가 1인 경우 입력 조각은 매월 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-227">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="0e0bb-228">external</span><span class="sxs-lookup"><span data-stu-id="0e0bb-228">external</span></span> | <span data-ttu-id="0e0bb-229">작업의 입력 데이터가 파이프라인에서 생성되지 않는 경우 이 속성은 true로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-229">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="0e0bb-230">이 속성은 입력 데이터 집합에서만 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="0e0bb-231">첫 번째 작업의 입력 데이터 집합의 경우 항상 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-231">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="0e0bb-232">**InputDataset.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-232">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="0e0bb-233">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-233">Create output dataset</span></span>
<span data-ttu-id="0e0bb-234">이제 Azure Blob Storage에 저장된 출력 데이터를 나타내는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-234">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="0e0bb-235">**솔루션 탐색기**에서 **테이블**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-235">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="0e0bb-236">목록에서 **Azure Blob**을 선택하고 파일의 이름을 **OutputDataset.json**로 변경한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-236">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="0e0bb-237">편집기에서 **JSON**을 다음 JSON으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-237">Replace the **JSON** in the editor with the following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
            "typeProperties": {
                "folderPath": "adfgetstarted/partitioneddata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            }
        }
    }
    ```
    <span data-ttu-id="0e0bb-238">JSON 코드 조각에서는 파이프라인의 Hive 작업에서 생성한 출력 데이터를 나타내는 **AzureBlobOutput**이라는 데이터 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-238">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="0e0bb-239">Hive 작업에서 생성된 출력 데이터가 `adfgetstarted`라는 Blob 컨테이너 및 `partitioneddata` 폴더에 배치되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-239">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="0e0bb-240">**가용성** 섹션은 출력 데이터 집합이 월 단위로 생성되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="0e0bb-241">출력 데이터 집합은 파이프라인의 일정을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-241">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="0e0bb-242">파이프라인은 해당 시작 및 종료 시간 사이에 매월 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-242">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="0e0bb-243">이러한 속성에 대한 설명은 **입력 데이터 집합 만들기** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-243">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="0e0bb-244">파이프라인에서 데이터 집합이 생성되므로 출력 데이터 집합에 외부 속성을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-244">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="0e0bb-245">**OutputDataset.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-245">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="0e0bb-246">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="0e0bb-246">Create pipeline</span></span>
<span data-ttu-id="0e0bb-247">지금까지 Azure Storage 연결된 서비스와 입력 및 출력 데이터 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-247">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="0e0bb-248">이제 **HDInsightHive** 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="0e0bb-249">Hive 작업에 대한 **입력**을 **AzureBlobInput**으로 설정하고 작업에 대한 **출력**을 **AzureBlobOutput**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-249">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="0e0bb-250">입력 데이터 집합의 조각은 매월 사용 가능(빈도: 월, 간격: 1)하고 출력 조각도 매월 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="0e0bb-251">**솔루션 탐색기**에서 **파이프라인**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-251">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="0e0bb-252">목록에서 **Hive 변환 파이프라인**을 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-252">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="0e0bb-253">**JSON**을 다음 코드 조각으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-253">Replace the **JSON** with the following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0e0bb-254">`<storageaccountname>`을 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-254">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
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
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0e0bb-255">`<storageaccountname>`을 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-255">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    <span data-ttu-id="0e0bb-256">JSON 코드 조각은 단일 작업(Hive 작업)으로 구성된 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-256">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="0e0bb-257">이 작업은 주문형 HDInsight 클러스터에서 입력 데이터를 처리하여 출력 데이터를 생성하는 Hive 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-257">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="0e0bb-258">파이프라인 JSON의 작업 섹션에서는 **HDInsightHive**로 설정된 형식을 가진 배열에 하나의 작업만이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-258">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="0e0bb-259">HDInsight Hive 작업에만 특정되는 형식 속성에서 Azure Storage 연결된 서비스에 있는 Hive 스크립트 파일, 스크립트 파일에 대한 경로 및 스크립트 파일에 대한 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-259">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="0e0bb-260">Hive 스크립트 파일 **partitionweblogs.hql**은 Azure Storage 계정(scriptLinkedService에 의해 지정됨)과 `adfgetstarted`라는 컨테이너의 `script` 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-260">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="0e0bb-261">`defines` 섹션은 Hive 스크립트에 Hive 구성 값(예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`)으로 전달되는 런타임 설정을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-261">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="0e0bb-262">파이프라인의 **start** 및 **end** 속성은 파이프라인의 활성 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-262">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="0e0bb-263">데이터 집합이 매월 생성되도록 구성했으므로 파이프라인에서 한 번만 조각이 생성됩니다(매월 시작 및 종료 날짜가 동일하기 때문).</span><span class="sxs-lookup"><span data-stu-id="0e0bb-263">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="0e0bb-264">작업 JSON에서 **linkedServiceName** – **HDInsightOnDemandLinkedService**에서 지정한 계산에 대해 Hive 스크립트가 실행되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-264">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="0e0bb-265">**HiveActivity1.json** 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-265">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="0e0bb-266">partitionweblogs.hql 및 input.log 종속성으로 추가</span><span class="sxs-lookup"><span data-stu-id="0e0bb-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="0e0bb-267">**솔루션 탐색기** 창에서 **종속성**을 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **기존 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-267">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="0e0bb-268">**C:\ADFGettingStarted**로 이동하고 **partitionweblogs.hql**, **input.log** 파일을 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-268">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="0e0bb-269">[자습서 개요](data-factory-build-your-first-pipeline.md)에서 필수 구성 요소의 일부로 이 두 파일을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-269">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="0e0bb-270">다음 단계에서 솔루션을 게시할 때 **partitionweblogs.hql** 파일은 `adfgetstarted` Blob 컨테이너의 **스크립트** 폴더에 업로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-270">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="0e0bb-271">데이터 팩터리 엔터티 게시/배포</span><span class="sxs-lookup"><span data-stu-id="0e0bb-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="0e0bb-272">이 단계에서는 Azure Data Factory 서비스에 프로젝트의 데이터 팩터리 엔터티(연결된 서비스, 데이터 집합 및 파이프라인)를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-272">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="0e0bb-273">게시 과정에서 데이터 팩터리의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-273">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="0e0bb-274">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-274">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="0e0bb-275">**Microsoft 계정에 로그인** 대화 상자가 표시되면 Azure 구독이 있는 계정의 자격 증명을 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-275">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="0e0bb-276">다음 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-276">You should see the following dialog box:</span></span>

   ![게시 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="0e0bb-278">**데이터 팩터리 구성** 페이지에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-278">In the **Configure data factory** page, do the following steps:</span></span>

    ![게시 - 새 데이터 팩터리 설정](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="0e0bb-280">**새 데이터 팩터리 만들기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="0e0bb-281">데이터 팩터리의 고유한 **이름** 을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-281">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="0e0bb-282">예: **DataFactoryUsingVS09152016**</span><span class="sxs-lookup"><span data-stu-id="0e0bb-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="0e0bb-283">이름은 전역적으로 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-283">The name must be globally unique.</span></span>
   3. <span data-ttu-id="0e0bb-284">**구독** 필드에서 올바른 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-284">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="0e0bb-285">모든 구독이 표시되지 않으면 구독의 관리자 또는 공동 관리자인 계정을 사용하여 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>
   4. <span data-ttu-id="0e0bb-286">생성되는 데이터 팩터리의 **리소스 그룹** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-286">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="0e0bb-287">데이터 팩터리의 **하위 지역** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-287">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="0e0bb-288">**다음**을 클릭하여 **항목 게시** 페이지로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-288">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="0e0bb-289">**다음** 단추를 사용할 수 없는 경우 **TAB** 키를 눌러 이름 필드에서 나갑니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-289">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0e0bb-290">게시할 때 **데이터 팩터리 이름 “DataFactoryUsingVS”를 사용할 수 없습니다.** 오류가 표시되는 경우 이름을 변경합니다(예: yournameDataFactoryUsingVS).</span><span class="sxs-lookup"><span data-stu-id="0e0bb-290">If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="0e0bb-291">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="0e0bb-292">**항목 게시** 페이지에서 모든 데이터 팩터리 엔터티가 선택되었는지 확인하고 **다음**을 클릭하여 **요약** 페이지로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-292">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![항목 페이지 게시](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="0e0bb-294">요약을 검토한 후 **다음**을 클릭하여 배포 프로세스를 시작하고 **배포 상태**를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-294">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![요약 페이지](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="0e0bb-296">**배포 상태** 페이지에 배포 프로세스의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-296">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="0e0bb-297">배포가 완료되면 마침을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-297">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="0e0bb-298">염두해 둘 중요한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-298">Important points to note:</span></span>

- <span data-ttu-id="0e0bb-299">**구독이 Microsoft.DataFactory 네임스페이스를 사용하도록 등록되어 있지 않습니다.**라는 오류를 수신하는 경우 다음 중 하나를 수행하고 다시 게시하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-299">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="0e0bb-300">Azure PowerShell에서 다음 명령을 실행하여 Data Factory 공급자를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-300">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="0e0bb-301">데이터 팩터리 공급자가 등록되어 있는지 확인하려면 다음 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-301">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="0e0bb-302">Azure 구독을 사용하여 [Azure 포털](https://portal.azure.com) 에 로그인하고 데이터 팩터리 블레이드로 이동하거나 Azure 포털에 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-302">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="0e0bb-303">이 작업은 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-303">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="0e0bb-304">데이터 팩터리의 이름은 나중에 DNS 이름으로 표시되므로 공개적으로 등록될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-304">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="0e0bb-305">데이터 팩터리 인스턴스를 만들려면 Azure 구독의 관리자 또는 공동 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-305">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="0e0bb-306">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="0e0bb-306">Monitor pipeline</span></span>
<span data-ttu-id="0e0bb-307">이 단계에서는 데이터 팩터리의 다이어그램 뷰를 사용하여 파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-307">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="0e0bb-308">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="0e0bb-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="0e0bb-309">[Azure Portal](https://portal.azure.com/)에 로그인하고 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-309">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="0e0bb-310">**더 많은 서비스**를 클릭하고 **데이터 팩터리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-310">Click **More services** and click **Data factories**.</span></span>
       
        ![데이터 팩터리 찾아보기](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="0e0bb-312">데이터 팩터리의 목록에서 데이터 팩터리의 이름을 선택합니다(예: **DataFactoryUsingVS09152016**).</span><span class="sxs-lookup"><span data-stu-id="0e0bb-312">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![데이터 팩터리 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="0e0bb-314">데이터 팩터리에 대한 홈페이지에서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-314">In the home page for your data factory, click **Diagram**.</span></span>

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="0e0bb-316">다이어그램 보기에 파이프라인의 개요와 이 자습서에 사용된 데이터 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-316">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="0e0bb-318">파이프라인의 모든 작업을 보려면 다이어그램에서 파이프라인을 마우스 오른쪽 단추로 클릭하고 파이프라인 열기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-318">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="0e0bb-320">파이프라인에서 HDInsightHive 활동이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-320">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="0e0bb-322">이전 보기를 탐색하려면 맨 위에서 breadcrumb 메뉴의 **데이터 팩터리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-322">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="0e0bb-323">**다이어그램 보기**에서 **AzureBlobInput** 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-323">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="0e0bb-324">조각이 **준비** 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-324">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="0e0bb-325">조각이 준비 상태로 표시되려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-325">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="0e0bb-326">잠시 대기한 후에 표시되지 않는 경우 오른쪽 컨테이너(`adfgetstarted`) 및 폴더(`inputdata`)에 배치된 입력 파일(input.log)이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-326">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="0e0bb-327">입력 데이터 집합의 **외부** 속성을 **true**로 설정했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-327">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="0e0bb-329">**X**를 닫아서 **AzureBlobInput** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-329">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="0e0bb-330">**다이어그램 보기**에서 **AzureBlobOutput** 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-330">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="0e0bb-331">현재 처리 중인 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-331">You see that the slice that is currently being processed.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="0e0bb-333">처리가 완료되면 **준비** 상태인 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-333">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0e0bb-334">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="0e0bb-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="0e0bb-335">따라서 파이프라인이 조각을 처리하는 데 **약 30분**이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-335">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>  
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="0e0bb-337">조각이 **준비** 상태이면 Blob Storage의 `adfgetstarted` 컨테이너에 있는 `partitioneddata` 폴더에서 출력 데이터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-337">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="0e0bb-339">자세한 내용을 보려면 **데이터 조각** 블레이드에서 조각을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-339">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="0e0bb-341">**작업 실행 목록**에서 작업 실행을 클릭하여 **작업 실행 세부 정보** 창에서 작업 실행에 대한 세부 정보를 봅니다(이 시나리오에서 Hive 작업).</span><span class="sxs-lookup"><span data-stu-id="0e0bb-341">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="0e0bb-343">로그 파일에서 실행되는 Hive 쿼리 및 상태 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-343">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="0e0bb-344">이러한 로그는 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="0e0bb-345">Azure 포털을 사용하여 이 자습서에서 만든 파이프라인 및 데이터 집합을 모니터링하는 방법에 대한 지침은 [데이터 집합 및 파이프라인 모니터링](data-factory-monitor-manage-pipelines.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="0e0bb-346">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="0e0bb-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="0e0bb-347">응용 프로그램 모니터링 및 관리를 사용하여 파이프라인을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-347">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="0e0bb-348">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="0e0bb-349">타일 모니터링 및 관리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-349">Click Monitor & Manage tile.</span></span>

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="0e0bb-351">응용 프로그램 모니터링 및 관리가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="0e0bb-352">**시작 시간** 및 **종료 시간**을 파이프라인 시작 시간(2016-04-01 오전 12시) 및 종료 시간(2016-04-02 오전 12시)에 맞게 변경하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-352">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="0e0bb-354">작업 창에 대한 자세한 내용을 보려면 **작업 창 목록**에서 작업 창을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-354">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="0e0bb-355">![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="0e0bb-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0e0bb-356">조각이 성공적으로 처리될 때 입력된 파일이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-356">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="0e0bb-357">따라서 조각을 다시 실행하거나 자습서를 다시 수행하려는 경우 `adfgetstarted` 컨테이너의 `inputdata` 폴더에 입력 파일(input.log)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-357">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="0e0bb-358">추가적인 참고 사항</span><span class="sxs-lookup"><span data-stu-id="0e0bb-358">Additional notes</span></span>
- <span data-ttu-id="0e0bb-359">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0e0bb-360">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0e0bb-361">예를 들어 원본에서 대상 데이터 저장소에 데이터를 복사하는 복사 작업 및 입력 데이터를 변환할 Hive 스크립트를 실행하는 HDInsight Hive 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-361">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="0e0bb-362">복사 작업에서 지원하는 모든 원본 및 싱크는 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="0e0bb-363">데이터 팩터리에서 지원하는 계산 서비스 목록은 [연결된 계산 서비스](data-factory-compute-linked-services.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-363">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="0e0bb-364">연결된 서비스는 데이터 저장소 또는 계산 서비스를 Azure Data Factory에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-364">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="0e0bb-365">복사 작업에서 지원하는 모든 원본 및 싱크는 [지원되는 데이터 저장소](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="0e0bb-366">데이터 팩터리에서 지원하는 계산 서비스 목록 및 여기에서 실행할 수 있는 [변환 작업](data-factory-data-transformation-activities.md)은 [연결된 계산 서비스](data-factory-compute-linked-services.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-366">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="0e0bb-367">Azure Storage 연결된 서비스 정의에서 사용된 JSON 속성에 대한 자세한 내용은 [Azure Blob 간에 데이터 이동](data-factory-azure-blob-connector.md#azure-storage-linked-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-367">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="0e0bb-368">주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0e0bb-369">자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="0e0bb-370">데이터 팩터리는 앞의 JSON으로 사용자에게 **Linux 기반** HDInsight 클러스터를 만들어 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-370">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="0e0bb-371">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="0e0bb-372">HDInsight 클러스터는 JSON(linkedServiceName)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="0e0bb-373">HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-373">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="0e0bb-374">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-374">This behavior is by design.</span></span> <span data-ttu-id="0e0bb-375">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="0e0bb-376">클러스터는 처리가 완료되면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-376">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="0e0bb-377">많은 조각이 처리될수록 Azure Blob 저장소에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="0e0bb-378">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="0e0bb-379">이러한 컨테이너의 이름은 `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp` 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="0e0bb-380">[Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob 저장소에서 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="0e0bb-381">현재 출력 데이터 집합이 일정을 결정하므로 작업이 출력을 생성하지 않는 경우 출력 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="0e0bb-382">활동이 입력을 가져오지 않으면 입력 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-382">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="0e0bb-383">이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="0e0bb-384">Azure Data Factory를 사용하여 데이터를 복사하는 방법에 대한 자습서는 [자습서: Blob Storage에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="0e0bb-385">서버 탐색기를 사용하여 데이터 팩터리 검토</span><span class="sxs-lookup"><span data-stu-id="0e0bb-385">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="0e0bb-386">**Visual Studio**의 메뉴에서 **보기**를 클릭한 다음 **서버 탐색기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="0e0bb-387">서버 탐색기 창에서 **Azure**를 확장한 다음 **Data Factory**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="0e0bb-388">**Visual Studio에 로그인**이 표시되면 Azure 구독과 연결된 **계정**을 입력하고 **계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="0e0bb-389">**암호**를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="0e0bb-390">Visual Studio에서는 구독에 있는 모든 Azure Data Factory에 대한 정보를 가져오려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="0e0bb-391">**데이터 팩터리 작업 목록** 창에 이 작업의 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-391">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![서버 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="0e0bb-393">데이터 팩터리를 마우스 오른쪽 단추로 클릭하고 **새 프로젝트로 데이터 팩터리 내보내기** 를 선택하여 기존 데이터 팩터리에 따라 Visual Studio 프로젝트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![데이터 팩터리 내보내기](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="0e0bb-395">Visual Studio용 데이터 팩터리 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="0e0bb-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="0e0bb-396">Visual Studio용 Azure Data Factory 도구를 업데이트하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="0e0bb-397">메뉴에서 **도구**를 클릭하고 **확장 및 업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-397">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="0e0bb-398">왼쪽 창에서 **업데이트**를 선택한 다음 **Visual Studio 갤러리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="0e0bb-399">**Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="0e0bb-400">이 항목이 표시되지 않으면 이미 최신 버전의 도구가 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-400">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="0e0bb-401">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="0e0bb-401">Use configuration files</span></span>
<span data-ttu-id="0e0bb-402">각 환경마다 다르게 연결된 서비스/테이블/파이프라인에 대한 속성을 구성하기 위해 Visual Studio의 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="0e0bb-403">Azure 저장소 연결 서비스에 대한 다음 JSON 정의를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-403">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="0e0bb-404">데이터 팩터리 엔터티를 배포하는 환경(개발/테스트/프로덕션)에 따라 서로 다른 accountname 및 accountkey에 대한 값으로 **connectionString**을 지정하려면</span><span class="sxs-lookup"><span data-stu-id="0e0bb-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="0e0bb-405">각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="0e0bb-406">구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="0e0bb-406">Add a configuration file</span></span>
<span data-ttu-id="0e0bb-407">다음 단계를 수행하여 각 환경에 대한 구성 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-407">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="0e0bb-408">Visual Studio 솔루션의 데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가**를 가리킨 다음 **새 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="0e0bb-409">왼쪽에 있는 설치된 템플릿 목록에서 **구성**을 선택하고 **구성 파일**을 선택한 다음, 구성 파일의 **이름**을 입력하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="0e0bb-411">다음 형식으로 구성 매개 변수와 해당 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-411">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="0e0bb-412">이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="0e0bb-413">이름을 지정하는 구문은 [JsonPath](http://goessner.net/articles/JsonPath/)입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="0e0bb-414">JSON에 다음 코드와 같은 값의 배열을 가진 속성이 있는 경우:</span><span class="sxs-lookup"><span data-stu-id="0e0bb-414">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
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
    ```

    <span data-ttu-id="0e0bb-415">다음 구성 파일(0부터 시작되는 인덱스 사용)과 같은 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="0e0bb-416">공백이 포함된 속성 이름</span><span class="sxs-lookup"><span data-stu-id="0e0bb-416">Property names with spaces</span></span>
<span data-ttu-id="0e0bb-417">속성 이름에 공백이 있으면 다음 예제(데이터베이스 서버 이름)와 같이 대괄호를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="0e0bb-418">구성을 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="0e0bb-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="0e0bb-419">VS에서 Azure 데이터 팩터리 엔터티를 게시하는 경우 해당 게시 작업에 사용하려는 구성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="0e0bb-420">구성 파일을 사용하여 Azure 데이터 팩터리 프로젝트에서 엔터티를 게시하려면</span><span class="sxs-lookup"><span data-stu-id="0e0bb-420">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="0e0bb-421">Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭하여 **게시 항목** 대화 상자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="0e0bb-422">기존 데이터 팩터리를 선택하거나 **데이터 팩터리 구성** 페이지에서 데이터 팩터리를 만드는 값을 지정하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="0e0bb-423">**항목 게시** 페이지에서 **배포 구성 선택** 필드에 사용 가능한 구성이 있는 드롭다운 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="0e0bb-425">사용하려는 **구성 파일**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-425">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="0e0bb-426">**요약** 페이지에서 JSON 파일의 이름이 표시되는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="0e0bb-427">배포 작업이 완료되면 **마침** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-427">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="0e0bb-428">배포할 때 구성 파일의 값은 엔터티가 Azure Data Factory 서비스에 배포되기 전에 JSON 파일에서 속성 값을 설정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="0e0bb-429">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="0e0bb-429">Use Azure Key Vault</span></span>
<span data-ttu-id="0e0bb-430">연결 문자열과 같은 중요한 데이터를 코드 리포지토리에 커밋하는 것은 보안 정책에 위배되는 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="0e0bb-431">Azure Key Vault에 중요 정보를 저장하고 Data Factory 엔터티를 게시하면서 사용하는 방법에 대한 자세한 내용은 GitHub의 [ADF 보안 게시](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish)(영문) 샘플을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="0e0bb-432">Visual Studio에 대한 보안 게시 확장을 통해 비밀이 Key Vault에 저장되도록 하고 이에 대한 참조만 연결된 서비스/배포 구성에 지정하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="0e0bb-433">이러한 참조는 Data Factory 엔터티를 Azure에 게시할 때 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-433">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="0e0bb-434">그런 다음 이러한 파일을 비밀을 노출하지 않고 원본 리포지토리에 커밋할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-434">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="0e0bb-435">요약</span><span class="sxs-lookup"><span data-stu-id="0e0bb-435">Summary</span></span>
<span data-ttu-id="0e0bb-436">이 자습서에서는 HDInsight hadoop 클러스터에서 Hive 스크립트를 실행하여 데이터를 처리하는 데 Azure 데이터 팩터리를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="0e0bb-437">Azure 포털에서 다음 단계를 수행하기 위해 데이터 팩터리 편집기를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="0e0bb-438">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="0e0bb-439">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="0e0bb-440">**Azure 저장소** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="0e0bb-441">**Azure HDInsight** 주문형 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="0e0bb-442">Azure 데이터 팩터리는 입력 데이터를 처리하고 출력 데이터를 생성하기 위해 적시에 HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="0e0bb-443">파이프라인에서 HDInsight Hive 작업에 대한 입력 및 출력 데이터를 설명하는 두 개의 **데이터 집합**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="0e0bb-444">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0e0bb-445">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0e0bb-445">Next Steps</span></span>
<span data-ttu-id="0e0bb-446">이 문서에서 파이프라인과 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="0e0bb-447">복사 작업을 사용하여 Azure Blob에서 Azure SQL로 데이터를 복사하는 방법은 [자습서: Azure Blob에서 Azure SQL로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="0e0bb-448">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정하여 두 활동을 연결하면 해당 활동을 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0e0bb-449">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="0e0bb-450">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0e0bb-450">See Also</span></span>
| <span data-ttu-id="0e0bb-451">항목</span><span class="sxs-lookup"><span data-stu-id="0e0bb-451">Topic</span></span> | <span data-ttu-id="0e0bb-452">설명</span><span class="sxs-lookup"><span data-stu-id="0e0bb-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="0e0bb-453">파이프라인</span><span class="sxs-lookup"><span data-stu-id="0e0bb-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="0e0bb-454">이 문서는 Azure Data Factory의 파이프라인 및 시나리오 또는 비즈니스를 위한 활동과 데이터 기반 워크플로를 활용하는 방법을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="0e0bb-455">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="0e0bb-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="0e0bb-456">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="0e0bb-457">데이터 변환 활동</span><span class="sxs-lookup"><span data-stu-id="0e0bb-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="0e0bb-458">이 문서에서는 Azure Data Factory에서 지원되는 데이터 변환 활동(예: 이 자습서에 사용된 HDInsight Hive 변환)의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="0e0bb-459">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="0e0bb-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="0e0bb-460">이 문서에서는 Azure Data Factory 응용 프로그램 모델의 예약 및 실행에 대한 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="0e0bb-461">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="0e0bb-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="0e0bb-462">이 문서는 모니터링 및 관리 앱을 사용하여 파이프라인을 모니터링하고 관리하고 디버그하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0e0bb-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
