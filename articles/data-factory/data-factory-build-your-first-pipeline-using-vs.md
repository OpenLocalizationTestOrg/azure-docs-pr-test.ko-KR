---
title: "aaaBuild 첫 번째 데이터 팩터리 (Visual Studio) | Microsoft Docs"
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
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="c28c7-103">자습서: Visual Studio를 사용하여 데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="c28c7-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c28c7-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c28c7-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c28c7-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c28c7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c28c7-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c28c7-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c28c7-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c28c7-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c28c7-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c28c7-109">REST API</span><span class="sxs-lookup"><span data-stu-id="c28c7-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="c28c7-110">이 자습서에서는 Visual Studio를 사용 하 여 Azure 데이터 팩터리에 toocreate 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-110">This tutorial shows you how toocreate an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="c28c7-111">Hello Data Factory 프로젝트 템플릿을 사용 하 여 Visual Studio 프로젝트 Data Factory 엔터티 (연결 된 서비스, 데이터 집합 및 파이프라인) 정의 하는 JSON 형식으로 만들고 게시/이러한 엔터티 toohello 클라우드 배포.</span><span class="sxs-lookup"><span data-stu-id="c28c7-111">You create a Visual Studio project using hello Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities toohello cloud.</span></span> 

<span data-ttu-id="c28c7-112">이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c28c7-113">이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="c28c7-114">hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="c28c7-115">이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="c28c7-116">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="c28c7-117">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c28c7-118">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c28c7-119">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="c28c7-120">연습: 데이터 팩터리 엔터티 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="c28c7-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="c28c7-121">다음은이 연습의 일부분으로 수행 하는 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-121">Here are hello steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="c28c7-122">2개의 연결된 서비스인 **AzureStorageLinkedService1** 및 **HDInsightOnDemandLinkedService1**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="c28c7-123">이 자습서에서는 입력 및 출력 데이터에 hello hive 작업에 대 한 hello 동일한 Azure Blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-123">In this tutorial, both input and output data for hello hive activity are in hello same Azure Blob Storage.</span></span> <span data-ttu-id="c28c7-124">주문형 HDInsight 클러스터 tooprocess 기존 입력된 데이터 tooproduce 출력 데이터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-124">You use an on-demand HDInsight cluster tooprocess existing input data tooproduce output data.</span></span> <span data-ttu-id="c28c7-125">hello 주문형 HDInsight 클러스터는 자동으로 생성 Azure 데이터 팩터리에서 hello 입력된 데이터의 처리 준비 toobe 경우 런타임 시.</span><span class="sxs-lookup"><span data-stu-id="c28c7-125">hello on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when hello input data is ready toobe processed.</span></span> <span data-ttu-id="c28c7-126">Toolink 데이터를 저장 하거나 hello 데이터 팩터리 서비스 런타임에 toothem 연결할 수 있도록 tooyour 데이터 팩터리를 계산 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-126">You need toolink your data stores or computes tooyour data factory so that hello Data Factory service can connect toothem at runtime.</span></span> <span data-ttu-id="c28c7-127">따라서 AzureStorageLinkedService1, hello를 사용 하 여 toohello 데이터 팩터리를 Azure 저장소 계정에 연결 하 고 HDInsightOnDemandLinkedService1 hello를 사용 하 여 주문형 HDInsight 클러스터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-127">Therefore, you link your Azure Storage Account toohello data factory by using hello AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using hello HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="c28c7-128">게시, hello 데이터 팩터리 toobe 생성에 대 한 hello 이름 또는 기존 데이터 팩토리 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-128">When publishing, you specify hello name for hello data factory toobe created or an existing data factory.</span></span>  
2. <span data-ttu-id="c28c7-129">두 개의 데이터 집합 만들기: **InputDataset** 및 **OutputDataset**, 있으며 hello Azure blob 저장소에에서 저장 된 hello 입/출력 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent hello input/output data that is stored in hello Azure blob storage.</span></span> 
   
    <span data-ttu-id="c28c7-130">이러한 데이터 집합 정의 hello 이전 단계에서 만든 toohello Azure 저장소 연결 된 서비스를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c28c7-130">These dataset definitions refer toohello Azure Storage linked service you created in hello previous step.</span></span> <span data-ttu-id="c28c7-131">InputDataset hello에 대 한 hello blob 컨테이너 (adfgetstarted)를 지정 하 고 hello hello 입력된 데이터와 함께 blob이 포함 된 폴더 (inptutdata).</span><span class="sxs-lookup"><span data-stu-id="c28c7-131">For hello InputDataset, you specify hello blob container (adfgetstarted) and hello folder (inptutdata) that contains a blob with hello input data.</span></span> <span data-ttu-id="c28c7-132">OutputDataset hello에 대 한 hello blob 컨테이너 (adfgetstarted)를 지정 하 고 hello 출력 데이터를 보유 하는 hello 폴더 (partitioneddata).</span><span class="sxs-lookup"><span data-stu-id="c28c7-132">For hello OutputDataset, you specify hello blob container (adfgetstarted) and hello folder (partitioneddata) that holds hello output data.</span></span> <span data-ttu-id="c28c7-133">구조, 가용성 및 정책과 같은 기타 속성도 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="c28c7-134">**MyFirstPipeline**이라는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="c28c7-135">이 연습에서는 hello 파이프라인에 활동이 하나만: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-135">In this walkthrough, hello pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="c28c7-136">이 활동 변환 하는 주문형 HDInsight 클러스터에서 하이브 스크립트를 실행 하 여 데이터 tooproduce 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-136">This activity transform input data tooproduce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c28c7-137">hive 작업에 대해 자세히 toolearn 참조 [Hive 작업](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="c28c7-137">toolearn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="c28c7-138">**DataFactoryUsingVS**라는 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="c28c7-139">Hello data factory와 모든 데이터 팩터리의 엔터티 (연결 된 서비스, 테이블 및 hello 파이프라인)를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-139">Deploy hello data factory and all Data Factory entities (linked services, tables, and hello pipeline).</span></span>
5. <span data-ttu-id="c28c7-140">를 게시 한 후 Azure 포털 블레이드, 모니터링 및 관리 응용 프로그램 toomonitor hello 파이프라인을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-140">After you publish, you use Azure portal blades and Monitoring & Management App toomonitor hello pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="c28c7-141">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c28c7-141">Prerequisites</span></span>
1. <span data-ttu-id="c28c7-142">자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span> <span data-ttu-id="c28c7-143">Hello를 선택할 수도 있습니다 **개요 및 필수 조건** hello 상위 tooswitch toohello 문서 hello 드롭 다운 목록에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-143">You can also select hello **Overview and prerequisites** option in hello drop-down list at hello top tooswitch toohello article.</span></span> <span data-ttu-id="c28c7-144">Hello 필수 구성 요소를 완료 한 후 뒤로 toothis 문서를 선택 하 여 전환 **Visual Studio** hello 드롭 다운 목록에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-144">After you complete hello prerequisites, switch back toothis article by selecting **Visual Studio** option in hello drop-down list.</span></span>
2. <span data-ttu-id="c28c7-145">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-145">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>  
3. <span data-ttu-id="c28c7-146">Hello 다음이 컴퓨터에 설치 되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-146">You must have hello following installed on your computer:</span></span>
   * <span data-ttu-id="c28c7-147">Visual Studio 2013 또는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c28c7-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="c28c7-148">Visual Studio 2013 또는 Visual Studio 2015용 Azure SDK를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="c28c7-149">너무 이동[Azure 다운로드 페이지](https://azure.microsoft.com/downloads/) 클릭 **VS 2013** 또는 **VS 2015** hello에 **.NET** 섹션.</span><span class="sxs-lookup"><span data-stu-id="c28c7-149">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="c28c7-150">Visual Studio에 대 한 hello 최신 Azure Data Factory 플러그 인을 다운로드: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) 또는 [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-150">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="c28c7-151">Hello 다음 단계를 수행 하 여 hello 플러그 인을 업데이트할 수도 있습니다: hello 메뉴를 클릭 **도구** -> **확장명 및 업데이트** -> **온라인**  ->  **Visual Studio 갤러리** -> **Visual Studio 용 Microsoft Azure 데이터 팩터리 도구** -> **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-151">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="c28c7-152">이제 Visual Studio toocreate Azure 데이터 팩터리를 사용 하 여 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-152">Now, let's use Visual Studio toocreate an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="c28c7-153">Visual Studio 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="c28c7-154">**Visual Studio 2013** 또는 **Visual Studio 2015**를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="c28c7-155">클릭 **파일**, 너무 가리킨**새로**를 클릭 하 고 **프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="c28c7-156">Hello 표시 되어야 **새 프로젝트** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c28c7-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="c28c7-157">Hello에 **새 프로젝트** 대화 상자에서 선택 hello **DataFactory** 템플릿과 클릭 **빈 데이터 팩터리 프로젝트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![새 프로젝트 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="c28c7-159">입력 한 **이름** hello 프로젝트에 대 한 **위치**, 및 hello에 대 한 이름을 **솔루션**를 클릭 하 고 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-159">Enter a **name** for hello project, **location**, and a name for hello **solution**, and click **OK**.</span></span>

    ![솔루션 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="c28c7-161">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-161">Create linked services</span></span>
<span data-ttu-id="c28c7-162">이 단계에서는 두 가지 연결된 서비스 **Azure Storage** 및 **주문형 HDInsight**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="c28c7-163">hello Azure 저장소 서비스 링크 Azure 저장소 계정 toohello 데이터 팩터리 hello 연결 정보를 제공 하 여 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-163">hello Azure Storage linked service links your Azure Storage account toohello data factory by providing hello connection information.</span></span> <span data-ttu-id="c28c7-164">데이터 팩터리 서비스 런타임 시 hello 연결 된 서비스 설정 tooconnect toohello Azure 저장소에서에서 연결 문자열 hello를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-164">Data Factory service uses hello connection string from hello linked service setting tooconnect toohello Azure storage at runtime.</span></span> <span data-ttu-id="c28c7-165">이 저장소 입력을 보유 하 고 hello 파이프라인과 hello에 대 한 출력 데이터 하이브 hello hive 활동에서 사용 하는 스크립트 파일 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-165">This storage holds input and output data for hello pipeline, and hello hive script file used by hello hive activity.</span></span> 

<span data-ttu-id="c28c7-166">HDInsight 클러스터 hello 주문형 HDInsight 연결 된 서비스와 자동 hello 입력된 데이터가 준비 tooprocessed 경우 런타임 시 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-166">With on-demand HDInsight linked service, hello HDInsight cluster is automatically created at runtime when hello input data is ready tooprocessed.</span></span> <span data-ttu-id="c28c7-167">지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 hello 클러스터가 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-167">hello cluster is deleted after it is done processing and idle for hello specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="c28c7-168">데이터 팩터리 솔루션 게시 하는 hello 시 이름 및 설정을 지정 하 여 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-168">You create a data factory by specifying its name and settings at hello time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c28c7-169">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="c28c7-170">마우스 오른쪽 단추로 클릭 **연결 된 서비스** hello 솔루션 탐색기에서 가리키고 너무**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-170">Right-click **Linked Services** in hello solution explorer, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="c28c7-171">Hello에 **새 항목 추가** 대화 상자에서 **Azure 저장소 연결 된 서비스** hello 목록 및 클릭에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-171">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span>
    <span data-ttu-id="c28c7-172">![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="c28c7-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="c28c7-173">대체 `<accountname>` 및 `<accountkey>` Azure 저장소 계정 및 키의 hello 이름의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-173">Replace `<accountname>` and `<accountkey>` with hello name of your Azure storage account and its key.</span></span> <span data-ttu-id="c28c7-174">toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-174">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="c28c7-175">![Azure Storage 연결 서비스](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="c28c7-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="c28c7-176">Hello 저장 **AzureStorageLinkedService1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-176">Save hello **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c28c7-177">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="c28c7-178">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **연결 된 서비스**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-178">In hello **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c28c7-179">**주문형 HDInsight 연결된 서비스**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="c28c7-180">Hello 대체 **JSON** 다음 JSON hello로:</span><span class="sxs-lookup"><span data-stu-id="c28c7-180">Replace hello **JSON** with hello following JSON:</span></span>

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

    <span data-ttu-id="c28c7-181">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-181">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="c28c7-182">속성</span><span class="sxs-lookup"><span data-stu-id="c28c7-182">Property</span></span> | <span data-ttu-id="c28c7-183">설명</span><span class="sxs-lookup"><span data-stu-id="c28c7-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="c28c7-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c28c7-184">ClusterSize</span></span> | <span data-ttu-id="c28c7-185">Hello HDInsight Hadoop 클러스터의 hello 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-185">Specifies hello size of hello HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="c28c7-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c28c7-186">TimeToLive</span></span> | <span data-ttu-id="c28c7-187">삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-187">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="c28c7-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c28c7-188">linkedServiceName</span></span> | <span data-ttu-id="c28c7-189">HDInsight Hadoop 클러스터에 의해 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-189">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="c28c7-190">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON (linkedServiceName)에 지정 된 hello blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-190">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="c28c7-191">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-191">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c28c7-192">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-192">This behavior is by design.</span></span> <span data-ttu-id="c28c7-193">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="c28c7-194">hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-194">hello cluster is automatically deleted when hello processing is done.</span></span>
    > 
    > <span data-ttu-id="c28c7-195">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c28c7-196">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-196">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c28c7-197">이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-197">hello names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="c28c7-198">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="c28c7-199">JSON 속성에 대한 자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="c28c7-200">Hello 저장 **HDInsightOnDemandLinkedService1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-200">Save hello **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="c28c7-201">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-201">Create datasets</span></span>
<span data-ttu-id="c28c7-202">이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-202">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="c28c7-203">이러한 데이터 집합 참조 toohello **AzureStorageLinkedService1** 이 자습서의 앞부분에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-203">These datasets refer toohello **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c28c7-204">Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-204">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="c28c7-205">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-205">Create input dataset</span></span>
1. <span data-ttu-id="c28c7-206">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **테이블**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-206">In hello **Solution Explorer**, right-click **Tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c28c7-207">선택 **Azure Blob** hello 목록에서 hello 파일의 이름을 변경 hello 너무**InputDataSet.json**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-207">Select **Azure Blob** from hello list, change hello name of hello file too**InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="c28c7-208">Hello 대체 **JSON** 다음 JSON 코드 조각은 hello로 hello 편집기에서:</span><span class="sxs-lookup"><span data-stu-id="c28c7-208">Replace hello **JSON** in hello editor with hello following JSON snippet:</span></span>

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
    <span data-ttu-id="c28c7-209">이 JSON 코드 조각은 라는 데이터 집합 정의 **AzureBlobInput** hello hive 활동 hello 파이프라인에 대 한 입력된 데이터를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for hello hive activity in hello pipeline.</span></span> <span data-ttu-id="c28c7-210">Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 `adfgetstarted` 및 라고 하는 hello 폴더 `inputdata`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-210">You specify that hello input data is located in hello blob container called `adfgetstarted` and hello folder called `inputdata`.</span></span>

    <span data-ttu-id="c28c7-211">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-211">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="c28c7-212">속성</span><span class="sxs-lookup"><span data-stu-id="c28c7-212">Property</span></span> | <span data-ttu-id="c28c7-213">설명</span><span class="sxs-lookup"><span data-stu-id="c28c7-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="c28c7-214">type</span><span class="sxs-lookup"><span data-stu-id="c28c7-214">type</span></span> |<span data-ttu-id="c28c7-215">hello type 속성이 너무 설정 되어**AzureBlob** 데이터가 Azure Blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-215">hello type property is set too**AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="c28c7-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c28c7-216">linkedServiceName</span></span> | <span data-ttu-id="c28c7-217">이전에 만든 AzureStorageLinkedService1 toohello를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-217">Refers toohello AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="c28c7-218">fileName</span><span class="sxs-lookup"><span data-stu-id="c28c7-218">fileName</span></span> |<span data-ttu-id="c28c7-219">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-219">This property is optional.</span></span> <span data-ttu-id="c28c7-220">이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-220">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="c28c7-221">이 경우 hello input.log만 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-221">In this case, only hello input.log is processed.</span></span>
    <span data-ttu-id="c28c7-222">type</span><span class="sxs-lookup"><span data-stu-id="c28c7-222">type</span></span> | <span data-ttu-id="c28c7-223">hello 로그 파일은 텍스트 형식으로 TextFormat를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-223">hello log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="c28c7-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c28c7-224">columnDelimiter</span></span> | <span data-ttu-id="c28c7-225">hello 로그 파일의 열 hello 쉼표 문자로 구분 됩니다 (`,`)</span><span class="sxs-lookup"><span data-stu-id="c28c7-225">columns in hello log files are delimited by hello comma character (`,`)</span></span>
    <span data-ttu-id="c28c7-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c28c7-226">frequency/interval</span></span> | <span data-ttu-id="c28c7-227">frequency tooMonth를 설정 하 고 간격은 1 매월 hello 입력된 조각이 사용할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-227">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span>
    <span data-ttu-id="c28c7-228">external</span><span class="sxs-lookup"><span data-stu-id="c28c7-228">external</span></span> | <span data-ttu-id="c28c7-229">이 속성 tootrue 경우 hello 활동에 대 한 입력된 데이터 hello hello 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-229">This property is set tootrue if hello input data for hello activity is not generated by hello pipeline.</span></span> <span data-ttu-id="c28c7-230">이 속성은 입력 데이터 집합에서만 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="c28c7-231">Hello hello 첫 번째 활동의 입력된 데이터 집합, 항상이 속성 설정 tootrue 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-231">For hello input dataset of hello first activity, always set it tootrue.</span></span>
4. <span data-ttu-id="c28c7-232">Hello 저장 **InputDataset.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-232">Save hello **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="c28c7-233">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-233">Create output dataset</span></span>
<span data-ttu-id="c28c7-234">이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent 출력 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-234">Now, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c28c7-235">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **테이블**, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-235">In hello **Solution Explorer**, right-click **tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="c28c7-236">선택 **Azure Blob** hello 목록에서 hello 파일의 이름을 변경 hello 너무**OutputDataset.json**를 클릭 하 고 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-236">Select **Azure Blob** from hello list, change hello name of hello file too**OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="c28c7-237">Hello 대체 **JSON** 다음 JSON hello로 hello 편집기에서:</span><span class="sxs-lookup"><span data-stu-id="c28c7-237">Replace hello **JSON** in hello editor with hello following JSON:</span></span>
    
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
    <span data-ttu-id="c28c7-238">라는 데이터 집합을 정의 하는 hello JSON 코드 조각은 **AzureBlobOutput** 나타내는 hello 파이프라인의 hello hive 활동에 의해 생성 되는 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-238">hello JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by hello hive activity in hello pipeline.</span></span> <span data-ttu-id="c28c7-239">데이터는 hello hive 작업에 의해 생성 되는 hello 출력 라는 hello blob 컨테이너에 배치 됩니다 지정 `adfgetstarted` 및 라고 하는 hello 폴더 `partitioneddata`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-239">You specify that hello output data is produced by hello hive activity is placed in hello blob container called `adfgetstarted` and hello folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="c28c7-240">hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-240">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="c28c7-241">hello 출력 데이터 집합 드라이브 hello 일정 hello 파이프라인의입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-241">hello output dataset drives hello schedule of hello pipeline.</span></span> <span data-ttu-id="c28c7-242">hello 파이프라인의 시작 및 종료 시간 사이의 매월 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-242">hello pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="c28c7-243">참조 **hello 입력된 데이터 집합을 만들** 섹션 이러한 속성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-243">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="c28c7-244">Hello dataset hello 파이프라인에 의해 생성 된 것과 hello 외부 속성에는 출력 데이터 집합 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c28c7-244">You do not set hello external property on an output dataset as hello dataset is produced by hello pipeline.</span></span>
4. <span data-ttu-id="c28c7-245">Hello 저장 **OutputDataset.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-245">Save hello **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="c28c7-246">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="c28c7-246">Create pipeline</span></span>
<span data-ttu-id="c28c7-247">만든 hello Azure 저장소 연결 된 서비스 및 입력 및 출력 데이터 집합 지금까지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-247">You have created hello Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="c28c7-248">이제 **HDInsightHive** 작업이 포함된 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c28c7-249">hello **입력** hello hive 활동 너무 설정 되어**AzureBlobInput** 및 **출력** 너무 설정**AzureBlobOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-249">hello **input** for hello hive activity is set too**AzureBlobInput** and **output** is set too**AzureBlobOutput**.</span></span> <span data-ttu-id="c28c7-250">입력된 데이터 집합의 조각을 매월 (주파수: 월, 간격: 1), hello 출력 조각이 너무 생성 매월 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and hello output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="c28c7-251">Hello에 **솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 **파이프라인**, 너무 가리킨**추가**를 클릭 하 고 **새 항목입니다.**</span><span class="sxs-lookup"><span data-stu-id="c28c7-251">In hello **Solution Explorer**, right-click **Pipelines**, point too**Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="c28c7-252">선택 **Hive 변환 파이프라인** hello 목록 및 클릭에서 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-252">Select **Hive Transformation Pipeline** from hello list, and click **Add**.</span></span>
3. <span data-ttu-id="c28c7-253">Hello 대체 **JSON** 다음 코드 조각 hello로:</span><span class="sxs-lookup"><span data-stu-id="c28c7-253">Replace hello **JSON** with hello following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c28c7-254">대체 `<storageaccountname>` hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-254">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

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
    > <span data-ttu-id="c28c7-255">대체 `<storageaccountname>` hello 저장소 계정 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-255">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    <span data-ttu-id="c28c7-256">hello JSON 코드 조각은 단일 활동 (Hive 활동)으로 구성 된 파이프라인을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-256">hello JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="c28c7-257">이 활동에서 주문형 HDInsight 클러스터 tooproduce 출력 데이터에서 하이브 스크립트 tooprocess 입력된 데이터를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-257">This activity runs a Hive script tooprocess input data on an on-demand HDInsight cluster tooproduce output data.</span></span> <span data-ttu-id="c28c7-258">Hello 파이프라인 JSON의 hello 활동 섹션 유형이 너무 설정 hello 배열에 활동이 하나만 참조**HDInsightHive**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-258">In hello activities section of hello pipeline JSON, you see only one activity in hello array with type set too**HDInsightHive**.</span></span> 

    <span data-ttu-id="c28c7-259">에서는 hello 유형 속성을 특정 tooHDInsight Hive 작업을 Azure 저장소 연결 서비스는 hello hive 스크립트 파일, hello 경로 toohello 스크립트 파일 및 매개 변수 toohello 스크립트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-259">In hello type properties that are specific tooHDInsight Hive activity, you specify what Azure Storage linked service has hello hive script file, hello path toohello script file, and parameters toohello script file.</span></span> 

    <span data-ttu-id="c28c7-260">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정 (hello scriptLinkedService로 지정 됨), 및 hello에 저장 된 `script` hello 컨테이너에 폴더 `adfgetstarted`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-260">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService), and in hello `script` folder in hello container `adfgetstarted`.</span></span>

    <span data-ttu-id="c28c7-261">hello `defines` 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-261">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="c28c7-262">hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-262">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span> <span data-ttu-id="c28c7-263">생성 된 월별, 따라서 (시작 및 종료 날짜에 동일한 hello month 이므로) 조각을 hello 파이프라인에서 생성 된 후에 hello dataset toobe를 구성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-263">You configured hello dataset toobe produced monthly, therefore, only once slice is produced by hello pipeline (because hello month is same in start and end dates).</span></span>

    <span data-ttu-id="c28c7-264">Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-264">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="c28c7-265">Hello 저장 **HiveActivity1.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-265">Save hello **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="c28c7-266">partitionweblogs.hql 및 input.log 종속성으로 추가</span><span class="sxs-lookup"><span data-stu-id="c28c7-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="c28c7-267">마우스 오른쪽 단추로 클릭 **종속성** hello에 **솔루션 탐색기** 창 너무 가리킨**추가**를 클릭 하 고 **기존 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-267">Right-click **Dependencies** in hello **Solution Explorer** window, point too**Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="c28c7-268">Toohello 이동 **C:\ADFGettingStarted** 선택 **partitionweblogs.hql**, **input.log** 파일과 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-268">Navigate toohello **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="c28c7-269">Hello에서 필수 구성 요소 중에이 두 파일을 만든 [자습서 개요](data-factory-build-your-first-pipeline.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-269">You created these two files as part of prerequisites from hello [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="c28c7-270">Hello 다음 단계에서 hello 솔루션을 게시할 때 hello **partitionweblogs.hql** 파일은 업로드 toohello **스크립트** 폴더 hello에 `adfgetstarted` blob 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-270">When you publish hello solution in hello next step, hello **partitionweblogs.hql** file is uploaded toohello **script** folder in hello `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="c28c7-271">데이터 팩터리 엔터티 게시/배포</span><span class="sxs-lookup"><span data-stu-id="c28c7-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="c28c7-272">이 단계에서는 hello Data Factory 엔터티에 (연결 된 서비스, 데이터 집합 및 파이프라인) 프로그램 프로젝트 toohello Azure 데이터 팩터리 서비스에에서 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-272">In this step, you publish hello Data Factory entities (linked services, datasets, and pipeline) in your project toohello Azure Data Factory service.</span></span> <span data-ttu-id="c28c7-273">게시의 hello 프로세스에서 데이터 팩토리에 대 한 hello 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-273">In hello process of publishing, you specify hello name for your data factory.</span></span> 

1. <span data-ttu-id="c28c7-274">Hello 솔루션 탐색기에서에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-274">Right-click project in hello Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="c28c7-275">표시 되 면 **tooyour Microsoft 계정 로그인** 대화 상자에서 Azure 구독이 있는 hello 계정에 대 한 자격 증명을 입력 하 고 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-275">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="c28c7-276">대화 상자를 수행 하는 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-276">You should see hello following dialog box:</span></span>

   ![게시 대화 상자](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="c28c7-278">Hello에 **구성 데이터 팩터리의** 페이지에서 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-278">In hello **Configure data factory** page, do hello following steps:</span></span>

    ![게시 - 새 데이터 팩터리 설정](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="c28c7-280">**새 데이터 팩터리 만들기** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="c28c7-281">고유한 입력 **이름** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-281">Enter a unique **name** for hello data factory.</span></span> <span data-ttu-id="c28c7-282">예: **DataFactoryUsingVS09152016**</span><span class="sxs-lookup"><span data-stu-id="c28c7-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="c28c7-283">hello 이름은 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-283">hello name must be globally unique.</span></span>
   3. <span data-ttu-id="c28c7-284">Hello hello에 대 한 올바른 구독이 선택 **구독** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-284">Select hello right subscription for hello **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="c28c7-285">모든 구독을 표시 되지 않으면 관리자 또는 hello 구독 공동 관리자 인 계정을 사용 하 여 로그인을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>
   4. <span data-ttu-id="c28c7-286">선택 hello **리소스 그룹** hello 데이터 팩터리 toobe 생성에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-286">Select hello **resource group** for hello data factory toobe created.</span></span>
   5. <span data-ttu-id="c28c7-287">선택 hello **지역** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-287">Select hello **region** for hello data factory.</span></span>
   6. <span data-ttu-id="c28c7-288">클릭 **다음** tooswitch toohello **게시 항목** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c28c7-288">Click **Next** tooswitch toohello **Publish Items** page.</span></span> <span data-ttu-id="c28c7-289">(키를 눌러 **탭** hello 이름 필드 tooif hello 부족 toomove **다음** 단추가 비활성화 됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c28c7-289">(Press **TAB** toomove out of hello Name field tooif hello **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="c28c7-290">Hello 오류가 나타나면 **"DataFactoryUsingVS" 데이터 팩터리 이름을 사용할 수 없으면** 을 게시할 때는 hello 이름 (예를 들어 yournameDataFactoryUsingVS)을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-290">If you receive hello error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change hello name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="c28c7-291">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="c28c7-292">Hello에 **게시 항목** 페이지에서 엔터티를 선택 하 고 클릭 하 여 데이터 팩터리를 hello 모든 **다음** tooswitch toohello **요약** 페이지.</span><span class="sxs-lookup"><span data-stu-id="c28c7-292">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>

    ![항목 페이지 게시](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="c28c7-294">Hello 요약을 검토 하 고 클릭 **다음** toostart hello 배포 프로세스와 보기 hello **배포 상태**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-294">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>

    ![요약 페이지](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="c28c7-296">Hello에 **배포 상태** 페이지 hello 배포 프로세스의 hello 상태 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-296">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="c28c7-297">Hello 배포를 완료 한 후 마침을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-297">Click Finish after hello deployment is done.</span></span>

<span data-ttu-id="c28c7-298">중요 한 사항 toonote:</span><span class="sxs-lookup"><span data-stu-id="c28c7-298">Important points toonote:</span></span>

- <span data-ttu-id="c28c7-299">Hello 오류가 나타나면: **이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c28c7-299">If you receive hello error: **This subscription is not registered toouse namespace Microsoft.DataFactory**, do one of hello following and try publishing again:</span></span>
    - <span data-ttu-id="c28c7-300">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-300">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="c28c7-301">데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-301">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="c28c7-302">Azure 구독에서 toohello hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-302">Login using hello Azure subscription in toohello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="c28c7-303">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-303">This action automatically registers hello provider for you.</span></span>
- <span data-ttu-id="c28c7-304">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-304">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
- <span data-ttu-id="c28c7-305">toobe 관리자 또는 공동 관리자의 hello Azure 구독 필요 toocreate 데이터 팩터리 인스턴스</span><span class="sxs-lookup"><span data-stu-id="c28c7-305">toocreate Data Factory instances, you need toobe an admin or co-admin of hello Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="c28c7-306">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c28c7-306">Monitor pipeline</span></span>
<span data-ttu-id="c28c7-307">이 단계에서는 hello 데이터 팩터리의 다이어그램 보기를 사용 하 여 hello 파이프라인을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-307">In this step, you monitor hello pipeline using Diagram View of hello data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="c28c7-308">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c28c7-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="c28c7-309">Toohello 로그인 [Azure 포털](https://portal.azure.com/), 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-309">Log in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>
   1. <span data-ttu-id="c28c7-310">**더 많은 서비스**를 클릭하고 **데이터 팩터리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-310">Click **More services** and click **Data factories**.</span></span>
       
        ![데이터 팩터리 찾아보기](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="c28c7-312">데이터 팩터리의 선택 hello 이름 (예: **DataFactoryUsingVS09152016**) 데이터 팩터리의 hello 목록에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-312">Select hello name of your data factory (for example: **DataFactoryUsingVS09152016**) from hello list of data factories.</span></span>
   
       ![데이터 팩터리 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="c28c7-314">데이터 팩토리에 대 한 hello 홈 페이지에서 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-314">In hello home page for your data factory, click **Diagram**.</span></span>

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="c28c7-316">다이어그램 보기 hello에 hello 파이프라인 및이 자습서에 사용 되는 데이터 집합에 대해 간략하게를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-316">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="c28c7-318">tooview hello 파이프라인에서 마우스 오른쪽 단추로 클릭 파이프라인 hello에 모든 활동 다이어그램 및 열기 파이프라인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-318">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="c28c7-320">Hello 파이프라인의 hello HDInsightHive 활동 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-320">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="c28c7-322">toonavigate toohello 이전 뷰를 다시 클릭 **Data factory** hello 위쪽 hello 이동 경로 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-322">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
6. <span data-ttu-id="c28c7-323">Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobInput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-323">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="c28c7-324">해당 hello 조각이에 속하는지 확인 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-324">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="c28c7-325">준비 상태가 몇 hello 조각 tooshow 분이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-325">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="c28c7-326">Hello 오른쪽 컨테이너에 배치 입력된 hello 파일 (input.log) 되었는지 확인 하면 잠시 후에 발생 하지 않습니다, 하는 경우 (`adfgetstarted`) 및 폴더 (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="c28c7-326">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="c28c7-327">만들고, 해당 hello **외부** hello 입력된 데이터 집합에 속성이 너무**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-327">And, make sure that hello **external** property on hello input dataset is set too**true**.</span></span> 

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="c28c7-329">클릭 **X** tooclose **AzureBlobInput** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-329">Click **X** tooclose **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="c28c7-330">Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-330">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="c28c7-331">현재 처리 중인 해당 hello 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-331">You see that hello slice that is currently being processed.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="c28c7-333">Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-333">When processing is done, you see hello slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c28c7-334">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="c28c7-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c28c7-335">따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-335">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>  
   
    ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="c28c7-337">Hello 조각화 된 경우 **준비** 상태, hello 확인 `partitioneddata` 폴더 hello에 `adfgetstarted` hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-337">When hello slice is in **Ready** state, check hello `partitioneddata` folder in hello `adfgetstarted` container in your blob storage for hello output data.</span></span>  

    ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="c28c7-339">에 대 한 hello 조각 toosee 세부 정보 클릭는 **데이터 조각을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-339">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

    ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="c28c7-341">Hello에서 실행할 활동을 클릭 **활동 실행 목록** 안에 (시나리오에서 하이브 활동)을 실행 하는 활동에 대 한 toosee 세부 정보는 **활동 실행 정보** 창.</span><span class="sxs-lookup"><span data-stu-id="c28c7-341">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="c28c7-343">Hello 로그 파일에서 실행 된 hello 하이브 쿼리 및 상태 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-343">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="c28c7-344">이러한 로그는 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="c28c7-345">참조 [모니터링 데이터 집합 및 파이프라인](data-factory-monitor-manage-pipelines.md) 어떻게 toouse hello Azure 포털 toomonitor hello 파이프라인 및 데이터 집합에서에서 만든이 자습서에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="c28c7-346">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c28c7-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="c28c7-347">모니터를 사용 하 여 & toomonitor 응용 프로그램 파이프라인을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-347">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="c28c7-348">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="c28c7-349">타일 모니터링 및 관리를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-349">Click Monitor & Manage tile.</span></span>

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="c28c7-351">응용 프로그램 모니터링 및 관리가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="c28c7-352">변경 hello **시작 시간** 및 **종료 시간** toomatch 시작 (04-01-2016 오전 12시) 시간 및 종료 시간 (2016-04-02 오전 12시) 파이프라인 및 클릭의 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-352">Change hello **Start time** and **End time** toomatch start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="c28c7-354">활동 창에 대 한 세부 정보 toosee hello에서 선택 **활동 창 목록** toosee 세부 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-354">toosee details about an activity window, select it in hello **Activity Windows list** toosee details about it.</span></span>
    <span data-ttu-id="c28c7-355">![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="c28c7-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c28c7-356">입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-356">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="c28c7-357">따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello 업로드 hello 입력된 파일 (input.log) toohello `inputdata` hello의 폴더 `adfgetstarted` 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-357">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello `inputdata` folder of hello `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="c28c7-358">추가적인 참고 사항</span><span class="sxs-lookup"><span data-stu-id="c28c7-358">Additional notes</span></span>
- <span data-ttu-id="c28c7-359">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c28c7-360">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c28c7-361">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 입력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-361">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="c28c7-362">참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="c28c7-363">참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-363">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="c28c7-364">연결 된 서비스 데이터 저장소를 연결 하거나 서비스 tooan Azure 데이터 팩터리를 계산 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-364">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="c28c7-365">참조 [데이터 저장소를 지원](data-factory-data-movement-activities.md#supported-data-stores-and-formats) 원본 및 싱크 hello 복사 작업에서 지 원하는 모든 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="c28c7-366">참조 [계산 연결 된 서비스](data-factory-compute-linked-services.md) hello 목록이 Data Factory에서 지 원하는 계산 서비스에 대 한 및 [변환 활동](data-factory-data-transformation-activities.md) 하에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-366">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="c28c7-367">참조 [에서 데이터 이동 tooAzure /](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 Azure 저장소 연결 서비스 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-367">See [Move data from/tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in hello Azure Storage linked service definition.</span></span>
- <span data-ttu-id="c28c7-368">주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c28c7-369">자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="c28c7-370">hello 데이터 팩터리가 **Linux 기반** hello JSON 앞에 있는 수에 대 한 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-370">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello preceding JSON.</span></span> <span data-ttu-id="c28c7-371">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="c28c7-372">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON (linkedServiceName)에 지정 된 hello blob 저장소에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-372">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="c28c7-373">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-373">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c28c7-374">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-374">This behavior is by design.</span></span> <span data-ttu-id="c28c7-375">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(timeToLive)가 없는 경우 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="c28c7-376">hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-376">hello cluster is automatically deleted when hello processing is done.</span></span>
    
    <span data-ttu-id="c28c7-377">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c28c7-378">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-378">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c28c7-379">이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-379">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="c28c7-380">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="c28c7-381">현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-381">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="c28c7-382">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-382">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 
- <span data-ttu-id="c28c7-383">이 자습서에서는 Azure Data Factory를 사용하여 데이터를 복사하는 방법을 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="c28c7-384">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-384">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-tooview-data-factories"></a><span data-ttu-id="c28c7-385">서버 탐색기 tooview 데이터 팩터리를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="c28c7-385">Use Server Explorer tooview data factories</span></span>
1. <span data-ttu-id="c28c7-386">**Visual Studio**, 클릭 **보기** 메뉴 hello 되 고 클릭 **서버 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-386">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="c28c7-387">Hello 서버 탐색기 창에서 확장 **Azure** 확장 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-387">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="c28c7-388">표시 되 면 **tooVisual Studio에에서 로그인**, hello 입력 **계정** 연결 된 Azure 구독 및 클릭 **계속**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-388">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="c28c7-389">**암호**를 입력하고 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="c28c7-390">Visual Studio에는 구독에서 모든 Azure 데이터 팩토리에 대 한 정보 tooget 하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-390">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="c28c7-391">Hello에이 작업의 hello 상태를 확인할 **데이터 팩터리에 작업 목록** 창.</span><span class="sxs-lookup"><span data-stu-id="c28c7-391">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![서버 탐색기](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="c28c7-393">데이터 팩터리를 마우스 오른쪽 단추로 클릭 하 고 선택할 수 **데이터 팩터리의 내보내기 tooNew 프로젝트** toocreate 기존 데이터 팩토리를 기반으로 한 Visual Studio 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-393">You can right-click a data factory, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![데이터 팩터리 내보내기](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="c28c7-395">Visual Studio용 데이터 팩터리 도구 업데이트</span><span class="sxs-lookup"><span data-stu-id="c28c7-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="c28c7-396">Visual Studio 용 Azure Data Factory 도구 tooupdate 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-396">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="c28c7-397">클릭 **도구** hello 메뉴를 선택 **확장명 및 업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-397">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="c28c7-398">선택 **업데이트** 에 왼쪽된 창의 hello 선택한 후 **Visual Studio 갤러리**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-398">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="c28c7-399">**Visual Studio용 Azure Data Factory 도구**를 선택하고 **업데이트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="c28c7-400">이 항목을 표시 되지 않으면 최신 버전의 hello 도구 hello이 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-400">If you do not see this entry, you already have hello latest version of hello tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="c28c7-401">구성 파일 사용</span><span class="sxs-lookup"><span data-stu-id="c28c7-401">Use configuration files</span></span>
<span data-ttu-id="c28c7-402">연결 된 서비스/테이블/파이프라인 각 환경에 대해 다른 방식에 대 한 Visual Studio tooconfigure 속성에서 구성 파일을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-402">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="c28c7-403">다음은 Azure 저장소 연결 서비스에 대 한 JSON 정의 hello를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-403">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="c28c7-404">toospecify **connectionString** accountname 및 accountkey hello (프로덕션/개발/테스트) 환경 toowhich 기준에 대 한 값이 서로 다른 배포 하는 데이터 팩터리 엔터티.</span><span class="sxs-lookup"><span data-stu-id="c28c7-404">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="c28c7-405">각 환경에 대한 별도의 구성 파일을 사용하여 이 동작을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="c28c7-406">구성 파일 추가</span><span class="sxs-lookup"><span data-stu-id="c28c7-406">Add a configuration file</span></span>
<span data-ttu-id="c28c7-407">Hello 다음 단계를 수행 하 여 각 환경에 대 한 구성 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-407">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="c28c7-408">Visual Studio 솔루션의 hello Data Factory 프로젝트를 마우스 오른쪽 단추로 클릭, 너무 가리킨**추가**를 클릭 하 고 **새 항목**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-408">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="c28c7-409">선택 **Config** hello hello 왼쪽에 설치 된 템플릿 목록에서 선택 **구성 파일**를 입력 한 **이름** hello 구성에 대 한 파일을 찾아 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-409">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![구성 파일 추가](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="c28c7-411">형식에 따라 hello에 구성 매개 변수 및 해당 값을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-411">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="c28c7-412">이 예제에서는 Azure 저장소 연결된 서비스 및 Azure SQL 연결된 서비스의 connectionString 속성을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="c28c7-413">Hello 구문 이름을 지정 하는 [JsonPath](http://goessner.net/articles/JsonPath/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-413">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="c28c7-414">JSON에 hello 코드 다음에 나와 있는 값의 배열을 포함 하는 속성:</span><span class="sxs-lookup"><span data-stu-id="c28c7-414">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="c28c7-415">다음 구성 파일 (사용 하 여 인덱스가 0부터 시작) hello에 표시 된 대로 속성을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-415">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="c28c7-416">공백이 포함된 속성 이름</span><span class="sxs-lookup"><span data-stu-id="c28c7-416">Property names with spaces</span></span>
<span data-ttu-id="c28c7-417">속성 이름에 공백이 있으면, 다음 예제 (데이터베이스 서버 이름) hello와 같이 대괄호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-417">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="c28c7-418">구성을 사용하여 솔루션 배포</span><span class="sxs-lookup"><span data-stu-id="c28c7-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="c28c7-419">Azure Data Factory 엔터티에 VS에서 게시 하는 hello 원하는 구성으로 toouse 해당 게시 작업에 대해 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-419">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="c28c7-420">구성 파일을 사용 하 여 Azure Data Factory 프로젝트에서 toopublish 엔터티:</span><span class="sxs-lookup"><span data-stu-id="c28c7-420">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="c28c7-421">데이터 팩터리 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **게시** toosee hello **게시 항목** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="c28c7-421">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="c28c7-422">기존 데이터 팩토리를 선택 하거나 hello에 데이터 팩터리 만들기에 대 한 값을 지정할 **구성 데이터 팩터리의** 페이지를 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-422">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="c28c7-423">Hello에 **게시 항목** 페이지: hello에 대 한 사용 가능한 구성으로 드롭 다운 목록을 보려면 **배포 구성 선택** 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-423">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![구성 파일 선택](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="c28c7-425">선택 hello **구성 파일** 있는지 toouse 선택한 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-425">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="c28c7-426">Hello에 대 한 JSON 파일의 hello 이름 표시 되는지 확인 **요약** 페이지 클릭 하 여 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-426">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="c28c7-427">클릭 **마침** hello 배포 작업이 완료 된 후입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-427">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="c28c7-428">를 배포할 때 hello 구성 파일에서 hello 값은 hello 엔터티는 배포 된 tooAzure 데이터 팩터리 서비스 전에 hello JSON 파일의 속성에 대 한 tooset 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-428">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="c28c7-429">Azure Key Vault 사용</span><span class="sxs-lookup"><span data-stu-id="c28c7-429">Use Azure Key Vault</span></span>
<span data-ttu-id="c28c7-430">권장 및 종종 연결 문자열 toohello 코드 저장소와 같은 보안 정책 toocommit 중요 한 데이터에 대 한 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-430">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="c28c7-431">참조 [ADF 게시 Secure](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure 키 자격 증명 모음에 중요 한 정보를 저장 하 고 사용 하 여 데이터 팩터리 엔터티를 게시 하는 동안에 대 한 GitHub toolearn 샘플.</span><span class="sxs-lookup"><span data-stu-id="c28c7-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="c28c7-432">Visual Studio 용 확장명 게시 Secure hello hello 비밀 toobe 주요 자격 증명 모음에 저장 된 있으며 참조 toothem만 연결 된 서비스에 지정 된 / 배포 구성.</span><span class="sxs-lookup"><span data-stu-id="c28c7-432">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="c28c7-433">Data Factory 엔터티에 tooAzure를 게시 하는 경우 이러한 참조는 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-433">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="c28c7-434">이러한 파일 비밀이 노출 하지 않고 커밋된 toosource 리포지토리 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-434">These files can then be committed toosource repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="c28c7-435">요약</span><span class="sxs-lookup"><span data-stu-id="c28c7-435">Summary</span></span>
<span data-ttu-id="c28c7-436">이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-436">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c28c7-437">데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c28c7-437">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="c28c7-438">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c28c7-439">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c28c7-440">**Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-440">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="c28c7-441">**Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-441">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="c28c7-442">Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="c28c7-443">두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="c28c7-444">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="c28c7-445">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c28c7-445">Next Steps</span></span>
<span data-ttu-id="c28c7-446">이 문서에서 파이프라인과 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c28c7-447">toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-447">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="c28c7-448">Hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-448">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c28c7-449">자세한 정보는 [데이터 팩터리의 예약 및 실행](data-factory-scheduling-and-execution.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c28c7-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="c28c7-450">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c28c7-450">See Also</span></span>
| <span data-ttu-id="c28c7-451">항목</span><span class="sxs-lookup"><span data-stu-id="c28c7-451">Topic</span></span> | <span data-ttu-id="c28c7-452">설명</span><span class="sxs-lookup"><span data-stu-id="c28c7-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c28c7-453">파이프라인</span><span class="sxs-lookup"><span data-stu-id="c28c7-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c28c7-454">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse tooconstruct 시나리오 또는 비즈니스에 대 한 워크플로 데이터 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-454">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c28c7-455">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="c28c7-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c28c7-456">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c28c7-457">데이터 변환 활동</span><span class="sxs-lookup"><span data-stu-id="c28c7-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="c28c7-458">이 문서에서는 Azure Data Factory에서 지원되는 데이터 변환 활동(예: 이 자습서에 사용된 HDInsight Hive 변환)의 목록을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="c28c7-459">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="c28c7-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c28c7-460">이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-460">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c28c7-461">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="c28c7-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c28c7-462">이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c28c7-462">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
