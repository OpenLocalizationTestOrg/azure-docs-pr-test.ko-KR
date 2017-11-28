---
title: "aaaBuild 첫 번째 데이터 팩터리 (Azure 포털) | Microsoft Docs"
description: "이 자습서에서는 데이터 팩터리 편집기를 사용 하 여 hello Azure 포털에서에서 샘플 Azure 데이터 팩터리 파이프라인을 만듭니다."
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
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="c4b51-103">자습서: Azure Portal을 사용하여 첫 번째 Azure Data Factory 빌드</span><span class="sxs-lookup"><span data-stu-id="c4b51-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c4b51-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="c4b51-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="c4b51-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="c4b51-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="c4b51-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4b51-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="c4b51-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c4b51-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="c4b51-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="c4b51-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="c4b51-109">REST API</span><span class="sxs-lookup"><span data-stu-id="c4b51-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="c4b51-110">이 문서에서는 설명 어떻게 toouse [Azure 포털](https://portal.azure.com/) toocreate 첫 번째 Azure 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="c4b51-111">다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="c4b51-112">이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="c4b51-113">이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="c4b51-114">hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="c4b51-115">이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="c4b51-116">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="c4b51-117">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="c4b51-118">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="c4b51-119">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4b51-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c4b51-120">Prerequisites</span></span>
1. <span data-ttu-id="c4b51-121">자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="c4b51-122">이 문서는 hello Azure 데이터 팩터리 서비스에 대 한 개념적인 개요를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="c4b51-123">통과 하는 것이 좋습니다 [소개 tooAzure Data Factory](data-factory-introduction.md) hello 서비스의 문서에 대 한 자세한 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="c4b51-124">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-124">Create data factory</span></span>
<span data-ttu-id="c4b51-125">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="c4b51-126">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="c4b51-127">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 데이터 tooproduct 출력 데이터를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="c4b51-128">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="c4b51-129">Toohello 로그인 [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c4b51-130">클릭 **새로** hello 왼쪽된 메뉴에서 클릭 **데이터 + 분석**, 클릭 하 고 **Data Factory**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![블레이드 만들기](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="c4b51-132">Hello에 **새 데이터 팩터리** 블레이드에서 입력 **GetStartedDF** hello 이름에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![새 데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="c4b51-134">hello Azure 데이터 팩터리에 hello 이름은 해야 **전역적으로 고유**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="c4b51-135">Hello 오류가 나타나면: **"GetStartedDF" 데이터 팩터리 이름을 사용할 수 없으면**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="c4b51-136">Hello hello 데이터 팩터리의 이름입니다 (예를 들어 yournameGetStartedDF)을 변경 하 고 다시 만들어 보십시오.</span><span class="sxs-lookup"><span data-stu-id="c4b51-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="c4b51-137">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="c4b51-138">hello 데이터 팩터리의 hello 이름으로 등록 될 수는 **DNS** hello 미래에 이름을 지정 하 고 따라서 공개적으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="c4b51-139">선택 hello **Azure 구독** hello 데이터 팩터리 toobe 만든 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="c4b51-140">기존 **리소스 그룹** 을 선택하거나 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="c4b51-141">Hello 자습서에 대 한 명명 된 리소스 그룹 만들기: **ADFGetStartedRG**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="c4b51-142">선택 hello **위치** hello 데이터 팩토리에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="c4b51-143">Hello 데이터 팩터리 서비스에서 지 원하는 영역 으로만 hello 드롭 다운 목록에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="c4b51-144">선택 **Pin toodashboard**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="c4b51-145">클릭 **만들기** hello에 **새 데이터 팩터리** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4b51-146">toocreate 데이터 팩터리 인스턴스 hello의 구성원 이어야 [데이터 팩터리 참가자](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello 구독/리소스 그룹 수준에서 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="c4b51-147">표시 상태와 함께 바둑판식으로 배열 하는 hello 다음 hello 대시보드에서: 데이터 팩터리를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![데이터 팩터리 만들기 상태](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="c4b51-149">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-149">Congratulations!</span></span> <span data-ttu-id="c4b51-150">첫 번째 데이터 팩터리 만들기가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="c4b51-151">보여 주는 hello 데이터 팩터리 페이지를 참조 하는 hello 데이터 팩터리에서 만들어진 후에 성공적으로, hello 데이터 팩터리의 내용을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![데이터 팩터리 블레이드](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="c4b51-153">Hello 데이터 팩터리에 파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="c4b51-154">연결 된 서비스 toolink 저장소/계산 tooyour 데이터 저장의 입력 정의 및 연결 된 데이터 저장소의 데이터 집합 toorepresent 입/출력 데이터를 출력 하 고 데이터 다음 이러한 데이터 집합을 사용 하는 작업으로 hello 파이프라인을 만들 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="c4b51-155">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-155">Create linked services</span></span>
<span data-ttu-id="c4b51-156">이 단계에서는 Azure 저장소 계정 및 주문형 Azure HDInsight 클러스터 tooyour 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c4b51-157">안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="c4b51-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="c4b51-158">hello HDInsight 연결 된 서비스에 사용 되는 toorun hello 파이프라인이 샘플에서의 hello 활동에 지정 된 Hive 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="c4b51-159">식별할 [데이터 저장소](data-factory-data-movement-activities.md)/[계산 서비스](data-factory-compute-linked-services.md) 시나리오에 사용 되 고 해당 서비스 toohello 데이터 팩터리에 연결 된 서비스를 만들어 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="c4b51-160">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="c4b51-161">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="c4b51-162">이 자습서를 사용 하 여 hello 스크립트 파일을 toostore 입/출력 데이터와 hello hql로 변환 하는 동일한 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="c4b51-163">클릭 **작성자 및 배포** hello에 **DATA FACTORY** 블레이드 **GetStartedDF**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="c4b51-164">데이터 팩터리 편집기 hello를 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-164">You should see hello Data Factory Editor.</span></span>

   ![작성 및 배포 타일](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="c4b51-166">**새 데이터 저장소**를 클릭하고 **Azure storage**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![새 데이터 저장소 - Azure Storage - 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="c4b51-168">표시 되어야 hello Azure 저장소를 만들기 위한 JSON 스크립트 hello 편집기에서 서비스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="c4b51-170">대체 **계정 이름** hello Azure 저장소 계정 이름으로 및 **계정 키** hello Azure 저장소 계정 액세스 키가 hello 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="c4b51-171">toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="c4b51-172">클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![배포 단추](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="c4b51-174">Hello 연결 된 서비스를 배포한 후 성공적으로 hello **Draft 1** 창 사라져야 나타나고 **AzureStorageLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![메뉴의 저장소 연결된 서비스](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="c4b51-176">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="c4b51-177">이 단계에서는 주문형 HDInsight 클러스터 tooyour 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="c4b51-178">hello HDInsight 클러스터는 자동으로 런타임 시 만들어지고 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="c4b51-179">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 추가**를 클릭하고 **새 계산**을 클릭하고 **주문형 HDInsight 클러스터**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![새 계산](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="c4b51-181">복사 및 붙여넣기 다음 코드 조각 toohello hello **Draft 1** 창.</span><span class="sxs-lookup"><span data-stu-id="c4b51-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="c4b51-182">hello JSON 코드 조각은 hello 속성 사용 되는 toocreate hello 요청 시 HDInsight 클러스터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="c4b51-183">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="c4b51-184">속성</span><span class="sxs-lookup"><span data-stu-id="c4b51-184">Property</span></span> | <span data-ttu-id="c4b51-185">설명</span><span class="sxs-lookup"><span data-stu-id="c4b51-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4b51-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="c4b51-186">ClusterSize</span></span> |<span data-ttu-id="c4b51-187">Hello HDInsight 클러스터의 hello 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="c4b51-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="c4b51-188">TimeToLive</span></span> | <span data-ttu-id="c4b51-189">삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="c4b51-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4b51-190">linkedServiceName</span></span> | <span data-ttu-id="c4b51-191">HDInsight에서 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="c4b51-192">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="c4b51-192">Note hello following points:</span></span>

   * <span data-ttu-id="c4b51-193">hello 데이터 팩터리가 **Linux 기반** JSON hello로 있습니다에 대 한 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="c4b51-194">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="c4b51-195">주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4b51-196">자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="c4b51-197">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="c4b51-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="c4b51-198">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="c4b51-199">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-199">This behavior is by design.</span></span> <span data-ttu-id="c4b51-200">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="c4b51-201">hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="c4b51-202">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="c4b51-203">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="c4b51-204">이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="c4b51-205">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="c4b51-206">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="c4b51-207">클릭 **배포** hello 명령 toodeploy hello 연결 된 서비스 모음에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![주문형 HDInsight 연결된 서비스 배포](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="c4b51-209">둘 다에 표시 되는지 확인 **AzureStorageLinkedService** 및 **HDInsightOnDemandLinkedService** hello 왼쪽 hello 트리 뷰에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="c4b51-211">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-211">Create datasets</span></span>
<span data-ttu-id="c4b51-212">이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="c4b51-213">이러한 데이터 집합 참조 toohello **AzureStorageLinkedService** 이 자습서의 앞부분에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="c4b51-214">Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="c4b51-215">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-215">Create input dataset</span></span>
1. <span data-ttu-id="c4b51-216">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![새 데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="c4b51-218">복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="c4b51-219">라는 데이터 집합 hello JSON 조각에 만드는 **AzureBlobInput** hello 파이프라인의 활동에 대 한 입력된 데이터를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="c4b51-220">Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **inputdata**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="c4b51-221">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="c4b51-222">속성</span><span class="sxs-lookup"><span data-stu-id="c4b51-222">Property</span></span> | <span data-ttu-id="c4b51-223">설명</span><span class="sxs-lookup"><span data-stu-id="c4b51-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="c4b51-224">type</span><span class="sxs-lookup"><span data-stu-id="c4b51-224">type</span></span> |<span data-ttu-id="c4b51-225">hello type 속성이 너무 설정 되어**AzureBlob** 데이터는 Azure blob 저장소에 있기 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="c4b51-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="c4b51-226">linkedServiceName</span></span> |<span data-ttu-id="c4b51-227">Toohello 참조 **AzureStorageLinkedService** 앞에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="c4b51-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="c4b51-228">folderPath</span></span> | <span data-ttu-id="c4b51-229">Hello blob 지정 **컨테이너** 및 hello **폴더** 입력된 blob이 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="c4b51-230">fileName</span><span class="sxs-lookup"><span data-stu-id="c4b51-230">fileName</span></span> |<span data-ttu-id="c4b51-231">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-231">This property is optional.</span></span> <span data-ttu-id="c4b51-232">이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="c4b51-233">이 자습서에서는 hello **input.log** 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="c4b51-234">type</span><span class="sxs-lookup"><span data-stu-id="c4b51-234">type</span></span> |<span data-ttu-id="c4b51-235">사용 하도록 hello 로그 파일은 텍스트 형식으로 **TextFormat**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="c4b51-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="c4b51-236">columnDelimiter</span></span> |<span data-ttu-id="c4b51-237">hello 로그 파일의 열으로 구분 됩니다 **쉼표 문자 (`,`)**</span><span class="sxs-lookup"><span data-stu-id="c4b51-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="c4b51-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="c4b51-238">frequency/interval</span></span> |<span data-ttu-id="c4b51-239">빈도 설정 너무**월** 간격은 및 **1**, 해당 hello를 의미 하는 분할 영역은 매월 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="c4b51-240">external</span><span class="sxs-lookup"><span data-stu-id="c4b51-240">external</span></span> | <span data-ttu-id="c4b51-241">이 속성은 너무**true** 경우 입력된 데이터 hello이이 파이프라인에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="c4b51-242">이 자습서에서는 hello input.log 파일을 만들지이 파이프라인에서 설정 하 여 hello 속성 tootrue 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="c4b51-243">이러한 JSON 속성에 대한 자세한 내용은 [Azure Blob 커넥터 문서](data-factory-azure-blob-connector.md#dataset-properties)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="c4b51-244">클릭 **배포** hello 명령 모음 toodeploy hello 새로 만든 데이터 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="c4b51-245">Hello 왼쪽의 트리 보기를 hello hello 데이터 집합이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="c4b51-246">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-246">Create output dataset</span></span>
<span data-ttu-id="c4b51-247">이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent hello 출력 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="c4b51-248">Hello에 **데이터 팩터리 편집기**, 클릭 **중... 더 많은** hello 명령 모음에서 **새 데이터 집합**를 선택 하 고 **Azure Blob 저장소**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="c4b51-249">복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="c4b51-250">라는 데이터 집합 hello JSON 조각에 만드는 **AzureBlobOutput**, hello hello 하이브 스크립트에 의해 생성 되는 hello 데이터 구조를 지정 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="c4b51-251">Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **partitioneddata**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="c4b51-252">hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="c4b51-253">참조 **hello 입력된 데이터 집합을 만들** 섹션 이러한 속성에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="c4b51-254">Hello dataset hello 데이터 팩터리 서비스에서 생성 된 것과 hello 외부 속성에는 출력 데이터 집합 설정 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="c4b51-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="c4b51-255">클릭 **배포** hello 명령 모음 toodeploy hello 새로 만든 데이터 집합에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="c4b51-256">데이터 집합의 hello 성공적으로 생성 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-256">Verify that hello dataset is created successfully.</span></span>

    ![연결된 서비스와 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="c4b51-258">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="c4b51-258">Create pipeline</span></span>
<span data-ttu-id="c4b51-259">이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="c4b51-260">입력된 조각이 매월 (빈도: 월, 간격: 1), 출력 조각이 매월, 생성 되 고 hello 활동에 대 한 hello 스케줄러 속성 toomonthly도 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="c4b51-261">hello 출력 데이터 집합 및 작업 스케줄러 hello에 대 한 hello 설정을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="c4b51-262">현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="c4b51-263">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="c4b51-264">다음 JSON hello에 사용 되는 hello 속성 hello 끝이 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="c4b51-265">Hello에 **데이터 팩터리 편집기**, 클릭 **줄임표 (...) 더 많은 명령이** 클릭 하 고 **새 파이프라인**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![새 파이프라인 단추](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="c4b51-267">복사한 hello 다음 코드 조각 toohello Draft 1 창에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c4b51-268">대체 **storageaccountname** hello hello JSON에서에서 저장소 계정의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="c4b51-269">Hello JSON 조각에는 HDInsight 클러스터에서 하이브 tooprocess 데이터를 사용 하는 단일 활동으로 구성 된 파이프라인을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="c4b51-270">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **AzureStorageLinkedService**), 및  **스크립트** hello 컨테이너에 폴더 **adfgetstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="c4b51-271">hello **정의** 섹션은 하이브 구성 값으로 toohello 하이브 스크립트에 전달 되는 사용 되는 toospecify hello 런타임 설정 (예: ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="c4b51-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="c4b51-272">hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="c4b51-273">Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c4b51-274">"파이프라인 JSON"을 참조 [파이프라인 및 활동 Azure Data Factory에](data-factory-create-pipelines.md) hello 예제에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="c4b51-275">Hello 다음을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="c4b51-276">**input.log** hello에 파일이 **inputdata** hello의 폴더 **adfgetstarted** hello Azure blob 저장소의에서 컨테이너</span><span class="sxs-lookup"><span data-stu-id="c4b51-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="c4b51-277">**partitionweblogs.hql** hello에 파일이 **스크립트** hello의 폴더 **adfgetstarted** hello Azure blob 저장소의에서 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="c4b51-278">Hello에서 단계를 완료 hello prerequisite [자습서 개요](data-factory-build-your-first-pipeline.md) 이러한 파일에 표시 되지 않으면 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="c4b51-279">대체 했는지 확인 **storageaccountname** hello hello에서 저장소 계정의 이름으로 JSON을 파이프라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="c4b51-280">클릭 **배포** hello 명령 모음 toodeploy hello 파이프라인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="c4b51-281">Hello 이후 **시작** 및 **끝** 시간이 지난 hello에 설정 된 및 **isPaused** 배포한 후에 즉시 집합 toofalse, hello 파이프라인 (hello 파이프라인의 활동)을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="c4b51-282">Hello 파이프라인 hello 트리 보기에 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![파이프라인과 트리 뷰](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="c4b51-284">축하합니다. 첫 번째 파이프라인 만들기가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="c4b51-285">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c4b51-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="c4b51-286">다이어그램 보기를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c4b51-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="c4b51-287">클릭 **X** tooclose 데이터 팩터리 편집기 블레이드를 toonavigate toohello Data Factory 블레이드를 다시 마우스 클릭 **다이어그램**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![다이어그램 타일](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="c4b51-289">다이어그램 보기 hello에 hello 파이프라인 및이 자습서에 사용 되는 데이터 집합에 대해 간략하게를 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![다이어그램 뷰](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="c4b51-291">tooview hello 파이프라인에서 마우스 오른쪽 단추로 클릭 파이프라인 hello에 모든 활동 다이어그램 및 열기 파이프라인을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![파이프라인 열기 메뉴](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="c4b51-293">Hello 파이프라인의 hello HDInsightHive 활동 표시 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![파이프라인 보기 열기](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="c4b51-295">toonavigate toohello 이전 뷰를 다시 클릭 **Data factory** hello 위쪽 hello 이동 경로 탐색 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="c4b51-296">Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobInput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="c4b51-297">해당 hello 조각이에 속하는지 확인 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="c4b51-298">준비 상태가 몇 hello 조각 tooshow 분이 걸릴 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="c4b51-299">잠시을 대기한 후에 발생 하지 않습니다, 경우 hello 오른쪽 컨테이너 (adfgetstarted) 및 폴더 (inputdata)에 배치 입력된 hello 파일 (input.log) 되었는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![준비 상태인 입력 조각](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="c4b51-301">클릭 **X** tooclose **AzureBlobInput** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="c4b51-302">Hello에 **다이어그램 보기**, hello 데이터 집합을 두 번 클릭 **AzureBlobOutput**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="c4b51-303">현재 처리 중인 해당 hello 조각이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-303">You see that hello slice that is currently being processed.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="c4b51-305">Hello 조각 참조 처리가 완료 되 면 **준비** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![데이터 집합](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="c4b51-307">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="c4b51-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="c4b51-308">따라서 hello 파이프라인 될 너무 걸릴 **약 30 분** tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="c4b51-309">Hello 조각화 된 경우 **준비** 상태, hello 확인 **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="c4b51-311">에 대 한 hello 조각 toosee 세부 정보 클릭는 **데이터 조각을** 블레이드입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![데이터 조각 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="c4b51-313">Hello에서 실행할 활동을 클릭 **활동 실행 목록** 안에 (시나리오에서 하이브 활동)을 실행 하는 활동에 대 한 toosee 세부 정보는 **활동 실행 정보** 창.</span><span class="sxs-lookup"><span data-stu-id="c4b51-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![작업 실행 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="c4b51-315">Hello 로그 파일에서 실행 된 hello 하이브 쿼리 및 상태 정보를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="c4b51-316">이러한 로그는 문제를 해결하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="c4b51-317">자세한 내용은 [Azure 포털 블레이드를 사용하여 파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4b51-318">입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="c4b51-319">따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="c4b51-320">앱 모니터링 및 관리를 사용하여 파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="c4b51-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="c4b51-321">모니터를 사용 하 여 & toomonitor 응용 프로그램 파이프라인을 관리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="c4b51-322">이 응용 프로그램을 사용하는 방법에 대한 자세한 내용은 [앱 모니터링 및 관리를 사용하여 Azure Data Factory 파이프라인 모니터링 및 관리](data-factory-monitor-manage-app.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c4b51-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="c4b51-323">클릭 **모니터링 및 관리** 데이터 팩토리에 대 한 hello 홈 페이지에 바둑판식으로 배열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![타일 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="c4b51-325">**응용 프로그램 모니터링 및 관리**가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="c4b51-326">변경 hello **시작 시간** 및 **종료 시간** toomatch 시작 및 종료 시간 프로그램 파이프라인을 하 고 클릭 **적용**합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![앱 모니터링 및 관리](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="c4b51-328">Hello에 활동을 선택 **활동 창** toosee 세부 정보를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![활동 창 세부 정보](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="c4b51-330">요약</span><span class="sxs-lookup"><span data-stu-id="c4b51-330">Summary</span></span>
<span data-ttu-id="c4b51-331">이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="c4b51-332">데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="c4b51-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="c4b51-333">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="c4b51-334">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="c4b51-335">**Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="c4b51-336">**Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="c4b51-337">Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="c4b51-338">두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="c4b51-339">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4b51-340">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c4b51-340">Next Steps</span></span>
<span data-ttu-id="c4b51-341">이 문서에서 파이프라인과 주문형 HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="c4b51-342">toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c4b51-343">참고 항목</span><span class="sxs-lookup"><span data-stu-id="c4b51-343">See Also</span></span>
| <span data-ttu-id="c4b51-344">항목</span><span class="sxs-lookup"><span data-stu-id="c4b51-344">Topic</span></span> | <span data-ttu-id="c4b51-345">설명</span><span class="sxs-lookup"><span data-stu-id="c4b51-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="c4b51-346">파이프라인</span><span class="sxs-lookup"><span data-stu-id="c4b51-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="c4b51-347">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="c4b51-348">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="c4b51-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="c4b51-349">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="c4b51-350">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="c4b51-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="c4b51-351">이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="c4b51-352">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="c4b51-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="c4b51-353">이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="c4b51-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
