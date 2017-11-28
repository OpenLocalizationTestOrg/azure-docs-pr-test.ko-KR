---
title: "Azure 데이터 팩터리를 사용 하 여 aaaUpdate 기계 학습 모델 | Microsoft Docs"
description: "Toocreate Azure 데이터 팩터리 및 Azure 기계 학습을 사용 하 여 예측 파이프라인을 생성 하는 방법을 설명 합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="936c0-103">업데이트 리소스 작업을 사용하여 Azure Machine Learning 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="936c0-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="936c0-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="936c0-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="936c0-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="936c0-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="936c0-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="936c0-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="936c0-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="936c0-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="936c0-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="936c0-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="936c0-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="936c0-114">이 문서 보완 hello 주요 Azure 데이터 팩터리-Azure 기계 학습 통합 문서: [Azure 기계 학습 및 Azure 데이터 팩터리를 사용 하 여 예측 파이프라인 만들기](data-factory-azure-ml-batch-execution-activity.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-114">This article complements hello main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="936c0-115">그렇게 이미 하지 않은 경우이 문서 전체를 읽기 전에 hello 기본 문서를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-115">If you haven't already done so, review hello main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="936c0-116">개요</span><span class="sxs-lookup"><span data-stu-id="936c0-116">Overview</span></span>
<span data-ttu-id="936c0-117">시간이 지남에 따라 hello hello Azure 기계 학습 점수 매기기 실험에 예측 모델에 새 입력된 데이터 집합을 통해 유지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-117">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="936c0-118">재교육를 완료 한 후 웹 서비스 hello와 점수 매기기 tooupdate hello ML 모델을 다시 학습 되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-118">After you are done with retraining, you want tooupdate hello scoring web service with hello retrained ML model.</span></span> <span data-ttu-id="936c0-119">hello 일반적인 단계 tooenable 재교육 및 웹 서비스를 통해 Azure ML 모델을 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-119">hello typical steps tooenable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="936c0-120">[Azure 기계 학습 스튜디오](https://studio.azureml.net)에서 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="936c0-121">Hello 모델 만족 스 러 우면 두 hello에 대 한 Azure 기계 학습 스튜디오 toopublish 웹 서비스를 사용할 **학습 실험** 및 평가 /**예측 실험**합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-121">When you are satisfied with hello model, use Azure ML Studio toopublish web services for both hello **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="936c0-122">hello 다음 표에서 설명 hello 웹 서비스를이 예제에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-122">hello following table describes hello web services used in this example.</span></span>  <span data-ttu-id="936c0-123">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](../machine-learning/machine-learning-retrain-models-programmatically.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="936c0-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="936c0-124">**학습 웹 서비스** - 학습 데이터를 수신하고 학습된 모델을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="936c0-125">hello 재교육의 hello 출력은 Azure Blob 저장소에.ilearner 파일.</span><span class="sxs-lookup"><span data-stu-id="936c0-125">hello output of hello retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="936c0-126">hello **끝점 기본** hello 교육을 게시할 때 실험을 웹 서비스에 대해 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-126">hello **default endpoint** is automatically created for you when you publish hello training experiment as a web service.</span></span> <span data-ttu-id="936c0-127">더 많은 끝점을 만들 수 있지만 hello 기본 끝점을 사용 하 여 hello 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-127">You can create more endpoints but hello example uses only hello default endpoint.</span></span>
- <span data-ttu-id="936c0-128">**점수 매기기 웹 서비스** - 레이블이 지정되지 않은 데이터 예제를 수신하고 예측을 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="936c0-129">예측의 hello 출력.csv 파일 또는 hello 실험의 hello 구성에 따라, Azure SQL 데이터베이스의 행 같은 다양 한 형식을 가질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-129">hello output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on hello configuration of hello experiment.</span></span> <span data-ttu-id="936c0-130">hello 예측 실험을 웹 서비스로 게시 하는 경우 사용자에 대 한 hello 기본 끝점이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-130">hello default endpoint is automatically created for you when you publish hello predictive experiment as a web service.</span></span> 

<span data-ttu-id="936c0-131">hello 다음 그림 보여주고 hello 관계 학습 및 Azure 기계 학습에서 끝점을 평가 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-131">hello following picture depicts hello relationship between training and scoring endpoints in Azure ML.</span></span>

![웹 서비스](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="936c0-133">Hello를 호출할 수 있습니다 **학습 웹 서비스** hello를 사용 하 여 **Azure ML 일괄 처리 실행 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-133">You can invoke hello **training web service** by using hello **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="936c0-134">학습 웹 서비스를 호출하는 것은 점수 매기기 데이터에 대해 Azure ML 웹 서비스(점수 매기기 웹 서비스)를 호출하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="936c0-135">이전 섹션에서는 커버 tooinvoke Azure ML 웹 서비스를 사용 하 여 Azure Data Factory를 자세히 파이프라인 하는 방법을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-135">hello preceding sections cover how tooinvoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="936c0-136">Hello를 호출할 수 있습니다 **웹 서비스 점수 매기기** hello를 사용 하 여 **Azure ML 업데이트 리소스 작업** hello 새로 학습 된 모델 tooupdate hello 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-136">You can invoke hello **scoring web service** by using hello **Azure ML Update Resource Activity** tooupdate hello web service with hello newly trained model.</span></span> <span data-ttu-id="936c0-137">연결 된 서비스 정의 제공 하는 예제 따르는 hello:</span><span class="sxs-lookup"><span data-stu-id="936c0-137">hello following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="936c0-138">웹 서비스 점수 매기기는 클래식 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="936c0-139">웹 서비스를 평가 하는 hello는 경우는 **클래식 웹 서비스**, hello를 두 번째로 만들 **기본이 아닌 및 업데이트할 수 있는 끝점** hello를 사용 하 여 [Azure 포털](https://manage.windowsazure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-139">If hello scoring web service is a **classic web service**, create hello second **non-default and updatable endpoint** by using hello [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="936c0-140">이에 대한 단계는 [끝점 만들기](../machine-learning/machine-learning-create-endpoint.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="936c0-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="936c0-141">Hello 기본값이 아닌 업데이트할 수 있는 끝점을 만든 후 다음 단계 hello지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-141">After you create hello non-default updatable endpoint, do hello following steps:</span></span>

* <span data-ttu-id="936c0-142">클릭 **일괄 처리 실행** tooget hello URI hello에 대 한 값 **인해 mlEndpoint** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-142">Click **BATCH EXECUTION** tooget hello URI value for hello **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="936c0-143">클릭 **업데이트 리소스** 링크 hello에 대 한 tooget hello URI 값 **updateResourceEndpoint** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-143">Click **UPDATE RESOURCE** link tooget hello URI value for hello **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="936c0-144">hello API 키가 hello 끝점 페이지 자체에 (hello 오른쪽 아래 모서리)입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-144">hello API key is on hello endpoint page itself (in hello bottom-right corner).</span></span>

![업데이트 가능한 끝점](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="936c0-146">다음 예에서는 hello hello AzureML 연결 서비스에 대 한 샘플 JSON 정의 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-146">hello following example provides a sample JSON definition for hello AzureML linked service.</span></span> <span data-ttu-id="936c0-147">hello 연결 된 서비스 hello apiKey 인증에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-147">hello linked service uses hello apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="936c0-148">웹 서비스 점수 매기기는 Azure Resource Manager 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="936c0-149">Hello 웹 서비스는 hello 새로운 유형의 Azure 리소스 관리자 끝점을 노출 하는 웹 서비스를 하는 경우 불필요 tooadd hello 둘째 **기본이 아닌** 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-149">If hello web service is hello new type of web service that exposes an Azure Resource Manager endpoint, you do not need tooadd hello second **non-default** endpoint.</span></span> <span data-ttu-id="936c0-150">hello **updateResourceEndpoint** hello에 연결 된 서비스는 hello 형식:</span><span class="sxs-lookup"><span data-stu-id="936c0-150">hello **updateResourceEndpoint** in hello linked service is of hello format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="936c0-151">Hello에 hello 웹 서비스를 쿼리할 때 hello URL에 대 한 자리 표시자에 대 한 값을 가져올 수 [Azure 컴퓨터 학습 웹 서비스 포털](https://services.azureml.net/)합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-151">You can get values for place holders in hello URL when querying hello web service on hello [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="936c0-152">hello 새로운 유형의 업데이트 리소스 끝점에는 AAD (Azure Active Directory) 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-152">hello new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="936c0-153">AzureML 연결된 서비스에서 **servicePrincipalId** 및 **servicePrincipalKey**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="936c0-154">참조 [toocreate 서비스 보안 주체 하 고 사용 권한을 toomanage Azure 리소스를 할당 하는 방법을](../azure-resource-manager/resource-group-create-service-principal-portal.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-154">See [how toocreate service principal and assign permissions toomanage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="936c0-155">샘플 AzureML 연결된 서비스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="936c0-156">hello 다음과 같은 시나리오 자세한 세부 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-156">hello following scenario provides more details.</span></span> <span data-ttu-id="936c0-157">Azure Data Factory 파이프라인에서 Azure ML 모델을 재학습 및 업데이트하는 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="936c0-158">시나리오: Azure ML 모델 재학습 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="936c0-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="936c0-159">이 섹션에서는 hello를 사용 하는 샘플 파이프라인 **Azure ML 일괄 처리 실행 활동** tooretrain 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-159">This section provides a sample pipeline that uses hello **Azure ML Batch Execution activity** tooretrain a model.</span></span> <span data-ttu-id="936c0-160">또한 사용 하 여 hello hello 파이프라인 **Azure ML 업데이트 리소스 작업** 웹 서비스를 평가 하는 hello에서 tooupdate hello 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-160">hello pipeline also uses hello **Azure ML Update Resource activity** tooupdate hello model in hello scoring web service.</span></span> <span data-ttu-id="936c0-161">hello 섹션은 또한 모든 JSON 조각을 hello 연결 된 서비스, 데이터 집합 및 hello 예제에서 파이프라인을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-161">hello section also provides JSON snippets for all hello linked services, datasets, and pipeline in hello example.</span></span>

<span data-ttu-id="936c0-162">Hello 샘플 파이프라인의 hello 다이어그램 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-162">Here is hello diagram view of hello sample pipeline.</span></span> <span data-ttu-id="936c0-163">볼 수 있듯이 hello Azure ML 일괄 처리 실행 작업은 hello 학습 입력 하 고 학습 출력 (iLearner 파일)를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-163">As you can see, hello Azure ML Batch Execution Activity takes hello training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="936c0-164">Azure ML 업데이트 리소스 작업 hello이 교육 출력 걸리며 업데이트 hello 웹 서비스 끝점을 점수 매기기 hello에서 모델.</span><span class="sxs-lookup"><span data-stu-id="936c0-164">hello Azure ML Update Resource Activity takes this training output and updates hello model in hello scoring web service endpoint.</span></span> <span data-ttu-id="936c0-165">hello 업데이트 리소스 작업 출력을 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-165">hello Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="936c0-166">hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-166">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![파이프라인 다이어그램](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="936c0-168">Azure Blob 저장소 연결된 서비스:</span><span class="sxs-lookup"><span data-stu-id="936c0-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="936c0-169">Azure 저장소 hello 같은 데이터가 hello을 보유 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-169">hello Azure Storage holds hello following data:</span></span>

* <span data-ttu-id="936c0-170">학습 데이터.</span><span class="sxs-lookup"><span data-stu-id="936c0-170">training data.</span></span> <span data-ttu-id="936c0-171">hello hello Azure ML 학습 웹 서비스에 대 한 입력된 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-171">hello input data for hello Azure ML training web service.</span></span>  
* <span data-ttu-id="936c0-172">iLearner 파일.</span><span class="sxs-lookup"><span data-stu-id="936c0-172">iLearner file.</span></span> <span data-ttu-id="936c0-173">hello hello Azure ML 학습 웹 서비스에서 출력 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-173">hello output from hello Azure ML training web service.</span></span> <span data-ttu-id="936c0-174">이 파일 hello 입력된 toohello 업데이트 리소스 작업 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-174">This file is also hello input toohello Update Resource activity.</span></span>  

<span data-ttu-id="936c0-175">Hello 연결 된 서비스의 hello 샘플 JSON 정의 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-175">Here is hello sample JSON definition of hello linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="936c0-176">학습 입력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="936c0-176">Training input dataset:</span></span>
<span data-ttu-id="936c0-177">hello 다음 데이터 집합이 나타냅니다 hello Azure ML 학습 웹 서비스에 대 한 hello 입력된 학습 데이터를.</span><span class="sxs-lookup"><span data-stu-id="936c0-177">hello following dataset represents hello input training data for hello Azure ML training web service.</span></span> <span data-ttu-id="936c0-178">Azure ML 일괄 처리 실행 활동 hello이 데이터이 집합을 입력 변수로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-178">hello Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "policy": {          
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

### <a name="training-output-dataset"></a><span data-ttu-id="936c0-179">학습 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="936c0-179">Training output dataset:</span></span>
<span data-ttu-id="936c0-180">hello 다음 데이터 집합이 나타냅니다 hello 출력 iLearner 파일을 hello Azure ML 학습 웹 서비스에서.</span><span class="sxs-lookup"><span data-stu-id="936c0-180">hello following dataset represents hello output iLearner file from hello Azure ML training web service.</span></span> <span data-ttu-id="936c0-181">Azure ML 일괄 처리 실행 작업 hello이 데이터이 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-181">hello Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="936c0-182">이 데이터 집합 hello 입력된 toohello Azure ML 업데이트 리소스 작업 이기도합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-182">This dataset is also hello input toohello Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="936c0-183">Azure ML 학습 끝점에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="936c0-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="936c0-184">다음 JSON 코드 조각은 hello hello 학습 웹 서비스의 toohello 기본 끝점을 가리키는 Azure 기계 학습 연결 서비스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-184">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello default endpoint of hello training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="936c0-185">**Azure 기계 학습 스튜디오**, 다음 tooget 값에 대 한 hello 수행 **인해 mlEndpoint** 및 **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="936c0-185">In **Azure ML Studio**, do hello following tooget values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="936c0-186">클릭 **웹 서비스** hello 왼쪽된 메뉴에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-186">Click **WEB SERVICES** on hello left menu.</span></span>
2. <span data-ttu-id="936c0-187">Hello 클릭 **학습 웹 서비스** 의 웹 서비스는 hello 목록에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-187">Click hello **training web service** in hello list of web services.</span></span>
3. <span data-ttu-id="936c0-188">फ 복사 너무**API 키** 입력란.</span><span class="sxs-lookup"><span data-stu-id="936c0-188">Click copy next too**API key** text box.</span></span> <span data-ttu-id="936c0-189">Hello 클립보드의 hello 키를 hello 데이터 팩터리 JSON 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-189">Paste hello key in hello clipboard into hello Data Factory JSON editor.</span></span>
4. <span data-ttu-id="936c0-190">Hello에 **Azure 기계 학습 스튜디오**, 클릭 **일괄 처리 실행** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-190">In hello **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="936c0-191">복사 hello **요청 URI** hello에서 **요청** 섹션 및 hello 데이터 팩터리 JSON 편집기에 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-191">Copy hello **Request URI** from hello **Request** section and paste it into hello Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="936c0-192">Azure ML 업데이트 가능한 점수 매기기 끝점에 대한 연결된 서비스:</span><span class="sxs-lookup"><span data-stu-id="936c0-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="936c0-193">다음 JSON 코드 조각은 hello toohello 기본값이 아닌 업데이트할 수 있는 끝점의 웹 서비스를 평가 하는 hello 가리키는 Azure 기계 학습 연결 서비스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-193">hello following JSON snippet defines an Azure Machine Learning linked service that points toohello non-default updatable endpoint of hello scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="936c0-194">자리 표시자 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="936c0-194">Placeholder output dataset:</span></span>
<span data-ttu-id="936c0-195">hello Azure ML 업데이트 리소스 작업에는 어떠한 출력도 생성 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-195">hello Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="936c0-196">그러나 Azure 데이터 팩터리 파이프라인의 한 출력 데이터 집합 toodrive hello 일정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-196">However, Azure Data Factory requires an output dataset toodrive hello schedule of a pipeline.</span></span> <span data-ttu-id="936c0-197">따라서 이 예에서는 더미/자리 표시자 데이터 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="936c0-198">파이프라인</span><span class="sxs-lookup"><span data-stu-id="936c0-198">Pipeline</span></span>
<span data-ttu-id="936c0-199">hello 파이프라인에는 두 개의 활동: **AzureMLBatchExecution** 및 **AzureMLUpdateResource**합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-199">hello pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="936c0-200">hello Azure ML 일괄 처리 실행 작업 hello 학습 데이터를 입력으로 사용 하 고 출력으로 iLearner 파일을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-200">hello Azure ML Batch Execution activity takes hello training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="936c0-201">hello 활동 데이터를 학습 하는 hello 입력이 포함 된 hello 학습 웹 서비스 (학습 실험을 웹 서비스로 노출)을 호출 하 고 hello 웹 서비스에서 hello ilearner 파일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-201">hello activity invokes hello training web service (training experiment exposed as a web service) with hello input training data and receives hello ilearner file from hello webservice.</span></span> <span data-ttu-id="936c0-202">hello placeholderBlob hello Azure Data Factory 서비스 toorun hello 파이프라인에 필요한 더미 출력 데이터 집합 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="936c0-202">hello placeholderBlob is just a dummy output dataset that is required by hello Azure Data Factory service toorun hello pipeline.</span></span>

![파이프라인 다이어그램](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
