---
title: "첫 번째 데이터 팩터리(Azure 포털) 빌드 | Microsoft Docs"
description: "이 자습서에서는 Azure 포털의 데이터 팩터리 편집기를 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="02b0d-103">자습서: Azure Portal을 사용하여 첫 번째 Azure Data Factory 빌드</span><span class="sxs-lookup"><span data-stu-id="02b0d-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="02b0d-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="02b0d-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="02b0d-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="02b0d-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="02b0d-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="02b0d-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="02b0d-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02b0d-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="02b0d-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="02b0d-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="02b0d-109">REST API</span><span class="sxs-lookup"><span data-stu-id="02b0d-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="02b0d-110">이 문서에서는 [Azure Portal](https://portal.azure.com/)을 사용하여 첫 번째 Azure Data Factory를 만드는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="02b0d-111">다른 도구/SDK를 사용하여 이 자습서를 수행하려면 드롭다운 목록에서 옵션 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="02b0d-112">이 자습서의 파이프라인에는 **HDInsight Hive 작업**이라는 하나의 작업이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="02b0d-113">이 작업은 Azure HDInsight 클러스터에서 입력 데이터를 변환하여 출력 데이터를 생성하는 Hive 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="02b0d-114">파이프라인은 지정된 시작 및 종료 시간 사이, 한 달에 한 번 실행되도록 예약됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="02b0d-115">이 자습서의 데이터 파이프라인은 출력 데이터를 생성하는 입력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="02b0d-116">Azure Data Factory를 사용하여 데이터를 복사하는 방법에 대한 자습서는 [자습서: Blob Storage에서 SQL Database로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="02b0d-117">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="02b0d-118">한 활동의 출력 데이터 집합을 다른 활동의 입력 데이터 집합으로 설정함으로써 두 활동을 연결하여 활동을 하나씩 차례로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="02b0d-119">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02b0d-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="02b0d-120">Prerequisites</span></span>
1. <span data-ttu-id="02b0d-121">[자습서 개요](data-factory-build-your-first-pipeline.md) 문서를 살펴보고 **필수 구성 요소** 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="02b0d-122">이 문서는 Azure Data Factory 서비스에 대한 개념적 개요를 제공하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="02b0d-123">서비스의 자세한 개요는 [Azure Data Factory 소개](data-factory-introduction.md) 문서를 읽어보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="02b0d-124">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-124">Create data factory</span></span>
<span data-ttu-id="02b0d-125">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="02b0d-126">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="02b0d-127">예를 들어 원본에서 대상 데이터 저장소에 데이터를 복사하는 복사 작업 및 입력 데이터를 제품 출력 데이터로 변환하는 Hive 스크립트를 실행하는 HDInsight Hive 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="02b0d-128">이 단계에서는 데이터 팩터리 만들기를 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="02b0d-129">[Azure 포털](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="02b0d-130">왼쪽 메뉴에서 **새로 만들기**를 클릭하고 **데이터 + 분석**을 클릭하고 **Data Factory**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![블레이드 만들기](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="02b0d-132">**새 데이터 팩터리** 블레이드에서 이름으로 **GetStartedDF**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![새 데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="02b0d-134">Azure Data Factory의 이름은 **전역적으로 고유**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="02b0d-135">**데이터 팩터리 이름 "GetStartedDF"를 사용할 수 없습니다**라는 오류를 수신하는 경우.</span><span class="sxs-lookup"><span data-stu-id="02b0d-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="02b0d-136">데이터 팩터리(예: yournameGetStartedDF)의 이름을 변경하고 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="02b0d-137">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="02b0d-138">데이터 팩터리의 이름은 나중에 **DNS** 이름으로 표시되므로 공개적으로 등록될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="02b0d-139">데이터 팩터리를 만들려는 위치의 **Azure 구독** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="02b0d-140">기존 **리소스 그룹** 을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="02b0d-141">이 자습서에서 **ADFGetStartedRG**라는 이름의 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="02b0d-142">데이터 팩터리의 **위치** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="02b0d-143">Data Factory 서비스에서 지원하는 지역만 드롭다운 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="02b0d-144">**대시보드에 고정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="02b0d-145">**새 Data Factory** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="02b0d-146">데이터 팩터리 인스턴스를 만들려면 구독/리소스 그룹 수준에서 [데이터 팩터리 참여자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) 역할의 구성원이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="02b0d-147">대시보드에서 데이터 팩터리 배포 중 상태의 타일이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![데이터 팩터리 만들기 상태](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="02b0d-149">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-149">Congratulations!</span></span> <span data-ttu-id="02b0d-150">첫 번째 데이터 팩터리 만들기가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="02b0d-151">데이터 팩터리 만들기를 완료한 후에는 데이터 팩터리 페이지가 표시되며 여기에 데이터 팩터리의 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="02b0d-153">데이터 팩터리에서 파이프라인을 만들기 전에 먼저 몇 가지 데이터 팩터리 엔터티를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="02b0d-154">먼저 데이터 저장소에 데이터 저장소/계산을 연결하는 연결된 서비스를 만들고 연결된 데이터 저장소에서 데이터를 나타내는 입력 및 출력 데이터 집합을 정의한 다음 이러한 데이터 집합을 사용하는 작업을 통해 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="02b0d-155">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-155">Create linked services</span></span>
<span data-ttu-id="02b0d-156">이 단계에서는 Azure Storage 계정 및 주문형 Azure HDInsight 클러스터를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="02b0d-157">Azure Storage 계정은 이 샘플의 파이프라인에 대한 입력 및 출력 데이터를 가집니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="02b0d-158">HDInsight 연결된 서비스는 이 샘플에서 파이프라인의 활동에 지정된 Hive 스크립트를 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="02b0d-159">시나리오에 사용되는 [데이터 저장소](data-factory-data-movement-activities.md)/[계산 서비스](data-factory-compute-linked-services.md)를 식별하고 연결된 서비스를 만들어 해당 서비스를 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="02b0d-160">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="02b0d-161">이 단계에서는 Azure Storage 계정을 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="02b0d-162">이 자습서에서는 동일한 Azure Storage 계정을 사용하여 입력/출력 데이터 및 HQL 스크립트 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="02b0d-163">**GetStartedDF**에 대한 **데이터 팩터리** 블레이드에서 **작성 및 배포**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="02b0d-164">데이터 팩터리 편집기가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-164">You should see the Data Factory Editor.</span></span>

   ![작성 및 배포 타일](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="02b0d-166">**새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="02b0d-168">편집기에 Azure 저장소 연결된 서비스를 만들기 위한 JSON 스크립트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="02b0d-170">**계정 이름**을 Azure 저장소 계정 이름으로 변경하고 **계정 키**를 Azure 저장소 계정의 액세스 키로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="02b0d-171">저장소 액세스 키를 가져오는 방법은 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)의 저장소 액세스 키 보기, 복사 및 생성 방법 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="02b0d-172">명령 모음에서 **배포** 를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![배포 단추](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="02b0d-174">연결된 서비스를 성공적으로 배포한 후에 **Draft-1** 창은 사라지고 왼쪽의 트리 보기에 **AzureStorageLinkedService**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![메뉴의 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="02b0d-176">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="02b0d-177">이 단계에서는 데이터 팩터리에 주문형 HDInsight 클러스터를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="02b0d-178">HDInsight 클러스터는 런타임 시 자동으로 만들어지며 처리가 완료되고 지정된 시간 동안 유휴 상태를 유지한 후에 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="02b0d-179">**데이터 팩터리 편집기**의 명령 모음에서 **... 추가**를 클릭하고 **새 계산**을 클릭하고 **주문형 HDInsight 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![새 계산](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="02b0d-181">다음 코드 조각을 복사하여 **Draft-1** 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="02b0d-182">JSON 코드 조각은 주문형 HDInsight 클러스터를 만드는데 사용될 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="02b0d-183">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="02b0d-184">속성</span><span class="sxs-lookup"><span data-stu-id="02b0d-184">Property</span></span> | <span data-ttu-id="02b0d-185">설명</span><span class="sxs-lookup"><span data-stu-id="02b0d-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="02b0d-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="02b0d-186">ClusterSize</span></span> |<span data-ttu-id="02b0d-187">HDInsight 클러스터의 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="02b0d-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="02b0d-188">TimeToLive</span></span> | <span data-ttu-id="02b0d-189">HDInsight 클러스터가 삭제되기 전 유휴 시간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="02b0d-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="02b0d-190">linkedServiceName</span></span> | <span data-ttu-id="02b0d-191">HDInsight에 의해 생성되는 로그를 저장하는데 사용될 저장소 계정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="02b0d-192">다음 사항에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-192">Note the following points:</span></span>

   * <span data-ttu-id="02b0d-193">데이터 팩터리는 JSON으로 사용자에게 **Linux 기반** HDInsight 클러스터를 만들어 줍니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="02b0d-194">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="02b0d-195">주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="02b0d-196">자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="02b0d-197">HDInsight 클러스터는 JSON(**linkedServiceName**)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="02b0d-198">HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="02b0d-199">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-199">This behavior is by design.</span></span> <span data-ttu-id="02b0d-200">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="02b0d-201">클러스터는 처리가 완료되면 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="02b0d-202">많은 조각이 처리될수록 Azure Blob 저장소에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="02b0d-203">작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="02b0d-204">이 컨테이너의 이름은 "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp" 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="02b0d-205">[Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob 저장소에서 컨테이너를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="02b0d-206">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="02b0d-207">명령 모음에서 **배포** 를 클릭하여 연결된 서비스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![주문형 HDInsight 연결된 서비스 배포](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="02b0d-209">왼쪽의 트리 뷰에서 **AzureStorageLinkedService** 및 **HDInsightOnDemandLinkedService**가 모두 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="02b0d-211">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-211">Create datasets</span></span>
<span data-ttu-id="02b0d-212">이 단계에서는 Hive 처리에 대한 입력 및 출력 데이터를 나타내는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="02b0d-213">이러한 데이터 집합은 이 자습서의 앞부분에서 만든 **AzureStorageLinkedService** 를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="02b0d-214">연결된 서비스는 Azure 저장소 계정을 가리키고 데이터 집합은 입력 및 출력 데이터를 가진 저장소의 컨테이너, 폴더, 파일 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="02b0d-215">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-215">Create input dataset</span></span>
1. <span data-ttu-id="02b0d-216">**데이터 팩터리 편집기**의 명령 모음에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 **Azure Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![새 데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="02b0d-218">다음 코드 조각을 복사하여 Draft-1 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="02b0d-219">JSON 조각에서 파이프라인의 활동에 대한 입력 데이터를 나타내는 **AzureBlobInput** 라는 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="02b0d-220">또한 결과가 **adfgetstarted**라는 Blob 컨테이너 및 **inputdata**라는 폴더에 저장되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="02b0d-221">다음 테이블은 코드 조각에 사용된 JSON 속성에 대한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="02b0d-222">속성</span><span class="sxs-lookup"><span data-stu-id="02b0d-222">Property</span></span> | <span data-ttu-id="02b0d-223">설명</span><span class="sxs-lookup"><span data-stu-id="02b0d-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="02b0d-224">type</span><span class="sxs-lookup"><span data-stu-id="02b0d-224">type</span></span> |<span data-ttu-id="02b0d-225">Azure Blob 저장소에 데이터가 있기 때문에 type 속성은 **AzureBlob**으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="02b0d-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="02b0d-226">linkedServiceName</span></span> |<span data-ttu-id="02b0d-227">이전에 만든 **AzureStorageLinkedService**를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="02b0d-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="02b0d-228">folderPath</span></span> | <span data-ttu-id="02b0d-229">입력 Blob이 포함된 Blob **컨테이너**와 **폴더**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="02b0d-230">fileName</span><span class="sxs-lookup"><span data-stu-id="02b0d-230">fileName</span></span> |<span data-ttu-id="02b0d-231">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-231">This property is optional.</span></span> <span data-ttu-id="02b0d-232">이 속성을 생략하면 folderPath의 모든 파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="02b0d-233">이 자습서에서는 **input.log**만 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="02b0d-234">type</span><span class="sxs-lookup"><span data-stu-id="02b0d-234">type</span></span> |<span data-ttu-id="02b0d-235">로그 파일이 텍스트 형식이므로 **TextFormat**을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="02b0d-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="02b0d-236">columnDelimiter</span></span> |<span data-ttu-id="02b0d-237">로그 파일의 열은 **쉼표(`,`)**로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="02b0d-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="02b0d-238">frequency/interval</span></span> |<span data-ttu-id="02b0d-239">**월** 및 간격을 설정한 빈도가 **1**인 경우 입력 조각은 매월 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="02b0d-240">external</span><span class="sxs-lookup"><span data-stu-id="02b0d-240">external</span></span> | <span data-ttu-id="02b0d-241">이 파이프라인에 의해 입력 데이터가 생성되지 않는 경우 이 속성은 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="02b0d-242">이 자습서에서는 이 파이프라인에 의해 input.log 파일이 생성되지 않으므로 이 속성을 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="02b0d-243">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="02b0d-244">명령 모음에서 **배포** 를 클릭하여 새로 만든 데이터 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="02b0d-245">왼쪽의 트리 보기에서 데이터 집합을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="02b0d-246">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-246">Create output dataset</span></span>
<span data-ttu-id="02b0d-247">Azure Blob 저장소에 저장된 출력 데이터를 나타내는 출력 데이터 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="02b0d-248">**데이터 팩터리 편집기**의 명령 모음에서 **... 추가**를 클릭하고 **새 데이터 집합**을 클릭하고 **Azure Blob Storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="02b0d-249">다음 코드 조각을 복사하여 Draft-1 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="02b0d-250">JSON 코드 조각에서 **AzureBlobOutput**이라는 데이터 집합을 만들고 Hive 스크립트에 의해 생성될 데이터의 구조를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="02b0d-251">또한 결과가 **adfgetstarted**라는 Blob 컨테이너와 **partitioneddata**라는 폴더에 저장되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="02b0d-252">**가용성** 섹션은 출력 데이터 집합이 월 단위로 생성되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
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
    <span data-ttu-id="02b0d-253">이러한 속성에 대한 설명은 **입력 데이터 집합 만들기** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="02b0d-254">데이터 팩터리 서비스에서 데이터 집합이 생성되므로 출력 데이터 집합에 외부 속성을 설정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="02b0d-255">명령 모음에서 **배포** 를 클릭하여 새로 만든 데이터 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="02b0d-256">데이터 집합이 성공적으로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-256">Verify that the dataset is created successfully.</span></span>

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="02b0d-258">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="02b0d-258">Create pipeline</span></span>
<span data-ttu-id="02b0d-259">이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="02b0d-260">입력 조각이 매월(빈도: 월, 간격: 1)이고 출력 조각이 매월 생성되며 작업에 대한 스케줄러 속성도 매월로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="02b0d-261">출력 데이터 집합 및 작업 스케줄러에 대한 설정이 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="02b0d-262">현재 출력 데이터 집합이 일정을 결정하므로 작업이 출력을 생성하지 않는 경우 출력 데이터 집합을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="02b0d-263">활동이 입력을 가져오지 않으면 입력 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="02b0d-264">다음 JSON에서 사용되는 속성은 이 섹션의 끝에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="02b0d-265">**데이터 팩터리 편집기**에서 **줄임표(…) 추가 명령**을 클릭하고 **새 파이프라인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![새 파이프라인 단추](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="02b0d-267">다음 코드 조각을 복사하여 Draft-1 창에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="02b0d-268">**storageaccountname** 을 JSON의 저장소 계정 이름으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
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
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="02b0d-269">JSON 코드 조각에서 Hive를 사용하여 HDInsight 클러스터에서 데이터를 처리하는 단일 작업으로 구성되는 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="02b0d-270">Hive 스크립트 파일 **partitionweblogs.hql**은 Azure Storage 계정(**AzureStorageLinkedService**라고 하는 scriptLinkedService에 의해 지정됨)과 **adfgetstarted** 컨테이너에 있는 **스크립트** 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="02b0d-271">**defines** 섹션은 Hive 스크립트에 Hive 구성 값(예: ${hiveconf:inputtable}, ${hiveconf:partitionedtable})으로 전달되는 런타임 설정을 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="02b0d-272">파이프라인의 **start** 및 **end** 속성은 파이프라인의 활성 기간을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="02b0d-273">작업 JSON에서 **linkedServiceName** – **HDInsightOnDemandLinkedService**에서 지정한 계산에 대해 Hive 스크립트가 실행되도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="02b0d-274">예제에서 사용되는 JSON 속성에 대한 자세한 내용은 [Azure Data Factory의 파이프라인 및 활동](data-factory-create-pipelines.md)에서 “파이프라인 JSON”을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="02b0d-275">다음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-275">Confirm the following:</span></span>

   1. <span data-ttu-id="02b0d-276">**input.log** 파일은 Azure Blob Storage에서 **adfgetstarted** 컨테이너의 **inputdata** 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="02b0d-277">**partitionweblogs.hql** 파일은 Azure Blob Storage에서 **adfgetstarted** 컨테이너의 **스크립트** 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="02b0d-278">파일이 표시되지 않는 경우 [자습서 개요](data-factory-build-your-first-pipeline.md) 에서 필수 단계를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="02b0d-279">**storageaccountname** 을 파이프라인 JSON의 저장소 계정 이름으로 변경했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="02b0d-280">명령 모음에서 **배포** 를 클릭하여 파이프라인을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="02b0d-281">**시작** 및 **종료** 시간이 과거에 설정되고 **isPaused**가 false로 설정되었기 때문에 파이프라인(파이프라인의 활동)은 실행을 배포한 후에 즉시 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="02b0d-282">트리 뷰에 파이프라인이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![파이프라인과 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="02b0d-284">축하합니다. 첫 번째 파이프라인 만들기가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="02b0d-285">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="02b0d-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="02b0d-286">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="02b0d-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="02b0d-287">**X**를 클릭하여 Data Factory 편집기 블레이드를 닫고 Data Factory 블레이드로 돌아가서 **다이어그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="02b0d-289">다이어그램 보기에 파이프라인의 개요와 이 자습서에 사용된 데이터 집합이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="02b0d-291">파이프라인의 모든 작업을 보려면 다이어그램에서 파이프라인을 마우스 오른쪽 단추로 클릭하고 파이프라인 열기를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="02b0d-293">파이프라인에서 HDInsightHive 활동이 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="02b0d-295">이전 보기를 탐색하려면 맨 위에서 breadcrumb 메뉴의 **데이터 팩터리** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="02b0d-296">**다이어그램 보기**에서 **AzureBlobInput** 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="02b0d-297">조각이 **준비** 상태인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="02b0d-298">조각이 준비 상태로 표시되려면 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="02b0d-299">잠시 대기한 후에 표시되지 않는 경우 오른쪽 컨테이너(adfgetstarted) 및 폴더(inputdata)에 배치된 입력 파일(input.log)이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="02b0d-301">**X**를 닫아서 **AzureBlobInput** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="02b0d-302">**다이어그램 보기**에서 **AzureBlobOutput** 데이터 집합을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="02b0d-303">현재 처리 중인 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-303">You see that the slice that is currently being processed.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="02b0d-305">처리가 완료되면 **준비** 상태인 조각이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="02b0d-307">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="02b0d-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="02b0d-308">따라서 파이프라인이 조각을 처리하는 데 **약 30분**이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="02b0d-309">조각이 **준비** 상태에 있으면 출력 데이터에 대한 Blob Storage의 **adfgetstarted** 컨테이너에 있는 **partitioneddata** 폴더를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="02b0d-311">자세한 내용을 보려면 **데이터 조각** 블레이드에서 조각을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="02b0d-313">**작업 실행 목록**에서 작업 실행을 클릭하여 **작업 실행 세부 정보** 창에서 작업 실행에 대한 세부 정보를 봅니다(이 시나리오에서 Hive 작업).</span><span class="sxs-lookup"><span data-stu-id="02b0d-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="02b0d-315">로그 파일에서 실행되는 Hive 쿼리 및 상태 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="02b0d-316">이러한 로그는 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="02b0d-317">자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02b0d-318">조각이 성공적으로 처리될 때 입력된 파일이 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="02b0d-319">따라서 조각을 다시 실행하거나 자습서를 다시 수행하려는 경우 adfgetstarted 컨테이너의 inputdata 폴더에 입력 파일(input.log)을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="02b0d-320">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="02b0d-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="02b0d-321">응용 프로그램 모니터링 및 관리를 사용하여 파이프라인을 모니터링할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="02b0d-322">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="02b0d-323">데이터 팩터리의 홈페이지에서 **모니터링 및 관리** 타일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="02b0d-325">**응용 프로그램 모니터링 및 관리**가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="02b0d-326">**시작 시간** 및 **종료 시간**을 파이프라인 시작 시간 및 종료 시간에 맞게 변경하고 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="02b0d-328">자세한 내용을 보려면 **작업 창** 목록에서 작업 창을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="02b0d-330">요약</span><span class="sxs-lookup"><span data-stu-id="02b0d-330">Summary</span></span>
<span data-ttu-id="02b0d-331">이 자습서에서는 HDInsight hadoop 클러스터에서 Hive 스크립트를 실행하여 데이터를 처리하는 데 Azure 데이터 팩터리를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="02b0d-332">Azure 포털에서 다음 단계를 수행하기 위해 데이터 팩터리 편집기를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="02b0d-333">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="02b0d-334">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="02b0d-335">**Azure 저장소** 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="02b0d-336">**Azure HDInsight** 주문형 연결된 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="02b0d-337">Azure 데이터 팩터리는 입력 데이터를 처리하고 출력 데이터를 생성하기 위해 적시에 HDInsight Hadoop 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="02b0d-338">파이프라인에서 HDInsight Hive 작업에 대한 입력 및 출력 데이터를 설명하는 두 개의 **데이터 집합**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="02b0d-339">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02b0d-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02b0d-340">Next Steps</span></span>
<span data-ttu-id="02b0d-341">이 문서에서 파이프라인과 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="02b0d-342">복사 작업을 사용하여 Azure Blob에서 Azure SQL로 데이터를 복사하는 방법은 [자습서: Azure Blob에서 Azure SQL로 데이터 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02b0d-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="02b0d-343">참고 항목</span><span class="sxs-lookup"><span data-stu-id="02b0d-343">See Also</span></span>
| <span data-ttu-id="02b0d-344">항목</span><span class="sxs-lookup"><span data-stu-id="02b0d-344">Topic</span></span> | <span data-ttu-id="02b0d-345">설명</span><span class="sxs-lookup"><span data-stu-id="02b0d-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="02b0d-346">파이프라인</span><span class="sxs-lookup"><span data-stu-id="02b0d-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="02b0d-347">이 문서는 Azure Data Factory의 파이프라인 및 시나리오 또는 비즈니스를 위한 활동과 종단 간 데이터 기반 워크플로 활용하는 방법을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="02b0d-348">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="02b0d-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="02b0d-349">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="02b0d-350">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="02b0d-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="02b0d-351">이 문서에서는 Azure Data Factory 응용 프로그램 모델의 예약 및 실행에 대한 내용을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="02b0d-352">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="02b0d-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="02b0d-353">이 문서는 모니터링 및 관리 앱을 사용하여 파이프라인을 모니터링하고 관리하고 디버그하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02b0d-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
