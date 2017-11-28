---
title: "aaaBuild 첫 번째 데이터 팩터리 (PowerShell) | Microsoft Docs"
description: "이 자습서에서는 Azure PowerShell을 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="95f6e-103">자습서: Azure PowerShell을 사용하여 첫 번째 Azure Data Factory 빌드</span><span class="sxs-lookup"><span data-stu-id="95f6e-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95f6e-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="95f6e-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="95f6e-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="95f6e-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="95f6e-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="95f6e-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="95f6e-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="95f6e-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="95f6e-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="95f6e-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="95f6e-109">REST API</span><span class="sxs-lookup"><span data-stu-id="95f6e-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="95f6e-110">이 문서에서는 Azure PowerShell toocreate 첫 번째 Azure 데이터 팩터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="95f6e-111">다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="95f6e-112">이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="95f6e-113">이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="95f6e-114">hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="95f6e-115">이 자습서에서는 hello 데이터 파이프라인 입력된 데이터 tooproduce 출력 데이터를 변환합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="95f6e-116">원본 데이터 저장소 tooa 대상 데이터 저장소에서 데이터를 복사 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="95f6e-117">방법에 대 한 자습서에 대 한 Azure 데이터 팩터리를 사용 하 여 toocopy 데이터 참조 [자습서: Blob 저장소 tooSQL 데이터베이스에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="95f6e-118">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="95f6e-119">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="95f6e-120">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95f6e-121">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95f6e-121">Prerequisites</span></span>
* <span data-ttu-id="95f6e-122">자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="95f6e-123">지침에 따라 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview) 문서 tooinstall에 최신 버전의 Azure PowerShell 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="95f6e-124">(선택 사항) 이 문서는 모든 hello 데이터 팩터리 cmdlet을 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="95f6e-125">데이터 팩터리 cmdlet에 대한 포괄적인 설명서는 [데이터 팩터리 Cmdlet 참조](/powershell/module/azurerm.datafactories) (영문)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="95f6e-126">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-126">Create data factory</span></span>
<span data-ttu-id="95f6e-127">이 단계를 사용 하 여 Azure PowerShell toocreate 라는 Azure 데이터 팩터리 **FirstDataFactoryPSH**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="95f6e-128">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="95f6e-129">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="95f6e-130">예를 들어 원본 tooa 대상 데이터 저장소와 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform에서 복사 작업 toocopy 데이터 입력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="95f6e-131">이 단계에서는 hello 데이터 팩터리를 만드는 것부터 시작 하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="95f6e-132">Azure PowerShell을 시작 하 고 hello 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="95f6e-133">이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="95f6e-134">닫았다가, 해야 toorun 이러한 명령을 다시.</span><span class="sxs-lookup"><span data-stu-id="95f6e-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="95f6e-135">Hello 다음 명령을 실행 하 고 hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="95f6e-136">이 계정에 대 한 모든 hello 구독 hello 명령 tooview 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="95f6e-137">다음 명령 tooselect hello 피드에 있는 toowork hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="95f6e-138">이 구독은 hello hello Azure 포털에서에서 사용 된 것 처럼 동일한 hello 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="95f6e-139">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="95f6e-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="95f6e-140">이 자습서의 hello 단계 중 일부 ADFTutorialResourceGroup 라는 hello 리소스 그룹을 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="95f6e-141">Toouse 필요한 다른 리소스 그룹을 사용 하는 경우이 자습서에서는 ADFTutorialResourceGroup 대신 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="95f6e-142">Hello 실행 **새로 AzureRmDataFactory** 라는 데이터 팩터리를 만드는 cmdlet **FirstDataFactoryPSH**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="95f6e-143">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="95f6e-143">Note hello following points:</span></span>

* <span data-ttu-id="95f6e-144">Azure Data Factory hello의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="95f6e-145">Hello 오류가 나타나면 **"FirstDataFactoryPSH" 데이터 팩터리 이름을 사용할 수 없으면**, hello 이름 (예를 들어 yournameFirstDataFactoryPSH)를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="95f6e-146">이 자습서의 단계를 수행하는 동안 ADFTutorialFactoryPSH 대신 이 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="95f6e-147">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="95f6e-148">toocreate 데이터 팩터리 인스턴스 해야 toobe hello Azure 구독 참가자/관리자</span><span class="sxs-lookup"><span data-stu-id="95f6e-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="95f6e-149">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 따라서 공개적으로 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="95f6e-150">Hello 오류가 나타나면: "**이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="95f6e-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="95f6e-151">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="95f6e-152">데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="95f6e-153">Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="95f6e-154">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="95f6e-155">파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="95f6e-156">연결 된 서비스 toolink 저장소/계산 tooyour 데이터 저장의 입력 정의 및 연결 된 데이터 저장소의 데이터 집합 toorepresent 입/출력 데이터를 출력 하 고 데이터 다음 이러한 데이터 집합을 사용 하는 작업으로 hello 파이프라인을 만들 먼저 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="95f6e-157">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-157">Create linked services</span></span>
<span data-ttu-id="95f6e-158">이 단계에서는 Azure 저장소 계정 및 주문형 Azure HDInsight 클러스터 tooyour 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="95f6e-159">안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="95f6e-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="95f6e-160">hello HDInsight 연결 된 서비스에 사용 되는 toorun hello 파이프라인이 샘플에서의 hello 활동에 지정 된 Hive 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="95f6e-161">데이터를 식별 합니다. 저장소/계산 서비스 시나리오에 사용 되 고 해당 서비스 toohello 데이터 팩터리에 연결 된 서비스를 만들어 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="95f6e-162">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="95f6e-163">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="95f6e-164">Hello를 사용 하 여 스크립트 파일을 toostore 입/출력 데이터와 hello hql로 변환 하는 동일한 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="95f6e-165">콘텐츠를 수행 하는 hello로 StorageLinkedService.json hello C:\ADFGetStarted 폴더에는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="95f6e-166">이미 존재 하지 않는 경우 ADFGetStarted hello 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="95f6e-167">대체 **계정 이름** hello Azure 저장소 계정 이름으로 및 **계정 키** hello Azure 저장소 계정 액세스 키가 hello 인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="95f6e-168">toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="95f6e-169">Azure PowerShell에서 toohello ADFGetStarted 폴더를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="95f6e-170">Hello를 사용할 수 있습니다 **새로 AzureRmDataFactoryLinkedService** 연결된 된 서비스를 만드는 cmdlet.</span><span class="sxs-lookup"><span data-stu-id="95f6e-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="95f6e-171">이 cmdlet 및 기타 데이터 팩터리 cmdlet이이 자습서에서 사용 하 여 값이 필요 하면 toopass hello에 대 한 *ResourceGroupName* 및 *DataFactoryName* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="95f6e-172">사용할 수 있습니다 **Get AzureRmDataFactory** tooget는 **DataFactory** 개체를 입력 하지 않고도 hello 개체를 전달 *ResourceGroupName* 및  *DataFactoryName* cmdlet을 실행할 때마다 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="95f6e-173">실행된 hello 다음 명령은 hello의 tooassign hello 출력 **Get AzureRmDataFactory** cmdlet tooa **$df** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="95f6e-174">이제 hello 실행 **새로 AzureRmDataFactoryLinkedService** hello를 만드는 cmdlet에 연결 된 **StorageLinkedService** 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="95f6e-175">Hello를 실행 하지 않은 경우 **Get AzureRmDataFactory** cmdlet 및 할당 된 hello 출력 toohello **$df** 변수에 값이 있는 toospecify hello에 대 한 *ResourceGroupName*및 *DataFactoryName* 다음과 같이 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="95f6e-176">Toorun hello 있는 hello 자습서의 hello 가운데에 Azure PowerShell을 닫으면 **Get AzureRmDataFactory** cmdlet 다음에 Azure PowerShell toocomplete hello 자습서를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="95f6e-177">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="95f6e-178">이 단계에서는 주문형 HDInsight 클러스터 tooyour 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="95f6e-179">hello HDInsight 클러스터는 자동으로 런타임 시 만들어지고 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="95f6e-180">주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="95f6e-181">자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="95f6e-182">라는 JSON 파일을 만들어 **HDInsightOnDemandLinkedService**hello에.json **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="95f6e-183">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="95f6e-184">속성</span><span class="sxs-lookup"><span data-stu-id="95f6e-184">Property</span></span> | <span data-ttu-id="95f6e-185">설명</span><span class="sxs-lookup"><span data-stu-id="95f6e-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="95f6e-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="95f6e-186">ClusterSize</span></span> |<span data-ttu-id="95f6e-187">Hello HDInsight 클러스터의 hello 크기를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="95f6e-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="95f6e-188">TimeToLive</span></span> |<span data-ttu-id="95f6e-189">삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="95f6e-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="95f6e-190">linkedServiceName</span></span> |<span data-ttu-id="95f6e-191">HDInsight에서 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="95f6e-192">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="95f6e-192">Note hello following points:</span></span>

   * <span data-ttu-id="95f6e-193">hello 데이터 팩터리가 **Linux 기반** JSON hello로 있습니다에 대 한 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="95f6e-194">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="95f6e-195">주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="95f6e-196">자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="95f6e-197">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="95f6e-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="95f6e-198">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="95f6e-199">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-199">This behavior is by design.</span></span> <span data-ttu-id="95f6e-200">주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리할 때마다 HDInsight 클러스터가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="95f6e-201">hello 클러스터는 hello 처리가 완료 되 면 자동으로 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="95f6e-202">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="95f6e-203">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="95f6e-204">이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="95f6e-205">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="95f6e-206">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="95f6e-207">Hello 실행 **새로 AzureRmDataFactoryLinkedService** hello를 만드는 cmdlet에는 연결 된 서비스 HDInsightOnDemandLinkedService를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="95f6e-208">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-208">Create datasets</span></span>
<span data-ttu-id="95f6e-209">이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="95f6e-210">이러한 데이터 집합 참조 toohello **StorageLinkedService** 이 자습서의 앞부분에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="95f6e-211">Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="95f6e-212">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-212">Create input dataset</span></span>
1. <span data-ttu-id="95f6e-213">라는 JSON 파일을 만들어 **InputTable.json** hello에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="95f6e-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="95f6e-214">라는 데이터 집합을 정의 하는 hello JSON **AzureBlobInput**을 hello 파이프라인의 활동에 대 한 입력된 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="95f6e-215">Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **inputdata**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="95f6e-216">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="95f6e-217">속성</span><span class="sxs-lookup"><span data-stu-id="95f6e-217">Property</span></span> | <span data-ttu-id="95f6e-218">설명</span><span class="sxs-lookup"><span data-stu-id="95f6e-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="95f6e-219">type</span><span class="sxs-lookup"><span data-stu-id="95f6e-219">type</span></span> |<span data-ttu-id="95f6e-220">hello type 속성 데이터는 Azure blob 저장소에 있기 때문에 tooAzureBlob 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="95f6e-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="95f6e-221">linkedServiceName</span></span> |<span data-ttu-id="95f6e-222">이전에 만든 StorageLinkedService toohello를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="95f6e-223">fileName</span><span class="sxs-lookup"><span data-stu-id="95f6e-223">fileName</span></span> |<span data-ttu-id="95f6e-224">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-224">This property is optional.</span></span> <span data-ttu-id="95f6e-225">이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="95f6e-226">이 경우 hello input.log만 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="95f6e-227">type</span><span class="sxs-lookup"><span data-stu-id="95f6e-227">type</span></span> |<span data-ttu-id="95f6e-228">hello 로그 파일은 텍스트 형식으로 TextFormat를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="95f6e-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="95f6e-229">columnDelimiter</span></span> |<span data-ttu-id="95f6e-230">hello 로그 파일의 열 hello 쉼표 문자 (,)으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="95f6e-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="95f6e-231">frequency/interval</span></span> |<span data-ttu-id="95f6e-232">frequency tooMonth를 설정 하 고 간격은 1 매월 hello 입력된 조각이 사용할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="95f6e-233">external</span><span class="sxs-lookup"><span data-stu-id="95f6e-233">external</span></span> |<span data-ttu-id="95f6e-234">이 속성 tootrue 경우 입력된 데이터 hello hello 데이터 팩터리 서비스에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="95f6e-235">Hello 다음 Azure PowerShell toocreate hello Data Factory 데이터 집합의 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="95f6e-236">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-236">Create output dataset</span></span>
<span data-ttu-id="95f6e-237">이제, hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent hello 출력 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="95f6e-238">라는 JSON 파일을 만들어 **OutputTable.json** hello에 **C:\ADFGetStarted** 폴더 콘텐츠를 다음 hello로:</span><span class="sxs-lookup"><span data-stu-id="95f6e-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="95f6e-239">라는 데이터 집합을 정의 하는 hello JSON **AzureBlobOutput**을 hello 파이프라인의 활동에 대 한 출력 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="95f6e-240">Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **partitioneddata**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="95f6e-241">hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="95f6e-242">Hello 다음 Azure PowerShell toocreate hello Data Factory 데이터 집합의 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="95f6e-243">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="95f6e-243">Create pipeline</span></span>
<span data-ttu-id="95f6e-244">이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="95f6e-245">입력된 조각이 매월 (빈도: 월, 간격: 1), 출력 조각이 매월, 생성 되 고 hello 활동에 대 한 hello 스케줄러 속성 toomonthly도 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="95f6e-246">hello 출력 데이터 집합 및 작업 스케줄러 hello에 대 한 hello 설정을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="95f6e-247">현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="95f6e-248">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="95f6e-249">다음 JSON hello에 사용 되는 hello 속성 hello 끝이 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="95f6e-250">콘텐츠 다음 hello로 MyFirstPipelinePSH.json hello C:\ADFGetStarted 폴더에는 JSON 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="95f6e-251">대체 **storageaccountname** hello hello JSON에서에서 저장소 계정의 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="95f6e-252">Hello JSON 조각에는 HDInsight 클러스터에서 하이브 tooprocess 데이터를 사용 하는 단일 활동으로 구성 된 파이프라인을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="95f6e-253">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **StorageLinkedService**), 및 **스크립트**  hello 컨테이너에 폴더 **adfgetstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="95f6e-254">hello **정의** 섹션은 수 있는 사용 되는 toospecify hello 런타임 설정을 toohello 하이브 스크립트 하이브 구성 값으로 전달 (예: ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="95f6e-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="95f6e-255">hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="95f6e-256">Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="95f6e-257">"파이프라인 JSON"을 참조 [파이프라인 및 활동 Azure Data Factory에](data-factory-create-pipelines.md) hello 예제에 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="95f6e-258">Hello 표시 되는지 확인 **input.log** hello에 대 한 파일 **adfgetstarted/inputdata** hello Azure blob 저장소 및 실행된 hello 명령 toodeploy hello 파이프라인 뒤의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="95f6e-259">Hello 이후 **시작** 및 **끝** 시간이 지난 hello에 설정 된 및 **isPaused** 배포한 후에 즉시 집합 toofalse, hello 파이프라인 (hello 파이프라인의 활동)을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="95f6e-260">축하합니다. Azure PowerShell을 사용하여 첫 번째 파이프라인 만들기를 완료하였습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="95f6e-261">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="95f6e-261">Monitor pipeline</span></span>
<span data-ttu-id="95f6e-262">이 단계를 진행 되는 상황에서 Azure 데이터 팩터리에 Azure PowerShell toomonitor 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="95f6e-263">실행 **Get AzureRmDataFactory** hello 출력 tooa 할당 **$df** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="95f6e-264">실행 **Get AzureRmDataFactorySlice** hello의 모든 분할 영역에 대 한 세부 정보 tooget **EmpSQLTable**, hello 파이프라인의 hello 출력 테이블 변수인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="95f6e-265">해당 hello StartDateTime 여기에서 지정 하는 hello 동일한 시작 hello 파이프라인 JSON에 지정 된 시간을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="95f6e-266">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-266">Here is hello sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="95f6e-267">실행 **Get AzureRmDataFactoryRun** tooget hello 활동 세부 정보를 특정 조각에 대 한 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="95f6e-268">다음은 hello 샘플 출력이입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-268">Here is hello sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="95f6e-269">있습니다 수 계속이 cmdlet을 실행 hello 분할 영역에 표시 될 때까지 **준비** 상태 또는 **실패** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="95f6e-270">Hello 조각 준비 상태에 있으면 확인 hello **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="95f6e-271">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![출력 데이터](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="95f6e-273">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="95f6e-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="95f6e-274">따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="95f6e-275">입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="95f6e-276">따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="95f6e-277">요약</span><span class="sxs-lookup"><span data-stu-id="95f6e-277">Summary</span></span>
<span data-ttu-id="95f6e-278">이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="95f6e-279">데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="95f6e-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="95f6e-280">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="95f6e-281">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="95f6e-282">**Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="95f6e-283">**Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="95f6e-284">Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="95f6e-285">두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="95f6e-286">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95f6e-287">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95f6e-287">Next steps</span></span>
<span data-ttu-id="95f6e-288">이 문서에서 파이프라인과 주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="95f6e-289">toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="95f6e-290">참고 항목</span><span class="sxs-lookup"><span data-stu-id="95f6e-290">See Also</span></span>
| <span data-ttu-id="95f6e-291">항목</span><span class="sxs-lookup"><span data-stu-id="95f6e-291">Topic</span></span> | <span data-ttu-id="95f6e-292">설명</span><span class="sxs-lookup"><span data-stu-id="95f6e-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="95f6e-293">데이터 팩터리 cmdlet 참조</span><span class="sxs-lookup"><span data-stu-id="95f6e-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="95f6e-294">데이터 팩터리 cmdlet에서 포괄적인 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95f6e-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="95f6e-295">파이프라인</span><span class="sxs-lookup"><span data-stu-id="95f6e-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="95f6e-296">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="95f6e-297">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="95f6e-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="95f6e-298">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="95f6e-299">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="95f6e-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="95f6e-300">이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="95f6e-301">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="95f6e-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="95f6e-302">이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="95f6e-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
