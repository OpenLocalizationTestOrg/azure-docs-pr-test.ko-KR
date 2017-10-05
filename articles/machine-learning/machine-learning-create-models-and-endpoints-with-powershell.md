---
title: "한 실험에서 여러 모델 만들기 | Microsoft Docs"
description: "PowerShell을 사용하여 알고리즘은 동일하지만 다른 학습 데이터 집합으로 여러 기계 학습 모델 및 웹 서비스 끝점을 만듭니다."
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: 21d8c1ee0877df8d317d5a14131dc574fa5303c4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="c649c-103">PowerShell을 사용하여 한 실험에서 여러 기계 학습 모델 및 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="c649c-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="c649c-104">일반적인 기계 학습 문제는 다음과 같습니다. 동일한 학습 워크플로를 포함하고 동일한 알고리즘을 사용하지만 입력으로 서로 다른 학습 데이터 집합을 포함하는 여러 모델을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="c649c-105">이 문서에서는 단일 실험을 사용하여 Azure 기계 학습 스튜디오에서 대규모로 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="c649c-106">예를 들어, 글로벌 자전거 임대 프랜차이즈 업체를 소유하고 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="c649c-107">기록 데이터를 기반으로 임대 수요를 예측하는 회귀 모델을 구축하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="c649c-108">전 세계 1,000곳의 임대 위치를 보유하고 날짜, 시간, 날씨 및 트래픽과 같은 중요한 기능을 포함하여 각 위치에 대한 데이터 집합을 수집했습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="c649c-109">모든 위치의 모든 데이터 집합에 대한 병합된 버전을 사용하여 모델을 한 번 학습할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="c649c-110">하지만 위치마다 환경이 고유하므로 각 위치에 대한 데이터 집합을 사용하여 회귀 모델을 별도로 학습하는 것이 더 나은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="c649c-111">이러한 방식으로 각 학습된 모델은 서로 다른 저장소 크기, 볼륨, 지리, 인구, 자전거 친화적인 교통 환경 *등*을 고려할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="c649c-112">이것은 가장 좋은 방법일 수 있지만 Azure 기계 학습에서 각각 고유한 위치를 나타내는 1,000번의 학습 실험을 만들고 싶지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="c649c-113">각 실험은 학습 데이터 집합을 제외하고 모두 동일한 구성 요소를 포함하므로 부담스러울 뿐만 아니라 매우 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="c649c-114">다행히 [Azure Machine Learning 재학습 API](machine-learning-retrain-models-programmatically.md)를 사용하고 [Azure Machine Learning PowerShell](machine-learning-powershell-module.md)로 작업을 자동화하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c649c-115">샘플 실행 속도를 빠르게 하려면 위치 수를 1,000개에서 10개로 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="c649c-116">하지만 동일한 원리와 절차가 1,000개의 위치에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="c649c-117">유일한 차이점은 1,000개 데이터 집합에서 학습하려는 경우 다음 PowerShell 스크립트를 병렬로 실행하는 것을 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="c649c-118">이 작업을 수행하는 방법은 이 문서의 범위를 벗어나는 내용이지만 인터넷에서 PowerShell 다중 스레딩의 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="c649c-119">학습 실험 설정</span><span class="sxs-lookup"><span data-stu-id="c649c-119">Set up the training experiment</span></span>
<span data-ttu-id="c649c-120">[Cortana Intelligence 갤러리](http://gallery.cortanaintelligence.com)에서 이미 만든 [학습 실험](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) 예제를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="c649c-121">[Azure 기계 학습 스튜디오](https://studio.azureml.net) 작업 영역에서 이 실험을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="c649c-122">이 예제를 함께 수행하려면 무료 작업 영역보다는 표준 작업 영역을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="c649c-123">고객당 끝점 하나(총 10개 끝점)를 만들고 무료 작업 영역이 3개 끝점으로 제한되므로 이를 위해서는 표준 작업 영역이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="c649c-124">무료 작업 영역만 있는 경우 3개의 위치만 허용하도록 아래 스크립트를 수정하세요.</span><span class="sxs-lookup"><span data-stu-id="c649c-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="c649c-125">이 실험에서는 **데이터 가져오기** 모듈을 사용하여 Azure 저장소 계정에서 학습 데이터 집합 *customer001.csv* 를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="c649c-126">모든 자전거 임대 위치에서 학습 데이터 집합을 수집하고 이를 *rentalloc001.csv*에서 *rentalloc10.csv*까지 범위의 파일 이름으로 동일한 Blob Store 위치에 저장한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="c649c-128">**웹 서비스 출력** 모듈이 **모델 학습** 모듈에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="c649c-129">이 실험을 웹 서비스로 배포할 때 해당 출력과 연결된 끝점에서 학습된 모델을 .ilearner 파일 형식으로 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="c649c-130">또한 **데이터 가져오기** 모듈에서 사용하는 URL에 대한 웹 서비스 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="c649c-131">이렇게 하면 각 위치에 대한 모델을 학습하기 위한 개별 학습 데이터 집합을 지정하는 데 매개 변수를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="c649c-132">이를 수행할 수 있는 다른 방법으로, SQL Azure 데이터베이스에서 데이터를 가져오는 데 SQL 쿼리와 웹 서비스 매개 변수를 사용하거나 단순히 **웹 서비스 입력** 모듈을 사용하여 데이터 집합을 웹 서비스에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="c649c-134">이제 학습 데이터 집합으로 *rental001.csv* 기본값을 사용하여 이 학습 실험을 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="c649c-135">**평가** 모듈의 출력을 보면(출력을 클릭하고 **시각화** 선택) *AUC* = 0.91이라는 적절한 성능을 보이는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="c649c-136">이제 이 학습 실험의 웹 서비스 출력을 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="c649c-137">학습 및 점수 매기기 웹 서비스 배포</span><span class="sxs-lookup"><span data-stu-id="c649c-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="c649c-138">학습 웹 서비스를 배포하려면 실험 캔버스 아래 **웹 서비스 설정** 단추를 클릭하고 **웹 서비스 배포**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="c649c-139">이 웹 서비스를 ""Bike Rental Training"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="c649c-140">이제 점수 매기기 웹 서비스를 배포해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="c649c-141">이 작업을 수행하려면 캔버스 아래에서 **웹 서비스 설정**을 클릭하고 **예측 웹 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="c649c-142">점수 매기기 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="c649c-143">웹 서비스로 작동하도록 하려면 입력 데이터에서 "cnt" 레이블 열을 제거하고 출력을 인스턴스 ID 및 해당 예측 값만으로 제한하는 등 약간의 조정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="c649c-144">해당 작업을 직접 저장하려면 미리 준비된 갤러리에서 단순히 [예측 실험](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) 을 열면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="c649c-145">웹 서비스를 배포하려면 예측 실험을 실행하고 캔버스 아래의 **웹 서비스 배포** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="c649c-146">점수 매기기 웹 서비스 이름을 "Bike Rental Scoring""으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="c649c-147">PowerShell에서 10개의 동일한 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="c649c-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="c649c-148">이 웹 서비스는 기본 끝점을 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="c649c-149">하지만 업데이트할 수 없으므로 기본 끝점에는 그다지 관심이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="c649c-150">각 위치당 하나씩 10개의 추가 끝점을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="c649c-151">이 작업을 PowerShell에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="c649c-152">먼저, PowerShell 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="c649c-153">그런 다음 아래 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="c649c-154">이제 10개의 끝점을 만들었고 모두 *customer001.csv*에서 동일한 학습 모델을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="c649c-155">Azure 관리 포털에서 이러한 내용을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-155">You can view them in the Azure Management Portal.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="c649c-157">PowerShell을 사용하여 별도의 학습 데이터 집합을 사용하도록 끝점 업데이트</span><span class="sxs-lookup"><span data-stu-id="c649c-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="c649c-158">다음 단계는 각 고객의 개별 데이터에서 고유하게 학습된 모델로 끝점을 업데이트하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="c649c-159">하지만 먼저 **Bike Rental Training** 웹 서비스에서 이러한 모델을 생성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="c649c-160">**Bike Rental Training** 웹 서비스를 다시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="c649c-161">10가지 서로 다른 모델을 생성하기 위해서는 10개의 서로 다른 학습 데이터 집합으로 BES 끝점을 10번 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="c649c-162">이를 위해 **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="c649c-163">Blob 저장소 계정에 대한 자격 증명을 `$configContent`, 즉 `AccountName`, `AccountKey` 및 `RelativeLocation` 필드에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="c649c-164">`AccountName`은 **클래식 Azure 관리 포털**(*저장소* 탭)에 표시되는 계정 이름 중 하나가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="c649c-165">저장소 계정에서 클릭하면 아래쪽의 **선택키 관리** 단추를 누르고 *기본 선택키*를 복사하여 해당 `AccountKey`를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="c649c-166">`RelativeLocation`은 새 모델을 저장할 저장소의 상대적인 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="c649c-167">예를 들어 아래 스크립트의 경로 `hai/retrain/bike_rental/`은 `hai`라는 컨테이너를 가리키고 `/retrain/bike_rental/`은 하위 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="c649c-168">현재 포털 UI 통해 하위 폴더를 만들 수는 없지만 [여러 Azure Storage 탐색기](../storage/common/storage-explorers.md)에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="c649c-169">다음과 같이 학습된 새 모델(.ilearner 파일)을 저장할 새 컨테이너를 저장소에 만드는 것이 좋습니다. 저장소 페이지 아래쪽의 **추가** 단추를 클릭하고 `retrain`으로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="c649c-170">요약하면 아래 스크립트의 필수 변경 내용은 `AccountName`, `AccountKey` 및 `RelativeLocation`(:`"retrain/model' + $seq + '.ilearner"`)과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="c649c-171">BES 끝점은 이 작업에 대해 지원되는 유일한 모드입니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="c649c-172">RRS는 학습된 모델을 생성하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="c649c-173">위에서 볼 수 있듯이 디스크에 실제로 복사본을 보관할 필요가 없으므로 10개의 서로 다른 BES 작업 구성 json 파일을 생성하는 대신, 구성 문자열을 동적으로 만들고 *InvokeAmlWebServceBESEndpoint* cmdlet의 **jobConfigString** 매개 변수에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="c649c-174">모든 항목을 제대로 진행했으면 잠시 후 *model001.ilearner*에서 *model010.ilearner*까지 10개의 .ilearner 파일이 Azure Storage 계정에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="c649c-175">이제 **Patch-AmlWebServiceEndpoint** PowerShell cmdlet을 사용하여 이러한 모델로 10개의 점수 매기기 웹 서비스 끝점을 업데이트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="c649c-176">프로그래밍 방식으로 이전에 만든 기본이 아닌 끝점만 패치할 수 있음을 다시 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="c649c-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="c649c-177">이 작업은 매우 신속하게 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-177">This should run fairly quickly.</span></span> <span data-ttu-id="c649c-178">실행이 끝나면 각각 임대 위치별 데이터 집합에서 고유하게 학습된 모델을 포함하는 10개의 예측 웹 서비스 끝점을 단일 학습 실험에서 모두 성공적으로 포함하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="c649c-179">이를 확인하려면 동일한 입력 데이터로 **InvokeAmlWebServiceRRSEndpoint** cmdlet을 사용하여 이러한 끝점을 호출하려고 시도할 수 있으며 모델이 서로 다른 학습 집합으로 학습되므로 다른 예측 결과가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="c649c-180">전체 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="c649c-180">Full PowerShell script</span></span>
<span data-ttu-id="c649c-181">전체 소스 코드 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c649c-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
