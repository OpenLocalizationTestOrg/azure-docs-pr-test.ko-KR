---
title: "Azure Data Factory를 사용하여 예측 데이터 파이프라인 만들기 | Microsoft Docs"
description: "Azure Data Factory 및 Azure 기계 학습을 사용하여 예측 파이프라인을 만드는 방법을 설명합니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d8e2c9583fc909e4e015e2d40473d2754529d8ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="ac5e9-103">Azure Machine Learning 및 Azure Data Factory를 사용하여 예측 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="ac5e9-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ac5e9-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="ac5e9-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ac5e9-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ac5e9-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ac5e9-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ac5e9-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ac5e9-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ac5e9-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ac5e9-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ac5e9-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="ac5e9-114">소개</span><span class="sxs-lookup"><span data-stu-id="ac5e9-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="ac5e9-115">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="ac5e9-115">Azure Machine Learning</span></span>
<span data-ttu-id="ac5e9-116">[Azure 기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/) 을 사용하여 예측 분석 솔루션을 빌드, 테스트 및 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="ac5e9-117">대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="ac5e9-118">**학습 실험 만들기**.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-118">**Create a training experiment**.</span></span> <span data-ttu-id="ac5e9-119">Azure ML Studio를 사용하여 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="ac5e9-120">ML Studio는 학습 데이터를 사용하여 예측 분석 모델을 학습하고 테스트하는 데 사용하는 시각적 공동 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="ac5e9-121">**예측 실험으로 변환**.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="ac5e9-122">기존 데이터로 모델을 학습시키고 새 데이터의 점수를 매기는 데 사용할 준비가 되면, 점수 매기기를 위해 실험을 준비하고 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="ac5e9-123">**웹 서비스로 배포**.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="ac5e9-124">점수 매기기 실험을 Azure 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="ac5e9-125">이 웹 서비스 끝점을 통해 데이터를 모델로 전송하고 모델로부터 결과 예측을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="ac5e9-126">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="ac5e9-126">Azure Data Factory</span></span>
<span data-ttu-id="ac5e9-127">Data Factory는 데이터의 **이동**과 **변환**을 조율하고 자동화하는 클라우드 기반의 데이터 통합 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="ac5e9-128">다양한 데이터 저장소에서 데이터를 수집하고 변환/처리하며 데이터 저장소에 결과 데이터를 게시할 수 있는 Azure Data Factory를 사용하여 데이터 통합 솔루션을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="ac5e9-129">Data Factory 서비스를 통해 데이터를 이동하고 변환하는 파이프라인을 실행한 다음 데이터 파이프라인을 지정된 일정(매시간, 매일, 매주 등)으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="ac5e9-130">또한 데이터 파이프라인 간의 종속성과 계보를 표시하는 다양한 시각화를 제공하며 문제를 쉽고 정확하게 파악하고 모니터링 경고를 설정하는 통합된 단일 보기에서 모든 데이터 파이프라인을 모니터링합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="ac5e9-131">[Azure Data Factory 소개](data-factory-introduction.md) 및 [첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 문서를 참조하여 Azure Data Factory 서비스를 빠르게 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="ac5e9-132">Data Factory 및 Machine Learning</span><span class="sxs-lookup"><span data-stu-id="ac5e9-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="ac5e9-133">Azure Data Factory를 사용하면 예측 분석을 위해 게시된 [Azure Machine Learning][azure-machine-learning] 웹 서비스를 사용하는 파이프라인을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="ac5e9-134">Azure 데이터 팩터리 파이프라인에서 **배치 실행 작업** 을 사용하여 Azure ML 웹 서비스를 호출하고 배치에 있는 데이터에 대한 예측을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="ac5e9-135">자세한 내용은 [배치 실행 작업을 사용하여 Azure ML 웹 서비스 호출](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="ac5e9-136">시간이 지남에 따라 Azure ML 점수 매기기 실험의 예측 모델은 새 입력 데이터 집합을 사용하여 다시 학습되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="ac5e9-137">다음 단계를 수행하여 데이터 팩터리 파이프라인에서 Azure ML 모델을 다시 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="ac5e9-138">웹 서비스로 학습 실험(예측 실험 아님)을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="ac5e9-139">이전 시나리오에서 웹 서비스로 예측 실험을 노출했으므로 Azure ML Studio에서 이 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="ac5e9-140">Azure ML 배치 실행 작업을 사용하여 학습 실험을 위한 웹 서비스를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="ac5e9-141">기본적으로, Azure ML 배치 실행 작업을 사용하여 학습 웹 서비스와 점수 매기기 웹 서비스를 모두 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="ac5e9-142">재학습으로 완료한 후에는 **Azure ML 업데이트 리소스 작업**을 사용하여 새로 학습한 모델로 점수 매기기 웹 서비스(웹 서비스로 노출된 예측 실험)를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="ac5e9-143">자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="ac5e9-144">배치 실행 작업을 사용하여 웹 서비스 호출</span><span class="sxs-lookup"><span data-stu-id="ac5e9-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="ac5e9-145">Azure 데이터 팩터리를 사용하여 데이터 이동 및 처리를 오케스트레이션한 다음 Azure 기계 학습을 사용하는 배치 실행을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="ac5e9-146">최상위 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="ac5e9-147">Azure 기계 학습 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="ac5e9-148">다음 값이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-148">You need the following values:</span></span>

   1. <span data-ttu-id="ac5e9-149">**요청 URI** .</span><span class="sxs-lookup"><span data-stu-id="ac5e9-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="ac5e9-150">웹 서비스 페이지에서 **배치 실행** 링크를 클릭하여 요청 URI를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="ac5e9-151">**API 키** .</span><span class="sxs-lookup"><span data-stu-id="ac5e9-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="ac5e9-152">게시한 웹 서비스를 클릭하여 API 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="ac5e9-153">**AzureMLBatchExecution** 작업을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![기계 학습 대시보드](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![배치 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="ac5e9-156">시나리오: Azure Blob 저장소의 데이터를 참조하는 웹 서비스 입력/출력을 사용하여 실험</span><span class="sxs-lookup"><span data-stu-id="ac5e9-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="ac5e9-157">이 시나리오에서는 Azure 기계 학습 웹 서비스는 Azure Blob 저장소의 파일에서 데이터를 사용하여 예측을 만들고 Blob 저장소에 예측 결과를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="ac5e9-158">다음 JSON은 AzureMLBatchExecution 작업이 포함된 Data Factory 파이프라인을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="ac5e9-159">작업에는 입력으로 **DecisionTreeInputBlob** 데이터 집합, 출력으로 **DecisionTreeResultBlob** 데이터 집합이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="ac5e9-160">**DecisionTreeInputBlob**은 **webServiceInput** JSON 속성을 사용하여 웹 서비스에 입력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="ac5e9-161">**DecisionTreeResultBlob**은 **webServiceOutputs** JSON 속성을 사용하여 웹 서비스에 출력으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="ac5e9-162">웹 서비스에서 다중 입력을 받을 경우 **webServiceInput**를 사용하는 대신에 **webServiceInputs** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-162">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="ac5e9-163">webServiceInputs 속성을 사용하는 예제는 [웹 서비스에는 다중 입력이 필요합니다](#web-service-requires-multiple-inputs) 섹션을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-163">See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.</span></span>
>
> <span data-ttu-id="ac5e9-164">**webServiceInput**/**webServiceInputs** 및 **webServiceOutputs** 속성(**typeProperties** 내)에서 참조하는 데이터 집합은 **inputs** 및 **outputs** 작업에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-164">Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="ac5e9-165">Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="ac5e9-166">WebServiceInputs, webServiceOutputs 및 globalParameters 설정에 대해 사용하는 이름은 실험에서의 이름과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-166">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="ac5e9-167">예상된 매핑을 확인하기 위해 일괄 처리 실행 도움말 페이지에서 Azure ML 끝점에 대한 샘플 요청 페이로드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-167">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> <span data-ttu-id="ac5e9-168">AzureMLBatchExecution 작업의 입력 및 출력만 웹 서비스에 매개 변수로 전달될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-168">Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service.</span></span> <span data-ttu-id="ac5e9-169">예를 들어 위의 JSON 조각에서 DecisionTreeInputBlob은 webServiceInput 매개 변수를 통해 웹 서비스에 입력으로 전달되는 AzureMLBatchExecution 작업에 대한 입력입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-169">For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="ac5e9-170">예</span><span class="sxs-lookup"><span data-stu-id="ac5e9-170">Example</span></span>
<span data-ttu-id="ac5e9-171">이 예제에서는 Azure 저장소를 사용하여 입력 및 출력 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="ac5e9-172">이 예제를 진행하기 전에 [Data Factory를 사용하여 첫 번째 파이프라인 빌드][adf-build-1st-pipeline] 자습서를 살펴보는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="ac5e9-173">이 예제에서는 Data Factory Editor를 사용하여 Data Factory 아티팩트(연결된 서비스, 데이터 집합, 파이프라인)를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="ac5e9-174">**Azure Storage**에 대한 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="ac5e9-175">입력 및 출력 파일이 서로 다른 저장소 계정에 있는 경우 연결된 서비스가 두 개 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="ac5e9-176">다음은 JSON 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="ac5e9-177">**입력** Azure Data Factory **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="ac5e9-178">다른 Data Factory 데이터 집합과 달리 이러한 데이터 집합은 **folderPath** 및 **fileName** 값을 둘 다 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="ac5e9-179">분할을 사용하여 각 배치 실행(각 데이터 조각)이 고유한 입력 및 출력 파일을 처리하거나 생성하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="ac5e9-180">입력을 CSV 파일 형식으로 변환하여 각 조각의 저장소 계정에 배치하는 업스트림 작업을 포함해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="ac5e9-181">이 경우 다음 예제에 표시된 **external** 및 **externalData** 설정을 포함하지 않으며, DecisionTreeInputBlob은 다른 작업의 출력 데이터 집합이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
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

    <span data-ttu-id="ac5e9-182">입력 csv 파일에는 열 머리글 행이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="ac5e9-183">**복사 작업**을 사용하여 csv를 만들고 Blob 저장소로 이동하는 경우 싱크 속성 **blobWriterAddHeader**를 **true**로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="ac5e9-184">예:</span><span class="sxs-lookup"><span data-stu-id="ac5e9-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="ac5e9-185">csv 파일에 머리글 행이 없는 경우 다음과 같은 오류가 표시될 수 있습니다. **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="ac5e9-186">**출력** Azure Data Factory **데이터 집합**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="ac5e9-187">이 예제에서는 분할을 사용하여 각 조각 실행의 고유한 출력 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="ac5e9-188">분할하지 않으면 작업에서 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="ac5e9-189">**AzureMLLinkedService** 형식의 **연결된 서비스**를 만들고 API 키 및 모델 배치 실행 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="ac5e9-190">끝으로, **AzureMLBatchExecution** 작업이 포함된 파이프라인을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="ac5e9-191">런타임에 파이프라인은 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="ac5e9-192">입력 데이터 집합에서 입력 파일의 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="ac5e9-193">Azure Machine Learning 배치 실행 API 호출</span><span class="sxs-lookup"><span data-stu-id="ac5e9-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="ac5e9-194">배치 실행 출력을 출력 데이터 집합에 지정된 Blob에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ac5e9-195">AzureMLBatchExecution 작업에는 0개 이상의 입력 및 1개 이상의 출력이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="ac5e9-196">**start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ac5e9-197">예: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="ac5e9-198">**end** 시간은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-198">The **end** time is optional.</span></span> <span data-ttu-id="ac5e9-199">**end** 속성 값을 지정하지 않는 경우 "**start + 48시간**"으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="ac5e9-200">파이프라인을 무기한 실행하려면 **종료** 속성 값으로 **9999-09-09**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="ac5e9-201">JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="ac5e9-202">AzureMLBatchExecution 작업에 대한 입력 지정은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-202">Specifying input for the AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="ac5e9-203">시나리오: 다양한 저장소의 데이터를 참조하는 판독기/기록기 모듈을 사용하여 실험</span><span class="sxs-lookup"><span data-stu-id="ac5e9-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="ac5e9-204">Azure ML 실험을 만들 때 다른 일반적인 시나리오는 판독기 및 기록기기 모듈을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="ac5e9-205">판독기 모듈은 실험으로 데이터를 로드할 때 사용되고 기록기 모듈은 실험에서 데이터를 저장할 때 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="ac5e9-206">판독기 및 기록기 모듈에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="ac5e9-207">판독기 및 작성기 모듈을 사용하는 경우 해당 판독기/기록기 모듈의 각 속성에 대해 웹 서비스 매개 변수를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="ac5e9-208">이러한 웹 매개 변수를 통해 런타임 중 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="ac5e9-209">예를 들어 Azure SQL 데이터베이스: XXX.database.windows.net을 사용하는 판독기 모듈을 사용하여 실험을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="ac5e9-210">웹 서비스를 배포한 후 웹 서비스의 소비자가 YYY.database.windows.net이라는 다른 Azure SQL Server를 지정할 수 있도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="ac5e9-211">웹 서비스 매개 변수를 사용하여 이 값을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> <span data-ttu-id="ac5e9-212">웹 서비스 입력 및 출력은 웹 서비스 매개 변수와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="ac5e9-213">첫 번째 시나리오에서 Azure ML 웹 서비스에 대해 입력 및 출력을 지정할 수 있는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-213">In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="ac5e9-214">이 시나리오에서는 판독기/기록기 모듈의 속성에 해당하는 웹 서비스에 대한 매개 변수를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-214">In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="ac5e9-215">웹 서비스 매개 변수를 사용하는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="ac5e9-216">Azure Machine Learning에서 지원하는 데이터 원본(예: Azure SQL Database) 중 하나에서 데이터를 읽는 판독기 모듈을 사용하는 Azure Machine Learning 웹 서비스를 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="ac5e9-217">배치 실행이 수행된 후 기록기 모듈(Azure SQL 데이터베이스)을 사용하여 결과가 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="ac5e9-218">웹 서비스 입력 및 출력이 실험에서 정의되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="ac5e9-219">이 경우 판독기 및 기록기 모듈에 대한 관련 웹 서비스 매개 변수를 구성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="ac5e9-220">이 구성을 통해 AzureMLBatchExecution 작업을 사용하는 경우 판독기/기록기 모듈을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="ac5e9-221">다음과 같이 작업 JSON의 **globalParameters** 섹션에서 웹 서비스 매개 변수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="ac5e9-222">다음 예제와 같이 웹 서비스 매개 변수 값을 전달하는 데 [데이터 팩터리 함수](data-factory-functions-variables.md) 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="ac5e9-223">웹 서비스 매개 변수는 대/소문자를 구분하므로 작업 JSON에서 지정한 이름이 웹 서비스에 의해 노출된 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-223">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="ac5e9-224">Azure Blob에서 여러 파일의 데이터를 읽는 판독기 모듈 사용</span><span class="sxs-lookup"><span data-stu-id="ac5e9-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="ac5e9-225">Pig, Hive와 같은 작업이 있는 빅 데이터 파이프라인은 확장명 없이 하나 이상의 출력 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="ac5e9-226">예를 들어 외부 Hive 테이블을 지정하는 경우 외부 Hive 테이블에 대한 데이터는 다음 이름 000000_0으로 Azure Blob 저장소에 저장될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="ac5e9-227">실험에서 판독기 모듈을 사용하여 여러 파일을 읽고 예측에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="ac5e9-228">Azure 기계 학습 실험에서 판독기 모듈을 사용하는 경우 입력으로 Azure Blob를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="ac5e9-229">Azure Blob 저장소에 있는 파일은 HDInsight에서 실행되는 Pig 및 Hive 스크립트에서 생성되는 출력 파일(예: 000000_0)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="ac5e9-230">판독기 모듈을 통해 **컨테이너, 디렉터리/blob에 대한 경로**를 구성하여 파일(확장명 없음)을 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="ac5e9-231">**컨테이너에 대한 경로**는 컨테이너를 가리키고 **디렉터리/blob**은 다음 이미지에 표시된 파일이 들어 있는 폴더를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="ac5e9-232">**컨테이너/폴더에 있는 모든 파일을 지정하는(즉, data/aggregateddata/year=2014/month-6/\*)** 별표, 즉 \*)는 실험의 일부로 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Azure Blob 속성](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="ac5e9-234">예</span><span class="sxs-lookup"><span data-stu-id="ac5e9-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="ac5e9-235">AzureMLBatchExecution 작업 및 웹 서비스 매개 변수가 포함된 파이프라인</span><span class="sxs-lookup"><span data-stu-id="ac5e9-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="ac5e9-236">위 JSON 예제에서</span><span class="sxs-lookup"><span data-stu-id="ac5e9-236">In the above JSON example:</span></span>

* <span data-ttu-id="ac5e9-237">배포된 Azure 기계 학습 웹 서비스는 판독기 및 기록기 모듈을 사용하여 Azure SQL 데이터베이스에서/로 데이터를 읽고/쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="ac5e9-238">이 웹 서비스는 네 개의 매개 변수, 즉 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호를 공개합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="ac5e9-239">**start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="ac5e9-240">예: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="ac5e9-241">**end** 시간은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-241">The **end** time is optional.</span></span> <span data-ttu-id="ac5e9-242">**end** 속성 값을 지정하지 않는 경우 "**start + 48시간**"으로 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="ac5e9-243">파이프라인을 무기한 실행하려면 **종료** 속성 값으로 **9999-09-09**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="ac5e9-244">JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="ac5e9-245">기타 시나리오</span><span class="sxs-lookup"><span data-stu-id="ac5e9-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="ac5e9-246">웹 서비스에는 다중 입력이 필요합니다</span><span class="sxs-lookup"><span data-stu-id="ac5e9-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="ac5e9-247">웹 서비스에서 다중 입력을 받을 경우 **webServiceInput**를 사용하는 대신에 **webServiceInputs** 속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="ac5e9-248">**webServiceInputs**에서 참조하는 데이터 집합은 또한 **입력** 작업에 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="ac5e9-249">Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="ac5e9-250">WebServiceInputs, webServiceOutputs 및 globalParameters 설정에 대해 사용하는 이름은 실험에서의 이름과 정확히 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="ac5e9-251">예상된 매핑을 확인하기 위해 일괄 처리 실행 도움말 페이지에서 Azure ML 끝점에 대한 샘플 요청 페이로드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="ac5e9-252">웹 서비스에는 입력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-252">Web Service does not require an input</span></span>
<span data-ttu-id="ac5e9-253">Azure ML 배치 실행 웹 서비스는 입력이 필요하지 않는 모든 워크플로(예: R 또는 Python 스크립트)를 실행하는 데 사용할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="ac5e9-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="ac5e9-254">또는 어떠한 GlobalParameters도 노출하지 않는 판독기 모듈로 실험을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="ac5e9-255">이 경우 AzureMLBatchExecution 작업은 다음과 같이 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="ac5e9-256">웹 서비스에는 입력/출력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="ac5e9-257">Azure ML 배치 실행 웹 서비스에는 웹 서비스 출력이 구성되어 있지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="ac5e9-258">이 예제에서는 웹 서비스 입력 또는 출력이 없으며 GlobalParameters도 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="ac5e9-259">작업 자체에 여전히 출력이 구성되어 있지만 webServiceOutput으로 제공된 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="ac5e9-260">웹 서비스는 판독기 및 기록기를 사용하며 작업은 다른 작업이 성공한 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="ac5e9-261">Azure ML 웹 서비스의 판독기 및 기록기 모듈은 GlobalParameters를 포함 또는 포함하지 않고 실행하도록 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="ac5e9-262">하지만 일부 업스트림 처리가 완료될 때만 서비스를 호출하도록 데이터 집합 종속성을 사용하는 파이프라인에 서비스 호출을 포함하려 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="ac5e9-263">또한 이 방법을 사용하여 배치 실행이 완료된 후 다른 작업을 트리거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="ac5e9-264">이 경우 웹 서비스 입력 또는 출력으로 이름을 지정하지 않고 입력 및 출력 작업을 사용하여 종속성을 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="ac5e9-265">**내용** 은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-265">The **takeaways** are:</span></span>

* <span data-ttu-id="ac5e9-266">실험 끝점에서 webServiceInput을 사용하면 Blob 데이터 집합으로 표시되고 작업 입력 및 webServiceInput 속성에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="ac5e9-267">그렇지 않은 경우 webServiceInput 속성은 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="ac5e9-268">실험 끝점에서 webServiceOutput을 사용하면 Blob 데이터 집합으로 표시되고 작업 출력 및 webServiceOutputs 속성에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="ac5e9-269">작업 출력 및 webServiceOutputs는 실험에서 각 출력의 이름으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="ac5e9-270">그렇지 않은 경우 webServiceOutputs 속성은 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="ac5e9-271">실험 끝점에서 globalParameter를 노출하는 경우 키, 값 쌍으로 작업 globalParameters 속성에 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="ac5e9-272">그렇지 않은 경우 globalParameters 속성은 생략됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="ac5e9-273">키는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-273">The keys are case-sensitive.</span></span> <span data-ttu-id="ac5e9-274">[Azure Data Factory 함수](data-factory-functions-variables.md) 를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="ac5e9-275">작업 typeProperties 속성에 참조되지 않고도 추가 데이터 집합이 작업 입력 및 출력 속성에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="ac5e9-276">이러한 데이터 집합은 조각 종속성을 사용한 실행에 적용되지만 그렇지 않은 경우 AzureMLBatchExecution 작업에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="ac5e9-277">업데이트 리소스 작업을 사용하여 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="ac5e9-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="ac5e9-278">재학습으로 완료한 후에는 **Azure ML 업데이트 리소스 작업**을 사용하여 새로 학습한 모델로 점수 매기기 웹 서비스(웹 서비스로 노출된 예측 실험)를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="ac5e9-279">자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="ac5e9-280">판독기 및 작성기 모듈</span><span class="sxs-lookup"><span data-stu-id="ac5e9-280">Reader and Writer Modules</span></span>
<span data-ttu-id="ac5e9-281">웹 서비스 매개 변수를 사용하는 일반적인 시나리오는 Azure SQL 판독기 및 기록기 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="ac5e9-282">판독기 모듈은 Azure Machine Learning Studio 외부 데이터 관리 서비스에서 실험으로 데이터를 로드하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="ac5e9-283">작성기 모듈은 사용자 실험에서 Azure Machine Learning Studio 외부 데이터 관리 서비스로 데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="ac5e9-284">Azure Blob/Azure SQL 판독기/기록기에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="ac5e9-285">이전 섹션의 예제에서는 Azure Blob 판독기 및 Azure Blob 기록기를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="ac5e9-286">이 섹션에서는 Azure SQL 판독기 및 Azure SQL 기록기를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ac5e9-287">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="ac5e9-287">Frequently asked questions</span></span>
<span data-ttu-id="ac5e9-288">**Q:** 빅 데이터 파이프라인에서 생성된 여러 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="ac5e9-289">모든 파일에서 작동하도록 AzureMLBatchExecution 작업을 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="ac5e9-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="ac5e9-290">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-290">**A:** Yes.</span></span> <span data-ttu-id="ac5e9-291">자세한 내용은 **Azure Blob에서 여러 파일의 데이터를 읽는 판독기 모듈 사용** 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="ac5e9-292">Azure ML 일괄 처리 점수 매기기 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="ac5e9-293">**AzureMLBatchScoring** 작업을 사용하여 Azure Machine Learning과 통합하는 경우 최신 **AzureMLBatchExecution** 작업을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="ac5e9-294">AzureMLBatchExecution 작업은2015년 8월 Azure SDK 및 Azure PowerShell 릴리스에서 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="ac5e9-295">AzureMLBatchScoring 작업을 사용하여 계속하려면 이 섹션을 계속 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="ac5e9-296">입/출력에 대해 Azure 저장소를 사용하는 Azure ML 일괄 처리 점수 매기기 작업</span><span class="sxs-lookup"><span data-stu-id="ac5e9-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="ac5e9-297">웹 서비스 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ac5e9-297">Web Service Parameters</span></span>
<span data-ttu-id="ac5e9-298">웹 서비스 매개 변수에 대한 값을 지정하려면 다음 예제와 같이 파이프라인 JSON의 **AzureMLBatchScoringActivty** 섹션에 **typeProperties** 섹션을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="ac5e9-299">다음 예제와 같이 웹 서비스 매개 변수 값을 전달하는 데 [데이터 팩터리 함수](data-factory-functions-variables.md) 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="ac5e9-300">웹 서비스 매개 변수는 대/소문자를 구분하므로 작업 JSON에서 지정한 이름이 웹 서비스에 의해 노출된 이름과 일치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac5e9-300">The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="ac5e9-301">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ac5e9-301">See Also</span></span>
* [<span data-ttu-id="ac5e9-302">Azure 블로그 게시물: Azure 데이터 팩터리 및 Azure 기계 학습 시작하기</span><span class="sxs-lookup"><span data-stu-id="ac5e9-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
