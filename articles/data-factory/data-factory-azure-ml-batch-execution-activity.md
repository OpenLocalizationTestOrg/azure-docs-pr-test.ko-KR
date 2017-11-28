---
title: "Azure 데이터 팩터리를 사용 하 여 aaaCreate 예측 데이터 파이프라인 | Microsoft Docs"
description: "Toocreate Azure 데이터 팩터리 및 Azure 기계 학습을 사용 하 여 예측 파이프라인을 생성 하는 방법을 설명 합니다."
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
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="75583-103">Azure Machine Learning 및 Azure Data Factory를 사용하여 예측 파이프라인 만들기</span><span class="sxs-lookup"><span data-stu-id="75583-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="75583-104">Hive 작업</span><span class="sxs-lookup"><span data-stu-id="75583-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="75583-105">Pig 작업</span><span class="sxs-lookup"><span data-stu-id="75583-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="75583-106">MapReduce 작업</span><span class="sxs-lookup"><span data-stu-id="75583-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="75583-107">Hadoop 스트리밍 작업</span><span class="sxs-lookup"><span data-stu-id="75583-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="75583-108">Spark 작업</span><span class="sxs-lookup"><span data-stu-id="75583-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="75583-109">Machine Learning Batch 실행 작업</span><span class="sxs-lookup"><span data-stu-id="75583-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="75583-110">Machine Learning 업데이트 리소스 작업</span><span class="sxs-lookup"><span data-stu-id="75583-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="75583-111">저장 프로시저 작업</span><span class="sxs-lookup"><span data-stu-id="75583-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="75583-112">Data Lake Analytics U-SQL 작업</span><span class="sxs-lookup"><span data-stu-id="75583-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="75583-113">.NET 사용자 지정 작업</span><span class="sxs-lookup"><span data-stu-id="75583-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="75583-114">소개</span><span class="sxs-lookup"><span data-stu-id="75583-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="75583-115">Azure 기계 학습</span><span class="sxs-lookup"><span data-stu-id="75583-115">Azure Machine Learning</span></span>
<span data-ttu-id="75583-116">[Azure 기계 학습](https://azure.microsoft.com/documentation/services/machine-learning/) toobuild, 테스트 및 예측 분석 솔루션을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you toobuild, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="75583-117">대략적인 관점에서 이 작업은 다음 세 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="75583-118">**학습 실험 만들기**.</span><span class="sxs-lookup"><span data-stu-id="75583-118">**Create a training experiment**.</span></span> <span data-ttu-id="75583-119">Hello Azure 기계 학습 스튜디오를 사용 하 여이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-119">You do this step by using hello Azure ML Studio.</span></span> <span data-ttu-id="75583-120">hello 기계 학습 스튜디오는 tootrain를 사용 하 여 학습 데이터를 사용 하 여 예측 분석 모델을 테스트 하는 시각적 공동 개발 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-120">hello ML studio is a collaborative visual development environment that you use tootrain and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="75583-121">**Tooa 예측 실험으로 변환**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-121">**Convert it tooa predictive experiment**.</span></span> <span data-ttu-id="75583-122">기존 데이터와 모델의 학습 및 준비 toouse 되 면 그 tooscore 새 데이터를 준비 하 고 점수 매기기 실험을 간소화 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-122">Once your model has been trained with existing data and you are ready toouse it tooscore new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="75583-123">**웹 서비스로 배포**.</span><span class="sxs-lookup"><span data-stu-id="75583-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="75583-124">점수 매기기 실험을 Azure 웹 서비스로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="75583-125">이 웹 서비스 끝점을 통해 데이터 tooyour 모델을 보내고 결과 예측을 hello 모델에서 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-125">You can send data tooyour model via this web service end point and receive result predictions fro hello model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="75583-126">Azure 데이터 팩터리</span><span class="sxs-lookup"><span data-stu-id="75583-126">Azure Data Factory</span></span>
<span data-ttu-id="75583-127">데이터 팩터리는 오케스트레이션 하 고 hello를 자동화 하는 클라우드 기반 데이터 통합 서비스 **이동** 및 **변환** 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-127">Data Factory is a cloud-based data integration service that orchestrates and automates hello **movement** and **transformation** of data.</span></span> <span data-ttu-id="75583-128">데이터 통합 솔루션 Azure 데이터 팩터리를 사용 하 고 수 있는 다양 한 데이터 저장소에서 데이터를 수집, hello 데이터 변환/프로세스가 hello 결과 데이터 toohello 데이터 저장소에 게시를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process hello data, and publish hello result data toohello data stores.</span></span>

<span data-ttu-id="75583-129">데이터 팩터리 서비스 이동 하 고 데이터를 변환 하는 toocreate 데이터 파이프라인을 허용 하 고 (시간별, 일별, 주별 등). 지정된 된 일정에 hello 파이프라인을 실행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="75583-129">Data Factory service allows you toocreate data pipelines that move and transform data, and then run hello pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="75583-130">또한 다양 한 시각화 기능 toodisplay hello 계보 및 데이터 파이프라인, 간의 종속성을 제공 하 고 모든 데이터 파이프라인에서 단일 통합된 뷰 tooeasily 정확 하 게 문제를 모니터링 하 고 모니터링 경고 설정.</span><span class="sxs-lookup"><span data-stu-id="75583-130">It also provides rich visualizations toodisplay hello lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view tooeasily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="75583-131">참조 [소개 tooAzure Data Factory](data-factory-introduction.md) 및 [첫 번째 파이프라인 빌드](data-factory-build-your-first-pipeline.md) 문서 tooquickly hello Azure 데이터 팩터리 서비스를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-131">See [Introduction tooAzure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles tooquickly get started with hello Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="75583-132">Data Factory 및 Machine Learning</span><span class="sxs-lookup"><span data-stu-id="75583-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="75583-133">Azure Data Factory 수 있도록 tooeasily 하면 게시 된 보고서를 사용 하는 파이프라인을 만들 [Azure 기계 학습] [ azure-machine-learning] 웹 서비스에 대 한 예측 분석 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-133">Azure Data Factory enables you tooeasily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="75583-134">Hello를 사용 하 여 **일괄 처리 실행 작업** 는 Azure 데이터 팩터리 파이프라인에서 일괄 처리의 hello 데이터에는 Azure ML 웹 서비스 toomake 예측을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-134">Using hello **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service toomake predictions on hello data in batch.</span></span> <span data-ttu-id="75583-135">참조 [일괄 처리 실행 작업 hello 웹 서비스를 사용 하 여 Azure 기계 학습 호출](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="75583-135">See [Invoking an Azure ML web service using hello Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="75583-136">시간이 지남에 따라 hello hello Azure 기계 학습 점수 매기기 실험에 예측 모델에 새 입력된 데이터 집합을 통해 유지 toobe가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-136">Over time, hello predictive models in hello Azure ML scoring experiments need toobe retrained using new input datasets.</span></span> <span data-ttu-id="75583-137">데이터 팩토리 파이프라인에서는 Azure ML 모델을 보존 하기 위해 hello 다음 단계를 수행 하 여 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-137">You can retrain an Azure ML model from a Data Factory pipeline by doing hello following steps:</span></span>

1. <span data-ttu-id="75583-138">Hello 학습 실험 (예측 하지 실험) 웹 서비스로 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-138">Publish hello training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="75583-139">Hello 이전 시나리오에서 웹 서비스로 tooexpose 예측 실험을 수행한 것 처럼 hello Azure 기계 학습 스튜디오에서에서이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-139">You do this step in hello Azure ML Studio as you did tooexpose predictive experiment as a web service in hello previous scenario.</span></span>
2. <span data-ttu-id="75583-140">Hello 학습 실험에 대 한 hello Azure ML 일괄 처리 실행 작업 tooinvoke hello 웹 서비스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-140">Use hello Azure ML Batch Execution Activity tooinvoke hello web service for hello training experiment.</span></span> <span data-ttu-id="75583-141">기본적으로, hello Azure ML 일괄 처리 실행 활동 tooinvoke 학습 웹 서비스 및 웹 서비스 점수 매기기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-141">Basically, you can use hello Azure ML Batch Execution activity tooinvoke both training web service and scoring web service.</span></span>

<span data-ttu-id="75583-142">재교육를 완료 한 후 업데이트 hello를 사용 하 여 웹 서비스 (웹 서비스로 노출 된 예측 실험) hello 새로 학습 된 모델 점수 매기기 hello **Azure ML 업데이트 리소스 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-142">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="75583-143">자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="75583-144">배치 실행 작업을 사용하여 웹 서비스 호출</span><span class="sxs-lookup"><span data-stu-id="75583-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="75583-145">Azure Data Factory tooorchestrate 데이터 이동 및 처리를 사용 하 고이 정보를 Azure 기계 학습을 사용 하 여 일괄 처리 실행을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-145">You use Azure Data Factory tooorchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="75583-146">Hello 최상위 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-146">Here are hello top-level steps:</span></span>

1. <span data-ttu-id="75583-147">Azure 기계 학습 연결된 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75583-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="75583-148">다음 값에는 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-148">You need hello following values:</span></span>

   1. <span data-ttu-id="75583-149">**요청 URI** hello 일괄 처리 실행 API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-149">**Request URI** for hello Batch Execution API.</span></span> <span data-ttu-id="75583-150">Hello를 클릭 하 여 hello 요청 URI를 찾을 수 있습니다 **일괄 처리 실행** hello 웹 서비스 페이지에 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-150">You can find hello Request URI by clicking hello **BATCH EXECUTION** link in hello web services page.</span></span>
   2. <span data-ttu-id="75583-151">**API 키** hello Azure 기계 학습 웹 서비스를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-151">**API key** for hello published Azure Machine Learning web service.</span></span> <span data-ttu-id="75583-152">Hello 웹 서비스 게시를 클릭 하 여 hello API 키를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-152">You can find hello API key by clicking hello web service that you have published.</span></span>
   3. <span data-ttu-id="75583-153">사용 하 여 hello **AzureMLBatchExecution** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-153">Use hello **AzureMLBatchExecution** activity.</span></span>

      ![기계 학습 대시보드](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![배치 URI](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a><span data-ttu-id="75583-156">시나리오: 웹 서비스 입력/출력 toodata Azure Blob 저장소에 참조를 사용 하 여 실험</span><span class="sxs-lookup"><span data-stu-id="75583-156">Scenario: Experiments using Web service inputs/outputs that refer toodata in Azure Blob Storage</span></span>
<span data-ttu-id="75583-157">이 시나리오에서는 hello Azure 컴퓨터 학습 웹 서비스에서 Azure blob 저장소의 파일에서 데이터를 사용 하 여 예측을 수행 하 고 hello blob 저장소에 hello 예측 결과 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-157">In this scenario, hello Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores hello prediction results in hello blob storage.</span></span> <span data-ttu-id="75583-158">hello 다음 JSON 정의 AzureMLBatchExecution 작업과 함께 데이터 팩터리 파이프라인 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-158">hello following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="75583-159">hello 활동에 데이터 집합이 두 hello **DecisionTreeInputBlob** 입력으로 및 **DecisionTreeResultBlob** hello 출력으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-159">hello activity has hello dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as hello output.</span></span> <span data-ttu-id="75583-160">hello **DecisionTreeInputBlob** hello를 사용 하 여 입력된 toohello 웹 서비스로 전달 되 **webServiceInput** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-160">hello **DecisionTreeInputBlob** is passed as an input toohello web service by using hello **webServiceInput** JSON property.</span></span> <span data-ttu-id="75583-161">hello **DecisionTreeResultBlob** hello를 사용 하 여 출력 toohello 웹 서비스로 전달 되 **webServiceOutputs** JSON 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-161">hello **DecisionTreeResultBlob** is passed as an output toohello Web service by using hello **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="75583-162">Hello를 사용 하 여 hello 웹 서비스 변수를 사용할 경우 여러 개의 입력 **webServiceInputs** 사용 하는 대신 속성 **webServiceInput**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-162">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="75583-163">Hello 참조 [웹 서비스 작업에 여러 개의 입력](#web-service-requires-multiple-inputs) hello webServiceInputs 속성을 사용 하는 예제에 대 한 섹션.</span><span class="sxs-lookup"><span data-stu-id="75583-163">See hello [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using hello webServiceInputs property.</span></span>
>
> <span data-ttu-id="75583-164">Hello에서 참조 되는 데이터 집합 **webServiceInput**/**webServiceInputs** 및 **webServiceOutputs** 속성 (에서  **typeProperties**) hello 활동에에서도 포함 해야 **입력** 및 **출력**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-164">Datasets that are referenced by hello **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in hello Activity **inputs** and **outputs**.</span></span>
>
> <span data-ttu-id="75583-165">Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-165">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="75583-166">webServiceInputs, webServiceOutputs, 및 globalParameters 설정에 사용할 수는 hello 이름에는 hello 실험에서 hello 이름과 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-166">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="75583-167">Azure 기계 학습 끝점 tooverify 예상 hello 매핑을 대 한 hello 일괄 처리 실행 도움말 페이지에 hello 샘플 요청 페이로드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-167">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>
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
> <span data-ttu-id="75583-168">유일한 입 / 출력 hello AzureMLBatchExecution 활동의 매개 변수 toohello 웹 서비스 변수로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-168">Only inputs and outputs of hello AzureMLBatchExecution activity can be passed as parameters toohello Web service.</span></span> <span data-ttu-id="75583-169">예를 들어 JSON 코드 조각은 위에 hello, DecisionTreeInputBlob은 입력된 toohello webServiceInput 매개 변수를 통해 웹 서비스는 입력된 toohello 변수로 전달 되는 AzureMLBatchExecution 활동에는 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-169">For example, in hello above JSON snippet, DecisionTreeInputBlob is an input toohello AzureMLBatchExecution activity, which is passed as an input toohello Web service via webServiceInput parameter.</span></span>   
>
>

### <a name="example"></a><span data-ttu-id="75583-170">예제</span><span class="sxs-lookup"><span data-stu-id="75583-170">Example</span></span>
<span data-ttu-id="75583-171">이 예에서는 사용 하 여 Azure 저장소 toohold 입력 및 출력 데이터 hello 둘 다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-171">This example uses Azure Storage toohold both hello input and output data.</span></span>

<span data-ttu-id="75583-172">Hello를 통과 하는 것이 좋습니다 [데이터 팩터리와 첫 번째 파이프라인 빌드] [ adf-build-1st-pipeline] 자습서이 예제를 진행 하십시오.</span><span class="sxs-lookup"><span data-stu-id="75583-172">We recommend that you go through hello [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="75583-173">이 예에서 hello 데이터 팩터리 편집기 toocreate 데이터 팩터리 아티팩트의 (연결 된 서비스, 데이터 집합, 파이프라인)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-173">Use hello Data Factory Editor toocreate Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="75583-174">**Azure Storage**에 대한 **연결된 서비스**를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="75583-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="75583-175">Hello 입력 및 출력 파일에 있는 경우 다른 저장소 계정에는 두 개의 연결 된 서비스가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-175">If hello input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="75583-176">다음은 JSON 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-176">Here is a JSON example:</span></span>

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
2. <span data-ttu-id="75583-177">Hello 만들기 **입력** Azure Data Factory **dataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-177">Create hello **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="75583-178">다른 Data Factory 데이터 집합과 달리 이러한 데이터 집합은 **folderPath** 및 **fileName** 값을 둘 다 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="75583-179">각 일괄 처리 실행 (각 데이터 조각) tooprocess toocause 분할을 사용 하 여 또는 고유한 입력을 생성 한 출력 파일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-179">You can use partitioning toocause each batch execution (each data slice) tooprocess or produce unique input and output files.</span></span> <span data-ttu-id="75583-180">Tooinclude 일부 업스트림 작업 tootransform hello hello CSV 파일 형식으로 입력 하 고 각 조각에 대 한 hello 저장소 계정에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-180">You may need tooinclude some upstream activity tootransform hello input into hello CSV file format and place it in hello storage account for each slice.</span></span> <span data-ttu-id="75583-181">Hello 하지 포함 경우 **외부** 및 **externalData** hello 뒤에 표시 된 예제에서는 하 여 DecisionTreeInputBlob 것은 다른 활동의 hello 출력 데이터 집합 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-181">In that case, you would not include hello **external** and **externalData** settings shown in hello following example, and your DecisionTreeInputBlob would be hello output dataset of a different Activity.</span></span>

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

    <span data-ttu-id="75583-182">입력된 csv 파일 hello 열 머리글 행에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-182">Your input csv file must have hello column header row.</span></span> <span data-ttu-id="75583-183">Hello를 사용 하는 경우 **복사 작업** hello blob 저장소로 toocreate/이동 hello csv hello 싱크 속성을 설정 해야 **blobWriterAddHeader** 너무**true**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-183">If you are using hello **Copy Activity** toocreate/move hello csv into hello blob storage, you should set hello sink property **blobWriterAddHeader** too**true**.</span></span> <span data-ttu-id="75583-184">예:</span><span class="sxs-lookup"><span data-stu-id="75583-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="75583-185">Hello csv 파일 hello 머리글 행이 없는 경우 hello 다음 오류가 표시 될 수 있습니다: **활동에서 오류가: 문자열을 읽는 동안 오류가 발생 합니다. Unexpected token: StartObject. Path '', line 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="75583-185">If hello csv file does not have hello header row, you may see hello following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="75583-186">Hello 만들기 **출력** Azure Data Factory **dataset**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-186">Create hello **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="75583-187">이 예제에서는 각 조각 실행에 대 한 분할 toocreate 고유한 출력 경로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-187">This example uses partitioning toocreate a unique output path for each slice execution.</span></span> <span data-ttu-id="75583-188">Hello 활동 hello 분할 수 없이 hello 파일을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="75583-188">Without hello partitioning, hello activity would overwrite hello file.</span></span>

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
4. <span data-ttu-id="75583-189">만들기는 **연결 된 서비스** 형식의: **AzureMLLinkedService**, hello API 키를 제공 하 및 일괄 처리 실행 URL을 모델링 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-189">Create a **linked service** of type: **AzureMLLinkedService**, providing hello API key and model batch execution URL.</span></span>

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
5. <span data-ttu-id="75583-190">끝으로, **AzureMLBatchExecution** 작업이 포함된 파이프라인을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="75583-191">런타임 시, 파이프라인 단계를 수행 하는 hello를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-191">At runtime, pipeline performs hello following steps:</span></span>

   1. <span data-ttu-id="75583-192">입력된 데이터 집합에서 hello 입력된 파일의 hello 위치를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="75583-192">Gets hello location of hello input file from your input datasets.</span></span>
   2. <span data-ttu-id="75583-193">Hello Azure 기계 학습 일괄 처리 실행 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-193">Invokes hello Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="75583-194">복사는 출력 데이터 집합에 지정 된 일괄 처리 실행 출력 toohello blob을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-194">Copies hello batch execution output toohello blob given in your output dataset.</span></span>

      > [!NOTE]
      > <span data-ttu-id="75583-195">AzureMLBatchExecution 작업에는 0개 이상의 입력 및 1개 이상의 출력이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-195">AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.</span></span>
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

      <span data-ttu-id="75583-196">**start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="75583-197">예: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="75583-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="75583-198">hello **끝** 으로 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-198">hello **end** time is optional.</span></span> <span data-ttu-id="75583-199">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간입니다.**"</span><span class="sxs-lookup"><span data-stu-id="75583-199">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="75583-200">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-200">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="75583-201">JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > <span data-ttu-id="75583-202">Hello AzureMLBatchExecution 활동에 대 한 입력을 지정 하는 것은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-202">Specifying input for hello AzureMLBatchExecution activity is optional.</span></span>
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a><span data-ttu-id="75583-203">시나리오: toorefer toodata 판독기/작성기 모듈을 사용 하 여 다양 한 저장소에서 실험</span><span class="sxs-lookup"><span data-stu-id="75583-203">Scenario: Experiments using Reader/Writer Modules toorefer toodata in various storages</span></span>
<span data-ttu-id="75583-204">Azure 기계 학습 실험을 만들 때 또 다른 일반적인 시나리오는 toouse 판독기 및 작성기 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-204">Another common scenario when creating Azure ML experiments is toouse Reader and Writer modules.</span></span> <span data-ttu-id="75583-205">hello 판독기는 실험에 사용 되는 tooload 데이터 고 hello 기록기 모듈은 실험에서 toosave 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-205">hello reader module is used tooload data into an experiment and hello writer module is toosave data from your experiments.</span></span> <span data-ttu-id="75583-206">판독기 및 기록기 모듈에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="75583-207">Hello 판독기 및 작성기 모듈을 사용할 경우 좋습니다 toouse 이러한 판독기/작성기 모듈의 각 속성에 대 한 웹 서비스 매개 변수는 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-207">When using hello reader and writer modules, it is good practice toouse a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="75583-208">이러한 웹 매개 변수 런타임 동안 tooconfigure hello 값을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-208">These web parameters enable you tooconfigure hello values during runtime.</span></span> <span data-ttu-id="75583-209">예를 들어 Azure SQL 데이터베이스: XXX.database.windows.net을 사용하는 판독기 모듈을 사용하여 실험을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="75583-210">Hello 웹 서비스가 배포 된 후 원하는 hello 웹 서비스 toospecify의 tooenable hello 소비자 YYY.database.windows.net 라는 다른 Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="75583-210">After hello web service has been deployed, you want tooenable hello consumers of hello web service toospecify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="75583-211">이 값 toobe 구성 된 웹 서비스 매개 변수 tooallow를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-211">You can use a Web service parameter tooallow this value toobe configured.</span></span>

> [!NOTE]
> <span data-ttu-id="75583-212">웹 서비스 입력 및 출력은 웹 서비스 매개 변수와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="75583-212">Web service input and output are different from Web service parameters.</span></span> <span data-ttu-id="75583-213">Hello 첫 번째 시나리오에서는 Azure 기계 학습 웹 서비스에 대 한 입력 및 출력 수 지정 하는 방법을 설명 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-213">In hello first scenario, you have seen how an input and output can be specified for an Azure ML Web service.</span></span> <span data-ttu-id="75583-214">이 시나리오에서는 tooproperties 판독기/작성기 모듈의 해당 하는 웹 서비스에 대 한 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-214">In this scenario, you pass parameters for a Web service that correspond tooproperties of reader/writer modules.</span></span>
>
>

<span data-ttu-id="75583-215">웹 서비스 매개 변수를 사용하는 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="75583-216">판독기 모듈 tooread 데이터를 Azure 기계 학습에서 지 원하는 hello 데이터 원본 중 하나를 사용 하는 배포 된 Azure 기계 학습 웹 서비스 (예: Azure SQL 데이터베이스).</span><span class="sxs-lookup"><span data-stu-id="75583-216">You have a deployed Azure Machine Learning web service that uses a reader module tooread data from one of hello data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="75583-217">Hello 일괄 처리 실행이 수행 된 후 기록기 모듈 (Azure SQL 데이터베이스)를 사용 하 여 hello 결과가 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-217">After hello batch execution is performed, hello results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="75583-218">웹 서비스 입력 및 출력 없음 hello 실험에서 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-218">No web service inputs and outputs are defined in hello experiments.</span></span> <span data-ttu-id="75583-219">이 경우 hello 판독기 및 작성기 모듈에 대 한 관련 웹 서비스 매개 변수를 구성 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-219">In this case, we recommend that you configure relevant web service parameters for hello reader and writer modules.</span></span> <span data-ttu-id="75583-220">이 구성은 hello AzureMLBatchExecution 활동을 사용 하는 경우 구성 모듈 toobe hello 읽기/쓰기를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-220">This configuration allows hello reader/writer modules toobe configured when using hello AzureMLBatchExecution activity.</span></span> <span data-ttu-id="75583-221">Hello에 웹 서비스 매개 변수를 지정 하면 **globalParameters** 다음과 같이 hello 활동 JSON 섹션.</span><span class="sxs-lookup"><span data-stu-id="75583-221">You specify Web service parameters in hello **globalParameters** section in hello activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="75583-222">사용할 수도 있습니다 [데이터 팩터리 함수](data-factory-functions-variables.md) hello에 대 한 값 hello 다음 예제와 같이 웹 서비스 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="75583-223">hello 웹 서비스 매개 변수가 대/소문자를 구분 하므로 hello 활동에서 지정 하는 hello 이름을 JSON과 일치 하는지 hello hello 웹 서비스에서 노출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-223">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="75583-224">판독기 모듈 tooread 데이터를 사용 하 여 Azure Blob에 여러 파일에서</span><span class="sxs-lookup"><span data-stu-id="75583-224">Using a Reader module tooread data from multiple files in Azure Blob</span></span>
<span data-ttu-id="75583-225">Pig, Hive와 같은 작업이 있는 빅 데이터 파이프라인은 확장명 없이 하나 이상의 출력 파일을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="75583-226">예를 들어 외부 하이브 테이블을 지정 하면 hello 외부 Hive 테이블에 대 한 hello 데이터 저장할 수 있습니다 Azure blob 저장소에 이름 000000_0 다음 hello로.</span><span class="sxs-lookup"><span data-stu-id="75583-226">For example, when you specify an external Hive table, hello data for hello external Hive table can be stored in Azure blob storage with hello following name 000000_0.</span></span> <span data-ttu-id="75583-227">여러 개의 파일을 실험 tooread에 hello 판독기 모듈을 사용할 수 있으며 예측에 대 한 사용.</span><span class="sxs-lookup"><span data-stu-id="75583-227">You can use hello reader module in an experiment tooread multiple files, and use them for predictions.</span></span>

<span data-ttu-id="75583-228">Azure 기계 학습 실험에서 hello 판독기 모듈을 사용할 때 Azure Blob을 입력으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-228">When using hello reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="75583-229">hello Azure blob 저장소의에서 hello 파일 hello 출력 파일 일 수 있습니다 (예: 000000_0) HDInsight에서 실행 되는 Pig 및 Hive 스크립트에 의해 생성 된입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-229">hello files in hello Azure blob storage can be hello output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="75583-230">hello 판독기 모듈 있습니다 tooread 파일 (확장명이 없는) hello를 구성 하 여 **경로 toocontainer, 디렉터리/blob**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-230">hello reader module allows you tooread files (with no extensions) by configuring hello **Path toocontainer, directory/blob**.</span></span> <span data-ttu-id="75583-231">hello **경로 toocontainer** 포인트 toohello 컨테이너 및 **디렉터리/blob** hello 다음 이미지와 같이 hello 파일이 포함 된 toofolder를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="75583-231">hello **Path toocontainer** points toohello container and **directory/blob** points toofolder that contains hello files as shown in hello following image.</span></span> <span data-ttu-id="75583-232">hello, 즉 별표 \*) **hello 컨테이너/폴더에 파일을 hello 모두 지정 (즉, 데이터/aggregateddata/년 = 2014/월-6 /\*)** hello 실험의 일환으로 읽혀집니다.</span><span class="sxs-lookup"><span data-stu-id="75583-232">hello asterisk that is, \*) **specifies that all hello files in hello container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of hello experiment.</span></span>

![Azure Blob 속성](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="75583-234">예</span><span class="sxs-lookup"><span data-stu-id="75583-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="75583-235">AzureMLBatchExecution 작업 및 웹 서비스 매개 변수가 포함된 파이프라인</span><span class="sxs-lookup"><span data-stu-id="75583-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

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

<span data-ttu-id="75583-236">위 예제 JSON hello에서:</span><span class="sxs-lookup"><span data-stu-id="75583-236">In hello above JSON example:</span></span>

* <span data-ttu-id="75583-237">hello Azure 컴퓨터 학습 웹 서비스에는 판독기와 기록기 모듈 tooread/쓰기 데이터를 사용 하 여 배포 / tooan Azure SQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-237">hello deployed Azure Machine Learning Web service uses a reader and a writer module tooread/write data from/tooan Azure SQL Database.</span></span> <span data-ttu-id="75583-238">이 웹 서비스는 hello 다음 4 개의 매개 변수가 노출: 데이터베이스 서버 이름, 데이터베이스 이름, 서버 사용자 계정 이름 및 서버 사용자 계정 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-238">This Web service exposes hello following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="75583-239">**start** 및 **end** 날짜/시간은 둘 다 [ISO 형식](http://en.wikipedia.org/wiki/ISO_8601)(영문)이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="75583-240">예: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="75583-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="75583-241">hello **끝** 으로 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-241">hello **end** time is optional.</span></span> <span data-ttu-id="75583-242">Hello에 대 한 값을 지정 하지 않으면 **끝** 로 계산 됩니다 속성을 "**start + 48 시간입니다.**"</span><span class="sxs-lookup"><span data-stu-id="75583-242">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="75583-243">toorun hello 파이프라인 무제한으로 지정 **9999-09-09** hello에 대 한 hello 값으로 **끝** 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-243">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span> <span data-ttu-id="75583-244">JSON 속성에 대한 자세한 내용은 [JSON 스크립트 참조](https://msdn.microsoft.com/library/dn835050.aspx) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="75583-245">기타 시나리오</span><span class="sxs-lookup"><span data-stu-id="75583-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="75583-246">웹 서비스에는 다중 입력이 필요합니다</span><span class="sxs-lookup"><span data-stu-id="75583-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="75583-247">Hello를 사용 하 여 hello 웹 서비스 변수를 사용할 경우 여러 개의 입력 **webServiceInputs** 사용 하는 대신 속성 **webServiceInput**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-247">If hello web service takes multiple inputs, use hello **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="75583-248">Hello에서 참조 되는 데이터 집합 **webServiceInputs** hello 활동에에서도 포함 해야 **입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-248">Datasets that are referenced by hello **webServiceInputs** must also be included in hello Activity **inputs**.</span></span>

<span data-ttu-id="75583-249">Azure ML 실험에서 웹 서비스 입력 및 출력 포트와 전역 매개 변수에는 사용자 지정할 수 있는 기본 이름("input1", "input2")이 붙어있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="75583-250">webServiceInputs, webServiceOutputs, 및 globalParameters 설정에 사용할 수는 hello 이름에는 hello 실험에서 hello 이름과 정확히 일치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-250">hello names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match hello names in hello experiments.</span></span> <span data-ttu-id="75583-251">Azure 기계 학습 끝점 tooverify 예상 hello 매핑을 대 한 hello 일괄 처리 실행 도움말 페이지에 hello 샘플 요청 페이로드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-251">You can view hello sample request payload on hello Batch Execution Help page for your Azure ML endpoint tooverify hello expected mapping.</span></span>

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

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="75583-252">웹 서비스에는 입력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-252">Web Service does not require an input</span></span>
<span data-ttu-id="75583-253">Azure ML 일괄 처리 실행 웹 서비스 사용된 toorun 모든 워크플로 수 있으며, 예: R 또는 Python 스크립트에는 필요 하지 않을 수 어떤 입력도 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-253">Azure ML batch execution web services can be used toorun any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="75583-254">또는 모든 GlobalParameters를 노출 하지 않는 판독기 모듈 hello 실험 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-254">Or, hello experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="75583-255">이 경우 hello AzureMLBatchExecution 활동 다음과 같이 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-255">In that case, hello AzureMLBatchExecution Activity would be configured as follows:</span></span>

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

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="75583-256">웹 서비스에는 입력/출력이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="75583-257">hello Azure ML 일괄 처리 실행 웹 서비스에 구성 된 웹 서비스 출력이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-257">hello Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="75583-258">이 예제에서는 웹 서비스 입력 또는 출력이 없으며 GlobalParameters도 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="75583-259">Hello 활동 자체에 구성 된 출력 하지만 webServiceOutput으로 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-259">There is still an output configured on hello activity itself, but it is not given as a webServiceOutput.</span></span>

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

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="75583-260">웹 서비스 사용 하 여 판독기 및 기록기 및 다른 작업이 성공한 경우에 hello 활동을 실행</span><span class="sxs-lookup"><span data-stu-id="75583-260">Web Service uses readers and writers, and hello activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="75583-261">hello는 Azure ML 웹 서비스 판독기 및 작성기 모듈 구성된 toorun 상관 없이 모든 GlobalParameters 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-261">hello Azure ML web service reader and writer modules might be configured toorun with or without any GlobalParameters.</span></span> <span data-ttu-id="75583-262">그러나 일부 업스트림 처리가 완료 된 경우에 데이터 집합 종속성 tooinvoke hello 서비스를 사용 하는 파이프라인에서 tooembed 서비스를 호출 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-262">However, you may want tooembed service calls in a pipeline that uses dataset dependencies tooinvoke hello service only when some upstream processing has completed.</span></span> <span data-ttu-id="75583-263">이 방식을 사용 하 여 hello 일괄 처리 실행이 완료 한 후에 다른 작업을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-263">You can also trigger some other action after hello batch execution has completed using this approach.</span></span> <span data-ttu-id="75583-264">이 경우 그 중 하나를 웹 서비스 입력 또는 출력으로 이름을 지정 하지 않고 작업 입력 및 출력을 사용 하 여 hello 종속성을 표현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-264">In that case, you can express hello dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

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

<span data-ttu-id="75583-265">hello **자** 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-265">hello **takeaways** are:</span></span>

* <span data-ttu-id="75583-266">실험 끝점은 webServiceInput를 사용 하는 경우: 그 blob 데이터 집합 표시 되 고 hello 작업의 입력 및 hello webServiceInput 속성에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in hello activity inputs and hello webServiceInput property.</span></span> <span data-ttu-id="75583-267">그렇지 않으면 hello webServiceInput 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-267">Otherwise, hello webServiceInput property is omitted.</span></span>
* <span data-ttu-id="75583-268">실험 끝점 webServiceOutput(s)를 사용 하는 경우: blob 데이터 집합으로 표시 되 고 hello webServiceOutputs 속성 및 hello 활동 출력에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in hello activity outputs and in hello webServiceOutputs property.</span></span> <span data-ttu-id="75583-269">hello 활동 출력 하 고 webServiceOutputs hello 실험에서 각 출력의 hello 이름별으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-269">hello activity outputs and webServiceOutputs are mapped by hello name of each output in hello experiment.</span></span> <span data-ttu-id="75583-270">그렇지 않으면 hello webServiceOutputs 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-270">Otherwise, hello webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="75583-271">실험 끝점 globalParameter(s)을 노출할 경우 hello 활동 globalParameters 속성의 키 값 쌍으로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-271">If your experiment endpoint exposes globalParameter(s), they are given in hello activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="75583-272">그렇지 않으면 hello globalParameters 속성을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-272">Otherwise, hello globalParameters property is omitted.</span></span> <span data-ttu-id="75583-273">hello 키 대/소문자를 구분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-273">hello keys are case-sensitive.</span></span> <span data-ttu-id="75583-274">[Azure 데이터 팩터리 함수](data-factory-functions-variables.md) hello 값에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in hello values.</span></span>
* <span data-ttu-id="75583-275">추가 데이터 집합 hello 활동 typeproperties에서 참조 하지 않고 hello 활동 입 / 출력 속성에 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-275">Additional datasets may be included in hello Activity inputs and outputs properties, without being referenced in hello Activity typeProperties.</span></span> <span data-ttu-id="75583-276">이러한 데이터 집합 조각 종속성을 사용 하 여 실행을 제어 합니다. 하지만 hello AzureMLBatchExecution 활동에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75583-276">These datasets govern execution using slice dependencies but are otherwise ignored by hello AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="75583-277">업데이트 리소스 작업을 사용하여 모델 업데이트</span><span class="sxs-lookup"><span data-stu-id="75583-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="75583-278">재교육를 완료 한 후 업데이트 hello를 사용 하 여 웹 서비스 (웹 서비스로 노출 된 예측 실험) hello 새로 학습 된 모델 점수 매기기 hello **Azure ML 업데이트 리소스 작업**합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-278">After you are done with retraining, update hello scoring web service (predictive experiment exposed as a web service) with hello newly trained model by using hello **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="75583-279">자세한 내용은 [업데이트 리소스 작업을 사용하여 모델 업데이트](data-factory-azure-ml-update-resource-activity.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="75583-280">판독기 및 작성기 모듈</span><span class="sxs-lookup"><span data-stu-id="75583-280">Reader and Writer Modules</span></span>
<span data-ttu-id="75583-281">웹 서비스 매개 변수를 사용 하기 위한 일반적인 시나리오에는 hello를 사용 하 여 Azure SQL 판독기 및 작성기입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-281">A common scenario for using Web service parameters is hello use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="75583-282">hello 판독기 모듈은 Azure 기계 학습 스튜디오 외부의 데이터 관리 서비스에서 실험에 사용 되는 tooload 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-282">hello reader module is used tooload data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="75583-283">hello 기록기 모듈은 Azure 기계 학습 스튜디오 외부의 데이터 관리 서비스에 실험에서 toosave 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-283">hello writer module is toosave data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="75583-284">Azure Blob/Azure SQL 판독기/기록기에 대한 자세한 내용은 MSDN 라이브러리의 [판독기](https://msdn.microsoft.com/library/azure/dn905997.aspx) 및 [기록기](https://msdn.microsoft.com/library/azure/dn905984.aspx) 항목을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="75583-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="75583-285">hello 이전 단원의 hello 예제 hello Azure Blob 판독기 및 작성기 Azure Blob을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-285">hello example in hello previous section used hello Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="75583-286">이 섹션에서는 Azure SQL 판독기 및 Azure SQL 기록기를 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="75583-287">질문과 대답</span><span class="sxs-lookup"><span data-stu-id="75583-287">Frequently asked questions</span></span>
<span data-ttu-id="75583-288">**Q:** 빅 데이터 파이프라인에서 생성된 여러 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="75583-289">Hello AzureMLBatchExecution 활동 toowork 모든 hello 파일에 사용할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="75583-289">Can I use hello AzureMLBatchExecution Activity toowork on all hello files?</span></span>

<span data-ttu-id="75583-290">**A:** 예.</span><span class="sxs-lookup"><span data-stu-id="75583-290">**A:** Yes.</span></span> <span data-ttu-id="75583-291">Hello 참조 **판독기 모듈 tooread 데이터를 사용 하 여 Azure Blob에 여러 파일의** 자세한 내용은 섹션.</span><span class="sxs-lookup"><span data-stu-id="75583-291">See hello **Using a Reader module tooread data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="75583-292">Azure ML 일괄 처리 점수 매기기 작업</span><span class="sxs-lookup"><span data-stu-id="75583-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="75583-293">Hello를 사용 하는 경우 **AzureMLBatchScoring** 와 Azure 기계 학습 작업 toointegrate, 권장 메서드 최신 hello를 사용 하는 **AzureMLBatchExecution** 활동입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-293">If you are using hello **AzureMLBatchScoring** activity toointegrate with Azure Machine Learning, we recommend that you use hello latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="75583-294">hello AzureMLBatchExecution 활동은 2015 년 8 월 릴리스의 Azure SDK 및 Azure PowerShell hello에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75583-294">hello AzureMLBatchExecution activity is introduced in hello August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="75583-295">Toocontinue hello AzureMLBatchScoring 활동을 사용 하 여 원하는 경우이 섹션 전체를 읽고 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-295">If you want toocontinue using hello AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="75583-296">입/출력에 대해 Azure 저장소를 사용하는 Azure ML 일괄 처리 점수 매기기 작업</span><span class="sxs-lookup"><span data-stu-id="75583-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

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

### <a name="web-service-parameters"></a><span data-ttu-id="75583-297">웹 서비스 매개 변수</span><span class="sxs-lookup"><span data-stu-id="75583-297">Web Service Parameters</span></span>
<span data-ttu-id="75583-298">웹 서비스 매개 변수에 대 한 toospecify 값 추가 **typeProperties** 섹션 toohello **AzureMLBatchScoringActivty** hello 파이프라인 hello 다음 예제와 같이 JSON의 섹션:</span><span class="sxs-lookup"><span data-stu-id="75583-298">toospecify values for Web service parameters, add a **typeProperties** section toohello **AzureMLBatchScoringActivty** section in hello pipeline JSON as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="75583-299">사용할 수도 있습니다 [데이터 팩터리 함수](data-factory-functions-variables.md) hello에 대 한 값 hello 다음 예제와 같이 웹 서비스 매개 변수를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="75583-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for hello Web service parameters as shown in hello following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> <span data-ttu-id="75583-300">hello 웹 서비스 매개 변수가 대/소문자를 구분 하므로 hello 활동에서 지정 하는 hello 이름을 JSON과 일치 하는지 hello hello 웹 서비스에서 노출 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75583-300">hello Web service parameters are case-sensitive, so ensure that hello names you specify in hello activity JSON match hello ones exposed by hello Web service.</span></span>
>
>

## <a name="see-also"></a><span data-ttu-id="75583-301">참고 항목</span><span class="sxs-lookup"><span data-stu-id="75583-301">See Also</span></span>
* [<span data-ttu-id="75583-302">Azure 블로그 게시물: Azure 데이터 팩터리 및 Azure 기계 학습 시작하기</span><span class="sxs-lookup"><span data-stu-id="75583-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
