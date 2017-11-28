---
title: "aaaCreate 하나의 실험에서 여러 모델 | Microsoft Docs"
description: "PowerShell toocreate 여러 기계 학습 모델을 사용 하 고 웹 서비스 끝점만 hello로 알고리즘이 동일 하지만 서로 다른 학습 데이터 집합입니다."
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
ms.openlocfilehash: 4a258a8ab26395d4169a058520151c860e16e169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="30745-103">PowerShell을 사용하여 한 실험에서 여러 기계 학습 모델 및 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="30745-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="30745-104">다음은 일반적인 컴퓨터 학습 문제: toocreate 많은 있는 모델을 hello를 원하는 같은 학습 워크플로 및 사용 하 여 같은 알고리즘을 hello 설치 했지만 입력으로 서로 다른 학습 데이터 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-104">Here's a common machine learning problem: You want toocreate many models that have hello same training workflow and use hello same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="30745-105">이 문서에서는 어떻게 toodo는 단일 실험만을 사용 하 여 Azure 기계 학습 스튜디오의 규모에이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-105">This article shows you how toodo this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="30745-106">예를 들어, 글로벌 자전거 임대 프랜차이즈 업체를 소유하고 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="30745-107">Toobuild 기록 데이터를 기반으로 회귀 모델 toopredict hello 임대 요청을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-107">You want toobuild a regression model toopredict hello rental demand based on historic data.</span></span> <span data-ttu-id="30745-108">1, 000 렌탈 지 hello 전 세계 있고 각 날짜, 시간, 날씨, 같은 중요 한 기능을 포함 하는 위치 및 특정 tooeach 위치는 트래픽을 대 한 데이터 집합을 수집 했습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-108">You have 1,000 rental locations across hello world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific tooeach location.</span></span>

<span data-ttu-id="30745-109">한 번 hello는 모든 데이터 집합의 병합 된 버전을 사용 하 여 모든 위치에서 모델을 학습 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-109">You could train your model once using a merged version of all hello datasets across all locations.</span></span> <span data-ttu-id="30745-110">각 위치에 있는 고유한 환경, 때문에 더 나은 방법은 하지만 tootrain 별도로 hello 데이터 집합을 사용 하 여 각 위치에 대 한 회귀 모델 수입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-110">But because each of your locations has a unique environment, a better approach would be tootrain your regression model separately using hello dataset for each location.</span></span> <span data-ttu-id="30745-111">이런 방식으로 각 학습 된 모델 계정 hello 다른 저장소 크기, 볼륨, geography, 인구, 자전거 친화적인 트래픽 환경에 걸리는 *등*합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-111">That way, each trained model could take into account hello different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="30745-112">Hello 가장 좋은 방법이 될 수 있는 않으려는 Azure 기계 학습에서 1, 000 toocreate 학습 실험 하나로 각 고유 위치를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-112">That may be hello best approach, but you don't want toocreate 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="30745-113">작업은 매우 복잡할 뿐만 이기도 hello hello 학습 데이터 집합을 제외 하 고 동일한 구성 요소 모두 각 실험 해야 하므로 매우 비효율적인 것 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all hello same components except for hello training dataset.</span></span>

<span data-ttu-id="30745-114">다행히 수이를 위해서는 hello를 사용 하 여 [Azure 기계 학습 API 재교육](machine-learning-retrain-models-programmatically.md) 자동화 hello, 작업 및 [Azure 컴퓨터 학습 PowerShell](machine-learning-powershell-module.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-114">Fortunately, we can accomplish this by using hello [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating hello task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="30745-115">샘플 더 빠르게 실행 toomake, hello 수가 1, 000 too10 위치 줄일 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-115">toomake our sample run faster, we'll reduce hello number of locations from 1,000 too10.</span></span> <span data-ttu-id="30745-116">하지만 hello 동일한 원칙 및 절차 적용 too1, 000 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-116">But hello same principles and procedures apply too1,000 locations.</span></span> <span data-ttu-id="30745-117">hello 유일한 차이점은 1, 000 데이터 집합에서 tootrain 하려는 경우 한다는 것 toothink hello 다음 동시에 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-117">hello only difference is that if you want tootrain from 1,000 datasets you probably want toothink of running hello following PowerShell scripts in parallel.</span></span> <span data-ttu-id="30745-118">어떻게이 문서에서는의 hello 범위를 벗어납니다 toodo에서 찾을 수의 PowerShell 예제 다중 스레딩을 hello 인터넷.</span><span class="sxs-lookup"><span data-stu-id="30745-118">How toodo that is beyond hello scope of this article, but you can find examples of PowerShell multi-threading on hello Internet.</span></span>  
> 
> 

## <a name="set-up-hello-training-experiment"></a><span data-ttu-id="30745-119">학습 실험 hello 설정</span><span class="sxs-lookup"><span data-stu-id="30745-119">Set up hello training experiment</span></span>
<span data-ttu-id="30745-120">예 toouse 여기 [학습 실험](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) hello에서 이미 만든 했으므로 [Cortana 인텔리전스 갤러리](http://gallery.cortanaintelligence.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-120">We're going toouse an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="30745-121">[Azure 기계 학습 스튜디오](https://studio.azureml.net) 작업 영역에서 이 실험을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="30745-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="30745-122">이 예제의 단계별 순서 toofollow에 무료 작업 영역 보다는 표준 작업 영역 toouse 있습니다 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-122">In order toofollow along with this example, you may want toouse a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="30745-123">म 만들게 됩니다 한 끝점-총 10 끝점-의 각 고객에 대 하 고 무료 작업 영역 제한 too3 끝점 이므로 표준 작업 영역을 해야 합니다입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited too3 endpoints.</span></span> <span data-ttu-id="30745-124">무료 작업 영역만 있는 경우 3 위치에 대 한 tooallow 아래 hello 스크립트를 수정만 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-124">If you only have a free workspace, just modify hello scripts below tooallow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="30745-125">사용 하 여 hello 실험은 **데이터 가져오기** 모듈 tooimport hello 학습 데이터 집합 *customer001.csv* Azure 저장소 계정에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-125">hello experiment uses an **Import Data** module tooimport hello training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="30745-126">모든 자전거 임대 위치에서 학습 데이터 집합을 수집 했으며 hello에서 범위의 파일 이름으로 같은 blob 저장소 위치에 저장을 가정해 보겠습니다 *rentalloc001.csv* 너무*rentalloc10.csv* .</span><span class="sxs-lookup"><span data-stu-id="30745-126">Let's assume we have collected training datasets from all bike rental locations and stored them in hello same blob storage location with file names ranging from *rentalloc001.csv* too*rentalloc10.csv*.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="30745-128">한 **웹 서비스 출력** 모듈이 toohello 추가 되어 **모델 학습** 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-128">Note that a **Web Service Output** module has been added toohello **Train Model** module.</span></span>
<span data-ttu-id="30745-129">이 실험을 웹 서비스로 배포 될 때 해당 출력을 연관 된 hello 끝점.ilearner 파일의 hello 형식의 hello 학습 된 모델을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-129">When this experiment is deployed as a web service, hello endpoint associated with that output will return hello trained model in hello format of a .ilearner file.</span></span>

<span data-ttu-id="30745-130">또한 설정 한다는 점에 유의에서는 웹 서비스 매개 변수를 hello URL에 대 한 해당 hello **데이터 가져오기** 모듈을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-130">Also note that we set up a web service parameter for hello URL that hello **Import Data** module uses.</span></span> <span data-ttu-id="30745-131">이 통해 각 위치에 대 한 toouse hello 매개 변수 toospecify 개별 학습 데이터 집합 hello 모델 tootrain 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-131">This allows us toouse hello parameter toospecify individual training datasets tootrain hello model for each location.</span></span>
<span data-ttu-id="30745-132">있는 방법이 있다면이 SQL 쿼리를 사용 하 여 SQL Azure 데이터베이스에서 웹 서비스 매개 변수 tooget 데이터 또는 단순히를 사용 하 여 같은 다른 방법으로 **웹 서비스 입력** 모듈 toopass dataset toohello에서 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-132">There are other ways we could have done this, such as using a SQL query with a web service parameter tooget data from a SQL Azure database, or simply using a  **Web Service Input** module toopass in a dataset toohello web service.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="30745-134">이제 hello 기본값을 사용 하 여이 학습 실험을 실행 해 보겠습니다 *rental001.csv* hello 학습 데이터 집합으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-134">Now, let's run this training experiment using hello default value *rental001.csv* as hello training dataset.</span></span> <span data-ttu-id="30745-135">Hello의 hello 출력을 보면 **평가** 모듈 (hello 출력을 클릭 하 고 선택 **시각화**)의 좋은 성능을 얻을 수 있는 것을 볼 수 있습니다 *AUC* 0.91 = 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-135">If you view hello output of hello **Evaluate** module (click hello output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="30745-136">이 시점에서 여러분 준비 toodeploy이 학습 실험에서 웹 서비스.</span><span class="sxs-lookup"><span data-stu-id="30745-136">At this point, we're ready toodeploy a web service out of this training experiment.</span></span>

## <a name="deploy-hello-training-and-scoring-web-services"></a><span data-ttu-id="30745-137">Hello 교육 및 웹 서비스를 평가 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-137">Deploy hello training and scoring web services</span></span>
<span data-ttu-id="30745-138">toodeploy hello 학습 웹 서비스를 클릭 하 여 hello **웹 서비스 설정** hello 실험 캔버스 아래 단추를 선택 하 고 **웹 서비스 배포**합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-138">toodeploy hello training web service, click hello **Set Up Web Service** button below hello experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="30745-139">이 웹 서비스를 ""Bike Rental Training"이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="30745-140">이제 toodeploy hello 점수 매기기 웹 서비스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-140">Now we need toodeploy hello scoring web service.</span></span>
<span data-ttu-id="30745-141">toodo이를 누르면 됩니다 **웹 서비스 설정** 선택한 hello 아래 캔버스로 **예측 웹 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-141">toodo this, we can click **Set Up Web Service** below hello canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="30745-142">점수 매기기 실험을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30745-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="30745-143">입력 데이터 hello에서 "cnt" hello 레이블 열을 제거 하 고 hello 출력 tooonly hello 인스턴스 id 및 hello 해당 제한 값을 예측와 같은 웹 서비스로 작동 하는 몇 가지 약간 조정 toomake toomake가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-143">We'll need toomake a few minor adjustments toomake it work as a web service, such as removing hello label column "cnt" from hello input data and limiting hello output tooonly hello instance id and hello corresponding predicted value.</span></span>

<span data-ttu-id="30745-144">toosave를 작동 하는 사용자가 직접 hello를 간단히 열 수 있습니다 [예측 실험](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) hello 이미 준비 된 갤러리에에서 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-144">toosave yourself that work, you can simply open hello [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in hello Gallery that's already been prepared.</span></span>

<span data-ttu-id="30745-145">hello 예측 실험 실행 toodeploy hello 웹 서비스는 hello 클릭 **웹 서비스 배포** hello 캔버스 아래 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-145">toodeploy hello web service, run hello predictive experiment, then click hello **Deploy Web Service** button below hello canvas.</span></span> <span data-ttu-id="30745-146">웹 서비스 "임대 점수 매기기 자전거" 점수 매기기 이름 hello "입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-146">Name hello scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="30745-147">PowerShell에서 10개의 동일한 웹 서비스 끝점 만들기</span><span class="sxs-lookup"><span data-stu-id="30745-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="30745-148">이 웹 서비스는 기본 끝점을 함께 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="30745-149">하지만 노력 hello 기본 끝점으로 관심이 있으므로 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-149">But we're not as interested in hello default endpoint since it can't be updated.</span></span> <span data-ttu-id="30745-150">필요한 요소 toodo는 각 위치에 대해 하나씩 10 toocreate 추가 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-150">What we need toodo is toocreate 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="30745-151">이 작업을 PowerShell에서 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="30745-152">먼저, PowerShell 환경을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and is properly set toopoint toohello valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="30745-153">Hello 다음 PowerShell 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-153">Then, run hello following PowerShell command:</span></span>

    # Create 10 endpoints on hello scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="30745-154">이제 10 끝점을 만들었으므로 하며, 동일한 학습 된 모델에서 학습 하는 hello 포함 *customer001.csv*합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-154">Now we've created 10 endpoints and they all contain hello same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="30745-155">Hello Azure 관리 포털에서에서 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-155">You can view them in hello Azure Management Portal.</span></span>

![이미지](./media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-hello-endpoints-toouse-separate-training-datasets-using-powershell"></a><span data-ttu-id="30745-157">Hello 끝점 toouse 별도 학습 데이터 집합 PowerShell을 사용 하 여 업데이트</span><span class="sxs-lookup"><span data-stu-id="30745-157">Update hello endpoints toouse separate training datasets using PowerShell</span></span>
<span data-ttu-id="30745-158">hello 다음 단계는 각 고객의 개별 데이터에 대해 고유 하 게 학습 된 모델을 tooupdate hello 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-158">hello next step is tooupdate hello endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="30745-159">먼저 다음 해야 tooproduce hello에서 이러한 모델 하지만 **자전거 임대 교육** 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-159">But first we need tooproduce these models from hello **Bike Rental Training** web service.</span></span> <span data-ttu-id="30745-160">뒤로 toohello 돌아가겠습니다 **자전거 임대 교육** 웹 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-160">Let's go back toohello **Bike Rental Training** web service.</span></span> <span data-ttu-id="30745-161">순서 tooproduce 10 서로 다른 모델에 10 개의 서로 다른 학습 데이터 집합으로 10 번 BES endpoint toocall 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-161">We need toocall its BES endpoint 10 times with 10 different training datasets in order tooproduce 10 different models.</span></span> <span data-ttu-id="30745-162">Hello에서는 **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-162">We'll use hello **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet toodo this.</span></span>

<span data-ttu-id="30745-163">Blob 저장소 계정에 대 한 tooprovide 자격 증명이 필요 합니다 `$configContent`, 즉, hello 필드 `AccountName`, `AccountKey` 및 `RelativeLocation`합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-163">You will also need tooprovide credentials for your blob storage account into `$configContent`, namely, at hello fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="30745-164">hello `AccountName` hello와 같이 계정 이름 중 하나일 수 있습니다 **클래식 Azure 관리 포털** (*저장소* 탭).</span><span class="sxs-lookup"><span data-stu-id="30745-164">hello `AccountName` can be one of your account names, as seen in hello **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="30745-165">저장소 계정을 클릭 하면 해당 `AccountKey` hello를 통해 확인할 수 있습니다 **액세스 키 관리** hello 아래쪽과 hello 복사에 단추 *기본 액세스 키*합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-165">Once you click on a storage account, its `AccountKey` can be found by pressing hello **Manage Access Keys** button at hello bottom and copying hello *Primary Access Key*.</span></span> <span data-ttu-id="30745-166">hello `RelativeLocation` 는 새 모델을 저장할 hello 경로 상대 tooyour 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="30745-166">hello `RelativeLocation` is hello path relative tooyour storage where a new model will be stored.</span></span> <span data-ttu-id="30745-167">예를 들어 hello 경로 `hai/retrain/bike_rental/` hello 스크립트 라는 포인트 tooa 컨테이너 아래에 `hai`, 및 `/retrain/bike_rental/` 는 하위 폴더가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-167">For instance, hello path `hai/retrain/bike_rental/` in hello script below points tooa container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="30745-168">현재 hello 포털 UI 통해 하위 폴더를 만들 수는 없지만 [여러 Azure 저장소 탐색기](../storage/common/storage-explorers.md) 수 있는 toodo 하므로 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-168">Currently, you cannot create subfolders through hello portal UI, but there are [several Azure Storage Explorers](../storage/common/storage-explorers.md) that allow you toodo so.</span></span> <span data-ttu-id="30745-169">새 컨테이너에에서 만들어야 저장소 toostore hello 새 학습 된 모델 (.ilearner 파일) 다음과 같은 것이 좋습니다.:에서 저장소 페이지에서 클릭 하 여 hello **추가** hello 아래쪽 단추 하 고 이름을 `retrain`합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-169">It is recommended that you create a new container in your storage toostore hello new trained models (.ilearner files) as follows: from your storage page, click on hello **Add** button at hello bottom and name it `retrain`.</span></span> <span data-ttu-id="30745-170">요약 하자면, 아래의 hello 필요한 변경을 toohello 스크립트와 관련 된 너무`AccountName`, `AccountKey` 및 `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="30745-170">In summary, hello necassary changes toohello script below pertain too`AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke hello retraining API 10 times
    # This is hello default (and hello only) endpoint on hello training web service
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
> <span data-ttu-id="30745-171">hello BES 끝점은 hello만이 작업에 대 한 모드를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-171">hello BES endpoint is hello only supported mode for this operation.</span></span> <span data-ttu-id="30745-172">RRS는 학습된 모델을 생성하는 데 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="30745-173">10 다른 BES 작업 구성 json 파일을 생성 하는 대신 위에서 볼 수 있듯이 우리 동적으로 hello 구성 문자열 대신 만들고 toohello 피드 *jobConfigString* hello의 매개 변수  **InvokeAmlWebServceBESEndpoint** cmdlet을 사용할 수 없으므로 없습니다 필요 tookeep 실제로 복사본을 디스크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create hello config string instead and feed it toohello *jobConfigString* parameter of hello **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need tookeep a copy on disk.</span></span>

<span data-ttu-id="30745-174">모든 코드가 정상적으로 작동 하는 경우 잠시 후 나타납니다 10.ilearner 파일에서 *model001.ilearner* 너무*model010.ilearner*, Azure 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* too*model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="30745-175">이제 우리 준비 tooupdate 웹 점수 매기기 우리의 10 hello를 사용 하 여 이러한 모델을 서비스 끝점 **패치 AmlWebServiceEndpoint** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="30745-175">Now we're ready tooupdate our 10 scoring web service endpoints with these models using hello **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="30745-176">Hello 기본값이 아닌 끝점을 프로그래밍 방식으로 앞에서 만든 패치만 म을 기억 하십시오.</span><span class="sxs-lookup"><span data-stu-id="30745-176">Remember again that we can only patch hello non-default endpoints we programmatically created earlier.</span></span>

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="30745-177">이 작업은 매우 신속하게 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-177">This should run fairly quickly.</span></span> <span data-ttu-id="30745-178">Hello 실행이 끝날 때 म 합니다 성공적으로 만들었습니다 10 예측 웹 서비스 끝점 각각 단일 학습 실험에서 모두 hello dataset 특정 tooa 임대 위치를 고유 하 게 교육 학습된 된 모델을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="30745-178">When hello execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on hello dataset specific tooa rental location, all from a single training experiment.</span></span> <span data-ttu-id="30745-179">tooverify이 hello를 사용 하 여 이러한 끝점을 호출 해 볼 수 있습니다 **InvokeAmlWebServiceRRSEndpoint** cmdlet을 제공 hello 동일한 데이터를 입력 하 고 hello 모델은 서로 다른 예측 결과 toosee 소요 될 수 있습니다 서로 다른 학습 집합으로 학습 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30745-179">tooverify this, you can try calling these endpoints using hello **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with hello same input data, and you should expect toosee different prediction results since hello models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="30745-180">전체 PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="30745-180">Full PowerShell script</span></span>
<span data-ttu-id="30745-181">Hello hello 전체 소스 코드 목록은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30745-181">Here's hello listing of hello full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume hello default configuration file exists and properly set toopoint toohello valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on hello scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke hello retraining API 10 times tooproduce 10 regression models in .ilearner format
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

    # Patch hello 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }
