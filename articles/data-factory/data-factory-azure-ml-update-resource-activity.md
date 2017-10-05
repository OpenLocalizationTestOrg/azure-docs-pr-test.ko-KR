---
title: "Azure Data Factory를 사용하여 Machine Learning 모델 업데이트 | Microsoft Docs"
description: "Azure Data Factory 및 Azure 기계 학습을 사용하여 예측 파이프라인을 만드는 방법을 설명합니다."
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
ms.openlocfilehash: e31a7a59d14de4382190b39bd70f3ddf6cf673ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="712f5-103">업데이트 리소스 작업을 사용하여 Azure Machine Learning 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="712f5-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="712f5-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="712f5-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="712f5-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="712f5-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="712f5-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="712f5-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="712f5-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="712f5-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="712f5-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="712f5-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="712f5-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="712f5-114">이 문서는 주요 Azure Data Factory - Azure Machine Learning 통합 문서인 [Azure Machine Learning 및 Azure Data Factory를 사용하여 예측 파이프라인 만들기](data-factory-azure-ml-batch-execution-activity.md)를 보완합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="712f5-115">수행하지 않았다면 이 문서를 읽기 전에 기본 문서를 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="712f5-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="712f5-116">개요</span><span class="sxs-lookup"><span data-stu-id="712f5-116">Overview</span></span>
<span data-ttu-id="712f5-117">시간이 지남에 따라 Azure ML 점수 매기기 실험의 예측 모델은 새 입력 데이터 집합을 사용하여 다시 학습되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="712f5-118">재학습으로 완료한 후에는 재학습한 ML 모델로 점수 매기기 웹 서비스를 업데이트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="712f5-119">웹 서비스를 통해 Azure ML 모델을 재학습하고 업데이트하는 일반적인 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="712f5-120">[Azure 기계 학습 스튜디오](https://studio.azureml.net)에서 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="712f5-121">모델에 만족하면 Azure ML Studio를 사용하여 **학습 실험** 및 점수 매기기/**예측 실험** 모두에 대해 웹 서비스를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="712f5-122">다음 표에서는 이 예제에 사용된 웹 서비스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="712f5-123">자세한 내용은 [프로그래밍 방식으로 기계 학습 모델 다시 학습](../machine-learning/machine-learning-retrain-models-programmatically.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="712f5-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="712f5-124">**학습 웹 서비스** - 학습 데이터를 수신하고 학습된 모델을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="712f5-125">재학습의 출력은 Azure Blob 저장소에서 .ilearner 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="712f5-126">웹 서비스로 학습 실험을 게시할 때 사용자에 대한 **기본 끝점** 이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="712f5-127">더 많은 끝점을 만들 수 있지만 예제에서는 기본 끝점만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="712f5-128">**점수 매기기 웹 서비스** - 레이블이 지정되지 않은 데이터 예제를 수신하고 예측을 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="712f5-129">예측의 출력은 실험의 구성에 따라 .csv 파일 또는 Azure SQL 데이터베이스의 행과 같은 다양한 형태를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="712f5-130">웹 서비스로 예측 실험을 게시할 때 사용자에 대한 기본 끝점이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="712f5-131">다음 그림에서는 Azure ML에서 학습 및 점수 매기기 끝점 간의 관계를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![웹 서비스](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="712f5-133">**Azure ML Batch 실행 작업**을 사용하여 **학습 웹 서비스**를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="712f5-134">학습 웹 서비스를 호출하는 것은 점수 매기기 데이터에 대해 Azure ML 웹 서비스(점수 매기기 웹 서비스)를 호출하는 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="712f5-135">이전 섹션에서는 Azure Data Factory 파이프라인에서 Azure ML 웹 서비스를 호출하는 방법에 대해 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="712f5-136">**scoring web service** 을 사용하여 두 번째 **Azure ML 업데이트 리소스 작업** 을 사용하여 새로 학습된 모델로 웹 서비스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="712f5-137">다음 예제에서는 연결된 서비스 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="712f5-138">웹 서비스 점수 매기기는 클래식 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="712f5-139">웹 서비스 점수 매기기가 **클래식 웹 서비스**인 경우 [Azure Portal](https://manage.windowsazure.com)을 사용하여 두 번째 **기본이 아닌 업데이트 가능한 끝점**을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="712f5-140">이에 대한 단계는 [끝점 만들기](../machine-learning/machine-learning-create-endpoint.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="712f5-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="712f5-141">기본이 아닌 업데이트 가능한 끝점을 만든 후 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="712f5-142">**배치 실행**을 클릭하여 **mlEndpoint** JSON 속성에 대한 URI 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="712f5-143">**업데이트 리소스** 링크를 클릭하여 **updateResourceEndpoint** JSON 속성에 대한 URI 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="712f5-144">API 키는 끝점 페이지 자체의 오른쪽 하단에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![업데이트 가능한 끝점](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="712f5-146">다음 예제에서는 AzureML 연결된 서비스에 샘플 JSON 정의를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="712f5-147">연결된 서비스는 인증을 위해 apiKey를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-147">The linked service uses the apiKey for authentication.</span></span>  

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

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="712f5-148">웹 서비스 점수 매기기는 Azure Resource Manager 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="712f5-149">웹 서비스가 Azure Resource Manager 끝점을 노출하는 새로운 유형의 웹 서비스인 경우 두 번째 **기본이 아닌** 끝점을 추가할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="712f5-150">연결된 서비스의 **updateResourceEndpoint**는 다음 형식을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="712f5-151">[Azure Machine Learning 웹 서비스 포털](https://services.azureml.net/)에서 웹 서비스를 쿼리할 때 URL에 대한 자리 표시자 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="712f5-152">새로운 유형의 업데이트 리소스 끝점에는 AAD(Azure Active Directory) 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="712f5-153">AzureML 연결된 서비스에서 **servicePrincipalId** 및 **servicePrincipalKey**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="712f5-154">[서비스 보안 주체 만들기 및 Azure 리소스를 관리하기 위한 권한 할당 방법](../azure-resource-manager/resource-group-create-service-principal-portal.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="712f5-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="712f5-155">샘플 AzureML 연결된 서비스 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
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

<span data-ttu-id="712f5-156">다음 시나리오는 보다 자세한 내용을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-156">The following scenario provides more details.</span></span> <span data-ttu-id="712f5-157">Azure Data Factory 파이프라인에서 Azure ML 모델을 재학습 및 업데이트하는 예제가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="712f5-158">시나리오: Azure ML 모델 재학습 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="712f5-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="712f5-159">이 섹션에서는 **Azure ML 배치 실행 작업** 을 사용하여 모델을 재학습하는 샘플 파이프라인을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="712f5-160">파이프라인은 또한 **Azure ML 업데이트 리소스 작업** 을 사용하여 점수 매기기 웹 서비스에서 모델을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="712f5-161">섹션에서는 또한 모든 연결된 서비스, 데이터 집합 및 파이프라인에 대한 JSON 코드 조각 예제도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="712f5-162">샘플 파이프라인의 다이어그램 보기는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="712f5-163">보다시피 Azure ML 배치 실행 작업은 학습 입력을 사용하여 학습 출력(iLearner 파일)을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="712f5-164">Azure ML 업데이트 리소스 작업이 이 학습 출력을 사용하여 점수 매기기 웹 서비스 끝점에서 모델을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="712f5-165">업데이트 리소스 작업은 출력을 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="712f5-166">placeholderBlob는 Azure 데이터 팩터리 서비스가 파이프라인을 실행하기 위해 필요로 하는 더미 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![파이프라인 다이어그램](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="712f5-168">Azure Blob 저장소 연결된 서비스:</span><span class="sxs-lookup"><span data-stu-id="712f5-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="712f5-169">Azure 저장소는 다음 데이터를 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="712f5-170">학습 데이터.</span><span class="sxs-lookup"><span data-stu-id="712f5-170">training data.</span></span> <span data-ttu-id="712f5-171">Azure ML 학습 웹 서비스에 대한 입력 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="712f5-172">iLearner 파일.</span><span class="sxs-lookup"><span data-stu-id="712f5-172">iLearner file.</span></span> <span data-ttu-id="712f5-173">Azure ML 학습 웹 서비스에서의 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="712f5-174">이 파일은 업데이트 리소스 작업에 대한 입력이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="712f5-175">연결된 서비스의 샘플 JSON 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-175">Here is the sample JSON definition of the linked service:</span></span>

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

### <a name="training-input-dataset"></a><span data-ttu-id="712f5-176">학습 입력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="712f5-176">Training input dataset:</span></span>
<span data-ttu-id="712f5-177">다음 데이터 집합은 Azure ML 학습 웹 서비스에 대한 입력 학습 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="712f5-178">Azure ML 배치 실행 작업은 이 데이터 집합을 입력으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

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

### <a name="training-output-dataset"></a><span data-ttu-id="712f5-179">학습 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="712f5-179">Training output dataset:</span></span>
<span data-ttu-id="712f5-180">다음 데이터 집합은 Azure ML 학습 웹 서비스에서 출력 iLearner 파일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="712f5-181">Azure ML 배치 실행 작업은 이 데이터 집합을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="712f5-182">이 데이터 집합은 Azure ML 업데이트 리소스 작업에 대한 입력이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="712f5-183">Azure ML 학습 끝점에 대한 연결된 서비스</span><span class="sxs-lookup"><span data-stu-id="712f5-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="712f5-184">다음 JSON 코드 조각은 학습 웹 서비스의 기본 끝점을 가리키는 Azure 기계 학습 연결된 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

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

<span data-ttu-id="712f5-185">**Azure ML Studio**에서 다음을 수행하여 **mlEndpoint** 및 **apiKey**에 대한 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="712f5-186">왼쪽 메뉴에서 **웹 서비스** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="712f5-187">웹 서비스 목록에서 **학습 웹 서비스** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="712f5-188">**API 키** 텍스트 상자 옆의 복사를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="712f5-189">클립보드의 키를 Data Factory JSON 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="712f5-190">**Azure ML studio**에서 **배치 실행** 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="712f5-191">**요청** 섹션에서 **요청 URI**를 복사하여 Data Factory JSON 편집기에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="712f5-192">Azure ML 업데이트 가능한 점수 매기기 끝점에 대한 연결된 서비스:</span><span class="sxs-lookup"><span data-stu-id="712f5-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="712f5-193">다음 JSON 코드 조각은 점수 매기기 웹 서비스의 기본이 아닌 업데이트 가능한 끝점을 가리키는 Azure 기계 학습 연결된 서비스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

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

### <a name="placeholder-output-dataset"></a><span data-ttu-id="712f5-194">자리 표시자 출력 데이터 집합:</span><span class="sxs-lookup"><span data-stu-id="712f5-194">Placeholder output dataset:</span></span>
<span data-ttu-id="712f5-195">Azure ML 업데이트 리소스 작업은 어떠한 출력도 생성하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="712f5-196">그러나 Azure Data Factory에서 파이프라인의 일정을 구동하려면 출력 데이터 집합이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="712f5-197">따라서 이 예에서는 더미/자리 표시자 데이터 집합을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="712f5-198">파이프라인</span><span class="sxs-lookup"><span data-stu-id="712f5-198">Pipeline</span></span>
<span data-ttu-id="712f5-199">파이프라인에는 **AzureMLBatchExecution** 및 **AzureMLUpdateResource**라는 두 활동이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="712f5-200">Azure ML 배치 실행 작업은 학습 데이터를 입력으로 사용하여 .iLearner 파일을 출력으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="712f5-201">이 작업은 입력 교육 데이터와 함께 학습 웹 서비스(웹 서비스로 노출된 학습 실험)를 호출하고 웹 서비스로부터 ilearner 파일을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="712f5-202">placeholderBlob는 Azure 데이터 팩터리 서비스가 파이프라인을 실행하기 위해 필요로 하는 더미 출력 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="712f5-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

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
