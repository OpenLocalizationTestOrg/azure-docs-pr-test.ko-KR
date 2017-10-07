---
title: "aaaBuild 첫 번째 데이터 팩터리 (REST) | Microsoft Docs"
description: "이 자습서에서는 데이터 팩터리 REST API를 사용하여 샘플 Azure Data Factory 파이프라인을 만듭니다."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 5d8e39bd598cca35f91d501bad74e8a8436f8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="af18c-103">자습서: 데이터 팩터리 REST API를 사용하여 첫 번째 Azure Data Factory 빌드</span><span class="sxs-lookup"><span data-stu-id="af18c-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="af18c-104">개요 및 필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="af18c-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="af18c-105">Azure 포털</span><span class="sxs-lookup"><span data-stu-id="af18c-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="af18c-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="af18c-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="af18c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af18c-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="af18c-108">Resource Manager 템플릿</span><span class="sxs-lookup"><span data-stu-id="af18c-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="af18c-109">REST API</span><span class="sxs-lookup"><span data-stu-id="af18c-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


<span data-ttu-id="af18c-110">이 문서에서는 데이터 팩터리 REST API toocreate 첫 번째 Azure 데이터 팩터리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-110">In this article, you use Data Factory REST API toocreate your first Azure data factory.</span></span> <span data-ttu-id="af18c-111">다른 도구/Sdk를 사용 하 여 toodo hello 자습서 hello 드롭 다운 목록에서 hello 옵션 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="af18c-112">이 자습서에서는 hello 파이프라인에는 하나의 활동: **HDInsight Hive 활동**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="af18c-113">이 활동 변환을 입력 데이터 tooproduce 출력 데이터는 Azure HDInsight 클러스터에서 하이브 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="af18c-114">hello 파이프라인은 예약 된 toorun은 hello 사이의 월 시작 및 종료 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span>

> [!NOTE]
> <span data-ttu-id="af18c-115">이 문서에서 모든 hello REST API를 다루지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-115">This article does not cover all hello REST API.</span></span> <span data-ttu-id="af18c-116">REST API에 대한 포괄적인 설명서는 [Data Factory REST API 참조](/rest/api/datafactory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-116">For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).</span></span>
> 
> <span data-ttu-id="af18c-117">파이프라인 하나에는 활동이 둘 이상 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="af18c-118">및 hello 입력 데이터 집합의 hello 다른 활동으로 한 활동의 hello 출력 데이터 집합을 설정 하 여 두 개의 활동 (활동 다음에 다른 실행)을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="af18c-119">자세한 내용은 [Data Factory에서 예약 및 실행](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="af18c-120">필수 조건</span><span class="sxs-lookup"><span data-stu-id="af18c-120">Prerequisites</span></span>
* <span data-ttu-id="af18c-121">자세히 읽고 [자습서 개요](data-factory-build-your-first-pipeline.md) 아티클과 전체 hello **필수** 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="af18c-122">컴퓨터에 [Curl](https://curl.haxx.se/dlwiz/) 을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-122">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="af18c-123">데이터 팩터리 REST 명령 toocreate와 hello CURL 도구를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-123">You use hello CURL tool with REST commands toocreate a data factory.</span></span>
* <span data-ttu-id="af18c-124">[이 문서](../azure-resource-manager/resource-group-create-service-principal-portal.md) 의 지침에 따라 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-124">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="af18c-125">Azure Active Directory에서 **ADFGetStartedApp** 이라는 웹 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-125">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="af18c-126">**클라이언트 ID** 및 **암호 키**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-126">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="af18c-127">**테넌트 ID**를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-127">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="af18c-128">Hello 할당 **ADFGetStartedApp** 응용 프로그램 toohello **데이터 팩터리 참가자** 역할입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-128">Assign hello **ADFGetStartedApp** application toohello **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="af18c-129">[Azure PowerShell](/powershell/azure/overview)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-129">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="af18c-130">시작 **PowerShell** 다음 명령이 실행된 하는 hello 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-130">Launch **PowerShell** and run hello following command.</span></span> <span data-ttu-id="af18c-131">이 자습서의 hello 끝날 때까지 Azure PowerShell를 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-131">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="af18c-132">닫고 다시 열 경우 toorun hello 명령을 다시 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-132">If you close and reopen, you need toorun hello commands again.</span></span>
  1. <span data-ttu-id="af18c-133">실행 **로그인 AzureRmAccount** hello 사용자 이름 및 toosign toohello Azure 포털에서에서 사용 하는 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-133">Run **Login-AzureRmAccount** and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
  2. <span data-ttu-id="af18c-134">실행 **Get AzureRmSubscription** tooview 모든 hello이 계정에 대 한 구독.</span><span class="sxs-lookup"><span data-stu-id="af18c-134">Run **Get-AzureRmSubscription** tooview all hello subscriptions for this account.</span></span>
  3. <span data-ttu-id="af18c-135">실행 **Get AzureRmSubscription-SubscriptionName NameOfAzureSubscription | 집합 AzureRmContext** 와 toowork 원하는 tooselect hello 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-135">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="af18c-136">대체 **NameOfAzureSubscription** hello 이름의 Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="af18c-136">Replace **NameOfAzureSubscription** with hello name of your Azure subscription.</span></span>
* <span data-ttu-id="af18c-137">라는 Azure 리소스 그룹 만들기 **ADFTutorialResourceGroup** hello 다음 hello PowerShell에서에서 명령을 실행 하 여:</span><span class="sxs-lookup"><span data-stu-id="af18c-137">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="af18c-138">이 자습서의 hello 단계 중 일부 ADFTutorialResourceGroup 라는 hello 리소스 그룹을 사용 하는 것을 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-138">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="af18c-139">다른 리소스 그룹을 사용 하는 경우이 자습서의 ADFTutorialResourceGroup 대신 리소스 그룹의 toouse hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-139">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="af18c-140">JSON 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-140">Create JSON definitions</span></span>
<span data-ttu-id="af18c-141">다음 JSON 파일 curl.exe 위치한 hello 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-141">Create following JSON files in hello folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="af18c-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="af18c-142">datafactory.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af18c-143">Tooprefix/접미사 ADFCopyTutorialDF toomake 수 있도록 이름은 전역적으로 고유 해야 하기 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-143">Name must be globally unique, so you may want tooprefix/suffix ADFCopyTutorialDF toomake it a unique name.</span></span>
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="af18c-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="af18c-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af18c-145">**accountname** 및 **accountkey**를 Azure Storage 계정의 이름 및 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-145">Replace **accountname** and **accountkey** with name and key of your Azure storage account.</span></span> <span data-ttu-id="af18c-146">toolearn tooget 저장소 액세스 키, 어떻게 tooview / 복사 / 재생성 저장소 액세스 키에 대 한 hello 정보를 볼 [저장소 계정 관리](../storage/common/storage-create-storage-account.md#manage-your-storage-account)합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-146">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
>
>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="af18c-147">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="af18c-147">hdinsightondemandlinkedservice.json</span></span>

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

<span data-ttu-id="af18c-148">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-148">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="af18c-149">속성</span><span class="sxs-lookup"><span data-stu-id="af18c-149">Property</span></span> | <span data-ttu-id="af18c-150">설명</span><span class="sxs-lookup"><span data-stu-id="af18c-150">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af18c-151">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="af18c-151">ClusterSize</span></span> |<span data-ttu-id="af18c-152">Hello HDInsight 클러스터의 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-152">Size of hello HDInsight cluster.</span></span> |
| <span data-ttu-id="af18c-153">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="af18c-153">TimeToLive</span></span> |<span data-ttu-id="af18c-154">삭제 하기 전에 hello HDInsight 클러스터에 대 한 해당 hello 유휴 시간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-154">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="af18c-155">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="af18c-155">linkedServiceName</span></span> |<span data-ttu-id="af18c-156">HDInsight에서 생성 되는 사용 되는 toostore hello 로그 hello 저장소 계정을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-156">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

<span data-ttu-id="af18c-157">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="af18c-157">Note hello following points:</span></span>

* <span data-ttu-id="af18c-158">hello 데이터 팩터리가 **Linux 기반** hello JSON 위에 있는 사용자에 대 한 HDInsight 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-158">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="af18c-159">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="af18c-160">주문형 HDInsight 클러스터를 사용하는 대신 **고유의 HDInsight 클러스터** 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="af18c-161">자세한 내용은 [HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="af18c-162">hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="af18c-162">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="af18c-163">HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-163">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="af18c-164">이 동작은 의도된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-164">This behavior is by design.</span></span> <span data-ttu-id="af18c-165">주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 기존 라이브 클러스터 없으면 조각이 처리 될 때마다 만들 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

    <span data-ttu-id="af18c-166">많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="af18c-167">Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-167">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="af18c-168">이러한 컨테이너의 hello 이름 패턴을 따르도록: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp"입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-168">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="af18c-169">와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="af18c-170">자세한 내용은 [주문형 HDInsight 연결된 서비스](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="af18c-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="af18c-171">inputdataset.json</span></span>

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

<span data-ttu-id="af18c-172">라는 데이터 집합을 정의 하는 hello JSON **AzureBlobInput**을 hello 파이프라인의 활동에 대 한 입력된 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-172">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="af18c-173">Hello 입력된 데이터는 라는 hello blob 컨테이너에 위치 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **inputdata**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-173">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

<span data-ttu-id="af18c-174">hello 다음 표에서 hello 조각에 사용 되는 hello JSON 속성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-174">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

| <span data-ttu-id="af18c-175">속성</span><span class="sxs-lookup"><span data-stu-id="af18c-175">Property</span></span> | <span data-ttu-id="af18c-176">설명</span><span class="sxs-lookup"><span data-stu-id="af18c-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af18c-177">type</span><span class="sxs-lookup"><span data-stu-id="af18c-177">type</span></span> |<span data-ttu-id="af18c-178">hello type 속성 데이터는 Azure blob 저장소에 있기 때문에 tooAzureBlob 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-178">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="af18c-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="af18c-179">linkedServiceName</span></span> |<span data-ttu-id="af18c-180">이전에 만든 StorageLinkedService toohello를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-180">refers toohello StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="af18c-181">fileName</span><span class="sxs-lookup"><span data-stu-id="af18c-181">fileName</span></span> |<span data-ttu-id="af18c-182">이 속성은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-182">This property is optional.</span></span> <span data-ttu-id="af18c-183">이 속성을 생략 하면 hello folderPath의 모든 hello 파일 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-183">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="af18c-184">이 경우 hello input.log만 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-184">In this case, only hello input.log is processed.</span></span> |
| <span data-ttu-id="af18c-185">type</span><span class="sxs-lookup"><span data-stu-id="af18c-185">type</span></span> |<span data-ttu-id="af18c-186">hello 로그 파일은 텍스트 형식으로 TextFormat를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-186">hello log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="af18c-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="af18c-187">columnDelimiter</span></span> |<span data-ttu-id="af18c-188">hello 로그 파일에 열 쉼표 문자 (,)으로 구분 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-188">columns in hello log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="af18c-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="af18c-189">frequency/interval</span></span> |<span data-ttu-id="af18c-190">frequency tooMonth를 설정 하 고 간격은 1 매월 hello 입력된 조각이 사용할 수 있음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-190">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
| <span data-ttu-id="af18c-191">external</span><span class="sxs-lookup"><span data-stu-id="af18c-191">external</span></span> |<span data-ttu-id="af18c-192">이 속성 tootrue 경우 입력된 데이터 hello hello 데이터 팩터리 서비스에서 생성 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-192">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="af18c-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="af18c-193">outputdataset.json</span></span>

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

<span data-ttu-id="af18c-194">라는 데이터 집합을 정의 하는 hello JSON **AzureBlobOutput**을 hello 파이프라인의 활동에 대 한 출력 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-194">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="af18c-195">Hello 결과 라는 hello blob 컨테이너에 저장 되도록 지정 또한 **adfgetstarted** 및 라고 하는 hello 폴더 **partitioneddata**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-195">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="af18c-196">hello **가용성** 섹션 월별로 hello 출력 데이터 집합의 생성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-196">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="af18c-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="af18c-197">pipeline.json</span></span>
> [!IMPORTANT]
> <span data-ttu-id="af18c-198">**storageaccountname** 을 Azure Storage 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-198">Replace **storageaccountname** with name of your Azure storage account.</span></span>
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }],
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="af18c-199">Hello JSON 조각에 HDInsight 클러스터에서 하이브 tooprocess 데이터를 사용 하는 단일 활동으로 구성 된 파이프라인을 만들게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-199">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess data on a HDInsight cluster.</span></span>

<span data-ttu-id="af18c-200">hello Hive 스크립트 파일 **partitionweblogs.hql**, hello Azure 저장소 계정에에서 저장 됩니다 (hello scriptLinkedService를 호출 하 여 지정 된 **StorageLinkedService**), 및 **스크립트**  hello 컨테이너에 폴더 **adfgetstarted**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-200">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

<span data-ttu-id="af18c-201">hello **정의** 섹션에서는 지정 된 Hive 구성 값으로 toohello 하이브 스크립트에 전달 되는 런타임 설정 (예: ${hiveconf: inputtable}, {hiveconf:partitionedtable} $).</span><span class="sxs-lookup"><span data-stu-id="af18c-201">hello **defines** section specifies runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="af18c-202">hello **시작** 및 **끝** hello 파이프라인의 속성 hello hello 파이프라인의 활성 기간을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-202">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

<span data-ttu-id="af18c-203">Hello 활동 JSON에서에서 hello로 지정 된 hello 계산에서 해당 hello 하이브 스크립트 실행 지정 **linkedServiceName** – **HDInsightOnDemandLinkedService**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-203">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> <span data-ttu-id="af18c-204">"파이프라인 JSON"을 참조 [파이프라인 및 활동 Azure Data Factory에](data-factory-create-pipelines.md) hello 앞 예제에에서 사용 되는 JSON 속성에 대 한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-204">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello preceding example.</span></span>
>
>

## <a name="set-global-variables"></a><span data-ttu-id="af18c-205">전역 변수 설정</span><span class="sxs-lookup"><span data-stu-id="af18c-205">Set global variables</span></span>
<span data-ttu-id="af18c-206">Azure PowerShell에서 명령을 직접 hello 값 바꾼 후 다음 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-206">In Azure PowerShell, execute hello following commands after replacing hello values with your own:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af18c-207">클라이언트 ID, 클라이언트 암호, 테넌트 ID 및 구독 ID를 가져오는 지침은 [필수 구성 요소](#prerequisites) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-207">See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.</span></span>
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="af18c-208">AAD로 인증</span><span class="sxs-lookup"><span data-stu-id="af18c-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="af18c-209">데이터 팩터리 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-209">Create data factory</span></span>
<span data-ttu-id="af18c-210">이 단계에서는 **FirstDataFactoryREST**라는 Azure Data Factory를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="af18c-211">데이터 팩터리에는 하나 이상의 파이프라인이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="af18c-212">파이프라인에는 하나 이상의 작업이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="af18c-213">예를 들어 한 복사 작업 toocopy 데이터 소스 tooa 대상 데이터 저장소 및 HDInsight Hive 활동 toorun 하이브 스크립트 tootransform 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-213">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform data.</span></span> <span data-ttu-id="af18c-214">Hello 명령을 toocreate hello 데이터 팩터리를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-214">Run hello following commands toocreate hello data factory:</span></span>

1. <span data-ttu-id="af18c-215">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-215">Assign hello command toovariable named **cmd**.</span></span>

    <span data-ttu-id="af18c-216">여기에서 지정한 일치 하는 항목 (ADFCopyTutorialDF) hello hello에 지정 된 이름이 hello 데이터 팩터리의 hello 이름이 하는지 확인 **datafactory.json**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-216">Confirm that hello name of hello data factory you specify here (ADFCopyTutorialDF) matches hello name specified in hello **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-217">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-217">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-218">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-218">View hello results.</span></span> <span data-ttu-id="af18c-219">Hello 데이터 팩토리에 hello에 대 한 JSON hello 참조 hello 데이터 팩터리 성공적으로 생성 된 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-219">If hello data factory has been successfully created, you see hello JSON for hello data factory in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="af18c-220">포인트 다음 참고 hello:</span><span class="sxs-lookup"><span data-stu-id="af18c-220">Note hello following points:</span></span>

* <span data-ttu-id="af18c-221">Azure Data Factory hello의 hello 이름 전역적으로 고유 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-221">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="af18c-222">결과에 hello 오류가 나타나는 경우: **"FirstDataFactoryREST" 데이터 팩터리 이름을 사용할 수 없으면**, 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-222">If you see hello error in results: **Data factory name “FirstDataFactoryREST” is not available**, do hello following steps:</span></span>
  1. <span data-ttu-id="af18c-223">Hello에 hello 이름 변경 (예를 들어 yournameFirstDataFactoryREST) **datafactory.json** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-223">Change hello name (for example, yournameFirstDataFactoryREST) in hello **datafactory.json** file.</span></span> <span data-ttu-id="af18c-224">데이터 팩터리 아티팩트에 대한 명명 규칙은 [데이터 팩터리 - 명명 규칙](data-factory-naming-rules.md) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="af18c-225">Hello 첫 번째 명령은에 있는 hello **$cmd** 변수 ְ ÷ ° × FirstDataFactoryREST hello 새 이름으로 바꾸고 hello 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-225">In hello first command where hello **$cmd** variable is assigned a value, replace FirstDataFactoryREST with hello new name and run hello command.</span></span>
  3. <span data-ttu-id="af18c-226">Hello 이후의 두 명령은 tooinvoke hello REST API toocreate hello 데이터 팩터리 및 인쇄 hello hello 작업 결과 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-226">Run hello next two commands tooinvoke hello REST API toocreate hello data factory and print hello results of hello operation.</span></span>
* <span data-ttu-id="af18c-227">toocreate 데이터 팩터리 인스턴스 해야 toobe hello Azure 구독 참가자/관리자</span><span class="sxs-lookup"><span data-stu-id="af18c-227">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="af18c-228">hello hello 데이터 팩터리의 이름입니다 hello 나중에 DNS 이름으로 등록 하 고 있으므로 공개 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-228">hello name of hello data factory may be registered as a DNS name in hello future and hence become publicly visible.</span></span>
* <span data-ttu-id="af18c-229">Hello 오류가 나타나면: "**이 구독이 지원 되지 않으면 등록 된 toouse 네임 스페이스 microsoft.datafactory가**" hello 다음 중 하나를 수행 하 고 다시 게시 하십시오.</span><span class="sxs-lookup"><span data-stu-id="af18c-229">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="af18c-230">Azure PowerShell에서 명령 tooregister hello 데이터 팩터리 공급자 hello를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-230">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="af18c-231">데이터 팩터리 공급자가 등록 되어 해당 hello 명령 tooconfirm 다음 hello를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-231">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="af18c-232">Hello에 Azure 구독을 hello 사용 하 여 로그인 [Azure 포털](https://portal.azure.com) tooa Data Factory 블레이드를 탐색 하 고 (또는) hello Azure 포털에서에서 데이터 팩터리를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-232">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="af18c-233">이 동작은 hello 공급자를 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-233">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="af18c-234">파이프라인을 만들기 전에 필요한 toocreate 몇 가지 Data Factory 엔터티에 먼저 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-234">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="af18c-235">먼저 연결 된 서비스 toolink 데이터 저장소/계산 tooyour 데이터 저장의 입력 정의 및 연결 된 데이터 저장소의 데이터 집합 toorepresent 데이터 출력을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-235">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="af18c-236">연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-236">Create linked services</span></span>
<span data-ttu-id="af18c-237">이 단계에서는 Azure 저장소 계정 및 주문형 Azure HDInsight 클러스터 tooyour 데이터 팩터리를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="af18c-238">안녕 보류 hello hello 파이프라인이 샘플에서에 대 한 입력 및 출력 데이터는 Azure 저장소 계정.</span><span class="sxs-lookup"><span data-stu-id="af18c-238">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="af18c-239">hello HDInsight 연결 된 서비스에 사용 되는 toorun hello 파이프라인이 샘플에서의 hello 활동에 지정 된 Hive 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-239">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="af18c-240">Azure 저장소 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="af18c-241">이 단계에서는 Azure 저장소 계정 tooyour 데이터 팩터리를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-241">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="af18c-242">이 자습서와 함께 hello를 사용 하면 스크립트 파일을 toostore 입/출력 데이터와 hello hql로 변환 하는 동일한 Azure 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-242">With this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="af18c-243">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-243">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-244">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-244">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-245">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-245">View hello results.</span></span> <span data-ttu-id="af18c-246">Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-246">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="af18c-247">Azure HDInsight 연결된 서비스 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="af18c-248">이 단계에서는 주문형 HDInsight 클러스터 tooyour 데이터 팩터리에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-248">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="af18c-249">hello HDInsight 클러스터는 자동으로 런타임 시 만들어지고 지정 된 시간 동안 hello에 대 한 처리 및 유휴을 완료 한 후 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-249">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="af18c-250">주문형 HDInsight 클러스터를 사용하는 대신 고유의 HDInsight 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="af18c-251">자세한 내용은 [연결된 서비스 계산](data-factory-compute-linked-services.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="af18c-252">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-252">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-253">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-253">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-254">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-254">View hello results.</span></span> <span data-ttu-id="af18c-255">Hello 연결 되어 있는 경우 서비스가 성공적으로 만들어졌습니다., hello에 연결 하는 hello 서비스에 대 한 JSON hello 참조 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-255">If hello linked service has been successfully created, you see hello JSON for hello linked service in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="af18c-256">데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-256">Create datasets</span></span>
<span data-ttu-id="af18c-257">이 단계에서는 toorepresent hello 입력 데이터 집합 만들기 및 하이브 처리에 대 한 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-257">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="af18c-258">이러한 데이터 집합 참조 toohello **StorageLinkedService** 이 자습서의 앞부분에서 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-258">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="af18c-259">Azure 저장소 계정을 연결 된 서비스 지점 tooan hello 및 데이터 집합 입력을 보유 하는 hello 저장소의 컨테이너, 폴더, 파일 이름 지정 및 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-259">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="af18c-260">입력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-260">Create input dataset</span></span>
<span data-ttu-id="af18c-261">이 단계에서는 hello 입력된 데이터 집합 toorepresent 입력된 데이터 hello Azure Blob 저장소에 저장 된 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-261">In this step, you create hello input dataset toorepresent input data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="af18c-262">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-262">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-263">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-263">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-264">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-264">View hello results.</span></span> <span data-ttu-id="af18c-265">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-265">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="af18c-266">출력 데이터 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-266">Create output dataset</span></span>
<span data-ttu-id="af18c-267">이 단계에서는 hello Azure Blob 저장소에에서 저장 된 hello 출력 데이터 집합 toorepresent 출력 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-267">In this step, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="af18c-268">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-268">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-269">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-269">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-270">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-270">View hello results.</span></span> <span data-ttu-id="af18c-271">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-271">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="af18c-272">파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="af18c-272">Create pipeline</span></span>
<span data-ttu-id="af18c-273">이 단계에서는 **HDInsightHive** 작업을 사용하여 첫 번째 파이프라인을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="af18c-274">입력된 조각이 매월 (빈도: 월, 간격: 1), 출력 조각이 매월, 생성 되 고 hello 활동에 대 한 hello 스케줄러 속성 toomonthly도 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="af18c-275">hello 출력 데이터 집합 및 작업 스케줄러 hello에 대 한 hello 설정을 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-275">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="af18c-276">현재 출력 데이터 집합 hello 활동 출력을 생성 하지 않는 경우에 출력 데이터 집합을 만들어야 하므로 어떤 드라이브 hello 일정입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-276">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="af18c-277">Hello 활동의 입력을 사용 하지 않습니다, hello 입력된 데이터 집합 만들기를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-277">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span>

<span data-ttu-id="af18c-278">Hello 표시 되는지 확인 **input.log** hello에 대 한 파일 **adfgetstarted/inputdata** hello Azure blob 저장소 및 실행된 hello 명령 toodeploy hello 파이프라인 뒤의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-278">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="af18c-279">Hello 이후 **시작** 및 **끝** 시간이 지난 hello에 설정 된 및 **isPaused** 배포한 후에 즉시 집합 toofalse, hello 파이프라인 (hello 파이프라인의 활동)을 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-279">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="af18c-280">명명 된 hello 명령 toovariable 할당 **cmd**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-280">Assign hello command toovariable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af18c-281">Hello 명령을 사용 하 여 실행 **Invoke-command**합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-281">Run hello command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af18c-282">Hello 결과 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-282">View hello results.</span></span> <span data-ttu-id="af18c-283">Hello에 hello 데이터 집합에 대 한 JSON hello 참조 hello 데이터 집합에서 성공적으로 만든 경우 **결과**, 그러지 않으면 오류 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-283">If hello dataset has been successfully created, you see hello JSON for hello dataset in hello **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="af18c-284">축하합니다. Azure PowerShell을 사용하여 첫 번째 파이프라인 만들기를 완료하였습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="af18c-285">파이프라인 모니터링</span><span class="sxs-lookup"><span data-stu-id="af18c-285">Monitor pipeline</span></span>
<span data-ttu-id="af18c-286">이 단계에서는 hello 파이프라인에 의해 생성 되는 데이터 팩터리 REST API toomonitor 분할 영역을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-286">In this step, you use Data Factory REST API toomonitor slices being produced by hello pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> <span data-ttu-id="af18c-287">주문형 HDInsight 클러스터 만들기는 일반적으로 시간이 소요됩니다.(대략 20분)</span><span class="sxs-lookup"><span data-stu-id="af18c-287">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="af18c-288">따라서 hello 파이프라인 tootake 될 **약 30 분** tooprocess hello 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-288">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
>

<span data-ttu-id="af18c-289">이 명령은 Invoke-command hello 및 실행 hello 다음 hello 분할 영역에 표시 될 때까지 **준비** 상태 또는 **실패** 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-289">Run hello Invoke-Command and hello next one until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="af18c-290">Hello 조각 준비 상태에 있으면 확인 hello **partitioneddata** 폴더 hello에 **adfgetstarted** hello에 대 한 blob 저장소에서 컨테이너 데이터를 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-290">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="af18c-291">주문형 HDInsight 클러스터의 hello 만들기에는 일반적으로 몇 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-291">hello creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![출력 데이터](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="af18c-293">입력된 파일 hello hello slice가 성공적으로 처리 될 때 삭제 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-293">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="af18c-294">따라서 toorerun hello 슬라이스를 싶거나 않는 다시 자습서 hello hello adfgetstarted 컨테이너의 hello 입력된 파일 (input.log) toohello inputdata 폴더를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-294">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

<span data-ttu-id="af18c-295">Azure 포털 toomonitor 분할 영역을 사용 하 고 문제를 해결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-295">You can also use Azure portal toomonitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="af18c-296">[Azure 포털을 사용하여 파이프라인 모니터링](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) 세부 정보를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="af18c-297">요약</span><span class="sxs-lookup"><span data-stu-id="af18c-297">Summary</span></span>
<span data-ttu-id="af18c-298">이 자습서에서는 Azure 데이터 팩터리 tooprocess 데이터 HDInsight hadoop 클러스터에서 하이브 스크립트를 실행 하 여 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-298">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="af18c-299">데이터 팩터리 편집기 단계를 수행 하는 hello Azure 포털 toodo hello에 hello을 사용 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="af18c-299">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="af18c-300">Azure **데이터 팩터리**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="af18c-301">두 개의 **연결된 서비스**를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="af18c-302">**Azure 저장소** 서비스 toolink 입/출력 파일 toohello 데이터 팩터리를 포함 하 여 Azure blob 저장소를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-302">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="af18c-303">**Azure HDInsight** 주문형 연결 된 서비스 toolink 주문형 HDInsight Hadoop 클러스터 toohello 데이터 팩터리입니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-303">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="af18c-304">Azure 데이터 팩터리를 만들고 HDInsight Hadoop 클러스터 적시에 tooprocess 입력된 데이터 생성 출력 데이터 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="af18c-305">두 개의 만든 **데이터 집합**는 hello 파이프라인에서 HDInsight Hive 활동에 대 한 입력 및 출력 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="af18c-306">**HDInsight Hive** 작업으로 **파이프라인**을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af18c-307">다음 단계</span><span class="sxs-lookup"><span data-stu-id="af18c-307">Next steps</span></span>
<span data-ttu-id="af18c-308">이 문서에서 파이프라인과 주문형 Azure HDInsight 클러스터에서 Hive 스크립트를 실행하는 변환 작업(HDInsight 작업)을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="af18c-309">toouse Azure Blob tooAzure SQL에서 복사 작업 toocopy 데이터를 확인 하려면 어떻게 toosee [자습서: Azure Blob tooAzure SQL에서에서 데이터를 복사](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-309">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="af18c-310">참고 항목</span><span class="sxs-lookup"><span data-stu-id="af18c-310">See Also</span></span>
| <span data-ttu-id="af18c-311">항목</span><span class="sxs-lookup"><span data-stu-id="af18c-311">Topic</span></span> | <span data-ttu-id="af18c-312">설명</span><span class="sxs-lookup"><span data-stu-id="af18c-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="af18c-313">데이터 팩터리 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="af18c-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="af18c-314">데이터 팩터리 cmdlet에서 포괄적인 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="af18c-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="af18c-315">파이프라인</span><span class="sxs-lookup"><span data-stu-id="af18c-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="af18c-316">이 문서에서는 파이프라인 및 Azure Data Factory에는 활동을 이해 하는 데 방법과 toouse 종단 간 데이터 기반 시나리오 또는 비즈니스에 대 한 워크플로 tooconstruct 하 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-316">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="af18c-317">데이터 집합</span><span class="sxs-lookup"><span data-stu-id="af18c-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="af18c-318">이 문서는 Azure Data Factory의 데이터 집합을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="af18c-319">예약 및 실행</span><span class="sxs-lookup"><span data-stu-id="af18c-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="af18c-320">이 문서는 Azure Data Factory 응용 프로그램 모델의 hello 예약 및 실행 측면을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-320">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="af18c-321">모니터링 앱을 사용하여 파이프라인 모니터링 및 관리</span><span class="sxs-lookup"><span data-stu-id="af18c-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="af18c-322">이 문서에서는 toomonitor를 관리 하 고 파이프라인을 디버깅 하는 방법을 설명 모니터링 및 관리 응용 프로그램 hello를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="af18c-322">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
